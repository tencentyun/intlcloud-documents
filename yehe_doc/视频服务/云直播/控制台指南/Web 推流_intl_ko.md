## 작업 시나리오
Tencent Cloud는 Web 푸시 스트리밍 기능을 제공하여 빠르게 푸시 스트리밍 주소를 생성할 수 있으며, 온라인 푸시 스트리밍 라이브 방송 테스트 기능을 제공합니다.

## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
- [푸시 스트리밍 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.
- 디바이스에 카메라가 설치되어 있어야 하며 브라우저에서 Flash 플러그 인의 카메라 호출 권한을 지원해야 합니다.

## 작업 순서
1. CSS 콘솔에 로그인하여 [Web Push](https://console.cloud.tencent.com/live/tools/webpush)를 선택합니다.
2. Web 푸시 스트리밍 페이지에서 다음을 설정합니다.
	- 푸시 스트리밍 도메인을 선택합니다.
	- 사용자 정의 스트림 이름 StreamName을 입력합니다. (예시: `test`)
	- 만료 시간을 선택합니다. (예시: `2020-04-13 23:59:59`)
	- AppName을 편집합니다. 한 도메인에 여러 개의 App 주소 경로를 구분하는 데 사용되며, 기본값은 live로 설정되어 있습니다.
3. [Start Push]를 선택하고 카메라 호출 권한을 허용하면 푸시 스트리밍을 시작할 수 있습니다.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)
4. [Domain Management]에서 이미 재생 도메인을 추가한 경우 하단에서 이미 생성한 재생 주소를 확인할 수 있으며, 재생 주소는 다음과 같이 네 부분으로 구성됩니다.
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
RTMP, FLV, HLS 프로토콜을 지원하며, 재생 주소 뒤에 있는 QR 코드를 클릭하면 라이트 버전 Demo QR 코드를 통해 재생 주소를 확인할 수 있습니다. 
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
