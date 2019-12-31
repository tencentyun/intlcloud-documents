Tencent Cloud는 클라우드 서버에서 소프트웨어 설치의 효율성을 향상하고 소프트웨어 다운로드 및 설치 비용을 줄이기 위해 Yum 다운로드 소스를 제공합니다. CentOS 환경에서 YUM을 통해 소프트웨어를 빠르게 설치할 수 있습니다.

Yum 다운로드 소스에 소프트웨어 소스를 추가할 필요없이 직접 패키지를 설치할 수 있습니다.

## 1. 설치 순서

1) root 권한으로 다음 커맨드를 통해 소프트웨어를 설치하십시오.
```
yum install [nginx][php][php-fpm][mariadb][mariadb-server][mysql][mysql-server]...
```

> 참고: CentOS 7부터 MariaDB는 yum 소스의 기본 데이터베이스 설치 패키지가 되었으며, CentOS 7 이상의 시스템에서 yum을 사용해 MySQL 패키지를 설치하면 MySQL을 사용할 수 없게 됩니다. 완전히 호환되는 MariaDB를 선택하거나 [여기](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7)를 참조하면서 MySQL 하위 버전을 설치할 수 있습니다.


2) 시스템은 관련 소프트웨어 패키지 및 종속 관계를 자동으로 검색하고, 사용자가 검색한 소프트웨어 패키지가 적합한지 여부를 확인하도록 인터페이스에 제시합니다. 아래 이미지를 참조하십시오.
![](http://mccdn.qcloud.com/static/img/f61a066066619f09fed1be6fa4a8a4b0/image.png)

3) "y" 입력 확인 후 소프트웨어 설치 시작 및 완료하면 "Complete"가 나타납니다. 아래 이미지를 참조하십시오.
![](http://mccdn.qcloud.com/static/img/e36f74f325c00814c3c840aeda9c26a6/image.png)

## 2. 설치된 소프트웨어 정보 조회
소프트웨어 설치 완료 후 다음 커맨드를 통해 소프트웨어 패키지의 구체적인 설치 디렉토리를 조회할 수 있습니다.

```
 rpm -ql 
```
예를 들면, nginx의 설치 디렉토리를 조회합니다.
![](http://mccdn.qcloud.com/img56a61fa482658.png)

다음 커맨드를 통해 소프트웨어 패키지의 버전 정보를 조회할 수 있습니다.
```
 rpm -q 
```
예를 들면, nginx의 버전을 쿼리합니다(실제 버전은 본 버전은 일치하지 않을 수 있으므로 실제로 쿼리한 버전을 기준으로 하십시오).
![](http://mccdn.qcloud.com/img56a621c372e23.png)