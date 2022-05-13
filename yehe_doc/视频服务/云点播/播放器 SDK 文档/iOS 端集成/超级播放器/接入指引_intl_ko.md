## 제품 개요

iOS용 Tencent Cloud RT-Cube Superplayer는 오픈 소스 Tencent Cloud 플레이어 컴포넌트입니다. 몇 줄의 코드로 Tencent Video와 유사한 강력한 재생 기능을 제공할 수 있습니다. 가로/세로 모드 전환, 해상도 선택, 제스처 및 작은 창 재생과 같은 기본 기능과 비디오 버퍼링, 소프트웨어/하드웨어 디코딩 전환 및 조정 가능한 속도 재생과 같은 특수 기능이 있습니다. 시스템 기본 플레이어보다 더 많은 형식을 지원하고 더 나은 호환성과 기능을 제공합니다. 또한 첫 번째 프레임 바로 재생과 저지연성의 장점을 보유하고 있으며 비디오 썸네일과 같은 고급 기능을 제공합니다.

## 버전 지원

본 문서에서 설명된 기능에 대한 Tencent Cloud RT-Cube 지원 현황은 다음과 같습니다.

| 버전                            | Smart                                               | Live                                                | UGSV                                                  | TRTC                                             | Player                                                | 모든 기능                                                       |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 지원                            | -                                                            | -                                                            | -                                                            | -                                                           | &#10003;                                                     | &#10003;                                                     |
| SDK 다운로드 | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=basicLive) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=interactivelive) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=shortVideo) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=video) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=player) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=allPart) |

다양한 버전의 SDK에 포함된 더 많은 기능은 [SDK 다운로드](https://cloud.tencent.com/document/product/1449/56978)를 참고하십시오.

## 프로젝트 주소[](id:sdkDownload)

iOS용 Tencent Cloud RT-Cube Superplayer의 프로젝트 주소는 [SuperPlayer_iOS](https://github.com/tencentyun/SuperPlayer_iOS)입니다.

## 타겟 오디언스

본 문서의 일부 내용은 Tencent Cloud의 독점적 기능이므로, 사용하기 전에 [Tencent Cloud](https://intl.cloud.tencent.com/) 관련 서비스를 활성화해 주십시오. 미등록 사용자는 [계정 등록](https://intl.cloud.tencent.com/login) 하시기 바랍니다.

## 통합[](id:guide)

이 프로젝트는 cocoapods를 통한 설치를 지원합니다. Podfile에 다음 코드만 추가하면 됩니다.

```ruby
pod 'SuperPlayer'
```

pod install 또는 pod update를 실행합니다.

### 플레이어 사용[](id:usePlayer)

플레이어의 메인 클래스는 `SuperPlayerView`로, 생성 후 비디오를 즉시 재생할 수 있습니다.

```objc
// 헤더 파일 삽입
#import <SuperPlayer/SuperPlayer.h>

// 플레이어 생성  
_playerView = [[SuperPlayerView alloc] init];
// 프록시 설정, 이벤트 수신에 사용
_playerView.delegate = self;
// 부모 View를 설정하면 _playerView가 자동으로 holderView 아래에 추가됩니다.
_playerView.fatherView = self.holderView;
```

```objc
//링크 도용 방지 비활성화
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// AppId 설정
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = "5285890799710670616"; // FileId 설정
[_playerView playWithModel:model];
```

```objc
//링크 도용 방지를 활성화하려면 Superplayer의 서명인 psign을 입력해야 합니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참고하십시오. https://cloud.tencent.com/document/product/266/42436
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppId 설정
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = "5285890799710173650"; // FileId 설정
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
```



코드를 실행하면 비디오가 휴대폰에서 재생되며, 인터페이스 대부분의 기능을 사용할 수 있음을 확인할 수 있습니다.

### FileId 선택[](id:FileId)

비디오 FileId는 일반적으로 비디오 업로드 후 서버에서 반환됩니다.

1. 클라이언트에서 비디오 배포 후 서버가 FileId를 클라이언트로 반환합니다.
2. 비디오가 서버에 업로드되면 업로드 확인 알림에 해당 FileId가 포함됩니다.

Tencent Cloud에 이미 파일이 존재하는 경우에는 [미디어 자산 관리](https://console.cloud.tencent.com/vod/media)에서 해당 파일을 찾아 FileId를 조회할 수 있습니다. 아래 이미지와 같이 ID는 FileId를 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b07b18356d680f156b9ae5fdb1e19f85.png)



### 타임스탬프 기능

길이가 긴 비디오 재생 시 타임스탬프를 통해 시청자의 관심 지점을 쉽게 찾을 수 있습니다. [미디어 파일 속성 변경](https://intl.cloud.tencent.com/document/product/266/37570) API를 사용하여 AddKeyFrameDescs.N 매개변수를 통해 비디오에 타임스탬프를 설정할 수 있습니다.

호출 후 플레이어 인터페이스에 새로운 요소가 추가됩니다.


### 작은 창 재생[](id:smallWindow)

작은 창 재생은 App의 Window에 일시 중단된 플레이어를 나타냅니다. 작은 창으로 재생하는 것은 매우 간단합니다. 적절한 위치에서 다음 코드를 호출하기만 하면 됩니다.

```objc
[SuperPlayerWindow sharedInstance].superPlayer = _playerView; // 작은 창에 표시할 플레이어 설정
[SuperPlayerWindow sharedInstance].backController = self;  // 반환된 view controller 설정
[[SuperPlayerWindow sharedInstance] show]; // 플로팅 디스플레이
```

<img src="https://qcloudimg.tencent-cloud.cn/raw/c5882ec8b3258a06174a9a2dd06dcbf4.png" width="350">

### 재생 종료[](id:exitPlayer)

플레이어가 필요하지 않은 경우 `resetPlayer`을 호출하여 플레이어 내부를 정리하고 메모리를 확보합니다.

```objc
[_playerView resetPlayer];
```

## 더 많은 기능[](id:morefeature)

전체 기능을 사용하려면 비디오 클라우드 툴 킷을 다운로드하거나 프로젝트 데모를 직접 실행하십시오.
<img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150">
