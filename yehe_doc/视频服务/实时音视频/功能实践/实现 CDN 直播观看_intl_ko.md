## 적용 시나리오
CDN 라이브 방송 시청은 ‘CDN 릴레이 라이브 방송’이라고도 하며, TRTC가 UDT 프로토콜을 통해 멀티미디어 데이터를 전송하는 반면 LVB CDN의 경우 RTMP, HLS, FLV등의 프로토콜을 통해 데이터 전송을 하기 때문에, TRTC의 멀티미디어 데이터가 **릴레이**로 CDN 라이브 방송으로 전달되어야만 시청자가 라이브 CDN을 통해 시청할 수 있습니다. 

TRTC에 CDN 시청을 접목하는 방식은 다음과 같은 2가지 문제를 해결하는 데에 주로 사용됩니다.
- **문제 1: 매우 높은 동시 시청 트래픽**
TRTC의 짧은 딜레이 시간 시청은 하나의 방에서 최대 10만명까지 지원 가능합니다. CDN 시청은 지연 시간이 다소 길지만 10만명 이상의 동시 시청 지원이 가능하며 CDN의 요금이 더욱 저렴합니다.
- **문제 2: 모바일 웹페이지 재생**
TRTC는 WebRTC API의 접근을 지원하지만 주로 Chrome 바탕화면 브라우저에 사용되며, 모바일 브라우저에서의 호환성이 매우 떨어지고 특히 안드로이드폰 브라우저의 WebRTC 지원 성능은 대체적으로 상당히 낮은 수준입니다. 따라서 모바일 디바이스에서 Web 화면을 통해 라이브 방송 컨텐츠를 즐기고 싶다면 HLS(m3u8) 재생 프로토콜을 추천하는데 이 역시 라이브 방송 CDN을 통해 HLS 프로토콜을 지원합니다. 


## 원리 설명
Tencent Cloud는 트랜스 코딩 클러스터를 사용해 TRTC의 멀티미디어 데이터를 라이브 방송 CDN 시스템에 릴레이하며, 해당 클러스터는 TRTC가 사용한 UDP 프로토콜을 표준화된 라이브 방송 RTMP 프로토콜로 전환합니다. 
<span id="directCDN"></span>
**싱글채널 화면의 릴레이 라이브 방송**
TRTC 방에 호스트가 한명 뿐인 경우, TRTC의 릴레이 푸시 스트림은 표준 RTMP 프로토콜의 다이렉트 푸시 기능과 동일하지만 나쁜 네트워크 상태에 대한 저항성은 TRTC의 UDP가 RTMP 보다 높습니다.
![](https://main.qcloudimg.com/raw/23ac68cb46b06cc4eb6000fa98500dc4.jpg)

<span id="mixCDN"></span>
**믹스채널 화면의 릴레이 라이브 방송**
TRTC가 가장 두각을 나타내는 분야는 멀티미디어 인터랙션으로 하나의 방에 여러 호스트가 있는 상황에서 CDN 시청 디바이스에 하나의 멀티미디어 화면만을 가져오려는 경우 [클라우드 혼합 스트림](https://intl.cloud.tencent.com/document/product/647/34618)을 이용해 다중 채널의 화면을 하나의 채널로 결합할 수 있는데, 그 원리는 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/77eeed776e61c3a6bd0e1669e5747727.jpg)

>? **다중 채널의 CDN 화면을 직접 스트리밍 하지 않는 이유는 무엇입니까?**
>다중 채널의 CDN 화면을 재생하는 경우 여러 채널의 딜레이 타임 조절이 어렵고 동시에 다중 채널 화면을 끌어오기 위해 더 많은 다운로드 트래픽이 소모되기 때문에 업계에서는 일반적으로 클라우드 혼합 스트리밍 솔루션을 채택하고 있습니다.

## 전제 조건
이미 Tencent [LVB](https://console.cloud.tencent.com/live) 서비스를 이용중입니다. 정부 관련 기관의 기준에 따라 라이브 방송은 반드시 스트리밍 도메인을 설정해야 하며, 구체적인 내용은 [외부 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참조하시기 바랍니다.

## 사용 순서

<span id="step1"></span>
### 1단계: 릴레이 푸시 스트림 기능 활성화

1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2. 왼쪽 메뉴에서 [애플리케이션 관리]를 선택한 후 대상 애플리케이션이 속한 라인의 [기능 설정]을 클릭합니다.
3. [릴레이 푸시 설정]에서 [릴레이 푸시 활성화] 우측의![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png)를 클릭하면, [릴레이 푸시 스트림 기능 활성화] 대화창이 뜨는데 여기서 [릴레이 푸시 스트림 기능 활성화]를 클릭하면 바로 활성화됩니다.


<span id="step2"></span>
### 2단계: 재생 도메인 설정 및 CNAME 완료
1. [LVB 콘솔](https://console.cloud.tencent.com/live/)에 로그인합니다.
2. 왼쪽 메뉴에서 [도메인 관리]를 선택하면 도메인 목록에 `xxxxx.livepush.myqcloud.com` 양식의 푸시 도메인이 추가된 것을 볼 수 있는데 여기에서 xxxxx는 bizid라고 하는 숫자로, TRTC 콘솔 >[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)>[애플리케이션 정보]에서 bizid 정보를 검색하실 수 있습니다.
3. [도메인 추가]를 클릭해 기존에 준비한 도메인을 입력하고 도메인 유형을 [재생 도메인]으로 선택한 후 가속 리전을 선택(디폴트 값은 [중국대륙]), [확인]을 클릭합니다. 
4. 도메인 추가가 완료되면 시스템에서 자동으로 CNAME 도메인(뒤에 `.liveplay.myqcloud.com`이 붙음)을 할당합니다. CNAME 도메인은 직접 액세스할 수 없으며, 도메인 서비스 제공 업체에서 CNAME 설정을 완료하고, 설정이 적용되면 LVB 서비스를 이용할 수 있습니다. 자세한 설정 방법은 [CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참조 바랍니다.

>! **푸시 도메인을 추가할 필요가 없습니다**, [1단계]에서 릴레이 라이브 방송 기능을 활성화하면 Tencent Cloud가 자동으로 LVB 콘솔에 `xxxxx.livepush.myqcloud.com` 형식의 푸시 도메인을 추가하는데, 해당 도메인은 Tencent LVB 서비스와 TRTC 서비스 간에 약정된 디폴트 푸시 도메인으로, 당분간은 수정이 불가합니다.

<span id="step3"></span>
### 3단계: TRTC의 멀티미디어 스트림과 라이브 방송 streamId의 연동
릴레이 푸시 스트림 기능을 켜면 TRTC 방 안의 모든 채널 화면마다 해당되는 재생 주소가 할당되는데, 주소 형식은 다음과 같습니다.
```
http://재생 도메인/live/[streamId].flv
```
주소의 streamId로 LVB에서 라이브 스트림을 고유하게 식별할 수 있으며, streamId는 사용자가 지정하거나 시스템이 생성한 기본값을 사용할 수 있습니다.

#### 방법1: 사용자 정의 streamId
‘TRTCCloud’에서 ‘enterRoom’함수를 호출 할 때, ‘TRTCParams’ 매개변수의 ‘streamId’ 매개변수를 설정하여 라이브 스트림 ID를 지정할 수 있습니다.
iOS 용 Objective-C 코드를 예로 들어 보겠습니다.

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC의 SDKAppID, 애플리케이션 생성 후 획득
param.roomId   = 1001;           // 방 번호
param.userId   = @"rexchang";    // 사용자 이름
param.userSig  = @"xxxxxxxx";    // 로그인 서명
param.role     = TRTCRoleAnchor; // 역할: 호스트
param.streamId = @"stream1001";  // 스트리밍 ID
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // LIVE 모드를 사용하십시오.
```
userSig의 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

#### 방법2; 시스템 생성 streamId
자동 릴레이 푸시가 활성화 된 후 사용자 정의 streamId를 지정하지 않으면 시스템이 다음 규칙에 따라 자동으로 streamId를 생성합니다.

- **streamId를 조합하는 데 사용되는 필드**
  - SDKAppID: [콘솔](https://console.cloud.tencent.com/trtc/app)>[애플리케이션 관리]>[애플리케이션 정보]에서 확인할 수 있습니다.
  - bizid: [콘솔](https://console.cloud.tencent.com/trtc/app)>[애플리케이션 관리]>[애플리케이션 정보]에서 확인할 수 있습니다.
  - roomId: ‘enterRoom’ 함수의 매개변수 ‘TRTCParams’ 중에서 사용자가 지정합니다.
  - userId: ‘enterRoom’ 함수의 매개변수 ‘TRTCParams’ 중에서 사용자가 지정합니다.
  - streamType: 카메라 화면을 main으로, 화면 공유를 aux로 합니다(WebRTC는 하나의 업스트림 채널만을 동시 지원하므로 WebRTC에서는 화면 공유의 스트리밍 유형을 main으로 합니다).

- **streamId 조합 컴퓨팅 규칙**
 <table>
<tr>
<th>조합</th>
<th>2020년 01월 09일 및 이후 생성된 애플리케이션</th>
<th>2020년 01월 09일 이전에 생성되어 사용된 애플리케이션</th>
</tr>
<tr>
<td>조합규칙</td>
<td>streamId = urlencode(sdkAppId_roomId_userId_streamType)</td>
<td>StreamId = bizid_MD5(roomId_userId_streamType)</td>
</tr>
<tr>
<td>컴퓨팅 예시</td>
<td>예시：sdkAppId = 12345678, roomId = 12345, userId = userA, 사용자는 현재 카메라를 사용하고 있습니다. <br>그러면：streamId = 12345678_12345_userA_main</td>
<td>예시：bizid = 1234, roomId = 12345, userId = userA, 사용자는 현재 카메라를 사용하고 있습니다. <br>그러면：streamId = 1234_MD5(12345_userA_main) = 1234_8D0261436C375BB0DEA901D86D7D70E8</td>
</tr>
</table>


<span id="step4"></span>
### 4단계: 다중 화면 제어를 위한 하이브리드 솔루션

믹싱된 라이브 방송 이미지를 얻으려면 TRTCCloud의 ‘setMixTranscodingConfig’ 인터페이스를 호출하여 클라우드 혼합 스트림 트랜스 코딩을 시작해야 하며, 해당 인터페이스의 매개변수인 `TRTCTranscodingConfig`를 구성에 적용할 수 있습니다.
 - 각 하위 화면의 배치 위치 및 크기.
 - 혼합 화면의 품질 및 인코딩 매개변수.

화면 레이아웃의 세부 배치 방법은 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618)을 참조하시고, 전체 프로세스에 관련된 개별 모듈의 관계는 [원리 설명](#mixCDN)을 참조하시기 바랍니다.

>! `setMixTranscodingConfig`는 장치에서 혼합 스트리밍을 실행하지 않고 혼합 스트리밍 구성을 클라우드로 전송하여 클라우드 서버에서 혼합 스트리밍과 트랜스 코딩을 실행합니다. 혼합 스트리밍과 트랜스 코딩 모두 원본 멀티미디어 데이터를 디코딩하고 다시 인코딩해야 하기 때문에 더 긴 처리 시간이 소요됩니다. 따라서 혼합 화면의 실제 시청 지연 시간은 단독 화면 보다 1s-2s 정도 깁니다.

<span id="step5"></span>
### 5단계: 재생 주소 가져오기 및 재생 연결
[2단계](#step2) 재생 도메인 설정과 [3단계](#step3) streamId의 매핑을 완료하면 라이브 방송의 재생 주소를 얻을 수 있습니다. 재생 주소의 표준 형식은 다음과 같습니다.
```
http://재생 도메인/live/[streamId].flv
```

예를 들어, 재생 도메인 이름이 ‘live.myhost.com’이고 방 항목 매개 변수를 사용하여 방(1001)에있는 사용자 userA의 라이브 방송 스트리밍 Id를 streamId = "streamd1001"로 지정합니다.
그러면 다음과 같은 3개의 재생 주소를 얻을 수 있습니다.
```
 rtmp 프로토콜의 재생 주소: rtmp://live.myhost.com/live/streamd1001
 flv 프로토콜의 재생 주소: http://live.myhost.com/live/streamd1001.flv
 hls 프로토콜의 재생 주소: http://live.myhost.com/live/streamd1001.m3u8
```

‘http’로 시작하고 ‘.flv’을 확장자명으로 하는 **http - flv** 주소를 권장합니다. 해당 주소는 재생 지연 시간이 짧고 바로 재생 효과가 좋으면서 안정성 및 신뢰성도 뛰어납니다.
플레이어 선택과 관련해서는 다음 표의 가이드 방안을 참조하시기 바랍니다.

| 플랫폼 | 연결 문서 | API 개요 | 지원포맷|
|:-------:|:-------:|:-------:|-------|
| iOS App| [액세스 가이드](https://intl.cloud.tencent.com/document/product/1071/38159) | TXLivePlayer(iOS)  | 권장 FLV |
| Android App | [액세스 가이드](https://intl.cloud.tencent.com/document/product/1071/38160) | TXLivePlayer(Android) | 권장 FLV |
| Web 브라우저 | 액세스 가이드 | - |  바탕화면 Chrome 브라우저 지원 FLV <br> Mac Safari 및 모바일 핸드폰 브라우저는 HLS만 지원 |


<span id="step6"></span>
### 6단계: 재생 딜레이 최적화

릴레이 라이브 방송이 시작된 뒤 http - flv 주소는 라이브 방송 CDN의 확산 및 배포를 거치게 되므로 시청 지연 시간이 TRTC 라이브 방송실의 통화 지연 시간 보다 확실히 길어집니다.
현재 Tencent Cloud LVB CDN 기술을 TXLivePlayer를 통해 구현할 경우 다음 표와 같은 딜레이 값을 얻을 수 있습니다:

| 릴레이 스트림 유형 | TXLivePlayer의 재생 모드 |  평균 딜레이 시간 |  테스트 결과 |
|:-------:|:-------:|:--------:|:---------:|
| 단독 화면 | 초고속모드（권장） | **2s - 3s** | 하단 그림의 좌측 비교 차트(주황색)|
| 혼합 화면 | 초고속모드（권장） | **4s - 5s** | 하단 그림의 우측 비교 차트(파란색)|

실제 측정된 딜레이 시간이 위의 표보다 더 긴 경우 다음 가이드에 따라 딜레이 시간을 최적화 할 수 있습니다:

- **TRTC SDK 자체 TXLivePlayer 사용**
ffmpeg 커널을 기반으로 패키지된 일반 ijkplayer 또는 ffmpeg 플레이어는 딜레이 시간을 조정할 수 없으며, 이러한 유형의 플레이어를 사용하여 위의 라이브 스트림 주소를 재생하면 일반적으로 딜레이 시간을 제어 할 수 없습니다. TXLivePlayer에는 딜레이를 제어할 수 있는 자체 개발된 재생 엔진이 탑재되어 있습니다.

- **TXLivePlayer의 재생 모드를 초고속 모드로 설정**
TXLivePlayerConfig의 세 가지 매개변수를 설정하여 초고속 모드를 구현할 수 있으며 [iOS](https://intl.cloud.tencent.com/document/product/1071/38159#Delay)를 예로 들어보겠습니다.
iOS 용 Objective-C 코드를 예로 들어 보겠습니다.
```
 // TXLivePlayer의 재생 모드를 초고속 모드로 설정
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // 최소 버퍼링 1s
    config.maxAutoAdjustCacheTime = 1; // 최대 버퍼링 1s
    [player setConfig:config];
    // 라이브 방송 재생 시작
```

<span id="expense"></span>
## 관련 비용

CDN 라이브 방송 시청 구현 비용에는 **시청료**와 **트랜스 코딩 비용**이 포함되어 있는데, 시청료는 기본료이고 트랜스 코딩 비용은 [다중 채널 화면 믹싱](# mixCDN)시에만 과금됩니다.

>!본문의 가격은 예시로 단순 참고용입니다. 실제 금액과 다른 경우 [LVB> 표준 라이브 방송](https://intl.cloud.tencent.com/document/product/267/2819)의 과금 설명을 기준으로 적용합니다. 

### 시청료: 라이브 방송 CDN을 통해 시청할 때 발생하는 비용

라이브 CDN을 통해 시청할 때 **LVB**는 시청으로 인하여 발생한 다운 스트림 트래픽/대역폭 요금을 청구하며, 실제 수요에 따라 본인에게 적합한 과금 방식을 선택할 수 있는데, 기본적으로는 트래픽 과금 방식이 적용됩니다. 자세한 내용은 [LVB > 표준 라이브 방송 > 트래픽 대역폭](https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#traffic-and-bandwidth) 과금 설명을 참조하세요. 


### 트랜스 코딩 비용: 다중 채널 화면 혼합 활성화 시 부과
[다중 채널 화면 믹싱](#mixCDN)을 활성화하는 경우, 혼합 스트림으로 인한 디코딩 및 인코딩이 필요하기 때문에 별도의 혼합 스트림 트랜스 코딩 비용이 발생합니다. 혼합 스트림 트랜스 코딩은 해상도 및 트랜스 코딩 시간에 따라 과금되며, 호스트용으로 해상도가 높을수록, 마이크 연결 시간(일반적으로 마이크 연결이 필요한 상황에서 혼합 스트림 트랜스 코딩이 필요함)이 길수록 비용이 높아집니다. 자세한 내용은 [LVB > 라이브 방송 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#lvb-transcoding) 과금 설명을 참조하십시오.

>예를 들어, [setVideoEncodrParam()](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam)을 통해 호스트의 비트레이트(videoBitrate)를 1500kbps, 해상도를 720P로 설정합니다. 호스트 1명과 시청자의 마이크 연결 시간이 1시간이고 해당 마이크 연결 시간 동안 [다중 채널 화면 믹싱](#mixCDN)을 활성화 하는 경우, ‘0.0057USD/분 × 60분 = 0.342USD’의 트랜스 코딩 비용이 발생합니다.

## FAQ
**라이브 방송 방 안에 사용자가 1명만 있을 때 왜 화면이 끊기고 흐릿해지나요?**
`enterRoom`의 TRTCAppScene 매개변수를 **TRTCAppSceneLIVE**로 지정합니다.
VideoCall 모드는 영상 통화에 최적화되어 있어 방에 1명의 사용자만 있을 경우 화면이 사용자의 네트워크 트래픽을 절약하기 위해 낮은 비트 레이트와 프레임 레이트를 유지하기 때문에 화면이 멈추고 흐릿한 것처럼 느껴질 수 있습니다.
