## 작업 시나리오

본 문서는 Windows Server 2012 R2 운영 체제의 CVM을 예로 들어, Windows CVM에 PHP 5.3 이전 버전과 PHP 5.3 이후 버전의 PHP을 설정하는 방법에 대해 소개합니다.


## 전제 조건

- Windows CVM에 로그인하고, 해당 CVM의 IIS 역할 추가 및 설치를 완료한 상태여야 합니다. 자세한 내용은 [IIS 설정 설치](https://intl.cloud.tencent.com/document/product/213/2755)를 참조 바랍니다.
- Windows CVM의 공인 IP를 가져온 상태여야 합니다. 자세한 내용은 [공인 IP 주소 가져오기](https://intl.cloud.tencent.com/document/product/213/17940)를 참조 바랍니다.

## 작업 순서

<span id="jump1"></span>
### PHP 5.3 이전 버전 설치

> [PHP 공식 홈페이지](http://windows.php.net/download/)에서는 더 이상 PHP 5.2 이전 버전의 설치 패키지를 다운로드할 수 없으므로, PHP 5.2 이전 버전이 필요할 경우 CVM에서 직접 검색하여 다운로드할 수 있습니다. 로컬에 직접 다운로드한 뒤, 설치 패키지를 CVM에 업로드할 수도 있습니다. Windows CVM에 파일을 업로드하는 자세한 방법은 [Windows CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/2761)를 참조 바랍니다. 아래의 작업 순서는 PHP 5.2.13 버전을 예로 들어 설명합니다.
> 
1. CVM에서 PHP 설치 패키지를 엽니다.
2. 설치 인터페이스의 안내에 따라 [Next]를 클릭합니다.
3. 아래 이미지와 같이, 'Web Server Setup' 인터페이스에서 [IIS FastCGI]을 선택하고 [Next]를 클릭합니다.
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png)
4. 설치 인터페이스의 안내에 따라 PHP 설치를 완료합니다.
4. 아래 이미지와 같이, `C:/inetpub/wwwroot` 디렉터리에서 `hello.php`와 같은 PHP 파일 하나를 생성합니다.

5. 신규 생성된 `hello.php` 파일에 다음과 같은 내용을 작성한 뒤 저장합니다.
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
6. 운영 체제 인터페이스에서 브라우저를 열고 `http://Windows CVM의 공인 IP/hello.php`에 액세스하여, 환경 설정이 성공적으로 완료되었는지 확인합니다.
열린 페이지가 다음과 같다면 설정이 성공적으로 완료되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)

<span id="jump"></span>
### PHP 5.3 이후 버전 설치

PHP 5.3 이후 버전은 설치 패키지 방식을 사용하지 않고, zip 파일 및 debug pack 이 두 가지 방식으로만 설치할 수 있습니다. 아래의 작업 순서는 zip 파일을 사용하여 Windows Server 2012 R2 환경에 PHP를 설치하는 방법을 예로 들어 설명합니다.

#### 소프트웨어 다운로드

1. 아래 이미지와 같이, CVM에서 [PHP 공식 홈페이지](http://windows.php.net/download/)에 액세스하여 PHP zip 설치 패키지를 다운로드합니다.
> IIS에서 PHP를 실행할 때, Non Thread Safe 버전의 x86 설치 패키지를 선택해야 합니다. 서버가 Windows Server 32bit(x86) 운영 체제라면, IIS를 Apache로 교체하고 Thread Safe 버전의 x86 설치 패키지를 선택해야 합니다.
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. 다운로드한 PHP 설치 패키지의 이름에 따라 Visual C++ Redistributable 설치 패키지를 다운로드 및 설치합니다.
다운로드 및 설치해야 하는 PHP 설치 패키지별 Visual C++ Redistributable 설치 패키지는 아래의 표와 같습니다.
<table>
<tr><th>PHP 설치 패키지 이름</th><th>Visual C++ Redistributable 설치 패키지 다운로드 주소</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2019</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2017</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable for Visual Studio 2015</a></td></tr>
</table>
 예를 들어, 다운로드한 PHP 설치 패키지 이름이 <code>PHP-7.1.30-nts-Win32-VC14-x86.zip</code>이라면, Microsoft Visual C++ Redistributable for Visual Studio 2015 설치 패키지를 다운로드 및 설치해야 합니다.

#### 설치 설정
1. 다운로드한 PHP zip 설치 패키지를 압축 해제합니다. 예: `C:\PHP` 디렉터리에 압축 해제합니다.
2. 아래 이미지와 같이, `C:\PHP` 디렉터리의 `php.ini-production` 파일을 복사하여, 해당 파일의 확장자를 `.ini`로 수정(파일명을 `php.ini`로 수정)합니다.
![](https://main.qcloudimg.com/raw/52d9a2098fe73c8ddb41366b9732a000.png)
3. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>를 클릭하여 서버 관리자를 엽니다.
4. 서버 관리자의 왼쪽 사이드바에서 [IIS]를 클릭합니다.
5. 아래 이미지와 같이, 오른쪽 IIS 관리 창의 [서버] 메뉴에서 서버 이름을 우클릭한 뒤, [Internet Information Sevices (IIS) 관리자]를 선택합니다.
![](https://main.qcloudimg.com/raw/55e0b4c86de284050e5d810e92650337.png)
6. 아래 이미지와 같이, 열린 'IIS(인터넷 정보 서비스) 관리자' 창의 왼쪽 사이드바에서 서버 이름을 클릭하면 서버의 메인 페이지로 이동합니다.
예: 10_141_9_72 서버 이름을 클릭하면 10_141_9_72 메인 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/ab0f2306624452d4a3ab9fd5389d5b1d.png)
7. 아래 이미지와 같이, [10_141_9_72 메인 페이지]에서 [처리기 매핑]을 더블 클릭하여 '처리기 매핑' 관리 인터페이스로 이동합니다.
![](https://main.qcloudimg.com/raw/916a9cc9ce1270dbbfe6ddbb58f937e7.png)
8. 오른쪽의 [작업] 메뉴에서 [모듈 매핑 추가]를 클릭하여 '모듈 매핑 추가' 창을 엽니다.
9. 아래 이미지와 같이, 열린 '모듈 매핑 추가' 창에서 다음의 정보를 입력하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/a4d139682fc14204acd77ac3d1ea10eb.png)
주요 매개변수 정보는 다음과 같습니다.
 - request 경로: `*.php`를 입력합니다.
 - 모듈: "FastCgiModule"을 선택합니다.
 - 실행 가능한 파일: PHP zip 설치 패키지의 php-cgi.exe 파일, 즉 `C:\PHP\php-cgi.exe`를 선택합니다.
 - 이름: 사용자 정의, 예를 들어 FastCGI를 입력합니다.
10. 팝업된 알림창에서 [예]를 클릭합니다. 
11. 왼쪽 사이드바에서 10_141_9_72 서버 이름을 클릭하여, 10_141_9_72 메인 페이지로 돌아갑니다.
12. 아래 이미지와 같이, [10_141_9_72 메인 페이지]에서 [기본 문서]를 더블 클릭하여 '기본 문서' 관리 인터페이스로 이동합니다.
![](https://main.qcloudimg.com/raw/6a896eeb929ae0104b1792e08bd895a6.png)
13. 오른쪽의 [작업] 메뉴에서 [추가]를 클릭하여 '기본 문서 추가' 창을 엽니다.
14. 아래 이미지와 같이, 열린 '기본 문서 추가' 창에서 [이름]에 `index.php`를 입력하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/2d09af5d86755dd481b13efb0b3619a2.png)
15. 왼쪽 사이드바에서 10_141_9_72 서버 이름을 클릭하여, 10_141_9_72 메인 페이지로 돌아갑니다.
16. 아래 이미지와 같이, [10_141_9_72 메인 페이지]에서 [FastCGI 설정]을 더블 클릭하여 'FastCGI 설정' 관리 인터페이스로 이동합니다.
![](https://main.qcloudimg.com/raw/2a0693d3b837804b546fc690b4fb5cee.png)
17. 아래 이미지와 같이, 'FastCGI 설정' 관리 인터페이스에서 FastCGI 응용 프로그램을 선택하고 [편집]을 클릭합니다.
![](https://main.qcloudimg.com/raw/2038fa0df5c08820dc028fb3635fcda4.png)
18. 아래 이미지와 같이, 열린 'FastCGI 응용 프로그램 편집' 창에서 [파일의 변경 내용 모니터]를 `php.ini` 파일의 경로로 설정합니다.
![](https://main.qcloudimg.com/raw/b1aa458607934a5331b51e22762d0dec.png)
19. `C:\inetpub\wwwroot` 디렉터리에서 PHP 파일 하나를 생성합니다. 예: `index.php` 파일 하나를 생성합니다.
20. 신규 생성된 `index.php` 파일에 다음과 같은 내용을 작성한 뒤 저장합니다.
```
<?php
phpinfo();
?>
```
21. 운영 체제 인터페이스에서 브라우저를 열고 `http://localhost/index.php`에 액세스하여, 환경 설정이 성공적으로 완료되었는지 확인합니다.
열린 페이지가 다음과 같다면 설정이 성공적으로 완료되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

