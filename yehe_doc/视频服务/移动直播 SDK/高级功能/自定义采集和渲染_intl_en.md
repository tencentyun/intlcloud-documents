## Sample Code
Regarding frequently asked questions among developers, Tencent Cloud offers an easy-to-understand API example project, which you can use to quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |


## Customizing Video to Publish

### iOS

<dx-tabs>
::: Method 1: modifying \sOpenGL\s textures
If you need to process video by yourself (for example, add subtitles) but want to leave the rest of the process to LiteAVSDK, follow the steps below.
1. Call [enableCustomVideoProcess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a36a27d1112103ca70954c72a5d9109ce) of `V2TXLivePusher` to enable custom video processing, so that you will receive the callback of video data.
2. There are two cases for image processing.
	-**The beauty filter component generates new textures.**
	If the beauty filter component you use generates a new texture frame (for the processed image) during image processing, please set `dstFrame.textureId` to a new texture ID in the callback API.
```objectiveC
   - (void) onProcessVideoFrame:(V2TXLiveVideoFrame _Nonnull)srcFrame dstFrame:(V2TXLiveVideoFrame _Nonnull)dstFrame
   {
       GLuint dstTextureId = renderItemWithTexture(srcFrame.textureId, srcFrame.width, srcFrame.height);
       dstFrame.textureId = dstTextureId;
   }
```
	- **The beauty filter component does not generate new textures.**
If the third-party beauty filter component you use does not generate new textures and you need to manually set an input texture and an output texture for the component, consider the following scheme:
```objectiveC
   - (void) onProcessVideoFrame:(V2TXLiveVideoFrame _Nonnull)srcFrame dstFrame:(V2TXLiveVideoFrame _Nonnull)dstFrame
   {
       thirdparty_process(srcFrame.textureId, srcFrame.width, srcFrame.height, dstFrame.textureId);
   }
```
3. You need some basic knowledge of OpenGL to deal with texture data and should refrain from high volume computing. This is because `onProcessVideoFrame` is called at the same frequency as the frame rate, and sophisticated processing may cause GPU overheating.
:::
::: Method 2: capturing data by yourself
If you want to use the SDK for encoding and publishing only and control other procedures such as video capturing and pre-processing (retouching, beauty filters, etc.) with your own code (which may be the case if, for example, you have integrated SenseTime or other products into your project), follow the steps below.

1. Call the [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a35e33064526da7f360c786a63d4e33e5) API of `V2TXLivePusher` to enable custom video capturing.
The SDK will stop capturing video data and will only execute publishing-related tasks such as encoding, QoS control, and delivery.
2. Use the [sendCustomVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a70770d15cc87cf91c174df97cf45a683) API of `V2TXLivePusher` to feed video data into the SDK.
<dx-codeblock>
::: objectiveC objectiveC
/**
 * @brief In the custom video capturing mode, send captured video data to the SDK<br/>
 *        In the custom video capturing mode, the SDK stops capturing video data and only encodes and sends data
 *        You can package the SampleBuffer captured into `V2TXLiveVideoFrame` and use this API to send data regularly
 *
 * @note You must call [enableCustomVideoCapture](@ref V2TXLivePusher#enableCustomVideoCapture:) to enable custom video capturing before [startPush](@ref V2TXLivePusher#startPush:)
 *
 * @param videoFrame Video frames {@link V2TXLiveVideoFrame} sent to the SDK
 *
 * @return Return code for {@link V2TXLiveCode}
 *         - `V2TXLIVE_OK`: successful
 *         - `V2TXLIVE_ERROR_INVALID_PARAMETER`: Operation failed because the video data is invalid.
 *         - `V2TXLIVE_ERROR_REFUSED`: You must call `enableCustomVideoCapture` to enable custom video capturing first.
 */
- (V2TXLiveCode)sendCustomVideoFrame:(V2TXLiveVideoFrame *)videoFrame;
:::
</dx-codeblock>
:::
</dx-tabs>

### Android

<dx-tabs>
::: Method 1: modifying \sOpenGL\s textures
If you need to process video by yourself (for example, add subtitles) but want to leave the rest of the process to LiteAVSDK, follow the steps below.
1. Call [enableCustomVideoProcess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ab3d49118931e09d1d4954674ff8a8102) of `V2TXLivePusher` to enable custom video processing, so that you will receive the callback of video data.
2. There are two cases for image processing.
	-  **The beauty filter component generates new textures.**
	If the beauty filter component you use generates a new texture frame (for the processed image) during image processing, please set `dstFrame.textureId` to a new texture ID in the callback API.
```java 
private class MyPusherObserver extends V2TXLivePusherObserver {
    @Override
    public void onGLContextCreated() {
        mFURenderer.onSurfaceCreated();
        mFURenderer.setUseTexAsync(true);
    }

    @Override
    public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
        dstFrame.texture.textureId = mFURenderer.onDrawFrameSingleInput(
                srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
        return 0;
    }

    @Override
    public void onGLContextDestroyed() {
        mFURenderer.onSurfaceDestroyed();
    }
}
```
	-  **The beauty filter component does not generate new textures.**
If the third-party beauty filter component you use does not generate new textures and you need to manually set an input texture and an output texture for the component, consider the following scheme:
```java 
    @Override
    public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
        thirdparty_process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height, dstFrame.texture.textureId);
        return 0;
    }
```
3. You need some basic knowledge of OpenGL to deal with texture data and should refrain from high volume computing. This is because `onProcessVideoFrame` is called at the same frequency as the frame rate, and sophisticated processing may cause GPU overheating.
:::
::: Method 2: capturing data by yourself
If you want to use the SDK for encoding and publishing only and control other procedures such as video capturing and pre-processing (retouching, beauty filters, etc.) with your own code (which may be the case if, for example, you have integrated SenseTime or other products into your project), follow the steps below.

1. Call the [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a9d945c58c4e0ff24e55aacef1ef3090f) API of `V2TXLivePusher` to enable custom video capturing.
The SDK will stop capturing video data and will only execute publishing-related tasks such as encoding, QoS control, and delivery.
2. Use the [sendCustomVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a3802124d90bf00434245d2956dad1fe4) API of `V2TXLivePusher` to feed video data into the SDK.
<dx-codeblock>
::: java java
/**
 * @brief In the custom video capturing mode, send captured video data to the SDK<br/>
 *        In the custom video capturing mode, the SDK stops capturing video data and only encodes and sends data
 *
 * @note  You need to call {@link V2TXLivePusher#enableCustomVideoCapture(boolean)} to enable custom video capturing before {@link V2TXLivePusher#startPush(String)}
 *
 * @param videoFrame Video frames {@link V2TXLiveVideoFrame} sent to the SDK
 *
 * @return Return code for {@link V2TXLiveCode}
 *         - `V2TXLIVE_OK`: successful
 *         - `V2TXLIVE_ERROR_INVALID_PARAMETER`: Operation failed because the video data is invalid.
 *         - `V2TXLIVE_ERROR_REFUSED`: You must call `enableCustomVideoCapture` to enable custom video capturing first.
 */
 public abstract int sendCustomVideoFrame(V2TXLiveVideoFrame videoFrame);
:::
</dx-codeblock>
 :::
 </dx-tabs>

## Customizing Video for Playback

### iOS
1. Set [V2TXLivePlayerObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html) to listen for events of [V2TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html).
<dx-codeblock>
::: objectiveC objectiveC
@interface V2TXLivePlayer : NSObject
/**
 * @brief Set callbacks for the player<br/>
 *        After setting callbacks, you can listen for events of V2TXLivePlayer,
 *       including the player status, playback volume, first audio/video frame, statistics, and warning and error messages.
 *
 * @param observer Target object for the player’s callbacks. For more information, see {@link V2TXLivePlayerObserver}
 */
- (void)setObserver:(id<V2TXLivePlayerObserver>)observer;
:::
</dx-codeblock>
2. Get the player’s video data from the [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a1ee10f163275f3b9316ce387573fcbe1) callback.
<dx-codeblock>
::: objectiveC objectiveC
/**
 * @brief Video frame information
 *        V2TXLiveVideoFrame is the raw data that describes a video frame before encoding or after decoding
 * @note It is used during custom video capturing to package the video frames to be sent, and during custom video rendering to get the packaged video frames
 */
 @interface V2TXLiveVideoFrame : NSObject

///**Field meaning:** video pixel format
///**Recommended value:** V2TXLivePixelFormatNV12
@property(nonatomic, assign) V2TXLivePixelFormat pixelFormat;

///**Field meaning:** video data container format
///**Recommended value:** V2TXLiveBufferTypePixelBuffer
@property(nonatomic, assign) V2TXLiveBufferType bufferType;

///**Field meaning:** video data when bufferType is V2TXLiveBufferTypeNSData
@property(nonatomic, strong, nullable) NSData *data;

///**Field meaning:** video data when bufferType is V2TXLiveBufferTypePixelBuffer
@property(nonatomic, assign, nullable) CVPixelBufferRef pixelBuffer;

///**Field meaning:** video width
@property(nonatomic, assign) NSUInteger width;

///**Field meaning:** video height
@property(nonatomic, assign) NSUInteger height;

///**Field meaning:** clockwise rotation of video
@property(nonatomic, assign) V2TXLiveRotation rotation;

/// **Field description:** video texture ID
@property (nonatomic, assign) GLuint textureId;

@end


@protocol V2TXLivePlayerObserver <NSObject>
@optional
/**
 * @brief Custom video rendering callback
 *
 * @note  You will receive this callback after calling [enableCustomRendering](@ref V2TXLivePlayer#enableCustomRendering:pixelFormat:bufferType:) to enable custom video rendering
 *
 * @param videoFrame Video frame data {@link V2TXLiveVideoFrame}
 */
- (void)onRenderVideoFrame:(id<V2TXLivePlayer>)player
                     frame:(V2TXLiveVideoFrame *)videoFrame
                 @end
                 :::
                 </dx-codeblock>

### Android
1. Set [V2TXLivePlayerObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html) to listen for callbacks of [V2TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html).
<dx-codeblock>
::: java java
public abstract void setObserver(V2TXLivePlayerObserver observer)
:::
</dx-codeblock>
2. Get the player’s video data from the [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a346a3206ad4d0f38385844c1456a012f) callback.
<dx-codeblock>
::: java java
public final static class V2TXLiveVideoFrame
{
    /// Video pixel format
    public V2TXLivePixelFormat pixelFormat = V2TXLivePixelFormat.V2TXLivePixelFormatUnknown;
    /// Video data container format
    public V2TXLiveBufferType bufferType   = V2TXLiveBufferType.V2TXLiveBufferTypeUnknown;
    /// Video texture pack
    public V2TXLiveTexture texture;
    /// Video data
    public byte[]       data;
    /// Video data
    public ByteBuffer   buffer;
    /// Video width
    public int          width;
    /// Video height
    public int          height;
    /// Clockwise rotation of video
    public int          rotation;
}

public abstract class V2TXLivePlayerObserver {
    /**
     * Callback for custom video rendering
     *
     * @param player The player object sending this callback
     * @param videoFrame Video frame data {@link V2TXLiveVideoFrame}
     */
    void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame);
}
:::
</dx-codeblock>
