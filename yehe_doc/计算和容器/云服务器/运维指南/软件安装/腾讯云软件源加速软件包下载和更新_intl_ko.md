## 개요

종속성을 설치할 때 공식 소스에 대한 느린 액세스 문제를 해결하기 위해 Tencent Cloud는 일부 소프트웨어에 대한 캐시 서비스를 설정했습니다. 현재 공중망 액세스 및 사설망 액세스를 지원하는 Tencent Cloud 소프트웨어 리포지토리를 사용하여 종속성 설치를 가속화할 수 있습니다.
- 공중망 액세스 주소: `http://mirrors.tencent.com`
- 사설망 액세스 주소: `http://mirrors.tencentyun.com/`

<dx-alert infotype="explain" title="">
- 본문은 Tencent Cloud 소프트웨어 저장소의 공중망 액세스 주소를 예로 들어 CVM에서 Tencent Cloud 소프트웨어 저장소의 소프트웨어 소스를 사용하는 방법을 소개합니다. 사설망으로 리포지토리에 액세스하는 경우 공중망 액세스 주소를 **사설망 액세스 주소로 바꾸십시오**.
- 본문에 사용된 소스 주소는 참고용입니다. **Tencent Cloud 소프트웨어 저장소**에서 최신 주소를 얻으십시오.
</dx-alert>


## 주의 사항

Tencent Cloud 소프트웨어 리포지토리는 각 소프트웨어 소스의 공식 웹사이트에서 하루에 한 번 소프트웨어 소스를 업데이트합니다.

## 전제 조건

CVM에 로그인되어 있어야 합니다.

## 작업 단계

### Tencent Cloud 이미지 소스를 사용하여 pip 가속화


<dx-alert infotype="notice" title="">
Tencent Cloud 이미지 소스를 사용하기 전에 CVM에 Python이 설치되어 있는지 확인하십시오.
</dx-alert>


#### 소프트웨어 소스 경로를 일시적으로 사용
다음 명령을 실행하여 Tencent Could PyPI를 사용하여 pip를 설치합니다.
```shell
pip install pip -i  PyPI가 있는 디렉터리
```
예를 들어 17monip 패키지를 설치하려고 하며 사용해야 하는 PyPI가 `http://mirrors.tencent.com/pypi/simple` 디렉터리에 있는 경우 다음 명령을 실행합니다.
```shell
pip install 17monip -i http://mirrors.tencent.com/pypi/simple --trusted-host mirrors.tencent.com 
```

#### 기본 소프트웨어 소스 경로 설정
다음 명령을 실행하여 `~/.pip/pip.conf` 파일의 `index-url` 매개변수를 Tencent Cloud 소프트웨어 리포지토리의 소스 경로로 수정합니다.

```shell
[global]
index-url = PyPI가 있는 디렉터리
trusted-host = 공중망/사설망 액세스 주소
```
예를 들어, 사용해야 하는 PyPI가 `http://mirrors.tencent.com/pypi/simple` 디렉터리에 있는 경우 다음 명령을 실행합니다.
```shell
[global]
index-url = http://mirrors.tencent.com/pypi/simple
trusted-host = mirrors.tencent.com
```

### Tencent Cloud 이미지 소스를 사용하여 Maven 가속화


<dx-alert infotype="notice" title="">
Tencent Cloud 이미지 소스를 사용하기 전에 CVM에 JDK 및 Maven이 설치되어 있는지 확인하십시오.
</dx-alert>


1. Maven 의 `settings.xml` 구성 파일을 여십시오.
2. `<mirrors>...</mirrors>` 코드 블록을 찾아 다음 내용을 `<mirrors>...</mirrors>` 코드 블록에 구성합니다.
```xml
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Tencent Cloud 이미지 소스를 사용하여 NPM 가속화


<dx-alert infotype="notice" title="">
Tencent Cloud 이미지 소스를 사용하기 전에 CVM에 Node.js 및 NPM이 설치되어 있는지 확인하십시오.
</dx-alert>


다음 명령을 실행하여 Tencent Cloud NPM을 사용하여 NPM을 설치합니다.
```shell
npm config set registry http://mirrors.tencent.com/npm/
```

### Tencent Cloud 이미지 소스를 사용하여 Docker 가속화

#### TKE 클러스터에서 Tencent Cloud Docker 사용

수동 구성이 필요하지 않습니다. Tencent Kubernetes Engine(TKE) 클러스터의 CVM이 노드를 생성하면 Docker가 자동으로 설치되고 Tencent Cloud 사설망 이미지로 구성됩니다.

#### CVM에서 Tencent Cloud Docker 사용



<dx-alert infotype="notice" title="">
Tencent Cloud Docker를 사용하기 전에 CVM에 Docker가 설치되어 있는지 확인하십시오.
Docker 1.3.2 이상 버전만 Docker Hub Mirro 메커니즘을 지원합니다. Docker 1.3.2 이상 버전을 설치하지 않았거나 설치된 버전이 너무 오래된 경우 먼저 설치하거나 업그레이드하십시오.
</dx-alert>


CVM의 운영 체제에 따라 다른 작업 단계를 선택하십시오.
- 다음 단계는 Ubuntu 14.04, Debian, CentOS 6, Fedora, openSUSE 및 기타 운영 체제에 대한 것입니다. 운영 체제의 다른 버전에 대한 구체적인 단계는 다를 수 있습니다.
 1. 다음 명령을 실행하여 `/etc/default/docker` 구성 파일을 엽니다.
```shell
vim /etc/default/docker
```
 2. **i**를 눌러 편집 모드로 전환하고 다음 내용을 입력한 후 저장합니다.
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Centos 7 운영 체제의 경우:
 1. 다음 명령을 실행하여 `/etc/docker/daemon.json` 구성 파일을 엽니다.
```shell
vim /etc/docker/daemon.json
```
 2. **i**를 눌러 편집 모드로 전환하고 다음 내용을 입력한 후 저장합니다.
```json
{
   "registry-mirrors": [
       "https://mirror.ccs.tencentyun.com"
  ]
}
```
- Boot2Docker가 설치된 Windows의 경우:
 1. Boot2Docker Start Shell에 액세스하고 다음 명령을 실행합니다.
```shell
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile  exit 
```
 2. Boot2Docker를 다시 시작합니다.

### Tencent Cloud 이미지를 사용하여 MariaDB 가속화


<dx-alert infotype="explain" title="">
다음 단계에서는 CentOS 7을 예로 들어 설명합니다. 특정 단계는 운영 체제에 따라 다릅니다.
</dx-alert>


1. 다음 명령을 실행하여 `/etc/yum.repos.d/` 아래에 `MariaDB.repo` 파일을 생성합니다.
```shell
vi /etc/yum.repos.d/MariaDB.repo
```
2. **i**를 눌러 편집 모드로 전환하고 다음 내용을 입력한 후 저장합니다.
```shell
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. 다음 명령을 실행하여 yum 캐시를 비웁니다.
```shell
yum clean all
```
4. 다음 명령을 실행하여 MariaDB를 설치합니다.
```shell
yum install MariaDB-client MariaDB-server
```

### Tencent Cloud 이미지를 사용하여 MongoDB 가속화


<dx-alert infotype="explain" title="">
다음 단계에서는 MongoDB 4.0을 예로 들어 설명합니다. 다른 버전을 설치해야 하는 경우 mirror 경로에서 버전 번호를 변경하십시오.
</dx-alert>


#### CentOS 또는 Redhat 시스템이 있는 CVM에서 Tencent Cloud MongoDB 사용

1. 다음 명령을 실행하여 `/etc/yum.repos.d/mongodb.repo` 파일을 생성합니다.
```shell
vi /etc/yum.repos.d/mongodb.repo
```
2. **i**를 눌러 편집 모드로 전환하고 다음 내용을 입력한 후 저장합니다.
```shell
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
2. 다음 명령을 실행하여 MongoDB를 설치합니다.
```shell
yum install -y mongodb-org
```

#### CVM에서 Debian 시스템으로 Tencent Cloud MongoDB 사용

1. 다른 Debian 버전에 따라 다음 명령을 실행하여 MongoDB GPG 공개 키를 가져옵니다.
```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 다음 명령을 실행하여 mirror 경로를 구성합니다.
```
#Debian 8
echo "deb http://mirrors.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 다음 명령을 실행하여 캐시를 지웁니다.
```shell
sudo apt-get clean all
```
4. 다음 명령을 실행하여 소프트웨어 패키지 리스트를 업데이트하십시오.
```shell
sudo apt-get update
```
5. 다음 명령을 실행하여 MongoDB를 설치합니다.
```shell
sudo apt-get install -y mongodb-org
```

#### Ubuntu 시스템의 CVM에서 Tencent Cloud MongoDB 사용

1. 다음 명령을 실행하여 MongoDB GPG 공개 키를 가져옵니다.
```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 다음 명령을 실행하여 mirror 경로를 구성합니다.
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 다음 명령을 실행하여 캐시를 지웁니다.
```shell
sudo apt-get clean all
```
4. 다음 명령을 실행하여 소프트웨어 패키지 리스트를 업데이트하십시오.
```shell
sudo apt-get update
```
5. 다음 명령을 실행하여 MongoDB를 설치합니다.
```shell
sudo apt-get install -y mongodb-org
```

### Tencent Cloud 이미지 소스를 사용하여 Rubygems 가속화


<dx-alert infotype="notice" title="">
Tencent Cloud 이미지 소스를 사용하기 전에 CVM에 Ruby가 설치되어 있는지 확인하십시오.
</dx-alert>


다음 명령을 실행하여 RubyGems 소스 주소를 수정합니다.
```shell
gem source -r https://rubygems.org/
gem source -a http://mirrors.tencent.com/rubygems/
```
