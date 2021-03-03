## 서문

NextCloud는 네트워크 디스크 생성에 사용되는 오픈 소스 클라이언트이자 서버 소프트웨어입니다. 누구나 이 소프트웨어로 직접 개인 네트워크 디스크 서비스를 구축할 수 있습니다.

NextCloud의 서버는 PHP로 작성되며, 하위 레이어 스토리지는 기본적으로 서버의 로컬 디스크에 저장됩니다. NextCloud 설정 변경을 통해 Tencent Cloud COS를 하위 레이어 스토리지로 사용함으로써 COS가 제공하는 저렴한 저장 비용, 높은 신뢰성, 재해 복구 능력, 무한한 저장 공간을 경험할 수 있습니다.

본 문서는 NextCloud 서버가 종속된 환경을 소개하고 로컬 스토리지와 COS의 차이를 분석한 뒤 실제로 개인 네트워크 디스크를 구축하는 방법을 설명합니다.

>! 기존의 NextCloud 서버 인스턴스를 로컬 스토리지에서 Tencent Cloud COS 사용으로 변경하면 기존 파일이 보이지 않을 수 있습니다. 기존 인스턴스의 저장 방식에 변경이 필요한 경우 본 튜토리얼에 따라 새로운 NextCloud 서버를 구축하고 Tencent Cloud COS를 사용하도록 설정한 다음 이전 인스턴스의 데이터를 새로운 인스턴스로 마이그레이션할 것을 권장합니다.

## NextCloud 서버 환경 소개

NextCloud의 서버는 PHP로 작성되며, 데이터베이스는 SQLite, MySQL, MariaDB 또는 PostgreSQL을 사용할 수 있습니다. 이중 SQLite는 성능의 제약으로 인해 실제 애플리케이션에는 일반적으로 권장되지 않습니다. PHP, MySQL과 관련된 서버 소프트웨어는 Windows 버전을 모두 갖추고 있지만, Windows에서 실행되는 NextCloud 서버에 텍스트 인코딩 등의 문제가 있을 수 있다는 NextCloud 커뮤니티의 피드백에 따라 공식 홈페이지는 Windows에 설치된 NextCloud 서버를 지원하지 않겠다고 발표했습니다.

<span id=1>

### 서버 설정

Tencent Cloud의 CVM에는 현재 여러 인스턴스 패밀리가 있고, 각 패밀리는 다시 여러 서브 유형으로 나뉩니다. 인스턴스 패밀리마다 각자 더 치중하는 포인트가 있습니다(예: 큰 용량의 메모리 또는 고IO 등). NextCloud는 개인, 가정 또는 중소기업 사용자에게 맞춰져 있으며 각 하드웨어 리소스에 대한 요구가 높지 않기 때문에 여러 리소스가 균형 있게 갖춰져 있는 표준형을 선택하면 충분히 만족스러운 사용이 가능합니다. 서브 유형의 경우 일반적으로 최신 서브 유형의 가성비가 더 좋기 때문에 최신 서브 유형을 선택하면 됩니다.

인스턴스 패밀리와 서브 유형을 확정하고 나면 구체적인 vCPU와 메모리 규격, 그리고 서로 다른 vCPU와 메모리 규격에 상응하는 내부 네트워크 대역폭 및 네트워크 송수신 패킷을 선택해야 합니다. PHP는 OPcache를 사용해 성능을 향상할 수 있지만, NextCloud 서버는 APCu를 사용한 메모리 캐시 성능 향상을 지원하므로 규격 선택 시 비교적 용량이 큰 메모리를 권장합니다.

CVM은 구매 후 사양 조정을 지원하므로, 1코어 vCPU와 4GB 메모리 같은 저사양 규격을 일단 구매한 다음 구축이 완료되어 실제로 런칭 사용한 후 사용자 수, 파일 수, CVM 관련 모니터링 데이터에 따라 규격을 높여 성능 향상이 필요한지 판단할 수 있습니다. 가정 또는 중소기업 등 사용자가 다수인 시나리오가 예상되는 경우 다수의 사용자가 충분히 만족하는 성능을 제공할 수 있는 듀얼코어 8GB ~ 4코어 16GB 사양의 구매를 권장합니다.

### 서버 운영 체제

주요 Linux 릴리스 버전은 모두 NextCloud 서버의 원활한 실행을 지원합니다. 소프트웨어 패키지 설치 시 사용하는 명령어(즉, 패키지 관리 툴)가 시스템마다 약간씩 다른 경우를 제외하면 다른 설정 작업은 차이가 없습니다.

>?본 문서는 CentOS 7.7 운영 체제의 CVM 실행을 예로 들어 후속 시연을 진행합니다.

### 데이터베이스

위의 내용과 같이 실제 애플리케이션에서는 보통 MySQL과 PHP를 함께 사용합니다. MariaDB는 MySQL의 '포크(fork)' 버전으로, MySQL과 고도의 호환이 가능합니다. 따라서 MySQL 5.7+, MariaDB 10.2+ 모두 NextCloud 서버와 잘 맞습니다.

Tencent Cloud는 호스팅되는 TencentDB for MySQL과 TencentDB for MariaDB를 제공합니다. CVM의 자체구축 데이터베이스에 비해 CDB는 1 마스터 1 슬레이브의 고가용성 모드를 기본으로 더 높은 신뢰성을 가지고 자동 백업 등 편리한 유지보수 작업을 제공하기 때문에 실제 애플리케이션에는 CDB 사용을 적극적으로 권장합니다.

>?본 문서는 TencentDB for MySQL 5.7 버전을 예로 들어 후속 시연을 진행합니다.

### Web 서버 및 PHP Runtime

NextCloud 서버는 `.htaccess`를 통해 일부 설정을 지정하기 때문에 Apache 서버 소프트웨어를 사용할 때 NextCloud 서버의 설정 항목을 직접 사용할 수 있습니다. Nginx는 최근 몇 년 동안 빠르게 발전한 Web 서버 소프트웨어로, Apache와 비교해 설치와 설정이 간단하고 리소스가 차지하는 용량이 적으며 부하 성능이 강하다는 장점이 있습니다. NextCloud 서버의 `.htaccess` 설정을 Nginx 설정으로 변환하면 NextCloud 서버의 실행을 효과적으로 지원할 수 있습니다. 본 문서는 Nginx 서버 소프트웨어를 사용하며, 참고를 위해 완전한 Nginx 설정 예시를 제공합니다.

PHP Runtime은 현재 PHP 7까지 나와 있습니다. 주요 점검 버전은 7.2, 7.3, 7.4를 포함하고 있으며, 세 버전 모두 NextCloud 서버를 지원하므로 최신 버전인 7.4를 사용하면 됩니다. NextCloud는 PHP의 일부 확장 모듈에 종속되어 있습니다. 아래에서 구체적인 확장 모듈의 요구 사항을 자세히 소개합니다.

### Tencent Cloud 네트워크 환경

Tencent Cloud는 현재 기본 네트워크와 사설 네트워크(VPC) 환경을 제공합니다. 기본 네트워크는 Tencent Cloud에 있는 모든 사용자의 공용 네트워크 리소스 풀입니다. 모든 CVM의 개인 IP 주소는 Tencent Cloud가 통합 할당하므로 IP 대역 구분이나 IP 주소를 사용자 마음대로 정의할 수 없습니다. 사설 네트워크는 사용자가 Tencent Cloud에 구축한, 논리적으로 격리된 가상 네트워크입니다. 사용자는 사설 네트워크에서 IP 대역, IP 주소, 라우팅 정책을 자유롭게 정의할 수 있습니다. 현재 기본 네트워크의 리소스 부족과 증설 불가로 인해 신규 가입 계정 및 일부 새로 생성한 가용존은 기본 네트워크를 지원하지 않습니다. 따라서 본 문서는 사설 네트워크를 예로 들어 후속 시연을 진행합니다.

>?사설 네트워크에 관한 자세한 소개는 [사설 네트워크 제품 개요](https://intl.cloud.tencent.com/document/product/215/535)를 참조하십시오.

## CBS와 COS 비교

CVM(Cloud Virtual Machine)에서 CBS는 CVM의 로컬 디스크 형식으로 운영 체제에 마운트됩니다. NextCloud는 기본적으로 파일 시스템을 사용해 클라우드 데이터를 저장하므로 NextCloud의 데이터를 운영 체제의 CBS에 직접 저장할 수 있습니다. 그렇다면 CBS와 비교해 COS를 사용하는 것에는 어떤 장점이 있을까요? CBS와 COS의 차이점을 몇 가지 측면에서 설명하겠습니다.

### 응용 시나리오

#### CBS

CBS는 블록 스토리지에 속해 있으므로 CVM 운영 체제에 직접 마운트하여 디스크로 사용할 수 있습니다. 일반적으로 운영 체제가 독점적으로 사용, 즉, 한 대의 CVM에만 마운트할 수 있으나 읽기/쓰기 성능이 높아 고IO 저딜레이 및 다른 CVM과 공유가 필요 없는 시나리오에 적합합니다.

#### COS

COS는 http 프로토콜로 읽기/쓰기 인터페이스를 제공하며, COS에 저장된 객체(파일)에 프로그래밍 방식을 통해 액세스해야 합니다. COS는 객체 키(Key, 파일 경로의 의미)를 인덱스로 사용하여 스토리지 용량 제한이 없습니다. 네트워크 전송을 사용하여 상대적으로 딜레이가 많이 되지만, 처리는 객체 레벨이므로 하나의 소프트웨어가 하나의 객체를 처리한 후 곧바로 다른 소프트웨어가 동일 객체를 처리할 수 있어서 성능에 대한 요구가 높지 않고, 저비용 대용량 스토리지 또는 공용 액세스가 필요한 시나리오에 적합합니다. 네트워크 디스크 애플리케이션 자체가 네트워크를 통해 전송되므로 딜레이에 대한 요구가 높지 않습니다. 또한 네트워크 디스크 클라이언트에서 시작해 네트워크 디스크 서버 및 COS로 이어지는 링크에서 속도와 딜레이 시간에 영향을 주는 요소는 주로 클라이언트가 있는 네트워크 환경이며, COS 자체는 속도에 영향을 주지 않기 때문에 네트워크 디스크 애플리케이션에는 COS가 적합합니다.



### 점검

#### CBS

CBS는 용량이 고정되어 있고 콘솔 또는 API를 통해 용량을 확장할 수 있습니다. 용량 확장 후에는 운영 체제에서 파티션을 확장해야 합니다. 파티션 확장 시 어느 정도의 파티션 오류 리스크와 점검 비용이 뒤따릅니다.

#### COS

COS는 필요에 따라 사용되며 총 용량과 객체 수(파일 수)에 제한이 없으므로 점검이 필요하지 않습니다.

### 데이터 보안

CBS와 COS 모두 사본을 여러 개 만들어 두는 것과 같은 방법을 사용하여 데이터의 신뢰성을 보장합니다.

## NextCloud 서버 실행 환경 구축

### NextCloud 서버가 종속된 클라우드 서비스 준비

#### Cloud Virtual Machine(CVM)

시작하려면 [CVM 시작하기](https://intl.cloud.tencent.com/zh/document/product/213/8036)를 참조하십시오.

#### TencentDB for MySQL

시작하려면 [TencentDB for MySQL 시작하기](https://intl.cloud.tencent.com/zh/document/product/236/37785)를 참조하십시오.

#### COS

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)을 열고 로그인합니다(최초 사용 시 객체 스토리지 서비스 활성화 필요). [버킷 리스트]에서 [버킷 생성]을 클릭하고 아래 설명에 따라 설정합니다.

| 설정 항목   | 설정값                                                           |
| -------- | ------------------------------------------------------------ |
| 이름     | 사용자 정의된 버킷 이름을 입력합니다(예: nextcloud). 주의: 해당 이름은 확정 후 변경이 불가능합니다. |
| 소속 리전 | 구매한 CVM의 소속 리전과 일치해야 합니다.                                  |
| 기타     | 기본값 유지                                                     |

2. 위의 설정을 마친 후 [확인]을 클릭하고 생성을 완료합니다.

### Web 서버와 PHP Runtime 설치 및 설정

#### Nginx 설치

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. 다음 명령어를 실행하여 Nginx를 설치합니다.
```bash
yum install nginx
```
다음과 같은 정보가 뜨면 `Y`를 누르고 Enter 키를 눌러 설치를 확인합니다(이하 동일).
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

계속해서 다음 명령어를 실행합니다.
**명령어 1:**
```bash
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

>?위의 명령어 실행 시 속도가 너무 느려지거나 진행이 멈춘 경우 `Ctrl+C`를 눌러 해당 명령어의 실행을 취소하고 재시작할 수 있습니다(이하 동일).

**명령어 2:**
```bash
yum-config-manager --enable remi-php74
```
**명령어 3:**
```bash
yum install php php-fpm
```

3. 설치 완료 후 다음 명령어를 실행하여 PHP 버전이 정상적으로 조회되는지 검증합니다.
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
    a) `wget` 명령어를 사용하여 서버에서 직접 설치 패키지를 다운로드합니다. 예: `/var/www/` 디렉터리로 이동 후 명령어 `wget https://download.nextcloud.com/server/releases/nextcloud-19.0.1.zip` 실행
    b) 로컬 컴퓨터에 다운로드한 후 SFTP 또는 SCP 등 소프트웨어를 통해 `/var/www/` 디렉터리에 설치 패키지를 업로드합니다.
    c) 로컬 컴퓨터에 다운로드한 후 lrzsz를 사용하여 업로드합니다. 방법은 다음과 같습니다.
  1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
  2. `yum install lrzsz`를 실행하여 lrzsz를 설치합니다.
  3. `cd /var/www/`를 실행하여 타깃 디렉터리로 이동합니다.
  4. `rz -bye`를 실행하고 SSH 툴에서 로컬로 다운로드할 NextCloud 서버 설치 패키지를 선택합니다(해당 조작은 SSH 툴에 따라 상이함).
2. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
3. `unzip nextcloud-<version>.zip`을 실행하여 설치 패키지를 압축 해제합니다(예: `unzip nextcloud-19.0.1.zip`).

#### PHP 설정

1. SSH 툴을 사용하여 구매한 서버에 로그인합니다.
2. `vim /etc/php-fpm.d/www.conf`를 실행하여 PHP-FPM 구성 파일을 열고 순서대로 설정 항목을 수정합니다. vim의 구체적인 사용법은 관련 자료를 참조하십시오. 다른 방식을 사용해 해당 구성 파일을 수정할 수도 있습니다.
   a) `user = apache`를 `user = nginx`로 수정합니다.
    b) `group = apache`를 `group = nginx`로 수정합니다.
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
   a) `cp /etc/nginx/nginx.conf ~/nginx.conf.bak`를 실행하여 기존 구성 파일을 홈(HOME) 디렉터리에 백업합니다.
   b) SFTP 또는 SCP 등 소프트웨어를 사용하여 기존 구성 파일을 로컬 컴퓨터에 다운로드합니다.
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
            include fastcgi_params;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param PATH_INFO $path_info;
            fastcgi_param modHeadersAvailable true;
            fastcgi_pass 127.0.0.1:9000;
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

## COS 사용을 위한 NextCloud 서버 설정

### COS 관련 정보 획득

1. Tencent Cloud [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 이전에 생성한 버킷을 찾아 버킷 이름을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/13e02915f8c2846d7dfa5f2fec0c355b.png)
3. 리디렉션 인터페이스에 [기본 정보]의 **버킷 이름**과 **소속 리전** 영어 부분을 기록합니다.
   ![](https://main.qcloudimg.com/raw/2aef2ba23a6a32305ad39b4ef10a970c.png)

### API 키 획득

1. Tencent Cloud [액세스 키 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인합니다.
2. 표의 [키]에 있는 **SecretId**와 **SecretKey**를 기록합니다. 표에 유효한 키가 없는 경우 왼쪽 위의 [키 생성]을 클릭하여 새로운 키를 생성합니다.
   ![](https://main.qcloudimg.com/raw/ebc71eebfd0d247ec159f700792e43de.png)

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

다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/a0a2dfc8946015f346b74d0e43e2b3f5.png)

2. 해당 파일을 저장하고 `/var/www/nextcloud/config/` 디렉터리에 업로드합니다(파일 이름은 `config.php`로 유지). SFTP 또는 SCP 소프트웨어를 통해 파일을 업로드할 수 있고, `rz -bye` 명령어를 통해 업로드할 수도 있습니다.
3. 다음 명령어를 실행하여 구성 파일의 소유자를 수정합니다.
```bash
chown nginx:nginx /var/www/nextcloud/config/config.php
```

## 도메인 설정

IP 주소 대신 도메인을 사용하여 NextCloud 서버에 액세스할 경우 도메인 등록 대행 기관과 도메인 리졸브 서비스 관련 문서를 참조하여 새 도메인을 등록하고 도메인을 귀하의 CVM IP 주소로 리졸브하여 ICP비안을 완료할 수 있습니다.

NextCloud 서버는 설치 과정에서 설치 시 사용하는 도메인 또는 IP 주소를 기록하므로, 설치 전 도메인 등록과 리졸브를 완료한 다음 도메인을 사용해 NextCloud 서버의 보안 인터페이스에 액세스할 것을 권장합니다.

NextCloud 서버 설치 완료 후 도메인 또는 IP 주소를 변경해야 할 경우 직접 `/var/www/nextcloud/config/config.php` 구성 파일의 `trusted_domains`를 수정할 수 있습니다. 세부 사항은 [NextCloud 공식 홈페이지 문서](https://docs.nextcloud.com/server/19/admin_manual/installation/installation_wizard.html#trusted-domains)를 참조하십시오.

## NextCloud 서버 설치

1. 브라우저를 사용하여 NextCloud 서버에 액세스한 후 관리자 및 사용자 이름과 비밀번호를 생성하고 기억합니다.
2. [스토리지와 데이터베이스]를 펼쳐 아래 표의 설명에 따라 설정합니다.

| 설정 항목                             | 설정값                                      |
| ---------------------------------- | --------------------------------------- |
| 데이터 리스트                           | /var/www/nextcloud/data(기본값 유지)     |
| 데이터베이스 설정                         | MySQL/MariaDB                           |
| 데이터베이스 사용자                         | root                                    |
| 데이터베이스 비밀번호                         | TencentDB for MySQL 초기화 시 입력한 root 암호 |
| 데이터베이스 이름                           | nextcloud(또는 사용된 적 없는 다른 데이터베이스 이름)   |
| 데이터베이스 서버(기본값: localhost) | TencentDB for MySQL의 내부 네트워크 주소               |


3. [설치 완료]를 클릭하고 NextCloud 서버 설치가 완료될 때까지 기다립니다.
4. 설치 과정에서 504 Gateway Timeout과 같은 오류 정보가 뜨는 경우 새로 고치고 다시 시도합니다.
5. 설치 완료 후 관리자 계정을 사용해 NextCloud 서버에 로그인하면 웹 페이지 버전의 NextCloud를 사용할 수 있습니다.

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
위의 설정은 NextCloud 공식 홈페이지가 권장한 5분에 한 번(분 수는 5의 배수) 실행을 사용했습니다. 5분 후 백그라운드 작업이 완료되면 브라우저를 열어 NextCloud 서버에 로그인할 수 있습니다. 오른쪽 위 사용자 이름의 첫 알파벳 아이콘을 클릭하여 [설정]으로 이동합니다. 왼쪽 메뉴에서 [기본 설정]으로 이동하면 [백그라운드 작업]에서 Cron이 기본값으로 선택된 것을 볼 수 있습니다.



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