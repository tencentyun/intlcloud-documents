본 문서에서는 화면을 공유하는 방법을 설명합니다. 현재 TRTC 룸은 한 번에 하나의 화면 공유 스트림만 가질 수 있습니다.

## 호출 가이드
### 화면 공유 활성화

[](id:step1)
#### 1단계: Activity 추가
manifest 파일에 다음 activity를 붙여넣습니다. 프로젝트 코드에 있을 경우에는 추가할 필요 없습니다.
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

[](id:step2)
#### 2단계: 화면 공유 시작
Android의 화면 공유를 시작하려면 `TRTCCloud`에서 [startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58) API를 호출하기만 하면 됩니다.

[startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)의 첫 매개변수 `encParams`를 설정하여 화면 공유의 인코딩 품질을 지정할 수 있습니다. `encParams`를 null로 지정할 경우 SDK는 자동으로 이전에 설정한 코드 매개변수를 사용합니다. 다음 설정을 권장합니다.

| 매개변수 항목 | 매개변수 이름 | 일반 권장 값 |  텍스트 교육 시나리오 |
|---------|---------|---------|-----|
| 해상도 | videoResolution | 1280 × 720 | 1920 × 1080 |
| 프레임 레이트 | videoFps | 10 FPS | 8 FPS |
| 최대 비트 레이트| videoBitrate| 1600 kbps | 2000 kbps |
| 해상도 어댑티브 | enableAdjustRes | NO | NO |

- 일반적으로 화면 공유 콘텐츠는 많은 변화가 없으므로 FPS를 높게 설정하는 것은 비경제적입니다. 권장 설정값은 10FPS입니다.
- 공유하는 화면 콘텐츠에 텍스트가 많이 포함되어 있는 경우 해상도와 비트 레이트를 알맞게 높이는 것이 좋습니다.
- 최대 비트 레이트(videoBitrate)란 화면 변화가 심할 때 최대로 출력되는 비트 레이트를 의미하며, 화면 콘텐츠의 변화가 적은 경우 실제 인코딩 비트 레이트는 비교적 낮습니다.

[](id:step3)
#### 3단계: 강제 종료를 방지하기 위해 플로팅 창 표시(선택 사항)
Android 7.0 시스템부터 백그라운드에서 실행되는 일반적인 App 프로세스는 CPU가 사용되고 있을 경우 시스템에 의해 강제 종료되는 현상이 쉽게 발생합니다. 그러므로 App이 백그라운드에서 화면을 공유하고 있을 때 플로팅 창 팝업을 통해 시스템에 의해 강제 종료되는 것을 막을 수 있습니다. 또한 휴대폰 화면에 플로팅 창을 표시하면 사용자에게 현재 화면 공유 중임을 알려 사용자의 프라이버시 노출을 방지할 수 있습니다.

[FloatingView.java](https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example/Basic/ScreenShare/src/main/java/com/tencent/trtc/screenshare/FloatingView.java)의 코드는 미니 플로팅 창을 만드는 방법의 예시를 제공합니다.
```java
public void showView(View view, int width, int height) {
        mWindowManager = (WindowManager) mContext.getSystemService(Context.WINDOW_SERVICE);
        int type = WindowManager.LayoutParams.TYPE_TOAST;
        //TYPE_TOAST는 4.4+ 시스템에만 적용됩니다. 더 낮은 버전 지원이 필요할 경우 TYPE_SYSTEM_ALERT(manifest에서 권한 선언 필요)를 사용합니다.
        //7.1(포함) 및 이상 시스템의 TYPE_TOAST를 제한했습니다.
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            type = WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY;
        } else if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
            type = WindowManager.LayoutParams.TYPE_PHONE;
        }
        mLayoutParams = new WindowManager.LayoutParams(type);
        mLayoutParams.flags = WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE;
        mLayoutParams.flags |= WindowManager.LayoutParams.FLAG_WATCH_OUTSIDE_TOUCH;
        mLayoutParams.width = width;
        mLayoutParams.height = height;
        mLayoutParams.format = PixelFormat.TRANSLUCENT;
        mWindowManager.addView(view, mLayoutParams);
}
```

### 공유 화면 시청
- **Mac/Window 공유 화면 시청**
  방의 Mac/Windows 사용자가 화면 공유를 실행하면 서브스트림을 통해 화면이 공유되고 방의 다른 사용자는 TRTCCloudListener의 [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390)을 통해 알림을 받습니다.

- **Android/iOS 공유 화면 시청**
  사용자가 Android/iOS를 통해 화면을 공유하는 경우 메인 스트림을 통해 공유됩니다. 방 안의 다른 사용자들은 TRTCCloudListener의 [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) 이벤트를 통해 알림를 수신합니다.
  

공유 화면을 시청할 사용자는 [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) API를 통해 원격 사용자의 기본 스트림 렌더링을 시작할 수 있습니다.