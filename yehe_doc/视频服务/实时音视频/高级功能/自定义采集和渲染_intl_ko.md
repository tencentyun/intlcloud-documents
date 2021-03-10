## 콘텐츠 소개
- **사용자 정의 비디오 수집**
귀하가 자체개발(또는 3rd party에게 구매)한 뷰티 필터 및 특수 효과 프로세스 모듈은 자체적으로 카메라가 촬영한 화면을 수집 및 처리해야 합니다. TRTCCloud의 `enableCustomVideoCapture` 인터페이스를 통해 TRTC SDK의 카메라 수집 및 이미지 처리 로직을 비활성화할 수 있으며, 비활성화 후 `sendCustomVideoData` 인터페이스를 이용해 TRTC SDK에 귀하의 비디오 데이터를 넣을 수 있습니다.

- **사용자 정의 비디오 렌더링**
TRTC SDK는 OpenGL을 사용해 비디오 화면을 렌더링합니다. 게임 개발에 사용하거나 귀하의 인터페이스 엔진에 TRTC SDK를 삽입해야 하는 경우 자체적으로 비디오 화면을 렌더링해야 합니다.

- **사용자 정의 오디오 수집**
특수 하드웨어 디바이스에서 TRTC SDK를 사용할 경우, 외부 오디오 수집 디바이스가 필요하고 자체적으로 오디오 데이터를 수집한다면 TRTCCloud의 `enableCustomAudioCapture` 인터페이스를 통해 TRTC SDK에 기본 설정된 오디오 수집 프로세스를 비활성화할 수 있습니다. 비활성화 후 `sendCustomAudioData` 인터페이스를 통해 TRTC SDK에 귀하의 오디오 데이터를 넣을 수 있습니다.
>!사용자 정의 오디오 수집을 활성화하면 반향 제거(AEC) 기능이 적용되지 않을 수 있습니다.

- **오디오 원본 데이터 획득**
오디오 모듈은 매우 복잡도가 높은 모듈로, SDK에서는 오디오 디바이스의 수집 및 재생 로직을 엄격하게 제어합니다. 어떤 시나리오에서 원격 사용자의 오디오 데이터를 획득해야 하거나 로컬 마이크에서 수집한 오디오 데이터를 획득해야 하는 경우 TRTC SDK에서 제공하는 콜백 인터페이스로 구현할 수 있습니다.

## 지원 플랫폼

| iOS | Android | Mac OS | Windows | WeChat 미니프로그램 | Chrome 브라우저|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|   &#10003;  |  &#10003;    | &#10003;   |  &#10003;  |   ×  |  ×   |

## 사용자 정의 비디오 수집

TRTCCloud의 `enableCustomVideoCapture` 인터페이스를 통해 TRTC SDK의 카메라 수집 및 이미지 처리 로직을 비활성화할 수 있으며, 비활성화 후 `sendCustomVideoData` 인터페이스를 이용해 TRTC SDK에 귀하의 비디오 데이터를 넣을 수 있습니다.

`sendCustomVideoData` 인터페이스에는 `TRTCVideoFrame`이라는 매개변수가 있으며, 해당 매개변수는 비디오 화면 프레임을 의미합니다. TRTC SDK의 비디오 데이터 입력에 대해 플랫폼별로 서로 다른 포맷 요구가 존재하며, 자세한 요구 사항은 다음과 같습니다.

### iOS 플랫폼

TRTC SDK는 NV12, i420의 두 가지 iOS 버전의 YUV 데이터 포맷을 지원합니다. iOS 플랫폼에서 비교적 성능이 높은 이미지 전달 방식은 CVPixelBufferRef 방식이며, 매개변수 형식은 다음과 같이 권장합니다.

| 매개변수 이름  | 매개변수 유형 |  권장 설정값 | 비고 설명|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 |  iOS 플랫폼 카메라에서 수집하는 비디오 원본 포맷은 NV12입니다. |
| bufferType | TRTCVideoBufferType| PixelBuffer | iOS에서 기본적으로 지원하는 비디오 프레임 포맷으로, 성능이 가장 좋습니다.|
| pixelBuffer| CVPixelBufferRef | TRTCVideoBufferType이 PixelBuffer인 경우 반드시 작성해야 합니다. | iPhone 카메라에서 수집하는 데이터는 NV12 포맷의 PixelBuffer입니다.|
| data| NSData\* | TRTCVideoBufferType이 NSData인 경우 반드시 작성해야 합니다. | 성능이 PixelBuffer 대비 떨어집니다. |
| timestamp| uint64_t | 0 | 0으로 설정할 수 있으며, 이 경우 SDK에서 자동으로 timestamp 필드를 작성합니다. 단, sendCustomVideoData의 호출 간격을 **균일하게** 제어하십시오.|
| width    | uint64_t| 비디오 화면 너비 | 전달 화면의 픽셀 폭을 정확하게 작성하십시오. |
| height   | uint32_t| 비디오 화면 높이 | 전달 화면의 픽셀 높이를 정확하게 작성하십시오. |
| rotation | TRTCVideoRotation| 입력하지 않음 | 해당 필드는 사용자 정의 렌더링에 사용되며, 여기에서는 설정하지 않습니다. |

**예시 코드**: [Demo](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo/CustomCapture/testCustomVideo) 폴더에서 `TestSendCustomVideoData.m` 파일은 로컬 비디오 파일에서 NV12 포맷의 PixelBuffer를 읽는 방법을 정의하고 있으며 SDK를 통해 후속 처리합니다.

```objectiveC
//TRTCVideoFrame을 어셈블리하고, 이를 trtcCloud 객체로 전달
TRTCVideoFrame* videoFrame = [TRTCVideoFrame new];
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
        
[trtcCloud sendCustomVideoData:videoFrame];      
```

### Android 플랫폼

Android 플랫폼에서는 두 가지 방식이 있습니다.

**1. buffer 방식**: 연결이 비교적 간단하지만 성능이 비교적 떨어져 해상도가 비교적 높은 시나리오에는 적합하지 않습니다.

buffer 방식은 직접 TRTC SDK에 byte[] 형식의 배열을 넣어야 하며, i420 및 NV21 두 가지 YUV 포맷을 지원합니다.

| 매개변수 이름  | 매개변수 유형 |  권장 설정값 | 비고 설명|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| int | TRTC_VIDEO_PIXEL_FORMAT_I420 또는<br> TRTC_VIDEO_PIXEL_FORMAT_NV21  | i420 및 NV21는 두 가지 서로 다른 YUV 데이터 포맷입니다. |
| bufferType | int | TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY | data 방식으로 YUV 데이터를 전달하라고 지정합니다.|
| texture  | TRTCTexture | buffer 방식은 입력하지 않음| i420 또는 NV21 포맷을 선택하는 경우 매개변수를 입력하지 않습니다.|
| data| byte[] | YUV 포맷의 데이터 buffer | 내부 패키지는 Java 유형의 메모리이며, Java 레이어에서 사용 시 적합합니다.|
| buffer| ByteBuffer | buffer 방식은 입력하지 않음 | 내부 패키지는 C/C++ 유형의 메모리이며, JNI 레이어에서 사용 시 적합합니다. |
| width    | uint64_t| 비디오 화면 너비 | 전달 화면의 픽셀 폭을 정확하게 작성하십시오. |
| height   | uint32_t| 비디오 화면 높이 | 전달 화면의 픽셀 높이를 정확하게 작성하십시오. |
| timestamp| long | 비디오 프레임 수집 시간 | 0으로 설정할 수 있으며, 이 경우 SDK에서 자동으로 timestamp 필드를 작성합니다. 단, sendCustomVideoData의 호출 간격을 **균일하게** 제어하십시오.|
| rotation | int| 입력하지 않음 | sendCustomVideoData 시 해당 필드를 입력할 필요 없습니다. |

**2. texture 방식**: 연결 시 일정한 OpenGL 기초가 필요하지만 성능이 비교적 좋으며, 특히 화면 해상도가 비교적 높은 경우 성능이 뛰어납니다.

texture는 TRTC SDK에 OpenGL 텍스쳐를 전달해야 하며, 해당 방식이 정상적으로 작동될 수 있도록 사전에 OpenGL 환경을 설정해야 합니다. 이에 따라 해당 방식의 연결은 난이도가 높습니다. OpenGL을 학습한 경험이 없는 경우, Tencent Cloud에서 제공하는 예시 코드 사용을 권장하며, 이는 [Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCSimpleDemo/customcapture/src/main/java/com/tencent/custom/customcapture)의 `customCapture` 폴더에 있고 다음과 같은 파일이 포함되어 있습니다.

| 파일 이름 | 소스 코드 로직 |
|---------|---------|
|TestSendCustomData.java   |     TRTCloud의 sendCustomVideoData 함수를 통해 SDK에 비디오 텍스쳐를 전달하는 방법의 예시입니다.|
|TestRenderVideoFrame.java  |      TRTCloud의 원본 렌더링 로직을 건너뛰고 직접 OpenGL을 이용해 화면을 렌더링하는 방법의 예시입니다.|
|VideoFrameReader.java    |    로컬에 있는 비디오 파일에서 한 프레임 한 프레임의 화면을 읽어옵니다.|
|decoder 폴더|  디코딩 모듈|
|opengl 폴더   |     OpenGL의 기본 함수를 캡슐화하여 더 쉽게 사용할 수 있습니다.|
|render 폴더    |    Egl의 기본 함수를 캡슐화하여 더 쉽게 사용할 수 있습니다.|

>! CPU 사용율이 너무 높아지는 것을 방지하기 위해 640 x 360 이상의 해상도에서는 texture 방식 사용을 권장하지 않습니다.


**예시 코드**: `TestSendCustomVideoData.java`의 코드 원리는 비교적 복잡합니다.
1. 코드에서는 먼저 GLThread 스레드를 실행합니다. 해당 스레드는 연결된 "화면 텍스쳐(SurfaceTexture)"에 콘텐츠가 작성될 때까지 대부분의 시간은 모두 대기 상태입니다.
2. 다음으로 MovieVideoFrameReader라는 모듈을 사용해 로컬 비디오 파일에서 한 프레임씩 화면을 읽어오고 해당 모든 화면 프레임을 다음에 생성하는 "화면 텍스쳐"에 작성합니다.
3. 작성된 모든 프레임은 1단계에서 생성한 GLThread 스레드를 깨워 다음의 `onTextureProcess` 콜백이 존재하게 됩니다. 해당 콜백 함수 중, 획득한 texture를 sendCustomVideoData 함수를 통해 SDK에 전달합니다.

```java
public int onTextureProcess(int textureId, EGLContext eglContext) {
        if (!mIsSending) return textureId;

        //비디오 프레임을 텍스쳐 방식을 통해 SDK에 삽입
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


## 사용자 정의 비디오 렌더링

TRTC SDK는 OpenGL을 사용해 비디오 화면을 렌더링합니다. 게임 개발에 사용하거나 귀하의 인터페이스 엔진에 TRTC SDK를 삽입해야 하는 경우 자체적으로 비디오 화면을 렌더링해야 합니다.

### iOS 플랫폼(Mac 포함)

TRTCCloud의 `setLocalVideoRenderDelegate`와 `setRemoteVideoRenderDelegate`를 통해 로컬 및 원격 화면의 사용자 정의 렌더링 콜백을 설정할 수 있으며, 관련 매개변수는 다음과 같습니다.

| 매개변수 이름  | 매개변수 유형 |  권장 설정값 | 비고 설명|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTCVideoPixelFormat_NV12 |  - |
| bufferType | TRTCVideoBufferType| TRTCVideoBufferType_PixelBuffer | iOS에서 기본적으로 지원하는 비디오 프레임 포맷으로, 성능이 가장 좋습니다.|

**예시 코드**: pixelFormat으로 TRTCVideoPixelFormat_NV12을 선택하고 bufferType으로 TRTCVideoBufferType_PixelBuffer를 선택하면 전체적으로 편리하게 NV12 포맷의 PixelBuffer를 비디오 화면으로 전환할 수 있습니다. Demo 폴더에 `TestRenderVideoFrame.m`이라는 파일이 있으며, 해당 파일에서는 다음 예시 코드를 통한 사용 방법을 소개합니다.
```objectiveC
- (void)onRenderVideoFrame:(TRTCVideoFrame *)frame 
                                userId:(NSString *)userId 
						        streamType:(TRTCVideoStreamType)streamType
{
    //userId가 nil이면 로컬 화면, 그렇지 않을 경우 원격 화면
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

### Android 플랫폼
TRTCCloud의 `setLocalVideoRenderListener`와 `setRemoteVideoRenderListener`를 통해 로컬 및 원격 화면의 사용자 정의 렌더링 콜백을 설정할 수 있으며, 관련 매개변수는 다음과 같습니다.

| 매개변수 이름  | 매개변수 유형 |  권장 설정값 | 비고 설명|
|:-------:|:-------:|:-------:| :-------: |
| pixelFormat| TRTCVideoPixelFormat | TRTC_VIDEO_PIXEL_FORMAT_NV21 | 사용자 정의 렌더링은 현재 texture 방식을 지원하지 않습니다.  |
| bufferType | TRTCVideoBufferType| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY 또는<br> TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER  | BYTE_BUFFER는 jni 레이어에서 사용 시 적합하며, BYTE_ARRAY는 Java 레이어 직접 작업 시 사용할 수 있습니다.|


## 사용자 정의 오디오 수집

TRTCCloud의 enableCustomAudioCapture 인터페이스를 통해 TRTC SDK에 기본 설정된 오디오 수집 프로세스를 비활성화할 수 있습니다. 비활성화 후 sendCustomAudioData 인터페이스를 통해 TRTC SDK에 귀하의 오디오 데이터를 넣을 수 있습니다.

`sendCustomAudioData` 인터페이스에서 `TRTCAudioFrame` 매개변수는 프레임 길이 20ms의 오디오 데이터를 의미합니다.
- `sendCustomAudioData`를 통해 SDK에 전송하는 데이터는 PCM 포맷의 압축하지 않은 오디오 원시 데이터여야 하며, ACC 또는 기타 압축 포맷은 불가능합니다.
- sampleRate와 channels 해상도는 오디오 샘플링 레이트와 사운드 채널 수를 의미하며, 전송하는 PCM 데이터와 정확하게 일치해야 합니다.
- 오디오 데이터 프레임별 시간은 20ms를 권장합니다. sampleRate가 48000이고 채널 수가 1개(싱글 사운드 채널)인 경우 sendCustomAudioData 호출 시마다 전송하는 buffer 길이는 48000 * 0.02s * 1 * 16bit = 15360bit = 1920바이트가 됩니다.
- timestamp은 0으로 설정할 수 있으며, timestamp을 0으로 설정하는 경우 SDK에서 자동으로 오디오 타임스탬프를 삽입합니다. 따라서 오디오 타임스탬프의 안정성을 위해 `sendCustomAudioData`를 **균일하게** 호출하고, 1회당 20ms의 빈도수를 유지하십시오. 그렇지 않을 경우 오디오가 끊기는 현상이 발생할 수 있습니다.

>! `sendCustomAudioData`를 사용할 경우 반향 제거(AEC) 기능이 적용되지 않을 수 있습니다.

## 오디오 원본 데이터 획득

오디오 모듈은 매우 복잡도가 높은 모듈로, SDK에서는 오디오 디바이스의 수집 및 재생 로직을 엄격하게 제어합니다. 어떤 시나리오에서 원격 사용자의 오디오 데이터를 획득해야 하거나 로컬 마이크에서 수집한 오디오 데이터를 획득해야 하는 경우 TRTCCloud의 플랫폼별 인터페이스를 통해 SDK에 콜백 함수 세 개를 통합할 수 있습니다.
>?TRTCCloud의 플랫폼별 인터페이스:
>iOS: `setAudioFrameDelegate`, Android: `setAudioFrameListener`, Windows: `setAudioFrameCallback`

- **onCapturedAudioFrame**
로컬 마이크에서 수집한 오디오 원본 데이터를 획득합니다. 사용자 정의 수집 모드를 제외하고는 SDK에서 마이크 오디오 수집 작업을 진행합니다. SDK에서 수집한 오디오 원본 데이터를 획득해야 하는 경우 해당 콜백 함수를 통해 획득할 수 있습니다.

- **onPlayAudioFrame**
해당 함수는 모든 원격 사용자의 오디오 데이터를 콜백하며, 이는 오디오 혼합 전의 데이터입니다. 특정 오디오 채널에 음성인식을 진행하는 경우 해당 콜백을 사용할 수 있습니다.

- **onMixedPlayAudioFrame**
각 오디오 데이터를 혼합한 후 스피커에 재생 전송 전 해당 함수를 통해 콜백합니다.

>!
>1. 위의 콜백 함수에는 시간이 소모되는 어떠한 작업도 해서는 안되며, 직접 복사하여 다른 스레드를 통해 처리하는 것을 권장합니다. 그렇지 않을 경우 오디오가 끊기거나 반향 제거(AEC) 기능이 적용되지 않을 수 있습니다.
>2. 위의 콜백 함수에서 콜백하는 데이터는 모두 읽기 및 복사가 가능하며 수정은 불가능합니다. 그렇지 않을 경우 각종 알 수 없는 결과가 나타날 수 있습니다.





