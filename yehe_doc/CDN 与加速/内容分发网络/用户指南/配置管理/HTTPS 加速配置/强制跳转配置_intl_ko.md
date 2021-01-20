## 설정 시나리오

Tencent Cloud CDN 서비스는 HTTPS/HTTP 강제 리디렉션의 설정을 지원합니다.

- 인증서를 구성한 후에 HTTPS 가속 실행하는 도메인은 301/302 리디렉션 방식을 지정하여 CDN 노드에 도달하는 모든 HTTP 요청을 HTTPS 요청으로 강제 리디렉션할 수 있습니다.
- 또한 301/302 리디렉션 방식을 지정하여 CDN 노드에 도달하는 모든 HTTPS 요청을 HTTP 요청으로 강제 리디렉션할 수 있습니다.
- 리디렉션 시 기본적으로 Response header를 부여하지 않습니다. 변경 가능합니다.

## 설정 가이드

### 설정 약관

HTTPS 강제 리디렉션을 설정하려면, 먼저 CDN에 HTTPS 가속을 활성화해야 합니다.

### 설정 설명

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 메뉴에서 [도메인 이름 관리]를 선택하고, 도메인 이름 우측의 [관리]를 클릭하면 [Https 설정]에서 [강제 리디렉션] 설정 스위치를 찾을 수 있습니다. 이 기능은 기본적으로 비활성화되어 있습니다.
<img src="https://main.qcloudimg.com/raw/b11157d848d39d4e4bba540598f35eba.png" style="width:700px"/>
클릭하고 활성화한 후에 리디렉션 타입, 리디렉션 방식 및 헤더 부여 여부를 설정할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/731d7bcb51286683d259691178bf2b39.png" style="width:450px"/>
확인을 클릭한 후 바로 사이트에 배포할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/2dcfbacf16b47fe600935f57aadd2e77.png" style="width:700px"/>

