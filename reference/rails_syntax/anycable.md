### anycable
- web socket 을 위한 action cable
- action cable 은 사용하기에 편리하고 개발이 빠르나 다른 web socket 서버들에 비해 속도가 느림
참고:https://evilmartians.com/chronicles/anycable-actioncable-on-steroids

- 그래서 anycable 등장
- rails의 action cable과 같은 프로토콜을 사용하기 때문에 client에는 이에 관한 소스 코드를 수정, 추가할 필요 없음
- anycable 의 구조
![image](https://user-images.githubusercontent.com/48708746/126638910-683bd9c1-4516-4019-8752-05c43bd4cbc6.png)


### 웹소켓
- html5의 표준 기술
- 하나의 tcp 접속에 전 이중 통신 채널을 제공하는 컴퓨터 통신 프로토콜
- 브라우저와 서버사이의 동적인 양방향 연결채널 구성


#### 특징
- gmail 처럼 실시간 특성 중시하는 웹앱에 사용하면 좋음
- 웹소켓 이용시 http 접속으로 양방향 메시지를 주고받을 수 있음
- 서버와 클라이언트가 특정 port 통해 연결 성립하고 있음
- 서버와 클라이언트가 연결을 계속 유지
- 서버와 클라이언트 양쪽에 소켓이 있고 두 소켓이 연결되면 서로 다른 프로세스끼리 데이터 전달 가능


#### 서버소켓
- 서버소켓은 클라이언트로부터 요청이 오기를 기다렸다 연결 요청이 들어오면 클라이언트와 연결을 맺고 다른 소켓 만듦

#### 클라이언트소켓
- 클라이언트 소켓은 기다릴 필요 없음. 
- 바로 소켓 생성
- 서버에 연결 요청, 데이터 전송


#### tcp 소켓과의 차이점
- 최초의 접속이 http 리퀘스트를 통해 handshaking 과정 이루어진다는 것
- http request 이용해 80, 443 포트 이용가능


### RPC
- 네트워크로부터 떨어져있는 컴퓨터에서 코드 실행하는 방식 ( remote procedure call )
- 코드를 메인코드와 작업코드로 독립시킬 수 있음
- 네트워크 연결하는 부분, 코드를 실행하는 부분 등 세부적으로 나눌 수 있음
- 따라서 rcp 를 이용한 네트워크 프로그램은 실행인자, 실행할 코드를 명확하게 해야함

##### rpc 사용 이유
- 분산 네트워크 환경에서 프로그래밍 쉽게 하기 위해
- 클라이언트, 서버간 커뮤니케이션에 필요한 정보는 감추고 일반 메소드 호출하는 것 처럼 호출


### redis
- key, value 기반의 오픈소스 인메모리 데이터 저장소
- 모든 데이터를 메모리에 저장하기 때문에 속도 빠름
- 인메모리이면서 데이터 영속성 보장
- db로 사용되기도 하고 cache나 message broker로도 사용
- 문자열, array, set, 정렬된 set 등의 데이터 형식 지원

#### pub / sub
- redies 에서는 message를 subscribe, publish 하는 기능도 제공됨
- 메시지를 받는 client와 server 는 channel 만 subscribe 하고 publish 함
- 따라서 client 입장에서는 channel 뒤에 어떤 server가 있는 지 신경쓸 필요 없이 channel 만 subscribe 하면 됨
- server 역시 어떤 subscriber가 있는지 신경 쓸 필요 없이 channel에 메시지를 publish 하면 됨
- 유사한 기능을 제공하는 apache kafk등과 다른 점은 메시지를 보존하지 않는다는 점
- 메시지를 전송한 후에 따로 저장하지 않고 삭제함
- publish 하는 시점에서 이미 실행한 subscribe 명령으로 대기하고 있는 클라이언트들에게만 메시지 전달
- 따라서 client 의 message 수신이 보장되지 않음

참고 : https://brunch.co.kr/@springboot/374

https://docs.spring.io/spring-data/data-redis/docs/current/reference/html/#get-started:first-steps:spring

