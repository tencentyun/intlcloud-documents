## 적용 시나리오
TRTC는 4가지 입장 모드를 지원합니다. 그중 영상 통화(VideoCall와 음성 통화(AudioCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 [라이브 방송 모드](https://intl.cloud.tencent.com/document/product/647/35108)라고 부릅니다.
통화 모드의 TRTC는 단일 방에 최대 300명이 동시에 접속할 수 있으며 최대 30명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.

## 원리 분석
TRTC 클라우드 서비스는 '인터페이스'와 '프록시' 라는 상이한 서버 노드로 구성됩니다.
- **인터페이스**
인터페이스 노드는 가장 우수한 회로와 고성능 기기를 채택하여 엔드 투 엔드의 마이크 통화 시 딜레이 시간이 짧고, 시간당 높은 과금이 적용됩니다.
- **프록시**
프록시 노드는 일반 회로와 일반 성능의 기기를 채택하여 동시 접속에 의한 시청 수요를 충족할 수 있으며, 시간당 낮은 과금이 적용됩니다.

통화 모드에서 TRTC 방에 입장한 모든 사용자는 인터페이스를 할당받습니다. 각 사용자 모두가 '호스트'로서 언제든지 발언할 수 있어(업스트림 동시 접속 최대 30개) 온라인 회의 등 시나리오의 사용에 적합합니다. 단, 단일 방 참가자 수는 300명으로 제한됩니다.


## 예시 코드
[Github]에 로그인하면 본 문서와 관련된 예시 코드를 받을 수 있습니다.
![](https://main.qcloudimg.com/raw/3ef83a68399c22ba0c1fbb079e3dfaf3.png)

>?Github 액세스가 느리다면 [TXLiteAVSDK_TRTC_Android_latest.zip](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip)을 직접 다운로드하십시오.

## 작업 순서
<span id="step1"> </span>
### 1단계: SDK 통합
다음의 방법으로 **TRTC SDK**를 프로젝트로 통합할 수 있습니다.
#### 방법1: 자동 로딩(aar)
TRTC SDK를 jcenter에 이미 배포했다면 gradle 자동 다운로드 설정을 통해 업데이트할 수 있습니다.
Android Studio에서 통합이 필요한 SDK 프로그램(TRTCSimpleDemo 통합 완료 시, 예시 코드 참고 가능)을 연 뒤 간단한 방법으로 'app/build.gradle' 파일을 수정하여 SDK를 통합할 수 있습니다.

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
3. [Sync Now]를 클릭하여 SDK를 동기화합니다.
 jcenter의 네트워크 연결이 정상이면, SDK가 자동 다운로드된 뒤 프로젝트로 통합됩니다.

#### 방법2: ZIP 다운로드 후 수동 통합
[ZIP 압축 프로그램](https://intl.cloud.tencent.com/document/product/647/34615)을 다운로드한 뒤 [빠른 통합(Android)](https://intl.cloud.tencent.com/document/product/647/35093)을 참조하여 SDK를 프로젝트에 통합하십시오.


<span id="step2"> </span>
### 2단계: App 권한 설정
'AndroidManifest.xml' 파일에서 카메라, 마이크, 네트워크의 신청 권한을 추가합니다.
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


<span id="step3"></span>
### 3단계: SDK 인스턴스 초기화 및 이벤트 리슨 콜백

1. [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35125) 인터페이스로 'TRTCCloud' 인스턴스를 생성합니다.
```
// trtcCloud 인스턴스 생성
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener(){
    // 콜백 프로세스
    ...
});
```
2. 'setListener' 속성을 설정하여 이벤트 콜백을 등록한 뒤 관련 이벤트와 오류 알림을 리슨합니다.
```
// 오류 알림 리스너, 오류 알림은 SDK가 실행을 지속할 수 없음을 뜻함.
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

<span id="step4"> </span>
### 4단계: 방 입장 매개변수 TRTCParams 어셈블리
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) 인터페이스 호출 시 핵심 매개변수[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59) 하나를 입력해야 합니다. 다음 필드는 매개변수 필수 작성 사항입니다.

| 매개변수 이름 | 필드 유형 | 보충 설명 | 작성 예시 | 
|---------|---------|---------|---------|
| sdkAppId | 숫자 | 애플리케이션 ID, <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID 조회 가능 |1400000123 | 
| userId  | 문자열 | 영문 알파벳 대소문자(a~z, A~Z), 숫자(0~9), 언더바, 하이픈만 입력 가능 |test_user_001 | 
| userSig | 문자열 | userId로 userSig 계산, 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166) 참조  | eJyrVareCeYrSy1SslI... |
| roomId | 숫자 | 숫자 유형의 방 번호입니다. 문자열 형식의 방 번호를 사용하려면 TRTCParams의 strRoomId를 사용하십시오. | 29834 |

>!TRTC에서는 2개의 동일한 userId로 동시에 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.

<span id="step5"> </span>
### 5단계: 방 생성 및 입장
1. [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)을 호출하여 TRTCParams 매개변수 'roomId'가 지정한 멀티미디어 방에 들어갈 수 있습니다. 해당 방이 존재하지 않는 경우 SDK는 필드 'roomId'를 방 번호로 하는 신규 방을 자동 생성합니다.
2. 응용 시나리오에 따라 적합한 **'appScene'** 매개변수를 설정하십시오. 잘못된 매개변수를 사용하는 경우 랙이 발생하거나 화면 해상도가 떨어질 수 있습니다.
 - 영상 통화는 'TRTC_APP_SCENE_VIDEOCALL'로 설정하십시오.
 - 음성 통화는 'TRTC_APP_SCENE_AUDIOCALL'로 설정하십시오.
3. 방에 입장하면 SDK는 'onEnterRoom(result)' 이벤트를 콜백합니다. 매개변수 'result'가 0보다 크면 방 입장 성공을 뜻하며, 세부 값은 방 입장 소요 시간으로, 단위는 밀리세컨드(ms)입니다. 'result'가 0보다 작으면 방 입장 실패를 뜻하며, 세부 값은 방 입장 실패 에러 코드입니다.

```
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId = userid;
    trtcParams.roomId = usersig;
    trtcParams.userSig = 908;
    mTRTCCloud.enterRoom(trtcParams, TRTC_APP_SCENE_VIDEOCALL);
}

@Override
public void onEnterRoom(long result) {
    if (result > 0) {
        toastTip("방 입장 성공, 총 소요 시간[\(result)]ms")
    } else {
        toastTip("방 입장 실패, 에러 코드[\(result)]")
    }
}
```
>! 
>- 방 입장에 실패하면 SDK는 동시에 `onError` 이벤트를 콜백하며, `errCode`([에러 코드](https://intl.cloud.tencent.com/document/product/647/35130)), `errMsg`(에러 원인), `extraInfo`(보관 매개변수)를 반환합니다.
>- 이미 방에 입장한 경우 `exitRoom()`을 호출하여 해당 방에서 퇴장해야만 다른 방에 들어갈 수 있습니다.

<span id="step6"> </span>
### 6단계: 원격 멀티미디어 스트림 구독
SDK는 자동 구독 및 수동 구독 기능을 지원합니다.

#### 자동 구독 모드(기본값)
자동 구독 모드에서 특정 방에 입장하면 SDK가 방에 입장한 다른 사용자의 오디오 스트림을 자동 수신하여 '바로 재생' 수준으로 재생합니다.
1. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) 이벤트가 공지되고, SDK는 원격 사용자의 음성을 자동 재생합니다.
2. [muteRemoteAudio(userId, true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f)를 이용하여 특정 userID의 오디오 데이터를 차단할 수 있으며, [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba)를 통해 모든 원격 사용자의 오디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 사용자의 오디오 데이터를 불러오지 않습니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) 이벤트가 공지됩니다. 단, 이때 SDK는 비디오 데이터 명령어 처리법을 수신받지 못해 비디오 데이터를 자동 처리하지 않습니다. [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)를 호출하여 원격 사용자의 비디오 데이터와 표시 'view'를 연결하십시오. 
4. [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f)를 통해 비디오 화면의 표시 모드를 지정하십시오.
 - Fill 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
 - Fit 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a)를 이용하여 특정 userID의 비디오 데이터를 차단할 수 있으며, [stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127)를 통해 모든 원격 사용자의 비디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 원격 사용자의 비디오 데이터를 불러오지 않습니다.

```
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    TXCloudVideoView remoteView = remoteViewDic[userId];
    if (available) {
        mTRTCCloud.startRemoteView(userId, remoteView);
        mTRTCCloud.setRemoteViewFillMode(userId, TRTC_VIDEO_RENDER_MODE_FIT);
    } else {
        mTRTCCloud.stopRemoteView(userId);
    }
}
```

>? 'onUserVideoAvailable()' 이벤트 콜백이 발생한 뒤 즉시 'startRemoteView()'를 호출하여 비디오 스트림을 구독하지 않으면 SDK는 5초 이내에 원격 비디오 데이터의 수신을 중지합니다.

#### 수동 구독 모드
[setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) 인터페이스를 이용해 SDK를 수동 구독 모드로 설정할 수 있습니다. 수동 구독 모드에서 SDK는 같은 방에 입장한 사용자의 멀티미디어 데이터를 자동 수신하지 않습니다. API 함수를 이용해 직접 트리거해야 합니다.

1. **방 입장 이전** [setDefaultStreamRecvMode(false, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) 인터페이스를 호출하면 SDK가 수동 구독 모드로 설정됩니다.
2. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) 이벤트가 공지됩니다. 이때 [muteRemoteAudio(userId, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f)를 호출하여 해당 사용자의 오디오 데이터를 수동 구독해야 SDK가 해당 사용자의 오디오 데이터를 수신한 뒤 디코딩하여 재생합니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) 이벤트가 공지됩니다. 이때 [startRemoteView(userId, remoteView)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)를 호출하여 해당 사용자의 비디오 데이터를 수동 구독해야 SDK가 해당 사용자의 비디오 데이터를 수신한 뒤 디코딩하여 재생합니다.


<span id="step7"> </span>
### 7단계: 로컬의 멀티미디어 스트림 배포
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e)를 호출하면 로컬 마이크 수집 기능이 실행되고, 수집한 음성을 인코딩한 뒤 송신할 수 있습니다.
2. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116)를 호출하면 로컬 카메라가 실행되고, 수집한 화면을 인코딩한 뒤 송신할 수 있습니다.
3. [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d)를 호출하면 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
 - Fill 모드는 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
 - Fit 모드는 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
4. [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) 인터페이스를 호출하면 로컬 비디오의 코드 매개변수를 설정할 수 있습니다. 해당 매개변수는 같은 방 사용자가 시청하는 화면의 [화질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.
```java
//예시 코드: 로컬의 멀티미디어 스트림 배포
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, mLocalView);
mTRTCCloud.startLocalAudio();
```

<span id="step8"> </span>
### 8단계: 현재 방에서 퇴장하기

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1)을 호출하여 방에서 퇴장합니다. 이때 SDK가 카메라와 마이크 등 기기를 차단 및 릴리스하기 때문에 [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) 콜백을 수신한 뒤에야 퇴장 처리됩니다.

```java
// 퇴장 호출 뒤 onExitRoom 이벤트 콜백 대기
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

>! App이 다수의 멀티미디어 SDK를 동시에 통합했다면 하드웨어 점유 상황을 고려하여 'onExitRoom' 콜백을 수신한 뒤 다른 멀티미디어 SDK를 실행하십시오.

