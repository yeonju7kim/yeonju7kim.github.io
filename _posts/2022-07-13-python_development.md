---
layout: post
title: python development tool
date: 2022-07-13 00:00:00 +0900
category: sw
use_math: true
comments: true
---

# Python 개발 툴

lightning 깃허브를 구경해보면서 python 개발 툴들에 대해 알게 돼서 나중에 필요할 때 보려고 정리해두었습니다.

pre-commit는 앞으로 자주 사용할 거 같습니다.

## pre-commit

https://pre-commit.com/

pre-commit hook은 코드를 커밋할 때마다 자동으로 특정 작업을 실행해줌.
- formatter : 코드 스타일을 통일
- linter : 코드에 잠재하고 있는 문제들을 찾아냄

### 설치

-  pip install pre-commit

### 사용법

- .pre-commit-config.yaml가 필요
  - pre-commit sample-config > .pre-commit-config.yaml
- 수동으로 하는 법
  - pre-commit run
- 자동화
  - pre-commit install

## pytest

- pytest: 테스트를 작성하는 데 있어 함수만 정의하면 되므로 편리합니다.
- 
- TDD(Test Driven Development)
  - 테스트 계획 및 코드를 작성
  - 테스트가 개발을 이끌어 나가는 것

### 설치

- pip install -U pytest
- pip3 install -U pytest

### 사용

1. 간단한 테스트

``` python
# first_test.py

# 테스트를 해보고 싶은 함수
def func(x):
    return x + 1

# 테스트 함수
def test_answer():
    assert func(3) == 5
```

```
$ pytest first_test.py
```

2. 클래스와 문자열 테스트

``` python
# Second test
class TestClass:
    def test_one(self):
        x = "Hello, hi"
        assert "h" in x

    def test_two(self):
        x = "what"
        assert hasattr(x, "who")
```

3. 실행

- python –m pytest tests(폴더이름)

### fixture

``` python
# test_calculator.py
from src.calculator import Calculator
def test_add():
    calculator = Calculator()
    assert calculator.add(1, 2) == 3
    assert calculator.add(2, 2) == 4

def test_subtract():
    calculator = Calculator()
    assert calculator.subtract(5, 1) == 4
    assert calculator.subtract(3, 2) == 1

def test_multiply():
    calculator = Calculator()
    assert calculator.multiply(2, 2) == 4
    assert calculator.multiply(5, 6) == 30

def test_divide():
    calculator = Calculator()
    assert calculator.divide(8, 2) == 4
    assert calculator.divide(9, 3) == 3
```

``` python
import pytest
from src.calculator import Calculator

@pytest.fixture
def calculator():
    calculator = Calculator()
    return calculator

def test_add(calculator):
    assert calculator.add(1, 2) == 3
    assert calculator.add(2, 2) == 4

def test_subtract(calculator):
    assert calculator.subtract(5, 1) == 4
    assert calculator.subtract(3, 2) == 1

def test_multiply(calculator):
    assert calculator.multiply(2, 2) == 4
    assert calculator.multiply(5, 6) == 30
```

## Unittest

- unittest: 테스트를 작성하기 위해 반드시 클래스를 정의해야 하므로 불편합니다.

## Unittest vs pytest 차이

https://www.bangseongbeom.com/unittest-vs-pytest.html