Flutter OpenGL 환경은 네이티브 환경과 격리되어 있으므로 Tencent Effect SDK를 Flutter에 직접 통합할 수 없습니다. 네이티브 측에서 이들 사이에 연결을 설정해야 합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/73bbc3c15e95db29a270fc4e1927a026.png" style="zoom:50%;" />

## 전반적인 구현 과정
1. Tencent Effect SDK 측에서 API 추상화 레이어를 생성하고 API를 구현합니다.
2. 애플리케이션이 시작되면 타사 게시자가 API를 사용하여 뷰티필터 인스턴스를 생성, 사용 및 종료할 수 있도록 타사 게시자에게 API를 등록합니다.
3. 타사 게시자는 뷰티필터 인스턴스를 만들고 종료하는 기능을 Flutter 측에 노출합니다.
4. Tencent Effect Flutter SDK를 사용하여 뷰티필터를 구성합니다.


### TRTC를 예로 들면
Tencent Effect 측에서 정의한 API:
```java
public interface ITXCustomBeautyProcesserFactory {

    /**
     * 뷰티필터 인스턴스 생성
     * @return
     */
    ITXCustomBeautyProcesser createCustomBeautyProcesser();

    /**
     * 뷰티필터 인스턴스 종료(이 API는 OpenGL 스레드에서 호출되어야 함)
     */
    void destroyCustomBeautyProcesser();
}
public interface ITXCustomBeautyProcesser {

   //비디오 프레임에 지원되는 픽셀 형식을 가져옵니다. Tencent Effect는 OpenGL 2D 텍스처를 지원합니다.
    TXCustomBeautyPixelFormat getSupportedPixelFormat();
    //비디오 프레임에 지원되는 컨테이너 형식을 가져옵니다. Tencent Effect는 최고의 성능을 제공하고 비디오 품질에 미치는 영향이 가장 적은 V2TXLiveBufferTypeTexture를 지원합니다.
    TXCustomBeautyBufferType getSupportedBufferType();
   //OpenGL 스레드에서 이 API를 호출합니다(srcFrame은 RGBA 텍스처와 width 및 height를 포함해야 함). 처리 후 텍스처 객체는 dstFrame의 texture.textureId에 포함됩니다.
    void onProcessVideoFrame(TXCustomBeautyVideoFrame srcFrame, TXCustomBeautyVideoFrame dstFrame);
}
```

1. TRTC는 등록 방법을 제공합니다. 애플리케이션이 실행되면 ITXCustomBeautyProcesserFactory의 구현 클래스인 'com.tencent.effect.tencent_effect_flutter.XmagicProcesserFactory'를 TRTC(네이티브 측)에 등록합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9b21d439c06afcf3b01ef969931dd992.png)
2. `Flutter` 레이어에서 사용자 지정 효과를 활성화 또는 비활성화하는 데 사용되는 `Future<V2TXLiveCode> enableCustomVideoProcess(bool enable)`를 제공합니다.
3. TRTC 네이티브 측에서 효과를 활성화 또는 비활성화합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5a8b502b3700bf853d13d9112536c4c8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/a58a0f003061b067a503138b92571894.png)



## 부록
**Tencent Effect에서 제공하는 추상화 레이어 의존성**
```groovy
///
implementation 'com.tencent.liteav:custom-video-processor:latest.release'
```
