# Chapter1 네트워크 프로그래밍과 소켓의 이해

## 01-1 네트워크 프로그래밍과 소켓의 이해

저자는 독자들이 초반부에 C언어를 배웠다는 가정 하에, 

콘솔 입출력 함수인 printf, scanf 이 익숙하다면 유사한 파일 입출력, 그리고 네트워크 프로그래밍을 모두 쉽게 배울 수 있습니다~



### 네트워크 프로그래밍과 소켓에 대한 매우 간단한 이해

#### 네트워크 프로그래밍?

네트워크로 연결된 서로 다른 두 컴퓨터가 데이터를 주고 받도록 하는 것



#### 데이터를 주고 받기 위해선 무엇이 필요할까?

##### 1. 물리적인 연결

물리적 연결 고민 필요없습니다~ 이미 인터넷이라는 네트워크엔 대부분의 컴퓨터가 연결되어 있거든요.

##### 2. 소프트웨어적인 데이터의 송수신 방법

오~ 이것도 걱정하실 필요없습니다. 세세한 내용은 다 숨기고 편하게 데이터를 송수신할 수 있도록 운영체제에서는 소켓(Socket)이라는 것을 제공해주거든요.

소켓을 통해서 데이터를 송수신할 수 있기 때문에 네트워크 프로그래밍을 소켓 프로그래밍이라고도 부릅니다.

> 여기서 잠깐! - 소켓의 어원
>
> 집에서 가전제품 동작시키려면 코드를 '소켓'에 꽂죠? 그 소켓을 통해서 전력 망에 연결되어 있어서 전력망의 전기를 가전 제품에 공급할 수 있게 되는 것이죠. 여기서 소켓의 의미가 나옵니다.
>
> 다른 컴퓨터와 데이터를 송수신하기 위해 인터넷이라는 네트워크 망에 연결하기 위해 사용되는 도구가 '소켓'인것이죠.
>
> 한편으로는 이 의미를 확장하여 소켓은 네트워크를 통한 두 컴퓨터의 연결을 의미하기도 합니다.



### 소켓의 구현

소켓은 전화기와 매우 유사합니다. 따라서 전화기와 소켓을 비유해가며 전체소켓 프로그래밍 흐름을 설명드리도록 하겠습니다. 약간의 다른 점이라면 송신, 수신 방법이기 때문에 이를 구분지어 설명하도록 하겠습니다.



#### 수신 전화기 - 소켓

전화를 받는 방법은 다음처럼 말할 수 있습니다.

##### 전화기의 전화 받는 방법

**1.전화기 구입**

전화기가 있어야 전화를 할 수 있겠죠? ㅎㅎ;

**2. 전화기에 전화번호 부여**

나의 전화번호를 알려줘야 누군가가 제 전화기로 연락할 수 있겠죵?

**3. 전화기에 케이블 연결하기**

전화망에 연결시켜주어 나에게 연락할 수 있는 상태로 해주는 것이죠.

**4. 연락이 오면 통화를 위해 수화기를 들기**

띠링띠링~ 연락이 온다면 수화기를 들어서 통신하잖아요~



이 과정을 소켓 프로그래밍에 대입해보겠습니다.

##### 소켓 프로그래밍에서 데이터를 받는 방법

**1. 소켓 생성 - (전화기 구입)**

소켓을 생성하는 함수입니다.

```c
#include <sys/socket.h>
int socket(int domain, int type, int protocol);
// 성공: file descriptor 반환, 실패: -1 반환
```

코드를 자세히 보지는 마시고 이런게 있구나~ 하고 넘어가세요. 

**2. socket bind - (전화번호 부여)**

```c
#include <sys/socket.h>
int bind(int sockfd, struct sockaddr *myaddr, socklen_t addrlen);
// 성공: 0 반환, 실패 -1 반환
```

이 과정에선 internet에서 주소에 해당하는 IP Address, Port Number라는 소켓의 주소정보를 할당해줍니다.

**3. socket listen - (케이블 연결)**

```c
#include <sys/socket.h>
int listen(int sockfd, int backlog);
// 성공: 0 반환, 실패 -1 반환
```

listen 함수 명에서 보이듯, 이 함수를 실행하면 누군가의 연결 요청을 수신할 수 있는 상태가 됩니다.

**4. socket accept - (수화기 들기)**

```c
#include <sys/socket.h>
int accpet(int sockfd, struct sockaddr *addr, socklen_t  *addrlen);
// 성공: file descriptor 반환, 실패 -1 반환
```

이 함수 호출을 통해, 연결 요청을 수락할 수 있습니다. 전화가 오는데 수화기를 안들면 안받겠다는 의미이고, 수화기를 들면 통화하겠다는 의미잖아요? ㅎㅎ



이 밑 그림을 바탕으로 개념을 확장해나갈 것이니 머리 속에 기억해두시길 바랍니다.



##### "Hello World!" 서버 프로그램 구현

연결 요청을 수락하는 기능의 프로그램을 서버(Server)라고 부릅니다. 앞서 배운 내용을 확인할 겸 실제 Hello world!라고 응답해주는 서버 프로그램을 작성해보도록 하겠습니다.

앞서 배운 것이 어디서 쓰였나 참고용으로만 봐주세요. 



--- 코드 삽입 ---

```c
```





#### 송신 전화기 - 소켓

전화거는 방법과 소켓으로 데이터 보내는 방법은 약간 차이가 있습니다. 따라서, 과정에 대한 비유는 설명드리지 않도록 하겠습니다. 하지만! server socket 프로그래밍보다 더 간단하니 걱정하지 마세요~ 

한편으로, 서버 프로그램에서 생성한 소켓을 서버 소켓 또는 listening 소켓이라 부르고, 연결 요청을 하는 소켓을 클라이언트 소켓이라고 부릅니다. 



**전화를 거는 기능의 함수**

```c
#include <sys/socket.h>
int connect(int sockfd, struct sockaddr *serv_addr, socklen_t addrlen);
```



클라이언트 프로그램에서는 단순히 소켓을 생성하고, connection 함수로 서버에 연결 요청하는 과정만 존재하죠. 다음 예제 코드에서 두 과정을 찾아보세요~

```c
```





실행과정에서 입력한 127.0.0.1은 로컬 IP Address를 의미합니다. 한 컴퓨터 내 통신을 주고 받기 위해선 이러한 방식을 선택하죠. 다른 컴퓨터와 연결하기 위해선 그 컴퓨터의 IP Address를 입력해주시면 됩니다.



## 01-2 리눅스 기반 파일 조작하기

리눅스에선 소켓과 파일을 동일하게 간주합니다. 따라서 파일 입출력 함수를 소켓 입출력에서 사용할 수 있지요. 따라서 파일 조작하는 방법에 대해 알아보겠습니다.



### 저 수준 파일 입출력(low-level File Access)과 파일 디스크립터(File Descriptor)

low-level의 의미는 단순하게, "표준에 상관없이 운영체제 자체에서 제공하는" 정도로 이해하시면 됩니다. 즉, 앞으로 언급할 내용은 ANSI 표준에서 정의한 함수가 아닌, 리눅스에서 제공해주는 파일 입출력에 대해 알아보겠습니다.

하지만! 파일 입출력을 알려면 파일 디스크립터에 대한 내용을 알아야 하죠. 



#### 파일 디스크립터

시스템으로부터 할당 받은 [파일 또는 소켓]에 부여된 정수를 의미합니다.

표준 입출력 및 표준 에러에도 리눅에선 파일 디스크립터를 할당하죠

| 파일 디스크립터 | 대상                       |
| --------------- | -------------------------- |
| 0               | 표준 입력: Standard Input  |
| 1               | 표준 출력: Standard Output |
| 2               | 표준 에러: Standard Error  |

이 때문에 파일을 열어서 반환된 파일 디스크립터의 번호는 3부터 시작하죠.





### 파일 열기

데이터를 읽거나 쓰기 위해서 파일을 열 때 사용하는 함수를 말씀드리겠습니다.

받는 인자의 갯수: 2개

1. 대상이 되는 파일의 이름 및 경로의 정보
2. 파일의 오픈 모드 정보(파일 특성 정보) 비트 OR 연산을 통해 하나 이상의 정보를 전달할 수 있습니다.

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

int open(const char *path, int flag);
// 성공: file descripter 반환, 실패 -1 반환
```



오픈 모드는 다음 것 들이 있습니다.



한편으로, OR 비트 연산으로 하나 이상의 정보를 전달할 수 있는 이유는... 각 옵션이 비트 벡터로 표현되기 때문입니다.

0x00000200   0010/0000/0000  O_CREAT  16진수. 1자리가 16자리의 수를 나타낼 수 있음 -> 4비트로 표현 가능

0x0001            0000/0000/0001 O_WRONLY

0x00000400   0100/0000/0000 O_TRUNC



​						 0110/0000/0001



###### 참고자료

왜 16진수 표시엔 0x가 붙을까?

https://www.quora.com/Why-do-hexadecimal-numbers-by-convention-start-with-0x-in-many-programming-languages





### 파일 닫기

파일을 연 다음에는 반드시 닫아주어야 합니다. memory leak때문이지요

> file descriptor는 os에서 file descriptor table이란 곳에서 저장됩니다. 한편, 프로세스에서는 단순히 int type의 local variable이므로 stack memory에 저장되죠.

```c
#include <unistd.h>

int close(int fd);

// 성공: 0 반환, 실패 -1 반환
```

위 함수를 호출 하면서 인자로 파일 디스크립터를 인자로 전달하면 파일을 종료하게 해줍니다. 그런데! 소켓과 파일은 동일하게 취급한다고 했잖아요? 소켓을 종료할 때도 위 함수 호출을 사용하죠.



### 파일에 데이터 쓰기

파일에 데이터를 출력(전송)하는 함수를 작성해보겠습니다. 이 함수 또한 소켓에서 데이터를 다른 컴퓨터에 전송할 때도 사용됩니다.

> 파일에 데이터를 출력, 전송한다. 말이 와닿지 않는다. 공부해보기!

```c
#include <unistd.h>

ssize_t write(int fd, const void * buf, size_t nbytes);
```



#### t로 끝나는 자료형

생소해보이는 ssize_t, size_t 같은 자료형을 primitive type이라고 부릅니다.

int type이 32bit(byte)라고 하지만, 보편적으로 운영체제가 32bit이기 때문입니다. 64bit 운영체제에서는 int type은 64bit이지요. ㄸ

따라서, 프로그램상 선택된 자료형의 변경을 요하게 됩니다. 그래서 size_t, ssize_t의 type def선언만 변경하여 작업하기 용이하도록 선언하는 것이죠. 

그래서 사용자가 정의하는 자료형과 구분하기 위해, 운영체제에서 정의하는 자료형은 _t가 붙어 있습니다. (운영체제의 환경에 따라 변경되므로)

t는 type의 약자로 보이네요.



### 예제

#### 파일 읽기, 열기

파일 열기, 읽기 예를 보여드리도록 하겠습니다.

#### 파일 열기

```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
void error_handling(char *smessage);

int main(void)
{
    int fd;
    char buf[] = "Let's go!\n";
    fd = open("data.txt",O_CREAT|O_WRONLY|O_TRUNC);
    if(fd == -1)
        error_handling("open() error!");
    printf("file descriptor: %d \n", fd);

    if(write(fd, buf, sizeof(buf)) == -1)
        error_handling("write() error!");
    close(fd);
    
    return 0;
}

void error_handling(char *message) {
    fputs(message, stderr);
    fputc('\n', stderr);
    exit(1);
}
```



#### 파일 읽기

```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
#define BUFF_SIZE 100
void error_handling(char *message);

int main(void)
{
    int fd;
    char buf[BUFF_SIZE];

    fd = open("data.txt", O_RDONLY);

    if(fd == -1)
        error_handling("open() error!");
    printf("file descriptor: %d \n", fd);

    if(read(fd, buf, sizeof(buf)) == -1)
        error_handling("read() error!");
    printf("file data: %s", buf);
    close(fd);

    return 0;
}

void error_handling(char *message)
{
    fputs(message, stderr);
    fputc('\n', stderr);
    exit(1);
}
```





#### 파일 디스크립터와 소켓

파일과 소켓을 생성해보고 반환되는 파일 디스크리벝의 값을 반환해보도록 하겠습니다.

```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <sys/socket.h>

int main(void)
{
    int fd1, fd2, fd3;
    
    fd1 = socket(PF_INET, SOCK_STREAM, 0);
    fd2 = open("data.txt", O_CREAT|O_WRONLY|O_TRUNC);
    fd3 = socket(PF_INET, SOCK_STREAM, 0);

    printf("file descriptor 1: %d\n", fd1);
    printf("file descriptor 2: %d\n", fd2);
    printf("file descriptor 3: %d\n", fd3);

    close(fd1);
    close(fd2);
    close(fd3);

    return 0;
}
```

