
## 연결 방식
다음과 같은 방법으로 TDSQL for MySQL 인스턴스에 연결할 수 있습니다.
- **사설망 연결**: CVM 인스턴스를 사용하여 TDSQL for MySQL 인스턴스의 사설망 주소에 연결할 수 있습니다. 이 방식은 Tencent Cloud의 고속 사설망을 활용하며 지연 시간이 짧은 것이 특징입니다.
 - 두 인스턴스는 동일한 계정 및 동일한 리전의 동일한 [VPC](https://intl.cloud.tencent.com/document/product/215/535)에 있거나 클래식 네트워크에 있어야 합니다.
 - 사설망 주소는 기본적으로 TencentDB에서 제공하며 [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)의 인스턴스 리스트 또는 인스턴스 세부 정보 페이지에서 볼 수 있습니다.
>?다른 VPC(동일하거나 다른 리전의 동일하거나 다른 계정)에 있는 CVM 및 TencentDB 인스턴스는 [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003)를 통해 사설망으로 상호 연결할 수 있습니다.
>
- **공중망 주소 연결**: 사설망을 통해 액세스할 수 없는 경우 공중망 주소에서 TDSQL for MySQL 인스턴스에 연결할 수 있습니다. 공중망 주소는 [수동으로 활성화](#waiwang)해야 합니다. [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)의 인스턴스 세부 정보 페이지에서 볼 수 있으며 더 이상 필요하지 않은 경우 비활성화할 수 있습니다.
 - 공중망 주소를 활성화하면 데이터베이스 서비스가 공중망에 노출되어 데이터베이스 침입이나 공격이 발생할 수 있습니다. 사설망을 사용하여 데이터베이스에 연결하는 것이 좋습니다.
 - TencentDB에 대한 공중망 연결은 데이터베이스의 개발 또는 보조 관리에 적합하지만, 잠재적으로 제어할 수 없는 요인으로 인해 DDOS 공격 및 대량의 버스트 트래픽 등 공중망 연결을 사용할 수 없게 될 수 있으므로 프로덕션 환경에서의 비즈니스 액세스에는 적합하지 않습니다.
 - 현재 공중망 액세스를 지원하는 리전은 광저우, 상하이, 베이징, 청두, 난징입니다.
 - 공중망 액세스 활성화를 위해서는 보안 그룹을 바인딩해야 하며, 자세한 내용은 [보안 그룹 설정](https://intl.cloud.tencent.com/document/product/1042/33348)을 참고하십시오.

## 준비 작업
### 계정 생성
1. [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인합니다. 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 들어갑니다.
2. 인스턴스 관리 페이지에서 **계정 관리** 탭을 선택하고 **계정 생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/148943eb024c9d3871b3c5d509de2e20.png)
3. 팝업 창에서 계정 이름, 호스트, 비밀번호 등을 입력합니다. 모든 항목이 올바른지 확인한 후 **확인, 다음 단계**를 클릭합니다.
호스트 이름은 실제 네트워크 송신 주소입니다. 필요한 경우 %를 입력하여 이 인스턴스가 모든 IP에 액세스할 수 있음을 나타낼 수 있습니다.
4. 권한 수정 팝업 창에서 필요에 따라 권한을 부여하고 **수정**을 클릭합니다. 변경 사항을 취소하려면 **수정 취소**를 클릭합니다.
왼쪽의 사이드바는 MySQL 관리와 완전히 호환되는 그래픽 인터페이스를 제공합니다. 권한은 열 수준에서 관리할 수 있습니다.
![](https://main.qcloudimg.com/raw/4a6bdfb7e48222945440db418e7f6de1.png)
5. 계정 리스트로 돌아가서 **권한 수정**을 클릭하여 사용자 권한을 수정하거나 **계정 복제**를 클릭하여 현재 계정 권한을 완전히 복사하여 새 계정을 생성할 수 있으며, **더 보기**를 클릭하여 비밀번호를 재설정 또는 계정을 삭제할 수 있습니다.
![](https://main.qcloudimg.com/raw/fe697afd0c76d921ce7961f4c57a9017.png)

### [(선택 사항)공중망 주소 활성화](id:waiwang)
1. [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인하고 인스턴스 리스트에서 인스턴스 ID를 클릭하여 인스턴스 세부 정보 페이지로 들어간 다음 기본 정보 섹션의 **공중망 주소** 옆에 있는 **활성화**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/16d255372b034ccf1525b21978c28d4d.png)
2. 성공적으로 활성화하면 **공중망 주소** 옆에 있는 공중망 주소와 포트 번호를 볼 수 있습니다. TDSQL for MySQL은 각 인스턴스에 고유한 공용 IP 및 포트 쌍을 할당합니다.


계정을 만들고 사설/공중망 주소를 얻은 후 3rd party 도구 및 프로그램 드라이버를 통해 TDSQL for MySQL에 연결할 수 있습니다.
- Windows에서는 명령 라인, 클라이언트, JDBC 드라이버의 연결 방법을 예로 들 수 있습니다.
- Linux에서는 명령 라인 연결 방법을 예로 들 수 있습니다.

## Windows 장치에서 연결
### Windows 명령 라인으로 연결
1. Windows 명령 라인 툴을 열고 MySQL의 올바른 경로 아래에 다음 명령을 입력합니다.
```
mysql -h 사설/공중망 주소 -P 포트 번호 -u 사용자 이름  -p
Enter password: **********(비밀번호 입력)
```
2. 다음과 같은 정보가 표시되면 데이터베이스가 성공적으로 연결된 것이며 작업을 진행할 수 있습니다.
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
```

### Windows 클라이언트 연결
1. MySQL Workbench 및 SQLyog와 같은 표준 SQL 클라이언트를 다운로드합니다. 여기에서는 SQLyog를 예로 듭니다.
2. SQLyog를 열고 **파일** > **새 연결**을 선택하고 호스트 주소, 포트, 사용자 이름 및 암호를 입력한 후 **연결**을 클릭합니다.
 - MySQL 호스트 주소: 이전에 얻은 인스턴스의 사설/공중망 주소를 입력합니다.
 - 사용자 이름: 이전에 생성한 계정 이름을 입력합니다.
 - 비밀번호: 계정의 비밀번호를 입력합니다. 암호를 잊어버린 경우 [콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에서 재설정하십시오.
 - 포트: 이전에 얻은 인스턴스의 포트 번호를 입력합니다.
3. 접속 성공 후의 인터페이스는 아래와 같습니다. 이 인터페이스에서 데이터베이스를 조작할 수 있습니다.

### Windows JDBC 드라이버 연결
TDSQL for MySQL은 프로그램 드라이버와의 연결을 지원합니다. 이 문서에서는 Java JDBC Driver for MySQL(Connector/J)을 예로 사용합니다.

1. [MySQL 공식 웹사이트](https://dev.mysql.com/downloads/connector/j/5.0.html)에서 JDBC jar 패키지를 다운로드하고 Java에서 참고하는 Library로 가져옵니다.
2. 다음 코드를 실행하여 JDBC를 호출합니다.
```
public static final String url = "사설/공중망 주소";
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

## Linux 장치에서 연결
### Linux 명령 라인으로 연결
본 문서에서는 CentOS 7.2 64비트의 CVM 인스턴스를 예로 들어 설명합니다. CVM 인스턴스 구매에 대한 자세한 내용은 [구매 방식](https://intl.cloud.tencent.com/document/product/213/506)을 참고하십시오.
1. Linux CVM에 로그인한 후, `yum install mysql`을 입력하고 CentOS의 패키지 관리 소프트웨어 Yum을 사용하여 Tencent Cloud의 이미지 소스에서 MySQL 클라이언트를 다운로드하여 설치합니다.
![](https://main.qcloudimg.com/raw/fe1470a47fd3311460a7cfd24f70a88a.png)
2. 명령 라인에 complete가 표시되면 MySQL 클라이언트가 성공적으로 설치된 것입니다.
3. `mysql -h 사설/공중망 주소 -P 포트 -u 사용자 이름 -p`를 입력하여 TDSQL for MySQL에 연결합니다. 그런 다음 샤딩을 수행할 수 있습니다.
아래의 이미지는 'show databases;'를 예시로 합니다.
![](https://main.qcloudimg.com/raw/c094ba46f8a3d321ad4a199d88d9d3e6.png)

