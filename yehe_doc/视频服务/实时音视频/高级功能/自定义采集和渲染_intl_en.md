## Overview

- **Custom video capturing**
  If you develop your own beauty filter and special effect processing modules or purchase from third parties, you need to capture and process camera data by yourself. You can call the `enableCustomVideoCapture` API of `TRTCCloud` to disable the camera capturing and image processing logic of the TRTC SDK, and use the `sendCustomVideoData` API to feed your own video data to the TRTC SDK.
- **Custom video rendering**
  The TRTC SDK uses OpenGL to render video images. If you use the SDK for game development or want to integrate it into your own UI engine, you must render video images by yourself.
- **Custom audio capturing**
  If you use the TRTC SDK on a special device, to capture your own audio data via an external device, you can call the `enableCustomAudioCapture` API of `TRTCCloud` to disable the TRTC SDK’s default audio capturing process, and use the `sendCustomAudioData` API to feed your own audio data to the TRTC SDK.
>!Enabling custom audio capturing may cause the acoustic echo cancellation (AEC) feature to fail.
- **Getting raw audio data**
  The audio module is a highly complex module, and the TRTC SDK needs to strictly control the capturing and playback logic of audio devices. In some cases, you can use the callback APIs of the SDK to get the audio data of a remote user or that captured by the local mic.

## Supported Platforms

|   iOS    | Android  |  macOS  | Windows  | Chrome |
| :------: | :------: | :------: | :------: | :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; |       ×       |

## Custom Video Capturing

You can call the `enableCustomVideoCapture` API of `TRTCCloud` to disable the TRTC SDK's camera capturing and image processing logic, and use the `sendCustomVideoData` API to feed your own video data to the TRTC SDK.

The `sendCustomVideoData` API includes a parameter named `TRTCVideoFrame`, which represents a video frame. To avoid performance loss, the TRTC SDK has requirements on the format of video data it receives, which vary with the platform used.

#### iOS
On iOS, the TRTC SDK supports data in two YUV formats: NV12 and I420. Image transferring via `CVPixelBufferRef` delivers higher performance on iOS. Given this, we recommend the following settings.

|  Parameter   |       Type       |                      Recommended Value                       |                           Note                           |
| :---------: | :------------------: | :-------------------------------------------------: | :----------------------------------------------------------: |
| pixelFormat | TRTCVideoPixelFormat |              TRTCVideoPixelFormat_NV12              |       NV12 is the format of the original video data captured by an iOS device.        |
| bufferType  | TRTCVideoBufferType  |                     PixelBuffer                     |            This is the video frame format supported by iOS, and it delivers the best performance.             |
| pixelBuffer| CVPixelBufferRef | Required if `TRTCVideoBufferType` is `PixelBuffer`. | The data captured by iPhone’s camera is NV12 formatted PixelBuffer. |
|    data     |       NSData\*       |   Required if `TRTCVideoBufferType` is `NSData`    |                    It is no match for PixelBuffer in terms of performance.                    |
|  timestamp  |       uint64_t       |                          0                          | It can be 0, in which case the SDK will fill the timestamp field automatically, but please make sure that `sendCustomVideoData` is called at largely regular intervals. |
|    width    |       uint64_t       |                   Width of the video image                    |                Keep it strictly in line with the pixel width of the video passed in.                |
|   height    |       uint32_t       |                   Height of the video image                    |                Keep it strictly in line with the pixel height of the video passed in.                |
|  rotation   |  TRTCVideoRotation   |                       Leave it empty                        | <ul style="margin:0"><li/>It is left empty by default. <li/>If you want to rotate the video, set it to `TRTCVideoRotation_0`, `TRTCVideoRotation_90`, `TRTCVideoRotation_180`, or `TRTCVideoRotation_270`. The SDK will rotate the video clockwise by the number of degrees set. For example, if `TRTCVideoRotation_90` is passed in, an image in the portrait mode will switch to the landscape mode after rotation.</ul> |

#### Sample code
The [demo](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo/CustomCapture/testCustomVideo) folder includes a file named `TestSendCustomVideoData.m`, which shows how to extract NV12 formatted PixelBuffer from a local video file and process the data using the SDK.

```objectiveC
// Assemble a `TRTCVideoFrame` and send it to a `trtcCloud` object.
TRTCVideoFrame* videoFrame = [TRTCVideoFrame new];
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
        
[trtcCloud sendCustomVideoData:videoFrame];      
```
#### Android
There are two custom video capturing schemes for Android, as shown below.
- **Buffer scheme**: this scheme is relatively easy, but it delivers mediocre performance and is therefore not recommended for scenarios with high requirements on resolution.
The buffer scheme involves feeding byte[] arrays to the TRTC SDK. Two YUV formats are supported: I420 and NV21.
<table>
<thead><tr><th>Parameter</th><th>Type</th><th>Recommended Value</th><th>Note</th></tr></thead>
<tbody><tr>
  <td>pixelFormat</td>
  <td>int</td>
  <td>TRTC_VIDEO_PIXEL_FORMAT_I420 or <br> TRTC_VIDEO_PIXEL_FORMAT_NV21</td>
  <td>I420 and NV21 are two different YUV data formats.</td>
</tr><tr>
  <td>bufferType</td>
  <td>int</td>
  <td>TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY</td>
  <td>Specify that Data is used to transfer YUV data.</td>
</tr><tr>
  <td>texture</td>
  <td>TRTCTexture</td>
  <td>Leave it empty if the buffer scheme is used.</td>
  <td>If the I420 or NV21 format is used, leave this parameter empty.</td>
</tr><tr>
  <td>data</td>
  <td>byte[]</td>
  <td>YUV formatted data buffers</td>
  <td>Memory in Java type is packed, which is suitable for use at the Java layer.</td>
</tr><tr>
  <td>buffer</td>
  <td>ByteBuffer</td>
  <td>Leave it empty if the buffer scheme is used.</td>
  <td>in C/C++ type is packed, which is suitable for use at the JNI layer.</td>
</tr><tr>
  <td>width</td>
  <td>uint64_t</td>
  <td>Width of the video image</td>
  <td>Keep it strictly in line with the pixel width of the video passed in.</td>
</tr><tr>
  <td>height</td>
  <td>uint32_t</td>
  <td>Height of the video image</td>
  <td>Keep it strictly in line with the pixel height of the video passed in.</td>
</tr><tr>
  <td>timestamp</td>
  <td>long</td>
  <td>Capturing time of video frames</td>
  <td>The value can be 0, in which case the SDK will fill the field automatically, but please make sure that `sendCustomVideoData` is called at largely <strong>regular intervals</strong>.</td>
</tr><tr>
  <td>rotation</td>
  <td>int</td>
  <td>Leave it empty</td>
  <td><li/>It is left empty by default.</li><li>If you want to rotate the video, set it to 0, 90, 180, or 270. The SDK will rotate the video clockwise by the number of degrees set. For example, if 90 is passed in, an image in the portrait mode will switch to the landscape mode after rotation.</li></td>
</tr></tbody></table>

- **Texture scheme: this scheme requires knowledge of OpenGL. It delivers superior performance, especially when video resolution is high.
The texture scheme involves passing OpenGL textures to the TRTC SDK. You need to set up an OpenGL environment for the scheme to work, which makes it rather challenging. If you have no knowledge of OpenGL, we recommend that you use the sample code we provide, which is in the `customCapture` folder of the [demo](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCSimpleDemo/customcapture/src/main/java/com/tencent/custom/customcapture). The folder contains the following items:
<table><thead><tr><th>File Name</th><th>Source Code Logic</th></tr></thead>
<tbody>
<tr><td>TestSendCustomData.java</td>
<td>Demonstrates how to feed video textures to the SDK via the `sendCustomVideoData` function of `TRTCCloud`.</td>
</tr><tr>
<td>TestRenderVideoFrame.java</td>
<td>Demonstrates how to ignore the rendering logic of `TRTCClou`d and render video images with OpenGL.</td>
</tr><tr>
<td>VideoFrameReader.java</td>
<td>Demonstrates how to extract video data frame by frame from a local video file.</td>
</tr><tr>
<td>`decoder` folder</td>
<td>Decoding module</td>
</tr><tr>
<td>`opengl` folder</td>
<td>Basic functions of OpenGL, which help enhance its usability</td>
</tr><tr>
<td>`render` folder</td>
<td>Basic functions of EGL, which help enhance its usability</td></tr>
</tbody></table>

>! To avoid excessively high CPU usage, you are advised to use the texture scheme for resolutions higher than 640 x 360.


#### Sample code
The code in `TestSendCustomVideoData.java` is more complicated.
1. The code first starts a GLThread thread, which is in the waiting state until content is drawn on the `SurfaceTexture` with which it is associated.
2. The code then uses a module named `MovieVideoFrameReader` to extract video images frame by frame from a local video file and draws the frames on the `SurfaceTexture` created.
3. Each time a frame is drawn, the GLThread thread created in step 1 wakes up, which triggers the `onTextureProcess` callback. The textures obtained from the callback are fed to the SDK through `sendCustomVideoData`.

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
#### Windows
Windows supports `TRTCVideoPixelFormat_I420` only. We recommend the following settings.
<table>
<thead><tr><th>Parameter</th><th>Type</th><th>Recommended Value</th><th>Note</th>
</tr></thead><tbody>
<tr>
  <td>videoFormat</td>
  <td>TRTCVideoPixelFormat</td>
  <td>TRTCVideoPixelFormat_I420</td>
  <td>Only `TRTCVideoPixelFormat_I420` is supported</td>
</tr><tr>
  <td>bufferType</td>
  <td>TRTCVideoBufferType</td>
  <td>TRTCVideoBufferType_Buffer</td>
  <td>Only `TRTCVideoBufferType_Buffer` is supported.</td>
</tr><tr>
  <td>textureId</td>
  <td>int</td>
  <td>Leave it empty</td>
  <td>Windows does not support textures.</td>
</tr><tr>
  <td>data</td>
  <td>char *</td>
  <td>Video frame buffer</td>
  <td>A frame of I420 data</td>
</tr><tr>
  <td>timestamp</td>
  <td>uint64_t</td>
  <td>0</td>
  <td>The value can be 0, in which case the SDK will fill the field automatically, but please make sure that `sendCustomVideoData` is called at largely <strong>regular intervals</strong>.</td>
</tr><tr>
  <td>width</td>
  <td>uint64_t</td>
  <td>Width of the video image</td>
  <td>Keep it strictly in line with the pixel width of the video passed in.</td>
</tr><tr>
  <td>height</td>
  <td>uint32_t</td>
  <td>Height of the video image</td>
  <td>Keep it strictly in line with the pixel height of the video passed in.</td>
</tr><tr>
  <td>rotation</td>
  <td>TRTCVideoRotation</td>
  <td>Video rotation degree</td>
  <td><li>It is left empty by default. </li><li>If you want to rotate the video, set it to <code>TRTCVideoRotation_0</code>, <code>TRTCVideoRotation_90</code>, <code>TRTCVideoRotation_180</code>, or <code>TRTCVideoRotation_270</code>. The SDK will rotate the video clockwise by the number of degrees set. For example, if <code>TRTCVideoRotation_90</code> is passed in, an image in the portrait mode will switch to the landscape mode after rotation.</li></td>
</tr></tbody></table>

#### Sample code
The [demo](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/sdkinterface/TRTCCloudCore.cpp) file includes a function named `sendCustomVideoFrame`, which shows how to extract I420 formatted buffers from a local video file and process the data using the SDK.

```C++
// Assemble a `TRTCVideoFrame` and send it to a `trtcCloud` object.
TRTCVideoFrame frame;
frame.videoFormat = LiteAVVideoPixelFormat_I420;
frame.length = bufferSize;
frame.data = _video_buffer;
frame.width = _video_width;
frame.height = _video_height;
m_pCloud->sendCustomVideoData(TRTCVideoStreamTypeBig, & frame);      
```
:::
</dx-tabs>





## Custom Video Rendering

The TRTC SDK uses OpenGL to render video images. If you use the SDK for game development or want to integrate it into your own UI engine, you must render video images by yourself.

#### iOS & macOS
You can call `setLocalVideoRenderDelegate` and `setRemoteVideoRenderDelegate` of `TRTCCloud` to configure callbacks for the custom rendering of local and remote video images. Below are the relevant parameters.

|  Parameter   |       Type       |            Recommended Value             |                Note                |
| :---------: | :------------------: | :-----------------------------: | :------------------------------------: |
| pixelFormat | TRTCVideoPixelFormat |    TRTCVideoPixelFormat_NV12    |                   -                    |
| bufferType  | TRTCVideoBufferType | TRTCVideoBufferType_PixelBuffer | This is the video frame format supported by iOS, and it delivers the best performance. |

[](id:example_ios)
#### Sample code
If you set `pixelFormat` to `TRTCVideoPixelFormat_NV12` and `bufferType` to `TRTCVideoBufferType_PixelBuffer`, it would be easy to convert a frame of NV12 formatted PixelBuffer into a video image. The `TestRenderVideoFrame.m` file in the demo folder demonstrates how this works:

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
#### Android
You can call `setLocalVideoRenderListener` and `setRemoteVideoRenderListener` of `TRTCCloud` to configure callbacks for the custom rendering of local and remote video images. Below are the relevant parameters.

|  Parameter   |       Type       |                           Recommended Value                           |                           Note                           |
| :---------: | :------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| pixelFormat | TRTCVideoPixelFormat |                 TRTC_VIDEO_PIXEL_FORMAT_NV21                 |             The texture scheme cannot be used for custom rendering at the moment.              |
| bufferType | TRTCVideoBufferType| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY or <br> TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER | `BYTE_BUFFER` is suitable for the JNI layer, and `BYTE_ARRAY` can be used for operations at the Java layer. |

[](id:example_android)
#### Sample code

<dx-codeblock>
::: Android java
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
:::
</dx-codeblock>
#### Windows
You can call `setLocalVideoRenderCallback` and `setRemoteVideoRenderCallback` of `TRTCCloud` to configure callbacks for the custom rendering of local and remote video images. Below are the relevant parameters.

|  Parameter   |         Type          |          Recommended Value           |                           Note                           |
| :---------: | :-----------------------: | :-------------------------: | :----------------------------------------------------------: |
| pixelFormat |   TRTCVideoPixelFormat    | TRTCVideoPixelFormat_BGRA32 | Callback of video frames in the `TRTCVideoPixelFormat_I420` or `TRTCVideoPixelFormat_BGRA32` format is supported. |
| bufferType  |    TRTCVideoBufferType    | TRTCVideoBufferType_Buffer  |           Only `TRTCVideoBufferType_Buffer` is supported            |
|  callback   | ITRTCVideoRenderCallback* |  ITRTCVideoRenderCallback*  |                       Custom rendering callback                       |

[](id:example_windows)
#### Sample code
If you set `pixelFormat` to `TRTCVideoPixelFormat_BGRA32` and `bufferType` to `TRTCVideoBufferType_Buffer`, it would be easy to convert a frame of BGRA32 formatted PixelBuffer into a video image. The `TXLiveAvVideoView.cpp` file in the demo demonstrates how this works:

<dx-codeblock>
::: Window c++
void TXLiveAvVideoView::renderFitMode(HDC hDC, unsigned char * buffer, int width, int height, RECT& rcImage)
{
    Point origin;
    origin.X = m_rcItem.left, origin.Y = m_rcItem.top;
    int viewWith = m_rcItem.right - m_rcItem.left;
    int viewHeight = m_rcItem.bottom - m_rcItem.top;
    
    bool bReDrawBg = false;
     
    if (m_bmi.bmiHeader.biWidth != width || m_bmi.bmiHeader.biHeight != height)
    {
        memset(&m_bmi, 0, sizeof(m_bmi));
        m_bmi.bmiHeader.biSize = sizeof(BITMAPINFOHEADER);
        m_bmi.bmiHeader.biWidth = width;
        m_bmi.bmiHeader.biHeight = height;
        m_bmi.bmiHeader.biPlanes = 1;
        m_bmi.bmiHeader.biBitCount = 32;
        m_bmi.bmiHeader.biCompression = BI_RGB;
        bReDrawBg = true;
    }
    // Start rendering.
    ::SetStretchBltMode(hDC, COLORONCOLOR);
    if (bReDrawBg)
        ::PatBlt(hDC, 0 + origin.X, 0 + origin.Y, viewWith, viewHeight, BLACKNESS);
    ::StretchDIBits(hDC, x + origin.X, y + origin.Y, width, height, 0, 0, width, height, m_argbRenderFrame.frameBuf, &m_bmi, DIB_RGB_COLORS, SRCCOPY);
}
:::
</dx-codeblock>


### Custom Audio Capturing

You can call the `enableCustomAudioCapture` API of `TRTCCloud` to disable the TRTC SDK's default audio data capturing process, and use the `sendCustomAudioData` API to feed your own audio data to the TRTC SDK.

The `sendCustomAudioData` API includes a parameter named `TRTCAudioFrame`, which represents a 20 ms audio frame.

- The data sent to the SDK through `sendCustomAudioData` must be uncompressed raw audio data in the PCM format. ACC or other compressed formats are not supported.
- `sampleRate` and `channels` represent the audio sample rate and number of audio channels respectively, which should be kept strictly in line with the PCM data passed in.
- The recommended duration of each audio frame is 20 ms. Suppose `sampleRate` is 48,000, and `channels` is 1 (mono). The byte length of the buffer passed in each time `sendCustomAudioData` is called would be 48,000 × 0.02s × 1 × 16 bits=15,360 bits=1,920 bytes.
- `timestamp` can be 0, in which case the SDK will fill the field automatically. To ensure audio stability and avoid choppy audio, please make sure that `sendCustomAudioData` is called at largely **regular intervals**, preferably every 20 ms.

>!Using `sendCustomAudioData` may cause AEC to fail.

## Getting Raw Audio Data

The audio module is a highly complex module, and the TRTC SDK needs to strictly control the capturing and playback logic of audio devices. In some cases, to get the audio data of a remote user or that captured by the local mic, you can use the APIs of `TRTCCloud` for different platforms to integrate the following callback functions into the SDK.

<dx-alert infotype="explain" title="APIs for different platforms:">
<ul style="margin:0"><li/><b>iOS: </b>setAudioFrameDelegate
<li/><b>Android: </b>setAudioFrameListener
<li/><b>Windows: </b>setAudioFrameCallback
</ul>
</dx-alert>

| API                  | Description                                                         |
| --------------------- | ------------------------------------------------------------ |
| onCapturedAudioFrame | Get the raw audio data captured by the local mic. In the non-custom capturing mode, the SDK is responsible for capturing audio, but you may want to get the raw audio data, which can be achieved using this callback function. |
| onPlayAudioFrame | This function calls back the audio data of each remote user, which is the data before audio mixing. You can use this callback if you want to perform speech recognition on a specific channel of audio. |
| onMixedPlayAudioFrame | This function calls back mixed audio data before it is fed into the speaker for playback. |

>!
>- Do not perform time-consuming operations with any of the above callback functions. We recommend that you copy them to another thread to avoid AEC failure and choppy audio.
>- The data called back by the above callback functions should only be read and copied. Modifications may lead to unexpected outcomes.





