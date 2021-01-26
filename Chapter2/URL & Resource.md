## URL & Resources

### URL (Uniform Resource Locator)

- 절대 URL<br>
  `http://joes-warehouse.com/tools.html`
- 상대 URL: tools.html 안의 HTML tag <br>
  `<a href="./hammaers.html">`<br>
  : 새로운 절대 경로는 `http://joes-warehouse.com/hammers.html` 가 되는 것
- 인터넷의 리소스를 가리키는 표준 이름으로 전자 정보의 장소, 접근 방식을 알려줌
- '스킴://서버위치/경로'

![](https://images.velog.io/images/wltjs10645/post/ad7b017d-3b49-4c8c-9971-06f74a553adf/image.png)

- **scheme**: 웹 클라이언트가 리소스에 어떻게 접근하는지 알려줌. (e.g. HTTP, FTP, SMTP)
- **host**: 서버의 위치.리소스가 어디에 호스팅 되어 있는 지 알 수 있음.
- **route**: 리소스의 경로.

### Scheme

| 스킴  | 내용                                                                                                                                                             |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| http  | 사용자 이름이나 비번을 제외한 일반 URL 포맷을 준수하는 Hypertext Transfer Protocol<br>http://<호스트>:<포트>/<경로>?<쿼리트스트링>#<프래그먼트><br>기본 포트: 80 |
| https | HTTP 커넥션 양 끝에서 암호화를 위해 보안 소켓 계층(Secure Sockets Layer, SSL)을 사용<br>기본 포트: 443                                                           |

더 많은 종류의 스킴은 p.44 참조!

### URN (Uniform Resource Name)

URL 의 단점은 리소스가 옮겨지면 더는 url 을 이용할 수 없다는 것이다. 그리고 url을 통해 접근할 수 있던 객체에 접근이 불가능해진다. <br>
이런 단점을 보완하기 위해 URN 이 등장했다. 리소스의 위치와 상관없이 그 객체 자체를 가리키는 이름을 사용하여 객체에 접근한다.
