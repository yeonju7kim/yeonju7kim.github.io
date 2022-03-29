---
layout: post
title: (AI502) 3. CNN
date: 2022-03-22 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 AI502수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## translation invariance

- 위치가 변해도 같은 추론값이 나와야 한다.
- CNN의 특징인 Weight sharing & Learn local features 때문에 translation invariance하다.

## Max pooling의 gradient update

max 값이 있었던 인덱스를 기억했다가 해당 pixel만 gradient update

## AlphaGo

- policy network : 다음 수를 둘 위치에 대한 확률 분포
- value network : 해당 착점에 대한 승률을 예측

## skip connection 의 장점

- gradient vanish 문제 적음