---
layout: post
title: [pytorch] hook
date: 2022-03-02 00:10:00 +0900
category: ongoing
use_math: true
comments: true
---

아래 게시물을 참고했습니다.

- <https://ichi.pro/ko/al-aya-hal-pytorch-teulig-49884369363658>
- <https://daebaq27.tistory.com/65#:~:text=hook%3A%20%EC%9D%BC%EB%B0%98%EC%A0%81%EC%9C%BC%EB%A1%9C%20hook%EC%9D%80,%EA%B1%B8%EC%96%B4%EB%86%93%EB%8A%94%20%EA%B2%BD%EC%9A%B0%EB%A5%BC%20%EC%9D%BC%EC%BB%AC%EC%9D%8C.&text=input%EC%9D%80%20positional%20arguments%EB%A7%8C,forward%20%EC%84%9C%EB%A7%8C%20%EC%A0%81%EC%9A%A9%EC%9D%B4%20%EB%90%9C%EB%8B%A4>.

---

## hook 란?

pytorch를 사용할 때, 디버깅을 위해 패키지 중간에 자기가 원하는 코드 끼워넣을 수 있는 기능이다.

---
## hook의 3가지 종류

### 포워드 프리 훅 : 포워드 패스 전에 실행

register_forward_pre_hook

### 포워드 훅 : 포워드 패스 후 실행

register_forward_hook

### 역방향 후크 : 역방향 패스 후 실행

register_full_backward_hook