## 제품 개요

iOS용 Tencent Cloud RT-Cube Player 컴포넌트는 오픈 소스 Tencent Cloud 플레이어 컴포넌트입니다. 몇 줄의 코드로 Tencent Video와 유사한 강력한 재생 기능을 제공할 수 있습니다. 가로/세로 모드 전환, 해상도 선택, 제스처 및 작은 창 재생과 같은 기본 기능과 비디오 버퍼링, 소프트웨어/하드웨어 디코딩 전환 및 조정 가능한 속도 재생과 같은 특수 기능이 있습니다. 시스템 기본 플레이어보다 더 많은 형식을 지원하고 더 나은 호환성과 기능을 제공합니다. 또한 첫 번째 프레임 바로 재생과 저지연성의 장점을 보유하고 있으며 비디오 썸네일과 같은 고급 기능을 제공합니다.

플레이어 컴포넌트가 비즈니스의 개별 요구를 충족할 수 없고 특정 개발 경험이 있는 경우 [RT-Cube Player SDK](https://cloud.tencent.com/document/product/881/20216)를 통합하여 플레이어 인터페이스 및 재생 기능의 개발을 사용자 지정할 수 있습니다.

## 준비 작업
1. [VOD](https://cloud.tencent.com/product/vod)를 활성화합니다. 계정을 등록하지 않으셨다면 먼저 [회원 가입](https://cloud.tencent.com/login) 하십시오.
2. App Store에서 Xcode를 다운로드합니다. 이미 수행한 경우 이 단계를 건너뜁니다.
3. [Cocoapods 웹 사이트](https://cocoapods.org/)의 가이드에 따라 Cocoapods를 다운로드하여 설치합니다. 이미 수행한 경우 이 단계를 건너뜁니다.

## 내용 요약
- [iOS용 Tencent Cloud RT-Cube Player 컴포넌트를 통합하는 방법](#step1)
- [플레이어 생성 및 사용 방법](#step3)

## 통합 준비
[](id:step1)
### 1단계: 프로젝트 다운로드
iOS용 Tencent Cloud RT-Cube Player는 [LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_iOS)에서 다운로드할 수 있습니다.

iOS용 Tencent Cloud RT-Cube Player 컴포넌트는 **[플레이어 컴포넌트 ZIP 패키지 다운로드](#zip)** 또는 **[Git 명령 실행](#git)**을 통해 다운로드할 수 있습니다.
<dx-tabs>
::: 플레이어 구성 요소 ZIP 패키지 다운로드[](id:zip)
**Code** > **Download ZIP**을 클릭하여 플레이어 컴포넌트 ZIP 패키지를 직접 다운로드할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Git 명령 실행[](id:git)
1. 먼저 컴퓨터에 Git이 설치되어 있는지 확인하십시오. 그렇지 않은 경우 [Git 설치 튜토리얼](https://git-scm.com/downloads)을 참고하여 설치할 수 있습니다.
2. 다음 명령을 실행하여 Player 컴포넌트 프로젝트의 코드를 로컬 시스템에 clone합니다.
```shell
git clone git@github.com:tencentyun/SuperPlayer_iOS.git
```
   다음 정보가 표시되면 프로젝트 코드가 로컬 시스템에 성공적으로 clone된 것입니다.
```shell
'SuperPlayer_iOS'에 복제 중...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
객체 수신 중: 100% (2637/2637), 571.20 MiB | 3.94 MiB/s, 완료.
delta 처리 중: 100% (1019/1019), 완료.
```
프로젝트 다운로드 후 프로젝트 소스 코드 압축 해제 후 생성되는 디렉터리는 다음과 같습니다.
<table>
<thead><tr><th>파일 이름</th><th>설명</th></tr></thead>
<tbody>
<tr><td>SDK</td>
<td>플레이어의 framework 정적 라이브러리 저장</td>
</tr><tr>
<td>Demo</td><td>Superplayer Demo 저장</td>
</tr><tr>
<td>App</td><td>프로그램 엔트리 UI</td>
</tr><tr>
<td>SuperPlayerDemo</td><td>Superplayer Demo</td>
</tr><tr><td>SuperPlayerKit</td><td>Superplayer 컴포넌트</td>
</tr></tbody></table>
:::
</dx-tabs>

[](id:step2)
### 2단계: 프로젝트 통합
이 단계에서는 플레이어를 통합하는 방법을 설명합니다. **[Cocoapods를 통해 통합](#cocoapods)**하거나 **[SDK 수동 다운로드](#manual)**한 다음 현재 프로젝트로 가져오기 하는 것이 좋습니다.
<dx-tabs>
::: Cocoapods를 통한 통합[](id:cocoapods)
1. 이 프로젝트는 Cocoapods를 통한 설치를 지원합니다. Podfile에 다음 코드만 추가하면 됩니다.
(1) Pod 모드로 SuperPlayer를 직접 통합
```objective-c
pod 'SuperPlayer
```
  Player 버전에 종속해야 하는 경우 podfile에 다음 종속성을 추가할 수 있습니다.
```objective-c
pod 'SuperPlayer/Player'
```
  프로 버전에 종속해야 하는 경우 podfile 파일에 다음 종속성을 추가할 수 있습니다.
```objective-c
pod 'SuperPlayer/Professional'
```

2. `pod install` 또는 `pod update`를 실행합니다.

:::
::: 수동 SDK 다운로드[](id:manual)
1. SDK + Demo 패키지를 다운로드하십시오. iOS용 Tencent Cloud RT-Cube Player는 [LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_iOS)에서 다운로드할 수 있습니다.
2. `TXLiteAVSDK_Player.framework`를 프로젝트로 가져오고 `Do Not Embed`를 선택합니다.
3. Demo/TXLiteAVDemo/SuperPlayerKit/SuperPlayer를 자신의 프로젝트 디렉터리에 복사합니다.
4. SuperPlayer는 AFNetworking, SDWebImage, Masonry, TXLiteAVSDK_Player를 포함한 타사 라이브러리에 의존합니다.
 1. TXLiteAVSDK_Player를 수동으로 통합하는 경우 필요한 시스템 라이브러리 및 library를 추가해야 합니다.
<b>시스템 Framework 라이브러리</b>: MetalKit, ReplayKit, SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, MobileCoreServices, VideoToolbox
<b>시스템 Library:</b> libz, libresolv,  libiconv, libc++, libsqlite3
구체적인 작업 단계 [참고](https://cloud.tencent.com/document/product/266/73872): 사용자 정의 개발 - VOD 시나리오 - 문서 액세스 - SDK 통합 1단계 - 수동 SDK 통합
또한 다음 이미지와 같이 TXLiteAVSDK_Player 파일 아래에 TXFFmpeg.xcframework 및 TXSoundTouch.scframework를 동적 라이브러리로 추가해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5834caae21d3413522c7d51d4b3b57b0.png)
 2. TXLiteAVSDK_Player를 Pod로 통합하면 라이브러리를 추가할 필요가 없습니다.


:::
</dx-tabs>

[](id:step3)
### 3단계: 플레이어 기능 사용
이 단계에서는 플레이어를 만들고 비디오 재생에 사용하는 방법을 설명합니다.

1. **플레이어 생성:**[](id:usePlayer)
플레이어의 메인 클래스는 `SuperPlayerView`이며, 비디오를 생성한 후 재생할 수 있습니다.
```xml
// 헤더 파일 삽입
#import <SuperPlayer/SuperPlayer.h>

// 플레이어 생성  
_playerView = [[SuperPlayerView alloc] init];
// 프록시 설정, 이벤트 수신에 사용
_playerView.delegate = self;
// 부모 View를 설정하면 _playerView가 자동으로 holderView 아래에 추가됩니다.
_playerView.fatherView = self.holderView;
```


2.  **비디오 재생:**
이 단계에서는 비디오를 재생하는 방법을 설명합니다. iOS용 Tencent Cloud RT-Cube Player 컴포넌트는 [VOD FileId](#fileid) 또는 [URL](#url)의 FileId를 통한 재생을 지원합니다. 완전한 기능을 사용하려면 **FileId를 통합**하는 것이 좋습니다.
<dx-tabs>
::: VOD에서 FileId를 통한 재생[](id:fileid)
비디오 FileId는 일반적으로 비디오 업로딩 후 서버에서 반환됩니다.

1. 클라이언트에서 비디오 배포 후 서버가 FileId를 클라이언트로 반환합니다.
2. 서버에서 비디오 업로드 시, 해당 FileId가 [업로드 확인](https://cloud.tencent.com/document/product/266/9757) 공지에 포함됩니다.
Tencent Cloud에 이미 파일이 존재하는 경우에는 [미디어 자산 관리](https://console.cloud.tencent.com/vod/media)에서 해당 파일을 찾아 FileId를 조회할 수 있습니다. 아래 이미지와 같이 ID는 FileId를 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
<dx-alert infotype="notice">
<li>FileId를 통해 재생하려면 먼저 Adaptive-HLS(10) 트랜스 코딩 템플릿을 사용하여 비디오를 트랜스 코딩하거나 Player 컴포넌트 서명 psign을 사용하여 재생할 비디오를 지정해야 합니다. 그렇지 않으면 비디오가 재생되지 않을 수 있습니다. 비디오를 트랜스 코딩하는 방법에 대한 자세한 내용은 [Player로 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38098)을 참고하십시오. psign을 생성하는 방법에 대한 자세한 내용은 [Player 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오.</li>
<li>FileId를 통한 재생 중 ‘no v4 play info’ 예외가 발생하면 위와 같은 문제가 있을 수 있습니다. 이 경우 상기 지침에 따라 조정하는 것이 좋습니다. [URL](#url)을 통해 재생할 원본 비디오의 재생 링크를 직접 얻을 수도 있습니다.</li>
<li>**트랜스 코딩되지 않은 원본 비디오는 재생 중에 호환성 문제가 발생할 수 있으므로 재생을 위해 비디오를 트랜스 코딩하는 것이 좋습니다.**</li></dx-alert>

<dx-codeblock>
:::  java
//링크 도용 방지가 비활성화된 재생 중에 ‘no v4 play info’ 예외가 발생하면 Adaptive-HLS(10) 트랜스 코딩 템플릿을 사용하여 비디오를 트랜스 코딩하거나 URL을 통해 재생할 원본 비디오의 재생 링크를 직접 가져오는 것이 좋습니다.

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppId 설정
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // FileId 설정
//비공개 암호화 재생을 위해서는 Player 컴포넌트의 서명인 psign을 입력해야 합니다. 서명 및 생성 방법에 관한 내용은 다음 링크를 참고하십시오. https://intl.cloud.tencent.com/document/product/266/38099
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
:::
</dx-codeblock>
:::
::: URL을 통한 재생[](id:url)
```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.videoURL = @"http://your_video_url.mp4";   // 재생할 동영상의 url 구성
[_playerView playWithModel:model];
```
:::
</dx-tabs>
- **재생 종료:**[](id:exitPlayer)
플레이어가 더 이상 필요하지 않으면 `resetPlayer`를 호출하여 플레이어의 내부 상태를 지우고 메모리를 확보하십시오.
```java
[_playerView resetPlayer];
```

이제 iOS용 Tencent Cloud RT-Cube Player 컴포넌트의 생성, 비디오 재생 및 재생 종료 기능 통합이 완료되었습니다.

[](id:moreFeature)
## 기능 사용[](id:moreFeature)

### 1. 전체 화면 재생

Player 컴포넌트는 제스처, 화면 댓글, 화면 캡처 및 해상도 전환을 통해 화면 잠금, 볼륨 및 밝기 제어를 설정할 수 있는 전체 화면 재생을 지원합니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Player 컴포넌트**에서 체험해볼 수 있으며, 전체 화면 아이콘을 탭하면 **전체 화면** 재생 모드로 이동할 수 있습니다.



창 재생 모드에서 다음 API를 호출하여 전체 화면 재생 모드로 들어갈 수 있습니다.

```objective-c
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player {
  //여기에서 전체 화면 모드로 전환한 후 로직 사용자 정의 가능
}
```

#### 


<dx-tabs>
::: 창 모드로 돌아가기[](id:window)
**Back**을 눌러 창 재생 모드로 돌아갑니다. SDK가 전체 화면 모드로 전환하는 로직 처리 후 트리거되는 프록시 메소드는 다음과 같습니다.

```objective-c
// 이벤트 반환
- (void)superPlayerBackAction:(SuperPlayerView *)player;
왼쪽 상단 모서리에서 Back을 탭하여 트리거
// 전체 화면 변경 알림
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player;
```
:::
::: 화면 잠금[](id:screenlock)
화면 잠금 작동은 몰입형 재생 상태를 가능하게 합니다. 버튼을 탭한 후 콜백 없이 SDK에서 처리됩니다.

```objective-c
// 화면 잠금 여부를 제어하기 위해 다음 API 호출 가능
@property(nonatomic, assign) BOOL isLockScreen;
```
:::
::: 댓글 자막[](id:barrage)
댓글 자막 기능이 활성화되면 사용자가 보낸 텍스트 댓글이 화면에 표시됩니다.

여기에서 SPDefaultControlView 객체를 가져오고 플레이어 view 초기화 중에 SPDefaultControlView의 댓글 자막 버튼에 대한 이벤트를 설정합니다. 화면 상의 댓글 내용과 view를 사용자 정의해야 합니다. 자세한 내용은 SuperPlayerDemo에서 CFDanmakuView, CFDanmakuInfo 및 CFDanmaku를 참고하십시오.

```objective-c
SPDefaultControlView *dv = (SPDefaultControlView *)**self**.playerView.controlView;
[dv.danmakuBtn addTarget:**self** action:**@selector**(danmakuShow:) forControlEvents:UIControlEventTouchUpInside];
```

CFDanmakuView: 초기화 중 댓글 자막의 속성을 구성합니다.

```objective-c
// 다음 속성이 필요합니다--------
// 댓글 자막 이모티콘 지속 시간
@property(nonatomic, assign) CGFloat duration;
// 화면에 댓글 자막 이모티콘의 지속시간 표시
@property(nonatomic, assign) CGFloat centerDuration;
// 댓글 자막 줄 높이
@property(nonatomic, assign) CGFloat lineHeight;
// 댓글 자막 줄 사이의 간격
@property(nonatomic, assign) CGFloat lineMargin;

// 댓글 자막의 최대 줄 수
@property(nonatomic, assign) NSInteger maxShowLineCount;

// 댓글 자막 중앙 위/아래의 최대 줄 수
@property(nonatomic, assign) NSInteger maxCenterLineCount;
```
:::
::: 화면 캡처[](id:screenshot)
Player 컴포넌트는 재생 중 현재 비디오 프레임을 캡처하는 기능을 제공하며 공유를 위해 스크린샷을 저장할 수 있습니다. Screencapture 버튼을 탭하면 화면 캡처 성공 또는 실패에 대한 콜백 없이 SDK에서 내부적으로 처리되며 캡처된 스크린샷의 폴더는 휴대폰 사진첩입니다.
:::
::: 해상도 전환[](id:resolution)
HD, SD 및 FHD와 같은 다양한 비디오 재생 해상도를 필요에 따라 선택할 수 있습니다. 버튼을 탭한 후 해상도 표시 view가 트리거되고 해상도 옵션은 콜백 없이 SDK에서 내부적으로 처리됩니다.
:::
</dx-tabs>


### 2. 플로팅 창 재생

Player 컴포넌트는 작은 플로팅 창 재생을 지원하므로 사용자가 비디오 재생을 중단하지 않고 다른 앱으로 전환할 수 있습니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Player 컴포넌트**에서 왼쪽 상단의 **Back**을 눌러 사용해 볼 수 있습니다.



```objective-c
// 세로 모드에서 재생하는 동안 Back 버튼을 탭하면 API가 트리거 됨
[SuperPlayerWindowShared setSuperPlayer:self.playerView];
[SuperPlayerWindowShared show];
// 메인 창으로 돌아가기 위해 플로팅 창을 탭하여 트리거되는 API
SuperPlayerWindowShared.backController = self;
```

### 3. 비디오 썸네일

Player 컴포넌트는 첫 번째 비디오 프레임을 재생 콜백 수신 이전에 표시할 비디오 썸네일의 사용자 정의를 지원합니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode)> **Player** > **Player 컴포넌트** > **썸네일 사용자 정의 데모**에서 사용해 볼 수 있습니다.

* Player 컴포넌트가 자동 재생 모드 `PLAY_ACTION_AUTO_PLAY`로 설정되면 비디오가 자동으로 재생되고 첫 번째 비디오 프레임이 로딩되기 전에 미리보기 이미지가 표시됩니다.
* Player 컴포넌트가 수동 재생 모드 `PLAY_ACTION_MANUAL_PLAY`로 설정된 경우 사용자가 **재생**을 탭한 후에만 비디오 재생이 시작됩니다. 썸네일은 첫 번째 비디오 프레임이 로딩될 때까지 표시됩니다.

비디오 썸네일은 아래 지침에 따라 URL 또는 로컬 File 주소 사용을 지원합니다. FileID를 통해 비디오를 재생하면 VOD에서 비디오 썸네일을 직접 구성할 수 있습니다.

```objective-c
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1400329071;
model.videoId = videoId;
//자동 PLAY_ACTION_AUTO_PLAY 또는 수동 PLAY_ACTION_MANUAL_PLAY로 설정할 수 있는 재생 모드
model.action  = PLAY_ACTION_MANUAL_PLAY; 
//썸네일 url을 설정합니다. coverPictureUrl이 설정되지 않은 경우 VOD 콘솔에서 구성한 썸네일이 자동으로 사용됩니다.
model.customCoverImageUrl = @"http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png"; 
[self.playerView playWithModel:model] 
```

### 4. 비디오 목록 루프

Player 컴포넌트는 비디오 목록 루프를 지원합니다. 즉, 비디오 목록이 제공된 후:

* 목록에 있는 비디오는 반복 재생될 수 있습니다. 다음 비디오는 자동으로 재생되거나 재생 중에 수동으로 전환될 수 있습니다.
* 목록의 마지막 비디오가 끝난 후 목록의 첫 번째 비디오가 자동으로 시작됩니다.

이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Player 컴포넌트** > **비디오 목록 루프 데모**에서 사용해 볼 수 있습니다.



```objective-c
//1단계: 루프 데이터를 위한 NSMutableArray 생성
NSMutableArray *modelArray = [NSMutableArray array];
SuperPlayerModel *model = [SuperPlayerModel new];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1252463788;
model.videoId = videoId;
[modelArray addObject:model];

model = [SuperPlayerModel new];
videoId = [SuperPlayerVideoId new];
videoId.fileId = @"4564972819219071679";
model.appId = 1252463788;
model.videoId = videoId;
[modelArray addObject:model];

//2단계: SuperPlayerView의 루프 API 호출
[self.playerView playWithModelList:modelArray isLoopPlayList:YES startIndex:0];
```

```objective-c
(void)playWithModelList:(NSArray *)playModelList isLoopPlayList:(BOOL)isLoop startIndex:(NSInteger)index;
```

API 매개변수 설명

| 매개변수           | 유형        | 설명        |
| ------------- | --------- | --------- |
| playModelList | NSArray * | 루프 데이터 목록    |
| isLoop        | Boolean   | 루프 여부      |
| index         | NSInteger | 재생을 시작할 비디오의 인덱스 |


### 5. PIP(Picture-in-Picture) 기능

PIP(Picture-in-Picture)는 iOS 9에서 출시되었지만 기존에는 iPad에서만 사용할 수 있었고, iPhone에서 PIP를 사용하려면 iOS 14로 업데이트해야 합니다.
현재 Tencent Cloud Player는 애플리케이션내/외 PIP(picture-in-picture) 기능을 지원할 수 있어 사용자의 요구를 크게 만족시킵니다. 사용하기 전에 백그라운드 모드를 활성화해야 합니다. 단계는 다음과 같습니다. XCode는 해당 Target -> Signing & Capabilities -> Background Modes를 선택하고 ‘Audio, AirPlay, and Picture in Picture’를 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png)



PIP 기능을 사용하는 코드 예시:																								

```objective-c
// PIP 입력
 if (![TXVodPlayer isSupportPictureInPicture]) {
    return;
 }
 [_vodPlayer enterPictureInPicture];

// PIP 종료
[_vodPlayer exitPictureInPicture];
```

### 6. 비디오 미리보기

Player 컴포넌트는 비VIP 회원 미리보기에 적합한 비디오 미리보기 기능을 지원합니다. 비디오 미리보기 지속 시간, 프롬프트 메시지 및 미리보기 최종 화면을 제어하기 위해 다른 매개변수를 전달할 수 있습니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Player 컴포넌트** > **미리보기 기능 데모**에서 사용해 볼 수 있습니다.



```objective-c
 //1단계: 미리보기 model 생성
 TXVipWatchModel *model = [[TXVipWatchModel alloc] init];
 model.tipTtitle = @"15초 동안 미리 보고 VIP 멤버십을 활성화하면 전체 비디오를 볼 수 있습니다";
 model.canWatchTime = 15;
 //2단계: 미리보기 model 설정
 self.playerView.vipWatchModel = model;
 //3단계: 미리보기 기능을 표시하는 메소드 호출
 [self.playerView showVipTipView];
```

  TXVipWatchModel 클래스 매개변수 설명:

| 매개변수          | 유형       | 설명        |
| ------------ | -------- | --------- |
| tipTtitle    | NSString | 프롬프트 메시지 미리보기    |
| canWatchTime | float    | 초 단위의 미리보기 지속 시간 |

### 7. 동적 워터마크

Player 컴포넌트를 사용하면 무단 녹화를 방지하기 위해 재생 화면에 불규칙하게 움직이는 텍스트 워터마크를 추가할 수 있습니다. 워터마크는 전체 화면 재생 모드와 창 재생 모드에서 모두 표시할 수 있습니다. 워터마크 텍스트, 크기 및 색상을 수정할 수 있습니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Player 컴포넌트** > **동적 워터마크 데모**에서 사용해 볼 수 있습니다.



```objective-c
//1단계: 비디오 소스 정보 model 생성
SuperPlayerModel *  playermodel   = [SuperPlayerModel new];
//비디오 소스의 다른 정보 추가
//2단계: 동적 워터마크 model 생성
DynamicWaterModel *model = [[DynamicWaterModel alloc] init];
//3단계: 동적 워터마크 데이터 설정
model.dynamicWatermarkTip = @"shipinyun";
model.textFont = 30;
model.textColor = [UIColor colorWithRed:255.0/255.0 green:255.0/255.0 blue:255.0/255.0 alpha:0.8];
playermodel.dynamicWaterModel = model;
//4단계: 동적 워터마크를 표시하는 메소드 호출
[self.playerView playWithModel:playermodel];
```

DynamicWaterModel 클래스 매개변수 설명:

| 매개변수                 | 유형       | 설명     |
| ------------------- | -------- | ------ |
| dynamicWatermarkTip | NSString | 워터마크 텍스트 정보 |
| textFont            | CGFloat  | 텍스트 크기   |
| textColor           | UIColor  | 텍스트 색상   |

## Demo 체험

더 많은 기능을 사용하려면 프로젝트 Demo를 직접 실행하거나 QR 코드를 스캔하여 Tencent Cloud RT-Cube App Demo를 다운로드할 수 있습니다.

### 프로젝트 Demo 실행

1. Demo 디렉터리에서 `pod update` 명령을 실행하여 `TXLiteAVDemo.xcworkspace` 파일을 다시 생성합니다.
2. 더블 클릭하여 프로젝트를 열고 인증서를 수정하고 실제 장치에서 프로젝트를 실행합니다.
3. Demo를 성공적으로 실행한 후 **Player** > **Player 컴포넌트**로 이동하여 플레이어 기능을 사용해 보십시오.

[](id:qrcode)
### Tencent Cloud RT-Cube App

**Tencent Cloud RT-Cube App** > **Player**에서 Player 컴포넌트의 더 많은 기능을 사용해 볼 수 있습니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/5c383bc7826d4f4835c9a7232cf9b50e.png" width="150">
