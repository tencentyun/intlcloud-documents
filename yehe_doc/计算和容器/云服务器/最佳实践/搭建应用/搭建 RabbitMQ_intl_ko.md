## 작업 시나리오
RabbitMQ는 Advanced Message Queuing Protocol(AMQP)의 오픈 소스 메시지 프록시 소프트웨어를 구현한 것으로, 서버에서 Erlang 언어 입력을 사용하며 Python, Ruby, .NET, Java, JMS, C, PHP, ActionScript, XMPP, STOMP, AJAX 등 다양한 클라이언트를 지원합니다. 편의성, 확장성 및 고가용성 등의 장점을 갖춘 RabbitMQ를 본 문서를 참조하여 Tencent Cloud CVM에 배포할 수 있습니다.

## 예시 버전
본문의 예시 작업에서 사용하는 소프트웨어의 버전 및 구성은 다음과 같습니다.
- Linux: Linux 운영 체제의 경우, 본 문서는 CentOS 7.7를 예시로 사용합니다.
- RabbitMQ Server: 오픈 소스 메시지 프록시 소프트웨어의 경우, 본 문서는 RabbitMQ Server 3.6.9를 예로 듭니다.
- Erlang: 프로그래밍 언어의 경우, 본 문서는 Erlang 19.3을 예로 듭니다.


## 전제 조건
- Linux CVM을 구입 완료해야 합니다.
- Linux 인스턴스에 보안 그룹 규칙(80, 5672 및 15672 포트 개방)이 설정되어 있어야 합니다. 자세한 내용은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조 바랍니다.

## 작업 단계
### Erlang 설치
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수 있습니다.
	- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
	- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)
2. 다음 명령어를 실행하여 종속 패키지를 설치합니다.
```
yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
```
3. 다음 명령어를 실행하여 Erlang 설치 패키지를 다운로드합니다.
```
wget http://erlang.org/download/otp_src_19.3.tar.gz
```
4. 다음 명령어를 실행하여 Erlang 설치 패키지를 압축 해제합니다.
```
tar xzf otp_src_19.3.tar.gz
```
5. 다음 명령어를 실행하여 erlang 폴더를 생성합니다.
```
mkdir /usr/local/erlang
```
6. 다음 명령어를 순서대로 실행하여 Erlang 설치를 컴파일합니다.
```
cd otp_src_19.3
```
```
./configure --prefix=/usr/local/erlang --without-javac
```
```
make && make install
```
7. 다음 명령어를 실행하여 profile 구성 파일을 엽니다.
```
vi /etc/profile
```
8. **i**를 눌러 편집 모드로 이동하고 파일 끝에 아래의 내용을 입력합니다.
```
export PATH=$PATH:/usr/local/erlang/bin
```
9. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 종료합니다.
10. 아래의 명령어를 실행하여 환경 변수가 즉시 적용되도록 합니다.
```
source /etc/profile
```

### RabbitMQ Server 설치
1. 다음 명령어를 실행하여 RabbitMQ Server 설치 패키지를 다운로드합니다.
```
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_9/rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
본문은 RabbitMQ 3.6.9 버전을 예시로 하며, RabbitMQ 공식 홈페이지에서 제공하는 다운로드 주소를 사용합니다. 다운로드 링크가 유효하지 않는 등 오류가 발생하거나 다른 RabbitMQ 버전이 필요한 경우 [rabbitmq-server](https://github.com/rabbitmq/rabbitmq-server/releases)에서 더 자세한 설치 관련 정보를 얻을 수 있습니다.
10. 다음 명령어를 실행하여 서명 키를 가져옵니다.
```
rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
```
11. 다음 명령어를 순서대로 실행하여 RabbitMQ Server를 설치합니다.
```
cd
```
```
yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
12. 다음 명령어를 순서대로 실행하여 부팅 시 RabbitMQ 자동 실행으로 설정하고 RabbitMQ를 실행합니다.
```
systemctl enable rabbitmq-server
```
```
systemctl start rabbitmq-server
```
13. 다음 명령어를 실행하여 RabbitMQ의 기본 guest 계정을 삭제합니다.
```
rabbitmqctl delete_user guest
```
14. <span id="Step6"></span>다음 명령어를 실행하여 신규 사용자를 생성합니다.
```
rabbitmqctl add_user 사용자 이름 비밀번호
```
15. 다음 명령어를 실행하여 신규 사용자를 관리자 계정으로 설정합니다.
```
rabbitmqctl set_user_tags 사용자 이름 administrator
```
16. 다음 명령어를 실행하여 관리자 계정에 모든 권한을 부여합니다.
```
rabbitmqctl set_permissions -p / 사용자 이름 ".*" ".*" ".*"
```


### 설치 확인
1. 다음 명령어를 실행하여 RabbitMQ의 Web 관리 인터페이스를 실행합니다.
```
rabbitmq-plugins enable rabbitmq_management
```
2. 브라우저를 사용하여 아래의 주소에 액세스합니다.
```
http://인스턴스 공인 IP:15672
```
인스턴스의 공인 IP 획득 방법은 [공인 IP 주소 획득](https://intl.cloud.tencent.com/document/product/213/17940)을 참고하십시오.
아래 이미지와 같은 인터페이스가 표시되면 RabbitMQ Server 설치에 성공했음을 의미합니다.
![](https://main.qcloudimg.com/raw/aacb15db11b5cf80dd6b7ba1dc80d331.png)
3. 아래 이미지와 같이 [6단계](#Step6)에서 생성한 관리자 계정으로 로그인하면 RabbitMQ 관리 인터페이스로 이동할 수 있습니다.
![](https://main.qcloudimg.com/raw/7f8d24062541be6ba8b271483343b20a.png)

