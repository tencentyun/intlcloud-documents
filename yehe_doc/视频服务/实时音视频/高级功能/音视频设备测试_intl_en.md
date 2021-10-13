## Overview

Given that it is difficult for users to detect device problems during a call, we recommend that you test devices such as cameras and mics before a video call.


## Platform Support

| iOS | Android | macOS | Windows  | Web|
|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ×  |    ×    |    &#10003;   |    &#10003;    |&#10003;    |  ×   |

## Testing Camera

You can use the `startCameraDeviceTestInView` API of `TRTCCloud` to test a camera and can use the `setCurrentCameraDevice` API to switch cameras during testing.

<dx-codeblock>
::: macOS Objective-C
// Open the camera testing page, on which you can preview camera images and switch cameras.
- (IBAction)startCameraTest:(id)sender {
    // Start camera testing. `cameraPreview` is `NSView` on macOS or `UIView` on iOS.
    [self.trtcCloud startCameraDeviceTestInView:self.cameraPreview];
}

// Close the camera testing page.
- (void)windowWillClose:(NSNotification *)notification{
    // Stop camera testing.
    [self.trtcCloud stopCameraDeviceTest];
}
:::
::: Windows (C++) C++
// Start camera testing. Pass in the control handle that renders video.
void TRTCMainViewController::startTestCameraDevice(HWND hwnd) 
{
     trtcCloud->startCameraDeviceTest(hwnd);
}

// Stop camera testing.
void TRTCMainViewController::stopTestCameraDevice() 
{
     trtcCloud->stopCameraDeviceTest();
}
:::
::: Windows (C#) c#
// Start camera testing. Pass in the control handle that renders video.
private void startTestCameraDevice(Intptr hwnd) 
{
     mTRTCCloud.startCameraDeviceTest(hwnd);
}

// Stop camera testing.
private void stopTestCameraDevice() 
{
     mTRTCCloud.stopCameraDeviceTest();
}
:::
</dx-codeblock>

## Testing Mic

You can use the `startMicDeviceTest` API of `TRTCCloud` to measure mic volume in real time. The result is returned via a callback.

<dx-codeblock>
::: macOS Objective-C
  // Sample code for mic testing
  -(IBAction)micTest:(id)sender {
    NSButton *btn = (NSButton *)sender;
    if (btn.state == 1) {
		    // Start mic testing.
        __weak __typeof(self) wself = self;
        [self.trtcCloud startMicDeviceTest:500  testEcho:^(NSInteger volume) {
            dispatch_async(dispatch_get_main_queue(), ^{
						    // Refresh the mic volume bar.
                [wself _updateInputVolume:volume];
            });
        }];
        btn.title = @"Stop test";
    }
    else{
		    // Stop mic testing.
        [self.trtcCloud stopMicDeviceTest];
        [self _updateInputVolume:0];
        btn.title = @"Start test";
    }
}
:::
::: Windows (C++) C++
// Sample code for mic testing
void TRTCMainViewController::startTestMicDevice() 
{
	// Set the interval for triggering the volume callback and listen for the `onTestMicVolume` callback. In the sample, the interval is set to 500 ms.
	uint32_t interval = 500; 
	// Start mic testing.
	trtcCloud->startMicDeviceTest(interval);
}

// Stop mic testing.
void TRTCMainViewController::stopTestMicDevice() 
{
     trtcCloud->stopMicDeviceTest();
}
:::
::: Windows (C#) c#
// Sample code for mic testing
private void startTestMicDevice() 
{
	// Set the interval for triggering the volume callback and listen for the `onTestMicVolume` callback. In the sample, the interval is set to 500 ms.
	uint interval = 500; 
	// Start mic testing.
	mTRTCCloud.startMicDeviceTest(interval);
}

// Stop mic testing.
private void stopTestMicDevice() 
{
     mTRTCCloud.stopMicDeviceTest();
}
:::
</dx-codeblock>



## Testing Speaker

You can use the `startSpeakerDeviceTest` API of `TRTCCloud` to test whether a speaker works properly by playing a default MP3 file.

<dx-codeblock>
::: macOS Objective-C
// Sample code for speaker testing
// Take an NSButton for example. In `xib`, set the title of the button in the on and off state to "Stop Test" and "Start Test".
- (IBAction)speakerTest:(NSButton *)btn {
    NSString *path = [[NSBundle mainBundle] pathForResource:@"test-32000-mono" ofType:@"mp3"];
    if (btn.state == NSControlStateValueOn) {
        // Click "Start Test".
        __weak __typeof(self) wself = self;
        [self.trtcEngine startSpeakerDeviceTest:path onVolumeChanged:^(NSInteger volume, BOOL playFinished) {
            // The subsequent steps involve the UI and need to be executed in the main queue.
            dispatch_async(dispatch_get_main_queue(), ^{
                // `_updateOutputVolume` means updating the speaker volume indicator on the UI.
                [wself _updateOutputVolume:volume];
                if (playFinished) {
                    // Set the button status to "Start Test" after playback is completed.
                    sender.state = NSControlStateValueOff;
                }
            });
        }];
    } else {
        // Click "Stop Test".
        [self.trtcEngine stopSpeakerDeviceTest];
        [self _updateOutputVolume:0];
    }
}

// Update the speaker volume indicator.
- (void)_updateOutputVolume:(NSInteger)volume {
    // `speakerVolumeMeter` is `NSLevelIndicator`.
    self.speakerVolumeMeter.doubleValue = volume / 255.0 * 10;
}
:::
::: Windows (C++) C++
// Sample code for speaker testing
void TRTCMainViewController::startTestSpeakerDevice(std::string testAudioFilePath) 
{
	// `testAudioFilePath` is the absolute path of the audio file (in WAV or MP3 format) and must be a UTF-8-encoded string.
	// Listen for the `onTestSpeakerVolume` callback to get the speaker volume.
	trtcCloud->startSpeakerDeviceTest(testAudioFilePath.c_str());
}

// Stop speaker testing.
void TRTCMainViewController::stopTestSpeakerDevice() {
	trtcCloud->stopSpeakerDeviceTest();
}
:::
::: Windows (C#) C#
// Sample code for speaker testing
private void startTestSpeakerDevice(string testAudioFilePath) 
{
	// `testAudioFilePath` is the absolute path of the audio file (in WAV or MP3 format) and must be a UTF-8-encoded string.
	// Listen for the `onTestSpeakerVolume` callback to get the speaker volume.
	mTRTCCloud.startSpeakerDeviceTest(testAudioFilePath);
}

// Stop speaker testing.
private void stopTestSpeakerDevice() {
	mTRTCCloud.stopSpeakerDeviceTest();
}
:::
</dx-codeblock>
