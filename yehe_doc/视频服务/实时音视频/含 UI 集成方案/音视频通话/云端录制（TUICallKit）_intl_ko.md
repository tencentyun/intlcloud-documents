본문은 TUICallKit의 클라우드 녹화를 활성화하여 중요한 통화를 보관하고 검토하는 방법을 설명합니다. 여기서 [자동 녹화](#Option1)와 [REST API 기반 녹화](#Option2)의 두 가지 방식을 제공합니다.

>? TUICallKit은 여러 기본 Tencent Cloud PaaS 서비스를 통합하며 오디오/비디오 기능은 [TRTC](https://www.tencentcloud.com/document/product/647/35078)에 의존합니다. TUICallKit의 온-클라우드 녹화 기능을 사용하려면 [TRTC 콘솔](https://console.tencentcloud.com/trtc/app)에서 설정해야 합니다.

[](id:Option1)
## 스키마1: 자동 녹화(권장)

자동 녹화 스키마를 사용하는 것이 좋습니다. 이 스키마에서는 사용자가 수동으로 녹음을 시작하거나 중지하지 않습니다. 대신 녹음 작업은 TRTC 백엔드에서 관리되며 업스트림되는 오디오/비디오 스트림이 있을 때 통화가 자동으로 녹음됩니다. **다음과 같이 쉽고 빠르게** 통합할 수 있습니다. 

1. TRTC 콘솔의 [애플리케이션 관리](https://console.tencentcloud.com/trtc/app)에서 대상 SDKAppId의 애플리케이션을 찾아 아래와 같이 기능 구성 페이지로 이동합니다.

2. 기능 구성 페이지의 온클라우드 녹화 구성 카드에서 **온클라우드 녹화 기능을 활성화**합니다. **글로벌 자동 녹화 템플릿** 카드에서 **템플릿 생성**을 클릭합니다.![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. 1v1 및 그룹 통화와 같은 음성/영상 통화 비즈니스 시나리오에 대해 다음 구성 매개변수 설정을 권장합니다. 필요에 따라 녹화 템플릿을 사용자 정의할 수도 있습니다.![img](https://qcloudimg.tencent-cloud.cn/raw/8f8a9d9d029d63fa2d70c1105630aa20.png)

>! 글로벌 녹화는 최대 8명의 사용자 스트림을 혼합할 수 있습니다. 통화에 8명 이상의 사용자(로컬 사용자 포함)가 포함된 경우 마지막 사용자의 스트림은 녹화되지 않습니다.

글로벌 자동 녹화 기능이 활성화된 후 전화를 받고 오디오/비디오가 업스트림되면 녹화 작업이 자동으로 실행되고 통화가 종료되면 녹화가 자동으로 중지됩니다. 사용자가 네트워크 상태가 좋지 않거나 기타 예외로 인해 방을 나가는 경우 녹화 백엔드는 불필요한 요금이 발생하지 않도록 구성된 MaxIdleTime 값(최대 유휴 시간, 기본적으로 5s)에 따라 녹화 작업을 자동으로 중지합니다.

4. **템플릿이 생성되면 글로벌 자동 녹화를 선택**합니다. 

[](id:Option2)
## 스키마2: REST API 기반 녹화

자동 녹화 스키마가 요구 사항을 충족하지 않는 경우 더 유연한 REST API 기반 녹화 스키마를 사용할 수도 있습니다. 이 스키마에서는 방의 지정된 앵커를 녹화 및 구독하고, 혼합 스트림의 레이아웃을 사용자 지정하고, 녹화 중에 레이아웃 및 구독을 업데이트할 수 있습니다. 그러나 **해당 기능을 사용하려면 비즈니스 백엔드 서비스와 함께 사용하고 복잡한 통합 작업을 수행해야 합니다**:

1. TRTC 콘솔의 [애플리케이션 관리](https://console.tencentcloud.com/trtc/app)에서 대상 SDKAppId의 애플리케이션을 찾아 아래와 같이 기능 구성 페이지로 이동합니다.

2. 기능 구성 페이지의 온클라우드 녹화 구성 카드에서 **온클라우드 녹화 기능을 활성화**합니다. **수동 사용자 지정 녹화**, 즉 REST API 기반 녹화 모드가 기본적으로 선택되어 있습니다.![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. 그런 다음 REST API [CreateCloudRecording](https://www.tencentcloud.com/document/product/647/46960)를 호출하여 클라우드 녹화를 시작할 수 있습니다. 여기에서 음성/영상 통화가 시작될 때 녹음을 시작하려면 [TUICallObserver](https://www.tencentcloud.com/document/product/647/51007)의 알림 이벤트를 청취하는 것이 좋습니다. 다음은 Java 코드 샘플입니다.

```java
TUICallEngine.createInstance(context).addObserver(new TUICallObserver() {
    @Override
    public void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole) {
        // 관련 REST API를 사용하여 녹화 작업을 시작하도록 비즈니스 백엔드에 지시합니다.
    }
});
```

4. 네트워크 불량이나 프로세스 종료 등의 예외적인 상황으로 클라이언트에서 통화가 끊길 수 있으므로 녹음을 중지하려면 TRTC 방 상태 콜백을 구독하고(자세한 내용은 [서버 이벤트 콜백 수신](https://www.tencentcloud.com/document/product/647/39558) 참고), REST API [DeleteCloudRecording](https://www.tencentcloud.com/document/product/647/46959)를 호출하여 녹음을 중지하는 것이 좋습니다. TRTC 룸 해제 콜백을 수신하면 온클라우드 녹화 작업을 중지합니다.

## FAQ

### 1. 자세한 녹화 시간은 어떻게 확인하나요?

자세한 녹화 시간은 TRTC 콘솔의 [온클라우드 녹화](https://console.tencentcloud.com/trtc/statistics/cloud-record) 페이지에서 확인할 수 있습니다.

### 2. 녹화된 파일은 어떻게 보나요?

[VOD 콘솔](https://console.tencentcloud.com/vod)에 로그인하고 왼쪽 사이드바에서 **비디오/오디오 관리**를 선택하고 목록 상단의 **접두사 검색**을 클릭한 다음 **접두사 검색**을 선택하고 검색 창에 키워드를 입력합니다. 녹화 파일 이름은 다음과 같은 형식입니다.

- MP4 단일 스트림 녹화 파일의 파일 이름 형식: `<SdkAppId>_<RoomId>_UserId_s_<UserId>_UserId_e_<MediaId>_<Index>.mp4`
- MP4 혼합 스트림 녹화 파일의 파일 이름 형식: `<SdkAppId>_<RoomId>_<Index>.mp4`