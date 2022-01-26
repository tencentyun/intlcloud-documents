본문은 멀티미디어 플랫폼의 일반적인 긴 비디오 재생 시나리오에 대한 Superplayer 재생의 긴 비디오 튜토리얼을 제공합니다. 사용자는 어댑티브 비트레이트 스트리밍, 비디오 썸네일 미리보기, 비디오 키 프레임 정보를 추가하면서 Web, iOS, Android 플레이어에서 비디오를 재생하는 방법을 익힐 수 있습니다.

## 학습 목표
이 단계의 튜토리얼을 통해 다음을 학습하게 됩니다.
- VOD에서 클라우드에서 어댑티브 비트레이트 스트리밍 전송(플레이어는 현재 대역폭에 따라 재생에 가장 적합한 비트 레이트를 동적으로 선택)
- VOD에서 비디오 키 프레임 정보 설정 방법
- VOD에서 스프라이트 이미지를 사용하여 썸네일을 만드는 방법
- 플레이어를 사용하여 재생하는 방법

읽기 전, VOD fileid의 개념을 이해하기 위해 Superplayer 가이드의 [1단계: Superplayer로 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38098) 섹션을 학습하십시오.

## 작업 단계
### 1단계: 어댑티브 비트레이트 스트리밍 및 스프라이트 이미지 변환
이 단계에서는 비디오를 어댑티브 비트레이트 스트리밍 및 스프라이트 이미지로 변환하는 방법을 소개합니다.
1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하여 **비디오 처리 설정**>**템플릿 설정**>**어댑티브 비트레이트 스트리밍 템플릿**을 선택합니다. **어댑티브 비트레이트 스트리밍 템플릿 변환 생성**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e941daca088dbf5ca8a40384fc3ade7f.png)
템플릿을 통해 사용자에게 필요한 어댑티브 비트레이트 스트리밍을 생성합니다. 본문에서는 480p, 720p 및 1080p 해상도의 3개의 서브 스트림을 포함하는 testAdaptive라는 이름의 어댑티브 비트레이트 스트리밍 템플릿을 생성합니다. 비디오 비트 레이트, 비디오 프레임 레이트 및 오디오 비트 레이트는 원본 비디오와 동일하게 유지됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/21ee0dba1c79bde7bea922188d8f5b28.png)
2. **비디오 처리 설정**>**템플릿 설정**>**화면 캡처 템플릿**을 선택하고 **화면 캡처 템플릿 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8bac06234f924cc2d9327b6e9791157d.png)
템플릿을 통해 사용자가 필요로 하는 스프라이트 이미지를 생성합니다. 본문에서는 샘플링 간격 5%, 작은 이미지의 행 수: 10, 작은 이미지의 열 수: 10의 testSprite라는 이름의 스프라이트 이미지 템플릿을 생성합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)
3. 태스크 플로우를 통해 어댑티브 비트레이트 스트리밍 템플릿과 스프라이트 이미지 템플릿을 추가합니다.
**비디오 처리 설정**>**태스크 플로우 설정**>**태스크 플로우 생성**을 선택하고 **태스크 플로우 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bc6e4fcd4e53b050fa5f6d59d83608c8.png)
작업 태스크 플로우를 통해 사용자가 처리할 작업을 추가합니다. 어댑티브 비트레이트 스트리밍을 재생하는 과정을 보여주기 위해 본 문에서는 testPlayVideo 태스크 플로우를 생성합니다. 태스크 플로우는 어댑티브 비트레이트 스트리밍 템플릿과 스프라이트 이미지 템플릿만 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/29ebf8e33157e9c342848c8f1c54ce6d.png)
4. **미디어 자산 관리**>**멀티미디어 관리**를 선택하여 처리할 비디오를 선택하고 **비디오 처리**>**어댑티브 비트레이트 스트리밍**>**태스크 플로우 선택**을 클릭하여 작업을 시작합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/31392ed275f4406b73ceb2d3c866e3ad.png)
5. **멀티미디어 관리**>**작업**>**관리**에서 처리된 작업 결과를 얻을 수 있습니다.

### 2단계: 비디오 키 프레임 정보 추가
이 단계에서는 새로운 비디오 키 프레임 정보 세트를 추가하는 방법을 안내합니다.
1. 클라우드 VOD 서버 API 문서>**미디어 자산 관리 관련 인터페이스**>[**미디어 파일 속성 수정**](https://intl.cloud.tencent.com/document/product/266/37570)으로 이동하여 디버깅을 클릭하고 클라우드 API 콘솔로 이동하여 디버깅 진행합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/69cc5e88d5858b25e6a21e59082c946a.png)
2. 매개변수 이름 **AddKeyFrameDescs.N**을 통해 지정된 비디오 키 프레임 정보 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/85eb2701162edf90c309d161af2bff99.png)
이렇게 클라우드에서의 작업이 완료되었습니다. VOD로 어댑티브 비트레이트 스트리밍을 전송했으며 비디오 스프라이트 이미지 및 관련 비디오 키 프레임 정보가 추가되었습니다.

### 3단계: 플레이어 통합
이 단계에서는 Web, iOS 및 Android 플레이어에서 어댑티브 비트레이트 스트리밍을 재생하고 썸네일 및 키 프레임 정보를 추가하는 방법을 안내합니다.

<dx-tabs>
::: Web
RT-Cube Superplayer를 통합하려면 [통합 가이드](https://intl.cloud.tencent.com/document/product/266/33976)를 참고하십시오. 플레이어 SDK 파일을 불러온 후 **미디어 자산 관리**를 이용하여 업로드 미디어 자산의 appId와 fileId를 추출하여 재생할 수 있습니다.

플레이어 구축 메소드는 'TCPlayer'이며, 플레이어의 인스턴스를 생성하여 재생할 수 있습니다.

#### 1. html 파일에 플레이어 컨테이너 배치

플레이어를 표시할 페이지에 플레이어 컨테이너를 추가합니다. 예를 들어 index.html에 다음 코드를 추가합니다(컨테이너 ID와 너비 및 높이를 사용자 지정할 수 있음).

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

#### 2. fileID로 재생

index.html 페이지의 초기화 코드에 다음 초기화 스크립트를 추가하고 획득한 fileID와 appID를 입력하여 재생합니다.

```
var player = TCPlayer('player-container-id', { // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 함
    fileID: '5285890799710670616', // 재생할 비디오의 fileID 입력(필수)
    appID: '1400329073' // VOD 계정의 appID 입력(필수)
});
```


:::
::: iOS
RT-Cube Superplayer를 통합하려면 [통합 가이드](https://intl.cloud.tencent.com/document/product/266/33976)를 참고하십시오. 통합 후 **미디어 자산 관리**를 이용하여 업로드 미디어 자산의 appId와 fileId를 추출하여 재생할 수 있습니다.

플레이어의 메인 클래스는 `SuperPlayerView`로, 생성 후 즉시 비디오를 재생할 수 있습니다.

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

#### fileId로 재생

```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// AppId 설정
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710670616"; // FileId 설정
[_playerView playWithModel:model];
```
:::
::: Android
RT-Cube Superplayer를 통합하려면 [통합 가이드](https://intl.cloud.tencent.com/document/product/266/33976)를 참고하십시오. 통합 후 **미디어 자산 관리**를 이용하여 업로드 미디어 자산의 appId와 fileId를 추출하여 재생할 수 있습니다.

플레이어의 메인 클래스는 `SuperPlayerView`로, 생성 후 즉시 비디오를 재생할 수 있습니다.

#### 1. 레이아웃 파일에 SuperPlayerView 생성

```xml
<!-- Superplayer-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. fileId로 재생

```java
//레이아웃 파일에 SuperPlayerView 삽입 후 인스턴스 생성
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);
//링크 도용 방지 비활성화
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppId 설정
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // FileId 설정
mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## 결론

상기와 같이 플레이어에서 스프라이트 이미지 미리 보기, 비디오 키 프레임 정보 및 동적 어댑티브 비트레이트 스트리밍을 자동으로 전환할 수 있습니다. 더 많은 기능은 [기능 설명](https://intl.cloud.tencent.com/document/product/266/42965)을 참고하십시오.
