본 문서에서는 Windows 2012 R2 시스템 버전 및 Windows 2008시스템 버전에서의 IIS 역할 추가 및 설치 과정에 대해 소개합니다.
## Windows 2012 R2 버전(예시)
 1. Windows CVM에 로그인하고 좌측 하단의 [시작(Start)]을 클릭 및 [서버 관리자(Server Manager)]를 선택하여 서버 관리 인터페이스를 열면 다음과 같이 표시됩니다.
![](//mc.qcloudimg.com/static/img/7b433cabe3d7349b5a38b359639e4c7c/image.png)

 2. [역할 및 기능 추가] 버튼을 누르고 역할 및 기능 추가 팝업창의 "시작 전" 페이지에서 [다음 단계] 버튼 클릭, "설치 유형 선택" 페이지에서 [역할 기반 또는 기능 기반 설치]를 선택한 후, [다음 단계] 버튼을 누릅니다.
![](//mc.qcloudimg.com/static/img/b0f5ffb889f4d23213f0811bd945b170/image.png)
![](//mc.qcloudimg.com/static/img/027fe90a3c882520662783bdcda97b94/image.png)
![](//mc.qcloudimg.com/static/img/919430e0493d9580c33eab871ffee557/image.png)

 3. 페이지 왼쪽에서 "서버 역할" 탭을 선택하고 [웹 서버(IIS)]를 체크하면 뜨는 팝업 창에서 [기능 추가] 버튼을 클릭한 후 [다음 단계] 버튼을 클릭합니다.
![](//mc.qcloudimg.com/static/img/0d69cbfd04d9a614eeb00559f34bafba/image.png)
![](//mc.qcloudimg.com/static/img/a254c87a59392801a4bf23521c9c1535/image.png)

 4. "기능" 탭에서 .Net3.5 를 체크하고 [다음 단계] 버튼을 누른 후, "웹 서버(IIS)" 선택을 마치면 [다음 단계]를 클릭합니다.
![](//mc.qcloudimg.com/static/img/703cda6d11a5cfc3a26f471f0535dc17/image.png)
![](//mc.qcloudimg.com/static/img/5d84575332b4c9c425bcdf0baa80f7e6/image.png)

 5. "역할 서비스" 탭에서 [CGI] 옵션을 선택 후 [다음 단계]를 클릭합니다.
![](//mc.qcloudimg.com/static/img/958f0c466a633ea6c58de651a4ad7982/image.png)

 6. 설치 확인 및 설치 완료 대기: 
![](//mc.qcloudimg.com/static/img/045b132f13b06c6e499b85ecb34a3f43/image.png)

 7. 설치 완료 후 CVM의 브라우저에서 ```http://localhost/```에 액세스하여 설치 성공 여부를 인증합니다. 다음과 같은 페이지가 나타나면 설치 성공입니다.
![](//mc.qcloudimg.com/static/img/e064cc1f765d68edf3dcfb0051d5dbfa/image.png)

## Windows 2008 버전(예시)
 1. Windows CVM에 로그인하고 좌측 하단의 [시작(Start)] 메뉴의 [관리 툴]에서 [서버 관리자]를 클릭하여 서버 관리자 페이지를 엽니다.
![](//mc.qcloudimg.com/static/img/787983bdedb15a6d496119c953d35e1a/image.png)

 2. [역할 및 기능 추가(Add Roles)]를 클릭하여 서버 역할을 추가하고 "Web Server(IIS)" 탭을 선택한 후 [다음 단계(Next)]를 클릭합니다.
![](//mccdn.qcloud.com/img56b1bb12831b3.png)
ㄴ![](//mccdn.qcloud.com/img56b1bcee2d9e8.png)

 3. 역할 서비스(Role Services) 선택 시, "CGI" 탭을 체크합니다.
![](//mccdn.qcloud.com/img56b1bd1b8f220.png)

 4. 설정 완료 후 [설치(install)를 눌러 설치합니다.
![](//mccdn.qcloud.com/img56b1bd4f18f1a.png)

 5. 브라우저에서 Windows CVM 공인 IP에 액세스하여 IIS 서비스가 정상적으로 실행되는지 확인합니다. 다음과 같이 표시되면 IIS 설치 및 설정에 성공했음을 의미합니다.
![](//mccdn.qcloud.com/img56b1bd7c5b0be.png)

