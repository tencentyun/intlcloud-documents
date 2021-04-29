

## 설정 시나리오
Tencent Cloud CDN은 리소스 콘텐츠 외에, 다음과 같은 원본 서버 헤더를 캐싱하고 사용자에게 반환하도록 기본 설정되어 있습니다,
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

사용자의 원본 서버에 특수 헤더가 있어 CDN이 이를 캐싱하고 사용자에게 반환해야 하는 경우, 헤더 캐시 설정을 활성합니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [도메인 관리]를 선택하고 도메인 오른쪽의 [관리]를 클릭하면 도메인 설정 페이지로 이동할 수 있으며, 세 번째 탭인 [캐시 설정]에서 HTTP 헤더의 캐시 설정을 확인할 수 있습니다. 기본적으로 활성화 상태로 설정되어 있으며 사용자의 필요에 따라 비활성화로 변경할 수 있습니다.
![](https://main.qcloudimg.com/raw/0fb4739f743b6242c463672a2f059098.png)
