VODは、オーディオとビデオをブラウザからアップロードするシナリオ向けに、Webアップロード用SDKを提供しています。SDKソースコードが必要な場合は、[SDKソースコード](https://github.com/tencentyun/vod-js-sdk-v6) にアクセスしてください。

## シンプルアップロード

### SDKのインポート

#### scriptのインポート方法
webpackを使用しない場合は、scriptタグを介してインポートすることができます。この方法では、グローバル変数`TcVod`が公開されます。scriptをインポートするには、次の2つの方法があります。
- **ローカルへのダウンロード**
	[SDKソースコード](https://github.com/tencentyun/vod-js-sdk-v6)をローカルにダウンロードし、次のようにインポートします。
```html
<script src="./vod-js-sdk-v6.js"></script>
```
>?インポートパスをローカルに保存されたパスに調整してください。
- **CDNリソースの使用**
	CDNリソースを使用すると、次の方法で直接インポートできます。
```html
<script src="https://cdn-go.cn/cdn/vod-js-sdk-v6/latest/vod-js-sdk-v6.js"></script>
```

[ここをクリック](https://tencentyun.github.io/vod-js-sdk-v6/)して、scriptによってインポートされたDemoをご確認ください。[ここをクリック](https://github.com/tencentyun/vod-js-sdk-v6/blob/master/docs/index.html)して、Demoソースコードをご確認ください。

#### npmのインポート方法
webpackを使用する場合（VueやReactなど）は、npmを介してインポートできます。
```js
// npm install vod-js-sdk-v6を実行した後に、importを実行してページに直接インポートします。
import TcVod from 'vod-js-sdk-v6'
```

[ここをクリック](https://github.com/tencentyun/vod-js-sdk-v6/tree/master/docs/import-demo) して、npmによってインポートされたDemoソースコードをご確認ください。

>!SDKはPromiseに依存しています。低いバージョンのブラウザでご自身によりインポートしてください。


###  アップロード署名を取得するための関数の定義

```js
function getSignature() {
  return axios.post(url).then(function (response) {
    return response.data.signature;
  })
};
```

>? `url`は、署名配布サービスのURLです。詳細については、[クライアントからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33921) をご参照ください。
> `signature`の計算ルールについては、[クライアントからのアップロード署名 ](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。

###  ビデオアップロードの例



```js
// importによってインポートした場合、new TcVod(opts) を実行します
// new TcVod.default(opts) は、scriptによってインポートされます 
const tcVod = new TcVod.default({
  getSignature: getSignature // 前文で説明したアップロード署名を取得する関数です
})

const uploader = tcVod.upload({
  mediaFile: mediaFile, // Fileタイプのメディアファイル（ビデオ、オーディオまたは画像）
})
uploader.on('media_progress', function(info) {
  console.log(info.percent) // 進行状況
})

// コールバック結果の説明
// type doneResult = {
//   fileId: string,
//   video: {
//     url: string
//   },
//   cover: {
//     url: string
//   }
// }
uploader.done().then(function (doneResult) {
  // deal with doneResult
}).catch(function (err) {
  // deal with error
})


```

>?
>- `new TcVod(opts)`のoptsは、インターフェースに関連するパラメータを参照します。 詳細については、[TcVodインターフェースの説明](#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) をご参照ください。
>- アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。
>- 指定されたサブアプリケーションにアップロードする必要がある場合は、[サブアプリケーションシステム-クライアントからのアップロード](https://intl.cloud.tencent.com/document/product/266/33987)をご参照ください。

## 高度な機能

### ビデオとカバーの同時アップロード

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.done().then(function (doneResult) {
  // deal with doneResult
})
```

### アップロードの進行状況の取得

SDKは、現在のアップロード進行状況をコールバック形式で表示します。

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})
// ビデオのアップロードが完了したとき
uploader.on('media_upload', function(info) {
  uploaderInfo.isVideoUploadSuccess = true;
})
// ビデオのアップロード進行状況
uploader.on('media_progress', function(info) {
  uploaderInfo.progress = info.percent;
})
// カバーをアップロードしたとき
uploader.on('cover_upload', function(info) {
  uploaderInfo.isCoverUploadSuccess = true;
})
// カバーのアップロード進行状況
uploader.on('cover_progress', function(info) {
  uploaderInfo.coverProgress = info.percent;
})

uploader.done().then(function (doneResult) {
  // deal with doneResult
})
```

`xxx_upload`と`xxx_progress`のコールバック値については、[マルチパートアップロード/タスクのコピー操作](https://intl.cloud.tencent.com/document/product/436/31538) をご参照ください。

### アップロードのキャンセル

SDKは、進行中のビデオまたはカバーのアップロードのキャンセルをサポートしています。

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.cancel()
```

### 中断からの再開

SDKでは、自動的にアップロードを再開できます。追加の操作は必要ありません。アップロードが予期せず終了した場合（ブラウザが閉じた、ネットワークが中断したなど）、中断したポイントから再度アップロードを続行できるため、アップロードを繰り返す時間が短縮されます。

## インターフェースの説明

### TcVod

| パラメータ名         | 入力必須   | タイプ       | パラメータの説明      |
| ------------ | ---- | -------- | --------- |
| getSignature    | はい     | Function     | アップロード署名を取得するための関数。  |
| appId    | いいえ    | number     | 入力後、組み込みの統計レポートに自動的に反映されます。  |
| reportId     | いいえ    | number     | 入力後、組み込みの統計レポートに自動的に反映されます。  |

### TcVod.upload

| パラメータ名         | 入力必須   | タイプ       | パラメータの説明      |
| ------------ | ---- | -------- | --------- |
| mediaFile    | いいえ    | File     | メディアファイル（ビデオ、オーディオまたは画像）。  |
| coverFile    | いいえ    | File     | カバーファイル。  |
| mediaName    | いいえ    | string     | メディアファイルのメタデータを上書きするファイル名。  |
| fileId    | いいえ    | string     | カバーを変更するときに渡されます。  |
| reportId    | いいえ    | number     | 入力後、組み込みの統計レポートに自動的に反映されます。コンストラクタの設定を上書きします。  |

### イベント

| イベント名         | 入力必須   |  イベントの説明      |
| ------------ | ---- |  --------- |
| media_upload    | いいえ    |  メディアファイルのアップロードが成功したとき。  |
| cover_upload    | いいえ    |  カバーのアップロードが成功したとき。  |
| media_progress    | いいえ    |  メディアファイルのアップロードの進行状況。  |
| cover_progress    | いいえ    |  カバーファイルのアップロードの進行状況。  |

## よくあるご質問

1. **`File`オブジェクトを取得する方法とは？**
`type`が`file`型の`input`タグを使用すると、`File`オブジェクトを取得できます。
2. **アップロードするファイルのサイズに制限はありますか？**
最大60GBをサポートしています。
3. **SDKがサポートしているブラウザのバージョンとは？**
Chrome、Firefox、`HTML5`およびIE10以降をサポートするその他の主流のブラウザ。
4. **アップロードの一時停止や再開などの機能を実装する方法とは？**
SDKの基盤となる層に、自動的に再開可能な機能が実装されているため、一時停止の本質は、`uploader.cancel()`メソッドを呼び出すことです。同様に、一時停止後のアップロード再開も、最初の`tcVod.upload`メソッドを呼び出すことで実行されます。違いは、アップロードが再開されるときに呼び出されるメソッドのパラメータは、以前にキャッシュされたパラメータである点です（例えば、グローバル変数を使用してアップロードの開始時にパラメータを保存して、アップロードの完了後にそれをクリアすることができます）。

