## 컴포넌트 개요

`TUILiveRoom`은 오픈 소스 비디오 라이브 스트리밍 시나리오 `UI` 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 `App`이 ‘인터랙티브 비디오 라이브 스트리밍’ 시나리오를 추가할 수 있습니다. `Android` 및 `iOS` 플랫폼용 소스 코드를 제공합니다. 기본 기능은 다음과 같습니다.
<table>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a1b4b04662bb342de1e7b713cb3f59ce.png"></td>
</tr>
</table>

[](id:model)

## 컴포넌트 통합
[](id:model.step1)
### 1단계: TUILiveRoom 컴포넌트 다운로드 및 가져오기
[Github](https://github.com/tencentyun/TUILiveRoom)로 이동하여 코드를 복제하거나 다운로드하고 `Android/Beauty`, `Android/Debug` 및 `Android/Source` 디렉터리를 프로젝트에 복사하고 다음 가져오기 작업을 완료합니다.

- 아래와 같이 `setting.gradle`에서 가져오기를 완료합니다.
```
include ':Beauty'
include ':Source'
include ':Debug'
```
- `app`의 `build.gradle` 파일에 `Source`에 대한 종속성을 추가합니다.
```
api project(":Source")
```
- 루트 디렉터리의 `build.gradle` 파일에 `TRTC SDK` 및 I`IM SDK`에 대한 종속성을 추가합니다.
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

[](id:model.step2)
### 2단계: 권한 요청 및 난독화 규칙 구성
1. AndroidManifest.xml에서 App에 대한 권한 요청을 구성합니다. SDK에는 다음 권한이 필요합니다(Android 6.0 이상에서는 런타임 시 카메라 및 저장소 읽기 권한 요청 필요).
<dx-codeblock>
::: java java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
:::
</dx-codeblock>
2. proguard-rules.pro 파일에서 SDK 관련 유형을 비난독화 리스트에 추가합니다.
<dx-codeblock>
::: java java
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### 3단계: 컴포넌트 초기화 및 로그인
<dx-codeblock>
::: java java
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
//useCDNFirst: true는 시청자가 CDN을 통해 라이브 스트림을 시청함을 의미하고 false는 시청자가 짧은 대기 시간 모드에서 라이브 스트림을 시청함을 의미
//yourCDNPlayDomain: CDN 라이브 스트리밍을 위한 재생 도메인 이름
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, CDNPlayDomain);
mLiveRoom.login(SDKAPPID, userId, userSig, config, 
    new TRTCLiveRoomCallback.ActionCallback() {
            @Override
            public void onCallback(int code, String msg) {
                if (code == 0) {
                    //로그인 성공
                }
            }
});
:::
</dx-codeblock>

**매개변수 설명:**
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 현재 사용자의 ID로, 문자(a-z 및 A-Z), 숫자(0-9), 하이픈(-) 및 언더바(\_)만 포함할 수 있는 문자열입니다. 사용자 계정 시스템과 일관성을 유지하는 것이 좋습니다.
- **userSig**: SDKAppId, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [데모 프로젝트](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.
- **config**: 전역 구성 정보입니다. 로그인 후에는 수정할 수 없으므로 로그인 중에 초기화하십시오.
- **useCDNFirst**: 청중이 라이브 스트림을 시청하는 방식을 지정합니다. true는 시청자가 CDN을 통해 라이브 스트림을 시청한다는 것을 의미하며, 이는 비용 효율적이지만 지연 시간이 높습니다. false는 청중이 저지연 모드에서 라이브 스트림을 시청한다는 것을 의미하며, 그 비용은 CDN 라이브 스트리밍과 공동 앵커링 사이에 있지만 지연 시간은 1초 이내입니다.
- **CDNPlayDomain**: CDN 라이브 스트리밍의 도메인 이름을 지정합니다. 이는 useCDNFirst가 true로 설정된 경우에만 적용됩니다. **CSS 콘솔** > [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에서 설정할 수 있습니다.
- **callback**: 로그인 콜백. 로그인에 성공하면 반환 code는 0입니다.



[](id:model.step4)
### 4단계: 인터랙티브 비디오 라이브 룸 구현
1. **앵커는 [TRTCLiveRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37333)을 통해 스트리밍을 시작합니다**.
<dx-codeblock>
::: java java
// 1.사용자 이름과 프로필 사진을 앵커로 설정
mLiveRoom.setSelfProfile("A", "your_face_url", null);

// 2.스트리밍 전에 카메라 미리보기를 활성화하고 뷰티 필터 설정
TXCloudVideoView view = new TXCloudVideoView(context);
parentView.add(view);
mLiveRoom.startCameraPreview(true, view, null);
mLiveRoom.getBeautyManager().setBeautyStyle(1);
mLiveRoom.getBeautyManager().setBeautyLevel(6);

// 3.방 생성
TRTCLiveRoomDef.TRTCCreateRoomParam param = new TRTCLiveRoomDef.TRTCCreateRoomParam();
param.roomName = "테스트 방";
mLiveRoom.createRoom(123456789, param, new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4.스트리밍을 시작하고 스트림을 CDN에 게시
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});
:::
</dx-codeblock>
2. **시청자는 [TRTCLiveRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37333)을 통해 시청합니다**.
```java
// 1. 서비스 백엔드에서 획득한 방 리스트가 roomList라고 가정할 경우
List<Integer> roomList = GetRoomList();

// 2. getRoomInfos 호출을 통해 방의 세부 정보 획득
mLiveRoom.getRoomInfos(roomList, new TRTCLiveRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCLiveRoomDef.TRTCLiveRoomInfo> list) {
        if (code == 0) {
            // 방의 세부 정보를 획득하면 앵커 리스트 페이지에 앵커 닉네임, 프로필 사진 등 관련 정보 표시 가능
        }
    }
})

// 3. 방 roomid 선택 후 입장
mLiveRoom.enterRoom(roomid, null);

// 4. 시청자가 앵커 입장 공지를 수신하면 재생 시작
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5. 시청자가 앵커 화면 재생
				//mTXCloudVideoView는 시청자를 위한 재생 view
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

3. **[TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37333)를 통해 관객과 앵커가 함께 공동 앵커링합니다.**
<dx-codeblock>
::: java java
// 1.시청자가 공동 앵커링 요청 발송
// LINK_MIC_TIMEOUT은 시간 초과 기간
mLiveRoom.requestJoinAnchor(mSelfUserId + "공동 앵커 요청", LINK_MIC_TIMEOUT
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4.앵커가 요청 수락
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5. 시청자가 카메라를 켜고 스트림을 푸시 시작
            mLiveRoom.startCameraPreview(true, view, null);
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2.앵커가 공동 앵커 요청 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // 3.앵커가 공동 앵커 요청 수락
        mLiveRoom.responseJoinAnchor(userInfo.userId, true, "공동 앵커에 동의");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 6.앵커는 공동 앵커 관객이 마이크를 켰다는 알림 수신
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7.앵커가 청중의 비디오 재생
        mLiveRoom.startPlay(userId, view, null);
    }
});
:::
</dx-codeblock>
4. **앵커는 [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37333)를 통해 PK합니다.**
<dx-codeblock>
::: java java
// 앵커 A:
// 12345 방 생성
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6.앵커 B의 진입에 대한 알림 수신
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 1.앵커 B에 PK 요청 보내기
mLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5.앵커 B가 요청을 수락했는지 여부에 대한 콜백 수신
        if (code == 0) {
            // 사용자 수락
        } else {
            // 사용자 거부
        }
    }
});

// 앵커 B:
// 54321 방 생성
mLiveRoom.createRoom(54321, param, null);

// 2.앵커 A의 요청 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3.앵커 A의 요청 수락
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4.앵커 A 진입 알림 수신 및 앵커 A 영상 재생
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>
5. **[TRTCLiveRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37333)를 통해 문자 채팅을 구현합니다.**
<dx-codeblock>
::: java java
// 발신측: 텍스트 메시지 발송
mLiveRoom.sendRoomTextMsg("Hello Word!", null);
// 수신측: 텍스트 메시지 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
	@Override
	public void onRecvRoomTextMsg(String roomId, 
			String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
			Log.d(TAG, userInfo.userName + "님이 발송한 메시지:" + message);
	}
});
:::
</dx-codeblock>
6. **[TRTCLiveRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37333)를 통해 화면 댓글을 구현합니다.**
<dx-codeblock>
::: java java
// 발신 측: 사용자 정의 Cmd를 통해 댓글 자막과 '좋아요' 메시지 구분 가능
// eg: "CMD_DANMU": 댓글 자막 메시지, "CMD_LIKE": '좋아요' 메시지
mTRTCChatSalon.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mLiveRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 수신측: 사용자 정의 메시지 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String roomId, String cmd, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // 댓글 자막 메시지 수신
            Log.d(TAG, userInfo.userName + "님이 발송한 댓글 자막 메시지:" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // '좋아요' 메시지 수신
            Log.d(TAG, userInfo.userName + "좋아요를 눌렀습니다!");
        }
    }
});
:::
</dx-codeblock>

## FAQ
요구 사항이나 피드백은 colleenyu@tencent.com으로 문의하십시오.
