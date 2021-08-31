## 효과

빠른 음성 통화 기능이 필요한 경우, Tencent Cloud가 제공하는 Demo를 기반으로 설정을 적합하게 수정하거나 TRTCCalling 모듈을 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

>! 이전에는 TRTCAudioCall 모듈이 제공되었으나, 구버전 모듈은 [모듈 라이브러리](https://github.com/tencentyun/LiteAVClassic)로 옮겨졌습니다. TRTCCalling 모듈은 IM 신호 인터페이스를 사용하여 구버전 모듈과 호환되지 않습니다.

[](id:ui)

## Demo UI 인터페이스 재사용

[](id:ui.step1)

### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후 [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예: TestAudioCall)을 입력한 후 [생성]을 클릭합니다.

>! 
해당 기능은 기본 PaaS 서비스인 Tencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [인스턴트 메시지 IM](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. 인스턴트 메시지 IM은 부가 서비스이며, 자세한 과금 규정은 [인스턴트 메시지 IM 요금 가이드](https://intl.cloud.tencent.com/document/product/1047/34350)를 참조하십시오.

[](id:ui.step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 수요에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

[](id:ui.step3)
### 3단계: Demo 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
3. 'GenerateTestUserSig.java' 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 지향의 인터페이스를 제공합니다. UserSig가 필요할 때 App에서 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

[](id:ui.step4)

### 4단계: Demo 실행

Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램인 `TRTCDemo`를 열고 [실행]을 클릭하면 Demo를 디버깅할 수 있습니다.

[](id:ui.step5)

### 5단계: Demo 소스 코드 수정

소스 코드 폴더 `trtccallingdemo`에는 두 개의 하위 폴더 ui와 model이 포함되어 있으며, ui 폴더는 모두 인터페이스 코드입니다.

| 파일 및 폴더                     | 기능 설명                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| TRTCAudioCallActivity.java       | 음성 통화의 메인 인터페이스입니다. 통화를 수신하거나 거부합니다. |
| TRTCCallingEntranceActivity.java | 대화 상대 선택 시 사용되는 인터페이스입니다. 등록된 사용자를 검색하고 통화를 요청할 수 있습니다. |
| audiolayout                      | 통화 중 사용자 화면의 렌더링과 레이아웃 로직에 사용합니다.                     |

[](id:model)

## 사용자 정의 UI 인터페이스 구현

[소스 코드] 폴더 `trtccallingdemo`에는 두 개의 하위 폴더 ui와 model이 있으며, model 폴더에는 Tencent Cloud가 구현한 재사용 가능 오픈 소스 모듈 TRTCCalling이 포함되어 있습니다. `TRTCCalling.java` 파일에서 이 모듈이 제공하는 인터페이스 함수를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

오픈 소스 모듈 TRTCCalling을 사용해 맞춤형 UI 인터페이스를 구현할 수 있습니다. 즉, model 부분만 재사용하여 UI 부분을 자체적으로 구현할 수 있습니다.

<span id="model.step1"></span>

### 1단계: SDK 통합

멀티미디어 통화 모듈 TRTCCalling은 TRTC SDK와 IM SDK에 종속되어 있습니다. 아래 절차에 따라 두 가지 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: Maven 라이브러리를 통한 종속**

1. dependencies에 TRTC SDK 및 IM SDK 종속을 추가합니다.
```
dependencies {
	complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    complie 'com.tencent.imsdk:imsdk:latest.release'

	// gson 리졸브를 사용하였으므로 google의 Gson 종속이 필요합니다.
    complie 'com.google.code.gson:gson:latest.release'
}
```
>?두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK) 및 [인스턴스 메시지 IM](https://github.com/tencentyun/TIMSDK)의 Github 첫 페이지에서 획득할 수 있습니다.

2. defaultConfig에서 App이 사용하는 CPU 구성을 지정합니다.
```
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
}
```
3. [Sync Now]를 클릭해 SDK를 동기화합니다.
>?네트워크의 jcenter 연결에 문제가 없을 경우 SDK가 자동으로 다운로드되어 프로그램에 통합됩니다.


**방법2: 로컬 AAR을 통한 종속**
개발 환경에서 maven 라이브러리 액세스가 느릴 경우, ZIP 패키지를 다운로드하고 통합 가이드 문서에 따라 수동으로 프로그램에 통합할 수 있습니다.

| SDK      | 다운로드 페이지                                                     | 통합 가이드                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK   | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)

### 2단계: 권한 및 난독화 규칙 설정

AndroidManifest.xml에서 App 권한을 설정합니다. SDK에는 다음 권한이 필요합니다(6.0 이상의 Android 시스템은 카메라 및 스토리지 읽기 동적 권한 신청 필요).

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

[](id:model.step3)

### 3단계: TRTCCalling 모듈 가져오기

다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.

```
trtccallingdemo/src/main/java/com/tencent/liteav/trtccalling/model 
```

[](id:model.step4)

### 4단계: 모듈 초기화 및 로그인

1. `TRTCCallingImpl.sharedInstance(context)`를 호출하여 모듈 인스턴스를 획득합니다.
2. `login(SDKAppID, userId, userSig, callback)`을 호출해 모듈에 로그인합니다. 주요 매개변수는 다음 테이블을 참조하십시오.
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
<td>현재 사용자의 ID, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시 부호(-), 언더바(_)만 허용됩니다.</td>
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


[](id:model.step5)

### 5단계: 1대1 음성 통화

1. 발신자: `TRTCCalling`의 `call()`을 호출하여 통화를 요청하고, 사용자 ID(userid)와 통화 유형(Type)을 전달합니다. 통화 유형 매개변수는 `TYPE_AUDIO_CALL`입니다.
2. 수신자: 수신자가 로그인 상태인 경우 `onInvited()`라는 이벤트 공지를 받게 됩니다. 수신자가 로그인 상태가 아니어도 통화 요청을 받게 하려면 [오프라인 수신](#model.offline)을 참조하십시오.
3. 수신자: 통화 수신을 원하는 경우 수신자는 `accept()` 함수를 호출할 수 있고, `reject()`를 호출하여 통화를 거부할 수도 있습니다.
4. 멀티미디어 터널이 구축되면 양측은 `onUserEnter()`라는 이벤트 공지를 받게 되며, 이는 양측이 통화에 입장했음을 의미합니다.

```
//1. 모듈 초기화
TRTCCalling sCall =  TRTCCallingImpl.sharedInstance(context);
//2. 리스너 등록
sCall.addDelegate(new TRTCCallingDelegate() {
    //...일부 수신 코드 생략
    public void onInvited(String sponsor, final List<String> userIdList, boolean isFromGroup, int callType) {
        // sponsor로부터 통화 요청을 받고 이 코드로 수신을 선택하더라도 reject()로 거부할 수 있습니다.
        sCall.accept();
    } 
});
//3. 모듈에 로그인합니다. 로그인이 완료되어야 모듈의 기타 기능 함수를 호출할 수 있습니다.
sCall.login(sdkappid, "aaa", usersig, new ActionCallback() {
    public void onSuccess() {
        //4. 이 부분은 인스턴스 코드입니다. 모듈에 로그인한 후 사용자 'aaa'를 호출하고 유형은 TYPE_AUDIO_CALL로 전달합니다.
        sCall.call("aaa", TRTCCalling.TYPE_AUDIO_CALL);
    }
});
```

<span id="model.step6"></span>

### 6단계: 그룹 음성 통화

1. 발신자: 그룹 영상 통화는 `TRTCCalling`의 `groupCall()` 함수를 호출하고 사용자 리스트(userIdList), 통화 유형(type), IM 그룹 ID(groupId)를 전달해야 합니다. userIdList와 통화 유형은 필수 입력 매개변수이며, 통화 유형을 `TYPE_AUDIO_CALL`로 전달해야 합니다. groupId는 옵션 매개변수입니다.
2. 수신자: `onInvited()` 이벤트 공지를 통해 이 요청을 받을 수 있습니다.
3. 수신자: 이벤트 공지를 받은 후 `accept()`로 통화를 수신하거나 `reject()`로 거부할 수 있습니다.
4. 일정 시간(기본 30s)이 지나도 응답이 없으면 수신자는 `onCallingTimeOut()` 이벤트 공지를, 발신자는 `onNoResp(String userId)` 이벤트 공지를 받게 됩니다. 다중 수신자가 모두 응답이 없을 경우 발신자는 `hangup()` 이벤트 공지를, 모든 수신자는 `onCallingCancel()` 이벤트 공지를 받게 됩니다.
5. 그룹 통화를 중단해야 할 경우 `hangup()`을 호출할 수 있습니다.
6. 통화 도중 사용자가 추가되거나 나갈 경우 다른 사용자는 모두 `onUserEnter()` 또는 `onUserLeave()` 이벤트 공지를 받게 됩니다.

>?인터페이스 `groupCall()`의 `groupID` 매개변수는 IM SDK 상의 그룹 ID로, 해당 매개변수를 입력할 경우 통화 요청 메시지가 그룹 메시지 시스템을 통해 전송됩니다. 해당 메시지 전송 방식은 간단하면서도 신뢰성이 높습니다. 입력하지 않는 경우 `TRTCCalling` 모듈이 개별 발송 방식을 사용하여 일일이 공지합니다.

```
// 앞부분 생략...
// 발신이 필요한 사용자 목록 취합
List<String> callList = new ArrayList();
callList.add("bbb");
callList.add("ccc");
callList.add("ddd");
// 한 IM 그룹에서 발송한 것이 아닌 경우, groupId는 비워둘 수 있습니다.
sCall.groupCall(callList, TRTCCalling.TYPE_AUDIO_CALL, "");
```

<span id="model.offline"></span>

### 7단계: 오프라인 수신

>?온라인 고객서비스 등 오프라인 수신 기능이 필요 없는 시나리오인 경우, [1단계](#model.step1)~[6단계](#model.step6)만 진행합니다. 소셜 시나리오에서는 오프라인 수신을 권장합니다.

IM SDK는 오프라인 푸시를 지원하지만, Android는 휴대폰 벤더마다 서로 다른 오프라인 푸시 서비스를 지원하므로 iOS 플랫폼보다 액세스가 복잡합니다. 따라서 사용 가능 기준을 충족하려면 해당하는 설정을 완료해야 합니다.

1. 해당하는 벤더의 푸시 채널에 필요한 인증서 등을 신청하고, 이를 인스턴스 메시지 IM 콘솔에 설정한 후 푸시 조건에 따라 인증서와 ID 등을 추가합니다. 자세한 작업 방법은 [인스턴스 메시지 IM > 오프라인 푸시(Android)](https://intl.cloud.tencent.com/document/product/1047/39156)를 참조하십시오.
2. 현재 TRTCCallingImpl의 sendModel 신호 발송 함수에는 오프라인 발송 함수가 통합되어 있습니다. App에서 오프라인 푸시를 설정하면 메시지를 오프라인 푸시할 수 있습니다.

[](id:api)

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
| groupCall       | IM 그룹 통화를 요청합니다. 요청 수신자는 onInvited 이벤트 공지를 받게 됩니다.            |
| accept          | 초대된 사용자 통화 수신                                      |
| reject          | 초대된 사용자 통화 거부                                      |
| hangup          | 통화 종료                                                  |
| startRemoteView | 원격 사용자의 카메라 데이터를 지정한 TXCloudVideoView로 렌더링합니다.    |
| stopRemoteView  | 특정 원격 사용자의 카메라 데이터 렌더링을 중지합니다.                          |
| openCamera      | 카메라를 활성화하고 지정한 TXCloudVideoView로 렌더링합니다.            |
| closeCamera     | 카메라 비활성화                                                |
| switchCamera    | 전면/후면 카메라 전환                                           |
| setMicMute      | mic 음소거 여부                                             |
| setHandsFree    | 핸즈프리 활성화 여부                                             |
