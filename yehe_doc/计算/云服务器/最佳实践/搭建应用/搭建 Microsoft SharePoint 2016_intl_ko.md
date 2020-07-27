## 작업 시나리오
본 문서는 CVM 인스턴스에 Microsoft SharePoint 2016을 구축하는 방법에 대해 소개합니다.

## 예시 소프트웨어 버전
본문의 예시 작업에서 사용하는 CVM 인스턴스 하드웨어의 사양은 다음과 같습니다.
- vCPU: 쿼드코어
- 메모리: 8GB

본문의 예시 작업에서 사용하는 소프트웨어의 버전은 다음과 같습니다.
- 운영 체제: Windows Server 2012 R2 데이터센터 버전의 64비트 중국어 버전
- 데이터베이스: SQL Server 2014

## 전제 조건
Windows CVM을 구비해야 합니다. CVM을 구매하지 않았다면, [Windows CVM 사용자 정의 설정](https://intl.cloud.tencent.com/document/product/213/10516)을 참조 바랍니다.

## 작업 순서

### 1단계: Windows 인스턴스 로그인
[RDP 파일을 사용하여 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5435)하거나 실제 작업 스타일에 따라 [원격 데스크톱 연결을 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32498)할 수 있습니다.

<span id="AddAD_DHCP_DNS_IIS"></span>
### 2단계: AD, DHCP, DNS, IIS 서비스 추가
1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>를 클릭하여 서버 관리자를 엽니다.
2. 아래 이미지와 같이, 왼쪽 메뉴에서 [로컬 서버]를 선택한 뒤 [IE 보안 강화 구성]을 찾습니다.
![](https://main.qcloudimg.com/raw/9192efa291cfbed136db9a6e3a7c3e59.png)
3. 아래 이미지와 같이 [IE 보안 강화 구성]의 사용을 사용 안 함으로 선택합니다.
![](https://main.qcloudimg.com/raw/8b860bb5dfc44ec4993c3a899058b1ae.png)
4. 왼쪽 메뉴에서 [대시보드]를 선택한 뒤 [역할 및 기능 추가]를 클릭하여 '역할 및 기능 추가 마법사' 창을 엽니다.
5. '역할 및 기능 추가 마법사' 창에서 기본 구성을 유지하고 [다음]을 3번 연속 클릭합니다.
6. 아래 이미지와 같이 '서버 역할 선택' 인터페이스에서 [Active Diretory 도메인 서비스], [DHCP 서버], [DNS 서버] 및 [웹 서버(IIS)]를 모두 선택한 뒤 팝업 창에서 [기능 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/532dc46bf0682427e9b210bf36e1986f.png)
7. [다음]을 클릭합니다.
8. 아래 이미지와 같이 '기능 선택' 인터페이스에서 [.NET Framework 3.5 기능]을 선택하고 팝업 창에서 [기능 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/44998bf3effff6bec51ea9c502ec8c9a.png)
9. 기본 구성을 유지한 채로 [다음]을 6번 연속 클릭합니다.
10. 설치 정보를 확인한 뒤 [설치]를 클릭합니다.
11. 설치가 완료되면 CVM을 재시작합니다.
12. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>를 클릭하여 서버 관리자를 엽니다.
13. 아래 이미지와 같이 서버 관리자 창에서 <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img>를 클릭하여 [이 서버를 도메인 컨트롤러로 업그레이드]를 선택합니다.
![](https://main.qcloudimg.com/raw/03def6c00f1bed979c9dde28ebbd2202.png)
14. <span id="step14"></span>아래 이미지와 같이 열린 'Active Directory 도메인 서비스 구성 마법사' 창의 '배포 작업을 선택합니다'에서 [새 포리스트를 추가합니다]를 선택하고, 루트 도메인 이름을 입력한 뒤 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/adb2e7cbed1580eebeb201d837f41efa.png)
15. <span id="step15"></span>아래 이미지와 같이 DSRM(디렉터리 서비스 복원 모드)의 암호를 설정한 뒤 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/dc24edd5f6d194cacc7b6ff8511417b7.png)
16. 기본 구성을 유지한 채로 [다음]을 4번 연속 클릭합니다.
17. [설치]를 클릭합니다.
18. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>를 클릭하여 서버 관리자를 엽니다.
19. 아래 이미지와 같이 서버 관리자 창에서 <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img>를 클릭하여 [DHCP 구성 완료]를 선택합니다.
![](https://main.qcloudimg.com/raw/132eb061b6fd53da22b6211fd2411537.png)
20. 'DHCP 설치 후 구성 마법사' 창이 열리면 [다음]을 클릭합니다.
21. 아래 이미지와 같이 기본 구성을 유지하고 [커밋]을 클릭하여 구성 설치를 완료합니다.
![](https://main.qcloudimg.com/raw/6dab6c5968282757ff2e146c74765772.png)
22. [닫기]를 클릭하여 창을 닫습니다.

### 3단계: 데이터베이스 SQL Server 2014 설치

1. CVM에서 브라우저를 열고 SQL Server 2014 공식 홈페이지에 액세스하여 SQL Server 2014 설치 패키지를 다운로드합니다.
> SQL Server 2014 설치 패키지는 타사 사이트 또는 다른 합법적인 경로를 통해서도 다운로드할 수 있습니다.
>
2. 'Setup.exe' 파일을 더블 클릭하여 SQL Server 설치 센터를 열어 설치 탭 인터페이스로 들어갑니다.
![](https://main.qcloudimg.com/raw/66c2d6df469197d5550ce2fbae3cc5c9.png)
3. [신규 SQL Server 단독 설치 또는 기존 설치에 기능 추가]를 클릭합니다.
4. 제품 키를 입력한 후 [다음]을 클릭합니다.
5. 사용 조건에서 [동의함]을 선택하고 [다음]을 클릭합니다.
6. 기본 구성을 유지한 채로 [다음]을 클릭합니다.
7. 설치 확인을 완료한 후 [다음]을 클릭합니다.
8. 기본 구성을 유지한 채로 [다음]을 클릭합니다.
9. 아래 이미지와 같이 '기능 선택' 인터페이스에서 [전체 선택]을 클릭하여 전체 기능을 선택한 뒤 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/15bb32c2d2121aadc092428911cefc16.png)
10. 아래 이미지와 같이 '인스턴스 구성' 인터페이스에서 [기본 인스턴스]를 선택한 후 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/3663ca417620325c7b45bc8c60996db7.png)
11. 아래 이미지와 같이 '서버 구성' 인터페이스에서 SQL Server 데이터베이스 엔진 및 SQL Server Analysis Services의 계정 이름 및 암호를 설정한 후 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/c0bb2b960115d66eda4e38b40a56fc78.png)
 - 'SQL Server 데이터베이스 엔진'의 계정 이름은 'NT AUTHORITY\NETWORK SERVICE'로 설정합니다.
 - 'SQL Server Analysis Services'의 계정 이름과 암호는 [2단계: AD, DHCP, DNS, IIS 서비스 추가](#AddAD_DHCP_DNS_IIS)의 [14](#step14) - [15](#step15)에서 설정한 도메인 이름 및 암호와 동일하게 설정합니다.
12. 아래 이미지와 같이 '데이터베이스 엔진' 인터페이스에서 [현재 사용자 추가]를 클릭하여 현재 계정을 SQL Server 관리자 계정으로 지정한 후 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/c0218409bfb7044221cb6c0fe1862588.png)
13. 아래 이미지와 같이 'Analysis Services 구성' 인터페이스에서 [현재 사용자 추가]를 클릭하여 현재 계정에 Analysis Services 관리자 권한을 추가한 후 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/43243a387cc67f20ea125fb2491df24d.png)
14. 기본 구성을 유지한 채로 [다음]을 클릭합니다.
15. 아래 이미지와 같이 'Distributed Replay Controller' 인터페이스에서 [현재 사용자 추가]를 클릭하여 현재 계정에 Distributed Replay Controller 권한을 추가한 후 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/46158b2f9a6e5f802c2ae27a2f5f0970.png)
16. 기본 구성을 유지한 채로 [다음]을 클릭합니다.
17. SQL Server의 구성을 확인한 후 [설치]를 클릭합니다.
18. SQL Server의 설치가 완료되면 [닫기]를 클릭합니다.


### 4단계: SharePoint 2016 설치

1. CVM에서 브라우저를 열고 Microsoft SharePoint 2016 공식 홈페이지에 액세스하여 Microsoft SharePoint 2016 설치 패키지를 다운로드합니다.
2. 아래 이미지와 같이 Microsoft SharePoint 2016 이미지 파일을 열어, 제품 준비 도구인 `prerequisiteinstaller.exe` 실행 파일을 더블 클릭하여 Microsoft SharePoint 2016 제품 준비 도구를 설치합니다.
![](https://main.qcloudimg.com/raw/2de50f6a3172bd870f86378e33f1f07e.png)
3. 아래 이미지와 같이 Microsoft SharePoint 2016 제품 준비 도구 설치 창에서 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/e5cd9c8ca37b36984258050443fdf5f1.png)
4. [동의함]을 선택하고 [다음]을 클릭합니다.
5. 아래 이미지와 같이 필수 구성 요소의 설치가 완료되면 [완료]를 클릭하여 CVM을 재시작합니다.
![](https://main.qcloudimg.com/raw/cc8f3bf7b151946d5fdd8f3882ea9549.png)
6. 아래 이미지와 같이 Microsoft SharePoint 2016 이미지 파일을 열어, `setup.exe` 설치 파일을 더블 클릭하면 Microsoft SharePoint 2016의 설치가 시작됩니다.
![](https://main.qcloudimg.com/raw/bf0369e20c77e1f57bfef3fef42fab31.png)
7. 제품 키를 입력한 후 [계속]을 클릭합니다.
8. [동의함]을 선택하고 [계속]을 클릭합니다.
9. 아래 이미지와 같이 설치할 디렉터리를 선택하고(본 예시에서는 기본 설정을 유지하지만 사용자는 실제 필요에 따라 파일 위치를 선택할 수 있습니다) [설치하기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/0dbdfedb241b02a7f2fdaefb1a7599af.png)
10. 아래 이미지와 같이 설치가 완료된 후 [SharePoint 제품 구성 마법사 실행]을 선택한 후 [완료]를 클릭합니다.
![](https://main.qcloudimg.com/raw/3fa47faa1f8bed1a8ec478260ee64481.png)

### 5단계: SharePoint 2016 구성

1. 아래 이미지와 같이 SharePoint 제품 구성 마법사가 실행되면 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/3e8d015ab34ab8de8172838dd21d31ac.png)
2. 팝업된 알림창에서 [예]를 클릭하여 제품 구성 프로세스 중 서비스를 다시 시작하는 것에 동의합니다.
3. 아래 이미지와 같이 [새 서버 팜 만들기]를 선택하고 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/f87545fb79d747bf64c38131fbb318d4.png)
4. 구성 데이터베이스 설정 및 데이터베이스 액세스 계정 정보를 지정한 후 [다음]을 클릭합니다.
SharePoint의 데이터베이스가 로컬 기기에 있으므로 로컬의 데이터베이스와 계정을 입력합니다.
![](https://main.qcloudimg.com/raw/cf9723c7885399e0e5004f1ecee4ea2d.png)
5. 서버 팜의 암호를 설정한 후 [다음]을 클릭합니다.
6. 아래 이미지와 같이 '다중 서버 팜'에서 [프런트 엔드]로 설정한 후 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/95da6977363606dd62835d12bc9b7ae2.png)
7. 아래 이미지와 같이 Sharepoint 관리 센터의 포트 번호(본 예시에서는 10000으로 설정하지만 실제 필요에 따라 포트 번호를 설정할 수 있습니다)를 설정한 후, [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/26ef65e1e8e229e9c67c2eafc40c0d32.png)
8. 아래 이미지와 같이 SharePoint의 구성을 확인한 후 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/a0e8ee05fcc2fc4b6f717bb0e03287af.png)
9. SharePoint 구성 적용이 완료되면 [완료]를 클릭합니다.

