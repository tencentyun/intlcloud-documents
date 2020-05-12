
## 설정 시나리오
Tencent Cloud CDN은 리소스 콘텐츠 외에, 다음 원본 서버의 헤더를 캐싱하고 사용자에게 리턴하도록 기본 설정되어 있습니다.
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

사용자의 원본 서버에 특수 헤더가 있으면 CDN이 이를 캐싱하고 사용자에게 리턴해야 하므로, 헤더 캐시 설정 활성화를 통해 이를 구현할 수 있습니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [Domain Management]를 선택하고 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지로 이동할 수 있습니다. 그중 세 번째 탭인 [Cache Configuration]에서 HTTP 헤더의 캐시 설정을 확인할 수 있으며 비활성화 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/c2a5552633d1b0bb5313a53c493459c7.png)

### 설정 수정
on-off 스위치를 클릭하여 HTTP 헤더 캐시 설정을 즉시 활성화 또는 비활성화할 수 있고, 설정이 전체 네트워크에 전달 및 적용되는 데까지 약 5분 정도 소요됩니다.
![](https://main.qcloudimg.com/raw/e17df48d27afd9fd4d49ec4168ca0a39.png)

>
> + 사용자의 가속 도메인 서비스 지역이 글로벌 가속이면 설정한 매개변수 캐시 설정이 글로벌 범위에 적용되며 중국 내, 중국 외를 다르게 설정할 수 없습니다.
> + 헤더의 캐시 설정은 전체 네트워크 업그레이드 중으로, 비활성화 클릭 시 오류 알림이 뜨면 업그레이드로 인한 것이니 [고객센터](https://cloud.tencent.com/act/event/connect-service)를 통해 백그라운드 설정을 비활성화할 수 있습니다.





