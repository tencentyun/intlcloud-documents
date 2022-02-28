
## 연결 방식
다음과 같은 방법으로 TDSQL for MySQL 인스턴스에 연결할 수 있습니다.
- **내부 네트워크 주소 연결**: 내부 네트워크 주소를 통해 TDSQL for MySQL을 연결하고 CVM을 사용해 CDB의 내부 네트워크 주소에 직접 연결합니다. 이 방식은 내부 고속 네트워크를 사용하므로 딜레이가 낮습니다.
 - CVM과 데이터베이스의 계정이 동일해야 하며, 동일한 [VPC](https://intl.cloud.tencent.com/document/product/215/535) 내(동일한 리전)에 있거나 기본 네트워크가 동일해야 합니다.
 - 내부 네트워크 주소는 기본적으로 TencentDB에서 제공하며 인스턴스 목록 또는 [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)의 인스턴스 세부 정보 페이지에서 볼 수 있습니다.
>?서로 다른 VPC(동일 계정/다른 계정, 동일 리전/다른 리전 포함)의 CVM과 데이터베이스에 대한 내부 네트워크 연결 방식은 [CCN](https://intl.cloud.tencent.com/zh/document/product/1003)을 참고하십시오.
>
- **외부 네트워크 주소 연결**: 내부 네트워크에 액세스할 수 없는 경우 외부 네트워크 주소에서 TDSQL for MySQL 인스턴스에 연결할 수 있습니다. 외부 네트워크 주소는 수동으로 활성화해야 합니다. 이는 [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)의 인스턴스 세부 정보 페이지에서 볼 수 있으며 더 이상 필요하지 않은 경우 비활성화할 수 있습니다.
 - 외부 네트워크 주소를 활성화하면, 데이터베이스 서비스가 공용 네트워크에 노출되어 데이터베이스가 침입 혹은 공격을 받을 수 있으므로, 내부 네트워크를 사용해 데이터베이스에 연결하시기를 권장합니다. 
 - CDB의 외부 네트워크 연결은 데이터베이스의 개발 혹은 관리 보조 시에 적합합니다. DDOS 공격, 돌발적인 대용량 트래픽 액세스 등과 같은 통제 불가능한 요소로 인해 외부 네트워크 연결을 사용할 수 없게 될 수 있으므로, 정식 비즈니스 연결에는 사용하지 않을 것을 권장합니다.

## 준비 작업
### 계정 생성
1. [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인합니다. 인스턴스 목록에서 인스턴스 ID 또는 ‘작업’ 열의 [관리]를 클릭하여 인스턴스 관리 페이지에 액세스합니다.
2. [계정 관리] 탭을 선택하고 [계정 생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/148943eb024c9d3871b3c5d509de2e20.png)
3. 팝업 창에서 계정 이름, 호스트, 비밀번호, 비고를 입력합니다. 모든 것이 올바른지 확인한 후 [확인]을 클릭합니다.
호스트 이름은 실제로 네트워크 송신 주소입니다. 필요한 경우 %를 입력하여 이 인스턴스가 모든 IP에 액세스할 수 있음을 나타낼 수 있습니다.
4. 권한 수정 창에서 필요에 따라 권한을 할당한 후 [설정 저장]을 클릭하면 권한 할당이 완료됩니다. 나중에 권한을 설정하려면 [나중에 설정]을 클릭합니다.
왼쪽의 사이드바는 MySQL 관리와 완전히 호환되는 그래픽 인터페이스를 제공합니다. 권한은 열 수준에서 관리할 수 있습니다.
![](https://main.qcloudimg.com/raw/4a6bdfb7e48222945440db418e7f6de1.png)
5. 계정 목록으로 돌아가서 [권한 수정]을 클릭하여 사용자 권한을 수정하고 [계정 복제]를 클릭하여 현재 계정 권한을 완전히 복사하여 새 계정을 만듭니다. [더보기]를 클릭하여 비밀번호를 재설정하고 계정을 삭제합니다.
![](https://main.qcloudimg.com/raw/fe697afd0c76d921ce7961f4c57a9017.png)

### (옵션)외부 네트워크 주소 활성화
1. [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인하고 인스턴스 목록에서 인스턴스 ID를 클릭하여 인스턴스 세부 정보 페이지로 들어간 다음 기본 정보 섹션에서 ‘외부 네트워크 IP’ 옆에 있는 [활성화]를 클릭합니다.
![](https://main.qcloudimg.com/raw/71a29582f85cbda585ed586341f9b351.png)
2. 성공적으로 활성화되면 ‘외부 네트워크 IP’ 옆에 있는 외부 네트워크 주소와 포트 번호를 볼 수 있습니다. TDSQL for MySQL은 각 인스턴스에 고유한 공용 IP 및 포트 쌍을 할당합니다.


계정을 만들고 내부/외부 네트워크 주소를 얻은 후 타사 도구 및 프로그램 드라이버를 통해 TDSQL for MySQL에 연결할 수 있습니다.
- Windows에서는 명령 라인, 클라이언트, JDBC 드라이버의 연결 방법을 예로 들 수 있습니다.
- Linux에서는 명령 라인 연결 방법을 예로 들 수 있습니다.

## Windows 장치에서 연결
### Windows 명령 라인 연결
1. Windows 명령 라인 툴을 열고 MySQL의 올바른 경로 아래에 다음 명령을 입력합니다.
```
mysql -h 내부/외부 네트워크 주소 -P 포트 번호 -u 사용자 이름  -p
Enter password: **********(비밀번호 입력)
```
2. 다음과 같은 정보가 표시되면 데이터베이스가 성공적으로 연결된 것이며 작업을 진행할 수 있습니다.
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
```

### Windows 클라이언트 연결
1. MySQL Workbench, SQLyog와 같은 표준 SQL 클라이언트를 다운로드합니다. 여기에서는 SQLyog를 예로 들어보겠습니다.
2. SQLyog를 열고 [파일]>[신규 연결]을 선택하고 호스트 주소, 포트, 사용자 이름 및 암호를 입력하고 [연결]을 클릭합니다.
 - MySQL 호스트 주소: 이전에 얻은 인스턴스의 내부/외부 네트워크 IP를 입력합니다.
 - 사용자 이름: 이전에 생성한 계정 이름을 입력합니다.
 - 비밀번호: 계정의 비밀번호를 입력합니다. 암호를 잊어버린 경우 [콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에서 재설정하십시오.
 - 포트: 이전에 얻은 인스턴스의 포트 번호를 입력합니다.
3. 접속 성공 후의 인터페이스는 아래와 같습니다. 이 인터페이스에서 데이터베이스를 조작할 수 있습니다.

### Windows JDBC 드라이버 연결
TDSQL for MySQL은 프로그램 드라이버와의 연결을 지원합니다. 이 문서에서는 Java JDBC Driver for MySQL(Connector/J)을 예로 사용합니다.

1. [MySQL 공식 웹사이트](https://dev.mysql.com/downloads/connector/j/5.0.html)에서 JDBC jar 패키지를 다운로드하고 Java에서 참조하는 Library로 가져옵니다.
2. 다음 코드를 실행하여 JDBC를 호출합니다.
```
public static final String url = "내부/외부 네트워크 주소";
public static final String name = "com.mysql.jdbc.Driver"; //JDBC 드라이버 호출
public static final String user = "사용자 이름";
public static final String password = "비밀번호";
//JDBC
Class.forName("com.mysql.jdbc.Driver"); 
Connection conn=DriverManager.getConnection("url, user, password");
//
conn.close();
```
3. 연결에 성공하면 데이터베이스에서 다른 작업을 수행할 수 있습니다.
>?TDSQL for MySQL은 테이블을 분할하고 데이터를 삽입할 때 shardkey를 표시해야 하므로 이러한 작업은 JDBC로 호출할 수 없습니다.

## Linux 장치에서 연결
### Linux 명령 라인으로 연결
본문은 CVM 인스턴스의 CentOS 7.2 64비트를 예로 들어 설명합니다. CVM 인스턴스 구매에 대한 자세한 내용은 [구매 방식](https://intl.cloud.tencent.com/document/product/213/506)을 참고하십시오.
1. Linux CVM에 로그인한 후, `yum install mysql`을 입력하고 CentOS의 패키지 관리 소프트웨어 Yum을 사용하여 Tencent Cloud의 이미지 소스에서 MySQL 클라이언트를 다운로드하여 설치합니다.
![](https://main.qcloudimg.com/raw/fe1470a47fd3311460a7cfd24f70a88a.png)
2. 명령 라인에 complete가 표시되면 MySQL 클라이언트가 성공적으로 설치된 것입니다.
3. `mysql -h 내부/외부 네트워크 주소 -P 포트 -u 사용자 이름 -p`를 입력하여 TDSQL for MySQL에 연결합니다. 그런 다음 샤딩을 수행할 수 있습니다.
아래의 이미지는 'show databases;'를 예시로 합니다.
![](https://main.qcloudimg.com/raw/c094ba46f8a3d321ad4a199d88d9d3e6.png)

