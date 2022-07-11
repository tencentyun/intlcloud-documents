본 문서는 앵커가 오디오/비디오 스트림을 게시하는 방법을 설명합니다. ‘게시’는 마이크와 카메라를 켜서 오디오를 듣고 비디오를 방의 다른 사용자에게 표시하는 것을 의미합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/b86c1df39b412bddf29d26bfaa9d5f02.png)
## 호출 가이드

[](id:step1)
### 1단계: 필수 단계 수행

[빠른 통합(iOS)](https://intl.cloud.tencent.com/document/product/647/35092)에 설명된 대로 SDK를 가져오고 애플리케이션 권한을 구성합니다.

[](id:step2)
### 2단계: 카메라 미리보기 활성화
**startLocalPreview** API를 호출하여 카메라 미리보기를 활성화하면 SDK가 카메라 권한에 대해 시스템에 적용됩니다. 카메라 이미지는 권한이 부여된 후에만 캡처할 수 있습니다.

로컬 비디오 이미지의 렌더링 매개변수를 설정하려면 **setLocalRenderParams** API를 호출하여 로컬 미리보기의 렌더링 매개변수를 설정할 수 있습니다. 미리보기가 활성화된 후 미리보기 매개변수를 설정하면 화면 떨림이 발생할 수 있으므로 미리보기 매개변수를 설정하려면 미리보기를 활성화하기 전에 이 API를 호출하는 것이 좋습니다.

카메라 제어 매개변수를 제어하려면 **TXDeviceManager** API를 호출하여 ‘전면 및 후면 카메라를 전환’하고 ‘초점 모드를 설정’하고 ‘플래시를 켜고 끄기’할 수 있습니다.

뷰티 필터 효과 및 화질은 [화면 품질 설정](https://intl.cloud.tencent.com/document/product/647/35153)에 안내된 대로 조정할 수 있습니다.

<dx-codeblock>
::: Android  java
// 로컬 비디오 이미지의 미리보기 모드 설정: 수평 미러링을 활성화하고 비디오 이미지의 채우기 모드를 설정합니다
TRTCCloudDef.TRTCRenderParams param = new TRTCCloudDef.TRTCRenderParams();
param.fillMode   = TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FILL;
param.mirrorType = TRTCCloudDef.TRTC_VIDEO_MIRROR_TYPE_AUTO;
mCloud.setLocalRenderParams(param);

// 로컬 카메라 미리보기 활성화(localCameraVideo는 로컬 비디오 이미지를 렌더링하는 데 사용되는 컨트롤입니다)
TXCloudVideoView cameraVideo = findViewById(R.id.txcvv_main_local);
mCloud.startLocalPreview(true, cameraVideo);

// TXDeviceManager를 사용하여 자동 초점을 활성화하고 플래시를 켭니다
TXDeviceManager manager = mCloud.getDeviceManager();
if (manager.isAutoFocusEnabled()) {
    manager.enableCameraAutoFocus(true);
}
manager.enableCameraTorch(true);
:::
::: iOS  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// 로컬 비디오 이미지의 미리보기 모드 설정: 수평 미러링을 활성화하고 비디오 이미지의 채우기 모드를 설정합니다
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode   = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorTypeAuto;
[self.trtcCloud setLocalRenderParams:param];

// 로컬 카메라 미리보기 활성화(localCameraVideoView는 로컬 비디오 이미지를 렌더링하는 데 사용되는 컨트롤입니다)
[self.trtcCloud startLocalPreview:YES view:localCameraVideoView];

// TXDeviceManager를 사용하여 자동 초점을 활성화하고 플래시를 켭니다
TXDeviceManager *manager = [self.trtcCloud getDeviceManager];
if ([manager isAutoFocusEnabled]) {
    [manager enableCameraAutoFocus:YES];
}
[manager enableCameraTorch:YES];
:::
::: Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// 로컬 비디오 이미지의 미리보기 모드 설정: 수평 미러링을 활성화하고 비디오 이미지의 채우기 모드를 설정합니다
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode   = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorTypeAuto;
[self.trtcCloud setLocalRenderParams:param];

// 로컬 카메라 미리보기 활성화(localCameraVideoView는 로컬 비디오 이미지를 렌더링하는 데 사용되는 컨트롤입니다)
[self.trtcCloud startLocalPreview:localCameraVideoView];
:::
::: Windows  C++
// 로컬 비디오 이미지의 미리보기 모드 설정: 수평 미러링을 활성화하고 비디오 이미지의 채우기 모드를 설정합니다
liteav::TRTCRenderParams render_params;
render_params.mirrorType = liteav::TRTCVideoMirrorType_Enable;
render_params.fillMode = TRTCVideoFillMode_Fill;
trtc_cloud_->setLocalRenderParams(render_params);

// 로컬 카메라 미리보기 활성화(view는 로컬 비디오 이미지를 렌더링하는 데 사용되는 제어 핸들입니다)
liteav::TXView local_view = (liteav::TXView)(view);
trtc_cloud_->startLocalPreview(local_view);
:::
</dx-codeblock>


[](id:step3)
### 3단계: 마이크 캡처 활성화
**startLocalAudio**를 호출하여 마이크 캡처를 시작할 수 있습니다. 이 API를 사용하려면 'quality' 매개변수를 사용하여 캡처 모드를 결정해야 합니다. 매개변수 이름이 quality이지만 정확히는 scene을 의미합니다. 높은 품질이 반드시 좋은 것은 아니며 비즈니스 시나리오에 따라 적절한 품질을 설정해야 합니다.

- **SPEECH**
이 모드에서 SDK 오디오 모듈은 오디오 신호를 캡처하고 가능한 한 환경 소음을 필터링하는 데 전념합니다. 또한 이 모드의 오디오 데이터는 열악한 네트워크 품질에 대한 내성이 가장 높습니다. 따라서 ‘화상 통화’ 및 ‘온라인 회의’와 같이 음성 통신을 강조하는 시나리오에 특히 적합합니다.
- **MUSIC**
이 모드에서 SDK는 높은 오디오 처리 대역폭과 스테레오 모드를 사용하여 캡처 품질을 최대화하고 오디오 DSP 모듈을 가장 낮은 수준으로 조정하여 가능한 최고의 오디오 품질을 제공합니다. 따라서 앵커가 전문 사운드 카드를 사용하여 음악을 라이브 스트리밍하는 경우 특히 ‘음악 라이브 스트리밍’ 시나리오에 적합합니다.
- **DEFAULT**
이 모드에서 SDK는 스마트 인식 알고리즘을 사용하여 현재 환경을 인식하고 그에 따라 가장 적합한 처리 모드를 선택합니다. 그러나 아무리 좋은 인식 알고리즘이라도 때로는 부정확할 수 있습니다. 제품 포지셔닝에 대해 잘 알고 있다면 SPEECH 또는 MUSIC을 선택하여 더 나은 오디오 커뮤니케이션이나 음악 품질을 즐길 것을 권장합니다.

<dx-codeblock>
::: Android  java
// 마이크 캡처를 활성화하고 quality를 SPEECH로 설정합니다(노이즈 억제가 높고 네트워크 상태가 좋지 않음)
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_SPEECH );

// 마이크 캡처를 활성화하고 quality를 MUSIC으로 설정합니다(최소 오디오 품질 손실로 Hi-Fi 오디오를 캡처하며 전문 사운드 카드와 함께 사용하는 것이 좋습니다)
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_MUSIC);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// 마이크 캡처를 활성화하고 quality를 SPEECH로 설정합니다(노이즈 억제가 높고 네트워크 상태가 좋지 않음)
[self.trtcCloud startLocalAudio:TRTCAudioQualitySpeech];

// 마이크 캡처를 활성화하고 quality를 MUSIC으로 설정합니다(최소 오디오 품질 손실로 Hi-Fi 오디오를 캡처하며 전문 사운드 카드와 함께 사용하는 것이 좋습니다)
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
:::
::: Windows  C++
// 마이크 캡처를 활성화하고 quality를 SPEECH로 설정합니다(노이즈 억제가 높고 네트워크 상태가 좋지 않음)
trtc_cloud_->startLocalAudio(TRTCAudioQualitySpeech);

// 마이크 캡처를 활성화하고 quality를 MUSIC으로 설정합니다(최소 오디오 품질 손실로 Hi-Fi 오디오를 캡처하며 전문 사운드 카드와 함께 사용하는 것이 좋습니다)
trtc_cloud_->startLocalAudio(TRTCAudioQualityMusic);
:::
</dx-codeblock>

[](id:step4)
### 4단계: TRTC 방 입장

[방 입장](https://intl.cloud.tencent.com/document/product/647/47645)의 안내에 따라 현재 사용자가 TRTC 방에 입장하도록 합니다. SDK는 방에 성공적으로 입장하면 원격 사용자에게 오디오 스트림을 게시하기 시작합니다.

>! 물론 방에 입장(enterRoom)한 후 카메라 미리보기 및 마이크 캡처를 활성화할 수 있습니다. 그러나 라이브 스트리밍 시나리오에서는 앵커가 마이크를 테스트하고 뷰티 필터를 조정하는 데 일정 시간이 필요합니다. 따라서 먼저 카메라와 마이크를 켜고 방에 들어가는 것이 더 일반적입니다.

<dx-codeblock>
::: Android  java
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

::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
self.trtcCloud.delegate = self;

// TRTC 방 입장 매개변수를 어셈블합니다. TRTCParams의 필드 값을 고유한 매개변수 값으로 교체합니다.
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

// TRTC 방 입장 매개변수를 어셈블합니다. TRTCParams의 필드 값을 고유한 매개변수 값으로 교체합니다
// Please replace each field in TRTCParams with your own parameters
liteav::TRTCParams params;
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = TRTCCloudDef.TRTCRoleAnchor;

// 시나리오가 ‘라이브 스트리밍’인 경우 애플리케이션 시나리오를 TRTC_APP_SCENE_LIVE로 설정합니다
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
trtc_cloud_->enterRoom(params, liteav::TRTCAppSceneLIVE);
:::
</dx-codeblock>


[](id:step5)
### 5단계: 역할 전환

**TRTC에서의 ‘역할’**
- ‘영상 통화’(TRTC_APP_SCENE_VIDEOCALL) 및 ‘음성 통화’(TRTC_APP_SCENE_AUDIOCALL) 시나리오에서는 이 두 시나리오에서 각 사용자가 기본적으로 앵커(Anchor)이기 때문에 방에 들어갈 때 역할을 설정할 필요가 없습니다.
- ‘비디오 라이브 스트리밍’(TRTC_APP_SCENE_LIVE) 및 ‘오디오 라이브 스트리밍’(TRTC_APP_SCENE_VOICE_CHATROOM) 시나리오에서 각 사용자는 방에 입장할 때 ‘앵커(Anchor)’ 또는 ‘시청자(Audience)’에게 자신의 ‘역할’을 설정해야 합니다.

**역할 스위치**
TRTC에서는 ‘앵커(Anchor)’만 오디오/비디오 스트림을 게시할 수 있지만 ‘시청자(Audience)’는 할 수 없습니다.
따라서 방에 입장할 때 역할을 ‘시청자(Audience)’로 설정하면 오디오/비디오 스트림을 게시하기 전에 먼저 **switchRole** API를 호출하여 역할을 ‘앵커(Anchor)’로 전환해야 합니다. 이 프로세스를 ‘마이크 켜기’이라고 합니다.

<dx-codeblock>
::: Android java
// 현재 역할이 시청자(Audience)인 경우 앵커(Anchor)로 전환하려면 먼저 switchRole을 호출해야 합니다
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
mCloud.switchRole(TRTCCloudDef.TRTCRoleAnchor);
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_DEFAULT);
mCloud.startLocalPreview(true, cameraVide);

// 역할 전환이 실패한 경우 onSwitchRole 콜백의 오류 코드는 0이 아닙니다
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
@Override
public void onSwitchRole(final int errCode, final String errMsg) {
    if (errCode != 0) {
        Log.d(TAG, "Switching operation failed...");
    }   
}
:::
::: iOS ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// 현재 역할이 시청자(Audience)인 경우 앵커(Anchor)로 전환하려면 먼저 switchRole을 호출해야 합니다
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityDefault];
[self.trtcCloud startLocalPreview:YES view:localCameraVideoView];

// 역할 전환이 실패한 경우 onSwitchRole 콜백의 오류 코드는 0이 아닙니다
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
- (void)onSwitchRole:(TXLiteAVError)errCode errMsg:(nullable NSString *)errMsg {
    if (errCode != 0) {
        NSLog(@"Switching operation failed... ");
    }   
}
:::
::: Mac ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// 현재 역할이 시청자(Audience)인 경우 앵커(Anchor)로 전환하려면 먼저 switchRole을 호출해야 합니다
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityDefault];
[self.trtcCloud startLocalPreview:localCameraVideoView];

// 역할 전환이 실패한 경우 onSwitchRole 콜백의 오류 코드는 0이 아닙니다
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
- (void)onSwitchRole:(TXLiteAVError)errCode errMsg:(nullable NSString *)errMsg {
    if (errCode != 0) {
        NSLog(@"Switching operation failed... ");
    }   
}
:::
::: Windows C++
// 현재 역할이 시청자(Audience)인 경우 앵커(Anchor)로 전환하려면 먼저 switchRole을 호출해야 합니다
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
trtc_cloud_->switchRole(liteav::TRTCRoleAnchor);
trtc_cloud_->startLocalAudio(TRTCAudioQualityDefault);
trtc_cloud_->startLocalPreview(hWnd);

// 역할 전환이 실패한 경우 onSwitchRole 콜백의 오류 코드는 ERR_NULL이 아닙니다(즉, 0)
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
void onSwitchRole(TXLiteAVError errCode, const char* errMsg) {
    if (errCode != ERR_NULL) {
        printf("Switching operation failed...");
    }
}
:::
</dx-codeblock>

**주의:** 방에 앵커가 너무 많으면 switchRole이 실패하고 TRTC는 onSwitchRole을 통해 오류 코드를 알려줍니다. 따라서 더 이상 오디오/비디오 스트림을 게시하지 않으려면 switchRole을 다시 호출하여 ‘시청자(Audience)’로 전환해야 합니다. 이 프로세스는 ‘마이크 끄기’라고 합니다.

>? 앵커만 오디오/비디오 스트림을 게시할 수 있지만 각 사용자를 앵커로 방에 들어오게 할 수는 없습니다. 구체적인 이유는 [한 방에 최대 몇 개의 동시 오디오/비디오 스트림이 있습니까?](#speed1)를 참고하십시오

## 고급 가이드

[](id:speed1)
### 1. 방은 최대 몇 개의 동시 오디오/비디오 스트림을 가질 수 있습니까?
TRTC 룸은 최대 **50**개의 동시 오디오/비디오 스트림을 가질 수 있으며 과도한 스트림은 ‘선착순’ 원칙에 따라 중단됩니다.
**역할 관리**가 잘 구현되는 한 50개의 동시 오디오/비디오 스트림은 일대일 화상 통화에서 수만 명의 사용자가 시청하는 라이브 스트림에 이르기까지 대부분의 시나리오에서 요구 사항을 충족할 수 있습니다.

소위 ‘역할 관리’는 방에 입장하는 사용자에게 역할을 할당하는 것입니다.
- 사용자가 라이브 스트리밍의 ‘앵커’, 온라인 교육의 ‘교사’ 또는 온라인 회의의 ‘호스트’인 경우 ‘앵커(Anchor)’ 역할을 할당받을 수 있습니다.
- 사용자가 라이브 스트리밍 ‘시청자’, 온라인 교육 ‘학생’ 또는 온라인 회의 ‘참석자’인 경우 ‘시청자(Audience)’ 역할을 할당해야 합니다. 그렇지 않으면 이렇게 많은 수의 사용자가 앵커 할당량을 즉시 ‘소진’하게 됩니다.

‘시청자’가 오디오/비디오 스트림(‘마이크 켜기’)을 게시하려는 경우에만 switchRole을 통해 ‘앵커’ 역할로 전환해야 합니다. 오디오/비디오 스트림을 더 이상 게시하지 않으려면(‘마이크 끄기’) 즉시 시청자 역할로 다시 전환해야 합니다.

적절한 역할 관리에 따라 일반적으로 한 방에 50명 이하의 ‘앵커’가 오디오/비디오 스트림을 동시에 게시해야 합니다. 그렇지 않으면 일반 사람들은 6명 이상의 사람들이 동시에 말할 때 스피커를 구별하기 어려워 방 전체가 ‘엉망’이 될 것입니다.









