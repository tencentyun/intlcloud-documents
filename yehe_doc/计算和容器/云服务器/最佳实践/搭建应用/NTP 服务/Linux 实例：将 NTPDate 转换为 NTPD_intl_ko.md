## 작업 시나리오

NTPDate는 중단점 업데이트를 사용하며, NTPD는 스테핑식의 점진적 시간 교정을 사용합니다. NTPDate 시간 동기화를 사용하고 있다면, 이미 탑재 및 실행 중인 서비스의 인스턴스에 대해 NTPD 시간 동기화를 사용하시기를 권장합니다. 본 문서는 CentOS 7.5 운영 체제의 CVM을 예로 들어 NTPDate를 NTPD로 전환하는 방법에 대해 소개합니다.

## 전제 조건
NTP 서비스의 통신 포트는 UDP 123으로, NTP 서비스를 설정하기 전에 UDP 123 포트가 개방된 상태를 유지해야 합니다.
해당 포트를 개방하지 않았다면 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조하여 개방하시기 바랍니다.

## 작업 순서

### NTPDate를 NTPD로 수동 전환
#### NTPDate 비활성화
1. 다음 명령어를 실행하여 crontab 설정을 내보낸 다음 NTPDate를 필터링합니다.
```
crontab -l |grep -v ntpupdate > /tmp/cronfile
```
2. 다음 명령어를 실행하여 NTPDate 설정을 업데이트합니다.
```
crontab /tmp/cronfile
```
3. 다음 명령어를 실행하여 `rc.local` 파일을 수정합니다.
```
vim rc.local
```
4. **i**를 눌러 편집 모드로 바꾸고, ntpupdate 설정 행을 삭제합니다.
5. "**Esc**"를 누르고 "**:wq**"를 입력하여 파일을 저장한 후 돌아갑니다.

#### NTPD 설정
1. 다음 명령어를 실행하여 NTP 서비스 구성 파일을 엽니다.
```
vi /etc/ntp.conf
```
2. 아래 이미지와 같이 **i**를 눌러 편집 모드로 바꾸고, server 관련 설정을 찾아 설정하고자 하는 타깃 NTP의 시계 원본 서버(예: `time1.tencentyun.com`)로 server를 수정한 다음, 불필요한 NTP 시계 원본 서버를 삭제합니다.
![server 설정](https://main.qcloudimg.com/raw/643dc5bbd2a42307ec10b5d38f756dda.png)
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장한 뒤 리턴합니다.


### Linux 인스턴스: NTPDate를 NTPD로 자동 전환
1. `ntpd_enable.sh` 스크립트를 다운로드 합니다.
```
wget https://image-10023284.cos.ap-shanghai.myqcloud.com/ntpd_enable.sh
```
2. 다음 명령어를 실행하여 `ntpd_enable.sh` 스크립트로 NTPDate를 NTPD로 전환합니다.
```
sh ntpd_enable.sh
```



