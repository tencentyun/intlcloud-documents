본문에서는 사용자 정의 오디오 캡처 및 렌더링을 구현하기 위해 TRTC SDK를 사용하는 방법을 설명합니다.

## 사용자 정의 오디오 캡처

TRTC SDK의 사용자 정의 오디오 캡처 기능은 기능 활성화와 SDK에 오디오 프레임 전송의 두 단계로 사용할 수 있습니다. 특정 API에 대한 자세한 안내는 아래를 참고하십시오. 또한 다양한 플랫폼에 대한 API-Example을 제공합니다.

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/main/TRTC-API-Example-OC/Advanced/LocalVideoShare/LocalVideoShareViewController.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C++/TRTC-API-Example-Qt/src/TestCustomCapture/test_custom_capture.cpp) 

### 사용자 정의 오디오 캡처 활성화

TRTC SDK의 사용자 정의 오디오 캡처 기능을 활성화하려면 TRTCCloud의 `enableCustomAudioCapture` API를 호출해야 합니다. 아래는 샘플 코드입니다.

<dx-codeblock>
::: Android  Java
TRTCCloud mTRTCCloud = TRTCCloud.shareInstance();
mTRTCCloud.enableCustomAudioCapture(true);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
[self.trtcCloud enableCustomAudioCapture:YES];
:::
::: Windows  C++
liteav::ITRTCCloud* trtc_cloud = liteav::ITRTCCloud::getTRTCShareInstance();
trtc_cloud->enableCustomAudioCapture(true);
:::
</dx-codeblock>


### 사용자 정의 오디오 프레임 전송

TRTCCloud의 'sendCustomAudioData' API를 사용하여 자신의 오디오 데이터로 TRTC SDK를 채울 수 있습니다. 아래는 샘플 코드입니다.

<dx-codeblock>
::: Android  Java
TRTCCloudDef.TRTCAudioFrame trtcAudioFrame = new TRTCCloudDef.TRTCAudioFrame();
trtcAudioFrame.data = data;
trtcAudioFrame.sampleRate = sampleRate;
trtcAudioFrame.channel = channel;
trtcAudioFrame.timestamp = timestamp;
mTRTCCloud.sendCustomAudioData(trtcAudioFrame);
:::
::: iOS&Mac  ObjC
TRTCAudioFrame *audioFrame = [[TRTCAudioFrame alloc] init];
audioFrame.channels = audioChannels;
audioFrame.sampleRate = audioSampleRate;
audioFrame.data = pcmData;
    
[self.trtcCloud sendCustomAudioData:audioFrame];
:::
::: Windows  C++
liteav::TRTCAudioFrame frame;
frame.audioFormat = liteav::TRTCAudioFrameFormatPCM;
frame.length = buffer_size;
frame.data = array.data();
frame.sampleRate = 48000;
frame.channel = 1;
getTRTCShareInstance()->sendCustomAudioData(&frame);
:::
</dx-codeblock>

>! `sendCustomAudioData`를 사용할 경우 반향 제거(AEC) 기능이 적용되지 않을 수 있습니다.




## 오디오 원본 데이터 획득

오디오 모듈은 매우 복잡한 모듈이며 TRTC SDK는 오디오 장치의 캡처 및 재생 로직을 엄격하게 제어해야 합니다. 경우에 따라 원격 사용자의 오디오 데이터 또는 로컬 마이크에 의해 캡처된 오디오 데이터를 가져오기 위해 다른 플랫폼용 TRTCCloud의 API를 사용할 수 있습니다. 또한 다음과 같은 플랫폼에 대한 API-Example도 제공합니다.

- [Android](https://github.com/LiteAVSDK/TRTC_Android/blob/main/TRTC-API-Example/Advanced/LocalVideoShare/src/main/java/com/tencent/trtc/mediashare/LocalVideoShareActivity.java)：
- [iOS](https://github.com/LiteAVSDK/TRTC_iOS/blob/main/TRTC-API-Example-OC/Advanced/LocalVideoShare/LocalVideoShareViewController.m)
- [Windows](https://github.com/LiteAVSDK/TRTC_Windows) 


### 오디오 콜백 설정
<dx-codeblock>
::: Android  Java
mTRTCCloud.setAudioFrameListener(new TRTCCloudListener.TRTCAudioFrameListener() {
        @Override
        public void onCapturedRawAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {

        }
    
        @Override
        public void onLocalProcessedAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {
    
        }
    
        @Override
        public void onRemoteUserAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame, String s) {
    
        }
    
        @Override
        public void onMixedPlayAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {
    
        }
    
        @Override
        public void onMixedAllAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {
            // 자세한 내용은 TRTC-API-Example의 사용자 정의 렌더링 도구 클래스 com.tencent.trtc.mediashare.helper.CustomFrameRender 참고  
        }
    }); 
:::
::: iOS&Mac ObjC
 [self.trtcCloud setAudioFrameDelegate:self];
 // MARK: - TRTCAudioFrameDelegate
 - (void)onCapturedRawAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onCapturedRawAudioFrame");
}

- (void)onLocalProcessedAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onLocalProcessedAudioFrame");
}

- (void)onRemoteUserAudioFrame:(TRTCAudioFrame *)frame userId:(NSString *)userId {
        NSLog(@"onRemoteUserAudioFrame");
}

- (void)onMixedPlayAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onMixedPlayAudioFrame");
}

- (void)onMixedAllAudioFrame:(TRTCAudioFrame *)frame {
        NSLog(@"onMixedAllAudioFrame");
}
:::
::: Windows C++
// 사용자 정의 오디오 데이터 콜백 설정
liteav::ITRTCCloud* trtc_cloud = liteav::ITRTCCloud::getTRTCShareInstance();
trtc_cloud->setAudioFrameCallback(callback)

// 오디오 데이터 사용자 정의 콜백

virtual void onCapturedRawAudioFrame(TRTCAudioFrame* frame) {
}

virtual void onLocalProcessedAudioFrame(TRTCAudioFrame* frame) {
}

virtual void onPlayAudioFrame(TRTCAudioFrame* frame, const char* userId) {
}

virtual void onMixedPlayAudioFrame(TRTCAudioFrame* frame) {
}
:::
</dx-codeblock>

>!
>- 상기 콜백 함수는 시간이 소요되는 어떠한 작업도 해서는 안 되며, 직접 복사하여 다른 스레드를 통해 처리할 것을 권장합니다. 그렇지 않을 경우 오디오가 끊기거나 반향 제거(AEC) 기능이 적용되지 않을 수 있습니다.
>- 상기 콜백 함수에서 콜백하는 데이터는 모두 읽기 및 복사가 가능하며 수정은 불가능합니다. 수정할 경우 알 수 없는 결과가 나타날 수 있습니다.
