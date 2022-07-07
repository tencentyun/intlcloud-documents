본 문서는 방에 있는 다른 사용자의 오디오/비디오 스트림을 구독하는 방법, 즉 다른 사용자의 오디오/비디오를 재생하는 방법을 설명합니다. 편의상 이 문서에서는 ‘방에 있는 다른 사용자’를 ‘원격 사용자’라고 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9b0ed566818d885be845b9bafb35b57c.png)

## 호출 가이드

[](id:step1)
### 1단계: 필수 단계 수행

[빠른 통합(iOS)](https://intl.cloud.tencent.com/document/product/647/35092)에 설명된 대로 SDK를 가져오고 App 권한을 구성합니다.

[](id:step2)
### 2단계: 구독 모드 설정(선택 사항)
TRTCCloud에서 **setDefaultStreamRecvMode** API를 호출하여 구독 모드를 설정할 수 있습니다. TRTC는 두 가지 구독 모드를 제공합니다.
- 자동 구독: SDK는 별도의 수동 조작 없이 원격 사용자의 오디오를 자동으로 재생합니다. 이것은 기본 구독 모드입니다.
- 수동 구독: SDK는 원격 사용자의 오디오를 자동으로 가져오거나 재생하지 않습니다. 오디오를 재생하려면 **muteRemoteAudio(userId, false)**를 수동으로 호출해야 합니다.
>! SDK의 기본 구독 모드는 자동 구독이므로 setDefaultStreamRecvMode를 호출할 필요가 없습니다. 그러나 수동 구독을 사용하려는 경우 setDefaultStreamRecvMode는 enterRoom보다 먼저 호출되어야만 적용된다는 점에 유의하십시오.


[](id:step3)
### 3단계: TRTC 방 입장
[방 입장](https://intl.cloud.tencent.com/document/product/647/47645)의 안내에 따라 현재 사용자가 TRTC 방에 입장하도록 합니다. 사용자는 성공적인 방 입장 후에만 원격 사용자의 오디오/비디오 스트림을 구독할 수 있습니다.


[](id:step4)
### 4단계: 오디오 스트림 재생
muteRemoteAudio("denny", true)를 호출하여 원격 사용자 denny를 음소거한 다음 muteRemoteAudio("denny", false) API를 호출하여 denny의 음소거를 해제할 수 있습니다.

<dx-codeblock>
::: Android  Java
// Mute user with id denny
mCloud.muteRemoteAudio("denny", true);
// Unmute user with id denny
mCloud.muteRemoteAudio("denny", false);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Mute user with id denny
[self.trtcCloud muteRemoteAudio:@"denny" mute:YES];
// Unmute user with id denny
[self.trtcCloud muteRemoteAudio:@"denny" mute:YES];
:::
::: Windows  C++
// Mute user with id denny
trtc_cloud_->muteRemoteAudio("denny", true);
// Unmute user with id denny
trtc_cloud_->muteRemoteAudio("denny", false);
:::
</dx-codeblock>


[](id:step5)
### 5단계: 비디오 스트림 재생

#### 1. 재생 시작 및 중지(startRemoteView + stopRemoteView)
startRemoteView를 호출하여 원격 사용자의 비디오 이미지를 재생할 수 있지만 사용자의 비디오 이미지를 전달하는 렌더링 컨트롤로 SDK에 view 객체를 전달한 후에만 가능합니다.

startRemoteView의 첫 번째 매개변수는 원격 사용자의 userId, 두 번째는 사용자의 스트림 유형, 세 번째는 전달할 view 객체입니다. 여기서 두 번째 매개변수 streamType에는 세 가지 유효한 값이 있습니다.:
- TRTCVideoStreamTypeBig : 사용자의 기본 스트림 이미지로, 일반적으로 사용자의 카메라 이미지를 전송하는 데 사용됩니다.
- TRTCVideoStreamTypeSub : 사용자의 서브 스트림 이미지로, 일반적으로 사용자의 화면 공유 이미지를 전송하는 데 사용됩니다.
- TRTCVideoStreamTypeSmall :  사용자의 기본 스트림 이미지의 작은 저화질 이미지. 사용자가 ‘듀얼 스트림 모드(enableEncSmallVideoStream)’를 활성화한 후에만 원격 사용자의 저화질 이미지를 재생할 수 있습니다. 원본 품질의 기본 스트림과 낮은 품질의 작은 스트림은 동시에 재생할 수 없습니다.

stopRemoteView API를 호출하여 한 원격 사용자의 비디오 재생을 중지하거나 stopAllRemoteView API를 호출하여 모든 원격 사용자의 비디오 재생을 중지할 수 있습니다.

<dx-codeblock>
::: Android  java
// denny의 카메라(‘기본 스트림’) 이미지 재생
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，cameraView);
// denny의 화면 공유(‘서브 스트림’) 이미지 재생
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB，screenView);
// denny의 저화질 영상 재생 (원본 화질의 기본 스트림과 저화질의 작은 스트림은 동시에 재생할 수 없음)
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SMALL，cameraView);
// denny의 카메라 이미지 재생 중지
mCloud.stopRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，cameraView);
// 모든 원격 사용자의 비디오 이미지 재생 중지
mCloud.stopAllRemoteView();
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// denny의 카메라(‘기본 스트림’) 이미지 재생
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeBig view:cameraView];
// denny의 화면 공유(‘서브 스트림’) 이미지 재생
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeSub view:screenView];
// denny의 저화질 영상 재생 (원본 화질의 기본 스트림과 저화질의 작은 스트림은 동시에 재생할 수 없음)
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeSmall view:cameraView];
// denny의 카메라 이미지 재생 중지
[self.trtcCloud stopRemoteView:@"denny" streamType:TRTCVideoStreamTypeBig view:cameraView];
// 모든 원격 사용자의 비디오 이미지 재생 중지
[self.trtcCloud stopAllRemoteView];
:::
::: Windows  C++
// denny의 카메라(‘기본 스트림’) 이미지 재생
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeBig, (liteav::TXView)(hWnd));
// denny의 화면 공유(‘서브 스트림’) 이미지 재생
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeSub, (liteav::TXView)(hScreenWnd));
// denny의 저화질 영상 재생 (원본 화질의 기본 스트림과 저화질의 작은 스트림은 동시에 재생할 수 없음)
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeSmall, (liteav::TXView)(hWnd));
// denny의 카메라 이미지 재생 중지
trtc_cloud_->stopRemoteView("denny", liteav::TRTCVideoStreamTypeBig);
// 모든 원격 사용자의 비디오 이미지 재생 중지
trtc_cloud_->stopAllRemoteView();
:::
</dx-codeblock>

#### 2. 재생 매개변수 설정(updateRemoteView + setRemoteRenderParams)

updateRemoteView API를 호출하여 재생 중에 view 객체를 변경할 수 있습니다. 이것은 비디오 렌더링 컨트롤을 전환하는 데 유용합니다.
setRemoteRenderParams를 사용하여 비디오 이미지 채우기 모드, 회전 각도 및 미러 모드를 설정할 수 있습니다.
- 채우기 모드: 채우기 모드 또는 맞춤 모드를 사용할 수 있습니다. 두 모드에서 원본 이미지 종횡비는 변경되지 않고 유지되지만 차이점은 검은색 바가 있는지 여부입니다.
- 회전 각도: 회전 각도를 0, 90, 180, 270도로 설정할 수 있습니다.
- 미러 모드: 이미지를 수평으로 뒤집을지 여부를 나타냅니다.

<dx-codeblock>
::: Android  java
// denny의 기본 스트림 이미지를 miniFloatingView와 같은 작은 플로팅 창으로 전환
mCloud.updateRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，miniFloatingView);

// 원격 사용자 denny의 기본 스트림 이미지의 채우기 모드를 채우기로 설정하고 미러 모드 비활성화
TRTCCloudDef.TRTCRenderParams param = new TRTCCloudDef.TRTCRenderParams();
param.fillMode   = TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FILL;
param.mirrorType   = TRTCCloudDef.TRTC_VIDEO_MIRROR_TYPE_DISABLE;
mCloud.setRemoteRenderParams("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，param);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// denny의 기본 스트림 이미지를 miniFloatingView와 같은 작은 플로팅 창으로 전환
[self.trtcCloud updateRemoteView:miniFloatingView streamType:TRTCVideoStreamTypeBig forUser:@"denny"];
// 원격 사용자 denny의 기본 스트림 이미지의 채우기 모드를 채우기로 설정하고 미러 모드 비활성화
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode     = TRTCVideoFillMode_Fill;
param.mirrorType   = TRTCVideoMirrorTypeDisable;
[self.trtcCloud setRemoteRenderParams:@"denny" streamType:TRTCVideoStreamTypeBig params:param];
:::
::: Windows  C++
// denny의 기본 스트림 이미지를 다른 창으로 전환(새 창의 핸들이 newView라고 가정)
trtc_cloud_->updateRemoteView("denny", liteav::TRTCVideoStreamTypeBig, (liteav::TXView)(newView));

// 원격 사용자 denny의 기본 스트림 이미지의 채우기 모드를 채우기로 설정하고 미러 모드 비활성화
liteav::TRTCRenderParams param;
param.fillMode = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorType_Enable;
trtc_cloud_->setRemoteRenderParams("denny", TRTCVideoStreamTypeBig, param);
:::
</dx-codeblock>


[](id:step6)
### 6단계: 방에 있는 원격 사용자의 오디오/비디오 상태 가져오기

4단계와 5단계에서 원격 사용자의 오디오/비디오 재생을 제어할 수 있습니다. 그러나 정보가 충분하지 않으면 다음을 알 수 없습니다:
- 현재 방에는 어떤 사용자가 있습니까?
- 카메라와 마이크가 켜져 있습니까?

이 문제를 해결하려면 SDK에서 다음 이벤트 콜백을 수신 대기해야 합니다:
**오디오 상태 변경 알림(onUserAudioAvailable)**
원격 사용자가 마이크를 켜고 끌 때 onUserAudioAvailable(userId, boolean)을 수신하여 상태 변경을 가져올 수 있습니다.

**비디오 상태 변경 알림(onUserVideoAvailable)**
원격 사용자가 카메라를 켜고 끌 때 onUserVideoAvailable(userId, boolean)을 수신하여 상태 변경을 가져올 수 있습니다.
원격 사용자가 화면 공유를 활성화/비활성화할 때 onUserSubStreamAvailable(userId, boolean)을 수신하여 상태 변경을 가져올 수 있습니다.

**사용자 방 입장/퇴장 알림(onRemoteUserEnter/LeaveRoom)**
원격 사용자가 현재 방에 들어갈 때 onRemoteUserEnterRoom(userId)을 사용하여 사용자의 userId를 얻을 수 있습니다. 원격 사용자가 현재 방을 나갈 때 onRemoteUserLeaveRoom(userId, reason)을 사용하여 사용자의 userId와 퇴장 이유를 얻을 수 있습니다.
>! 구체적으로, onRemoteUserEnter/LeaveRoom은 앵커의 방 입/퇴장 알림만 받을 수 있습니다. 이는 방에 많은 수의 온라인 시청자가 있을 때 방 입/퇴장 알림을 자주 수신하는 문제를 방지합니다.

이러한 이벤트 콜백을 사용하면 다음 샘플 코드를 참고하여 방에 있는 사용자와 카메라와 마이크를 켰는지 여부를 알 수 있습니다. 여기서 mCameraUserList, mMicrophoneUserList 및 mUserList는 각각 다음 정보를 유지하는 데 사용됩니다.
- 방에 있는 사용자(앵커)
- 카메라를 켠 사용자
- 마이크를 켠 사용자

<dx-codeblock>
::: Android  java
// 원격 사용자의 비디오 상태 변경 사항을 가져오고 카메라를 켠 사용자 목록 업데이트(mCameraUserList)
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    available？mCameraUserList.add(userId) : mCameraUserList.remove(userId);
}

// 원격 사용자의 오디오 상태 변경 사항을 가져오고 마이크를 켠 사용자 목록 업데이트(mMicrophoneUserList)
@Override
public void onUserAudioAvailable(String userId, boolean available) {
    available？mMicrophoneUserList.add(userId) : mMicrophoneUserList.remove(userId);
}

// 원격 사용자의 방 입장 알림을 받고 원격 사용자 목록(mUserList) 업데이트
@Override
public void onRemoteUserEnterRoom(String userId) {
    mUserList.add(userId)；
}

// 원격 사용자의 퇴장 알림을 받고 원격 사용자 목록(mUserList) 업데이트
@Override
public void onRemoteUserLeaveRoom(String userId，int reason) {
    mUserList.remove(userId)；
}
:::
::: iOS&Mac  ObjC
// 원격 사용자의 비디오 상태 변경 사항을 가져오고 카메라를 켠 사용자 목록 업데이트(mCameraUserList)
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available{
    if (available)  {
        [mCameraUserList addObject:userId];
    } else {
        [mCameraUserList removeObject:userId];
    }
}

// 원격 사용자의 오디오 상태 변경 사항을 가져오고 마이크를 켠 사용자 목록 업데이트(mMicrophoneUserList)
- (void)onUserAudioAvailable:(NSString *)userId available:(BOOL)available{
    if (available)  {
        [mMicrophoneUserList addObject:userId];
    } else {
        [mMicrophoneUserList removeObject:userId];
    }
}

// 원격 사용자의 방 입장 알림을 받고 원격 사용자 목록(mUserList) 업데이트
- (void)onRemoteUserEnterRoom:(NSString *)userId{
    [mUserList addObject:userId];
}

// 원격 사용자의 퇴장 알림을 받고 원격 사용자 목록(mUserList) 업데이트
- (void)onRemoteUserLeaveRoom:(NSString *)userId reason:(NSInteger)reason{
    [mUserList removeObject:userId];
}
:::
::: Windows  C++
// 원격 사용자의 비디오 상태 변경 사항을 가져오고 카메라를 켠 사용자 목록 업데이트(mCameraUserList)
void onUserVideoAvailable(const char* user_id, bool available) {
    available ? mCameraUserList.push_back(user_id) : mCameraUserList.remove(user_id);
}

// 원격 사용자의 오디오 상태 변경 사항을 가져오고 마이크를 켠 사용자 목록 업데이트(mMicrophoneUserList)
void onUserAudioAvailable(const char* user_id, bool available) {
    available ? mMicrophoneUserList.push_back(user_id) : mMicrophoneUserList.remove(user_id);
}

// 원격 사용자의 방 입장 알림을 받고 원격 사용자 목록(mUserList) 업데이트
void onRemoteUserEnterRoom(const char* user_id) {
    mUserList.push_back(user_id);
}

// 원격 사용자의 퇴장 알림을 받고 원격 사용자 목록(mUserList) 업데이트
void onRemoteUserLeaveRoom(const char* user_id, int reason) {
    mUserList.remove(user_id);
}
:::
</dx-codeblock>


## 고급 가이드

### 1. 다른 ‘음소거’ 방법의 차이점은 무엇입니까?
완전히 다른 방식으로 작동하는 세 가지 음소거 방법이 있습니다.
- **방법1: 플레이어가 오디오 스트림 구독을 중지함**
원격 사용자 denny의 오디오 재생을 중지하려면 muteRemoteAudio("denny", true) 함수를 호출하면 SDK가 denny에서 오디오 데이터 스트림 가져오기를 중지합니다. 이 모드에서는 더 적은 트래픽이 사용됩니다. 그러나 SDK는 오디오 재생을 재개하기 위해 오디오 데이터 풀 프로세스를 다시 시작해야 하므로 ‘음소거’ 상태에서 ‘음소거 해제 상태’로 전환하는 속도가 느립니다.

- **방법2: 재생 볼륨 레벨을 0으로 조정**
음소거 상태를 더 빠르게 전환하려면 setRemoteAudioVolume("denny", 0)을 사용하여 원격 사용자 denny의 재생 볼륨 수준을 0으로 설정할 수 있습니다. 이 API는 네트워크 작업을 포함하지 않기 때문에 매우 빠르게 적용됩니다.

- **방법3: 원격 사용자 마이크 끄기**
본 문서에 설명된 모든 작업은 플레이어에서 수행되며 현재 사용자에게만 적용됩니다. 예를 들어 muteRemoteAudio("denny", true)를 호출하여 원격 사용자 denny를 음소거하면 방의 다른 사용자는 여전히 denny를 들을 수 있습니다.
denny의 소리를 완전히 ‘없애’려면 denny의 오디오 게시 동작에 영향을 주어야 합니다. 자세한 내용은 [오디오/비디오 스트림 게시](https://intl.cloud.tencent.com/document/product/647/47634)를 참고하십시오.
