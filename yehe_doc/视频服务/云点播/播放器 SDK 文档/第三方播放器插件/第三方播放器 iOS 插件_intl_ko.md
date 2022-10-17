타사 Player iOS 플러그인은 타사 또는 독점 플레이어를 사용하여 Tencent Cloud PaaS 리소스에 연결하려는 고객을 위해 VOD에서 제공하는 Player 플러그인입니다. 일반적으로 Player 기능을 커스터마이징하길 원하는 고객이 사용합니다.


## SDK 다운로드
타사 Player iOS 플러그인 및 Demo는 [TXCPlayerAdapterSDK_iOS](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.2.0/TXCPlayerAdapterSDK_1.2.0_iOS.zip)를 참고하십시오. 

## 통합 가이드

### 환경 요건

HTTP 요청에 대한 지원을 구성하려면 프로젝트의 info.plist 파일에서 `App Transport Security Settings->Allow Arbitrary Loads`를 YES로 설정해야 합니다.

### 컴포넌트 종속성

`GCDWebServer` 컴포넌트 종속성을 추가합니다.   

```objective-c
pod "GCDWebServer", "~> 3.0"
```

GCDWebServer는 GCD를 기반으로 하는 경량 HTTP server이며 OS X & iOS에서 사용할 수 있습니다. 이 라이브러리는 Web 기반 파일 업로드 및 WebDAV server와 같은 확장 기능도 구현합니다.

### 플레이어 사용

변수를 선언한 다음 인스턴스를 만듭니다. 플레이어의 메인 클래스는 `TXCPlayerAdapter`이며, 동영상을 생성한 후 재생할 수 있습니다.

FileId는 일반적으로 비디오가 업로드된 후 서버에서 반환됩니다.

1. 비디오가 클라이언트에 게시된 후 서버는 클라이언트에 fileId를 반환합니다.
2. 동영상이 서버에 업로드되면 업로드 확인 알림에 해당 fileId가 포함됩니다.


파일이 이미 Tencent Cloud에 있는 경우 [미디어 자산](https://console.cloud.tencent.com/vod/media)으로 이동하여 찾을 수 있습니다. 클릭 후 오른쪽의 비디오 세부 정보에서 관련 매개변수를 볼 수 있습니다.

```objective-c
NSInteger appId; ////Tencent Cloud VOD에서 appid 신청 가능
NSString *fileId;
//psign은 Player 서명입니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참고하십시오. https://cloud.tencent.com/document/product/266/42436
NSString *pSign = self.pSignTextView.text;
    
TXCPlayerAdapter *adapter = [TXCPlayerAdapter shareAdapterWithAppId:appId];
```

비디오 정보 요청 및 비디오 재생:

```objective-c
id<ITXCPlayerAssistorProtocol> assistor = [TXCPlayerAdapter createPlayerAssistorWithFileId:fileId pSign:pSign];
[assistor requestVideoInfo:^(id<ITXCPlayerAssistorProtocol> response, NSError *error) {
    if (error){
        NSLog(@"create player assistor error : %@",error);
        [self.view makeToast:error.description duration:5.0 position:CSToastPositionBottom];
        return;
    }
    [weakSelf avplayerPlay:response]; //비디오 재생
}];



- (void)avplayerPlay:(id<ITXCPlayerAssistorProtocol>)response
{
    AVPlayerViewController *playerVC = [[AVPlayerViewController alloc] init];
    self.playerVC = playerVC;
    TXCStreamingInfo *info = response.getStreamingInfo;
    AVPlayer *player = [[AVPlayer alloc] initWithURL:[NSURL URLWithString:info.playUrl]];
    playerVC.player = player;
    playerVC.title = response.getVideoBasicInfo.name;
    [self.navigationController pushViewController:playerVC animated:YES];
    
    [player addObserver:self forKeyPath:@"status" options:NSKeyValueObservingOptionNew context:nil];
}
```

사용 후 Player 종료:

```objective-c
[TXCPlayerAdapter destroy];
```



## SDK API 설명

### Adatper 초기화
이 API는 Adapter 싱글톤을 초기화하는 데 사용됩니다.

**API**

```
+ (instancetype)shareAdapterWithAppId:(NSUInteger)appId;
```

**매개변수 설명**

appId: appid 입력(서브 애플리케이션을 사용하는 경우 subappid 입력)

### Adatper 종료
이 API는 어댑터를 폐기하는 데 사용됩니다. 프로그램 종료 후 호출할 수 있습니다.

**API**

```
+ (void)destroy;
```

### 플레이어의 보조 클래스 생성

플레이어의 보조 클래스는 재생 fileId를 가져오고 DRM 암호화 API를 처리하는 데 사용할 수 있습니다.

**API**

```
+ (id<ITXCPlayerAssistorProtocol>)createPlayerAssistorWithFileId:(NSString *)fileId
                                                           pSign:(NSString *)pSign;
```

**매개변수 설명**

| 매개변수 | 유형   | 설명               |
| :----- | :----- | :----------------- |
| fileId | String | 재생할 비디오의 fileId |
| pSign  | String | Player 서명     |

### 비디오 재생 정보 요청

이 API는 Tencent Cloud VOD 서버에서 재생할 동영상의 스트림 정보를 요청하는 데 사용됩니다.

**API**

```objective-c
- (void)requestVideoInfo:(ITXCRequestVideoInfoCallback)completion;
```

**매개변수 설명**

| 매개변수         | 유형                         | 설명         |
| :------------- | :--------------------------- | :----------- |
| completion | ITXCRequestVideoInfoCallback | 비동기 콜백 함수 |



### 플레이어의 보조 클래스 종료

이 API는 보조 클래스를 종료하는 데 사용됩니다. 플레이어 종료 또는 다음 비디오 재생으로 전환 시 호출할 수 있습니다.

**API**

```
+ (void)destroyPlayerAssistor:(id<ITXCPlayerAssistorProtocol>)assistor;
```



### 기본 비디오 정보 얻기

이 API는 비디오 정보를 가져오는 데 사용되며 `id<ITXCPlayerAssistorProtocol>.requestVideoInfo`가 다시 호출된 후에만 적용됩니다.

**API**

```
- (TXCVideoBasicInfo *)getVideoBasicInfo;
```

**매개변수 설명**

TXCVideoBasicInfo의 매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 설명                 |
| :---------- | :----- | :------------------- |
| name        | String | 비디오 이름             |
| size        | Int    | 비디오 크기(바이트) |
| duration    | Float  | 비디오 길이(초)   |
| description | String | 비디오 설명             |
| coverUrl    | String | 비디오 썸네일             |



### 비디오 스트림 정보 가져오기

이 API는 비디오 스트림 정보 목록을 가져오는 데 사용되며 `id<ITXCPlayerAssistorProtocol>.requestVideoInfo`가 다시 호출된 후에만 적용됩니다.

**API**

```
- (TXCStreamingInfo *)getStreamingInfo;
```

**매개변수 설명**

TXCStreamingInfo의 매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 설명                                                         |
| :--------- | :----- | :----------------------------------------------------------- |
| playUrl    | String | 재생 URL                                                     |
| subStreams | List   | [TXCSubStreamInfo](#TXCSubStreamInfo) 유형의 어댑티브 비트스트림 서브스트림 정보 |

TXCSubStreamInfo 의 매개변수는 다음과 같습니다: [](id:TXCSubStreamInfo)

| 매개변수         | 유형   | 설명                                 |
| :------------- | :----- | :----------------------------------- |
| type           | String | 서브스트림 유형. 유효 값: video |
| width          | Int    | 서브스트림 비디오 너비(px)               |
| height         | Int    | 서브스트림 비디오 높이(px)               |
| resolutionName | String | 플레이어에 표시되는 서브스트림 비디오 사양 이름       |

### 키 프레임 타임스탬프 정보 가져오기

이 API는 비디오 키 프레임 타임스탬프 정보를 가져오는 데 사용되며 `id<ITXCPlayerAssistorProtocol>.requestVideoInfo`가 다시 호출된 후에만 적용됩니다.

**API**

```
- (NSArray<TXCKeyFrameDescInfo *> *)getKeyFrameDescInfos;
```

**매개변수 설명**

TXCKeyFrameDescInfo의 매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 설명          |
| :--------- | :----- | :------------ |
| timeOffset | Float  | 1.1           |
| content    | String | ‘지금 시작...’ |



### 썸네일 정보 가져오기

이 API는 썸네일 정보를 가져오는 데 사용되며 `id<ITXCPlayerAssistorProtocol>.requestVideoInfo`가 다시 호출된 후에만 적용됩니다.

**API**

```
- (TXCImageSpriteInfo *)getImageSpriteInfo;
```

**매개변수 설명**

TCXImageSpriteInfo의 매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 설명                               |
| :-------- | :----- | :--------------------------------- |
| imageUrls | List   | String 유형의 썸네일 다운로드 URL 배열 |
| webVttUrl | String | 썸네일 VTT 파일 다운로드 URL            |
