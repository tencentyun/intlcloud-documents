Tencent Cloud TRTC는 iOS 플랫폼에서 두 가지 화면 공유 방법을 지원합니다.
- **애플리케이션 내 공유**
현재 App 화면만 공유할 수 있으며, 해당 기능은 iOS 13 버전 이상의 운영 체제에서만 지원합니다. 현재 App 이외의 화면 콘텐츠는 공유할 수 없어 개인정보 보호 요구가 높은 시나리오에 적합합니다.

- **애플리케이션 간 공유**
애플의 Replaykit 솔루션을 기반으로 시스템 전체의 화면 콘텐츠 공유가 가능합니다. 다만, 현재 App에서 별도로 Extension 확장 컴포넌트를 제공해야 하므로 애플리케이션 내 공유 대비 연결 절차가 더 많습니다.

>! 주의해야 할 점은 TRTC SDK의 모바일 버전이 데스크톱 버전과 같이 “서브 채널 공유”를 지원하지 않는다는 것입니다. iOS와 Android 시스템은 모두 백그라운드에서 실행되는 App에 카메라 사용 권한을 제한하여 서브 채널 공유의 의미가 그리 크지 않습니다.

## 지원 플랫폼

| iOS | Android | Mac OS | Windows |Electron| WeChat 미니프로그램 | Chrome 브라우저|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## 애플리케이션 내 공유

애플리케이션 내 공유 방법은 간단합니다. TRTC SDK가 제공하는 인터페이스 [startScreenCaptureInApp](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5dbd40c4ad65152e85591c8535b4ee90)을 호출하여 코드 매개변수 `TRTCVideoEncParam`를 전송하기만 하면 됩니다. 해당 매개변수는 nil로 설정할 수 있으며, 이 때 SDK는 화면 공유 전 코드 매개변수를 사용하게 됩니다.

iOS 화면 공유에 권장되는 코드 매개변수는 다음과 같습니다.

| 매개변수 항목 | 매개변수 명칭 | 일반 권장 값 |  텍스트 교육 시나리오 |
|---------|---------|---------|-----|
| 해상도 | videoResolution | 1280 × 720 | 1920 × 1080 |
| 프레임 레이트 | videoFps | 10 FPS | 8 FPS |
| 최고 비트 레이트| videoBitrate| 1600 kbps | 2000 kbps |
| 해상도 어댑티브 | enableAdjustRes | NO | NO |

- 일반적으로 화면 공유의 콘텐츠는 변동이 심하지 않으므로 FPS를 높게 설정하는 경우 금액 부담이 심해지므로 10 FPS로 설정하기를 권장합니다.
- 공유하는 화면 콘텐츠에 텍스트가 많이 포함되어 있는 경우 해상도와 비트 레이트 설정을 적합하게 향상시킬 수 있습니다.
- 최고 비트 레이트(videoBitrate)란 화면 변화가 심할 때의 최고 출력 비트 레이트를 의미하며, 화면 콘텐츠 변화가 비교적 적은 경우에는 실제 인코딩 비트 레이트가 비교적 낮습니다.


## 애플리케이션 간 공유

### 예시 코드
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo/)의 **Screen** 디렉터리에 애플리케이션 간 공유 예시 코드가 포함되어 있으며, 다음 파일이 포함되어 있습니다.

```
├─ TRTCSimpleDemo              // TRTC 간소화 Demo
|  ├─ Screen                   // 애플리케이션 간 화면 공유 기능 예시
|  |  ├─ RTC                   // TRTC에서 통화 모드 실행을 위한 예시 코드, 해당 모드에서는 역할 개념이 없음
|  |  |  ├─ TXReplayKit_Screen // 녹화 프로세스 Broadcast Upload Extension 코드는 2단계 참조
|  |  |  |  ├─ SampleHandler.swift // 시스템 녹화 데이터 수신에 사용
|  |  |  |  ├─ Info.plist                          
|  |  |  |  ├─ TXReplayKit_Screen.entitlements //프로세스 간에 통신하는 AppGroup 정보 설정에 사용
|  |  |  
|  |  ├─ ScreenEntranceViewController.swift    // 기능으로 들어가는 인터페이스
|  |  ├─ ScreenViewController.swift            // 녹화 상태 표시 인터페이스
|  |  ├─ TRTCBroadcastExtensionLauncher.swift  // 시스템 녹화 알람에 사용하는 보조 코드
```

[README](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCSimpleDemo/README.md)의 가이드를 통해 해당 예시 Demo를 제작할 수 있습니다.


### 연결 절차

iOS 시스템에서의 애플리케이션 간 화면 공유 시에는 메인 App 프로세스에 맞춰 푸시 스트림을 진행해야 하므로 Extension 녹화 프로세스를 추가해야 합니다. Extension 녹화 프로세스는 시스템에서 녹화가 필요할 때 생성하며 시스템이 수집한 화면 이미지를 수신합니다. 따라서 다음 절차가 필요합니다.

1. App Group을 생성하고 XCode에서 설정(선택사항)을 진행합니다. 이는 Extension 녹화 프로세스가 메인 App 프로세스와 프로세스 간 통신을 진행하기 위한 절차입니다.
2. 프로그램에 Broadcast Upload Extension의 Target을 생성하고, 여기에 SDK 압축 패키지 중 확장 모듈을 위해 사용자 정의된 `TXLiteAVSDK_ReplayKitExt.framework`를 통합합니다.
3. 메인 App의 수신 로직과 연결하여 메인 App이 Broadcast Upload Extension에서 수신되는 녹화 데이터를 기다리게 합니다.
4. Demo에서 사전에 실행한 helper class(RPSystemBroadcastPickerView`)를 사용하여 VooV Meeting 시뮬레이션 iOS 버전에서 버튼 하나를 클릭하면 화면 공유 알람 효과(선택사항)를 구현할 수 있습니다.

>! 1단계를 건너뛴 경우, 즉 App Group을 설정하지 않은 경우(인터페이스 nil로 전송)에도 화면 공유를 실행할 수 있습니다. 그러나 안정성이 저하되는 문제가 발생하므로 절차가 많아도 최대한 정확한 App Group을 설정하여 화면 공유 기능의 안정성을 확보하십시오.

<span id="createGroup"> </span>
#### 1단계: App Group 생성
Tencent Cloud 계정을 사용하여 [**https://developer.apple.com/**](https://developer.apple.com/)에 로그인해 다음 작업을 완료합니다. **작업 완료 후 상응하는 Provisioning Profile을 다시 다운로드해야 합니다**.

1. [Certificates, IDs & Profiles]을 클릭합니다.
2. 오른쪽에 있는 + 버튼을 클릭합니다.
3. [App Groups]를 선택하고 [Continue]를 클릭합니다.
4. 팝업되는 테이블에 Description 및 Identifier를 입력합니다. Identifier에는 인터페이스에 전송되는 상응하는 AppGroup 매개변수가 필요합니다. 완료 후 [Continue]를 클릭합니다.
 ![](https://main.qcloudimg.com/raw/43dd60f5053b21c167ee3a8dbe7d16f9/Create_AppGroup.jpg)
5. Identifier 페이지로 돌아와 왼쪽 상단 메뉴에서 [App IDs]를 선택한 후 App ID(메인 App과 Extension의 AppID는 동일하게 설정해야 함)를 클릭합니다.
6. [App Groups]를 선택하고 [Edit]을 클릭합니다.
7. 팝업되는 테이블에서 방금 생성한 App Group을 선택하고 [Continue]를 선택하면 편집 페이지로 돌아오고, [Save]를 클릭하면 저장됩니다.
 ![](https://main.qcloudimg.com/raw/962c1b705433aa62c9617f90d28238c5/Apply_AppGroup.jpg)
8. Provisioning Profile을 다시 다운로드하고 XCode에 설정합니다.

<span id="createExtension"> </span>
#### 2단계: Broadcast Upload Extension 생성
1. Xcode 메뉴에서 순서대로 [File], [New], [Target...]을 클릭한 후 [Broadcast Upload Extension]을 선택합니다.
2. 팝업되는 대화 상자에 관련 정보를 입력합니다. [Include UI Extension]을 선택할 **필요 없으며** [Finish]를 클릭하여 생성합니다.
3. 다운로드한 SDK 압축 패키지 중 TXLiteAVSDK_ReplayKitExt.framework를 프로그램으로 드래그하고 방금 생성한 Target을 선택합니다.
4. 추가한 Target을 선택한 후, 순서대로 [+ Capability]를 클릭한 뒤 [App Groups]를 더블 클릭합니다. 다음 이미지를 참조하십시오.
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 작업 완료 후 다음 이미지와 같이 문서 리스트에 `Target 이름.entitlements`로 된 파일을 생성하고, 해당 문서를 선택한 뒤 + 버튼을 클릭하여 상기 App Group을 입력하면 됩니다.
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. 메인 App의 Target을 선택하고 **상기 메인 App의 Target과 동일하게 처리합니다.**
6. 신규 생성한 Target은 Xcode에서 자동으로 "SampleHandler.m" 파일을 생성하며 다음과 같이 코드를 변경하는데 사용합니다. **코드 상의 APPGROUP을 위에서 생성한 App Group Identifier로 변경해야 합니다.**

```objc
#import "SampleHandler.h"
@import TXLiteAVSDK_ReplayKitExt;

#define APPGROUP @"group.com.tencent.liteav.RPLiveStreamShare"

@interface SampleHandler() <TXReplayKitExtDelegate>
@end

@implementation SampleHandler
// 주의사항: 해당 부분 APPGROUP을 위에서 생성한 App Group Identifier로 변경해야 합니다.
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
다음과 같이 메인 App의 수신 로직을 연결합니다. 이는 사용자가 화면 공유 트리거 전, 항상 Broadcast Upload Extension 프로세스의 녹화 데이터를 수신할 수 있도록 메인 App을 “대기” 상태로 만드는 작업입니다.
1. TRTCCloud 카메라 캡처가 비활성화되었는지 확인해 주시고, 비활성화되지 않은 경우 [stopLocalPreview](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3)를 호출하여 카메라 캡처를 비활성화합니다.
2. [startScreenCaptureByReplaykit:appGroup:](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff)을 호출하고 [1단계](#createGroup)에서 설정한 AppGroup을 전송하여 SDK를 “대기” 상태로 만듭니다.
3. 사용자의 화면 공유 트리거를 대기합니다. [4단계](#launch) “트리거 버튼”을 구현하지 않는 경우 사용자가 iOS 시스템 제어 센터에서 녹화 버튼을 길게 눌러 트리거해야 화면을 공유할 수 있으며, 해당 작업 절차는 다음 이미지와 같습니다.
4. [stopScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) 인터페이스를 호출하여 언제든지 화면 공유를 중단할 수 있습니다.

```
// 화면 공유를 시작하려면 APPGROUP을 위에서 생성한 App Group Identifier로 변경해야 합니다.
- (void)startScreenCapture {
    TRTCVideoEncParam *videoEncConfig = [[TRTCVideoEncParam alloc] init];
    videoEncConfig.videoResolution = TRTCVideoResolution_1280_720;
    videoEncConfig.videoFps = 10;
    videoEncConfig.videoBitrate = 2000;
		//APPGROUP을 위에서 생성한 App Group Identifier로 변경해야 합니다.
    [[TRTCCloud sharedInstance] startScreenCaptureByReplaykit:videoEncConfig
                                                     appGroup:APPGROUP];
}

// 화면 공유 종료
- (void)stopScreenCapture {
    [[TRTCCloud sharedInstance] stopScreenCapture];
}

// 화면 공유 실행 이벤트 통지는 TRTCCloudDelegate를 통해 수신할 수 있습니다.
- (void)onScreenCaptureStarted {
    [self showTip:@"화면 공유 시작"];
}
```

<span id="launch"> </span>
#### 4단계: 화면 공유 트리거 버튼 추가(선택 사항)
[3단계](#receive)까지는 화면 공유 시 사용자가 제어 센터에서 녹화 버튼을 길게 눌러야만 수동으로 실행되는 방법입니다. 이제 VooV Meeting과 유사하게 버튼 클릭으로 트리거할 수 있는 방법을 소개하겠습니다.

1. [Demo](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo/Screen)에서 `TRTCBroadcastExtensionLauncher` 유형을 찾아 프로그램에 추가합니다.
2. 프로그램 인터페이스에 버튼을 만들고, 해당 버튼의 상응하는 함수에 `TRTCBroadcastExtensionLauncher`의 `launch` 함수를 호출하면 화면 공유 기능이 요청됩니다.
```
// 사용자 정의 버튼 응답 방법
- (IBAction)onScreenButtonTapped:(id)sender {
    [TRTCBroadcastExtensionLauncher launch];
}
```

>! 애플은 iOS 12.0에 `RPSystemBroadcastPickerView`가 추가되어 애플리케이션에서 실행 프로그램이 팝업되어 사용자가 화면 공유 실행을 확인할 수 있습니다. 현재 `RPSystemBroadcastPickerView`는 사용자 정의 인터페이스를 지원하지 않으며 공식 요청 방법도 존재하지 않습니다.
>TRTCBroadcastExtensionLauncher는 `RPSystemBroadcastPickerView`의 서브 View가 UIButton을 찾아 해당 버튼 이벤트를 트리거하는 원리입니다.
> **해당 방법은 APPLE에서 공식적으로 권장하는 방법이 아니므로 시스템 업데이트 시 유효하지 않을 수 있습니다. 따라서 [4단계](#launch)는 선택 사항으로, 해당 방법을 이용하는 데에 따른 리스크가 발생할 수 있으며 본사는 이에 대한 책임을 지지 않습니다.**

## 화면 공유 보기
- **Mac/Window 화면 공유 보기**
  방 안에 있는 Mac/Windows 사용자가 화면 공유 기능을 실행하면 서브스트림을 통해 화면이 공유됩니다. 방 안의 다른 사용자들은 TRTCCloudDelegate의 [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) 이벤트를 통해 해당 통지를 수신합니다.
  공유 화면을 보고 싶은 사용자는 [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) 인터페이스를 통해 사용자의 서브스트림 화면의 원격 렌더링을 활성화할 수 있습니다.

- **Android/iOS 화면 공유 보기**
  사용자가 Android/iOS를 통해 화면을 공유하는 경우 주요 화면을 공유합니다. 방 안의 다른 사용자들은 TRTCCloudDelegate의 [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트를 통해 통지를 수신합니다.
  공유 화면을 보고 싶은 사용자는 [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) 인터페이스를 통해 사용자의 주요 화면의 원격 렌더링을 활성화할 수 있습니다.







