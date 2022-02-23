## 효과
당사 App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 실시간 음성 및 영상 통화의 효과를 체험할 수 있습니다.
<table>
<tr>
   <th>발신자</th>
   <th>수신자</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>


>! 음성 및 영상 통화 기능을 빠르게 구현할 수 있도록 TUICalling 컴포넌트를 최적화하였습니다. 통화 UI는 TUICalling 컴포넌트 내부에 구현되어 있으므로 UI에 신경을 쓸 필요가 없습니다.

[](id:ui)

## App 실행 및 체험

[](id:ui.step1)

### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, **개발 지원>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. 애플리케이션 이름(예: `TestVideoCall`)을 입력한 후 **생성**을 클릭합니다.
3. **다운로드 완료, 다음 단계**를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.


[](id:ui.step2)
### 2단계: App 소스 코드 다운로드
[TUICalling](https://github.com/tencentyun/TUICalling)에서 소스 코드를 Clone 혹은 다운로드 합니다.

[](id:ui.step3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)
### 4단계: App 실행

Android Studio(버전 3.5 이상)를 사용하여 소스 프로젝트 `TUICalling`을 열고, **실행**을 클릭하여 App 디버깅을 시작합니다.



## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.

### 사용자 A
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 호출할 userId를 입력하고 검색을 클릭합니다.
3. **호출**을 클릭하고 **영상 통화**를 선택합니다. **수신자가 애플리케이션 로그인 상태가 아니면 호출에 실패할 수 있으니 확인하시기 바랍니다.**<br>

### 사용자 B
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 메인 페이지로 이동하여 전화 수신을 기다립니다.



[](id:model)
## 연결 프로세스

[소스 코드](https://github.com/tencentyun/TUICalling/tree/master/Android/Source/src/main/java/com/tencent/liteav/trtccalling) 폴더 `Source`에는 두 개의 하위 폴더 ui와 model이 있으며, model 폴더에는 Tencent Cloud가 외부에 공개한 오픈 소스 컴포넌트 TUICallingManager가 포함되어 있습니다.  `TUICalling.java`  파일에서 이 컴포넌트가 제공하는 인터페이스 함수를 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0de26d679e6e0dc1d9aeadb6dbf6f8aa.png)


오픈 소스 컴포넌트 TUICalling의 TUICallingManager를 사용하면, 복잡한 호출 UI 인터페이스 및 로직을 직접 구현하지 않고도 음성 및 영상 통화 기능을 쉽게 구현할 수 있습니다.

[](id:model.step1)
### 1단계: SDK 통합

음성 및 영상 통화 컴포넌트 TUICalling은 TRTC SDK와 IM SDK에 종속되어 있습니다. 아래 단계에 따라 두 가지 SDK를 프로젝트에 통합할 수 있습니다.

#### 방법1: Maven 라이브러리를 통한 종속

1. dependencies에 TRTCSDK와 IMSDK의 종속 패키지를 추가합니다.
<dx-codeblock>
::: java java
dependencies {
    compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    compile 'com.tencent.imsdk:imsdk:latest.release'

    // gson 리졸브를 사용하였으므로 google의 Gson 종속이 필요합니다.
    compile 'com.google.code.gson:gson:latest.release'
}
:::
</dx-codeblock>
>?두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK) 및 [IM](https://github.com/tencentyun/TIMSDK)의 Github 첫 페이지에서 획득할 수 있습니다.
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
3. **Sync Now**를 클릭해 SDK를 동기화합니다.
>?네트워크의 jcenter 연결에 문제가 없을 경우 SDK가 자동으로 다운로드되어 프로그램에 통합됩니다.


#### 방법2: 로컬 AAR을 통한 종속
개발 환경에서 Maven 라이브러리 액세스가 느릴 경우, ZIP 패키지를 다운로드하고 통합 가이드 문서에 따라 수동으로 프로그램에 통합할 수 있습니다.

| SDK      | 다운로드 페이지                                                     | 통합 가이드                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK   | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)

### 2단계: 권한 및 난독화 규칙 설정

AndroidManifest.xml에서 App 권한을 설정합니다. SDK에는 다음 권한(6.0 이후 버전 Android 시스템의 경우 카메라 및 스토리지 읽기 동적 권한 신청 필요)이 필요합니다.

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

proguard-rules.pro 파일에서 SDK 관련 유형을 비난독화 리스트에 추가합니다.

```
-keep class com.tencent.** { *; }
```

[](id:model.step3)

### 3단계: TUICalling 컴포넌트 가져오기

Source 디렉터리를 프로젝트에 복사하고 `setting.gradle`에서 가져오기를 완료합니다. 다음을 참고하십시오.

```
include ':Source'
```

[](id:model.step4)

### 4단계: 컴포넌트 초기화 및 로그인

1. `TUICallingManager.sharedInstance()`를 호출하여 컴포넌트를 초기화합니다.
2. `TUILogin.init(context, SDKAppID, config, listener)`를 호출하여 로그인을 초기화합니다.
3. `TUILogin.login(userId, userSig, callback)`을 호출하여 컴포넌트에 로그인합니다. 주요 매개변수는 다음 테이블을 참고하십시오.
 <table>
<tr><th>매개변수 이름</th><th>역할</th></tr>
<tr>
<td>SDKAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(_)만 허용됩니다. 실제 비즈니스 계정 시스템에 따라 직접 설정하는 것을 권장합니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명으로, 계산 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
</tr>
</tr><tr>
<td>config</td>
<td>SDK 구성. 로그 레벨 및 로그 콜백을 설정하는 데 사용됩니다. (null 전송 가능), 자세한 내용은 아래 예시 코드를 참고하십시오.</td>
</tr><tr>
</tr><tr>
<td>listener</td>
<td>IM 리스너. 강제 로그 아웃, userSig 만료 등과 같은 일부 필수 시스템 콜백 알림을 수신하는 데 사용됩니다. 자세한 내용은 아래 예시 코드를 참고하십시오.</td>
</tr><tr>
</tr><tr>
<td>callback</td>
<td>결과 리스너에 로그인합니다. 로그인 성공 여부를 알립니다. 자세한 내용은 아래 예시 코드를 참고하십시오.</td>
</tr><tr>
</table>
<dx-codeblock>
::: java java
     // 컴포넌트 초기화
     TUICallingManager manager = TUICallingManager.sharedInstance();
  // 로그인
  V2TIMSDKConfig config = new V2TIMSDKConfig();
  config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_DEBUG);
  config.setLogListener(new V2TIMLogListener() {
        @Override
        public void onLog(int logLevel, String logContent) {
                
        }
  });
  TUILogin.init(this, ${사용자 SDKAPPID}, config, new V2TIMSDKListener() {

            @Override
            public void onKickedOffline() {  // 강제 오프라인 알림
                mIsKickedOffline = true;
                checkUserStatus();
            }
    
            @Override
            public void onUserSigExpired() { // suerSig 만료 알림
                mIsUserSigExpired = true;
                checkUserStatus();
            }
  });
  TUILogin.login("${사용자 userId}", "${사용자 userSig}", new V2TIMCallback() {
            @Override
            public void onError(int code, String msg) {
                Log.d(TAG, "code: " + code + " msg:" + msg);
            }

            @Override
            public void onSuccess() {
                Log.d(TAG, "onSuccess");
            }
  });

:::
</dx-codeblock>

[](id:model.step5)

### 5단계: 음성 및 영상 통화 구현

1. 발신자: TUICallingManager의 `call();` 메소드를 호출하여 통화를 요청하고, 사용자 ID 배열(userids) 및 통화 유형(type)을 전송합니다. 통화 유형 매개변수 `TUICalling.Type.AUDIO`(음성 통화) 또는 `TUICalling.Type.VIDEO`(영상 통화) 또한 전송합니다. 사용자 ID 배열(userids)에 userId가 하나만 있으면 1:1 통화이며, 사용자 ID 배열(userids)에 userId가 여러 개(>=2) 있으면 다중 사용자 통화입니다.
2. 수신자: 수신자가 로그인 상태인 경우 해당 인터페이스가 자동으로 실행됩니다. 오프라인 통화 요청 수신 구현 방법은 [오프라인 수신](#model.offline)을 참고하십시오.


<dx-codeblock>
::: java java
// 1. 컴포넌트 초기화
TUICallingManager manager = TUICallingManager.sharedInstance();
// 2. 리스너 등록
manager.setCallingListener(new TUICalling.TUICallingListener() {
            @Override
            public boolean shouldShowOnCallView() {
                return true;
            }

            @Override
            public void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, final View tuiCallingView) {
                if (!shouldShowOnCallView() || null == tuiCallingView) {
                    return;
                }
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(FrameLayout.LayoutParams.MATCH_PARENT, FrameLayout.LayoutParams.MATCH_PARENT);
                        mCallingView = tuiCallingView;
                        addContentView(tuiCallingView, params);
                    }
                });
            }
    
            @Override
            public void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime) {
                removeView();
            }
    
            @Override
            public void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message) {
                if (TUICalling.Event.CALL_FAILED == event) {
                    removeView();
                }
            }
});
// 3. 통화 발신
manager.call(userIDs, TUICalling.Type.VIDEO);
:::
</dx-codeblock>

[](id:model.offline)

### 6단계: 오프라인 통화 구현

>?온라인 고객서비스 등 오프라인 수신 기능이 필요 없는 시나리오인 경우, [1단계](#model.step1) - [5단계](#model.step5)만 진행합니다. 소셜 시나리오에서는 오프라인 수신을 권장합니다.

IM SDK는 오프라인 푸시를 지원하지만, Android는 휴대폰 벤더마다 서로 다른 오프라인 푸시 서비스를 지원하므로 iOS 플랫폼보다 액세스가 복잡합니다. 따라서 사용 가능 기준을 충족하려면 해당하는 설정을 완료해야 합니다.

1. 해당 벤더의 푸시 채널에 필요한 인증서 등을 신청하고, 이를 IM 콘솔에 설정한 후 푸시 조건에 따라 인증서와 ID 등을 추가합니다. 자세한 작업 방법은 [IM > 오프라인 푸시(Android)](https://intl.cloud.tencent.com/document/product/1047/39156)를 참고하십시오.
2. 현재 TRTCCallingImpl의 sendModel 신호 발송 함수에는 오프라인 발송 함수가 통합되어 있습니다. App에서 오프라인 푸시를 설정하면 메시지를 오프라인 푸시할 수 있습니다.

[](id:api)

## 컴포넌트 API 리스트

TUICalling 컴포넌트의 API 리스트는 다음과 같습니다.

| 인터페이스 함수        | 인터페이스 기능                                                 |
| --------------- | --------------------------------------------------------- |
| call            | C2C 통화 초대         |
| receiveAPNSCalled          | 초대된 사용자 통화 수신                                      |
| setCallingListener          | 리스너 설정                                     |
| setCallingBell          | 벨소리 설정(30초 이내 권장)                                                 |
| enableMuteMode | 음소거 모드 활성화    |
| enableCustomViewRoute      | 사용자 정의 뷰 활성화. 활성화 후 발신/수신 시작 콜백 중 CallingView 인스턴스가 수신되며 개발자가 직접 표시 방법을 결정합니다. 주의: 전체 화면 또는 비례 화면으로 표시해야 합니다. 그렇지 않으면 이상 경고가 표시됩니다.            |

