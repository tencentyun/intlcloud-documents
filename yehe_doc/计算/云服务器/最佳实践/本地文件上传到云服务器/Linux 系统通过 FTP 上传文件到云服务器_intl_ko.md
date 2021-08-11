## 작업 시나리오

본 문서는 Linux 시스템의 로컬 기기에서 FTP 서비스를 통해 로컬 파일을 CVM에 업로드하는 방법을 소개합니다.

## 전제 조건

CVM에 FTP 서비스가 구축되어 있어야 합니다.
- CVM이 Linux 운영 체제일 경우, 자세한 작업 방식은 [Linux CVM에서 FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10912)을 참조 바랍니다.
- CVM이 Windows 운영 체제일 경우, 자세한 작업 방식은 [Windows CVM에서 FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10414)을 참조 바랍니다.

## 작업 순서

### CVM 연결
1. 다음 명령어를 실행하여 ftp를 설치합니다.
> Linux 시스템의 로컬 기기에 ftp가 설치되어 있다면, 이 단계를 건너뛰고 다음 단계를 진행하시기 바랍니다.
>
```
yum -y install ftp
```
2. 다음 명령어를 실행하여 로컬 컴퓨터에 CVM을 연결하고, 인터페이스 안내에 따라 FTP 서비스의 사용자 이름과 비밀번호를 입력합니다.
```
ftp CVM의 IP 주소
```
아래의 인터페이스로 이동하면 연결 성공입니다.
![](https://main.qcloudimg.com/raw/9d93f45167addf70e023a21543af59f8.png)

### 파일 업로드
다음 명령어를 실행하여 로컬 파일을 CVM에 업로드합니다.
```
put local-file [remote-file]
```
예시: 로컬 파일 `/home/1.txt`를 CVM에 업로드.
```
put /home/1.txt 1.txt
```

### 파일 다운로드
다음 명령어를 실행하여 CVM의 파일을 로컬에 다운로드합니다.
```
get [remote-file] [local-file]
```
예시: CVM의 `A.txt` 파일을 로컬 `/home` 디렉터리에 다운로드.
```
get A.txt /home/A.txt
```

