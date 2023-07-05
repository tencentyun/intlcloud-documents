## 작업 시나리오
WordPress는 PHP 언어를 사용해 개발한 블로그 플랫폼입니다. WordPress를 통해 개인의 블로그 플랫폼을 구축해 사용할 수 있습니다. 본 문서는 Windows Server 2012 운영 체제의 Tencent Cloud 서버를 예시로 하며, WordPress 개인 웹 사이트를 수동으로 구축합니다.

<dx-alert infotype="notice" title="">
Tencent Cloud는 클라우드 마켓의 이미지 환경을 통해 WordPress 개인 블로그를 배포할 것을 권장하며, 수동 구축 과정이 오래 걸릴 수 있습니다.
</dx-alert>



## 소프트웨어
WordPress 개인 사이트는 PHP 5.6.20 이상 및 MySQL 5.0 이상에서 구축할 수 있습니다. 보안성 강화를 위해 WordPress 개인 사이트 구축 시 PHP 7.3 이상, MySQL 5.6 이상 버전 설치를 권장합니다.

본 문에서 구축한 WordPress 개인 사이트의 구성 버전과 설명은 다음과 같습니다.
- Windows: Windows 운영 체제, 본 문은 Windows Server 2012 R2 데이터센터 Edition의 64비트 중국어 버전을 예로 들어 설명합니다.
- IIS: Web 서버의 경우, 본 문은 IIS 8.5를 예시로 사용합니다.
- MySQL: 본 문은 데이터베이스 MySQL 8.0.19를 예시로 사용합니다.
- PHP: 스크립트 언어의 경우, 본 문은 PHP 7.1.30를 예시로 사용합니다.
- WordPress: 블로그 플랫폼, 본 문은 WordPress 5.9를 예시로 사용합니다.


## 작업 단계

### 1단계: CVM(Cloud Virtual Machine) 로그인
[RDP 파일을 사용하여 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/zh/document/product/213/5435).
실제 작업 스타일에 따라 [데스크탑에 원격 연결하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32498)할 수 있습니다.

### 2단계: WIPM 환경 구축
[WIPM 환경 수동 구축](https://intl.cloud.tencent.com/zh/document/product/213/33143)을 참고하여 다음을 수행합니다.
1. IIS 서비스를 설치합니다.
2. PHP 5.6.20 이상 버전 환경을 배포합니다.
3. MySQL 5.6 이상 버전 데이터베이스를 설치합니다.

### 3단계: WordPress 설치 및 설정

<dx-alert infotype="explain" title="">
WordPress는 WordPress 공식 홈페이지에서 최신 중국어 버전의 WordPress를 다운로드하여 설치할 수 있으며, 이 튜토리얼에서는 WordPress 중국어 버전을 사용합니다.
</dx-alert>



1. WordPress를 다운로드하고 WordPress 설치 패키지를 CVM에 압축 해제합니다.
예를 들어, WordPress 설치 패키지의 압축을 'C:\wordpress' 디렉터리에 해제합니다.
2. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"> >  <img src="https://main.qcloudimg.com/raw/ca83b4e70e201fe9ff98dc1f2b207cee.png" style="margin: -3px 0px;"> >  **MySQL 5.6 Command Line Client**를 클릭하여, MySQL 명령 라인 클라이언트를 엽니다.
3. MySQL 명령 라인 클라이언트에서 다음 명령을 실행하여 WordPress 데이터베이스를 생성합니다.
예를 들어 ‘wordpress’ 데이터베이스를 생성합니다.
```
create database wordpress;
```
4. WordPress의 압축 해제 설치 경로에서 `wp-config-sample.php` 파일을 찾아 복사하고, 파일 이름을 `wp-config.php`로 변경합니다.
5. 'wp-config.php' 파일을 텍스트 편집기로 열고 관련 설정 정보를 [3단계: MySQL 데이터베이스 설치](https://intl.cloud.tencent.com/document/product/213/10190)의 내용으로 수정합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5900f1b371a512f7c058783caeccc719.png)
6. `wp-config.php` 파일을 저장합니다.
7. <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-5px 0px">을(를) 클릭하여 서버 관리자를 엽니다.
8. 서버 관리자의 왼쪽 사이드바에서 **IIS**를 선택하고 오른쪽 IIS 관리 창의 **서버** 열에서 서버 이름을 우클릭하고 **Internet Information Sevices(IIS) 관리자**를 선택합니다.
9. 열려 있는 'Internet Information Sevices (IIS)관리자' 창의 왼쪽 사이드바에서 서버 이름을 차례로 펼쳐 **웹사이트**를 클릭하여 ‘웹사이트’ 관리 페이지로 이동합니다.
10. **웹사이트**에서 80번 포트에 바인딩된 웹사이트를 삭제합니다.
웹 사이트의 바인딩 포트를 점유되어 있지 않는 다른 포트 번호로 수정할 수도 있습니다. 예를 들어 포트 8080으로 수정합니다.
11. 오른쪽의 **작업** 열에서 **웹 사이트 추가**를 클릭합니다.
12. 팝업 창에서 다음 정보를 입력하고 **확인**을 클릭합니다.
    - **웹 사이트 이름**: 사용자 정의합니다. 예: wordpress.
    - **응용 프로그램 풀**: **DefaultAppPool**로 선택합니다.
    - **물리적 경로**: `C:\wordpress`와 같이 WordPress가 압축 해제된 경로를 선택합니다.
13. PHP의 압축 해제 설치 경로에서 `php.ini` 파일을 열고 다음 콘텐츠를 수정합니다.
    1. PHP 버전에 따라 해당 설정 매개변수를 수정합니다.
       - PHP 버전 5.X의 경우 `extension=php_mysql.dll`을 찾아 앞의 `;`을 삭제합니다.
       - PHP 버전 7.X의 경우 `extension=php_mysqli.dll` 또는 `extension=mysqli`를 찾아 앞의 `;`을 삭제합니다.
    2. `extension_dir = "ext"`를 찾아 앞의 `;`을 삭제합니다.
14. `php.ini` 파일을 저장합니다.

### 4단계: WordPress 설정 인증

1. 브라우저를 이용하여 `http://localhost/wp-admin/install.php`에 액세스하여 WordPress 설치 페이지로 이동하여 WordPress 설정을 시작합니다.
2. WordPress 설치 마법사에 따라 아래의 설치 정보를 입력하고 **WordPress 설치**를 클릭해 설치를 완료합니다.
<table>
	<tr><th width="16%">필수 정보</th><th>설명</th></tr>
	<tr><td>웹 사이트 제목</td><td>WordPress 웹 사이트 이름.</td></tr>
	<tr><td>사용자 이름</td><td>WordPress 관리자 명칭. 보안상의 이유로 admin 명칭과 다르게 설정하길 권장합니다. 기본 사용자 이름이 admin과 비교하여 크래킹이 더 어렵기 때문입니다.</td></tr>
	<tr><td>비밀번호</td><td>강력한 기본 비밀번호 또는 사용자 정의 비밀번호를 사용할 수 있습니다. 기존 비밀번호는 재사용하지 마시고 비밀번호는 안전한 곳에 보관하시기 바랍니다.</td></tr>
	<tr><td>귀하의 이메일</td><td>공지를 받을 이메일 주소입니다.</td></tr>
</table>
이제 WordPress 블로그에 로그인할 수 있으며, 블로그에 게시글을 업로드할 수 있습니다.

## FAQ
CVM 사용 도중 문제가 생겼을 경우, 아래의 문서를 참고하여 실제 상황에 따라 문제를 분석 및 해결할 수 있습니다.
- CVM 로그인 문제는 [키 관련 문제](https://intl.cloud.tencent.com/document/product/213/18120), [로그인 및 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참고하십시오.
- CVM 네트워크 문제는 [IP 주소 문제](https://intl.cloud.tencent.com/document/product/213/17285), [포트 관련 문제](https://intl.cloud.tencent.com/document/product/213/2502)를 참고하십시오.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/zh/document/product/213/17351)를 참고하십시오.

