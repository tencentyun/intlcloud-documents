Tencent Effect SDK는 **뷰티 효과**, **필터**, **특수 효과**를 제공합니다. Web SDK에서도 모두 지원됩니다. 필터 및 특수 효과의 경우 먼저 리소스 목록을 가져와 EffectId를 지정하여 SDK에서 구성해야 합니다.

## 뷰티 효과
초기화하는 동안 뷰티 효과 매개변수를 전달할 수 있습니다. ArSdk의 `setBeautify`를 호출하여 미화 효과를 설정할 수도 있습니다.
- 현재 SDK는 다음과 같은 뷰티 효과를 지원합니다.
```typescript
type BeautifyOptions = {
	whiten?: number, // 브라이트닝 효과. 값 범위: 0-1
	dermabrasion?: number // 매끄러운 피부 효과. 값 범위: 0-1
	lift?: number // 갸름한 얼굴 효과. 값 범위: 0-1
	shave?: number // 얼굴 너비. 값 범위: 0-1
	eye?: number // 큰 눈 효과. 값 범위: 0-1
	chin?: number // 턱 효과. 값 범위: 0-1
}
```
- 뷰티 효과를 설정하려면 SDK의 'setBeautify'를 호출합니다.
```javascript
sdk.setBeautify({
	whiten: 0.2,
	dermabrasion: 0,
	lift: 0.3,
	shave:0.1,
	eye: 0.9,
	chin: 0
})
```

## 필터
필터 생성 비용이 상대적으로 높기 때문에 직접 사용할 수 있는 몇 가지 내장 필터를 제공합니다.
1. 내장 필터 목록을 가져옵니다.
```javascript
const filterList = await sdk.getCommonFilter()
```
2. 필터 구성
```javascript
sdk.setFilter(filterList[0].EffectId, 0.5)
```


## 특수 효과
SDK에 내장된 효과를 사용하거나 [콘솔](https://console.cloud.tencent.com/vcube/creator)에서 제작한 효과를 사용할 수 있습니다.


```javascript
// 내장 효과 가져오기
// 기본적으로 내장된 메이크업 효과와 스티커가 반환됩니다. Label 매개변수를 사용하여 반환할 리소스 유형을 지정할 수 있습니다.
const presetEffectList = await sdk.getEffectList({
	Type: 'Preset'
	// Label: [‘스티커’] (스티커만 반환)
})

// 사용자 정의 효과 가져오기
const customEffectList = await sdk.getEffectList({
	Type: 'Custom'
})

// `getEffectList`의 요청 매개변수를 전달합니다.
const lipList = await sdk.getEffectList({
	PageNumber: 0,
	PageSize: 10,
	Name: '',
	Label: [‘립 메이크업’], // 반환할 리소스 유형 지정
	Type: 'Custom'
})
const eyeList = await sdk.getEffectList({
	PageNumber: 0,
	PageSize: 10,
	Name: '',
	Label: ['눈 화장'], // 반환할 리소스 유형 지정
	Type: 'Custom'
})
// 특수 효과 구성
sdk.setEffect([lipList[0].EffectId, eyeList[0].EffectId])

// 사용할 효과+강도 지정
sdk.setEffect([
{
	id: lipList[0].EffectId,
	intensity: 0.5
}, 
{
	id: eyeList[0].EffectId,
	intensity: 0.7
})
// 필터 강도만 설정
sdk.setEffect([
{
	id: lipList[0].EffectId,
	intensity: 0.5,
	filterIntensity: 0
}, 
{
	id: eyeList[0].EffectId,
	intensity: 0.7,
	filterIntensity: 1
})
```


>! 특수 효과를 사용자 정의할 때 효과에 필터를 추가할 수 있습니다. 이러한 경우 filterIntensity를 사용하여 필터의 강도를 조정할 수 있습니다.

## 뷰티 효과 비활성화
AI 탐지의 성능 오버헤드가 높기 때문에 리소스를 절약하기 위해 SDK는 뷰티 효과 또는 특수 효과가 사용되지 않을 때 AI 감지를 자동으로 비활성화하고 효과가 적용될 때 AI 감지를 다시 활성화합니다.
```javascript
// 모든 SDK 설정을 지워야 AI 감지를 비활성화할 수 있습니다.
sdk.setBeautify({
	whiten: 0,
	dermabrasion: 0,
	lift: 0,
	shave:0,
	eye: 0,
	chin: 0
})
sdk.setEffect('')
```
