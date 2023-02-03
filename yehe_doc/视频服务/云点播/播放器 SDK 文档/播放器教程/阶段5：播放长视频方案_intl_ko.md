본문은 플레이어를 사용하여 오디오/비디오 플랫폼에서 일반적인 긴 비디오를 재생하는 방법을 설명합니다.  Web, iOS 및 Android 버전의 플레이어를 다루고 KEY [링크 도용 방지](https://cloud.tencent.com/document/product/266/78306), 어댑티브 비트레이트 스트리밍, 비디오 썸네일 미리 보기 및 비디오 타임스탬프 기능에 대해 자세히 설명합니다.

## 학습 목표
이 문서를 읽고 나면 다음을 알 수 있습니다.
- 유효 기간, 시청자 수, 재생 시간 등을 설정할 수 있는 KEY 링크 도용 방지 구성 방법
- VOD에서 클라우드에서 어댑티브 비트스트림을 출력하는 방법(플레이어는 현재 대역폭에 따라 재생에 가장 적합한 비트 레이트를 동적으로 선택할 수 있음)
- 비디오 타임스탬프를 설정하는 방법
- VOD에서 이미지 스프라이트를 썸네일로 사용하는 방법
- 플레이어 사용법

읽기 전, VOD fileid의 개념을 이해하기 위해 Player 가이드의 [1단계: Player로 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38098) 섹션을 학습하십시오.

## 작업 단계
### 1단계: KEY 링크 도용 방지 활성화
아래 예시는 계정 아래의 기본 배포 도메인에 대한 KEY 링크 도용 방지를 활성화하는 방법을 보여줍니다.
>!프로덕션 환경에서 도메인 이름에 대한 링크 도용 방지를 직접 활성화하지 마십시오. 그렇지 않으면 프로덕션 환경에서 비디오 재생이 실패할 수 있습니다.

1. VOD 콘솔에 로그인하여 [배포 및 재생]>[[도메인 이름]](https://console.cloud.tencent.com/vod/distribute-play/domain)을 선택하고 설정 페이지로 이동합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pyHf434_1.png" width="900" />

2. ‘액세스 제어’ 탭을 클릭하고 [Key 링크 도용 방지]를 찾은 다음 회색 버튼을 클릭하여 활성화하고 팝업 창에서 [생성]을 클릭하여 임의의 Key를 생성한 다음 [확인]을 클릭하여 구성을 저장하고 적용합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/azQ5558_2.jpg" width="722" />

### 2단계: 어댑티브 비트스트림 및 스프라이트 이미지 변환
이 단계에서는 비디오를 어댑티브 비트스트림 및 스프라이트 이미지로 변환하는 방법을 소개합니다.
1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하여 **비디오 처리 설정**>**템플릿 설정**>**어댑티브 비트레이트 스트리밍 템플릿**을 선택합니다. **템플릿 생성**을 클릭합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3gkP770_3.png" style="zoom:67%;" />

필요에 따라 템플릿을 통해 어댑티브 비트스트림을 생성합니다. 본문에서는 480p, 720p 및 1080p 해상도의 3개의 서브 스트림을 포함하는 testAdaptive라는 이름의 어댑티브 비트레이트 스트리밍 템플릿을 보여줍니다 비디오 비트 레이트, 비디오 프레임 레이트 및 오디오 비트 레이트는 원본 비디오와 동일하게 유지됩니다.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/XIga303_4.jpg)

2. **비디오 처리 설정**>**템플릿 설정**>**스크린샷 템플릿**을 선택하고 **스크린샷 템플릿 생성**을 클릭합니다.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/mVrf686_5.png)

템플릿을 통해 사용자가 필요로 하는 스프라이트 이미지를 생성합니다. 본문에서는 샘플링 간격 5%, 작은 이미지의 행 수: 10, 작은 이미지의 열 수: 10의 testSprite라는 이름의 스프라이트 이미지 템플릿을 생성합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)

3. 태스크 플로우를 통해 어댑티브 비트레이트 스트리밍 템플릿과 스프라이트 이미지 템플릿을 추가합니다.
**비디오 처리**>**태스크 플로우 설정**을 선택하고 **태스크 플로우 생성**을 클릭합니다.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/sUGF476_7.jpg)

작업 태스크 플로우를 통해 사용자가 처리할 작업을 추가합니다. 어댑티브 비트레이트 스트리밍을 재생하는 과정을 보여주기 위해 본 문에서는 testPlayVideo 태스크 플로우를 생성합니다. 태스크 플로우는 어댑티브 비트레이트 스트리밍 템플릿과 스프라이트 이미지 템플릿만 추가합니다.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e45517_8.jpg)

4. **미디어 자산**>**오디오/비디오 관리**를 선택하고 대상 비디오(FileId: 387xxxxx8142975036)를 선택한 다음 **태스크 플로우**를 클릭하고 태스크 플로우 템플릿을 선택하여 작업을 시작합니다.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LAPx726_9.png)

5. 이 때 **작업 관리**>[**오디오/비디오 관리**](https://console.cloud.tencent.com/vod/task) 페이지에서 작업 실행 상태를 확인하고 완료 후 작업 결과를 확인할 수 있습니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/wrMs396_10.jpg" width="900" />

### 3단계: 비디오 타임스탬프 추가
이 단계에서는 새로운 비디오 타임스탬프 세트를 추가하는 방법을 안내합니다.
1. VOD 서버 API>**미디어 자산 관리 API**>[**ModifyMediaInfo**](https://intl.cloud.tencent.com/document/product/266/37570)로 이동하여 디버그를 클릭하여 디버깅을 위해 TencentCloud API 콘솔로 들어갑니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3hHA645_11.jpg)
2.**AddKeyFrameDescs.N** 매개변수를 통해 지정된 비디오 타임스탬프를 추가합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dpvW350_12.jpg)
이렇게 클라우드에서 작업을 완료하고 어댑티브 비트스트림 및 이미지 스프라이트를 출력하고 비디오 타임스탬프를 추가했습니다.

### 4단계: Player 서명 생성
이 단계에서는 서명 툴을 사용하여 플레이어가 비디오를 재생할 서명을 빠르게 생성할 수 있습니다.
**배포 및 재생**>[**플레이어 서명 툴**](https://console.cloud.tencent.com/vod/distribute-play/signature)을 선택하고 다음 정보를 입력합니다.
 - **비디오 fileId**: **2단계**에서 사용한 FileId(387xxxxx8142975036)를 입력합니다.
 - **서명 만료 시간**: 플레이어 서명 만료 시간을 입력합니다. 비워두면 서명이 만료되지 않습니다.
 - **재생 가능한 비디오 유형**: **암호화되지 않은 어댑티브 비트레이트**를 선택합니다.
 - **재생 가능한 어댑티브 비트레이트 스트리밍 템플릿**: `testAdaptive (1429229)`을 선택합니다.
 - **썸네일 미리보기용 이미지 스프라이트 템플릿**: `testSprite (131353)`을 선택합니다.
 - **링크 도용 방지 및 암호화**: 토글을 켜고 다음과 같이 구성합니다.
  - **링크 만료 시간**: 획득한 링크 도용 방지 서명의 만료 시간으로 설정합니다.
  - **최대 재생 IP 수**: 재생 가능한 최대 IP 수를 설정합니다.

**생성**을 클릭하여 서명 문자열을 가져옵니다.




### 5단계: 플레이어 통합
4단계 후에는 비디오 재생에 필요한 세 가지 매개변수인 `appId`, `fileId` 및 `psign`(플레이어 서명)을 얻었습니다.
이 단계에서는 Web, iOS 및 Android 플레이어에서 어댑티브 비트스트림, 썸네일 및 타임스탬프를 재생하는 방법을 설명합니다.

<dx-tabs>
::: Web
[통합 가이드](https://intl.cloud.tencent.com/document/product/266/33977)의 안내에 따라 RT-Cube Player를 통합해야 합니다. 플레이어의 SDK 파일을 가져온 후 `appId`, `fileId` 및 `psign`(플레이어 서명)을 사용하여 동영상을 재생할 수 있습니다.

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
    fileID: '387xxxxx8142975036', // 재생할 비디오의 fileID
    appID: '1400329073', // 비디오를 재생하기 위한 VOD 계정의 appID
    psign:'psignxxxx'   // psign은 Player 서명입니다. 서명 및 생성 방법에 대한 자세한 내용은 [Player 서명](https://www.tencentcloud.com/document/product/266/38099)을 참고하십시오.
});
```


:::
::: iOS
[통합 가이드](https://intl.cloud.tencent.com/document/product/266/33976)의 안내에 따라 RT-Cube Player를 통합해야 합니다. 통합 완료 후 `appId`, `fileId` 및 `psign`(플레이어 서명)을 사용하여 비디오를 재생할 수 있습니다.

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
model.videoId.fileId = @"387xxxxx8142975036"; // FileId 설정
// pSign은 Player 서명입니다. 서명 및 생성 방법에 대한 자세한 내용은 [Player 서명](https://www.tencentcloud.com/document/product/266/38099)을 참고하십시오.
model.videoId.pSign = @"psignxxxx";
[_playerView playWithModelNeedLicence:model];
[_playerView playWithModel:model];
```
:::
:::  Android
[통합 가이드](https://intl.cloud.tencent.com/document/product/266/33975)의 안내에 따라 RT-Cube Player를 통합해야 합니다. 통합 완료 후 `appId`, `fileId` 및 `psign`(플레이어 서명)을 사용하여 비디오를 재생할 수 있습니다.

플레이어의 메인 클래스는 `SuperPlayerView`로, 생성 후 즉시 비디오를 재생할 수 있습니다.

#### 1. 레이아웃 파일에 SuperPlayerView 생성

```xml
<!-- Player-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. fileId로 재생

```java
//레이아웃 파일에 SuperPlayerView 삽입 후 인스턴스 생성
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);

SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppId 설정
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "387xxxxx8142975036"; // FileId 설정
// pSign은 Player 서명입니다. 서명 및 생성 방법에 대한 자세한 내용은 [Player 서명](https://www.tencentcloud.com/document/product/266/38099)을 참고하십시오.
model.videoId.pSign = "psignxxxx";

mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## 요약

이제 링크 도용 방지가 활성화된 미디어 파일을 재생하고, 이미지 스프라이트 및 비디오 타임스탬프를 보고, 플레이어에서 동적 어댑티브 비트스트림을 자동으로 전환할 수 있습니다.
자세한 기능은 [기능 설명](https://intl.cloud.tencent.com/document/product/266/42965)을 참고하십시오.
