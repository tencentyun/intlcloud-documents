## Android 플랫폼 기반
Tencent Cloud TRTC는 Android 시스템에서 화면 공유를 지원하며, TRTC SDK를 통해 현재 시스템의 화면 콘텐츠를 방 안의 다른 사용자에게 공유합니다. 이 기능에 관한 주의 사항은 다음과 같습니다.

- TRTC Android 버전의 화면 공유는 데스크톱 버전처럼 '서브 채널 공유'를 지원하지 않으므로, 화면 공유 실행 시 먼저 카메라의 수집을 중지하지 않으면 충돌이 발생할 수 있습니다.
- Android 시스템의 백그라운드 App이 지속적으로 CPU를 사용할 경우 시스템에 의해 강제로 종료될 수 있으며, 화면 공유 자체도 CPU를 소모하게 됩니다. 이 충돌을 해결하려면 App에서 화면 공유를 실행함과 동시에 Android 시스템에 플로팅 창을 팝업해야 합니다. Android는 포그라운드 UI의 App 프로세스를 강제 종료하지 않으므로, 해당 방법을 사용하면 다음과 같이 사용자의 App이 계속해서 화면 공유를 진행하고 자동으로 회수되지 않습니다. 


### 화면 공유 실행
Android의 화면 공유를 활성화하고 `TRTCCloud`의 [startScreenCapture()](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html) 인터페이스를 호출합니다. 단, 선명하고 안정적인 화면 공유를 위해 다음 세 가지 문제에 유의해야 합니다.

#### Activity 추가
manifest 파일에 다음 activity를 붙여넣습니다. 프로젝트 코드에 있을 경우에는 추가할 필요 없습니다.
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

#### 비디오 인코딩 매개변수 설정
[startScreenCapture()](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html)의 첫 번째 매개변수인 `encParams` 설정을 통해 화면 공유의 인코딩 품질을 지정할 수 있습니다. `encParams`를 null로 지정할 경우 SDK는 자동으로 이전에 설정한 인코딩 매개변수를 사용합니다. 매개변수 권장 설정값은 다음과 같습니다.

| 매개변수 항목 | 매개변수 이름 | 일반 권장 값 |  텍스트 교육 시나리오 |
|---------|---------|---------|-----|
| 해상도 | videoResolution | 1280 × 720 | 1920 × 1080 |
| 프레임 레이트 | videoFps | 10 FPS | 8 FPS |
| 최대 비트 레이트| videoBitrate| 1600 kbps | 2000 kbps |
| 해상도 어댑티브 | enableAdjustRes | NO | NO |
>?
>- 일반적으로 화면 공유 콘텐츠는 많은 변화가 없으므로 FPS를 높게 설정하는 것은 비경제적입니다. 권장 설정값은 10FPS입니다.
>- 공유하는 화면 콘텐츠에 텍스트가 많이 포함되어 있는 경우 해상도와 비트 레이트를 알맞게 높이는 것이 좋습니다.
>- 최대 비트 레이트(videoBitrate)란 화면 변화가 심할 때 최대로 출력되는 비트 레이트를 의미하며, 화면 콘텐츠의 변화가 적은 경우 실제 인코딩 비트 레이트는 비교적 낮습니다.

#### 팝업 플로팅 창의 강제 종료 방지
Android 7.0 시스템부터 백그라운드에서 실행되는 일반적인 App 프로세스는 CPU가 사용되고 있을 경우 시스템에 의해 강제 종료되는 현상이 쉽게 발생합니다. 그러므로 App이 백그라운드에서 화면을 공유하고 있을 때 플로팅 창 팝업을 통해 시스템에 의해 강제 종료되는 것을 막을 수 있습니다. 또한 휴대폰 화면에 플로팅 창을 표시하면 사용자에게 현재 화면 공유 중임을 알려 사용자의 프라이버시 노출을 방지할 수 있습니다.

##### 방법: 일반 플로팅 창 팝업
'VooV Meeting'과 유사한 미니 플로팅 창을 팝업합니다. 예시 코드 [tool.dart](https://github.com/c1avie/trtc_demo/blob/master/lib/page/trtcmeetingdemo/tool.dart)를 참고하십시오.
```
//화면 공유 시 미니 플로팅 창을 팝업해 백그라운드 애플리케이션으로 전환되어 강제 종료되는 현상 방지
  static void showOverlayWindow() {
    SystemWindowHeader header = SystemWindowHeader(
      title: SystemWindowText(
          text: "화면 공유 중", fontSize: 14, textColor: Colors.black45),
      decoration: SystemWindowDecoration(startColor: Colors.grey[100]),
    );
    SystemAlertWindow.showSystemWindow(
      width: 18,
      height: 95,
      header: header,
      margin: SystemWindowMargin(top: 200),
      gravity: SystemWindowGravity.TOP,
    );
  }
```

## iOS 플랫폼 기반
- **[애플리케이션 내 공유](#Internal)**
현재 App의 화면만 공유할 수 있다는 의미입니다. 해당 기능은 iOS 13 버전 이상의 운영 체제에서만 지원됩니다. 현재 App 이외의 화면 콘텐츠를 공유할 수 없으므로 높은 수준의 개인 정보 보호가 필요한 시나리오에 적합합니다.
- **[애플리케이션 간 공유](#Cross)**
Apple의 Replaykit 솔루션을 기반으로 시스템 전체의 화면 콘텐츠 공유가 가능합니다. 단, 현재 App에서 별도로 Extension 확장 모듈을 제공해야 하므로 애플리케이션 내 공유보다 연결 절차가 더 많습니다.

>! TRTC SDK의 모바일 버전은 데스크톱 버전처럼 '서브 채널 공유'를 지원하지 않는다는 것에 주의하십시오. iOS와 Android 시스템은 모두 백그라운드에서 실행되는 App에 카메라 사용 권한을 제한하므로 서브 채널을 공유해도 큰 효과가 없습니다.

[](id:Internal)
### 방법1: iOS 플랫폼에서의 애플리케이션 내 공유

애플리케이션 내 공유 방법은 매우 간단합니다. TRTC SDK에서 제공하는 [startScreenCapture](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html) 인터페이스를 호출하여 인코딩 매개변수 `TRTCVideoEncParam`을 전송하고 매개변수 `appGroup`을 `''`로 설정하면 됩니다. `TRTCVideoEncParam` 매개변수는 null로 설정할 수 있으며, 이때 SDK는 화면 공유 전에 설정된 인코딩 매개변수를 사용합니다.

iOS 화면 공유 시 다음과 같은 인코딩 매개변수를 권장합니다.

| 매개변수 항목 | 매개변수 이름 | 일반 권장 값 |  텍스트 교육 시나리오 |
|---------|---------|---------|-----|
| 해상도 | videoResolution | 1280 × 720 | 1920 × 1080 |
| 프레임 레이트 | videoFps | 10 FPS | 8 FPS |
| 최대 비트 레이트| videoBitrate| 1600 kbps | 2000 kbps |
| 해상도 어댑티브 | enableAdjustRes | NO | NO |

>?
>- 일반적으로 화면 공유 콘텐츠는 많은 변화가 없으므로 FPS를 높게 설정하는 것은 비경제적입니다. 권장 설정값은 10FPS입니다.
>- 공유하는 화면 콘텐츠에 텍스트가 많이 포함되어 있는 경우 해상도와 비트 레이트를 알맞게 높이는 것이 좋습니다.
>- 최대 비트 레이트(videoBitrate)란 화면 변화가 심할 때 최대로 출력되는 비트 레이트를 의미하며, 화면 콘텐츠의 변화가 적은 경우 실제 인코딩 비트 레이트는 비교적 낮습니다.

[](id:Cross)
### 방법2: iOS 플랫폼에서의 애플리케이션 간 공유

#### 예시 코드
[Github](https://github.com/c1avie/trtc_demo)의 **trtc_demo/ios** 디렉터리에 애플리케이션 간 공유 예시 코드가 저장되어 있으며, 다음 파일이 포함되어 있습니다.

```
├── Broadcast.Upload        //녹화 프로세스 Broadcast Upload Extension 코드는 2단계 참고
│   ├── Broadcast.Upload.entitlements       //프로세스 간에 통신하는 AppGroup 정보 설정에 사용
│   ├── Broadcast.UploadDebug.entitlements  //프로세스 간에 통신하는 AppGroup 정보 설정에 사용(debug 환경)
│   ├── Info.plist
│   └── SampleHandler.swift     // 시스템 녹화 데이터 수신에 사용
├── Resource                    // 리소스 파일
├── Runner                      // TRTC 라이트 Demo
├── TXLiteAVSDK_ReplayKitExt.framework      //TXLiteAVSDK_ReplayKitExt SDK
```

[README](https://github.com/c1avie/trtc_demo/blob/master/README.md)의 가이드를 참고하여 해당 예시 Demo를 실행할 수 있습니다.


#### 연결 절차
iOS 시스템에서 애플리케이션 간 화면 공유 시 메인 App 프로세스의 푸시 스트림을 위해 Extension 녹화 프로세스를 추가해야 합니다. Extension 녹화 프로세스는 화면을 녹화해야 할 때 시스템에서 생성하며, 시스템에서 수집한 화면 이미지를 수신합니다. 따라서 다음과 같은 절차를 수행해야 합니다.
1. App Group을 생성하고 XCode에서 설정(옵션)을 진행합니다. Extension 녹화 프로세스와 메인 App 프로세스 간의 통신을 가능하게 하는 과정입니다.
2. 프로그램에 Broadcast Upload Extension의 Target을 생성하고, 여기에 SDK 압축 패키지 중 확장 모듈을 위해 사용자 정의된 `TXLiteAVSDK_ReplayKitExt.framework`를 통합합니다.
3. 메인 App이 Broadcast Upload Extension에서 수신되는 녹화 데이터를 대기하도록 메인 App의 수신 로직과 연결합니다.
4. `pubspec.yaml` 파일을 편집하고 `replay_kit_launcher` 플러그 인을 가져와 TRTC Demo Screen에서 버튼 하나만 클릭하면 화면 공유 효과(옵션)를 호출하는 것과 유사한 기능을 구현합니다.
```
# trtc sdk와 replay_kit_launcher 가져오기
dependencies:
  tencent_trtc_cloud: ^0.2.1
  replay_kit_launcher: ^0.2.0+1
```

>! [1단계](#Step1)를 건너뛴 경우, 즉 App Group을 설정하지 않은 경우(인터페이스가 null 전송)에도 화면 공유를 실행할 수 있습니다. 그러나 안정성이 저하되는 문제가 발생하므로, 절차가 많더라도 최대한 정확한 App Group을 설정하여 화면 공유 기능의 안정성을 확보하십시오.

[](id:createGroup)[](id:Step1)
#### 1단계: App Group 생성
사용자 계정으로 [**https://developer.apple.com/**](https://developer.apple.com/)에 로그인하여 다음 작업을 완료합니다. **작업 완료 후 해당 Provisioning Profile을 다시 다운로드해야 합니다**.

1. [Certificates, IDs & Profiles]를 클릭합니다.
2. 오른쪽 인터페이스에서 + 버튼을 클릭합니다.
3. [App Groups]를 선택하고 [Continue]를 클릭합니다.
4. 팝업된 테이블에 Description과 Identifier를 입력합니다. Identifier는 인터페이스의 해당 AppGroup 매개변수를 전송해야 합니다. 설정 완료 후 [Continue]를 클릭합니다.
 ![](https://main.qcloudimg.com/raw/43dd60f5053b21c167ee3a8dbe7d16f9/Create_AppGroup.jpg)
5. Identifier 페이지로 돌아와 왼쪽 상단 메뉴에서 [App IDs]를 선택한 후 사용자의 App ID(메인 App과 Extension AppID는 동일하게 설정해야 함)를 클릭합니다.
6. [App Groups]를 선택하고 [Edit]을 클릭합니다.
7. 팝업된 테이블에서 방금 생성한 App Group을 선택한 후 [Continue]를 선택하면 편집 페이지가 반환됩니다. [Save]를 클릭하여 저장합니다.
![](https://main.qcloudimg.com/raw/962c1b705433aa62c9617f90d28238c5/Apply_AppGroup.jpg)
8. Provisioning Profile을 다시 다운로드하고 XCode에 설정합니다.

[](id:createExtension)
#### 2단계: Broadcast Upload Extension 생성
1. Xcode 메뉴에서 순서대로 [File]>[New]>[Target...]을 클릭한 후 [Broadcast Upload Extension]을 선택합니다.
2. 팝업되는 대화 상자에 관련 정보를 입력합니다. [Include UI Extension]을 선택할 **필요 없으며** [Finish]를 클릭하여 생성합니다.
3. 다운로드한 SDK 압축 패키지의 TXLiteAVSDK_ReplayKitExt.framework를 프로그램에 드래그하고 방금 생성한 Target을 선택합니다.
4. 추가한 Target을 선택한 후, 순서대로 [+ Capability]를 클릭한 다음 [App Groups]를 더블 클릭합니다. 다음 이미지를 참고하십시오.
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 작업을 완료하면 파일 리스트에 `Target 이름.entitlements`라는 파일이 생성됩니다. 다음 이미지와 같이 해당 파일을 선택한 후 + 버튼을 클릭하여 상기 App Group을 입력하면 됩니다.
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. 메인 App의 Target을 선택하고 **메인 App의 Target도 위의 단계에 따라 동일하게 처리합니다.**
6. Target 생성 과정에서 Xcode는 'SampleHandler.swift'라는 이름의 파일을 자동으로 생성하고 다음과 같은 코드로 대체합니다. **코드의 APPGROUP을 위에서 생성한 App Group Identifier로 변경해야 합니다.**
<dx-codeblock>
::: iOS swift

import ReplayKit
import TXLiteAVSDK_ReplayKitExt


let APPGROUP = "group.com.tencent.comm.trtc.demo"

class SampleHandler: RPBroadcastSampleHandler, TXReplayKitExtDelegate {

    let recordScreenKey = Notification.Name.init("TRTCRecordScreenKey")
    
    override func broadcastStarted(withSetupInfo setupInfo: [String : NSObject]?) {
        // User has requested to start the broadcast. Setup info from the UI extension can be supplied but optional.
        TXReplayKitExt.sharedInstance().setup(withAppGroup: APPGROUP, delegate: self)
    }
    
    override func broadcastPaused() {
        // User has requested to pause the broadcast. Samples will stop being delivered.
    }
    
    override func broadcastResumed() {
        // User has requested to resume the broadcast. Samples delivery will resume.
    }
    
    override func broadcastFinished() {
        // User has requested to finish the broadcast.
        TXReplayKitExt.sharedInstance() .finishBroadcast()
    }
    
    func broadcastFinished(_ broadcast: TXReplayKitExt, reason: TXReplayKitExtReason) {
        var tip = ""
        switch reason {
        case TXReplayKitExtReason.requestedByMain:
            tip = "화면 공유 종료됨"
            break
        case TXReplayKitExtReason.disconnected:
            tip = "애플리케이션 종료"
            break
        case TXReplayKitExtReason.versionMismatch:
            tip = "통합 오류(SDK 버전 번호 불일치)"
            break
        default:
            break
        }
        
        let error = NSError(domain: NSStringFromClass(self.classForCoder), code: 0, userInfo: [NSLocalizedFailureReasonErrorKey:tip])
        finishBroadcastWithError(error)
    }
    
    override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer, with sampleBufferType: RPSampleBufferType) {
        switch sampleBufferType {
        case RPSampleBufferType.video:
            // Handle video sample buffer
            TXReplayKitExt.sharedInstance() .sendVideoSampleBuffer(sampleBuffer)
            break
        case RPSampleBufferType.audioApp:
            // Handle audio sample buffer for app audio
            break
        case RPSampleBufferType.audioMic:
            // Handle audio sample buffer for mic audio
            break
        @unknown default:
            // Handle other sample buffer types
            fatalError("Unknown type of sample buffer")
        }
    }
}
:::
</dx-codeblock>

[](id:receive)
#### 3단계: 메인 App의 수신 로직 연결
다음 절차에 따라 메인 App의 수신 로직에 연결합니다. 사용자가 화면 공유를 트리거하기 전에 메인 App이 언제든지 Broadcast Upload Extension 프로세스에서 보내는 녹화 데이터를 수신할 수 있도록 '대기' 상태가 되어야 합니다.
1. TRTCCloud 카메라 수집이 비활성화되었는지 확인합니다. 비활성화되지 않은 경우 [stopLocalPreview](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalPreview.html)를 호출하여 카메라 수집을 비활성화하십시오.
2. [startScreenCapture](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html)를 호출하고 [1단계](#createGroup)에서 설정한 AppGroup을 전송하여 SDK를 '대기' 상태로 전환합니다.
3. 사용자가 화면 공유를 시작할 때까지 기다립니다. [4단계](# launch)의 “트리거 버튼”이 구현되지 않은 경우에는 사용자가 iOS 시스템의 제어 센터에서 화면 녹화 버튼을 길게 눌러 트리거해야만 화면 공유가 가능하며, 해당 조작 과정은 다음 그림과 같습니다.

4. [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) 인터페이스를 호출하여 언제든지 화면 공유를 중단할 수 있습니다.
<dx-codeblock>
::: dart 
// 화면 공유를 시작하려면 APPGROUP을 앞서 생성한 App Group으로 변경해야 합니다. 
trtcCloud.startScreenCapture(
    TRTCVideoEncParam(
        videoFps: 10,
        videoResolution: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720,
        videoBitrate: 1600,
        videoResolutionMode: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT,
    ),
    iosAppGroup,
);

// 화면 공유 종료
await trtcCloud.stopScreenCapture();


// 화면 공유 실행 이벤트 공지는 TRTCCloudListener를 통해 수신할 수 있습니다.
onRtcListener(type, param){
    if (type == TRTCCloudListener.onScreenCaptureStarted) {
      //화면 공유 시작
    }
}
:::
</dx-codeblock>

[](id:launch)
#### 4단계: 화면 공유 트리거 버튼 추가(옵션)
[3단계](#receive)까지 화면 공유는 사용자가 제어 센터에서 녹화 버튼을 길게 눌러 수동으로 실행하는 방법입니다. 이와 달리 TRTC Demo Screen과 유사하게 버튼 클릭으로 효과를 트리거하는 방법은 다음과 같습니다.


1. `replay_kit_launcher` 플러그 인을 프로그램에 추가합니다.
2. 프로그램 인터페이스에 버튼을 만들고, 버튼의 응답 함수에 `ReplayKitLauncher.launchReplayKitBroadcast(iosExtensionName);` 함수를 호출하면 화면 공유 기능을 호출할 수 있습니다.
```
// 사용자 정의 버튼 응답 방법
onShareClick() async {
   if (Platform.isAndroid) {
      if (await SystemAlertWindow.requestPermissions) {
        MeetingTool.showOverlayWindow();
      }
    } else {
      //화면 공유 기능은 실제 디바이스에서만 테스트 가능
      ReplayKitLauncher.launchReplayKitBroadcast(iosExtensionName);
    }
}
```

## 공유 화면 시청
- **Android/iOS 공유 화면 시청**
  사용자가 Android/iOS를 통해 화면 공유를 시작하면 메인 스트림을 통해 공유됩니다. 방 안의 다른 사용자들은 TRTCCloudListener의 [onUserVideoAvailable](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html) 이벤트를 통해 이 공지를 수신하게 됩니다.
  공유 화면을 시청하려는 사용자는 [startRemoteView](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startRemoteView.html) 인터페이스를 통해 원격 사용자의 메인 스트림 화면을 렌더링합니다.

## FAQ
 **한 개의 방에서 동시에 몇 개 채널의 화면을 공유할 수 있나요?**
현재 TRTC 멀티미디어 방별로 한 채널의 화면만 공유할 수 있습니다.
