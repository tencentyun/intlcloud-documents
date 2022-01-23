VOD의 동영상에 대한 업로드, 삭제, 동영상 처리 등의 작업을 이벤트라고 할 수 있습니다. 이벤트 실행에는 일정 시간이 소요됩니다. 이벤트가 완료되면 VOD는 즉시 애플리케이션 서비스에 실행 결과를 알립니다. 즉, 이벤트 알림을 보냅니다.

VOD는 다음 유형의 이벤트 알림을 지원합니다.

<table>
    <tr>
        <th style="width:30%">
            분류
        </th>
        <th style="width:70%">
            이벤트 알림
        </th>
    </tr>
    <tr>
        <td rowspan=3>
            업로드 및 삭제
        </td>
        <td>
				    <a href="https://intl.cloud.tencent.com/document/product/266/33950">비디오 업로드 완료</a>
        </td>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33951">URL에서 비디오 가져오기 완료</a>
        </td>
    </tr>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33952">비디오 삭제 완료</a>
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            비디오 처리
        </td>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33953">태스크 플로우 상태 변경</a>
        </td>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33954">동영상 편집 완료</a>
        </td>
    </tr>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/35571">동영상 합성 완료</a>
        </td>
    </tr>
</table>

이벤트 알림 모드에는 ‘일반 콜백’ 및 ‘신뢰할 수 있는 콜백’이 있습니다. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하여 콜백 모드를 설정하고 콜백을 수신할 이벤트를 선택할 수 있습니다. 자세한 내용은 [콜백 설정](https://intl.cloud.tencent.com/document/product/266/14055)을 참고하십시오.

- 일반 콜백: 콘솔에서 콜백 URL을 구성합니다. 이벤트가 완료된 후 시스템은 알림 콘텐츠가 포함된 이 URL로 HTTP 요청을 보냅니다.
- 신뢰할 수 있는 콜백: 이벤트가 완료된 후 VOD 시스템은 알림을 내장된 메시지 대기열에 넣고, 애플리케이션 서비스는 서버 API를 통해 대기열의 알림을 소비합니다.



## 일반 콜백

일반 콜백은 App 서비스가 이벤트 알림을 수동적으로 수신하는 모드입니다. 콜백 URL이 설정되고 일반 콜백 모드가 선택되면 VOD는 이벤트가 완료된 후 콜백 URL에 대한 콜백을 시작합니다.

VOD에 의해 시작된 일반 콜백은 HTTP 요청으로, 요청 본문은 JSON 형식이고 콘텐츠는 EventHandle 매개변수를 제외한 [EventContent 구조](https://intl.cloud.tencent.com/document/product/266/34187#EventContent)입니다.
[작업 상태 변경 알림](https://intl.cloud.tencent.com/document/product/266/33953)을 예로 들어 보겠습니다. 콜백의 `EventType` 매개변수는 `ProcedureStateChanged`이며 정보는 `ProcedureStateChangeEvent` 매개변수([ProcedureTask](https://intl.cloud.tencent.com/document/product/266/34187#ProcedureTask) 구조)로 표시됩니다.

## 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백은 App 서비스가 이벤트 알림을 VOD로 능동적으로 가져오는 모드입니다. 신뢰할 수 있는 콜백 모드가 선택되면 VOD 시스템은 이벤트 알림을 대기열에 넣고, App 서비스는 서버 API를 통해 대기열의 알림을 소비합니다.
App 서비스가 [Pull Events](https://intl.cloud.tencent.com/document/product/266/34183) API를 통해 메시지를 받은 후 확인을 위해 [Confirm Events](https://intl.cloud.tencent.com/document/product/266/34184) API를 호출해야 합니다. 메시지는 VOD 대기열에서 제거되기 전에 수신 확인을 거쳐야 하므로 ‘일반 콜백’보다 ‘신뢰할 수 있는 콜백’의 신뢰도가 높습니다. **이벤트 알림 신뢰도에 대한 요구 사항이 높은 경우 ‘신뢰할 수 있는 콜백’ 모드를 사용하는 것이 좋습니다**.
