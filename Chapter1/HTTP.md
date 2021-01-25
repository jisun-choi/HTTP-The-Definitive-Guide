## Web Client & Server

![](https://images.velog.io/images/wltjs10645/post/c339a636-233b-4ba8-b7c8-b81a2de802fd/image.png)

## Resources

- 정적 파일: 텍스트, html, ms docs, jpeg, avi etc
- 동적 리소스: 사용자가 누구인지, 어떤 정보를 요청하는 지등에 따라 다른 콘텐츠를 생성할 수 있음.
  (e.g. 주식거래 gateway, 전자상거래 gateway etc)

### MIME

- Multipurpose Internet Mail Extensions:
  원래 메일을 주고 받을 때 이용하기 위한 포맷이었으나 유용성이 입증되어 HTTP 통신에도 채택됨
- 웹 서버는 모든 HTTP 객체 데이터에 MIME 타입을 붙이고 브라우저는 MIME 타입을 통해 다룰 수 있는 객체인 지 확인

```
# 여기서 image 는 MIME 타입에 해당
content-type: image/jpeg
content-length: 12984
```

### URI

- Uniform Resource Identifier:
  인터넷의 우편물 주소같은 것으로 정보 리소스를 고유하게 식별하고 위치를 지정할 수 있다.
  - URL(Uniform resource locator): 특정 서버에서 하나의 자원에 대한 구체적인 위치를 서술
  - URN(Uniform resource name): 하나의 자원에 대해 위치에 영향 받지 않는 유일한 이름

## Transaction

- request & response
  ![](https://images.velog.io/images/wltjs10645/post/aa6e10f1-0eef-4ed6-abc0-25423b1efb92/image.png)

### Method

- 모든 HTTP 요청 메시지는 하나의 메소드를 가진다.(action을 정의: GET, PUT, POST ...)

### Status Code

- 모든 HTTP 응답 메시지는 상태 코드와 함께 반환 (e.g. 200. 404 ...)

### 웹페이지는 여러 객체로 이루어진 리소스의 모음

## Message

- 시작줄
- 헤더
- 본문

## TCP Connection

- Transmission Control Protocol

### TCP/IP

- 패킷 교환 네트워크 프로토콜의 집합으로 어떤 종류의 컴퓨터나 네트워크든 신뢰성 있는 의사소통을 가능하게 함
  = 오류 없는 데이터 전송 & 순서에 맞는 전달 & 조각나지 않는 데이터 스트림을 보장
  ![](https://images.velog.io/images/wltjs10645/post/ab0b0958-76b3-48e3-b599-c43295d8938a/image.png)

### IP address & Port number

클라이언트가 서버와 통신하려면 그 전에 IP 주소와 포트번호를 통해 client <-> server 사이에 TCP/IP 커넥션을 맺는다.

#### 웹브라우저가 HTTP 통신을 통해 리소스를 보여주는 원리

1. 브라우저가 서버의 URL 에서 host 명을 추출
2. 서버의 host 명을 IP 로 변환
3. URL 에서 포트번호를 추출
4. 웹서버와 TCP 커넥션을 맺음
5. 브라우저->서버 HTTP 요청을 보냄
6. 서버->브라우저 HTTP 응답을 돌려줌
7. 커넥션이 닫히고 브라우저는 문서를 보여줌
