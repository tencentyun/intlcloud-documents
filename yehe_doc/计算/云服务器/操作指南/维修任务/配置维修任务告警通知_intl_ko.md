## 작업 시나리오

CVM 인스턴스의 유지 보수 작업에 대한 경보 알림을 설정하여 예외 발생 시 이메일, SMS, 전화 등을 통해 즉시 알림을 받을 수 있습니다. 본문은 [EventBridge](https://intl.cloud.tencent.com/document/product/1108/42267)를 사용하여 EventBridge 콘솔에서 CVM 인스턴스에 대한 경보 알림을 설정하는 방법을 설명합니다.

## 작업 단계
1. [EventBridge 콘솔](https://console.cloud.tencent.com/eb)에 로그인한 후, [Activating EventBridge](https://intl.cloud.tencent.com/document/product/1108/42272)를 참고하여 서비스를 활성화합니다.
2. 왼쪽 사이드바에서 **[이벤트 규칙](https://console.cloud.tencent.com/eb/rule)**을 선택하고 ‘이벤트 규칙’ 페이지 상단에서 대상 리전 및 이벤트 버스를 선택한 후 **이벤트 규칙 생성**을 클릭합니다.
3. ‘이벤트 규칙 생성’ 페이지로 이동합니다.
    1. ‘기본 정보’에서 아래와 같이 **규칙 이름** 매개변수를 설정합니다. 다음 이미지 참고:
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/zHwA899_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102346.png)
    2. ‘이벤트 패턴’에서 필요에 따라 아래와 같이 ‘이벤트 매칭’ 매개변수를 설정합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/bQp2060_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102608.png)
       - **Tencent Cloud 서비스**: 드롭다운 목록에서 **CVM**을 선택합니다.
       - **이벤트 유형**: 드롭다운 목록에서 필요에 따라 옵션을 선택합니다.
   3. **다음**을 클릭합니다.
   4. ‘딜리버리 대상’의 ‘트리거 방법’ 드롭다운 목록에서 필요에 따라 옵션을 선택합니다.
      - ‘트리거 방법’으로 **CLS**를 선택합니다. 자세한 내용은 [CLS Log Target](https://intl.cloud.tencent.com/document/product/1108/46992)을 참고하십시오.
      - ‘트리거 방법’으로 **메시지 푸시**를 선택합니다. 자세한 내용은 [Message Push Target](https://intl.cloud.tencent.com/document/product/1108/46779)을 참고하십시오.
4. **완료**를 클릭하여 설정을 완료합니다.
