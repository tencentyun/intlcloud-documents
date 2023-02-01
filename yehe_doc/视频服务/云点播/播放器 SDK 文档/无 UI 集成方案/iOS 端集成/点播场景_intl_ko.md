## 준비 작업
1. [VOD](https://intl.cloud.tencent.com/)를 활성화합니다. 계정을 등록하지 않으셨다면 먼저 [회원 가입](https://intl.cloud.tencent.com/login)을 하십시오.
2. App Store에서 Xcode를 다운로드합니다. 이미 수행한 경우 이 단계를 건너뜁니다.
3. [Cocoapods 웹 사이트](https://cocoapods.org/)의 가이드에 따라 Cocoapods를 다운로드하여 설치합니다. 이미 수행한 경우 이 단계를 건너뜁니다.

## 내용 요약
* iOS용 플레이어 SDK 통합 방법
* Player SDK를 사용하여 VOD를 재생하는 방법
* Player SDK의 기본 기능을 사용하여 더 많은 기능을 구현하는 방법

## SDK 통합
[](id:step1)

### 1단계: SDK ZIP 파일 다운로드
[통합 가이드](https://www.tencentcloud.com/document/product/266/49669)의 안내에 따라 SDK ZIP 파일을 다운로드하고 통합합니다.


### 2단계: License 권한 설정
이미 관련 License 권한을 획득한 경우, [Tencent Cloud RT-Cube 콘솔](https://www.tencentcloud.com/account/login)에서 License URL과 License Key를 획득해야 합니다.

아직 필요한 License가 없다면 [Adding and Renewing a License](https://www.tencentcloud.com/document/product/266/51098)의 안내에 따라 라이선스를 받을 수 있습니다.

License 정보를 획득한 후 SDK의 해당 인터페이스를 호출하기 전에 다음 인터페이스를 통해 License를 초기화하고 `- [AppDelegate application:didFinishLaunchingWithOptions:]`에서 다음 설정하는 것이 좋습니다.

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<획득한 licenseUrl>";
    NSString * const licenceKey = @"<획득한 key>";
        
    //TXLiveBase는 "TXLiveBase.h" 헤더 파일에 위치
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
```

[](id:step2)

### 3단계: SDK 액세스 환경 설정

고객 비즈니스의 더 높은 보안성과 품질을 보장하고, 고객이 다양한 국가 및 지역의 법률 및 규정을 준수할 수 있도록 Tencent Cloud는 두 가지 세트의 SDK 액세스 환경을 제공합니다. 글로벌 사용자에게 서비스를 제공하는 경우 다음 인터페이스를 사용하여 글로벌 액세스 환경을 구성하는 것이 좋습니다.

```objective-c
// 글로벌 사용자에게 서비스를 제공하는 경우 SDK 액세스 환경을 글로벌 액세스 환경으로 구성합니다
[TXLiveBase setGlobalEnv:"GDPR"]
```

### 4단계: Player 객체 생성

VOD 기능을 구현하기 위해 플레이어 SDK의 TXVodPlayer 모듈을 사용합니다.

```objectivec
TXVodPlayer *_txVodPlayer = [[TXVodPlayer alloc] init];
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

[](id:step3)

### 5단계: 렌더링 View 생성

iOS에서 view는 기본 UI 렌더링 단위로 사용됩니다. 따라서 플레이어가 비디오 이미지를 표시할 수 있도록 크기와 위치를 조정할 수 있는 view를 구성해야 합니다.

```objectivec
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

기술적으로 플레이어는 사용자가 제공하는 view(예시 코드의 \_myView)에서 직접 비디오 이미지를 렌더링하지 않습니다. 대신 view 위에 OpenGL 렌더링을 위한 서브 뷰(subView)를 만듭니다.

view의 크기와 위치를 변경하여 비디오 이미지의 크기를 조정할 수 있습니다. SDK는 그에 따라 비디오 이미지를 변경합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/235b2e8e6fc3eb328ba05a4c5d251da7.jpg)

**애니메이션을 만드는 방법**
 view 애니메이션에 큰 유연성이 허용되지만 보기의 frame 속성이 아닌 transform을 수정해야 합니다.

```objectivec
[UIView animateWithDuration:0.5 animations:^{
     _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // 1/3로 축소
 }];
```

[](id:step4)

### 6단계: 재생 시작

TXVodPlayer는 필요에 따라 선택할 수 있는 두 가지 재생 모드를 지원합니다.

<dx-tabs>
::: URL 방식
  TXVodPlayer는 내부적으로 재생 프로토콜을 자동으로 인식합니다. 재생 URL을 startPlay 함수에 전달하기만 하면 됩니다.
```objectivec
// URL의 비디오 리소스 재생
NSString* url = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
[_txVodPlayer startVodPlay:url];

// 샌드박스 로컬 비디오 리소스 재생
// Documents 경로 가져오기
NSString *documentPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject];
// 로컬 이미지 경로 가져오기
NSString *videoPath = [NSString stringWithFormat:@"%@/video1.m3u8",documentPath];
[_txVodPlayer startVodPlay:videoPath];

```
:::
::: fileId 방식
```objectivec
TXPlayerAuthParams *p = [TXPlayerAuthParams new];
p.appId = 1252463788;
p.fileId = @"4564972819220421305";
// psign은 Player 서명입니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참고하십시오. https://www.tencentcloud.com/document/product/266/38099
p.sign = @"psignxxxxx"; // Player 서명
[_txVodPlayer startVodPlayWithParams:p];
```
[미디어 자산](https://console.cloud.tencent.com/vod/media)으로 이동하여 찾을 수 있습니다. 클릭하면 오른쪽의 비디오 세부정보에서 fileId를 볼 수 있습니다.
fileId를 통해 비디오를 재생하면 플레이어가 실제 재생 URL에 대한 백엔드를 요청합니다. 네트워크가 비정상적이거나 fileId가 존재하지 않으면 `PLAY_ERR_GET_PLAYINFO_FAIL` 이벤트가 수신됩니다. 그렇지 않으면 `PLAY_EVT_GET_PLAYINFO_SUCC`가 수신되어 요청이 성공했음을 나타냅니다.
:::
</dx-tabs>

### 7단계: 재생 중지

재생을 중지할 때 현재 UI를 종료하기 전에 **removeVideoWidget**을 사용하여 view 컨트롤을 종료하는 것을 잊지 마십시오. 이렇게 하면 메모리 유출 및 화면 깜박임 문제를 방지할 수 있습니다.

```objectivec
// 재생 중지
[_txVodPlayer stopPlay];
[_txVodPlayer removeVideoWidget]; // view 제어 종료 기억
```

## 기본 기능 사용
### 1. 재생 제어

#### 재생 시작

```objective-c
// 재생 시작
[_txVodPlayer startVodPlay:url];
```

#### 재생 일시 중지

```objective-c
// 비디오 일시 중지
[_txVodPlayer pause];
```

#### 재생 재개

```objective-c
// 비디오 재개
[_txVodPlayer resume];
```

#### 재생 중지

```objective-c
// 비디오 중지
[_txVodPlayer stopPlay];
```

#### 재생 진행률 조정(Seek)

사용자가 진행 표시줄을 드래그하면 seek를 호출하여 지정된 위치에서 재생을 시작할 수 있습니다. Player SDK는 정확한 seek를 지원합니다.

```objective-c
int time = 600; // 값이 int 유형인 경우, 단위: 초
// 재생 진행률 조정
[_txVodPlayer seek:time];
```

#### 재생 시작 시간 지정

startVodPlay를 처음 호출하기 전에 재생 시작 시간을 지정할 수 있습니다.
```objective-c
float startTimeInSecond = 60; // 단위: 초
[_txVodPlayer setStartTime:startTimeInSecond];  // 재생 시작 시간 설정
[_txVodPlayer startVodPlay:url];
```


### 2. 이미지 조정
- **view: 크기 및 위치**
setupVideoWidget의 view 매개변수의 크기와 위치를 조정하여 view의 크기와 위치를 수정할 수 있습니다. SDK는 구성에 따라 view의 크기와 위치를 자동으로 조정합니다.
- **setRenderMode: 가로 세로 채우기 또는 가로 세로 맞추기**
<table>
<tr><th>값</th><th>설명</th></tr>
<tr>
<td>RENDER_MODE_FILL_SCREEN</td>
<td>이미지는 전체 화면을 채우도록 크기가 조정되고 초과 부분은 잘립니다. 이 모드에는 검은색 막대가 없지만 이미지가 전체적으로 표시되지 않을 수 있습니다.</td>
</tr><tr>
<td>RENDER_MODE_FILL_EDGE</td>
<td>이미지는 가장 긴 면에 맞게 동일한 비율로 크기가 조정됩니다. 크기 조정 후 어느 쪽도 화면을 초과하지 않습니다. 이미지가 중앙에 있고 검은색 막대가 있을 수 있습니다.</td>
</tr></table>

- **setRenderRotation: 이미지 회전**
<table>
<tr><th>값</th><th>설명</th></tr>
<tr>
<td>HOME_ORIENTATION_RIGHT</td>
<td>home 버튼은 비디오 이미지의 오른쪽에 있음</td>
</tr><tr>
<td>HOME_ORIENTATION_DOWN</td>
<td>home 버튼은 비디오 이미지 아래에 있음</td>
</tr><tr>
<td>HOME_ORIENTATION_LEFT</td>
<td>home 버튼은 비디오 이미지 왼쪽에 있음</td>
</tr><tr>
<td>HOME_ORIENTATION_UP</td>
<td>home 버튼은 비디오 이미지 위에 있음</td>
</tr></table>

### 3. 조정 가능한 속도 재생
VOD 플레이어는 조정 가능한 속도 재생을 지원합니다. 'setRate' API를 사용하여 VOD 재생 속도를 0.5X, 1.0X, 1.2X, 2X 등으로 설정할 수 있습니다.


 ```objectivec
// 1.2 배속으로 재생 설정
[_txVodPlayer setRate:1.2]; 
// 재생 시작
[_txVodPlayer startVodPlay:url];
 ```

### 4. 재생 루프

```objective-c
// 재생 루프 설정
[_txVodPlayer setLoop:true];
// 현재 재생 루프 상태 가져오기
[_txVodPlayer loop];
```

### 5. 음소거/음소거 해제

```objective-c
// 플레이어를 음소거하거나 음소거 해제합니다. true: 음소거, false: 음소거 해제
[_txVodPlayer setMute:true];
```

### 6. 화면 캡처

**snapshot**을 호출하여 현재 비디오의 스크린샷을 캡처합니다. 이 방법은 비디오의 프레임을 캡처합니다. UI를 캡처하려면 iOS 시스템의 해당 API를 사용하십시오.

### 7. 롤 이미지 광고
플레이어 SDK를 사용하면 다음과 같이 광고용 UI에 롤 이미지를 추가할 수 있습니다.
* 'autoPlay'가 NO로 설정된 경우 플레이어는 비디오를 정상적으로 로딩하지만 즉시 재생을 시작하지는 않습니다.
* 사용자는 플레이어가 로딩된 후 비디오 재생이 시작되기 전에 플레이어 UI에서 롤 이미지 광고를 볼 수 있습니다.
* 광고 표시 중지 조건이 충족되면 resume API가 호출되어 비디오 재생이 시작됩니다.

### 8. HTTP-REF
TXVodPlayConfig의 headers는 URL이 임의로 복사되는 것을 방지하기 위해 일반적으로 사용되는 Referer 필드(Tencent Cloud는 보다 안전한 서명 기반 링크 도용 방지 솔루션 제공) 및 클라이언트 인증을 위한 Cookie 필드와 같이 HTTP 요청 헤더를 설정하는 데 사용할 수 있습니다.

```objective-c
NSMutableDictionary<NSString *, NSString *> *httpHeader = [[NSMutableDictionary alloc] init];
[httpHeader setObject:@"${Referer Content}" forKey:@"Referer"];
[_config setHeaders:httpHeader];
[_txVodPlayer setConfig:_config];
```

### 9. 하드웨어 가속
소프트웨어 디코딩만 사용하면 Blu-ray(1080p) 이상 화질의 비디오를 원활하게 재생하기가 매우 어렵습니다. 따라서 주요 시나리오가 게임 라이브 스트리밍인 경우 하드웨어 가속을 사용하는 것이 좋습니다.

소프트웨어와 하드웨어 디코딩 간에 전환하기 전에 먼저 **stopPlay**를 호출해야 하고, 전환 후 **startVodPlay**를 호출해야 합니다. 그렇지 않으면 심한 흐림 현상이 발생합니다.

```objectivec
[_txVodPlayer stopPlay];
_txVodPlayer.enableHWAcceleration = YES;
[_txVodPlayer startVodPlay:_flvUrl type:_type];
```

### 10. 해상도 설정
SDK는 hls의 다중 비트 레이트 형식을 지원하므로 사용자는 다른 비트 레이트의 스트림 간에 전환할 수 있습니다. PLAY_EVT_PLAY_BEGIN 이벤트를 수신한 후 다음과 같이 여러 비트 레이트의 배열을 가져올 수 있습니다.
```objectivec
NSArray *bitrates = [_txVodPlayer supportedBitrates]; //여러 비트 레이트의 배열 가져오기
```

재생 중에 언제든지 `-[TXVodPlayer setBitrateIndex:]`를 호출하여 비트 레이트를 전환할 수 있습니다. 전환하는 동안 다른 스트림의 데이터를 가져옵니다. SDK는 부드러운 전환을 구현하기 위해 Tencent Cloud 다중 비트 레이트 파일에 최적화되어 있습니다.
### 11. 어댑티브 비트 레이트 스트리밍
SDK는 HLS의 어댑티브 비트 레이트 스트리밍을 지원합니다. 이 기능이 활성화되면 플레이어는 현재 대역폭을 기반으로 재생에 가장 적합한 비트 레이트를 동적으로 선택할 수 있습니다. `PLAY_EVT_PLAY_BEGIN` 이벤트를 수신한 후 다음과 같이 어댑티브 비트 레이트 스트리밍을 활성화할 수 있습니다.
```objectivec
[_txVodPlayer setBitrateIndex:-1]; //index 매개변수에 -1을 전달
```
재생 중에 언제든지 `-[TXVodPlayer setBitrateIndex:]`를 호출하여 다른 비트 레이트로 전환할 수 있습니다. 전환 후에는 어댑티브 비트 레이트 스트리밍이 비활성화됩니다.

### 12. 매끄러운 비트레이트 전환

비트레이트 전환은 시간이 많이 걸릴 수 있습니다. 사용자 경험을 개선하기 위해 매끄러운 비트레이트 전환을 활성화하여 재생 중에 비트레이트를 부드럽고 매끄럽게 변경할 수 있습니다.

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
// YES로 설정하면 IDR 프레임 정렬 시 비트레이트를 원활하게 변경할 수 있습니다. NO로 설정하면 다중 비트레이트 URL을 더 빠르게 열 수 있습니다.
[_config setSmoothSwitchBitrate:YES];
[_txVodPlayer setConfig:_config];
```

### 13. 재생 진행 리스닝

VOD 진행률에는 **로딩 진행률** 및 **재생 진행률**의 두 가지 측정 항목이 있습니다. 현재 SDK는 이벤트 알림을 통해 실시간으로 두 가지 진행률 지표를 알려줍니다. 이벤트 알림 내용에 대한 자세한 내용은 [이벤트 리스닝](#listening)을 참고하십시오.


```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param {
    if (EvtID == PLAY_EVT_PLAY_PROGRESS) {
            // 로딩 진행률, 단위: 초. 소수 부분은 밀리초
            float playable = [param[EVT_PLAYABLE_DURATION] floatValue];
                [_loadProgressBar setValue:playable];
                
            // 재생 진행률, 단위: 초. 소수 부분은 밀리초
            float progress = [param[EVT_PLAY_PROGRESS] floatValue];
                [_seekProgressBar setValue:progress];
                
            // 총 비디오 길이, 단위: 초. 소수 부분은 밀리초
            float duration = [param[EVT_PLAY_DURATION] floatValue];
            // 지속 시간 표시 등을 설정하는 데 사용할 수 있음
    }
}
```


### 14. 재생 네트워크 속도 리스닝

[이벤트 리스닝](#listening)을 통해 비디오가 지연될 때 현재 네트워크 속도를 표시할 수 있습니다.

* 'onNetStatus'의 'NET_SPEED'를 사용하여 현재 네트워크 속도를 확인할 수 있습니다. 자세한 사용 방법은 [재생 상태 피드백(onNetStatus)](#status)을 참고하십시오.
* `PLAY_EVT_PLAY_LOADING` 이벤트가 감지된 후 현재 네트워크 속도가 표시됩니다.
* `PLAY_EVT_VOD_LOADING_END` 이벤트 수신 후 현재 네트워크 속도를 보여주는 화면이 숨겨집니다.

### 15. 비디오 해상도 획득

플레이어 SDK는 URL 문자열을 통해 비디오를 재생합니다. URL에는 비디오 정보가 포함되어 있지 않으며 이러한 정보를 로딩하려면 클라우드 서버에 액세스해야 합니다. 따라서 SDK는 비디오 정보를 이벤트 알림으로만 애플리케이션에 보낼 수 있습니다. 자세한 내용은 [이벤트 리스닝](#listening)을 참고하십시오.

**해상도 정보**
<dx-tabs>
::: 방법1
'onNetStatus'의 'VIDEO_WIDTH' 및 'VIDEO_HEIGHT'를 사용하여 비디오 너비와 높이를 가져옵니다. 자세한 안내는 [상태 피드백(onNetStatus)](#status)을 참고하십시오.
:::
::: 방법2
`-[TXVodPlayer width]` 및 `-[TXVodPlayer height]`를 직접 호출하여 현재 비디오 너비와 높이를 가져옵니다.
:::
</dx-tabs>

### 16. 플레이어 버퍼 크기

일반 비디오 재생 시 네트워크에서 버퍼링되는 데이터의 최대 크기를 미리 조절할 수 있습니다. 최대 버퍼 크기가 구성되지 않은 경우 플레이어는 기본 버퍼 정책을 사용하여 원활한 재생 환경을 보장합니다.

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // 재생 중 최대 버퍼 크기. 단위: MB
[_txVodPlayer setConfig:_config];  // config를 _txVodPlayer에 전달
```

### 17. 로컬 비디오 캐시[](id:cache)
짧은 비디오 재생 시나리오에서는 일반 사용자가 이미 시청한 비디오를 다시 로딩하기 위해 트래픽을 다시 소비할 필요가 없도록 로컬 비디오 파일 캐시가 필요합니다.

- **지원되는 형식:** SDK는 HLS(m3u8) 및 MP4의 두 가지 일반적인 VOD 형식으로 비디오 캐싱을 지원합니다.
- **활성화 시간:** SDK는 기본적으로 캐시 기능을 활성화하지 않습니다. 대부분의 비디오를 한 번만 시청하는 시나리오에서는 활성화하지 않는 것이 좋습니다.
- **활성화 방법:** 활성화하려면 로컬 캐시 디렉터리 및 캐시 크기의 두 가지 매개변수를 구성해야 합니다.
```objectivec
//재생 엔진의 전역 캐시 디렉터리 설정
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *documentsDirectory = [paths objectAtIndex:0];
NSString *preloadDataPath = [documentsDirectory stringByAppendingPathComponent:@"/preload"];
if (![[NSFileManager defaultManager] fileExistsAtPath:preloadDataPath]) {
     [[NSFileManager defaultManager] createDirectoryAtPath:preloadDataPath
                               withIntermediateDirectories:NO
                                                attributes:nil
                                                     error:&error];
[TXPlayerGlobalSetting setCacheFolderPath:preloadDataPath];
//재생 엔진 캐시 크기 설정
[TXPlayerGlobalSetting setMaxCacheSize:200];
// 재생 시작
[_txVodPlayer startVodPlay:url];                         
```

>? 이전 버전에서 구성에 사용된 TXVodPlayConfig#setMaxCacheItems API는 사용되지 않았으므로 권장하지 않습니다.

## 고급 기능 사용

### 1. 비디오 사전 로딩

#### 1단계: 비디오 사전 로딩 사용

UGSV 재생 시나리오에서 사전 로딩 기능은 원활한 시청 환경에 기여합니다. 비디오를 시청하는 동안 백엔드에서 재생할 다음 비디오의 URL을 로딩할 수 있습니다. 다음 비디오로 전환되면 미리 로딩되어 즉시 재생할 수 있습니다.

비디오 사전 로딩은 즉각적인 재생 효과를 제공할 수 있지만 특정 성능 오버헤드가 있습니다. 회사에서 많은 비디오를 사전 로딩해야 하는 경우 [비디오 사전 다운로드](#download)와 함께 이 기능을 사용하는 것이 좋습니다.

이것이 비디오 재생에서 매끄러운 전환이 작동하는 방식입니다. TXVodPlayer에서 isAutoPlay를 사용하여 다음과 같이 기능을 구현할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg" width=850px>

```objectivec
// 재생 비디오 A: isAutoPlay가 YES로 설정되어 있으면 startVodPlay가 호출될 때 비디오가 즉시 로딩되어 재생됩니다.
NSString* url_A = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
_player_A.isAutoPlay = YES;
[_player_A startVodPlay:url_A];

// 비디오 A를 재생할 때 비디오 B를 사전 로딩하려면 isAutoPlay를 NO로 설정합니다.
NSString* url_B = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
_player_B.isAutoPlay = NO;
[_player_B startVodPlay:url_B];
```

비디오 A가 종료되고 비디오 B가 자동 또는 수동으로 전환된 후 resume 기능을 호출하여 비디오 B를 즉시 재생할 수 있습니다.

>! autoPlay를 false로 설정한 후 resume을 호출하기 전에 비디오 B가 준비되었는지 확인하십시오. 즉, 비디오 B의 PLAY_EVT_VOD_PLAY_PREPARED (2013, 플레이어가 준비되었으며 비디오를 재생할 수 있음) 이벤트가 감지된 후에만 호출해야 합니다.

```objectivec
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    // 비디오 A가 끝나면 끊김 없는 전환을 위해 비디오 B 재생을 직접 시작
    if (EvtID == PLAY_EVT_PLAY_END) {
            [_player_A stopPlay];
            [_player_B setupVideoWidget:mVideoContainer insertIndex:0];
            [_player_B resume];
        }
}
```

#### 2단계: 비디오 사전 로딩 버퍼 구성

- 불안정한 네트워크 환경에서 보다 원활하게 비디오를 재생하기 위해 큰 버퍼를 설정할 수 있습니다.

- 트래픽 소모를 줄이기 위해 더 작은 버퍼를 설정할 수 있습니다. 

##### 버퍼 크기 사전 로딩

이 API는 사전 로딩 시나리오에서 재생이 시작되기 전에 최대 버퍼 크기를 제어하는 데 사용됩니다(즉, 비디오 재생이 시작되기 전에 player의 AutoPlay가 false로 설정됨).

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxPreloadSize:(2)];;  // 최대 사전 로딩 버퍼 크기. 단위: MB, 트래픽 소비를 줄이기 위해 비즈니스 상황에 따라 설정
[_txVodPlayer setConfig:_config];  // config를 _txVodPlayer에 전달
```

##### 재생 버퍼 크기 

일반 비디오 재생 시 네트워크에서 버퍼링되는 데이터의 최대 크기를 미리 조절할 수 있습니다. 최대 버퍼 크기가 구성되지 않은 경우 플레이어는 기본 버퍼 정책을 사용하여 원활한 재생 환경을 보장합니다.

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // 재생 중 최대 버퍼 크기. 단위: MB
[_txVodPlayer setConfig:_config];  // config를 _txVodPlayer에 전달
```

### 2. 비디오 사전 다운로드[](id:download)
플레이어 인스턴스를 생성하지 않고 미리 비디오 콘텐츠의 일부를 다운로드하여 플레이어를 사용할 때 비디오 재생을 더 빠르게 시작할 수 있습니다. 이는 더 나은 재생 경험을 제공하는 데 도움이 됩니다.

재생 서비스를 이용하시기 전에 [비디오 캐시](#cache)가 설정되어 있는지 확인하십시오.
>?
>- TXPlayerGlobalSetting은 전역 캐시 설정 API이며 원래 TXVodConfig API는 사용하지 않았습니다.
>- 전역 캐시 디렉터리 및 크기 설정은 플레이어의 TXVodConfig에서 구성한 것보다 우선순위가 높습니다.

사용 예시:

```objective-c
//재생 엔진의 전역 캐시 디렉터리 설정
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *documentsDirectory = [paths objectAtIndex:0];
NSString *preloadDataPath = [documentsDirectory stringByAppendingPathComponent:@"/preload"];
if (![[NSFileManager defaultManager] fileExistsAtPath:preloadDataPath]) {
     [[NSFileManager defaultManager] createDirectoryAtPath:preloadDataPath 
      												 withIntermediateDirectories:NO 
      																					attributes:nil 
      																							 error:&error]; //Create folder
}
[TXPlayerGlobalSetting setCacheFolderPath:preloadDataPath];

//재생 엔진 캐시 크기 설정
[TXPlayerGlobalSetting setMaxCacheSize:200];
NSString *m3u8url = "http://****";
int taskID = [[TXVodPreloadManager sharedManager] startPreload:m3u8url 
 																									 preloadSize:10 
 																					 preferredResolution:1920*1080 
 																											delegate:self];


//사전 다운로드 취소
[[TXVodPreloadManager sharedManager] stopPreload:taskID];
```

### 3. 비디오 다운로드
비디오 다운로드를 통해 사용자는 온라인 비디오를 다운로드하고 오프라인에서 볼 수 있습니다. 또한 플레이어 SDK는 로컬 암호화 기능을 제공하므로 다운로드한 로컬 파일은 계속 암호화되어 지정된 플레이어에서만 해독 및 재생할 수 있습니다. 이 기능은 다운로드한 비디오가 무단으로 배포되는 것을 효과적으로 방지하고 비디오 보안을 보호할 수 있습니다.

HLS 스트리밍 미디어는 로컬에 직접 저장할 수 없으므로 다운로드하여 로컬 파일로 재생할 수 없습니다. 'TXVodDownloadManager' 기반의 비디오 다운로드 방식을 사용하여 오프라인 HLS 재생을 구현할 수 있습니다.

> ! 
> - 현재 `TXVodDownloadManager`는 HLS 파일만 캐시할 수 있으며, MP4 및 FLV 파일은 캐시할 수 없습니다.
>- 플레이어 SDK는 이미 로컬 MP4 및 FLV 파일 재생을 지원합니다.
[](id:offline1)
#### 1단계: 준비 작업

`TXVodDownloadManager`는 싱글톤으로 설계되었습니다. 따라서 여러 다운로드 객체를 만들 수 없습니다. 다음과 같이 사용됩니다.

```objective-c
TXVodDownloadManager *downloader = [TXVodDownloadManager shareInstance];
// 다운로드 디렉터리를 설정합니다. ‘ TXPlayerGlobalSetting #setCacheFolderPath’의 구성이 먼저 적용됩니다.
[downloader setDownloadPath:"<다운로드 디렉터리 지정>"];
```

[](id:offline2)
#### 2단계: 다운로드 시작
fileid 또는 URL로 다운로드를 시작할 수 있습니다.
<dx-tabs>

::: fileid 방식
fileid를 통해 다운로드하려면 적어도 appId 및 fileId를 전달해야 합니다. userName에 값을 지정하지 않으면 기본적으로 ‘default’가 사용됩니다. **참고: Fileid를 통해서만 암호화된 비디오를 다운로드할 수 있으며 psign 매개변수를 입력해야 합니다.**

```objective-c
TXVodDownloadDataSource *source = [[TXVodDownloadDataSource alloc] init];    
source.appId = 1252463788;
source.fileId = @"4564972819220421305";
// // psign은 Player 서명입니다. 서명 및 생성 방식에 관한 내용은 [Player 서명](https://www.tencentcloud.com/document/product/266/38099)을 참고하십시오. 
source.pSign = @"xxxxxxxxxx";

// 다운로드 해상도 지정
// 유효한 값: 원본: TXVodQualityOD, LD: TXVodQualityFLU, SD: TXVodQualitySD, HD: TXVodQualityHD, FHD: TXVodQualityFHD, 2K: TXVodQuality2K, 4K: TXVodQuality4K
source.quality = TXVodQualityHD;  // HD
    
// ** 다운로드에 레거시 v2 프로토콜을 사용하는 경우 TXVodDownloadDataSource의 auth 속성을 통해 appId 및 fileId 매개변수를 설정하십시오. **
// source.auth = auth;  ** 기본적으로 설정할 필요가 없습니다 **
    
[downloader startDownload:dataSource];
```
:::

::: URL 방식
다운로드 URL만 전달하면 됩니다. 중첩되지 않은 HLS, 즉 단일 비트스트림 HLS만 지원됩니다. 개인 암호화의 경우 fileid를 사용하십시오.

```objective-c
[downloader startDownloadUrl:@"http://1253131631.vod2.myqcloud.com/26f327f9vodgzp1253131631/f4bdff799031868222924043041/playlist.m3u8"]
```

:::

</dx-tabs>


[](id:offline3)
#### 3단계: 작업 정보 받기 

작업 정보를 받기 전에 먼저 콜백 delegate를 설정해야 합니다.

```objective-c
downloader.delegate = self;
```

다음 작업 콜백을 받을 수 있습니다.
<table><thead>
<tr><th width="55%">콜백 메시지</th><th>설명</th></tr>
</thead>
<tbody><tr>
<td>-[TXVodDownloadDelegate onDownloadStart:]</td>
<td>작업 시작. 즉, SDK가 다운로드를 시작함</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadProgress:]</td>
<td>작업 진행 상황. 다운로드하는 동안 SDK는 이 API를 자주 호출합니다. 여기에서 표시된 진행 상황을 업데이트할 수 있습니다.</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadStop:]</td>
<td>작업 중지. <code>stopDownload</code>를 호출하여 다운로드를 중지할 때 이 메시지가 수신되면 다운로드가 성공적으로 중지됩니다.</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadFinish:]</td>
<td>다운로드 완료. 이 콜백이 수신되면 전체 파일이 다운로드된 것이며 다운로드한 파일은 TXVodPlayer로 재생할 수 있습니다.</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadError:errorMsg:]</td>
<td>다운로드 오류. 다운로드 중에 네트워크 연결이 끊어지면 이 API가 다시 호출되고 다운로드 작업이 중지됩니다. 모든 오류 코드는 <code>TXDownloadError</code>를 참고하십시오.</td>
</tr>
</tbody></table>

downloader는 한 번에 여러 파일을 다운로드할 수 있으므로 콜백 API는 'TXVodDownloadMediaInfo' 객체를 전달합니다. URL 또는 dataSource에 액세스하여 다운로드 소스를 확인하고 다운로드 진행률 및 파일 크기와 같은 기타 정보를 얻을 수 있습니다.

[](id:offline4)
#### 4단계: 다운로드 중지

`-[TXVodDownloadManager stopDownload:]` 메소드를 호출하여 다운로드를 중지할 수 있습니다. 매개변수는 `-[TXVodDownloadManager sartDownloadUrl:]`에 의해 반환된 객체입니다. **SDK는 체크포인트 재시작을 지원합니다**. 다운로드 디렉터리가 변경되지 않은 경우, 파일 다운로드를 재개할 때 중지된 지점부터 다운로드가 시작됩니다.

#### 5단계: 다운로드 관리

모든 계정 또는 지정된 계정의 다운로드 목록을 가져올 수 있습니다.

```objective-c
NSArray<TXVodDownloadMediaInfo *> *array = [[[TXVodDownloadManager shareInstance] getDownloadMediaInfoList] mutableCopy];
// “default” 사용자의 다운로드 목록 가져오기
for (TXVodDownloadMediaInfo *info in array) {
    if ([info.userName isEqualToString:@"default"]) {
        // “default” 사용자의 다운로드 목록 저장
    }
}
```

FileId 또는 URL의 다운로드 정보를 가져옵니다.

`-[TXVodDownloadManager getDownloadMediaInfo:]` API를 통해 Fileid의 다운로드 정보(예: 현재 다운로드 상태 및 진행률)를 얻으려면 AppID, Fileid 및 qualityId를 전달해야 합니다.

```objective-c
// fileId의 다운로드 정보 가져오기
TXVodDownloadMediaInfo *sourceMediaInfo = [[TXVodDownloadMediaInfo alloc] init];
TXVodDownloadDataSource *dataSource = [[TXVodDownloadDataSource alloc] init];
dataSource.appId = 1252463788;
dataSource.fileId = @"4564972819220421305";
dataSource.pSign = @"psignxxxx";
dataSource.quality = TXVodQualityHD;
sourceMediaInfo.dataSource = dataSource;
TXVodDownloadMediaInfo *downlaodMediaInfo =  [[TXVodDownloadManager shareInstance] getDownloadMediaInfo:sourceMediaInfo];

// 다운로드 중인 파일의 전체 크기를 Byte 단위로 가져옵니다. 이 API는 fileid를 통한 다운로드에만 적용됩니다.
// 참고: 전체 크기는 VOD 콘솔에 업로드된 원본 파일의 크기를 의미합니다. 현재 어댑티브 비트레이트 스트리밍 이후의 서브스트림 크기는 얻을 수 없습니다.
downlaodMediaInfo.size; //  다운로드 중인 파일의 전체 크기 가져오기
downlaodMediaInfo.duration;   // 총 소요시간 가져오기
downlaodMediaInfo.playableDuration; // 다운로드한 동영상의 재생 가능 시간 가져오기
downlaodMediaInfo.progress;   // 다운로드 진행률 가져오기
downlaodMediaInfo.playPath;   // 오프라인 재생을 시작하기 위해 플레이어에 전달할 수 있는 오프라인 재생 경로 가져오기
downlaodMediaInfo.downloadState;  // 다운로드 상태 가져오기, 자세한 내용은 STATE_xxx 상수 참고
[downlaodMediaInfo isDownloadFinished];  // YES가 반환되면 다운로드가 완료된 것임
```

URL의 다운로드 정보를 얻으려면 URL 정보를 전달하기만 하면 됩니다.

```objective-c
// fileId의 다운로드 정보 가져오기
TXVodDownloadMediaInfo *sourceMediaInfo = [[TXVodDownloadMediaInfo alloc] init];
mediaInfo.url = @"videoURL";
TXVodDownloadMediaInfo *downlaodMediaInfo =  [[TXVodDownloadManager shareInstance] getDownloadMediaInfo:sourceMediaInfo];
```

다운로드 정보 및 관련 파일 삭제:

다운로드를 재개할 필요가 없다면 `-[TXVodDownloadManager deleteDownloadFile:]` 메소드를 호출하여 파일을 삭제하여 저장 공간을 확보하십시오.

### 4. 암호화된 재생

비디오 암호화 솔루션은 온라인 교육과 같이 비디오 저작권을 보호해야 하는 시나리오에서 사용됩니다. 비디오 리소스를 암호화하려면 플레이어를 변경하고 비디오 소스를 암호화 및 트랜스 코딩해야 합니다. 자세한 내용은 [비디오 암호화 개요](https://www.tencentcloud.com/document/product/266/38131)를 참고하십시오.

Tencent Cloud 콘솔에서 암호화된 비디오의 appId, fileId 및 psign을 가져오고 비디오를 재생합니다.
```objective-c
TXPlayerAuthParams *p = [TXPlayerAuthParams new];
p.appId = 1252463788; // Tencent Cloud 계정의 appId
p.fileId = @"4564972819220421305"; // 비디오의 fileId
// psign은 Player 서명입니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참고하십시오. https://www.tencentcloud.com/document/product/266/38099
p.sign = @"psignxxxxx"; // Player 서명
[_txVodPlayer startVodPlayWithParams:p];
```

### 5. 플레이어 구성 

statPlay를 호출하기 전에 setConfig를 호출하여 플레이어 연결 시간 초과 기간, 진행 콜백 간격 및 캐시된 파일의 최대 수와 같은 플레이어 매개변수를 구성할 수 있습니다. TXVodPlayConfig를 사용하면 세부 매개변수를 구성할 수 있습니다. 자세한 내용은 [기본 구성 API](https://www.tencentcloud.com/document/product/266/47844#txvodplayconfig)를 참고하십시오. 다음은 구성 예시 코드입니다.

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setEnableAccurateSeek:true];  // 정확한 seek 활성화 여부 설정, 기본값: true
[_config setMaxCacheItems:5];  // 캐시된 파일의 최대 수를 5로 설정
[_config setProgressInterval:200];  // 진행 콜백 간격 설정, 단위: 밀리초
[_config setMaxBufferSize:50];  // 최대 사전 로딩 버퍼 크기 설정, 단위: MB
[_txVodPlayer setConfig:_config];  // config를 _txVodPlayer에 전달
```

##### 재생 시작 시 해상도 지정

 HLS 다중 비트 레이트 비디오 소스를 재생할 때 비디오 스트림 해상도 정보를 미리 알고 있으면 재생이 시작되기 전에 기본 해상도를 지정할 수 있으며 플레이어는 기본 해상도 이하에서 스트림을 선택하여 재생합니다. 이렇게 하면 재생이 시작된 후 필요한 비트스트림으로 전환하기 위해 setBitrateIndex를 호출할 필요가 없습니다.

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
// 전달된 매개변수는 비디오 너비와 높이의 곱(너비 * 높이)입니다. 사용자 정의 값을 전달할 수 있습니다.
[_config setPreferredResolution:720*1280];
[_txVodPlayer setConfig:_config];  // config를 _txVodPlayer에 전달
```

##### 재생 진행 콜백 간격 설정

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setProgressInterval:200];  // 진행 콜백 간격 설정, 단위: 밀리초
[_txVodPlayer setConfig:_config];  // config를 _txVodPlayer에 전달
```

[](id:listening)

## 플레이어 이벤트 리스닝
TXVodPlayListener 리스너를 TXVodPlayer 객체에 바인딩하여 onPlayEvent(이벤트 알림) 및onNetStatus(상태 피드백)를 사용하여 정보를 애플리케이션에 동기화할 수 있습니다.

### 이벤트 공지(onPlayEvent)

#### 재생 이벤트
| 이벤트 ID               |   코드  |  설명                 |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_BEGIN    |  2004|  비디오 재생 시작됨 |
|PLAY_EVT_PLAY_PROGRESS |  2005|  비디오 재생 진행률. 현재 재생 진행률, 로딩 진행률, 총 비디오 재생 시간을 알려줌     |
|PLAY_EVT_PLAY_LOADING  |  2007|  비디오을 loading하는 중입니다. 비디오 재생이 재개되면 LOADING_END 이벤트가 보고됨 |
|PLAY_EVT_VOD_LOADING_END   |  2014|  비디오 loading이 종료되고 비디오 재생이 재개됨|
| VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seek 완료, 10.3 버전부터 지원|
| VOD_PLAY_EVT_LOOP_ONCE_COMPLETE           | 6001 | 연속 재생, 루프 재생 완료(10.8 버전 부터 지원) |

#### 이벤트 중지
| 이벤트 ID                 |    코드  |  설명                |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_END      |  2006|  비디오 재생 종료   |
|PLAY_ERR_NET_DISCONNECT |  -2301  |  네트워크 연결이 끊겼고 여러 번 재시도한 후에도 다시 연결할 수 없습니다. 플레이어를 다시 시작하여 더 많은 연결 재시도를 수행할 수 있음 |
|PLAY_ERR_HLS_KEY       | -2305 | HLS 암호 해독 key를 가져오기 실패 |

#### 경고 이벤트
SDK의 일부 내부 이벤트를 알리는 데만 사용되는 다음 이벤트는 무시할 수 있습니다.

| 이벤트 ID                 |    코드  |  설명                    |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 현재 비디오 프레임 디코딩 실패  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 현재 오디오 프레임 디코딩 실패  |
| PLAY_WARNING_RECONNECT           |  2103  | 네트워크 연결 끊김 및 자동 재연결 수행(세 번의 시도 실패 후 `PLAY_ERR_NET_DISCONNECT` 이벤트 발생)|
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | 하드웨어 디코더 시작 실패, 소프트웨어 디코더가 대신 사용됨   |


#### 연결 이벤트
다음 서버 연결 이벤트는 주로 서버 연결 시간을 측정하고 수집하는 데 사용됩니다.

| 이벤트 ID                     |    코드  |  설명                    |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_VOD_PLAY_PREPARED     |  2013    | 플레이어가 준비되었으며 재생 시작 가능. autoPlay가 false로 설정되어 있으면 이 이벤트를 수신한 후 resume을 호출하여 재생을 시작해야함     |
| PLAY_EVT_RCV_FIRST_I_FRAME|  2003    | 네트워크는 첫 번째 렌더링 가능한 비디오 데이터 패킷(IDR)을 수신함  |

#### 이미지 품질 이벤트
다음 이벤트는 이미지 변경 정보를 가져오는 데 사용됩니다.

| 이벤트 ID                     |    코드  |  설명                    |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_CHANGE_RESOLUTION|  2009    | 비디오 해상도가 변경됨               |
| PLAY_EVT_CHANGE_ROATION   |  2011    | MP4 비디오 회전 각도 |


#### 비디오 정보 이벤트
| 이벤트 ID                     |    코드  |  설명                    |
| :-----------------------  |:-------- |  :------------------------ |
|PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | 재생된 파일의 정보 가져오기 성공 |

fileId를 통해 비디오를 재생하고 재생 요청이 성공하면 SDK는 일부 요청 정보를 상위 레이어에 알리고, PLAY_EVT_GET_PLAYINFO_SUCC 이벤트를 수신한 후 param을 구문 분석하여 비디오 정보를 얻을 수 있습니다.

|   비디오 정보                   |  설명                   |
| :------------------------  |  :------------------------ |
| EVT_PLAY_COVER_URL     | 비디오 썸네일 URL |
| EVT_PLAY_URL  | 비디오 재생 URL |
| EVT_PLAY_DURATION | 비디오 길이 |

```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    if (EvtID == PLAY_EVT_VOD_PLAY_PREPARED) {
        // 플레이어 준비 완료 이벤트가 수신되고 pause, resume, getWidth, getSupportedBitrates API를 호출할 수 있음
    } else if (EvtID == PLAY_EVT_PLAY_BEGIN) {
        // 재생 시작 이벤트 수신
    } else if (EvtID == PLAY_EVT_PLAY_END) {
        // 재생 종료 이벤트 수신
    }
}
```

[](id:status)

### 상태 피드백(onNetStatus)
상태 피드백은 푸셔의 현재 상태에 대한 실시간 피드백을 제공하기 위해 0.5초마다 한 번씩 트리거됩니다. 현재 비디오 재생 상태를 더 잘 이해할 수 있도록 SDK 내부에서 일어나는 일을 알려주는 대시보드 역할을 할 수 있습니다.
<table>
<tr><th>매개변수</th><th>설명</th></tr><tr>
<td>CPU_USAGE</td><td>현재 순간 CPU 사용률</td>
</tr><tr>
<td>VIDEO_WIDTH</td><td>비디오 해상도 - 너비</td>
</tr><tr>
<td>VIDEO_HEIGHT</td><td>비디오 해상도 - 높이</td>
</tr><tr>
<td>NET_SPEED</td><td>현재 네트워크 데이터 수신 속도</td>
</tr><tr>
<td>VIDEO_FPS</td><td>스트리밍 미디어의 현재 비디오 프레임 레이트</td>
</tr><tr>
<td>VIDEO_BITRATE</td><td>스트리밍 미디어의 현재 비디오 비트 레이트, 단위: kbps</td>
</tr><tr>
<td>AUDIO_BITRATE</td><td>스트리밍 미디어의 현재 오디오 비트 레이트, 단위: kbps</td>
</tr><tr>
<td>V_SUM_CACHE_SIZE</td><td>버퍼(jitterbuffer) 크기입니다. 현재 버퍼 길이가 0이면 지연이 곧 발생</td>
</tr><tr>
<td>SERVER_IP</td><td>연결된 서버 IP</td>
</tr></table>
다음은 onNetStatus를 사용하여 비디오 재생 정보를 가져오는 예시 코드입니다.
```objective-c
- (void)onNetStatus:(TXVodPlayer *)player withParam:(NSDictionary *)param {
    //현재 CPU 사용률 가져오기
    float cpuUsage = [[param objectForKey:@"CPU_USAGE"] floatValue];
    //비디오 너비 가져오기
    int videoWidth = [[param objectForKey:@"VIDEO_WIDTH"] intValue];
    //비디오 높이 가져오기
    int videoHeight = [[param objectForKey:@"VIDEO_HEIGHT"] intValue];
    // 실시간 속도 가져오기
    int  speed = [[param objectForKey:@"NET_SPEED"] intValue];
    //스트리밍 미디어의 현재 비디오 프레임 레이트 가져오기
    int fps = [[param objectForKey:@"VIDEO_FPS"] intValue];
    //스트리밍 미디어의 현재 비디오 비트 레이트 가져오기, 단위: kbps
    int videoBitRate = [[param objectForKey:@"VIDEO_BITRATE"] intValue];
    //스트리밍 미디어의 현재 오디오 비트 레이트 가져오기, 단위: kbps
    int audioBitRate = [[param objectForKey:@"AUDIO_BITRATE"] intValue];
    //버퍼(jitterbuffer) 크기 가져오기, 현재 버퍼 길이가 0이므로 곧 지연이 발생함
    int jitterbuffer = [[param objectForKey:@"V_SUM_CACHE_SIZE"] intValue];
    //연결된 서버 IP 가져오기
    NSString *ip = [param objectForKey:@"SERVER_IP"];
}
```

## 시나리오별 기능

### 1. SDK 기반 Demo 컴포넌트

Tencent Cloud는 플레이어 SDK를 기반으로 [플레이어 컴포넌트](https://intl.cloud.tencent.com/document/product/266/33976)를 개발했습니다. 품질 모니터링, 비디오 암호화, TESHD, 해상도 전환 및 작은 창 재생을 통합하고 모든 VOD 및 라이브 재생 시나리오에 적합합니다. 전체 기능을 캡슐화하고 상위 레이어 UI를 제공하여 인기 있는 비디오 App에 필적하는 재생 프로그램을 빠르게 만들 수 있습니다.

### 2. 오픈 소스 GitHub 프로젝트

플레이어 SDK를 기반으로 Tencent Cloud는 몰입형 비디오 플레이어, 비디오 Feed 스트림 및 다중 레이어 재사용 컴포넌트를 개발했으며 향후 버전에서 더 많은 사용자 시나리오 기반 구성 요소를 제공할 예정입니다. [Player_iOS](https://github.com/LiteAVSDK/Player_iOS)를 다운로드하여 컴포넌트를 사용해 볼 수 있습니다.
