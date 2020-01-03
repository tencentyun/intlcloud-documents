## 작업 시나리오
본 문서는 CentOS 7.2 64비트 시스템을 예시로 들며, vsftpd를 FTP 서비스 포트로, FileZilla을 클라이언트로 사용합니다. Linux CVM에 FTP 서비스를 구축하는 방법을 안내합니다.

## 작업 순서
### vsftpd 설치
1. Linux CVM에 로그인하십시오.
2. 아래의 명령어를 실행하여 vsftpd를 설치하십시오.
``` 
yum install vsftpd -y
```

### 서비스 시작
1. 아래의 명령어를 실행하여 서비스를 시작하십시오.
```
systemctl start vsftpd
```
2. 아래의 명령어를 실행하여 서비스가 시작되었는지 확인하십시오.
```
netstat -tunlp
```
아래의 정보와 같은 리턴 유형은 vsftpd 서비스 시작이 성공되었음을 나타냅니다.
![](http://mc.qcloudimg.com/static/img/6cc74de5689106ce763be98bfe7f5d24/image.png)

### (옵션) vsftpd 서비스 검증
> FTP 서비스 포트 구성의 원활한 완성을 보장하기 위해, 로컬 컴퓨터 또는 기타 CVM에서 작업 순서를 실행하여 vsftpd 서비스가 시작에 성공했는지 재차 검증할 수 있습니다. 아래의 작업 순서는 Linux 운영 체제의 로컬 컴퓨터를 예시로 합니다. 만약 로컬 컴퓨터가 Windows/Mac OS일 경우, 컴퓨터가 telnet 기능을 시작했는지 확인하십시오.
>
1. 로컬 컴퓨터 운영 체제의 인터페이스에서 telnet 서비스를 설치하십시오.
> 만약 사용자의 로컬 컴퓨터가 Windows/Mac OS 운영 체제일 경우, 이 단계는 건너뛰십시오.
>
```
yum -y install  telnet
```
3. 아래의 명령어를 실행하여 vsftpd 서비스가 시작에 성공했는지 테스트하십시오.
```
telnet +CVM 공용 네트워크 IP + 21
```
아래 정보와 같은 유형이 리턴되면 성공적으로 시작되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/47ad66d7be133b6d69d60c3e5b719dbd.png)

<span id = "jump">  </span>

### vsftpd 구성
1. 아래의 명령어를 실행하여 vsftpd 구성 파일을 여십시오.
```
vi /etc/vsftpd/vsftpd.conf
```
2. “**i**” 또는 “**Insert**”를 눌러 편집 모드로 전환하여, 파일 중의 ‘anonymous_enable=YES’를 ‘anonymous_enable=NO’로 변경하십시오. 아래 이미지를 참조하십시오.
![](http://mc.qcloudimg.com/static/img/4e7770981eae42e7b16a2a5a7866a6a6/image.png)
3. “**Esc**”를 누르고 “**:wq**”를 입력하여 파일을 저장한 뒤 돌아가십시오.

### FTP 사용자 추가
1. 아래의 명령어를 실행하여 `ftpuser1` 사용자를 추가하십시오.
``` 
useradd -m -d /home/ftpuser1 -s /sbin/nologin ftpuser1
```
2. 아래의 명령어를 실행하여 `ftpuser1` 사용자의 비밀번호를 설정하십시오.
```
passwd ftpuser1
```
사용자 생성, 사용자 비밀번호 설정을 완료했습니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/eec9ba9d188bf8b82a846fed73e02b52.png)

## 후속 작업
FTP 서비스 구축을 완료한 후, 이것을 기반으로 파일을 업로드 또는 다운로드할 수 있습니다. 예시로 [Windows 머신의 FTP를 통한 파일 업로드](https://intl.cloud.tencent.com/document/product/213/2132)가 있습니다.

## FAQ
### FTP 클라이언트의 연결 시간이 초과되거나 디렉터리 읽기가 실패한 경우
#### 문제 설명
로컬에서 FTP 클라이언트를 사용해 연결 시 일부 사용자는 연결 시간이 초과되거나 디렉터리 읽기가 실패하는 문제와 마주칩니다. 아래 이미지를 참조하십시오.
![](http://mc.qcloudimg.com/static/img/eb7beaf8c5a6e683257e94dd754e3f25/image.jpg)
PASV 커맨드에서 문제가 나타날 경우, FTP 프로토콜이 Tencent Cloud 네트워크 아키텍처에서 적절하지 않은 것이 원인입니다. FTP 클라이언트는 기본적으로 수동 모드로 전송되므로 통신 과정 중 서버 포트의 IP 주소를 찾아 연결을 진행합니다. 그러나 Tencent Cloud의 공용 네트워크 IP는 ENI에 직접적으로 배치되지 않습니다. 그리하여 수동 모드에서 클라이언트는 유효 IP를 찾지 못하며, CVM 개인 IP만 찾을 수 있으나 개인 IP는 공용 네트워크와 직접 통신할 수 없습니다. 따라서 연결할 수 없습니다.

#### 해결 방법
1. 클라이언트 전송 모드를 자동으로 변경하십시오.
2. 만약 클라이언트의 네트워크 환경이 수동 모드를 필요로 하는 경우 서비스 포트에서 [vsftpd 구성](#jump)의 구성 파일에 아래와 같은 명령을 새로 추가해야 합니다.
```
pasv_address=XXX.XXX.XXX.XXX     //(공용 네트워크 IP)
pasv_enable=YES
pasv_min_port=1024
pasv_max_port=2048
```

### FTP 클라이언트가 파일 업로드를 실패한 경우
#### 문제 설명

Linux 시스템 환경에서 vsftp를 통해 파일을 업로드할 경우 아래와 같은 오류 정보를 표시합니다.
```
553 Could not create file
```

#### 해결 방법
1. 아래의 명령어를 실행하여 서버 디스크 용량의 사용률을 검사하십시오.
```
df -h
```
 - 디스크 용량이 부족할 경우 파일이 업로드되지 않을 수 있습니다. 디스크 용량이 큰 파일을 삭제하길 권장합니다.
 - 디스크 용량이 정상일 경우 다음 단계를 진행하십시오.
2. 아래의 명령어를 실행하여 FTP 디렉터리의 쓰기 권한이 있는지 검사하십시오.
```
ls -l /home/test      
# /home/test FTP 디렉터리를 실제 FTP 디렉터리로 수정하십시오.
```
 - 결과로 돌아가기 중 ‘w’가 없을 경우 사용자의 쓰기 권한이 없는 것을 나타냅니다. 다음 단계를 진행하십시오.
 - 결과로 돌아가기 중 ‘w’가 있을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하고 피드백을 보내십시오.
3. 아래의 명령어를 실행하여 FTP 디렉터리에 쓰기 권한을 추가하십시오.
```
chmod +w /home/test 
# /home/test FTP 디렉터리를 실제 FTP 디렉터리로 수정하십시오.
```
4. 아래의 명령어를 실행하여 쓰기 권한 설정이 성공하였는지 다시 검사하십시오.
```
ls -l /home/test   
# /home/test FTP 디렉터리를 실제 FTP 디렉터리로 수정하십시오.
``` 




