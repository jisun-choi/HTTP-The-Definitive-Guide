## Connection

### TCP connection

**TCP/IP**: 패킷 교환 네트워크 프로토콜들의 집합으로 일단 커넥션이 맺어지면 네트워크를 통해 주고받는 메세지들은 손실, 손상, 순서 뒤바뀜 없이 안전하게 전달될 것이 보장됨 <br>
`http://www.joes-hardware.com:80/power-tools.html`

- 브라우저가 호스트 명(www.joes-hardware.com) 을 추출
- 브라우저가 해당 호스트에 대한 IP 주소를 얻음
- 브라우저가 포트번호를 얻음
- 브라우저가 IP 주소의 80 포트로 TCP 커넥션을 생성
- 브라우저-> 서버 GET 요청 보냄
- 서버에서 온 응답 메세지 받음
- 커넥션 종료시킴

1.  TCP 는 바이트들을 순서에 맞게 정확히 전달한다.
2.  TCP 는 데이터 스트림을 segment 단위로 나눠서 IP 패킷이라는 봉투에 담아 데이터를 전달한다. <br>

**IP packet** <br>

- IP header (20bytes)
- TCP header (20bytes)
- TCP data

![](https://images.velog.io/images/wltjs10645/post/edf82f6f-a941-4cae-8d67-66f9de3bbe9b/image.png)

3.  TCP 커넥션 유지
    port # 를 통해 여러 개의 커넥션을 유지한다. <br>
    TCP 커넥션을 식별하는 4가지 값 (유일한 커넥션): <br>
    <발신지 IP주소, 발신지 포트, 수신지 IP주소, 수신지 포트><br>
    예를 들어, 서로 다른 두개의 TCP 커넥션은 4가지 주소 구성값이 전부 같을 수는 없다. (일부는 가능)
4.  TCP 소켓 프로그래밍 p.90
