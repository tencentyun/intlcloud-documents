このドキュメントでは、主にTRTC SDKを使用してカスタムビデオキャプチャとレンダリングを実装する方法を紹介します。ビデオキャプチャとビデオレンダリングの2つの部分に分かれています。

## ビデオキャプチャのカスタマイズ

TRTC SDKのカスタムビデオキャプチャ機能の有効化は、機能の有効化とSDKへのビデオフレームの送信の2つの手順に分かれています。具体的なAPIの使用手順は次のとおりです。また、対応するプラットホームのAPI-Exampleも提供します：

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/main/TRTC-API-Example-OC/Advanced/LocalVideoShare/LocalVideoShareViewController.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 

### カスタムビデオキャプチャ機能の有効化

まず、TRTCCloudの`enableCustomVideoCapture`インターフェースを呼び出して、TRTC SDKのカスタムビデオキャプチャ機能を有効にする必要があります。有効にすると、TRTC SDK独自のカメラ取得および画像処理ロジックがスキップされ、エンコードおよび送信機能のみが保持されます。サンプルコードは次のとおりです：

<dx-codeblock>
::: Android  Java
TRTCCloud mTRTCCloud = TRTCCloud.shareInstance();
mTRTCCloud.enableCustomVideoCapture(TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG, true);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
[self.trtcCloud enableCustomVideoCapture:TRTCVideoStreamTypeBig enable:YES];
:::
::: Windows  C++
liteav::ITRTCCloud* trtc_cloud = liteav::ITRTCCloud::getTRTCShareInstance();
trtc_cloud->enableCustomVideoCapture(TRTCVideoStreamType::TRTCVideoStreamTypeBig, true);
:::
</dx-codeblock>


### カスタムビデオフレームの送信

次に、TRTCCloudの`sendCustomVideoData`インターフェースを使用して、TRTC SDKに独自のビデオデータを送信できます。サンプルコードは次のとおりです：

>? 不要な性能の低下を回避するために、TRTC SDKに入力されるビデオデータには、プラットフォームごとに異なるフォーマット要件があります。詳細については、APIドキュメント：[簡体字中国語](https://liteav.sdk.qcloud.com/doc/api/zh-cn/index.html)、[English](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_TRTCSDK_Download.html)を参照してください。


<dx-codeblock>
::: Android  Java
// Androidプラットフォームには、BufferとTextureの2つのスキームがあります。ここでは、Textureスキームを例として取り上げます。これを推薦します！
TRTCCloudDef.TRTCVideoFrame videoFrame = new TRTCCloudDef.TRTCVideoFrame();
videoFrame.texture = new TRTCCloudDef.TRTCTexture();
videoFrame.texture.textureId = textureId;
videoFrame.texture.eglContext14 = eglContext;
videoFrame.width = width;
videoFrame.height = height;
videoFrame.timestamp = timestamp;
videoFrame.pixelFormat = TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D;
videoFrame.bufferType = TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE;
mTRTCCloud.sendCustomVideoData(TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG, videoFrame);
:::
::: iOS&Mac  ObjC
// iOS/Macプラットフォームでは、カメラによってネイティブに取得されたビデオ形式はNV12であり、ネイティブにサポートされ、最高の性能を発揮するビデオフレーム形式はCVPixelBufferRefであり、I420およびOpenGL 2Dテクスチャ形式を同時にサポートします。ここで、CVPixelBufferRefを例として取り上げます。これを推薦します。
TRTCVideoFrame *videoFrame = [[TRTCVideoFrame alloc] init];
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelBuffer = imageBuffer;
videoFrame.timestamp = timeStamp;
        
[[TRTCCloud sharedInstance] sendCustomVideoData:TRTCVideoStreamTypeBig frame:videoFrame];   
:::
::: Windows  C++
// Windowsプラットフォームは現在、Bufferスキームのみをサポートしており、この方法で機能を実装することを推薦します。
liteav::TRTCVideoFrame frame;
frame.timestamp = getTRTCShareInstance()->generateCustomPTS();
frame.videoFormat = liteav::TRTCVideoPixelFormat_I420;
frame.bufferType = liteav::TRTCVideoBufferType_Buffer;
frame.length = buffer_size;
frame.data = array.data();
frame.width = YUV_WIDTH;
frame.height = YUV_HEIGHT;
getTRTCShareInstance()->sendCustomVideoData(&frame);

:::
</dx-codeblock>





## ビデオレンダリングのカスタマイズ

カスタムレンダリングは、主にローカルプレビュー画面のレンダリングとリモートユーザー画面のレンダリングに分けられています。基本的な原則として、ローカル/リモートのカスタムレンダリングコールバックを設定し、TRTC SDKは対応するビデオフレーム（つまり、TRTCVideoFrame）をコールバック関数`onRenderVideoFrame`に渡し、開発者は受信したビデオフレームに応じてレンダリングをカスタマイズできます。このプロセスには、特定のOpenGL基盤が必要です。また、対応するプラットフォームのAPI-Exampleも提供しています：

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)：
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/aa3026c07baeda553aec491702382683d5486a32/TRTC-API-Example-Swift/CustomCapture/testCustomVideo/TestRenderVideoFrame.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 


### ローカルプレビュー画面のレンダリングコールバックの設定
<dx-codeblock>
::: Android  Java
mTRTCCloud.setLocalVideoRenderListener(TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE, new TRTCCloudListener.TRTCVideoRenderListener() {
    @Override
    public void onRenderVideoFrame(String suserId int streamType, TRTCCloudDef.TRTCVideoFrame frame) {
        // 詳細については、TRTC-API-Exampleのカスタムレンダリングのツールクラスをご参照ください：com.tencent.trtc.mediashare.helper.CustomFrameRender  
    }
});
:::
::: iOS&Mac ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
[self.trtcCloud setLocalVideoRenderDelegate:self pixelFormat:TRTCVideoPixelFormat_NV12 bufferType:TRTCVideoBufferType_PixelBuffer];
:::
::: Windows C++
```
// 具体的な実装については、TRTC-API-Example-Qtのtest_custom_render.cppを参照してください。
void TestCustomRender::onRenderVideoFrame(
    const char* userId,
    liteav::TRTCVideoStreamType streamType,
    liteav::TRTCVideoFrame* frame) {
  if (gl_yuv_widget_ == nullptr) {
    return;
  }

  if (streamType == liteav::TRTCVideoStreamType::TRTCVideoStreamTypeBig) {
    // レンダリングウィンドウを調整します
    emit renderViewSize(frame->width, frame->height);
    // ビデオフレームを描画します
    gl_yuv_widget_->slotShowYuv(reinterpret_cast<uchar*>(frame->data),
                                frame->width, frame->height);
  }
}
```
:::
</dx-codeblock>


### リモートユーザー画面のレンダリングコールバックの設定
<dx-codeblock>
::: Android  Java
mTRTCCloud.setRemoteVideoRenderListener(userId, TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_I420, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY, new TRTCCloudListener.TRTCVideoRenderListener() {
    @Override
    public void onRenderVideoFrame(String userId, int streamType, TRTCCloudDef.TRTCVideoFrame frame) {
         // 詳細については、TRTC-API-Exampleのカスタムレンダリングのツールクラスをご参照ください：com.tencent.trtc.mediashare.helper.CustomFrameRender  
    }
});
:::
::: iOS&Mac ObjC
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
        else{
            videoView = strongSelf.localVideoView;
        }
        videoView.image = [UIImage imageWithCIImage:[CIImage imageWithCVImageBuffer:frame.pixelBuffer]];
        videoView.contentMode = UIViewContentModeScaleAspectFit;
        CFRelease(frame.pixelBuffer);
    });
}
:::
::: Windows C++
```
// 具体的な実装については、TRTC-API-Example-Qtのtest_custom_render.cppを参照してください。
void TestCustomRender::onRenderVideoFrame(
    const char* userId,
    liteav::TRTCVideoStreamType streamType,
    liteav::TRTCVideoFrame* frame) {
  if (gl_yuv_widget_ == nullptr) {
    return;
  }

  if (streamType == liteav::TRTCVideoStreamType::TRTCVideoStreamTypeBig) {
    // レンダリングウィンドウを調整します
    emit renderViewSize(frame->width, frame->height);
    // ビデオフレームを描画します
    gl_yuv_widget_->slotShowYuv(reinterpret_cast<uchar*>(frame->data),
                                frame->width, frame->height);
  }
}
```
:::
</dx-codeblock>
