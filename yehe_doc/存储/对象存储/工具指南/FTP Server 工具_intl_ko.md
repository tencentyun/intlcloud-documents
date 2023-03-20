## 기능 개요

COS FTP Server는 FTP 프로토콜을 통해 COS(Cloud Object Storage)에 저장된 객체 및 디렉터리에 대해 직접 파일 업로드, 다운로드, 삭제 및 폴더 생성 등의 작업을 할 수 있습니다. FTP Server 툴은 Python으로 구현되어 설치가 더욱 간편합니다.

## 기능 설명

**업로드 메커니즘**: 업로드된 파일을 로컬에 저장하지 않고 스트리밍합니다. 작업 디렉토리가 표준 FTP 프로토콜을 사용하여 구성되고 실제 디스크 스토리지 용량이 사용되지 않는 한 작동합니다.
**다운로드 메커니즘**: 다운로드한 파일이 직접 스트리밍되어 클라이언트로 반환됩니다.
**디렉터리 메커니즘**: bucket은 전체 FTP 서버의 루트 디렉터리 역할을 하며 bucket 아래에 여러 서브 디렉터리를 만들 수 있습니다.
**멀티 bucket 바인딩**: 동시에 여러 개의 bucket을 바인딩할 수 있습니다.
>? 멀티 bucket 바인딩: 여러 버킷을 다른 FTP Server 작업 경로(home_dir)를 통해 바인딩할 수 있습니다. 따라서 각 bucket과 사용자에게 고유한 home_dir이 할당되었는지 확인하십시오.
>
**삭제 제한**: ftp 사용자가 파일을 삭제할 수 있는지 여부를 식별하기 위해 새 FTP Server의 각 FTP 사용자에 대해 delete_enable 옵션을 구성할 수 있습니다.
**지원되는 FTP 명령:** put, mput, get, rename, delete, mkdir, ls, cd, bye, quite, size.
**지원되지 않는 FTP 명령:** append, mget(네이티브 mget 명령은 지원되지 않지만 FileZilla 클라이언트와 같은 특정 Windows 클라이언트에서는 일괄 다운로드가 허용됩니다)

>? FTP Server 툴은 체크포인트 재시작을 지원하지 않습니다.
>

## 사용하기

#### 시스템 환경

- 운영 체제: Linux. Tencent CentOS 시리즈의 [CVM](https://www.tencentcloud.com/document/product/213)을 권장합니다. 현재 Windows 시스템은 지원되지 않습니다.
- psutil 종속 Linux 패키지: 다른 Linux 배포판의 이름에 따라 python-devel 또는 python-dev입니다. `yum install python-devel` 또는 `aptitude install python-dev`와 같은 Linux 패키지 관리자를 사용하여 추가됩니다.
- Python 인터프리터 버전: Python 2.7. Python 설치 및 구성에 대한 자세한 내용은 [Python](https://intl.cloud.tencent.com/document/product/436/10866)을 참고하십시오.
>? FTP Server는 Python 3을 지원하지 않습니다.
>
- 종속 패키지:
 - [cos-python-sdk-v5](https://pypi.org/project/cos-python-sdk-v5/) (≥1.6.5)
 - [pyftpdlib](https://pypi.org/project/pyftpdlib/) (≥1.5.2)
 - [psutil](https://pypi.org/project/psutil/)(>=5.6.1)


#### 사용 제한

COS XML 버전에 적용됩니다.

#### 설치 및 운영

FTP Server 툴 다운로드 주소: [cos-ftp-server](https://github.com/tencentyun/cos-ftp-server-V5). 설치 단계는 다음과 같습니다.

1. FTP Server 디렉터리를 입력하고 setup.py를 실행하여 FTP Server와 종속 라이브러리를 설치합니다(네트워크 필요).
```bash
python setup.py install   # 귀하의 계정은 sudo를 사용하거나 root 권한이 있어야 합니다.
```
2. 구성 예시 파일 `conf/vsftpd.conf.example`을 복사하고 이름을 `conf/vsftpd.conf`로 지정합니다. bucket 및 사용자 정보를 올바르게 구성하려면 [구성 파일](#conf)을 참고하십시오.
3. ftp_server.py를 실행해 FTP Server를 실행합니다.
```bash
python ftp_server.py
```
다음 두 가지 방법으로도 FTP Server를 실행할 수 있습니다.
 - nohup 명령을 실행하여 백엔드 프로세스에서 시작합니다.
```bash
nohup python ftp_server.py >> /dev/null 2>&1 &
```
 - screen 명령을 실행하여 백엔드에서 실행합니다(screen 툴을 설치해야 함).
```bash
screen -dmS ftp
screen -r ftp
python ftp_server.py
#단축키 Ctrl+A+D를 사용해 메인 screen으로 돌아갑니다.
```

#### 실행 중지

- FTP Server를 직접 실행 중이거나 screen 명령으로 백엔드에서 실행 중인 경우 `Ctrl+C` 단축키 조합으로 중지할 수 있습니다. 
- FTP 서버가 nohup 명령으로 시작된 경우 다음 방법으로 중지할 수 있습니다.
```bash
ps -ef | grep python | grep ftp_server.py | grep -v grep | awk '{print $2}' | xargs -I{} kill {}
```


<a id="conf"></a>
## 구성 파일

FTP Server 툴의 구성 예시 파일은 `conf/vsftpd.conf.example`입니다. vsftpd.conf를 복사하고 이름을 지정한 후 다음과 같이 구성합니다.
```conf
[COS_ACCOUNT_0]
cos_secretid = COS_SECRETID    # 귀하의 SECRETID로 교체
cos_secretkey = COS_SECRETKEY  # 귀하의 SECRETKEY로 교체
cos_bucket = examplebucket-1250000000
cos_region = region   # 귀하의 버킷 리전으로 교체
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user0      # FTP를 마운트할 로컬 경로로 교체(기기에 실제로 존재하는 경로로 설정해야 하며, 소프트 링크는 지원하지 않음)
ftp_login_user_name=user1   # 사용자 지정 사용자 이름으로 대체
ftp_login_user_password=pass1   # 사용자 지정 사용자 비밀번호로 대체
authority=RW                # 사용자의 읽기/쓰기 권한(R: 읽기 권한, W: 쓰기 권한, RW: 읽기/쓰기 권한)
delete_enable=true # true는 FTP 사용자가 기본적으로 파일을 삭제할 수 있도록 허용, false는 사용자가 파일을 삭제하는 것을 금지

[COS_ACCOUNT_1]
cos_secretid = COS_SECRETID    # 귀하의 SECRETID로 교체
cos_secretkey = COS_SECRETKEY  # 귀하의 SECRETKEY로 교체
cos_bucket = examplebucket-1250000000
cos_region = region   # 귀하의 버킷 리전으로 교체
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user1     # FTP를 마운트할 로컬 경로로 교체(기기에 실제로 존재하는 경로로 설정해야 하며, 소프트 링크는 지원하지 않음)
ftp_login_user_name=user0   # 사용자 지정 사용자 이름으로 대체
ftp_login_user_password=pass1   # 사용자 지정 사용자 비밀번호로 대체
authority=RW               # 사용자의 읽기/쓰기 권한(R: 읽기 권한, W: 쓰기 권한, RW: 읽기/쓰기 권한)
delete_enable=false        # true는 FTP 사용자가 기본적으로 파일을 삭제할 수 있도록 허용, false는 사용자가 파일을 삭제하는 것을 금지

[NETWORK]
# FTP Server가 게이트웨이 또는 NAT 뒤에 있는 경우 이 섹션을 사용하여 게이트웨이의 IP 주소 또는 도메인 이름을 FTP 서버의 IP 주소로 지정할 수 있습니다.
masquerade_address = XXX.XXX.XXX.XXX
# FTP Server의 수신 포트는 기본적으로 2121입니다. WAF는 이 포트를 허용해야 합니다(예를 들어 Tencent Cloud CVM에 FTP Server를 배포하는 경우 CVM 보안 그룹에서 이 포트를 허용해야 함).
listen_port = 2121			
# passive_port는 passive 모드에서 사용 가능한 포트 범위를 설정하며 기본값은 [60000, 65535]입니다. WAF(예: CVM 보안 그룹)는 이 범위를 허용해야 합니다.
passive_port = 60000,65535      


[FILE_OPTION]
# 기본적으로 단일 파일의 최대 크기는 200G입니다. 한도를 초과하지 않는 것이 좋습니다.
single_file_max_size = 21474836480

[OPTIONAL]
# 다음 설정의 경우 특별히 필요한 경우가 아니면 default 설정을 사용하십시오. 필요한 경우 적절한 정수를 입력하십시오.
min_part_size       = default
upload_thread_num   = default
max_connection_num  = 512
max_list_file       = 10000                # ls 명령으로 나열할 최대 파일 수. 이 한도를 초과하는 것은 권장하지 않습니다. 그렇지 않으면 ls 명령의 긴 대기 시간이 발생합니다.
log_level           = INFO                 # 로그 출력 레벨 설정
log_dir             = log                  # 로그를 저장할 디렉터리 설정, 기본값: FTP Server 디렉터리 아래의 log
```


>?
>- 각 사용자를 서로 다른 bucket에 바인딩하고 싶은 경우, [COS_ACCOUNT_X]의 section을 추가하면 됩니다.
서로 다른 COS_ACCOUNT_X의 section에 대한 설명은 다음과 같습니다.
 - 각 ACCOUNT의 사용자 이름(ftp_login_user_name)과 사용자 홈 디렉터리(home_dir)는 반드시 서로 달라야 하며 홈 디렉터리는 반드시 시스템에 실제 존재하는 디렉터리여야 합니다.
 - 각 COS FTP Server에서 동시 로그인 허용 사용자 수는 100명을 초과할 수 없습니다.
 - endpoint와 region은 동시에 적용될 수 없으며, 공유 클라우드 COS 서비스를 사용하는 경우 region 필드를 올바르게 입력하십시오 endpoint는 개인화 배포 환경에서 일반적으로 사용됩니다. region과 endpoint를 모두 입력하는 경우 endpoint가 우선 적용됩니다.
>- 구성 파일의 OPTIONAL 부분은 고급 사용자를 위해 업로드 성능을 조정하는 데 사용됩니다. 서버 성능에 따라 부분 크기와 동시 업로드 스레드 수를 합리적으로 조정하여 최적의 업로드 속도를 얻을 수 있습니다. 일반 사용자는 조정 없이 기본 설정을 유지할 수 있습니다.
한편, 최대 연결 수에 대한 제한 옵션이 제공됩니다. 제한을 설정하지 않으려면 최대 연결 수에 제한이 없음을 의미하는 0을 입력합니다(서버 성능에 따라 합리적인 평가가 필요함).
>- 일반적으로 구성 파일의 masquerade_address 섹션에 클라이언트가 COS FTP Server에 연결하는 데 사용하는 IP 주소를 지정하는 것이 좋습니다. 관련 문의 사항은 [FTP Server 툴](https://intl.cloud.tencent.com/document/product/436/30588) FAQ 문서를 참고하십시오.
 - FTP Server에 둘 이상의 IP 주소가 있고 ifconfig 명령을 실행한 후 공중망 IP 119.xxx.xxx.xxx에 매핑되는 개인 ENI IP 10.xxx.xxx.xxx를 얻는다고 가정합니다. 이때 FTP Server가 masquerade_address를 클라이언트가 Server에 접속하기 위해 사용하는 공중망 IP(119.xxx.xxx.xxx)로 명시적으로 설정하지 않으면 Passive 모드의 FTP Server는 사설망 IP(10.xxx.xxx.xxx)를 사용하여 클라이언트에게 패킷을 반환할 수 있습니다. 결과적으로 클라이언트는 FTP Server에 연결할 수 있지만 클라이언트에 데이터 패킷을 제대로 반환할 수 없습니다. 따라서 일반적으로 masquerade_address를 클라이언트가 Server에 연결하는 데 사용하는 IP 주소로 설정하는 것이 좋습니다.
>- 구성 파일에서 listen_port는 COS FTP Server의 수신 포트를 설정하며 기본값은 2121입니다. passive_port는 COS FTP Server에 대한 데이터 채널 수신 포트의 범위를 설정하며 기본값은 [60000, 65535]입니다. 클라이언트가 COS FTP Server에 연결할 때 WAF가 이 두 섹션에서 구성된 포트를 허용하는지 확인하십시오.

## 빠른 실행

### Linux ftp 명령을 사용하여 COS FTP Server에 액세스

1. Linux ftp 클라이언트 설치
```sh
yum install -y ftp
```
2. Linux 명령 라인을 열고 `ftp [ip 주소] [포트 번호]`명령을 사용하여 COS FTP Server에 연결하십시오(예: 다음과 같은 명령 실행).
```sh
ftp 192.xxx.xx.103 2121
```
 - ftp 명령에서 IP 필드는 예시 구성 파일 `conf/vsftpd.conf.example`의 **masquerade_address** 섹션에 해당합니다. 이 예에서 IP는 192.xxx.xx.103으로 설정됩니다.
 - ftp 명령에서 포트 필드는 예시 구성 파일 `conf/vsftpd.conf.example`의 **listen_port** 섹션에 해당합니다. 이 예에서 포트는 2121로 설정됩니다.
3. 상기 명령어를 실행하면 **Name**과 **Password**가 입력된 것을 확인할 수 있습니다. COS FTP Server에 대한 ftp_login_user_name 및 ftp_login_user_password 섹션의 내용을 복사하여 붙여넣으면 연결이 성공합니다.
 - **Name**: 예시 구성 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_name**(구성 필요)에 해당합니다.
 - **Password**: 예시 구성 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_password**(구성 필요)에 해당합니다.

### FileZilla를 사용하여 COS FTP Server에 액세스

1. [FileZilla 클라이언트](https://filezilla-project.org/)를 다운로드 및 설치합니다.
2. FileZilla 클라이언트에서 COS FTP Server에 대한 액세스 정보를 구성한 후 **빠른 연결**을 클릭하십시오.
 - **호스트(H):** 예시 구성 파일 conf/vsftpd.conf.example의 **masquerade_address**에 해당합니다. 이 예에서 IP는 192.xxx.xx.103으로 설정됩니다.
>!COS FTP Server가 게이트웨이 또는 NAT 뒤에 있는 경우 이 섹션을 사용하여 게이트웨이의 IP 주소 또는 도메인 이름을 서버의 IP 주소로 지정할 수 있습니다.
 - **사용자 이름(U):** 예시 구성 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_name**(구성 필요)에 해당합니다.
 - **비밀번호(W):** 예시 구성 파일 `conf/vsftpd.conf.example`의 **ftp_login_user_password**(구성 필요)에 해당합니다.
 - **포트(P):** 예시 구성 파일 `conf/vsftpd.conf.example`의 **listen_port**에 해당합니다. 이 예시에서 포트는 2121로 설정됩니다.



## FAQ

FTP Server를 사용하는 동안 오류가 발생하거나 업로드 제한에 대해 문의 사항이 있는 경우 [FTP Server 툴](https://intl.cloud.tencent.com/document/product/436/30588) FAQ를 참고하십시오.
