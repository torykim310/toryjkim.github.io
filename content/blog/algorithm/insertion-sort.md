---
title: Insertion Sort
date: 2021-04-04 12:04:74
category: algorithm
thumbnail: { thumbnailSrc }
draft: false
---

# Jump to Insertion Sort

## 1. About Insertion Sort

삽입 정렬은 가장 기본적인 정렬 알고리즘 중에 하나입니다.
기본적으로 정렬되지 않은 부분과 정렬된 부분으로 나눌 수 있습니다. 우선 정렬되지 않는 부분을 순차적으로 순회합니다. 이 때 각 데이터가 정렬된 부분의 어느 위치에 삽입되어야 정렬 상태를 유지하는지 찾아내고 삽입합니다.

## 2. Time Complexity

시간 복잡도는 정렬할 부분을 순회하기 위한 O(n)과 삽입될 위치를 찾기 위한 O(n)이 곱해져 평균적으로 O(n^2)의 시간복잡도를 가지게 됩니다. 하지만 만약에 삽입될 위치를 찾는 과정에서 단 한번에 삽입될 위치를 찾게 되는 최선의 상황에는 O(n) 시간복잡도를 가지게 됩니다.

- 최악: O(n^2)
- 평균: O(n^2)
- 최선: O(n)

## 3. Code

- 처음 코드 작성

```Python
def insertion_sort(arr):
    for unsorted_idx in range(1, len(arr)):
        for sorted_idx in range(0, unsorted_idx):
            if arr[sorted_idx] > arr[unsorted_idx]:
                value = arr[unsorted_idx]
                del arr[unsorted_idx]
                arr.insert(sorted_idx, value)
                break
```

- 참고 후 코드 작성

```Python
def insertion_sort(arr):
    for unsorted_idx in range(1, len(arr)):
        j = unsorted_idx - 1 # 정렬된 부분의 가장 오른쪽 인덱스
        value_to_sort = arr[unsorted_idx]
        while j >= 0 and arr[j] > value_to_sort:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = value_to_sort

```

첫 코드에서 리스트의 중앙에 있는 요소를 삭제할 때 O(n)의 시간복잡도와 삽입될 위치를 찾아가는 과정 O(n)의 시간 복잡도, 마지막으로 삽입되는 순간 O(n)의 시간 복잡도가 소요된다. 참고 후 코드는 삽입할 위치를 찾아가는 과정에서 O(n)만의 시간 복잡도와 삽입할 때 O(1)이 소요되기 때문에 같은 O(n)의 시간 복잡도 일지라도 더 효율적인 알고리즘이다.
