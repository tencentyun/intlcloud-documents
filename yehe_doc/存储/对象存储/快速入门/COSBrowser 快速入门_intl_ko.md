COS(Cloud Object Storage)를 처음 사용하신다면 COS [버킷](https://intl.cloud.tencent.com/document/product/436/13312), [객체](https://intl.cloud.tencent.com/document/product/436/13324), [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518) 및 [FAQ](https://intl.cloud.tencent.com/document/product/436/6282)부터 숙지하시기 바랍니다.

COSBrowser는 Tencent Cloud의 COS가 선보이는 시각화 인터페이스 툴입니다. Windows, macOS, Linux, Android 및 iOS를 지원하며, 보다 간편하고 인터랙티브한 사용 경험을 제공합니다. 편리하게 COS 리소스를 조회, 전송, 관리해 보십시오.
Windows 플랫폼의 COSBrowser에서의 버킷 생성, 객체 업로드, 객체 다운로드 및 객체 공유 방법은 다음과 같습니다.


## 전제 조건

1. Tencent Cloud 계정으로 COS 서비스를 활성화해야 합니다. COS 서비스를 비활성화한 경우, [COS 콘솔](https://console.cloud.tencent.com/cos5)에서 안내에 따라 활성화하십시오.
2. COSBrowser 툴은 API 키로 로그인합니다. [API Keys](https://console.cloud.tencent.com/cam/capi) 관리 페이지에서 먼저 API 키를 생성하십시오.


## 1단계: COSBrowser 다운로드 및 설치하기

Windows 환경의 COSBrowser 시스템 사양: Windows 7 32/64비트 이상, Windows Server 2008 R2 64비트 이상을 지원하며, 기타 시스템 사양의 COSBrowser는 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)에서 다운로드하십시오.


<div style="background-color:#00A4FF; width: 250px; height: 35px; line-height:35px; text-align:center;"><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe" target="_blank"  style="color: white; font-size:16px;">클릭 후 COSBrowser 다운로드</a></div><br>



## 2단계: COSBrowser 로그인하기

[API Keys](https://console.cloud.tencent.com/cam/capi)를 이용해 COSBrowser에 로그인합니다.


## 3단계: 버킷 생성하기

1. 로그인 성공 후 툴 인터페이스에서 왼쪽 위의 [버킷 추가]를 클릭합니다.
2. 팝업창에 버킷 정보를 입력합니다.
 - 이름: 사용자 정의 버킷 이름, examplebucket을 입력합니다.
 - 리전: 버킷 소속 리전, 본인과 가장 근접한 지역을 선택합니다. 예를 들어 ‘선전’에 있는 경우, 리전을 ‘광저우’로 선택합니다.
 - 액세스 권한: 버킷 액세스 권한, ‘개인 읽기 및 쓰기’를 선택합니다.
![](https://main.qcloudimg.com/raw/d5c11a8be17d9a3462c0ca73ee189c73.png)
3. [확인]을 클릭하면 버킷이 생성됩니다.


## 4단계: 객체 업로드하기

1. 3단계에서 생성한 버킷을 클릭하여 버킷 관리 페이지로 이동합니다.
2. [업로드]>[파일 선택]을 선택하여 exampleobjext.txt와 같이 버킷에 업로드할 로컬 파일을 선택합니다.
3. [업로드]를 클릭하면 exampleobjext.txt를 버킷에 업로드할 수 있습니다.


## 5단계: 객체 다운로드하기



#### 방법1


1. COSBrowser 툴 오른쪽 상단의 <img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;">를 클릭하면 리스트 뷰로 전환됩니다. 리스트 뷰 화면에서는 이 절차를 생략해도 됩니다.
2. 파일 오른쪽 작업 열의 <img src="https://main.qcloudimg.com/raw/0631f784902fb5e146ac0d0f6befe346.jpg"  style="margin:0;">를 클릭하여 파일을 다운로드합니다.


#### 방법2

1. 마우스 오른쪽 버튼으로 파일 클릭 후, 드롭다운 메뉴에서 [고급 다운로드]를 클릭합니다.
2. COSBrowser 툴의 고급 다운로드 팝업창에서 필요에 따라 ‘이름 변경’, ‘덮어쓰기’ 또는 ‘건너뛰기’를 선택합니다.
![](https://main.qcloudimg.com/raw/6e533ea1b75df3de7dba029a6976f844.png)
3. [다운로드]를 클릭하면 선택한 파일이 다운로드됩니다.


## 6단계: 객체 공유하기

COS에 저장된 모든 파일은 관련 링크를 통해 액세스할 수 있습니다. 파일이 개인 읽기 권한이라면 임시 서명을 요청하여 유효 시간이 부여된 임시 액세스 링크를 생성할 수 있습니다. 객체의 링크 생성 방법은 다음과 같은 두 가지입니다.

#### 방법1

1. COSBrowser 툴 오른쪽 상단의 <img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;">를 클릭하면 리스트 뷰로 전환됩니다. 리스트 뷰 화면에서는 이 절차를 생략해도 됩니다.
2. 파일 오른쪽 작업 열의 <img src="https://main.qcloudimg.com/raw/37acaeb370eb77e1bb0c792d542792e2.jpg"  style="margin:0;">를 클릭합니다.
3. COSBrowser 툴 상단에 [임시 링크 복사 완료, 유효 시간 2시간]이라고 표시되면, 링크 생성 및 복사가 완료되었음을 의미합니다.
4. 해당 링크로 파일을 액세스합니다. 해당 방법으로 생성된 파일 링크의 유효 시간은 2시간이며, 유효 시간을 직접 입력할 경우, 방법2를 참조하십시오.


#### 방법2

1. COSBrowser 툴 오른쪽 상단의 <img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;">를 클릭하면 리스트 뷰로 전환됩니다. 리스트 뷰 화면에서는 이 절차를 생략해도 됩니다.
1. 파일 오른쪽 작업 열에서 [**...**]를 클릭한 뒤, 드롭다운 메뉴의 [공유]를 클릭합니다.
![](https://main.qcloudimg.com/raw/1ab8d2c4a61ae3e0b94c06c9d65ce3f7.png)
2. 사용자 정의 복사 링크 팝업창에서 파일 링크를 설정합니다. 파일이 개인 읽기 및 쓰기 권한이라면 [서명을 보유한 임시 링크 복사….]를 선택합니다. 링크는 설정한 시간에 한해 유효합니다.
![](https://main.qcloudimg.com/raw/1d4b5c7f047c2ecfa8fb182a9daed1d2.png)
3. [복사]를 클릭하여 임시 파일 링크를 복사하면 해당 링크를 통해 파일에 액세스할 수 있습니다.



## 추가 기능

COSBrowser는 위 기능 외에도 버킷 액세스 권한 수정, 파일 미리보기 등 많은 기능을 보유하고 있습니다. 자세한 사항은 [데스크톱 기능 리스트](https://intl.cloud.tencent.com/document/product/436/11366#.E6.A1.8C.E9.9D.A2.E7.AB.AF.E5.8A.9F.E8.83.BD.E5.88.97.E8.A1.A8) 문서를 참조하십시오.


## 문제 해결

사용 시 문제가 발생할 경우, [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 문의하시기 바랍니다.

## 관련 문서

모바일 (iOS, Android)의 COSBrowser, 다음 문서를 참조하십시오.

- [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)
- 모바일 사용 설명
