## 初期化パラメータ
SDKを初期化するConfigは次のパラメータをサポートしています。
<table>
<thead><tr><th>パラメータ</th><th>説明</th><th width=200px>タイプ</th><th>渡す必要があるかどうか</th></tr></thead>
<tbody>
<tr>
<td>module</td>
<td>モジュール設定</td>
<td><pre style="color:white">
type ModuleConfig = {
  beautify: boolean // デフォルトはtrueです
  segmentation: boolean // デフォルトはfalseです
}
</pre></td>
<td>いいえ、デフォルトは <code>{beautify: true, segmentation: false}</code>です</td></tr>
<tr>
<td>auth</td>
<td>認証パラメータ</td>
<td><pre style="color:white;margin:0;">
type AuthConfig = {
  licenseKey: string // コンソール <a href="https://console.cloud.tencent.com/vcube/web"><strong> Web License管理</strong></a>取得
  appId: string // コンソール <a href="https://console.cloud.tencent.com/developer"><strong>アカウント情報</strong></a> &gt; <strong>基本情報</strong>APPID確認
  authFunc:() => Promise<{
    signature:string,
    timestamp:string
  }> // License設定の使用 をご参照ください。
}
</pre></td>
<td>はい</td></tr><tr>
<td>input</td>
<td>入力ソース</td>
<td>MediaStream|HTMLImageElement|String</td>
<td>いいえ</td></tr>
<tr>
<td>camera</td>
<td>内蔵カメラ</td>
<td><pre style="color:white;margin:0">
type CameraConfig = {
	width: number, // 撮影画面の幅
	height: number, // 撮影画面の高さ
	mirror: boolean, // 左右ミラーオン/オフ
    frameRate: number // 画面収集フレームレート
}
</pre></td>
<td>いいえ</td></tr><tr>
<td>beautify</td>
<td>美顔パラメータ</td>
<td><pre style="color:white;margin:0">
type BeautifyOptions = {
	whiten?: number, // 美白 0-1
	dermabrasion?: number // 美肌0-1
	lift?: number // 小顔0-1
	shave?: number // 顎を細くする0-1
	eye?: number // デカ目0-1
	chin?: number // 下あご0-1
}
</pre></td>
<td>いいえ</td></tr>
<tr>
<td>background</td>
<td>背景パラメータ</td>
<td><pre style="color:white">
type BackgroundOptions = {
	type: 'image' | 'blur' | 'transparent', 
	src?: string
}
</pre></td>
<td>いいえ</td>
</tr>
<tr>
<td>loading</td>
<td>内蔵loading iconの設定</td>
<td><pre style="color:white;margin:0">
type loadingConfig = {
	enable: boolean,
	size?: number
	lineWidth?: number
	strokeColor?: number
}
</pre></td>
<td>いいえ</td>
</tr>
</tbody>
</table>

## コールバックイベント
```javascript
let effectList = [];
let filterList = [];
// sdkのコールバック使用法
sdk.on('created', () => {
	// ページ表示のためにcreatedコールバックでエフェクトおよびフィルターリストをプルします
	sdk.getEffectList({
        Type: 'Preset',
        Label: 'メイクアップ',
	}).then(res => {
		effectList = res
	});
	sdk.getCommonFilter().then(res => {
		filterList = res
	})
})
sdk.on('cameraReady', async () => {
	// camerareadyコールバック内でより早く出力画面を取得することができます。この時初期化で渡された美顔パラメータはまだ有効ではありません
	// できるだけ早く画面を表示する必要がありますが、画面が表示されたらすぐに美顔を要求されるわけではないシーンに適用されます
	// その後美顔が有効になった後streamを更新する必要はなく、SDK内部で処理されます
	const arStream = await ar.getOutput();
	// ローカル再生
	// localVideo.srcObject = arStream

})
sdk.on('ready', () => {
	// readyコールバック内で出力画面を取得します。この時初期化で渡された美顔パラメータは有効です
	// 上記のcameraReadyでoutputを取得することとは異なり、画面を表示するとすぐに美顔がありますが、できるだけ早く画面を表示する必要はありません
	// 自身の業務ニーズに応じて処理方式を選択することができます
	const arStream = await ar.getOutput();
	// ローカル再生
	// localVideo.srcObject = arStream

	// readyコールバックでsetBeautify/setEffect/setFilterなどのレンダリング方法を呼び出すことができます
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
		filterIntensity: 0.5 // 0.1.18およびそれ以降のバージョンはeffect内のフィルターの強度を単独で設定することをサポートしています。渡されない場合、デフォルトではエフェクトのintensityに一致します
	});
	sdk.setFilter(filterList[0].EffectId, 0.5)
})

```

| イベント  | 説明                            | コールバックパラメータ  |
| ----- |-------------------------------| --------- |
| created | SDK 認証を完了してインスタンスの作成に成功したときにトリガーされます            | -         |
| cameraReady | SDKの画面生成時にトリガーされます。この場合は、outputに画面がありますが美顔は有効にすることができません | -         |
| ready | SDK 内部で初期化の完了を検出した時にトリガーされます。この場合は、output画面に美顔があり、新たなエフェクトを設定することもできます           | -         |
| error | SDKにエラーが発生した時にトリガーされます                   | errorオブジェクト |


## オブジェクトメソッド
<table>
<thead><tr><th>インターフェース</th><th width=200px>パラメータ</th><th>戻る</th>
<th>　　　　説明　　　　</th></tr></thead>
<tbody><tr>
<td>async getOutput(fps)</td>
<td>- fps：出力するメディアストリームのフレームレートを設定します。デフォルトでは設定する必要はありません</td>
<td>MediaStream|String</td>
<td>Web端末でのみ提供</td>
</tr>
<tr>
<td>setBeautify(options)</td>
<td>options：美顔パラメータオブジェクト
<pre style="color: white;margin: 0px;overflow: scroll;display: block;width: 300px;">
type BeautifyOptions = {
  whiten?: number, // 美白 0-1
  dermabrasion?: number // 美肌0-1
  lift?: number // 小顔0-1
  shave?: number // 顎を細くする0-1
  eye?: number // デカ目0-1
  chin?: number // 下あご0-1
}</pre>
</td>
<td>-</td>
<td>美顔パラメータを設定するには、美顔モジュールを起動する必要があります</td>
</tr>
<tr>
<td>setEffect(effects, callback)</td>
<td><ul style="margin:0">
   <li>effects：エフェクト ID | effectオブジェクト | エフェクト ID / effect配列
	<pre style="color: white;margin: 0px;overflow: scroll;display: block;width: 300px;">
effect:{
	id: string,
	intensity: number, // エフェクト強度、デフォルトは1、範囲は0-1です
	filterIntensity: number // エフェクト内のフィルター強度を単独で制御します。デフォルトはintensityで、範囲は0-1です (0.1.18およびそれ以降のバージョンでサポートしています)
}</pre>
	<li>callback：成功したコールバックを設定します</ul></td>
<td>-</td>
<td>エフェクトを設定するには、美顔モジュールを起動する必要があります</td>
</tr>
<tr>
<td>setBackground(options)</td>
<td><pre style="color:white;margin:0">
{
	type: 'image|blur|transparent',
	src: string // imageタイプのみ必要
}</pre>
</td>
<td>-</td>
<td>背景を設定するには人物画像分割モジュールを起動する必要があります</td>
</tr>
<tr>
<td>setFilter(id, intensity, callback)</td>
<td>
   <li>id：フィルターID
   <li>intensity：フィルター強度、範囲は0-1です
   <li>callback：成功したコールバックの設定</td>
<td>-</td>
<td>フィルターの設定</td>
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
<td>エフェクトリスト</td>
<td>エフェクトリストのプル</td>
</tr>
<tr>
<td>getEffect(effectId)</td>
<td>effectId：エフェクト ID</td>
<td>単一のエフェクト情報</td>
<td>エフェクトを指定する情報をプルします</td>
</tr>
<tr>
<td>getCommonFilter()</td>
<td>-</td>
<td>内蔵フィルターリスト</td>
<td>内蔵フィルターリストを取得します</td>
</tr>
<tr>
<td>async updateInputStream(src:MediaStream) <br><b>（0.1.19バージョン以降にサポート）</b></td>
<td>src：新しい入力ストリームMediaStream</td>
<td>-</td>
<td>入力ストリームを更新します</td>
</tr>
<tr>
<td>disable()</td>
<td>-</td>
<td></td>
<td>顔検出を無効化して、未処理のオリジナル画面に戻ると、CPU使用率を低下させることができます</td>
</tr>
<tr>
<td>enable()</td>
<td>-</td>
<td></td>
<td>顔検出を復元して、美顔などのエフェクトが有効な画面に戻ります</td>
</tr>
<tr>
<td>destroy()</td>
<td>-</td>
<td>-
</td>
<td>現在のsdkインスタンスおよび関連するテクスチャリソースを破棄します</td>
</tr>
</tbody></table>


## エラー処理
error コールバックで返されるオブジェクトにはエラーコードとエラー情報が含まれ、エラー処理をしやすくします。
```javascript
sdk.on('error', (error) => {
	// error コールバックでエラーを処理します
	const {code, message} = error
	...
})
```

| エラーコード  | 意味                | 備考  |
| ----- | ------------------- | --------- |
| 10000001 | 現在のブラウザ環境は互換性がありません | Chrome、Firefox、Safariの使用をユーザーにお勧めします     |
| 10000002 | 現在のレンダリングコンテキストは失われます | - |
| 10000003 | レンダリングには時間がかかります | ビデオの解像度を下げるか機能をブロックすることを検討してください |
| 10000005 | 入力ソースの解析エラー | -       |
| 10001101 | エフェクトエラーの設定 | -         |
| 10001102 | フィルターエラーの設定   | - |
| 10001103 | エフェクト強度のパラメータが不正確です   | - |
| 10001201 | ユーザーカメラの起動に失敗しました   | - |
| 10001202 | カメラ中断   | - |
| 20002001 | 認証パラメータがありません | - |
| 20001001 | 認証失敗   | Licenseが作成されているかどうか、署名が正確かどうかを確認してください |
| 20001002 | インターフェースリクエストに失敗しました | コールバックはインターフェースがから返されたデータを転送します。具体的な情報については[インターフェースエラーコード](https://intl.cloud.tencent.com/document/product/1143/50107) をご参照ください|

### 現在のレンダリングコンテキストを処理すると失われます
一部のPCは長時間バックエンドをカットされるシナリオでcontextlost処理エラーがトリガーされる可能性があります。`ArSdk.prototype.resetCore(input: MediaStream)`を呼び出してレンダリングコンテキストを復元することができます。
```JavaScript
sdk.on('error', async (error) => {
	if (error.code === 10000002) {
		const newInput = await navigator.mediaDevices.getUserMedia({...})
		await sdk.resetCore(newInput)
	}
})
```
