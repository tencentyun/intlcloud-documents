본 문서는 Windows Server 2012 R2 예시를 사용하여 MySQL 5.5 구축 순서에 대해 자세히 소개합니다.

일반적으로 Windows 시스템은 SQL Server 데이터베이스를 사용하지만, SQL Server는 유료 제품으로서 사용자가 직접 권한을 부여하므로 [Tencent Cloud SQL Server 데이터베이스 CDB 인스턴스](http://cloud.tencent.com/product/sqlserver.html)를 구매할 수 있습니다.

## 1단계: MySQL 설치 패키지 다운로드
&nbsp;&nbsp;&nbsp;CVM에서 브라우저를 열고 다운로드 주소를 입력합니다:https://dev.mysql.com/downloads/mysql/5.5.html#downloads
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](//mc.qcloudimg.com/static/img/b1da1513321247e0daf1163f529d4cd9/image.png)

## 2단계: 프로그램 설치
 1. 설치 프로그램을 실행하여 [다음 단계(Next)]를 클릭한 후 프로토콜 동의에 체크합니다.
![](//mc.qcloudimg.com/static/img/8dd2fc106b09c3538c1dd407c02adea4/image.png)
 
 2. 일반 설치 방식(Typical)을 선택합니다.
![](//mc.qcloudimg.com/static/img/9f45d5441da017feca7eb9bdc11260fd/image.png)

 3. MySQL 설정 가이드 옵션(Luanch the MySQL Instance Configuration Wizard)에 체크합니다.
	![](//mc.qcloudimg.com/static/img/1a6b6ad499c0c00d294d6f24d5ee1645/image.png)

## 3단계: MySQL 설정


 1. MySQL의 유형을 설정합니다. 여기에서는 상세 설정(Detailed Configuration)을 예시로 사용합니다.
  - 상세 설정(Detailed Configuration)은 서버 설정을 보다 세밀하게 제어하기 원하는 고급 사용자에게 적합합니다.
  - 표준 설정(Standard Configuration)은 서버 설정을 고려하지 않고 MySQL의 빠른 시작을 원하는 신규 사용자에게 적합합니다.
 
 > **참고: **
 > 표준 설정(Standard Configuration)은 운영 체제와 호환되지 않을 수 있습니다. 상세 설정을 선택하길 권장합니다.

	![](//mc.qcloudimg.com/static/img/434424a84d76f9492c511f567ae2d03f/image.png)
 
 2. MySQL 서버 유형을 설정합니다. 여기서는 개발자 기기(Developer Machine)를 예시로 사용합니다.
  - 개발자 기기(Developer Machine)는 일반적인 개인용 데스크탑 워크스테이션을 대표합니다. 여러 데스크탑 애플리케이션을 동시에 실행할 경우 MySQL 서버가 최소한의 리소스를 차지하도록 설정됩니다.
  - 서버 기기(Server Machine)는 서버를 말합니다. MySQL 서버는 FTP, email 및 web 서버 등 다른 애플리케이션과 동시에 실행할 수 있습니다. MySQL 서버는 적정량의 리소스를 차지하도록 설정됩니다.
  - MySQL 전용 서버 기기(Dedicated MySQL Server Machine)는 MySQL 서비스만 실행하는 서버를 말합니다. MySQL 서버는 모든 리소스를 차지하도록 설정됩니다.

	![](//mc.qcloudimg.com/static/img/11b1162dd70e46882a43933f517dcaf4/image.png)

 3. MySQL 데이터베이스를 설정합니다. 여기서는 멀티 기능 데이터베이스(Multifunctional Database)를 예시로 사용합니다.
  - 멀티 기능 데이터베이스(Multifunctional Database)는 InnoDB와 MyISAM 스토리지 엔진을 동시에 사용하고, 두 엔진 간에 리소스를 균일하게 할당합니다. 주로 2개의 스토리지 엔진을 사용하는 사용자에게 추천합니다.
  - 트랜잭션 데이터베이스만 처리(Transactional Database Only)는 InnoDB와 MyISAM 스토리지 엔진을 동시에 사용하며, 대부분의 서버 리소스를 InnoDB 스토리지 엔진에 보냅니다. InnoDB의 사용 빈도가 높고 MyISAM은 가끔 사용하는 사용자에게 추천합니다.
  - 비 트랜잭션 데이터베이스만 처리(Non-Transactional Database Only)는 InnoDB 스토리지 엔진의 사용을 완전히 금지하고, 모든 서버 리소스를 MyISAM 스토리지 엔진에 보냅니다. InnoDB를 사용하지 않는 사용자에게 추천합니다.
 
 ![](//mc.qcloudimg.com/static/img/37972855d5c880e59b5310a7872491f1/image.png)

 4. MySQL의 InnoDB 테이블 용량을 설정합니다. 여기서는 기본 설정을 선택합니다.
	![](//mc.qcloudimg.com/static/img/c4c8e8710e27b202a9694b2c1be0f4f6/image.png)

 5. MySQL 동시 접속을 설정합니다. 여기서는 의사 결정 지원(Decision Support)을 예시로 사용합니다.
  - 의사 결정 지원(Decision Support), 대량의 동시 연결이 필요 없는 상황에 적합합니다.
  - 온라인 트랜잭션 처리(Online Transaction Processing), 대량의 동시 연결이 필요한 상황에 적합합니다.
  - 수동 설정(Manual Setting), 서버 동시 연결 최댓값을 수동 설정하기에 적합합니다.
 
 ![](//mc.qcloudimg.com/static/img/ef17aa905ea5bdd50b1ad61b416be4ea/image.png)

 6. MySQL의 네트워크 옵션을 설정합니다. TCP/IP 네트워크 사용 또는 사용 금지를 설정하고, MySQL 서버 연결에 사용되는 포트 번호를 설정할 수 있습니다.
 > **참고: **
 > 기본 상태에서 TCP/IP 네트워크 시작
 > 3306 포트 기본 사용
 
	 ![](//mc.qcloudimg.com/static/img/b864e47b1e4b0e87cd5015007f9bd8dc/image.png)

 7. MySQL 문자 세트를 설정합니다. 여기서는 표준 문자 세트(Standard Character Set)를 예시로 사용합니다.
  - 표준 문자 세트(Standard Character Set), Latin1을 서버의 기본 문자 세트에 사용합니다.
  - 다중 언어 지원(Best Support For Multilingualism), UTF8을 서버의 기본 문자 세트에 사용합니다.
  - 수동 설정/교정 규칙(Manual Selected Default Character Set/Collation), 목록에서 원하는 문자 세트를 선택합니다.
 
	![](//mc.qcloudimg.com/static/img/31c4f7f13a2b5b6aa0754cc3e4bd526e/image.png)

 8. MySQL 서비스 옵션을 선택합니다. 명령줄로 MySQL을 관리할 수 있도록 두 가지 모두 선택할 것을 권장합니다.
	![](//mc.qcloudimg.com/static/img/9f24e245f4b5d08e9d0658aa21cd70cd/image.png)

 9. root 비밀번호를 설정합니다.
	![](//mc.qcloudimg.com/static/img/65a265bcc69d6a75f0da51387dd3aedf/image.png)

 10. 설정 완료. [Excute]를 클릭하여 설치를 완료합니다.
	![](//mc.qcloudimg.com/static/img/fd815f05c40d11c61d801a321131e3ec/image.png)

## 4단계: MySQL 테스트 로그인

1. CVM에서 [시작]을 클릭하고 [검색(아이콘)]을 클릭한 후 ```cmd```를 입력하여 관리자 명령 창을 엽니다.
![](//mc.qcloudimg.com/static/img/c7920f20daff62d136f6ba7987fb2ac8/image.png)

2. 명령어 ```mysql -u root -p```를 입력하고 엔터를 누릅니다.
 
3. 설정한 root 비밀번호로 MySQL에 로그인하면 다음의 그림과 같이 설치 성공 화면이 표시됩니다.
![](//mc.qcloudimg.com/static/img/18aef21cabf34db1bca266a8977018f4/image.png)


