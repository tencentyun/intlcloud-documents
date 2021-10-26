## 작업 시나리오
본문은 Windows Server 2012 R2 데이터센터 버전인 64비트 중국어 버전 운영 체제 Cloud Virtual Machine(CVM)을 예시로, MySQL 8.0.19를 구축하는 자세한 순서를 소개합니다.
일반적으로 Windows 시스템은 SQL Server 데이터베이스를 사용하지만 SQL Server는 유료 제품이므로 사용자가 직접 권한을 부여하거나 [TencentDB for SQL Server](https://intl.cloud.tencent.com/product/sqlserver)를 구매할 수 있습니다.

## 작업 순서

### MySQL 설치 패키지 다운로드
1. CVM에 로그인합니다.
2. CVM에서 브라우저를 열고 [MySQL 공식 홈페이지](https://www.mysql.com/)를 방문하여 MySQL 설치 패키지를 다운로드합니다.

### MySQL 기본 환경 설치

1. 더블 클릭하여 MySQL 설치 패키지를 열고 "Choosing a Setup Type" 설치 인터페이스에서 [Developer Default]을 선택하고 [Next]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/4077db7bfe9f7b97e1d7ddd649efa966.png)
2. "Check Requirements" 설치 인터페이스에서 [Execute]를 클릭하고 인터페이스 안내에 따라 MySQL 기본 환경을 설정합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/16a5f7190d7720562681528072cf8129.png)
3. [Next]를 클릭합니다.
4. "Installation" 설치 인터페이스에서 [Execute]을 클릭하여 MySQL에 필요한 설치 패키지를 설치합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/1b4a3e338bb816e7c47b4603a7a1dbb4.png)
5. MySQL에 필요한 설치 패키지가 설치된 후 [Next]을 클릭하여 "Product Configuration" 설정 인터페이스로 이동합니다.


###  MySQL 구성

#### MySQL 서비스 구성

1. "Product Configuration" 구성 인터페이스에서 [Next]를 클릭합니다.
2. “Hight Availability” 인터페이스에서 [Standalone MySQL Server / Classic MySQL Replication]을 선택하고, [Next]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/5355f286598388f9e9846bf8122e6d98.png)
3. "Type and Networking" 구성 인터페이스에서 기본 구성을 유지하고 [Next]를 클릭합니다. 아래 이미지를 참고하십시오.
>? 
> - TCP/IP 네트워크 기본 실행.
> - 3306 포트 기본 사용.
> 
![](https://main.qcloudimg.com/raw/fbece2fafb34beb5825ae294a8e214fd.png)
4. "Authentication Method" 구성 인터페이스에서 기본 구성을 유지하고 [Next]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/402624aaf02dce01ca2912d3548c03de.png)
5. root 비밀번호를 설정하고 [Next]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/a0472f0b93c590997e78c2f590a0f901.png)
6. "Windows Service" 구성 인터페이스에서 기본 구성을 유지하고 [Next]을 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/a85625c446218a275e743ff0ec599ece.png)
7. “Apply Configuration” 구성 인터페이스에서, [Execute]를 클릭합니다.
![](https://main.qcloudimg.com/raw/2ee6000630d88774951ddf8aaea16fbb.png)
8. [Finish]를 클릭하여 MySQL 서비스 구성을 완료합니다.

#### MySQL 라우터 구성

1. “Product Configuration” 구성 인터페이스에서 [Next]를 클릭합니다.
2. “MySQL Router Configuration” 인터페이스에서 기본 구성을 유지하고, [Finish]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/adece1334b6e1579eb2ace782cf47c59.png)

#### MySQL 구성 예시

1. “Product Configuration” 구성 인터페이스에서 [Next]를 클릭합니다.
2. “Connect To Server” 구성 인터페이스에서, root 비밀번호를 입력하고, [Check]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/ab8637391012a14ab2e5160c61675912.png)
3. root 비밀번호 인증 완료 후, [Next]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/bff0aece8da11d15a52f4db91b4d7e69.png)
4. “Apply Configuration” 구성 인터페이스에서, [Execute]를 클릭합니다.
![](https://main.qcloudimg.com/raw/8fe1f90eed50860e064044b314719cf6.png)
5. [Finish]를 클릭하여 MySQL 예시 구성을 완료합니다.
6. “Product Configuration” 구성 인터페이스에서 [Next]를 클릭합니다.
7. “Installation Complete” 인터페이스에서 실제 필요에 따라 실행할 MySQL 환경을 선택하고, [Finish]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/13f46296b85b00ce7e3bd08be13108c9.png)
 - 아래 이미지와 같이 MySQL 스테이징이 성공적으로 열리면 MySQL 설치가 완료된 것입니다.
![](https://main.qcloudimg.com/raw/288f4cfbf1a9671b73dff64a940e0dc1.png)
 - 아래 이미지와 같이 MySQL Shell이 성공적으로 열리면 MySQL 설치가 완료된 것입니다.
![](https://main.qcloudimg.com/raw/90b788ffe3a8f92e0e5e70f35fb94356.png)


### 보안 그룹 규칙 추가

구매한 CVM 인스턴스의 보안 그룹에 인바운드 규칙을 추가하고 3306포트를 릴리스합니다.
구체적인 작업은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.






