## 효과
Tencent Cloud의 App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 인터랙션 마이크 연결, 호스트 PK, 저지연 시청, 댓글 자막 채팅 등과 같은 ILVB 시나리오의 TRTC 관련 기능을 체험할 수 있습니다.

비디오 ILVB 기능에 빠르게 액세스해야 하는 경우 Tencent Cloud에서 제공하는 App을 기반으로 직접 수정하거나 TRTCLiveRoom 컴포넌트로 사용자 정의 UI 인터페이스를 구현할 수도 있습니다.

[](id:DemoUI)
## App UI 인터페이스 재사용

[](id:ui.step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 지원] > [[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)]을 선택합니다.
2. 애플리케이션 이름(예: `TestLiveRoom`)을 입력한 후 [생성]을 클릭합니다.
3. [다운로드 완료, 다음 단계]를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/10479)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.


[](id:ui.step2)
### 2단계: App 소스 코드 다운로드
[TUILiveRoom](https://github.com/tencentyun/TUILiveRoom)을 클릭하여 이동하거나, 소스 코드를 Clone 혹은 다운로드 합니다.


[](id:ui.step3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>! 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)
### 4단계: App 실행
Android Studio(3.5 이후 버전)를 사용하여 소스 코드 프로젝트인 `TUILiveRoom`을 열고 [실행]을 클릭하면 즉시 해당 App이 디버깅됩니다.

[](id:ui.step5)
### 5단계: App 소스 코드 수정
소스 코드 Source 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더에는 인터페이스 코드가 포함되어 있습니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| anchor | 호스트 관련 UI 구현 코드. |
| audience | 시청자 관련 UI 구현 코드. |
| common | 범용 UI 컴포넌트 구현 코드. |
| widget       | 범용 컨트롤러.                           |



## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.

### 사용자 A
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 입장 후 [방 생성]을 클릭합니다.
3. 방 이름을 입력하고 [라이브 방송 시작]을 클릭합니다.

### 사용자 B
1. 사용자 이름을 입력합니다(**사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다**).
2. 사용자 A가 생성한 방 번호를 입력한 후 방 입장을 클릭합니다.<br>


>! 방 번호는 사용자 A의 방 상단에서 확인할 수 있습니다.



## 방 상태 수신&PK 목록 연결
다음과 같이 방 상태는 `LiveRoomManager`를 사용하여 수신할 수 있습니다.
<dx-codeblock>
::: java java
LiveRoomManager.getInstance().addCallback(new LiveRoomManager.RoomCallback() {
    /**
     * 방 생성
     * @param roomId
     * @param callback 내부 프로세스 결과 공지에 사용
     */
    @Override
    public void onRoomCreate(int roomId, final LiveRoomManager.ActionCallback callback) {
        // doSomething
    }

    /**
     * 방 폐기
     * @param roomId
     * @param callback 내부 프로세스 결과 공지에 사용
     */
    @Override
    public void onRoomDestroy(int roomId, final LiveRoomManager.ActionCallback callback) {
        // doSomething
    }
    
    /**
     * 방 리스트 획득
     * @param callback
     */
    @Override
    public void onGetRoomIdList(final LiveRoomManager.GetCallback callback) {
        // 방 리스트 획득은 사용자 점검을 통해 사용자 간의 PK에 사용합니다.
        if(callback != null) {
            if(success) {
                // 콜백 완료, 방 리스트 전송
                callback.onSuccess(roomList);
            } else {
                // 방 리스트 획득 실패
                callback.onError(code, message);
            }
        }
    }
});
:::
</dx-codeblock>
사용자의 편리한 액세스를 위해 Callback 방식으로 콜백을 진행합니다. 예를 들어, 방 리스트 획득 시 비동기화 작업을 진행해야 하는 경우 Callback 방식이 더 효율적입니다.


[](id:model)
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TUILiveRoom/tree/master/Android/Source/src/main/java/com/tencent/liteav/liveroom)의 Source 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며 model 폴더에는 재사용할 수 있는 오픈 소스 컴포넌트 TRTCLiveRoom이 포함되어 있습니다. `TRTCChatSalon.java` 파일에서 해당 컴포넌트가 제공하는 인터페이스 함수를 확인할 수 있으며 해당 인터페이스로 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)

[](id:model.step1)
### 1단계: SDK 통합
비디오 ILVB 컴포넌트 TRTCLiveRoom은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 두 개의 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: Maven 웨어하우스를 통한 종속**
1. dependencies에 TRTCSDK와 IMSDK의 종속 패키지를 추가합니다.
<dx-codeblock>
::: java java
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
:::
</dx-codeblock>
>?두 SDK의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK)의 Github 메인 페이지에서 가져올 수 있습니다.
2. defaultConfig에서 App이 사용하는 CPU 구성을 지정합니다.
<dx-codeblock>
::: java java
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
:::
</dx-codeblock>
3. [Sync Now]를 클릭하면 SDK가 자동으로 다운로드되고 프로그램에 통합됩니다.

**방법2: 로컬 AAR을 통한 종속**
maven 라이브러리 액세스가 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참조하여 프로젝트에 통합할 수 있습니다.
<table>
<tr>
<th>SDK</th>
<th>다운로드 페이지</th>
<th>통합 가이드</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">통합 가이드 문서</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">통합 가이드 문서</a></td>
</tr>
</table>

[](id:model.step2)
### 2단계: 권한 및 난독화 규칙 설정
AndroidManifest.xml에서 App 권한을 설정합니다. SDK에는 다음 권한(6.0 이후 버전 Android 시스템의 경우 카메라 및 스토리지 읽기 동적 권한 신청 필요)이 필요합니다.
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

proguard-rules.pro 파일에서 SDK 관련 유형을 비난독화 리스트에 추가합니다.
<dx-codeblock>
::: java java
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### 3단계: TRTCLiveRoom 컴포넌트 가져오기
다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.
<dx-codeblock>
::: java java
src/main/java/com/tencent/liteav/liveroom/model
:::
</dx-codeblock>

[](id:model.step4)
### 4단계: 컴포넌트 생성 및 로그인
1. sharedInstance 인터페이스를 호출하여 TRTCLiveRoom 컴포넌트의 인스턴스 객체를 생성합니다.
2. TRTCLiveRoomConfig 객체를 생성합니다. 해당 객체에서는 useCDNFirst와 CDNPlayDomain 속성을 설정할 수 있습니다.
 - useCDNFirst 속성: 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자의 CDN을 통한 시청을 의미하며 요금이 저렴하지만, 딜레이가 많이 발생합니다. false는 일반 시청자의 저지연 시청을 의미하며 요금이 CDN과 마이크 연결 요금의 중간이지만, 딜레이가 1s 이내로 제어됩니다.
 - CDNPlayDomain 속성: useCDNFirst를 true로 설정해야만 적용되며 CDN을 통해 시청하는 재생 도메인을 지정하는 데 사용합니다. 라이브 방송 콘솔에 로그인하여 [[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)] 페이지에서 설정할 수 있습니다.
3. `login` 함수를 호출해 컴포넌트에 로그인하고, 다음 표를 참조해 핵심 매개변수를 입력합니다.
 <table>
<tr>
<th>매개변수 이름</th>
<th>역할</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr>
<tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다. 사업체의 실제 계정 시스템에 맞게 설정할 것을 권장합니다.</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
</tr>
<tr>
<td>config</td>
<td>전역 설정 정보이니 로그인 시 초기화하십시오. 로그인 후에는 변경할 수 없습니다.<ul style="margin:0;">
<li>useCDNFirst 속성: 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자의 CDN을 통한 시청을 의미하며 요금이 저렴하지만, 딜레이가 많이 발생합니다. false는 일반 시청자의 저지연 시청을 의미하며 요금이 CDN과 마이크 연결 요금의 중간이지만, 딜레이가 1s 이내로 제어됩니다.</li>
<li>CDNPlayDomain 속성: useCDNFirst를 true로 설정해야만 적용되며 CDN을 통해 시청하는 재생 도메인을 지정하는 데 사용합니다. 라이브 방송 콘솔에 로그인하여 [<a href="https://console.cloud.tencent.com/live/domainmanage">도메인 관리</a>] 페이지에서 설정할 수 있습니다.</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>로그인 콜백이며, 성공 시 code는 0입니다.</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
//useCDNFirst: true는 일반 시청자의 CDN을 통한 시청을, false는 일반 시청자의 저지연 시청을 의미
//yourCDNPlayDomain: CDN을 통한 시청 시 설정하는 재생 도메인
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, yourCDNPlayDomain);
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

[](id:model.step5)
### 5단계: 호스트 방송 시작
1. 호스트는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트는 방송 시작 전에 `startCameraPreview`를 호출하여 카메라 미리보기를 활성화할 수 있으며 인터페이스에 뷰티 필터 조절 버튼 호출을 설정하고 `getBeautyManager`를 통해 뷰티 필터를 설정할 수 있습니다.
>?엔터프라이즈 버전 이외의 SDK는 얼굴 변경과 스티커 효과 등 고급 뷰티필터 기능을 지원하지 않습니다.
3. 호스트는 뷰티 필터 효과 조정 후, `createRoom` 을 호출하여 새로운 라이브 룸을 생성할 수 있습니다.
4. 호스트가 `startPublish` 를 호출해 푸시 스트리밍을 시작합니다. CDN 을 통한 시청을 지원하려면 login 시 전송되는 `TRTCLiveRoomConfig` 매개변수에서 `useCDNFirst` 와 `CDNPlayDomain` 을 지정하고 `startPublish` 에서 라이브 방송 풀 스트림용 streamID를 지정하십시오.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

<dx-codeblock>
::: java java
// 1. 호스트 닉네임 및 프로필 사진 설정
mLiveRoom.setSelfProfile("A", "your_face_url", null);

// 2. 호스트 방송 시작 전 미리보기 및 뷰티 필터 매개변수 설정
TXCloudVideoView view = new TXCloudVideoView(context);
parentView.add(view);
mLiveRoom.startCameraPreview(true, view, null);
mLiveRoom.getBeautyManager().setBeautyStyle(1);
mLiveRoom.getBeautyManager().setBeautyLevel(6);

// 3. 호스트 방 생성
TRTCLiveRoomDef.TRTCCreateRoomParam param = new TRTCLiveRoomDef.TRTCCreateRoomParam();
param.roomName = "테스트 방";
mLiveRoom.createRoom(123456789, param, new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. 호스트 푸시 스트림 활성화 및 CDN에 스트림 배포
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});
:::
</dx-codeblock>

[](id:model.step6)
### 6단계: 시청자 시청
1. 시청자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 시청자는 서비스 백엔드로부터 최신 라이브 룸 리스트를 획득합니다.
>?App에 있는 라이브 룸 리스트는 참고용입니다. 라이브 룸 리스트의 서비스 로직은 매우 다양하며 현재 Tencent Cloud는 라이브 룸 리스트 관리 서비스를 제공하지 않습니다. 라이브 룸 리스트는 직접 관리하시기 바랍니다.
3. 시청자가 `getRoomInfos`를 호출해 방의 세부 정보를 가져옵니다. 해당 정보는 호스트가 `createRoom`을 호출하여 라이브 룸 생성 시 설정한 간단한 설명 정보입니다.
>!라이브 룸 리스트에 포괄적인 정보가 충분히 포함되어 있다면 `getRoomInfos` 호출 관련 단계는 건너뛸 수 있습니다.
4. 시청자가 하나의 라이브 룸을 선택하고 `enterRoom`을 호출하여 방 번호를 입력하면 즉시 해당 방에 입장할 수 있습니다.
5. `startPlay`를 호출하고 호스트의 userId를 전송하여 재생을 시작합니다.
 - 라이브 룸 리스트에 호스트의 userId 정보가 포함되어 있는 경우, 시청자가 직접 `startPlay`를 호출하고 호스트의 userId를 전송하여 즉시 재생을 시작할 수 있습니다.
 - 방 입장 전 호스트 userId를 획득할 수 없는 경우, 시청자는 방 입장 후 `onAnchorEnter`의 이벤트 콜백을 수신하게 됩니다. 해당 콜백에 호스트의 userId 정보가 포함되어 있으므로 `startPlay`를 호출하면 즉시 재생됩니다. 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

<dx-codeblock>
::: java java
// 1. 서비스 백엔드에서 획득한 방 리스트가 roomList라고 가정할 경우
List<Integer> roomList = GetRoomList();

// 2. getRoomInfos 호출을 통해 방의 세부 정보 획득
mLiveRoom.getRoomInfos(roomList, new TRTCLiveRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCLiveRoomDef.TRTCLiveRoomInfo> list) {
        if (code == 0) {
            // 방의 세부 정보를 획득하면 호스트 리스트 페이지에 호스트 닉네임, 프로필 사진 등 관련 정보 표시 가능
        }
    }
})

// 3. 방 roomid 선택 후 입장
mLiveRoom.enterRoom(roomid, null);

// 4. 시청자가 호스트 입장 공지를 수신하면 재생 시작
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5. 시청자가 호스트 화면 재생
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>

[](id:model.step7)
### 7단계: 시청자와 호스트 마이크 연결
1. 시청자가 requestJoinAnchor를 호출하여 호스트에게 마이크 연결을 요청합니다.
2. 호스트가 TRTCLiveRoomDelegate#onRequestJoinAnchor(시청자의 마이크 연결 요청) 이벤트 공지를 수신합니다.
3. 호스트가 responseJoinAnchor를 호출하여 시청자의 마이크 연결 요청에 대한 수락 여부를 결정합니다.
4. 시청자가 `TRTCLiveRoomDelegate#responseCallback` 이벤트 공지를 수신합니다. 해당 공지에는 호스트가 처리한 결과가 포함되어 있습니다.
5. 호스트가 마이크 연결 요청을 수락하면 시청자는 `startCameraPreview`를 호출하여 로컬 카메라를 활성화하고 startPublish를 호출하여 시청자 푸시 스트리밍을 실행할 수 있습니다.
6. 호스트는 시청자 푸시 스트림 실행 공지 후 `TRTCLiveRoomDelegate#onAnchorEnter`(다른 채널의 멀티미디어 스트림 도착) 공지를 수신하며 해당 공지에는 시청자의 userId가 포함되어 있습니다.
7. 호스트가 startPlay를 호출하면 마이크가 연결된 시청자의 비디오 화면을 볼 수 있습니다.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

<dx-codeblock>
::: java java
// 1. 시청자가 마이크 연결 요청 발송
mLiveRoom.requestJoinAnchor(mSelfUserId + "님이 마이크 연결을 요청합니다.", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. 호스트가 시청자 요청 수락
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5. 시청자가 미리보기 실행 및 푸시 스트림 활성화
            mLiveRoom.startCameraPreview(true, view, null);
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2. 호스트가 마이크 연결 요청 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // 3. 상대방의 마이크 연결 요청 수락
        mLiveRoom.responseJoinAnchor(userInfo.userId, true, "마이크 연결 수락");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 6. 호스트가 마이크가 연결된 시청자의 마이크 켜짐 공지 수신
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7. 호스트가 시청자 화면 재생
        mLiveRoom.startPlay(userId, view, null);
    }
});
:::
</dx-codeblock>

[](id:model.step8)
### 8단계: 호스트 간의 PK
1. 호스트 A가 requestRoomPK를 호출하여 호스트 B에게 PK 요청을 발송합니다.
2. 호스트 B는 `TRTCLiveRoomDelegate onRequestRoomPK` 콜백 공지를 수신합니다.
3. 호스트 B는 `responseRoomPK`를 호출하여 호스트 A의 PK 요청에 대한 수락 여부를 결정합니다.
4. 호스트 B는 호스트 A의 요청을 수락한 후 `TRTCLiveRoomDelegate onAnchorEnter` 공지를 기다렸다가 `startPlay`를 호출하여 호스트 A를 표시합니다.
5. 호스트 A가 PK 요청 수락 여부에 대한 `responseCallback` 콜백 공지를 수신합니다.
6. 호스트 A의 요청이 수락되면 `TRTCLiveRoomDelegate onAnchorEnter` 공지를 기다렸다가 `startPlay`를 호출하여 호스트 B를 표시합니다.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

<dx-codeblock>
::: java java
// 호스트 A:
// 호스트 A가 12345 방 생성
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6. B의 방 입장 공지 수신
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 1. 호스트 A가 호스트 B에게 PK 요청 발송
mLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5. 수락 여부 콜백 수신
        if (code == 0) {
            // 사용자 수락
        } else {
            // 사용자 거부
        }
    }
});

// 호스트 B:
// 호스트 B가 54321 방 생성
mLiveRoom.createRoom(54321, param, null);

// 2. 호스트 B가 호스트 A의 메시지 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3. 호스트 B가 호스트 A의 요청 수락에 회답
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4. 호스트 B가 호스트 A의 방 입장 공지 수신 후, 호스트 A의 화면 재생
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>

[](id:model.step9)
### 9단계: 문자 채팅 및 댓글 자막 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
 IM의 백엔드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
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
- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
사용자 정의 메시지는 '좋아요' 메시지 발송과 같은 사용자 정의 신호 전송에 주로 사용됩니다.
<dx-codeblock>
::: java java// 발신 측: 사용자 정의 Cmd를 통해 댓글 자막과 '좋아요' 메시지 구분 가능
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
            Log.d(TAG, userInfo.userName + "님이 좋아합니다.");
        }
    }
});
:::
</dx-codeblock>
