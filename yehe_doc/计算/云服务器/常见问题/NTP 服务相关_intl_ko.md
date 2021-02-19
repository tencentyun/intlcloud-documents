### NTP 서비스 설정 후 NTP 동기화 간격은 어떻게 조정합니까?
[NTP 서비스 설정](https://intl.cloud.tencent.com/document/product/213/32381) 후, ntpd 서비스를 재시작해 NTP 동기화 간격을 재설정할 수 있습니다. ntpd 동기화 간격 수동 설정이 필요한 경우 다음 절차를 참고하십시오.
1. 다음 명령어를 실행하여 NTP 설정 파일을 수정합니다.
```
vi /etc/ntp.conf
```
2. **i**를 눌러 편집 모드로 들어간 후 다음을 설정합니다.
  1. `server time1.tencentyun.com iburst`가 있는 경우, 행 처음에 `#`을 추가하여 주석을 입력합니다.
  2. 다음 설정을 추가합니다. 여기서 `minpoll 4`는 최소 2<sup>4</sup>, `maxpoll 5`는 최대 2<sup>5</sup>를 의미합니다.
```
server time1.tencentyun.com minpoll 4 maxpoll 5
```
설정 완료 후 다음 이미지와 같이 나타나면 **:wq**를 입력하여 수정 사항을 저장하고 나갑니다.
![](https://main.qcloudimg.com/raw/02d6457d29b4c573605e3c79c5ccfc9f.png)
3. ntpd 서비스 재시작 후 `ntpd -p` 명령어를 실행하면 다음 이미지와 같이 poll 값이 16(2<sup>4</sup>)인 것을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/9fa0c72751de74d3b6e72cc1ca831952.png)

### Tencent Cloud의 ntpd 타임 원본 서버에서 제공하는 시간은 어디에서 획득하는 것입니까?
NTP 시계는 메이저 Beidou 타임 서버를 사용합니다.
 
### NTP 서비스 설정에서 localhost.localdomain timeout 오류가 발생하는 이유와 해결 방법은 무엇입니까?
오류 정보는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/1b3158135475e6cfbee28d2373685616.png)
해당 오류는 POSTROUTING을 진행한 경우 발생할 수 있습니다. 점검 및 확인해 주시고, 해당 작업을 진행한 경우 `ntp.conf` 프로파일 상의 소스 IP를 eth0의 IP로 변경해 주시면 됩니다.

### 오프 클라우드 서버와 온 클라우드 서버에서 공용으로 하나의 NTP를 사용할 수 있습니까? NTP 동기화 주소를 제공합니까?
내부 네트워크 NTP는 Tencent Cloud 상의 인스턴스만 사용할 수 있으며, 오프 클라우드 서버가 외부 네트워크를 지원하는 경우 외부 네트워크 NTP 소스를 통해 동기화할 수 있습니다. 주소는 다음과 같습니다.
- 내부 네트워크 NTP 서버
```
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```
- 외부 네트워크 NTP 서버
```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

### 사용자 정의 이미지를 생성하는 CVM과 정상 시간이 일치하지 않는 이유는 무엇입니까?
NTP 서비스를 활성화했는지 확인하십시오. 계속해서 NTP 동기화 기능을 사용해야 하는 경우 해당 인스턴스의 운영 체제에 따라 다음 문서를 참고하여 NTP를 설정하고, 설정 완료 후 다시 사용자 정의 이미지를 생성하면 됩니다.
 - [Linux 인스턴스: NTP 서비스 설정](https://intl.cloud.tencent.com/document/product/213/32381)
 - [Windows 인스턴스: NTP 서비스 설정](https://intl.cloud.tencent.com/document/product/213/32380)

### CVM에서 ping으로 NTP 서버를 확인할 수 없습니다. NPT 동기화에 영향이 있습니까?
영향이 없습니다. NTP 도메인은 ping을 사용할 수 없습니다. NTP 서비스가 정상적으로 액세스되는지 확인하면 됩니다.

### 사용자 정의 이미지 생성에 사용하는 CVM에 ntp.conf가 환원되는 이유는 무엇입니까?
시스템 내 Cloud-Init가 초기화되기 때문입니다. 사용자 정의 이미지 생성 전에 `/etc/cloud/cloud.cfg`의 NTP 관련 설정을 삭제하십시오. 자세한 내용은 [Cloud-Init 및 Cloudbase-Init 문제](https://intl.cloud.tencent.com/document/product/213/19670)를 참조하십시오.

### 내부 네트워크 DNS가 변경되면 구체적으로 어떤 영향이 있습니까?
Tencent Cloud 내부 리졸브와 관련된 모든 서비스가 영향을 받습니다. 예를 들면 다음과 같습니다.
- yum 소스는 기본적으로 Tencent 내부 네트워크 도메인으로 설정되어 있어 yum 다운로드에 영향을 미칩니다. DNS가 변경되는 경우 yum 소스를 변경해야 합니다.
- 데이터 모니터링 리포트에 영향을 미치며, 해당 기능은 내부 네트워크 도메인에 종속되어 있습니다.
- 서버 시간 NTP 동기화 기능에 영향을 미치며, 해당 기능은 내부 네트워크 도메인에 종속되어 있습니다.

### Windows 시스템 인스턴스 로컬 시간을 미국 동부 시간으로 설정했는데 재시작 후 다시 베이징 시간으로 돌아가는 이유는 무엇입니까?
해당 인스턴스에 windowstime 서비스가 활성화되어 있는지 확인하십시오. 해당 서비스가 정상적으로 실행되지 않으면 수동으로 활성화합니다. 서비스 활성화 후 인스턴스 시스템 시간이 자동으로 동기화되며, 해당 서비스를 부팅 시 자동 실행으로 설정하는 것을 권장합니다.

### ntpq -np 명령어로 동기화 시간을 확인할 수 없는 이유는 무엇입니까?
오류 정보는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/88972a2aeda155c10000e8576d16bbe9.png)
해당 오류는 통상적으로 `/etc/ntp.conf`의 listen 네트워크 디바이스에 IP가 설정되어 있지 않거나 인스턴스가 아닌 내부 네트워크 메인 IP로 설정되었을 때 나타납니다. 확인 및 점검해 주시고, 이와 같이 설정한 경우 메인 IP 변경 후 ntpd를 재시작하면 됩니다.

### 외부 네트워크 NTP 타임 서버를 사용하여 시간을 동기화하면 오류가 발생하는데 어떻게 해결해야 합니까?
외부 네트워크 NTP 타임 서버를 사용하여 시간을 동기화하면 다음 이미지와 같이 `no server suitable for synchronization found` 오류가 발생합니다.
![](https://main.qcloudimg.com/raw/1909910bc2a86a5f93e09f4601654327.png)
인스턴스의 공인 IP가 DDOS 공격을 받을 때 NTP 반사 보안 정책이 트리거되어 Tencent Cloud에 액세스하는 소스 포트 123의 외부 네트워크 트래픽을 모두 차단했기 때문일 수 있으며, 시간 동기화에 오류가 발생할 수 있습니다. 인스턴스 사용 시 최대한 내부 네트워크 NTP 타임 서버를 사용해 시간을 동기화하는 것을 권장합니다.
