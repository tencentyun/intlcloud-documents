Tencent Cloud TRTC는 화면 공유 기능을 지원합니다. Mac 플랫폼에서는 메인 채널 공유와 서브 채널 공유, 두 가지 화면 공유 방법을 지원합니다.
- **서브 채널 공유**
TRTC에서 단독으로 화면 공유 채널 업스트림의 비디오 스트림을 활성화할 수 있으며, “서브 채널(**substream**)”이라고 부릅니다. 서브 채널 공유는 호스트가 동시에 카메라 화면과 스크린 화면, 두 채널의 화면을 업스트림하는 것입니다. 이는 VooV Meeting의 사용 방법으로, `startScreenCapture` 인터페이스를 호출하는 경우 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeSub`으로 지정하여 해당 모드를 활성화할 수 있습니다. 해당 채널 화면을 시청할 경우 전용 `startRemoteSubStreamView` 인터페이스가 필요합니다.

- **메인 채널 공유**
TRTC 에서 우리는 일반적으로 카메라가 통과하는 터널을 “메인 채널(**bigstream**)”이라고 하며, 메인 채널 공유는 카메라 터널 공유 화면입니다. 해당 모드에서 호스트는 1개의 업스트림 비디오 스트림만 있으며, 업스트림 카메라 화면이나 업스트림 스크린 화면은 충돌이 있습니다. `startScreenCapture` 인터페이스를 호출하는 경우 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeBig`으로 지정해 해당 모드를 활성화할 수 있습니다.

## 지원 플랫폼

| iOS | Android | Mac OS | Windows |Electron| WeChat 미니프로그램 | Chrome 브라우저|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## 공유 타깃 획득
[getScreenCaptureSourcesWithThumbnailSize](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8e5286e1035b64b7d2bf8fadd721123) 를 통해 공유할 수 있는 창 리스트를 열거할 수 있으며, 모든 공유 가능한 타깃은 `TRTCScreenCaptureSourceInfo` 객체입니다.

Mac OS의 데스크톱 화면도 공유 가능 타깃입니다. 일반적인 Mac 창의 type은 `TRTCScreenCaptureSourceTypeWindow`이며, 데스크 화면의 type은 `TRTCScreenCaptureSourceTypeScreen`입니다.

type 이외의 모든 `TRTCScreenCaptureSourceInfo`는 다음 필드 정보가 있습니다.

| 필드 | 유형 | 의미|
|:-------:|:--------:| :---------------:|
| type |TRTCScreenCaptureSourceType| 수집 소스 유형: 지정 유형은 창 혹은 화면|
| sourceId | NSString| 수집 소스 ID: 창, 해당 필드는 지시 창 핸들을 가리킵니다.<br>화면, 해당 필드는 화면 ID를 가리킵니다. |
| sourceName| NSString | 창 이름, 화면일 경우Screen0 Screen1... 반환 |
| extInfo| NSDictionary | 공유 창의 부가 정보 |
| thumbnail| NSImage | 창 썸네일 |
| icon | NSImage | 창 아이콘 |

위 정보로 간단한 리스트 페이지를 구현하고 공유 타깃을 열거해 사용자가 선택하게 할 수 있습니다.

## 공유 타깃 선택
TRTC SDK는 3가지 공유 모드를 지원합니다. [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18)으로 지정할 수 있습니다.

- **전체 화면 공유**:
전체 화면 창을 공유하고 멀티 모니터 화면 분할을 지원합니다. type이 `TRTCScreenCaptureSourceTypeScreen`인 screenSource 매개변수를 지정하고 rect를 { 0, 0, 0, 0 }으로 설정해야 합니다.

- **지정 지역 공유**:
화면의 어떤 구역을 공유하며, 사용자가 지정한 구역 위치의 좌표가 필요합니다. type이 `TRTCScreenCaptureSourceTypeScreen`인 screenSource 매개변수를 지정하고 captureRect를 비 NULL로 설정해야 합니다. 예: { 100, 100, 300, 300 }

- **지정 창 공유**:
타깃 창의 콘텐츠 공유로, 사용자가 어떤 창을 공유할지 선택해야 합니다. type이 `TRTCScreenCaptureSourceTypeWindow`인 screenSource 매개변수를 설정하고 captureRect를 { 0, 0, 0, 0 }으로 설정해야 합니다.


>? 추가 매개변수 2개:
> - 매개변수 capturesCursor은 마우스 포인터의 캡처 여부를 지정할 때 사용합니다.
> - 매개변수 highlight는 현재 공유 중인 창의 하이라이트 및 캡처한 아이콘이 가려졌을 경우 사용자에게 가림 제거 알림 여부 지정 시 사용합니다. 이 부분의 UI 특수효과는 SDK 내부에 구현됩니다.


## 화면 공유 시작

 - 공유 타깃 선택 후 [startScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) 인터페이스를 사용하면 화면 공유를 실행할 수 있습니다.
 - 두 함수 [pauseScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280)와 [stopScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb)의 차이는 pause의 화면 콘텐츠 수집 중지 여부와 중지된 순간의 화면 연동입니다. 원격에서는 [resumeScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af257a8fb6969fe908ca68a039e6dba15) 시까지 마지막 프레임만 보게 됩니다.

```Objective-C
 /**
 *  7.6 [화면 공유] 화면 공유 실행
 *  @param view 렌더링 제어 파일이 있는 상위 제어 파일
 */
- (void)startScreenCapture:(NSView *)view;

/**
 *  7.7 [화면 공유] 화면 수집 중지
 *  @return 0: 성공 <0:실패
 */
- (int)stopScreenCapture;

/**
 *  7.8 [화면 공유] 화면 공유 일시 중지
 *  @return 0: 성공 <0:실패
 */
- (int)pauseScreenCapture;

/**
 *  7.9 [화면 공유] 화면 공유 복구
 *
 *  @return 0: 성공 <0:실패
 */
- (int)resumeScreenCapture;
```

## 화면 화질 설정
[setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) 인터페이스에서 해상도, 비트 레이트, 프레임 레이트 등 화면 공유의 화질을 설정할 수 있습니다. 다음 값을 참조하십시오.

| 해상도 레벨 | 해상도 | 프레임 레이트 | 비트 레이트 |
|:-------------:|:---------:|:---------:| :---------: |
| 초고화질(HD+) | 1920 × 1080 | 10 | 800 kbps |
| 고화질(HD) | 1280 × 720 | 10 | 600 kbps |
| 표준 화질(SD) | 960 × 720 | 10 | 400 kbps |

## 화면 공유 보기
- **Mac/Window 화면 공유 보기**
  방 안에 있는 Mac/Windows 사용자가 화면 공유 기능을 실행하면 서브스트림을 통해 화면이 공유됩니다. 방 안의 다른 사용자들은 TRTCCloudDelegate의 [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) 이벤트를 통해 해당 통지를 수신합니다.
  공유 화면을 보고 싶은 사용자는 [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) 인터페이스를 통해 사용자의 서브스트림 화면의 원격 렌더링을 활성화할 수 있습니다.

- **Android/iOS 화면 공유 보기**
  사용자가 Android/iOS를 통해 화면을 공유하는 경우 주요 화면을 공유합니다. 방 안의 다른 사용자들은 TRTCCloudDelegate의 [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트를 통해 통지를 수신합니다.
  공유 화면을 보고 싶은 사용자는 [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) 인터페이스를 통해 사용자의 주요 화면의 원격 렌더링을 활성화할 수 있습니다.



```Objective-C
//예시 코드: 화면 공유 보기

- (void)onUserSubStreamAvailable:(NSString *)userId available:(BOOL)available {
    if (available) {
        [self.trtcCloud startRemoteSubStreamView:userId view:self.capturePreviewWindow.contentView];
    } else {
        [self.trtcCloud stopRemoteSubStreamView:userId];
    }
}
```

## FAQ
**방에서는 동시에 몇 명이 화면을 공유할 수 있습니까?**
현재 한 TRTC 멀티미디어 방에서는 한 채널의 화면만 공유할 수 있습니다.

**지정 창 공유(SourceTypeWindow) 시 창의 크기가 달라질 경우 비디오 스트리밍의 해상도도 변경됩니까?**
기본적으로 SDK 내부에서는 공유한 창의 크기에 따라 자동으로 코드 매개변수를 조정합니다.
고정 해상도가 필요한 경우 setSubStreamEncoderParam 인터페이스를 호출하여 화면 공유 코드 매개변수를 설정하거나 startScreenCapture 호출 시 해당 코드 매개변수를 지정해야 합니다.
