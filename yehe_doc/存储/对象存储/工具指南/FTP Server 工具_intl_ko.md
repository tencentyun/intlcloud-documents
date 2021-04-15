## 기능 개요

COS FTP Server는 FTP 프로토콜을 통해 COS에 저장된 객체 및 디렉터리에 대해 직접 파일 업로드, 다운로드, 삭제 및 폴더 생성 등의 작업을 할 수 있습니다. FTP Server 툴은 Python으로 구현되어 설치가 더욱 간편합니다.

## 기능 설명

**업로드 메커니즘**: 스트림 방식으로 업로드하며, 로컬 디스크를 거치지 않습니다. 표준 FTP 프로토콜에 따라 작업 디렉터리를 설정하면 되며, 실제 디스크 스토리지 용량을 점유하지 않습니다.
**다운로드 메커니즘**: 직접 스트림 방식으로 클라이언트에 반환합니다.
**디렉터리 메커니즘**: bucket이 전체 FTP Server의 루트 디렉터리가 되며, bucket에 몇 개의 서브 디렉터리를 구축할 수 있습니다.
**멀티 bucket 바인딩**: 동시에 여러 개의 bucket을 바인딩할 수 있습니다.
>?멀티 bucket 바인딩: 서로 다른 FTP Server 작업 경로(home_dir)를 통해 구현되므로, 서로 다른 bucket 및 사용자 정보 지정 시 반드시 home_dir이 달라야 합니다.

**삭제 작업 제한**: 새로운 FTP Server에서는 ftp 사용자별로 delete_enable 옵션을 설정하여 해당 FTP 사용자에게 파일 삭제 권한을 허용할 것인지 여부를 식별할 수 있습니다.
**지원하는 FTP 명령어**:put, mput, get, rename, delete, mkdir, ls, cd, bye, quite, size
**지원하지 않는 FTP 명령어**:append, mget(네이티브 mget 명령어를 지원하지 않으나, FileZilla 클라이언트와 같은 일부 Windows 클라이언트에서는 일괄 다운로드 가능)

>?FTP Server 툴은 현재 중단 시점부터 다시 전송하기 기능을 제공하지 않습니다.

## 사용하기

#### 시스템 환경

- 운영 체제: Linux. Tencent CentOS 시리즈 [CVM](https://intl.cloud.tencent.com/document/product/213)(권장 사용). 현재 Windows 시스템은 지원하지 않습니다.
- psutil 종속의 Linux 시스템 패키지: python-devel(또는python-dev, 각 Linux 릴리스 버전에 따라 이름이 다름). Linux의 패키지 관리 툴을 이용해 추가합니다. 예시: `yum install python-devel` 또는 `aptitude install python-dev`
- Python 인터프리터 버전: Python 2.7. [Python 설치 및 설정](https://intl.cloud.tencent.com/document/product/436/10866)을 참조하여 설치 및 설정하십시오.
>? FTP Server 툴은 Python 3을 지원하지 않습니다.
>
- 종속 패키지:
 - [cos-python-sdk-v5](https://pypi.org/project/cos-python-sdk-v5/) (≥1.6.5)
 - [pyftpdlib](https://pypi.org/project/pyftpdlib/) (≥1.5.2)
 - [psutil](https://pypi.org/project/psutil/)(>=5.6.1)


#### 사용 제한

COS XML 버전에 적용됩니다.

#### 설치 실행

FTP Server 툴 다운로드 주소: [cos-ftp-server](https://github.com/tencentyun/cos-ftp-server-V5). 설치 방법은 다음과 같습니다.

1. FTP Server 디렉터리로 이동한 후, setup.py를 실행해 FTP Server 및 관련 종속 라이브러리(인터넷 연결 필요)를 설치합니다.
```bash
python setup.py install   # 사용자의 계정 sudo 또는 root 권한이 필요할 수 있습니다.
```
2. 설정 예시 파일 `conf/vsftpd.conf.example`을 복사하여 이름을 `conf/vsftpd.conf`로 변경합니다. 본 문서의 [구성 파일](#conf) 섹션을 참조하여 bucket 및 사용자 정보를 올바르게 설정합니다.
3. ftp_server.py를 실행해 FTP Server를 실행합니다.
```bash
python ftp_server.py
```
다음 두 가지 방법으로도 FTP Server를 실행할 수 있습니다.
 - nohup 명령어를 사용하여 백그라운드 프로세스 방식을 통해 실행:
```bash
nohup python ftp_server.py >> /dev/null 2>&1 &
```
 - screen 명령어를 사용하여 백그라운드에서 실행(screen 툴 설치 필요):
```bash
screen -dmS ftp
screen -r ftp
python ftp_server.py
#단축키 Ctrl+A+D를 사용해 메인 screen으로 돌아오면 됩니다.
```

#### 실행 중지

- FTP Server를 직접 실행하거나 screen 방식으로 백그라운드에서 실행한 경우, 단축키 `Ctrl+C`를 사용해 FTP Server 실행을 중지할 수 있습니다. 
- nohup 명령어를 통해 실행한 경우, 다음과 같은 방식으로 실행을 중지할 수 있습니다.
```bash
ps -ef | grep python | grep ftp_server.py | grep -v grep | awk '{print $2}' | xargs -I{} kill {}
```


<a id="conf"></a>
## 구성 파일

FTP Server 툴의 구성 예시 파일은 `conf/vsftpd.conf.example`입니다. 해당 파일을 복사하여 이름을 vsftpd.conf로 변경하고, 다음 설정 항목에 따라 설정합니다.
```conf
[COS_ACCOUNT_0]
cos_secretid = COS_SECRETID    # 사용자의 SECRETID로 변경
cos_secretkey = COS_SECRETKEY  # 사용자의 SECRETKEY로 변경
cos_bucket = examplebucket-1250000000
cos_region = region   # 사용자의 버킷 리전으로 변경
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user0
ftp_login_user_name=user0   #사용자 정의한 계정으로 변경
ftp_login_user_password=pass0   #사용자 정의한 비밀번호로 변경
authority=RW                # 해당 사용자의 읽기/쓰기 권한 설정(R: 읽기 권한, W: 쓰기 권한, RW: 읽기/쓰기 권한 모두 부여)
delete_enable=true		 # true: 해당 ftp 사용자의 삭제 작업 허용(기본), false: 해당 사용자 삭제 작업 금지

[COS_ACCOUNT_1]
cos_secretid = COS_SECRETID    # 사용자의 SECRETID로 변경
cos_secretkey = COS_SECRETKEY  # 사용자의 SECRETKEY로 변경
cos_bucket = examplebucket-1250000000
cos_region = region   # 사용자의 버킷 리전으로 변경
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user1
ftp_login_user_name=user1   #사용자 정의한 계정으로 변경
ftp_login_user_password=pass1   #사용자 정의한 비밀번호로 변경
authority=RW               # 해당 사용자의 읽기/쓰기 권한 설정(R: 읽기 권한, W: 쓰기 권한, RW: 읽기/쓰기 권한 모두 부여)
delete_enable=false        # true: 해당 ftp 사용자의 삭제 작업 허용(기본), false: 해당 사용자 삭제 작업 금지

[NETWORK]
# FTP Server가 특정 게이트웨이 또는 NAT에 있는 경우, 이 설정 항목을 통해 게이트웨이의 IP 주소 또는 도메인을 FTP에 지정합니다.
masquerade_address = XXX.XXX.XXX.XXX
# FTP Server의 수신 포트는 기본적으로 2121로 설정되어 있습니다. 방화벽은 해당 포트를 허용해야 하므로 주의하십시오. 예를 들어 FTP Server 툴을 Tencent Cloud CVM에 배포하는 경우, CVM 보안 그룹에 해당 포트를 허용해야 합니다.
listen_port = 2121			
# passive_port는 passive 모드에서 포트의 선택 범위를 설정할 수 있으며, 기본적으로 [60000, 65535] 구간에서 선택합니다. 방화벽(예: CVM 보안 그룹)에 해당 구간의 포트를 허용해야 하므로 주의하십시오.
passive_port = 60000,65535      


[FILE_OPTION]
# 기본적으로 단일 파일 크기는 최대 200G까지 지원하며, 너무 크게 설정하는 것은 권장하지 않습니다.
single_file_max_size = 21474836480

[OPTIONAL]
# 다음 설정은 특별한 요구가 없다면 default 설정을 유지하시기 바랍니다. 설정이 필요한 경우 정수를 사용해 합리적으로 설정하십시오.
min_part_size       = default
upload_thread_num   = default
max_connection_num  = 512
max_list_file       = 10000                # ls 명령어는 열거할 파일의 최대 개수로, 너무 크게 설정하지 않는 것을 권장합니다. 너무 크게 설정하는 경우 Is 명령어 딜레이 시간이 길어집니다.
log_level           = INFO                 # 로그 출력 레벨 설정
log_dir             = log                  # 로그를 저장할 디렉터리 설정, 기본값: FTP Server 디렉터리의 log 디렉터리
```


>?
>- 각 사용자를 서로 다른 bucket에 바인딩하고 싶은 경우, [COS_ACCOUNT_X]의 section을 추가하면 됩니다.
서로 다른 COS_ACCOUNT_X의 section에 대한 설명은 다음과 같습니다.
>  - 각 ACCOUNT의 사용자 이름(ftp_login_user_name)과 사용자의 홈 디렉터리(home_dir)는 반드시 모두 달라야 하며, 홈 디렉터리는 시스템에 실제 존재하는 디렉터리여야 합니다.
>  - 각 COS FTP Server가 허용하는 동시 로그인 사용자 수는 100을 초과할 수 없습니다.
>  - endpoint와 region은 동시에 적용할 수 없습니다. 공유 클라우드 COS 서비스 사용 시 region 필드만 정확하게 입력하면 되고, endpoint는 사유화 배포 환경에 주로 사용됩니다. region과 endpoint를 모두 입력하는 경우 endpoint가 우선 적용됩니다.
>  - 구성 파일의 OPTIONAL 항목에서는 고급 사용자에게 업로드 성능을 조절할 수 있는 옵션을 제공합니다. 기기의 성능에 따라 업로드 멀티 파트 크기 및 동시 업로드 스레드 수를 합리적으로 조절할 수 있어 업로드 속도를 더욱 향상시킬 수 있습니다. 일반적으로 조절할 필요 없이 기본값으로 유지하면 됩니다.
또한 최대 연결 수의 제한 옵션을 제공합니다. 최대 연결 수를 제한하고 싶지 않은 경우, 0을 입력하면 최대 연결 수를 제한하지 않겠다는 의미입니다(단, 기기 성능에 따라 합리적으로 평가해야 함).
>- 구성 파일의 masquerade_address 설정 항목은 일반적으로 클라이언트에서 COS FTP Server 연결에 사용하는 IP 주소로 지정하는 것을 권장합니다. 관련 문의 사항은 [FTP Server 툴](https://intl.cloud.tencent.com/document/product/436/30588) FAQ 문서를 참조하십시오.
>  - FTP Server에 여러 개의 IP 주소가 있을 때, ifconfig 명령어를 실행하여 공인 네트워크에 매핑된 ENI IP 10.xxx.xxx.xxx를 획득하였고, 매핑된 공인 IP가 119.xxx.xxx.xxx라 가정합니다. 이때 FTP Server에서 masquerade_address가 클라이언트에서 server에 액세스 할 때의 공인 IP(119.xxx.xxx.xxx)임을 명시적으로 설정하지 않은 경우, FTP Server는 Passive 모드에서 내부 네트워크 주소(10.xxx.xxx.xxx)를 사용하여 클라이언트에 패킷을 반환하게 됩니다. 이 경우, 클라이언트에서 FTP Server에 연결할 순 있지만, 클라이언트에 데이터 패킷을 정상적으로 반환할 수 없게 됩니다. 따라서 일반적인 상황에서는 masquerade_address를 클라이언트에서 Server 연결 시 사용하는 IP로 설정하는 것을 권장합니다.
>- 구성 파일의 listen_port 설정 항목은 COS FTP Server의 수신 포트로, 기본적으로 2121로 설정되어 있습니다. passive_port 설정 항목은 COS FTP Server의 데이터 채널 수신 포트 범위이며, 기본적으로 [60000, 65535] 구간에서 선택합니다. 클라이언트에서 COS FTP Server 연결 시, listen_port와 passive_port에 설정한 포트를 반드시 방화벽에 허용해야 합니다.

## 빠른 실행

### Linux ftp 명령어를 사용하여 COS FTP Server에 액세스

1. Linux 명령 라인에서 명령어 `ftp [ip 주소] [포트 번호]`를 사용해 COS FTP Server에 연결합니다(예: 다음과 같은 명령어 실행).
```sh
ftp 192.xxx.xx.103 2121
```
 - ftp 명령어에서 예시 파일 `conf/vsftpd.conf.example`의 **masquerade_address**가 IP 설정 항목입니다. 본 예시에서는 IP를 192.xxx.xx.103으로 설정합니다.
 - ftp 명령어에서 예시 파일 `conf/vsftpd.conf.example`의 **listen_port**가 포트 설정 항목입니다. 본 예시에서는 2121로 설정합니다.
2. 위 명령어를 실행하면 **Name**과 **Password** 입력 항목이 나타납니다. COS FTP Server 설정 항목인 ftp_login_user_name과 ftp_login_user_password에서 설정한 내용을 입력하면 연결이 완료됩니다.
 - **Name**: 예시 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_name**이 해당 설정 항목입니다(설정 필요).
 - **Password**: 예시 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_password**가 해당 설정 항목입니다(설정 필요).

### FileZilla를 사용하여 COS FTP Server에 액세스

1. [FileZilla 클라이언트](https://filezilla-project.org/)를 다운로드 및 설치합니다.
2. FileZilla 클라이언트에서 COS FTP Server의 액세스 정보를 설정한 후 [즉시 연결]을 클릭합니다.
 - **호스트(H):**예시 파일 conf/vsftpd.conf.example의**masquerade_address**가 해당 설정 항목 입니다. 본 예시에서는 IP를 192.xxx.xx.103으로 설정합니다.
>!COS FTP Server가 특정 게이트웨이 또는 NAT에 있는 경우, 이 설정 항목을 통해 게이트웨이의 IP 주소 또는 도메인을 COS FTP Server에 지정합니다.
 - **사용자 이름(U):**예시 파일 `conf/vsftpd.conf.example`의**ftp_login_user_name**이 해당 설정 항목입니다. (설정 필요)
 - **비밀번호(W):**예시 파일 `conf/vsftpd.conf.example`의**ftp_login_user_password**가 해당 설정 항목입니다. (설정 필요)
 - **포트(P):**예시 파일 `conf/vsftpd.conf.example`의**listen_port**가 해당 설정 항목입니다. 본 예시에서는 2121로 설정합니다.


## FAQ

FTP Server 툴 사용 중 오류가 발생하거나 업로드 제한에 대해 문의 사항이 있는 경우 [FTP Server 툴](https://intl.cloud.tencent.com/document/product/436/30588) FAQ를 참조하십시오.
