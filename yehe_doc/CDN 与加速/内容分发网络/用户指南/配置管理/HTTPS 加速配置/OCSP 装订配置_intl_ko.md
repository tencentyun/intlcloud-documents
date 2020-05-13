## 설정 시나리오
OCSP Stapling 을 활성화하여 서버가 TLS 핸드셰이킹 시 이미 캐싱한 OCSP 쿼리 결과를 클라이언트에 전송함으로써, 클라이언트에서 CA로 요청을 보내지 않아도 인증할 수 있습니다. OCSP 고정을 통해 TLS 핸드셰이킹의 효율을 크게 향상하고, 사용자의 인증 시간을 단축할 수 있습니다.

Tencent Cloud CDN은 OCSP Stapling 설정을 자체 활성화 또는 비활성화할 수 있습니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [Domain Management]를 선택하고 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지의 마지막 탭인 [Advanced Configuration]에서 [Stapling Configuration]을 확인할 수 있으며 비활성화 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/063f1f4f85850f9faafdea14a2507711.png)

### 설정 수정
HTTPS 가속 도메인을 설정하면 직접 on-off 스위치를 클릭하여 OCSP 고정 설정을 활성화 또는 비활성화할 수 있으며 인증서 설정을 삭제하면 OCSP 고정 설정이 동기화되어 적용이 취소됩니다.
![](https://main.qcloudimg.com/raw/73f0f5763dfc99956272f846aed079a4.png)

>도메인의 서비스 지역이 글로벌인 경우, OCSP 고정 설정은 글로벌 범위에 적용되며 중국 내, 중국 외를 다르게 설정할 수 없습니다.

