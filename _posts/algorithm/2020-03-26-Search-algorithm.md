---
date: 2020-03-25 03:00:00
layout: post
title: 탐색 알고리즘
subtitle: 선형 탐색과 이진 탐색 알고리즘
description: 선형 탐색과 이진 탐색 알고리즘을 알아보고 python을 통해 구현해보자
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
# Search algorithm



## 선형 탐색(Linear Search)

**List** 내 담긴 데이터를 처음부터 끝까지 하나하나씩 탐색하는 방법으로 정렬이 되지 않은 List를 탐색할 떄 사용한다.

<img src="/assets/img/contents/algorithm/Search_algorithm/image-20200326035008835.png" alt="image-20200326035008835" style="zoom:80%;" />

원하는 값을 찾을 때까지 탐색한다.



## 이진 탐색 (Binary Search)

**정렬되어있는 List**를 전제로 사용하는 탐색 방법으로 List의 반씩 제외시키면서 탐색하므로 선형 탐색에 비해 속도가 빠르다.

<img src="/assets/img/contents/algorithm/Search_algorithm/image-20200326035406839.png" alt="image-20200326035406839" style="zoom:80%;" />

중간값을 먼저 선택 후 찾고자 하는 값을 기준으로 왼쪽 또는 오른쪽을 남긴다.

<img src="/assets/img/contents/algorithm/Search_algorithm/image-20200326035504252.png" alt="image-20200326035504252" style="zoom:80%;" />

똑같이 남은 값들 중 중간값을 찾고 찾고자 하는 값을 기준으로 왼쪽 또는 오른쪽을 남긴다.

<img src="/assets/img/contents/algorithm/Search_algorithm/image-20200326035547925.png" alt="image-20200326035547925" style="zoom:80%;" />

반복 후 원하는 값을 찾아낸다.

## 두 알고리즘 간 속도 비교

<img src="/assets/img/contents/algorithm/Search_algorithm/image-20200326035759149.png" alt="image-20200326035759149" style="zoom:80%;" />

위 리스트(길이: 총 16)를 예시로 비교를 해보자

- `선형 탐색`
  - 가장 금방 되는 경우: 1번(찾고자 하는 값이 ‘2’일 때) 
  - 가장 오래 걸리는 경우: 16번(찾고자 하는 값이 ‘53’일 때 혹은 값이 없을 때)

- `이진 탐색`
  - 가장 금방 되는 경우: 1번(찾고자 하는 값이 ‘19’일 때) 
  - 가장 오래 걸리는 경우: 4번(찾고자 하는 값이 ‘0’일 때 혹은 값이 없을 때)

추가적으로 예시를 들자면, 페이스북 같은 경우 약 23억명의 유저가 있다.  `선형 탐색`의 경우 최악의 경우 **23억 번** 을 수행해야 할 수 있다. 반면 `이진 탐색`의 경우 최악의 경우 **31번**을 수행해야 한다. 그만큼 이진 탐색이 선형 탐색보다 효과적임을 알 수 있다 정렬이 되어있다는 전제조건만 있다면 말이다. 

시간복잡도는 N개의 List를 탐색한다고 가정할 경우 `선형 탐색`의 경우 `O(N)`으로 표시한다. 

`이진 탐색`은  N, N/2, N/4, N/8, … , 1으로 실행되는데 `2^m = N` 으로 나타낼 수 있고 여기서 m은 걸리는 경우의 수가 된다. 즉 `O(logN) `으로 표기할 수 있다.



## 코드

python 기반으로 코드를 작성하였음.

<script src="https://gist.github.com/madfalc0n/e3296f3b3d45580f55cc5c69afa6d00a.js"></script>