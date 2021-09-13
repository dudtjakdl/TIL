> 해당 문서는 [모든 개발자를 위한 HTTP 웹 기본 지식 (김영한 강사)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)을 보고 복습한 내용을 정리했습니다.

# HTTP

- HTTP (HyperText Transfer Protocol)
  - html, text, 이미지, 음성, 영상, 파일, json, xml 등 거의 모든 형태의 데이터 전송 가능
  - 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
  - 클라이언트 서버 구조
  - 무상태 프로토콜 (Stateless)
  - 비연결성
  - 단순함, 확장 가능
- 역사
  - HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전, 기반 프로토콜은 TCP
  - HTTP/2 2015년: 성능 개선, 기반 프로토콜은 TCP
  - HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선

# 클라이언트 서버 구조

- Request(요청) Response(응답) 구조
- 클라이언트는 서버에 요청을 보냄
- 서버는 요청에 대한 결과를 만들어서 클라이언트에 응답을 보냄

# Stateful vs Stateless

## 상태유지 프로토콜 (Stateful)

![상태유지](https://backtony.github.io/assets/img/post/http/2-2.PNG)

- 서버가 클라이언트의 상태를 보존함
- 장점 : 클라이언트의 데이터 전송량이 적음
- 단점 : 항상 같은 서버가 유지되어야 함 (서버 장애에 대처 불가능)
- 브라우저 쿠키와 서버 세션등을 이용해 로그인 기능과 같은 상태 유지가 필요한 경우에 사용
- 상태 유지는 최소한만 사용

## 무상태 프로토콜 (Stateless)

![무상태](https://backtony.github.io/assets/img/post/http/2-3.PNG)

- 서버가 클라이언트의 상태를 보존하지 않음
- 장점 : 서버 확장성이 높음 (스케일 아웃 - 수평 확장 유리)
- 단점 : 클라이언트의 데이터 전송량이 많음
- 로그인이 필요 없는 단순한 서비스 소개 화면에 사용

# 비연결성

- HTTP는 기본적으로 연결을 유지하지 않는 모델임
- 초 단위 이하의 빠른 속도로 응답 가능
- 서버 자원 효율적으로 사용 가능
- 요청이 발생할 때마다 TCP/IP 연결을 새로 맺어야 함 - 3 way handshake 시간 추가
- 요청이 발생할 때마다 자바스크립트, css, 이미지 등 자원이 다운로드 됨 - 현재는 HTTP 지속 연결(Persistent Connections)로 문제 해결

# HTTP 메시지

![HTTP 메시지](https://backtony.github.io/assets/img/post/http/2-4.PNG)

```
start-line
*( header-field CRLF )
CRLF
[ message-body ]
```

## HTTP 요청 메시지

```
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com

```

- stat-line = request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)
  - HTTP 메서드 (GET, POST, PUT, DELETE 등등)
  - 요청 대상 (절대경로[?쿼리])
  - HTTP 버전 (HTTP/1.1)
- header-field = field-name ":" OWS field-value OWS (OWS: 띄어쓰기 허용)
  - HTTP 전송에 필요한 모든 부가정보
- message-body
  - 실제 전송할 데이터 (HTML 문서, 이미지, 영상, JSON 등등)
  - 위 예시에는 없음 (요청 메시지도 body 본문을 가질 수 있음)

## HTTP 응답 메시지

```
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
 <body>...</body>
</html>
```

- start-line = status-line = HTTP-version SP status-code SP reason-phrase CRLF
  - HTTP 버전 (HTTP/1.1)
  - HTTP 상태 코드
    - 200: 성공
    - 400: 클라이언트 요청 오류
    - 500: 서버 내부 오류
  - 이유 문구 (이해하기 쉽게 OK와 같이 작성)
- header-field = field-name ":" OWS field-value OWS (OWS: 띄어쓰기 허용)
  - HTTP 전송에 필요한 모든 부가정보
- message-body
  - 실제 전송할 데이터 (HTML 문서, 이미지, 영상, JSON 등등)
