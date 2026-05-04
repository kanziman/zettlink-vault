---
url: https://www.linkedin.com/feed/update/urn:li:activity:7450519481509920769/
title: "AEO/GEO보다 더 중요한 건 Agent Feasibility 아닐까  요즘 AI 검색, AEO(AI En"
channel: 정성영
upload_date: 2026-05-05
duration: ""
date_saved: 2026-05-05
content_source: linkedin_post
raw_path: ""
tags: []
---

AEO/GEO보다 더 중요한 건 Agent Feasibility 아닐까

요즘 AI 검색, AEO(AI Engine Optimization) 이야기를 많이 한다.

내 서비스가 에이전트에게 잘 발견되게 하자.
검색되고, 인용되고, 추천되게 하자.

물론 중요하다.

Jeffrey Kim 님 덕분에, 시야가 여기서 좀더 넒어졌다.

핵심은 단지 에이전트에게 잘 보이는가가 아니라,
에이전트가 내 서비스를 끝까지 수행할 수 있는가에 더 가까운 것 아닐까.

이걸 나는 일단 Agent Feasibility라고 부르고 싶다.

정의해보면 이렇다.

Agent Feasibility란, 우리 서비스가 에이전트에게 얼마나 잘 이해되고, 접근되고, 호출되고, 실패에서 복구되며, 끝까지 과업을 완료할 수 있게 설계되어 있는가를 보는 프레임이다.

이 관점에서 보면 AX보다 먼저 필요한 건
조직 슬로건이 아니라 제품 자체를 agent-native하게 다시 쓰는 일일 수 있다.

내 서비스는 에이전트가 쓰기 쉬운 구조인가?

이 질문이 먼저다.

예를 들어 에이전트가 잘 쓰는 서비스는 대체로 이런 특징이 있다고 한다:

• 공식 API나 CLI가 있다
• README와 문서가 명확하다
• 프론트엔드가 안정적이다
• RSS나 structured feed가 있다
• 접근 가능한 리소스 파일이 있다
• URL 패턴이 예측 가능하다

이건 결국
에이전트가 이해하고, 탐색하고, 호출하고, 반복 사용하기 쉬운가의 문제다.

반대로 사람에게는 멀쩡해 보여도
에이전트에겐 거의 작업 불가능한 구조도 있다고 한다:

• 과도한 로그인/회원가입
• 본인인증, 2FA
• 보안 플러그인 설치 강제
• Cloudflare 차단
• 지나친 페이지네이션
• 모바일 앱 전용 구조
• 짧은 세션과 반복 쿠키 리셋

사람은 이 정도 마찰을 참고 넘어간다.
근데 에이전트는 여기서 쉽게 멈춘다.

그러다 보니
앞으로의 서비스 경쟁은
“에이전트에게 발견되는가”보다
“에이전트가 이 서비스를 끝까지 수행할 수 있는가”로 이동할 가능성이 크다.

AI discoverability 다음으로 Agent Feasibility Audit를 봐야 한다.

1. Discoverability — 에이전트가 entry point를 찾을 수 있는가
2. Interpretability — 문서/API/schema를 이해하기 쉬운가
3. Executability — 실제 호출과 작업 완료가 가능한가
4. Statefulness — 상태 조회, 이어하기, 멱등성이 가능한가
5. Recoverability — 실패 시 재시도와 복구가 가능한가
6. Guardrailed Access — 막기만 하는 게 아니라 안전하게 허용하는가

좋은 서비스는 agent가 통과하도록 설계되고,
나쁜 서비스는 agent를 로그인·검증·차단 루프에 가둔다.

---
작성자: 정성영
URL: https://www.linkedin.com/feed/update/urn:li:activity:7450519481509920769/
