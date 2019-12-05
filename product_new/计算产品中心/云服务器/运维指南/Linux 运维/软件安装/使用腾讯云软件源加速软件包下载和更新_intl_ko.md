## 작업 시나리오

Tencent Cloud는 소프트웨어를 설치할 때 공식 소스의 액세스 속도가 느린 문제를 해결하기 위해 일부 소프트웨어에 캐시 서비스를 구축했습니다. Tencent Cloud 소프트웨어 원본 서버를 사용하여 종속 패키지의 설치 속도를 향상할 수 있습니다. 사용자가 자유롭게 서비스 아키텍처를 구축할 수 있도록 현재 Tencent Cloud 소프트웨어 원본 서버에서는 공용 네트워크에 액세스 및 개인 네트워크에 액세스하는 것을 지원합니다.
- 공용 네트워크 액세스 주소: `http://mirrors.cloud.tencent.com/`
- 개인 네트워크 액세스 주소: `http://mirrors.tencentyun.com/`

> 
> - 본 문서는 Tencent Cloud 원본 서버 사이트의 공용 네트워크 액세스 주소를 예로 들어 클라우드 서버에서 Tencent Cloud 소프트웨어 소스에 있는 소프트웨어 소스를 어떻게 사용하는지 설명합니다. Tencent Cloud 소프트웨어 소스 원본 서버를 개인 네트워크 방식을 통해 액세스해야 할 경우 공용 네트워크 액세스 주소**를 개인 네트워크 액세스 주소**로 교환하십시오.
> - 본 문서에서 다루는 Tencent Cloud 소프트웨어 소스 주소는 참조용으로만 제공되며, **Tencent Cloud 소프트웨어 원본 서버**에서 최신 주소를 얻으십시오.
>

### 주의 사항

Tencent Cloud 원본 서버는 매일 각 소프트웨어 소스의 공식 사이트에서 각 소프트웨어 리소스를 동기화합니다. 

## 전제 조건

클라우드 서버에 로그인하십시오. 

## 작업 절차

### Tencent Cloud 미러 이미지 소스의 가속 pip 사용
> 사용 전 클라우드 서버에 Python이 설치하였는지 확인하십시오. 
>
#### 소프트웨어 소스 경로의 임시 사용
커맨드를 실행하기 전 Tencent Cloud PyPI 소프트웨어 소스를 사용하여 pip를 설치하십시오.
```
pip install -i  PyPI  소프트웨어 소스가 있는 디렉터리
```
예를 들어, 사용하시는 PyPI 소프트웨어 소스가  `http://mirrors.cloud.tencent.com/pypi/simple/17monip` 디렉터리에 있을 경우，다음 커맨드를 실행하십시오.
```
pip install -i http://mirrors.cloud.tencent.com/pypi/simple/17monip
```

#### 기본 소프트웨어 소스 경로로 설정
다음 커맨드를 실행하여，`~/.pip/pip.conf` 파일의 `index-url` 파라미터를 Tencent Cloud 소프트웨어 소스 경로로 수정하십시오.

```
[global]
index-url = PyPI 소프트웨어 소스가 있는 디렉터리
trusted-host = 공용 네트워크/개인 네트워크 액세스 주소
```
예를 들어, 사용하는 PyPI 소프트웨어 소스가  `http://mirrors.cloud.tencent.com/pypi/simple/17monip` 디렉터리에 있을 경우 다음 커맨드를 실행하십시오.
```
[global]
index-url = http://mirrors.cloud.tencent.com/pypi/simple/17monip
trusted-host = mirrors.cloud.tencent.com
```

### Tencent Cloud 미러 이미지 소스를 사용하여  Maven 가속화
> 사용 전 클라우드 서버에서 JDK 및 Maven를 설치하였는지 확인하십시오.
>
1. Maven 의 `settings.xml` 구성 파일을 여십시오.
2. `<mirrors>...</mirrors>` 코드블럭을 찾은 후, 다음 내용을 `<mirrors>...</mirrors>` 코드블럭에 구성하십시오.
```
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.cloud.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Tencent Cloud 미러 이미지 소스를 사용하여 NPM 가속화
> 사용 전 클라우드 서버에 Node.js 및 NPM이 설치되어 있는지 확인하십시오.
>
다음 커맨드를 실행하여 Tencent Cloud NPM 소프트웨어 소스를 사용하여 NPM을 설치하십시오.
```
npm config set registry http://mirrors.cloud.tencent.com/npm/
```

### Tencent Cloud 미러 이미지를 사용하여 Docker 가속화

#### TKE 클러스터에서 Tencent Cloud Docker 소프트웨어 소스를 사용하십시오.

수동으로 구성할 필요 없이 TKE (Tencent Kubernetes Engine) 클러스터의 클라우드 서버 CVM은 노드를 생성할 때, 자동으로 Docker 서비스를 설치하고 Tencent Cloud 개인 네트워크 미러 이미지를 구성합니다. 

#### 클라우드 서버에서 Tencent Cloud의 Docker 소프트웨어 소스 사용하기

> 사용 전 클라우드 서버에 Docker를 설치하였는지 확인하십시오.
> Docker 1.3.2 에디션 이상에서 Docker Hub Mirror 메커니즘을 지원합니다. 1.3.2 에디션 이상의 Docker를 설치하지 않았거나 Docker 에디션이 낮으면 설치 또는 업그레이드 작업을 실행하십시오.
> 
클라우드 서버의 작업 시스템 유형에 따라 다른 작업 절차를 선택하십시오.
- Ubuntu 14.04, Debian, CentOS 6, Fedora, openSUSE 등 시스템 작업에 적합하며, 다른 에디션의 시스템 작업의 자세한 작업 절차는 다소 차이가 있습니다.
 1. 다음 커맨드를 실행하여 `/etc/default/docker` 구성 파일을 여십시오.
```
vim /etc/default/docker
```
 2. **i**를 눌러 편집 모드로 바꾸고 다음 콘텐츠를 추가하여 저장하십시오.
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Centos 7 작업 시스템에 적합합니다:
 1. 다음 커맨드를 실행하여 `/etc/sysconfig/docker` 구성 파일을 여십시오. 
```
vim /etc/sysconfig/docker
```
 2. **i**를 눌러 편집 모드로 바꾸고 다음 콘텐츠를 추가하여 저장하십시오.
```
OPTIONS='--registry-mirror=https://mirror.ccs.tencentyun.com'
```
- Boot2Docker를 설치한 Windows 작업 시스템에 적합합니다.
 1. Boot2Docker Start Shell에 들어가 다음 커맨드를 실행하십시오.
```
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile  exit 
```
 2. Boot2Docker를 재시작하십시오.

### Tencent Cloud 미러 이미지를 사용하여 MariaDB 가속화
> 다음 작업 절차는 CentOS 7을 예로 하며，다른 작업 시스템의 자세한 작업 절차는 다소 차이가 있을 수 있습니다.
>
1. 다음 커맨드를 실행하여 `/etc/yum.repos.d/` 에서 `MariaDB.repo` 파일을 생성하십시오.
```
vi /etc/yum.repos.d/MariaDB.repo
```
2. **i**를 눌러 편집 모드로 바꾸고 다음 콘텐츠를 작성하고 저장하십시오.
```
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.cloud.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. 다음 커맨드를 실행하여 yum 캐시를 삭제하십시오.
```
yum clean all
```
4. 다음 커맨드를 실행하여 MariaDB를 설치하십시오.
```
yum install MariaDB-client MariaDB-server
```

### Tencent Cloud 미러 이미지를 사용하여 MongoDB 가속화
> 다음 작업 절차는 MongoDB 4.0 에디션 설치를 예로 하여, 다른 에디션을 설치해야 할 경우, mirror 경로의 에디션 번호를 변경하십시오.
>
#### CentOS 및 Redhat 시스템의 클라우드 서버에서 Tencent Cloud  MongoDB 소프트웨어 소스 사용

1. 다음 커맨드를 실행하여 `/etc/yum.repos.d/mongodb.repo` 파일을 작성하십시오.
```
vi /etc/yum.repos.d/mongodb.repo
```
2. **i**를 눌러 편집 모드로 바꾸고 다음 콘텐츠를 작성하고 저장하십시오.
```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.cloud.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
2. 다음 커맨드를 실행하여 MongoDB를 설치하십시오.
```
yum install -y mongodb-org
```

#### Debian 시스템의 클라우드 서버의 Tencent Cloud MongoDB 소프트웨어 소스 사용

1. Debian 에디션이 다르므로, 다음의 다른 커맨드를 실행하여 MongoDB GPG 공개키를 가져오십시오.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 다음 커맨드를 실행하여 mirror 경로를 구성하십시오.
```
#Debian 8
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 다음 커맨드를 실행하여 소프트웨어 패키지 리스트를 업데이트하십시오.
```
sudo apt-get update
```
4. 다음 커맨드를 실행하여 MongoDB를 설치하십시오.
```
sudo apt-get install -y mongodb-org
```

#### Ubuntu 시스템의 클라우드 서버 Tencent Cloud MongoDB 소프트웨어 소스 사용

1. 다음 커맨드를 실행하여 MongoDB GPG 공개키를 가져오십시오.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 다음 커맨드를 실행하여 mirror 경로를 구성하십시오.
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 다음 커맨드를 실행하여 소프트웨어 패키지 리스트를 업데이트하십시오.
```
sudo apt-get update
```
4. 다음 커맨드를 실행하여 MongoDB를 설치하십시오.
```
sudo apt-get install -y mongodb-org
```

### Tencent Cloud 미러 이미지 소스를 사용하여 Rubygems 가속화
> 사용 전 클라우드 서버에 Ruby를 설치하였는지 확인하십시오.
>
다음 커맨드를 실행하여 RubyGems 소스 주소를 수정하십시오.
```
gem source -r https://rubygems.org/
gem source -a http://mirrors.cloud.tencent.com/rubygems/
```
