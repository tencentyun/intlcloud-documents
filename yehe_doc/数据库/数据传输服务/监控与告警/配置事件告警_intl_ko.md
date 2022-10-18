## 작업 시나리오
DTS는 EventBridge를 사용하여 데이터 마이그레이션, 동기화 및 구독 작업 중 이벤트를 모니터링하고 알람 규칙을 설정할 수 있습니다. EventBridge는 이벤트가 트리거되는 즉시 알림을 보내 조치를 취할 수 있도록 합니다. 

본문에서는 이벤트 알람의 범위, 알림 형식, 알림 기간, 수신자 그룹 등 이벤트 알람에 대한 알림 규칙을 설정하는 방법에 대해 설명합니다. 

## 작업 단계
1. [EventBridge 콘솔](https://console.cloud.tencent.com/eb)에 로그인합니다.
2. 최초 로그인 시 [Activating EventBridge](https://intl.cloud.tencent.com/document/product/1108/42272)의 안내에 따라 시스템에서 서비스 인증을 요청합니다. 이미 승인한 경우 이 단계를 건너뜁니다.
3. 왼쪽 사이드바에서 **이벤트 규칙**을 선택하고 **광저우** 리전 및 **default** 이벤트 버스를 선택한 다음 **이벤트 규칙 생성**을 클릭합니다.
Tencent Cloud 서비스의 이벤트 버스는 기본적으로 모두 광저우에 저장되어 있으므로 여기에서 리전 및 이벤트 버스에 대한 다른 옵션을 선택할 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/01bd03e8bdad4b11276e2a8fdfa516a9.png)
4. 이벤트 규칙을 구성하고 **다음**을 클릭합니다.
 - **NewDTS(데이터 마이그레이션/동기화/구독 (Kafka Edition))**
    ![](https://qcloudimg.tencent-cloud.cn/raw/5feb1408d29bc9c825423fd77449a30d.png)
 - **이전 DTS(데이터 구독만 해당)**
    ![](https://qcloudimg.tencent-cloud.cn/raw/29819a0c4d5a00137927c171c49ab374.png)
<table>
<thead><tr><th>매개변수</th><th>설명</th></tr></thead>
<tbody><tr>
<td>규칙 이름</td>
<td>서비스를 구분하기 위한 규칙 이름을 입력하십시오. 이는 한 번 구성되면 수정할 수 없습니다.</td></tr>
<tr>
<td>규칙 패턴</td>
<td><strong>기본값</strong>을 선택합니다.</td></tr>
<tr>
<td>Tencent Cloud 서비스</td>
<td><ul><li>NewDTS 작업(마이그레이션/동기화/구독(Kafka Edition))의 경우 <strong>데이터 전송 서비스(DTS)</strong>를 선택합니다. </li><li>이전 DTS 작업(구독만 해당)의 경우 <strong>DTS 데이터 구독</strong>을 선택합니다.</li></ul></td></tr>
<tr>
<td>이벤트 유형</td>
<td><ul><li>NewDTS 작업(마이그레이션/동기화/구독(Kafka Edition))의 경우 <strong>데이터 마이그레이션 작업 중단</strong>, <strong>데이터 동기화 작업 중단</strong> 및 <strong>데이터 구독 작업 중단</strong>을 선택하십시오. </li><li>이전 DTS 작업(구독만 해당)의 경우 <strong>모든 이벤트</strong>가 기본적으로 선택됩니다.</li></ul></td></tr>
</tbody></table>
5. 알림 방식, 수신자, 전달 방식을 설정하고 트리거 방식에서 **메시지 푸시**를 선택한 후 **완료**를 클릭합니다.
새로운 수신자 사용자/사용자 그룹을 추가하려면 생성을 위해 [CAM](https://console.cloud.tencent.com/cam) 콘솔로 이동한 후 이 단계의 **수신자**에서 선택합니다.
다른 트리거 방법을 구성하려면 하단의 **추가**를 클릭하여 더 많은 딜리버리 타깃을 추가합니다.
6. 이벤트 규칙 목록으로 돌아가 생성된 이벤트 규칙이 활성화되었는지 확인합니다. 그 후 작업 예외가 경보를 트리거하면 구성된 수신자가 메시지 알림을 수신합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/cda96cd6cc44dbd7c139bab1a13e0972.png)

