COS FTP 서버는 FTP 프로토콜을 통해 파일 업로드/다운로드, 삭제 및 폴더 생성 등을 포함하여 COS의 객체 및 디렉터리를 직접 조작하는 데 사용할 수 있습니다. FTP 서버 도구는 Python를 사용하여 설치를 보다 쉽게 만듭니다.

## 시작하기

### 운영 체제

운영 체제: Linux, Tencent CentOS 시리즈 [CVM](https://cloud.tencent.com/document/product/213)을 추천하여 Windows 시스템에서 일시적으로 지원되지 않습니다.

Python 인터프리터 버전: Python 2.7, [Python 설치 및 구성](https://cloud.tencent.com/document/product/436/10866)을 참조하여 설치 및 구성을 할 수 있습니다.

의존 패키지:
- cos-python-sdk-v5(>=1.6.5)
- pyftpdlib(>=1.5.2)


### 사용 제한

COS XML 버전에 적용됩니다.

### 설치 및 실행

링크 획득: [cos-ftp-server](https://github.com/tencentyun/cos-ftp-server-V5)

1. setup.py를 실행하여 FTP Server 및 관련 의존 라이브러리를 설치합니다(네트워킹 필요).
```bash
python setup.py install   # sudo 계정이나 root 권한이 필요합니다.
```
2. 구성 예시 파일 conf/vsftpd.conf.example를 복사하여 conf/vsftpd.conf로 명명합니다. [구성 파일](#conf) 섹션을 참조하여 버킷 및 사용자 정보를 정확하게 구성하십시오.
3. ftp_server.py를 실행하여 FTP Server를 시작합니다.
```bash
python ftp_server.py
```
이외에, FTP Server를 시작하는 방법은 다음과 같이 두 가지가 있습니다.
 - nohup 명령을 사용하여 백그라운드 프로세스로 시작합니다.
```bash
nohup python ftp_server.py >> /dev/null 2>&1 &
```
 - screen 명령을 사용하여 백그라운드에서 실행(screen 도구 설치 필요)합니다.
```bash
screen -dmS ftp
screen -r ftp
python ftp_server.py
#단축키를 사용하여 메인 화면으로 전환하면 됩니다.
Ctrl+A+D
```

### 중지

- 직접 실행 중이거나 screen 방식으로 백그라운드에서 실행 중인 FTP Server일 경우 단축키 `Ctrl+C`를 사용하여 FTP Serve의 실행을 중지할 수 있습니다.

- nohup 명령으로 시작할 경우 다음과 같이 중지할 수 있습니다.
```bash
ps -ef | grep python | grep ftp_server.py | grep -v grep | awk '{print $2}' | xargs -I{} kill {}
```


## 기능 설명

**업로드 메커니즘**: 스트림의 방식으로 업로드됩니다. 로컬 디스크에 남지 않고 표준 FTP 프로토콜에 따라 작업 디렉터리를 배치하면 됩니다. 실제적 디스크 스토리지 공간을 차지하지 않습니다.
**다운로드 메커니즘**: 직접 스트림의 방식으로 클라이언트로 반환됩니다.
**디렉터리 메커니즘**: 버킷은 전체 FTP Server의 루트 디렉터리로 아래에 여러 개의 하위 디렉터리를 만들 수 있습니다.
**여러 개의 버킷 바인딩**: 여러 개의 버킷을 동시에 바인딩할 수 있습니다.
**조작 제한 삭제**: 새로운 FTP 서버에서 각 ftp 사용자에 대해 `delete_enable` 옵션을 배치하여 해당 ftp 사용자의 파일 삭제를 허용할지 여부를 표시할 수 있습니다.

>?여러 개의 버킷 바인딩: 서로 다른 FTP 서버 작업 경로(`home_dir`)를 통해 구현되므로 서로 다른 버킷과 사용자 정보를 지정할 때 `home_dir`가 다르다는 것을 확보해야 합니다.


### 지원되는 FTP 명령

- put
- mput
- get
- rename
- delete
- mkdir
- ls
- cd
- bye
- quite
- size

### 지원되지 않는 FTP 명령

- append
- mget(원본 mget 명령은 지원되지 않지만 FileZilla 클라이언트와 같은 특정 Windows 클라이언트에서는 파일을 일괄적으로 다운로드할 수 있습니다.)

>?FTP 서버 도구로는 일시적으로 중단점에서 업로드를 다시 시작할 수 없습니다.

<a id="conf"></a>
## 파일 구성

 FTP 서버 도구의 구성 예시 파일은 conf/vsftpd.conf.example입니다. 복사하고 vsftpd.conf로 명명하며 다음과 같은 구성 항목에 따라 구성하십시오.
```conf
[COS_ACCOUNT_0]
cos_secretid = XXXXXX
cos_secretkey = XXXXXX
cos_bucket = {bucket name}-123
cos_region = ap-xxx
cos_protocol = https
#cos_endpoint = ap-xxx.myqcloud.com
home_dir = /home/user0
ftp_login_user_name=user0
ftp_login_user_password=pass0
authority=RW
delete_enable=true					 # true는 해당 FTP 사용자의 삭제 조작을 허용(기본값)하는 것이며, false는 해당 사용자의 삭제 조작을 금지하는 것입니다.

[COS_ACCOUNT_1]
cos_secretid = XXXX
cos_secretkey = XXXXX
cos_bucket = {bucket name}-123
cos_region = ap-xxx
cos_protocol = https
#cos_endpoint = ap-xxx.myqcloud.com
home_dir = /home/user1
ftp_login_user_name=user1
ftp_login_user_password=pass1
authority=RW
delete_enable=false

[NETWORK]
masquerade_address = XXX.XXX.XXX.XXX        # FTP 서버가 어떤 게이트웨이 또는 NAT 뒤에 위치하면 이 배치 항목을 통해 게이트웨이의 IP 주소 또는 도메인 이름을 FTP에 지정할 수 있습니다.
listen_port = 2121					   # FTP 서버의 수신 포트는 기본적으로 2121이며 방화벽은 해당 포트를 내보내야 합니다

passive_port = 60000,65535             # passive_port는 passive 모드에서 포트의 선택 범위를 설정할 수 있으며, 기본적으로(60000, 65535) 구간에서 선택됩니다

[FILE_OPTION]
# 기본적으로 단일 파일의 최대 크기는 200GB이며 너무 크게 설정하지 마십시오.
single_file_max_size = 21474836480

[OPTIONAL]
# 다음 설정은 특별히 필요하지 않으면 default 설정을 유지하는 것을 권장합니다. 설정이 필요하면, 하나의 정수를 합리적으로 기입해 주십시오.
min_part_size       = default
upload_thread_num   = default
max_connection_num  = 512
max_list_file       = 10000                # ls 명령의 최대적으로 열거할 수 있는 파일 수이므로 너무 크게 설정하지 마십시오. 그렇지 않으면 ls 명령이 매우 높게 지연됩니다.
log_level           = INFO                 # 로그 출력 클래스 설정
log_dir             = log                  # 로그의 저장 디렉터리를 설정합니다. 기본적으로 FTP 서버 디렉터리 아래의 log 디렉터리로 설정합니다.
```

각 사용자를 다른 버킷에 바인딩 하려면 `[COS_ACCOUNT_X]`의 section만 추가하면 됩니다.

서로 다른`COS_ACCOUNT_X`의 section에는 다음과 같은 설명 사항이 있습니다.

1. 각 ACCOUNT 아래의 사용자 이름 (`ftp_login_user_name`)과 사용자의 메인 디렉터리(`home_dir`)는 달라야 하며, 메인 디렉터리는 시스템에 존재하는 디렉터리여야 합니다.
2. 각 COS FTP 서버가 동시에 로그인할 수 있는 사용자 수는 100을 초과하면 안 됩니다.
3. `endpoint`와 `region`은 동시에 적용되지 않습니다. 공용 클라우드 COS 서비스를 사용하려면 `region` 필드를 정확하게 입력하면 됩니다. `endpoint`는 사유화 배치 환경에서 흔히 사용됩니다. `region`과 `endpoint`를 동시에 입력할 경우 `endpoint`가 우선적으로 적용됩니다.

구성 파일의 OPTIONAL 옵션은 고급 사용자에게 업로드 성능을 조정하는 데 사용할 수 있는 선택 가능 옵션으로, CVM 성능에 따라 업로드 멀티파트의 크기와 동시 발생한 업로드의 스레드를 합리적으로 조정하여 더 나은 업로드 속도를 획득할 수 있습니다. 일반적으로 사용자는 조정할 필요가 없고 기본값으로 유지하면 됩니다.
동시에 최대 연결 수에 대한 제한 옵션이 제공됩니다. 최대 연결 수를 제한하지 않으려면 0을 입력하면 됩니다. 즉, 최대 연결 수를 제한하지 않음을 표시할 수 있습니다(단, CVM의 성능에 따른 합리적 평가 필요).


## FAQ
FTP 서버 도구 사용 중 오류가 발생하거나 업로드 제한에 대한 질문이 있다면 [FTP 서버 도구 FAQ](https://cloud.tencent.com/document/product/436/30742)를 참조하십시오.
