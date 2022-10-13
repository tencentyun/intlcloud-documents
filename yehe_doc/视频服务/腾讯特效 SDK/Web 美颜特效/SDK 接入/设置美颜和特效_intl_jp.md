SDKは**美顔**、**フィルター**、**エフェクト**などの効果を提供しており、いずれもWeb端末をサポートしています。フィルターおよびエフェクトはまず素材リストを取得し、さらに素材のEffectIdによってSDKで設定する必要があります。

## 美顔
初期化時に美顔パラメータを渡すことができるだけでなく、ArSdkの`setBeautify`メソッドで美顔を設定することもできます。
- SDKが現在サポートしている美顔効果は次のとおりです。
```typescript
type BeautifyOptions = {
	whiten?: number, // 美白 0-1
	dermabrasion?: number // 美肌0-1
	lift?: number // 小顔0-1
	shave?: number // 顎を細くする0-1
	eye?: number // デカ目0-1
	chin?: number // 下あご0-1
}
```
- SDKインスタンスの`setBeautify`メソッドを呼び出して美顔パラメータを設定します。
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

## フィルター
フィルター画像の制作は高コストとなるため、直接使用できる内蔵フィルターを提供しています。
1. 内蔵フィルターリストを取得します。
```javascript
const filterList = await sdk.getCommonFilter()
```
2. フィルターを設定します。
```javascript
sdk.setFilter(filterList[0].EffectId, 0.5)
```


## エフェクト
SDKで[コンソール](https://console.cloud.tencent.com/vcube/creator) で制作したエフェクトを直接設定することも、提供されている内蔵効果を使用することもできます。


```javascript
// 内蔵エフェクトの取得
// デフォルトでは内蔵メイクアップおよびステッカー素材が返され、Labelパラメータによって特定のタイプの素材を指定して返すことができます
const presetEffectList = await sdk.getEffectList({
	Type: 'Preset'
	// Label: ['ステッカー'] 内蔵ステッカーのみを返します
})

// 自作エフェクトを取得します
const customEffectList = await sdk.getEffectList({
	Type: 'Custom'
})

// リストのリクエストパラメータを渡します
const lipList = await sdk.getEffectList({
	PageNumber: 0,
	PageSize: 10,
	Name: '',
	Label: ['リップメイク'], // 用エフェクトのタグフィルタリング
	Type: 'Custom'
})
const eyeList = await sdk.getEffectList({
	PageNumber: 0,
	PageSize: 10,
	Name: '',
	Label: ['アイメイク'], // 用エフェクトのタグフィルタリング
	Type: 'Custom'
})
// エフェクトの設定
sdk.setEffect([lipList[0].EffectId, eyeList[0].EffectId])

// エフェクト+強度の設定
sdk.setEffect([
{
	id: lipList[0].EffectId,
	intensity: 0.5
}, 
{
	id: eyeList[0].EffectId,
	intensity: 0.7
})
// エフェクト内のフィルター強度の単独設定
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


>! エフェクト制作ツールは、エフェクト内へのフィルターの追加をサポートしているため、複数のエフェクトを重ね合わせた場合、フィルターはデフォルトではオーバーレイ処理がなされます。単独で制御する必要がある場合は、filterIntensityを使用して単独制御することができます。

## 美顔を終了します
AI検出のパフォーマンス消費は大きいため、可能な限りリソースを節約します。SDKに美顔とエフェクト効果の設定がない場合は、自動的にAI検出を終了し、再び効果を設定すると自動的に起動します。
```javascript
// SDKで設定したすべての効果をクリアして検出をオフにします
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
