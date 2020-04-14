사용자는 FTP 터널을 통해 애플리케이션을 자신의 서버에서 CVM으로 업로드할 수 있습니다.

## 1. CVM에서 FTP 서비스 설정

1) root 권한에서 다음과 같은 명령어를 통해 Vsftp를 설치합니다(예: CentOS 시스템)

```
yum install vsftpd
```


2) vsftpd 서비스를 실행하기 전에 CVM에 로그인하여 환경설정 파일을 수정해야 하며, 익명 로그인은 사용할 수 없습니다.

다음 명령어로 설정 파일을 엽니다.

```
vim /etc/vsftpd/vsftpd.conf
```

설정 파일에서 11번째 행의  
```
anonymous_enable=YES 를 
```
anonymous_enable=NO 로 

```
수정하면
```
익명으로 로그인할 수 없습니다.

3) 설정 적용 불러오기

```
cat /etc/vsftpd/vsftpd.conf |grep ^[^#] 
```
출력 결과는 다음과 같습니다.

```
local_enable=YES
write_enable=YES
local_umask=022
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_umask=022
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
xferlog_std_format=YES
listen=YES
pam_service_name=vsftpd
userlist_enable=YES
tcp_wrappers=YES
```

4) vsftpd 서비스를 실행합니다.

```
service vsftpd start
```

5) FTP 사용자 계정을 설정합니다.
다음 명령어로 FTP 사용자 계정을 설정합니다.

```
useradd
```
계정은 "ftpuser1", 목록은 /home/ftpuser1 로, 또한 ssh를 통한 로그인 금지로 설정:

```
useradd -m -d /home/ftpuser1 -s /sbin/nologin ftpuser1
```

다음 명령어로 계정 비밀번호를 설정합니다.

```
passwd
```
위 계정의 비밀번호가 "ftpuser1"이라고 할 때 : 

```
passwd ftpuser1
```

설정 완료 후 해당 계정으로 FTP 서버에 접속할 수 있습니다.

6) vsftpd의 pam 설정을 수정한 후 사용자는 자신이 설정한 FTP 계정 및 비밀번호를 사용해 CVM에 접속할 수 있습니다

다음 명령어를 사용하여 pam을 수정할 수 있습니다.

```
 vim /etc/pam.d/vsftpd
```

콘텐츠를 다음과 같이 수정합니다.

```
#%PAM-1.0 
auth required /lib64/security/pam_listfile.so item=user sense=deny file=/etc/ftpusers onerr=succeed 
auth required /lib64/security/pam_unix.so shadow nullok 
auth required /lib64/security/pam_shells.so 
account required /lib64/security/pam_unix.so 
session required /lib64/security/pam_unix.so 
```

다음 명령어를 통해 수정된 파일이 올바른지 확인합니다.

```
cat /etc/pam.d/vsftpd
```

출력 결과는 다음과 같습니다.

```
auth required /lib64/security/pam_listfile.so item=user sense=deny file=/etc/ftpusers onerr=succeed 
auth required /lib64/security/pam_unix.so shadow nullok 
auth required /lib64/security/pam_shells.so 
account required /lib64/security/pam_unix.so 
session required /lib64/security/pam_unix.so 
```

다음 명령어로 vsftpd 서비스를 재시작하여 수정 결과를 적용합니다.

```
service vsftpd restart
```

결과 값:

```
Shutting down vsftpd: [ OK ]
Starting vsftpd for vsftpd: [ OK ]
```

## 2. 파일을 Linux CVM에 업로드
1) 오픈 소스 소프트웨어 FileZilla를 다운로드한 후 설치합니다.
FileZilla의 3.5.1, 3.5.2 버전을 사용 바랍니다(3.5.3 버전의 FileZilla을 사용하면 FTP 업로드에 오류가 발생할 수 있습니다).
FileZilla 공식 홈페이지에서는 최신 3.5.3 버전만 다운로드할 수 있으므로, 3.5.1 및 3.5.2 버전의 다운로드 주소를 검색하여 진행 바랍니다. 3.5.1 버전 다운로드 링크: http://www.oldapps.com/filezilla.php?old_filezilla=6350

2) FTP 연결
FileZilla를 실행하여 다음 이미지 예시와 같이 설정한 후 "빠른 연결"을 클릭합니다.
![](//mccdn.qcloud.com/img56b0593f99e17.png)

>설정 정보 설명:
- 호스트: CVM의 공인 IP([CVM 콘솔](https://console.cloud.tencent.com/cvm)에 로그인하여 해당 CVM의 공인 IP를 조회할 수 있습니다).
- 사용자 이름: 이전 단계에서 설정한 FTP 사용자 계정을 "ftpuser1"을 예시로 사용합니다.
- 비밀번호: 이전 단계에서 설정한 FTP 사용자 계정 비밀번호를 "ftpuser1"을 예시로 사용합니다.
- 포트: FTP 리스너 포트로 기본 값 "21"입니다.

3) 파일을 Linux CVM에 업로드합니다.

파일 업로드 시 마우스 커서로 로컬 파일을 선택하고 원격 서버에 드래그하면 바로 Linux CVM에 업로드됩니다.

> 주의: CVM의 FTP 터널은 tar 압축 파일 업로드 후의 자동 압축 해제 및 tar 파일 삭제 기능을 지원하지 않습니다.

파일 업로드 예시는 다음 그림을 참고 바랍니다.

![](//mccdn.qcloud.com/img56b05a11b4b80.png)