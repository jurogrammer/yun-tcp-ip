# 04 - 1 TCP와 UDP에 대한 이해

# TCP/IP

### TCP 정의

transmission Control Protocol



### TCP/IP 프로토콜 스택

* 레이어 설명
* 실제적으로 계층의 담당은 누가 하는가?



### TCP/IP 프로토콜 스택 탄생배경

* 인터넷을 통한 효율적인 데이터의 송수신

* 개방형 시스템(Open System)

  많은 사람들이 따르도록 한 시스템



### 각 레이어의 설명

* Physical Layer

* Link Layer

* Network Layer

  라우터

  손실 가능성. packet loss, packet error

  하나의 패킷 전송에만 관심을 두어 만들어짐.

* Transport Layer

  Network Layer 계층의 손실에 대해 통제해줌.

* Application Layer

  소켓 프로그래밍 부분 HTTP, SMTP, P2P....





# Server 리뷰

### 함수 호출 순서

socket() 서버소켓 생성

bind() 소켓 주소 할당

listen() 연결요청 대기상태

accept() 연결 허용

read()/write() 데이터 송수신

close() 연결종료

### 연결요청 대기상태로의 진입

```c
#include <sys/socket.h>

int listen(int sock, int backlog);
```



listen시 전달 받은 소켓의 연결요청 대기 상태에 둘 수 있다.

backlog => queue를 의미.

보통 서버는 최소 15이상을 할당한다.



### 연결 요청을 위한 소켓 accept

```c
#include <sys/socket.h>

int accpet(int sock, struct sockaddr * addr, socklen_t * addrlen);
```

sock: 서버 소켓 전달

addr: 연결 요청한 클라이언트의 주소 정보

addrlen: addr주소의 변수크기를 바이트 단위 전달.

* 대기 큐에 없으면 블로킹 상태
* 큐에 있는 요청을 받음.

packet -> byte 단위. 내부적으로 



# Client 리뷰

### 함수 호출 순서

1.socket() 소켓생성

2.connect() 연결요청

3.read()/write() 데이터 송수신

4.close() 연결종료



### 연결요청

```c
#include <sys/socket.h>

int connect(int sock, struct sockaddr * servaddr, socklen_t addrlen);
```



connect: 연결요청 접수 (데이터 받을 수 있는 상태 아님)

-> 연결요청 대기 큐에 등록된 상태를 의미하며, 반드시 서비스가 즉각 이루어지지 않을 수 있다.

서버의 상태에 따라 연결요청 중단.



* 이때, client 소켓의 IP, Port넘버 배정받음