### 컨테이너에 bash가 없으면 어떻게 해야 합니까?

컨테이너에 bash가 없으면 명령 라인에 실행하려는 명령을 입력합니다. 그러면 명령의 결과가 화면에 표시됩니다. 명령 라인은 자동 완성과 같은 특정 기능이 없는 단순한 bash로 간주할 수 있습니다. 계속 진행하기 전에 bash 설치 명령을 실행하는 것이 좋습니다.

### apt-get을 사용한 소프트웨어 설치가 왜 이렇게 느린가요?
`apt-get`을 사용하여 소프트웨어를 설치하는 데 너무 많은 시간이 걸리는 경우 중국 외부의 소프트웨어 소스에 대한 서버 액세스가 느리기 때문일 수 있습니다. 다양한 운영 체제의 컨테이너에 대한 가속화 솔루션을 제공합니다. 필요한 경우 솔루션을 선택할 수 있습니다.

#### 주의사항
가속 솔루션을 선택하기 전에 아래 지침에 따라 컨테이너의 운영 체제를 확인하십시오.
 - Ubuntu: `cat /etc/lsb-release`를 실행하여 `/etc/lsb-release` 파일이 있는지 확인합니다.
 - CentOS: `cat /etc/redhat-release`를 실행하여 `/etc/redhat-release` 파일이 있는지 확인합니다.
 - Debian: `cat /etc/debian_version`을 실행하여 `/etc/debian_version` 파일이 있는지 확인합니다.

#### 솔루션<span id="solve"></span>

##### Ubuntu 16.04
Ubuntu 16.04를 실행하는 컨테이너의 경우 터미널에서 다음 명령을 실행하여 apt 소스를 Tencent Cloud 소스 서버로 설정합니다.
```shell
cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
ENDOF
```

##### CentOS 7

CentOS 7을 실행하는 컨테이너의 경우 아래 지침에 따라 소스 주소를 직접 변경하여 설치 속도를 높입니다.
1. 컨테이너에서 다음 코드를 복사하고 실행합니다.
```shell
cat << ENDOF > /etc/yum.repos.d/CentOS-Base.repo
[os]
name=Qcloud centos os - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/os/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
[updates]
name=Qcloud centos updates - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/updates/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[centosplus]
#name=Qcloud centosplus - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/centosplus/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[cloud]
#name=Qcloud centos contrib - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/cloud/$basearch/openstack-kilo/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[cr]
#name=Qcloud centos cr - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/cr/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
[extras]
name=Qcloud centos extras - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/extras/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[fasttrack]
#name=Qcloud centos fasttrack - \basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/fasttrack/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
ENDOF
```
2. 다음 명령을 실행하여 YUM 캐시를 지우고 다시 작성하십시오.
```
yum clean all && yum clean metadata && yum clean dbcache && yum makecache
```

##### Debian

Debian을 실행하는 컨테이너의 경우 터미널에서 다음 명령을 실행하여 apt 소스를 Tencent Cloud 소스 서버로 설정합니다.
```shell
cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/debian stretch main contrib non-free
deb http://mirrors.tencentyun.com/debian stretch-updates main contrib non-free
deb http://mirrors.tencentyun.com/debian-security stretch/updates main

deb-src http://mirrors.tencentyun.com/debian stretch main contrib non-free
deb-src http://mirrors.tencentyun.com/debian stretch-updates main contrib non-free
deb-src http://mirrors.tencentyun.com/debian-security stretch/updates main
ENDOF
```

#### 결론

컨테이너에서 소스 주소를 직접 변경하는 것은 임시 솔루션입니다. 컨테이너 스케쥴링이 변경되면 변경 사항이 무효화됩니다. 따라서 이미지 생성 시 다음과 같은 방법으로 이 문제를 해결할 것을 권장합니다.

컨테이너 이미지 생성을 위해 Dockerfile 파일의 RUN 필드에 해당 운영 체제용 [솔루션](#solve)에서 제공하는 소스 주소를 추가합니다. 예를 들어 Ubuntu 운영 체제를 실행하는 이미지의 Dockerfile 파일에 다음 코드를 추가합니다.
```shell
RUN cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
#deb http://mirrors.tencentyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
#deb http://mirrors.tencentyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
#deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
#deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-backports main restricted universe multiverse
ENDOF
```



### 컨테이너에 로그인한 후 vim 및 netstat와 같은 도구를 찾을 수 없으면 어떻게 해야 합니까?

apt-get install vim 및 apt-get install net-tools(CentOS에서 yum install vim 실행)와 같은 명령을 실행하여 필요한 도구를 다운로드합니다.

### apt-get install 명령을 실행할 때 도구를 찾을 수 없으면 어떻게 해야 합니까?

다음과 같이 소프트웨어 프로그램을 설치합니다.
1. 다음 명령을 실행하여 소프트웨어 목록을 업데이트합니다.
```
apt-get update
```
2. 다음 명령을 실행하여 소프트웨어 프로그램을 설치합니다(CentOS에서 yum updateinfo 실행).
```
apt-get install
```

### 컨테이너에서 사내(in-house) 툴을 어떻게 사용합니까?

원격 터미널 페이지로 이동하여 오른쪽 하단 모서리에 있는 파일 도우미를 클릭하고 도구를 업로드합니다.

### 로컬 분석을 위해 dump 또는 로그와 같은 라이브 파일을 어떻게 업로드합니까?

원격 터미널 페이지로 이동하여 오른쪽 하단 모서리에 있는 파일 도우미를 클릭하고 파일을 업로드합니다.

### 파일을 컨테이너에 업로드하거나 로컬 시스템에 파일을 다운로드할 수 없는 이유는 무엇입니까?

이 문제는 tar 프로그램이 컨테이너 이미지에 포함되어 있지 않은 경우에 발생합니다. 이를 수정하려면 apt-get install vim 또는 apt-get install net-tools(CentOS에서 yum install vim 실행)를 실행하여 tar 프로그램을 설치하고 다시 시도하십시오.

### 이전에 설치한 도구를 찾을 수 없는 이유는 무엇입니까?

Kubernetes가 컨테이너를 다시 스케쥴링하면 이미지를 가져와서 새 컨테이너를 만들고 이미지에 없는 도구는 새 컨테이너에 설치되지 않습니다. 따라서 이미지를 만들 때 몇 가지 일반적인 문제 해결 도구를 설치하는 것이 좋습니다.

### 콘솔에서 텍스트를 복사하려면 어떻게 합니까?

강조 표시하고 복사하여 텍스트를 복사할 수 있습니다.

### 복사한 텍스트를 어떻게 붙여넣나요?

Shift + Insert를 눌러 복사한 텍스트를 붙여넣습니다.

### 연결이 끊어진 이유는 무엇입니까?

이는 컨테이너 상태를 수정하는 다른 페이지의 컨테이너 또는 CVM에서 일부 작업을 수행하거나 현재 페이지가 3분 이상 유휴 상태로 유지될 때 발생합니다. 두 경우 모두 서버는 연결을 끊습니다.

### top과 같은 명령을 실행할 때 TERM environment variable not set 오류가 발생하면 어떻게 해야 합니까?

export TERM linux를 실행합니다.

### 긴 절대 경로가 있는 디렉터리를 입력할 때 bash 프롬프트에 ‘<’와 경로의 일부만 표시되는 이유는 무엇입니까?

bash 프롬프트는 기본적으로 ‘username@hostname 현재 디렉터리’를 표시하도록 설정되어 있습니다. 현재 경로가 너무 길면 bash는 기본적으로 ‘<’와 경로의 마지막 부분만 표시합니다.

