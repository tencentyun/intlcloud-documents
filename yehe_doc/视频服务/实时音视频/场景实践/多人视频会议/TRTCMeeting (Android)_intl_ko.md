TRTCMeeting은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM) 서비스를 기반으로 구성되며, 다음 기능을 지원합니다.
- 호스트가 회의 방을 생성하고 참석자가 방 번호를 입력한 후 회의 참여.
- 참석자 간 화면 공유.
- 다양한 텍스트 메시지 및 사용자 정의 메시지 발송 지원.

TRTCMeeting은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [다중 사용자 화상 회의(Android)](https://intl.cloud.tencent.com/document/product/647/37283)를 참고하십시오.
- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 사용하는 저지연 화상 회의 컴포넌트입니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)의 MeetingRoom을 이용해 회의 중 채팅방 기능을 구현합니다.


<h2 id="TRTCMeeting">TRTCMeeting API 개요</h2>

### SDK 기본 함수

| API | 설명 |
|-----|-----|
| [sharedInstance](#sharedinstance) | 싱글톤 객체 가져오기. |
| [destroySharedInstance](#destroysharedinstance) | 싱글톤 객체 폐기. |
| [setDelegate](#setdelegate) | 이벤트 콜백 설정.|
| [setDelegateHandler](#setdelegatehandler) | 이벤트 콜백이 존재하는 스레드 설정. |
| [login](#login) | 로그인.|
| [logout](#logout) | 로그아웃.|
| [setSelfProfile](#setselfprofile) | 개인 프로필 정보 수정.|

### 회의 방 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [createMeeting](#createmeeting) | 회의 방 생성(호스트 호출).|
| [destroyMeeting](#destroymeeting) | 회의 방 폐기(호스트 호출).|
| [enterMeeting](#entermeeting) | 회의 방 입장(참석자 호출).|
| [leaveMeeting](#leavemeeting) | 회의 방 퇴장(참석자 호출).|

### 원격 사용자 관련 인터페이스
| API | 설명 |
|-----|-----|
| [getUserInfoList](#getuserinfolist) | 방 안의 모든 참석자 리스트 가져오기, enterMeeting() 성공 후 호출해야만 유효.|
| [getUserInfo](#getuserinfo) | 방 안의 지정된 참석자 상세 정보 가져오기, enterMeeting() 성공 후 호출해야만 유효.|
| [startRemoteView](#startremoteview) | 지정된 참석자의 원격 비디오 화면 재생.|
| [stopRemoteView](#stopremoteview) | 원격 비디오 화면 재생 중지. |
| [setRemoteViewFillMode](#setremoteviewfillmode) | 사용자 ID에 따라 원격 이미지 렌더링 모드 설정, |
| [setRemoteViewRotation](#setremoteviewrotation) | 원격 이미지의 시계 방향 회전 각도 설정. |
| [muteRemoteAudio](#muteremoteaudio) | 지정된 참석자 오디오 차단. |
| [muteRemoteVideoStream](#muteremotevideostream) | 지정된 참석자 비디오 스트림 차단. |

### 로컬 비디오 작업 인터페이스

| API | 설명 |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | 로컬 비디오 화면 미리보기 시작.|
| [stopCameraPreview](#stopcamerapreview) | 로컬 비디오 수집 및 미리보기 중지.|
| [switchCamera](#switchcamera) | 전면/후면 카메라 전환.|
| [setVideoResolution](#setvideoresolution) | 해상도 설정. |
| [setVideoFps](#setvideofps) | 프레임 레이트 설정.|
| [setVideoBitrate](#setvideobitrate) | 비트 레이트 설정.|
| [setLocalViewMirror](#setlocalviewmirror) | 로컬 화면 미리보기 모드 설정.|

### 로컬 오디오 작업 인터페이스

| API | 설명 |
|-----|-----|
| [startMicrophone](#startmicrophone) | 마이크 수집 시작.|
| [stopMicrophone](#stopmicrophone) | 마이크 수집 중지.|
| [setAudioQuality](#setaudioquality) | 오디오 품질 설정.|
| [muteLocalAudio](#mutelocalaudio) | 로컬 음소거 활성화.|
| [setSpeaker](#setspeaker) | 스피커 활성화 설정.|
| [setAudioCaptureVolume](#setaudiocapturevolume) | 마이크 수집 음량 설정.|
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 재생 음량 설정.|
| [startFileDumping](#startfiledumping) | 녹음 시작.|
| [stopFileDumping](#stopfiledumping) | 녹음 중지.|
| [enableAudioEvaluation](#enableaudioevaluation) | 음량 크기 알림 활성화.|

### 녹화 인터페이스

| API | 설명 |
|-----|-----|
| [startScreenCapture](#startscreencapture) | 화면 공유 시작. |
| [stopScreenCapture](#stopscreencapture) | 화면 수집 중지.|
| [pauseScreenCapture](#pausescreencapture) | 화면 공유 일시 정지.|
| [resumeScreenCapture](#resumescreencapture) | 화면 공유 재개.|

### 뷰티 필터 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | 뷰티 필터 관리 객체 [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager) 가져오기.|

### 공유 관련 인터페이스

| API | 설명 |
|-----|-----|
| [getLiveBroadcastingURL](#getlivebroadcastingurl) | CDN 공유 링크 가져오기.|

### 메시지 발송 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | 방 안에서 텍스트 메시지 발송, 일반적으로 채팅에 사용.|
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의(신호) 메시지 발송.|


<h2 id="TRTCMeetingDelegate">TRTCMeetingDelegate API 개요</h2>

### 범용 이벤트 콜백

| API | 설명 |
|-----|-----|
| [onError](#onerror) | 오류 콜백.|

### 회의 방 이벤트 콜백

| API | 설명 |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | 회의 방 폐기 콜백.|
| [onNetworkQuality](#onnetworkquality)     | 네트워크 상태 콜백.   |
| [onUserVolumeUpdate](#onuservolumeupdate) | 사용자 통화 음량 콜백.|

### 참석자 입장/퇴장 이벤트 콜백

| API | 설명 |
|-----|-----|
| [onUserEnterRoom](#onuserenterroom) | 새로운 참석자 입장 알림 수신.|
| [onUserLeaveRoom](#onuserleaveroom) | 참석자 퇴장 알림 수신.|

### 참석자 멀티미디어 이벤트 콜백

| API | 설명 |
|-----|-----|
| [onUserVideoAvailable](#onuservideoavailable) | 참석자 카메라 On/Off 알림.|
| [onUserAudioAvailable](#onuseraudioavailable) | 참석자 마이크 On/Off 알림.|


### 메시지 이벤트 콜백

| API | 설명 |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | 텍스트 메시지 수신.|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신.|

### 녹화 이벤트 콜백

| API                                                 | 설명           |
| --------------------------------------------------- | -------------- |
| [onScreenCaptureStarted](#onscreencapturestarted) | 녹화 시작 알림. |
| [onScreenCapturePaused](#onscreencapturepaused)   | 녹화 일시 정지 콜백. |
| [onScreenCaptureResumed](#onscreencaptureresumed) | 녹화 재개 콜백. |
| [onScreenCaptureStoped](#onscreencapturestoped)   | 녹화 중지 콜백. |

## SDK 기본 함수

[](id:sharedInstance)
### sharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283) 싱글톤 객체를 가져옵니다.
```java
 public static synchronized TRTCMeeting sharedInstance(Context context);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| context | Context | Android 컨텍스트로, 내부가 ApplicationContext로 전환되어 시스템 API 호출에 사용됩니다. |



### destroySharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283) 싱글톤 객체를 폐기합니다.
>?인스턴스 폐기 후에는 외부에 캐시된 TRTCMeeting 인스턴스를 다시 사용할 수 없으며, 다시 [sharedInstance](#sharedInstance)를 호출해 새로운 인스턴스를 가져와야 합니다.

```java
public static void destroySharedInstance();
```

### setDelegate

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283) 이벤트 콜백은 TRTCMeetingDelegate를 통해 [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283)의 다양한 상태에 대한 알림을 받아볼 수 있습니다.
```java
public abstract void setDelegate(TRTCMeetingDelegate delegate);
```

>?setDelegate는 TRTCMeeting의 콜백 프록시입니다.   

### setDelegateHandler

이벤트 콜백이 존재하는 스레드를 설정합니다.
```java
public abstract void setDelegateHandler(Handler handler);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| handler | Handler | TRTCMeeting 상의 다양한 상태 알림 콜백은 해당 handler를 통해 통지합니다. setDelegate와 함께 사용하지 마십시오. |

### login

로그인합니다.
```java
public abstract void login(int sdkAppId,
	 String userId, String userSig,
	 TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| sdkAppId | int |  TRTC 콘솔 >[[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]> 애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId | String | 현재 사용자 ID입니다. 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| userSig | String | Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |
| callback | ActionCallback | 로그인 콜백이며, 성공 시 code는 0입니다. |


### logout

로그아웃합니다.
```java
public abstract void logout(TRTCMeetingCallback.ActionCallback callback);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| callback | ActionCallback | 로그아웃 콜백이며, 성공 시 code는 0입니다. |

   

### setSelfProfile

개인 정보를 수정합니다.
```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userName | String | 닉네임. |
| avatarURL | String | 프로필 사진 주소. |
| callback | ActionCallback | 개인 정보 설정 콜백이며, 성공 시 code는 0입니다. |

   


## 회의 방 관련 인터페이스 함수
### createMeeting

회의를 생성합니다(호스트 호출).
```java
public abstract void createMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| roomId | int | 회의 방 식별 번호이며, 귀사에서 할당하고 통합 관리합니다. |
| callback | ActionCallback | 방 생성 결과 콜백이며, 성공 시 code는 0입니다. |

호스트 정상 호출 프로세스는 다음과 같습니다. 
1. [호스트]가 `createMeeting()`을 호출하여 회의를 생성하면, 회의 방 생성 여부가 ActionCallback을 통해 호스트에게 통지됩니다.
2. [호스트]가 `startCameraPreview()`를 호출하여 카메라 미리보기를 시작할 때 뷰티 필터 매개변수를 조정할 수 있습니다. 
3. [호스트]가 `startMicrophone()`을 호출해 마이크 수집을 시작합니다.

   

### destroyMeeting

회의 방을 폐기합니다(호스트 호출). 호스트는 회의 생성 후 해당 함수를 호출해 회의를 폐기할 수 있습니다.
```java
public abstract void destroyMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| roomId | int | 회의 방 식별 번호이며, 귀사에서 할당하고 통합 관리합니다. |
| callback | ActionCallback | 방 폐기 결과 콜백이며, 성공 시 code는 0입니다. |


### enterMeeting

회의 방에 입장합니다(참석자 호출).
```java
public abstract void enterMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| roomId | int | 회의 방 식별 번호입니다. |
| callback | ActionCallback | 방 입장 결과 콜백이며, 성공 시 code는 0입니다. |


참석자의 회의 입장 정상 호출 프로세스는 다음과 같습니다. 
1. [참석자]가 `enterMeeting`을 호출하고 roomId를 전달하면 회의 방에 입장합니다.
2. [참석자]가 `startCameraPreview()`를 호출해 카메라 미리보기를 시작하고 `startMicrophone()`을 호출해 마이크 수집을 시작합니다.
3. [참석자]가 `onUserVideoAvailable` 이벤트를 수신하면 `startRemoteView(userId)`를 호출하고 참석자 userId를 전달하면 재생이 시작됩니다.
   

### leaveMeeting

회의 방에서 퇴장합니다(참석자 호출).
```java
public abstract void leaveMeeting(TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| callback | ActionCallback | 방 퇴장 결과 콜백이며, 성공 시 code는 0입니다. |


## 원격 사용자 관련 인터페이스

### getUserInfoList

방 안의 모든 참석자 리스트를 가져옵니다. enterMeeting() 성공 후 호출해야만 유효합니다.


```java
public abstract void getUserInfoList(TRTCMeetingCallback.UserListCallback userListCallback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userListCallback | UserListCallback | 사용자 상세 정보 콜백. |


### getUserInfo

방 안의 지정된 참석자 상세 정보를 가져옵니다. enterMeeting() 성공 후 호출해야만 유효합니다.
```java
public abstract void getUserInfo(String userId, TRTCMeetingCallback.UserListCallback userListCallback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID.|
| userListCallback | UserListCallback | 사용자 상세 정보 콜백. |


### startRemoteView

지정된 참석자의 원격 비디오 화면을 재생합니다. `onUserVideoAvailable()`이 true로 콜백되면 해당 인터페이스를 호출합니다.
```java
public abstract void startRemoteView(String userId, TXCloudVideoView view, final TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 재생할 사용자 ID.|
| view | TXCloudVideoView | 비디오 화면 view 컨트롤러.|
| callback | ActionCallback | 작업 콜백.|

### stopRemoteView

원격 비디오 화면을 재생을 중지합니다. `onUserVideoAvailable()`이 false로 콜백되면 해당 인터페이스를 호출합니다.
```java
public abstract void stopRemoteView(String userId, final TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 재생을 중지할 사용자 ID.|
| callback | ActionCallback | 작업 콜백.|

### setRemoteViewFillMode

사용자 ID에 따라 원격 이미지 렌더링 모드를 설정합니다.
```java
public abstract void setRemoteViewFillMode(String userId, int fillMode);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID.|
| fillMode | int  | 채우기 또는 맞추기 모드, 기본값: 채우기(FILL). 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f)를 참고하십시오. |



### setRemoteViewRotation

원격 이미지의 시계 방향 회전 각도를 설정합니다.
```java
public abstract void setRemoteViewRotation(String userId, int rotation);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID. |
| rotation | int  | 시계 방향 회전 각도. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69)를 참고하십시오. |



### muteRemoteAudio

원격 오디오를 음소거합니다.
```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID. |
| mute | boolean | true: 음소거 켜기, false: 음소거 끄기.|

   

### muteRemoteVideoStream

지정된 참석자의 비디오 스트림을 차단합니다.
```java
public abstract void muteRemoteVideoStream(String userId, boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID. |
| mute | boolean | true: 차단, false: 차단 해제.|


​      

## 로컬 비디오 작업 인터페이스
### startCameraPreview

로컬 비디오 화면 미리보기를 시작합니다.
```java
public abstract void startCameraPreview(boolean isFront, TXCloudVideoView view);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| isFront | boolean | true: 전면 카메라, false: 후면 카메라. |
| view | TXCloudVideoView | 비디오 모니터를 탑재한 컨트롤러. |

   

### stopCameraPreview

로컬 비디오 수집 및 미리보기를 중지합니다.
```java
public abstract void stopCameraPreview();
```

   

### switchCamera

전면/후면 카메라를 전환합니다.
```java
public abstract void switchCamera(boolean isFront);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| isFront | boolean | 전면/후면 카메라를 전환합니다. true: 전면 카메라, false: 후면 카메라. |


### setVideoResolution

해상도를 설정합니다.

```java
public abstract void setVideoResolution(int resolution);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| resolution | int | 비디오 해상도, 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#aa3b72c532f3ffdf64c6aacab26be5f87)를 참고하십시오. |



### setVideoFps

프레임 레이트를 설정합니다.
```java
public abstract void setVideoFps(int fps);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| fps | int | 비디오에서 수집하는 프레임 레이트. |

>?[권장 설정값] 15fps 또는 20fps를 권장합니다. 5fps는 랙이 심하게 발생하며, 10fps 이하는 약간의 랙이 발생하고, 20fps 이상은 너무 높습니다(영화 프레임 레이트 24fps).


### setVideoBitrate

비트 레이트를 설정합니다.
```java
public abstract void setVideoBitrate(int bitrate);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| bitrate | int | 비트 레이트, SDK는 타깃 비트 레이트에 따라 인코딩하며, 네트워크가 불안정한 상태에서만 자체적으로 비디오 비트 레이트를 줄입니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html)를 참고하십시오. |

>? [권장 설정값] TRTCVideoResolution의 각 단계별 권장 최적 비트 레이트를 참고하고, 이를 기반으로 적합하게 높일 수 있습니다. 예를 들어 TRTC_VIDEO_RESOLUTION_1280_720의 권장 비트 레이트는 1200kbps이지만, 1500kbps로 설정하여 더 선명한 화면을 볼 수도 있습니다.



### setLocalViewMirror

로컬 화면 미리보기 모드를 설정합니다.
```java
public abstract void setLocalViewMirror(int type);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| type | int | 이미지 모드. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1)를 참고하십시오. |

## 로컬 오디오 작업 인터페이스

### startMicrophone

마이크 수집을 시작합니다.
```java
public abstract void startMicrophone();
```

### stopMicrophone

마이크 수집을 중지합니다.
```java
public abstract void stopMicrophone();
```

### setAudioQuality

오디오 품질을 설정합니다.
```java
public abstract void setAudioQuality(int quality);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| quality | int | 오디오 음질. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)를 참고하십시오. |


### muteLocalAudio

로컬 오디오를 음소거/음소거 취소합니다.
```java
public abstract void muteLocalAudio(boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| mute | boolean | 오디오를 음소거/음소거 취소합니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)를 참고하십시오. |



### setSpeaker

스피커를 활성화합니다.
```java
public abstract void setSpeaker(boolean useSpeaker);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| useSpeaker | boolean | true: 스피커 false: 헤드셋 |



### setAudioCaptureVolume

마이크의 수집 음량을 설정합니다.
```java
public abstract void setAudioCaptureVolume(int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| volume | int | 수집 음량으로, 0-100으로 설정할 수 있으며 기본 값은 100입니다. |


### setAudioPlayoutVolume

재생 음량을 설정합니다.
```java
public abstract void setAudioPlayoutVolume(int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| volume | int | 재생 음량으로, 0-100으로 설정할 수 있으며 기본 값은 100입니다. |


### startFileDumping

녹음을 시작합니다.
```java
public abstract void startFileDumping(TRTCCloudDef.TRTCAudioRecordingParams trtcAudioRecordingParams);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| trtcAudioRecordingParams | TRTCCloudDef.TRTCAudioRecordingParams | 녹음 매개변수. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams)를 참고하십시오. |

>? 해당 방법으로 호출하면 SDK에서 통화 중 모든 오디오(로컬 오디오, 원격 오디오, BGM 등 포함)를 하나의 파일로 녹음합니다. 방 입장 여부에 상관 없이 해당 인터페이스를 호출하면 모두 적용되며, exitMeeting 호출 시 녹음 중인 경우 녹음은 자동으로 중지됩니다.

### stopFileDumping

녹음을 중지합니다.
```java
public abstract void stopFileDumping();
```

### enableAudioEvaluation

음량 크기 알림을 활성화합니다.
```java
public abstract void enableAudioEvaluation(boolean enable);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| enable | boolean |  true: 활성화, false: 비활성화. |

>? 활성화하면 음량 크기값에 대한 SDK의 평가를 onUserVolumeUpdate에서 가져옵니다.

## 녹화 인터페이스
### startScreenCapture

화면 공유를 시작합니다.
```java
public abstract void startScreenCapture(TRTCCloudDef.TRTCVideoEncParam encParams, TRTCCloudDef.TRTCScreenShareParams screenShareParams);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| encParams | TRTCCloudDef.TRTCVideoEncParam | 화면 공유 설정 시 인코딩 매개변수입니다. 위의 권장 설정을 참고하십시오. encParams가 null인 경우, startScreenCapture 호출 전 인코딩 매개변수 설정이 적용됩니다. |
| screenShareParams | TRTCCloudDef.TRTCScreenShareParams | 화면 공유 특수 설정을 설정합니다. 시스템으로 인한 App 강제 종료를 방지하고 사용자 프라이버시 보호를 위해 floatingView 설정을 권장합니다. |

>? 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)를 참고하십시오.

### stopScreenCapture

화면 수집을 중지합니다.
```java
public abstract void stopScreenCapture();
```

### pauseScreenCapture

화면 공유를 일시 정지합니다.
```java
public abstract void pauseScreenCapture();
```

### resumeScreenCapture

화면 공유를 재개합니다.
```java
public abstract void resumeScreenCapture();
```

## 공유 인터페이스
### getLiveBroadcastingURL

CDN 공유 링크를 가져옵니다.
```java
public abstract String getLiveBroadcastingURL();
```

반환값 리스트

| 반환값 | 유형 | 의미 |
|-----|-----|-----|
| url  | String  | CDN 공유 링크. |

## 뷰티 필터 관련 인터페이스 함수
### getBeautyManager

뷰티 필터 관리 객체 [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)를 가져옵니다.
```java
public abstract TXBeautyManager getBeautyManager();
```

뷰티 필터 관리를 통해 다음 기능을 사용할 수 있습니다.
- '뷰티 필터 스타일', '미백', '안색 보정', '눈 크게', '갸름하게', 'V라인', '턱 조정', '얼굴 짧게', '코 작게', '반짝이는 눈', '치아 미백', '아래 눈꺼풀 조정', '주름 제거', '팔자 주름 제거' 등 뷰티 효과를 설정할 수 있습니다.
- '헤어 라인', '눈 간격', '눈 각도', '입 모양', '콧볼', '코 위치', '입술 두께', '얼굴형'을 조정할 수 있습니다.
- 얼굴 효과(소재) 등 동적 효과를 설정할 수 있습니다.
- 메이크업 효과를 추가합니다.
- 손 동작을 인식합니다.


## 메시지 발송 관련 인터페이스 함수
### sendRoomTextMsg

방 안에서 텍스트 메시지를 발송합니다.
```java
public abstract void sendRoomTextMsg(String message, TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| message | String | 텍스트 메시지. |
| callback | ActionCallback | 발송 결과 콜백.|

   

### sendRoomCustomMsg

사용자 정의 텍스트 메시지를 발송합니다.
```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCMeetingCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| cmd | String | 명령어. 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message | String | 텍스트 메시지. |
| callback | ActionCallback | 발송 결과 콜백.|

   

## TRTCMeetingDelegate 이벤트 콜백

## 범용 이벤트 콜백
### onError

오류 콜백.
>?SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 따라 적절한 인터페이스를 사용자에게 제시해야 합니다.

```java
void onError(int code, String message);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| code | int | 오류 코드. |
| message | String | 오류 정보. |



## 방 이벤트 콜백
### onRoomDestroy

방 폐기 콜백. 호스트가 퇴장하면 방 안에 있는 모든 사용자는 해당 알림을 받게 됩니다.
```java
void onRoomDestroy(String roomId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| roomId | String | 방 ID. |

### onNetworkQuality

네트워크 상태 콜백.
```java
 void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality, List<TRTCCloudDef.TRTCQuality> remoteQuality);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | 업스트림 네트워크 품질. |
| remoteQuality | List&lt;TRTCCloudDef.TRTCQuality&gt; | 다운스트림 네트워크 품질. |

>? 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b)를 참고하십시오.


### onUserVolumeUpdate

음량 크기 알림을 활성화하여 모든 참석자의 음량 크기를 통지합니다.
```java
void onUserVolumeUpdate(String userId, int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID. |
| volume | int | 음량 크기이며, 0-100으로 설정할 수 있습니다. |



## 참석자 입장/퇴장 이벤트 콜백
### onUserEnterRoom

새로운 참석자 입장을 통지합니다.
```java
void onUserEnterRoom(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 새로 방에 입장한 참석자의 사용자 ID. |


### onUserLeaveRoom

참석자의 퇴장을 통지합니다.
```java
void onUserLeaveRoom(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 퇴장한 참석자의 사용자 ID. |


## 참석자 멀티미디어 이벤트 콜백
### onUserVideoAvailable

참석자의 카메라 On/Off를 통지합니다.
```java
void onUserVideoAvailable(String userId, boolean available);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID. |
| available | boolean | true: 사용자가 카메라 켬, false: 사용자가 카메라 끔. |

   

### onUserAudioAvailable

참석자의 마이크 On/Off를 통지합니다.
```java
void onUserAudioAvailable(String userId, boolean available);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 사용자 ID. |
| available | boolean | true: 사용자가 마이크 켬, false: 사용자가 마이크 끔. |

   

## 메시지 이벤트 콜백
### onRecvRoomTextMsg

텍스트 메시지를 수신합니다.
```java
void onRecvRoomTextMsg(String message, TRTCMeetingDef.UserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| message | String | 텍스트 메시지.|
| userInfo | TRTCMeetingDef.UserInfo | 발신자 사용자 정보.|

   

### onRecvRoomCustomMsg

사용자 정의 메시지를 수신합니다.
```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCMeetingDef.UserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| cmd | String | 명령어, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다.|
| message | String | 텍스트 메시지.|
| userInfo | TRTCMeetingDef.UserInfo | 발신자 사용자 정보. |


## 녹화 이벤트 콜백

### onScreenCaptureStarted

녹화 시작을 통지합니다.

```java
void onScreenCaptureStarted();
```

### onScreenCapturePaused

녹화 일시 정지를 통지합니다.

```java
void onScreenCapturePaused();
```

### onScreenCaptureResumed

녹화 재개를 통지합니다.

```java
void onScreenCaptureResumed();
```

### onScreenCaptureStoped

녹화 중지를 통지합니다.

```java
void onScreenCaptureStopped(int reason);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | 중지 사유입니다. 0: 사용자가 중지, 1: 다른 애플리케이션으로 인한 강제 중지 |





