## 작업 시나리오

본 문서는 Windows Server 2012 R2 운영 체제와 Windows Server 2008 운영 체제를 예로, Windows CVM에서 IIS 역할 추가 및 설치 방법에 대해 소개합니다.

## 작업 순서
### Windows Server 2012 R2 운영 체제
1. Windows CVM에 로그인합니다.
2. 아래 이미지와 같이 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>를 클릭하여 서버 관리자를 엽니다.
![](https://main.qcloudimg.com/raw/4bdac63da39ed206ef3c3951d6ed5a13.png)
3. [역할 및 기능 추가]를 클릭하면 '역할 및 기능 추가 마법사' 창이 팝업됩니다.
4. '역할 및 기능 추가 마법사' 창에서 [다음]을 클릭합니다.
5. 아래 이미지와 같이 '설치 유형 선택' 인터페이스에서 [역할 기반 또는 기능 기반 설치]를 선택하고, [다음]을 2회 연속 클릭합니다.
![](https://main.qcloudimg.com/raw/9d97da8191fddcb8c1f97ee37cced18b.png)
6. 아래 이미지와 같이, '서버 역할 선택' 인터페이스에서 [웹 서버(IIS)]를 선택하고 [다음]을 클릭합니다.
'Web 서버(IIS)에 필요한 기능 추가' 대화 상자가 팝업됩니다.
![](https://main.qcloudimg.com/raw/def5577522de9a686b2c8b71db2d86f0.png)
7. 아래 이미지와 같이 'Web 서버(IIS)에 필요한 기능 추가' 대화 상자가 팝업되면 [기능 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/b1647bf6ee80ddf744c03e5521e6ee46.png)
8. [다음]을 클릭합니다.
9. 아래 이미지와 같이 '기능 선택' 인터페이스에서 [.NET Framework 3.5 기능]을 선택하고 [다음]을 2회 연속 클릭합니다.
![](https://main.qcloudimg.com/raw/4c1e5002e5e609242d49735add718d15.png)
10. 아래 이미지와 같이, '역할 서비스 선택' 인터페이스에서 [CGI]를 선택하고 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/9c4077b5e2eeab6c04e01fe4b9d629e6.png)
11. 아래 이미지와 같이 설치 정보를 확인한 후 [설치]를 클릭하고 설치가 완료될 때까지 기다립니다.
![](https://main.qcloudimg.com/raw/b39550bd4ae3d6e4be50040a165fa417.png)
12. 설치 완료 후 CVM의 브라우저에서 `http://localhost/`에 액세스하여 IIS가 성공적으로 설치되었는지 확인합니다.
다음과 같은 인터페이스가 나타나면 설치 성공입니다.
![](https://mc.qcloudimg.com/static/img/e064cc1f765d68edf3dcfb0051d5dbfa/image.png)

### Windows Server 2008 운영 체제

1. Windows CVM에 로그인합니다.
2. 아래 이미지와 같이 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/0e33f3dc1042244ab225ca32c5396296.png" style="margin: 0;"></img>를 클릭하여 서버 관리자를 엽니다.
![](https://main.qcloudimg.com/raw/62d29927e615d282e79a8278b06b5053.png)
3. 아래 이미지와 같이 왼쪽 사이드바에서 [역할]을 선택하고, 오른쪽 창에서 [역할 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/d83b0a8fd599232cdd3df72e8dd99d40.png)
4. 아래 이미지와 같이 '역할 추가 마법사' 창에서 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/1ef476b1e0f16b25f622995792cb4eca.png)
5. 아래 이미지와 같이 '서버 역할 선택' 인터페이스에서 [Web 서버(IIS)]를 선택하고 [다음]을 2회 연속 클릭합니다.
![](https://main.qcloudimg.com/raw/11854282507a671f46ba9bf0998b7a4d.png)
6. 아래 이미지와 같이, '역할 서비스 선택' 인터페이스에서 [GCI]를 선택하고 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/227b434e77fc922761e4d9f03e0fc465.png)
7. 아래 이미지와 같이 설치 정보를 확인한 후 [설치]를 클릭하고 설치가 완료될 때까지 기다립니다.
![](https://main.qcloudimg.com/raw/074a6961e17ab3d3185c3504472509e4.png)
8. 설치 완료 후 CVM의 브라우저에서 `http://localhost/`에 액세스하여 IIS가 성공적으로 설치되었는지 확인합니다.
다음과 같은 인터페이스가 나타나면 설치 성공입니다.
![](https://main.qcloudimg.com/raw/b11cd8170e7646daa3b9ca904b181cf4.png)

