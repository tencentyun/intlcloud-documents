TRTCMeeting은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM) 서비스를 기반으로 구성되며, 다음 기능을 지원합니다.
- 호스트가 회의 방을 생성하고 참석자가 방 번호를 입력한 후 회의 참여.
- 참석자 간 화면 공유.
- 다양한 텍스트 메시지 및 사용자 정의 메시지 발송 지원.

TRTCMeeting은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [그룹 멀티미디어 방(Flutter)](https://intl.cloud.tencent.com/document/product/647/41945)을 참고하십시오.
- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 사용하는 저지연 화상 회의 컴포넌트입니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)의 MeetingRoom을 이용해 회의 중 채팅방 기능을 구현합니다.

[](id:TRTCMeeting)

## TRTCMeeting API 개요
### SDK 기본 인터페이스

| API        | 설명       |
|-----|-----|
| [sharedInstance](#sharedinstance) | 싱글톤 객체 가져오기.|
| [destroySharedInstance](#destroysharedinstance) | 싱글톤 객체 폐기.|
| [registerListener](#registerlistener) | 이벤트 리스너 설정.|
| [unRegisterListener](#unregisterlistener) | 이벤트 리스너 폐기.|
| [login](#login) | 로그인.|
| [logout](#logout)      | 로그아웃.|
| [setSelfProfile](#setselfprofile) | 개인 정보 수정.|

### 회의 방 관련 인터페이스

| API        | 설명       |
|-----|-----|
| [createMeeting](#createmeeting) | 회의 방 생성(호스트 호출).|
| [destroyMeeting](#destroymeeting) | 회의 방 폐기(호스트 호출).|
| [enterMeeting](#entermeeting) | 회의 방 입장(참석자 호출).|
| [leaveMeeting](#leavemeeting) | 회의 방 퇴장(참석자 호출).|
| [getUserInfoList](#getuserinfolist) | 방 안의 모든 참석자 리스트 가져오기, enterMeeting() 성공 후 호출해야만 유효.|
| [getUserInfo](#getuserinfo) | 방 안의 지정된 참석자 상세 정보 가져오기, enterMeeting() 성공 후 호출해야만 유효.|

### 원격 사용자 관련 인터페이스

| API        | 설명       |
|-----|-----|
| [startRemoteView](#startremoteview) | 지정된 참석자의 원격 비디오 화면 재생.|
| [stopRemoteView](#stopremoteview) | 지정된 참석자의 원격 비디오 화면 재생 중지.|
| [setRemoteViewParam](#setremoteviewparam) | 지정된 참석자의 원격 이미지 렌더링 매개변수 설정.|
| [muteRemoteAudio](#muteremoteaudio) | 지정된 참석자의 원격 오디오 음소거/음소거 해제.|
| [muteAllRemoteAudio](#muteallremoteaudio) | 모든 참석자의 원격 오디오를 음소거/음소거 해제.|
| [muteRemoteVideoStream](#muteremotevideostream) | 지정된 참석자의 원격 비디오 일시 정지/재개.|
| [muteRemoteVideoStream](#muteremotevideostream) | 모든 참석자의 원격 비디오 스트림 일시 정지/재개.|

### 로컬 비디오 작업 인터페이스

| API        | 설명       |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | 로컬 비디오 화면 미리보기 시작.|
| [stopCameraPreview](#stopcamerapreview) | 로컬 비디오 수집 및 미리보기 중지.|
| [switchCamera](#switchcamera) | 전면/후면 카메라 전환.|
| [setVideoEncoderParam](#setvideoencoderparam) | 비디오 인코더 관련 매개변수 설정.|
| [setLocalViewMirror](#setlocalviewmirror) | 로컬 화면 미리보기 모드 설정.|

### 로컬 오디오 작업 API

| API        | 설명       |
|-----|-----|
| [startMicrophone](#startmicrophone)     | 마이크 수집 시작 |
| [stopMicrophone](#stopmicrophone)      | 마이크 수집 종료 |
| [muteLocalAudio](#mutelocalaudio)      | 로컬 음소거 활성화/비활성화.|
| [setSpeaker](#setspeaker) | 스피커 혹은 핸드셋 활성화 설정.|
| [setAudioCaptureVolume](#setaudiocapturevolume) | 마이크 수집 음량 설정.|
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 재생 음량 설정.|
| [startAudioRecording](#startaudiorecording) | 녹음 시작.|
| [stopAudioRecording](#stopaudiorecording) | 녹음 중지.|
| [enableAudioVolumeEvaluation](#enableaudiovolumeevaluation) | 볼륨 알림 활성화.|

### 녹화 인터페이스

| API        | 설명       |
|-----|-----|
| [startScreenCapture](#startscreencapture) | 화면 공유 시작.|
| [stopScreenCapture](#stopscreencapture) | 화면 수집 중지.|
| [pauseScreenCapture](#pausescreencapture) | 화면 수집 일시 정지.|
| [resumeScreenCapture](#resumescreencapture) | 화면 수집 재개.|

### 관련 관리 객체 인터페이스 가져오기

| API        | 설명       |
|-----|-----|
| [getDeviceManager](#getdevicemanager) | 장치 관리 객체 [TXDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html) 가져오기.|
| [getBeautyManager](#getbeautymanager) | 뷰티 필터 관리 객체 [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html) 가져오기.|

### 메시지 발송 관련 API

| API        | 설명       |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | 회의 중 텍스트 메시지 발송, 일반적으로 채팅에 사용.|
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의 텍스트 메시지 발송.|

[](id:TRTCLiveRoomDelegate)
## TRTCLiveRoomDelegate API 개요
### 일반적인 이벤트 콜백

| API        | 설명       |
|-----|-----|
| [onError](#onerror) | 오류 콜백.|
| [onWarning](#onwarning) | 경고 콜백.|
| [onKickedOffline](#onkickedoffline) | 다른 사용자가 동일한 계정으로 로그인 시 강제 로그아웃.|

### 회의 방 이벤트 콜백

| API        | 설명       |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | 회의 방 폐기 콜백.|
| [onNetworkQuality](#onnetworkquality) | 네트워크 상태 콜백.|
| [onUserVolumeUpdate](#onuservolumeupdate) | 사용자 통화 음량 콜백.|

### 참석자 입장/퇴장 이벤트 콜백

| API        | 설명       |
|-----|-----|
| [onEnterRoom](#onenterroom) | 로컬 입장 콜백.|
| [onLeaveRoom](#onleaveroom) | 로컬 퇴장 콜백.|
| [onUserEnterRoom](#onuserenterroom) | 신규 참석자 입장 콜백.|
| [onUserLeaveRoom](#onuserleaveroom) | 참석자 퇴장 콜백.|

### 참석자 멀티미디어 이벤트 콜백

| API        | 설명       |
|-----|-----|
| [onUserAudioAvailable](#onuseraudioavailable) | 참석자 마이크 On/Off 콜백.|
| [onUserVideoAvailable](#onuservideoavailable) | 참석자 카메라 On/Off 콜백.|
| [onUserSubStreamAvailable](#onusersubstreamavailable) | 참석자 서브스트림 활성화/비활성화 콜백.|

### 메시지 이벤트 콜백

| API        | 설명       |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | 텍스트 메시지 수신 콜백.|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신 콜백.|

### 녹화 이벤트 콜백

| API        | 설명       |
|-----|-----|
| [onScreenCaptureStarted](#onscreencapturestarted) | 녹화 시작 콜백.|
| [onScreenCapturePaused](#onscreencapturepaused) | 녹화 일시 정지 콜백.|
| [onScreenCaptureResumed](#onscreencaptureresumed) | 녹화 재개 콜백.|
| [onScreenCaptureStoped](#onscreencapturestoped) | 녹화 중지 콜백.|

## SDK 기본 인터페이스
### sharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945) 싱글톤 객체를 가져옵니다.
```dart
static Future<TRTCMeeting> sharedInstance();
```

### destroySharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945) 싱글톤 객체를 폐기합니다.
```dart
static void destroySharedInstance();
```
>? 인스턴스 폐기 후에는 외부에 캐시된 TRTCMeeting 인스턴스를 재사용할 수 없으며, 다시 [sharedInstance](#sharedinstance)를 호출해 새로운 인스턴스를 가져와야 합니다.

### registerListener

이벤트 리스너를 설정하면 TRTCMeetingDelegate를 통해 [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945)의 다양한 상태 알림을 받을 수 있습니다.
```dart
void registerListener(MeetingListenerFunc func);
```
>? func는 TRTCMeeting의 프록시 콜백입니다.

### unRegisterListener

이벤트 리스너를 폐기합니다.
```dart
void unRegisterListener(MeetingListenerFunc func);
```

### login

로그인합니다.
```dart
Future<ActionCallback> login(int sdkAppId, String userId, String userSig);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| sdkAppId | int | TRTC 콘솔 >[[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]> 애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다.|
| userId | String | 현재 사용자 ID입니다. 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(\_)만 허용됩니다.|
| userSig | String | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 및 사용 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |

### logout

로그아웃합니다.
```dart
Future<ActionCallback> logout();
```

### setSelfProfile

개인 정보를 수정합니다.
```dart
Future<ActionCallback> setSelfProfile(String userName, String avatarURL);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userName | String | 사용자 닉네임.|
| avatarURL | String | 사용자 프로필 사진 주소.|

## 회의 방 관련 인터페이스
### createMeeting

회의를 생성합니다(호스트 호출).
```dart
Future<ActionCallback> createMeeting(int roomId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| roomId | int | 회의 방 식별 번호이며, 귀하가 자체적으로 할당 및 통합 관리합니다.|

호스트 정상 호출 프로세스는 다음과 같습니다. 
1. [호스트]가 `createMeeting()`을 호출하고 `roomId`를 전송하여 회의를 생성하면, 회의 방 생성 여부가 `ActionCallback` 을 통해 호스트에게 통지됩니다. 
2. [호스트]가 `startCameraPreview()`를 호출하여 카메라 미리보기를 시작할 때 뷰티 필터 매개변수를 조정할 수 있습니다.
3. [호스트]가 `startMicrophone()`을 호출해 마이크 수집을 시작합니다.

### destroyMeeting

회의 방을 폐기합니다(호스트 호출). 호스트는 회의 생성 후 해당 함수를 호출해 회의를 폐기할 수 있습니다.
```dart
Future<ActionCallback> destroyMeeting(int roomId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| roomId | int | 회의 방 식별 번호이며, 귀하가 자체적으로 할당 및 통합 관리합니다.|

### enterMeeting

회의 방에 입장합니다(참석자 호출).
```dart
Future<ActionCallback> enterMeeting(int roomId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| roomId | int | 회의 방 식별 번호.|

참석자의 회의 입장 정상 호출 프로세스는 다음과 같습니다. 
1. [참석자]가 `enterMeeting()` 을 호출하고 `roomId`를 전송하면 회의 방에 입장됩니다.
2. [참석자]가 `startCameraPreview()`를 호출해 카메라 미리보기를 시작하고 `startMicrophone()`을 호출해 마이크 수집을 시작합니다.
3. [참석자]가 `onUserVideoAvailable` 이벤트를 수신하면 `startRemoteView()`가 호출되고 참석자 `userId`가 전송되어 재생이 시작됩니다.

### leaveMeeting

회의 방에서 퇴장합니다(참석자 호출).
```dart
Future<ActionCallback> leaveMeeting();
```

### getUserInfoList

방 안의 모든 참석자 리스트를 가져옵니다. enterMeeting() 성공 후 호출해야만 유효합니다.
```dart
Future<UserListCallback> getUserInfoList(List<String> userIdList);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userIdList | List&lt;String&gt; | 가져와야 하는 userId 리스트.|

### getUserInfo

방 안의 지정된 참석자 세부 정보 정보를 가져옵니다. enterMeeting() 성공 후 호출해야만 유효합니다.
```dart
Future<UserListCallback> getUserInfo(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 지정된 참석자 ID.|

## 원격 사용자 관련 인터페이스
### startRemoteView

지정된 참석자의 원격 영상 화면을 재생합니다.
```dart
Future<void> startRemoteView(String userId, int streamType, int viewId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 지정된 참석자 ID.|
| streamType | int | 시청할 비디오 스트림 유형. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19)를 참고하십시오.|
| viewId | int | TRTCCloudVideoView에 의해 생성된 viewId.|

### stopRemoteView

지정된 참석자의 원격 영상 화면 재생을 중지합니다.
```dart
Future<void> stopRemoteView(String userId, int streamType);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 지정된 참석자 ID.|
| streamType | int | 시청할 비디오 스트림 유형. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19)를 참고하십시오.|

### setRemoteViewParam

지정된 참석자의 원격 이미지 렌더링 매개변수를 설정합니다.
```dart
Future<void> setRemoteViewParam(String userId, int streamType,
  {int fillMode, int rotation, int mirrorType});
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 지정된 참석자 ID.|
| streamType | int | 시청할 비디오 스트림 유형. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19)를 참고하십시오.|
| fillMode | int | 이미지 렌더링 모드. 채우기(기본값) 또는 맞추기 모드. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ae697c0f66077568d33d0996064776b50)를 참고하십시오.|
| rotation | int | 이미지의 시계 방향 회전. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ab3d380890a5e0b7b6a29bc5d0e58f8e8)를 참고하십시오.|
| mirrorType | int | 이미지 모드. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ae5d847e0006bf2cd689b1116721109ca)를 참고하십시오.|

### muteRemoteAudio

지정된 참석자의 원격 오디오를 음소거/음소거 해제합니다.
```dart
Future<void> muteRemoteAudio(String userId, bool mute);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 지정된 참석자 ID.|
| mute | boolean | true: 음소거, false: 음소거 해제.|

### muteAllRemoteAudio

모든 참석자의 원격 오디오를 음소거/음소거 해제합니다.
```dart
Future<void> muteAllRemoteAudio(bool mute);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| mute | boolean | true: 음소거, false: 음소거 해제.|

### muteRemoteVideoStream

지정된 참석자의 원격 비디오를 일시 정지/재개합니다.
```dart
Future<void> muteRemoteVideoStream(String userId, bool mute);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 지정된 참석자 ID.|
| mute | boolean | true: 일시 정지, false: 재개.|

### muteAllRemoteVideoStream

모든 참석자의 원격 비디오 스트림을 일시 정지/재개합니다.
```dart
Future<void> muteAllRemoteVideoStream(bool mute);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| mute | boolean | true: 일시 정지, false: 재개.|

## 로컬 비디오 작업 인터페이스
### startCameraPreview

로컬 비디오 화면 미리보기를 시작합니다.
```dart
Future<void> startCameraPreview(bool isFront, int viewId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| isFront | boolean | true: 전면 카메라, false: 후면 카메라.|
| viewId | int | TRTCCloudVideoView에 의해 생성된 viewId.|

### stopCameraPreview

로컬 비디오 수집 및 미리보기를 중지합니다.
```dart
Future<void> stopCameraPreview();
```

### switchCamera

전면/후면 카메라를 전환합니다.
```dart
Future<void> switchCamera(bool isFront);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| isFront | boolean | true: 전면 카메라, false: 후면 카메라.|

### setVideoEncoderParam

비디오 인코더의 관련 매개변수를 설정합니다.
```dart
Future<void> setVideoEncoderParam({
  int videoFps,
  int videoBitrate,
  int videoResolution,
  int videoResolutionMode,
});
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| videoFps | int | 비디오 수집 프레임 레이트.|
| videoBitrate | int | 비트 레이트. SDK는 타깃 비트 레이트에 따라 인코딩하며, 네트워크가 불안정한 상태에서만 자체적으로 비디오 비트 레이트를 줄입니다.|
| videoResolution | int | 비디오 해상도.|
| videoResolutionMode | int | 해상도 모드.|
>? 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam)를 참고하십시오.

### setLocalViewMirror

로컬 화면 미리보기 모드를 설정합니다.
```dart
Future<void> setLocalViewMirror(bool isMirror);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| isMirror | boolean | 이미지 미리보기 모드 활성화 여부. true: 활성화, false: 비활성화.|

## 로컬 오디오 작업 API
### startMicrophone

마이크 수집을 시작합니다.
```dart
Future<void> startMicrophone({int quality});
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| quality | int | 오디오 음질. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a4451651bf7fc810efc4400964c3c0408)를 참고하십시오.|

### stopMicrophone

마이크 수집을 중지합니다.
```dart
Future<void> stopMicrophone();
```

### muteLocalAudio

로컬 음소거를 활성화/비활성화합니다.
```dart
Future<void> muteLocalAudio(bool mute);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| mute | boolean | true: 음소거, false: 음소거 해제.|

### setSpeaker

스피커 또는 핸드셋을 활성화합니다.
```dart
Future<void> setSpeaker(bool useSpeaker);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| useSpeaker | boolean | true: 스피커, false: 핸드셋.|

### setAudioCaptureVolume

마이크 수집 볼륨을 설정합니다.
```dart
Future<void> setAudioCaptureVolume(int volume);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| volume | int | 수집 볼륨은 0 - 100으로 설정할 수 있으며 기본값은 100입니다.|

### setAudioPlayoutVolume

재생 볼륨을 설정합니다.
```dart
Future<void> setAudioPlayoutVolume(int volume);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| volume | int | 재생 볼륨은 0 - 100으로 설정할 수 있으며 기본값은 100입니다.|

### startAudioRecording

녹음을 시작합니다.
```dart
Future<int?> startAudioRecording(String filePath);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| filePath | String | 녹음 파일 저장 경로. 경로는 사용자가 지정해야 합니다. 경로가 존재하고 쓰기가 가능한지 확인하십시오. 경로는 파일 이름 및 형식 확장자가 정확해야 합니다. 형식 확장자는 녹음 파일의 형식을 결정합니다. 현재 지원되는 형식은 PCM, WAV 및 AAC입니다.|

### stopAudioRecording

녹음을 중지합니다.
```dart
Future<void> stopAudioRecording();
```

### enableAudioVolumeEvaluation

볼륨 알림을 활성화합니다.
```dart
Future<void> enableAudioVolumeEvaluation(int intervalMs);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| intervalMs | int | onUserVoiceVolume 콜백의 트리거 간격을 결정합니다. 단위는 ms, 최소 간격은 100ms입니다. 0보다 작거나 같으면 콜백이 비활성화됩니다. 300ms로 설정하는 것을 권장합니다.|

## 녹화 인터페이스
### startScreenCapture

화면 공유를 시작합니다.
```dart
Future<void> startScreenCapture({
  int videoFps,
  int videoBitrate,
  int videoResolution,
  int videoResolutionMode,
  String appGroup,
});
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| videoFps | int | 비디오 수집 프레임 레이트.|
| videoBitrate | int | 비트 레이트. SDK는 타깃 비트 레이트에 따라 인코딩하며, 네트워크가 불안정한 상태에서만 자체적으로 비디오 비트 레이트를 줄입니다.|
| videoResolution | int | 비디오 해상도.|
| videoResolutionMode | int | 해상도 모드.|
| appGroup | String | 이 매개변수는 iOS에서만 유효하며 Android 에서는 이 매개변수에 주목할 필요가 없습니다. 이 매개변수는 메인 App과 Broadcast가 공유하는 Application Group Identifier입니다.|
>? 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam)를 참고하십시오.

### stopScreenCapture

화면 수집을 중지합니다.
```dart
Future<void> stopScreenCapture();
```

### pauseScreenCapture

화면 수집을 일시 정지합니다.
```dart
Future<void> pauseScreenCapture();
```

### resumeScreenCapture

화면 수집을 재개합니다.
```dart
Future<void> resumeScreenCapture();
```

## 관련 관리 객체 인터페이스 가져오기
### getDeviceManager

장치 관리 객체 [TXDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html)를 가져옵니다.
```dart
getDeviceManager();
```

### getBeautyManager

뷰티 필터 관리 객체 [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html)를 가져옵니다.
```dart
getBeautyManager();
```

뷰티 필터 관리를 통해 다음 기능을 사용할 수 있습니다.
- '뷰티 필터 스타일', '미백', '안색 보정', '눈 크게', '갸름하게', 'V라인', '턱 조정', '얼굴 짧게', '코 작게', '반짝이는 눈', '치아 미백', '아래 눈꺼풀 조정', '주름 제거', '팔자 주름 제거' 등 뷰티 효과를 설정할 수 있습니다.
- '헤어 라인', '눈 간격', '눈 각도', '입 모양', '콧볼', '코 위치', '입술 두께', '얼굴형'을 조정할 수 있습니다.
- 얼굴 효과(소재) 등 동적 효과를 설정할 수 있습니다.
- 메이크업 효과를 추가합니다.
- 손 동작을 인식합니다.

## 메시지 발송 관련 인터페이스
### sendRoomTextMsg

회의 중 텍스트 메시지 발송, 일반적으로 채팅에 사용합니다.
```dart
Future<ActionCallback> sendRoomTextMsg(String message);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| message  | String   | 텍스트 메시지.|

### sendRoomCustomMsg

사용자 정의 텍스트 메시지를 발송합니다.
```dart
Future<ActionCallback> sendRoomCustomMsg(String cmd, String message);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| cmd | String | 명령어, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다.|
| message  | String   | 텍스트 메시지.|

## TRTCMeetingDelegate 이벤트 콜백
## 일반적인 이벤트 콜백
### onError

오류 콜백.
>? SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 따라 인터페이스를 통해 사용자에게 적절히 안내해야 합니다.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| errCode | int | 오류 코드.|
| errMsg | String | 오류 정보.|
| extraInfo | String | 확장 정보 필드는 각 오류 코드별 추가 정보를 제공하여 문제 확인에 도움을 줍니다.|

### onWarning

경고 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| warningCode | int | 오류 코드.|
| warningMsg | String | 경고 정보.|
| extraInfo | String | 확장 정보 필드는 각 오류 코드별 추가 정보를 제공하여 문제 확인에 도움을 줍니다.|

### onKickedOffline

다른 사용자가 동일한 계정으로 로그인하여 강제 로그아웃됩니다.

## 회의 방 이벤트 콜백
### onRoomDestroy

회의 방 폐기 콜백. 호스트가 퇴장하면 방 안에 있는 모든 사용자는 해당 알림을 받게 됩니다.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| roomId | String |회의 방 ID.|

### onNetworkQuality

네트워크 상태 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | 업스트림 네트워크 품질.|
| remoteQuality | List&lt;TRTCCloudDef.TRTCQuality&gt; | 다운스트림 네트워크 품질.|

### onUserVolumeUpdate

사용자 통화 볼륨 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userVolumes | List | 현재 대화 중인 모든 방 참석자의 볼륨 범위: 0 - 100.|
| totalVolume | int | 모든 원격 참석자의 총 볼륨 범위: 0 - 100.|

## 참석자 입장/퇴장 이벤트 콜백
### onEnterRoom

로컬 입장 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| result | int | 0보다 클 경우 입장 소요시간(ms)을 나타내며, 0보다 작을 경우 입장 오류 코드입니다.|

### onLeaveRoom

로컬 퇴장 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| reason | int | 퇴장 사유, 0: LeaveMeeting 호출한 자체 퇴장, 1: 서버에 의한 강제 퇴장, 2: 전체 회의 해산.|

### onUserEnterRoom

신규 참석자 입장 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 신규 입장 참석자의 사용자 ID.|

### onUserLeaveRoom

참석자 퇴장 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 퇴장한 참석자의 사용자 ID.|

## 참석자 멀티미디어 이벤트 콜백
### onUserAudioAvailable

참석자 마이크 활성화/비활성화 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId    | String | 사용자 ID.|
| available | boolean | true: 사용자가 마이크 켬, false: 사용자가 마이크 끔.|

### onUserVideoAvailable

참석자 카메라 활성화/비활성화 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId    | String | 사용자 ID.|
| available | boolean | true: 사용자가 카메라 켬, false: 사용자가 카메라 끔.|

### onUserSubStreamAvailable

참석자 서브 스트림 이미지 활성화/비활성화 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| userId    | String | 사용자 ID.|
| available | boolean | true: 사용자가 서브 스트림 켬, false: 사용자가 서브 스트림 끔.|

## 메시지 이벤트 콜백
### onRecvRoomTextMsg

텍스트 메시지 수신 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| message  | String   | 텍스트 메시지.|
| sendId | String | 발신자 ID.|
| userAvatar | String | 발신자 프로필 사진.|
| userName | String | 발신자 닉네임.|

### onRecvRoomCustomMsg

사용자 지정 메시지 수신 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| command | String | 명령어는 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다.|
| message  | String   | 텍스트 메시지.|
| sendId | String | 발신자 ID.|
| userAvatar | String | 발신자 프로필 사진.|
| userName | String | 발신자 닉네임.|

## 녹화 이벤트 콜백
### onScreenCaptureStarted

녹화 시작 콜백.

### onScreenCapturePaused

녹화 일시 정지 콜백.

### onScreenCaptureResumed

녹화 재개 콜백.

### onScreenCaptureStoped

녹화 중지 콜백.

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| reason | int  | 중지 사유. 0: 사용자 자체 중지, 1: 화면 창이 닫혀 중지됨.|
