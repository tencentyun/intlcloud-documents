본 문서는 Windows CVM의 PHP 설정을 소개하고 있습니다. [PHP 5.3 이후 버전 설치](#jump)와 [PHP 5.3 및 이전 버전 설치](#jump1)를 소개하고 있으니 사용자는 수요에 따라 관련 내용을 조회하시기 바랍니다.
## 전제 조건
Windows CVM에서 PHP 를 설정하려면 IIS 역할 추가 및 설치를 완료해야 하며, 자세한 내용은 문서 [IIS 설치 설정](
/doc/product/213/2755)을 참조 바랍니다.

### PHP 5.3 이후 버전 설치
<span id="jump">  </span>
PHP 5.3 버전부터 설치 패키지 모드를 삭제하고 zip 파일과 debug pack 두 가지 방식으로만 설치할 수 있습니다. Windows Server 2012 R2 환경에서의 zip 설치를 예시로 사용합니다.

### 소프트웨어 다운로드

 1. CVM에서 PHP zip 설치 패키지(다운로드 주소: http://windows.php.net/download/)를 다운로드 합니다.
>참고:
>IIS에서 실행 시 반드시 Non Thread Safe(NTS)의 x86 패키지를 선택해야 합니다. Windows Server 32bit (x64)에서 반드시 PHP를 x64로 선택해야 한다면, IIS를 선택할 수 없고, 이때 대체 옵션으로 Apache를 사용할 수 있습니다.

	다음과 같은 설치 패키지를 선택할 수 있습니다.
  ![](//mc.qcloudimg.com/static/img/d02eb264ae4d5fbaaf8fd01a08433c61/image.png)
  ![](//mc.qcloudimg.com/static/img/f719e6893f1addd0b260d0c740e4e0ba/image.png)
  ![](//mc.qcloudimg.com/static/img/24ca3df57de6195ad45adabad1c5dc13/image.png)

 2. PHP 5.3 이상 버전의 설치는 Visual C++ Redistributable Update에 따릅니다. 다운로드 받은 PHP 설치 패키지 이름과 아래의 테이블에 표시된 상관관계에 따라 VC Update 설치 프로그램을 다운로드 및 설치합니다.

| PHP 설치 패키지 이름 | Visual C++ Redistributable 설치 패키지 다운로드 주소 |
|---------|---------|---------|
| php-x.x.x-nts-Win32-VC14-x86.zip | [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-cn/download/details.aspx?id=48145) |
| php-x.x.x-nts-Win32-VC11-x86.zip | [Visual C++ Redistributable for Visual Studio 2012 Update 4](https://www.microsoft.com/zh-cn/download/details.aspx?id=30679) |
| php-x.x.x-nts-Win32-VC9-x86.zip | [Microsoft Visual C++ 2008 SP1 Redistributable Package (x86)](https://www.microsoft.com/zh-cn/download/details.aspx?id=5582) |

  다운로드 받은 PHP 설치 패키지가 아래의 그림과 같을 경우
![](//mccdn.qcloud.com/static/img/974ac7192d8f10236fcc27bfd54b8aed/image.png)

테이블 첫째 줄의 상관관계에 따라 VS 2015 버전의 설치 패키지를 다운로드 하고, 다음과 같은 두 개의 `.exe`포맷 파일을 다운로드 및 설치합니다.
![](//mc.qcloudimg.com/static/img/7128c0b621f2534cecddd23b6f3efdb9/image.png)


### 설치 설정
 1. PHP zip 설치 패키지를 압축 해제하고(본 사례에서는 `C:\PHP`로 압축 해제), 아래의 그림과 같이 `php.ini-production`을 복사한 후 `php.ini`로 이름을 변경합니다.
![](//mc.qcloudimg.com/static/img/1be9b1771a93852aff909b08159a5b79/image.png)

 2. [서버 관리자]-[IIS]를 클릭하고 로컬 IIS에서 우클릭으로 IIS관리자를 선택합니다.
![](//mc.qcloudimg.com/static/img/f0387eeb456b7d60e8a5b601cbd3c6b0/image.png)

	왼쪽 호스트 이름(IP)을 클릭하여 메인 페이지로 돌아온 다음 [처리 프로그램 매핑]을 더블클릭 합니다.
![](//mc.qcloudimg.com/static/img/898aa0d2f61c467d333601b75c57704c/image.png)

	오른쪽 [추가 모듈 매핑] 버튼을 클릭한 후 팝업창에 다음과 같은 정보를 작성하고 [확인] 버튼을 클릭하여 저장합니다.
![](//mc.qcloudimg.com/static/img/6f0fd95475a7c00a5779592d15a7753e/image.png)

	>**참고: **
	>실행 가능한 파일로 `php-cgi.exe`를 선택할 수 없다면 파일 확장자를 .exe로 변경하세요: ![](//mc.qcloudimg.com/static/img/d749a9fe4c77f6ea7b55afd8fd37e808/image.png)

 3. 왼쪽 호스트 이름(IP)을 클릭하여 메인 페이지로 돌아온 다음 [기본 문서]를 더블클릭 합니다.
![](//mc.qcloudimg.com/static/img/b5861a95bf6aafd8f4bcaf1c12e9f9be/image.png)

	오른쪽 [추가] 버튼을 클릭하여 `index.php`라는 이름의 기본 문서를 추가합니다.
![](//mc.qcloudimg.com/static/img/6b2543227fec95d1b9bed5f4260a86bb/image.png)

 4. 좌측 호스트 이름(IP)을 클릭하여 메인 페이지로 돌아온 다음 [FastCGI 설정]을 더블클릭 합니다.
![](//mc.qcloudimg.com/static/img/aa23422c038b1024354f01ed0cb3ab73/image.png)

	오른쪽 [편집] 버튼을 클릭하여 [파일에 대한 변경 모니터링]에서 `php.ini` 경로를 선택합니다.
![](//mc.qcloudimg.com/static/img/b4f1ec7d39519dc7d2e89d52ed8a1a87/image.png)
![](//mc.qcloudimg.com/static/img/a2acbed50587552c6ef7ed796b82eb36/image.png)

 5. `C:\inetpub\wwwroot` 디렉터리에서 1개의 PHP 파일 `index.php`를 생성하고 아래의 내용을 입력합니다.
```
<?php
phpinfo();
?>
```

 6. CVM에서 브라우저를 열고 `http://localhost/index.php`에 액세스하여 환경 설정 성공 여부를 조회합니다. 페이지에 다음과 같이 표시되면 설정 성공입니다.
![](//mc.qcloudimg.com/static/img/46eec848975e77e770569eb5d8849d37/image.png)



## PHP 5.3 및 이전 버전 설치
<span id="jump1">  </span>
>참고:
> http://windows.php.net/download/ 공식 다운로드 주소는 더는 PHP 5.3 및 이전 버전의 다운로드를 지원하지 않으니, PHP 5.3 및 이전 버전이 필요한 경우 로컬 다운로드 후 CVM에 파일을 업로드하거나 CVM 네트워크에서 검색하시기 바랍니다. 파일 업로드는 [여기](https://cloud.tencent.com/document/product/213/2761)를 참조하세요.

 1. CVM에서 PHP 설치 패키지를 엽니다.

 2. 아래의 그림과 같이, Web 서버(Web Server Setup) 선택 시, "IIS FastCGI"를 선택합니다.
![](//mc.qcloudimg.com/static/img/ef2f5959779cd733934d11ecbcb4a7f5/image.png)

 4. 설치 인터페이스의 가이드에 따라 PHP 설치를 완료합니다.

 4. 아래의 그림과 같이, `C:/inetpub/wwwroot`디렉터리에서 1개의 PHP 파일 `hello.php`을 생성합니다.
![](//mc.qcloudimg.com/static/img/31d992849b04c1bc76c0d4ca61ab8a4b/image.png)

	`hello.php` 파일에 아래의 내용을 입력합니다.

	```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
	```

 5. 브라우저에서 Windows CVM 공인 IP에 액세스하여 환경 설정 성공 여부를 조회합니다. 페이지에 다음과 같이 표시되면 설정 성공입니다.
![](//mc.qcloudimg.com/static/img/89cebc1127f5c76790c2a9bf3be9fd1f/image.png)


