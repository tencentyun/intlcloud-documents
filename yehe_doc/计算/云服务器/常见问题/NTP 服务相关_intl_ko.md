### 설정된 NTP 서비스의 동기화 간격을 어떻게 조정합니까?
Linux 인스턴스에서 [NTP 서비스 설정](https://intl.cloud.tencent.com/document/product/213/32381) 후 ntpd를 다시 시작하여 동기화 간격을 재설정할 수 있습니다. ntpd 동기화 간격을 수동으로 설정하려면 다음 단계를 수행하십시오.
1. 다음 명령을 실행하여 NTP 구성 파일을 수정합니다.
```
vi /etc/ntp.conf
```
2. **i**를 눌러 편집 모드로 들어가 다음과 같이 설정합니다.
  1. `server time1.tencentyun.com iburst`의 시작 부분에 `#` 기호를 추가하여 주석 처리합니다.
  2. 다음 구성을 추가합니다. 여기서 `minpoll 4`는 최소 간격이 2<sup>4</sup>임을 의미하고 `maxpoll 5`는 최대 간격이 2<sup>5</sup>임을 의미합니다.
```
server time1.tencentyun.com minpoll 4 maxpoll 5
```
결과는 다음과 같아야 합니다. **:wq**를 입력하여 변경 사항을 저장하고 파일을 닫습니다.
![](https://main.qcloudimg.com/raw/02d6457d29b4c573605e3c79c5ccfc9f.png)
3. ntpd를 다시 시작하고 `ntpd -p`를 실행합니다. 다음 그림과 같이 poll 값은 16(즉, 2<sup>4</sup>)입니다.
![](https://main.qcloudimg.com/raw/9fa0c72751de74d3b6e72cc1ca831952.png)

### Tencent Cloud의 ntpd 서버의 시간 소스는 무엇입니까?
NTP 서버는 일반적으로 BeiDou 위성 시계를 사용합니다.
 
### NTP 설정이 localhost.localdomain timeout 오류를 보고하면 어떻게 해야 합니까?
오류가 다음 이미지와 같은 경우:
![](https://main.qcloudimg.com/raw/1b3158135475e6cfbee28d2373685616.png)
POSTROUTING을 실행했는지 확인합니다. 그렇다면 `ntp.conf` 구성 파일의 소스 IP를 eth0의 IP 주소로 변경하십시오.

### 오프 클라우드 서버가 Tencent Cloud CVM과 NTP를 공유할 수 있습니까? NTP 동기화 주소는 무엇입니까?
Tencent Cloud는 Tencent Cloud 리소스에 대한 개인 NTP 서버를 제공합니다. 다른 장치의 경우 동기화를 위해 Tencent Cloud에서 제공하는 공용 NTP 서버를 사용할 수 있습니다.
- 개인 NTP 서버
```plaintext
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```
- 공용 NTP 서버
```plaintext
ntp.tencent.com
ntp1.tencent.com
ntp2.tencent.com
ntp3.tencent.com
ntp4.tencent.com
ntp5.tencent.com
```
다음은 이전 공용 NTP 서버 주소이며 이전 주소를 계속 사용할 수 있지만 새 공용 NTP 서버 주소를 설정하여 사용하는 것이 좋습니다.
```plaintext
time.cloud.tencent.com
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

### 사용자 정의 이미지에서 생성된 CVM 인스턴스의 시간이 잘못된 이유는 무엇입니까?
NTP 서비스가 활성화되어 있는지 확인하십시오. NTP 동기화 기능을 나중에 사용하려면 운영체제별로 다음 문서를 참고하여 NTP를 설정하십시오. 그런 다음 사용자 정의 이미지를 다시 만듭니다.
 - [Linux 인스턴스에서 NTP 서비스 설정](https://intl.cloud.tencent.com/document/product/213/32381)
 - [Windows 인스턴스에서 NTP 서비스 설정](https://intl.cloud.tencent.com/document/product/213/32380)



### 사용자 정의 이미지에서 생성된 CVM의 ntp.conf 콘텐츠가 복원되는 이유는 무엇입니까?
Cloud-Init 초기화로 인해 발생할 수 있습니다. 사용자 정의 이미지를 생성하기 전에 `/etc/cloud/cloud.cfg`에서 NTP 관련 구성을 삭제하십시오. 자세한 내용은 [Cloud-Init 및 Cloudbase-Init](https://intl.cloud.tencent.com/document/product/213/19670)를 참고하십시오.

### 수정된 개인 네트워크 DNS는 어떤 영향을 미칩니까?
Tencent Cloud 비공개 도메인 이름 리졸브와 관련된 모든 서비스가 영향을 받습니다. 예를 들면 다음과 같습니다.
- yum 저장소는 Tencent Cloud 개인 도메인 이름을 사용합니다. DNS 변경 후 yum 저장소를 수정해야 합니다.
- 모니터링 데이터의 리포트는 개인 도메인 이름을 사용하며 영향을 받습니다.
- NTP 기능은 서버 시간을 동기화하는 개인 도메인 이름에 따라 달라지며 영향을 받습니다.

### 다시 시작한 후 Windows 인스턴스의 현지 시간이 구성된 EST에서 베이징 시간으로 재설정되는 이유는 무엇입니까?
인스턴스에서 windowstime 서비스가 활성화되어 있는지 확인하십시오. 인스턴스의 시스템 시간을 자동으로 동기화하려면 수동으로 활성화해야 할 수 있습니다. 서비스 자동 시작을 활성화하는 것이 좋습니다.

### ntpq -np 명령을 사용하여 동기화 시간을 볼 수 없는 이유는 무엇입니까?
오류는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/88972a2aeda155c10000e8576d16bbe9.png)
`/etc/ntp.conf` 구성 파일에서 listen을 위해 구성된 IP가 없거나 잘못된 IP인지 확인하십시오. 인스턴스의 기본 개인 IP로 변경하고 ntpd를 다시 시작합니다.

### 공용 NTP 서버를 사용하여 시간을 동기화할 때 발생한 오류를 어떻게 수정합니까?
`no server suitable for synchronization found` 오류는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/1909910bc2a86a5f93e09f4601654327.png)
인스턴스의 공용 IP 주소에 대한 DDOS 공격에 대한 NTP 보호 정책으로 인해 발생할 수 있습니다. 이 정책은 Tencent Cloud의 소스 포인트(123)에서 모든 공용 인바운드 트래픽을 차단하고 동기화 예외를 발생시킵니다. 개인 NTP 서버를 사용하여 시간을 동기화하는 것이 좋습니다.



