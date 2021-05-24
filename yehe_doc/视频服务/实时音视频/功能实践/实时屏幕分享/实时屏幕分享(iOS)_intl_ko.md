Tencent Cloud TRTC는 iOS 플랫폼에서 두 가지 화면 공유 방법을 지원합니다.
- **애플리케이션 내 공유**
즉, 현재 App의 화면만 공유 가능하며, 해당 기능은 iOS 13 버전 이상의 운영체제에서만 지원됩니다. 현재 App 이외의 화면 콘텐츠를 공유할 수 없으므로 높은 수준의 개인 정보 보호가 필요한 상황에 적합합니다. 
- **애플리케이션 간 공유**
애플의 Replaykit 솔루션을 기반으로 시스템 전체의 화면 콘텐츠 공유가 가능합니다. 다만, 현재 App에서 별도로 Extension 확장 컴포넌트를 제공해야 하므로 공유를 위한 애플리케이션 내 연결 절차가 더 많습니다.

>! 주의해야 할 점은 TRTC SDK의 모바일 버전이 데스크톱 버전과 같이 “서브 채널 공유”를 지원하지 않는다는 것입니다. iOS와 Android 시스템은 모두 백그라운드에서 실행되는 App에 카메라 사용 권한을 제한하여 서브 채널 공유의 의미가 그리 크지 않습니다.

## 지원 플랫폼

| iOS | Android | Mac OS | Windows |Electron| Chrome 브라우저|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |  &#10003;  |

## 애플리케이션 내 공유

애플리케이션 내 공유 솔루션 구현은 매우 간단합니다. TRTC SDK에서 제공하는 [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5dbd40c4ad65152e85591c8535b4ee90) 인터페이스를 호출하고 인코딩 매개변수`TRTCVideoEncParam`을 전달하기만 하면 됩니다. 해당 매개 변수를 nil로 설정할 수 있는데, 이때 SDK는 화면 공유 전에 설정된 코딩 매개변수를 사용합니다.

iOS 화면 공유 시 다음과 같은 인코딩 매개변수를 권장합니다.

| 매개변수 항목 | 매개변수 이름 | 일반 권장 값 |  텍스트 교육 시나리오 |
|---------|---------|---------|-----|
| 해상도 | videoResolution | 1280 × 720 | 1920 × 1080 |
| 프레임 레이트 | videoFps | 10 FPS | 8 FPS |
| 최대 비트 레이트| videoBitrate| 1600 kbps | 2000 kbps |
| 해상도 어댑티브 | enableAdjustRes | NO | NO |

- 보통 화면 공유 콘텐츠는 변화가 심하지 않아 FPS를 높게 설정하면 비경제적입니다. 10FPS로 설정하는 것을 권장합니다.
- 공유하는 화면 콘텐츠에 텍스트가 많이 포함되어 있는 경우 해상도와 비트 레이트를 알맞게 높이는 것이 좋습니다.
- 최대 비트 레이트(videoBitrate)란 화면 변화가 심할 때의 최고 출력 비트 레이트를 의미하며, 화면 콘텐츠의 변화가 적으면 실제 인코딩 비트 레이트가 낮습니다.


## 애플리케이션 간 공유

### 예시 코드
[Github]의 **Screen** 디렉터리에 애플리케이션 간 공유 예시 코드가 저장되어 있으며, 다음 파일이 포함되어 있습니다.

```
├─ TRTCSimpleDemo              // TRTC 간소화 Demo
|  ├─ Screen                   // 애플리케이션 간 화면 공유 기능 예시
|  |  ├─ RTC                   // TRTC에서 통화 모드 실행을 위한 예시 코드, 해당 모드에서는 역할의 개념이 없음
|  |  |  ├─ TXReplayKit_Screen // 녹화 프로세스 Broadcast Upload Extension 코드는 2단계 참조
|  |  |  |  ├─ SampleHandler.swift // 시스템 녹화 데이터 수신에 사용
|  |  |  |  ├─ Info.plist                          
|  |  |  |  ├─ TXReplayKit_Screen.entitlements //프로세스 간에 통신하는 AppGroup 정보 설정에 사용
|  |  |  
|  |  ├─ ScreenEntranceViewController.swift    // 기능으로 이동하는 인터페이스
|  |  ├─ ScreenViewController.swift            // 녹화 상태 표시 인터페이스
|  |  ├─ TRTCBroadcastExtensionLauncher.swift  // 시스템 녹화 알람에 사용하는 보조 코드
```

[README]의 가이드를 참조해 해당 예시 Demo를 제작할 수 있습니다.


### 연결 절차

iOS 시스템에서 애플리케이션 간 화면 공유의 경우, 메인 App 프로세스와 함께 푸시 스트리밍을 진행하기 위해 Extension 화면 녹화 프로세스를 추가해야 합니다. Extension 화면 녹화 프로세스는 화면을 녹화해야 할 때 시스템에서 생성하며, 시스템에서 수집한 화면 이미지를 수신합니다. 따라서 다음과 같은 절차를 수행해야 합니다.

1. App Group을 구성하고 XCode에 설치합니다(옵션). 이 단계는 Extension 화면 녹화 프로세스와 메인 App 프로세스 간의 통신을 가능하게 하기 위한 과정입니다.
2. 프로그램에 Broadcast Upload Extension의 Target을 생성하고, 여기에 SDK 압축파일 중 확장 모듈을 위해 사용자 정의된 `TXLiteAVSDK_ReplayKitExt.framework`를 통합합니다.
3. 메인 App이 Broadcast Upload Extension에서 수신되는 녹화 데이터를 대기하도록 메인 App의 수신 로직과 연결합니다.
4. Demo에서 사전에 실행한 helper class(RPSystemBroadcastPickerView`)를 사용하여 VooV Meeting과 비슷하게 iOS 버전에서 버튼 하나를 클릭하면 화면 공유 알람 효과(옵션)을 구현할 수 있습니다.

>! 1단계를 건너뛰기한 경우, 즉 App Group을 설정하지 않은 경우(인터페이스 nil 전송)에도 화면 공유를 실행할 수 있습니다. 그러나 안정성이 저하되는 문제가 발생하므로 절차가 많아도 최대한 정확한 App Group을 설정하여 화면 공유 기능의 안정성을 확보하십시오.

<span id="createGroup"> </span>
#### 1단계: App Group 생성
본인의 계정으로 [**https://developer.apple.com/**](https://developer.apple.com/)에 로그인하여 다음 작업을 완료합니다. **작업 완료 후 관련 Provisioning Profile을 다시 다운로드해야 합니다**.

1. [Certificates, IDs & Profiles]을 클릭합니다.
2. 오른쪽 인터페이스에서 + 버튼을 클릭합니다.
3. [App Groups]를 선택하고 [Continue]를 클릭합니다.
4. 팝업 양식에 Description와 Identifier를 작성합니다. 여기에서 Identifier는 인터페이스에서 해당 AppGroup의 매개변수를 전달해야 합니다. 설정 완료 후 [Continue]를 클릭합니다.
 ![](https://main.qcloudimg.com/raw/43dd60f5053b21c167ee3a8dbe7d16f9/Create_AppGroup.jpg)
5. Identifier 페이지로 돌아와 왼쪽 상단 메뉴에서 [App IDs]를 선택한 후 App ID(메인 App과 Extension AppID는 동일하게 설정해야 함)를 클릭합니다.
6. [App Groups]를 선택하고 [Edit]를 클릭합니다.
7. 팝업된 창에서 방금 생성한 App Group을 선택한 뒤 [Continue]를 선택하면 편집 페이지로 돌아옵니다. 다시 [Save]를 클릭하여 저장합니다.
 ![](https://main.qcloudimg.com/raw/962c1b705433aa62c9617f90d28238c5/Apply_AppGroup.jpg)
8. Provisioning Profile을 다시 다운로드하고 XCode에 설정합니다.

<span id="createExtension"> </span>
#### 2단계: Broadcast Upload Extension 생성
1. Xcode 메뉴에서 순서대로 [File], [New], [Target...]을 클릭한 후 [Broadcast Upload Extension]을 선택합니다.
2. 팝업되는 대화 상자에 관련 정보를 입력합니다. [Include UI Extension]을 선택할 **필요 없으며** [Finish]를 클릭하여 생성합니다.
3. 다운로드한 SDK 압축파일에서 TXLiteAVSDK_ReplayKitExt.framework를 프로그램으로 드래그하고 방금 생성한 Target을 선택합니다.
4. 추가한 Target을 선택한 후, 순서대로 [+ Capability]를 클릭한 뒤 [App Groups]를 더블 클릭합니다. 다음 이미지를 참조하십시오.
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 작업을 완료하면 다음 이미지와 같이 파일 리스트에 `Target 이름.entitlements`으로 된 파일이 생성됩니다. 해당 파일을 선택한 뒤 + 버튼을 클릭하여 상기 App Group을 입력하면 됩니다.
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. 메인 App의 Target을 선택하고 **메인 App의 Target도 상술한 단계에 따라 동일하게 처리합니다.**
6. 새로 생성된 Target 중에 Xcode는 "SampleHandler.m"이라는 이름의 파일을 자동 생성하고 다음과 같은 코드로 대체합니다.** 코드의 APPGROUP을 위에서 생성한 App Group Identifier**로 변경해야 합니다.

```objc
#import "SampleHandler.h"
@import TXLiteAVSDK_ReplayKitExt;

#define APPGROUP @"group.com.tencent.liteav.RPLiveStreamShare"

@interface SampleHandler() <TXReplayKitExtDelegate>
@end

@implementation SampleHandler
// 주의사항: 해당 단계의 APPGROUP을 앞서 생성한 App Group Identifier로 변경해야 합니다.
- (void)broadcastStartedWithSetupInfo:(NSDictionary<NSString *,NSObject *> *)setupInfo {
    [[TXReplayKitExt sharedInstance] setupWithAppGroup:APPGROUP delegate:self];
}

- (void)broadcastPaused {
    // User has requested to pause the broadcast. Samples will stop being delivered.
}

- (void)broadcastResumed {
    // User has requested to resume the broadcast. Samples delivery will resume.
}

- (void)broadcastFinished {
    [[TXReplayKitExt sharedInstance] finishBroadcast];
    // User has requested to finish the broadcast.
}

#pragma mark - TXReplayKitExtDelegate
- (void)broadcastFinished:(TXReplayKitExt *)broadcast reason:(TXReplayKitExtReason)reason
{
    NSString *tip = @"";
    switch (reason) {
        case TXReplayKitExtReasonRequestedByMain:
            tip = @"화면 공유 종료됨";
            break;
        case TXReplayKitExtReasonDisconnected:
            tip = @"애플리케이션 종료";
            break;
        case TXReplayKitExtReasonVersionMismatch:
            tip = @"통합 오류(SDK 버전 불일치)";
            break;
    }

    NSError *error = [NSError errorWithDomain:NSStringFromClass(self.class)
                                         code:0
                                     userInfo:@{
                                         NSLocalizedFailureReasonErrorKey:tip
                                     }];
    [self finishBroadcastWithError:error];
}

- (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType {
    switch (sampleBufferType) {
        case RPSampleBufferTypeVideo:
            [[TXReplayKitExt sharedInstance] sendVideoSampleBuffer:sampleBuffer];
            break;
        case RPSampleBufferTypeAudioApp:
            // Handle audio sample buffer for app audio
            break;
        case RPSampleBufferTypeAudioMic:
            // Handle audio sample buffer for mic audio
            break;
            
        default:
            break;
    }
}
@end
```

<span id="receive"> </span>
#### 3단계: 메인 App의 수신 로직 연결
다음 절차에 따라 메인 App의 수신 로직에 연결합니다. 즉, 사용자가 화면 공유를 시작하기 전에 메인 App이 언제든지 Broadcast Upload Extension 프로세스에서 보내는 화면 녹화 데이터를 수신 가능하도록 "대기" 상태에 있어야 합니다. 
1. TRTCCloud 카메라 캡처가 비활성화되었는지 확인합니다. 비활성화되지 않은 경우 [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3)를 호출하여 카메라 캡처를 비활성화합니다.
2. [startScreenCaptureByReplaykit:appGroup:](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff) 방법을 호출하고 [1단계](#createGroup)에서 설정한 AppGroup을 전달하여 SDK를 “대기” 상태로 전환합니다.
3. 사용자가 화면 공유를 시작할 때까지 기다립니다. [4단계](# launch)의 “트리거 버튼”이 구현되지 않은 경우에는 사용자가 iOS 시스템의 제어 센터에서 화면 녹화 버튼을 길게 눌러 트리거해야만 화면 공유가 가능하며, 해당 조작 과정은 다음 그림과 같습니다.
4. [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) 인터페이스를 호출하여 언제든지 화면 공유를 중단할 수 있습니다.

```
// 화면 공유를 시작하려면 APPGROUP을 앞서 생성한 App Group Identifier로 변경해야 합니다.
- (void)startScreenCapture {
    TRTCVideoEncParam *videoEncConfig = [[TRTCVideoEncParam alloc] init];
    videoEncConfig.videoResolution = TRTCVideoResolution_1280_720;
    videoEncConfig.videoFps = 10;
    videoEncConfig.videoBitrate = 2000;
    //APPGROUP을 앞서 생성한 App Group Identifier로 변경해야 합니다.
    [[TRTCCloud sharedInstance] startScreenCaptureByReplaykit:videoEncConfig
                                                     appGroup:APPGROUP];
}

// 화면 공유를 종료합니다.
- (void)stopScreenCapture {
    [[TRTCCloud sharedInstance] stopScreenCapture];
}

// 화면 공유 실행 이벤트 알림은 TRTCCloudDelegate를 통해 수신할 수 있습니다.
- (void)onScreenCaptureStarted {
    [self showTip:@"화면 공유 시작"];
}
```

<span id="launch"> </span>
#### 4단계: 화면 공유 트리거 버튼 추가(옵션)
[3단계](#receive)까지는 화면 공유 시 사용자가 제어 센터에서 녹화 버튼을 길게 눌러야만 수동으로 실행되는 방법입니다. 이제 VooV Meeting과 유사하게 버튼 클릭으로 트리거할 수 있는 방법을 소개하겠습니다.

1. [Demo]에서 `TRTCBroadcastExtensionLauncher` 클래스를 찾아 프로그램에 추가합니다.
2. 프로그램 인터페이스에 버튼을 만들고, 해당 버튼의 상응하는 함수에 `TRTCBroadcastExtensionLauncher`의 `launch` 함수를 호출하면 화면 공유 기능이 요청됩니다.

```
 // 사용자 정의 버튼 응답 방법
 - (IBAction)onScreenButtonTapped:(id)sender {
    [TRTCBroadcastExtensionLauncher launch];
}
```

>!
애플은 iOS 12.0에 `RPSystemBroadcastPickerView`를 추가하여 애플리케이션에서 런처를 팝업할 수 있도록 함으로써 사용자가 화면 공유 여부를 확인할 수 있도록 했습니다. `RPSystemBroadcastPickerView`는 현재까지는 아직 커스텀 인터페이스를 지원하지 않고 있으며 공식적인 호출 방법도 없습니다.
>- TRTCBroadcastExtensionLauncher의 작동 원리는 `RPSystemBroadcastPickerView`의 하위 View를 순회하여, UIButton을 찾고 클릭 이벤트를 트리거하는 방식입니다.
> - **그러나 이 솔루션은 애플에서 공식적으로 권장하는 방식이 아니며, 신규 시스템 업데이트에서 무효화될 수도 있기 때문에 [4단계](#launch)는 단순 선택사항으로 해당 솔루션 적용 시 사용자가 위험을 감수해야 합니다.**

## 공유 화면 보기
- **Mac / Window 공유 화면 보기**
  방 안에 있는 Mac / Windows 사용자가 화면 공유를 시작하면 서브스트림을 통해 공유가 진행됩니다. 방 안의 다른 사용자는 TRTCCloudDelegate의 [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) 이벤트를 통해 이 알림을 받습니다.
  공유 화면을 보고 싶은 사용자는 [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) 인터페이스를 통해 원격 사용자의 서브 스트림 화면을 렌더링할 수 있습니다.

- **Android / iOS 공유 화면 보기**
  사용자가 Android/iOS를 통해 화면 공유를 시작하면 메인스트림을 통해 공유가 진행됩니다. 방 안의 다른 사용자들은 TRTCCloudDelegate의 [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트를 통해 이 알림을 받습니다.
  공유 화면을 보고 싶은 사용자는 [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) 인터페이스를 통해 원격 사용자의 메인 스트림 화면을 렌더링할 수 있습니다.







