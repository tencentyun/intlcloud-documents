Tencent Cloud TRTC는 Android 시스템에서 화면 공유를 지원하며, 현재 시스템의 화면 콘텐츠를 TRTC SDK를 통해 방 안의 다른 사용자에게 공유합니다. 이 기능에 관한 주의 사항은 다음과 같습니다.

- TRTC Android 버전의 화면 공유는 데스크톱 버전처럼 '서브 채널 공유'를 지원하지 않으므로, 화면 공유 실행 시 먼저 카메라의 수집을 중지하지 않으면 충돌이 발생할 수 있습니다.
- Android 시스템의 백그라운드 App이 지속적으로 CPU를 사용할 경우 시스템에 의해 강제로 종료될 수 있으며, 화면 공유 자체도 CPU를 소모하게 됩니다. 이 충돌을 해결하려면 App에서 화면 공유를 실행함과 동시에 Android 시스템에 플로팅 창을 팝업해야 합니다. Android는 포그라운드 UI의 App 프로세스를 강제 종료하지 않으므로, 해당 방법을 사용하면 다음과 같이 사용자의 App이 계속해서 화면 공유를 진행하고 자동으로 회수되지 않습니다. 



## 지원 플랫폼

| iOS | Android | Mac OS | Windows |Electron|  Chrome 브라우저|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |  &#10003;  |

## 화면 공유 실행
Android의 화면 공유를 활성화해야 합니다. `TRTCCloud`의 [startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58) 인터페이스를 호출하면 됩니다. 하지만 안정적이고 선명한 공유 효과를 구현하려면 다음 세 가지 문제를 확인하십시오.

#### Activity 추가
manifest 파일에 다음 activity를 붙여넣습니다. 프로젝트 코드에 있을 경우에는 추가할 필요 없습니다.
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

#### 비디오 인코딩 매개변수 설정
[startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)의 첫 매개변수 `encParams`를 설정하여 화면 공유의 코딩 품질을 지정할 수 있습니다. `encParams`를 null로 지정할 경우 SDK는 자동으로 이전에 설정한 코드 매개변수를 사용합니다. 매개변수 권장 설정은 다음과 같습니다.

| 매개변수 항목 | 매개변수 이름 | 일반 권장 값 |  텍스트 교육 시나리오 |
|---------|---------|---------|-----|
| 해상도 | videoResolution | 1280 × 720 | 1920 × 1080 |
| 프레임 레이트 | videoFps | 10 FPS | 8 FPS |
| 최대 비트 레이트| videoBitrate| 1600 kbps | 2000 kbps |
| 해상도 어댑티브 | enableAdjustRes | NO | NO |

- 일반적으로 화면 공유 콘텐츠는 많은 변화가 없으므로 FPS를 높게 설정하는 것은 비경제적입니다. 권장 설정값은 10FPS입니다.
- 공유하는 화면 콘텐츠에 텍스트가 많이 포함되어 있는 경우 해상도와 비트 레이트를 알맞게 높이는 것이 좋습니다.
- 최고 비트 레이트(videoBitrate)란 화면 변화가 심할 때의 최고 출력 비트 레이트를 의미하며, 화면 콘텐츠 변화가 비교적 적은 경우에는 실제 인코딩 비트 레이트가 비교적 낮습니다.

#### 팝업 플로팅 창의 강제 종료 방지
Android 7.0 시스템에서 백그라운드에서 실행되는 일반 App 프로세스로 전환합니다. 하지만 CPU가 사용되고 있을 경우 시스템에서 강제로 종료할 수 있습니다. 그러므로 App이 백그라운드로 전환되어 화면 공유를 진행할 경우에는 플로팅 창 팝업으로 시스템에 의해 강제 종료되는 것을 막을 수 있습니다. 동시에 휴대폰 화면에 플로팅 창을 표시할 경우 사용자에게 현재 화면 공유 중임을 알려 사용자의 프라이버시 유출을 막을 수 있습니다.

- **솔루션1: 일반 플로팅 창 팝업**
‘VooV Meeting’과 비슷한 미니 플로팅 창을 팝업해야 합니다. 예시 코드 [FloatingView.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Basic/ScreenShare/src/main/java/com/tencent/trtc/screenshare/FloatingView.java)의 구현을 참고하십시오.
```java
public void showView(View view, int width, int height) {
        mWindowManager = (WindowManager) mContext.getSystemService(Context.WINDOW_SERVICE);
        //TYPE_TOAST는 4.4+ 시스템에만 적용됩니다. 더 낮은 버전 지원이 필요할 경우 TYPE_SYSTEM_ALERT(manifest에서 권한 선언 필요)를 사용합니다.
        //7.1(포함) 및 이상 시스템의 TYPE_TOAST를 제한했습니다.
        int type = WindowManager.LayoutParams.TYPE_TOAST;
        if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
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

- **솔루션2: 카메라 미리보기 창 팝업**
- TRTC Android 버전의 화면 공유는 데스크톱 버전처럼 ‘서브 채널 공유’를 지원하지 않으므로 화면 공유 실행 시 카메라 채널의 비디오 데이터는 업스트림이 불가하며, 그렇지 않을 경우 충돌이 발생할 수 있습니다.
그럼 어떻게 해야 화면과 카메라 화면을 동시에 공유할 수 있을까요?
답은 간단합니다. 화면에 카메라 화면을 플로팅 창으로 띄우면 됩니다. 그러면 TRTC가 화면을 수집함과 동시에 카메라 화면을 함께 공유할 수 있습니다.

## 공유 화면 시청
- **Mac/Window 공유 화면 시청**
  방 안에 있는 Mac/Windows 사용자가 화면 공유를 실행하면 서브스트림을 통해 공유가 시작됩니다. 방 안의 다른 사용자는 TRTCCloudDelegate의 [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) 이벤트를 통해 이 공지를 수신합니다.
  공유 화면을 시청하려면 [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) 인터페이스를 통해 원격 사용자의 서브스트림 화면을 렌더링합니다.

- **Android / iOS 공유 화면 시청**
  사용자가 Android/iOS를 통해 화면을 공유하는 경우 메인 스트림을 통해 공유됩니다. 방 안의 다른 사용자들은 TRTCCloudListener의 [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) 이벤트를 통해 알림를 수신합니다.
  공유 화면을 시청하려는 사용자는 [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) 인터페이스를 통해 사용자의 주요 화면을 원격 렌더링합니다.


```java
//예시 코드: 공유 화면 시청
 @Override
 public void onUserSubStreamAvailable(String userId, boolean available) {
    startRemoteSubStreamView(userId);
}
```

## FAQ
 **한 개의 방에서 동시에 몇 개 채널의 화면을 공유할 수 있나요?**
현재 TRTC 멀티미디어 방별로 한 채널의 화면만 공유할 수 있습니다.


