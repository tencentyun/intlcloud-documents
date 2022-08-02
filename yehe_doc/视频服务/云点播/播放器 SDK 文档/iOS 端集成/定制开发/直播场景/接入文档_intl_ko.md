본문은 MLVB(Mobile Live Video Broadcasting) SDK를 사용하여 라이브 스트리밍을 구현하는 방법을 설명합니다.

## 예시 코드
Tencent Cloud는 개발자가 자주 묻는 질문과 관련하여 이해하기 쉬운 API-Example 프로젝트를 제공하므로 다양한 API 사용법을 빠르게 배울 수 있습니다.

| 플랫폼 |                         GitHub 주소                           |
| :------: | :----------------------------------------------------------: |
|   iOS    | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## 준비 작업
1. 더 나은 사용자 경험을 위해 [CSS](https://intl.cloud.tencent.com/product/css) 활성화를 권장합니다. CSS(Cloud Streaming Services)를 사용할 필요가 없으면 이 단계를 건너뜁니다.
2. App Store에서 Xcode를 다운로드합니다. 이미 수행한 경우 이 단계를 건너뜁니다.
3. [Cocoapods 웹 사이트](https://cocoapods.org/)의 가이드에 따라 Cocoapods를 다운로드하여 설치합니다. 이미 수행한 경우 이 단계를 건너뜁니다.


## 내용 요약
* iOS용 플레이어 SDK를 통합하는 방법
* 라이브 재생을 위한 플레이어 SDK 사용 방법
* 플레이어 SDK의 기본 기능을 사용하여 더 많은 라이브 스트리밍 기능을 구현하는 방법

## SDK 통합
### 1단계: SDK ZIP 파일 다운로드
SDK 통합 가이드의 지침에 따라 SDK ZIP 파일을 다운로드하고 SDK를 App에 통합합니다.


### 2단계: Player 객체 생성
Tencent 비디오 Cloud SDK의 TXLivePlayer 모듈은 라이브 스트림 재생 기능을 구현합니다.
```objectivec
TXLivePlayer _txLivePlayer = [[TXLivePlayer alloc] init];
```

### 3단계: 렌더링 View 생성
iOS에서 view는 기본 UI 렌더링 단위로 사용됩니다. 따라서 플레이어가 비디오 이미지를 표시할 수 있도록 크기와 위치를 조정할 수 있는 view를 구성해야 합니다.

```objectivec
// setupVideoWidget을 사용하여 렌더링 영역을 결정하는 view를 플레이어에 바인딩합니다. 첫 번째 매개변수 frame은 v1.5.2부터 사용되지 않습니다.
[_txLivePlayer setupVideoWidget:CGRectMake(0, 0, 0, 0) containView:_myView insertIndex:0];
```

기술적으로 플레이어는 사용자가 제공하는 view(예시 코드의 \_myView)에서 직접 비디오 이미지를 렌더링하지 않습니다. 대신 view 위에 OpenGL 렌더링을 위한 서브 뷰(subView)를 만듭니다.

view의 크기와 위치를 변경하여 비디오 이미지의 크기를 조정할 수 있습니다. SDK는 그에 따라 비디오 이미지를 변경합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/235b2e8e6fc3eb328ba05a4c5d251da7.jpg)
 <dx-alert infotype="explain" title="애니메이션을 만드는 방법?">
view 애니메이션에 큰 유연성이 허용되지만 보기의 frame 속성이 아닌 transform을 수정해야 합니다.

```objectivec
  [UIView animateWithDuration:0.5 animations:^{
            _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // 1/3로 축소
        }];
```
</dx-alert>

### 4단계: 재생 시작
```objectivec
NSString* flvUrl = @"http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
[_txLivePlayer startPlay:flvUrl type:PLAY_TYPE_LIVE_FLV];
```

| 옵션 | 열거 값 | 설명 |
|---------|---------|---------|
| PLAY_TYPE_LIVE_RTMP | 0 | 전달된 URL은 RTMP 라이브 스트리밍 URL |
| PLAY_TYPE_LIVE_FLV | 1 | 전달된 URL은 FLV 라이브 스트리밍 URL |
| PLAY_TYPE_LIVE_RTMP_ACC | 5 | 저지연 연결 URL(마이크 연결 시나리오에만 해당) |
| PLAY_TYPE_VOD_HLS | 3 | 전달된 URL은 HLS(m3u8) 재생 URL |


<dx-alert infotype="explain" title="HLS(m3u8) 소개">
지연 시간이 너무 높기 때문에(HLS 프로토콜이 VOD에 적합하지만) App에서 라이브 스트리밍 비디오 소스를 재생하는 데 HLS 프로토콜을 사용하지 않는 것이 좋습니다. 대신 LIVE_FLV 및 LIVE_RTMP 재생 프로토콜을 사용하는 것이 좋습니다.
</dx-alert>

### 5단계: 재생 중지
재생을 중지할 때 현재 UI를 종료하기 전에 **removeVideoWidget**을 사용하여 view 컨트롤을 종료하는 것을 잊지 마십시오. 이렇게 하면 메모리 유출 및 화면 깜박임 문제를 방지할 수 있습니다.

```objectivec
// 재생 중지
[_txLivePlayer stopPlay];
[_txLivePlayer removeVideoWidget]; // view 컨트롤을 종료하는 것 기억
```

## 사용 방법
본문에서는 일반적인 라이브 스트리밍 기능을 사용하는 방법을 설명합니다.


### 1. 이미지 조정
- **view: 크기 및 위치**
setupVideoWidget의 view 매개변수의 크기와 위치를 조정하여 view의 크기와 위치를 수정할 수 있습니다. SDK는 구성에 따라 view의 크기와 위치를 자동으로 조정합니다.

- **setRenderMode: 화면 채우기 or 화면 맞춤**
<table>
<thead>
<tr>
<th>값</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_MODE_FILL_SCREEN</td>
<td>이미지는 전체 화면을 채우도록 크기가 조정되고 초과 부분은 잘립니다. 이 모드에는 검은색 막대가 없지만 이미지가 전체적으로 표시되지 않을 수 있습니다.</td>
</tr>
<tr>
<td>RENDER_MODE_FILL_EDGE</td>
<td>이미지는 가장 긴 면에 맞게 조정됩니다. 크기 조정 후 어느 쪽도 화면을 초과하지 않습니다. 이미지가 중앙에 있고 검은색 막대가 있을 수 있습니다.</td>
</tr>
</tbody></table>
- **setRenderRotation: 이미지 회전**
<table>
<thead>
<tr>
<th>값</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_ROTATION_PORTRAIT</td>
<td>일반 재생(Home 버튼은 비디오 이미지 아래에 있음)</td>
</tr>
<tr>
<td>RENDER_ROTATION_LANDSCAPE</td>
<td>이미지를 시계 방향으로 270도 회전(Home 버튼은 비디오 이미지 왼쪽에 있음)</td>
</tr>
</tbody></table>



### 2. 재생 일시 중지
기술적으로 말하면 라이브 재생을 일시 중지할 수 없습니다. 본문에서 재생을 일시 중지한다는 것은 **비디오 이미지를 정지**하고 **오디오 비활성화**를 의미하는 반면 비디오 소스는 클라우드에서 계속 스트리밍됩니다. resume을 호출하면 재개된 시점부터 재생이 시작됩니다. 이는 재생을 일시 중지하거나 다시 시작할 때 로컬 비디오 파일을 일시 중지하거나 다시 시작할 때와 동일한 방식으로 플레이어가 작동하는 VOD와 다릅니다.

```objectivec
// 재생 일시 중지
[_txLivePlayer pause];
// 재생 재개
[_txLivePlayer resume];
```

### 3. 메시지 수신
이 기능은 오디오/비디오 라인을 통해 게시자의 특정 사용자 정의 메시지를 시청자에게 전달하는 데 사용됩니다. 다음 시나리오에 적용할 수 있습니다.
(1) 온라인 퀴즈: 게시자는 완벽하게 동기화된 ‘오디오-이미지-질문’으로 시청자에게 <strong>질문</strong>을 전달합니다.
(2) 라이브 쇼: 게시자가 시청자에게 <strong>가사</strong>를 전달합니다. 비디오 인코딩 품질 저하의 영향을 받지 않고 플레이어에서 실시간으로 가사를 표시할 수 있습니다.
(3) 온라인 교육: 게시자는 시청자에게 <strong>레이저 포인터</strong> 및 <strong>낙서</strong> 작업을 전달하여 플레이어의 콘텐츠에 실시간으로 동그라미를 치고 밑줄을 긋습니다.

이 기능은 다음과 같이 사용할 수 있습니다.
- TXLivePlayConfig의 **enableMessage**를 **YES**로 설정합니다.
- TXLivePlayer가 **TXLivePlayListener**를 사용하여 **PLAY_EVT_GET_MESSAGE (2012)** 메시지를 수신하도록 합니다.

```objectiveC
 -(void) onPlayEvent:(int)EvtID withParam:(NSDictionary *)param {
    [self asyncRun:^{
        if (EvtID == PLAY_EVT_GET_MESSAGE) {
            dispatch_async(dispatch_get_main_queue(), ^{
                if ([_delegate respondsToSelector:@selector(onPlayerMessage:)]) {
                    [_delegate onPlayerMessage:param[@"EVT_GET_MSG"]];
                }
            });
        }
    }];
}
```

### 4. 화면 캡처
**snapshot**을 호출하여 현재 이미지를 프레임으로 캡처할 수 있습니다. 이 기능은 현재 라이브 스트리밍 비디오의 프레임만 캡처할 수 있습니다. 전체 UI를 캡처하려면 iOS 시스템의 API를 호출해야 합니다.



### 5. 라이브 스트림 녹화
라이브 스트림 녹화는 라이브 스트리밍 시나리오에서 확장된 기능입니다. 시청자는 라이브 스트림을 시청할 때 녹화 버튼을 클릭하여 라이브 스트림 세그먼트를 녹화하고 Tencent Cloud VOD와 같은 비디오 배포 플랫폼을 통해 게시할 수 있습니다. 이를 통해 WeChat Moments와 같은 소셜 미디어 플랫폼에 UGC 메시지로 비디오를 배포할 수 있습니다.



```objectivec
// 다음 샘플 코드는 라이브 스트리밍 시나리오에서 녹화 기능을 표시하는 데 사용됨
//
// TXVideoRecordListener를 지정하여 녹화 진행 상황과 결과를 동기화
_txLivePlayer.recordDelegate = recordListener;
// 녹화 시작. 이 API는 녹화 버튼의 응답 기능에 배치할 수 있습니다. 현재는 비디오 소스만 녹화할 수 있으며 화면 댓글과 같은 다른 데이터는 지원되지 않습니다.
[_txLivePlayer startRecord: RECORD_TYPE_STREAM_SOURCE]; 
// ...
// ...
// 녹화 중지. 이 API는 중지 버튼의 응답 기능에 배치 가능
[_txLivePlayer stopRecord];                             
```
- 녹화 진행 상황은 시간으로 측정되며 TXVideoRecordListener의 onRecordProgress를 통해 알려줍니다.
- 녹화된 파일은TXVideoRecordListener의 onRecordComplete를 통해 MP4 파일로 알려줍니다.
- TXUGCPublish는 비디오 업로드 및 게시를 구현하는 데 사용됩니다. 자세한 안내는 [iOS](https://intl.cloud.tencent.com/document/product/1069/38016)를 참고하십시오.


### 6. 매끄러운 해상도 전환
매일 사용하는 동안 네트워크 상태는 지속적으로 변경됩니다. 네트워크 상태가 좋지 않은 경우 낮은 이미지 품질로 전환하면 지연이 줄어들 수 있으며 네트워크 상태가 개선되면 더 높은 품질의 비디오로 전환할 수 있습니다.
일반적으로 스트림이 전환되면 재생이 중단되어 비디오 이미지 불연속성, 블랙 스크린 및 랙과 같은 문제가 발생할 수 있습니다. 매끄러운 전환 솔루션을 사용하면 라이브 스트리밍을 중단하지 않고 다른 스트림으로 전환할 수 있습니다.

해상도 전환 API는 라이브 스트리밍이 시작된 후 언제든지 호출할 수 있습니다.
```objectivec
// 스트림 재생 중 http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e.flv,
// 비트 레이트가 900Kbps인 새 스트림으로 전환
[_txLivePlayer switchStream:@"http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e_900.flv"];
```

>?매끄러운 해상도 전환 기능을 사용하려면 백엔드에서 PTS 정렬을 구성해야 합니다. 사용이 필요한 경우에는 [티켓 제출](https://console.cloud.tencent.com/workorder)하여 신청하십시오.

### 7. 라이브 스트림 다시보기
타임 시프트 기능을 사용하면 라이브 스트리밍 중 이전 시점으로 돌아가 해당 시점부터 재생을 재개할 수 있습니다. 인터랙션이 필요하지 않지만 시청자가 스포츠 및 게임 이벤트와 같이 비디오를 되감아 다시 재생하기를 원하는 시나리오에 매우 적합합니다.

```objectivec
// 타임 시프트를 설정하기 전에 먼저 startPlay 호출
// 재생 시작 …
[TXLiveBase setAppID:@"1253131631"]; // appId 구성
[_txLivePlayer prepareLiveSeek];     // 백엔드가 라이브 스트리밍 시작 시간 요청
```
올바른 구성 후 현재 진행 상황은 PLAY_EVT_PLAY_PROGRESS 이벤트에서 0부터 시작하지 않고 실제 재생 시작 시간을 기준으로 계산됩니다.
seek 메소드를 호출하여 이전 시점부터 라이브 스트리밍 다시 시작
```objectivec
[_txLivePlayer seek:600]; // 10분부터 재생 시작
```

타임 시프트에 연결하려면 백엔드에서 다음 설정을 구성합니다.

1. 녹화: 타임 시프트 지속 시간과 타임 시프트 저장 기간을 설정합니다.
2. 재생: 타임 시프트에서 메타데이터 획득을 활성화합니다.

>? 타임 시프트 기능은 현재 베타 테스트 중입니다. 사용이 필요한 경우에는 [티켓 제출](https://console.cloud.tencent.com/workorder)하여 신청하십시오.

### 8. 지연 시간 조정
SDK의 라이브 재생(LVB) 기능은 ffmpeg가 아니라 Tencent Cloud의 독점 재생 엔진을 기반으로 하므로 SDK가 오픈 소스 플레이어보다 더 나은 지연 시간 제어를 제공합니다. 쇼룸, 게임 스트리밍 및 하이브리드 시나리오에 사용할 수 있는 3가지 지연 시간 제어 모드를 제공합니다.

- **제어 모드 비교**
<table>
<thead>
<tr>
<th>제어 모드</th>
<th>랙 레이트</th>
<th>평균 지연 시간</th>
<th>적용 시나리오</th>
<th>작동 원리</th>
</tr>
</thead>
<tbody><tr>
<td>초고속 모드</td>
<td>초고속 모드보다 가능성 높음</td>
<td>2s- 3s</td>
<td>라이브쇼(온라인퀴즈)</td>
<td>더 나은 지연 시간 제어 기능이 있으며 짧은 지연 시간이 필요한 시나리오에 적합</td>
</tr>
<tr>
<td>원활 모드</td>
<td>랙 레이트 가장 낮음</td>
<td>&gt;= 5s</td>
<td>게임 라이브 스트리밍(Tencent Penguin eSports)</td>
<td>배틀 로얄 게임과 같이 비트 레이트가 높은 게임 라이브 스트리밍 시나리오에 적합</td>
</tr>
<tr>
<td>자동 모드</td>
<td>네트워크 조건에 자체 적응</td>
<td>2s-8s</td>
<td>하이브리드 시나리오</td>
<td>시청자의 네트워크가 좋을수록 지연 시간이 짧아지며, 시청자의 네트워크가 나쁠수록 지연 시간이 길어짐</td>
</tr>
</tbody></table>

- **세 가지 모드를 통합하는 코드**
```objectivec
TXLivePlayConfig*  _config = [[TXLivePlayConfig alloc] init];
// 자동 모드
_config.bAutoAdjustCacheTime   = YES;
_config.minAutoAdjustCacheTime = 1; 
_config.maxAutoAdjustCacheTime = 5;
// 초고속 모드
_config.bAutoAdjustCacheTime   = YES;
_config.minAutoAdjustCacheTime = 1;
_config.maxAutoAdjustCacheTime = 1;
// 원활 모드
_config.bAutoAdjustCacheTime   = NO;
_config.cacheTime              = 5;

[_txLivePlayer setConfig:_config];

// 구성 후 재생 시작
```

>? Stutter 및 지연 시간 제어에 대한 자세한 내용은 [Video Stutter](https://intl.cloud.tencent.com/document/product/1071/39362)를 참고하십시오.

### 9. 초저지연 재생
라이브 플레이어는 약 <strong>400ms</strong>의 초저지연 라이브 재생을 지원합니다. <strong>원격 클로 머신</strong> 및 <strong>마이크 연결</strong>과 같이 지연 시간에 대한 요구 사항이 매우 엄격한 시나리오에서 사용할 수 있습니다. 이 기능에 대해 다음 정보를 알아야 합니다.

- **이 기능을 활성화할 필요는 없습니다**
이 기능을 미리 활성화할 필요는 없지만 클라우드 서비스 제공 업체 간에 초저지연 연결을 구현하는 데 기술 및 기타 어려움이 있기 때문에 라이브 스트림이 Tencent Cloud에 있어야 합니다.

- **재생 URL은 링크 도용 방지로 구성되어야 합니다**
재생 URL은 일반 CDN URL이 될 수 없으며 링크 도용 방지 서명을 포함해야 합니다. 서명 계산 방법에 대한 자세한 내용은 [txTime&txSecret](https://intl.cloud.tencent.com/document/product/267/31560)을 참고하십시오.

- **ACC는 재생 유형으로 지정해야 합니다**
startPlay 재생 기능을 호출할 때 type을 **PLAY_TYPE_LIVE_RTMP_ACC**로 설정해야 하며 SDK는 RTMP-UDP 프로토콜을 사용하여 라이브 스트림을 직접 가져옵니다.

- **동시에 재생되는 스트림 수에 제한이 있습니다**
현재 최대 10개의 스트림을 동시에 재생할 수 있습니다. 지연 시간이 짧은 회선의 비용은 CDN 회선보다 훨씬 높기 때문에 사용자는 이 기능을 매우 짧은 지연 시간이 필요하지 않은 시나리오에 사용하기보다는 실제로 높은 인터랙션이 필요한 시나리오에서만 사용하는 것이 좋습니다.

- **Obs의 지연 시간이 요구 사항을 충족하지 않습니다**
[TXLivePusher](https://intl.cloud.tencent.com/document/product/1071/38157)를 사용하는 경우 [setVideoQuality](https://intl.cloud.tencent.com/document/product/1071/38157)를 호출하여 `quality` 를 MAIN_PUBLISHER 또는 VIDEO_CHAT으로 설정합니다. 스트리밍 끝에서 데이터가 쌓이는 경향이 있기 때문에 Obs로 짧은 지연 시간을 달성하기 어렵습니다.

- **재생시간으로 청구됩니다**
이 기능은 재생 시간에 따라 청구되며 요금은 풀 스트림 수에 따라 달라지지만 오디오/비디오 스트림 비트 레이트에는 영향을 미치지 않습니다. 가격에 대한 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/1071/38114)를 참고하십시오.

### 10. 비디오 정보 획득
Player SDK는 URL 문자열을 통해 비디오를 재생합니다. URL에는 비디오 정보가 포함되어 있지 않으며 이러한 정보를 로드하려면 클라우드 서버에 액세스해야 합니다. 따라서 SDK는 비디오 정보를 이벤트 알림으로만 애플리케이션에 보낼 수 있습니다. 자세한 내용은 [이벤트 리스닝](#monitor)을 참고하십시오.

예를 들어 'onNetStatus'의 'NET_STATUS_VIDEO_WIDTH' 및 'NET_STATUS_VIDEO_HEIGHT'를 사용하여 비디오 너비와 높이를 얻을 수 있습니다. 자세한 사용 방법은 [상태 피드백(onNetStatus)](#onNetStatus)을 참고하십시오.

[](id:monitor)
## 이벤트 리스닝
`TXLivePlayListener`를 `TXLivePlayer` 객체에 바인딩할 수 있습니다. 그러면 모든 내부 SDK 상태 메시지는 `onPlayEvent`([이벤트 공지](#onPlayEvent)) 및 `onNetStatus`([상태 콜백](#onNetStatus)) 메시지를 통해 공지합니다.

[](id:onPlayEvent)
### 이벤트 공지(onPlayEvent)
#### 1. 재생 이벤트
| 이벤트 ID                 |    코드  |  설명                    |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_EVT_CONNECT_SUCC     |  2001    | 서버 연결됨                |
| PLAY_EVT_RTMP_STREAM_BEGIN|  2002    | 서버가 연결되고 스트림 풀이 시작됨(RTMP URL에 대해서만 발생) |
| PLAY_EVT_RCV_FIRST_I_FRAME|  2003    | 네트워크가 첫 번째 렌더링 가능한 비디오 데이터 패킷(IDR)을 수신함  |
|PLAY_EVT_PLAY_BEGIN    |  2004|  비디오 재생이 시작되고 로딩 아이콘 애니메이션(있는 경우)이 종료됨 |
|PLAY_EVT_PLAY_LOADING|  2007|  비디오 loading 중, 비디오 재생이 재개되면 BEGIN 이벤트가 보고됨|
|PLAY_EVT_GET_MESSAGE|  2012|  오디오/비디오 스트림에서 메시지 수신에 사용됨. 자세한 내용은 [메시지 수신](#Message) 참고.|

- **PLAY_LOADING 수신 후 재생 이미지를 숨기지 마십시오**
PLAY_LOADING -> PLAY_BEGIN 사이의 시간 길이가 불확실하기 때문에(5s 또는 5ms일 수 있음) 일부 사용자는 LOADING 시 재생 이미지를 숨기고, BEGIN 시 이미지를 표시하여 심각한 이미지 깜박임(특히 라이브 스트리밍에서)을 유발할 수 있습니다. 비디오 재생 이미지 위에 반투명 loading 애니메이션을 배치하는 것이 좋습니다.

#### 2. 이벤트 중지
| 이벤트 ID                 |    코드  |  설명                    |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_END      |  2006|  비디오 재생 종료      |
|PLAY_ERR_NET_DISCONNECT |  -2301  |  네트워크 연결 끊김 및 여러 번 재시도한 후에도 다시 연결 불가. 플레이어를 다시 시작하여 연결 재시도 가능. |

- **라이브 스트리밍이 종료되었는지 어떻게 확인합니까?**
다양한 표준의 다양한 구현 원칙으로 인해 많은 라이브 스트림에 대해 종료 이벤트(오류 코드 2006)가 반환되지 않습니다. 대신 호스트가 스트림을 푸시할 때 SDK는 곧 데이터 스트림 가져오기 실패(WARNING_RECONNECT)를 발견하고 3번의 시도 실패 후 PLAY_ERR_NET_DISCONNECT 이벤트가 발생할 때까지 재시도합니다.

 따라서 두 오류 코드 2006 및 -2301을 모두 수신하고 라이브 스트리밍의 종료를 결정하는 데 사용해야 합니다.


#### 3. 경고 이벤트
이벤트 정보를 동기화하기 위한 화이트박스 SDK 설계 철학에 따라서만 제공되는 다음 이벤트는 무시해도 됩니다.

| 이벤트 ID                 |    코드  |  설명                    |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 현재 비디오 프레임 디코딩 실패  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 현재 오디오 프레임 디코딩 실패  |
| PLAY_WARNING_RECONNECT           |  2103  | 네트워크 연결 끊김, 자동 재연결 실행(3번의 시도 실패 후 PLAY_ERR_NET_DISCONNECT 이벤트 발생) |
| PLAY_WARNING_RECV_DATA_LAG       |  2104  | 네트워크에서 불안정한 패킷 전송. 불충분한 다운스트림 대역폭 또는 호스트의 아웃바운드 스트림이 고르지 않기 때문에 발생할 수 있음|
| PLAY_WARNING_VIDEO_PLAY_LAG      |  2105  | 비디오 재생 랙 발생|
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | 하드웨어 디코더 시작 실패, 소프트웨어 디코더가 대신 사용됨   |
| PLAY_WARNING_VIDEO_DISCONTINUITY |  2107  | 현재 비디오 프레임은 불연속적이므로 특정 프레임이 삭제될 수 있음|
| PLAY_WARNING_DNS_FAIL            |  3001  | RTMP-DNS 실패(RTMP 재생 URL에 대해서만 발생)|
| PLAY_WARNING_SEVER_CONN_FAIL     |  3002  | RTMP 서버 연결 실패(RTMP 재생 URL에 대해서만 발생)|
| PLAY_WARNING_SHAKE_FAIL          |  3003  | RTMP 서버 핸드셰이크 실패(RTMP 재생 URL에 대해서만 발생)|

[](id:onNetStatus)
### 상태 피드백(onNetStatus)
공지는 푸셔의 현재 상태에 대한 실시간 피드백을 제공하기 위해 1초에 한 번씩 트리거됩니다. SDK 내부에서 일어나는 일을 알려주는 대시보드 역할을 할 수 있으므로 현재 네트워크 상태와 비디오 정보를 더 잘 이해할 수 있습니다.

|   매개변수                   |  설명                   |
| :------------------------  |  :------------------------ |
| NET_STATUS_CPU_USAGE     | 현재 순간 CPU 사용률 |
| NET_STATUS_VIDEO_WIDTH | 비디오 해상도 - 너비 |
| NET_STATUS_VIDEO_HEIGHT| 비디오 해상도 - 높이 |
|NET_STATUS_NET_SPEED     | 현재 네트워크 데이터 수신 속도 |
|NET_STATUS_NET_JITTER    | 네트워크 지터. 지터가 클수록 네트워크가 더 불안정함 |
|NET_STATUS_VIDEO_FPS     | 스트리밍 미디어의 현재 비디오 프레임 속도    |
|NET_STATUS_VIDEO_BITRATE | 스트리밍 미디어의 현재 비디오 비트 레이트, 단위: kbps|
|NET_STATUS_AUDIO_BITRATE | 스트리밍 미디어의 현재 오디오 비트 레이트,단위: kbps|
|NET_STATUS_CACHE_SIZE    | 버퍼(jitterbuffer) 크기, 현재 버퍼 길이가 0이면 랙 곧 발생|
| NET_STATUS_SERVER_IP | 연결된 서버 IP |


