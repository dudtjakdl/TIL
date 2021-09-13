> 해당 문서는 [모든 개발자를 위한 HTTP 웹 기본 지식 (김영한 강사)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)을 보고 복습한 내용을 정리했습니다.

# URI

    "URI는 로케이터(locator), 이름(name) 또는 둘다 추가로 분류될 수 있다"

![URI](https://media.vlpt.us/images/kimdukbae/post/f613cb08-de69-4cbb-b410-cc0a1a574f2c/image.png)

- URI (Uniform Resource Identifier)
  - Uniform : 리소스 식별하는 통일된 방식
  - Resource : 자원, URI로 식별할 수 있는 모든 것
  - Identifier : 다른 항목과 구분하는데 필요한 정보
- URL : Uniform Resource Locator
- URN : Uniform Resource Name

## URL과 URN

    URL 예시: foo://example.com:8042/over/there?name=ferret#nose
    URN 예시: urn:example:animal:ferret:nose

- URL - Locator: 리소스가 있는 위치를 지정

- URN - Name: 리소스에 이름을 부여

위치(Locator)는 별할 수 있지만, 이름(Name)은 변하지 않는다. URN 이름만으로 실제 리소스를 찾을 수 있는 방법은 보편화 되지 않았다.

# URL

    구조 scheme://[userinfo@]host[:port][/path][?query][#fragment]

    예시 https://www.google.com:443/search?q=hello&hl=ko

- scheme
  - 주로 프로토콜 사용 (http, https, ftp 등등)
- userinfo
  - URL에 사용자정보를 포함해서 인증
  - 거의 사용하지 않음
- host
  - 호스트명 (www.google.com)
  - 도메인명 또는 IP 주소를 직접 사용가능
- port
  - 포트 번호 (443)
  - 일반적으로 생략
  - http는 80, https는 443
- path
  - 리소스 경로(/search)
  - 계층적 구조
- query
  - 쿼리 파라미터 (q=hello&hl=ko)
  - key=value 형태
  - ?로 시작, &로 추가 가능
- fragment
  - html 내부 북마크 등에 사용
  - 서버에 전송하는 정보 아님

# 웹 브라우저 요청 흐름

    웹 브라우저가 구글 서버에 https://www.google.com/search?q=hello&hl=ko 에 해당하는 요청을 보냈을 경우를 가정

1. DNS 조회 -> IP 주소 검색
2. HTTP 요청 메시지 생성
3. 패킷 생성 (패킷 안에 전송 데이터인 HTTP 메시지 포함)
4. 요청 패킷 전달
5. 요청 패킷 도착
6. HTTP 응답 메시지 생성
7. 응답 패킷 전달
8. 응답 패킷 도착
9. 웹 프라우저 HTML 렌더링
