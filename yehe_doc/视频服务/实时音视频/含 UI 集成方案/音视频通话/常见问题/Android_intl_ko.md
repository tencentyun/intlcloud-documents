### TUICallKit에 IM SDK를 통합하지 않고 TRTC 기능만 사용할 수 없나요?

**할 수 없습니다.** TUIKit의 모든 컴포넌트는 발신 통화 신호 및 통화 중 회선 신호와 같은 기본 로직에 대해 IM SDK에 의존합니다. 이미 IM 서비스를 구매했다면 TUICallKit 로직에 따라 사용할 수 있습니다.

### ‘The package you purchased does not support this ability’라는 오류 메시지가 표시되면 어떻게 해야 합니까?

상기 오류가 발생하면 TRTC를 활성화하지 않았거나 TRTC 패키지가 만료되었음을 나타냅니다. TRTC 활성화 방법은 [1단계: 서비스 활성화](https://www.tencentcloud.com/document/product/647/50991#step1)를 참고하십시오. 활성화 후 무료 평가판 패키지를 받을 수 있습니다.

### TUICallKit이 충돌했고 오류 메시지는 "No implementation found for xxxx"이었습니다. 어떻게 해야 하나요?

스택 추적은 다음과 같습니다.

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

>! **TUICallkit은 에뮬레이터를 지원하지 않습니다. 실제 기기에서 테스트해 보십시오.** 실제 기기에서 위와 같은 오류가 발생한다면, TUICallKit 컴포넌트가 의존하는 일부 API가 JNI를 기반으로 하기 때문이며, 경우에 따라 Android Studio에서 Native .so를 패키징하지 않을 수 있습니다. APK를 빌드할 때 라이브러리. 이 경우 프로젝트를 Clean하면 됩니다.

### allowBackup 오류가 발생하면 어떻게 해야 하나요?

**오류 메시지**: `Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml`

**원인**: IM SDK에서 allowBackup의 기본값은 false이며, 이는 애플리케이션에 대한 백업 및 복구가 비활성화되어 있음을 의미합니다.

**해결 방법**: `AndroidManifest.xml` 파일에서 allowBackup 속성을 삭제하거나 값을 false로 변경합니다. 또는 `AndroidManifest.xml` 파일의 application에 `tools:replace="android:allowBackup"`을 추가하여 IM SDK 구성을 고유한 구성으로 교체합니다.

### TUICallKit은 오프라인 통화 푸시를 지원합니까?

**지원합니다**. Android의 경우 TUIOfflinePush 컴포넌트를 사용하여 오프라인 통화 푸시를 구현합니다. 자세한 사용법은 [Android](https://www.tencentcloud.com/document/product/1047/39156)를 참고하십시오. 이 컴포넌트는 [TUICallKit](https://github.com/tencentyun/TUICalling/tree/main/Android)에도 내장되어 있습니다.

### 통화가 제한 시간 내에 있고 오프라인 초대 대상자가 온라인 상태가 되면 TUICallKit이 수신 통화 보기를 표시합니까?

초대받은 사람이 온라인 상태가 될 때 App의 상태에 따라 몇 가지 경우가 있습니다.

![img](https://qcloudimg.tencent-cloud.cn/raw/1b82ef1bcc5dbc5b0a2d7bf6e4c9d772.jpg)

초대받은 사람이 다시 온라인 상태가 된 후 수신 통화 보기가 표시되지 않으면 로그에서 'onReceiveNewInvitation'을 검색하고 기록 메시지를 가져왔는지 확인하십시오. 로그 데이터를 찾을 수 없는 경우 [문의하기](https://intl.cloud.tencent.com/contact-us)를 통해 도움을 받으십시오.

### 애플리케이션이 백그라운드 상태일 때, 통화 수신 표시를 위해 포그라운드로 자동 전환되지 않는 이유는 무엇입니까?

**애플리케이션에 백그라운드에서 ‘자동 시작’ 또는 ‘플로팅 창’ 권한이 부여되었는지 확인합니다.**

다른 벤더 또는 다른 Android 버전에서도 이를 구현하려면 다른 권한이 필요합니다. 권한의 이름도 다를 수 있습니다. 예를 들어 Xiaomi 6의 경우 백그라운드에서 팝업 권한만 필요하지만 Redmi의 경우 백그라운드에서 팝업 및 플로팅 창 권한이 모두 필요합니다.

>? 필요한 모든 권한을 수동으로 부여했지만 여전히 애플리케이션이 포그라운드로 전환되지 않는 경우 벤더 호환성 문제일 수 있습니다.
