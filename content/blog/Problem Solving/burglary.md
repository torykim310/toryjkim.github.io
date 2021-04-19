---
title: burglary
date: 2021-04-07 11:04:89
category: Problem Solving
thumbnail: { thumbnailSrc }
draft: false
---

## 문제

> 도둑이 어느 마을을 털 계획을 하고 있습니다. 이 마을의 모든 집들은 아래 그림과 같이 동그랗게 배치되어 있습니다. 각 집들은 서로 인접한 집들과 방범장치가 연결되어 있기 때문에 인접한 두 집을 털면 경보가 울립니다.

<div style="text-align:center">
    <img src="https://grepp-programmers.s3.amazonaws.com/files/ybm/e7dd4f51c3/a228c73d-1cbe-4d59-bb5d-833fd18d3382.png"/>
    <cite>
        <a href="https://grepp-programmers.s3.amazonaws.com/files/ybm/e7dd4f51c3/a228c73d-1cbe-4d59-bb5d-833fd18d3382.png" target="_black">burglary image</a> by Programmers
    </cite>
</div>

> 각 집에 있는 돈이 담긴 배열 money가 주어질 때, 도둑이 훔칠 수 있는 돈의 최댓값을 return 하도록 solution 함수를 작성하세요.

## 제한사항

- 이 마을에 있는 집은 `3`개 이상 `1,000,000`개 이하입니다.
- money 배열의 각 워소는 `0` 이상 `1,000` 이하인 정수입니다.

## 나의 풀이

```Python
def solution(money):
    # not_pick_last_case
    money_0 = money[:-1]
    dp = [0] * len(money_0)
    dp[0] = money_0[0]
    dp[1] = max(money_0[0],money_0[1])

    for i in range(2, len(money_0)):
        dp[i] = max(dp[i-2] + money_0[i], dp[i-1])

    first_max = dp[-1]
    # pick_last_house
    money_1 = money[1:]
    dp = [0] * len(money_1)
    dp[0] = money_1[0]
    dp[1] = max(money_1[0],money_1[1])
    for i in range(2, len(money_1)):
        dp[i] = max(dp[i-2] + money_1[i], dp[i-1])
    second_max = dp[-1]
    return max(first_max, second_max)
```

## 접근법

우선 문제를 보고 어떻게 인접하지 않은 집들을 털수 있을까 생각해 보았다. 집이 홀수일 때, 짝수일 때를 나누어 생각해보았고 어떤 규칙에 따라 집을 찾아가는 greedy 방식을 사용하면 최대 1,000,000개가 되는 집들 사이로 어떤 경우가 최대가 되는지를 파악해야 했다. 어쩌면 factorial 형태로 모든 경우의 수를 따져야 될 수 도 있고, 명확하게 어떤 순서로 집을 털어야 하는지 방법이 떠오르지 않았다. 그래서 이럴 때 최적해를 반환하는 f(n)이 f(n-a)와 어떤 관계가 있는지 파악할 수 있다면 해답을 찾을 수 있기 때문에 다음으로 떠올렸던 방법이 DP다.

f(n)을 1번부터 n번 집까지 물건을 훔치는 경우의 수 중에서 최대의 금액을 훔친 경우라고 가정했다. 여기서 꼭 짚고 넘어가야하는 것이 도둑은 인접한 집을 털수없다는 점이다. 이 개념을 연장하면 n번 집을 털었는지 아닌지를 기준으로 두 가지로 나눠서 생각해 볼수있다. n번 집을 털어서 최대 금액이 되었다면 n-1번 집을 털지 않았다는 뜻이 되고 이를 식으로 표현하면 `f(n) = f(n-2) + money[n]`이 된다. 반면 n번째 집을 털지 않았을 때라면 n-1번째 집을 털어서 최대로 훔칠수 있는 가능성이 생기고 이를 식으로 표현해보면 `f(n) = f(n-1)` 이된다. 즉 이 두 가지 중에 큰 값이 최대로 훔친 금액이 되는 것이다.

하지만 위의 방식으로 문제를 풀면 한가지 문제점이 있다. 만약 도둑이 n번째 집을 털고서 최대한 많은 금액을 훔쳤다면 이 때 1번째 집도 같이 털어서 최대가 되는 경우가 생길 수 있다는 점이다. n번째와 1번째는 인접한 곳이기 때문에 조건에 어긋난다. 그래서 n번째 집을 털어서 최대가 됐다는 가정에는 1번째 집을 아예 제외시켜야 한다. 그 코드가 바로 아래 코드가 된다.

```Python
money_1 = money[1:]
dp = [0] * len(money_1)
dp[0] = money_1[0]
dp[1] = max(money_1[0],money_1[1])
for i in range(2, len(money_1)):
    dp[i] = max(dp[i-2] + money_1[i], dp[i-1])
second_max = dp[-1]
```

그런데 여기서 한 가지 더 따져야 할 조건이 있다. 곰곰이 생각해보면 1번째 집을 제외하고, n번째 집을 털지 않았을 때 최대가 되는 경우가 발생하는데, 그렇다면 1번째 집을 포함해서 n번째 집을 털지 않았을 때가 최대가 되는 경우도 있지 않을까? 라는 생각에 탄생한 코드가 1번째 집을 포함하고 n번째 집을 제외한 경우의 수중 최대를 찾는 코드이다.

```Python
money_0 = money[:-1]
dp = [0] * len(money_0)
dp[0] = money_0[0]
dp[1] = max(money_0[0],money_0[1])

for i in range(2, len(money_0)):
    dp[i] = max(dp[i-2] + money_0[i], dp[i-1])
```

이 둘중 최대값을 찾고 반환하면 해답을 얻을 수 있다.
