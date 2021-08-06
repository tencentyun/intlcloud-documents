본 문서는 초기화 인스턴스 생성 후 내부 네트워크 또는 외부 네트워크 주소를 통해 MySQL 인스턴스에 연결하는 방법을 소개합니다.

## 준비 과정
- 초기화한 MySQL 인스턴스를 준비합니다. 자세한 내용은 [MySQL 인스턴스 초기화](https://intl.cloud.tencent.com/document/product/236/3128)를 참고하십시오.
- 데이터베이스 계정을 준비하고 MySQL 액세스를 허용할 IP에 권한을 부여합니다. 자세한 내용은 [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900), [액세스 권한을 부여할 호스트 주소 변경](https://intl.cloud.tencent.com/document/product/236/31903)을 참고하십시오. 직접 root 계정을 사용할 수도 있습니다.
- CVM과 MySQL의 보안 그룹의 인바운드/아웃바운드 규칙을 설정하여 MySQL 액세스를 허용하는 IP를 제한할 수 있습니다. 자세한 내용은 [CDB 보안 그룹 관리](https://intl.cloud.tencent.com/document/product/236/14470)를 참고하십시오.

## 연결 방식
TencentDB for MySQL 연결 방법은 다음과 같습니다.
- **내부 네트워크 주소 연결**: 내부 네트워크 주소를 통해 TencentDB for MySQL을 연결하고 CVM을 사용해 CDB의 내부 네트워크 주소에 직접 연결합니다. 이 방식은 내부 고속 네트워크를 사용하므로 딜레이가 낮습니다.
 - CVM과 데이터베이스의 계정이 동일해야 하며, 동일한 [VPC](https://intl.cloud.tencent.com/document/product/215/535) 내(동일한 리전)에 있거나 기본 네트워크가 동일해야 합니다.
 - 내부 네트워크 주소 시스템을 기본으로 제공하며, [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 리스트 혹은 인스턴스 상세 페이지에서 조회할 수 있습니다.
>?서로 다른 VPC(동일 계정/다른 계정, 동일 리전/다른 리전 포함)의 CVM과 데이터베이스에 대한 내부 네트워크 연결 방식은 [CCN](https://intl.cloud.tencent.com/zh/document/product/1003)을 참고하십시오.
>
- **외부 네트워크 연결**:내부 네트워크를 통해 연결할 수 없을 때는 외부 네트워크 주소로 TencentDB for MySQL에 연결할 수 있습니다.외부 네트워크 주소를 [수동 활성화](#waiwang)해야 하며, [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 조회할 수 있습니다. 불필요한 경우 비활성화할 수 있습니다.
 - 광저우, 상하이, 베이징, 청두, 충칭, 난징, 중국홍콩, 싱가포르, 서울, 도쿄, 실리콘밸리, 프랑크푸르트 리전의 마스터 인스턴스는 외부 네트워크 연결 주소 활성화를 지원합니다.읽기 전용 인스턴스는 외부 네트워크 리전 활성화를 지원합니다. 콘솔을 기준으로 참고하시기 바랍니다.
 - 외부 네트워크 주소를 활성화하면, 데이터베이스 서비스가 공용 네트워크에 노출되어 데이터베이스가 침입 혹은 공격을 받을 수 있습니다.내부 네트워크를 사용해 데이터베이스에 연결하는 것을 권장합니다. 
 - CDB의 외부 네트워크 연결은 데이터베이스의 개발 혹은 관리 보조 시에 적합합니다. DDOS 공격, 돌발적인 대용량 트래픽 액세스 등과 같은 통제 불가능한 요소로 인해 외부 네트워크 연결을 사용할 수 없게 될 수 있으므로, 정식 비즈니스 연결에는 사용하지 않을 것을 권장합니다.


아래의 예시는 각각 Windows CVM 또는 Linux CVM에서 로그인한 후 내부/외부 네트워크 등 두 가지 방식으로 TencentDB for MySQL에 연결하는 방법을 소개합니다.
## Windows CVM에서 연결
1. Windows CVM에 로그인하여, <a href="https://intl.cloud.tencent.com/zh/document/product/213/10516" target="_blank">Windows CVM 빠른 구성</a>을 참고 바랍니다.
2. 표준 SQL 클라이언트를 다운로드합니다.
>?MySQL Workbench 다운로드를 권장합니다. 시스템에 따라 적합한 버전의 설치 프로그램을 다운로드하며, 다운로드 주소는 https://dev.mysql.com/downloads/workbench/를 참고 바랍니다.
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. 인터페이스에 표시된 [Login], [Sign Up] 및 [No, thanks, just start my download.] 중에서 [No, thanks, just start my download.]를 선택하여빠르게 다운로드합니다.
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. CVM에 MySQL Workbench를 설치합니다.
>?
>- 컴퓨터에 Microsoft .NET Framework 4.5 및 Visual C++ Redistributable for Visual Studio 2015가 설치되어있어야 합니다.
>- MySQL Workbench 설치 마법사에서 [Download Prerequisites]를 클릭하면 상응하는 페이지로 리디렉션되며, 해당 페이지에서 두 종류의 소프트웨어를 다운로드 및 설치한 후에 MySQL Workbench를 설치합니다.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. MySQL Workbench를 연 다음, [Database]>[Connect to Database]를 선택하여, MySQL 데이터베이스 인스턴스의 내부 네트워크(혹은 외부 네트워크) 주소, 사용자 이름 및 비밀번호를 입력한 후 [OK]을 클릭해 로그인합니다.
 - Hostname:내부 네트워크(혹은 외부 네트워크) 주소를 입력합니다.[MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 내부(또는 외부) 네트워크 주소 및 포트 번호를 확인할 수 있습니다. 외부 네트워크 주소의 경우 활성화 여부를 확인하고, 자세한 내용은 [외부 네트워크 활성화](#waiwang)를 참고하십시오.
 - Port:내부 네트워크(혹은 외부 네트워크)에 해당하는 포트입니다.
 - Username:root로 기본 설정되어 있으며, 외부 네트워크로 연결한 경우 편리한 관리 및 제어를 위해 단독 [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 권장합니다.
 - Password:Username에 해당하는 비밀번호이며, 비밀번호를 잊어버린 경우 [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)을 통해 변경할 수 있습니다.
![](https://main.qcloudimg.com/raw/946b50fb05de11d7c68c2262ac4fe933.png)
6. 다음과 같이 로그인에 성공하면 나타나는 페이지에서 MySQL 데이터베이스의 각종 모드와 객체를 확인할 수 있으며, 표를 생성하거나 데이터 삽입 및 조회 등의 작업을 수행할 수 있습니다.
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## Linux CVM에서 연결
1. Linux CVM에 로그인한 뒤, <a href="https://intl.cloud.tencent.com/zh/document/product/236/31901" target="_blank">Linux CVM 빠른 구성</a>을 참고 바랍니다.
2. CentOS 7.2 64비트 시스템의 CVM을 예시로 하며, 다음의 명령어를 실행하여 MySQL 클라이언트를 설치합니다.
```
yum install mysql
```
MySQL 클라이언트 설치가 끝나면 'Complete!'라는 알림이 표시됩니다.
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)
3. 연결 방식이 서로 다르므로, 적합한 작업을 선택합니다.
 - **내부 네트워크 연결 시**
    1. 다음 명령어를 실행하여 MySQL 데이터베이스 인스턴스에 로그인합니다.
```
mysql -h hostname -u username -p
```
      - hostname:타깃 MySQL 데이터베이스 인스턴스의 내부 네트워크 주소로 변경합니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 조회할 수 있습니다.
    	- username:기본 설정 사용자 이름인 root로 변경합니다.
    2. `Enter password:`가 표시되면 MySQL 인스턴스 root 계정에 해당하는 비밀번호를 입력합니다. 비밀번호를 잊어버린 경우 [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)을 통해 변경할 수 있습니다.
    본 예시에서 'MySQL [(none)]>' 표시는 MySQL에 로그인에 성공했음을 의미합니다.
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **외부 네트워크 연결 시**

    1. 다음 명령어를 실행하여 MySQL 데이터베이스 인스턴스에 로그인합니다.
```
mysql -h hostname -P port -u username -p
```
      - hostname：타깃 MySQL 데이터베이스 인스턴스의 내부 네트워크 주소로 변경합니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 외부 네트워크의 주소 및 포트 번호를 확인할 수 있습니다.외부 네트워크 주소가 비활성화 상태이면 [외부 네트워크 주소 활성화](#waiwang)를 참고하여 활성화하시기 바랍니다.
      - port:외부 네트워크의 포트 번호로 변경합니다.
      - username:외부 네트워크 연결 사용자 이름으로 변경합니다. 외부 네트워크로 연결할 경우, 편리한 관리 및 제어를 위해 단독 [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 권장합니다.
    2. ‘Enter password:'가 표시되면,외부 네트워크로 연결한 사용자 이름과 상응하는 비밀번호를 입력합니다. 비밀번호를 잊어버렸을 경우 [비밀번호 재설정](https://intl.cloud.tencent.com/zh/document/product/236/31901)을 통해 변경할 수 있습니다.
    본 예시의 hostname은 59281c4exxx.myqcloud.com이며, 외부 네트워크 포트 번호는 15311입니다.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. 'MySQL \[(none)]>' 프롬프트에서 실행할 MySQL 서버에 SQL 명령을 발송할 수 있습니다. 구체적인 명령 라인은 [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html)를 참고 바랍니다.
아래의 이미지에서는 'show databases;'를 예시로 합니다.
![](https://main.qcloudimg.com/raw/2873c8675d0ce123771a63dbf05df8b9.png)

## 부록1:인스턴스 연결 불가 관련 문제
인스턴스 연결 불가와 관련된 문제가 발생하면 [원클릭 연결 진단 툴](https://intl.cloud.tencent.com/document/product/236/31927)을 사용하여 문제를 진단하고, 결과 보고에 따라 [인스턴스 연결 불가](https://intl.cloud.tencent.com/document/product/236/40333)에서 적합한 솔루션을 찾아보시길 권장합니다.

## 부록2:네트워크 연결성 인증 방법
telnet 명령어를 사용하여 네트워크 연결성 문제를 빠르게 파악하고 진단하시기 바랍니다. 자세한 내용은 [telnet 명령어](https://intl.cloud.tencent.com/document/product/236/31929)를 참고하십시오.

telnet으로 CDB 네트워크 액세스가 정상임을 검증한 후에도 CVM에서 명령 라인을 통해 CDB에 로그인할 때 오류 메시지가 출력된다면 [인스턴스 연결 관련 문제(https://intl.cloud.tencent.com/document/product/236/37783)를 참고하십시오.

## [부록3:외부 네트워크 연결 주소 활성화](id:waiwang)
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 리스트에서 인스턴스 이름 혹은 '작업' 열의 [관리]를 클릭하여 인스턴스 상세 페이지를 엽니다.
2. 인스턴스 상세 페이지의 '외부 네트워크 주소' 부분에서 [활성화]를 클릭합니다.
>?외부 네트워크 주소와 외부 네트워크 포트 정보가 있으면 외부 네트워크 주소가 활성화된 것입니다.
>
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
3. 팝업창에서 [확인]을 클릭합니다.
>?
>- 활성화가 완료되면 기본 정보에서 외부 네트워크 주소를 조회할 수 있습니다.
>- 스위치 버튼으로 외부 네트워크 연결 권한을 비활성화할 수 있으며, 외부 네트워크를 다시 활성화해도 도메인에 해당하는 외부 네트워크 주소는 변경되지 않습니다.
