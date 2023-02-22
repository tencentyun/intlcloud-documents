Drupal은 PHP로 작성된 오픈 소스 콘텐츠 관리 프레임워크(Content Management Framework)로, 콘텐츠 관리 시스템(Content Management System)과 PHP 개발 프레임워크(Framework)로 구성되어 있습니다. Drupal은 개인 블로그에서 대규모 커뮤니티에 이르기까지 풍부한 기능을 갖춘 동적 웹 사이트를 구축하는 데 사용할 수 있습니다.
본 튜토리얼은 CVM 인스턴스에서 Drupal 전자상거래 웹사이트를 구축하는 방법을 설명합니다.
사용된 소프트웨어 환경: CentOS7.2, Drupal7.56, PHP5.4.16.

### CVM 인스턴스에 로그인
CVM 인스턴스 구매 및 접근 방법에 대한 자세한 내용은 [Linux 기반 CVM 시작하기](https://www.tencentcloud.com/document/product/213/10517)를 참고하십시오.

### MariaDB 서비스 설치
1. MariaDB는 기본적으로 CentOS v7 이상에서 지원되므로 여기서는 MariaDB를 사용합니다. `yum`을 사용하여 CVM 인스턴스에 MariaDB 서비스를 설치합니다.
```
yum install mariadb-server mariadb -y
```
2. MariaDB 서비스를 실행합니다.
```
systemctl start mariadb
```
3. Drupal용 데이터베이스(이름: drupal)를 생성합니다.
```
mysqladmin -u root -p create drupal
```
여기서 drupal은 Drupal 서비스에서 사용되는 데이터베이스 이름입니다.
4. 데이터베이스에 사용자를 생성합니다.
```
mysql -u root -p
```
사용자에게 권한을 부여하고 권한 부여가 성공한 후 데이터베이스를 종료합니다.
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON drupal.* TO 'username'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
exit
```
여기서 username은 Drupal 서비스에서 사용하는 데이터베이스 사용자 이름이며, password는 Drupal 서비스에서 사용하는 데이터베이스 비밀번호입니다.

### Apache 서비스 설치
1. CVM 인스턴스에 `yum`을 사용해 Apache를 설치합니다.
```
yum install httpd -y
```
2. Apache 서비스를 실행합니다.
```
service httpd start
```
3. Apache를 테스트합니다.
>!이 단계에서는 CVM 인스턴스의 보안 그룹에서 출처가 **all**이고 포트 프로토콜이 **TCP:80**인 인바운드 규칙을 구성해야 합니다. 보안 그룹을 구성하는 방법에 대한 자세한 내용은 [보안 그룹](https://intl.cloud.tencent.com/document/product/213/12452)을 참고하십시오.
>
로컬 브라우저에 `http://115.xxx.xxx.xxx/`를 입력합니다(여기서 `115.xxx.xxx.xxx`는 CVM 인스턴스의 공중망 IP). 다음 페이지가 나타나면 Apahce가 성공적으로 시작된 것입니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/uIMz720_4.png)

### PHP 설치 
1. `yum`을 사용하여 CVM 인스턴스에 PHP 및 해당 확장을 설치합니다.
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
4. 로컬 브라우저에 `http://115.xxx.xxx.xxx/info.php`를 입력합니다(여기서 `115.xxx.xxx.xxx`는 CVM 인스턴스의 공중망 IP). 다음 페이지가 나타나면 PHP가 성공적으로 설치된 것입니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/sphx991_5.png)

### Drupal 서비스 설치
1. Drupal 설치 패키지를 다운로드합니다.
```
wget http://ftp.drupal.org/files/projects/drupal-7.56.zip
```
2. 웹 사이트의 루트 디렉터리에 압축을 해제합니다.
```
unzip drupal-7.56.zip 
mv drupal-7.56/* /var/www/html/
```
3. 중국어 번역 키트를 다운로드합니다.
```
cd /var/www/html/
wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/7.x/drupal/drupal-7.56.zh-hans.po
```
4. `sites` 디렉터리가 속한 소유자 및 그룹을 수정합니다.
```
chown -R apache:apache /var/www/html/sites
```
5. Apache 서비스를 재시작합니다.
```
service httpd restart
```
6. 로컬 브라우저에 `http://115.xxx.xxx.xxx/`(여기서 `115.xxx.xxx.xxx`는 CVM 인스턴스의 공중망 IP)를 입력하여 Drupal의 설치 인터페이스로 이동하고 설치할 버전을 선택한 다음 [Save and continue]를 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/sphx991_5.png)
7. 설치 언어를 선택하고, [Save and continue]를 클릭합니다.
8. 데이터베이스를 설정하고, **mariadb 서비스 설치**에서 구성한 데이터베이스 정보를 입력합니다.
9. 사이트 정보를 입력합니다.
10. Drupal 설치를 완료합니다.
11. `http://115.xxx.xxx.xxx/`(여기서 `115.xxx.xxx.xxx`는 CVM 인스턴스의 공중망 IP)에 액세스하여 웹 사이트를 사용자 지정할 수 있습니다.
