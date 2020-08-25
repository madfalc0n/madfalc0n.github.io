---
date: 2020-05-25 03:00:00
layout: post
title: Dynamic Programming 알고리즘
subtitle: Dynamic Programming 알고리즘
description: Dynamic Programming 알고리즘을 이해하고 구현해보자!
image: /assets/img/banner/coding.jpg
optimized_image: /assets/img/banner/coding.jpg
category: algorithm
tags:
  - python
  - algorithm
author: madfalc0n
paginate: true
comments: true
---
# Dynamic Programming

최적의 부분으로 나눌 수 있고 중복되는 부분이 있다면 한번 계산한 결과를 버리지 않고 다시 활용하는 것

- 하나의 문제는 단 한번만 풀도록 하는 알고리즘
- 문제에서 규칙성을 찾아 점화식을 세우는 것이 중요하다.



## 가정

1. `최적 부분 구조(Optimal Substructure)`가 있어야 한다.
   1. 부분 문제들의 `최적의 답`을 이용해서 기존 문제들의 `최적의 답`을 구할 수 있다는 것
   2. 즉, **기존문제**를 **부분 문제**로 나눠서 풀 수 있다. 
2. `중복되는 부분 문제(Overlapping Subproblems)`가 있어야 한다.
   1. 구해야할 답들이 중복으로 나올 수 있다.
   2. 중복으로 나오는 답은 결과를 미리 배열에 저장해놓고 불러다온다



## 종류

접근방식에는 **Memoization**방식 과 **Tabulation** 방식으로 나뉘는데 둘의 공통점은 중복되는 부분 문제의 비효율성을 해결한다.

1. 상향식 접근(Bottom-up Approach, **Tabulation**)

   - 테이블 방식으로 정리해가는 방식

   - 아래에서 위로 문제를 푸는 방식
   - **반복문**을 사용한다.
   - 반복문을 이용해 가장 작은 부분부터 모두 계산하기 때문에 중간에 필요없는 답까지 계산하게 될 수 있다.
   - 재귀호출을 하지 않아 스택이 계속 쌓이는 오류가 발생하지 않는다(Memoization의 단점).

2. 하향식 접근(Top-down Approach, **Memoization**)

   - 여러개의 큰 문제를 작은 문제로 분할한 다음 각각의 결과를 결합해 큰 문제를 해결하는 것
   - **재귀호출** 방식을 사용한다.
   - 재귀호출이 많이 일어나면 스택이 계속 쌓이게 되면서 오류가 발생할 수 있다.
   - 필요한 계산이 무엇인지 요구를 하기 때문에 필요없는 답은 계산하지 않는다(Tabulation의 단점). 

   

## 예시

### 1.피보나치 수열

#### 가정

- 피보나치 수열의 기본공식은 다음과 같다.
  - D[i] = D[i-1] + D[i-2]

```python
def pivo(x):
    if x == 1:
        return 1
    if x == 2:
        return 1
    return pivo(x-1) + pivo(x-2)

print(pivo(10))
# 55
```

#### 문제점

- 해당 코드에는 시간복잡도와 관련해서 문제가 발생한다.

  <img src="/assets/img/contents/algorithm/Dynamic_programming/fivo.PNG" alt="fivo" style="zoom:50%;" />

  - Function 들이 겹치는 부분인데 처음 F(n-1)하고 F(n-2)를 했을 때 값의 저장이 되지 않으므로 각자 자기 줄기를 계속 뻗어나갈 때마다 계산을 수행하게 된다.
  - 시간복잡도는 O(2^n) 이 된다.

#### 해결방법

- 각 계산된 함수는 배열에 저장하여 기존 계산된 값 호출 시 불러오면 시간복잡도는 O(n)이 된다.

  <img src="/assets/img/contents/algorithm/Dynamic_programming/pivo_sol.jpg" alt="pivo_sol" style="zoom:50%;" />

  > 수행절차에서 4번과 5번은 배열에 저장된 값을 불러오게 되므로 시간복잡도는 O(n)

- 소스코드

  ```python
  memo = {1:1, 2:1}
  
  def fivo(x):
      if x == 1:
          return 1
      if x == 2:
          return 1
      if x not in memo:
          memo[x] = fivo(x - 1) + fivo(x - 2)
      return memo[x]
  
  print(fivo(50))
  #12586269025
  #메모이제이션을 사용하지 않는다면 2^50 시간복잡도가 수행된다.
  ```

  

