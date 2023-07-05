## 작업 시나리오
본문은 Windows Server 2012 R2 데이터센터 버전인 64비트 영어 버전 운영 체제 Cloud Virtual Machine(CVM)을 예시로, MySQL 8.0.19를 구축하는 자세한 순서를 소개합니다.
일반적으로 Windows 시스템은 SQL Server 데이터베이스를 사용하지만 SQL Server는 유료 제품이므로 사용자가 직접 권한을 부여하거나 [TencentDB for SQL Server](https://intl.cloud.tencent.com/zh/products/sqlserver)를 구매할 수 있습니다.

## 작업 단계

### MySQL 설치 패키지 다운로드
1. CVM에 로그인합니다.
2. CVM에서 브라우저를 열고 [MySQL 공식 홈페이지](https://www.mysql.com/)를 방문하여 MySQL 설치 패키지를 다운로드합니다.

### MySQL 기본 환경 설치

1. 더블 클릭하여 MySQL 설치 패키지를 열고 “Choosing a Setup Type” 설치 인터페이스에서 **Developer Default**를 선택하고 **Next**를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/46578b0e47c0a8283c72680070578916.png)
2. “Check Requirements” 설치 인터페이스에서 **Execute**를 클릭하고 인터페이스 안내에 따라 MySQL 기본 환경을 설정합니다.
3. **Next**를 클릭합니다.
4. “Installation” 설치 인터페이스에서 **Execute**를 클릭하여 MySQL에 필요한 설치 패키지를 설치합니다.
5. MySQL에 필요한 설치 패키지가 설치된 후 **Next**를 클릭하여 “Product Configuration” 설정 인터페이스로 이동합니다.


###  MySQL 구성

#### MySQL 서비스 구성

1. “Product Configuration” 구성 인터페이스에서 **Next**를 클릭합니다.
2. “Hight Availability” 인터페이스에서 **Standalone MySQL Server / Classic MySQL Replication**을 선택하고, **Next**를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/821c0ab18a477ffdf3458889ff698b08.png)
3. “Type and Networking” 구성 인터페이스에서 기본 구성을 유지하고 **Next**를 클릭합니다.
<dx-alert infotype="explain" title="">
- TCP/IP 네트워크 기본 실행.
- 3306 포트 기본 사용.
</dx-alert>
4. “Authentication Method” 설정 인터페이스에서 <b>Use Legacy Authentication Method(Retain MySQL 5.x Compatibility)</b>를 선택하고 **Next**를 클릭합니다. 아래 이미지를 참고하십시오.
본 문서는 WordPress 웹 사이트 구축을 위해 이 옵션을 설정하며 필요에 따라 선택할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/599dff879af20e25ce1d8e7fb5b1a33f.png)
5. root 비밀번호를 설정하고 **Next**를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/a85f3a6affb6d71dda27a7a1fe5a5870.png)
6. “Windows Service” 구성 인터페이스에서 기본 구성을 유지하고 **Next**를 클릭합니다. 아래 이미지를 참고하십시오.
7. “Apply Configuration” 구성 인터페이스에서, **Execute**를 클릭합니다.
8. **Finish**를 클릭하여 MySQL 서비스 구성을 완료합니다.

#### MySQL 라우터 구성

1. “Product Configuration” 구성 인터페이스에서 **Next**를 클릭합니다.
2. “MySQL Router Configuration” 인터페이스에서 기본 구성을 유지하고, **Finish**를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/f13a5db6d40390a3b5c650e00720d587.png)

#### MySQL 구성 예시

1. “Product Configuration” 구성 인터페이스에서 **Next**를 클릭합니다.
2. “Connect To Server” 구성 인터페이스에서, root 비밀번호를 입력하고, **Check**를 클릭합니다.
3. root 비밀번호 인증 완료 후, **Next**를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/5e4157ae76b5ae7aa4f7e9d99f40bfe8.png)
4. “Apply Configuration” 구성 인터페이스에서, **Execute**를 클릭합니다.
5. **Finish**를 클릭하여 MySQL 예시 구성을 완료합니다.
6. “Product Configuration” 구성 인터페이스에서 **Next**를 클릭합니다.
7. “Installation Complete” 인터페이스에서 실제 필요에 따라 실행할 MySQL 환경을 선택하고, **Finish**를 클릭합니다.
   - 아래 이미지와 같이 MySQL 스테이징이 성공적으로 열리면 MySQL 설치가 완료된 것입니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7f960c3d6e8c26f9fb68ee9de5d5b96b.png)
   - 아래 이미지와 같이 MySQL Shell이 성공적으로 열리면 MySQL 설치가 완료된 것입니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/985d2e239aae0bcc1d84f51e3eecd296.png)


### 보안 그룹 규칙 추가

구매한 CVM 인스턴스의 보안 그룹에 인바운드 규칙을 추가하고 3306포트를 릴리스합니다.
구체적인 작업은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.





