> 해당 문서는 [Do it! 자료구조와 함께 배우는 알고리즘 입문 : 파이썬 편 (시바타 보요 저)](http://www.yes24.com/Product/Goods/91219874)을 보고 정리한 내용입니다.
- 본 문서에 작성된 코드는 **파이썬 (Python)** 으로 작성하였습니다.
- 책을 보며 공부하면서 도움이 된 파이썬 문법과 개념은 [Python 폴더](https://github.com/dudtjakdl/TIL/blob/main/Python)의 문서에 정리하였습니다.
- 그 외 추가 내용은 인터넷 검색을 통해 공부하고 덧붙여 정리하였습니다.

# 재귀
    재귀 (recursion) : 어떠한 것을 정의할 때 자기 자신을 포함하고 다시 자기 자신을 사용(참조)하는 것.

![재귀 개념 예시](https://upload.wikimedia.org/wikipedia/commons/b/b3/Screenshot_Recursion_via_vlc.png)

위 그림은 화면 가운데에 계속해서 같은 화면이 반복해서 나타나는 재귀 개념을 표현한 예시이다.

![재귀 호출](https://cdn.programiz.com/sites/tutorial2program/files/cpp-function-recursion-working.png)

그리고 재귀 개념을 프로그래밍에 적용 했을 때, 어떤 함수가 자기 자신과 똑같은 함수를 다시 호출하는 것을 **재귀 호출(recursive call)** 이라 한다.

> 이미지 출처 https://ko.wikipedia.org/wiki/%EC%9E%AC%EA%B7%80_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)

> 이미지 출처 https://www.programiz.com/cpp-programming/recursion

## 팩토리얼
재귀를 사용하는 대표적인 알고리즘의 예로 팩토리얼(factorial)이 있다.

양의 정수 n의 패토리얼(n!)의 재귀적 정의는 다음과 같다.

    n!의 정의 (n은 양의 정수)
     - 0! = 1
     - n > 0이면 n! = n * (n-1)!

위 정의를 factorial() 함수로 구현하면 다음과 같다.

```python
def factorial(n: int) -> int:
    if n > 0:
        return n * fatorial(n - 1)
    else:
        return 1
```
하지만 재귀를 이용한 팩토리얼 함수는 재귀의 원리를 이해하기 위한 가장 간단한 예제일 뿐, 실제로는 재귀 함수로 구현하지 않는 것이 더 효율적이다.

* 파이썬은 math 모듈이 factorial() 함수를 제공한다. ```math.factorial(x)``` 를 입력하면 정수 x의 팩토리얼값을 반환한다.

## 유클리드 호제법

유클리드 호제법(유클리드 알고리즘)은 2개의 정수의 최대공약수를 구하는 알고리즘이다.

![유클리드 호제법](https://lh3.googleusercontent.com/pw/ACtC-3cVc-M8kNP4u5wvNilsNzdLbG6gltJviX3jeAm9RUHc6njlqLntO7VzX4hUnGtqsdOpePbE4yhiKjWhyrv5rSh1sWnF5b_YrnNDceSxsYjFYQXFhxbjYkxc8uj8_csTS3LtsMeXXbst6VC2M9d0mmpY=w487-h338-no?authuser=0)

위 그림과 같이 두 수를 각각의 변으로 하는 직사각형 안을 정사각형 여러 개로 계속 쪼개는 과정을 반복할 때, 만들 수 있는 정사각형 가운데 가장 작은 정사각형의 변은 처음 직사각형의 가로 세로 변의 최대 공약수(GCD)와 같다.

이러한 과정을 공식화하면 다음과 같다.

     두 정수 x와 y의 최대 공약수를 gcd(x, y)로 표기할 때,
     - y가 0이면 gcd(x, y) = x
     - y가 0이 아니면 gcd(x, y) = gcd(y, x % y)

위 공식을 이용하여 유클리드 알고리즘을 재귀적으로 구현하면 다음과 같다.

```python
def gcd(x: int, y: int) -> int:
    if y == 0:
        return x
    else:
        return gcd(y, x % y)
```
* 파이썬은 math 모듈이 gcd() 함수를 제공한다. ```math.gcd(x, y)``` 를 입력하면 x와 y의 최대공약수를 반환한다.

## 하노이의 탑

하노이의 탑(tower of hanoi)은 큰 원반은 아래에, 작은 원반은 위에 위치하는 규칙을 지키며 기둥 3개를 이용하여 원반 n개를 옮기는 문제이다.

기둥 A에 원반 3개가 있을 때, 하노이의 탑 규칙을 적용하여 기둥 C로 옮기는 과정은 다음 그림과 같다.

![하노이의 탑](https://media.geeksforgeeks.org/wp-content/uploads/tower-of-hanoi.png)

이와 같이 원반을 최소 횟수로 옮기는 알고리즘을 하노이의 탑 알고리즘이라 한다.

하노이의 탑 알고리즘은 재귀 개념을 적용하여 설명할 수 있다.

![하노이의 탑 재귀](https://miro.medium.com/max/875/1*eR2gxp8mKeaEWbbj4-cLMQ.png)

위 그림과 같이 출발 기둥에 n개의 원반이 있을 때, 원반 n개를 목적지 기둥에 옮기는 과정은 다음과 같다.

    1. 출발 기둥의 원반 n - 1 개를 중간 기둥으로 옮긴다.
    2. 출발 기둥의 제일 밑바닥에 있는 원반을 목적지 기둥으로 옮긴다.
    3. 중간 기둥의 원반 n - 1 개를 목적지 기둥으로 옮긴다.

이때 1번과 3번 과정에서 n -1 개의 원반을 옮기는 과정은 재귀적으로 동작한다.

위 과정을 참고하여 하노이의 탑을 구현하는 프로그램은 다음과 같다.

```python
def tower_of_hanoi(n: int, a: int, b: int) -> None:
    """원반 n개를 a기둥에서 b기둥으로 옮기는 함수"""
    if n > 1:
        tower_of_hanoi(n - 1, a, 6 - a - b)
    print(f"원반[{n}]을 기둥 {a} -> 기둥 {b}")
    if n > 1:
        tower_of_hanoi(n - 1, 6 - a - b, b)

# 6 - a - b 는 a와 b 기둥을 뺀 나머지 보조 기둥의 번호를 구하기 위한 식이다.
```

> 이미지 출처 https://www.geeksforgeeks.org/c-program-for-tower-of-hanoi/

> 이미지 출처  https://medium.com/@jamalmaria111/tower-of-hanoi-js-algorithm-3f667fa46f0f

## 8퀸 문제

재귀 알고리즘을 적용할 수 있는 또 다른 예제로 8퀸 문제(8-Queen problem)이 있다. 

8퀸 문제는 **8개의 퀸이 서로 잡을 수 없도록 8 x 8 체스판에 가로, 세로, 대각선이 중복되지 않도록 배치**하는 문제이다.

![8_queen](https://miro.medium.com/max/1000/1*Zm2pbDR5CS2w2xeUbTBxQQ.png)

위 그림은 8퀸 문제의 해결 방법 중에 하나이다. 이렇게 총 해결 방법은 92가지가 있다.

그런데 8퀸 문제는 재귀 개념을 이용하여 해를 탐색할 수 있다.

![8_queen_recursion](https://i.ibb.co/9Y4SVPJ/algorithm-n-queens-problems3.png)

위 그림과 같이 퀸이 (0, 0)에 놓였을 때 분기가 나뉘고, 또 다음 행에 퀸이 놓였을 때 분기가 계속 나뉜다. 이런 과정을 반복하여 재귀적으로 경우의 수를 나누면 8퀸 문제의 조건을 만족하는 모든 해를 찾을 수 있다.

8 x 8 체스판을 2차 배열로 정의하고 퀸이 놓이지 않았으면 값이 0, 퀸이 놓였으면 값이 1이라고 가정했을 때, 위 재귀 개념을 참고하여 8퀸 문제의 해를 구하는 프로그램을 구현하였다.


 
```python
chess = [[0] * 8] * 8           # 8 x 8 체스판 행렬 0으로 초기화
col_chk = [False] * 8           # 각 열에 퀸을 배치했는지 체크
right_diag_chk = [False] * 15   # 대각선 방향(↙↗)으로 퀸을 배치했는지 체크
left_diag_chk = [False] * 15    # 대각선 방향( ↘↖)으로 퀸을 배치했는지 체크

def chess_print() -> None:
    """퀸을 놓은 체스판을 □와 ■로 출력"""
    for i in range(8):
        for j in range(8):
            print('■' if chess[i][j] else '□', end='')
        print()
    print()

def queen(row: int) -> None:
    for col in range(8):
        if (not col_chk[col] and not right_diag_chk[row + col] and not left_diag_chk[col - row + 7]):
            """열과 대각선에 퀸이 배치 되지 않았을 시"""
            chess[row] = [0] * 8    # 행에 퀸이 중복되지 않도록 행 초기화
            chess[row][col] = 1     # 퀸을 row 행 col 열에 놓기
            if row == 7:            # 퀸을 마지막 행까지 다 놓았을 시 출력
                chess_print()
            else:
                col_chk[col] = right_diag_chk[row + col] = left_diag_chk[col - row + 7] = True
                queen(row + 1)        # 다음 행에 퀸 놓기
                col_chk[col] = right_diag_chk[row + col] = left_diag_chk[col - row + 7] = False

if __name__ == '__main__':
    queen(0)
```

> 이미지 출처 https://medium.com/@paabrown/solving-the-n-queens-problem-6891e3d21b0

> 이미지 출처 http://dawoonjeong.com/algorithm-backtracking/