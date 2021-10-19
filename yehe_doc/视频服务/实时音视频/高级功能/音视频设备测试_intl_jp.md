## 内容紹介

ビデオ通話の前に、カメラおよびマイクなどのデバイスのテストを先に行うことを推奨します。テストしないと、ユーザーが実際にビデオ通話を行うときにデバイスの問題を見つけることが難しくなります。


## この機能のプラットフォームのサポート

| iOS | Android | Mac OS | Windows  |Electron  | Web端末|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ×  |    ×    |    &#10003;   |    &#10003;    |&#10003;    |  &#10003;（[Web 端](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html)）   |


## カメラテスト

TRTCCloudの`startCameraDeviceTestInView`インターフェースを使用すればカメラテストが行えます。テストのプロセスでは`setCurrentCameraDevice`関数をコールすることでカメラを切り替えられます。

<dx-codeblock>
::: MacプラットフォームObjective-C
// カメラテストインターフェースの表示（カメラのプレビュー、カメラの切り替えのサポート）
- (IBAction)startCameraTest:(id)sender {
    // カメラテストの開始。 cameraPreviewをmacOSのNSViewまたはiOSプラットフォームのUIView
    [self.trtcCloud startCameraDeviceTestInView:self.cameraPreview];
}

//カメラテストインターフェースの停止
- (void)windowWillClose:(NSNotification *)notification{
    // カメラテストの終了
    [self.trtcCloud stopCameraDeviceTest];
}
:::
::: Windowsプラットフォーム（C++） C++
// カメラテストの開始。レンダリングする必要のあるビデオの制御ハンドルを渡します。
void TRTCMainViewController::startTestCameraDevice(HWND hwnd) 
{
     trtcCloud->startCameraDeviceTest(hwnd);
}

// カメラテストの停止
void TRTCMainViewController::stopTestCameraDevice() 
{
     trtcCloud->stopCameraDeviceTest();
}
:::
::: Windowsプラットフォーム（C#） c#
// カメラテストの開始。レンダリングする必要のあるビデオの制御ハンドルを渡します。
private void startTestCameraDevice(Intptr hwnd) 
{
     mTRTCCloud.startCameraDeviceTest(hwnd);
}

// カメラテストの停止
private void stopTestCameraDevice() 
{
     mTRTCCloud.stopCameraDeviceTest();
}
:::
</dx-codeblock>

## マイクテスト

TRTCCloudの`startMicDeviceTest`関数を使用すると、マイクの音量を測定でき、コールバック関数はリアルタイムでマイク音量値を返します。

<dx-codeblock>
::: MacプラットフォームObjective-C
  // マイクテストサンプルコード
  -(IBAction)micTest:(id)sender {
    NSButton *btn = (NSButton *)sender;
    if (btn.state == 1) {
		    //マイクテストの開始
        __weak __typeof(self) wself = self;
        [self.trtcCloud startMicDeviceTest:500  testEcho:^(NSInteger volume) {
            dispatch_async(dispatch_get_main_queue(), ^{
						    // マイク音量のプログレスバーの更新
                [wself _updateInputVolume:volume];
            });
        }];
        btn.title = @"テストの停止";
    }
    else{
		    //マイクテストの終了
        [self.trtcCloud stopMicDeviceTest];
        [self _updateInputVolume:0];
        btn.title = @"テスト開始";
    }
}
:::
::: Windowsプラットフォーム（C++） C++
// マイクテストサンプルコード
void TRTCMainViewController::startTestMicDevice() 
{
	// 音量コールバック率の設定。ここでは500msに1回コールバック。 onTestMicVolumeコールバックインターフェースで監視。
	uint32_t interval = 500; 
	// マイクテストの開始
	trtcCloud->startMicDeviceTest(interval);
}

// マイクテストの終了
void TRTCMainViewController::stopTestMicDevice() 
{
     trtcCloud->stopMicDeviceTest();
}
:::
::: Windowsプラットフォーム（C#） c#
// マイクテストサンプルコード
private void startTestMicDevice() 
{
	// 音量コールバック率の設定。ここでは500msに1回コールバック。 onTestMicVolumeコールバックインターフェースで監視。
	uint interval = 500; 
	// マイクテストの開始
	mTRTCCloud.startMicDeviceTest(interval);
}

// マイクテストの終了
private void stopTestMicDevice() 
{
     mTRTCCloud.stopMicDeviceTest();
}
:::
</dx-codeblock>



## スピーカーテスト

TRTCCloudの`startSpeakerDeviceTest`関数を使用し、デフォルトのmp3オーディオデータを再生することで、スピーカーが正常に動作しているかテストします。

<dx-codeblock>
::: MacプラットフォームObjective-C
// スピーカーテストサンプルコード
// NSButtonのクリックイベントを例にすると、xibの中ではButtonをOnおよびOffの下のタイトルでそれぞれ「テスト終了」および「テスト開始」に設定しています。
- (IBAction)speakerTest:(NSButton *)btn {
    NSString *path = [[NSBundle mainBundle] pathForResource:@"test-32000-mono" ofType:@"mp3"];
    if (btn.state == NSControlStateValueOn) {
        // 「テスト開始」のクリック
        __weak __typeof(self) wself = self;
        [self.trtcEngine startSpeakerDeviceTest:path onVolumeChanged:^(NSInteger volume, BOOL playFinished) {
            // 以下のUI操作に関しては、main queueに切り替えてから実行する必要があります
            dispatch_async(dispatch_get_main_queue(), ^{
                // ここでは、_updateOutputVolumeは更新ページのスピーカー音量インジケータです
                [wself _updateOutputVolume:volume];
                if (playFinished) {
                    // 再生完了時にはボタンのステータスを「テスト開始」にします
                    sender.state = NSControlStateValueOff;
                }
            });
        }];
    } else {
        // 「テスト終了」をクリック
        [self.trtcEngine stopSpeakerDeviceTest];
        [self _updateOutputVolume:0];
    }
}

// スピーカー音量インジケータの更新
- (void)_updateOutputVolume:(NSInteger)volume {
    // speakerVolumeMeterはNSLevelIndicatorです
    self.speakerVolumeMeter.doubleValue = volume / 255.0 * 10;
}
:::
::: Windowsプラットフォーム（C++） C++
// スピーカーテストサンプルコード
void TRTCMainViewController::startTestSpeakerDevice(std::string testAudioFilePath) 
{
	// testAudioFilePathオーディオファイルの絶対パス。パス文字列にはUTF-8エンコードフォーマットを使用し、ファイルフォーマットはwav、mp3をサポート。
	// onTestSpeakerVolumeコールバックインターフェースからスピーカーテスト音量値をモニタします。
	trtcCloud->startSpeakerDeviceTest(testAudioFilePath.c_str());
}

// スピーカーテストを終了
void TRTCMainViewController::stopTestSpeakerDevice() {
	trtcCloud->stopSpeakerDeviceTest();
}
:::
::: Windowsプラットフォーム（C#） C#
// スピーカーテストサンプルコード
private void startTestSpeakerDevice(string testAudioFilePath) 
{
	// testAudioFilePathオーディオファイルの絶対パス。パス文字列にはUTF-8エンコードフォーマットを使用し、ファイルフォーマットはwav、mp3をサポート。
	// onTestSpeakerVolumeコールバックインターフェースからスピーカーテスト音量値をモニタします。
	mTRTCCloud.startSpeakerDeviceTest(testAudioFilePath);
}

// スピーカーテストを終了
private void stopTestSpeakerDevice() {
	mTRTCCloud.stopSpeakerDeviceTest();
}
:::
</dx-codeblock>
