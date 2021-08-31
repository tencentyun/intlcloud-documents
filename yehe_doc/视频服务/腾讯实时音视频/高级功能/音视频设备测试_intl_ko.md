## 콘텐츠 소개

영상 통화 전, 먼저 카메라와 마이크 등 디바이스를 테스트하시기 바랍니다. 테스트하지 않는 경우 사용자가 실제 통화 시 디바이스 문제를 발견하기 매우 어렵습니다.


## 해당 기능을 지원하는 플랫폼

| iOS | Android | Mac OS | Windows | Electron | web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ×  |    ×    |    &#10003;   |    &#10003;    |&#10003;  |  ×   |

## 카메라 테스트

TRTCCloud의 `startCameraDeviceTestInView` 인터페이스를 이용하여 카메라를 테스트할 수 있으며, 테스트 중 `setCurrentCameraDevice` 함수를 호출해 카메라를 전환할 수 있습니다.

- **Mac 플랫폼**

``` Objective-C
// 카메라 테스트 인터페이스 표시(카메라 미리보기, 카메라 전환 지원)
- (IBAction)startCameraTest:(id)sender {
    // 카메라 테스트 시작. cameraPreview: macOS의 NSView 또는 iOS플랫폼의 UIView
    [self.trtcCloud startCameraDeviceTestInView:self.cameraPreview];
}

//카메라 테스트 인터페이스 종료
- (void)windowWillClose:(NSNotification *)notification{
    // 카메라 테스트 종료
    [self.trtcCloud stopCameraDeviceTest];
}
```

- **Windows 플랫폼(C++ 버전)**

``` C++
// 카메라 테스트 실행. 렌더링할 비디오의 컨트롤러 전달
void TRTCMainViewController::startTestCameraDevice(HWND hwnd) 
{
     trtcCloud->startCameraDeviceTest(hwnd);
}

// 카메라 테스트 종료
void TRTCMainViewController::stopTestCameraDevice() 
{
     trtcCloud->stopCameraDeviceTest();
}
```

* **Windows 플랫폼(C# 버전)**

```c#
// 카메라 테스트 실행. 렌더링할 비디오의 컨트롤러 전달
private void startTestCameraDevice(Intptr hwnd) 
{
     mTRTCCloud.startCameraDeviceTest(hwnd);
}

// 카메라 테스트 종료
private void stopTestCameraDevice() 
{
     mTRTCCloud.stopCameraDeviceTest();
}
```

## 마이크 테스트

TRTCCloud의 `startMicDeviceTest` 함수를 이용하여 마이크 음량을 테스트할 수 있으며, 콜백 함수로 실시간 마이크 음량 값을 반환할 수 있습니다.

- **Mac 플랫폼**

``` Objective-C
  // 마이크 테스트 예시 코드
  -(IBAction)micTest:(id)sender {
    NSButton *btn = (NSButton *)sender;
    if (btn.state == 1) {
		    //마이크 테스트 시작
        __weak __typeof(self) wself = self;
        [self.trtcCloud startMicDeviceTest:500  testEcho:^(NSInteger volume) {
            dispatch_async(dispatch_get_main_queue(), ^{
						    // 마이크 음량 진행 바 새로고침
                [wself _updateInputVolume:volume];
            });
        }];
        btn.title = @"테스트 종료";
    }
    else{
		    //마이크 테스트 종료
        [self.trtcCloud stopMicDeviceTest];
        [self _updateInputVolume:0];
        btn.title = @"테스트 시작";
    }
}
```

- **Windows 플랫폼(C++ 버전)**

``` C++
// 마이크 테스트 예시 코드
void TRTCMainViewController::startTestMicDevice() 
{
	// 음량 콜백 빈도수 설정입니다. 본 예시 코드에서는 500ms에 한 번 콜백하며, onTestMicVolume에서 인터페이스를 콜백합니다.
	uint32_t interval = 500; 
	// 마이크 테스트 시작
	trtcCloud->startMicDeviceTest(interval);
}

// 마이크 테스트 종료
void TRTCMainViewController::stopTestMicDevice() 
{
     trtcCloud->stopMicDeviceTest();
}
```

* **Windows 플랫폼(C# 버전)**

```c#
// 마이크 테스트 예시 코드
private void startTestMicDevice() 
{
	// 음량 콜백 빈도수 설정입니다. 본 예시 코드에서는 500ms에 한 번 콜백하며, onTestMicVolume에서 인터페이스를 콜백합니다.
	uint interval = 500; 
	// 마이크 테스트 시작
	mTRTCCloud.startMicDeviceTest(interval);
}

// 마이크 테스트 종료
private void stopTestMicDevice() 
{
     mTRTCCloud.stopMicDeviceTest();
}
```

## 스피커 테스트

TRTCCloud의 `startSpeakerDeviceTest` 함수를 사용해 일부 기본 설정된 mp3 오디오를 재생하여 스피커가 정상 작동되는지 테스트합니다.

- **Mac 플랫폼**

``` Objective-C
// 스피커 테스트 예시 코드
// NSButton의 클릭 이벤트를 예시로, xib에서 Button이 On 및 Off될 때 제목이 "테스트 종료", "테스트 시작"이 되도록 설정합니다.
- (IBAction)speakerTest:(NSButton *)btn {
    NSString *path = [[NSBundle mainBundle] pathForResource:@"test-32000-mono" ofType:@"mp3"];
    if (btn.state == NSControlStateValueOn) {
        // "테스트 시작" 클릭
        __weak __typeof(self) wself = self;
        [self.trtcEngine startSpeakerDeviceTest:path onVolumeChanged:^(NSInteger volume, BOOL playFinished) {
            // 다음의 UI 관련 작업은 main queue로 전환해 실행해야 함
            dispatch_async(dispatch_get_main_queue(), ^{
                // 여기에서 _updateOutputVolume는 인터페이스 업데이트 중의 스피커 음량 측정기
                [wself _updateOutputVolume:volume];
                if (playFinished) {
                    // 재생 완료 시 버튼 상태 "테스트 시작" 상태로 설정
                    sender.state = NSControlStateValueOff;
                }
            });
        }];
    } else {
        // "테스트 종료" 클릭
        [self.trtcEngine stopSpeakerDeviceTest];
        [self _updateOutputVolume:0];
    }
}

// 스피커 음량 측정기 업데이트
- (void)_updateOutputVolume:(NSInteger)volume {
    // speakerVolumeMeter는 NSLevelIndicator
    self.speakerVolumeMeter.doubleValue = volume / 255.0 * 10;
}

```

- **Windows 플랫폼(C++ 버전)**

``` C++
// 스피커 테스트 예시 코드
void TRTCMainViewController::startTestSpeakerDevice(std::string testAudioFilePath) 
{
	// testAudioFilePath: 오디오 파일의 절대 경로. 경로 문자열은 UTF-8 인코딩 포맷을 사용하였으며 wav, mp3 파일 포맷을 지원합니다.
	// onTestSpeakerVolume에서 인터페이스를 콜백하여 스피커 테스트 음량 값을 수신합니다.
	trtcCloud->startSpeakerDeviceTest(testAudioFilePath.c_str());
}

// 스피커 테스트 종료
void TRTCMainViewController::stopTestSpeakerDevice() {
	trtcCloud->stopSpeakerDeviceTest();
}
```

* **Windows 플랫폼(C# 버전)**

```c#
// 스피커 테스트 예시 코드
private void startTestSpeakerDevice(string testAudioFilePath) 
{
	// testAudioFilePath: 오디오 파일의 절대 경로. 경로 문자열은 UTF-8 인코딩 포맷을 사용하였으며 wav, mp3 파일 포맷을 지원합니다.
	// onTestSpeakerVolume에서 인터페이스를 콜백하여 스피커 테스트 음량 값을 수신합니다.
	mTRTCCloud.startSpeakerDeviceTest(testAudioFilePath);
}

// 스피커 테스트 종료
private void stopTestSpeakerDevice() {
	mTRTCCloud.stopSpeakerDeviceTest();
}
```
