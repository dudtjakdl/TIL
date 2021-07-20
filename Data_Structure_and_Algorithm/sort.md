> 해당 문서는 [Do it! 자료구조와 함께 배우는 알고리즘 입문 : 파이썬 편 (시바타 보요 저)](http://www.yes24.com/Product/Goods/91219874)을 보고 정리한 내용입니다.
- 본 문서에 작성된 코드는 **파이썬 (Python)** 으로 작성하였습니다.
- 책을 보며 공부하면서 도움이 된 파이썬 문법과 개념은 [Python 폴더](https://github.com/dudtjakdl/TIL/blob/main/Python)의 문서에 정리하였습니다.
- 그 외 추가 내용은 인터넷 검색을 통해 공부하고 덧붙여 정리하였습니다.

# 정렬
    정렬 (sorting) : 데이터 집합의 원소들을 대소 관계나 번호 순서와 같이 일정한 순서대로 바꾸어 늘어놓는 작업

    오름차순 (ascending order) : 값이 작은 데이터를 앞쪽에 늘어놓는 것
    내림차순 (descending order) : 값이 큰 데이터를 앞쪽에 늘어놓는 것

정렬 알고리즘은 정렬을 수행하는 알고리즘이다. 대부분의 정렬 알고리즘 과정에는 데이터의 *교환, 선택, 삽입*이 일어나며 정렬 알고리즘에서 자주 등장하는 핵심 기술이다.

정렬 알고리즘을 하나의 배열 안에서 수행할 수 있는 경우에는 **내부 정렬**을 사용하고, 그렇지 않은 경우에는 **외부 정렬**을 사용한다. 외부 정렬은 정렬한 데이터가 배열의 크기를 넘어서서 하나의 배열에 저장할 수 없는 경우에 사용하는 알고리즘이다.

## 버블 정렬
    버블 정렬 (bubble sort) : 이웃한 두 원소의 대소 관계를 비교하여 필요에 따라 교환을 반복하는 알고리즘. 단순 교환 정렬이라고도 한다.

![버블 정렬](https://i2.wp.com/www.computersciencebytes.com/wp-content/uploads/2016/10/bubble_sort.png?w=556)

- 이웃한 원소를 비교하고 교환하는 과정을 **패스(pass)** 라고 한다.
- 원소 수가 n일때, 모든 원소의 정렬을 수행하려면 패스를 n - 1 번 수행해야 한다.
- 패스를 한 번 수행할 때마다 정렬할 대상과 비교 횟수가 1개씩 줄어든다.
- 시간 복잡도는 O(n^2) 이다.

```python
def bubble_sort(a: MutableSequence) -> None:
    n = len(a)
    for i in range(n - 1):
        for j in range(n - 1 - i):
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
```

버블 정렬의 알고리즘의 성능을 개선시키는 방법도 있다. 

첫번째 방법은 어떤 패스의 원소 교환 횟수가 0이면 모든 원소가 정렬을 완료했다는 의미이므로, 다음 패스를 진행하지 않아도 된다. 즉, 각 패스마다 원소 교환 횟수를 저장한 뒤 그 값이 0이면 다음 패스를 진행하지 않고 함수를 종료한다.

두번째 방법은 스캔 범위를 제한하는 방법이다. 각 패스마다 마지막으로 교환한 위치를 저장하고 그 뒤는 이미 정렬이 되어있다는 뜻이므로, 다음 패스에서 마지막 교환 위치까지만 스캔 범위를 지정하여 정렬을 수행한다.

> 이미지 출처 http://www.computersciencebytes.com/sorting-algorithms/bubble-sort/

### 셰이커 정렬

하지만 배열 [9, 1, 2, 3, 4] 와 같이 가장 큰 원소가 앞쪽에 있을 경우, 9를 한 패스마다 뒤로 이동해야 하기 때문에 버블 정렬 알고리즘의 성능이 나빠진다.

이런 문제를 해결하기 위해 버블 정렬을 개선한 알고리즘이 **셰이커 정렬(shaker sort)** 이다. 셰이커 정렬은 양방향 버블 정렬, 칵테일 정렬, 칵테일 셰이커 정렬 이라고도 한다.

셰이커 정렬은 홀수 패스에서는 뒤부터 비교를 시작해 작은 원소를 앞으로 이동시키며, 짝수 패스에서는 앞에서부터 비교를 시작해 큰 원소를 뒤로 이동시킨다.

```python
def shaker_sort(a: MutableSequence) -> None:
    left = 0
    right = len(a) - 1
    last = right
    while left < right:
        for j in range(right, left, -1): # 홀수 패스 (작은 원소를 앞으로)
            if a[j - 1] > a[j]:
                a[j - 1], a[j] = a[j], a[j - 1]
                last = j
        left = last

        for j in range(left, right): # 짝수 패스 (큰 원소를 뒤로)
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
                last = j
        right = last
```

## 선택 정렬

    선택 정렬 (selection sort) : 가장 작은 원소를 아직 정렬하지 않은 부분의 맨 앞 원소와 교환하여 배열을 정렬하는 알고리즘

![선택 정렬](https://i0.wp.com/studyalgorithms.com/wp-content/uploads/2014/01/selection-sort.jpg?w=432&ssl=1)

- 시간 복잡도는 O(n^2) 이다.

선택 정렬에서 한 패스의 원소 교환 과정은 다음과 같다.

1. 아직 정렬되지 않은 부분에서 가장 작은 원소 min을 선택한다.
2. min과 아직 정렬되지 않은 부분의 맨 앞 원소를 교환한다.

```python
def selection_sort(a: MutableSequence) -> None:
    n = len(a)
    for i in range(n - 1):
        min = i
        for j in range(i + 1, n):
            if a[min] > a[j]:
                min = j
        a[i], a[min] = a[min], a[i]
```

> 이미지 출처 https://studyalgorithms.com/array/selection-sort/
## 삽입 정렬
### 단순 삽입 정렬
    단순 삽입 정렬 (straight insertion sort) : 아직 정렬되지 않은 부분의 맨 앞 원소를 정렬된 부분의 알맞은 위치에 삽입하는 알고리즘

![단순 삽입 정렬](https://www.alphacodingskills.com/python/img/insertion-sort.PNG)

- 두번째 원소부터 주목(focus)하여 앞 부분의 원소와 비교한다.
- focus한 원소를 정렬된 부분의 알맞은 위치에 삽입했을 때, 그 뒤에 원소는 모두 한칸씩 뒤로 이동시킨다.
- 시간 복잡도는 O(n^2) 이다.

```python
def insertion_sort(a: MutableSequence) -> None:
    n = len(a)
    for focus in range(1, n):
        i = focus
        tmp = a[focus]
        while i > 0 and a[i - 1] > tmp:
            a[i] = a[i - 1]
            j -= 1
        a[i] = tmp
```

> 이미지 출처 https://algopoolja.tistory.com/19

### 이진 삽입 정렬