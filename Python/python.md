- 분류 없이 나열. 내용이 쌓이면 목차를 나누어 정리할 예정!

## 이터러블 객체
이터러블 객체란 **반복할 수 있는 객체**를 말하며, 파이썬의 대표적인 이터러블 자료형으로는 `list, str, tuple, dic, set` 등이 있다.

## 뮤터블 자료형
`list, dic, set` 등이 있으며, 값을 변경할 수 있다.
```python
>>> a = [1, 2, 3]
>>> id(a)
2166069121864
>>> a[0] = 10
>>> a
[10, 2, 3]
>>> id(a)
2166069121864
```

## 이뮤터블 자료형
`int, float, str, tuple` 등이 있으며 값을 변경할 수 없다.
```python
>>> n = 12; 
>>> id(n)
140721142207648
>>> n += 1
>>> id(n)
140721142207680

# int형 정수형 객체 12의 값 자체를 변경하는 것이 불가능하므로, 다른 정수형 객체 13을 참조하도록 업데이트한다.
```

## range() 함수
range() 함수는 이터러블 객체를 생성한다.
```python
range(n) # 0 이상 n 미만인 수를 차례로 나열하는 수열
range(a, b) # a 이상 b 미만인 수를 차례로 나열하는 수열
range(a, b, step) # a 이상 b 미만인 수를 step 간격으로 나열하는 수열
```

## enumerate() 함수
enumerate() 함수는 인덱스와 원소를 짝지어 튜플로 꺼내는 내장 함수이다.

```python
# 예시
x = ['John', 'George', 'Paul', 'Ringo']

for i, name in enumerate(x): # (0, 'John'), (1, 'George'), ... 
    print(f'x[{i}] = {name}')
```
`enumerate(x, 1)` 처럼 두번째 인자에 숫자를 넣으면 인덱스가 그 숫자부터 시작되어 짝지어진다.


## a와 b의 값을 교환
```python
a, b = b, a # a와 b의 값을 교환 (단일 대입문 사용)

if a > b:
    a, b = b, a # a와 b를 오름차순으로 정렬

# 우변의 b, a는 두값을 압축한 튜플 (b, a)로 생성된다.
```
```python
# 예시
def reverse_array(a: MutableSequence) -> None:
    """뮤터블 시퀀스형 a의 원소를 역순으로 정렬"""
    n = len(a)
    for i in range(n//2):
        a[i], a[n - i - 1] = a[n - i - 1], a[i]
```
## 파이썬 변수와 객체의 특징
파이썬에서는 데이터, 함수, 클래스, 모듈, 패키지 등을 모두 **객체(object)** 로 취급한다. 그래서 파이썬의 변수는 **값을 가지지 않는다**는 특징이 있다. 

즉, 변수에 어떤 값을 대입하면 값이 아니라 **식별 번호(메모리 주소)가 바뀐다.**

* 파이썬 변수는 객체를 참조하는 객체에 연결된 이름에 불과하다.
* 모든 객체는 메모리를 차지하고, 자료형뿐만 아니라 식별 번호(identity)를 가진다.
* 대입식은 값 자체가 아니라 참조하는 객체의 식별 번호(메모리 주소)를 대입한다.

```python
# 예시 1
>>> a = [1, 2, 3, 4, 5]
>>> b = a
>>> a is b
True
>>> a[2] = 9
>>> a
[1, 2, 9, 4, 5]
>>> b
[1, 2, 9, 4, 5]
```
위 예시의 ```b = a``` 대입문을 실행하면 b는 a가 참조하는 곳의 리스트를 참조한다. *즉, 대입에서 복사되는 것은 값이 아니라 참조하는 곳이다.*

따라서 a의 원솟값이 바뀌면 b의 원솟값도 바뀐다.

```python
# 예시 2
>>> a = [1, 2, 3, 4, 5]
>>> b = a[:]
>>> a is b
False
>>> a[2] = 9
>>> a
[1, 2, 9, 4, 5]
>>> b
[1, 2, 3, 4, 5]
```
하지만 대입문이 아닌 ```b = a[:]``` 슬라이싱을 통해 값을 할당하면 결과가 다르다. 

슬라이싱을 통해 값을 할당하면 기존의 a 객체가 아닌 새로운 객체가 생성되어 b에 대입되고, 서로 영향을 받지 않는다.

### 얕은 복사 (shallow copy)
객체가 갖는 멤버의 값을 새로운 객체로 복사할 때 객체가 참조 자료형의 멤버를 포함할 경우 얕은 복사라고 한다. 이는 참조값만 복사하는 방식이다.
```python
>>> x = [[1, 2, 3], [4, 5, 6]]
>>> y = x.copy()    # x를 y로 얕은 복사
>>> x[0] is y[0]    
True                
>>> x[0][1] = 9
>>> x
[[1, 9, 3], [4, 5, 6]]
>>> y
[[1, 9, 3], [4, 5, 6]]
```
```x[0] is y[0]``` 의 결과가 **True** 이므로 리스트 내부의 객체들은 복사되지 않았다. 리스트는 뮤터블 자료형이므로 ```x[0][1] = 9``` 실행시 복사된 y 내부의 객체도 값이 변화한다.

또한, 슬라이싱을 통한 값의 복사도 얕은 복사에 해당한다.
```python
>>> x = [[1, 2, 3], [4, 5, 6]]
>>> y = x[:]    # 슬라이싱을 통한 복사
>>> x[0] is y[0]    
True                
>>> x[0][1] = 9
>>> x
[[1, 9, 3], [4, 5, 6]]
>>> y
[[1, 9, 3], [4, 5, 6]]
```

### 깊은 복사 (deep copy)
참조값 뿐만 아니라 참조하는 객체 자체를 복사할 경우 깊은 복사라 한다. 객체가 갖는 모든 멤버(값과 참조 형식 모두)를 복사하므로 전체 복사라고도 한다.
```python
>>> import copy             # deepcopy를 사용하기 위한 copy 모듈을 임포트
>>> x = [[1, 2, 3], [4, 5, 6]]
>>> y = copy.deepcopy(x)    # x를 y로 깊은 복사
>>> x[0] is y[0]
False
>>> x[0][1] = 9
>>> x
[[1, 9, 3], [4, 5, 6]]      # 대입된 9가 출력됨
>>> y
[[1, 2, 3], [4, 5, 6]]      # y 배열은 영향을 받지 않음
```
```x[0] is y[0]``` 의 결과가 **False** 이므로 리스트 내부의 객체들까지 모두 새롭게 복사된 걸 확인할 수 있다. 
## 함수 어노테이션
파이썬에서는 자료형 선언없이 변수나 함수를 자유롭게 사용할 수 있지만, 명시적으로 해석하기 어려운 경우가 있다. 그래서 등장한 기능이 파이썬 3 이상에서 사용 가능한 *어노테이션(annotation, 주석 달기)* 이다. 함수 어노테이션은 함수의 **매개변수와 반환값의 자료형**을 나타내는 역할을 한다.

```python
# 예시
from typing import Any, Sequence

def max_of(a: Sequence) -> Any:
    """시퀀스형 a 원소의 최댓값을 반환"""
    maximum = a[0]
    for i in range(1, len(a)):
        if maximum > a[i]:
            maximum = a[i]
    return maximum

# Any: 제약이 없는 임의의 자료형을 의미
# Sequence: 시퀀스형을 의미. 리스트, 배열, 문자열, 튜플 등이 있음
```

## call by object reference
파이썬에서 인수 전달은 실제 인수인 객체에 대한 참조를 값으로 전달하여 매개변수에 대입된다. 즉, 함수의 실행 시작 시점에서 매개변수는 실제 인수와 같은 객체를 참조한다. 파이썬 공식 문서에서는 이를 *call by value*와 *call by reference*의 중간적인 방식인 **객체 참조에 의한 전달 (call by object reference)** 라고 설명한다.

실제 함수에서 매개변수의 값을 변경하면 인수의 형(type)에 따라 다음과 같이 구분된다.

    1. 인수가 이뮤터블일 때: 함수 안에서 매개변수의 값을 변경하면 다른 객체를 생성하고 그 객체에 대한 참조로 업데이트 된다. 따라서 매개변수의 값을 변경해도 호출하는 쪽의 실제 인수에는 영향을 주지 않는다.

    2. 인수가 뮤터블일 때: 함수 안에서 매개변수의 값을 변경하면 객체 자체를 업데이트한다. 따라서 매개변수의 값을 변경하면 호출하는 쪽의 실제 인수는 값이 변경된다.

## 모듈
파이썬에서 하나의 스크립트 프로그램을 **모듈(module)** 이라 한다. 확장자(.py)를 포함하지 않는 파일의 이름 자체를 모듈 이름으로 사용한다.

모듈도 객체이다. 모듈은 프로그램이 처음 임포트되는 시점에 그 모듈 객체가 생성되며 초기화 된다.

### __ name __
모듈 객체 __ name __은 모듈 이름을 나타내는 변수이며 작성 규칙은 다음과 같다.
- 스크립트 프로그램이 직접 실행될 때 변수 __ name __은 ' __main __' 이다.
- 스크립트 프로그램이 임포트될 때 변수 __ name __ 은 원래의 모듈 이름이다.

```python
# 예시
if __name__ == "__main__":
    print("스크립트 프로그램을 직접 시행할 때만 출력")

# 스크립트 프로그램을 직접 시행했을 경우 참이 되어 프린트문 출력
# 다른 스크립트 프로그램에서 임포트한 경우에는 거짓이 되므로 if문 실행 X
```

## for - else, while - else
파이썬에서는 반복문(for, while)에 else를 적용할 수 있다. 반복이 모두 끝나 반복문의 실행이 종료되면 else문이 실행되며, 반복문 실행 중간에 break로 나가게 되면 else문이 실행되지 않는다.
```python
# 예시
lst = [1, 2, 3, 4, 5]

for i in lst:
    if i == 0:
        print("리스트 안에 0이 있습니다.")
        break
else:
    print("리스트 안에 0이 없습니다.")

# 실행결과: 리스트 안에 0이 없습니다.
```

## enum

열거형(enumeration)은 서로 관련이 있는 고유한 상숫값의 집합이다. 열거형 자체는 이터레이트(iterate) 될 수 있으며, 상수를 나타내는 데 사용되기 때문에 열거형 멤버의 이름은 **대문자**를 사용하는 것이 좋다.

```python
from enum import Enum   # enum 내장 모듈 불러오기

class Color(Enum):      # Enum 클래스 확장을 통한 Color 열거형 타입 생성 
    RED = 1
    BLUE = 2
    GREEN = 3 
```

enum 타입의 상수 인스턴스는 ```name``` 과 ```value``` 속성을 가진다.

```python
>>> Color.RED.name
'RED'
>>> Color.RED.value
1
```

enum 타입은 이터러블 객체이므로 ```for```문을 통한 순회가 가능하다.

```python
>>> for color in Color:
        print(color)

Color.RED
Color.BLUE
Color.GREEN
```

또한 일반 함수 호출을 통해 enum 타입을 정의할 수도 있다.

```python
>>> Color1 = Enum("Color1", "RED BLUE GREEN")
>>> list(Color1)
[<Color1.RED: 1>, <Color1.BLUE: 2>, <Color1.GREEN: 3>]

>>> Color2 = Enum("Color2", ['WHITE', 'BLACK', 'BROWN'])
>>> list(Color2)
[<Color2.WHITE: 1>, <Color2.BLACK: 2>, <Color2.BROWN: 3>]
```
> 참고 https://python.flowdas.com/library/enum.html

> 참고 https://www.daleseo.com/python-enum/

## 예외 처리
파이썬에서는 프로그램을 실행하다가 오류(error)가 발생하면 예외 처리(Exception) 메시지를 내보낼 수 있다. 

예외 처리를 적절히 수행하면 프로그램이 중간에 중단되는 것을 막을 수 있어 사용성과 완성도가 높은 프로그램을 짤 수 있다.

### try - except - finally
파이썬 예외 처리의 기본 구조는 다음과 같다. 

```python
try:
    실행 명령문 1
    실행 명령문 2
except 에러 종류 1:
    예외 처리 명령문 1
    예외 처리 명령문 2
except 에러 종류 2:
    예외 처리 명령문 1
    예외 처리 명령문 2
finally: # 에러 발생과 상관없이 항상 try문 다음에 실행
    실행 명령문 1
    실행 명령문 2
```
finally 구문은 보통 열린 파일을 닫거나 자원을 해제하는 작업을 수행한다.

except문 뒤에 **as err** 을 추가하면 err 변수(기본 에러 메시지)를 사용할 수 있다.

```python
except ZeroDivisionError as err:
    print(err)

# 예외 발생 시 실행 결과: division by zero
```

모든 에러에 대한 예외 처리를 전부 할 수 없을 경우, 에러 종류에 **Exception**을 쓰면 지금까지 정의되지 않은 모든 에러에 대한 예외 처리가 가능하다.

```python
except Exception as err:
    print("알 수 없는 에러가 발생하였습니다.")
    print(err)
```
> 참고 https://nadocoding.tistory.com/72?category=902275

### raise
raise문으로 프로그램의 예외 처리를 의도적으로 내보낼 수 있다.

사용 방법은 ```raise 에러 종류```와 같이 입력하며 다음 예시처럼 사용할 수 있다.

```python
try:
    print("한자리 숫자만 입력하세요.")
    num = int(input("숫자 입력: "))
    if num >= 10:
        raise ValueError:
    print(num)
except ValueError:
    print("잘못된 값을 입력하였습니다.")
```
### 사용자 정의 예외 처리
ValueError, ZeroDivisionError 등 파이썬이 제공하는 예외 처리를 표준 내장 예외처리라고 한다. 기본으로 제공되는 예외 처리 말고도 사용자가 직접 정의하여 예외 처리를 발생시킬 수 있다.

사용자 정의 예외 처리는 **Exception 클래스(또는 그 파생 클래스)** 에서 파생하는 것이 원칙이다. 즉, Exception 클래스의 하위 클래스로 정의하여 사용해야 한다.

```python
class FullError(Exception):
    pass

try:
    lst = [None] * 5
    i = 0
    while True:
        if i >= len(lst):
            raise FullError
        lst[i] = i
        i += 1
except FullError:
    print("리스트가 꽉 찼습니다.")

```