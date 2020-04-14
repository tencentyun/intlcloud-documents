## 작업 시나리오

Tencent Cloud는 소프트웨어를 설치할 때 공식 소스의 액세스 속도가 느린 문제를 해결하기 위해 일부 소프트웨어에 캐시 서비스를 구축했습니다. Tencent Cloud 소프트웨어 원본 서버를 사용하여 종속 패키지의 설치 속도를 향상할 수 있습니다. 사용자가 자유롭게 서비스 아키텍처를 구축할 수 있도록 현재 Tencent Cloud 소프트웨어 원본 서버에서는 공용 네트워크 액세스 및 내부 네트워크를 지원합니다.
- 공용 네트워크 액세스 주소: `http://mirrors.cloud.tencent.com/`
- 내부 네트워크 액세스 주소: `http://mirrors.tencentyun.com/`

> 
> - 본 문서는 Tencent Cloud 소프트웨어 원본 서버 사이트의 공용 네트워크 액세스 주소를 예로 들어 Cloud Virtual Machine(CVM)에서 어떻게 Tencent Cloud 소프트웨어 원본 서버 내의 소프트웨어 보관소를 사용하는지 설명합니다. Tencent Cloud 소프트웨어 원본 서버에 내부 네트워크 방식을 통해 액세스해야 할 경우 공용 네트워크 액세스 주소를 **내부 네트워크 액세스 주소**로 교체하세요.
> - 본 문서에서 다루는 Tencent Cloud 소프트웨어 보관소 주소는 참고용이며, **Tencent Cloud 소프트웨어 원본 서버**에서 최신 주소를 획득 바랍니다.
>

### 주의 사항

Tencent Cloud 소프트웨어 원본 서버는 매일 각 소프트웨어 보관소의 공식 사이트에서 각 소프트웨어 리소스를 동기화합니다.

## 전제 조건

CVM에 로그인하였습니다.

## 작업 순서

### Tencent Cloud 미러 이미지 소스를 사용하여 pip 가속화
> 사용 전 CVM에 Python이 설치되었는지 확인하세요.
>
#### 소프트웨어 보관소 경로의 임시 사용
다음 명령어를 실행하여 Tencent Cloud PyPI 소프트웨어 보관소를 사용하여 pip를 설치합니다.
```
pip install -i  PyPI  소프트웨어 보관소가 위치한 디렉터리
```
예시, 사용할 PyPI 소프트웨어 보관소가 `http://mirrors.cloud.tencent.com/pypi/simple/17monip` 디렉터리에 있으면, 다음 명령어를 실행합니다.
```
pip install -i http://mirrors.cloud.tencent.com/pypi/simple/17monip
```

#### 기본 소프트웨어 보관소 경로로 설정
다음 명령어를 실행하여, `~/.pip/pip.conf` 파일의 `index-url` 매개변수를 Tencent Cloud 소프트웨어 보관소 경로로 수정합니다.

```
[global]
index-url = PyPI 소프트웨어 보관소가 위치한 디렉터리
trusted-host = 공용 네트워크/내부 네트워크 액세스 주소
```
예시, 사용할 PyPI 소프트웨어 보관소가 `http://mirrors.cloud.tencent.com/pypi/simple/17monip` 디렉터리에 있으면, 다음 명령어를 실행합니다.
```
[global]
index-url = http://mirrors.cloud.tencent.com/pypi/simple/17monip
trusted-host = mirrors.cloud.tencent.com
```

### Tencent Cloud 미러 이미지 소스를 사용하여 Maven 가속화
> 사용 전 CVM에서 JDK 및 Maven을 설치했는지 확인하세요.
>
1. Maven 의 `settings.xml` 구성 파일을 엽니다.
2. `<mirrors>...</mirrors>` 코드 블록을 찾은 후, 다음 내용을 `<mirrors>...</mirrors>` 코드 블록에 구성합니다.
```
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.cloud.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Tencent Cloud 미러 이미지 소스를 사용하여 NPM 가속화
> 사용 전 CVM에 Node.js 및 NPM이 설치되어 있는지 확인합니다.
>
다음 명령어를 실행하고, Tencent Cloud NPM 소프트웨어 보관소를 사용하여 NPM을 설치합니다.
```
npm config set registry http://mirrors.cloud.tencent.com/npm/
```

### Tencent Cloud 미러 이미지를 사용하여 Docker 가속화

#### TKE 클러스터에서 Tencent Cloud Docker 소프트웨어 보관소를 사용합니다.

수동으로 구성할 필요 없이 Tencent Kubernetes Engine(TKE ) 클러스터의 CVM 호스트가 노드를 생성할 때, 자동으로 Docker 서비스를 설치하고 Tencent Cloud 내부 네트워크 미러 이미지를 구성합니다.

#### CVM에서 Tencent Cloud의 Docker 소프트웨어 보관소 사용하기

> 사용 전 CVM에 Docker를 설치했는지 확인하세요.
> Docker 1.3.2 버전 이상부터 Docker Hub Mirror 메커니즘을 지원합니다. 1.3.2 버전 이상의 Docker를 설치하지 않았거나 Docker 버전이 낮으면 먼저 설치 또는 업그레이드 작업을 실행하세요.
> 
CVM의 운영 체제 유형에 맞는 작업 순서를 선택합니다.
- Ubuntu 14.04, Debian, CentOS 6, Fedora, openSUSE 등 운영 체제에 적용되며, 다른 버전의 운영 체제의 경우 세부 작업 순서에 약간의 차이가 있습니다.
 1. 다음 명령어를 실행하여 `/etc/default/docker` 구성 파일을 엽니다.
```
vim /etc/default/docker
```
 2. **i**를 눌러 편집 모드로 바꾸고, 다음 내용을 추가한 후 저장합니다.
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Centos 7 운영 체제에 적용됩니다.
 1. 다음 명령어를 실행하여 `/etc/sysconfig/docker` 구성 파일을 엽니다.
```
vim /etc/sysconfig/docker
```
 2. **i**를 눌러 편집 모드로 바꾸고, 다음 내용을 추가한 후 저장합니다.
```
OPTIONS='--registry-mirror=https://mirror.ccs.tencentyun.com'
```
- Boot2Docker를 설치한 Windows 운영 체제에 적용됩니다.
 1. Boot2Docker Start Shell에 접속하여 다음 명령어를 실행합니다.
```
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile  exit 
```
 2. Boot2Docker를 재시작합니다.

### Tencent Cloud 미러 이미지를 사용하여 MariaDB 가속화
> 다음 작업 순서는 CentOS 7을 예로 들며, 다른 운영 체제의 경우 세부 작업 순서에 약간의 차이가 있습니다.
>
1. 다음 명령어를 실행하여 `/etc/yum.repos.d/` 에 `MariaDB.repo` 파일을 생성합니다.
```
vi /etc/yum.repos.d/MariaDB.repo
```
2. **i**를 눌러 편집 모드로 바꾸고, 다음 내용을 입력한 후 저장합니다.
```
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.cloud.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. 다음 명령어를 실행하여 yum 캐시를 삭제합니다.
```
yum clean all
```
4. 다음 명령어를 실행하여 MariaDB를 설치합니다.
```
yum install MariaDB-client MariaDB-server
```

### Tencent Cloud 미러 이미지를 사용하여 MongoDB 가속화
> 다음 작업 순서는 MongoDB 4.0 버전 설치를 예로 하여, 다른 버전을 설치해야 할 경우, mirror 경로의 버전 번호를 변경하세요.
>
#### CentOS 및 Redhat 시스템의 CVM에서 Tencent Cloud  MongoDB 소프트웨어 보관소 사용

1. 다음 명령어를 실행하여 `/etc/yum.repos.d/mongodb.repo` 파일을 생성합니다.
```
vi /etc/yum.repos.d/mongodb.repo
```
2. **i**를 눌러 편집 모드로 바꾸고, 다음 내용을 입력한 후 저장합니다.
```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.cloud.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
2. 다음 명령어를 실행하여 MongoDB를 설치합니다.
```
yum install -y mongodb-org
```

#### Debian 시스템의 CVM의 Tencent Cloud MongoDB 소프트웨어 보관소 사용

1. Debian 버전에 따라, 아래와 같이 각각의 명령어를 실행하여 MongoDB GPG 공개키를 가져옵니다.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 다음 명령어를 실행하여 mirror 경로를 구성합니다.
```
#Debian 8
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 다음 명령어를 실행하여 패키지 리스트를 업데이트합니다.
```
sudo apt-get update
```
4. 다음 명령어를 실행하여 MongoDB를 설치합니다.
```
sudo apt-get install -y mongodb-org
```

#### Ubuntu 시스템의 CVM의 Tencent Cloud MongoDB 소프트웨어 보관소 사용

1. 다음 명령어를 실행하여 MongoDB GPG 공개키를 가져옵니다.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 다음 명령어를 실행하여 mirror 경로를 구성합니다.
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 다음 명령어를 실행하여 패키지 리스트를 업데이트합니다.
```
sudo apt-get update
```
4. 다음 명령어를 실행하여 MongoDB를 설치합니다.
```
sudo apt-get install -y mongodb-org
```

### Tencent Cloud 미러 이미지 소스를 사용하여 Rubygems 가속화
> 사용 전 CVM에 Ruby를 설치했는지 확인하세요.
>
다음 명령어를 실행하여 RubyGems 소스 주소를 수정합니다.
```
gem source -r https://rubygems.org/
gem source -a http://mirrors.cloud.tencent.com/rubygems/
```
