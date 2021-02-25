## Overview
- **Custom video capturing**
If you develop your own beauty filter and special effect processing modules or purchase from third parties, you need to capture and process camera data by yourself. You can call the `enableCustomVideoCapture` API of `TRTCCloud` to disable the TRTC SDK's camera data capturing and processing logic, and use the `sendCustomVideoData` API to feed your own video data to the TRTC SDK.
- **Custom video rendering**
The TRTC SDK uses OpenGL to render video images. If you use the SDK for game development or want to integrate it into your own UI engine, you must render video images by yourself.
- **Custom audio capturing**
If you use the TRTC SDK on a special device, to capture your own audio data via an external device, you can call the `enableCustomAudioCapture` API of `TRTCCloud` to disable the TRTC SDK’s default audio capturing process, and use the `sendCustomAudioData` API to feed your own audio data to the TRTC SDK.
>!Enabling custom audio capturing may cause the acoustic echo cancellation (AEC) feature to fail.
- **Getting raw audio data**
The audio module is highly complex, and the TRTC SDK needs to strictly control the capturing and playback logic of audio devices. In some cases, you can use the callback APIs of the SDK to get the audio data of a remote user or that captured by the local mic.

## Supported Platforms

| iOS | Android | macOS | Windows | Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|
|   &#10003;  |  &#10003;    | &#10003;   |  &#10003;  |  ×   |

## Custom Video Capturing

You can call the `enableCustomVideoCapture` API of `TRTCCloud` to disable the TRTC SDK's camera data capturing and processing logic, and use the `sendCustomVideoData` API to feed your own video data to the TRTC SDK.

The `sendCustomVideoData` API includes a parameter named `TRTCVideoFrame`, which represents a video frame. To avoid performance loss, the TRTC SDK has requirements on the format of video data it receives, which vary with the platform used.

### iOS

On iOS, the TRTC SDK supports data in two YUV formats: NV12 and i420. Image transferring via `CVPixelBufferRef` delivers higher performance on iOS. Given this, we recommend the following settings.

| Parameter Name  | Parameter Type |  Recommended Value | Note |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 | NV12 is the original format of the video data captured by an iOS device. |
| bufferType | TRTCVideoBufferType| PixelBuffer | This is the video frame format supported by iOS, and it delivers the best performance. |
| pixelBuffer| CVPixelBufferRef | Required if `TRTCVideoBufferType` is `PixelBuffer`. | The data captured by iPhone’s camera is NV12 formatted PixelBuffer. |
| data| NSData\* | Required if `TRTCVideoBufferType` is `NSData`. | NSData is no match for PixelBuffer in terms of performance. |
| timestamp| uint64_t | 0 | If it is 0, the SDK will set the `timestamp` field automatically, but please make sure that `sendCustomVideoData` is called at largely **regular** intervals. |
| width    | uint64_t| Video image width | Keep it strictly in line with the pixel width of the video passed in. |
| height   | uint32_t| Video image height | Keep it strictly in line with the pixel height of the video passed in. |
| rotation | TRTCVideoRotation|Leave it empty |  <li/>It is left empty by default. <li/>If you want to rotate the video, set it to `TRTCVideoRotation_0`, `TRTCVideoRotation_90`, `TRTCVideoRotation_180`, or `TRTCVideoRotation_270`. The SDK will rotate the video clockwise by the number of degrees set. For example, if `TRTCVideoRotation_90` is passed in, an image in the portrait mode will switch to the landscape mode after rotation. |

**Sample code**: the [demo](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo/CustomCapture/testCustomVideo) folder includes a file named `TestSendCustomVideoData.m`, which shows how to extract NV12 formatted PixelBuffer from a local video file and process the data using the SDK.

```objectiveC
// Assemble `TRTCVideoFrame` and send it to a trtcCloud object.
TRTCVideoFrame* videoFrame = [TRTCVideoFrame new];
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
        
[trtcCloud sendCustomVideoData:videoFrame];      
```

### Android

There are two custom video capturing schemes for Android.

**1. Buffer scheme**: integration using this scheme is relatively easy, but it delivers mediocre performance and is therefore not recommended for scenarios with high requirements on resolution.

The buffer scheme involves feeding byte[] arrays to the TRTC SDK. Two YUV formats are supported: i420 and NV21.

| Parameter Name  | Parameter Type |  Recommended Value | Note |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| int | TRTC_VIDEO_PIXEL_FORMAT_I420 or <br> TRTC_VIDEO_PIXEL_FORMAT_NV21  | i420 and NV21 are two different YUV data formats. |
| bufferType | int | TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY | Specify the data type in which YUV data is transferred. |
| texture  | TRTCTexture | Leave it empty if the buffer scheme is used. | If the i420 or NV21 format is used, leave this parameter empty. |
| data| byte[] | YUV formatted data buffers | Memory in Java type is packed, which is suitable for use at the Java layer. |
| buffer| ByteBuffer | Leave it empty if the buffer scheme is used. | Memory in C/C++ type is packed, which is suitable for use at the JNI layer. |
| width    | uint64_t| Video image width | Keep it strictly in line with the pixel width of the video passed in. |
| height   | uint32_t| Video image height | Keep it strictly in line with the pixel height of the video passed in. |
| timestamp| long | Capturing time of video frames | If the value is 0, the SDK will set the field automatically, but please make sure that `sendCustomVideoData` is called at largely **regular** intervals. |
| rotation | int| Leave it empty. | <li/>It is left empty by default. <li/>If you want to rotate the video, set it to 0, 90, 180, or 270. The SDK will rotate the video clockwise by the number of degrees set. For example, if 90 is passed in, an image in the portrait mode will switch to the landscape mode after rotation. |

**2. Texture scheme**: integration via this scheme requires knowledge of OpenGL. It delivers superior performance, especially when video resolution is high.

The texture scheme involves passing OpenGL textures to the TRTC SDK. For this scheme to work, you need to set up an OpenGL environment in advance. As a result, integration via this scheme is quite demanding on developers. If you have no knowledge of OpenGL, we recommend that you use the sample code we provide, which is in the `customCapture` folder of the [demo](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCSimpleDemo/customcapture/src/main/java/com/tencent/custom/customcapture). The folder contains the following items:

| File Name | Source Code Logic |
|---------|---------|
|TestSendCustomVideoData.java| Demonstrates how to feed video textures to the SDK via the `sendCustomVideoData` function of `TRTCCloud` |
|TestRenderVideoFrame.java| Demonstrates how to ignore the rendering logic of `TRTCCloud` and render video images with OpenGL |
|VideoFrameReader.java    |    Demonstrates how to extract video data frame by frame from a local video file|
| `decoder` folder | Decoding module |
| `opengl` folder   |     Basic functions of OpenGL, which facilitate the use of the code|
| render folder    |    Basic functions of EGL, which facilitate the use of the code|

>! To avoid excessively high CPU usage, you are advised to use the texture scheme for resolutions higher than 640 x 360.


**Sample code**: the code in `TestSendCustomVideoData.java` is complicated.
1. The code first starts a GLThread thread, which is in the waiting state until content is drawn on the `SurfaceTexture` with which it is associated.
2. The code then uses a module named `MovieVideoFrameReader` to extract video images frame by frame from a local video file and draws the frames on the `SurfaceTexture` created.
3. Each time a frame is drawn, the GLThread thread created in step 1 wakes up, hence the `onTextureProcess` callback below. Pass the textures obtained from the callback to the SDK through `sendCustomVideoData`.

```java
public int onTextureProcess(int textureId, EGLContext eglContext) {
        if (!mIsSending) return textureId;

        // Feed video frames as textures to the SDK.
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


## Custom Video Rendering

The TRTC SDK uses OpenGL to render video images. If you use the SDK for game development or want to integrate it into your own UI engine, you must render video images by yourself.

### iOS (including iMac)

You can call `setLocalVideoRenderDelegate` and `setRemoteVideoRenderDelegate` of `TRTCCloud` to configure custom rendering callbacks for local and remote video images. Below are the relevant parameters.

| Parameter Name  | Parameter Type |  Recommended Value | Note |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 |  - |
| bufferType | TRTCVideoBufferType| TRTCVideoBufferType_PixelBuffer | This is the video frame format supported by iOS, and it delivers the best performance. |

[](id:example_ios)
#### Sample code
If you set `pixelFormat` to `TRTCVideoPixelFormat_NV12` and `bufferType` to `TRTCVideoBufferType_PixelBuffer`, it would be easy to convert a frame of NV12 formatted PixelBuffer into a video image. The specific method is demonstrated by the code in `TestRenderVideoFrame.m`, which you can find in the demo folder.

```objectiveC
- (void)onRenderVideoFrame:(TRTCVideoFrame *)frame 
                                userId:(NSString *)userId 
						        streamType:(TRTCVideoStreamType)streamType
{
    // If `userId` is `nil`, the image rendered is the local image; otherwise it is a remote image.
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

### Android
You can call `setLocalVideoRenderListener` and `setRemoteVideoRenderListener` of `TRTCCloud` to set custom rendering callbacks for local and remote video images. Below are the relevant parameters.

| Parameter Name  | Parameter Type |  Recommended Value | Note |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTC_VIDEO_PIXEL_FORMAT_NV21 | Custom rendering does not support the texture scheme for the time being. |
| bufferType | TRTCVideoBufferType| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY or <br> TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER  |  `BYTE_BUFFER` is suitable for the JNI layer, and `BYTE_ARRAY` can be used for operations at the Java layer. |

[](id:example_android)
#### Sample code
```
    public void onRenderVideoFrame(String userId, int streamType, final TRTCCloudDef.TRTCVideoFrame frame) {
        if (!userId.equals(mUserId) || mSteamType != streamType) {
            // If the `id` or `streamtype` of the rendering callback does not match,
            return;
        }
        if (frame.texture != null) {
            // Wait for the texture drawing of `frame.texture` to finish.
            GLES20.glFinish();
        }
        Size mSurfaceSize; // Set the height and width of the surface.
        GpuImageI420Filter mYUVFilter;
        GLES20.glViewport(0, 0, mSurfaceSize.width, mSurfaceSize.height);
        GLES20.glBindFramebuffer(GLES20.GL_FRAMEBUFFER, 0);
        GLES20.glClearColor(0, 0, 0, 1.0f);
        GLES20.glClear(GLES20.GL_DEPTH_BUFFER_BIT | GLES20.GL_COLOR_BUFFER_BIT);
        if (frame.data != null) {
            mYUVFilter.loadYuvDataToTexture(frame.data, frame.width, frame.height);
        } else {
            mYUVFilter.loadYuvDataToTexture(frame.buffer, frame.width, frame.height);
        }         
        mYUVFilter.onDraw(NO_TEXTURE, mGLCubeBuffer, mGLTextureBuffer);
        
    }
```

### Custom Audio Capturing

You can call the `enableCustomAudioCapture` API of `TRTCCloud` to disable the TRTC SDK's default audio data capturing process, and use the `sendCustomAudioData` API to feed your own audio data to the TRTC SDK.

The `sendCustomAudioData` API includes a parameter named `TRTCAudioFrame`, which represents a 20 ms audio frame.
- The data sent to the SDK through `sendCustomAudioData` must be uncompressed raw audio data in the PCM format. ACC or other compressed formats are not supported.
- `sampleRate` and `channels` represent the audio sample rate and audio channel number respectively, which should be kept strictly in line with the PCM data passed in.
- The recommended duration of each audio frame is 20 ms. Suppose `sampleRate` is 48,000, and `channels` is 1 (mono). The byte length of the buffer passed in each time `sendCustomAudioData` is called would be 48,000 x 0.02s x 1 x 16 bits=15,360 bits=1,920 bytes.
- If `timestamp` is set to 0, the SDK will set the field automatically. Therefore, to ensure the stability of the audio timestamp, please make sure that `sendCustomAudioData` is called at largely **regular** intervals, preferably every 20 ms; otherwise the audio may be choppy.

>!Using `sendCustomAudioData` may AEC to fail.

## Getting Raw Audio Data

The audio module is highly complex, and the TRTC SDK needs to strictly control the capturing and playback logic of audio devices. In some cases, to get the audio data of a remote user or that captured by the local mic, you can use the APIs `TRTCCloud` offers for different platforms to integrate the following callback functions into the SDK.

>? The `TRTCCloud` API used for different platforms are:
>- iOS：setAudioFrameDelegate
>- Android：setAudioFrameListener
>- Windows：setAudioFrameCallback

| Callback Function | Description |
|---------|---------|
| onCapturedAudioFrame | Get the raw audio data captured by the local mic. In the non-custom capturing mode, the SDK is responsible for capturing audio, but you may want to get the raw audio data, which can be achieved using this callback function. |
| onPlayAudioFrame | This function calls back the audio data of each remote user, which is the data before audio mixing. You can use this callback if you want to perform speech recognition on a specific channel of audio. |
| onMixedPlayAudioFrame | This function calls back mixed audio data before it is fed into the speaker for playback. |

>!
>- Do not perform time-consuming operations with any of the above callback function. We recommend that you copy the data to another thread for processing to avoid AEC failure and choppy audio.
>- The data called back by the above callback functions can only be read and copied. Modifications to the data may lead to unexpected outcomes.
