## 작업 시나리오

마이그레이션, 동기화 또는 구독 작업을 생성한 후 지정된 ID가 있는 작업의 이벤트 알람 알림만 수신하고 다른 작업은 수신하지 않으려면 이 문서를 참고하여 구성할 수 있습니다. 

## 작업 단계

1. [EventBridge 콘솔](https://console.cloud.tencent.com/eb)에 로그인합니다.
2. 최초 로그인 시 [Activating EventBridge](https://intl.cloud.tencent.com/document/product/1108/42272)의 안내에 따라 시스템에서 서비스 인증을 요청합니다. 이미 승인한 경우 이 단계를 건너뜁니다.
3. 왼쪽 사이드바에서 **이벤트 규칙**을 선택하고 **광저우** 리전 및 **default** 이벤트 버스를 선택한 다음 **이벤트 규칙 생성**을 클릭합니다.
Tencent Cloud 서비스의 이벤트 버스는 기본적으로 모두 광저우에 저장되어 있으므로 여기에서 리전 및 이벤트 버스에 대한 다른 옵션을 선택할 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/01bd03e8bdad4b11276e2a8fdfa516a9.png)
4. 이벤트 규칙을 구성하고 **다음**을 클릭합니다.
  - 규칙 이름: 서비스를 구분하기 위한 규칙 이름을 입력하며, 한번 설정하면 수정할 수 없습니다.
  - 규칙 패턴: **사용자 지정 이벤트**를 선택합니다.
  - 규칙 패턴 미리보기: 다음 샘플 코드를 복사하여 샘플 작업 ID를 모니터링할 DTS 작업의 실제 ID로 바꿉니다. 여러 작업을 쉼표","로 구분할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/29819a0c4d5a00137927c171c49ab374.png" style="zoom:90%;" />
```
// 단일 작업 ID에 대한 알림 수신 예시
    {
     "source":"dts.cloud.tencent",
     "subject":"sync-jt12XXgt"
    }
		
// 여러 작업 ID에 대한 알림 수신 예시
    {
     "source":"dts.cloud.tencent",
     "subject":["sync-jt12XXgt","dts-a5uqXXhs"]
    }
```
DTS 콘솔의 작업 ID 예시:
<img src="https://qcloudimg.tencent-cloud.cn/raw/2fc7012d10930e23f27310cecb121137.png" >
5. 알림 방식, 수신자, 전달 방식을 설정하고 트리거 방식에서 **메시지 푸시**를 선택한 후 **완료**를 클릭합니다.
새로운 수신자 사용자/사용자 그룹을 추가하려면 [CAM](https://console.cloud.tencent.com/cam) 콘솔에서 구성한 후 이 단계의 **수신자**에서 선택합니다.
다른 트리거 방법을 구성하려면 하단의 **추가**를 클릭하여 더 많은 딜리버리 타깃을 추가합니다.
6. 이벤트 규칙 목록으로 돌아가 생성된 이벤트 규칙이 활성화되었는지 확인합니다. 그 후 작업 예외가 경보를 트리거하면 구성된 수신자가 메시지 알림을 수신합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/cda96cd6cc44dbd7c139bab1a13e0972.png)
