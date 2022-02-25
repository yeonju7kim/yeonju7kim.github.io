---
layout: post
title: python의 여러가지 sort 방법
date: 2022-02-25 00:00:10 +0900
category: python
use_math: true
comments: true
---
본 포스팅은 아래 게시물을 참고했습니다.

https://www.geeksforgeeks.org/sort-sorteda-np-argsorta-np-lexsortb-python/

책을 읽던 중 argsort를 보고, python에 여러가지 sort 방법이 있다는 것을 알게됐다. 그래서 이번에는 python의 여러가지 sort 방법에 대해 정리해보았다.

### 1. a.sort()
> 원래 배열을 정렬하고, return None

### 2. b = sorted(a)
> 원래 배열은 그대로 두고, 정렬된 배열을 return

### 3. np.argsort(a)
> 원래 배열은 그대로 두고, index를 값에 따라 정렬해서 return

### 4. np.lexsort((b, a))
> 