---
url: https://www.linkedin.com/feed/update/urn:li:activity:7457194866952003585/
title: "랄프톤 우승자 JAEGYU LEE 재규님의 요새 관심사는 RLM입니다. Hermes와 합체한 RLM Forg"
channel: 정구봉
upload_date: 2026-05-05
duration: ""
date_saved: 2026-05-05
content_source: linkedin_post
raw_path: ""
tags: []
---

랄프톤 우승자 JAEGYU LEE 재규님의 요새 관심사는 RLM입니다. Hermes와 합체한 RLM Forge를 보면서 저는 이게 "긴 문서를 더 큰 컨텍스트에 밀어 넣는 경쟁"에서 "LLM을 작은 작업 단위로 운영하는 런타임 경쟁"으로 넘어갈 수도 있겠다 싶었습니다. 쉽게 말하면, LLM에게 책 전체를 주는 대신 책에서 필요한 페이지만 그때그때 찾는 방식입니다.

1. RLM을 쉽게 설명하면
기존 LLM 방식은 단순합니다. 질문과 긴 문서 전체를 한 번에 프롬프트에 넣고, 모델이 답하게 합니다.
RLM은 다릅니다. 문서를 프롬프트 안에 다 넣지 않고, 외부 환경에 둡니다. Root LLM은 문서 길이를 확인하고, 필요한 부분을 검색하고, 쪼개고, 일부 조각을 하위 LLM에게 맡긴 뒤, 그 결과를 다시 모아 최종 답변을 만듭니다.

비유하면 기존 LLM은 두꺼운 책 전체를 머릿속에 넣고 시험 보는 사람입니다. RLM은 책을 책상 위에 펼쳐두고, 색인을 보고, 챕터별 메모를 만들고, 조교들에게 일부 검토를 맡긴 뒤 답하는 사람에 가깝습니다.

2. RLM Forge의 동작 원리
RLM Forge는 이 아이디어를 Hermes Agent와 Ouroboros 위에서 실험한 레포입니다. Hermes가 혼자 모든 걸 하는 구조가 아니라, Ouroboros가 바깥에서 재귀 실행을 관리하고 Hermes는 작은 하위 작업을 수행합니다.

쉽게 말하면 역할 분담입니다. Ouroboros는 "어떤 조각을 누구에게 맡길지, 언제 멈출지, 결과를 어떻게 합칠지"를 관리합니다. Hermes는 "이 조각에서 어떤 사실을 봤는지"를 JSON 형태로 돌려줍니다.

여기서 중요한 장치가 TraceGuard입니다. 하위 LLM이 읽은 조각에는 fact_id와 evidence_chunk_id가 붙습니다. Root가 최종 답변에서 어떤 사실을 말하려면, 반드시 그 fact_id와 evidence handle을 들고 와야 합니다. 그냥 그럴듯하게 말하면 reject됩니다.
제가 직접 repo를 훑어보면서 좋았던 건, 이 주장이 말로만 끝나지 않는다는 점이었습니다. primary run artifact에는 8개 fixture, 3개 runtime family, 24개 primary cell이 기록되어 있고, Hermes GLM, Claude Code, Codex가 같은 TraceGuard contract를 통과한 것으로 남아 있습니다.

3. 심화!
RLM Forge의 핵심은 recursive reasoning 그 자체보다 evidence-gated parent synthesis입니다. child call이 만든 evidence manifest를 부모 합성 단계의 허용된 claim surface로 제한합니다.

TraceGuard는 의미를 추론하는 judge가 아닙니다. 구조적 validator입니다. 부모 답변에 fact_id가 없거나, fact_id는 있는데 evidence handle이 없거나, handle이 다른 chunk를 가리키거나, manifest에 없는 fact를 주장하면 reject합니다.

그래서 이 레포의 재미있는 지점은 "RLM이 long-context보다 항상 더 똑똑하다"가 아닙니다. 실제 benchmark에서도 vanilla와 RLM이 1.00 대 1.00으로 동률인 구간이 있습니다. 대신 RLM Forge가 보여주는 건 다른 주장입니다.

긴 문서 추론에서 중요한 건 컨텍스트 창 크기만이 아니라, 누가 어떤 evidence를 봤고, 부모 답변이 그 evidence 위에서만 조립됐는지 검증하는 실행 계약입니다.
저는 이 방향이 AI agent harness의 다음 관심사가 될 가능성이 높다고 봅니다. 모델을 더 크게 만드는 것만으로는 부족합니다. 이제는 모델이 읽고, 나누고, 맡기고, 합치고, 증거 없는 주장을 버리는 런타임이 필요합니다.

RLM은 큰 머리 하나가 아니라, 책상과 색인과 조교와 검수표를 가진 작업 방식입니다.

https://lnkd.in/guZSBZR6

---
작성자: 정구봉
URL: https://www.linkedin.com/feed/update/urn:li:activity:7457194866952003585/
