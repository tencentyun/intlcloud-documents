
## 작업 시나리오
주소 생성기를 통해 이미 추가한 푸시 스트리밍/재생 도메인을 빠르게 선택하고 해당 푸시 스트리밍/재생 주소를 생성할 수 있습니다.

## 전제 조건
[CSS 콘솔](https://console.cloud.tencent.com/live)의 [도메인 관리](https://intl.cloud.tencent.com/document/product/267/31056)에는 1개 이상의 사용 가능한 도메인이 있어야 합니다.

## 작업 순서
1. CSS 콘솔에 로그인하여 [CSS Toolkit]>[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택해 주소 생성기 페이지로 이동합니다.
3. 주소 생성기 페이지에서 다음과 같이 설정합니다.
	1. 생성 유형에서 **푸시 스트리밍 도메인** 또는 **재생 도메인**을 선택합니다.
	2. 도메인 관리에서 추가한 해당하는 도메인을 선택합니다.
	3. AppName은 한 도메인에 여러 개의 App 주소 경로를 구분하는 데 사용되며, 기본값은 live로 설정되어 있습니다.
> AppName은 사용자 정의 편집할 수 있으며, 영문 알파벳, 숫자, 부호만 지원됩니다.
	4. 사용자 정의 스트림 이름 StreamName을 작성합니다. (예시: `liveteststream`)
	5. 주소 만료 시간을 선택합니다. (예시: `2019-11-30 23:59:59`)
3. [Generator Address]을 클릭하면 도메인 주소가 생성됩니다.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

>
>- 생성되는 푸시 스트리밍/재생 주소는 다음과 같이 네 부분으로 구성됩니다.
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
>- 생성되는 재생 주소는 RTMP, FLV, HLS 프로토콜을 지원하며, 재생 주소 뒤에 있는 QR 코드를 클릭하면 라이트 버전 Demo QR 코드를 통해 재생 주소를 확인할 수 있습니다. 
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
