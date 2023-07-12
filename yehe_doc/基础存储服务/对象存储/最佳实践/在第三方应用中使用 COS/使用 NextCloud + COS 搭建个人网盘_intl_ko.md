## 서문

NextCloud는 오픈 소스 클라이언트 및 서버 소프트웨어 애플리케이션으로 개인 온라인 파일 스토리지 서비스를 직접 만들 수 있도록 도와줍니다.

NextCloud 서버는 PHP로 작성되었으며 서버의 로컬 디스크를 기본 스토리지로 사용합니다. COS(Cloud Object Storage)를 기본 스토리지로 사용하도록 NextCloud 구성을 수정하여 더 낮은 스토리지 비용으로 더 높은 안정성, 더 강력한 재해 복구 기능 및 무제한 스토리지 공간을 누릴 수 있습니다.

본 문서는 NextCloud 서버가 의존하는 환경과 로컬 스토리지와 COS의 차이점을 비교 분석하고 개인 온라인 파일 스토리지 서비스 구축 방법을 설명합니다.

>! 기존의 NextCloud 서버 인스턴스를 로컬 스토리지에서 COS로 전환하면 기존 파일이 보이지 않을 수 있습니다. 기존 인스턴스의 저장 방법을 변경하려면 새로운 NextCloud 서버를 구축하고 COS를 스토리지로 구성한 다음 이전 인스턴스에서 새 인스턴스로 데이터를 마이그레이션하는 것이 좋습니다.
>

## NextCloud 서버 환경 소개

NextCloud의 서버는 PHP로 작성되며, 데이터베이스는 SQLite, MySQL, MariaDB 또는 PostgreSQL을 사용할 수 있습니다. 이중 SQLite는 성능의 제약으로 인해 실제 애플리케이션에는 일반적으로 권장되지 않습니다. PHP, MySQL과 관련된 서버 소프트웨어는 Windows 버전을 모두 갖추고 있지만, Windows에서 실행되는 NextCloud 서버에 텍스트 인코딩 등의 문제가 있을 수 있다는 NextCloud 커뮤니티의 피드백에 따라 공식 홈페이지는 Windows에 설치된 NextCloud 서버를 지원하지 않겠다고 발표했습니다.

<span id=1></span>
### 서버 구성

Cloud Virtual Machine(CVM)은 현재 각각 여러 서브 패밀리가 있는 여러 인스턴스 패밀리를 제공합니다. 다른 인스턴스 패밀리는 큰 메모리 또는 높은 IO와 같은 다른 강점을 가지고 있습니다. NextCloud는 개인, 가정, 중소기업 사용자를 대상으로 하므로 하드웨어 리소스에 대한 요구 사항이 낮고 리소스가 균형 잡힌 표준형 모델을 선택할 수 있습니다. CVM 인스턴스 서브 패밀리의 경우 일반적으로 최신 제품이 비용 대비 성능이 높으므로 최신 서브 패밀리를 선택하면 됩니다.

인스턴스 패밀리 및 서브 패밀리를 결정한 후 특정 vCPU 및 메모리 사양을 선택해야 합니다(사설망 대역폭 및 PPS는 사양에 따라 다름). PHP용 OPcache를 사용하여 성능을 향상시킬 수 있으며, NextCloud 서버는 APCu 메모리 캐시를 사용하여 성능을 더욱 향상시킬 수 있으므로 대용량 메모리를 선택하는 것이 좋습니다.

구매 후 CVM 인스턴스 구성을 조정할 수 있으므로 1코어 vCPU와 4GB MEM과 같은 낮은 사양의 인스턴스를 먼저 구매하고 온라인 파일 스토리지 서비스를 구축하여 운영 환경에 런칭한 후 사용자 및 파일 수와 CVM 모니터링 데이터를 기반으로 성능 향상을 위한 사양 업그레이드 여부를 결정합니다. 가정 또는 중소기업과 같은 다중 사용자 시나리오에서 서비스를 사용해야 하는 경우 충분한 성능을 제공하기 위해 2코어 8GB MEM 또는 4코어 16GB MEM 인스턴스를 구매하는 것이 좋습니다.

### 서버 운영 체제

주요 Linux 릴리스 버전은 NextCloud 서버를 잘 유지할 수 있습니다. 이들의 구성은 소프트웨어 패키지 설치에 사용되는 명령(패키지 관리 툴)을 제외하고는 기본적으로 동일합니다.

>? 본문은 CentOS 7.7의 CVM 인스턴스를 예로 들어 설명합니다.
>

### 데이터베이스

앞서 언급한 바와 같이 실제 업무에서는 MySQL을 PHP와 함께 사용하는 것이 일반적입니다. MariaDB는 MySQL의 '포크(fork)' 버전으로, MySQL과의 호환성이 높기 때문에 NextCloud 서버는 MySQL 5.7+ 또는 MariaDB 10.2+에서 잘 실행될 수 있습니다.

Tencent Cloud는 TencentDB for MySQL과 TencentDB for MariaDB를 제공합니다. 두 서비스 모두 원본-복제 고가용성 아키텍처를 채택하고 CVM에서 자체 구축한 데이터베이스에 비해 안정성이 더 높습니다. 또한 자동 백업과 같은 사용하기 쉬운 Ops 기능을 지원합니다. 따라서 실제 비즈니스에서 TencentDB를 사용하는 것이 좋습니다.

>? 본문은 TencentDB for MySQL 5.7 인스턴스를 예로 들어 설명합니다.
>

### Web 서버 및 PHP Runtime

일부 NextCloud 서버 구성은 `.htaccess` 파일에 지정되어 있으므로 Apache 서버 소프트웨어 애플리케이션을 사용할 때 NextCloud의 내장 구성 항목을 직접 사용할 수 있습니다. Nginx는 최근 급속도로 발전하고 있는 Web 서버 소프트웨어 애플리케이션으로 Apache에 비해 설치 및 구성이 쉽고 리소스 사용량이 적으며 로드 용량이 큰 것이 특징입니다. NextCloud 서버의 `.htaccess` 구성을 Nginx 구성으로 변환하여 NextCloud 서버를 더 잘 유지할 수 있습니다. 본문은 Nginx 서버 소프트웨어 애플리케이션을 사용하며 참고용으로 완전한 Nginx 구성 예시를 제공합니다.

PHP Runtime은 PHP 7로 업그레이드되었으며 주요 유지 관리 버전에는 모두 NextCloud 서버를 지원하는 7.2, 7.3 및 7.4가 포함됩니다. 여기에서는 최신 버전 7.4를 사용합니다. 또한 NextCloud는 특정 PHP 모듈에 의존합니다. 특정 모듈에 대한 요구 사항은 아래에 자세히 설명되어 있습니다.

### Tencent Cloud 네트워크 환경

현재 Tencent Cloud는 클래식 네트워크 및 VPC 환경을 제공합니다. 클래식 네트워크는 모든 Tencent Cloud 사용자가 공유하는 공중망 리소스 풀로, 모든 CVM 인스턴스의 사설망 IP가 Tencent Cloud에 의해 할당되며 IP 범위 또는 IP 주소를 사용자 지정할 수 없습니다. VPC는 Tencent Cloud에서 논리적으로 격리된 네트워크 공간입니다. VPC에서 IP 범위, IP 주소 및 라우팅 정책을 사용자 지정할 수 있습니다. 현재 클래식 네트워크 리소스가 부족하고 확장할 수 없기 때문에 클래식 네트워크는 더 이상 새 계정과 일부 새 AZ에서 지원되지 않습니다. 따라서 이 문서에서는 VPC를 예로 들어 설명합니다.

>? VPC에 대한 자세한 내용은 [개요](https://intl.cloud.tencent.com/document/product/215/535)를 참고하십시오.
>

## CBS와 COS의 비교

CBS(Cloud Block Storage) 디스크는 CVM 인스턴스의 로컬 디스크로 운영 체제에 마운트됩니다. NextCloud는 기본적으로 파일 시스템을 사용하여 온라인 파일 스토리지 데이터를 저장하므로 NextCloud 데이터를 운영 체제의 CBS 디스크에 직접 저장할 수 있습니다. CBS와 비교하여 COS는 다음과 같은 이점을 제공합니다.

### 사용 사례

#### CBS

CBS는 일종의 블록 스토리지로 CVM 운영 체제에 디스크로 직접 마운트할 수 있습니다. 일반적으로 CBS 디스크는 운영 체제에서만 사용되며 하나의 CVM 인스턴스에만 마운트할 수 있습니다. 그러나 읽기/쓰기 성능이 높고 높은 IO와 낮은 대기 시간이 필요한 시나리오에 적합하며 하나의 CVM 인스턴스에서만 독점적으로 사용됩니다.

#### COS

COS는 HTTP 프로토콜을 통해 읽기/쓰기 API를 개방하므로 프로그래밍을 통해 COS에 저장된 객체(파일)에 액세스해야 합니다. 파일 경로와 같은 객체 Key를 인덱스로 사용하며 저장 용량이 무제한입니다. 데이터가 네트워크를 통해 전송되기 때문에 COS는 속도가 느리고 대기 시간이 더 깁니다. 그러나 객체에 대한 작업이 수행되므로 애플리케이션에서 객체를 조작한 후 다른 애플리케이션에서 즉시 동일한 객체를 조작할 수 있습니다. 결론적으로 COS는 고성능이 필요하지 않지만 비용 효율적인 대용량 스토리지 또는 공유 액세스가 필요한 시나리오에 적합합니다. 다음과 같은 이유로 온라인 파일 스토리지 애플리케이션을 COS와 함께 사용하는 것이 더 적합합니다. 온라인 파일 스토리지 애플리케이션은 네트워크를 통해 데이터를 전송하며 짧은 대기 시간이 필요하지 않습니다. 온라인 파일 저장 클라이언트에서 서버로 그리고 COS로 연결되는 속도와 대기 시간은 주로 클라이언트 네트워크에 따라 달라집니다. COS는 자체 속도를 제한하지 않습니다.



### 유지 관리

#### CBS

CBS에는 고정 용량이 있으며 콘솔 또는 Tencent Cloud API를 통해 확장할 수 있습니다. 확장 후에는 운영 체제에 파티션을 추가해야 하며 파티션 예외가 발생할 수 있으며 일정한 유지 관리 비용이 발생합니다.

#### COS

COS는 주문형으로 사용되며 총 용량이나 객체(파일)의 수를 제한하지 않으므로 유지 관리가 전혀 필요하지 않습니다.

### 데이터 보안

CBS와 COS 모두 데이터의 신뢰성을 보장하기 위해 다중 복사와 같은 방법을 사용합니다.

## NextCloud 서버 실행 환경 구축

### NextCloud 서버가 의존하는 Tencent Cloud 제품 준비

#### CVM
CVM을 시작하려면 [사용자 정의 구성](https://intl.cloud.tencent.com/document/product/213/8036)을 참고하십시오.


#### TencentDB for MySQL

시작하려면 [MySQL 인스턴스 생성](https://intl.cloud.tencent.com/document/product/236/37785)을 참고하십시오.


#### COS

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인(처음 사용하는 경우 COS를 먼저 활성화해야 함)하고 **버킷 리스트** 페이지로 이동하여 **버킷 생성**을 클릭하고 다음과 같이 구성합니다.
<table>
	<tr><th>구성 항목</th><th>값</th></tr>
	<tr><td>이름</td><td>nextcloud와 같은 사용자 정의 버킷 이름을 입력하십시오. 한 번 확인된 이름은 변경할 수 없습니다.</td></tr>
	<tr><td>리전</td><td>CVM 인스턴스의 리전을 선택합니다 </td></tr>
	<tr><td>기타</td><td>기본 설정을 유지합니다</td></tr>
</table>
2. 상기 구성 항목을 설정한 후 **확인**을 클릭합니다.

### Web 서버와 PHP Runtime 설치 및 구성

#### Nginx 설치

1. SSH 툴을 사용하여 새로 구매한 서버에 로그인합니다.
2. 다음 명령을 실행하여 Nginx를 설치합니다.
```bash
yum install nginx
```
 다음과 같은 정보가 뜨면 `Y`와 Enter 키를 눌러 설치를 확인합니다(이하 동일).
```bash
Is this ok [y/d/N]:
```
3. 다음과 같은 정보가 뜨면 설치가 완료된 것입니다.
```bash
Complete!
[root@VM-0-10-centos ~]#
```
4. 다음 명령어를 실행하여 Nginx 버전이 정상적으로 조회되는지 검증합니다.
```bash
nginx -v
```
 다음과 같은 정보가 뜨면 설치 검증이 끝난 것입니다.
```bash
nginx version: nginx/1.16.1
```

#### PHP 설치

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. 다음 명령어를 실행하여 PHP 7.4를 설치합니다.
```bash
yum install epel-release yum-utils
```
3. 다음 명령을 순서대로 실행합니다.
**명령어 1:**
```bash
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
>? 명령 실행이 너무 느리거나 오랫동안 중단된 경우 `Ctrl+C`를 눌러 실행을 취소하고 명령을 다시 실행할 수 있습니다(이하 동일).
>
**명령어 2:**
```bash
yum-config-manager --enable remi-php74
```
 **명령어 3:**
```bash
yum install php php-fpm
```
4. 설치 완료 후 다음 명령어를 실행하여 PHP 버전이 정상적으로 조회되는지 검증합니다.
```bash
php -v
```
 다음과 같은 정보가 뜨면 설치 검증이 끝난 것입니다.
```bash
PHP 7.4.8 (cli) (built: Jul 9 2020 08:57:23) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
```

#### PHP 모듈 설치

NextCloud는 기본적인 PHP 외에도 다른 PHP 모듈에 종속되어 일부 기능을 실행합니다. NextCloud의 종속에 관련된 자세한 모듈 정보는 [NextCloud 공식 홈페이지 문서](https://docs.nextcloud.com/server/19/admin_manual/installation/source_installation.html#prerequisites-for-manual-installation)를 참조하십시오.

본 튜토리얼에는 NextCloud 필수 PHP 모듈이 설치됩니다. NextCloud의 다른 옵션 기능을 사용할 계획이라면 종속된 기타 PHP 모듈에 주의하여 설치하십시오.

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. 다음 명령어를 실행하여 PHP 모듈을 설치합니다.
```bash
yum install php-xml php-gd php-mbstring php-mysqlnd php-intl php-zip
```
3. 설치 완료 후 다음 명령어를 실행하여 설치된 PHP 모듈을 조회합니다.
```bash
php -m
```
4. 기타 모듈 설치가 필요한 경우 `yum install <php-module-name>`을 다시 실행하면 됩니다.

#### NextCloud 서버 코드 업로드 및 압축 해제

1. [NextCloud 공식 홈페이지](https://nextcloud.com/install/#instructions-server)에서 NextCloud 서버 설치 패키지 최신 버전을 다운로드한 다음 서버 `/var/www/` 디렉터리에 업로드합니다. 다음과 같은 방법으로 업로드할 수 있습니다.
 1. `wget` 명령어를 사용하여 서버에서 직접 설치 패키지를 다운로드합니다. 예: `/var/www/` 디렉터리로 이동 후 명령어 `wget https://download.nextcloud.com/server/releases/nextcloud-19.0.1.zip` 실행
 2. 로컬 컴퓨터에 다운로드한 후 SFTP 또는 SCP 등 소프트웨어를 통해 `/var/www/` 디렉터리에 설치 패키지를 업로드합니다.
 3. 로컬 컴퓨터에 다운로드한 후 lrzsz를 사용하여 업로드합니다. 방법은 다음과 같습니다.
    1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
    2. `yum install lrzsz`를 실행하여 lrzsz를 설치합니다.
    3. `cd /var/www/`를 실행하여 타깃 디렉터리로 이동합니다.
    4. `rz -bye`를 실행하고 SSH 툴에서 로컬로 다운로드할 NextCloud 서버 설치 패키지를 선택합니다(해당 조작은 SSH 툴에 따라 상이함).
2. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
3. `unzip nextcloud-<version>.zip`을 실행하여 설치 패키지를 압축 해제합니다(예: `unzip nextcloud-19.0.1.zip`).

#### PHP 설정

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. `vim /etc/php-fpm.d/www.conf`를 실행하여 PHP-FPM 구성 파일을 열고 순서대로 설정 항목을 수정합니다. vim의 구체적인 사용법은 관련 자료를 참조하십시오. 다른 방식을 사용해 해당 구성 파일을 수정할 수도 있습니다.
 1. `user = apache`를 `user = nginx`로 수정합니다.
 2. `group = apache`를 `group = nginx`로 수정합니다.
3. 수정 완료 후 `:wq`를 입력하여 파일을 저장하고 종료합니다. vim의 구체적인 작업 가이드는 관련 문서를 참조하십시오.
4. 다음 명령어를 실행하여 PHP가 Nginx 사용에 최적화되도록 디렉터리 소유자를 수정합니다.
```bash
chown -R nginx:nginx /var/lib/php
```
5. 계속해서 다음 명령어를 실행하고 PHP-FPM 서비스를 실행합니다.
**명령어 1:**
```bash
systemctl enable php-fpm   # 명령어 1
```
 **명령어 2:**
```bash
systemctl start php-fpm   # 명령어 2
```

#### Nginx 설정

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. 다음 명령어를 실행하여 웹 사이트 디렉터리 소유자를 수정합니다.
```bash
chown -R nginx:nginx /var/www
```
3. 기존의 Nginx 구성 파일 `/etc/nginx/nginx.conf`를 백업합니다. 다음 조작이 가능합니다.
 1. `cp /etc/nginx/nginx.conf ~/nginx.conf.bak`를 실행하여 기존 구성 파일을 홈(HOME) 디렉터리에 백업합니다.
 2. SFTP 또는 SCP 등 소프트웨어를 사용하여 기존 구성 파일을 로컬 컴퓨터에 다운로드합니다.
4. `/etc/nginx/nginx.conf`를 다음 내용으로 수정 또는 대체합니다.


```plaintext
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /var/www/nextcloud;

        add_header Referrer-Policy "no-referrer" always;
        add_header X-Content-Type-Options "nosniff" always;
        add_header X-Download-Options "noopen" always;
        add_header X-Frame-Options "SAMEORIGIN" always;
        add_header X-Permitted-Cross-Domain-Policies "none" always;
        add_header X-Robots-Tag "none" always;
        add_header X-XSS-Protection "1; mode=block" always;

        client_max_body_size 512M;
        fastcgi_buffers 64 4K;

        gzip on;
        gzip_vary on;
        gzip_comp_level 4;
        gzip_min_length 256;
        gzip_proxied expired no-cache no-store private no_last_modified no_etag auth;
        gzip_types application/atom+xml application/javascript application/json application/ld+json application/manifest+json application/rss+xml application/vnd.geo+json application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/bmp image/svg+xml image/x-icon text/cache-manifest text/css text/plain text/vcard text/vnd.rim.location.xloc text/vtt text/x-component text/x-cross-domain-policy;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            try_files $uri $uri/ =404;
            index index.php;
        }

        location ~ ^\/(?:build|tests|config|lib|3rdparty|templates|data)\/ {
            deny all;
        }
        location ~ ^\/(?:\.|autotest|occ|issue|indie|db_|console) {
            deny all;
        }

        location ~ ^\/(?:index|remote|public|cron|core\/ajax\/update|status|ocs\/v[12]|updater\/.+|oc[ms]-provider\/.+)\.php(?:$|\/) {
            fastcgi_split_path_info ^(.+?\.php)(\/.*|)$;
            set $path_info $fastcgi_path_info;
            try_files $fastcgi_script_name =404;
            include        fastcgi_params;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            fastcgi_param PATH_INFO $path_info;
            fastcgi_param modHeadersAvailable true;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_intercept_errors on;
            fastcgi_request_buffering off;
        }

        location ~ ^\/(?:updater|oc[ms]-provider)(?:$|\/) {
            try_files $uri/ =404;
            index index.php;
        }

        location ~ \.(css|js|svg|gif)$ {
            add_header Cache-Control "max-age=15778463";
        }

        location ~ \.woff2?$ {
            add_header Cache-Control "max-age=604800";
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2 default_server;
#        listen       [::]:443 ssl http2 default_server;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        location / {
#        }
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}
```



5. 계속해서 다음 명령어를 실행하고 Nginx 서비스를 실행합니다.
**명령어 1:**

```bash
systemctl enable nginx
```

 **명령어 2:**
```bash
systemctl start nginx
```

## COS를 사용하도록 NextCloud 서버 구성

### COS 정보 가져오기

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 이전에 생성한 버킷을 찾아 버킷 이름을 클릭합니다.
![](https://main.qcloudimg.com/raw/13e02915f8c2846d7dfa5f2fec0c355b.png)
3. 왼쪽 사이드바에서 **개요**를 선택하고 **기본 정보**의 **버킷 이름** 및 **리전**에 정보를 기록합니다.
![](https://main.qcloudimg.com/raw/2aef2ba23a6a32305ad39b4ef10a970c.png)

### API 키 획득

리스크를 줄이기 위해 서브 계정 키를 사용하고 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)을 따르는 것이 좋습니다. 서브 계정 키를 얻는 방법에 대한 자세한 내용은 [Access Key](https://intl.cloud.tencent.com/document/product/598/32675)를 참고하십시오.



### NextCloud 서버 구성 파일 수정

1. 텍스트 편집 툴을 사용하여 `config.php`를 생성하고 다음 내용을 입력한 후 주석에 따라 관련 값을 수정합니다.


```php
<?php
$CONFIG = array(
  'objectstore' => array(
    'class' => '\\OC\\Files\\ObjectStore\\S3',
    'arguments' => array(
      'bucket' => 'nextcloud-1250000000', // 버킷 이름(공간의 이름)
      'autocreate' => false,
      'key'  => 'AKIDxxxxxxxx', // 사용자의 SecretId로 변경
      'secret' => 'xxxxxxxxxxxx', // 사용자의 SecretKey로 변경
      'hostname' => 'cos.<Region>.myqcloud.com', // <Region>을 소속 리전으로 수정(예: ap-shanghai)
      'use_ssl' => true,
    ),
  ),
);
```


 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yJvR645_b14a23e2cac3ac988745fcd82fe56e18.png)
2. 해당 파일을 저장하고 `/var/www/nextcloud/config/` 디렉터리에 업로드합니다(파일 이름은 `config.php`로 유지). SFTP 또는 SCP 소프트웨어를 통해 파일을 업로드할 수 있고, `rz -bye` 명령어를 통해 업로드할 수도 있습니다.

3. 다음 명령어를 실행하여 구성 파일의 소유자를 수정합니다.

```bash
chown nginx:nginx /var/www/nextcloud/config/config.php
```

## 도메인 이름 구성

NextCloud 서버에 IP 주소가 아닌 도메인 이름을 사용하려면, 도메인 이름을 등록하고 CVM IP 주소로 리졸브하고, 도메인 등록 기관의 안내 문서에 따라 ICP 비안을 받을 수 있습니다.

NextCloud 서버는 설치 시 사용한 도메인 이름이나 IP 주소를 기록하므로 설치 전에 도메인 이름을 등록, 리졸브 및 ICP 비안을 받아 도메인 이름을 사용하여 NextCloud 서버의 보안 페이지로 이동하는 것이 좋습니다.

NextCloud 서버 설치 완료 후 도메인 또는 IP 주소를 변경해야 할 경우 직접 `/var/www/nextcloud/config/config.php` 구성 파일의 `trusted_domains`를 수정할 수 있습니다. 세부 사항은 [NextCloud 공식 홈페이지 문서](https://docs.nextcloud.com/server/19/admin_manual/installation/installation_wizard.html#trusted-domains)를 참조하십시오.

## NextCloud 서버 설치

1. 브라우저를 사용하여 NextCloud 서버에 액세스한 후 관리자 및 사용자 이름과 비밀번호를 생성하고 기억합니다.
2. **스토리지와 데이터베이스**를 확장하고 다음과 같이 구성합니다.

<table>
	<tr><th>구성 항목</th><th>값</th></tr>
	<tr><td>데이터 폴더</td><td>/var/www/nextcloud/data(기본값 유지)</td></tr>
	<tr><td>데이터베이스 구성</td><td>MySQL/MariaDB</td></tr>
	<tr><td>데이터베이스 사용자</td><td>root</td></tr>
	<tr><td>데이터베이스 비밀번호</td><td>TencentDB for MySQL 초기화 중에 입력한 root 사용자의 비밀번호</td></tr>
	<tr><td>데이터베이스 이름</td><td>nextcloud(또는 사용하지 않는 다른 이름)</td></tr>
	<tr><td>데이터베이스 호스트(기본적으로 localhost가 표시됨)</td><td>TencentDB for MySQL 인스턴스의 사설망 주소</td></tr>
</table>
3.   **설치 완료**를 클릭하고 NextCloud 서버 설치가 완료될 때까지 기다립니다.
4.   설치 과정에서 504 Gateway Timeout과 같은 오류 정보가 뜨는 경우 새로고침 후 다시 시도합니다.
5.   설치 완료 후 관리자 계정을 사용해 NextCloud 서버에 로그인하면 웹 페이지 버전의 NextCloud를 사용할 수 있습니다.

## NextCloud 서버 환경 최적화

### 백그라운드 작업

NextCloud 서버는 사용자와 상호작용이 필요하지 않을 때 데이터베이스 정리와 같은 백그라운드 작업을 실행하는 경우가 있습니다. PHP 실행 특성상 PHP 기반 프로그램은 내부적으로 하나의 독립된 작업 진행 또는 스레드를 유지할 수 없으므로 백그라운드 작업과 같은 시나리오는 외부에서 호출하여 대응하는 PHP 프로그램으로 실행해야 합니다.

NextCloud 서버는 세 가지 백그라운드 작업 호출 방식을 제공합니다. 기본값은 웹 페이지에 로그인한 사용자를 통해 브라우저에서 자동으로 AJAX 요청을 보낸 후 서버의 백그라운드 작업 실행을 호출하는 방식으로, 사용자의 로그인 상태에 크게 의존합니다. 사용자가 로그인하지 않으면 이러한 백그라운드 작업은 실행될 수 없으므로 신뢰성이 가장 낮습니다.

AJAX 기반 백그라운드 작업의 신뢰성이 떨어지는 문제를 피하고자 Linux의 cron을 사용한 백그라운드 작업 설정을 권장합니다. Linux의 cron은 작업 호출 시간을 정확하게 제어합니다. 설정 가능한 Interval은 분, 시간, 한 달 중 특정 일, 월, 요일을 포함합니다. 예를 들어 5분마다(분 수는 5의 배수) 또는 매시 10분 등으로 설정할 수 있습니다. 일부 운영 체제는 초 단위, 연 단위도 지원하여 매우 효율적입니다. cron에 대한 설명과 설정은 관련 자료를 참조하십시오.

NextCloud 서버의 백그라운드 작업을 위해 cron을 설정하는 방법을 소개합니다.

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. 다음 명령어를 실행하여 PHP 모듈을 설치합니다.
```bash
yum install php-posix
```
3. 다음 명령어를 실행하여 nginx 계정에 사용할 cron 설정을 열거나 생성합니다.
```bash
crontab -u nginx -e
```
4. 다음 편집 인터페이스는 vi/vim입니다. `i` 키를 눌러 편집 모드로 이동한 후 한 행을 삽입합니다. 내용은 다음과 같습니다.
```plaintext
*/5 * * * * php -f /var/www/nextcloud/cron.php
```
`ESC`를 눌러 편집 모드를 종료하고 `:wq`를 입력하여 저장 후 종료합니다. vi/vim의 구체적인 작업 가이드는 관련 문서를 참조하십시오.
상기 구성에서는 공식적으로 권장되는 실행 빈도를 5분에 한 번씩 설정합니다. 백그라운드 작업이 5분 안에 실행된 후에는 브라우저를 열어 NextCloud 서버에 로그인할 수 있습니다. 그 후, 오른쪽 상단 모서리에서 사용자 이름 첫 글자를 클릭하여 **설정** 페이지로 이동한 후, 좌측 사이드바에서 **기본 설정**을 선택하면 기본적으로 Cron이 **백그라운드 작업**으로 선택되어 있는 것을 확인할 수 있습니다.


### 메모리 캐시

PHP는 OPcache를 사용하여 성능을 향상할 수 있습니다. NextCloud 서버도 APCu를 사용한 메모리 캐시 성능 향상을 지원합니다. 아래 관련 작업 과정을 소개합니다.

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. 다음 명령어를 실행하여 PHP 모듈을 설치합니다.
```bash
yum install php-pecl-apcu
```
3. 계속해서 다음 명령어를 실행하여 Nginx와 PHP-FPM을 재시작합니다.
**명령어 1:**
```bash
systemctl restart nginx
```
 **명령어 2:**
```bash
systemctl restart php-fpm
```
4. `vim /var/www/nextcloud/config/config.php`를 실행하여 NextCloud 서버의 구성 파일을 열고 `$CONFIG = array (`에 한 행 `'memcache.local' => '\OC\Memcache\APCu',`을 추가합니다. 파일을 저장하고 종료합니다.
![](https://main.qcloudimg.com/raw/eaa28e013991aad579cf6abc2a34d9bb.png)
5. cron 설정으로 백그라운드 작업을 최적화한 후 PHP의 apc 설정 변경이 필요합니다. `vim /etc/php.d/40-apcu.ini`를 실행하여 PHP APCu의 구성 파일을 열고 `;apc.enable_cli=0`을 `apc.enable_cli=1`로 수정(주의: 맨 앞의 세미콜론을 모두 삭제)한 다음 저장하고 종료합니다. `/etc/php.d/40-apcu.ini` 경로가 존재하지 않을 경우 직접 `/etc/php.d/` 디렉터리에서 apc 또는 apcu 문구가 들어간 `.ini` 구성 파일을 찾아 편집합니다.
![](https://main.qcloudimg.com/raw/1c57fe0a2078aa0ca5dd7ba07b23fe86.png)

## 클라이언트 액세스 설정

NextCloud 공식 홈페이지가 제공하는 데스크톱 동기화 클라이언트와 모바일 클라이언트는 NextCloud 공식 홈페이지 또는 애플리케이션 스토어에서 다운로드할 수 있습니다. NextCloud 설정 시 NextCloud의 서버 주소(도메인 또는 IP)를 입력해야 합니다. 그런 다음 사용자 이름과 비밀번호를 입력하고 로그인하면 바로 클라이언트를 사용할 수 있습니다.






