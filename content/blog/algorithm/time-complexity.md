---
title: Time Complexity
date: 2021-04-04 17:04:78
category: algorithm
thumbnail: { thumbnailSrc }
draft: false
---

# Jump to Complexity

## 1. Algorithm

알고리즘이란 문제를 해결하기 위한 여러 동작들의 모임입니다. 서로 다른 두 개의 알고리즘이 같은 결과를 출력할지라도 소비되는 컴퓨터의 메모리와, 출력까지 소요되는 시간은 달라지게 됩니다. 즉, 메모리와 시간이 알고리즘을 측정할 수 있는 기준이 됩니다.

## 2. Complexity

알고리즘이 어떤 문제를 해결하는데 걸리는 시간을 시간 복잡도, 소비하는 메모리의 크기를 공간복잡도라고 부르고 있습니다.

## 2. Scape Complexity

공간 복잡도는 알고리즘이 동작하기 위해 필요한 공간의 크기 입니다. 대부분의 알고리즘이 중복되는 연산의 중간과정을 저장하고 재사용하기 위해 메모리를 소비합니다.

## 3. Time Complexity

알고리즘이 동작하는 데에 걸리는 시간 또는 연산의 횟수

#### 3.1. 시간 복잡도의 계산 방법

반복문과 조건문을 고려해서 실행 횟수를 분석하는 방법이 있습니다.

<img src="./images/analize_time_complexity.png" alt="analize time complextity"/>

위 코드는

1. n은 알고리즘이 처리해야할 자료의 크기
2. for 문의 i에 대입되는 연산 횟수 n번
3. sum 변수와 array[i]의 덧샘 연산 횟수 n번
4. 덧샘 연산이 끝나고 sum 변수에 대입되는 연산 횟수 n번

으로 총 3n번의 시간복잡도를 가지게 됩니다.

**NOTE:** 조건문과 같이 경우에 따라 반복되는 횟수가 달라지는 경우가 있습니다. 따라서 최악의 경우, 최선의 경우, 평균적인 경우로 알고리즘의 복잡도를 정의할 수 있습니다. 그리고 일반적으로는 **최악의 경우**에 대해 알고리즘의 복잡도를 정의합니다.

## 4. Asymtotic Notation (점진적 표기법)

보통 n의 크기가 작을 때는 소요되는 시간이 매우 작습니다.
따라서 알고리즘에 입력되는 자료의 개수 n이 충분히 커졌을 때 알고리즘의 성능에 따라 사용자는 영향을 받게 됩니다.

이렇게 n이 충분이 크다고 가정한 상태에서 하드웨어 성능을 배제하고 알고리즘의 성능만을 공평하게 비교할 수있는 효율적인 표기 방법이 **점진적 표기법** 입니다.

- 복잡도 순위
- O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(2^n) < O(n!)
  - 상수, 로그, 선형, 선형로그, 다항식(제곱), 지수, 팩토리얼

### 4.1. Big-O Notation

Big-O는 시간의 상한을 나타냅니다. 시간의 상한이란 예를 들어 O(n^2)으로 표기된 Big-O 표기법은 O(1), O(n) 처럼 O(n^2)보다 높은 성능을 보여주는 시간 복잡도를 모두 포함한다는 의미입니다. 즉, 보통 최악의 경우를 많이 생각하기 때문에 최악의 Big-O 표기법은 해당 알고리즘이 **최악의 경우**에도 표기된 **성능을 보장**한다는 의미로 해석할 수 있습니다.

<img src="./images/Big-O-Graph.png" alt="Big-O-Graph"/>

- 시간 복잡도 f(n) 의 Big-O Notaion(정의):
- O(g(n)) = { f(n)|0 <= f(n) <= c\*g(n) for all n >= n0 > 0}

- 예시
  - ![3(n+1)^2 \in O(n^2)](<https://render.githubusercontent.com/render/math?math=3(n%2B1)%5E2%20%5Cin%20O(n%5E2)>)
  - ![n^{1.998} \in O(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E%7B1.998%7D%20%5Cin%20O(n%5E2)>)
  - ![n^2 + n\log n + 3 \in O(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E2%20%2B%20n%5Clog%20n%20%2B%203%20%5Cin%20O(n%5E2)>)
  - ![n^2 \in O(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E2%20%5Cin%20O(n%5E2)>)
  - ![n \in O(n^2)](<https://render.githubusercontent.com/render/math?math=n%20%5Cin%20O(n%5E2)>)

### 4.2. Big-Omega Notation

Big-Omega는 하한을 나타냅니다.

<img src="./images/Big-Omega-Graph.png" alt="Big-O-Graph"/>

- 시간복잡도 f(n)의 Big-Omega Notation(정의):
- Ω(g(n)) = { f(n)|0 <= c\*g(n) <= f(n) for all n >= n0 > 0}

- 예시
  - ![3(n+1)^2 \in \text{Ω}(n^2)](<https://render.githubusercontent.com/render/math?math=3(n%2B1)%5E2%20%5Cin%20%5Ctext{Ω}(n%5E2)>)
  - ![n^{2.002} \in \text{Ω}(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E%7B2.002%7D%20%5Cin%20%5Ctext{Ω}(n%5E2)>)
  - ![n^2 + NlogN + 3 \in \text{Ω}(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E2%20%2B%20NlogN%20%2B%203%20%5Cin%20%5Ctext{Ω}(n%5E2)>)
  - ![n^2 \in \text{Ω}(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E2%20%5Cin%20%5Ctext{Ω}(n%5E2)>)
  - ![n^3 \in \text{Ω}(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E3%20%5Cin%20%5Ctext{Ω}(n%5E2)>)

### 4.3 Big-Theta Notation

Big-Theta는 상한과 하한의 교집합을 나타냅니다.

<img src="./images/Big-Theta-Graph.png" alt="Big-O-Graph"/>

- 시간복잡도 f(n)의 Big-Theta Notation(정의):

- ![f(n)](<https://render.githubusercontent.com/render/math?math=f(n)>) 의 Big-Theta Notation 정의:

  - ![\text{Θ}(g(n)) = { f(n)|0 \le c_1 \cdot g(n) \le f(n) \le c_2 \cdot g(n)\space\space \text{for all}\space n \ge n_0 > 0 }\space \space \text{for}\space \space \exists c_1 > 0,\space\exists c_2 > 0.](<https://render.githubusercontent.com/render/math?math=%5Ctext{Θ}(g(n))%20%3D%20%5C%7B%20f(n)%7C0%20%5Cle%20c_1%20%5Ccdot%20g(n)%20%5Cle%20f(n)%20%5Cle%20c_2%20%5Ccdot%20g(n)%5Cspace%5Cspace%20%5Ctext%7Bfor%20all%7D%5Cspace%20n%20%5Cge%20n_0%20%3E%200%20%5C%7D%5Cspace%20%5Cspace%20%5Ctext%7Bfor%7D%5Cspace%20%5Cspace%20%5Cexists%20c_1%20%3E%200%2C%5Cspace%5Cexists%20c_2%20%3E%200.>)

- 예시
  - ![3(n+1)^2 \in \text{Θ}(n^2)](<https://render.githubusercontent.com/render/math?math=3(n%2B1)%5E2%20%5Cin%20%5Ctext{Θ}(n%5E2)>)
  - ![n^2 + n\log n + 3 \in \text{Θ}(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E2%20%2B%20n%5Clog%20n%20%2B%203%20%5Cin%20%5Ctext{Θ}(n%5E2)>)
  - ![n^2 \in \text{Θ}(n^2)](<https://render.githubusercontent.com/render/math?math=n%5E2%20%5Cin%20%5Ctext{Θ}(n%5E2)>)
  - ![n^3 \in \text{Θ}(n^3)](<https://render.githubusercontent.com/render/math?math=n%5E3%20%5Cin%20%5Ctext{Θ}(n%5E3)>)
