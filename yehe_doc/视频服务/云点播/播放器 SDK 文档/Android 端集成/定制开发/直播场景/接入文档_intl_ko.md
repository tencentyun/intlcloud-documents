본문은 MLVB(Mobile Live Video Broadcasting) SDK를 사용하여 라이브 스트리밍을 구현하는 방법을 설명합니다.

## 예시 코드
Tencent Cloud는 이해하기 쉬운 API 예시 프로젝트를 제공하여 다양한 API 사용법을 빠르게 배울 수 있도록 지원합니다.

| 플랫폼 |                         GitHub 주소                          |
| :------: | :----------------------------------------------------------: |
|   iOS    | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## 준비 작업
1. 더 나은 사용자 경험을 위해 [CSS](https://intl.cloud.tencent.com/product/css) 활성화를 권장합니다. CSS(Cloud Streaming Services)를 사용할 필요가 없으면 이 단계를 건너뜁니다.
2. [Android Studio](https://developer.android.com/studio)에서 Android Studio를 다운로드하여 설치합니다. 이미 수행한 경우 이 단계를 건너뜁니다.


## 내용 요약
* Android용 플레이어 SDK를 통합하는 방법
* 라이브 재생을 위한 플레이어 SDK 사용 방법
* 플레이어 SDK의 기본 기능을 사용하여 더 많은 라이브 스트리밍 기능을 구현하는 방법



## SDK 통합
### 1단계: SDK ZIP 파일 다운로드
SDK 통합 가이드의 지침에 따라 SDK ZIP 파일을 다운로드하고 SDK를 App에 통합합니다.


### 2단계: View 추가
SDK는 기본적으로 동영상 렌더링을 위한 TXCloudVideoView를 제공합니다. 먼저 레이아웃 xml 파일에 다음 코드를 추가합니다.
```xml
<com.tencent.rtmp.ui.TXCloudVideoView
            android:id="@+id/video_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_centerInParent="true"
            android:visibility="gone"/>
```

### 3단계: Player 객체 생성
플레이어 SDK의 **TXLivePlayer** 모듈은 라이브 재생 기능을 구현하는 데 사용됩니다. **setPlayerView** API를 사용하여 모듈을 UI에 방금 추가한 **video_view** 컨트롤과 연결합니다.
```java
//mPlayerView는 1단계에서 추가한 view
TXCloudVideoView mView = (TXCloudVideoView) view.findViewById(R.id.video_view);

//player 객체 생성
TXLivePlayer mLivePlayer = new TXLivePlayer(getActivity());

//player 객체를 view와 연결
mLivePlayer.setPlayerView(mView);
```

### 4단계: 재생 실행
```java
String flvUrl = "http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
mLivePlayer.startPlay(flvUrl, TXLivePlayer.PLAY_TYPE_LIVE_FLV); //FLV 권장
```

| 옵션                  | 열거 값 | 설명                               |
| ----------------------- | ------ | ---------------------------------- |
| PLAY_TYPE_LIVE_RTMP     | 0      | 전달된 URL은 RTMP 라이브 스트리밍 URL        |
| PLAY_TYPE_LIVE_FLV      | 1      | 전달된 URL은 FLV 라이브 스트리밍 URL         |
| PLAY_TYPE_LIVE_RTMP_ACC | 5      | 저지연 URL(마이크 연결 시나리오에만 적용 가능) |
| PLAY_TYPE_VOD_HLS       | 3      | 전달된 URL은 HLS(m3u8) 재생 URL  |


>?지연 시간이 너무 길기 때문에(HLS 프로토콜이 VOD에 적합하지만) App에서 라이브 스트리밍 비디오 소스를 재생하는 데 HLS 프로토콜을 사용하지 않는 것이 좋습니다. 대신 LIVE_FLV 및 LIVE_RTMP 재생 프로토콜을 사용하는 것이 좋습니다.

### 5단계: 재생 중지
재생을 중지할 때, 특히 startPlay의 다음 호출 전에 **view 컨트롤을 종료**해야 합니다. 이렇게 하면 **메모리 유출과 화면 깜박임 문제를 방지할 수 있습니다**.

또한 재생 UI를 종료할 때 **렌더링 View에 대한 'onDestroy()' 함수를 호출해야 합니다**. 이렇게 하면 **메모리 유출 및 Receiver not registered 알람을 방지할 수 있습니다**.
```java
@Override
public void onDestroy() {
    super.onDestroy();
    mLivePlayer.stopPlay(true); // true는 마지막 프레임 이미지를 지우는 것을 표시
    mView.onDestroy(); 
}
```

stopPlay 의 boolean 매개변수는 ‘마지막 프레임 이미지를 지울지 여부’를 나타냅니다. RTMP SDK 라이브 플레이어의 초기 버전에는 pause 기능이 없습니다. 따라서 이 boolean 값은 마지막 프레임 이미지를 지우는 데 사용됩니다.

VOD가 중지된 후 마지막 프레임 이미지를 유지하려면 재생 중지 이벤트를 수신한 후 아무 것도 하지 마십시오. 재생은 기본적으로 마지막 프레임에서 중지됩니다.


## 사용하는 방법
본문은 일반적인 라이브 스트리밍 기능을 사용하는 방법을 설명합니다.

### 1. 이미지 조정
- **view: 크기 및 위치**
**1단계**에서 추가한 video_view 컨트롤의 크기와 위치를 조정하여 비디오 이미지의 크기와 위치를 수정할 수 있습니다.

- **setRenderMode: 화면 채우기 또는 화면 맞춤**

| 값                        | 설명                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| RENDER_MODE_FULL_FILL_SCREEN  | 이미지는 전체 화면을 채우도록 크기가 조정되고 초과 부분은 잘립니다. 이 모드에는 검은색 막대가 없지만 이미지가 전체적으로 표시되지 않을 수 있습니다. |
| RENDER_MODE_ADJUST_RESOLUTION | 이미지의 긴 쪽이 화면에 맞게 조정됩니다. 이 모드에서는 이미지의 어느 쪽도 화면 가장자리를 초과하지 않습니다. 이미지가 중앙에 있고 검은색 막대가 있을 수 있습니다. |

- **setRenderRotation: 이미지 회전**

| 값                    | 설명                                       |
| ------------------------- | ------------------------------------------ |
| RENDER_ROTATION_PORTRAIT  | 일반 재생(Home 버튼은 비디오 이미지 아래에 있음)            |
| RENDER_ROTATION_LANDSCAPE | 비디오 이미지를 시계 방향으로 270도 회전(Home 버튼은 이미지 왼쪽에 있음) |

```Java
// 채우기 모드 설정
mLivePlayer.setRenderMode(TXLiveConstants.RENDER_MODE_ADJUST_RESOLUTION);
// 비디오 회전 설정
mLivePlayer.setRenderRotation(TXLiveConstants.RENDER_ROTATION_LANDSCAPE);
```




### 2. 재생 일시 중지
기술적으로 말하면 라이브 재생을 일시 중지할 수 없습니다. 본문에서 재생을 일시 중지한다는 것은 **비디오 이미지를 정지**하고 **오디오 비활성화**를 의미하는 반면 비디오 소스는 클라우드에서 계속 스트리밍됩니다. resume을 호출하면 재개된 시점부터 재생이 시작됩니다. 이는 재생을 일시 중지하거나 다시 시작할 때 로컬 비디오 파일을 일시 중지하거나 다시 시작할 때와 동일한 방식으로 플레이어가 작동하는 VOD와 다릅니다.

```java
// 재생 일시 중지
mLivePlayer.pause();
// 재생 재개
mLivePlayer.resume();
```

### 3. 메시지 수신
이 기능은 오디오/비디오 데이터와 함께 게시자의 사용자 지정 message를 청중에게 전달하는 데 사용됩니다. 다음 시나리오에 적용할 수 있습니다.

- 온라인 퀴즈: 푸셔가 시청자에게 **질문**을 전달합니다. 원활한 ‘사운드-이미지-질문’ 동기화가 달성될 수 있습니다.
- 라이브 쇼: 푸셔가 관객에게 **가사**를 전달합니다. 가사는 플레이어에 실시간으로 표시될 수 있으며 비디오 인코딩 품질 저하의 영향을 받지 않습니다.
- 온라인 교육: 게시자는 시청자에게 **레이저 포인터** 및 **낙서** 작업을 전달하여 플레이어의 콘텐츠에 실시간으로 동그라미를 치고 밑줄을 긋습니다.

이 기능은 다음과 같이 사용할 수 있습니다.
- TXLivePlayConfig의 **setEnableMessage**를 **true**로 설정합니다.
- TXLivePlayer가 **TXLivePlayListener**를 사용하여 **PLAY_EVT_GET_MESSAGE(2012)** 메시지를 수신하도록 합니다.

```java
//Android용 예시 코드
    mTXLivePlayer.setPlayListener(new ITXLivePlayListener() {
        @Override
        public void onPlayEvent(int event, Bundle param) {
            if (event == TXLiveConstants.PLAY_ERR_NET_DISCONNECT) {
                roomListenerCallback.onDebugLog("[AnswerRoom] 풀 스트림 실패: 네트워크 연결 끊김");
                roomListenerCallback.onError(-1, "네트워크 연결 끊김, 풀 스트림 실패");
            }
            else if (event == TXLiveConstants.PLAY_EVT_GET_MESSAGE) {
                String msg = null;
                try {
                    msg = new String(param.getByteArray(TXLiveConstants.EVT_GET_MSG), "UTF-8");
                    roomListenerCallback.onRecvAnswerMsg(msg);
                } catch (UnsupportedEncodingException e) {
                    e.printStackTrace();
                }
            }
        }
        @Override
        public void onNetStatus(Bundle status) {
        }
        });
```

### 4. 화면 캡처
라이브 스트리밍 비디오의 스크린샷을 캡처하려면 **snapshot**을 호출하십시오. 이 방법은 비디오의 프레임을 캡처합니다. UI를 캡처하려면 Android 시스템의 해당 API를 사용하십시오.



```java
mLivePlayer.snapshot(new ITXSnapshotListener() {
    @Override
    public void onSnapshot(Bitmap bmp) {
        if (null != bmp) {
           //스크린샷 bitmap 가져오기
        }
    }
});
```

### 5. 라이브 스트림 녹화
라이브 스트림 녹화는 라이브 스트리밍 시나리오에서 확장된 기능입니다. 시청자는 라이브 스트림을 시청할 때 녹화 버튼을 클릭하여 라이브 스트림 세그먼트를 녹화하고 Tencent Cloud VOD와 같은 비디오 배포 플랫폼을 통해 게시할 수 있습니다. 이를 통해 WeChat Moments와 같은 소셜 미디어 플랫폼에 UGC 메시지로 비디오를 배포할 수 있습니다.



```java
//ITXVideoRecordListener를 지정하여 녹화 진행 상황과 결과 동기화
mLivePlayer.setVideoRecordListener(recordListener);
//녹화 시작. 이 API는 녹화 버튼의 응답 기능에 배치할 수 있습니다. 현재는 영상 소스만 녹화가 가능하며, 화면 댓글과 같은 기타 데이터는 녹화 불가능
mLivePlayer.startRecord(int recordType);
// ...
// ...
//녹화 중지. 이 API는 중지 버튼의 응답 기능에 배치 가능
mLivePlayer.stopRecord();
```

- 녹화 진행 상황은 시간으로 측정되며 ITXVideoRecordListener의 onRecordProgress를 통해 알려줍니다.
- 녹음된 파일은 ITXVideoRecordListener의 onRecordComplete를 통해 MP4 파일로 알려줍니다.
- TXUGCPublish는 비디오 업로드 및 게시를 구현하는 데 사용됩니다. 자세한 안내는 [Android](https://intl.cloud.tencent.com/document/product/1069/38026)를 참고하십시오.

### 6. 매끄러운 해상도 전환
매일 사용하는 동안 네트워크 상태는 지속적으로 변경됩니다. 네트워크 상태가 좋지 않은 경우 낮은 이미지 품질로 전환하면 랙이 줄어들 수 있으며 네트워크 상태가 개선되면 더 높은 품질의 비디오로 다시 전환할 수 있습니다.
일반적으로 스트림이 전환되면 재생이 중단되어 비디오 이미지 불연속성, 블랙 스크린 및 랙과 같은 문제가 발생할 수 있습니다. 매끄러운 전환 솔루션을 사용하면 라이브 스트리밍을 중단하지 않고 다른 스트림으로 전환할 수 있습니다.

해상도 전환 API는 라이브 스트리밍이 시작된 후 언제든지 호출할 수 있습니다.
```java
// 스트림 재생 중 http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e.flv,
// 비트 레이트가 900Kbps인 새 스트림으로 전환
mLivePlayer.switchStream("http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e_900.flv");
```

>?매끄러운 해상도 전환 기능을 사용하려면 백엔드에서 PTS 정렬을 구성해야 합니다. 사용이 필요한 경우에는 [티켓 제출](https://console.cloud.tencent.com/workorder)하여 신청하십시오.

### 7. 라이브 스트림 다시보기
타임 시프트 기능을 사용하면 라이브 스트리밍 중 이전 시점으로 돌아가 해당 시점부터 재생을 재개할 수 있습니다. 인터랙션이 필요하지 않지만 시청자가 스포츠 및 게임 이벤트와 같이 비디오를 되감아 다시 재생하기를 원하는 시나리오에 매우 적합합니다.

```java
// 타임 시프트를 설정하기 전에 먼저 startPlay 호출
// 재생 시작 …
TXLiveBase.setAppID("1253131631"); // appId 구성
mLivePlayer.prepareLiveSeek();     // 백엔드가 라이브 스트리밍 시작 시간 요청
```
올바른 구성 후 현재 진행 상황은 PLAY_EVT_PLAY_PROGRESS 이벤트에서 0부터 시작하지 않고 실제 재생 시작 시간을 기준으로 계산됩니다.
seek 메소드를 호출하여 이전 시점부터 라이브 스트리밍 다시 시작
```java
mLivePlayer.seek(600); // 10분부터 재생 시작
```

타임 시프트에 연결하려면 백엔드에서 다음 설정을 구성합니다.

- 녹화: 타임 시프트 지속시간과 타임 시프트 저장 기간을 설정합니다.
- 재생: 타임 시프트에서 메타데이터 획득을 활성화합니다.

타임 시프트 기능은 현재 베타 테스트 중입니다. 사용이 필요한 경우에는 [티켓 제출](https://console.cloud.tencent.com/workorder)하여 신청하십시오.

### 8. 지연 시간 조정
SDK의 라이브 재생(LVB) 기능은 ffmpeg가 아니라 Tencent Cloud의 독점 재생 엔진을 기반으로 하므로 SDK가 오픈 소스 플레이어보다 더 나은 지연 시간 제어를 제공합니다. 쇼룸, 게임 스트리밍 및 하이브리드 시나리오에 사용할 수 있는 3가지 지연 시간 제어 모드를 제공합니다.

- **제어 모드 비교**

| 제어 모드 | 랙 레이트     | 평균 지연 시간 | 적용 가능한 시나리오             | 설명                                                 |
| -------- | ---------- | -------- | -------------------- | -------------------------------------------------------- |
| 신속 모드 | 상대적으로 높은 | 2s - 3s  | 라이브쇼(온라인퀴즈) | 더 나은 지연 시간 제어 기능이 있으며 짧은 지연 시간이 필요한 시나리오에 적합       |
| 부드러운 모드 | 최저 | >= 5s    | 게임 라이브 스트리밍(Tencent Penguin eSports) | 배틀 로얄 게임과 같이 비트 레이트가 높은 게임 라이브 스트리밍 시나리오에 적합   |
| 자동 모드 | 네트워크 적응 | 2s - 8s  | 하이브리드 시나리오 | 시청자의 네트워크가 좋을수록 지연 시간이 짧아지며, 시청자의 네트워크가 나쁠수록 지연 시간이 길어짐 |


- **세 가지 모드를 통합하는 코드**
```java
TXLivePlayConfig mPlayConfig = new TXLivePlayConfig();
//
//자동 모드
mPlayConfig.setAutoAdjustCacheTime(true);
mPlayConfig.setMinAutoAdjustCacheTime(1);
mPlayConfig.setMaxAutoAdjustCacheTime(5);
//
//초고속 모드
mPlayConfig.setAutoAdjustCacheTime(true);
mPlayConfig.setMinAutoAdjustCacheTime(1);
mPlayConfig.setMaxAutoAdjustCacheTime(1);
//
//원활 모드
mPlayConfig.setAutoAdjustCacheTime(false);
mPlayConfig.setCacheTime(5);
//
mLivePlayer.setConfig(mPlayConfig);
//구성 후 재생 시작
```

>?Stutter 및 지연 시간 제어에 대한 자세한 내용은 [Video Stutter](https://intl.cloud.tencent.com/document/product/1071/39362)를 참고하십시오.

### 9. 초저지연 재생
라이브 플레이어는 약 **400ms**의 초저지연 라이브 재생**을 지원합니다. **원격 클로 머신 및 마이크 연결**과 같이 지연 시간에 대한 요구 사항이 매우 엄격한 시나리오에서 사용할 수 있습니다. 이 기능에 대해 다음 정보를 알아야 합니다.

- **이 기능을 활성화할 필요는 없습니다**
이 기능을 미리 활성화할 필요는 없지만 클라우드 서비스 제공 업체 간에 초저지연 연결을 구현하는 데 기술 및 기타 어려움이 있기 때문에 라이브 스트림이 Tencent Cloud에 있어야 합니다.

- **재생 URL은 링크 도용 방지로 구성되어야 합니다**
재생 URL은 일반 CDN URL이 될 수 없으며 링크 도용 방지 서명을 포함해야 합니다. 서명 계산 방법에 대한 자세한 내용은 [**txTime 및 txSecret**](https://intl.cloud.tencent.com/document/product/267/31560)을 참고하십시오.

- **ACC는 재생 유형으로 지정해야 합니다**
startPlay 재생 기능을 호출할 때 type을 **PLAY_TYPE_LIVE_RTMP_ACC**로 설정해야 하며 SDK는 RTMP-UDP 프로토콜을 사용하여 라이브 스트림을 직접 가져옵니다.

- **동시 재생 스트림 수 제한이 있습니다**
현재 최대 **10개**의 스트림을 동시에 재생할 수 있습니다. 지연 시간이 짧은 회선의 비용은 CDN 회선보다 훨씬 높기 때문에 사용자는 이 기능을 매우 짧은 지연 시간이 필요하지 않은 시나리오에 사용하기보다는 실제로 높은 인터랙션이 필요한 시나리오에서만 사용하는 것이 좋습니다.

- **Obs의 지연 시간이 요구 사항을 충족하지 않습니다**
[TXLivePusher](https://intl.cloud.tencent.com/document/product/1071/38158)를 사용하는 경우 [setVideoQuality](https://intl.cloud.tencent.com/document/product/1071/38158)를 호출하여 `quality` 를 MAIN_PUBLISHER 또는 VIDEO_CHAT으로 설정합니다. 스트리밍 끝에서 데이터가 쌓이는 경향이 있기 때문에 Obs로 짧은 지연 시간을 달성하기 어렵습니다.

- **재생시간으로 청구됩니다**
이 기능은 재생 시간에 따라 청구되며 요금은 풀 스트림 수에 따라 달라지지만 오디오/비디오 스트림 비트 레이트에는 영향을 미치지 않습니다. 가격에 대한 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/1071/38114)를 참고하십시오.


### 10. 영상 정보 획득
Player SDK는 URL 문자열을 통해 비디오를 재생합니다. URL에는 비디오 정보가 포함되어 있지 않으며 이러한 정보를 로딩하려면 클라우드 서버에 액세스해야 합니다. 따라서 SDK는 비디오 정보를 이벤트 알림으로만 애플리케이션에 보낼 수 있습니다. 자세한 내용은 [이벤트 리스닝](#monitor)을 참고하십시오.

예를 들어 'onNetStatus'의 'NET_STATUS_VIDEO_WIDTH' 및 'NET_STATUS_VIDEO_HEIGHT'를 사용하여 비디오 너비와 높이를 얻을 수 있습니다. 자세한 사용 방법은 [상태 피드백(onNetStatus)](#onNetStatus)을 참고하십시오.

[](id:monitor)
## 이벤트 리스닝
`TXLivePlayListener`를 `TXLivePlayer` 객체에 바인딩할 수 있습니다. 그러면 모든 내부 SDK 상태 메시지는 `onPlayEvent`([이벤트 공지](#onPlayEvent)) 및 `onNetStatus`([상태 콜백](#onNetStatus)) 메시지를 통해 공지합니다.

[](id:onPlayEvent)
### 이벤트 공지(onPlayEvent)
#### 1. 재생 이벤트
| 이벤트 ID                      | 코드 | 설명                                                   |
| ---------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN       | 2004 | 비디오 재생 시작                                               |
| PLAY\_EVT\_PLAY\_PROGRESS    | 2005 | 비디오 재생 진행률(현재 재생 진행률, 로딩 진행률, 총 비디오 재생 시간 포함)      |
| PLAY\_EVT\_PLAY\_LOADING     | 2007 | 비디오 loading 중, 비디오 재생이 재개되면 LOADING\_END 이벤트가 보고됨 |
| PLAY\_EVT\_VOD\_LOADING\_END | 2014 | 비디오 loading 종료, 비디오 재생이 재개됨                        |

**PLAY_LOADING 수신 후 재생 이미지를 숨기지 마십시오**: PLAY_LOADING -> PLAY_BEGIN 사이의 시간 길이가 불확실하기 때문에(5s 또는 5ms일 수 있음) 일부 사용자는 LOADING 시 재생 이미지를 숨기고, BEGIN 시 이미지를 표시하여 심각한 이미지 깜박임(특히 라이브 스트리밍에서)을 유발할 수 있습니다. **비디오 재생 이미지 위에 반투명 로딩 애니메이션을 배치하는 것이 좋습니다.**

#### 2. 이벤트 중지
| 이벤트 ID                 | 코드  | 설명                                               |
| :---------------------- | :---- | :----------------------------------------------------- |
| PLAY_EVT_PLAY_END       | 2006  | 비디오 재생 종료                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | 네트워크 연결이 끊겼고 여러 번 재시도한 후에도 다시 연결할 수 없습니다. 플레이어를 다시 시작하여 더 많은 연결 재시도를 수행할 수 있습니다. |
| PLAY_ERR_HLS_KEY        | -2305 | HLS 암호 해독 key 가져오기 실패                                  |

**라이브 스트리밍이 종료되었는지 어떻게 확인합니까?**
다양한 표준의 다양한 구현 원칙으로 인해 많은 라이브 스트림에 대해 종료 이벤트(오류 코드 2006)가 반환되지 않습니다. 대신 호스트가 스트림을 푸시할 때 SDK는 곧 데이터 스트림 가져오기 실패(WARNING_RECONNECT)를 발견하고 3번의 시도 실패 후 PLAY_ERR_NET_DISCONNECT 이벤트가 발생할 때까지 재시도합니다.

따라서 두 오류 코드 2006 및 -2301을 모두 수신하고 라이브 스트리밍의 종료를 결정하는 데 사용합니다.

#### 3. 경고 이벤트
SDK의 일부 내부 이벤트를 알리는 데만 사용되는 다음 이벤트는 무시할 수 있습니다.

| 이벤트 ID                           | 코드 | 설명                                                     |
| :-------------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_WARNING_VIDEO_DECODE_FAIL    | 2101 | 현재 비디오 프레임 디코딩 실패                                           |
| PLAY_WARNING_AUDIO_DECODE_FAIL    | 2102 | 현재 오디오 프레임 디코딩 실패                                           |
| PLAY_WARNING_RECONNECT            | 2103 | 네트워크 연결 끊김, 자동 재연결 실행(3번의 시도 실패 후 PLAY_ERR_NET_DISCONNECT 이벤트 발생) |
| PLAY_WARNING_HW_ACCELERATION_FAIL | 2106 | 하드웨어 디코더 시작 실패, 소프트웨어 디코더가 대신 사용됨                                       |

[](id:onNetStatus)
### 상태 피드백(onNetStatus)
공지는 푸셔의 현재 상태에 대한 실시간 피드백을 제공하기 위해 1초에 한 번씩 트리거됩니다. SDK 내부에서 일어나는 일을 알려주는 대시보드 역할을 할 수 있으므로 현재 네트워크 상태와 비디오 정보를 더 잘 이해할 수 있습니다.
<table>
<tr><th>매개변수</th><th>설명</th></tr>
<tr>
<td>NET_STATUS_CPU_USAGE</td><td>현재 순간 CPU 사용률</td>
</tr><tr>
<td>NET_STATUS_VIDEO_WIDTH</td><td>비디오 해상도 - 너비</td>
</tr><tr>
<td>NET_STATUS_VIDEO_HEIGHT</td><td>비디오 해상도 - 높이</td>
</tr><tr>
<td>NET_STATUS_NET_SPEED</td><td>현재 네트워크 데이터 수신 속도</td>
</tr><tr>
<td>NET_STATUS_VIDEO_FPS</td><td>스트리밍 미디어의 현재 비디오 프레임 레이트</td>
</tr><tr>
<td>NET_STATUS_VIDEO_BITRATE</td><td>스트리밍 미디어의 현재 비디오 비트 레이트(Kbps)</td>
</tr><tr>
<td>NET_STATUS_AUDIO_BITRATE</td><td>스트리밍 미디어의 현재 오디오 비트 레이트(Kbps)</td>
</tr><tr>
<td>NET_STATUS_CACHE_SIZE</td><td>버퍼(jitterbuffer) 크기, 현재 버퍼 길이가 0이면 랙 곧 발생</td>
</tr><tr>
<td>NET_STATUS_SERVER_IP</td><td>연결된 서버 IP</td>
</tr></table>