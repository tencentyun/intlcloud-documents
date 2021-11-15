Drupal은 PHP 언어를 사용하여 작성한 오픈 소스 콘텐츠 관리 프레임워크(Content Management Framework)로, 콘텐츠 관리 시스템(Content Management System)과 PHP 개발 프레임워크Framework)로 구성되어 있습니다. Drupal은 여러 가지 기능과 서비스를 제공하는 동적 웹 사이트 구축에 사용되며, 개인 블로그부터 대형 SNS 사이트까지 다양한 애플리케이션의 웹 사이트 프로젝트를 지원합니다.
본 튜토리얼을 통해 Tencent Cloud CVM에서의 Drupal 전자 상거래 웹 사이트 구축 방법을 확인할 수 있습니다.
소프트웨어 사용 환경: CentOS7.2, Drupal7.56, PHP5.4.16

### CVM 인스턴스에 로그인


### MariaDB 서비스 설치
1. CentOS7 이상 버전에서는 기본적으로 MariaDB 데이터베이스를 지원하므로 MariaDB 데이터베이스를 사용합니다. CVM 인스턴스에서 `yum`을 사용해 MariaDB 서비스를 설치합니다.
```
yum install mariadb-server mariadb -y
```
2. MariaDB 서비스를 실행합니다.
```
systemctl start mariadb
```
3. Drupal에 데이터베이스를 생성합니다(본 튜토리얼에서는 데이터베이스 이름을 drupal로 지정).
```
mysqladmin -u root -p create drupal
```
여기서 drupal은 Drupal 서비스에서 사용하는 데이터베이스 이름입니다.
4. 데이터베이스에 사용자를 생성합니다.
```
mysql -u root -p
```
사용자에게 권한을 부여한 후, 데이터베이스에서 로그아웃합니다.
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON drupal.* TO 'username'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
exit
```
여기서 username은 Drupal 서비스에서 사용하는 데이터베이스 사용자 이름이며, password는 Drupal 서비스에서 사용하는 데이터베이스 비밀번호입니다.

### Apache 서비스 설치
1. CVM 인스턴스에서 `yum`을 사용해 Apache를 설치합니다.
```
yum install httpd -y
```
2. Apache 서비스를 실행합니다.
```
service httpd start
```
3. Apache를 테스트합니다.
>!이 단계에서 사용자는 CVM 보안 그룹에서 출처를 **all**로 설정하고, 포트 프로토콜을 **TCP:80**인 Inbound rule로 설정해야 합니다. 보안 그룹 설정은 [보안 그룹](https://cloud.tencent.com/document/product/213/12452)을 참조하십시오.
>
>사용자 로컬 브라우저에 `http://115.xxx.xxx.xxx/`를 입력하면(`115.xxx.xxx.xxx`는 사용자의 CVM 공용 IP 주소), 다음 화면이 나타나면서 Apache가 실행됩니다.
>![](https://main.qcloudimg.com/raw/c9b20e150bd5330feef6d978b8308629.png)

### PHP 설치 
1. CVM 인스턴스에서 `yum`을 사용해 PHP와 PEAR(PHP Extension and Application Repository)를 설치합니다.
```
yum install php php-dom php-gd php-mysql php-pdo -y
```
2. 아래의 예시 코드와 같이, CVM의 `/var/www/html` 디렉터리에 info.php 파일을 생성하여 PHP가 성공적으로 설치되었는지 확인합니다.
```
<?php phpinfo(); ?>
```
3. Apache 서비스를 재시작합니다.
```
service httpd restart
```
4. 사용자 로컬 브라우저에 `http://115.xxx.xxx.xxx/info.php`를 입력합니다(`115.xxx.xxx.xxx`는 사용자의 CVM 공용 IP 주소). 다음 화면이 나타나면 PHP 설치가 완료된 것입니다.
![](//mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)

### Drupal 서비스 설치
1. Drupal 설치 패키지를 다운로드합니다.
```
wget http://ftp.drupal.org/files/projects/drupal-7.56.zip
```
2. 웹 사이트 루트 디렉터리에 압축 해제합니다.
```
unzip drupal-7.56.zip 
mv drupal-7.56/* /var/www/html/
```
3. 중국어 번역 패키지를 다운로드합니다.
```
cd /var/www/html/
wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/7.x/drupal/drupal-7.56.zh-hans.po
```
4. `sites` 디렉터리의 소속 마스터 그룹을 변경합니다.
```
chown -R apache:apache /var/www/html/sites
```
5. Apache 서비스를 재시작합니다.
```
service httpd restart
```
6. 사용자의 로컬 브라우저에 `http://115.xxx.xxx.xxx/`를 입력합니다(`115.xxx.xxx.xxx`는 사용자의 CVM 공용 IP 주소). Drupal 설치 인터페이스에서 설치 버전을 선택하고, [Save and continue]를 클릭합니다.
![](https://main.qcloudimg.com/raw/f52af1bb9822ddefc1989df9a0a95e8c.png)
7. 설치 언어를 선택하고, [Save and continue]를 클릭합니다.
![](https://main.qcloudimg.com/raw/11a8f788ebd0595e6afdff936656c2cc.png)
8. 데이터베이스를 설정하고, **mariadb 서비스 설치**에서 설정한 데이터베이스 정보를 입력합니다.

9. 사이트 정보를 입력합니다.

10. Drupal 설치를 완료합니다.

11. 추후 `http://115.xxx.xxx.xxx/`(`115.xxx.xxx.xxx`는 사용자의 CVM 공용 IP 주소)에 액세스해 웹 사이트를 개성화할 수 있습니다.