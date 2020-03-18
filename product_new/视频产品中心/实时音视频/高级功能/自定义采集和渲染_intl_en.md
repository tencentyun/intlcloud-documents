## Introduction
- **Custom video capture**
If you develop (or purchase a third-party) beauty filter and special effects processing module, you need to capture and process the camera image by yourself. You can turn off the TRTC SDK's own camera image capture and processing logic through the `enableCustomVideoCapture` API of TRTCCloud, and then use the `sendCustomVideoData` API to populate the TRTC SDK with your own video data.

- **Custom video rendering**
The TRTC SDK uses OpenGL to render video image. If you are using it in game development or need to embed it in your own UI engine, you must render video image by yourself.

- **Custom audio capture**
If you are using the TRTC SDK on a special hardware device, when you need to use an external sound capture device to capture sound data, you can turn off the TRTC SDK's default sound capture process through the `enableCustomAudioCapture` API of TRTCCloud, and then use the `sendCustomAudioData` API to populate the TRTC SDK with your own audio data.
>!After custom audio capture is enabled, the acoustic echo cancellation (AEC) feature may fail.

- **Get raw audio data**
The sound module is highly complex, and the SDK needs to strictly control the capture and playback logic of the sound device. In some scenarios, when you need to get the audio data of a remote user or that captured by a local mic, you can implement it through the corresponding callback API provided by the TRTC SDK.

## Supported Platforms

| iOS | Android | macOS | Windows | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|   &#10003;  |  &#10003;    | &#10003;   |  &#10003;  |   ×  |  ×   |

## Custom Video Capture

You can turn off the TRTC SDK's own camera image capture and processing logic through the `enableCustomVideoCapture` API of TRTCCloud, and then use the `sendCustomVideoData` API to populate the TRTC SDK with your own video data.

There is a parameter named `TRTCVideoFrame` in the `sendCustomVideoData` API. It represents a frame of video image. In order to avoid performance loss, there are different format requirements for the video data input to the TRTC SDK on different platforms as shown below:

### iOS

The TRTC SDK supports both `NV12` and `i420` YUV data formats for iOS. On iOS, the relatively high-performance image transfer method is `CVPixelBufferRef`; therefore, the following parameter formats are recommended:

| Parameter Name | Parameter Type | Recommended Value | Remarks |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 | The video natively captured by the camera on iOS is in NV12 format. | 
| bufferType | TRTCVideoBufferType| PixelBuffer | This is the video frame format natively supported by iOS and has the best performance. |
| pixelBuffer| CVPixelBufferRef | Required if `TRTCVideoBufferType` is `PixelBuffer`. | The data captured by the camera on iPhone is `PixelBuffer` in NV12 format. |
| data| NSData\* | Required if `TRTCVideoBufferType` is `NSData`. | Its performance is not as good as `PixelBuffer`. |
| timestamp| uint64_t | 0 | 0 can be entered here, and the SDK will automatically set the `timestamp` field. However, please "evenly" set the calling interval of `sendCustomVideoData`. |
| width    | uint64_t| Video image width | Please strictly enter the pixel width of the video image passed in. |
| height   | uint32_t| Video image height | Please strictly enter the pixel height of the video image passed in. |
| rotation | TRTCVideoRotation| Empty | This field is used for custom rendering and does not need to be set here. |

**Sample code**: There is a file named `TestSendCustomVideoData.m` in the demo folder, which shows how to read out a `PixelBuffer` in NV12 format from a local video file and process it with the SDK.

```objectiveC
// Assemble a `TRTCVideoFrame` and send it to the trtcCloud object
TRTCVideoFrame* videoFrame = [TRTCVideoFrame new];
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
        
[trtcCloud sendCustomVideoData:videoFrame];      
```

### Android

There are two schemes for Android:

**1. `buffer` scheme**: its connection is easy but its performance is poor, so it is not suitable for scenarios with high resolution.

The `buffer` scheme requires that an array in byte[] format be inserted directly into the TRTC SDK. It supports two YUV formats, namely, i420 and NV21.

| Parameter Name | Parameter Type | Recommended Value | Remarks |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| int | TRTC_VIDEO_PIXEL_FORMAT_I420 or <br> TRTC_VIDEO_PIXEL_FORMAT_NV21  | i420 and NV21 are two different YUV data formats. | 
| bufferType | int | TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY | It indicates to transfer YUV data in the `data` method. |
| texture  | TRTCTexture | Empty for the `buffer` scheme | If i420 or NV21 format is selected, leave this parameter empty. |
| data| byte[] | Data buffer in YUV format | Memory in Java type is packed, which is suitable for use at the Java layer. |
| buffer| ByteBuffer | Empty for the `buffer` scheme | Memory in C/C++ type is packed, which is suitable for use at the JNI layer. |
| width    | uint64_t| Video image width | Please strictly enter the pixel width of the video image passed in. |
| height   | uint32_t| Video image height | Please strictly enter the pixel height of the video image passed in. |
| timestamp| long | Capture time of video frame | 0 can be entered here, and the SDK will automatically set the `timestamp` field. However, please "evenly" set the calling interval of `sendCustomVideoData`. |
| rotation | int| Empty | This field is not required if `sendCustomVideoData` is selected. |

**2. `texture` scheme: its connection requires certain knowledge of OpenGL, but its performance is good, especially when the video resolution is high.

The `texture` scheme needs to pass OpenGL textures to the TRTC SDK. In order to ensure the normal operation of this scheme, you need to set up the OpenGL environment in advance. As a result, the connection of this scheme is very difficult. If you have no knowledge of OpenGL, you are recommended to use the provided sample code directly, which is located in the `customCapture` folder of the demo, including:

| File Name | Source Code Logic | 
|---------|---------|
|TestSendCustomVideoData.java| Demonstrates how to feed video textures to the SDK via the `sendCustomVideoData` function of TRTCCloud. |
|TestRenderVideoFrame.java| Demonstrates how to ignore the original rendering logic of TRTCCloud and render the video image with OpenGL. |
|MovieVideoFrameReader.java| Reads the video image frame by frame from a local video file. |
| openGLBaseModule/EglCore.java | Encapsulates the basic functions of OpenGL to make it easier to use. |
| openGLBaseModule/EglSurfaceBase.java | Encapsulates the basic functions of GLSurface to make it easier to use. |
| openGLBaseModule/GLFilter.java| There are many types of textures on Android, and they cannot be mixed. This class encapsulates some basic operations for texture conversion. |
| openGLBaseModule/GLThread.java| Encapsulates a basic OpenGL thread. Generally, OpenGL rendering on Android needs to be driven by an independent thread. |

> For resolutions above 640x360, the `texture` scheme is recommended so as to avoid excessive CPU utilization.


**Sample code**: the code in `TestSendCustomVideoData.java` is quite complicated:
1. The code first starts a GLThread thread, which is in waiting status most of the time until its associated `SurfaceTexture` is drawn.
2. The code next uses a module named `MovieVideoFrameReader` to read the video image frame by frame from the local video file and draw the frames on the `SurfaceTexture` created in the previous step.
3. Each time a frame is drawn, the GLThread thread created in the first step will be waken up once, so there will be the `onTextureProcess` callback below. In this callback function, the obtained textures are passed to the SDK through the `sendCustomVideoData` function:

```java
public int onTextureProcess(int textureId, EGLContext eglContext) {
        if (!mIsSending) return textureId;

        // Populate video frames to the SDK through texture
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

The TRTC SDK uses OpenGL to render video image. If you are using it in game development or need to embed it in your own UI engine, you must render video image by yourself.

### iOS (including iMac)

Custom rendering callbacks for local and remote video images can be set through `setLocalVideoRenderDelegate` and `setRemoteVideoRenderDelegate` of TRTCCloud. The relevant parameters are as follows:

| Parameter Name | Parameter Type | Recommended Value | Remarks |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 |  - | 
| bufferType | TRTCVideoBufferType| TRTCVideoBufferType_PixelBuffer | This is the video frame format natively supported by iOS and has the best performance. |

**Sample code**: If `TRTCVideoPixelFormat_NV12` is selected for `pixelFormat` and `TRTCVideoBufferType_PixelBuffer` is selected for `bufferType`, then you can easily convert a frame of `PixelBuffer` in NV12 format into a frame of video image. There is a file named `TestRenderVideoFrame.m` in the demo folder, which shows how to use this method with the following sample code.
```objectiveC
- (void)onRenderVideoFrame:(TRTCVideoFrame *)frame 
                                userId:(NSString *)userId 
						        streamType:(TRTCVideoStreamType)streamType
{
    // If `userId` is `nil`, the image is local image; otherwise, it is remote image
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
Custom rendering callbacks for local and remote video images can be set through `setLocalVideoRenderListener` and `setRemoteVideoRenderListener` of TRTCCloud. The relevant parameters are as follows:

| Parameter Name | Parameter Type | Recommended Value | Remarks |
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTC_VIDEO_PIXEL_FORMAT_NV21 | Custom rendering does not support the `texture` scheme currently. | 
| bufferType | TRTCVideoBufferType| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY or <br> TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER  |  `BYTE_BUFFER` is suitable for the JNI layer, while `BYTE_ARRAY` can be used in direct operations at the Java layer. |


## Custom Audio Capture

You can turn off the TRTC SDK's default sound capture process through the `enableCustomAudioCapture` API of TRTCCloud, and then use the `sendCustomAudioData` API to populate the TRTC SDK with your own audio data.

There is a parameter named `TRTCAudioFrame` in the `sendCustomAudioData` API, which represents a frame of audio data lasting for 20 ms:
- The data sent to the SDK through `sendCustomAudioData` must be uncompressed raw audio data in PCM format but not in AAC or other compressed formats.
- `sampleRate` and `channels` represent the sample rate and number of sound channels of the audio respectively, which should strictly match the PCM data passed in.
- The recommended duration of each frame of audio data is 20 ms. For a simple calculation, if the `sampleRate` is 48,000 and `channels` is 1 (mono), then the length of the `buffer` passed in each time `sendCustomAudioData` is called should be 48000 * 0.02s * 1 * 16 bits = 15360 bits = 1920 bytes.
- `timestamp` can be 0. In this case, the SDK will automatically populate the audio timestamp. Therefore, in order to ensure the stability of the audio timestamp, please call `sendCustomAudioData` **evenly** (i.e., once every 20 ms); otherwise, the sound will be intermittent.

>Using `sendCustomAudioData` may cause acoustic echo cancellation (AEC) to fail.

## Getting Raw Audio Data

The sound module is highly complex, and the SDK needs to strictly control the capture and playback logic of the sound device. In some scenarios, when you need to get the audio data of a remote user or that captured by a local mic, you can integrate the three callback functions into the SDK through the APIs of TRTCCloud for different platforms.
>? The APIs of TRTCCloud for different platforms are as follows:
>iOS: `setAudioFrameDelegate`; Android: `setAudioFrameListener`; Windows: `setAudioFrameCallback`.

- **onCapturedAudioFrame**
Get the raw audio data captured by the local mic. In non-custom capture mode, the SDK will be responsible for mic sound capture, but you may also need to get the raw audio data captured by the SDK, which can be done through this callback function.

- **onPlayAudioFrame**
This function will call back the sound data of each remote user, which is the data before mixing. You can use this callback if you want to perform speech recognition on a certain channel of audio.

- **onMixedPlayAudioFrame**
After all audio data is mixed, it will be called back by this function before being sent to the speaker for playback.

>
1. Do not perform any time-consuming operation in this callback function. It is recommended to directly copy the data to another thread for processing; otherwise, intermittent sound or acoustic echo cancellation (AEC) failure may occur.
2. The data called back by the above callback functions can only be read and copied but not modified; otherwise, various uncertain consequences may occur.





