본문에서는 TRTC SDK를 사용하여 사용자 정의 비디오 캡처 및 렌더링을 구현하는 방법을 설명합니다.

## 사용자 정의 비디오 캡처

TRTC SDK의 사용자 정의 비디오 캡처 기능은 기능 활성화와 SDK로 비디오 프레임 전송의 두 단계로 사용할 수 있습니다. 특정 API에 대한 자세한 안내는 아래를 참고하십시오. 또한 다양한 플랫폼에 대한 API-Example을 제공합니다.

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/main/TRTC-API-Example-OC/Advanced/LocalVideoShare/LocalVideoShareViewController.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 

### 사용자 정의 비디오 캡처 활성화

TRTC SDK의 사용자 정의 비디오 캡처 기능을 활성화하려면 TRTCCloud의 `enableCustomVideoCapture` API를 호출해야 합니다. 그러면 TRTC SDK의 카메라 캡처 및 이미지 처리 로직은 건너뛰고 인코딩 및 전송 기능만 유지됩니다. 아래는 샘플 코드입니다.

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


### 사용자 정의 비디오 프레임 전송

그런 다음 TRTCCloud의 `sendCustomVideoData` API를 사용하여 TRTC SDK에 자신의 비디오 데이터를 전송할 수 있습니다. 아래는 샘플 코드입니다.

>? 성능 손실을 방지하기 위해 다양한 플랫폼에서 TRTC SDK에 입력되는 비디오 데이터에 대해 다양한 형식 요구 사항이 있습니다. 자세한 내용은 [LiteAVSDK 개요](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_TRTCSDK_Download.html)를 참고하십시오.


<dx-codeblock>
::: Android  Java
// Android에는 Buffer 및 Texture의 두 가지 구성표를 사용할 수 있습니다(권장). 여기에서는 Texture를 예시로 사용했습니다.
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
// iOS/Mac에서 카메라로 캡처한 비디오는 NV12 형식이고 기본적으로 지원되는 최고 성능의 비디오 프레임 형식은 CVPixelBufferRef이며 I420 및 OpenGL 2D 텍스처 형식도 지원됩니다(권장). 여기에서는 CVPixelBufferRef가 예시로 사용되었습니다.
TRTCVideoFrame *videoFrame = [[TRTCVideoFrame alloc] init];
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelBuffer = imageBuffer;
videoFrame.timestamp = timeStamp;
        
[[TRTCCloud sharedInstance] sendCustomVideoData:TRTCVideoStreamTypeBig frame:videoFrame];   
:::
::: Windows  C++
// 현재 Windows에서는 Buffer 구성표만 사용할 수 있으며 기능 구현에 권장됩니다.
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





## 사용자 정의 비디오 렌더링

사용자 정의 랜더링은 크게 로컬 비디오 랜더링과 원격 비디오 랜더링으로 나뉩니다. 로컬/원격 사용자 정의 렌더링에 대한 콜백을 설정할 수 있으며, TRTC SDK는 콜백 함수 `onRenderVideoFrame`을 통해 해당 비디오 프레임(TRTCVideoFrame)을 전달합니다. 그런 다음 수신된 비디오 프레임의 렌더링을 사용자 정의할 수 있습니다. 이 프로세스에는 OpenGL에 대한 특정 지식이 필요합니다. 또한 다양한 플랫폼에 대한 API-Example을 제공합니다.

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)：
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/aa3026c07baeda553aec491702382683d5486a32/TRTC-API-Example-Swift/CustomCapture/testCustomVideo/TestRenderVideoFrame.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 


### 로컬 비디오 렌더링 콜백 설정
<dx-codeblock>
::: Android  Java
mTRTCCloud.setLocalVideoRenderListener(TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE, new TRTCCloudListener.TRTCVideoRenderListener() {
    @Override
    public void onRenderVideoFrame(String suserId int streamType, TRTCCloudDef.TRTCVideoFrame frame) {
        // 자세한 내용은 TRTC-API-Example의 사용자 정의 렌더링 도구 클래스 com.tencent.trtc.mediashare.helper.CustomFrameRender 참고  
    }
});
:::
::: iOS&Mac ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
[self.trtcCloud setLocalVideoRenderDelegate:self pixelFormat:TRTCVideoPixelFormat_NV12 bufferType:TRTCVideoBufferType_PixelBuffer];
:::
::: Windows C++
```
// 구체적인 구현은 TRTC-API-Example-Qt의 test_custom_render.cpp 참고
void TestCustomRender::onRenderVideoFrame(
    const char* userId,
    liteav::TRTCVideoStreamType streamType,
    liteav::TRTCVideoFrame* frame) {
  if (gl_yuv_widget_ == nullptr) {
    return;
  }

  if (streamType == liteav::TRTCVideoStreamType::TRTCVideoStreamTypeBig) {
    // 렌더링 창 조정
    emit renderViewSize(frame->width, frame->height);
    // 비디오 프레임 그리기
    gl_yuv_widget_->slotShowYuv(reinterpret_cast<uchar*>(frame->data),
                                frame->width, frame->height);
  }
}
```
:::
</dx-codeblock>


### 원격 비디오의 렌더링 콜백 설정
<dx-codeblock>
::: Android  Java
mTRTCCloud.setRemoteVideoRenderListener(userId, TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_I420, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY, new TRTCCloudListener.TRTCVideoRenderListener() {
    @Override
    public void onRenderVideoFrame(String userId, int streamType, TRTCCloudDef.TRTCVideoFrame frame) {
         // 자세한 내용은 TRTC-API-Example의 사용자 정의 렌더링 도구 클래스 com.tencent.trtc.mediashare.helper.CustomFrameRender 참고  
    }
});
:::
::: iOS&Mac ObjC
- (void)onRenderVideoFrame:(TRTCVideoFrame *)frame 
                    userId:(NSString *)userId 
                streamType:(TRTCVideoStreamType)streamType
{
    //userId가 nil이면 로컬 화면, 그렇지 않을 경우 원격 화면
    CFRetain(frame.pixelBuffer);
    __weak __typeof(self) weakSelf = self;
    dispatch_async(dispatch_get_main_queue(), ^{
        TestRenderVideoFrame *strongSelf = weakSelf;
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
// 구체적인 구현은 TRTC-API-Example-Qt의 test_custom_render.cpp 참고
void TestCustomRender::onRenderVideoFrame(
    const char* userId,
    liteav::TRTCVideoStreamType streamType,
    liteav::TRTCVideoFrame* frame) {
  if (gl_yuv_widget_ == nullptr) {
    return;
  }

  if (streamType == liteav::TRTCVideoStreamType::TRTCVideoStreamTypeBig) {
    // 렌더링 창 조정
    emit renderViewSize(frame->width, frame->height);
    // 비디오 프레임 그리기
    gl_yuv_widget_->slotShowYuv(reinterpret_cast<uchar*>(frame->data),
                                frame->width, frame->height);
  }
}
```
:::
</dx-codeblock>
