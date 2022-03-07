## 작업 시나리오

Network Time Protocol daemon(NTPD)은 Linux 운영 체제의 데몬 프로세스 중 하나로, NTP 프로토콜을 완벽히 구현하였으며 로컬 시스템과 시계 원본 서버 간의 시간을 교정하는 데 사용됩니다. NTPD는 중단점 업데이트를 사용하는 NTPDate와 달리 스테핑식의 점진적인 시간 교정을 사용하므로 시간 점프 현상이 발생하지 않습니다. 본 문서는 CentOS 7.5 운영 체제의 CVM을 예로 들어 NTPD의 설치 및 설정 방법에 대해 소개합니다.

## 주의 사항

- 일부 운영 체제는 chrony를 기본 NTP 서비스로 사용하고 있으므로, NTPD가 실행 중인지와 부팅 시 자동 실행으로 되어 있는지 확인해야 합니다.
 - `systemctl is-active ntpd.service` 명령어를 사용하여 NTPD가 실행 중인지 확인할 수 있습니다.
 - `systemctl is-enabled ntpd.service` 명령어를 사용하여 NTPD가 부팅 시 자동 실행으로 되어 있는지 확인할 수 있습니다.
- NTP 서비스의 통신 포트는 UDP 123으로, NTP 서비스를 설정하기 전에 UDP 123 포트가 개방된 상태를 유지해야 합니다.
해당 포트를 개방하지 않았다면 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조하여 개방하시기 바랍니다.

## 작업 순서

### NTPD 설치

다음 명령어를 실행하여 NTPD가 설치되어 있는지 확인합니다.
```
rpm -qa | grep ntp
```
 - 아래와 같은 결과가 출력된다면 NTPD가 설치되어 있음을 의미합니다.
![ntpd의 설치 여부 판단](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
 - NTPD가 설치되어 있지 않다면 `yum install ntp`를 통해 NTPD를 설치합니다.
```
yum -y install ntp
```
NTPD는 기본적으로 클라이언트 실행 방식을 사용합니다.

### NTP 설정
1. 다음 명령어를 실행하여 NTP 서비스 구성 파일을 엽니다.
```
vi /etc/ntp.conf
```
2. 아래 이미지와 같이 **i**를 눌러 편집 모드로 바꾸고, server 관련 설정을 찾아 설정하고자 하는 타깃 NTP의 시계 원본 서버(예: `time1.tencentyun.com`)로 server를 수정한 다음, 불필요한 NTP 시계 원본 서버를 삭제합니다.
![server 설정](https://main.qcloudimg.com/raw/643dc5bbd2a42307ec10b5d38f756dda.png)
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장한 뒤 리턴합니다.

### NTPD 실행

다음 명령어를 실행하여 NTPD 서비스를 재시작합니다.
```
systemctl restart ntpd.service
```

### NTPD 상태 확인

다음 명령어를 실제 수요에 맞게 실행하여 NTPD의 상태를 확인합니다. 
- 다음 명령어를 실행하여, NTP 서비스 포트인 UDP 123 포트가 정상적으로 리슨되고 있는지 확인합니다.
```
netstat -nupl
```
아래와 같은 결과가 출력된다면 정상적으로 리슨되고 있음을 의미합니다.
![netstat -nupl](https://main.qcloudimg.com/raw/d7da764d05135959154920b81fa9f1e4.png)
- 다음 명령어를 실행하여 NTPD의 상태가 정상인지 확인합니다.
```
service ntpd status
```
아래와 같은 결과가 출력된다면 NTPD의 상태가 정상임을 의미합니다.
![ntpd status](https://main.qcloudimg.com/raw/321e56d0f7797f382d9f6903c0315f96.png)
- 다음 명령어를 실행하여 더 자세한 NTP 서비스 정보를 받을 수 있습니다.
```
ntpq -p
```
다음과 유사한 결과를 리턴합니다.
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **remote**: 이 요청에 응답하는 NTP 서버의 이름.
 - **refid**: NTP 서버가 사용하는 상위 레벨의 NTP 서버.
 - **st**: remote 원격 서버의 레벨. 서버는 1-16 사이의 숫자로 레벨의 높고 낮음을 설정하며, 부하 및 네트워크 혼잡을 완화하기 위해 원칙상으로는 레벨 1의 서버에는 직접적으로 연결하지 않도록 권장합니다.
 - **when**: 지난번 요청 성공 이후부터 지금까지의 시간(초).
 - **poll**: 로컬 기기와 원격 서버가 얼마의 시간에 한 번 동기화(단위는 초)하는지 의미합니다. 초기에 NTP를 실행할 때의 poll 값은 비교적 낮으므로, 서버와의 동기화 빈도수가 늘어날 수 있습니다. 가능한 빨리 올바른 시간 범위로 변경하시기 바랍니다. 변경한 후에는 poll 값이 점점 늘어나며 동기화 빈도수는 상대적으로 줄어들게 됩니다.
 - **reach**: 8진수 값으로, 서버와 연결할 수 있는지 테스트하는 데 사용합니다. 한 번 연결에 성공할 때마다 reach의 값이 늘어납니다.
 - **delay**: 로컬 기기에서 NTP 서버로 동기화 요청을 보낼 때의 round trip time입니다.
 - **offset**: 호스트는 NTP 시계를 통해 동기화할 타임 소스의 시간 오프셋을 동기화하며 단위는 밀리세컨드(ms)입니다. offset이 0에 가까울수록 호스트와 NTP 서버의 시간이 더 가깝습니다.
 - **jitter**: 통계에 사용하는 값. 특정 기준으로 연속하는 숫자 내 offset의 분포 현황을 통계합니다. 즉 jitter 값의 절댓값이 작을수록 CVM의 시간이 더 정확합니다.

### NTPD를 부팅 시 실행되도록 설정

1. 다음 명령어를 실행하여 NTPD를 부팅 시 자동 실행으로 설정합니다.
```
systemctl enable ntpd.service
```
2. 다음 명령어를 실행하여 chrony가 부팅 시 실행으로 설정되었는지 확인합니다.
```
systemctl is-enabled chronyd.service
```
chrony가 부팅 시 실행으로 설정되었다면, 다음 명령어를 실행하여 chrony를 부팅 시 자동 실행에서 삭제합니다.
chrony와 NTPD가 충돌하여 NTPD의 부팅 시 실행이 실패할 수 있습니다.
```
systemctl disable chronyd.service
```

### NTPD의 보안성 향상

다음 명령어를 차례대로 실행하여 `/etc/ntp.conf` 구성 파일의 보안성을 향상합니다.
```
interface ignore wildcard
```
```
interface listen eth0
```
