## 작업 시나리오

본 문서는 Windows Server 2012 R2 운영 체제 CVM을 예로 들어 Windows CVM에 PHP 7.0 및 이전 버전과 PHP 7.0 이후 버전을 구성한 PHP에 대해 소개합니다.


## 전제 조건

- Windows CVM에 이미 로그인 되었으며 해당 CVM에서 IIS 역할 추가 및 설치를 완료하였습니다. 자세한 내용은 [IIS 구성 설치](https://intl.cloud.tencent.com/document/product/213/2755)를 참조하십시오.
-이미 Windows CVM의 공용 네트워크 IP를 가져왔습니다. 자세한 내용은 [공용 네트워크 IP 주소 가져오기](https://intl.cloud.tencent.com/document/product/213/17940)를 참조하십시오.

## 작업 순서

<span id="jump1"></span>
### PHP 7.0 및 이전 버전 설치

> [PHP 공식 사이트](http://windows.php.net/download/)는 더이상 PHP 7.0 및 이전 버전의 설치 패키지 다운로드를 제공하지 않으므로 PHP 7.0 및 이전 버전이 필요할 경우 CVM에서 직접 검색 및 다운로드할 수 있습니다. 또한 로컬에 직접 다운로드하고 설치 패키지를 CVM에 업로드할 수 있습니다. Windows CVM에 파일을 업로드 하는 방법은 [Windows CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/2761)를 참조하십시오. 다음 작업 순서는 PHP 5.2.13 버전을 예로 들어 설명합니다.
> 
1. CVM에서 PHP 설치 패키지를 여십시오.
2. 설치 인터페이스의 가이드에 따라 [Next]를 클릭하십시오.
3. "Web Server Setup" 인터페이스에서[IIS FastCGI]을 선택하고 [Next]를 클릭하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png)
4. 설치 인터페이스의 가이드에 따라 PHP 설치를 완료하십시오.
5. `C:/inetpub/wwwroot` 디렉터리에서 1개 PHP 파일을 생성하십시오. 예를 들면 1개 `hello.php` 파일을 생성합니다. 아래 이미지를 참조하십시오.
5. 새로 생성된 `hello.php` 파일에서 다음과 같은 내용을 입력하고 저장하십시오.
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
6. 운영 체제 인터페이스에서 브라우저를 열고 `http://Windows CVM 공용 네트워크 IP/hello.php`를 액세스하여 환경 구성이 성공적으로 완료되었는지 조회하십시오.
열려 있는 페이지가 다음과 같이 표시되면 구성이 성공적으로 완료되었음을 표시합니다.
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)

<span id="jump"></span>
### PHP 7.0 이후 버전 설치

PHP 7.0 이후 버전은 zip 파일 및 debug pack 두 가지 방식으로 설치됩니다. 다음 작업은 zip 파일 방식으로 Windows Server 2012 R2 환경에 PHP를 설치하는 것을 예로 들었습니다.

#### 소프트웨어 다운로드

1. CVM에서 [PHP 공식 사이트](http://windows.php.net/download/)를 액세스하고 PHP zip 설치 패키지를 다운로드합니다. 아래 이미지를 참조하십시오.
> IIS에서 PHP를 실행할 경우 Non Thread Safe 버전의 x86 설치 패키지를 선택해야 합니다. Windows Server 32bit (x64) 운영 체제에 PHP를 설치할 경우 IIS을 Apache으로 교체하고 Non Thread Safe 버전의 x64 설치 패키지를 선택해야 합니다.
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. 다운로드한 PHP 설치 패키지 이름에 따라 Visual C++ Redistributable 설치 패키지를 다운로드 및 설치합니다.
PHP 설치 패키지는 다운로드 및 설치해야 하는 Visual C++ Redistributable 설치 패키지에 대해 다음 표와 같이 안내합니다.
<table>
<tr><th>PHP 설치 패키지 이름</th><th>Visual C++ Redistributable 설치 패키지 다운로드 주소</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2019</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2017</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable for Visual Studio 2015</a></td></tr>
</table>
 예를 들면 다운로드한 PHP 설치 패키지 이름이 <code>PHP-7.0.6-nts-Win32-VC14-x86.zip</code>일 경우, Microsoft Visual C++ Redistributable for Visual Studio 2015 설치 패키지를 다운로드 및 설치해야 합니다.

#### 설치 구성
1. 다운로드한 PHP zip 설치 패키지를 압축 해제합니다. 예를 들면 `C:\PHP` 디렉터리에 압축 해제합니다.
2. `C:\PHP` 디렉터리의 `php.ini-production` 파일을 복사하고 해당 파일의 접미사를 `.ini`(`php.ini`파일로 이름 바꾸기)로 수정합니다. 아래 이미지를 참조하십시오
3. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>를 클릭하고 서버 관리자를 여십시오.
4. 서버 관리자의 왼쪽 사이드바에서 [IIS]를 클릭합니다.
5. 오른쪽 IIS 관리 창에서 [서버]열에 있는 서버 이름을 마우스 우클릭하여 [Internet Information Sevices (IIS)관리자]를 선택합니다. 아래 이미지를 참조하십시오.
6. 열려 있는 "Internet Information Sevices (IIS)관리자" 창에서 왼쪽 사이드바의 서버 이름을 클릭하고 서버 홈페이지로 진입합니다. 아래 이미지를 참조하십시오.
예를 들면 10_141_9_72 서버 이름을 클릭하고 10_141_9_72 홈페이지에 진입합니다.
7. [10_141_9_72 홈페이지]에서 [프로그램 처리 매핑]을 더블 클릭하여 "프로그램 처리 매핑" 관리 인터페이스로 진입합니다. 아래 이미지를 참조하십시오.
8. 오른쪽 [작업]열에서 [모듈 매핑 추가]를 클릭하여 "모듈 매핑 추가" 창을 여십시오.
9. 열려 있는 "모듈 매핑 추가" 창에서 다음과 같은 정보를 입력하고[확인]을 클릭합니다. 아래 이미지를 참조하십시오.
주요 파라미터 정보는 다음과 같습니다.
 - request 경로: `*.php`을 입력합니다.
 - 모듈: "FastCgiModule"을 선택합니다.
 - 실행 가능한 파일: PHP zip 설치 패키지의 php-cgi.exe 파일, `C:\PHP\php-cgi.exe`을 선택합니다.
 - 이름: 사용자 정의 FastCGI를 입력합니다.
10.  팝업된 알림 상자에서 [예]를 클릭합니다. 
11. 왼쪽 사이드바의 10_141_9_72 서버 이름을 클릭하고 10_141_9_72 홈페이지로 돌아갑니다.
12.  [10_141_9_72 홈페이지]에서 [기본 문서]를 더블 클릭하여 "기본 문서" 관리 인터페이스에 진입합니다. 아래 이미지를 참조하십시오.
13.  오른쪽의 [작업]열에서 [추가]를 클릭하여 "기본 문서 추가" 창을 여십시오.
14.  열려 있는 "기본 문서 추가" 창에서 [이름]을 `index.php`로 입력하고 [확인]을 클릭합니다. 아래 이미지를 참조하십시오.
15.  왼쪽 사이드바의 10_141_9_72 서버 이름을 클릭하고 10_141_9_72 홈페이지로 돌아갑니다.
16.  [10_141_9_72 홈페이지]에서 [FastCGI 설정]을 더블 클릭하여 "FastCGI 설정" 관리 페이지로 진입합니다. 아래 이미지를 참조하십시오.
17.  "FastCGI 설정" 관리 인터페이스에서 FastCGI 애플리케이션을 선택하고 [편집]을 클릭합니다. 아래 이미지를 참조하십시오.
18.  열려 있는 "FastCGI 애플리케이션 편집" 창에서 [파일 변경 모니터링]을 `php.ini` 파일 경로로 설정합니다. 아래 이미지를 참조하십시오.
19. `C:\inetpub\wwwroot` 디렉터리에서 1개 PHP 파일을 생성합니다. 예를 들면 1개 `index.php` 파일을 생성합니다.
20. 새로 생성된 `index.php` 파일에서 다음과 같은 내용을 입력하고 저장합니다.
```
<?php
phpinfo();
?>
```
21. 운영 체제 인터페이스에서 브라우저를 열고 `http://localhost/index.php`를 액세스하여 환경 구성이 성공적으로 완료되었는지 확인합니다.
열려 있는 페이지가 다음과 같이 표시되면 구성이 성공적으로 완료되었음을 표시합니다.
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

