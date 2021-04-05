---
title: Quick Sort
date: 2021-04-03 20:04:76
category: algorithm
thumbnail: { thumbnailSrc }
draft: false
---

# Jump to Quick Sort 🚴

## 1. About Quick Sort

퀵 정렬은 분할[1]과 정복[2]을(Divide and conquer) 적극적으로 활용한 정렬 알고리즘이다.

퀵 정렬은 PIVOT이라는 기준값이 존재한다. 이 PIVOT을 기준으로 작은 값의 범위, 큰 값의 범위로 나누는 분할&정복 과정을 반복하는 알고리즘이다.

<div style="text-align:center"><img src="./images/Sorting_quicksort_anim.gif" alt="this slowpoke moves"/><div>

## 2. Code

case1:

1. 리스트의 중앙을 pivot으로 선택.
2. 왼쪽 끝에서 오른쪽으로 리스트를 조회하며 발견된 PIVOT 보다 큰 값과 오른쪽 끝에서 왼쪽으로 조회하며 발견된 PIVOT보다 작은 값을 SWAP.
3. 두 지점이 교차할 때 까지 1번과 2번 과정을 반복.
4. 교차 지점을 기준으로 왼쪽 리스트와 오른쪽 리스트에 대해 1번부터 3번까지 반복.

```python
def quick_sort(arr):
    def sort(arr, left, right):
        if right <= left:
            return
        mid = partition(arr, left, right)
        sort(arr, left, mid - 1)
        sort(arr, mid, right)
    def partition(arr, left, right):
        print('begin',arr)
        pivot = (left + right) // 2
        while left <= right:
            while arr[left] < arr[pivot]:
                # pivot 보다 큰 값을 가진 인덱스를 찾는다.
                left += 1
            while arr[right] > arr[pivot]:
                # pivot 보다 작은 값을 가진 인덱스를 찾는다.
                right -= 1
            if left <= right:
                arr[right], arr[left] = arr[left], arr[right]
                right -= 1
                left += 1
            print('ing',arr, left, right)
        return left
    sort(arr, 0, len(arr) - 1)
x = [0,1]
quick_sort(x)
print(x)
```

### 2.1. 디테일 조건

퀵정렬 처럼 구현 과정에서 while로 반복문을 처리하는 경우와 재귀함수를 실행하는 경우 종료조건을 매우 엄밀하게 설정해 주어야 한다.

1. 재귀함수의 종료조건: 처음 리스트가 분할되며 left와 right가 같아지는 순간이 더이상 분할될 수 없는 종료조건이라고 생각했다. 하지만 right가 left보다 작아지는 순간이 발생한다.

**예시**

```python
'''in quick_sort function'''
mid = partition(arr, left, right) # left = 0, right = 1
sort(arr, left, mid - 1) # left = 1, mid = 0
sort(arr, mid, right)

'''in partition method'''
if left <= right:
    print(left,right)
    arr[right], arr[left] = arr[left], arr[right]
    right -= 1
    left += 1
return right # 0 => mid가 됨
```

- left와 right가 같은 경우는 이미 return을 시키고 있기 때문에 제외한다.

- left가 0이고 right 가 1인 경우를 살펴보자.
  이부분에서 정렬이 되어있는 경우라면 right가 왼쪽으로 이동해서 0의 위치에 있게 된다. 그리고 left와 right가 같기 때문에 조건문에서 재자리 스왑이 일어나는 동시에 left는 1 right는 -1 이 된다. 따라서 **mid는 기존 left의 -1** 이 된 상태로 반환된다. 즉 left는 0 mid 는 -1이 되기 때문에 종료 조건문을 right <= left로 수정해 주어야 한다.

- 하지만 만약 return left를 해준다면,
  **mid는 기존 left보다 1 커진 값**을 반환한다.
  따라서 mid가 1가 되고 다음 퀵정렬의 왼쪽 범위는 `sort(arr, left, mid - 1)`로 left(0), mid(1) - 1 이기 때문에 == 조건에서 탈출된다. 또한 다음 퀵정렬의 오른쪽 범위는
  `sort(arr, mid, right)`로 mid(1) right(1)이기 때문에 == 조건에서 탈출하게 된다.

```python
while left <= right:
    while arr[left] < arr[pivot]: # pivot 보다 큰 값을 가진 인덱스를 찾는다.
        left += 1
    while arr[right] > arr[pivot]: # pivot 보다 작은 값을 가진 인덱스를 찾는다.
        right -= 1
```

- 만약 `if left <= right`를 `if left < right`로 수정해주면 어떤 일이 발생할까? left와 right가 같아지는 순간 while 문을 벗어날 수 없게 된다. => left <= right 조건에서도 반복되기 때문에.

- 이 때 위의 조건을 탈출하기 위해 `while left < right`로 바꿔주면, left가 0 right가 1처럼 1 인덱스가 차이나고 정렬이 되어있는 경우라면, partition의 안쪽에서는 left와 right가 모두 0이 되는 상황이 발생한다. 이때 mid는 left와 같아은 값을 반환한다. 즉 `sort(arr, mid, right)`는 계속 0과 1을 입력하게 되어 재귀문을 빠져나갈 수 없게 된다.
  => `sort(arr, mid, right)는 mid가 left와 같아지는 상황이 발생하면 무조건 재귀에 빠지게 된다.

---

**주석**:

[1] 분할: 커다란 문제를 작은 문제로 나누어 해결하는 과정

[2] 정복: 분할된 부분을 특정 기준에 맞게 만들어 가는 과정

**참조**:

1. [quicksort-wikipedia](https://en.wikipedia.org/wiki/Quicksort#:~:text=Quicksort%20is%20a%20divide%2Dand,sometimes%20called%20partition%2Dexchange%20sort.)
