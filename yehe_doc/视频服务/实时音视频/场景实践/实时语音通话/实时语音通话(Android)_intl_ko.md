## 효과












빠르게 음성 통화 기능을 실행해야 할 경우, 제공되는 Demo를 수정하여 적용하거나 TRTCCalling 모듈을 사용해 UI 인터페이스를 정의하십시오.

>! 이전에 제공한 TRTCAudioCall 모듈의 구버전은 [모듈 라이브러리](https://github.com/tencentyun/LiteAVClassic)로 이동되었습니다. TRTCCalling 모듈은 IM 신호 인터페이스를 사용하며, 구버전 모듈과는 호환되지 않습니다.

<span id="ui"> </span>

## Demo의 UI 인터페이스 재사용

<span id="ui.step1"></span>

### 1단계: 신규 애플리케이션 생성

1. TRTC 콘솔에 로그인하여 [Development Assistance]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 이름(예: `TestAudioCall`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

>! 이 기능은 동시에 Tencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 및 [실시간 통신 IM](https://intl.cloud.tencent.com/document/product/1047)를 기초로 한 PAAS 서비스로, TRTC 활성화 후 동기화해 실시간 IM 서비스를 활성화시킵니다. 실시간 통신 IM은 부가 서비스에 속하며, 자세한 과금 규정은 [실시간 통신 IM 가격 설명](https://intl.cloud.tencent.com/document/product/1047/34350)을 참조하십시오.

<span id="ui.step2"></span>

### 2단계: SDK와 Demo 소스 코드 다운로드

1. 커서를 상응하는 카드로 이동 후 [[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android)]를 클릭하여 Github(혹은 [ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip) 클릭)로 이동하여 SDK 및 Demo 소스 코드를 다운로드합니다.
   ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 확인할 수 있습니다.

<span id="ui.step3"></span>

### 3단계: Demo 프로그래밍 파일 설정

1. [2단계](#ui.step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
   - SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
   - SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.

![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)

4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!
>본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 본 방법에서의 SECRETKEY는 디컴파일로 크래킹되기 쉬워, 일단 키가 유출되면 해커가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 사용자의 App이 비즈니스 서버로 동적 UserSig 획득을 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166#Server)을 참조하십시오.

<span id="ui.step4"></span>

### 4단계: Demo 실행

Android Studio(3.5 버전 이상)를 사용하여 오픈 소스 프로그램인 `TRTCDemo`를 열고 [실행]을 클릭하면 됩니다.

<span id="ui.step5"></span>

### 5단계: Demo 소스 코드 수정

소스 코드 폴더 `trtccallingdemo` 에는 두 개의 하위 폴더 ui와 model이 포함되어 있으며, ui 폴더는 모두 인터페이스 코드입니다.

| 파일 및 폴더                     | 기능 설명                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| TRTCAudioCallActivity.java       | 음성 통화 메인 인터페이스를 표시하고, 이 인터페이스에서 통화 수락과 거절을 완료합니다. |
| TRTCCallingEntranceActivity.java | 대화상대를 선택에 사용하는 화면입니다. 이 화면을 통해 회원 가입한 사용자를 검색하고 통화 요청을 할 수 있습니다. |
| audiolayout                      | 통화 중 사용자 화면의 렌더링과 배치 로직에 사용합니다.                     |

<span id="model"> </span>

## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtccallingdemo/src/main/java/com/tencent/liteav/trtccalling) 폴더 `trtccallingdemo`에는 두 개의 하위 폴더 ui와 model이 포함되어 있으며, model 폴더에는 Tencent Cloud가 구현한 재사용 가능 오픈 소스 모듈 TRTCCalling이 포함되어 있습니다. `TRTCCalling.java` 파일에서 이 모듈이 제공하는 인터페이스 함수를 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

오픈 소스 컴포넌트 TRTCCalling을 사용해 UI 인터페이스를 실행하고, model 부분을 재사용해 직접 UI 부분을 실행할 수 있습니다.

<span id="model.step1"> </span>

### 1단계: SDK 통합

멀티미디어 통화 모듈 TRTCCalling은 TRTC SDK와 IM SDK에 종속됩니다. 다음 단계를 따라 두 SDK를 프로젝트로 통합할 수 있습니다.

**방법1: Maven 라이브러리 종속**

1. dependencies에서 TRTC SDK 및 IM SDK 종속을 추가합니다.
```
dependencies {
	complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    complie 'com.tencent.imsdk:imsdk:latest.release'

	// gson 리졸브를 사용하였으므로 google의 Gson 종속이 필요합니다.
    complie 'com.google.code.gson:gson:latest.release'
}
```
>? 2개의 SDK 제품의 최신 버전 넘버, [TRTC](https://github.com/tencentyun/TRTCSDK) 및 [실시간 통신 IM](https://github.com/tencentyun/TIMSDK)의 Github 첫 페이지에서 획득할 수 있습니다.

2. defaultConfig에서 앱이 사용하는 CPU 구성을 지정합니다.
```
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
}
```
3. [Sync Now]를 클릭해 SDK를 동기화합니다.
>?네트워크의 jcenter 연결에 문제가 없을 경우 SDK를 자동으로 다운로드하여 프로그램에 통합할 수 있습니다.


**방법2: 로컬 AAR 종속**
개발 환경에서 maven 라이브러리 액세스가 느릴 경우, ZIP을 다운로드하고 통합 문서를 따라 수동으로 프로그램에 통합할 수 있습니다.

| SDK      | 다운로드 페이지                                                     | 통합 가이드                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [통합 문서](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK   | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [통합 문서](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>

### 2단계: 권한 및 난독화 규칙 설정

AndroidManifest.xml에서 App 권한을 설정합니다. SDK는 다음 권한이 필요합니다(6.0이상 Android 시스템의 필요 동향은 카메라 신청 및 스토리지 열람 권한).

```
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
```

proguard-rules.pro 파일에서 SDK 관련 사항을 비난독화 리스트에 추가합니다.

```
-keep class com.tencent.** { *; }
```

<span id="model.step3"> </span>

### 3단계: TRTCCalling 모듈 가져오기

다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.

```
trtccallingdemo/src/main/java/com/tencent/liteav/trtccalling/model 
```

<span id="model.step4"> </span>

### 4단계: 초기화 및 모듈 로그인

1. `TRTCCallingImpl.sharedInstance(context)`를 호출하여 컴포넌트 인스턴스를 획득합니다.
2. `login(SDKAppID, userId, userSig, callback)` 을 호출해 모듈 로그인을 완료합니다. 그 중 몇몇 주요 매개변수는 다음 표를 참조하십시오.
 <table>
<tr>
<th>매개변수 이름</th>
<th>역할</th>
</tr>
<tr>
<td>SDKAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 조회할 수 있습니다.</td>
</tr>
<tr>
<td>userId</td>
<td>현재 사용자의 ID, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다.</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명으로, 계산 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참조하십시오.</td>
</tr>
</table>
<pre>
// 초기화
sCall = TRTCCallingImpl.sharedInstance(context);
sCall.login(1400000123, "userA", "xxxx", new ActionCallback());
</pre>


<span id="model.step5"> </span>

### 5단계: 1v1 음성 통화 실현

1. 발신자: `TRTCCalling`의 `call()`을 호출해 통화 요청을 발신하고 사용자 ID(userid)와 통화 유형(type)을 전달합니다. 통화 유형 매개변수는 `TYPE_AUDIO_CALL`을 전달합니다.
2. 수신자: 수신자가 로그인 상태일 경우 `onInvited()`라는 이름의 이벤트 알림을 받습니다. 수신자가 로그인 상태가 아니어도 통화 요청을 받게 하려면 [오프라인 수신](#model.offline)을 참조하십시오.
3. 수신자: 통화 수신을 원할 경우 수신자는 `accept()` 함수를 호출하거나 `reject()`를 호출하여 통화를 거절할 수 있습니다.
4. 양측의 멀티미디어 터널 생성 완료 후에는 양측 모두 `onUserEnter()`라는 이름의 이벤트 알림을 받게 되며, 이는 양측이 통화에 입장했음을 의미합니다.

```
//1. 모듈 초기화
TRTCCalling sCall =  TRTCCallingImpl.sharedInstance(context);
//2. 리스너 등록
sCall.addDelegate(new TRTCCallingDelegate() {
    //...일부 리스너 코드 생략
    public void onInvited(String sponsor, final List<String> userIdList, boolean isFromGroup, int callType) {
        // sponsor로부터 통화 요청을 받고 이곳의 코드가 받기를 선택하더라도 reject()로 거절할 수 있습니다.
        sCall.accept();
    } 
});
//3. 모듈에 로그인 합니다. 로그인이 완료 되어야 모듈의 기타 기능 함수를 호출할 수 있습니다.
sCall.login(sdkappid, "aaa", usersig, new ActionCallback() {
    public void onSuccess() {
        //4. 이곳은 인스턴스 코드입니다. 컴포넌트 로그인에 성공한 후 사용자를 “aaa”로 호출, 유형은TYPE_AUDIO_CALL로 전달합니다.
        sCall.call("aaa", TRTCCalling.TYPE_AUDIO_CALL);
    }
});
```

<span id="model.step6"> </span>

### 6단계: 그룹 음성 통화 실현

1. 발신자: 다중 사용자 영상 통화 시 `TRTCCalling `의 `groupCall()` 함수를 호출하고 사용자 목록(userIdList), 통화 유형(type), IM 그룹 ID(groupId)에 전달해야 합니다. 그중, userIdList에는 반드시 매개변수를 입력해야 하며, 통화 유형에는 반드시 매개변수를 입력해 `TYPE_AUDIO_CALL`을 전달하고, groupId에서는 매개변수를 선택해야 합니다.
2. 수신자: `onInvited()` 이벤트 알림으로 이 요청을 수락할 수 있습니다.
3. 수신자: 이벤트 알림을 수신한 후 `accept()`를 호출해 통화를 수락할 수 있으며, `reject()`로 통화를 거절할 수도 있습니다.
4. 일정 시간(기본30s) 초과 시에도 응답이 없을 경우 수신자는 `onCallingTimeOut()` 이벤트 알림을, 발신자는 `onNoResp(String userId)` 이벤트 알림을 받게 됩니다. 통화 발신자가 여러 요청의 응답을 받지 못할 경우에는`hangup()`, 수신자들은 `onCallingCancel()` 이벤트 알림을 받습니다.
5. 현재 다중 사용자 통화를 나가야 할 경우 `hangup()`을 호출할 수 있습니다.
6. 통화 도중 사용자가 추가되거나 나갈 경우 다른 사용자는 모두 `onUserEnter()` 및 `onUserLeave()` 이벤트 알림을 받습니다.

>?인터페이스 `groupCall()`의 `groupID` 매개변수는 IM SDK상의 그룹 ID로, 해당 매개변수를 입력하는 경우 통화 요청 메시지가 그룹 정보 메시지를 통해 전송됩니다. 해당 메시지 전송 방식은 비교적 간단하면서 신뢰성이 높습니다. 입력하지 않는 경우 `TRTCCalling` 모듈이 개별 발송 방식을 사용하여 1개씩 통지합니다.

```
// 앞부분 생략...
// 발신이 필요한 사용자 목록 취합
List<String> callList = new ArrayList();
callList.add("bbb");
callList.add("ccc");
callList.add("ddd");
// 한 IM 그룹에 발송하지 않은 경우, groupId는 비워둘 수 있습니다.
sCall.groupCall(callList, TRTCCalling.TYPE_AUDIO_CALL, "");
```

<span id="model.offline"> </span>

### 7단계: 오프라인 통화 구현

>?서비스가 온라인 고객서비스 등 오프라인 수신 기능이 필요 없는 시나리오일 경우, 상술한 [1단계1](#model.step1) - [6단계](#model.step6) 연결을 완료하십시오. 하지만 서비스가 소셜 시나리오일 경우에는 오프라인 수신을 추천합니다.

IM SDK는 오프라인 푸시를 지원합니다. 하지만 Android의 각 휴대폰 벤더는 각자 오프라인 푸시 서비스를 지원하기 때문에 복잡도가 iOS 플랫폼보다 높아야 합니다. 상응하는 설정을 해야 사용 가능 표준에 도달할 수 있습니다.

1. 상응하는 벤더의 푸시 채널에 필요한 인증서 등을 신청하고 실시간 IM 콘솔에 설정하여 푸시 조건에 따라 인증서와 ID 등을 추가합니다. 자세한 작업 단계는 [실시간 통신 IM > 오프라인 푸시(Android)](https://intl.cloud.tencent.com/document/product/1047/34336)를 참조하십시오.
2. 현재 TRTCCallingImpl의 sendModel 신호 발송 함수 중 오프라인 발송 함수가 통합되어 있습니다. App의 오프라인 푸시를 설정하면 메시지 오프라인 푸시가 가능합니다.

<span id="api"> </span>

## 모듈 API 리스트

TRTCCalling 모듈의 API 인터페이스 리스트는 다음과 같습니다.

| 인터페이스 함수        | 인터페이스 기능                                                  |
| --------------- | --------------------------------------------------------- |
| addDelegate     | TRTCCalling 리스너를 추가하면 사용자는 해당 리스너를 통해 상태 공지를 받을 수 있습니다. |
| removeDelegate  | 리스너 제거                                                |
| destroy         | 인스턴스 폐기                                                 |
| login           | IM에 로그인합니다. 모든 기능은 먼저 로그인한 후 사용할 수 있습니다.                 |
| logout          | IM에서 로그아웃합니다. 로그아웃 후에는 발신 기능을 사용할 수 없습니다.                        |
| call            | C2C 통화에 초대합니다. 초대받은 사람은 onInvited 이벤트 공지를 받게 됩니다.         |
| groupCall       | IM 그룹 통화 요청, 요청 수신자는 onInvited 이벤트공지 수신            |
| accept          | 초대된 사용자 통화 수신                                      |
| reject          | 초대된 사용자 통화 거절                                      |
| hangup          | 통화 종료                                                  |
| startRemoteView | 원격 사용자의 카메라 데이터를 지정한 TXCloudVideoView로 렌더링합니다.    |
| stopRemoteView  | 원격 사용자의 카메라 데이터 렌더링을 중지합니다.                          |
| openCamera      | 카메라를 활성화하고 지정한 TXCloudVideoView로 렌더링합니다.            |
| closeCamera     | 카메라 끄기                                                |
| switchCamera    | 앞뒤 카메라 변경.                                           |
| setMicMute      | mic 음소거 여부                                             |
| setHandsFree    | 핸즈프리 활성화 여부                                             |
