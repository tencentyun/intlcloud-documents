## 작업 시나리오
실제 필요에 따라 콜백 모드를 설정할 수 있습니다. 비디오 처리가 완료된 후 시스템은 처리 결과 및 상태를 지정된 모드를 통해 지정된 주소로 제출합니다. 콜백 모드에는 다음이 포함됩니다.
- 일반 콜백: 사용자 정의 콜백 URL 설정을 지원합니다. 이벤트 완료 후 시스템은 알림 내용이 포함된 이 URL로 HTTP 요청을 보냅니다.
- 안정적인 콜백: 이벤트가 완료된 후 VOD 시스템은 알림을 내장된 메시지 대기열에 넣고 App 서버는 서버 API를 통해 대기열의 알림을 가져와 사용합니다. 이벤트 알림 신뢰도에 대한 요구 사항이 높은 경우 이 모드를 사용하는 것이 좋습니다.



## 작업 단계

1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하고 왼쪽 사이드바에서 [콜백 설정]을 클릭하여 ‘콜백 설정’ 페이지로 들어갑니다.
2. [설정]을 클릭하여 콜백을 설정합니다.
![](https://main.qcloudimg.com/raw/cb7e3f9fec12cb8bf5bd5070d63fe24e.png)
3. 실제 필요에 따라 다음 매개변수를 구성합니다.
 - 콜백 모드: 일반 콜백 또는 안정적인 콜백을 선택합니다.
 - 콜백 URL: 이 매개변수는 콜백 모드가 [일반 콜백]으로 설정된 경우에만 표시됩니다. 실제 필요에 따라 App 백엔드의 콜백 수신 주소를 설정하십시오.
 - 콜백 이벤트: 비디오 업로드 완료, 태스크 플로우 상태 변경, 트랜스코딩, 스프라이트 이미지 생성, 스티칭, 삭제, 편집, 시점 화면 캡처 및 클리핑 등 콜백 수신 대상 이벤트를 선택합니다.
 >
 >- 그 중 태스크 플로우 상태 변경, 비디오 편집 완료, 비디오 자르기 완료는 기본 콜백 이벤트입니다.
 >- 원하는 콜백 이벤트 우측의 <img src="https://main.qcloudimg.com/raw/a710a753ba2162f8913e180be4c93269.png"/>을(를) 클릭하면 해당 문서를 볼 수 있습니다.
