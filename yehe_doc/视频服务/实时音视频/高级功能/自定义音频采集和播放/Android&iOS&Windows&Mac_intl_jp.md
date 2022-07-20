このドキュメントでは、主にTRTC SDKを使用して、カスタムオーディオのキャプチャと取得を実装する方法を紹介します。オーディオキャプチャとオーディオ取得の2つの部分に分かれています。

## オーディオキャプチャのカスタマイズ

TRTC SDKのカスタムオーディオキャプチャ機能の有効化は、機能の有効化とSDKへのオーディオフレームの送信の2つの手順に分かれています。具体的なAPIの使用手順は次のとおりです。また、対応するプラットホームのAPI-Exampleも提供します：

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/main/TRTC-API-Example-OC/Advanced/LocalVideoShare/LocalVideoShareViewController.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 

### カスタムオーディオキャプチャ機能の有効化

まず、TRTCCloudの`enableCustomAudioCapture`インターフェースを呼び出して、TRTC SDKのカスタムオーディオキャプチャ機能を有効にしてください。サンプルコードは次のとおりです：

<dx-codeblock>
::: Android  Java
TRTCCloud mTRTCCloud = TRTCCloud.shareInstance();
mTRTCCloud.enableCustomAudioCapture(true);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
[self.trtcCloud enableCustomAudioCapture:YES];
:::
::: Windows  C++
liteav::ITRTCCloud* trtc_cloud = liteav::ITRTCCloud::getTRTCShareInstance();
trtc_cloud->enableCustomAudioCapture(true);
:::
</dx-codeblock>


### カスタムオーディオフレームの送信

次に、TRTCCloudの`sendCustomVideoData`インターフェースを使用して、TRTC SDKに自身の音声データを送信できます。サンプルコードは次のとおりです：

<dx-codeblock>
::: Android  Java
TRTCCloudDef.TRTCAudioFrame trtcAudioFrame = new TRTCCloudDef.TRTCAudioFrame();
trtcAudioFrame.data = data;
trtcAudioFrame.sampleRate = sampleRate;
trtcAudioFrame.channel = channel;
trtcAudioFrame.timestamp = timestamp;
mTRTCCloud.sendCustomAudioData(trtcAudioFrame);
:::
::: iOS&Mac  ObjC
TRTCAudioFrame *audioFrame = [[TRTCAudioFrame alloc] init];
audioFrame.channels = audioChannels;
audioFrame.sampleRate = audioSampleRate;
audioFrame.data = pcmData;
    
[self.trtcCloud sendCustomAudioData:audioFrame];
:::
::: Windows  C++
liteav::TRTCAudioFrame frame;
frame.audioFormat = liteav::TRTCAudioFrameFormatPCM;
frame.length = buffer_size;
frame.data = array.data();
frame.sampleRate = 48000;
frame.channel = 1;
getTRTCShareInstance()->sendCustomAudioData(&frame);
:::
</dx-codeblock>

>! endCustomAudioData`を使用すると、エコーキャンセル(AEC)の機能が無効になる場合があります。




## オーディオ生データの取得

音声モジュールは非常に複雑なモジュールで、SDKは音声デバイスのキャプチャおよび再生のロジックを厳密に制御する必要があります。一部のシーンにおいて、リモートユーザーのオーディオデータまたはローカルマイクによってキャプチャされたオーディオデータを取得する必要がある場合は、TRTCCloudに対応する異なるプラットフォームのインターフェースを介して取得することができ、対応するプラットフォームのAPI-Exampleも提供します：

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)：
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/main/TRTC-API-Example-OC/Advanced/LocalVideoShare/LocalVideoShareViewController.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows) 


### オーディオコールバック関数の設定
<dx-codeblock>
::: Android  Java
mTRTCCloud.setAudioFrameListener(new TRTCCloudListener.TRTCAudioFrameListener() {
        @Override
        public void onCapturedRawAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {

        }
    
        @Override
        public void onLocalProcessedAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {
    
        }
    
        @Override
        public void onRemoteUserAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame, String s) {
    
        }
    
        @Override
        public void onMixedPlayAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {
    
        }
    
        @Override
        public void onMixedAllAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {
            // 詳細については、TRTC-API-Exampleのカスタムレンダリングのツールクラスをご参照ください：com.tencent.trtc.mediashare.helper.CustomFrameRender  
        }
    }); 
:::
::: iOS&Mac ObjC
 [self.trtcCloud setAudioFrameDelegate:self];
 // MARK: - TRTCAudioFrameDelegate
 - (void)onCapturedRawAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onCapturedRawAudioFrame");
}

- (void)onLocalProcessedAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onLocalProcessedAudioFrame");
}

- (void)onRemoteUserAudioFrame:(TRTCAudioFrame *)frame userId:(NSString *)userId {
        NSLog(@"onRemoteUserAudioFrame");
}

- (void)onMixedPlayAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onMixedPlayAudioFrame");
}

- (void)onMixedAllAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onMixedAllAudioFrame");
}
:::
::: Windows C++
// オーディオデータのカスタムコールバックの設定
liteav::ITRTCCloud* trtc_cloud = liteav::ITRTCCloud::getTRTCShareInstance();
trtc_cloud->setAudioFrameCallback(callback)

// オーディオデータのカスタムコールバック

virtual void onCapturedRawAudioFrame(TRTCAudioFrame* frame) {
}

virtual void onLocalProcessedAudioFrame(TRTCAudioFrame* frame) {
}

virtual void onPlayAudioFrame(TRTCAudioFrame* frame, const char* userId) {
}

virtual void onMixedPlayAudioFrame(TRTCAudioFrame* frame) {
}
:::
</dx-codeblock>

>!
>- 音声が途切れたりエコーキャンセル(AEC)が無効になったりするトラブルが発生するおそれがありますので、上述のコールバック関数では時間のかかる操作を行わず、直接コピーして別のスレッドで処理することを推奨します。
>- 各種の不確実な影響が生じるおそれがありますので、上述のコールバック関数でコールバックされたデータはいずれも読み取りとコピーのみが許可され、修正することはできません。
