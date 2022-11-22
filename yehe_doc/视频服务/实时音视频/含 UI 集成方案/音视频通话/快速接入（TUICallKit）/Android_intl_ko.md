본문에서는 TUICallKit 컴포넌트의 액세스를 최단 시간에 완료하는 방법에 대해 설명합니다. 본 문서를 따르면, 다음 몇 가지 주요 단계를 한 시간 내에 완료하고 최종적으로 UI 인터페이스로 영상 통화 기능을 얻을 수 있습니다.

## 환경 준비

Android 4.1(SDK API Level 16)까지 호환됩니다. Android 5.0(SDK API Level 21) 이후 버전 사용을 권장합니다.

Android Studio 3.5 이상 버전(Gradle 3.5.4 이상 버전).

Android 4.1 이상이 설치된 기기.

[](id:step1)
##  1단계: 서비스 활성화

TUICallKit은 Tencent Cloud의 두 가지 유료 PaaS 서비스 [Instant Messaging(IM)](https://www.tencentcloud.com/document/product/1047) 및 [Tencent Real-Time Communication(TRTC)](https://www.tencentcloud.com/document/product/647)을 기반으로 하는 오디오/비디오 통신 컴포넌트입니다. 아래 단계에 따라 관련 서비스를 활성화하고 60일 무료 베타 서비스를 체험할 수 있습니다.

1. [IM 콘솔](https://console.tencentcloud.com/im)에 로그인하고 **애플리케이션 생성**을 클릭하고 팝업 대화 상자에 애플리케이션 이름을 입력하고 **확인**을 클릭합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/571d5bed98a46752933169fbf4136271.png)

2. 방금 생성한 애플리케이션을 클릭하여 기본 구성 페이지로 이동하고 TUICallKit의 7일 무료 평가판을 보려면 페이지 오른쪽 하단 모서리에 있는 TRTC 활성화에서 무료 평가판을 클릭하십시오. 애플리케이션을 공식 릴리스하려면 구매를 클릭하여 구매 페이지로 이동합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

>! 다양한 비즈니스 요구 사항에 따라 IM 음성/영상 통화 기능의 다양한 유료 버전을 사용할 수 있습니다. IM 구매 페이지에서 사용 가능한 기능에 대해 자세히 알아보고 원하는 버전을 구매할 수 있습니다.

3. 같은 페이지에서 **SDKAppID**와 **키(SecretKey)**를 찾아 기록해 둡니다. [4단계: TUI 컴포넌트 로그인](#step4)에서 사용될 예정입니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/5c1b56dc1972d836c85579dd16b0634d.png)


>? **참고:** **무료 체험**을 클릭하면 이전에 [TRTC](https://www.tencentcloud.com/document/product/647/35078) 서비스를 사용한 적이 있는 일부 사용자에게 다음 메시지가 표시됩니다.

```java
[-100013]:TRTC service is  suspended. Please check if the package balance is 0 or the Tencent Cloud accountis in arrears
```
새로운 IM 음성 및 영상 통화 기능은 [TRTC](https://www.tencentcloud.com/document/product/647/35078) 및 [IM](https://www.tencentcloud.com/document/product/1047)의 두 가지 기본 PaaS 서비스가 통합되어 있으므로, [TRTC](https://www.tencentcloud.com/document/product/647/35078)의 무료 할당량(10000분)이 만료되거나 소진되면 이 서비스를 활성화할 수 없습니다. 예시 이미지와 같이 [TRTC 콘솔](https://console.tencentcloud.com/trtc/app)을 클릭하여 SDKAppID에 해당하는 애플리케이션 관리 페이지에서 후불 기능을 활성화한 후 다시 **애플리케이션을 활성화**하면 음성 및 영상 통화 기능을 정상적으로 체험할 수 있습니다.

[](id:step2)
## 2단계: 컴포넌트 다운로드 및 가져오기

[Github](https://github.com/tencentyun/TUICalling)에서 코드를 복제/다운로드한 다음 아래와 같이 Android 디렉터리 아래의 tuicallkit 서브 디렉터리를 현재 프로젝트의 app과 동일한 수준 디렉터리로 복사합니다.

![img](https://qcloudimg.tencent-cloud.cn/raw/4b6a74f2ee2f5d8eab00061b9fc1f112.png)

[](id:step3)
## 3단계: 프로젝트 구성 완료
1. 프로젝트의 루트 디렉터리에서 'setting.gradle' 파일을 찾고 다음 코드를 추가합니다. 이 파일은 [2단계](#step2)에서 다운로드한 tuicallkit 컴포넌트를 현재 프로젝트로 가져올 수 있습니다.

```java
include ':tuicallkit'
```

2. app 디렉터리에서 'build.gradle' 파일을 찾아 다음 코드를 추가합니다. 이 파일은 현재 새로 추가된 tuicallkit 컴포넌트에 대한 현재 app의 종속을 선언합니다.
```java
api project(':tuicallkit')
```
>? TUICallKit 프로젝트에는 기본 종속성인 `TRTC SDK`, `IM SDK`, `tuicallengine` 및 공용 라이브러리 `tuicore`가 있으며 개발자가 별도로 구성할 필요가 없습니다. 버전을 업그레이드하려면 `tuicallkit/build.gradle` 파일을 수정하기만 하면 됩니다.

3. SDK 내에서 Java의 리플렉션 특성을 사용하기 때문에 SDK의 일부 클래스를 난독화 방지 목록에 추가해야 하므로 `proguard-rules.pro` 파일에 다음 코드를 추가해야 합니다.
```bash
-keep class com.tencent.** { *; }
```
>! TUICallKit은 내부적으로 카메라, 마이크, 읽기 저장 권한 등을 동적으로 신청할 수 있도록 도와드립니다. 업무 문제로 인해 삭제해야 하는 경우 `tuicallkit/src/main/AndroidManifest.xml`을 수정합니다.

[](id:step4)
## 4단계: TUI 컴포넌트 로그인

프로젝트에 다음 코드를 추가하는 것은 TUICore에서 관련 인터페이스를 호출하여 TUI 컴포넌트의 로그인을 완료하는 것입니다. TUICallKit의 다양한 기능은 로그인이 성공한 후에야 정상적으로 사용할 수 있기 때문에 이 단계는 매우 중요합니다. 따라서 관련 매개변수가 올바르게 구성되었는지 확인하십시오.
```java
//로그인 결과에 대한 리스너 설정
private final TUILoginListener mLoginListener = new TUILoginListener() {    
    @Override    
    public void onKickedOffline() {        
        super.onKickedOffline();        
        Log.i(TAG, "You have been kicked off the line. Please login again!"); 
        //logout();
    }    
    @Override    
    public void onUserSigExpired() {        
        super.onUserSigExpired();       
        Log.i(TAG, "Your user signature information has expired");        
        //logout();    
    }
};
TUILogin.addLoginListener(mLoginListener);

//로그인
TUILogin.login(context, 
    1400000001,     // 1단계에서 얻은 SDKAppID로 교체하십시오
    "denny",        // UserID로 바꾸십시오
    "xxxxxxxxxxx",  // 콘솔에서 UserSig를 계산하고 이 위치에 입력할 수 있습니다
    new TUICallback() {
    @Override
    public void onSuccess() {
        Log.i(TAG, "login success");
    }

    @Override
    public void onError(int errorCode, String errorMessage) {
        Log.e(TAG, "login failed, errorCode: " + errorCode + " msg:" + errorMessage);
    }
});
```

**매개변수 설명:** 여기에서는 login 함수에 사용되는 몇 가지 주요 매개변수에 대해 자세히 설명합니다.

- **SDKAppID**: 1단계의 마지막 순서에서 이미 얻었으므로 여기서 더 이상 반복하지 않습니다.
- **UserID**: 현재 사용자 ID입니다. 영어 알파벳(a-z, A-Z), 숫자(0~9), 하이픈(-), 언더바(_)의 문자열로 구성합니다.
- **UserSig**: [1단계](#step1)의 3번째 순서에서 획득한 SecretKey를 사용하여 SDKAppID, UserID 등의 정보를 암호화하면, Tencent Cloud가 현재 사용자의 TRTC 서비스 사용 가능 여부를 식별하는 인증용 티켓인 UserSig를 얻을 수 있습니다. 콘솔의 [**보조 툴**](https://console.cloud.tencent.com/im/tool-usersig)을 통해 일시적으로 사용 가능한 UserSig를 생성할 수 있습니다.

자세한 내용은 [UserSig 계산 방법](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.

>? **이 단계는 지금까지 개발자들로부터 가장 많은 피드백을 받은 단계이기도 합니다. 자주 발생하는 문제는 다음과 같습니다.**
- SDKAppID 설정 오류. 중국 사이트의 SDKAppID는 일반적으로 140으로 시작하는 10자리 정수입니다.
- UserSig가 암호화 키(SecretKey)와 일치하지 않는 경우 SecretKey를 UserSig로 직접 구성하지 않고 SDKAppID, UserID, 만료 시간 등의 정보를 SecretKey로 암호화하여 UserSig를 얻습니다.
- UserID는 ‘1’, ‘123’, ‘111’ 등의 간단한 문자열로 설정됩니다. **TRTC는 동일한 UserID의 다중 단말 로그인을 지원하지 않기 때문에**, 여러 사람이 공동으로 개발할 경우,‘1’, ‘123’, ‘111’과 같은 UserID는 동료에 의해 쉽게 점유되어 로그인 실패의 원인이 될 수 있으므로 디버깅할 때 인식도가 높은 UserID를 설정하는 것이 좋습니다.

>! Github의 예시 코드는 genTestUserSig 함수를 사용하여 현재 액세스 프로세스를 더 빠르게 실행할 수 있도록 로컬에서 UserSig를 계산하지만 이 솔루션은 App 코드에 SecretKey를 노출하므로 SecretKey를 업그레이드하고 보호하려면 UserSig의 계산 로직을 서버에 두는 것을 강력히 권장합니다. app은 TUICallKit 컴포넌트가 사용될 때마다 서버에서 실시간으로 계산된 UserSig를 요청합니다.

[](id:step5)
## 5단계: 전화 걸기

### 1:1 영상 통화

TUICallKit의 call 함수를 호출하고 통화 유형 및 수신자의 userId를 지정하여 음성 또는 영상 통화를 시작할 수 있습니다.
```java
// 1:1 영상 통화 시작(UserID가 mike라고 가정)
TUICallKit.createInstance(context).call("mike", TUICallDefine.MediaType.Video); 
```

| 매개변수     | 유형                    | 의미                                                  |
| ------------- | ----------------------- | ----------------------------------------------------- |
| userId        | String                  | 대상 사용자의 ID: `"mike"`                           |
| callMediaType | TUICallDefine.MediaType | 통화의 미디어 유형. 예시: `TUICallDefine.MediaType.Video` |

### 그룹 영상 통화

TUICallKit의 groupCall 함수를 호출하고 통화 유형 및 수신자의 UserID 목록을 지정하여 그룹 내에서 음성 또는 영상 통화를 시작할 수 있습니다.
```java
TUICallKit.createInstance(context).groupCall("12345678", Arrays.asList("jane", "mike", "tommy"),TUICallDefine.MediaType.Video);
```

| 매개변수     | 유형                    | 의미                                                      |
| ------------- | ----------------------- | --------------------------------------------------------- |
| groupId       | String                  | 그룹 Id. 예시: `"12345678"`                               |
| userIdList | List | 대상 사용자의 UserID 값 목록. 예시: `{"jane", "mike", "tommy"}` |
| callMediaType | TUICallDefine.MediaType | 통화의 미디어 유형. 예시: `TUICallDefine.MediaType.Video`     |

>? [Android, iOS, macOS](https://www.tencentcloud.com/document/product/1047/48466)의 안내에 따라 그룹을 생성할 수 있습니다. [IM TUIKit](https://intl.cloud.tencent.com/document/product/1047/34286)을 사용하여 채팅 및 통화 시나리오를 원스톱으로 통합할 수도 있습니다.

TUICallKit은 현재 그룹에 속하지 않은 사용자 간의 다중 사용자 영상 통화를 지원하지 않습니다. 그러한 필요가 있는 경우 colleenyu@tencent.com으로 문의하십시오.

[](id:step6)
## 6단계: 전화 수신

TUICallKit 컴포넌트는 전화 요청을 받으면 자동으로 알람을 울리는 수신 인터페이스입니다. 그러나 Android 시스템 권한 때문에 다음과 같은 경우로 나뉩니다.

- App이 포그라운드에 있을 때 초대가 수신되면 호출 인터페이스가 자동으로 팝업되고 벨소리가 재생됩니다.
- App이 백그라운드에 있지만 '플로팅 창 권한' 또는 '백그라운드 팝업 애플리케이션'과 같은 권한을 부여한 경우에도 호출 인터페이스가 자동으로 팝업되고 벨소리가 재생됩니다.
- App이 백그라운드에 있고 '플로팅 창 권한' 또는 '백그라운드 팝업 애플리케이션'을 허용하지 않은 경우 TUICallKit은 벨소리를 재생하여 사용자에게 응답하거나 끊으라는 메시지를 표시합니다.
- App 프로세스가 종료된 경우, [오프라인 푸시(Android)](https://www.tencentcloud.com/document/product/647/50991)에 설명된 대로 오프라인 푸시 기능을 사용하여 상태 표시줄 알림을 통해 사용자에게 전화를 받거나 거절하도록 요청할 수 있습니다.

[](id:step7)
## 7단계: 더 많은 특성

### 1. 닉네임 및 프로필 사진 설정

닉네임이나 프로필 사진을 사용자 지정하려면 다음 인터페이스를 사용하여 업데이트할 수 있습니다.
```java
TUICallKit.createInstance(context).setSelfInfo("jack", "https:/****/user_avatar.png", callback);
```

>! 사용자 개인정보 제한으로 인해 친구가 아닌 사용자와의 통화 시 수신자의 닉네임 및 프로필 사진 업데이트가 딜레이될 수 있으며, 통화 성공 후 원활하게 업데이트 됩니다.

### 2. 오프라인 푸시

상기 단계를 완료한 후 음성 또는 영상 통화를 걸거나 받을 수 있습니다. 그러나 응용 프로그램이 백그라운드에 있거나 응용 프로그램이 닫힌 후에도 사용자가 전화 초대를 받을 수 있도록 하려면 오프라인 푸시 기능도 구현해야 합니다. 자세한 내용은 [오프라인 푸시(Android)](https://www.tencentcloud.com/document/product/647/50991)를 참고하십시오.

### 3. 플로팅 창 기능

플로팅 창 기능을 활성화하려면 TUICallKit 컴포넌트 초기화 시 다음 인터페이스를 호출하여 이 기능을 활성화할 수 있습니다.
```java
TUICallKit.createInstance(context).enableFloatWindow(true);
```

### 4. 통화 상태 수신

만약 귀하의 업무에서 통화 시작, 종료, 통화 중 네트워크 품질 등 **통화 상태를 수신**하려면 다음 이벤트를 수신할 수 있습니다.
```java
TUICallEngine.createInstance(context).addObserver(new TUICallObserver() {
    @Override
    public void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole) {
    }
    public void onCallEnd(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType,TUICallDefine.Role callRole, long totalTime) {
    }
    public void onUserNetworkQualityChanged(List<TUICommonDefine.NetworkQualityInfo> networkQualityList) {
    }
});
```

### 5. 사용자 지정 벨소리

수신 전화의 벨소리를 사용자 지정하려면 다음 인터페이스를 통해 설정할 수 있습니다.

```java
TUICallKit.createInstance(context).setCallingBell(filePath);
```

## FAQ

### 1. ‘The package you purchased does not support this ability’라는 오류 메시지가 표시되면 어떻게 해야 합니까?

오류 메시지는 애플리케이션의 오디오/비디오 통화 기능 패키지가 만료되었거나 활성화되지 않았음을 나타냅니다. TUICallKit을 계속 사용하려면 [1단계](#step1)의 지침에 따라 음성/영상 통화 기능을 요청하거나 활성화할 수 있습니다.

### 2. 플랜은 어떻게 구매하나요?

자세한 내용은 [가격 개요](https://www.tencentcloud.com/document/product/647/50553)를 참고하십시오. 기타 궁금한 사항이 있으시면 페이지 우측의 프리세일 패키지 상담을 클릭하시거나 QQ 그룹 **592465424**에 가입하여 상담 및 피드백 부탁드립니다.

### 3. TUICallKit이 크래쉬되고 "No implementation found for xxxx" 로그가 출력되면 어떻게 해야 합니까?

다음은 스택 정보입니다.

```java
java.lang.UnsatisfiedLinkError: No implementation found for void com.tencent.liteav.base.Log.nativeWriteLogToNative(int, java.lang.String, java.lang.String) (tried Java_com_tencent_liteav_base_Log_nativeWriteLogToNative and Java_com_tencent_liteav_base_Log_nativeWriteLogToNative__ILjava_lang_String_2Ljava_lang_String_2)
       at com.tencent.liteav.base.Log.nativeWriteLogToNative(Native Method)
       at com.tencent.liteav.base.Log.i(SourceFile:177)
       at com.tencent.liteav.basic.log.TXCLog.i(SourceFile:36)
       at com.tencent.liteav.trtccalling.model.impl.base.TRTCLogger.i(TRTCLogger.java:15)
       at com.tencent.liteav.trtccalling.model.impl.ServiceInitializer.init(ServiceInitializer.java:36)
       at com.tencent.liteav.trtccalling.model.impl.ServiceInitializer.onCreate(ServiceInitializer.java:101)
       at android.content.ContentProvider.attachInfo(ContentProvider.java:2097)
       at android.content.ContentProvider.attachInfo(ContentProvider.java:2070)
       at android.app.ActivityThread.installProvider(ActivityThread.java:8168)
       at android.app.ActivityThread.installContentProviders(ActivityThread.java:7709)
       at android.app.ActivityThread.handleBindApplication(ActivityThread.java:7573)
       at android.app.ActivityThread.access$2600(ActivityThread.java:260)
       at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2435)
       at android.os.Handler.dispatchMessage(Handler.java:110)
       at android.os.Looper.loop(Looper.java:219)
       at android.app.ActivityThread.main(ActivityThread.java:8668)
       at java.lang.reflect.Method.invoke(Native Method)
       at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:513)
       at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1109)
```

**TUICallkit은 가상 컴퓨터에서 지원되지 않으며 실제 디바이스에서 실행해야 합니다.** 상기 예외가 실제 디바이스에서 발생하는 경우 TUICallKit에 의존하는 TRTC SDK와 같은 SDK의 일부 API는 JNI를 통해 구현되지만 Android Studio는 일부 조건에서 APK를 컴파일할 때 Native .so 라이브러리를 패키징하지 않을 수 있습니다. 이 경우 프로젝트를 다시 Clean하면 됩니다.

>? 자세한 내용은 [FAQ(Android)](https://www.tencentcloud.com/document/product/647/51022)를 참고하십시오.

## 교류 및 피드백

요구 사항이나 피드백이 있는 경우 colleenyu@tencent.com으로 문의하십시오.
