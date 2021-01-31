## Conenction header

- HTTP 는 클라이언트 & 서버 사이에 프락시, 캐시 서버와 같이 중개 서버가 놓이는 것을 허용하는데 커넥션 관리를 위해 Http connection header 를 사용한다.
- 다시 말해, 커넥션 헤더에는 특정 커넥션에만 해당하는 옵션 지정이 가능하다.
- 커넥션 관리를 제대로 하지 않으면 TCP 성능 저하의 주요 원인이 된다. <br>
  (e.g. 순차적인 트랜젝션 처리로 인한 지연 이슈) <br>
  **http 커넥션의 성능 향상을 위한 기술들** <br>
  - parallel connection: 여러 개의 TCP 커넥션으로 동시 HTTP 요청
  - persistent connection: 커넥션의 맺고 끊음으로 인한 지연을 방지하기 위해 TCP 커넥션을 재활용
  - pipelined connection: 공유 TCP 커넥션을 통해 병렬 HTTP 요청
  - multiplexed connection: request & response 를 중재

### 병렬 커넥션

![](https://images.velog.io/images/wltjs10645/post/7ab7ac5e-bcbc-498c-82ed-4b5ef56199ad/image.png)

- 병렬 커넥션은 페이지를 더 빠르게 내려 받는다.
  : HTML 페이지를 먼저 내려받고 남은 세개의 트랜잭션의 각각 별도의 커넥션에서 병렬로 처리됨
- 병렬 커넥션이 항상 더 빠른 것은 아니다.
  : 클라이언트 네트워크의 대역폭이 좁을 때; 또한 과도한 커넥션은 메모리 소모가 심하고 자체적인 성능 문제를 발생 시킴. 따라서 브라우저는 적은 수의 (대부분 4개) 병렬 커넥션을 이용하고 서버는 특정 클라이언트가 과도한 커넥션을 맺을 경우 임의로 끊을 수 있다.

#### 병렬 커넥션의 한계

- 각 트랜잭션마다 새로운 커넥션을 맺고 끊기 때문에 시간, 대역폭 소요됨
- 각 새로운 커넥션은 TCP slow start 로 인해 성능 저하
- 실제 연결 가능한 병렬 커넥션의 수는 제한 됨

### 지속 커넥션

보통 한 웹페이지에 대한 데이터를 가져오기 위해 동일 서버에 여러 번 HTTP 요청을 보내게 된다. 이 속성을 site locality 라고 부름. 클라이언트나 서버가 커넥션을 끊기 전까지 트랜잭션 간에도 커넥션을 유지하는 것을 지속하는 것이 지속 커넥션인데 이미 맺어진 커넥션을 재사용하여 커넥션에 필요한 pre-work 시간을 절약할 수 있다.

#### 지속 커넥션의 장점

- 커넥션을 위한 사전 작업과 지연을 줄여줌
- 튜닝된 커넥션 유지 & 커넥션 수를 줄여줌

하지만 지속 커넥션 관리를 잘못할 경우 계속 연결된 상태로 수많은 커넥션이 쌓여 로컬의 리소스 뿐만 아니라 원격 클라이언트, 서버의 리소스를 불필요하게 소모하게 됨.

#### 따라서, 병렬 커넥션과 지속 커넥션을 함께 쓰는 것이 효과적임

#### HTTP/1.0+: Keep-Alive 커넥션

- 클라이언트가 요청에 `Connection: Keep-Alive` 헤더를 포함시켜 보내면 서버는 같은 헤더를 포함시켜 응답을 보낸다. 응답 헤더에 keep-alive 가 없으면 keep-alive 를 지원하지 않는 서버이며 응답 메세지 전송 후 커넥션을 끊을 것이라고 추정

```
#서버가 5개의 추가 트랜잭션을 처리될 동안 커넥션 유지 or 2분 동안 커넥션 유지
Connection: Keep-Alive
Keep-Alive: max=5, timeout=120
```

- dumb-proxy & proxy-connection (다시 공부 필요..)

#### HTTP/1.1: 지속 커넥션

- HTTP/1.1 에서는 별도 설정을 하지 않으면 모든 커넥션을 지속 커넥션으로 인식, 띠라서 트랜잭션 후 다음 커넥션을 끊으려면 Connection:close 헤더를 명시해야 함

### 커넥션 끊기

커넥션은 에러가 아니더라도 언제든 끊어질 수 있다. HTTP application은 커넥션이 끊어질 때에 적절히 대응할 수 있어야함! <br>
**idempotent (멱등성)**: 트랜잭션이 몇 번 실행됐는 지와 관계없이 동일한 결과를 반환한다. (e.g. GET, OPTIONS etc) <br>
POST 같이 멱등하지 않은 요청은 파이프 라인을 통해 요청하면 안되고 요청을 다시 보내야 한다면 이전 요청에 대한 응답을 받을 때까지 기다려야함. 그렇지 않으면 요청이 꼬여서 알 수 없는 결과를 초래할 수 있음.

### TCP 커넥션은 양방향이다.

커넥션의 양쪽에는 데이터 입출력을 위한 큐가 있다.

- 서버 전체끊기
- 서버 출력 절반 끊기
- 서버 입력 절반 끊기
  ![](https://images.velog.io/images/wltjs10645/post/c0345317-8dc1-4923-a013-bba937532e96/image.png)