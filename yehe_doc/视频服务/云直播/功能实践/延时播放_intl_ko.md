딜레이 재생은 클라이이언트에서 풀 스트림 시 진행하는 딜레이 재생 기능으로 주로 중요 라이브 방송 이벤트에서 돌발 상황을 방지하기 위해 사용되며 사전에 프로세싱하여 매개변수를 통해 직접 설정할 수 있습니다.   

## 주의 사항
딜레이 재생은 현재 두 가지 방식으로 구현됩니다. 
- [딜레이 재생 인터페이스](https://intl.cloud.tencent.com/document/product/267/30850)를 호출하여 딜레이 기능을 구현합니다. 
- **푸시 스트림 주소**뒤에 txDelayTime 매개변수를 추가하여 빠르게 딜레이 기능을 구현합니다. 자세한 내용은 [푸시 스트리밍 설정](#push_delay)을 참고하십시오.

>? 인터페이스를 호출하면 캐시 설정까지 포함될 수 있고 적용 시간을 통제하기 어렵기 때문에 인터페이스 방식은 권장하지 않습니다. 푸시 스트림 주소 뒤에 직접 매개변수를 추가하는 방법을 통한 빠른 구현을 권장합니다.

## 준비 작업
1. [Tencent CSS 서비스](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)를 활성화하고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료해야 합니다. 
2. CSS 콘솔에 로그인한 후, [[도메인 이름 관리]](https://console.cloud.tencent.com/live/domainmanage)를 선택하고, [도메인 추가]를 클릭하여 ICP 비안을 받은 풀 스트림 도메인을 추가합니다. 자세한 내용은 [외부 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참고하십시오.

[](id:push_delay)
## 푸시 스트림 설정
1, CSS 콘솔의 [라이브 방송 툴 박스]>[[주소 생성기]](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)에서 푸시 스트림 주소를 생성합니다.
![](https://main.qcloudimg.com/raw/025aeea991996ddc35e6b61341714282.png)
2. 푸시 스트리밍 뒤에 `txDelayTime` 매개변수를 추가하고, OBS를 통해 푸시 스트리밍합니다. 구체적인 작업 방법은 [OBS 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31569)을 참고하십시오.
![](https://main.qcloudimg.com/raw/11cc2aee28d263e5740b1b6d0701652f.png)
>! txDelayTime에 딜레이 시간(단위: 초, 최댓값: 600초), Integer 유형을 입력합니다.


## 딜레이 재생
1. CSS 콘솔의 [라이브 방송 툴 박스]>[주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)에서 해당 풀 스트림 주소를 생성합니다. 
2. [VLC](https://intl.cloud.tencent.com/document/product/267/32483), FFmepg 등 툴을 사용하여 재생할 수 있습니다. 재생 관련 자세한 내용은 [라이브 방송 재생](https://intl.cloud.tencent.com/document/product/267/31559)을 참고하십시오.
![]

 이상의 비교를 통해 재생 화면의 딜레이는 34s임을 알 수 있습니다. 하지만 설정한 딜레이 시간은 30s이기 때문에 푸시 스트림 주소에 txDelayTime 매개변수를 추가하는 방식으로 딜레이 재생 효과를 구현하였습니다. 
