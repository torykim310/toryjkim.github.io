---
title: Abstract Data Type
date: 2021-04-12 20:04:37
category: data structure
thumbnail: { thumbnailSrc }
draft: false
---

## 추상자료형이란?

값이나 연산의 집합으로 정의되는 **자료형의 수학적 모델**.

### 특징

1. ADT만 알고있다면 하나의 ADT로 부터 구현된 여러개의 자료구조들을 ADT에 정의된 방법으로 동일하게 사용할 수 있다. ex) ADT:List, DS: ArrayList, LinkedList)
2. 또한 동일한 결과를 보여주는 두 자료구조라도 내부 구현방식은 다를 수 있기 때문에, 알고리즘상 유리한 자료구조를 상황에 맞게 선택할 수 있다.
3. DS 개발자 입장에서는 ADT를 참조해서 DS를 만들면 되기 때문에, 비교적 원활하게 원하는 기능을 구현할 수 있다.

### 자료구조와의 차이점

- 구현 여부
  - 자료 구조는 실제로 구현되어, 사용할 수 있다. ex)Java의 추상 자료형 Interface는 아무런 구현이 되어있지 않다.
