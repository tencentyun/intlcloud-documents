## 적용 시나리오
TRTC는 4가지 입장 모드를 지원합니다. 그 중 영상 통화(VideoCall)와 음성 통화(AudioCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 [라이브 방송 모드](https://intl.cloud.tencent.com/document/product/647/35108)라고 부릅니다.
통화 모드의 TRTC는 단일 방에 최대 300명이 동시에 접속할 수 있으며 최대 50명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.

## 원리 분석
TRTC 클라우드 서비스는 '인터페이스 노드'와 '프록시 노드'라는 두 가지 서버 노드로 구성되어 있습니다.
- **인터페이스 노드**
최고 품질의 회로와 고성능 기기를 사용해 단말기 간의 저지연 마이크 연결 통화 처리에 적합하며, 시간당 단가가 비싼 편입니다.
- **프록시 노드**
일반 회로와 일반 성능 기기를 채택하여 동시 접속에 의한 풀 스트림 시청 수요 처리에 적합하며, 시간당 단가가 저렴한 편입니다.

통화 모드에서는 TRTC 방에 있는 모든 사용자가 인터페이스 노드에 할당되므로, 모두가 '호스트'인 셈입니다. 모든 사용자가 언제든지 발언(업스트림 동시 접속 최대 50회선 가능)할 수 있어 온라인 회의와 같은 시나리오에 적합합니다. 단, 방 하나의 수용 인원은 300명으로 제한됩니다.
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## 예시 코드
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example)에 로그인하여 본문과 관련된 예시 코드를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/cdef573133900a8dce22dcca5242fcfc.png)

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
      compile ’com.tencent.liteav:LiteAVSDK_TRTC:latest.release’
}
```
2. defaultConfig에서 App이 사용하는 CPU 구성을 지정합니다.
>?현재 TRTC SDK는 armeabi , armeabi-v7a, arm64-v8a를 지원합니다.
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
[ZIP 압축 프로그램](https://intl.cloud.tencent.com/document/product/647/34615)을 다운로드한 뒤 [빠른 통합(Android)](https://intl.cloud.tencent.com/document/product/647/35093)을 참고하여 SDK를 프로젝트에 통합하십시오.


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

1. [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35125) 인터페이스로 'TRTCCloud' 인스턴스를 생성합니다.
```
// trtcCloud 인스턴스 생성
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener(){
    // 콜백 프로세스
    ...
});
```
2. `setListener` 속성을 설정하고 이벤트 콜백을 등록한 다음, 관련 이벤트와 오류 공지를 리슨합니다.
```
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
| userId | 문자열 | 영어 알파벳 대소문자(a-z, A-Z)와 숫자(0-9), 언더바(_), 대시 부호(-)만 허용됩니다. 업무 실제 계정 시스템에 맞게 설정할 것을 권장합니다. | test_user_001 |
| userSig | 문자열 | userId를 기반으로 userSig를 계산할 수 있습니다. 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.| eJyrVareCeYrSy1SslI... |
| roomId | 숫자 | 숫자 유형의 방 번호입니다. 문자열 형식의 방 번호를 사용하려면 TRTCParams에서 strRoomId를 사용하십시오. | 29834 |

>! TRTC에서는 같은 userId 2개로 방에 동시 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.

[](id:step5)
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
    trtcParams.roomId = 908;
    trtcParams.userSig = usersig;
    mTRTCCloud.enterRoom(trtcParams, TRTC_APP_SCENE_VIDEOCALL);
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
>! 
>- 방 입장에 실패하면 SDK는 동시에 `onError` 이벤트를 콜백하며, `errCode`([에러 코드](https://intl.cloud.tencent.com/document/product/647/35130)), `errMsg`(에러 원인), `extraInfo`(보관 매개변수)를 반환합니다.
>- 이미 방에 입장한 경우 `exitRoom()`을 호출하여 해당 방에서 퇴장해야만 다른 방에 들어갈 수 있습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

[](id:step6)
### 6단계: 원격 멀티미디어 스트림 구독
SDK는 자동 구독 및 수동 구독 기능을 지원합니다.

#### 자동 구독 모드(기본값)
자동 구독 모드에서 특정 방에 입장하면 SDK가 방에 입장한 다른 사용자의 오디오 스트림을 자동 수신하여 '바로 재생' 수준으로 재생합니다.
1. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) 이벤트가 공지되고, SDK는 원격 사용자의 음성을 자동 재생합니다.
2. [muteRemoteAudio(userId, true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f)를 이용하여 특정 userId의 오디오 데이터를 차단할 수 있으며, [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba)를 통해 모든 원격 사용자의 오디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 사용자의 오디오 데이터를 불러오지 않습니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) 이벤트가 수신됩니다. 단, 이 때 SDK는 비디오 데이터 명령어 처리 방법을 수신하지 못해 비디오 데이터를 자동 처리하지 않습니다. [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)를 호출하여 원격 사용자의 비디오 데이터와 `view` 표시를 연결합니다.
4. [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f)를 통해 영상 화면의 표시 모드를 지정할 수 있습니다.
 - Fill 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
 - Fit 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a)를 이용하여 특정 userId의 비디오 데이터를 차단할 수 있으며, [stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127)를 통해 모든 원격 사용자의 비디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 원격 사용자의 비디오 데이터를 불러오지 않습니다.

```
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    TXCloudVideoView remoteView = remoteViewDic[userId];
    if (available)  {
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
2. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) 이벤트가 수신됩니다. 이 때 [muteRemoteAudio(userId, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f)를 호출하여 해당 사용자의 오디오 데이터를 수동 구독해야 SDK가 해당 사용자의 오디오 데이터를 수신한 뒤 디코딩하여 재생합니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) 이벤트가 수신됩니다. 이 때 [startRemoteView(userId, remoteView)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)를 호출하여 해당 사용자의 비디오 데이터를 수동 구독해야 SDK가 해당 사용자의 비디오 데이터를 수신한 뒤 디코딩하여 재생합니다.


[](id:step7)
### 7단계: 로컬의 멀티미디어 스트림 배포
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e)를 호출하여 마이크 수집을 활성화하고 수집된 오디오를 인코딩 및 발송합니다.
2. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116)를 호출하여 로컬 카메라를 활성화하고 수집된 화면 코덱을 발송할 수 있습니다.
3. [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d)를 호출하여 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
 - Fill 모드는 채우기를 의미합니다. 화면은 같은 비율로 확대되거나 잘릴 수 있지만, 검은 부분은 없습니다.
 - Fit 모드는 맞추기를 의미합니다. 화면은 해당 콘텐츠가 다 표시되도록 같은 비율로 축소될 수 있고, 검은 부분이 있을 수 있습니다.
4. [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) 인터페이스를 호출하면 로컬 비디오의 코드 매개변수를 설정할 수 있습니다. 해당 매개변수는 같은 방 사용자가 시청하는 화면의 [화질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.
```java
//예시 코드: 로컬 멀티미디어 스트림 배포
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, mLocalView);
mTRTCCloud.startLocalAudio();
```

[](id:step8)
### 8단계: 현재 방에서 퇴장하기

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


