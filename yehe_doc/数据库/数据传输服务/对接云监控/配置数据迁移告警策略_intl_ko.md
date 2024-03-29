## 작업 시나리오
CM을 사용하여 데이터 마이그레이션 중 중요한 지표 및 이벤트에 대한 알람 규칙을 설정할 수 있습니다. 메트릭이 예외적이거나 이벤트가 발생하면 CM에서 즉시 공지를 보내 적절한 조치를 취할 수 있습니다. 

DTS는 일부 중요한 이벤트에 대한 기본 알람 설정을 지원합니다. 즉, 사용자가 옵션을 설정하지 않고도 작업이 시작될 때 이벤트를 자동으로 모니터링하고 트리거된 이벤트를 알려줍니다. 현재 이 기능은 ‘데이터 마이그레이션 작업 중단’ 이벤트에 대해 지원됩니다.

## 알람 정책 추가
1. [CM 콘솔](https://console.cloud.tencent.com/monitor)에 로그인합니다.
2. **알람 설정** > **알람 정책**을 클릭하여 알람 정책 설정 페이지로 들어갑니다.
3. **추가**를 클릭하고 아래와 같이 새 알람 정책을 설정합니다.
<table>
<tr><th width="10%">설정 유형</th><th width="15%">설정 항목</th><th width="80%">설명</th></tr>
<tr>
<td  rowspan="4">기본 정보</td>
<td>정책 이름</td><td>사용자 정의 정책 이름.</td></tr>
<tr>
<td>비고</td><td>사용자 정의 정책 설명.</td></tr>
<tr>
<td>모니터링 유형</td><td>클라우드 제품 모니터링.</td></tr>
<tr>
<td>정책 유형</td>
<td>모니터링할 Tencent Cloud 서비스의 원하는 정책 유형을 선택합니다. 여기에서는 <strong>DTS/데이터 마이그레이션</strong>을 선택합니다.
<ul>
<li>데이터 마이그레이션: 데이터 마이그레이션 시나리오의 메트릭 및 이벤트가 모니터링됩니다.</li>
<li>데이터 동기화: 데이터 동기화 시나리오의 메트릭 및 이벤트가 모니터링됩니다.</li>
<li>데이터 구독(Kafka 버전): 새 DTS에서 데이터 구독(Kafka 버전)의 메트릭 및 이벤트가 모니터링됩니다.</li>
<li>데이터 구독: 이전 DTS에서 데이터 구독의 메트릭 및 이벤트가 모니터링됩니다.</li></ul></td></tr>
<tr>
<td rowspan="4">알람 정책</td>
<td>알람 객체</td>
<td>
<ul>
<li>인스턴스 ID를 선택하면 사용자가 선택한 인스턴스에 알람 정책이 바인딩됩니다.</li>
<li>인스턴스 그룹을 선택하면 사용자가 선택한 인스턴스 그룹에 알람 정책이 바인딩됩니다.</li>
<li>전체 객체를 선택하면 해당 알람 정책은 현재 계정이 권한을 가진 모든 인스턴스를 바인딩합니다.</li></ul></td>
<tr>
<td>수동 설정<br>(지표 알람)</td>
<td>
<ul>
<li>알람 트리거 조건: 일부<strong> 또는 </strong>모든<strong> 메트릭이</strong> 설정된 조건을 충족할 때 알람을 트리거하도록 선택할 수 있습니다. <ul><li>설정 예시: 메트릭은 ‘원본 데이터베이스에서 읽은 RPS’, 통계 기간은 1분, 비교 관계는 ‘보다 작음’, 임계값은 ‘1’, 연속 모니터링 기간은 ‘3개의 연속 데이터 포인트’입니다.</li>
<li>설정 효과: ‘원본 데이터베이스에서 읽은 RPS’ 메트릭은 1분에 한 번 수집됩니다. DTS가 초당 원본 데이터베이스에서 읽은 행 수가 3회 연속 1 미만이면 알람이 트리거됩니다.</li></ul></li>
<li>알람 빈도: 반복되는 공지 알람의 빈도를 매시간, 2시간, 1일……과 같이 사용자 정의할 수 있습니다.</li></ul></td></tr>
<tr>
<td>수동 설정<br>(이벤트 알람)</td>
<td>모니터링할 이벤트를 선택합니다. ‘데이터 마이그레이션 작업 중단’ 이벤트는 기본적으로 시스템에 이미 설정되어 있습니다.</td></tr>
<tr>
<td>템플릿 선택</td>
<td> 템플릿 선택을 클릭하고 드롭다운 리스트에서 설정된 템플릿을 선택합니다. 자세한 설정은 <a href="https://intl.cloud.tencent.com/document/product/248/38911">트리거 조건 템플릿 설정</a>을 참고하십시오. 새로 생성된 템플릿이 표시되지 않으면 오른쪽의 <strong>새로고침<strong>을 클릭하십시오.</td></tr>
<tr>
<td>알람 공지 설정</td>
<td>공지 템플릿</td>
<td>시스템 사전 설정 공지 템플릿과 사용자 정의 공지 템플릿 선택을 지원합니다. 각 알람 정책은 최대 3개의 공지 템플릿만 바인딩할 수 있습니다.</li></td></tr>
<tr>
<td>고급 설정</td>
<td >Auto Scaling</td>
<td>활성화 및 설정 완료 후 알람 조건에 부합하면 Auto Scaling 정책이 트리거되어 스케일 다운 또는 확장이 가능합니다.</td></tr>
</table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/eb85779c0a56fe502e79de7218927a06.png" alt="">
4. 상기 정보를 설정한 후 **저장**을 클릭합니다.

## 알람 정책 수정
1. [CM 콘솔](https://console.cloud.tencent.com/monitor)에 로그인합니다.
2. **알람 설정** > **알람 정책**을 클릭하고 수정할 정책의 이름/ID를 클릭하면 알람 정책 관리 페이지로 진입합니다.
3. 트리거 조건, 알람 객체, 알람 공지 등의 정보를 수정합니다.
