## 콘텐츠 소개

영상 통화 시작 전에 카메라, 마이크 등의 장치를 먼저 테스트 해볼 것을 권장합니다. 그렇지 않으면 사용자가 실제로 통화를 진행하는 동안 장치 문제를 발견하기 어렵습니다.




## 기능이 지원되는 플랫폼

| iOS | Android | Mac OS | Windows | Electron | web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ×  |    ×    |    &#10003;   |    &#10003;    |&#10003;  |  ×   |

## 카메라 테스트

TRTCCloud의 'startCameraDeviceTestInView' 인터페이스를 사용하여 카메라 테스트를 진행합니다. 테스트 과정 중 'setCurrentCameraDevice' 함수를 호출하여 카메라를 전환할 수 있습니다.

<dx-codeblock>
::: Mac플랫폼 Objective-C
// 카메라 테스트 인터페이스 표시(카메라 미리보기, 카메라 전환 지원)
- (IBAction)startCameraTest:(id)sender {
    // 카메라 테스트 시작, cameraPreview는 macOS의 NSView 또는 iOS 플랫폼의 UIView
    [self.trtcCloud startCameraDeviceTestInView:self.cameraPreview];
}

//카메라 테스트 인터페이스 닫기
- (void)windowWillClose:(NSNotification *)notification{
    // 카메라 테스트 종료
    [self.trtcCloud stopCameraDeviceTest];
}
:::
::: Windows플랫폼(C++) C++
// 카메라 테스트 실행. 렌더링할 비디오의 컨트롤 핸들을 전달합니다.
void TRTCMainViewController::startTestCameraDevice(HWND hwnd) 
{
     trtcCloud->startCameraDeviceTest(hwnd);
}

//  카메라 테스트 종료
void TRTCMainViewController::stopTestCameraDevice() 
{
     trtcCloud->stopCameraDeviceTest();
}
:::
::: Windows플랫폼(C#) c#
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
:::
</dx-codeblock>

## 마이크 테스트

TRTCCloud의 `startMicDeviceTest` 함수를 이용하여 마이크 볼륨을 테스트할 수 있으며, 콜백 함수로 실시간 마이크 볼륨 값을 반환할 수 있습니다.

<dx-codeblock>
::: Mac플랫폼 Objective-C
  // 마이크 테스트 예시 코드
  -(IBAction)micTest:(id)sender {
    NSButton *btn = (NSButton *)sender;
    if (btn.state == 1) {
		    //마이크 테스트 시작
        __weak __typeof(self) wself = self;
        [self.trtcCloud startMicDeviceTest:500  testEcho:^(NSInteger volume) {
            dispatch_async(dispatch_get_main_queue(), ^{
						    // 마이크 볼륨 프로그레스 바 새로고침
                [wself _updateInputVolume:volume];
            });
        }];
        btn.title = @'테스트 종료';
    }
    else{
		    //마이크 테스트 종료
        [self.trtcCloud stopMicDeviceTest];
        [self _updateInputVolume:0];
        btn.title = @'테스트 시작';
    }
}
:::
::: Windows플랫폼(C++) C++
// 마이크 테스트 예시 코드
void TRTCMainViewController::startTestMicDevice() 
{
	// 볼륨 콜백 빈도 설정. 본 예시 코드에서는 500ms 마다 한 번씩 콜백하며, onTestMicVolume 콜백 인터페이스를 수신합니다.
	uint32_t interval = 500; 
	// 마이크 테스트 시작
	trtcCloud->startMicDeviceTest(interval);
}

// 마이크 테스트 종료
void TRTCMainViewController::stopTestMicDevice() 
{
     trtcCloud->stopMicDeviceTest();
}
:::
::: Windows플랫폼(C#) c#
// 마이크 테스트 예시 코드
private void startTestMicDevice() 
{
	// 볼륨 콜백 빈도 설정. 본 예시 코드에서는 500ms 마다 한 번씩 콜백하며, onTestMicVolume 콜백 인터페이스를 수신합니다.
	uint interval = 500; 
	// 마이크 테스트 시작
	mTRTCCloud.startMicDeviceTest(interval);
}

// 마이크 테스트 종료
private void stopTestMicDevice() 
{
     mTRTCCloud.stopMicDeviceTest();
}
:::
</dx-codeblock>



## 스피커 테스트

TRTCCloud의 `startSpeakerDeviceTest` 함수를 사용해 일부 기본 설정된 mp3 오디오를 재생하여 스피커가 정상 작동되는지 테스트합니다.

<dx-codeblock>
::: Mac플랫폼 Objective-C
// 스피커 테스트 예시 코드
// NSButton의 클릭 이벤트를 예시로, xib에서 Button이 On 및 Off될 때 제목이 '테스트 종료', '테스트 시작'이 되도록 설정합니다.
- (IBAction)speakerTest:(NSButton *)btn {
    NSString *path = [[NSBundle mainBundle] pathForResource:@'test-32000-mono' ofType:@'mp3'];
    if (btn.state == NSControlStateValueOn) {
        // '테스트 시작' 클릭
        __weak __typeof(self) wself = self;
        [self.trtcEngine startSpeakerDeviceTest:path onVolumeChanged:^(NSInteger volume, BOOL playFinished) {
            // 다음의 UI 관련 작업은 main queue로 전환해 실행해야 합니다.
            dispatch_async(dispatch_get_main_queue(), ^{
                // 여기에서 _updateOutputVolume은 업데이트 페이지의 스피커 볼륨 지표입니다.
                [wself _updateOutputVolume:volume];
                if (playFinished) {
                    // 재생 완료 시 버튼 상태 '테스트 시작' 상태로 설정
                    sender.state = NSControlStateValueOff;
                }
            });
        }];
    } else {
        // '테스트 종료' 클릭
        [self.trtcEngine stopSpeakerDeviceTest];
        [self _updateOutputVolume:0];
    }
}

// 스피커 볼륨 측정기 업데이트
- (void)_updateOutputVolume:(NSInteger)volume {
    // speakerVolumeMeter는 NSLevelIndicator임
    self.speakerVolumeMeter.doubleValue = volume / 255.0 * 10;
}
:::
::: Windows플랫폼(C++) C++
// 스피커 테스트 예시 코드
void TRTCMainViewController::startTestSpeakerDevice(std::string testAudioFilePath) 
{
	// testAudioFilePath: 오디오 파일의 절대 경로. 경로 문자열은 UTF-8 인코딩 포맷을 사용하였으며 wav, mp3 파일 포맷을 지원합니다.
	// onTestSpeakerVolume에서 인터페이스를 콜백하여 스피커 테스트 볼륨 값을 모니터링합니다.
	trtcCloud->startSpeakerDeviceTest(testAudioFilePath.c_str());
}

// 스피커 테스트 종료
void TRTCMainViewController::stopTestSpeakerDevice() {
	trtcCloud->stopSpeakerDeviceTest();
}
:::
::: Windows플랫폼(C#) C#
// 스피커 테스트 예시 코드
private void startTestSpeakerDevice(string testAudioFilePath) 
{
	// testAudioFilePath: 오디오 파일의 절대 경로. UTF-8 형식의 문자열이어야 합니다. 지원되는 파일 형식: wav, mp3 
	// onTestSpeakerVolume 콜백 인터페이스에서 스피커 테스트 볼륨 값 수신.
	mTRTCCloud.startSpeakerDeviceTest(testAudioFilePath);
}

// 스피커 테스트 종료
private void stopTestSpeakerDevice() {
	mTRTCCloud.stopSpeakerDeviceTest();
}
:::
</dx-codeblock>
