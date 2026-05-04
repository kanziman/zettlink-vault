---
url: https://www.linkedin.com/feed/update/urn:li:activity:7454276876363038720/
title: "openclaw github은 자동으로 운영됩니다. Peter가 만든 clawsweeper는 Codex 50"
channel: 정구봉
upload_date: 2026-05-04
duration: ""
date_saved: 2026-05-04
content_source: linkedin_post
raw_path: ""
tags: []
---

openclaw github은 자동으로 운영됩니다. Peter가 만든 clawsweeper는 Codex 50개를 24시간 병렬로 돌리면서 issue와 PR을 깊게 읽고, 이미 main에 반영됐거나 재현이 안 되거나 액션할 수 없는 것들을 정리합니다. Peter 말로는 오늘만 약 4000개를 닫았고, 수천 개가 pipeline에 남아 있습니다.

제가 제일 좋았던 건 close 숫자가 아니었습니다.

대시보드가 없습니다.

정확히는 README가 대시보드입니다. clawsweeper는 일하면서 README를 계속 갱신합니다. 지금 열린 issue/PR이 몇 개인지, 몇 개가 검토됐는지, 최근 24시간 동안 어떤 판단이 내려졌는지, audit health가 어떤지 전부 README에 남습니다.

저는 이런 운영 자동화를 볼 때 항상 별도 dashboard 페이지부터 찾습니다. 직접 작은 자동화를 만들 때도 비슷한 실패를 많이 했습니다. 운영 화면은 멋있게 만들었는데, 정작 source of truth가 문서, 로그, DB, Slack에 흩어졌습니다.

그런데 생각해보니 clawsweeper 방식이 훨씬 맞습니다.

오픈소스 repo에서 가장 오래 살아남는 인터페이스는 README입니다.

이슈는 닫히고, PR은 머지되고, workflow run은 흘러갑니다. 그런데 README는 항상 repo의 현관입니다. 사람이 처음 들어오는 곳이기도 하고, 에이전트가 다음 작업을 시작할 때 읽는 곳이기도 합니다.

그래서 “Readme is the new dashboard”라는 말이 계속 남습니다.

LLM 시대의 운영 도구는 화면을 하나 더 만드는 게 아닐 수 있습니다. 이미 모두가 읽는 문서를 살아있는 상태판으로 만드는 것일 수 있습니다. repo가 자기 상태를 설명하고, 자기 backlog를 정리하고, 자기 운영 기록을 남깁니다.

메인테이너가 repo를 운영하는 시대에서, repo가 스스로를 운영하는 시대로 넘어가고 있습니다.

https://lnkd.in/g4-2eNx6

---
작성자: 정구봉
URL: https://www.linkedin.com/feed/update/urn:li:activity:7454276876363038720/
