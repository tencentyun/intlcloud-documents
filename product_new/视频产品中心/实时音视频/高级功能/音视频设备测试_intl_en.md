## Introduction

Before a video call is made, it is recommended to test the devices such as camera and mic; otherwise, it is difficult to find device problems when the user actually makes a call.

<img style="border:0; max-width:100%; height:auto; box-sizing:content-box; box-shadow: 0px 0px 0px #ccc; margin: 0px 0px 0px 0px;" src="https://main.qcloudimg.com/raw/fced7778482de4edfbe94bfcf8ec5f20.jpg" />


## Platforms That Support This Feature

| iOS | Android | macOS | Windows | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ✖  |    ✖    |    ✔   |    ✔    |    ✖    |   ✖    |

## Testing Camera

You can use the `startCameraDeviceTestInView` API of TRTCCloud to perform camera test. During the test, you can switch cameras by calling the `setCurrentCameraDevice` function.

- **macOS**

``` Objective-C
// Display the camera test page (where camera preview and switch are supported)
- (IBAction)startCameraTest:(id)sender {
    // Start camera test. `cameraPreview` is `NSView` on macOS or `UIView` on iOS
    [self.trtcCloud startCameraDeviceTestInView:self.cameraPreview];
}

// Close the camera test page
- (void)windowWillClose:(NSNotification *)notification{
    // Stop camera test
    [self.trtcCloud stopCameraDeviceTest];
}
```

- **Windows (C++ edition)**

``` C++
// Start camera test. Pass in the control handle of the video to be rendered
void TRTCMainViewController::startTestCameraDevice(HWND hwnd) 
{
     trtcCloud->startCameraDeviceTest(hwnd);
}

// Stop camera test
void TRTCMainViewController::stopTestCameraDevice() 
{
     trtcCloud->stopCameraDeviceTest();
}
```

* **Windows (C# edition)**

```c#
// Start camera test. Pass in the control handle of the video to be rendered
private void startTestCameraDevice(Intptr hwnd) 
{
     mTRTCCloud.startCameraDeviceTest(hwnd);
}

// Stop camera test
private void stopTestCameraDevice() 
{
     mTRTCCloud.stopCameraDeviceTest();
}
```

## Testing Mic

Use the `startMicDeviceTest` function of TRTCCloud to test the mic volume, and the callback function will return the real-time mic volume level.

- **macOS**

``` Objective-C
  // Sample code for mic test
  -(IBAction)micTest:(id)sender {
    NSButton *btn = (NSButton *)sender;
    if (btn.state == 1) {
		    // Start mic test
        __weak __typeof(self) wself = self;
        [self.trtcCloud startMicDeviceTest:500  testEcho:^(NSInteger volume) {
            dispatch_async(dispatch_get_main_queue(), ^{
						    // Refresh the progress bar of mic volume
                [wself _updateInputVolume:volume];
            });
        }];
        btn.title = @"Stop test";
    }
    else{
		    // Stop mic test
        [self.trtcCloud stopMicDeviceTest];
        [self _updateInputVolume:0];
        btn.title = @"Start test";
    }
}
```

- **Windows (C++ edition)**

``` C++
// Sample code for mic test
void TRTCMainViewController::startTestMicDevice() 
{
	// Set the volume callback frequency, which is once every 500 ms here. Listen on the `onTestMicVolume` callback API
	uint32_t interval = 500; 
	// Start mic test
	trtcCloud->startMicDeviceTest(interval);
}

// Stop mic test
void TRTCMainViewController::stopTestMicDevice() 
{
     trtcCloud->stopMicDeviceTest();
}
```

* **Windows (C# edition)**

```c#
// Sample code for mic test
private void startTestMicDevice() 
{
	// Set the volume callback frequency, which is once every 500 ms here. Listen on the `onTestMicVolume` callback API
	uint interval = 500; 
	// Start mic test
	mTRTCCloud.startMicDeviceTest(interval);
}

// Stop mic test
private void stopTestMicDevice() 
{
     mTRTCCloud.stopMicDeviceTest();
}
```

## Testing Speaker

Use the `startSpeakerDeviceTest` function of TRTCCloud to test whether the speaker is working by playing a default mp3 audio clip.

- **macOS**

``` Objective-C
// Sample code for speaker test
// Taking the click event of `NSButton` as an example, set the caption of the button in `On` and `Off` status to "Stop Test" and "Start Test" respectively in `xib`
- (IBAction)speakerTest:(NSButton *)btn {
    NSString *path = [[NSBundle mainBundle] pathForResource:@"test-32000-mono" ofType:@"mp3"];
    if (btn.state == NSControlStateValueOn) {
        // Click "Start Test"
        __weak __typeof(self) wself = self;
        [self.trtcEngine startSpeakerDeviceTest:path onVolumeChanged:^(NSInteger volume, BOOL playFinished) {
            // The following involves UI operations, which need to be executed after switching to the main queue
            dispatch_async(dispatch_get_main_queue(), ^{
                // Here, `_updateOutputVolume` is the speaker volume indicator in the update page
                [wself _updateOutputVolume:volume];
                if (playFinished) {
                    // Set the button status to "Start Test" after playback is completed
                    sender.state = NSControlStateValueOff;
                }
            });
        }];
    } else {
        // Click "Stop Test"
        [self.trtcEngine stopSpeakerDeviceTest];
        [self _updateOutputVolume:0];
    }
}

// Update speaker volume indicator
- (void)_updateOutputVolume:(NSInteger)volume {
    // `speakerVolumeMeter` is `NSLevelIndicator`
    self.speakerVolumeMeter.doubleValue = volume / 255.0 * 10;
}

```

- **Windows (C++ edition)**

``` C++
// Sample code for speaker test
void TRTCMainViewController::startTestSpeakerDevice(std::string testAudioFilePath) 
{
	// `testAudioFilePath` is the absolute path to the audio file, which must be a string in UTF-8 format. Supported file formats: wav, mp3
	// Listen on the speaker test volume level from the `onTestSpeakerVolume` callback API
	trtcCloud->startSpeakerDeviceTest(testAudioFilePath.c_str());
}

// Stop speaker test
void TRTCMainViewController::stopTestSpeakerDevice() {
	trtcCloud->stopSpeakerDeviceTest();
}
```

* **Windows (C# edition)**

```c#
// Sample code for speaker test
private void startTestSpeakerDevice(string testAudioFilePath) 
{
	// `testAudioFilePath` is the absolute path to the audio file, which must be a string in UTF-8 format. Supported file formats: wav, mp3
	// Listen on the speaker test volume level from the `onTestSpeakerVolume` callback API
	mTRTCCloud.startSpeakerDeviceTest(testAudioFilePath);
}

// Stop speaker test
private void stopTestSpeakerDevice() {
	mTRTCCloud.stopSpeakerDeviceTest();
}
```
