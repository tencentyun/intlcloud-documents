## 작업 시나리오
LNMP 환경은 Linux 시스템에서 Nginx + MySQL + PHP 웹 사이트 서버 아키텍처를 나타냅니다. 본 문서는 openSUSE 42.3의 LNMP 환경 설정에 대해 설명합니다.
본 문서에는 소프트웨어 설치 내용이 있습니다. 소프트웨어 설치 방법을 숙지하시기 바랍니다. [openSUSE 환경에서 zypper를 통한 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2047)를 참조하십시오.
LNMP 구성 및 사용 버전 설명
- Linux: Linux 시리즈, 본문에서는 openSUSE42.3을 사용합니다.
- Nginx: Web 서버 프로그램은 Web 프로그램을 분석하며, Nginx1.14.2를 사용합니다.
- MySQL: 데이터베이스 관리 시스템으로 MySQL5.6.43을 사용합니다.
- PHP: Web 서버에서 웹 페이지를 생성하는 프로그램은 PHP7.0.7을 사용합니다.

## 작업 순서
### 미러 이미지 소스 구성
1. 클라우드 서버에 로그인하십시오.
2. 다음 커맨드를 실행하여 미러 이지미를 추가하십시오.
```
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/oss suseOss
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/non-oss suseNonOss
```
3. 다음 커맨드를 실행하여 미러 이미지 소스를 업데이트하십시오.
```
zypper ref
```

### Nginx 설치 구성
1. 다음 커맨드를 실행하여 Nginx를 설치하십시오.
``` 
zypper install -y nginx
```
2. 다음 커맨드를 순서대로 클릭하여 Nginx 서비스를 시작하고 재부팅 시 자동으로 서비스를 오픈하도록 설정하십시오.
```
systemctl start nginx
systemctl enable nginx
```
3. 다음 커맨드를 실행하여 Nignx 구성 파일을 수정하십시오.
```
vim /etc/nginx/nginx.conf
```
4. "**i**" 또는 "**Insert**"를 눌러 편집 모드로 전환하십시오.
5. server{...}를 찾고 다음 내용으로 바꾸십시오.
```
server {
	listen       80;
	server_name  localhost;

	#access_log  /var/log/nginx/host.access.log  main;
	location / {
			root   /srv/www/htdocs/;
			index  index.php index.html index.htm;
	}

	#error_page  404              /404.html;
	# redirect server error pages to the static page /50x.html
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
			root   /srv/www/htdocs/;
	}

	# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ \.php$ {
			root           /srv/www/htdocs/;
			fastcgi_pass   127.0.0.1:9000;
			fastcgi_index  index.php;
			fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
			include        fastcgi_params;
	}
}
```
7. 입력이 완료되면 "**Esc**"를 누르고 "**:wq**"를 입력하여 파일을 저장하고 돌아가십시오.
8. 다음 커맨드를 실행하여 Nginx 서비스를 재시작하십시오.
```
systemctl restart nginx
```
9. 다음 커맨드를 실행하여 새로운 `index.html` 홈페이지를 생성하십시오.
```
vi /srv/www/htdocs/index.html
```
10. “**i**” 또는 “**Insert**”를 눌러 편집 모드로 전환하고, 다음 내용을 입력하십시오:
```html
<p> hello world!</p>
```
10. 입력이 완료되면 "**Esc**"를 누르고 "**:wq**"를 입력하여 파일을 저장하고 돌아가십시오.
11. 브라우저에서 openSUSE 클라우드 서버 인스턴스의 공용 네트워크 IP에 액세스하여 Nginx 서비스가 정상적으로 실행되고 있는지 조회하십시오.
아래 이미지와 같이 새로운 Nignx의 설치 구성이 완료되었습니다.
![](https://main.qcloudimg.com/raw/df09d1fe6baed50cebd89ef7402db4b2.png)

### MySQL 설치 구성
1. 다음 커맨드를 실행하여 MySQL을 설치하십시오.
```
zypper install -y mysql-community-server mysql-community-server-tools
```
2. 다음 커맨드를 순서대로 실행하여 MySQL 서비스를 시작하고 재부팅 시 자동으로 서비스를 오픈하도록 설정하십시오.
```
systemctl start mysql 
systemctl enable mysql
```

3. 다음 커맨드를 실행하여 MySQL에 최초 로그인하십시오.
> MySQL에 최초 로그인하면 시스템에 비밀번호를 문의 메시지가 표시됩니다. 비밀번호 입력 작업이 진행하지 않으면 **Enter**를 눌러 MySQL에 이동하십시오.
>
```
mysql -u root -p
```
MySQL에 성공적으로 이동되었습니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/1e9daf876fb08c70674789865688f695.png)
4. 다음 커맨드를 실행하여 root 비밀번호를 수정하십시오.
```
update mysql.user set password = PASSWORD('새로운 비밀번호를 입력하십시오') where user='root';
```
5. 다음 커맨드를 실행하여 구성을 활성화하십시오.
```
flush privileges;
```
6. 다음 커맨드를 실행하여 MySQL을 종료하십시오.
```
\q
```

### PHP 설치 및 구성
다음 커맨드를 실행하여 PHP를 설치하십시오.
```
zypper install -y php7 php7-fpm php7-mysql
```

### Nginx와 PHP-FPM의 통합
1. 다음 커맨드를 순서대로 실행하여, `/etc/php7/fpm` 디렉터리에 이동하여 'php-fpm.conf.default' 파일을 복사하고 `php-fpm.conf` 파일로 이름을 바꾸십시오.
```
cd /etc/php7/fpm
cp php-fpm.conf.default php-fpm.conf
``` 
2. 다음 커맨드를 순서대로 실행하여, `/etc/php7/fpm/php-fpm.d` 디렉터리에 이동하여 `www.conf.default` 파일을 복사하고 `www.conf` 파일로 이름을 바꾸십시오.
```
cd /etc/php7/fpm/php-fpm.d
cp www.conf.default www.conf
```
4. 다음 커맨드를 순서대로 클릭하여 서비스를 시작하고 재부팅 시 자동으로 서비스를 오픈하도록 설정하십시오.
```
systemctl start php-fpm
systemctl enable php-fpm
```

## 환경 구성 검증
1. 다음 커맨드를 실행하여 테스트 파일 index.php를 만드십시오.
```
vim /srv/www/htdocs/index.php
```
2. “**i**” 또는 “**Insert**”를 눌러 편집 모드로 전환하고, 다음 내용을 입력하십시오.
```
<?php
	echo "hello new world!";
?>
```
3. "**Esc**"를 누르고 "**:wq**"를 입력하여 파일을 저장하고 돌아가십시오.
4. 브라우저에서 openSUSE 클라우드 서버의 공용 네트워크 IP에 액세스하십시오.
아래 이미지와 같이 LNMP 환경 설정이 완료되었습니다.
![](https://main.qcloudimg.com/raw/0adc6168e7407931c597228520b35413.png)

