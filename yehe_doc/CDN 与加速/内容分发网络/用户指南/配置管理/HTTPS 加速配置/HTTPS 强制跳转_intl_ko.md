## 설정 시나리오
Tencent Cloud CDN은 HTTPS 강제  리디렉션을 지원합니다. 이미 인증서를 설정하여 HTTPS 가속을 진행 중인 도메인은 301/302 리디렉션 방식을 지정하여 CDN 노드에 도달하는 모든 HTTP 요청을 HTTPS로 강제 리디렉션할 수 있습니다.
## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [Domain Management] 선택하고 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지의 마지막 탭인 [Advanced Configuration]에서 이미 HTTPS 인증서가 설정되어 있는 도메인과 [강제 리디렉션] on-off 스위치를 확인할 수 있습니다. 강제 리디렉션은 비활성화 상태로 기본 설정되어 있습니다:
![](https://main.qcloudimg.com/raw/3a60e71f17f830bf4ae4d00d4efd1124.png)
### 설정 수정
오른쪽 [Edit]을 클릭하여 301/302 리디렉션 전환을 할 수 있고 직접 on-off 스위치를 통해서도 설정을 비활성화할 수 있습니다.
![](https://main.qcloudimg.com/raw/f0b2fab0919635c6ba3c4784083cf942.png)
![](https://main.qcloudimg.com/raw/ba7f5a597ae182e019cb13704fbad9ef.png)

>도메인의 서비스 지역이 글로벌일 경우, HTTPS 강제 리디렉션 설정이 글로벌 범위에 적용되며 중국 내, 중국 외를 다르게 설정할 수 없습니다.
