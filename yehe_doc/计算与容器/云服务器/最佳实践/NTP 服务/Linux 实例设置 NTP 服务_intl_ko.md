## 작업 시나리오

NTPD(Network Time Protocol daemon)는 Linux 운영 체제의 보호 프로세스 중의 하나로 NTP 프로토콜을 완전히 구현하였고 로컬 시스템과 시계 원본 서버 간의 시간을 교정하는 데 사용됩니다. NTPD는 NTPDate와 달리 스텝 바이 스텝식의 점차 시간을 교정하는 것이고 시간 점프가 발생하지 않지만 NTPDate는 중단점 업데이트입니다. 본 문은 NTPD의 설치와 사용을 소개합니다.

## 주의사항

* 일부 작업의 경우, 운영 체제는 기본 NTP 서비스로 chrony를 채택합니다. “systemctl is-active ntpd.service”를 사용하여 NTPD의 정상적인 운영 여부를 조회하고 “systemctl is-enabled ntpd.service”을 사용하여 NTPD가 컴퓨터 시작과 함께 자동으로 실행되는지 조회합니다. 자세한 내용은 아래의 NTPD를 컴퓨터 실행과 함께 자동으로 실행하도록 설정하는 부분을 참조하시길 바랍니다.
* NTP 서비스의 통신 포트는 UDP 123입니다. NTP 서비스 설정 이전에 UDP 123 포트가 이미 열렸음을 보장하십시오. 사용자는 netstat -nupl을 통해 인스턴스의 UDP 123 포트 활성화 여부를 조회할 수 있습니다. 사용자는 문서 [보안 그룹 운영 가이드](https://intl.cloud.tencent.com/document/product/213/18197)를 참조하여 UDP 123 포트 통과를 허가할 수 있습니다.

> **참고:**
> 본 문의 다음 작업은 모두 CentOS 7.5 64bit 인스턴스에서 진행됩니다.

## 작업 순서
### 설치

- 다음 명령어를 사용해 NTPD의 설치 여부를 판단합니다.
```
rpm -qa | grep ntp
```
![ntpd의 설치 여부 판단](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
- 설치하지 않았으면 yum install ntp를 사용해 설치합니다. 아무런 설정도 하지 않으면 NTPD는 클라이언트 모드에서 기본 작업을 합니다.
```
yum -y install ntp
```

### 설정
- vim으로 NTP 서비스 설정 파일을 열고 편집합니다.
```
vi /etc/ntp.conf
```
- server 관련 설정을 찾아 server를 사용자가 설정해야 하는 타깃 NTP 시계 원본 서버로 수정하고 잠시 필요하지 않은 NTP 시계 원본 서버를 삭제합니다.
![server 설정](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)

### 실행
- “service ntpd start”로 NTP 서비스를 실행하고 NTP가 이미 실행되었으면 “service ntpd restart”로 재시작합니다.
```
service ntpd start
```
![ntp 실행](https://main.qcloudimg.com/raw/470afd5f311b5ba3ad321ed12d974c88.png)

### 상태 점검
- netstat으로 NTP 서비스 포트 udp 123의 정상 모니터링 여부를 조회합니다.
```
netstat -nupl
```
![netstat -nupl](https://main.qcloudimg.com/raw/e7eb5ed8529fdc1366210ef76cf09bd3.png)
- 다음 명령어를 사용하여 NTPD 상태의 정상 여부를 조회합니다.
```
service ntpd status
```
![ntpd status](	https://main.qcloudimg.com/raw/8af337c167f295938f5edbc005032809.png)
- “ntpstat”를 사용하여 NTPD가 정상적으로 실행되었는 지, NTP 시계 원본 서버로 정확히 설정되었는지 조회할 수 있습니다. 해당 명령어는 현재 NTP 시계 원본 서버의 IP 주소를 출력할 수 있습니다. 이 IP 주소는 상기 설정한 NTP 시계 원본 서버의 IP 주소(“nslookup 도메인”을 사용하여 도메인에 대응되는 IP 주소를 획득할 수 있음)여야 합니다.
![ntpstat](https://main.qcloudimg.com/raw/83d49c87c485989123acbb9a30d92d0c.png)

- 더 자세한 NTP 서비스 정보는 ntpq -p를 사용해 획득할 수 있습니다.
![ntpq](https://main.qcloudimg.com/raw/87df34053b422b0c03e038e4e5a9fde0.png)
> remote: 이 요청에 응답하는 NTP 서버의 이름.
> refid: NTP 서버가 사용하는 상위 레벨의 NTP 서버.
> st: remote 원격 서버의 레벨. NTP는 레이어형 구조로, 상단의 서버, 멀티 레이어의 Relay Server 그리고 클라이언트까지 있기 때문에 서버를 높은 레벨에서 낮은 레벨까지 1-16으로 설정할 수 있습니다. 부하와 네트워크 막힘을 줄이기 위해 원칙적으로 레벨 1인 서버로 직접 연결하는 것을 피해야 합니다.
> when: 지난번 요청 성공 이후부터 지금까지의 초수.
> poll: 로컬 머신과 원격 서버가 얼마 동안 한 번씩 동기화(단위:초)하는 지를 나타내는 값. 처음 NTP를 실행할 때 이 poll 값은 비교적 작고 서버와의 동기화 빈도도 증가하게 되며 정확한 시간 범위로 빠르게 조정할 수 있습니다. 그 후 poll 값은 점차 커지고 동기화의 빈도도 상응하여 줄어듭니다.
> reach: 이는 팔진법 값이며 서버와 연결할 수 있는 지를 테스트하는 데 사용됩니다. 매번 성공적으로 연결할 때마다 그 값은 증가합니다.
> delay: 로컬 머신에서 NTP 서버로 동기화 요청을 보낼 때의 round trip time입니다.
> offset: 호스트는 NTP 시계를 통해 동기화하는 타임 소스의 시간 오프셋을 동기화하며 단위는 밀리세컨드(ms)입니다. offset이 0에 가까울 수록 호스트와 NTP 서버의 시간이 더 가깝습니다.
> jitter: 이것은 통계에 사용되는 값입니다. 이는 특정한 연속된 연결 수에서 offset의 분포를 집계했습니다. 간단하게 말해 이 값의 절대 값이 작을 수록 호스트의 시간이 더 정확합니다.

### NTPD를 컴퓨터 시작과 함께 실행되게 설정

- 다음 명령어를 사용하여 NTPD를 컴퓨터 시작과 함께 자동으로 실행되게 설정합니다.
```
systemctl enable ntpd.service
```

- 다음 명령어를 사용하여 chrony가 컴퓨터 시작과 함께 실행되도록 설정되어 있는지를 조회합니다.
```
systemctl is-enabled chronyd.service
```

- chrony와 NTPD가 충돌하면 NTPD 실행에 실패할 수 있습니다. 다음 명령어를 사용하여 chrony를 컴퓨터 시작과 함께 실행에서 제거해야 합니다.
```
systemctl disable chronyd.service
```


