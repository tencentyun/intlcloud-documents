본 문서는 TRTC 방에 들어가는 방법을 설명합니다. 오디오/비디오 방에 입장한 후에만 사용자는 방에 있는 다른 사용자의 오디오/비디오 스트림을 구독하거나 사용자 자신의 오디오/비디오 스트림을 다른 사용자에게 게시할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6000fddd57940b43688685b247941fbf.png)

## 호출 가이드

[](id:step1)
### 1단계: SDK 가져오기 및 App 권한 설정
[iOS](https://intl.cloud.tencent.com/document/product/647/35092)에 안내된 대로 SDK를 가져옵니다.

[](id:step2)
### 2단계: SDK 인스턴스 생성 및 이벤트 리스너 설정
플랫폼별 초기화 API를 호출하여 TRTC 객체 인스턴스를 생성합니다.
<dx-codeblock>
::: Android java
// 싱글톤 모드에서 SDK 인스턴스 생성 및 이벤트 리스너 설정
// Create trtc instance(singleton)  and set up event listeners
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(this);
:::
::: iOS&Mac ObjC
// 싱글톤 모드에서 SDK 인스턴스 생성 및 이벤트 리스너 설정
// Create trtc instance(singleton)  and set up event listeners
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
:::
::: Windows C++
// 싱글톤 모드에서 SDK 인스턴스 생성 및 이벤트 리스너 설정
// Create trtc instance(singleton)  and set up event listeners
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);
:::
</dx-codeblock>

[](id:step3)
### 3단계: SDK 이벤트 수신 대기
이벤트 콜백 API를 설정하여 SDK 동작 중 오류, 알람, 트래픽 통계, 네트워크 품질 정보 및 다양한 오디오/비디오 이벤트를 들을 수 있습니다.
<dx-codeblock>
::: Android
비즈니스 클래스가 **TRTCCloudListener**를 상속하도록 하고 onError 함수를 다시 로딩한 후, **setListener** API를 사용하여 this 포인터를 SDK에 전달하여 현재 클래스의 SDK에서 콜백 이벤트를 수신 대기합니다.
```java
// SDK 이벤트를 수신하고 ‘카메라 사용 권한이 없습니다’와 같은 오류 메시지에 대한 로그를 출력합니다.
// Listen to the "onError" event and print logs for errors such as "camera is not authorized"
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(this);

@Override
public void onError(int errCode, String errMsg, Bundle extraInfo) {
    if (errCode == TXLiteAVCode.ERR_CAMERA_NOT_AUTHORIZED) {
        Log.d(TAG, "Current application is not authorized to use the camera");
    }
}
```
:::
::: iOS&Mac ObjC
비즈니스 클래스가 **TRTCCloudDelegate**를 상속하도록 하고 onError 함수를 다시 로딩한 후, TRTCCloud의 **delegate** 속성을 사용하여 this 포인터를 SDK에 전달하여 현재 클래스의 SDK에서 콜백 이벤트를 수신 대기합니다.
```ObjectiveC
// SDK 이벤트를 수신하고 ‘카메라 사용 권한이 없습니다’와 같은 오류 메시지에 대한 로그를 출력합니다.
// Listen to the "onError" event and print logs for errors such as "camera is not authorized"
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;

- (void)onError:(TXLiteAVError)errCode
         errMsg:(nullable NSString *)errMsg
        extInfo:(nullable NSDictionary *)extInfo{
    if (ERR_CAMERA_NOT_AUTHORIZED == errCode) {
        NSString *errorInfo = @"Current application is not authorized to use the camera：";
        errorInfo = [errorInfo stringByAppendingString errMsg];
        [self toastTip:errorInfo];
    }
}
```
:::
::: Windows C++
비즈니스 클래스가 **ITRTCCloudCallback**을 상속하도록 하고 onError 함수를 다시 로딩한 후, **addCallback** API를 사용하여 SDK에 대한 this 포인터를 전달하여 현재 클래스의 SDK에서 콜백 이벤트를 수신합니다.
```C++
// SDK 이벤트를 수신하고 ‘카메라 사용 권한이 없습니다’와 같은 오류 메시지에 대한 로그를 출력합니다.
// Listen to the "onError" event and print logs for errors such as "camera is not authorized"
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);

// "onError" 함수를 다시 로딩합니다.
void onError(TXLiteAVError errCode, const char* errMsg, void* extraInfo) {
    if (errCode == ERR_CAMERA_NOT_AUTHORIZED) {
        printf("Current application is not authorized to use the camera");
    }
}
```
:::
</dx-codeblock>

[](id:step4)
### 4단계: 방 입장 매개변수 TRTCParams 준비
enterRoom API를 호출할 때 'TRTCParams' 및 'TRTCAppScene'이라는 두 가지 주요 매개변수를 입력해야 합니다.

#### 매개변수1: TRTCAppScene
이 매개변수는 응용 시나리오를 **라이브 스트리밍** 또는 **실시간 통화**로 지정하는 데 사용됩니다.
- **실시간 통화:**
'TRTCAppSceneVideoCall'과 'TRTCAppSceneAudioCall'의 두 가지 옵션이 있으며 각각 영상 통화와 음성 통화입니다. 이 모드는 일대일 음성/영상 통화 또는 최대 300명의 참석자를 위한 온라인 회의에 적합합니다.

- **라이브 스트리밍:**
라이브 스트리밍에는 비디오 라이브 스트리밍과 오디오 라이브 스트리밍인 'TRTCAppSceneLIVE'와 'TRTCAppSceneVoiceChatRoom'의 두 가지 옵션이 있습니다. 이 모드는 최대 10만명의 사용자에게 라이브 스트리밍에 적합합니다. 그러나 방의 사용자(**anchor** 또는 **audience**)에 대한 TRTCParams 매개변수에 **role** 필드를 지정해야 합니다

#### 매개변수2: TRTCParams
TRTCParams는 많은 필드로 구성됩니다. 그러나 일반적으로 다음 필드를 설정하는 방법에만 주의하면 됩니다:

| 매개변수 | 설명 | 비고 | 데이터 유형 | 샘플 값 |
|---------|---------|---------|---------|---------|
| SDKAppID | 애플리케이션 ID | <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 볼 수 있습니다. 존재하지 않는 경우 ‘애플리케이션 생성’을 클릭하여 애플리케이션을 생성합니다. | 숫자 | 1400000123 |
| userId | 사용자 ID | 사용자 이름. 영어 대문자 및 소문자(a-z, A-Z), 숫자(0-9), 밑줄 및 하이픈만 포함할 수 있습니다. TRTC에서는 하나의 userId가 두 개의 다른 장치에서 동시에 같은 방에 들어갈 수 없습니다. | 문자열 | ‘denny’ 또는 ‘123321’|
| userSig | 방 입장 서명 | [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)의 안내에 따라 SDKAppID와 userId를 기반으로 userSig를 계산할 수 있습니다. | 문자열 | eJyrVareCeYrSy1SslI... |
| roomId | 방 ID | 숫자 유형의 방 ID입니다. 문자열 형식의 방 ID를 사용하려면 roomId 필드 대신 **strRoomId** 필드만 사용하십시오. strRoomId와 roomId는 함께 사용할 수 없기 때문입니다. | 숫자 | 29834 |
| strRoomId | 방 ID | 문자열 유형의 방 ID입니다. strRoomId와 roomId를 혼동하지 마십시오. TRTC 백엔드에서는 ‘123’과 123을 서로 다른 방으로 간주합니다.  | 숫자 | 29834 |
| role | 역할 | ‘앵커’와 ‘시청자’의 두 가지 역할이 있습니다. 이 필드는 TRTCAppScene이 `TRTCAppSceneLIVE` 또는 `TRTCAppSceneVoiceChatRoom` 라이브 스트리밍 시나리오로 설정된 경우에만 필요합니다. | 열거 | TRTCRoleAnchor 또는 TRTCRoleAudience   |

>!
>- TRTC에서 하나의 userId는 두 개의 다른 장치에서 동시에 같은 방에 들어갈 수 없습니다. 그렇지 않으면 충돌이 발생합니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.


[](id:step5)
### 5단계: 방 입장(enterRoom)
4단계에서 설명한 두 개의 매개변수 TRTCAppScene과 TRTCParams를 준비한 후 enterRoom API 함수를 호출하여 방에 들어갈 수 있습니다.

<dx-codeblock>
::: Android  Java
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(mTRTCCloudListener);

// TRTC 방 입장 매개변수를 어셈블합니다. TRTCParams의 필드 값을 고유한 매개변수 값으로 교체합니다
// Please replace each field in TRTCParams with your own parameters
TRTCCloudDef.TRTCParams param = new TRTCCloudDef.TRTCParams();
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = TRTCCloudDef.TRTCRoleAnchor;

// 시나리오가 ‘라이브 스트리밍’인 경우 애플리케이션 시나리오를 TRTC_APP_SCENE_LIVE로 설정합니다
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
mCloud.enterRoom(param, TRTCCloudDef.TRTC_APP_SCENE_LIVE);        
:::

::: iOS&Mac  objectivec
self.trtcCloud = [TRTCCloud sharedInstance];
self.trtcCloud.delegate = self;

// TRTC 방 입장 매개변수를 어셈블합니다. TRTCParams의 필드 값을 고유한 매개변수 값으로 교체합니다
// Please replace each field in TRTCParams with your own parameters
TRTCParams *params = [[TRTCParams alloc] init];
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.roomId = 123321; // Please replace with your own room number
params.userId = @"denny";   // Please replace with your own userid  
params.userSig = @"xxx"; // Please replace with your own userSig
params.role = TRTCRoleAnchor;

// 시나리오가 ‘라이브 스트리밍’인 경우 애플리케이션 시나리오를 TRTC_APP_SCENE_LIVE로 설정합니다
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
[self.trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
:::

::: Windows  C++
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);

// TRTC 방 입장 매개변수를 어셈블합니다. TRTCParams의 필드 값을 고유한 매개변수 값으로 교체합니다.
// Please replace each field in TRTCParams with your own parameters
liteav::TRTCParams params;
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = liteav::TRTCRoleAnchor;

// 시나리오가 ‘라이브 스트리밍’인 경우 애플리케이션 시나리오를 TRTC_APP_SCENE_LIVE로 설정합니다
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
trtc_cloud_->enterRoom(params, liteav::TRTCAppSceneLIVE);        
:::
</dx-codeblock>

**이벤트 콜백**
방 입장이 성공하면 SDK는 onEnterRoom(result) 이벤트를 다시 호출합니다. 여기서 result는 0보다 큰 값으로 방 입장 소요 시간(밀리초)을 나타냅니다.
방 입장이 실패하면 SDK는 onEnterRoom(result) 이벤트도 다시 호출하지만 'result' 값은 방 입장 실패에 대한 오류 코드를 나타내는 음수가 됩니다.
<dx-codeblock>
::: Android Java
// SDK의 onEnterRoom 이벤트를 수신하여 방 입장 결과를 얻습니다
// Listen to the onEnterRoom event of the SDK and learn whether the room is successfully entered
@Override
public void onEnterRoom(long     result) {
    if (result > 0) {
        Log.d(TAG, "Enter room succeed");
    } else {
        Log.d(TAG, "Enter room failed");
    }
}
:::
::: iOS&Mac ObjC
// SDK의 onEnterRoom 이벤트를 수신하여 방 입장 결과를 얻습니다
// Listen to the onEnterRoom event of the SDK and learn whether the room is successfully entered
- (void)onEnterRoom:(NSInteger)result {
    if (result > 0) {
        [self toastTip:@"Enter room succeed!"];
    } else {
        [self toastTip:@"Enter room failed!"];
    }
}
:::
::: Windows C++
// SDK의 onEnterRoom 이벤트를 수신하여 방 입장 결과를 얻습니다
// override to the onEnterRoom event of the SDK and learn whether the room is successfully entered
void onEnterRoom(int result) {
    if (result > 0) {
        printf("Enter room succeed");
    } else {
        printf("Enter room failed");
    }
}
:::
</dx-codeblock>
