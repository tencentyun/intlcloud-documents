## 작업 시나리오
본 문서에서는 CVM 인스턴스에서 Microsoft SharePoint 2016을 구축하는 방법을 소개합니다.

## 소프트웨어
본 문서에서는 다음 하드웨어 사양의 CVM 인스턴스를 예시로 사용합니다.
- vCPU: 4코어
- 메모리: 8GB

본 문서에서는 다음 소프트웨어 버전을 예시로 사용합니다.
- 운영 체제: Windows Server 2012 R2 데이터센터 64비트(영어)
- 데이터베이스: SQL Server 2014

## 전제 조건
Windows CVM을 구입했습니다. 아직 설정하지 않은 경우 [Windows CVM 커스텀 설정](https://intl.cloud.tencent.com/document/product/213/10516)을 참고하십시오.

## 작업 단계

### 1단계: Windows 인스턴스에 로그인
[RDP 파일을 통한 Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435)하거나 [원격 데스크탑을 사용하여 Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32498)할 수 있습니다.


### 2단계: AD, DHCP, DNS 및 IIS 서비스 추가[](id:AddAD_DHCP_DNS_IIS)
1. 바탕 화면에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>을(를) 클릭하여 서버 관리자를 엽니다.
2. 왼쪽 사이드바에서 **로컬 서버**를 선택하고 아래와 같이 **IE 보안 강화 구성**을 찾습니다.
![](https://main.qcloudimg.com/raw/c2b0791555bbc910cea70732c75daa0f.png)
3. 아래와 같이 **IE 보안 강화 구성**을 비활성화합니다.
![](https://main.qcloudimg.com/raw/6acbf171bc703100401e48e362539b21.png)
4. 왼쪽 사이드바에서 **대시보드**를 선택하고 **역할 및 기능 추가**를 클릭합니다.
5. ‘역할 및 기능 추가 마법사’ 창에서 기본 구성을 유지하고 **다음**을 3번 클릭합니다.
6. ‘서버 역할’ 페이지에서 **Active Directory 도메인 서비스**, **DHCP 서버**, **DNS 서버**, **Web 서버(IIS)**를 선택하고 아래와 같이 팝업 창에서 **기능 추가**를 클릭합니다.
![](https://main.qcloudimg.com/raw/a2bb1c86c9277ca870c629ecf5b0d3f5.png)
7. **다음**을 클릭합니다.
8. ‘기능’ 페이지에서 ‘.NET Framework 3.5 기능’을 선택하여 아래와 같이 **기능 추가**를 클릭합니다.
![](https://main.qcloudimg.com/raw/bf47abbb95ad42b9d6c720c3bb2c846b.png)
9. 기본 구성을 유지하고 확인 페이지가 나타날 때까지 **다음**을 클릭합니다.
10. 설치를 확인하고 **설치**를 클릭합니다.
11. 설치가 완료되면 CVM을 다시 시작합니다.


### 3단계: AD 서비스 구성
1. 바탕 화면에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>을(를) 클릭하여 서버 관리자를 엽니다.
2. <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin:-3px 0px">을(를) 클릭하여 아래와 같이 **이 서버를 도메인 컨트롤러로 승격**을 선택합니다.
![](https://main.qcloudimg.com/raw/1e6aa1d75044898357709909bb969c6f.png)
3. [](id:step14) 열린 ‘Active Directory 도메인 서비스 설정 마법사’ 창에서 **새 포리스트 추가**를 선택하고 루트 도메인 이름 필드에 도메인 이름을 입력한 후 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/017acc0e5939632f3808698f36320fd2.png)
4. [](id:step15) DSRM(디렉터리 서비스 복원 모드) 암호를 설정하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/078672b95294790e4985108bd58d8504.png)
5. 기본 구성을 유지하고 구성이 완료될 때까지 **다음**을 클릭합니다.
6. **설치**를 클릭합니다.

### 4단계: DHCP 서비스 구성
1. 바탕 화면에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>을(를) 클릭하여 서버 관리자를 엽니다.
2. <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin:-3px 0px">을(를) 클릭하여 아래와 같이 **DHCP 구성 완료**를 선택합니다.
![](https://main.qcloudimg.com/raw/4c65a7990acc647866d73c1b5ba20a6c.png)
3. ‘DHCP 설치 후 설정 마법사’ 창에서 **다음**을 클릭합니다.
4. 기본 구성을 유지하고 **커밋**을 클릭하여 설치를 완료합니다.
![](https://main.qcloudimg.com/raw/4162a8fbde1b7af1d8fadacaa61965cf.png)
5. **닫기**를 클릭합니다.

### 5단계: SQL Server 2014 데이터베이스 설치

1. CVM에서 브라우저를 열고 SQL Server 2014 공식 사이트에서 SQL Server 2014 설치 패키지를 다운로드합니다.
<dx-alert infotype="explain" title="">
3rd party 웹 사이트 또는 기타 유효한 채널에서 SQL Server 2014 설치 패키지를 얻을 수도 있습니다.
</dx-alert>
2. 아래와 같이 ‘Setup.exe’ 파일을 더블클릭하여 설치 마법사를 시작하여 **새 SQL Server 독립 실행형 설치 또는 기능 추가**를 클릭합니다.
![](https://main.qcloudimg.com/raw/f2cc33aef5ec2662238ffeca56d08a7d.png)
3. 제품 키 페이지에서 제품 키를 입력하고 **다음**을 클릭합니다.
4. ‘사용 조건에 동의합니다’를 선택하고 **다음**을 클릭합니다.
5. 기본 구성을 유지하고 **다음**을 클릭합니다.
6. 설치 확인이 완료되면 **다음**을 클릭합니다.
7. 기본 구성을 유지하고 **다음**을 클릭합니다.
8. ‘기능 선택’ 페이지에서 **모두 선택**을 클릭하여 모든 기능을 선택하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/92eac7b681dae5937bafa484874ae122.png)
9. ‘인스턴스 구성’ 페이지에서 **기본 인스턴스**를 선택하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/2bf1682b927b66224c574435ee35e7af.png)
10. ‘서버 구성’ -> 서비스 계정 페이지에서 SQL Server 데이터베이스 엔진 및 SQL Server Analysis Services에 대한 계정과 암호를 구성하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/1310d9db077772be6dad6f58a698273e.png)
 - ‘SQL Server 데이터베이스 엔진’의 계정 이름을 ‘NT AUTHORITY\NETWORK SERVICE’로 설정합니다.
 - ‘SQL Server Analysis Services’의 계정 이름과 암호를 [2단계: AD, DHCP, DNS 및 IIS 서비스 추가](#AddAD_DHCP_DNS_IIS)에서 [14](#step14) - [15](#step15)에서 구성한 도메인 이름과 암호로 설정합니다.
11. ‘데이터베이스 엔진 구성’ -> 서버 구성 페이지에서 **현재 사용자 추가**를 선택하여 현재 계정을 SQL Server의 관리자 계정으로 사용하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/90ac80988b45a6b08650d97fd0d08c09.png)
12. ‘Analysis Services 구성’ -> 계정 프로비저닝 페이지에서 **현재 사용자 추가**를 선택하여 현재 계정에 Analysis Services에 대한 관리자 권한을 부여하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/5fda4e9b2ac31d8394ab0dfa14847d73.png)
13. 기본 구성을 유지하고 **다음**을 클릭합니다.
14. 아래와 같이 ‘Distributed Replay Controller’ 페이지에서 **현재 사용자 추가**를 클릭하여 현재 계정에 Distributed Replay 컨트롤러 서비스에 대한 액세스 권한을 부여합니다. **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/2b67cc38051c51cb88ba7bbb740027b3.png)
15. 기본 구성을 유지하고 설치가 완료될 때까지 **다음**을 클릭합니다.


### 4단계: SharePoint 2016 설치

1. CVM에서 브라우저를 열고 Microsoft SharePoint 2016 공식 사이트에서 Microsoft SharePoint 2016 설치 패키지를 다운로드합니다.
2. Microsoft SharePoint 2016 이미지 파일을 열고 아래와 같이 준비 도구의 실행 파일 `prerequisiteinstaller.exe`를 더블클릭하여 Microsoft SharePoint 2016 준비 도구를 설치합니다.
![](https://main.qcloudimg.com/raw/1c6c2e0970ea456bbabd4a77ef454a5e.png)
3. Microsoft SharePoint 2016 준비 도구의 설치 마법사를 열고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/4b42cde60ca558a7c905c6f8031e3a50.png)
4. ‘사용권 계약 조건에 동의합니다’를 선택하고 **다음**을 클릭합니다.
5. 준비 도구가 설치된 후 **완료**를 클릭하여 CVM을 다시 시작합니다.
![](https://main.qcloudimg.com/raw/a8c14625c359decb9941511e267ea2a6.png)
6. Microsoft SharePoint 2016 이미지 파일을 열고 설치 파일 `setup.exe`를 더블클릭하여 Microsoft SharePoint 2016을 설치합니다.
![](https://main.qcloudimg.com/raw/2614739955551657148d9c3a72e566df.png)
7. 제품 키를 입력하고 **계속**을 클릭합니다.
8. ‘이 계약 조건에 동의합니다’를 선택하고 **계속**을 클릭합니다.
9. 설치 디렉터리를 선택하고(이 예시에서는 기본 구성을 유지하지만 필요에 따라 디렉터리를 지정할 수 있음) **지금 설치**를 클릭합니다.
![](https://main.qcloudimg.com/raw/3ea703e1632ec78b3f8f4b961c189208.png)
10. 설치가 완료되면 ‘지금 SharePoint 제품 구성 마법사 실행’을 선택하고 **닫기**를 클릭합니다.
![](https://main.qcloudimg.com/raw/368fa9a4cdb3b47a77c554db855737e0.png)

### 5단계: SharePoint 2016 구성

1. SharePoint 제품 구성 마법사 창에서 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/73aa25130b0e24e6784760a28d6d8fe2.png)
2. 팝업 대화 상자에서 **예**를 클릭하면 구성 중에 서비스를 다시 시작할 수 있습니다.
3. **새 서버 팜 만들기**를 선택하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/b66da626c4883f2f2fb1b75bce6042f6.png)
4. 아래와 같이 구성 데이터베이스 설정 지정 페이지에서 구성 데이터베이스와 액세스 계정을 설정하고 **다음**을 클릭합니다.
SharePoint 데이터베이스는 로컬 호스트에 있으므로 로컬 데이터베이스와 계정을 입력합니다.
![](https://main.qcloudimg.com/raw/d1ccac780ddb9fb308b071fe385ad3f6.png)
5. 서버 팜의 암호를 입력하고 **다음**을 클릭합니다.
6. ‘다중 서버 팜’에 대해 **프런트 엔드**를 선택하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/c23051f73ae543002bc9c15d3d2b3387.png)
7. SharePoint 관리 센터의 포트 번호를 지정하고(이 예시에서는 10000을 사용하지만 필요에 따라 포트 번호를 구성할 수 있음) **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/c7622761e6eb45b1935fccc851379b29.png)
8. 아래와 같이 SharePoint 구성을 확인하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/8d97c6aff42bb8b27fb3e108fa3d16d8.png)
9. Sharepoint 구성이 완료되면 **마침**을 클릭합니다.

