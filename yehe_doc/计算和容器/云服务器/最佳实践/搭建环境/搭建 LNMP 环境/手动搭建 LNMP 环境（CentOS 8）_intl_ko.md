## 작업 시나리오
LNMP 환경이란 Linux 시스템에서 Nginx + MySQL/MariaDB + PHP로 구성된 웹 사이트 서버 아키텍처입니다. 본 문서에서는 Tencent Cloud 클라우드 서버(CVM)에서 LNMP 환경을 수동 구축하는 방법을 소개합니다.

LNMP 환경 수동 구축 시에는 Linux 명령어에 익숙해야 하며 설치 프로그램 사용 방법 및 버전 호환성을 이해해야 합니다.

## 소프트웨어 버전 예시
LNMP 환경 구축 소프트웨어 버전 및 설명은 다음과 같습니다.
Linux: Linux 운영 체제의 경우, 본 문서는 CentOS 8.0을 예시로 사용합니다.
Nginx: Web 서버의 경우, 본 문서는 Nginx 1.18.0을 예시로 사용합니다.
MySQL: 데이터베이스의 경우, 본 문서는 MySQL 8.0.21을 예시로 사용합니다.
PHP: 스크립트 언어의 경우, 본 문서는 PHP 7.4.11을 예시로 사용합니다.

## 전제 조건
Linux CVM을 구비해야 합니다. CVM을 구매하지 않았다면, [Linux CVM 사용자 정의 설정](https://intl.cloud.tencent.com/document/product/213/10517)을 참조하십시오.

## 작업 순서
### 순서 1: Linux 인스턴스 로그인
[표준 방식으로 Linux 인스턴스 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수도 있습니다.
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32501)

### 순서 2: Nginx 설치 및 설정
1. 다음 명령어를 실행하여 Nginx를 설치합니다.
>?본 문서는 Nginx 1.18.0 설치를 예시로 사용합니다. [Ngingx 공식 홈페이지 설치 패키지](http://nginx.org/packages/centos/8/x86_64/RPMS/?spm=a2c4g.11186623.2.31.557423bfYPMd6u)에서 CentOS 8에 적용되는 더 많은 버전을 다운로드할 수 있습니다.
>
```
dnf -y install http://nginx.org/packages/centos/8/x86_64/RPMS/nginx-1.18.0-1.el8.ngx.x86_64.rpm
```
1. 다음 명령어를 실행하여 Nginx 버전을 확인합니다.
```
nginx -v
```
다음과 유사한 결과가 리턴되면 설치가 완료된 것입니다.
```
nginx version: nginx/1.18.0
```
3. 다음 명령어를 실행하여 Nginx 구성 파일 경로를 확인합니다.
```
cat /etc/nginx/nginx.conf
```
include 설정 항목 Nginx 구성 파일의 기본 경로인 ‘/etc/nginx/conf.d/*.conf’를 확인할 수 있습니다.
4. 다음 명령어를 차례로 실행하여 구성 파일 기본 경로에 백업을 진행합니다.
```
cd /etc/nginx/conf.d
```
```
cp default.conf default.conf.bak
```
5. 다음 명령어를 실행하여 default.conf 파일을 열어줍니다.
6. **i**를 클릭해 편집 모드로 전환한 후 default.conf 파일을 편집합니다.
  1. location의 index 항목에 index.php를 추가합니다. (다음 이미지 참고)
![](https://main.qcloudimg.com/raw/32df0b8ba82278cd96cf86152738677e.png)
  2. location ~ \.php$ 앞에 있는 ‘#’를 삭제하고 다음의 설정 사항을 수정합니다.
    - root 항목을 사용자 웹 사이트 디렉터리로 설정합니다. 즉, location의 root 항목으로, 본 문서에서는 ‘/usr/share/nginx/html;’를 예시로 사용합니다.
    - fastcgi_pass 항목은 ‘unix:/run/php-fpm/www.sock;’으로 수정하고，Nginx는 UNIX 소켓과 PHP-FPM을 사용해 연결합니다. 해당 설정은 ‘/etc/php-fpm.d/www.conf’ 파일 내 listen 설정과 일치해야 합니다.
    - fastcgi_param SCRIPT_FILENAME 후의 ‘$document_root$fastcgi_script_name;’을 ‘$document_root$fastcgi_script_name;’으로 대체합니다.
    수정 완료 후는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/2e4bff09d70399881bfbf995390a58d3.png) 
7. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 리턴합니다.
8. 다음 명령어를 순서대로 실행하여 Nginx를 실행하고 부팅 시 자동 실행으로 설정합니다.
```
systemctl start nginx
```
```
systemctl enable nginx
```

### 순서 3: MySQL 설치 및 설정
1. 다음 명령어를 실행하여 MySQL을 설치합니다.
```
dnf -y install @mysql
```
2. 다음 명령어를 실행하여 MySQL 버전을 확인합니다.
```
mysql -V
```
다음과 유사한 결과가 리턴되면 설치가 완료된 것입니다.
```
mysql  Ver 8.0.21 for Linux on x86_64 (Source distribution)
```
3. 다음 명령어를 순서대로 실행하여 MySQL을 실행하고 부팅 시 자동 실행으로 설정합니다.
```
systemctl enable --now mysqld
```
```
systemctl status mysqld
```
4. 다음 명령어를 실행하여 MySQL의 보안성 작업을 실행하고 비밀번호를 설정합니다.
```
mysql_secure_installation
```
다음 순서에 따라 해당 작업을 실행합니다.
  1 ‘y’를 입력한 후 **Enter** 를 눌러 관련 설정을 시작합니다.
  2. 비밀번호 인증 정책 적용 강도를 선택합니다. 비밀번호 인증 정책 높음 선택을 권장합니다. ‘2’를 입력하고 **Enter**를 누릅니다.
    - 0: 낮음
    - 1: 중간
    - 2: 높음
  3. MySQL 비밀번호를 설정하고 확인합니다. 비밀번호 입력 시 화면에는 표시되지 않습니다.
  4. ‘y’를 입력하고 **Enter**를 누른 후, 다시 비밀번호를 입력합니다.
  5. ‘y’를 입력하고 **Enter**를 눌러 닉네임 사용자를 제거합니다.
  6. MySQL 원격 연결 허용 여부를 설정합니다.
    - 원격 연결이 필요 없는 경우 ‘y’를 입력하고 **Enter**를 누릅니다.
    - 원격 연결이 필요한 경우 ‘n’을 입력하고 **Enter**를 누릅니다.
  7. ‘y’를 입력하고 **Enter**를 눌러 test 데이터베이스 및 test 데이터베이스 액세스 권한을 삭제합니다.
  8. ‘y’를 입력하고 **Enter**를 눌러 권한 리스트를 다시 로딩합니다.

## 순서 4: PHP 설치 및 설정
1. 다음 명령어를 순서대로 실행하여 epel 원본을 추가 및 업데이트합니다.
```
dnf -y install epel-release
```
```
dnf update epel-release
```
2. 다음 명령어를 순서대로 실행하여 캐시에서 사용하지 않는 소프트웨어 패키지를 삭제하고 소프트웨어 보관소를 업데이트합니다.
```
dnf clean all
```
```
dnf makecache
```
3. 다음 명령어를 실행하여 remi 원본을 설치합니다.
>?PHP 7.4.11 설치 시에는 remi 원본 설치가 필요합니다. 실제 설치하는 PHP 버전에 따라 해당 명령어를 실행하시기 바랍니다.
>
```
dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
```
4. 다음 명령어를 실행하여 PHP 7.4 모듈을 실행합니다.
```
dnf module install php:remi-7.4
```
5. 다음 명령어를 실행하여 PHP에 상응하는 모듈을 설치합니다.
```
dnf install php php-curl php-dom php-exif php-fileinfo php-fpm php-gd php-hash php-json php-mbstring php-mysqli php-openssl php-pcre php-xml libsodium
```
6. 다음 명령어를 실행하여 PHP 버전을 확인합니다.
```
php -v
```
다음과 유사한 결과가 리턴되면 설치가 완료된 것입니다.
```
PHP 7.4.11 (cli) (built: Sep 29 2020 10:17:06) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.11, Copyright (c), by Zend Technologies
```
7. 다음 명령어를 실행하여 www.conf 파일을 열어줍니다.
```
vi /etc/php-fpm.d/www.conf
```
8. **i**를 눌러 편집 모드로 전환하여 www.conf 파일을 편집합니다.
9. user = apache와 group = apache을 user = nginx와 group = nginx로 수정합니다. (다음 이미지 참고)
![](https://main.qcloudimg.com/raw/ceb9c202ebe56c9bd9265e86c0ad2333.png)
10. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 리턴합니다.
11. 다음 명령어를 순서대로 실행하여 PHP-FPM을 실행하고 부팅 시 자동 실행으로 설정합니다.
```
systemctl start php-fpm
```
```
systemctl enable php-fpm
```

### 환경 설정 검증
1. 다음 명령어를 실행하여 테스트 파일을 생성합니다.
> ‘/usr/share/nginx/html’은 Nginx에서 설정한 웹 사이트 디렉터리입니다. 본 문서에서는 해당 디렉터리를 예시로 사용합니다.
>
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. 로컬 브라우저에서 다음 주소에 액세스하여 환경 설정이 완료되었는지 확인합니다. 인스턴스의 공인 IP 획득 방법은 [공인 IP 주소 획득](https://intl.cloud.tencent.com/document/product/213/17940)을 참조하십시오.
```
http://CVM 인스턴스 공인 IP/index.php
```
다음과 같은 결과가 나타나면 환경 설정이 완료된 것입니다.
![](https://main.qcloudimg.com/raw/182c0f73df20d66216a9b73d571b2093.png)

## 관련 작업
LNMP 환경 구축을 완료한 후에는 이를 기반으로 [Wordpress 개인 사이트 수동 구축](https://intl.cloud.tencent.com/document/product/213/8044) 사례를 진행하여 더 많은 CVM 관련 기능을 확인할 수 있습니다.

## FAQ

CVM 사용 도중 문제가 생겼을 경우, 아래의 문서를 참조하여 실제 상황에 따라 문제를 분석 및 해결할 수 있습니다.

- CVM 로그인 문제는 [비밀번호 및 키](https://intl.cloud.tencent.com/document/product/213/18120), [로그인 및 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참조하십시오.
- CVM 네트워크 문제는 [IP 주소](https://intl.cloud.tencent.com/document/product/213/17285), [포트 및 보안 그룹](https://intl.cloud.tencent.com/document/product/213/2502)을 참조하십시오.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/document/product/213/17351)를 참조하십시오.

