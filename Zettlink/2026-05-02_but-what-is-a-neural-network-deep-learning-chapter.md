---
url: https://www.youtube.com/watch?v=aircAruvnKk
title: But what is a neural network? | Deep learning chapter 1
channel: 3Blue1Brown
upload_date: 2017-10-05
duration: 18:40
date_saved: 2026-05-02
content_source: subtitle_ko
tags: 
  - deep-learning
  - neural-networks
  - machine-learning
  - computer-vision
  - mathematics
  - tutorial
  - lecture
---

# But what is a neural network? | Deep learning chapter 1

## 요약
이 영상은 3Blue1Brown의 딥러닝 시리즈 첫 번째 장으로, 신경망의 기본 구조와 작동 원리를 수학적으로 설명합니다. 필기체 숫자 인식을 예시로 들어 입력층, 은닉층, 출력층의 계층 구조, 가중치(weights)와 편향(bias), 시그모이드 함수 등의 핵심 개념을 상세히 다룹니다. 신경망이 어떻게 픽셀에서 시작해 부분적 특징을 인식한 후 최종 숫자를 판별하는지 계층적 추상화 과정을 설명하며, 행렬 벡터 표현을 통해 복잡한 신경망을 수식으로 간결하게 표현하는 방법을 보여줍니다.

## 인사이트
- 신경망의 은닉층은 입력값의 추상화된 특징을 점진적으로 학습합니다. 첫 번째 은닉층은 픽셀의 조합으로 작은 선분이나 곡선 같은 에지를 인식하고, 다음 층은 이를 조합해 동그라미나 특정 패턴을 인식하며, 최종적으로 이들의 조합으로 숫자를 분류합니다.
- 가중치와 편향은 신경망의 학습 가능한 매개변수로서 각각 다른 의미를 갖습니다. 가중치는 입력층의 특정 패턴을 감지하도록 하고, 편향은 뉴런이 활성화되기 위해 필요한 임계값을 결정합니다.
- 시그모이드 함수는 가중 합을 0과 1 사이의 확률값으로 압축하여 뉴런의 활성화 정도를 표현하지만, 현대의 신경망은 훈련이 더 효율적인 ReLU 함수를 주로 사용합니다.
- 신경망 전체는 784개의 입력을 받아 10개의 출력을 생성하는 극도로 복잡한 함수이며, 약 13,000개의 가중치와 편향 같은 매개변수를 조정하여 작동합니다. 이러한 복잡성이 오히려 신경망의 강력함의 원천입니다.

---
채널: 3Blue1Brown
URL: https://www.youtube.com/watch?v=aircAruvnKk
