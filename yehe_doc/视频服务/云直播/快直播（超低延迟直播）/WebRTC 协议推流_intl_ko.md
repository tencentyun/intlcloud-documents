TXLivePusher 푸시 스트리밍 SDK는 주로 비디오 클라우드의 LEB(초저지연 라이브 스트리밍) 푸시 스트리밍에 사용되며, 브라우저가 수집한 멀티미디어 화면을 WebRTC를 통해 라이브 스트리밍 서버로 푸시하는 역할을 합니다. 현재 카메라 푸시 스트리밍, 화면 녹화 푸시 스트리밍 및 로컬 미디어 파일 푸시 스트리밍을 지원합니다.

## 기본 지식

연결 전 다음 기본 지식을 알아두어야 합니다.

### 푸시 스트리밍 주소 조합

Tencent Cloud CSS 서비스 사용 시, 푸시 스트리밍 URL은 아래와 같이 Tencent Cloud 표준에 부합하는 푸시 스트리밍 URL 형식을 충족해야 하며 네 부분으로 구성됩니다.

![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)

인증 Key 부분은 옵션이며, 링크 도용 방지가 필요한 경우 푸시 스트리밍 인증을 활성화하십시오. 구체적인 설명은 [라이브 방송 URL 직접 조합](https://intl.cloud.tencent.com/document/product/267/38393)을 참고하십시오.

### 브라우저 지원

LEB 푸시 스트리밍은 WebRTC를 기반으로 구현되며 WebRTC에 대한 운영체제 및 브라우저의 지원에 종속되어 있습니다.

또한 브라우저의 멀티미디어 화면 캡처 기능은 모바일에서 제대로 지원되지 않습니다. 예를 들어, 모바일 브라우저는 화면 녹화를 지원하지 않으며 iOS 14.3 이상에서만 사용자 카메라 장치 가져오기가 지원됩니다. 따라서 푸시 스트리밍 SDK는 주로 데스크톱 브라우저에 적합하며, 최신 버전의 chrome, Firefox 및 Safari 브라우저에서 LEB 푸시 스트리밍이 모두 지원됩니다.

모바일은 [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38157) 사용을 통한 푸시 스트리밍을 권장합니다.

## 연결 방법

### 1단계: 페이지 준비 작업

라이브 방송 푸시 스트리밍을 진행할 페이지(데스크톱)에 초기화 스크립트를 가져옵니다.

```html
<script src="https://imgcache.qq.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```
>? 스크립트는 HTML의 body 부분에 삽입되어야 하며 head 부분에 삽입되면 오류가 보고됩니다.

도메인 제한 영역에 있는 경우 다음 링크를 가져옵니다.

```html
<script src="https://cloudcache.tencent-cloud.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```

### 2단계: HTML에 컨테이너 배치

로컬 멀티미디어 화면을 표시해야 하는 페이지 위치에 플레이어 컨테이너를 추가합니다. 즉, div를 넣고 이름을 id_local_video와 같이 지정하면 로컬 비디오 화면이 컨테이너에서 렌더링됩니다. 컨테이너의 크기 제어의 경우 div의 CSS 양식을 사용하여 제어할 수 있으며 샘플 코드는 다음과 같습니다.

```html
<div id="id_local_video" style="width:100%;height:500px;display:flex;align-items:center;justify-content:center;"></div>
```

### 3단계: 라이브 방송 푸시 스트리밍
1. **푸시 스트리밍 SDK 인스턴스 생성: **
전역 객체 'TXLivePusher'를 통해 SDK 인스턴스를 생성하고, 후속 작업은 해당 인스턴스를 통해 완료합니다.
```javascript
var livePusher = new TXLivePusher();
```
2. **로컬 비디오 플레이어 컨테이너 지정: **
로컬 비디오 플레이어 컨테이너 div를 지정하면 브라우저에서 수집한 멀티미디어 화면이 div로 렌더링됩니다.
```javascript
livePusher.setRenderView('id_local_video');
```
>?'setRenderView'를 호출하여 생성된 video 요소는 기본적으로 소리가 나며, 음소거가 필요한 경우 video 요소를 직접 가져오기 하여 작업할 수 있습니다.
>```javascript
>document.getElementById('id_local_video').getElementsByTagName('video')[0].muted = true;
>```
```
3. **멀티미디어 품질 설정: **
멀티미디어 스트림 수집 이전에 먼저 멀티미디어 품질을 설정하고, 사전 설정된 품질 매개변수가 요구 사항을 충족하지 않는 경우 개별적인 사용자 정의 설정을 진행할 수 있습니다.
​```javascript
// 비디오 품질 설정
livePusher.setVideoQuality('720p');
// 오디오 품질 설정
livePusher.setAudioQuality('standard');
// 프레임 레이트 사용자 정의
livePusher.setProperty('setVideoFPS', 25);
```
4. **스트림 수집 시작: **
현재 카메라 디바이스, 마이크 디바이스 수집, 화면 녹화 및 로컬 미디어 파일 스트림 수집을 지원합니다. 멀티미디어 스트림이 성공적으로 수집되면 로컬로 수집된 멀티미디어 화면이 플레이어 컨테이너에서 재생됩니다.
```javascript
// 카메라 켜기
livePusher.startCamera();
// 마이크 켜기
livePusher.startMicrophone();
```
5. **푸시 스트리밍 시작: **
Tencent Cloud LEB 푸시 스트리밍 주소를 전달하고 푸시 스트리밍을 시작합니다. 푸시 스트리밍 주소의 형식은 [Tencent Cloud LVB URL](https://intl.cloud.tencent.com/document/product/267/38393)을 참고하십시오. RTMP 푸시 스트리밍 주소 앞의 `rtmp://`를 `webrtc://`로 바꾸면 됩니다.
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```
>?푸시 스트리밍 이전에 멀티미디어 스트림이 수집되었는지 확인하십시오. 그렇지 않으면 푸시 스트리밍 인터페이스 호출이 실패하게 됩니다. 멀티미디어 스트림 수집 후 자동 푸시 스트리밍을 구현하려면 콜백 이벤트 알림을 통해, 첫 번째 프레임이 성공적으로 수집되었다는 알림을 받으면 스트림을 다시 푸시합니다. 비디오 스트림과 오디오 스트림이 동시에 수집된 경우 첫 번째 비디오 프레임과 첫 번째 오디오 프레임의 콜백 알림을 모두 수신한 후 푸시 스트림밍을 진행해야 합니다.

```javascript
var hasVideo = false;
var hasAudio = false;
var isPush = false;
livePusher.setObserver({
		onCaptureFirstAudioFrame: function() {
			hasAudio = true;
			if (hasVideo && !isPush) {
				isPush = true;
				livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
			}
		},
		onCaptureFirstVideoFrame: function() {
			hasVideo = true;
			if (hasAudio && !isPush) {
				isPush = true;
				livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
			}
		}
});
```

</dx-codeblock>
6. **LEB 푸시 스트리밍 중지: **
```javascript
livePusher.stopPush();
```
7. **멀티미디어 스트림 수집 중지: **
```javascript
// 카메라 끄기
livePusher.stopCamera();
// 마이크 끄기
livePusher.stopMicrophone();
```

## 고급 전략
### 호환성
SDK는 WebRTC와 브라우저의 호환성을 확인하는 스태틱 메소드를 제공합니다.

<dx-codeblock>
::: javascript javascript
TXLivePusher.checkSupport().then(function(data) {  
	// WebRTC 지원 여부  
	if (data.isWebRTCSupported) {    
		console.log('WebRTC Support');  
	} else {    
		console.log('WebRTC Not Support');  
	}  
	// H264 인코딩 지원 여부  
	if (data.isH264EncodeSupported) {    
		console.log('H264 Encode Support');  
	} else {    
		console.log('H264 Encode Not Support');  
	}
});
:::
</dx-codeblock>

### 콜백 이벤트 알림
SDK는 현재 콜백 이벤트 알림을 제공하고 있으며, Observer 설정을 통해 SDK 내부 상태 정보 및 WebRTC 관련 데이터 통계를 알아볼 수 있습니다. 자세한 내용은 [TXLivePusherObserver](https://intl.cloud.tencent.com/document/product/1071/41272)를 참고하십시오.
<dx-codeblock>
::: javascript javascript
livePusher.setObserver({
	// 푸시 스트리밍 경고 메시지
	onWarning: function(code, msg) {
		console.log(code, msg);
	},
	// 푸시 스트리밍 연결 상태
	onPushStatusUpdate: function(status, msg) {
		console.log(status, msg);
	},
	// 푸시 스트리밍 통계 데이터
	onStatisticsUpdate: function(data) {
		console.log('video fps is ' + data.video.framesPerSecond);
	}
});
:::
</dx-codeblock>

### 디바이스 관리

SDK는 사용자가 디바이스 리스트 가져오기, 디바이스 전환과 같은 작업을 수행하는 데 도움이 되는 디바이스 관리 인스턴스를 제공합니다.
<dx-codeblock>
::: javascript javascript
var deviceManager = livePusher.getDeviceManager();
// 디바이스 리스트 가져오기
deviceManager.getDevicesList().then(function(data) {
	data.forEach(function(device) {
			console.log(device.deviceId, device.deviceName);  
	});
});
// 카메라 디바이스 전환
deviceManager.switchCamera('camera_device_id');
:::
</dx-codeblock>





