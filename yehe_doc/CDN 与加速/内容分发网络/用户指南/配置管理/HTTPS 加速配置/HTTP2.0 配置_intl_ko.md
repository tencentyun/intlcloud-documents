## 설정 시나리오
이미 인증서가 설정되어 HTTPS 가속이 활성화된 도메인은 HTTP2.0 프로토콜 지원을 자체 활성화할 수 있습니다.
>현재는 HTTP2.0 액세스만 지원하고 HTTP2.0 프로토콜 원본 요청은 지원하지 않습니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [Domain Management]를 선택하고 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지의 마지막 탭인 [Advanced Configuration]에서 [HTTP2.0 Configurations]을 확인할 수 있으며 기본적으로 활성화 상태입니다:
![](https://main.qcloudimg.com/raw/6baf0831d42acad8b8ab1a0c705805bf.png)

### 설정 수정
on-off 스위치를 클릭하여 HTTP2.0 설정을 활성화 또는 비활성화할 수 있으며 인증서 설정을 삭제하면 HTTP2.0 설정이 동기화되어 적용이 취소됩니다.
![](https://main.qcloudimg.com/raw/f26532a1f9ebbe14633b9726b0ed58de.png)

>도메인의 서비스 지역이 글로벌인 경우, HTTP2.0 설정은 글로벌 범위에 적용되며 중국 내, 중국 외를 다르게 설정할 수 없습니다.

