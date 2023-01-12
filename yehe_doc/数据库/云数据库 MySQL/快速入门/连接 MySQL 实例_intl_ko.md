본문은 사설망 또는 공중망을 통해 초기화된 TencentDB for MySQL 인스턴스에 연결하는 방법을 설명합니다.

## 준비 작업
- 초기화한 MySQL 인스턴스를 준비합니다. 자세한 내용은 [MySQL 인스턴스 초기화](https://intl.cloud.tencent.com/document/product/236/37785)를 참고하십시오.
- 데이터베이스 계정을 준비하고 MySQL 액세스를 허용할 IP에 권한을 부여합니다. 자세한 내용은 [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900), [액세스 권한을 부여할 호스트 주소 변경](https://intl.cloud.tencent.com/document/product/236/31903)을 참고하십시오. 직접 root 계정을 사용할 수도 있습니다.
- CVM과 MySQL의 보안 그룹의 인바운드/아웃바운드 규칙을 설정하여 MySQL 액세스를 허용하는 IP를 제한할 수 있습니다. 자세한 내용은 [CDB 보안 그룹 관리](https://intl.cloud.tencent.com/document/product/236/14470)를 참고하십시오.

## 연결 방식
>!TencentDB for MySQL 인스턴스에 연결하려면 사설망 또는 공중망에 관계없이 해당 포트를 열어야 합니다. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 목록에서 인스턴스 ID를 클릭하고 인스턴스 세부 정보 페이지에서 해당 포트 번호를 볼 수 있습니다.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/b2QI771_8.png)
>
>- TencentDB for MySQL는 기본적으로 사설망 포트 3306을 사용하며 포트 사용자 지정을 지원합니다. 기본 포트가 변경되면 보안 그룹에서 새 포트를 열어야 합니다.
>- TencentDB for MySQL 공용 포트는 시스템에서 자동으로 할당되며 사용자 정의할 수 없습니다. 공중망 액세스가 활성화되면 보안 그룹의 ACL에 의해 제어됩니다. 보안 정책을 구성할 때 사설 포트 3306을 열어야 합니다.
>- TencentDB for MySQL 콘솔의 보안 그룹 페이지에 표시되는 보안 그룹 규칙은 TencentDB for MySQL 인스턴스의 사설망 및 공중망(활성화된 경우) 주소에 적용됩니다.
>
>TencentDB for MySQL 연결 방법은 다음과 같습니다.
- **사설망 연결**: CVM 인스턴스를 사용하여 TencentDB 인스턴스의 사설망 주소에 연결할 수 있습니다. 이 방법은 Tencent Cloud의 고속 사설망을 활용하며 지연이 적습니다.
 - 두 인스턴스는 동일한 계정 및 동일한 리전의 동일한 [VPC](https://intl.cloud.tencent.com/document/product/215/535)에 있거나 클래식 네트워크에 있어야 합니다.
 - 사설망 주소는 기본적으로 TencentDB에서 제공하며 [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 목록 또는 인스턴스 세부 정보 페이지에서 볼 수 있습니다.
>?서로 다른 VPC(동일 계정/다른 계정, 동일 리전/다른 리전 포함)에 있는 CVM 및 TencentDB 인스턴스는 [CCN](https://www.tencentcloud.com/document/product/1003)을 참고하십시오.
>
- **공중망 연결**: 사설망에 액세스할 수 없는 경우 공중망 주소에서 TencentDB for MySQL 인스턴스에 연결할 수 있습니다. 공중망 주소는 [수동으로 활성화](#waiwang)해야 합니다. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 세부 정보 페이지에서 볼 수 있으며 더 이상 필요하지 않은 경우 비활성화할 수 있습니다. 공중망 액세스를 활성화하려면 [CDB 보안 그룹 관리](https://intl.cloud.tencent.com/document/product/236/14470)의 지침에 따라 보안 그룹도 적절하게 구성해야 합니다.
 - 공중망 주소는 광저우, 상하이, 베이징, 청두, 충칭, 난징, 중국홍콩, 싱가포르, 서울, 도쿄, 실리콘밸리 및 프랑크푸르트 리전의 소스 인스턴스에 대해 활성화할 수 있습니다. 읽기 전용 인스턴스에 대해 공중망 주소를 활성화할 수 있는 리전에 대한 최신 정보는 콘솔에서 찾을 수 있습니다.
 - 공중망 액세스를 활성화하면 데이터베이스 서비스가 공중망에 노출되어 데이터베이스 침입이나 공격이 발생할 수 있습니다. 사설망을 사용하여 데이터베이스에 연결하는 것이 좋습니다. 
 - TencentDB에 대한 공중망 연결은 데이터베이스의 개발 또는 보조 관리에 적합하지만, 잠재적으로 제어할 수 없는 요인으로 인해 DDOS 공격 및 대량의 버스트 트래픽 등 공중망 연결을 사용할 수 없게 될 수 있으므로 프로덕션 환경에서의 비즈니스 액세스에는 적합하지 않습니다.


다음은 사설망 및 공중망을 통해 Windows 및 Linux CVM 인스턴스에서 TencentDB for MySQL 인스턴스에 로그인하는 방법을 설명합니다.
## Windows CVM 인스턴스에서 연결
1. Windows CVM에 로그인합니다. 자세한 내용은 <a href="https://www.tencentcloud.com/document/product/213/10516" target="_blank">Windows CVM 커스텀 설정</a>을 참고하십시오.
2. 표준 SQL 클라이언트를 다운로드합니다.
>?MySQL Workbench 다운로드를 권장합니다. 시스템에 따라 적합한 버전의 설치 프로그램을 다운로드하며, 다운로드 주소는 https://dev.mysql.com/downloads/workbench/를 참고하십시오.
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. 인터페이스에 표시된 **Login**, **Sign Up** 및 **No, thanks, just start my download.** 중에서 **No thanks, just start my download.**를 선택한 다음 다운로드합니다.
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. CVM에 MySQL Workbench를 설치합니다.
>?
>- 컴퓨터에 Microsoft .NET Framework 4.5 및 Visual C++ Redistributable for Visual Studio 2015가 설치되어있어야 합니다.
>- MySQL Workbench 설치 마법사에서 **Download Prerequisites**를 클릭하면 상응하는 페이지로 리디렉션되며, 해당 페이지에서 두 종류의 소프트웨어를 다운로드 및 설치한 후에 MySQL Workbench를 설치합니다.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. MySQL Workbench를 연 다음, **Database** > **Connect to Database**를 선택하여, MySQL 데이터베이스 인스턴스의 사설망(혹은 공중망) 주소, 사용자 이름 및 비밀번호를 입력한 후 **OK**를 클릭해 로그인합니다.
 - Hostname: 사설망(혹은 공중망) 주소를 입력합니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 사설망/공중망의 주소 및 포트 번호를 확인할 수 있습니다. 공중망 주소라면 활성화 여부를 확인하시기 바라며, 자세한 내용은 [공중망 활성화](#waiwang)를 참고하십시오.
 - Port: 사설망(혹은 공중망)에 상응하는 포트입니다.
 - Username: root로 기본 설정되어 있으며, 공중망으로 연결한 경우 편리한 관리 및 제어를 위해 단독 [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 권장합니다.
 - Password: Username에 해당하는 비밀번호이며, 비밀번호를 잊어버린 경우 [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)을 통해 변경할 수 있습니다.
![](https://main.qcloudimg.com/raw/946b50fb05de11d7c68c2262ac4fe933.png)
6. 다음과 같이 로그인에 성공하면 나타나는 페이지에서 MySQL 데이터베이스의 각종 모드와 객체를 확인할 수 있으며, 테이블을 생성하거나 데이터 삽입 및 쿼리 등의 작업을 수행할 수 있습니다.
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## Linux CVM 인스턴스에서 연결
1. Linux CVM에 로그인 합니다. [Linux CVM 커스텀 설정](https://www.tencentcloud.com/document/product/213/10517)을 참고하십시오.
2. CentOS 7.2 64비트 시스템의 CVM을 예시로 하며, 다음의 명령어를 실행하여 MySQL 클라이언트를 설치합니다.
```
yum install mysql
```
MySQL 클라이언트 설치가 끝나면 'Complete!'라는 알림이 표시됩니다.
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)
3. 연결 방식이 서로 다르므로, 적합한 작업을 선택합니다.
 - **사설망 연결 시**
    1. 다음 명령어를 실행하여 MySQL 데이터베이스 인스턴스에 로그인합니다.
```
mysql -h hostname -u username -p
```
      - hostname: 대상 MySQL 데이터베이스 인스턴스의 사설망 주소로 변경합니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 조회할 수 있습니다.
>?
>- MySQL 기본 포트는 3306입니다.
>- 포트가 3306인 경우 hostname을 IP 주소로 바꾸면 됩니다. 예를 들어 사설망 주소가 10.16.0.11:3306인 경우 10.16.0.11만 입력하면 됩니다.
>- 포트가 수정되면 연결 명령은 포트 번호를 추가해야 합니다. 즉, `mysql -h hostname -P port -u username -p`, 예시 `mysql -h 10.16.0.11 -P 5308 -u username -p`
>
		- username: 기본 설정된 사용자 이름인 root로 변경합니다.
    2. `Enter password:` 메시지가 표시되면 TencentDB for MySQL 인스턴스의 root 계정에 해당하는 비밀번호를 입력합니다. 비밀번호를 잊은 경우 [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)의 안내에 따라 비밀번호를 재설정할 수 있습니다.
    본 예시에서 'MySQL [(none)]>' 표시는 MySQL에 로그인에 성공했음을 의미합니다.
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **공중망 연결 시:**
    1. 다음 명령어를 실행하여 MySQL 데이터베이스 인스턴스에 로그인합니다.
```
mysql -h hostname -P port -u username -p
```
      - hostname: 대상 MySQL 데이터베이스 인스턴스의 공중망 주소로 변경합니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 공중망의 주소 및 포트 번호를 확인할 수 있습니다. 공중망 주소가 비활성화 상태라면, [공중망 활성화](#waiwang)를 참고하여 활성화해 주시기 바랍니다.
      - port: 공중망의 포트 번호로 변경합니다.
      - username: 공중망 연결 사용자 이름으로 변경합니다. 공중망으로 연결할 경우 편리한 관리 및 제어를 위해 단독 [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 권장합니다.
    2. `Enter password:` 메시지가 표시되면 공중망으로 연결 사용자 이름에 해당하는 비밀번호를 입력합니다. 비밀번호를 잊은 경우 [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)의 안내에 따라 비밀번호를 재설정할 수 있습니다.
    본 예시의 hostname은 59281c4exxx.myqcloud.com이며, 공중망 포트 번호는 15311입니다.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. 'MySQL \[(none)]>' 프롬프트에서 실행할 MySQL 서버에 SQL 명령을 발송할 수 있습니다. 구체적인 명령 라인은 [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html)를 참고하십시오.
아래의 이미지에서는 'show databases;'를 예시로 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/faa7e8137e03b72f95d7a92faa971a42.png)

## 부록1: 인스턴스 연결 불가 관련 문제
인스턴스 연결 불가와 관련된 문제가 발생하면 [원클릭 연결 진단 툴](https://intl.cloud.tencent.com/document/product/236/31927)을 사용하여 문제를 진단하고, 결과 보고에 따라 [인스턴스 연결 불가](https://intl.cloud.tencent.com/document/product/236/40333)에서 적합한 솔루션을 찾아보시길 권장합니다.

## 부록2: 네트워크 연결성 인증 방법
telnet 명령을 사용하여 네트워크 연결 문제를 신속하게 해결하고 찾을 것을 권장합니다. 자세한 내용은 [telnet 명령](https://cloud.tencent.com/document/product/236/34375#.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88)를 참고하십시오.

telnet으로 CDB 네트워크 액세스가 정상임을 검증한 후에도 CVM에서 명령 라인을 통해 CDB에 로그인할 때 오류 메시지가 출력된다면 [인스턴스 연결 관련 문제](https://intl.cloud.tencent.com/document/product/236/37783)를 참고하십시오.

## [부록3: 공중망 연결 주소 활성화](id:waiwang)
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb/ ) 로그인 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 인스턴스 상세 페이지의 **공중망 주소**에서 **활성화**를 클릭합니다.
>?공중망 주소와 공중망 포트 정보가 있으면 공중망 주소가 활성화된 것입니다.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7F5X882_18.png)
3. 팝업 창에서 **확인**을 클릭합니다.
>?
>- 활성화가 완료되면 기본 정보에서 공중망 주소를 조회할 수 있습니다.
>- 스위치 버튼으로 공중망 연결 권한을 비활성화할 수 있으며, 공중망을 다시 활성화해도 도메인에 해당하는 공중망 주소는 변경되지 않습니다.
