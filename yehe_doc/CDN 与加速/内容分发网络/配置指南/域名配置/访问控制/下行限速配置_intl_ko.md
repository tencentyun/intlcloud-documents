
## 설정 시나리오

Tencent Cloud CDN은 다운스트림 속도 제한 설정을 제공하며, 서버의 단일 링크 다운스트림의 최대 처리량 속도를 설정합니다.
다운스트림 속도 제한 설정을 통해 CDN 피크 대역폭을 일정 부분 제어할 수 있으며, 전자상거래, 게임 업데이트 배포 등 시나리오에서 주로 사용됩니다.

>! 다운스트림 속도 제한을 설정하면 사용자 액세스 및 CDN 가속 효과에 어느 정도 영향을 주므로 사용 시 주의해야 합니다.

## 설정 가이드

### 설정 제한

- 다운스트림 속도 제한 규칙은 최대 10개까지 설정할 수 있습니다.
- 속도 제한 단위는 KB/s, 자연수로 입력하며 값의 범위 구간은 1~1000000입니다.
- 적용 유형은 모든 파일, 파일 유형, 파일 디렉터리, 지정 파일 경로의 4가지 모드를 지원하며, 정규식 매칭은 지원하지 않습니다.
- 다수 규칙의 우선순위는 위에서 아래로 높아지며, 제일 아래쪽의 우선순위가 제일 위쪽보다 높습니다.

### 설정 설명

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [Domain Management]를 선택하고, 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지로 이동합니다. 두 번째 탭인 [Access Control]에 다운스트림 속도 제한 설정이 존재하며 기본값은 비활성화 상태입니다.
![](https://main.qcloudimg.com/raw/c9ea85be753b60096b8088b048ac626a.png)
[속도 제한 규칙 추가]를 클릭해 규칙을 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/02e033c829da553acc5eeb9bca864528.png)
규칙 추가가 완료되면 전체 설정이 비활성화 상태로 되어, 현재 네트워크 서비스에 영향을 미치지 않습니다.
![](https://main.qcloudimg.com/raw/e0006ace8527cc13c381666b22f21790.png)
[ON] 버튼을 클릭해 설정한 속도 제한 규칙을 CDN 전체 네트워크 노드에 배포할 수 있습니다.
![](https://main.qcloudimg.com/raw/4b9685cb889210accb67d11f1b389ae8.png)

## 설정 예시

가속 도메인이 `cloud.tencent.com`인 다운스트림 속도 제한 설정은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/7ee9a5167aa054c8e99c15267e38eba3.png)
사용자 액세스 리소스가 `http://cloud.tencent.com/test.mp4`인 경우 서버에서 다운스트림 속도 200KB/s로 응답합니다.
사용자 액세스 리소스가 `http://cloud.tencent.com/test.flv`인 경우 서버에서 다운스트림 속도 400KB/s로 응답합니다.
