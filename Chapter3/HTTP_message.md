## 메세지의 흐름

- 메세지가 서버로 이동하는 것을 인바운드라고 하며 모든 처리가 끝난 후 아웃바운드로 다시 클라이언트로 복귀한다.
- 모든 메세지는 다운스트림으로 흐른다. 메세지의 발송자는 수신자의 업스트림!
  ![](https://images.velog.io/images/wltjs10645/post/5a76b437-7caf-46b3-8d0f-c41ea8dff811/image.png)

## 메세지의 구성

HTTP 메세지 = 데이터의 구조화 된 블록 <br>

- 시작줄: 어떤 메세지인 지 서술
- 헤더: 메세지의 속성
- 본문: 데이터를 담고 있고 없을 수도 있음
- 시작줄 & 헤더는 단순 아스키 문자열이고 본문은 문자열 or 이진데이터 or null

![](https://images.velog.io/images/wltjs10645/post/1c39f71d-b2f3-47f8-b237-733471adc19d/image.png)

## Request & Response message format

- HTTP/1.1 에서 버전을 비교할 때는 1 & 1로 해석해야 한다. 예를 들어 HTTP/2.22 는 HTTP/2.3 보다 크다. 22>3 이기 때문에.

Request message format

```
<method><request URL><version> --request line
<header>
---CRLF(줄바꿈문자열)---
<contents>
```

Response message format

```
<version><status code><reason-phrase> --response line
<header>
---CRLF(줄바꿈문자열)---
<contents>
```

## Header

궁금하면 p.76로 🤗~
