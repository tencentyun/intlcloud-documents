## 기능 개요

COS FTP Server는 FTP 프로토콜을 통해 파일 업로드, 다운로드, 삭제 및 폴더 생성 작업 등 직접 COS 상의 객체 및 디렉터리를 조작할 수 있습니다. FTP Server 툴은 Python을 사용하여 실현되어 설치가 더욱 간편합니다.

## 기능 설명

**업로드 메커니즘**: 스트리밍 방식으로 업로드하여 로컬 디스크에 저장하지 않습니다. 표준 FTP 프로토콜에 따라 작업 디렉터리를 설정하면 되며, 실제로 디스크의 저장 용량을 점유하지 않습니다.
**다운로드 메커니즘**: 직접 스트리밍 방식으로 클라이언트에 반환합니다.
**디렉터리 메커니즘**: bucket이 전체 FTP Server의 루트 디렉터리가 되며, bucket 하위에 여러 개의 디렉터리를 생성할 수 있습니다.
**멀티 bucket 바인딩**: 동시에 여러 개의 bucket을 바인딩할 수 있습니다.
>멀티 bucket 바인딩: 각 FTP Server 작업 경로(home_dir)별로 실현합니다. 따라서 서로 다른 bucket과 사용자 정보를 지정하는 경우 반드시 home_dir이 달라야 합니다.

**삭제 작업 제한**: 새로운 FTP Server에서 각 ftp 사용자에게 delete_enable 옵션을 설정하여 해당 FTP 사용자에게 파일을 삭제할 수 있는 권한 허용 여부를 표시할 수 있습니다.
**지원하는 FTP 명령어:**put, mput, get, rename, delete, mkdir, ls, cd, bye, quite, size
**지원하지 않는 FTP 명령어:**append, mget(네이티브 mget 명령어는 지원하지 않습니다. 단, 일부 Windows 클라이언트에서는 일괄 다운로드를 할 수 있습니다. 예: FileZilla 클라이언트)

>FTP Server 툴은 현재 중단된 시점부터 이어서 전송하는 기능을 지원하지 않습니다.

## 시작하기

#### 시스템 환경

- 운영 체제: Linux 및 Tencent CentOS(권장 사용)의 [CVM](https://intl.cloud.tencent.com/document/product/213)을 사용할 수 있으며, 현재 Windows 시스템은 지원하지 않습니다.
- psutil 종속 Linux 시스템 패키지: python-devel(또는 python-dev, 각 Linux 릴리스 버전에 따라 이름 상이)이며, Linux의 패키지 관리 툴에 추가할 수 있습니다. 예시: `yum install python-devel` 또는 `aptitude install python-dev`
- Python 인터프리터 버전: Python 2.7, [Python 설치 및 설정](https://intl.cloud.tencent.com/document/product/436/10866)을 참조하여 설치 및 설정하십시오.
- 종속 패키지:
 - [cos-python-sdk-v5](https://pypi.org/project/cos-python-sdk-v5/) (≥1.6.5)
 - [pyftpdlib](https://pypi.org/project/pyftpdlib/) (≥1.5.2)
 - [psutil](https://pypi.org/project/psutil/)(>=5.6.1)


#### 사용 제한

COS XML 버전에 사용합니다.

#### 설치 실행

FTP Server 툴 다운로드 주소: [cos-ftp-server](https://github.com/tencentyun/cos-ftp-server-V5), 설치 방법은 다음과 같습니다.

1. FTP Server 디렉터리에 들어가 setup.py를 실행해 FTP Server 및 관련 종속 라이브러리(인터넷 연결 필요)를 설치합니다.
```bash
python setup.py install   # 여기에서 계정 sudo 또는 root 권한이 필요할 수 있음
```
2. 설정 예시 파일인 `conf/vsftpd.conf.example`을 `conf/vsftpd.conf`로 이름을 변경하여 복사합니다. 본 문서의 [구성 파일](#conf) 섹션을 참고하여 bucket과 사용자 정보를 정확하게 설정합니다.
3. ftp_server.py를 실행하여 FTP Server를 시작합니다.
```bash
python ftp_server.py
```
FTP Server은 다음 두 가지 방법으로 실행할 수 있습니다.
 - nohup 명령어를 사용해 백그라운드 프로세스 방식으로 실행:
```bash
nohup python ftp_server.py >> /dev/null 2>&1 &
```
 - screen 명령어를 사용해 백그라운드에서 실행(screen 툴 설치 필요):
```bash
screen -dmS ftp
screen -r ftp
python ftp_server.py
#단축키 Ctrl+A+D를 사용해 홈 screen으로 전환하면 됩니다.
```

#### 실행 중지

- 직접 실행하거나 screen 방식으로 백그라운드에서 FTP Server를 실행하는 경우, 단축키 `Ctrl+C`를 사용하여 FTP Server 실행을 중지할 수 있습니다. 
- nohup 명령어로 실행한 경우 다음 방법을 사용해 중지할 수 있습니다.
```bash
ps -ef | grep python | grep ftp_server.py | grep -v grep | awk '{print $2}' | xargs -I{} kill {}
```


<a id="conf"></a>
## 구성 파일

FTP Server 툴의 설정 예시 파일은 `conf/vsftpd.conf.example`이며, 이름을 vsftpd.conf로 변경하고 복사하여 다음 항목을 설정합니다.
```conf
[COS_ACCOUNT_0]
cos_secretid = COS_SECRETID    # 사용자 SECRETID로 대체
cos_secretkey = COS_SECRETKEY  # 사용자 SECRETKEY로 대체
cos_bucket = examplebucket-1250000000
cos_region = region   # 사용자 버킷 리전으로 대체
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user0
ftp_login_user_name=user0   #사용자가 지정한 계정으로 대체
ftp_login_user_password=pass0   #사용자가 지정한 비밀번호로 대체
authority=RW                # 해당 사용자의 읽기/쓰기 권한 설정, R: 읽기 권한, W: 쓰기 권한, RW: 읽기/쓰기 권한 모두 부여
delete_enable=true		 # true: 해당 ftp 사용자에게 삭제 작업 허용(기본값), false: 해당 사용자 삭제 작업 불가

[COS_ACCOUNT_1]
cos_secretid = COS_SECRETID    # 사용자 SECRETID로 대체
cos_secretkey = COS_SECRETKEY  # 사용자 SECRETKEY로 대체
cos_bucket = examplebucket-1250000000
cos_region = region   # 사용자 버킷 리전으로 대체
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user1
ftp_login_user_name=user1   #사용자가 지정한 계정으로 대체
ftp_login_user_password=pass1   #사용자가 지정한 비밀번호로 대체
authority=RW               # 해당 사용자의 읽기/쓰기 권한 설정, R: 읽기 권한, W: 쓰기 권한, RW: 읽기/쓰기 권한 모두 부여
delete_enable=false        # true: 해당 ftp 사용자에게 삭제 작업 허용(기본값), false: 해당 사용자 삭제 작업 불가

[NETWORK]
# FTP Server가 특정 게이트웨이 또는 NAT에 있으며 해당 설정 항목을 통해 게이트웨이 IP 주소 또는 도메인을 FTP에 지정할 수 있습니다.
masquerade_address = XXX.XXX.XXX.XXX
# FTP Server의 수신 포트의 기본값은 2121로 설정되어 있으며, 방화벽에서 해당 포트에 대해 통과 허용해야 합니다(예: FTP Server 툴을 Tencent Cloud CVM에 배포하는 경우 CVM 보안 그룹에서 해당 포트의 통과를 허용해야 함).
listen_port = 2121			
# passive_port는 passive 모드에서 포트의 선택 범위를 설정할 수 있습니다. 기본값은 [60000, 65535] 구간에서 선택하며, 방화벽(예: CVM 보안 그룹)에서 해당 구간의 포트에 대해 통과를 허용해야 합니다.
passive_port = 60000,65535      


[FILE_OPTION]
# 기본적으로 단일 파일 크기는 최대 200G까지 설정할 수 있으며, 너무 크게 설정하는 것은 권장하지 않습니다.
single_file_max_size = 21474836480

[OPTIONAL]
# 다음 설정은 특별한 요구가 없는 경우 default로 설정하기를 권장합니다. 설정해야 하는 경우 합리적으로 판단하여 정수를 입력하십시오.
min_part_size       = default
upload_thread_num   = default
max_connection_num  = 512
max_list_file       = 10000                # ls 명령어는 최대로 출력 가능한 파일 수로, 너무 크게 설정하는 것은 권장하지 않습니다. 그렇지 않을 경우 Is 명령어 딜레이가 매우 높아집니다.
log_level           = INFO                 # 로그 출력 레벨 설정
log_dir             = log                  # 로그 저장 디렉터리 설정, 기본적으로 FTP Server 디렉터리의 log 디렉터리에 저장
```


>
>- 각 사용자를 서로 다른 bucket에 바인딩할 경우 [COS_ACCOUNT_X]의 section을 추가하기만 하면 됩니다.
각 COS_ACCOUNT_X의 section에 대한 설명은 다음과 같습니다.
 - 각 ACCOUNT의 사용자 이름(ftp_login_user_name)과 사용자 홈 디렉터리(home_dir)는 반드시 서로 달라야 하며 홈 디렉터리는 반드시 시스템에 실제 존재하는 디렉터리여야 합니다.
 - 각 COS FTP Server에서 동시 로그인 허용 사용자 수는 100명을 초과할 수 없습니다.
 - endpoint와 region은 동시에 적용될 수 없으며, 공유 클라우드 COS 서비스를 사용하는 경우 region 필드만 정확하게 입력하면 됩니다. endpoint는 개인화 배포 환경에 자주 사용됩니다. region과 endpoint를 모두 입력하는 경우 endpoint가 우선 적용됩니다.
>- 구성 파일의 OPTIONAL 옵션은 고급 사용자가 업로드 성능을 조정할 수 있도록 제공하는 옵션 항목입니다. 기기의 성능에 따라 멀티파트 업로드 크기 및 동시 접속 업로드의 스레드 수를 합리적으로 조정하여 업로드 속도를 더욱 향상시킬 수 있습니다. 일반 사용자는 조정할 필요 없으며, 기본값을 유지하면 됩니다.
또한 최대 연결 수 제한 옵션을 제공하며, 최대 연결 수를 제한하고 싶지 않은 경우 0으로 설정하면 최대 연결 수를 제한하지 않겠다는 의미입니다(단, 사용자 기기 성능에 따라 합리적으로 평가해야 함).
>- 구성 파일의 masquerade_address 설정 항목은 일반적으로 클라이언트에서 COS FTP Server 연결 시 사용하는 IP 주소입니다. 이에 대한 문의 사항이 있는 경우 [FTP Server 툴](https://intl.cloud.tencent.com/document/product/436/30588)의 FAQ 문서를 참조하십시오.
 - FTP Server에 여러 IP 주소가 있는 경우 ifconfig 명령어를 실행하여 외부 네트워크에 매핑된 ENI IP 10.xxx.xxx.xxx를 획득하였고, 매핑된 공인 IP를 119.xxx.xxx.xxx로 가정합니다. 이 때 FTP Server에 masquerade_address를 클라이언트가 server에 액세스할 때의 공인 IP(119.xxx.xxx.xxx)로 명시적으로 설정하지 않은 경우, FTP Server가 Passive 모드에서 클라이언트에 내부 네트워크 주소(10.xxx.xxx.xxx)를 사용하여 반환하게 됩니다. 이 때 클라이언트에서 FTP Server에 연결할 수 있게 되지만 정상적으로 클라이언트에 데이터 패킷을 반환하지 않게 됩니다. 따라서 일반적인 상황의 경우 masquerade_address를 클라이언트에서 Server 연결 시 사용하는 IP 주소로 설정하는 것을 권장합니다.
>- 구성 파일의 listen_port 설정 항목은 COS FTP Server의 수신 포트이며, 기본값은 2121입니다. passive_port 설정 항목은 COS FTP Server의 데이터 채널 수신 포트 범위이며, 기본값은 [60000, 65535] 구간에서 선택합니다. 클라이언트에서 COS FTP Server 연결 시 방화벽이 listen_port와 passive_port에 설정한 포트에 대해 통과를 허용해야 합니다.

## 빠른 체험

### Linux ftp 명령어를 사용하여 COS FTP Server 액세스

1. 다음 명령어 예시와 같이 Linux 명령 라인에서 명령어 `ftp [ip 주소] [포트 번호]`를 사용해 COS FTP Server에 연결합니다.
```sh
ftp 192.xxx.xx.103 2121
```
 - ftp 명령어에서 IP 설정은 해당 설정 예시 파일 `conf/vsftpd.conf.example`의 **masquerade_address** 설정 항목입니다. 본 예시에서는 IP를 192.xxx.xx.103으로 설정합니다.
 - ftp 명령어에서 포트 설정은 해당 설정 예시 파일 `conf/vsftpd.conf.example`의 **listen_port** 설정 항목입니다. 본 예시에서는 2121로 설정합니다.
2. 상기 명령어를 실행하면 설정해야 할 **Name**과 **Password** 항목이 나타나며 COS FTP Server 설정 항목 ftp_login_user_name과 ftp_login_user_password의 설정 내용을 입력하면 연결이 완료됩니다.
 - **Name**: 해당 설정 예시 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_name** 설정 항목(설정 필요)입니다.
 - **Password**: 해당 설정 예시 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_password** 설정 항목(설정 필요)입니다.

### FileZilla를 사용하여 COS FTP Server 액세스

1. [FileZilla 클라이언트](https://filezilla-project.org/)를 다운로드하고 설치합니다.
2. FileZilla 클라이언트에서 COS FTP Server의 액세스 정보를 설정한 후 [빠른 연결]을 클릭합니다.
 - **호스트(H): **해당 설정 예시 파일 conf/vsftpd.conf.example의 **masquerade_address** 설정 항목입니다. 본 예시에서는 ip를 192.xxx.xx.103으로 설정합니다.
>COS FTP Server가 특정 게이트웨이 또는 NAT에 있으며 해당 설정 항목을 통해 게이트웨이 IP 주소 또는 도메인을 COS FTP Server에 지정할 수 있습니다.
 - **사용자 이름(U): **해당 설정 예시 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_name** 설정 항목(설정 필요)입니다.
 - **비밀번호(W): **해당 설정 예시 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_password** 설정 항목(설정 필요)입니다.
 - **포트(P): **해당 설정 예시 파일 `conf/vsftpd.conf.example`의 **listen_port** 설정 항목입니다. 본 예시에서는 2121로 설정합니다.


## FAQ

FTP Server 툴 사용 중, 오류가 발생하거나 업로드 제한에 대한 문의사항이 있는 경우 [FTP Server 툴](https://intl.cloud.tencent.com/document/product/436/30588)의 FAQ를 참조하십시오.
