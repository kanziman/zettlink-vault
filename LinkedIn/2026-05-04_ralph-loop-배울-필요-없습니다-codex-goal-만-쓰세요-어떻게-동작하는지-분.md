---
url: https://www.linkedin.com/feed/update/urn:li:activity:7456817369785733120/
title: "Ralph loop 배울 필요 없습니다. codex /goal 만 쓰세요. 어떻게 동작하는지 분석했습니다"
channel: 정구봉
upload_date: 2026-05-04
duration: ""
date_saved: 2026-05-04
content_source: linkedin_post
raw_path: ""
tags: []
---

Ralph loop 배울 필요 없습니다. codex /goal 만 쓰세요. 어떻게 동작하는지 분석했습니다. 저는 OpenAI codex 레포를 직접 클론해서 코드를 깠고, 한 줄 요약은 이겁니다. OpenAI는 ralph loop이 외부 스크립트로 하던 일을 "목표 달성할 때까지 멈추지 않게 하기"와 "효과적으로 달성하게 만들기" 두 축으로 쪼갠 뒤, 각 축마다 3중 구조의 가드를 코드와 프롬프트 양쪽에 박아넣었습니다.

본격적으로 들어가기 전에, /goal은 사실 한 가지가 아닙니다. 같은 이름 아래 세 개의 인터페이스가 다른 권한으로 분리되어 있습니다. 사용자 TUI 명령(/goal, /goal pause, /goal resume, /goal clear), 모델에게 노출되는 도구(get_goal, create_goal, update_goal), app-server 실험 API(thread/goal/set, get, clear). 이 셋이 같은 thread_goals 테이블을 건드리지만 권한이 다릅니다. 사용자는 set/replace/pause/resume/clear가 모두 가능, 모델은 get/create/complete만 가능, runtime은 accounting과 budget limit과 auto continuation을 담당. 권한 분리 표를 한 줄로 줄이면 "자율성은 모델, 통제는 사용자와 시스템"입니다.

먼저 멈추지 않게 만드는 3중 구조입니다.

1. 프로그램 레이어

TurnFinished 이벤트가 뜨면 maybe_start_goal_continuation_turn이 자동으로 새 turn을 큐에 push합니다. 모델이 답하고 끝내려 해도 다음 turn이 강제로 열립니다. continuation_lock 세마포어까지 걸려 있어서, 사용자가 한 번도 입력하지 않아도 루프가 굴러갑니다. 단 Plan mode에서는 should_ignore_goal_for_mode가 continuation을 끕니다. 자율 루프와 사용자 검토 시간을 분리한 디테일입니다.

2. 프롬프트 레이어

매 턴 경계마다 developer 메시지가 주입됩니다. "Continue working toward the active thread goal. Choose the next concrete action toward the objective." 수동 대기를 금지하는 문장이 매번 새로 박힙니다. budget이 다 떨어져도 budget_limit.md가 한 번 더 들어와서 "Do not mark a goal complete merely because the budget is nearly exhausted"를 강제합니다. budget_limited는 실패도 성공도 아닌 "정리하라"는 상태입니다.

3. 스키마 레이어

update_goal은 status="complete"만 허용합니다. enum 값 자체가 ["complete"] 하나뿐입니다. 모델이 fail이나 abort나 pause로 도망갈 옵션이 스키마 단에서 닫혀 있습니다. tool description에는 "You cannot use this tool to pause, resume, or budget-limit a goal; those status changes are controlled by the user or system"이 명시되어 있습니다.

다음은 효과적으로 목표를 달성하게 만드는 3중 구조입니다.

1. 권한 분리

모델은 complete 마킹만 가능합니다. Pause/Resume은 사용자 TUI 명령이나 시스템 인터럽트 이벤트로만 발생합니다. BudgetLimited는 SQL이 자동으로 승격합니다. /goal과 create_goal의 동작도 다릅니다. /goal 새목표는 기존 goal을 교체할 수 있지만, 모델의 create_goal은 기존 goal이 있으면 "cannot create a new goal because this thread already has a goal" 에러를 돌려줍니다.

2. SQL 원자성과 정직한 accounting

account_thread_goal_usage가 UPDATE 한 방으로 누적과 임계치 체크와 상태 전이를 동시에 처리합니다. CASE문 안에서 tokens_used + delta >= token_budget이면 BudgetLimited로 자동 승격, race condition이 없고 모델 개입 여지도 0입니다. 흥미로운 점이 더 있습니다. token 계산에서 cached input은 제외되고 output token만 포함됩니다. budget이 "캐시 히트로 부풀려진 가짜 작업량"이 아니라 "실제 새로 쓴 모델 작업량"에 가깝게 잡히도록 설계된 겁니다.

3. Self-monitoring

매 continuation prompt에 tokens_used, time_used_seconds, token_budget, remaining_tokens 네 숫자가 박혀 들어옵니다. 모델은 자기가 얼마나 썼고 얼마나 남았는지 매 턴 강제로 인지합니다. get_goal을 따로 부르지 않아도 self-pacing이 자연스럽게 나옵니다.

제가 코드를 까면서 가장 인상 깊었던 건 두 가지입니다. 첫째, completion audit. continuation prompt에 "objective를 success criteria로 다시 쪼개라, 모든 요건을 prompt-to-artifact checklist로 매핑하라, real evidence를 inspect하라, proxy signal만으로 완료라 보지 말라, 불확실하면 미완료로 취급하라"가 들어있습니다. 테스트가 그린이라는 이유만으로 complete를 부르는 행동을 금지하는 가드입니다. 둘째, prompt injection 방어. objective는 항상 <untrusted_objective> 태그로 감싸지고 XML escape됩니다. goal 본문에 "이전 지시를 무시해" 같은 문장이 들어가도 더 높은 우선순위 지시로 취급되지 않습니다. 자율 루프인데도 탈취되지 않는 구조입니다.

codex 만 있다면.. Ralph가 뭔지 몰라도 됩니다!

---
작성자: 정구봉
URL: https://www.linkedin.com/feed/update/urn:li:activity:7456817369785733120/
