## SDK 통합
[](id:step1)
### 1단계: SDK 가져오기
```javascript
import { ArSdk } from 'tencentcloud-webar';// SDK 클래스
```
프로젝트에 컴파일이 필요하지 않은 경우 다음 방법을 사용하여 SDK를 가져올 수도 있습니다.
```html
<script charset="utf-8" src="https://webar-static.tencent-cloud.com/ar-sdk/resources/latest/webar-sdk.umd.js"></script>
```

[](id:step2)
### 2단계: 인스턴스 초기화
1. SDK 인스턴스를 초기화합니다.
```javascript
// 인증 매개변수 가져오기
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 자세한 내용은 「License 구성 및 사용 - 서명」 참고
};
// SDK 입력 스트림
const stream = await navigator.mediaDevices.getUserMedia({
	audio: true,
	video: { width: w, height: h }
})

const config = {
    module: { // 0.2.0의 새로운 기능
		beautify: true, // 스티커는 물론 뷰티 및 메이크업 효과를 제공하는 효과 모듈 활성화 여부
		segmentation: true // 배경을 변경할 수 있는 키잉 모듈 활성화 여부
	},
	auth: authData, // 인증 매개변수
    input: stream, // input 스트림
	beautify: { // 초기화를 위한 효과 매개변수(선택 사항)
		whiten: 0.1,
		dermabrasion: 0.3,
		eye: 0.2,
		chin: 0,
		lift: 0.1,
		shave: 0.2
	}
}
const sdk = new ArSdk(
	// sdk를 초기화하기 위해 config 객체 전달
	config
)
```
>! 효과 및 세그먼트 모듈을 로딩하는 데 시간이 걸리고 리소스가 소모됩니다. 초기화 중에 필요한 모듈만 활성화할 수 있습니다. 활성화되지 않은 모듈은 로딩되거나 초기화되지 않으며 해당 기능을 사용할 수도 없습니다.

2. input의 경우 `string|HTMLImageElement`를 전달하여 이미지를 처리할 수도 있습니다.
```javascript
const config = {
	auth: authData, // 인증 매개변수
    input: 'https://xxx.png', // input 스트림
}
const sdk = new ArSdk(
	// sdk를 초기화하기 위해 config 객체 전달
	config
)

// created 콜백에 효과 및 필터 목록을 표시할 수 있습니다. 자세한 내용은 「SDK 통합 - 매개변수 및 API」 참고
sdk.on('created', () => {
    // 내장 메이크업 효과 가져오기
    sdk.getEffectList({
        Type: 'Preset',
        Label: '메이크업',
    }).then(res => {
        effectList = res
    });
    // 내장 필터 가져오기
    sdk.getCommonFilter().then(res => {
        filterList = res
    })
})

// ready 콜백에서 setBeautify/setEffect/setFilter 호출
// 자세한 내용은 「SDK 통합 - 뷰티 효과 및 효과 구성」 참고
sdk.on('ready', () => {
    // 뷰티 효과 구성
    sdk.setBeautify({
        whiten: 0.2
    });
    // 특수 효과 구성
    sdk.setEffect({
        id: effectList[0].EffectId,
        intensity: 0.7
    });
    // 필터 구성
    sdk.setFilter(filterList[0].EffectId, 0.5)
})
```

[](id:step3)
### 3단계: 스트림 재생
`ArSdk.prototype.getOutput`을 호출하여 출력 스트림을 가져옵니다.
다른 콜백에서 얻는 출력 스트림은 약간 다릅니다. 귀하의 필요에 맞는 것을 선택하십시오.

- 가능한 한 빨리 비디오 이미지를 표시하려면 `cameraReady` 콜백에서 스트림을 가져와서 재생하십시오. SDK가 리소스를 로딩하지 않았거나 초기화를 완료하지 않았기 때문에 원본 동영상만 재생할 수 있습니다.
```javascript
sdk.on('cameraReady', async () => {
	// cameraReady 콜백에서 출력 스트림을 가져와 비디오 이미지를 더 빨리 표시할 수 있습니다. 그러나 이 시점에서 초기화 매개변수가 적용되지 않았기 때문에 얻은 출력 스트림은 원래 스트림과 동일합니다.
	// 가능한 한 빨리 비디오 이미지를 표시하고 싶지만 표시되는 순간 비디오에 뷰티 효과를 적용할 필요가 없는 경우 이 방법을 선택할 수 있습니다.
	// 뷰티 효과가 작동하기 시작한 후에는 stream을 업데이트할 필요가 없습니다.
	const output = await ar.getOutput();
    // video를 사용하여 출력 스트림을 미리보기
	const video = document.createElement('video')
    video.setAttribute('playsinline', '');
    video.setAttribute('autoplay', '');
    video.srcObject = output
    document.body.appendChild(video)
    video.play()
})
```
- 초기화 및 효과 적용 후 동영상을 재생하려면 ready 재생에서 출력 스트림을 가져와서 재생하십시오.
```javascript
sdk.on('ready', async () => {
    // ready 콜백에서 출력 스트림을 가져오면 초기화 뷰티 효과 매개변수가 이 시점에서 적용되었기 때문에 얻은 output stream에 뷰티 효과가 표시됩니다.
	// ready 콜백은 cameraReady보다 늦게 발생합니다. 비디오가 표시되는 순간 효과를 보여주길 원하지만 가능한 한 빨리 표시되기를 기대하지 않는 경우 output 스트림을 ready 상태로 가져올 수 있습니다.
	const output = await ar.getOutput();
    // video를 사용하여 출력 스트림 미리보기
    const video = document.createElement('video')
    video.setAttribute('playsinline', '');
    video.setAttribute('autoplay', '');
    video.srcObject = output
    document.body.appendChild(video)
    video.play()
})
```

[](id:step4)
### 4단계: 출력 가져오기
`MediaStream`을 가져온 후 라이브 스트리밍 SDK(예: TRTC Web SDK 또는 LEB Web SDK)를 사용하여 스트림을 게시할 수 있습니다.
```javascript
const output = await sdk.getOutput()
```


>!
>- 전달된 input이 이미지인 경우 string 형식의 DataURL이 반환됩니다. 그렇지 않으면 `MediaStream`이 반환됩니다.
>- 출력 스트림의 `video` 트랙은 ArSdk에 의해 실시간으로 처리됩니다. `audio` 트랙(있는 경우)이 유지됩니다.
>- getOutput은 비동기 API입니다. SDK 초기화가 완료되고 스트림을 생성할 수 있는 경우에만 출력이 반환됩니다.
>- FPS 매개변수를 getOutput에 전달하여 출력 프레임 레이트(예시: 15)를 지정할 수 있습니다. 이 매개변수를 전달하지 않으면 원래 프레임 레이트가 유지됩니다.
>- getOutput을 여러 번 호출하여 다양한 시나리오에 대해 서로 다른 프레임 레이트의 스트림을 생성할 수 있습니다(예시: 미리 보기에는 높은 프레임 레이트를 사용하고 스트림 게시에는 낮은 프레임 레이트를 사용할 수 있음).

[](id:step5)
### 5단계: 필터 및 효과 구성
자세한 내용은 [Configuring Filters and Effects](https://intl.cloud.tencent.com/document/product/1143/50104)를 참고하십시오.

## 입력 스트림 업데이트(v0.1.19부터 지원)
장치를 변경하거나 카메라를 활성화/비활성화한 후 새 입력 스트림을 sdk에 공급하려는 경우 sdk를 다시 초기화할 필요가 없습니다. 입력 스트림을 업데이트하려면 `sdk.updateInputStream`을 호출하기만 하면 됩니다.
다음 코드는 컴퓨터의 기본 카메라에서 외부 카메라로 전환한 후 updateInputStream을 사용하여 입력 스트림을 업데이트하는 방법을 보여줍니다.

```javascript

async function getVideoDeviceList(){
    const devices = await navigator.mediaDevices.enumerateDevices()
    const videoDevices = []
    devices.forEach((device)=>{
        if(device.kind === 'videoinput'){
            videoDevices.push({
                label: device.label,
                id: device.deviceId
            })
        }
    })
    return videoDevices
}

async function initDom(){
    const videoDeviceList = await getVideoDeviceList()
    let dom = ''
    videoDeviceList.forEach(device=>{
        dom = `${dom}
        <button id=${device.id} onclick='toggleVideo("${device.id}")'>${device.label}<nbutton>
        `
    })
    const div = document.createElement('div');
    div.id = 'container';
    div.innerHTML = dom;
    document.body.appendChild(div);
}

async function toggleVideo(deviceId){
    const stream = await navigator.mediaDevices.getUserMedia({
        video: {
            deviceId,
            width: 1280,
            height: 720,
          }
    })
	// sdk에서 제공하는 API를 호출하여 입력 스트림을 변경합니다. SDK는 기존 트랙을 stop합니다.
	// 입력 스트림이 업데이트된 후에는 getOutput을 다시 호출할 필요가 없습니다. SDK가 출력을 가져옵니다.
    sdk.updateInputStream(stream) 
}

initDom()

```

## 감지 일시 중지 및 재개
disable 및 enable을 호출하여 수동으로 감지를 일시 중지하고 다시 시작할 수 있습니다. 감지를 일시 중지하면 CPU 사용량을 줄일 수 있습니다.
```html
<button id="disable">감지 비활성화</button>
<button id="enable">감지 활성화</button>
```
```javascript
// 감지를 비활성화하고 원본 스트림 출력
disableButton.onClick = () => {
    sdk.disable()
}
// 감지 활성화 및 처리된 스트림 출력
enableButton.onClick = () => {
    sdk.enable()
}
```
