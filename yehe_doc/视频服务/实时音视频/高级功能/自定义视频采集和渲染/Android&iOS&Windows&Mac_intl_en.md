This document describes how to use the TRTC SDK to implement custom video capturing and rendering.

## Custom Video Capturing

The custom video capturing feature of the TRTC SDK can be used in two steps: enabling the feature and sending video frames to the SDK. For detailed directions of specific APIs, see below. We also provide API examples for different platforms:

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/main/TRTC-API-Example-OC/Advanced/LocalVideoShare/LocalVideoShareViewController.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 

### Enabling custom video capturing

To enable the custom video capturing feature of the TRTC SDK, you need to call the `enableCustomVideoCapture` API of `TRTCCloud`. Then, the TRTC SDK's camera capturing and image processing logic will be skipped, and only its encoding and transfer capabilities will be retained. Below is the sample code:

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


### Sending custom video frames

Then, you can use the `sendCustomVideoData` API of `TRTCCloud` to populate the TRTC SDK with your own video data. Below is the sample code:

>? In order to avoid performance loss, there are different format requirements for the video data input to the TRTC SDK on different platforms. For more information, see [LiteAVSDK Overview](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_TRTCSDK_Download.html).


<dx-codeblock>
::: Android  Java
// Two schemes are available for Android: Texture (recommended) and Buffer. Texture is used as an example here.
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
// On iOS and macOS, the video captured by the camera is in NV12 format. The natively supported and best-performing video frame format is CVPixelBufferRef, and I420 and OpenGL 2D texture formats are also supported. CVPixelBufferRef is used as an example here, which is recommended. 
TRTCVideoFrame *videoFrame = [[TRTCVideoFrame alloc] init];
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelBuffer = imageBuffer;
videoFrame.timestamp = timeStamp;
        
[[TRTCCloud sharedInstance] sendCustomVideoData:TRTCVideoStreamTypeBig frame:videoFrame];   
:::
::: Windows  C++
// Only the Buffer scheme is available for Windows currently and is recommended for feature implementation.
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





## Custom Video Rendering

Custom rendering is mainly divided into rendering of the local video and rendering of the remote video. You can set the callback for local/remote custom rendering, and the TRTC SDK will pass the corresponding video frames (`TRTCVideoFrame`) through the callback function `onRenderVideoFrame`. Then, you can customize the rendering of the received video frames. This process requires certain knowledge of OpenGL. We also provide API examples for different platforms:

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java):
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/aa3026c07baeda553aec491702382683d5486a32/TRTC-API-Example-Swift/CustomCapture/testCustomVideo/TestRenderVideoFrame.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 


### Setting the local video rendering callback
<dx-codeblock>
::: Android  Java
mTRTCCloud.setLocalVideoRenderListener(TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE, new TRTCCloudListener.TRTCVideoRenderListener() {
    @Override
    public void onRenderVideoFrame(String suserId int streamType, TRTCCloudDef.TRTCVideoFrame frame) {
        // For more information, see the custom rendering tool class `com.tencent.trtc.mediashare.helper.CustomFrameRender` in `TRTC-API-Example`  
    }
});
:::
::: iOS&Mac ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
[self.trtcCloud setLocalVideoRenderDelegate:self pixelFormat:TRTCVideoPixelFormat_NV12 bufferType:TRTCVideoBufferType_PixelBuffer];
:::
::: Windows C++
```
// For specific implementation, see `test_custom_render.cpp` in `TRTC-API-Example-Qt`
void TestCustomRender::onRenderVideoFrame(
    const char* userId,
    liteav::TRTCVideoStreamType streamType,
    liteav::TRTCVideoFrame* frame) {
  if (gl_yuv_widget_ == nullptr) {
    return;
  }

  if (streamType == liteav::TRTCVideoStreamType::TRTCVideoStreamTypeBig) {
    // Adjust the rendering window
    emit renderViewSize(frame->width, frame->height);
    // Draw video frames
    gl_yuv_widget_->slotShowYuv(reinterpret_cast<uchar*>(frame->data),
                                frame->width, frame->height);
  }
}
```
:::
</dx-codeblock>


### Setting the rendering callback of remote video
<dx-codeblock>
::: Android  Java
mTRTCCloud.setRemoteVideoRenderListener(userId, TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_I420, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY, new TRTCCloudListener.TRTCVideoRenderListener() {
    @Override
    public void onRenderVideoFrame(String userId, int streamType, TRTCCloudDef.TRTCVideoFrame frame) {
         // For more information, see the custom rendering tool class `com.tencent.trtc.mediashare.helper.CustomFrameRender` in `TRTC-API-Example`  
    }
});
:::
::: iOS&Mac ObjC
- (void)onRenderVideoFrame:(TRTCVideoFrame *)frame 
                    userId:(NSString *)userId 
                streamType:(TRTCVideoStreamType)streamType
{
    // If `userId` is `nil`, the image rendered is the local image; otherwise it is a remote image.
    CFRetain(frame.pixelBuffer);
    __weak __typeof(self) weakSelf = self;
    dispatch_async(dispatch_get_main_queue(), ^{
        TestRenderVideoFrame *strongSelf = weakSelf;
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
:::
::: Windows C++
```
// For specific implementation, see `test_custom_render.cpp` in `TRTC-API-Example-Qt`
void TestCustomRender::onRenderVideoFrame(
    const char* userId,
    liteav::TRTCVideoStreamType streamType,
    liteav::TRTCVideoFrame* frame) {
  if (gl_yuv_widget_ == nullptr) {
    return;
  }

  if (streamType == liteav::TRTCVideoStreamType::TRTCVideoStreamTypeBig) {
    // Adjust the rendering window
    emit renderViewSize(frame->width, frame->height);
    // Draw video frames
    gl_yuv_widget_->slotShowYuv(reinterpret_cast<uchar*>(frame->data),
                                frame->width, frame->height);
  }
}
```
:::
</dx-codeblock>
