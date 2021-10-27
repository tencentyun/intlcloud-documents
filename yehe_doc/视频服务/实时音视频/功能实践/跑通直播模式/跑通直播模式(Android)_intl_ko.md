## 적용 시나리오
TRTC는 4가지 입장 모드를 지원합니다. 영상 통화(VideoCall), 음성 통화(VoiceCall)는 [통화 모드](https://intl.cloud.tencent.com/document/product/647/35103)라고 부르고, 비디오 ILVB(Live)와 오디오 ILVB(VoiceChatRoom)는 라이브 방송 모드라고 부릅니다.
라이브 방송 모드의 TRTC는 방 하나에 최대 10만 명이 동시 접속할 수 있으며 마이크 연결 딜레이 300ms 미만, 시청 딜레이 1000ms 미만, 매끄러운 마이크 켜짐/꺼짐 전환 기술을 갖추고 있습니다. 저지연 ILVB, 10만 명이 참여하는 인터랙션 강의, 비디오 소개팅, 온라인 교육, 원격 교육, 초대형 회의 등의 응용 시나리오에 적합합니다.

## 원리 분석
TRTC 클라우드 서비스는 '인터페이스 노드'와 '프록시 노드'라는 두 가지 서버 노드로 구성되어 있습니다.
-   **인터페이스 노드**
최고 품질의 회로와 고성능 기기를 사용해 단말기 간의 저지연 마이크 연결 통화 처리에 적합하며, 시간당 단가가 비싼 편입니다.
-   **프록시 노드**
이 노드는 일반 품질의 회로와 일반 성능의 기계를 사용해 동시 접속이 많은 풀 스트림 시청 수요 처리에 뛰어납니다. 단위 시간당 과금이 비교적 저렴합니다.

라이브 방송 모드에서 TRTC는 역할의 개념을 도입했습니다. 사용자는 '호스트'와 '시청자' 역할로 나뉘고, '호스트'는 인터페이스 노드에, '시청자'는 프록시 노드에 할당됩니다. 하나의 방에 들어가는 시청자 수의 최댓값은 10만 명입니다.
'시청자'가 마이크를 켜려면 먼저 역할 전환(switchRole)을 통해 '호스트'가 되어야만 발화할 수 있습니다. 역할 전환의 과정에서 사용자는 프록시 노드에서 인터페이스 노드로 마이그레이션되며, TRTC 고유의 저지연 시청 기술과 매끄러운 마이크 켜짐/꺼짐 전환 기술 덕분에 전체 전환 시간이 대폭 단축되었습니다.
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## 예시 코드
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example)에 로그인하여 본문과 관련된 예시 코드를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/959efe00790a0a2952f8837a48baec25.png)

>?Github 액세스 속도가 느리다면 [TXLiteAVSDK_TRTC_Android_latest.zip](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip)을 직접 다운로드 할 수도 있습니다.

## 작업 단계
[](id:step1)
### 1단계: SDK 통합
아래의 방법 중에서 하나를 택해 **TRTC SDK**를 프로젝트에 통합할 수 있습니다.
#### 방법1: 자동 로딩(aar)
TRTC SDK를 jcenter에 이미 배포했다면 gradle 자동 다운로드 설정을 통해 업데이트할 수 있습니다.
Android Studio를 사용해 통합이 필요한 SDK 프로그램(TRTC-API-Example는 이미 통합 완료, 참고용 예시 코드 제공 가능)을 연 후, 간단한 단계를 거쳐 `app/build.gradle` 파일을 수정하면 SDK 통합이 완료됩니다.

1. dependencies에서 TRTCSDK 종속을 추가합니다.
```
dependencies {
      compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. defaultConfig에서 앱이 사용하는 CPU 구성을 지정합니다.
>?현재 TRTC SDK는 armeabi, armeabi-v7a, arm64-v8a를 지원합니다.
>
```
 defaultConfig {
      ndk {
          abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
      }
  }
```
3. [Sync Now]를 클릭해 SDK를 동기화합니다.
 네트워크에서 jcenter 연결에 문제가 없으면 SDK는 자동으로 다운로드되어 프로그램에 통합됩니다.

#### 방법2: ZIP 패키지를 다운로드하여 수동으로 통합
[ZIP 압축 패키지](https://intl.cloud.tencent.com/document/product/647/34615)를 다운로드하고 [빠른 통합(Android)](https://intl.cloud.tencent.com/document/product/647/35093)을 참고하여 SDK를 프로세스에 통합할 수 있습니다.


[](id:step2)
### 2단계: App 권한 설정
`AndroidManifest.xml` 파일에 카메라, 마이크 및 네트워크 신청 권한을 추가합니다.

```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />

<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```


[](id:step3)
### 3단계: SDK 인스턴스 초기화 및 이벤트 콜백 수신

1. [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35125) 인터페이스를 사용해 `TRTCCloud` 인스턴스를 생성합니다.
 ```java
// trtcCloud 인스턴스 생성
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener());
 ```
2. `setListener` 속성을 설정하고 이벤트 콜백을 등록한 다음, 관련 이벤트와 오류 공지를 리슨합니다.
```java
// 오류 공지는 리스너가 필요하며, SDK가 계속해서 실행될 수 없음을 의미
@Override
public void onError(int errCode, String errMsg, Bundle extraInfo) {
    Log.d(TAG, "sdk callback onError");
    if (activity != null) {
        Toast.makeText(activity, "onError: " + errMsg + "[" + errCode+ "]" , Toast.LENGTH_SHORT).show();
        if (errCode == TXLiteAVCode.ERR_ROOM_ENTER_FAIL) {
            activity.exitRoom();
        }
    }
}
```

[](id:step4)
### 4단계: 입장 매개변수 TRTCParams 어셈블리
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) 인터페이스를 호출할 경우, 핵심 매개변수 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)를 입력해야 합니다. 해당 매개변수가 포함하는 필수 입력 필드는 다음과 같습니다.

| 매개변수 이름 | 필드 유형 | 보충 설명 |입력 예시 |
|---------|---------|---------|---------|
| sdkAppId | 숫자 | 애플리케이션 ID, <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.|1400000123 |
| userId | 문자열 | 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(_)만 허용됩니다. |test_user_001 |
| userSig | 문자열 | userId를 기반으로 userSig를 계산할 수 있습니다. 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. | eJyrVareCeYrSy1SslI... |
| roomId | 숫자 | 문자열 타입의 방 번호 미지원이 기본값임. 이 타입으로 방 번호 설정 시 방 입장 속도 느려짐. 문자열 타입의 방 번호를 꼭 사용해야 할 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 문의 | 29834 |

>!
>- TRTC에서는 같은 userId 2개로 방에 동시 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

[](id:step5)
### 5단계: 호스트의 카메라 미리보기 및 마이크 음성 수집 활성화
1. 호스트는 [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116)를 호출하여 로컬 카메라 미리보기를 활성화할 수 있습니다. SDK가 시스템에 카메라 사용 권한을 요청하게 됩니다.
2. 호스트는 [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d)를 호출하여 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
 - Fill 모드는 '채우기'를 의미합니다. 화면은 같은 비율로 확대되거나 잘릴 수 있지만, 검은 부분은 없습니다.
 - Fit 모드는 '맞추기'를 의미합니다. 화면은 해당 콘텐츠가 다 표시되도록 같은 비율로 축소될 수 있고, 검은 부분이 있을 수 있습니다.
3. 호스트는 [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) 인터페이스를 호출하여 로컬 비디오의 인코딩 매개변수를 설정할 수 있습니다. 해당 매개변수는 방에 있는 다른 사용자가 사용자의 화면을 시청할 때 느끼는 [화질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.
4. 호스트는 [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e)를 호출하여 마이크를 활성화합니다. SDK가 시스템에 마이크 사용 권한을 요청하게 됩니다.

```java
//예시 코드: 로컬 멀티미디어 스트림 배포
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, localView);
// 로컬 비디오 인코딩 매개변수 설정
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_960_540;
encParam.videoFps = 15;
encParam.videoBitrate = 1200;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
mTRTCCloud.setVideoEncoderParam(encParam);
mTRTCCloud.startLocalAudio();
```

[](id:step6)
### 6단계: 호스트의 뷰티 필터 효과 설정

1. 호스트는 [getBeautyManager()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb)를 호출하여 뷰티 필터 설정 인터페이스[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)를 획득할 수 있습니다.
2. 호스트는 [setBeautyStyle()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10)을 호출하여 뷰티 필터 스타일을 설정할 수 있습니다.
 - Smooth: 매끈하게. SNS 인플루언서 느낌의 뚜렷한 효과를 줍니다.
 - Nature: 내추럴. 피부 보정 알고리즘은 얼굴의 디테일을 더 많이 유지하여 자연스러운 느낌을 줍니다.
 - Pitu: [엔터프라이즈 버전](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise)에서만 지원합니다.
3. 호스트 측에서 [setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#a3931ccd8fa54bb846783ab4d6ca2874b)을 호출하여 피부 보정 레벨을 설정합니다. 일반적으로 5로 설정합니다.
4. 호스트는 [setWhitenessLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#ab08c07ce725dbb8769b61fe0c76b0e95)을 호출하여 미백 레벨을 설정할 수 있습니다. 일반적으로 5로 설정합니다.


[](id:step7)
### 7단계: 호스트의 방 생성 및 푸시 스트리밍 시작
1. 호스트는 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)에서 필드 `role`을 **`TRTCCloudDef.TRTCRoleAnchor`**로 설정하여 현재 사용자의 역할이 호스트라는 것을 표시합니다.
2. 호스트는 [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)을 호출하여 TRTCParams 매개변수 필드 `roomId`의 값이 방 번호인 멀티미디어 방을 생성하고 **`appScene`** 매개변수를 지정할 수 있습니다.
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE: 비디오 ILVB 모드(이 문서에서 예시에 사용된 모드)
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM: 오디오 ILVB 모드
3. 방 생성에 성공하면 호스트는 멀티미디어 데이터의 인코딩과 전송 프로세스를 시작합니다. 이와 동시에, SDK는 [onEnterRoom(result)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) 이벤트를 콜백합니다. 매개변수 `result`가 0보다 크면 입장 성공이며, 해당 값은 입장에 걸리는 시간을 밀리초(ms) 단위로 나타냅니다. `result`가 0보다 작으면 입장 실패이며, 해당 값은 입장 실패의 에러 코드입니다.

```java
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId = userid;
    trtcParams.roomId = 908;
    trtcParams.userSig = usersig;
    mTRTCCloud.enterRoom(trtcParams, TRTCCloudDef.TRTC_APP_SCENE_LIVE);
}

@Override
public void onEnterRoom(long result) {
    if (result > 0) {
        toastTip("입장 성공, 총 소요 시간[\(result)]ms")
    } else {
        toastTip("입장 실패, 에러 코드[\(result)]")
    }
}
```

[](id:step8)
### 8단계: 시청자의 방 입장 후 라이브 방송 시청
1. 시청자는 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)의 필드 `role`을 **`TRTCCloudDef.TRTCRoleAudience`**로 설정하여 현재 사용자의 역할이 시청자라는 것을 표시합니다.
2. 시청자는 [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)을 호출하여 TRTCParams 매개변수 중 `roomId`가 가리키는 멀티미디어 방에 입장하고 **`appScene`** 매개변수를 지정할 수 있습니다.
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE: 비디오 ILVB 모드(이 문서에서 예시에 사용된 모드)
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM: 오디오 ILVB 모드
3. 호스트 화면 시청
 - 시청자가 사전에 호스트의 userId를 알고 있을 경우, 입장 성공 후 곧바로 호스트 `userId`를 사용해 [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)를 호출하여 호스트의 화면을 볼 수 있습니다.
 - 시청자는 입장 성공 후 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) 이벤트 공지를 받게 됩니다. 시청자가 사전에 호스트의 userId를 모를 경우, 콜백에서 확인한 호스트 `userId`를 사용해 [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)를 호출하여 호스트의 화면을 볼 수 있습니다.

[](id:step9)
### 9단계: 시청자와 호스트의 마이크 연결
1. 시청자는 [switchRole(TRTCCloudDef.TRTCRoleAnchor)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66)을 호출하여 역할을 호스트(TRTCCloudDef.TRTCRoleAnchor)로 전환합니다.
2. 시청자는 [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116)를 호출하여 로컬 화면을 활성화할 수 있습니다.
3. 시청자는 [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e)를 호출하여 마이크 음성 수집을 활성화합니다.

```java
//예시 코드: 시청자 마이크 켜짐
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAnchor);
mTrtcCloud.startLocalAudio();
mTrtcCloud.startLocalPreview(mIsFrontCamera, localView);

//예시 코드: 시청자 마이크 꺼짐
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAudience);
mTrtcCloud.stopLocalAudio();
mTrtcCloud.stopLocalPreview();
```


[](id:step10)
### 10단계: 호스트 간 크로스 룸 마이크 연결 PK

TRTC에서는 서로 다른 멀티미디어 룸의 두 호스트가 기존의 라이브 룸 시나리오에서 퇴장하지 않고도 '크로스 룸 통화' 기능을 통해 마이크를 연결하여 '크로스 룸 마이크 연결 PK'가 가능합니다.

1. 호스트 A는 [connectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) 인터페이스를 호출합니다. 현재 인터페이스 매개변수는 JSON 포맷입니다. 호스트 B의 `roomId`와 `userId`를 {"roomId": "978","userId": "userB"}` 포맷으로 만든 매개변수를 인터페이스 함수에 전달해야 합니다.
2. 크로스 룸에 성공하면 호스트 A는 [onConnectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) 이벤트 콜백을 받게 됩니다. 이와 동시에 두 라이브 방송 방에 있는 모든 사용자는 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05)과 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) 이벤트 공지를 받게 됩니다.
 예를 들어 방 '001'의 호스트 A가 `connectOtherRoom()`을 통해 방 '002'의 호스트 B와 크로스 룸 통화를 연결하면, 방 '001'의 사용자는 호스트 B의 `onUserVideoAvailable(B, true)` 콜백과 `onUserAudioAvailable(B, true)` 콜백을 받게 됩니다. 그리고 방 '002'의 사용자는 호스트 A의 `onUserVideoAvailable(A, true)` 콜백과 `onUserAudioAvailable(A, true)` 콜백을 받게 됩니다.
3. 두 방의 사용자는 [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)를 호출하여 상대 방 호스트의 화면을 볼 수 있게 되고, 소리는 자동으로 재생됩니다.

```java
//예시 코드: 크로스 룸 마이크 연결 PK
mTRTCCloud.ConnectOtherRoom(String.format("{\"roomId\":%s,\"userId\":\"%s\"}", roomId, username));
```

[](id:step11)
### 11단계: 현재 방 퇴장

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1)을 호출하여 퇴장합니다. SDK는 퇴장 시 카메라, 마이크 등 하드웨어 디바이스를 비활성화 및 릴리스해야 합니다. 따라서 퇴장은 금방 완료되는 동작이 아니며, [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) 콜백을 받아야만 퇴장이 완료되었다고 할 수 있습니다.

```java
// 퇴장 호출 후 onExitRoom 이벤트 콜백 대기
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

>! 애플리케이션에서 여러 개의 멀티미디어 SDK가 동시에 통합되었을 경우, `onExitRoom` 콜백을 받은 후 다른 멀티미디어 SDK를 재실행하십시오. 그렇지 않으면 하드웨어 점유율 문제가 나타날 수 있습니다.

