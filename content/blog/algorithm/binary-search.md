---
title: Binary Search
date: 2021-04-04 21:04:73
category: algorithm
thumbnail: { thumbnailSrc }
draft: false
---

# Jump into Binary Search

정렬된 자료에서 탐색하는 알고리즘입니다.
나열된 자료들 중에서 중앙에 있는 값을 기준으로 찾고자 하는 값이 큰 경우 혹은 작은 경우에 따라 찾아야 하는 자료의 범위가 반씩 줄어들기 때문에 시간 복잡도는 O(logN)이 됩니다.

## 1. 구현

### recursion

```Python
def binary_search(arr, v):
    def partition(left, right):
        if right < left:
            return
        nonlocal is_searched
        mid = (left + right) // 2
        if arr[mid] == v:
            is_searched = True
            return
        elif arr[mid] > v:
            partition(left, mid - 1)
        else:
            partition(mid + 1, right)

    is_searched = False
    partition(0, len(arr) - 1)

    return is_searched
```

### iteration

```Python
import time
def binary_search(arr, v):
    left = 0
    right = len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        # 인덱스를 더해 반으로 나누면 홀수는 중앙, 짝수는 중앙의 왼쪽
        if arr[mid] == v:
            return True
        elif arr[mid] < v:
            left = mid + 1
        else:
            right = mid - 1
    return False
```
