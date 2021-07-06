> 해당 문서는 [Do it! 자료구조와 함께 배우는 알고리즘 입문 : 파이썬 편 (시바타 보요 저)](http://www.yes24.com/Product/Goods/91219874)을 보고 정리한 내용입니다.
- 본 문서에 작성된 코드는 **파이썬 (Python)** 으로 작성하였습니다.
- 책을 보며 공부하면서 도움이 된 파이썬 문법과 개념은 [Python 폴더](https://github.com/dudtjakdl/TIL/blob/main/Python)의 문서에 정리하였습니다.
- 그 외 추가 내용은 인터넷 검색을 통해 공부하고 덧붙여 정리하였습니다.

# 스택
    스택 (stack) : 데이터를 임시 저장할 때 사용하는 자료구조. 데이터의 입력과 출력 순서가 후입선출(LIFO) 방식이다.
    
    * LIFO(Last In First Out) : 가장 나중에 넣은 데이터를 가장 먼저 꺼낸다는 뜻 

![스택](https://media.vlpt.us/images/tiiranocode/post/0c3b8a68-f29c-4836-91ff-2f0ef25dc704/stack.png)

데이터를 넣고 꺼내는 작업을 맨 위부터 수행하며, 푸시한 데이터는 스택 꼭대기에 쌓이고 팝을 하면 방금 푸시한 데이터를 꺼낼 수 있다.

- 푸시 (push) : 스택에 데이터를 넣는 작업
- 팝 (pop) : 스택에서 데이터를 꺼내는 작업
- 꼭대기 (top) : 푸시하고 팝하는 윗부분
- 바닥 (bottom) : 푸시하고 팝하는 아랫부분

> 이미지 출처 https://velog.io/@tiiranocode/%EC%9E%90%EB%A3%8C-%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9Dstack-%ED%81%90queue

# 큐
    큐 (queue) : 데이터를 임시 저장할 때 사용하는 자료구조. 데이터의 입력과 출력 순서가 선입선출(FIFO) 방식이다.
    
    * FIFO(First In First Out) : 가장 먼저 넣은 데이터를 가장 먼저 꺼낸다는 뜻

## 배열 큐
![배열 큐](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrggJc%2FbtqBYup5Umc%2Flwy2BDsqrJt8U4TfwCUyU1%2Fimg.png)

- 인큐 (enqueue) : 큐에 데이터를 추가하는 작업
- 디큐 (dequeue) : 큐에 데이터를 꺼내는 작업
- 프런트 (front) : 데이터를 꺼내는 쪽
- 리어 (rear) : 데이터를 넣는 쪽 

배열 큐는 인큐를 할 때 배열의 맨 끝에 원소를 삽입하면 되므로 복잡도 O(1)인 비교적 적은 비용으로 구현할 수 있다.

하지만 디큐를 할 때는 배열의 맨 앞의 원소를 꺼내고 난 후 2번째 이후의 모든 원소를 앞쪽을 옮겨야 하므로 복잡도 O(n)의 비용이 발생한다. 따라서 비교적 효율성이 떨어진다는 단점이 있다.

## 링 버퍼 큐
![링 버퍼 큐](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbyX7wL%2FbtqBVeW4HDD%2FXMTALPcf1KYjxzSQvDB77K%2Fimg.png)
**링 버퍼(ring buffer)** 는 배열 맨 끝의 원소 뒤에 맨 앞의 원소가 연결되는 자료구조이다. front 와 rear 변수로 어떤 원소가 맨 앞이고, 맨 끝인지 식별할 수 있다. *(front와 rear는 논리적인 데이터 순서일 뿐 배열의 물리적 원소의 순서는 아니다.)*

    - 프런트(front): 맨 앞 원소의 인덱스
    - 리어(rear): 맨 끝 원소 바로 뒤의 인덱스 (다음 인큐되는 데이터가 저장되는 위치)

링 버퍼로 큐를 구현하면 원소를 옮길 필요 없이 front와 rear의 업데이트하면 된다. 따라서 인큐와 디큐 처리의 복잡도가 O(1)이 된다.

> 이미지 출처 https://juyeop.tistory.com/13

### 링 버퍼의 활용
링 버퍼는 오래된 데이터를 버리는 용도로 활용할 수 있다.

예를 들어 크기가 capacity인 배열에 데이터를 계속해서 입력할 때, 오래된 데이터는 새로운 데이터가 덮어써서 가장 나중에 들어온 데이터 capacity개만 저장하는 경우이다. 이를 코드로 구현하면 다음과 같다.

```python
capacity = int(input("링 버퍼의 크기를 입력하세요: "))  # 링 버퍼(배열)의 크기 
a = [None] * capacity   # 입력받은 값을 저장하는 배열

count = 0   # 데이터를 입력받은 개수

while True:
    idx = count % capacity
    a[idx] = int(input(f"{count + 1}번째 정수를 입력하세요.: "))
    count += 1
    
    retry = input("계속 입력을 할까요?(Y: Yes / N: No) ")
    if retry in ['N', 'n']: # N이나 n을 입력하면 데이터 입력 종료
        break
        

i = count - capacity    # i: 가장 오래된(먼저 들어온) 데이터가 저장된 index 값

while True:
    if i >= capacity:
        i -= capacity
    else:
        break
    
if i < 0: i = 0

# 가장 오래된 데이터부터 배열 값 출력 
for _ in range(capacity):
    print(f"a[{i % capacity}] = {a[i % capacity]}")
    i += 1
```

## 덱 (deque)
양방향 대기열인 **덱(deque: double-ended queue)** 은 맨 앞과 맨 끝 양쪽에서 데이터를 넣고 꺼낼 수 있는 자료구조이다.

![덱](https://pythontic.com/deque.jpg)

- 각 양쪽에 2개의 포인터 변수를 사용하여 삭제, 삽입을 할 수 있다.
- 파이썬에서는 collections.deque 내장 컨테이너로 제공된다.
- 큐와 스택을 합친 형태와 비슷하다.

> 이미지 출처 https://pythontic.com/containers/deque/introduction





