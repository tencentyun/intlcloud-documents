LAMP는 Linux+Apache+Mysql/MariaDB+Perl/PHP/Python을 가리키며, 동적 웹사이트 또는 서버를 구축하는 데 사용되는 오픈 소스 소프트웨어입니다. 프로그램은 각각 독립적이지만, 항상 함께 사용되기 때문에 상호 호환성이 점점 증가하고 있습니다. 또한 공동으로 강력한 Web 응용 프로그램 플랫폼을 구성합니다.
본 튜토리얼은 사용자가 다음 과정을 완료할 수 있도록 안내합니다: 1개의 Tencent CDB 인스턴스를 실행하고, Tencent CVM을 통해 1개의 LAMP 응용 프로그램을 설정하여, Tencent CDB 인스턴스의 고가용성 환경을 연결하는데 사용합니다.
Tencent CDB 인스턴스를 실행하면 데이터베이스와 환경의 라이프사이클을 각각 분리합니다. 이를 통해 사용자가 여러 서버에서 동일한 데이터베이스로 연결할 수 있도록 합니다. 또한 사용자가 데이터베이스 설치, 배포, 버전 업데이트 및 장애 처리 등의 문제에 더 이상 신경 쓰지 않을 수 있도록 데이터베이스의 유지보수를 간소화합니다.

>?본 튜토리얼에서 사용하는 CDB 인스턴스와 CVM 인스턴스는 동일 리전에 속합니다. 사용자의 CDB 인스턴스와 CVM 인스턴스가 다른 리전에 속할 경우, [외부 네트워크 액세스](https://intl.cloud.tencent.com/document/product/236/3130)를 참조하십시오.

### CDB 인스턴스 초기화
CDB의 구매와 초기화는 [구매 방식](https://intl.cloud.tencent.com/document/product/236/5160)과 [MySQL 데이터베이스 초기화](http://intl.cloud.tencent.com/document/product/236/3128)를 참조하십시오.

### CVM 인스턴스에 로그인하십시오.
CVM의 구매와 액세스는 [Linux CVM 시작하기](http://intl.cloud.tencent.com/document/product/213/2936)를 참조하십시오. 본 튜토리얼에서는 CentOS 시스템을 사용합니다.

### MySQL 클라이언트 설치
1. CVM 인스턴스에서 `yum`을 사용해 MySQL 클라이언트를 설치합니다.
```
yum install mysql -y
```
![](//mc.qcloudimg.com/static/img/8b952d6d7d767413a6558e82df092d44/image.png)
2. 설치가 완료되면 Tencent CDB 인스턴스에 연결됩니다.
```
mysql -h hostname -u username -p
```
![](//mc.qcloudimg.com/static/img/297856a53959582220b9bba6f06ce9f6/image.png)
이 중, hostname은 데이터베이스 인스턴스의 개인 IP 주소이며, username은 사용자의 데이터베이스 사용자 이름입니다.
3. 연결 성공 후 즉시 데이터베이스에서 나가 다음 작업을 진행할 수 있습니다.
```
quit;
```

### Apache 서비스 설치
1. CVM 인스턴스에서 `yum`을 사용해 Apache를 설치합니다.
```
yum install httpd -y
```
![](//mc.qcloudimg.com/static/img/dc142f813e8e8474a5994e2e841828f2/image.png)
2. Apache 서비스를 실행합니다.
```
service httpd start
```
3. Apache 테스트
>!이 단계에서 사용자는 CVM 보안 그룹에서 출처를 **all**로 설정하고, 포트 프로토콜을 **TCP:80**인 Inbound rule로 설정해야 합니다. 보안 그룹 설정은 [Security Group](http://intl.cloud.tencent.com/document/product/213/12452)을 참조하십시오.
>
사용자 로컬 브라우저에 `http://xxx.xxx.xxx.xxx/`를 입력하면(이 중, `xxx.xxx.xxx.xxx`는 사용자의 CVM 공인 IP 주소입니다), 다음 화면이 나타나면서 Apache가 실행됩니다.
![](https://main.qcloudimg.com/raw/80941070a1a309ba484527473c915221.png)

### PHP 설치 
1. CVM 인스턴스에서 `yum`을 사용해 PHP를 설치합니다.
```
yum install php -y
```
![](//mc.qcloudimg.com/static/img/61a0864ddbb70e65c63ad5093e8165d4/image.png)

### 프로젝트 테스트 LAMP 환경 생성
1. 아래의 예시 코드와 같이, CVM의 `/var/www/html` 디렉터리에서 1개의 info.php 파일을 생성합니다.
```
<?php phpinfo(); ?>
```
2. Apache 서비스를 재시작합니다.
```
service httpd restart
```
3. 사용자 로컬 브라우저에 `http://xxx.xxx.xxx.xxx/info.php`를 입력하면(이 중, `xxx.xxx.xxx.xxx`는 사용자의 CVM 공인 IP 주소입니다), 다음 화면이 나타나면서 LAMP 서비스 배포에 성공합니다.
![](//mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)
