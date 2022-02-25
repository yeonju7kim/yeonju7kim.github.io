---
layout: post
title: python의 여러가지 sort 방법
date: 2022-02-25 00:00:10 +0900
category: python
use_math: true
comments: true
---
본 포스팅은 아래 게시물을 참고했습니다.

- https://www.geeksforgeeks.org/sort-sorteda-np-argsorta-np-lexsortb-python/

- https://runebook.dev/ko/docs/numpy/reference/generated/numpy.lexsort

책을 읽던 중 argsort를 보고, python에 여러가지 sort 방법이 있다는 것을 알게됐다. 그래서 이번에는 python의 여러가지 sort 방법에 대해 정리해보았다.

### 1. a.sort()
> 원래 배열을 정렬하고, return None

### 2. b = sorted(a)
> 원래 배열은 그대로 두고, 정렬된 배열을 return

### 3. b = np.argsort(a)
> 간접정렬 방법, 원래 배열은 그대로 두고, index를 값에 따라 정렬해서 return

### 4. ind = np.lexsort((b, a))
> a로 정렬한 다음 b로 정렬한다.

``` python
>>> a = [1,5,1,4,3,4,4] # 첫 번째 열
>>> b = [9,4,0,4,0,2,1] # 두 번째 열
>>> ind = np.lexsort((b,a)) # a로 정렬 한 다음 b로 정렬
>>> ind
array([2, 0, 4, 6, 5, 3, 1])

>>> [(a[i],b[i]) for i in np.argsort(a)]
[(1, 9), (1, 0), (3, 0), (4, 4), (4, 2), (4, 1), (5, 4)]

# 어휘적으로 정렬
>>> x = np.array([(1,9), (5,4), (1,0), (4,4), (3,0), (4,2), (4,1)],
...              dtype=np.dtype([('x', int), ('y', int)]))
>>> np.argsort(x) # or np.argsort(x, order=('x', 'y'))
array([2, 0, 4, 6, 5, 3, 1])

```