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