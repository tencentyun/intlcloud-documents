## 内容紹介
- **ビデオキャプチャのカスタマイズ**
美顔や特殊処理モジュールを自社開発（またはサードパーティから購入）する場合は、カメラで撮影した画面を自身でキャプチャし処理する必要があります。TRTCCloud の `enableCustomVideoCapture` インターフェースを介してTRTC SDK 自体のカメラキャプチャと画像処理ロジックをオフにします。その後、 `sendCustomVideoData` インターフェースを使用して TRTC SDKに自身のビデオデータを入力することができます。

- **ビデオレンダリングのカスタマイズ**
TRTC SDKはOpenGLを使用してビデオ画面のレンダリングを行います。ゲーム開発に使用する場合、または自身のインターフェースエンジンにTRTC SDKを埋め込む場合は、自身でビデオ画面をレンダリングする必要があります。

- **オーディオキャプチャのカスタマイズ**
特殊なハードウェアデバイスでTRTC SDKを使用し、外部の音声キャプチャデバイスに接続して自身で音声データをキャプチャする必要がある場合は、TRTCCloud の `enableCustomAudioCapture` インターフェースを介してTRTC SDK デフォルトのサウンドキャプチャプロセスをオフにする必要があります。その後、 `sendCustomAudioData` インターフェースを使用してTRTC SDK に自身の声音データを入力することができます。
>!オーディオキャプチャのカスタマイズを有効にすると、エコーキャンセル（AEC）機能が無効になる場合があります。

- **オーディオ生データの取得**
音声モジュールは非常に複雑で、SDK は音声デバイスのキャプチャおよび再生ロジックを厳密に制御する必要があります。一部シーンにおいて、リモートユーザーのオーディオデータまたはローカルマイクによってキャプチャされたオーディオデータを取得する必要がある場合は、TRTC SDK によって提供される対応するコールバックインターフェースを介して取得することができます。

## サポートするプラットフォーム

|   iOS    | Android  |  Mac OS  | Windows  | WeChat Mini Program| Chrome ブラウザ |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|   &#10003;  |  &#10003;    | &#10003;   |  &#10003;  |   ×  |  ×   |

## ビデオキャプチャのカスタマイズ

TRTCCloud の `enableCustomVideoCapture` インターフェースを介してTRTC SDK 自体のカメラキャプチャと画像処理ロジックをオフにします。その後、 `sendCustomVideoData` インターフェースを使用して TRTC SDKに自身のビデオデータを入力することができます。

 `sendCustomVideoData` インターフェースに `TRTCVideoFrame`と呼ばれるビデオ画像のフレームを表すパラメータがあります。不要なパフォーマンスロスを回避するため、TRTC SDKに入力されるビデオデータには、プラットフォームごとに異なるフォーマット要件があります。具体的な要件は次のとおりです。

### iOS プラットフォーム

TRTC SDK は NV12 と i420という2種の iOS バージョンの YUV データ形式をサポートします。iOS プラットフォームにおいて、より高性能な画像転送方法は CVPixelBufferRefであるため、次のパラメータ形式を推奨します。

| パラメータ名  | パラメータタイプ |  推奨値 | 付注|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 |  iOS プラットフォーム上のカメラによってネイティブにキャプチャされるビデオ形式はNV12です。 |
| bufferType | TRTCVideoBufferType| PixelBuffer | iOS においてネイティブにサポートされるビデオフレーム形式であり、最も高いパフォーマンスを発揮します。|
| pixelBuffer| CVPixelBufferRef | TRTCVideoBufferType が PixelBufferである場合は、入力する必要があります。 | iPhone のCCDカメラによってキャプチャされるデータは NV12 形式の PixelBufferです。|
| data| NSData\* | TRTCVideoBufferType が NSDataである場合は、入力する必要があります。 | パフォーマンスは PixelBufferほど高くありません。 |
| timestamp| uint64_t | 0 | 0を入力できます。SDKはこのようにtimestamp フィールドへの入力をカスタマイズできますが、sendCustomVideoData の呼び出し間隔を**均等**に制御してください。 |
| width    | uint64_t| ビデオ画面の幅 | 入力画面のピクセル幅を正確に入力してください。 |
| height   | uint32_t| ビデオ画面の高さ | 入力画面のピクセル高さを正確に入力してください。 |
| rotation | TRTCVideoRotation| 入力しません | このフィールドはレンダリングのカスタマイズに使用するため、設定する必要はありません。 |

**サンプルコード**： [Demo] フォルダに、ローカルビデオファイルからNV12形式のPixelBufferを読み取り、SDKを介して後続の処理を実行する方法について説明する`TestSendCustomVideoData.m`と呼ばれるファイルがあります。

```objectiveC
//TRTCVideoFrame をアセンブルし、trtcCloud オブジェクトに送信します
TRTCVideoFrame* videoFrame = [TRTCVideoFrame new];
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
        
[trtcCloud sendCustomVideoData:videoFrame];      
```

### Android プラットフォーム

Android プラットフォームについては、2種の方法があります。

**1. buffer **：ドッキングすることは比較的簡単ですが、パフォーマンスが低く、高解像度のシーンには適していません。

buffer では、byte []型の配列をTRTCSDKに直接挿入することが要求され、i420およびNV21のYUVフォーマットをサポートします。

| パラメータ名  | パラメータタイプ |  推奨値 | 付注|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| int | TRTC_VIDEO_PIXEL_FORMAT_I420 または<br> TRTC_VIDEO_PIXEL_FORMAT_NV21  | i420 と NV21 は2種の異なる YUV データフォーマットです。 |
| bufferType | int | TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY | 使用するdata の方式を指定して YUV データを入力します。|
| texture  | TRTCTexture | buffer 方法は入力しません| i420 または NV21の2種のフォーマットを選択する場合、このパラメータは入力しません。|
| data| byte[] | YUV フォーマットのデータ buffer | 内部パッケージはJavaタイプのメモリであり、Javaレイヤーでの使用に適しています。|
| buffer| ByteBuffer | buffer 方法は入力しません | 内部パッケージは C/C++ タイプのメモリであり、 JNI レイヤーでの使用に適しています。 |
| width    | uint64_t| ビデオ画面の幅 | 入力画面のピクセル幅を正確に入力してください。 |
| height   | uint32_t| ビデオ画面の高さ | 入力画面のピクセル高さを正確に入力してください。 |
| timestamp|long | ビデオフレームのキャプチャ時間  | 0を入力できます。SDKはこのようにtimestamp フィールドへの入力をカスタマイズできますが、sendCustomVideoData の呼び出し間隔を**均等**に制御してください。 |
| rotation | int| 入力しません | sendCustomVideoData 時には、このフィールドに入力する必要はありません。 |

**2. texture **：ドッキングには特定のOpenGL基盤が必要ですが、特に画面の解像度が高い場合は、パフォーマンスが向上します。

textureはTRTC SDKにOpenGL テクスチャを渡す必要があります。この方法の正常な動作を保証するには、事前にOpenGL 環境を設定しておく必要があるため、この方法のドッキング難度は極めて高いものとなっています。OpenGLを学んだことがない場合は、当社が提供するサンプルコードを直接使用することを推奨します。サンプルコードは[Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare) の `customCapture` フォルダにあり、次のファイルが含まれています。

| ファイル名 | ソースコードロジック |
|---------|---------|
|TestSendCustomData.java   |     TRTCloudのsendCustomVideoData関数を介してビデオテクスチャをSDKにフィードする方法を示します。|
|TestRenderVideoFrame.java  |      TRTCloudオリジナルのレンダリングロジックをスキップして、自身でOpenGLを使用して画面をレンダリングする方法を示します。|
|VideoFrameReader.java    |    ローカルのビデオファイルから、フレームごとに画面を読み取ります。|
|decoder フォルダ|  デコードモジュール|
|opengl フォルダ   |     OpenGLの基本関数をカプセル化して、より使いやすくします。|
|render フォルダ    |    Eglの基本関数をカプセル化して、より使いやすくします。|

>! 640 x 360 以上の解像度については、texture を使用し、過剰なCPU 利用率を回避することを推奨します。


**サンプルコード**：`TestSendCustomVideoData.java` のコード原理はかなり複雑です。
1. コードはまずGLThreadスレッドを開始します。このスレッドは、関連する「サーフェース（SurfaceTexture）」にコンテンツが描画されるまで、ほとんどの場合、待機状態にあります。
2. コードは次にローカルビデオファイルからフレームごとにビデオ画面を読み取り、前述の手順で作成した「サーフェース」上にフレームごとに画面を描画するためのMovieVideoFrameReaderと呼ばれるモジュールを使用します。
3. フレームが描画されるたびに、手順1で作成した GLThread スレッドがウェイクアップされ、次の `onTextureProcess` コールバックがあり、このコールバック関数で取得した textureがsendCustomVideoData 関数を介して SDKに渡されます。

```java
public int onTextureProcess(int textureId, EGLContext eglContext) {
        if (!mIsSending) return textureId;

        //テクスチャ方式を介してビデオフレームをSDKに入力します
        TRTCCloudDef.TRTCVideoFrame videoFrame = new TRTCCloudDef.TRTCVideoFrame();
        videoFrame.texture = new TRTCCloudDef.TRTCTexture();
        videoFrame.texture.textureId = textureId;
        videoFrame.texture.eglContext14 = eglContext;
        videoFrame.width = mPlayThread.getVideoWidth();
        videoFrame.height = mPlayThread.getVideoHeight();
        videoFrame.pixelFormat = TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D;
        videoFrame.bufferType = TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE;
        mTRTCCloud.sendCustomVideoData(videoFrame);
        return textureId;
    }
```


## ビデオレンダリングのカスタマイズ

TRTC SDKはOpenGLを使用してビデオ画面のレンダリングを行います。ゲーム開発に使用する場合、または自身のインターフェースエンジンにTRTC SDKを埋め込む場合は、自身でビデオ画面をレンダリングする必要があります。

### iOS プラットフォーム（Macを含む）

TRTCCloud の `setLocalVideoRenderDelegate` と `setRemoteVideoRenderDelegate`を介してローカルとリモート画面のレンダリングカスタマイズのコールバックを設定します。関連パラメータは次のとおりです。

| パラメータ名  | パラメータタイプ |  推奨値 | 付注|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 |  - |
| bufferType | TRTCVideoBufferType| TRTCVideoBufferType_PixelBuffer | iOS においてネイティブにサポートされるビデオフレーム形式であり、最も高いパフォーマンスを発揮します。|

**サンプルコード**：pixelFormatが  TRTCVideoPixelFormat_NV12を選択し、bufferTypeが TRTCVideoBufferType_PixelBufferを選択する場合は、NV12形式のPixelBufferをビデオイメージに簡単に変換することができます。Demo フォルダに `TestRenderVideoFrame.m` と呼ばれるファイルがあり、その中に次のサンプルコードを使用したこの方法の使用法が示されています。
```objectiveC
- (void)onRenderVideoFrame:(TRTCVideoFrame *)frame 
                                userId:(NSString *)userId 
						        streamType:(TRTCVideoStreamType)streamType
{
    //userIdがnilの場合はローカル画面、nilでない場合はリモート画面です
    CFRetain(frame.pixelBuffer);
    __weak __typeof(self) weakSelf = self;
    dispatch_async(dispatch_get_main_queue(), ^{
        TestRenderVideoFrame* strongSelf = weakSelf;
        UIImageView* videoView = nil;
        if (userId) {
            videoView = [strongSelf.userVideoViews objectForKey:userId];
        }
        else {
            videoView = strongSelf.localVideoView;
        }
        videoView.image = [UIImage imageWithCIImage:[CIImage imageWithCVImageBuffer:frame.pixelBuffer]];
        videoView.contentMode = UIViewContentModeScaleAspectFit;
        CFRelease(frame.pixelBuffer);
    });
}
```

### Android プラットフォーム
TRTCCloud の `setLocalVideoRenderListener` と `setRemoteVideoRenderListener`を介してローカルとリモート画面のカスタマイズレンダリングのコールバックを設定します。関連パラメータは次のとおりです。

| パラメータ名  | パラメータタイプ |  推奨値 | 付注|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTC_VIDEO_PIXEL_FORMAT_NV21 | カスタマイズレンダリングは現在のところ、texture をサポートしていません。  |
| bufferType | TRTCVideoBufferType| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY または<br> TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER  | BYTE_BUFFERは jni レイヤーでの使用に適し、BYTE_ARRAYはJava レイヤーでの直接操作に使用することができます。|


## オーディオキャプチャのカスタマイズ

TRTCCloud の `enableCustomAudioCapture` インターフェースを介してTRTC SDK デフォルトのサウンドキャプチャプロセスをオフにする必要があります。その後、 `sendCustomAudioData` インターフェースを使用してTRTC SDK に自身の声音データを入力することができます。

 `sendCustomAudioData` インターフェースに1フレームが20msの長さのオーディオデータを表す`TRTCAudioFrame`と呼ばれるパラメータがあります。
-  `sendCustomAudioData`  を介して SDKに 送信されるデータは 、AAC や他の圧縮形式ではなく、PCM フォーマットの非圧縮オーディオ生データでなければなりません。
- sampleRate と channelsはそれぞれサウンドサンプリングレートとサウンドチャンネル数を意味します。渡されるPCM データと厳密に一致させてください。
- フレームごとのオーディオデータの推奨時間は20msであり、次のように計算することができます。sampleRate が48000、サウンドチャンネルが1（モノラル）である場合、 sendCustomAudioData の各呼び出しで渡されるbufferの長さは：48000 * 0.02s * 1 * 16bit = 15360bit = 1920ビットでなければなりません。
- timestamp は0にすることができます。 timestamp が0である場合、SDK はオーディオタイムスタンプを自動的に入力します。以上より、オーディオタイムスタンプの安定性を確保するため、 `sendCustomAudioData`を**均等**に呼び出し、20msに1度の頻度を確保してください。そうしなければ、声音が途切れるという結果を招くおそれがあります。

>! endCustomAudioData`を使用すると、エコーキャンセル（AEC）の機能が無効になる場合があります。

## オーディオ生データの取得

音声モジュールは非常に複雑で、SDK は音声デバイスのキャプチャおよび再生ロジックを厳密に制御する必要があります。一部シーンにおいて、リモートユーザーのオーディオデータまたはローカルマイクによってキャプチャされたオーディオデータを取得する必要がある場合は、TRTCCloudに対応する異なるプラットフォームのインターフェースを介して 3つのコールバック関数をSDKに統合できます。
>?TRTCCloudに対応する異なるプラットフォームのインターフェースはそれぞれ次のとおりです。
>iOS：`setAudioFrameDelegate`、Android：`setAudioFrameListener`、Windows：`setAudioFrameCallback`。

- **onCapturedAudioFrame**
ローカルマイクがキャプチャしたオーディオ生データを取得します。カスタマイズされていないキャプチャモードにおいて、SDKは マイクの声音キャプチャ作業を担当しますが、SDK がキャプチャした音声生データを取得する必要のある場合は、このコールバック関数を介して取得できます。

- **onPlayAudioFrame**
この関数はミキシング前のデータである各リモートユーザーの音声データをコールバックします。あるチャネルの音声に対する音声識別を実行する場合は、このコールバックを使用することができます。

- **onMixedPlayAudioFrame**
各チャネルのオーディオデータをミキシングした後、再生のためにスピーカーに送信される前に、この関数を介してコールバックされます。

>!
>1. 音声が途切れたりエコーキャンセル（AEC）が無効になったりするトラブルが発生するおそれがありますので、上述のコールバック関数では時間のかかる操作を行わず、直接コピーして別のスレッドで処理することを推奨します。
>2. 各種の不確実な影響が生じるおそれがありますので、上述のコールバック関数でコールバックされたデータはいずれも読み取りとコピーのみが許可され、修正することはできません。





