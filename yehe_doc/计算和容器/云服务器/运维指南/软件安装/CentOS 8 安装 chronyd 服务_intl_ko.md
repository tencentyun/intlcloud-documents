## 작업 시나리오
현재 네이티브 CentOS 8는 ntp 서비스 설치를 지원하지 않아 시간이 부정확한 문제가 발생할 수 있습니다. 따라서 chronyd를 사용해 시간 서비스를 조정해야 합니다. 본 문서에서는 CentOS 8 운영 체제의 Tencent Cloud CVM에 chronyd 시간 서비스를 설치 및 설정하는 방법에 대해 소개합니다.

## 작업 순서
### chronyd 서비스 설치 및 설정
1. CVM 인스턴스에 로그인하십시오. 자세한 내용은 [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)을 참조하십시오.
2. 아래의 명령어를 실행하여 chronyd 서비스 설치하십시오.
```
yum -y install chrony
```
3. 다음 명령어를 실행하여 `chrony.conf` 구성파일을 수정합니다.
```
vim /etc/chrony.conf
```
4. **i**를 눌러 편집 모드로 들어간 뒤 `#log measurements statistics tracking` 뒤에서 줄바꿈하고 다음 내용을 입력합니다.
```
server time1.tencentyun.com iburst
server time2.tencentyun.com iburst
server time3.tencentyun.com iburst
server time4.tencentyun.com iburst
server time5.tencentyun.com iburst
```
편집 완료 후의 모습은 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/578e072599f8d50ea188d3911a9d76c7.png)
5. **Esc**를 누르고 **:wq**를 입력한 뒤 저장하고 편집 모드를 종료합니다.
6. 다음 명령어를 순서대로 실행하여 부팅 시 chronyd 서비스를 자동 실행하고 서비스를 재시작하도록 설정합니다.
```
systemctl restart chronyd
```
```
systemctl enable chronyd
```

### 서비스 설정 점검
1. 다음 명령어를 실행하여 시간이 동기화되었는지 확인합니다.
```
date
```
2. 다음 명령어를 실행하여 시간 동기화 상태를 확인합니다.
```
chronyc sourcestats -v
```
아래와 유사한 결과가 반환되면 설정이 성공했음을 나타냅니다.
![](https://main.qcloudimg.com/raw/6a5f584638de922f5e80b5b138541c9e.png)

## 부록
### 자주 쓰는 명령어
<table>
<tr>
<th>명령</th><th>설명</th>
</tr>
<tr>
<td>
<code>chronyc sources -v</code>
</td>
<td>시간 동기화 소스 조회. </td>
</tr>
<tr>
<td>
<code>chronyc sourcestats -v</code>
</td>
<td>시간 동기화 소스 상태 조회. </td>
</tr>
<tr>
<td>
<code>timedatectl set-local-rtc 1</code>
</td>
<td>하드웨어 시간 설정, 기본값은 UTC.
</td>
</tr>
<tr>
<td>
<code>timedatectl set-ntp yes</code>
</td>
<td>NTP 시간 동기화 활성화. </td>
</tr>
<tr>
<td>
<code>chronyc tracking</code>
</td>
<td>시간 서버 조정. </td>
</tr>
<tr>
<td>
<code>chronyc -a makestep</code>
</td>
<td>시스템 시간 강제 동기화. </td>
</tr>
</table>
