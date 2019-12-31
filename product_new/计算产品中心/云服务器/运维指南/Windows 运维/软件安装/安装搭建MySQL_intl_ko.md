## 작업 시나리오
본 문서는 Windows Server 2012 R2 데이터센터 버전인 64비트 중문 버전 운영 체제 CVM을 예로 합니다. MySQL 5.5를 구축하기 위한 자세한 순서를 소개합니다.
일반적으로 Windows 시스템은 SQL Server 데이터를 사용하지만 SQL Server 는 유료 제품으로서 사용자가 직접 권한을 부여하거나 [TencentDB for SQL Server 인스턴스](http://cloud.tencent.com/product/sqlserver.html)를 구매할 수 있습니다.

## 작업 순서

### MySQL 설치 패키지 다운로드
1. CVM에 로그인하십시오.
2. CVM에서 브라우저를 열고 `https://dev.mysql.com/downloads/mysql/5.5.html#downloads` 를 액세스한 후 MySQL 설치 패키지를 다운로드합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/b96236244404b3e65d3e750dec8ea8c0.png)

### MySQL 설치

1. 더블 클릭으로 MySQL 설치 패키지를 열고 "MySQL Server 5.5 Setup" 설치 인터페이스에서[Next]를 클릭합니다.
2. [I accept the terms in the License Agreement]를 선택하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/fd10bf4885214fc586940663f37b29bd.png)
3. [Typical]를 클릭합니다. 아래 이미지를 참조하십시오.
Typical 은 일반적인 설치 방법을 표시합니다.
![](https://main.qcloudimg.com/raw/85292c920bafd81c341e23214c01eac7.png)
4. [Install]을 클릭하고 MySQL를 설치합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/e4e73dd70f382ed5d3abcbda619f07ea.png)
5. [Luanch the MySQL Instance Configuration Wizard]를 선택하고[Finish]를 클릭합니다. 아래 이미지를 참조하십시오.
MySQL 설치 창을 종료하고 MySQL 의 구성 가이드 인터페이스에 진입합니다.
![](https://main.qcloudimg.com/raw/46932c0a2868178be1cbdb1af02a1716.png)

### MySQL 구성

1. MySQL 구성 가이드 인터페이스에서[Next]를 클릭합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/018a37f73b3493f2f72a58393530eb60.png)
2.[Detailed Configuration]를 선택하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
> 작업 순서는 Detailed Configuration 를 예로 들어 설명합니다.
>
![](https://main.qcloudimg.com/raw/64374e0257e0b5c13838bd4fc2a3631e.png)
 - Detailed Configuration(상세 구성)은 서버 구성을 보다 세밀하게 제어하려는 고급 사용자에게 적합합니다.
 - Standard Configuration(표준 구성)은 서버 구성을 고려하지 않고 빠른 MySQL 시작을 요구하는 신규 사용자에게 적합합니다. 표준 구성은 운영 체제와 호환되지 않을 수 있어 상세 구성 선택을 권장합니다.
3. [Developer Machine]을 선택하고[Next]를 클릭합니다. 아래 이미지를 참조하십시오.
> 작업 순서는 Developer Machine 를 예로 들어 설명합니다.
>
![](https://main.qcloudimg.com/raw/40ba999555a5f7de8299aeb09b4f7fdd.png)
 - Developer Machine(개발자 기기)은 일반적인 개인용 바탕 화면 작업 스테이션을 대표합니다. 여러 바탕 화면 애플리케이션을 동시에 실행할 경우 MySQL 서버는 최소 리소스를 차지하는 상태로 구성됩니다.
 - Server Machine(서버 기기)은 서버를 대표합니다. MySQL 서버는 FTP,  email 및 web 서버 등 다른 애플리케이션을 동시에 실행합니다. MySQL 서버는 적절한 비율의 리소스를 차지하는 상태로 구성됩니다.
 - Dedicated MySQL Server Machine(MySQL 서버 전용)은 MySQL 서비스만 실행하는 서버를 대표합니다. MySQL 서버는 모든 리소스를 차지하는 상태로 구성됩니다.
4. [Multifunctional Database]를 선택하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
> 작업 순서는 Multifunctional Database 를 예로 들어 설명합니다.
>
![](https://main.qcloudimg.com/raw/20a581e1af44694cc0f3188438f10742.png)
 - Multifunctional Database(멀티 기능 데이터베이스)는 동시에 InnoDB 및 MyISAM 스토리지 엔진을 사용하고 두 엔진 사이에 리소스를 평균으로 할당합니다. 두 스토리지 엔진을 자주 사용하는 사용자에게 추천합니다.
 - Transactional Database Only(트랜잭션 데이터베이스만 처리)는 동시에 InnoDB 및 MyISAM 스토리지 엔진을 사용하며 대부분 서버 리소스는 InnoDB 스토리지 엔진에 보냅니다. InnoDB를 자주 사용하고 MyISAM은 가끔 사용하는 사용자에게 추천합니다.
 - Non-Transactional Database Only(비 트랜잭션 데이터베이스만 처리)은 InnoDB 스토리지 엔진 사용을 전면 금지하고 모든 서버 리소스를 MyISAM 스토리지 엔진에 보냅니다. InnoDB 을 사용하지 않는 사용자에게 추천합니다.
5. 기존 구성을 유지하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/7cef832b46fdf9855d02e21762ce8978.png)
6. [Decision Support (DSS)/OLAP]를 선택하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
> 작업 순서는 Decision Support (DSS)/OLAP 을 예로 들어 설명합니다.
>
![](https://main.qcloudimg.com/raw/6e0158904bd05862c423d84b33adb260.png)
 - Decision Support (DSS)/OLAP(의사 결정 지원)은 대량의 병렬 연결이 않은 상황에 적합합니다.
 - Online Transaction Processing (OLTP)(온라인 트랜잭션 처리)은 대량의 병렬 연결이 필요한 상황에 적합합니다.
 - Manual Setting(인공 설정)은 수동 설정으로 서버에 연결하는 최댓값입니다.
7. TCP/IP 네트워크를 설정하여 MySQL 서버에 연결된 포트 번호를 구성하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
> 
> - TCP/IP 네트워크 기본 시작
> - 3306 포트 기본 사용
> 
![](https://main.qcloudimg.com/raw/15dafbfbb27d6195effc8d94aa9a109f.png)
8. [Standard Character Set]를 선택하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
> 작업 순서는 Standard Character Set 를 예로 들어 설명합니다.
>
![](https://main.qcloudimg.com/raw/d995acdb742ead678d3909305e560e7f.png)
 - Standard Character Set(표준 문자 세트)는 Latin1 서버 문자 세트를 기본으로 합니다.
 - Best Support For Multilingualism(다중 언어 지원)은 UTF8 서버 문제 세트를 기본으로 합니다.
 - Manual Selected Default Character Set/Collation(인공 설정/교정 규칙)은 아래 목록에서 문자 세트를 선택합니다. 
9. [Install As Windows Service]와 [Include Bin Directory in Windows PATH]을 선택하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/4e3f9b7c330a0f59e3ed319ddc8b882d.png)
10. root 비밀번호를 설정하고 [Next]를 클릭합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/8c66302686ca7c47eb32583b4722e4f8.png)
11. [Execute]를 클릭하고 MySQL를 구성합니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/328fa1f3eb39ed00f9492ffcf5b93c46.png)
12.[Finish]를 클릭하고 구성을 완료합니다.

### MySQL 설치 성공 여부 검증

1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> > [실행]을 마우스 우클릭하여 실행 창을 엽니다.
2. 실행 창에 **cmd**를 입력하고 **Enter**를 누르면 관리자 커맨드 창이 열립니다.
3. 관리자 커맨드 창에서 다음 명령어를 실행합니다.
```
mysql -u root -p
```
4. 설정한 root 비밀번호를 입력하고 **Enter**를 눌러 MySQL에 로그인합니다.
다음과 같은 인터페이스 정보가 나타나면 구성이 성공적으로 설치되었음을 표시합니다.




