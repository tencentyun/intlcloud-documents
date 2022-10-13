## 초기화 매개변수
SDK의 Config는 다음 초기화 매개변수를 지원합니다.
<table>
<thead><tr><th>매개변수</th><th>설명</th><th width=200px>유형</th><th>필수 여부</th></tr></thead>
<tbody>
<tr>
<td>module</td>
<td>모듈 구성</td>
<td><pre style="color:white">
type ModuleConfig = {
  beautify: boolean // 기본값: true
  segmentation: boolean // 기본값: false
}
</pre></td>
<td>No, 기본값: <code>{beautify: true, segmentation: false}</code></td></tr>
<tr>
<td>auth</td>
<td>인증 매개변수</td>
<td><pre style="color:white;margin:0;">
type AuthConfig = {
  licenseKey: string // 콘솔의 <a href="https://console.cloud.tencent.com/vcube/web"><strong> Web License 관리</strong></a> 에서 가져오기
  appId: string // 콘솔의 <a href="https://console.cloud.tencent.com/developer"><strong>계정 정보</strong></a> &gt; <strong>기본 정보</strong>에서 APPID 보기
  authFunc:() => Promise<{
    signature:string,
    timestamp:string
  }> // License 구성 및 사용  참고
}
</pre></td>
<td>Yes</td></tr><tr>
<td>input</td>
<td>입력</td>
<td>MediaStream|HTMLImageElement|String</td>
<td>No</td></tr>
<tr>
<td>camera</td>
<td>내장 카메라 구성</td>
<td><pre style="color:white;margin:0">
type CameraConfig = {
	width: number, // 비디오 너비
	height: number, // 비디오 높이
	mirror: boolean, // 비디오 수평 뒤집기 여부
    frameRate: number // 캡처 프레임 레이트
}
</pre></td>
<td>No</td></tr><tr>
<td>beautify</td>
<td>뷰티 필터 효과</td>
<td><pre style="color:white;margin:0">
type BeautifyOptions = {
	whiten?: number, // 브라이트닝 효과. 값 범위: 0-1
	dermabrasion?: number // 매끄러운 피부 효과. 값 범위: 0-1
	lift?: number // 갸름한 얼굴 효과. 값 범위: 0-1
	shave?: number // 얼굴 너비. 값 범위: 0-1
	eye?: number // 큰 눈 효과. 값 범위: 0-1
	chin?: number // 턱 효과. 값 범위: 0-1
}
</pre></td>
<td>No</td></tr>
<tr>
<td>background</td>
<td>배경 매개변수</td>
<td><pre style="color:white">
type BackgroundOptions = {
	type: 'image' | 'blur' | 'transparent', 
	src?: string
}
</pre></td>
<td>No</td>
</tr>
<tr>
<td>loading</td>
<td>내장 loading icon 구성</td>
<td><pre style="color:white;margin:0">
type loadingConfig = {
	enable: boolean,
	size?: number
	lineWidth?: number
	strokeColor?: number
}
</pre></td>
<td>No</td>
</tr>
</tbody>
</table>

## 콜백 이벤트
```javascript
let effectList = [];
let filterList = [];
// sdk의 콜백 사용
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
sdk.on('cameraReady', async () => {
	// cameraReady 콜백에서 출력 스트림을 가져오면 비디오 이미지를 더 빨리 표시할 수 있지만 초기화 매개변수는 이 시점에서 적용되지 않습니다.
	// 비디오 이미지를 가능한 한 빨리 표시하지만 비디오가 표시되는 순간에 효과를 적용할 필요가 없는 경우 이 방법을 선택할 수 있습니다.
	// 뷰티 필터 적용 후 stream을 업데이트할 필요가 없습니다.
	const arStream = await ar.getOutput();
	// 로컬 재생
	// localVideo.srcObject = arStream

})
sdk.on('ready', () => {
	// ready 콜백에서 출력 스트림을 가져옵니다. 이제 초기화 매개변수가 적용되었습니다.
	// 비디오가 표시되는 순간 효과를 보여주길 원하지만 가능한 한 빨리 표시되기를 기대하지 않는 경우 output 스트림을 cameraReady로 가져올 수 있습니다.
	// 두 가지 방법 중에서 필요에 맞는 방법을 선택합니다.
	const arStream = await ar.getOutput();
	// 로컬 재생
	// localVideo.srcObject = arStream

	// ready 콜백에서 setBeautify/setEffect/setFilter 호출
	sdk.setBeautify({
		whiten: 0.3
	});
	sdk.setEffect({
		id: effectList[0].EffectId,
		intensity: 0.7
	});
	sdk.setEffect({
		id: effectList[0].EffectId,
		intensity: 0.7,
		filterIntensity: 0.5 // v0.1.18 이상에서는 이 매개변수를 사용하여 특수 effect의 필터 강도를 설정할 수 있습니다. 이 매개변수를 전달하지 않으면 효과에 대해 지정된 intensity가 사용됩니다.
	});
	sdk.setFilter(filterList[0].EffectId, 0.5)
})

```

| 콜백  | 설명                            | 반환 값  |
| ----- |-------------------------------| --------- |
| created | SDK 인증이 완료되고 인스턴스가 생성되었습니다.            | -         |
| cameraReady | SDK의 비디오 output을 생성했습니다(뷰티 필터는 아직 적용되지 않음). | -         |
| ready | 감지가 초기화되었습니다. 이제 효과가 output 비디오에 적용됩니다. 효과 설정을 변경할 수 있습니다.           | -         |
| error | SDK 오류 발생 시 트리거                   | error 객체 |


## 객체 메소드
<table>
<thead><tr><th>API</th><th width=200px>요청 매개변수</th><th>응답 매개변수</th>
<th>　　　　설명　　　　</th></tr></thead>
<tbody><tr>
<td>async getOutput(fps)</td>
<td>- fps(선택 사항): 출력 프레임 레이트</td>
<td>MediaStream|String</td>
<td>이 API는 Web SDK에서만 사용할 수 있습니다.</td>
</tr>
<tr>
<td>setBeautify(options)</td>
<td>options: 뷰티 필터 매개변수 객체
<pre style="color: white;margin: 0px;overflow: scroll;display: block;width: 300px;">
type BeautifyOptions = {
  whiten?: number, // 브라이트닝 효과. 값 범위: 0-1
  dermabrasion?: number // 매끄러운 피부 효과. 값 범위: 0-1
  lift?: number // 갸름한 얼굴 효과. 값 범위: 0-1
  shave?: number // 얼굴 너비. 값 범위: 0-1
  eye?: number // 큰 눈 효과. 값 범위: 0-1
  chin?: number // 턱 효과. 값 범위: 0-1
}</pre>
</td>
<td>-</td>
<td>뷰티 필터를 구성하려면 뷰티 필터 모듈을 활성화해야 합니다.</td>
</tr>
<tr>
<td>setEffect(effects, callback)</td>
<td><ul style="margin:0">
   <li>effects: 효과 ID | effect 객체 | 효과 ID / effect 배열
	<pre style="color: white;margin: 0px;overflow: scroll;display: block;width: 300px;">
effect:{
	id: string,
	intensity: number, // 효과 강도, 기본값: 1, 값 범위: 0-1
	filterIntensity: number // 효과의 필터 강도(v0.1.18 이상에서 지원됨). 값 범위: 0-1. 기본적으로 이 매개변수는 intensity와 동일
}</pre>
	<li>callback: 설정 성공 콜백</ul></td>
<td>-</td>
<td>특수 효과를 구성하려면 뷰티 필터 모듈을 활성화해야 합니다.</td>
</tr>
<tr>
<td>setBackground(options)</td>
<td><pre style="color:white;margin:0">
{
	type: 'image|blur|transparent',
	src: string // 이 매개변수는 유형이 image인 경우에만 필요합니다.
}</pre>
</td>
<td>-</td>
<td>배경을 구성하려면 키잉 모듈을 활성화해야 합니다.</td>
</tr>
<tr>
<td>setFilter(id, intensity, callback)</td>
<td>
   <li>id: 필터 ID
   <li>intensity: 필터 강도, 값 범위: 0-1
   <li>callback: 설정 성공 콜백</td>
<td>-</td>
<td>이 API는 필터를 설정하는 데 사용됩니다.</td>
</tr>
<tr>
<td>getEffectList(params)</td>
<td><pre style="color:white;margin:0">
{
	PageNumber: number,
	PageSize: number,
	Name: '',
	Label: Array,
	Type: 'Custom|Preset'
}</pre>
</td>
<td>효과 목록</td>
<td>이 API는 효과의 목록 풀링에 사용됩니다.</td>
</tr>
<tr>
<td>getEffect(effectId)</td>
<td>effectId: 효과 ID</td>
<td>단일 특수 효과 정보</td>
<td>이 API는 특정 효과의 정보 풀링에 사용됩니다.</td>
</tr>
<tr>
<td>getCommonFilter()</td>
<td>-</td>
<td>내장 필터 목록</td>
<td>이 API는 내장 필터를 가져오는 데 사용됩니다.</td>
</tr>
<tr>
<td>async updateInputStream(src:MediaStream) <br><b>(v0.1.19부터 지원)</b></td>
<td>src: 새로운 입력 스트림(MediaStream)</td>
<td>-</td>
<td>이 API는 입력 스트림을 업데이트하는 데 사용됩니다.</td>
</tr>
<tr>
<td>disable()</td>
<td>-</td>
<td></td>
<td>이 API는 얼굴 감지를 비활성화하는 데 사용됩니다. 비활성화되면 원시 스트림이 반환됩니다. CPU 사용량을 줄일 수 있습니다.</td>
</tr>
<tr>
<td>enable()</td>
<td>-</td>
<td></td>
<td>이 API는 얼굴 감지를 활성화하는 데 사용됩니다. 활성화되면 반환된 스트림이 처리됩니다.</td>
</tr>
<tr>
<td>destroy()</td>
<td>-</td>
<td>-
</td>
<td>이 API는 sdk 인스턴스를 종료하고 텍스처 리소스를 지우는 데 사용됩니다.</td>
</tr>
</tbody></table>


## 오류 처리
error 콜백에 의해 반환된 오류 객체에는 문제 해결을 용이하게 하는 오류 코드와 오류 메시지가 포함됩니다.
```javascript
sdk.on('error', (error) => {
	// error 콜백에서 오류 처리
	const {code, message} = error
	...
})
```

| 에러 코드  | 설명                | 비고  |
| ----- | ------------------- | --------- |
| 10000001 | 지원되지 않는 브라우저 | Chrome, Firefox, Safari 사용 권장      |
| 10000002 | 렌더링 컨텍스트 누락 | - |
| 10000003 | 렌더링 시간 오래 걸림 | 해상도를 낮추거나 일부 기능을 비활성화하는 것을 고려하십시오 |
| 10000005 | 입력 구문 분석 오류 | -       |
| 10001101 | 특수 효과를 구성하는 동안 오류 발생 | -         |
| 10001102 | 필터를 구성하는 동안 오류 발생   | - |
| 10001103 | 유효하지 않은 효과 강도   | - |
| 10001201 | 카메라 시작 실패   | - |
| 10001202 | 카메라 중단   | - |
| 20002001 | 인증 매개변수 누락 | - |
| 20001001 | 인증 실패   | License를 생성했고 서명이 올바른지 확인하십시오 |
| 20001002 | API 요청 실패 | 오류 콜백은 API에서 반환한 데이터를 반환합니다. 자세한 내용은 [API Error Codes](https://intl.cloud.tencent.com/document/product/1143/50107)를 참고하십시오. |

### 누락된 렌더링 컨텍스트 오류 처리
일부 PC에서는 SDK가 오랫동안 백그라운드에 있으면 contextlost 오류가 발생할 수 있습니다. 이러한 경우 `ArSdk.prototype.resetCore(input: MediaStream)`를 호출하여 렌더링을 재개할 수 있습니다.
```JavaScript
sdk.on('error', async (error) => {
	if (error.code === 10000002) {
		const newInput = await navigator.mediaDevices.getUserMedia({...})
		await sdk.resetCore(newInput)
	}
})
```
