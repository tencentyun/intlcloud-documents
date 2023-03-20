
COSBrowser는 Tencent Cloud COS(Cloud Object Storage)에서 시작한 시각적 인터페이스 툴로 COS 리소스를 보다 쉽고 간단하게 보고, 전송하고, 관리하고, 상호 작용할 수 있습니다. 현재 데스크톱 및 모바일 클라이언트에서 사용할 수 있습니다. 자세한 내용은 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)를 참고하십시오.

본문은 COSBrowser를 사용하여 빠르게 버킷을 생성하고 객체를 업로드, 다운로드 및 공유하는 방법을 설명합니다.


## 전제 조건

1. Tencent Cloud 계정에서 COS를 활성화합니다.
>?
>- Tencent Cloud 계정이 없다면 [About Account](https://www.tencentcloud.com/document/product/378)의 안내에 따라 생성하십시오.
>- COS를 활성화하지 않은 경우 [COS 콘솔](https://console.cloud.tencent.com/cos5)로 이동하여 메시지에 따라 활성화합니다.
2. COS를 처음 사용하는 경우 다음의 기본 개념을 먼저 숙지하시기 바랍니다.
 - [버킷(Bucket)](https://intl.cloud.tencent.com/document/product/436/13312): 객체 저장 수단으로 객체를 저장하는 '컨테이너'의 기능을 하며, 하나의 버킷에는 무수한 객체를 저장할 수 있습니다.
 - [객체(Object)](https://intl.cloud.tencent.com/document/product/436/13324): COS의 기본 단위로 이미지, 문서, 멀티미디어 파일 등 다양한 포맷의 데이터를 의미합니다.
 - [리전(Region)](https://intl.cloud.tencent.com/document/product/436/6224): Tencent Cloud의 호스팅 데이터 센터가 분포된 지역으로 COS 데이터를 리전의 버킷에 저장합니다.


## 1단계: COSBrowser 다운로드 및 설치하기


1. Windows용 COSBrowser 예로 듭니다. 클릭하여 [COSBrowser](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe)를 다운로드합니다.
2. 다운로드 후 메시지에 따라 설치할 설치 패키지를 더블클릭합니다.


>?
>- Windows용 COSBrowser의 시스템 요구 사항: Windows 7 32/64비트 이상, Windows Server 2008 R2 64비트 이상.
>- [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)에서 다른 운영 체제용 COSBrowser를 다운로드할 수 있습니다.



## 2단계: COSBrowser 로그인하기

Windows용 COSBrowser는 API Keys, Tencent Cloud 계정 및 공유 링크를 통한 로그인을 포함하여 여러 로그인 방법을 지원합니다. 아래는 Tencent Cloud 계정을 예로 들어 설명합니다.


## 3단계: 버킷 생성하기

1. 로그인한 후 COSBrowser 페이지의 왼쪽 상단 모서리에 있는 **버킷 생성**을 클릭합니다.
2. 팝업창에 버킷 정보를 입력합니다.
![](https://main.qcloudimg.com/raw/d5c11a8be17d9a3462c0ca73ee189c73.png)
 - 버킷 이름: 사용자 정의 버킷 이름, examplebucket을 입력합니다.
 - 리전: 버킷이 속한 리전을 말하며, 가장 가까운 지역을 선택합니다. 예를 들어 선전에 있는 경우 리전으로 광저우, 즉 ap-guangzhou를 선택할 수 있습니다. 
 - 액세스 권한: 버킷 액세스 권한, ‘개인 읽기 및 쓰기’를 선택합니다.
 - 버킷 태그/MAZ 구성은 선택 사항입니다. 본 예시에서는 무시합니다.
3. **확인**을 클릭합니다. 버킷 리스트에서 생성된 버킷을 확인할 수 있습니다.


## 4단계: 객체 업로드하기

1. 새로 생성된 버킷을 클릭하여 버킷 관리 페이지로 이동합니다.
2. **업로드 > 파일 선택**을 클릭하고 버킷에 업로드할 로컬 파일(예: exampleobject.txt)을 선택합니다.
3. **업로드**를 클릭하면 exampleobject.txt를 버킷에 업로드할 수 있습니다.


## 5단계: 객체 다운로드하기

대상 파일을 우클릭하고 **다운로드**를 클릭합니다.

## 6단계: 객체 공유하기

COSBrowser를 사용하면 URL 또는 QR 코드를 통해 파일을 공유할 수 있습니다. 아래는 URL을 예로 들어 설명합니다.

1. 대상 파일을 선택하고 우측의 <img src="https://main.qcloudimg.com/raw/37acaeb370eb77e1bb0c792d542792e2.jpg"  style="margin:0;">을(를) 클릭하면 공유 URL이 빠르게 생성됩니다.
>?파일이 버킷의 개인 읽기/쓰기 권한을 상속하므로 생성된 공유 URL은 임시이며 2시간 동안만 유효합니다.
2. 생성된 URL을 수신자에게 전송합니다. 그러면 수신자가 온라인으로 파일에 액세스하거나 다운로드할 수 있습니다.
>?
>기본적으로 공유 파일을 브라우저에서 직접 열 수 있는 경우 임시 URL에 액세스하면 파일을 다운로드하지 않고 온라인에서 직접 미리 볼 수 있습니다.


## 추가 기능

COSBrowser는 위 기능 외에도 버킷 액세스 권한 수정, 파일 미리보기 등 많은 기능을 보유하고 있습니다. 자세한 사항은 [데스크톱 기능 리스트](https://intl.cloud.tencent.com/document/product/436/11366#.E6.A1.8C.E9.9D.A2.E7.AB.AF.E5.8A.9F.E8.83.BD.E5.88.97.E8.A1.A8) 문서를 참고하십시오.

## 질문이 있으십니까?

사용 과정 중 문제가 발생한 경우 [FAQ](https://intl.cloud.tencent.com/document/product/436/35735)를 참고하거나 [문의하기](https://intl.cloud.tencent.com/contact-sales)를 통해 지원을 요청해 주시기 바랍니다.

## 관련 문서

모바일(iOS, Android) 기반 COSBrowser에 대한 자세한 내용은 다음 문서를 참고하십시오.

- [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)
- [모바일 버전 기능](https://intl.cloud.tencent.com/document/product/436/41616)
