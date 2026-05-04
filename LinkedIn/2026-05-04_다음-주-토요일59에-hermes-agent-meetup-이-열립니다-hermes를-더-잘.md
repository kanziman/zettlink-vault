---
url: https://www.linkedin.com/feed/update/urn:li:activity:7456500334203564032/
title: "다음 주 토요일(5/9)에 Hermes Agent Meetup 이 열립니다. Hermes를 더 잘 쓰기 위해"
channel: 정구봉
upload_date: 2026-05-04
duration: ""
date_saved: 2026-05-04
content_source: linkedin_post
raw_path: ""
tags: []
---

다음 주 토요일(5/9)에 Hermes Agent Meetup 이 열립니다. Hermes를 더 잘 쓰기 위해 오늘부터 로그를 남겨봅니다. 결론부터, Hermes는 Claude Code를 대체하지 않아요. 그리고 벌써 Hermes 가 제 Codex 토큰의 절반을 씁니다 하하!

# day1. memory dump ?
"가져오겠습니다. 하지만 덤프하지 않습니다." Hermes Agent한테 Claude Code에서 쌓아온 메모리, skills, transcripts를 통째로 옮겨달라고 하면 거부합니다. 

저는 Claude Code를 오래 써왔고, Codex를 주로 쓰고 있어요. 자산이 꽤 쌓였고, 글로벌 CLAUDE.md, 프로젝트 skills, repo의 MEMORY.md 등이 많아요. Hermes를 사용하면서 갈아타면서 "이거 다 넣으면 바로 똑똑해지지 않을까?" 싶었어요.

매 세션 startup script에 지난 3년치 회의록을 전부 끼워 넣은 뇌를 상상해보세요. 무관한 작업에도 옛 프로젝트의 편향이 따라붙고, 새 컨텍스트는 매번 그 무게랑 싸워야 합니다. 하루는 강력해 보이지만, 그 다음부터 모든 작업이 오염됩니다.

그래서 Hermes는 raw import 대신 분류부터 했어요.

1. USER.md — 안 바뀌는 사용자 선호
"Python은 uv, TypeScript는 bun", "Explore subagent로 메인 컨텍스트 오염 막기" 같은 작업 스타일.

2. MEMORY.md — 안정적인 환경/프로젝트 사실
Deep Thought 미션 한 줄, 5도메인 폴더 구조, 자주 쓰는 절대경로. 컴팩트하게.

3. skills — 재사용 가능한 절차
linkedin-write, weekly-sync 같은 워크플로우. 메모리가 아니라 procedural memory로 따로 분리합니다.

4. external_dirs — repo가 source-of-truth인 skills
~/.hermes/skills로 복사하면 fork가 생기고 stale 돼요. config에 외부 디렉토리를 등록하고 read-only로 스캔만 시킵니다.
Codex, Claude Code 의 스킬 등은 여기로!

LangChain의 Deep Agent 메모리 분류도 비슷한 점을 시사합니다. 좀 더 의미를 해석하기 쉽게 볼 수 있어요. semantic(사실, 선호) / episodic(경험, 로그) / procedural(워크플로우). 셋을 한 통에 부으면 안 됩니다.

결국 핵심은 import 볼륨이 아니라 memory hygiene(오염 막기!)이에요. 에이전트 마이그레이션은 백업 복원이 아니라 큐레이션입니다.

---
제가 느끼는 기존 툴과 가장 큰 차이점은 연역 vs 귀납입니다. 그리고 모델의 지능이 충분히 똑똑해졌기 때문에 귀납적으로 동작하는 Hermes 가 잘 동작하게 된 것 같아요. 이 점을 중심으로 작성해보겠습니다.
https://luma.com/1cwwvh0p

---
작성자: 정구봉
URL: https://www.linkedin.com/feed/update/urn:li:activity:7456500334203564032/
