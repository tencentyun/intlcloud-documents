[](id:normal)
## 일반 모드
일반 모드에서 getOutput을 호출하여 `cameraReady` 콜백에 출력 스트림을 가져오면 효과가 아직 작동하지 않기 때문에 얻은 스트림은 SDK에 입력되는 입력 스트림과 동일하며 효과가 작동하기 시작하면 SDK는 자동으로 출력 스트림에 적용합니다. getOutput은 다시 호출할 필요가 없습니다. 비디오 이미지를 최대한 빨리 표시하지만 비디오가 재생되는 순간 효과를 적용할 필요가 없는 경우 이 방법을 사용할 수 있습니다.

반면 `ready` 콜백에서 getOutput을 호출하면 얻은 출력 스트림이 처리됩니다. `ready` 콜백은 `cameraReady`보다 늦게 발생하기 때문에 비디오가 표시되는 순간에 효과를 적용하고 싶지만 비디오가 가능한 한 빨리 재생되기를 기대하지 않는 경우 `ready` 콜백에서 getOutput을 호출할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/38365734db212ba293fbd283cdcbf3a9.jpg)

예시 코드는 다음과 같습니다.

```javascript
// 인증 매개변수 가져오기
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 자세한 내용은 「License 구성 및 사용 - 서명」을 참고하십시오.
};

// 일반 모드에서 SDK를 초기화할 때 input 또는 camera 매개변수를 전달합니다.
const config = {
	auth: authData, // 인증 매개변수
    beautify: { // 뷰티필터 매개변수
        whiten: 0.1,
        dermabrasion: 0.5,
        lift: 0,
        shave: 0,
        eye: 0.2,
        chin: 0,
    },
    input: inputStream // SDK에 입력되는 input 스트림 데이터를 준비합니다. 자세한 내용은 「매개변수 및 메소드 - 초기화 매개변수」를 참고하십시오.
}
const sdk = new ArSdk(
	// sdk를 초기화하기 위해 config 객체를 전달합니다.
	config
)
// 인증 성공 후 sdk는 즉시 created 콜백을 트리거합니다.
sdk.on('created', () => {
    // created 콜백에서 필터 및 효과 목록을 풀링하여 표시합니다.
    sdk.getEffectList({
        Type: 'Preset',
        Label: '메이크업',
    }).then(res => {
        effectList = res
    });
    sdk.getCommonFilter().then(res => {
        filterList = res
    })
})

// 다른 콜백에서 getOutput을 호출하여 얻은 데이터는 약간 다릅니다. 귀하의 필요에 맞는 것을 선택하십시오.
sdk.on('cameraReady', async () => {
	const output = await sdk.getOutput() // 뷰티필터 매개변수가 적용되지 않았습니다.
    // 스트림 재생
    ...
})
sdk.on('ready', async () => {
    const output = await sdk.getOutput() // 뷰티필터 매개변수가 적용되었습니다.
    // 스트림 재생
    ...
    // ready 콜백에서 setEffect/setBeautify/setFilter를 호출합니다.
})

```

[](id:preliminary)
## 사전 초기화(v0.2.0부터 지원)
SDK를 처음 로딩할 때 탐지 모듈을 초기화하기 위해 정적 리소스를 다운로드해야 합니다. 결과적으로 SDK의 로딩은 네트워크 상태의 영향을 받습니다. 일부 시나리오에서는 가능한 한 빨리 비디오 이미지를 표시하고 싶을 수 있으므로 정적 리소스를 미리 로딩하는 사전 초기화 계획을 제공합니다.

**사전 초기화를 위한 사용 사례**
- 사례1: 웹페이지 초기화 시 효과 SDK가 필요하지 않습니다. 사용자가 특정 작업을 수행한 후에만 비디오가 표시됩니다.
- 사례2: 페이지 B에 뷰티필터 효과가 필요하고 페이지 B는 페이지 A에서 리디렉션합니다.
이러한 경우 리소스를 미리 로딩하고(가능한 한 빨리), 필요한 경우 SDK에 입력 스트림을 제공한 다음 처리된 출력 스트림을 얻을 수 있습니다.

예시: 사례1의 경우 웹 페이지가 초기화될 때 리소스를 로딩할 수 있습니다. 사례2의 경우 페이지 A에서 SDK 인스턴스를 가져와 페이지 B로 전달할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6cc0d286584d1a10db1e5764b167f092.jpg)

**아래 코드는 사례1에서 작동합니다**
```html
<button id="start">카메라 활성화</button>
```
```javascript
// 인증 정보 가져오기
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 자세한 내용은 「License 구성 및 사용 - 서명」을 참고하십시오.
};

// sdk 초기화 시 input 또는 camera 매개변수를 전달하지 마십시오. 인스턴스를 얻은 후 sdk는 필요한 리소스 로딩을 시작합니다.
const config = {
	auth: authData, // 인증 매개변수
    beautify: { // 뷰티필터 매개변수
        whiten: 0.1,
        dermabrasion: 0.5,
        lift: 0,
        shave: 0,
        eye: 0.2,
        chin: 0,
    },
}
const sdk = new ArSdk(
	// sdk를 초기화하기 위해 config 객체를 전달합니다.
	config
)
// 인증 성공 후 sdk는 즉시 created 콜백을 트리거합니다.
sdk.on('created', () => {
    // created 콜백에서 필터 및 효과 목록을 풀링하여 표시합니다.
    sdk.getEffectList({
        Type: 'Preset',
        Label: '메이크업',
    }).then(res => {
        effectList = res
    });
    sdk.getCommonFilter().then(res => {
        filterList = res
    })
})
// resourceReady는 필요한 리소스가 준비되었음을 나타냅니다. 이 콜백을 수신한 후 initCore를 호출하여 SDK에 입력 스트림을 제공할 수 있습니다.
sdk.on('resourceReady', () => {
})
// 이 모드에서 SDK는 initCore가 호출된 후에만 ready 콜백을 트리거합니다.
sdk.on('ready', async () => {
	const output = await sdk.getOutput() // 뷰티필터가 적용되었습니다.
    // 스트림 재생
    ...
    // ready 콜백에서 setEffect/setBeautify/setFilter를 호출합니다.
})
// 사용자가 카메라를 켤 때 SDK에 스트림 데이터 제공
document.getElementById('start').onclick = async function(){
    const devices = await navigator.mediaDevices.enumerateDevices()
    const cameraDevice = devices.find(d=>d.kind === 'videoinput')
    navigator.mediaDevices.getUserMedia({
        audio: false,
        video: {
            deviceId: cameraDevice.deviceId
            ... // 기타 설정
        }
    }).then(mediaStream => {
        // 이 모드에서는 resourceReady 콜백 후에 initCore를 호출해야 합니다.
        sdk.initCore({
            input: mediaStream // SDK에 입력되는 스트림 데이터를 input으로 준비합니다. 자세한 내용은 「SDK 통합 - 매개변수 및 API」를 참고하십시오.
        })
    })    
}
```

