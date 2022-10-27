## 학습 목표

이 문서에서는 DRM 솔루션을 사용하여 동영상을 암호화하고 플레이어를 사용하여 암호화된 동영상을 재생하는 방법을 보여줍니다.

## 전제 조건
시작하기 전에 다음을 수행하십시오.

### VOD 활성화
VOD를 활성화하려면 다음 단계를 따르십시오.

1. [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985) 및 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다.
2. VOD 서비스를 구매합니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/266/2838)를 참고하십시오.
3. **클라우드 서비스**>**비디오 서비스**>[**VOD**](https://console.cloud.tencent.com/vod)를 선택하여 VOD 콘솔로 이동합니다.

이제 VOD가 활성화됐습니다. 

### FairPlay 인증서 정보 얻기

[FairPlay 인증서 정보를 신청하는 방법](https://www.tencentcloud.com/document/product/266/46643)을 참고하십시오.

### FairPlay 인증서 정보 제출

[Submitting FairPlay Certificate Information to VOD](https://intl.cloud.tencent.com/document/product/266/49668)를 참고하십시오.


## 1단계: 링크 도용 방지 활성화

아래 예시는 계정 아래의 기본 배포 도메인에 대한 Key 링크 도용 방지를 활성화하는 방법을 보여줍니다.
>? 이미 사용 중인 도메인 이름에 대해 링크 도용 방지를 활성화하지 않는 것이 좋습니다. 재생이 실패할 수 있기 때문입니다.

1. VOD 콘솔에 로그인하여 [배포 및 재생]>[[도메인 관리]](https://console.cloud.tencent.com/vod/distribute-play/domain)를 선택하고 ‘기본 배포 도메인’을 찾아 오른쪽의 [설정]을 클릭합니다. 독립 실행형 [액세스 제어] 설정 페이지로 이동합니다.
   <img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. [Key 링크 도용 방지]를 켭니다. 팝업 창에서 [랜덤 Key 생성]을 클릭하여 임의의 Key를 생성합니다(`testtest`라고 가정). Key를 복사하고 [확인]을 클릭합니다. 나중에 이 Key를 사용하여 재생 서명을 생성합니다.
   ![image-KEY](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## 2단계: 비디오 DRM 암호화

1. VOD 콘솔에서 **미디어 자산**>[**비디오 관리**](https://console.cloud.tencent.com/vod/media)를 선택하고 타깃 비디오(FileId: 387702299667618135)를 선택한 후 **비디오 처리**를 클릭하십시오.

   ![image-20220426211316803](https://qcloudimg.tencent-cloud.cn/raw/4eab2858c67f4efbf1383a3b03810428.png)

2. 비디오 처리 페이지에서:
 - **처리 유형**은 **태스크 플로우**를 선택합니다.
 - **작업 흐름 템플릿**으로 **WidevineFairPlayPreset**을 선택합니다.
 ![image-20220425192205432](https://qcloudimg.tencent-cloud.cn/raw/cef2c1e79343ea9688654791b6fb6762.png)

>?
>- WidevineFairPlayPreset은 사전 설정된 작업 흐름입니다. 어댑티브 비트레이트 스트리밍 템플릿 11 또는 13, 포인트 스크린샷 템플릿 10(썸네일 생성용) 및 이미지 스프라이트 템플릿 10을 사용합니다.
>- 어댑티브 비트레이트 스트리밍 템플릿 11은 `FairPlay`에 의해 암호화된 다중 비트레이트 스트림을 생성하고, 어댑티브 비트레이트 스트리밍 템플릿 13은 `Widevine`에 의해 암호화된 다중 비트레이트 스트림을 생성합니다.

3. **확인**을 클릭하고 ‘비디오 상태’가 ‘처리 중’에서 ‘정상’으로 변경될 때까지 기다리십시오. 이는 비디오 처리가 완료되었음을 나타냅니다.
<img src="https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png" width="" />
4. 비디오의 ‘작업’ 열에서 **관리**를 클릭하여 관리 페이지로 이동합니다.
 - ‘기본 정보’ 탭을 클릭하면 생성된 썸네일과 어댑티브 비트레이트 스트리밍 출력(템플릿 ID: 11 및 13)을 볼 수 있습니다.

   ![image-20220426201159056](https://qcloudimg.tencent-cloud.cn/raw/696e894ed0c3665990c12cc57ebf23bf.png)

 - 생성된 이미지 스프라이트(템플릿 ID: 10)를 보려면 ‘스크린샷 정보’ 탭을 클릭합니다.

   ![image-20220426201309975](https://qcloudimg.tencent-cloud.cn/raw/1a5878fd0286c46ef487bdf81ad8503a.png)

## 3단계: Player 서명 생성

Player 서명은 과거 재생 정보를 조회하는 데 사용됩니다. 생성 방법은 [Player 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오. Player 서명 생성을 위한 PayLoad는 다음과 같습니다.

```json
{
  "appId": 1500012416,
  "fileId": "387702299667618135",
  "currentTimeStamp": 1650886156,
  "expireTimeStamp": 1966435200,
  "urlAccessInfo": {
    "t": "75356B80",
    "us": "72d4cd1101"
  },
  "pcfg":"advanceDrmPreset"
}
```

Key는 `testtest`입니다. 생성된 Player 서명(`psign`)은 다음과 같습니다.

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

## 4단계: 플레이어에서 DRM으로 암호화된 비디오를 재생합니다.

### Web

#### VOD 플레이어 사용하기

VOD 플레이어를 사용하여 DRM으로 암호화된 동영상을 재생하려면 플레이어를 초기화할 때 동영상의 파일 ID와 VOD 계정의 appID를 전달하기만 하면 됩니다.


#### step 1: 파일 가져오기

플레이어의 양식 파일과 스크립트 파일을 웹페이지로 가져옵니다.

```
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.3/tcplayer.min.css" rel="stylesheet">
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.3/libs/hls.min.1.1.5.js"></script>
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.3/tcplayer.v4.5.3.min.js"></script>
```

#### step 2: 플레이어 컨테이너 추가

플레이어를 표시할 위치에 플레이어 컨테이너를 추가합니다.

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

> ? 컨테이너 ID와 컨테이너의 높이 및 너비를 사용자 지정할 수 있습니다.

#### step 3: 초기화 코드 추가

페이지 초기화 코드에 다음 스크립트를 추가하고 필요한 초기화 매개변수를 전달합니다.

```
var player = TCPlayer('player-container-id', {
    appID: '1500012416', // VOD 계정의 appID (필수)
    fileID: '387702299667618135', // 재생할 동영상의 filID (필수)
    psign: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg',
    // 기타 매개변수는 https://intl.cloud.tencent.com/document/product/266/39105 참고
});
```

### iOS

iOS에서 `FileId를 통해` 방식으로 DRM으로 암호화된 동영상을 재생하려면 통합 가이드 를 참고하십시오.

>? DRM을 지원하는 플레이어 SDK에 대한 티켓을 제출하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/1cba8f5fffad9827a267314ced65d078.png)

### Android

Android에서 `FileId를 통해` 방식으로 DRM으로 암호화된 동영상을 재생하려면 [통합 가이드](https://intl.cloud.tencent.com/document/product/266/49670#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E5.90.AF.E5.8A.A8.E6.92.AD.E6.94.BE)를 참고하십시오.

> ? 액세스 전, 티켓을 제출하여 DRM을 지원하는 플레이어 SDK를 받으십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/77ec9a38fc9530305affa447df8f9e14.png)

## 결론

이제 DRM 솔루션을 사용하여 동영상을 암호화하고 플레이어에서 암호화된 동영상을 재생하는 방법을 배웠습니다.

> ? 질문이 있으시면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 하십시오.
