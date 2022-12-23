>?스트림 푸시 SDK는 현재 베타 테스트 중입니다. 공식 버전의 과금 규칙이 적용됩니다.

SDK는 여러 비디오 스트림 혼합(예: PiP), 이미지 효과 처리(예: 미러링 및 필터), 기타 요소(예: 워터마크 및 텍스트) 추가를 포함하여 다양한 비디오 스트림 이미지 처리 기능을 제공합니다. 기본 프로세스는 다음과 같습니다. SDK는 먼저 여러 스트림을 수집하고 로컬에서 혼합하여 이미지를 결합하고 오디오를 혼합합니다. 그런 다음 다른 효과를 처리합니다. 모든 기능은 브라우저의 지원에 의존하므로 SDK에는 브라우저 성능에 대한 특정 요구 사항이 있습니다. 구체적인 API 프로토콜은 [TXVideoEffectManager](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXVideoEffectManager.html)를 참고하십시오. 본문은 로컬 스트림 혼합의 기본 사용법을 설명합니다.

## 기본 사용
로컬 스트림 혼합 기능을 사용하려면 SDK를 초기화하고 SDK 인스턴스 livePusher를 가져와야 합니다. 초기화 코드는 [WebRTC 프로토콜 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/41620)을 참고하십시오.

### 1단계: 비디오 효과 관리 인스턴스 가져오기
```javascript
var videoEffectManager = livePusher.getVideoEffectManager();
```

### 2단계: 로컬 스트림 혼합 활성화
먼저 로컬 스트림 혼합 기능을 활성화해야 합니다. 기본적으로 SDK는 하나의 비디오 스트림과 오디오 스트림만 수집합니다. 이 기능이 활성화되면 SDK는 브라우저에서 로컬로 혼합되는 여러 스트림을 수집할 수 있습니다.
```javascript
videoEffectManager.enableMixing(true);
```

### 3단계: 스트림 혼합 매개변수 설정
스트림 혼합 매개변수, 특히 스트림 혼합 후 비디오 출력의 해상도와 프레임 레이트를 설정합니다.
```javascript
videoEffectManager.setMixingConfig({
	videoWidth: 1280,
	videoHeight: 720,
	videoFramerate: 15
});
```

### 4단계: 여러 스트림 수집
로컬 스트림 혼합이 활성화되면 SDK는 카메라 및 공유 화면과 같은 여러 스트림을 수집하기 시작합니다. 후속 작업에 필요하므로 스트림 ID를 유지해야 합니다.
```javascript
var cameraStreamId = null;
var screenStreamId = null;

livePusher.startCamera().then((streamId) => {
	cameraStreamId = streamId;
}).catch((error) => {
	console.log('카메라 켜기 실패:'+ error.toString());
});

livePusher.startScreenCapture().then((streamId) => {
	screenStreamId = streamId;
}).catch((error) => {
	console.log('화면 공유 실패:'+ error.toString());
});
```

### 5단계: 이미지 레이아웃 설정

수집된 두 스트림의 이미지 레이아웃을 설정합니다. 여기에서 공유 화면이 메인 이미지로 표시되며 카메라 이미지는 왼쪽 상단에 표시됩니다. 특정 매개변수 구성에 대해서는 [TXLayoutConfig](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXVideoEffectManager.html#~TXLayoutConfig)를 참고하십시오.
```javascript
videoEffectManager.setLayout([{
	streamId: screenStreamId,
	x: 640,
	y: 360,
	width: 1280,
	height: 720,
	zOrder: 1
}, {
	streamId: cameraStreamId,
	x: 160,
	y: 90,
	width: 320,
	height: 180,
	zOrder: 2
}]);
```

### 6단계: 미러링 효과 설정
카메라에 의해 수집된 이미지가 실제로 반전되므로 카메라 이미지를 미러링합니다.
```javascript
	videoEffectManager.setMirror({
	streamId: cameraStreamId,
	mirrorType: 1
});
```

### 7단계: 워터마크 추가
이미지 객체를 준비하고 비디오 스트림 이미지에 워터마크로 추가합니다. 여기에서 워터마크 이미지는 오른쪽 상단 모서리에 배치됩니다.
```javascript
var image = new Image();
image.src = './xxx.png'; // 이미지 주소는 다른 도메인에 속할 수 없음에 유의해야하며, 그렇지 않으면 도메인 간 문제가 발생합니다

videoEffectManager.setWatermark({
	image: image,
	x: 1230,
	y: 50,
	width: 100,
	height: 100,
	zOrder: 3
});
```

### 8단계: 스트림 푸시 시작
상기 단계를 거친 후 PiP 레이아웃, 미러링된 이미지 및 워터마크 출력이 포함된 비디오 스트림을 서버로 푸시합니다.
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```

>? WebRTC 기반 스트림 혼합 API에 대한 자세한 내용은 [TXLivePusher](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXLivePusher.html)를 참고하십시오.