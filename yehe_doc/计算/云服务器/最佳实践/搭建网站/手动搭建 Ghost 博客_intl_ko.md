## 작업 시나리오
Ghost는 Node.js 언어로 작성된 오픈 소스 블로그 플랫폼으로, Ghost를 사용하여 블로그를 빠르게 구축하고 온라인 게시 프로세스를 간소화할 수 있습니다. 이 문서는 Tencent Cloud CVM에서 Ghost 개인 웹사이트를 수동으로 구축하는 방법을 설명합니다.

Ghost 웹 사이트 구축을 위해 자주 사용하는 명령어인 [Ubuntu 환경에서 Apt-get을 통해 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2123)등의 Liunx 운영 체제와 명령어를 숙지해야 합니다.

## 소프트웨어
본문에서 Ghost 블로그를 구축하는 데 사용된 운영 체제 및 소프트웨어 버전은 다음과 같습니다.
- 운영체제: Ubuntu 20.04.
- Nginx: 본 문서는 Web 서버 Nginx 1.18.0을 예시로 사용합니다.
- MySQL: 본 문서는 데이터베이스 MySQL 8.0.25를 예시로 사용합니다.
- Node.js: 본 문서는 런타임 환경 Node.js 14.17.0 버전을 예시로 사용합니다.
- Ghost： Ghost 4.6.4


## 전제 조건
- Linux CVM을 구비해야 합니다. CVM을 구매하지 않았다면, [Linux CVM 커스텀 설정](https://intl.cloud.tencent.com/document/product/213/10517)을 참고하시기 바랍니다.
- Ghost 블로그 설정에는 이미 ICP비안이 완료되고, CVM 리졸브가 완료된 도메인을 사용해야 합니다.



## 작업 순서

### 1단계: Linux 인스턴스 로그인
[Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다. 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수도 있습니다.
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)

### 2단계: 신규 사용자 생성
1. Ubuntu 운영 체제의 CVM에 로그인한 후, [로그인, 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참고하여 root 사용자로 전환하십시오.
2, 다음 명령어를 실행하여 신규 사용자를 생성하십시오. 본 문서는 ‘user’를 예시로 사용합니다.
>! 사용자 이름으로 ‘ghost’를 사용하지 마십시오. Ghost-CLI와 충돌할 수 있습니다. 
>
```
adduser user
```
 1. 안내에 따라 사용자 비밀번호를 입력 및 확인합니다. 비밀번호는 표시 안 함으로 기본 설정되어 있으며 입력 후 **Enter**를 누르면 다음 단계로 넘어갑니다.
 2. 실제 상황에 따라 사용자 관련 정보를 입력합니다. 입력하지 않아도 **Enter**를 눌러 다음 단계를 진행할 수 있습니다.
 3. **Y**를 입력하여 정보를 확인한 후, **Enter**를 눌러 설정을 완료하면 다음과 같이 표시됩니다.
 ![](https://main.qcloudimg.com/raw/66ca399607b89f2653668eb4b0cb71f5.png)
3. 다음 명령어를 실행하여 사용자 권한을 추가합니다.
```
usermod -aG sudo user
```
4. 다음 명령어를 실행하여 ‘user’로 전환합니다.
```
su - user
```

### 3단계: 설치 패키지 업데이트
다음 명령어를 순서대로 실행하여 설치 패키지를 업데이트합니다.
>? 인터페이스의 안내에 따라 ‘user’의 비밀번호를 입력하고 **Enter**를 눌러 업데이트를 시작합니다.
>
```
sudo apt-get update
```
```
sudo apt-get upgrade -y
```

### 4단계: 환경 설정
#### Nginx 설치 및 설정
다음 명령어를 실행하여 Nginx를 설치합니다.
```
sudo apt-get install -y nginx 
```

#### MySQL 설치 및 설정
1. 다음 명령어를 실행하여 MySQL을 설치합니다.
```
sudo apt-get install -y mysql-server 
```
2. 다음 명령어를 실행하여 MySQL을 연결합니다.
```
sudo mysql
```
3. <span id=“atabase”></span> 다음 명령어를 실행하여 Ghost가 사용할 데이터베이스를 생성합니다. 본문은 ‘ghost_data’를 예시로 사용합니다.
```
CREATE DATABASE ghost_data;
```
4. <span id=“sercet”></span> 다음 명령어를 실행하여 root 계정 비밀번호를 설정합니다.
```
ALTER USER ’root’@’localhost’ IDENTIFIED WITH mysql_native_password BY ’ root 계정 비밀번호를 입력합니다.
```
5. 다음 명령어를 실행하여 MySQL을 종료합니다.
```
\q
```

#### Node.js 설치 및 설정
1. 다음 명령어를 실행하여 Node.js가 지원하는 설치 버전을 추가합니다.
>? Ghost 각 버전마다 Node.js에 대한 버전 요구 사항이 다르므로 [upported Node versions](https://ghost.org/docs/faq/node-versions/) 및 다음 명령어를 참고하여 해당 명령어를 실행합니다.
>
```
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash
```
2. 다음 명령어를 실행하여 Node.js를 설치합니다.
```
sudo apt-get install -y nodejs
```

#### Ghost-CLI 설치
다음 명령어를 실행하여 Ghost-CLI을 설치하여 Ghost를 빠르게 설정합니다.
```
sudo npm install ghost-cli@latest -g
```

### 5단계: Ghost 설치 및 설정
1. 다음 명령어를 순서대로 실행하여 Ghost 설치 디렉터리를 설정 및 이동합니다.
```
sudo mkdir -p /var/www/ghost
```
```
sudo chown user:user /var/www/ghost
```
```
sudo chmod 775 /var/www/ghost
```
```
cd /var/www/ghost
```
2. 다음 명령어를 실행하여 Ghost를 설치합니다.
```
ghost install
```
3. 다음 이미지를 참고하여 설치 프로세스를 완료합니다.
![](https://main.qcloudimg.com/raw/4fa1bccb961fa6c05c01892e5fbfd367.png)
주요 설정은 다음과 같습니다.
 1. **Enter your blog URL**: ‘http://(도메인 이름)’ 형식의 도메인을 입력합니다.
 2. **Enter your MySQL  hostname**: 데이터베이스 연결 주소를 입력합니다. ‘localhost’를 입력한 다음 **Enter**를 누릅니다.
 3. **Enter your MySQL username**: 데이터베이스 사용자 이름을 입력합니다. ‘root’를 입력한 다음 **Enter**를 누릅니다.
 4. **Enter your MySQL password**: 데이터베이스 비밀번호를 입력하고 [root 계정 비밀번호 설정](#sercet)에서 설정한 비밀번호를 입력한 다음 **Enter**를 누릅니다.
 5. **Enter your database name**: Ghost가 사용할 데이터베이스를 입력합니다. [데이터베이스 생성](#database)에서 생성한 ‘ghost_data’를 입력한 다음 **Enter**를 누릅니다.
 6. **Do you wish to set up SSL?**: HTTPS 액세스를 활성화하려면 **Y**를 입력한 다음 **Enter**를 누릅니다.
 실제 상황과 페이지 안내에 따라 나머지 설정을 완료합니다. 설정을 완료하면 인터페이스 하단에 Ghost 관리자 액세스 주소가 출력됩니다.
4. 다음 이미지와 같이 로컬 브라우저를 통해 Ghost의 관리자 액세스 주소에 액세스한 후, 개인 블로그 설정을 시작합니다.
>? HTTPS 액세스를 활성화한 경우, ‘https://’를 사용하여 액세스 또는 블로그 설정 등의 작업을 할 수 있습니다.
>
[Create your account]를 클릭하여 관리자 계정을 생성합니다.
![](https://main.qcloudimg.com/raw/e2eeacd71eec4c27660eeb4797f83f2a.png)
5. 다음 이미지와 같이 관련 정보를 입력한 후, [Last step]을 클릭합니다.
![](https://main.qcloudimg.com/raw/a7a81f16b811bdceeb429116ee23081c.png)
6. 블로그 생성에 다른 사람을 초대할 수 있으며, 이 단계는 생략 가능합니다.
7. 다음 이미지와 같이 관리 인터페이스에 들어가서 블로그를 관리합니다.
![](https://main.qcloudimg.com/raw/fd9071dba9748ce8125f8597be0d248a.png)
다음 이미지와 같이 설정이 끝나면 로컬 브라우저를 사용하여 설정된 ‘www.xxxxxxxx.xx’ 도메인을 액세스하여 블로그를 확인합니다.
![](https://main.qcloudimg.com/raw/055decab4524eb9f2f5602fbd0502c7c.png)

## FAQ
CVM 사용 도중 문제가 생겼을 경우, 아래의 문서를 참고하여 실제 상황에 따라 문제를 분석 및 해결할 수 있습니다.
- CVM 로그인 문제는 [키 관련 문제](https://intl.cloud.tencent.com/document/product/213/18120), [로그인, 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참고하십시오.
- CVM 네트워크 문제는 [IP 주소 문제](https://intl.cloud.tencent.com/document/product/213/17285), [포트 관련 문제](https://intl.cloud.tencent.com/document/product/213/2502)를 참고하십시오.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/document/product/213/17351)를 참고하십시오.

 

 

 
