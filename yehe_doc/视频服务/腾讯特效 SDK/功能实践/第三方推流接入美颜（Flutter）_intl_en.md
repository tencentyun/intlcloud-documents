Because the Flutter OpenGL environment is isolated from a native environment, you cannot integrate the Tencent Effect SDK directly into Flutter. You need to establish connections between them at the native side.
<img src="https://qcloudimg.tencent-cloud.cn/raw/73bbc3c15e95db29a270fc4e1927a026.png" style="zoom:50%;" />

## How It Works
1. Create an API abstraction layer and implement the API at the Tencent Effect SDK side.
2. When the application is launched, register the API with the third-party publisher so that the third-party publisher can use it to create, use, and terminate an effect instance.
3. The third-party publisher exposes the capabilities of creating and terminating effect instances to the Flutter side.
4. Use the Tencent Effect Flutter SDK to configure effects.


### Example (TRTC)
API defined at the Tencent Effect side
```java
public interface ITXCustomBeautyProcesserFactory {

    /**
     * Create an instance
     * @return
     */
    ITXCustomBeautyProcesser createCustomBeautyProcesser();

    /**
     * Terminate an instance (this API must be called in the OpenGL thread)
     */
    void destroyCustomBeautyProcesser();
}
public interface ITXCustomBeautyProcesser {

   // Get the pixel formats supported for video frames. Tencent Effect supports OpenGL 2D textures.
    TXCustomBeautyPixelFormat getSupportedPixelFormat();
    // Get the container formats supported for video frames. Tencent Effect supports V2TXLiveBufferTypeTexture, which delivers the best performance and has the smallest impact on video quality.
    TXCustomBeautyBufferType getSupportedBufferType();
   // Call this API in the OpenGL thread (`srcFrame` must include RGBA textures and the width and height). After processing, the texture object will be included in `texture.textureId` of `dstFrame`.
    void onProcessVideoFrame(TXCustomBeautyVideoFrame srcFrame, TXCustomBeautyVideoFrame dstFrame);
}
```

1. TRTC offers a registration method. When the application is launched, register `com.tencent.effect.tencent_effect_flutter.XmagicProcesserFactory`, the implementation class of `ITXCustomBeautyProcesserFactory` with TRTC (at the native side).
![](https://qcloudimg.tencent-cloud.cn/raw/9b21d439c06afcf3b01ef969931dd992.png)
2. At the `Flutter` layer, provide `Future<V2TXLiveCode> enableCustomVideoProcess(bool enable)`, which is used to enable or disable custom effects.
3. Enable or disable effects at the TRTC native side.
![](https://qcloudimg.tencent-cloud.cn/raw/5a8b502b3700bf853d13d9112536c4c8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/a58a0f003061b067a503138b92571894.png)



## Appendix
**The abstraction layer dependency provided by Tencent Effect**
```groovy
///
implementation 'com.tencent.liteav:custom-video-processor:latest.release'
```
