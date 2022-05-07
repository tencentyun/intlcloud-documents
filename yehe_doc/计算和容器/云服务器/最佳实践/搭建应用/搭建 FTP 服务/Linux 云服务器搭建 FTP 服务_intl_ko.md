## 작업 시나리오
Vsftpd(very secure FTP daemon)는 수많은 Linux 릴리스 버전의 기본 FTP 서버입니다. 본문은 CentOS 7.6 64비트 운영 체제의 Tencent Cloud Virtual Machine(CVM)을 예시로, vsftpd 소프트웨어를 사용하여 Linux CVM의 FTP 서비스를 구축하는 방법을 설명합니다.

## 소프트웨어
본 문서에 구축한 FTP 서비스 구성 버전은 아래와 같습니다.
- Linux 운영 체제: 본 문서는 공용 이미지 CentOS 7.6을 예로 듭니다.
- Vsftpd: 본 문서는 vsftpd 3.0.2를 예로 듭니다.


## 작업 단계
### 1단계: CVM(Cloud Virtual Machine) 로그인
[Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다. 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수도 있습니다.
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)

### 2단계: vsftpd 설치
1. 다음 명령어를 실행하여 vsftpd를 설치합니다.
```
yum install -y vsftpd
```
2. 다음 명령어를 실행하여 부팅 시 vsftpd 자동 실행으로 설정합니다.
```
systemctl enable vsftpd
```
3. 다음 명령어를 실행하여 FTP 서비스를 실행합니다.
```
systemctl start vsftpd
```
4. 다음 명령어를 실행하여 서비스가 실행되었는지 확인합니다.
```
netstat -antup | grep ftp
```
아래와 같은 결과가 표시되면 FTP 서비스가 실행된 것입니다.
![](https://main.qcloudimg.com/raw/2a7abf80253a8469c9340878d89b452a.png)
이때 vsftpd가 익명 액세스 모드를 기본값으로 설정하므로 사용자 이름, 비밀번호 없이도 바로 FTP 서버에 로그인할 수 있습니다. 이 방식으로 FTP 서버에 로그인한 사용자는 수정 및 파일 업로드 권한이 없습니다.


### 3단계: vsftpd 설정<span id="user"></span>
1. 다음 명령어를 실행하여 FTP 서비스 사용을 위해 사용자 ID를 생성합니다. 본 문서는 ftpuser를 예로 듭니다.
```
useradd ftpuser
```
2. 다음 명령어를 실행하여 사용자 ftpuser의 비밀번호를 설정합니다.
```
passwd ftpuser
```
비밀번호를 입력한 후 **Enter**를 눌러 설정을 확인합니다. 비밀번호는 표시 안 함으로 기본 설정되어 있으며, 본 문서는 `tf7295TFY`를 예로 듭니다.
3. 다음 명령어를 실행하여 FTP 서비스에 사용할 파일 디렉터리를 생성합니다. 본 문서는 `/var/ftp/test`를 예로 듭니다.
```
mkdir /var/ftp/test
```
4. 다음 명령어를 실행하여 디렉터리 권한을 수정합니다.
```
chown -R ftpuser:ftpuser /var/ftp/test
```
5. 다음 명령어를 실행하여 `vsftpd.conf` 파일을 엽니다.
```
vim /etc/vsftpd/vsftpd.conf
```
6. **i**를 눌러 편집 모드로 전환하고 실제 수요에 따라 FTP 모드를 선택한 후 구성 파일 `vsftpd.conf`을 수정합니다.[](id:config)
<dx-alert infotype="notice" title="">
FTP는 능동 모드와 수동 모드를 통해 클라이언트 컴퓨터와 연결하고 데이터를 전송할 수 있습니다. 대다수 클라이언트 컴퓨터의 방화벽 설정과 리얼 IP를 획득할 수 없는 등의 이유로 **수동 모드**를 선택하여 FTP 서비스를 구축할 것을 권장합니다. 아래의 수정 예시는 수동 모드 설정이므로, 능동 모드를 선택해야 한다면 [FTP 능동 모드 설정](#port)으로 이동하십시오.
</dx-alert>
i. 다음의 설정 매개변수를 수정하여 익명 사용자와 로컬 사용자의 로그인 권한을 설정하고, 예외 사용자 리스트 파일을 지정하는 경로를 설정한 후 IPv4 sockets 리슨을 시작합니다.
```
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
listen=YES
```
ii. 줄 맨 앞에 `#`을 추가하여 `listen_ipv6=YES` 설정 매개변수를 주석 처리하고, IPv6 sockets 리슨을 종료합니다.
```
#listen_ipv6=YES
```
iii.  다음 설정 매개변수를 추가하고 수동 모드를 활성화하여, 로컬 사용자가 로그인한 후 위치한 디렉터리와 CVM이 데이터 전송에 사용할 포트 범위 값을 설정합니다.
```
local_root=/var/ftp/test
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=xxx.xx.xxx.xx #사용자의 Linux CVM의 공인 IP로 수정
pasv_min_port=40000
pasv_max_port=45000
```
7. **Esc**를 누르고 **:wq**를 입력하여 저장한 후 종료합니다.
8. 다음 명령어를 실행하여 `chroot_list` 파일을 생성 및 편집합니다.[](id:create)
```
vim /etc/vsftpd/chroot_list
```
9. **i**를 눌러 편집 모드로 전환하여 사용자 이름을 한 줄에 하나씩 입력합니다. 설정을 완료하면 **Esc**를 누르고 **:wq**를 입력하여 저장한 후 종료합니다.
설정된 사용자는 홈 디렉터리에 잠겨 있지 않게 됩니다. 예외 사용자를 설정할 필요가 없다면 이 단계를 건너뛸 수 있으며, **:wq**를 입력하여 파일을 종료합니다.
10. 다음 명령어를 실행하여 FTP 서비스를 재시작합니다.
```
systemctl restart vsftpd
```

### 4단계: 보안 그룹 설정
FTP 서비스를 구축한 후 실제 사용하는 FTP 모드에 따라 Linux CVM에 **인바운드 규칙**을 열어줘야 합니다. 자세한 사항은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.
대다수의 클라이언트 컴퓨터는 LAN에서 IP 주소 전환을 거칩니다. 따라서 FTP 능동 모드를 선택했다면 클라이언트 컴퓨터가 획득한 리얼 IP 주소를 확인하십시오. 그렇지 않으면 클라이언트가 FTP 서버에 로그인할 수 없게 됩니다.
- 능동 모드: 포트 21 개방.
- 수동 모드: 포트 21 개방 및 [구성 파일 수정](#config)에서 설정한 `pasv_min_port`와 `pasv_max_port` 사이의 모든 포트를 개방합니다. 본 문서는 40000 ~ 45000 범위의 포트를 개방합니다.

### 5단계: FTP 서비스 인증
FTP 클라이언트 소프트웨어, 브라우저 또는 파일 리소스 관리자 등의 툴을 통해 FTP 서비스를 인증할 수 있습니다. 본 문서는 클라이언트의 파일 리소스 관리자를 예로 듭니다.
1. 클라이언트의 IE 브라우저를 열어 **툴** > **Internet 옵션** > **고급**을 클릭하고, 선택한 FTP 모드에 따라 수정합니다.
 - 능동 모드: ‘수동 FTP 사용’ 선택 취소.
 - 수동 모드: ‘수동 FTP 사용’ 선택.
2. 클라이언트의 컴퓨터를 열어 경로 입력란에 아래 주소를 입력하여 액세스합니다.
```
ftp://CVM 공인 IP:21
```
![](https://main.qcloudimg.com/raw/40cef1738cb1d2fad07d2ef219822d2f.png)
3. ‘로그인 정보’ 팝업 창에 [vsftpd 구성](#user)에서 설정한 사용자 이름과 비밀번호를 입력합니다.
본 문서에서 사용한 사용자 이름은 `ftpuser`이고, 비밀번호는 `tf7295TFY`입니다.
4. 로그인에 성공한 후 파일을 업로드하거나 다운로드할 수 있습니다.


## 부록
### FTP 능동 모드 설정[](id:port)
능동 모드에서 수정해야 하는 설정은 다음과 같으며, 나머지 구성은 기본 설정을 유지합니다.
```
anonymous_enable=NO      #익명 사용자의 로그인 차단
local_enable=YES         #로컬 사용자 로그인 허용
chroot_local_user=YES    #전체 사용자를 홈 디렉터리로 제한
chroot_list_enable=YES   #예외 사용자 리스트 활성화
chroot_list_file=/etc/vsftpd/chroot_list  #사용자 리스트 파일 지정, 해당 리스트에 포함된 사용자는 홈 디렉터리에 제한되지 않음
listen=YES               #IPv4 sockets 리슨
#줄 맨 앞에 #을 추가하여 다음 매개변수 주석 처리
#listen_ipv6=YES         #IPv6 sockets 리슨 닫기
#다음 매개변수 추가
allow_writeable_chroot=YES
local_root=/var/ftp/test #로컬 사용자가 로그인 후 위치한 디렉터리 설정
```
**Esc**를 누르고 **:wq**를 입력하여 저장한 후 종료하고, [8단계](#create)로 이동하여 vsftpd 설정을 완료합니다.

### FTP 클라이언트의 파일 업로드 실패
#### 문제 설명
Linux 시스템 환경에서 vsftp를 통해 파일을 업로드할 경우 아래와 같은 오류 정보를 표시합니다.
```
553 Could not create file
```

#### 솔루션
1. 다음 명령어를 실행하여 서버 디스크 용량을 점검합니다.
```
df -h
```
 - 디스크 용량이 부족할 경우 파일을 업로드할 수 없게 됩니다. 디스크 용량이 큰 파일을 삭제하십시오.
 - 디스크 용량이 정상일 경우 다음 단계를 진행하십시오.
2. 다음 명령어를 실행하여 FTP 디렉터리에 쓰기 권한이 있는지 확인합니다.
```
ls -l /home/test      
# /home/test가 FTP 디렉터리입니다. 실제 FTP 디렉터리로 수정하십시오.
```
 - 반환 결과에 ‘w’가 없으면 사용자에게 쓰기 권한이 없음을 의미합니다. 다음 단계를 진행하십시오.
 - 반환 결과에 ‘w’가 있으면 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category
)을 통해 문의해주시기 바랍니다.
3. 다음 명령어를 실행하여 FTP 디렉터리에 쓰기 권한을 추가합니다.
```
chmod +w /home/test 
# /home/test가 FTP 디렉터리입니다. 실제 FTP 디렉터리로 수정하십시오.
```
4. 다음 명령어를 실행하여 쓰기 권한 설정에 성공했는지 다시 확인합니다.
```
ls -l /home/test   
# /home/test가 FTP 디렉터리입니다. 실제 FTP 디렉터리로 수정하십시오.
```
