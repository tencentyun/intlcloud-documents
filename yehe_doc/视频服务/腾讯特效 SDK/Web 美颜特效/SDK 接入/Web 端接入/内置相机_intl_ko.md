장치의 내장 카메라와 함께 SDK를 사용하려는 경우 또는 내장 카메라와 많은 상호 작용이 비즈니스에 포함되는 경우 이 초기화 모드를 선택할 수 있습니다.

[](id:step1)
## 1단계: SDK 가져오기
```javascript
import { ArSdk } from 'tencentcloud-webar';// SDK 클래스
```
프로젝트에 컴파일이 필요하지 않은 경우 다음 방법을 사용하여 SDK를 가져올 수도 있습니다.
```html
<script charset="utf-8" src="https://webar-static.tencent-cloud.com/ar-sdk/resources/latest/webar-sdk.umd.js"></script>
```

[](id:step2)
## 2단계: 인스턴스 초기화
SDK 인스턴스를 초기화합니다.
```javascript
// 인증 정보 가져오기
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 자세한 내용은 「License 구성 및 사용 - 서명」을 참고하십시오.
};

const config = {
    module: { // 0.2.0의 새로운 기능
		beautify: true, // 스티커는 물론 뷰티 및 메이크업 효과를 제공하는 효과 모듈 활성화 여부
		segmentation: true // 배경을 변경할 수 있는 키잉 모듈 활성화 여부
	},
    auth: authData, // 인증 정보
    camera: { // camera 매개변수 전달
        width: 1280,
        height: 720
    },
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
	// sdk를 초기화하기 위해 config 객체를 전달합니다.
	config
)

let effectList = [];
let filterList = [];

sdk.on('created', () => {
    // created 콜백에 효과 및 필터 목록을 표시할 수 있습니다. 자세한 내용은 「SDK 통합 - 매개변수 및 API」를 참고하십시오.
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

// ready 콜백에서 setBeautify/setEffect/setFilter를 호출합니다.
// 자세한 내용은 「SDK 통합 - 필터 및 효과 구성」을 참고하십시오.
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
>! 
>- 효과 및 세그먼트 모듈을 로딩하는 데 시간이 걸리고 리소스가 소모됩니다. 초기화 중에 필요한 모듈만 활성화할 수 있습니다. 활성화되지 않은 모듈은 로딩되거나 초기화되지 않습니다.
>- config의 camera 매개변수를 지정하면 SDK가 장치의 카메라에서 캡처하는 비디오 데이터가 입력으로 사용됩니다. 또한 몇 가지 기본 기기 관리 API도 제공합니다. 자세한 내용은 [5단계: 장치 제어](#step5)를 참고하십시오.

[](id:step3)
## 3단계: 스트림 재생
SDK는 플레이어에게 웹 페이지에서 빠른 미리 보기를 제공합니다. 다른 콜백에서 얻는 player는 약간 다릅니다. 귀하의 필요에 맞는 것을 선택하십시오.

- 가능한 한 빨리 비디오 이미지를 표시하려면 'cameraReady' 콜백에서 플레이어를 가져오십시오. 이 시점에서 SDK가 리소스를 로딩하지 않았거나 초기화를 완료하지 않았기 때문에 플레이어는 원본 동영상만 재생할 수 있습니다.
```javascript
sdk.on('cameraReady', async () => {
	// SDK의 player를 초기화합니다. my-dom-id는 플레이어 컨테이너의 id입니다.
    const player = await sdk.initLocalPlayer('my-dom-id')
    // 동영상 재생
    await player.play()
})
```
- 초기화 및 효과 적용 후 동영상을 재생하려면 ready 재생 상태에서 플레이어를 가져옵니다.
```javascript
sdk.on('ready', async () => {
    // SDK의 player를 초기화합니다. my-dom-id는 플레이어 컨테이너의 id입니다.
    const player = await sdk.initLocalPlayer('my-dom-id')
    // 동영상 재생
    await player.play()
})
```

>! 
>- initLocalPlayer로 얻은 플레이어는 기본적으로 음소거되어 있습니다. 플레이어의 음소거를 해제하면 에코가 발생할 수 있습니다.
>- 획득한 player는 `sdk.getOutput()` API와 통합됩니다.

initLocalPlayer로 얻은 player 객체는 다음 API와 통합됩니다.

| API          | 설명                       | 요청 매개변수        | 반환값           |
| :-------------- | :------------------------- | :---------- | :--------------- |
| play            | 비디오 재생                       | -           | Promise;         |
| pause           | 비디오 일시 중지(스트림을 중지하지 않으며 재생을 재개할 수 있음) | -           | -                |
| stop            | 비디오 중지( 스트림 중지)       | -           | -                |
| mute            | 재생 음소거                       | -           | -                |
| unmute          | 재생 음소거 해제                   | -           | -                |
| setMirror       | 미러 모드 설정                   | true\|false | -                |
| getVideoElement | 내장 비디오 요소 가져오기        | -           | HTMLVideoElement |
| destroy            | 인스턴스 종료                                                  |

>! 플레이어는 camera [장치 제어](#step5)의 영향을 받습니다. 카메라 설정이 LocalPlayer 설정보다 우선합니다.
>- 예를 들어 `camera.muteVideo`를 호출하여 비디오를 비활성화한 후 localPlayer가 play를 호출해도 재생이 시작되지 않습니다.
>- `camera.unmuteVideo`를 호출하여 비디오를 활성화하면 localPlayer가 자동으로 재생을 재개합니다.
>따라서 camera를 설정하면 localPlayer를 수동으로 제어할 필요가 없으며 camera 장치의 상태를 관리하기만 하면 됩니다.

[](id:step4)
## 4단계: 출력 가져오기
스트림을 게시해야 하는 경우 getOutput을 호출하여 출력 스트림을 가져옵니다.
MediaStream을 가져온 후 라이브 스트리밍 SDK(예: TRTC Web SDK 또는 LEB Web SDK)를 사용하여 스트림을 게시할 수 있습니다.

```javascript
const output = await sdk.getOutput()
```
>!
>- 내장 카메라를 사용하는 경우 getOutput이 반환하는 모든 미디어의 유형은 `MediaStream`입니다.
>- 출력 스트림의 video 트랙은 ArSdk에 의해 실시간으로 처리됩니다. `audio` 트랙(있는 경우)이 유지됩니다.
>- getOutput은 비동기 API입니다. sdk 초기화가 완료되고 스트림을 생성할 수 있는 경우에만 출력이 반환됩니다.
>- FPS 매개변수를 getOutput에 전달하여 출력 프레임 레이트(예시: 15)를 지정할 수 있습니다. 이 매개변수를 전달하지 않으면 원래 프레임 레이트가 유지됩니다.

[](id:step5)
## 5단계: 장치 제어
sdk.camera 인스턴스를 사용하여 카메라를 활성화 및 비활성화하거나 다른 카메라 작업을 수행할 수 있습니다.
```javascript
const output = await sdk.getOutput()
// todo 여기에서 일부 비즈니스 로직 생략
// ...

// sdk.camera는 getOutput 이후에 초기화됩니다. 인스턴스를 직접 가져올 수 있습니다.
const cameraApi = sdk.camera

// 장치 목록 가져오기
const devices = await cameraApi.getDevices()
console.log(devices)
// 비디오 트랙 비활성화
// cameraApi.muteVideo()
// 비디오 트랙 활성화
// cameraApi.unmuteVideo()
// 장치 id를 지정하여 다른 카메라로 변경(여러 카메라가 있는 경우)
// await cameraApi.switchDevices('video', 'your-device-id')
```
가능한 한 빨리 `sdk.camera` 인스턴스를 얻으려면 cameraReady 콜백에서 가져올 수 있습니다.
```javascript
// todo 여기에서 일부 초기화 매개변수를 생략합니다.
// ...
const sdk = new ArSdk(
    config
)

let cameraApi;
sdk.on('cameraReady', async () => {
    cameraApi = sdk.camera
    // 장치 목록 가져오기
    const devices = await cameraApi.getDevices()
    console.log(devices)
    // 비디오 트랙 비활성화
    // cameraApi.muteVideo()
    // 비디오 트랙 활성화
    // cameraApi.unmuteVideo()
    // 장치 id를 지정하여 다른 카메라로 변경(여러 카메라가 있는 경우)
    // await cameraApi.switchDevices('video', 'your-device-id')
})
```
내장된 `camera`는 카메라를 제어할 수 있도록 다음 API를 제공합니다.
<table>
<thead><tr><th>API</th><th>설명</th><th>요청 매개변수</th><th>반환 값</th></tr></thead>
<tbody>
<tr>
<td>getDevices</td>
<td>모든 장치 가져오기</td>
<td>-</td>
<td>Promise&lt;Array&lt;MediaDeviceInfo&gt;&gt;</td>
</tr><tr>
<td>switchDevice</td>
<td>다른 기기로 변경</td>
<td><code>type:string, deviceId:string</code></td>
<td>Promise
</td>
</tr>
<tr>
<td>muteAudio</td>
<td>카메라 스트림 음소거</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>unmuteAudio</td>
<td>카메라 스트림의 음소거 해제</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>muteVideo</td>
<td>카메라 스트림의 비디오를 비활성화합니다. 비디오 트랙만 비활성화되며 스트림은 중지되지 않습니다.</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>unmuteVideo</td>
<td>카메라 스트림의 비디오 활성화</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>stopVideo</td>
<td>카메라를 비활성화합니다. 이렇게 하면 비디오 스트림이 중지되지만 오디오 스트림은 영향을 받지 않습니다.</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>restartVideo</td>
<td>카메라를 활성화합니다. 이 API는 stopVideo 이후에만 호출할 수 있습니다.</td>
<td>-</td>
<td>Promise</td>
</tr>
<tr>
<td>stop</td>
<td>카메라와 오디오 장치 비활성화</td>
<td>-</td>
<td>-</td>
</tr>
</tbody></table>



