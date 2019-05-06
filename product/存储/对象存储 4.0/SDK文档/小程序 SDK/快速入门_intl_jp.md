## ダウンロードおよびインストール

### 関連するリソース

ミニプログラムスリムSDKリソースダウンロードアドレス：[GitHub ダウンロード](https://github.com/tencentyun/cos-wx-sdk-v5)。

### 環境依存関係

WeChatのミニプログラム環境に適します。

### SDKインストール
ミニプログラムSDKのインストールは、手動インストールとnpmインストールの2つの方法があります。具体的なインストール方法は、以下のとおりです。

- 手動インストール
ソースコードの[cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js)をミニプログラムコードディレクトリにコピーします。コードは、相対パスで参照できます。
```shell
var COS = require('./cos-wx-sdk-v5.js')
```
- npmインストール
ミニプログラムコードは、webpackでパッケージされた場合、npmを介して依存ソフトウェアをインストールすればよい。
```shell
npm install cos-wx-sdk-v5
```
ミニプログラムコードは、`var COS = require('cos-wx-sdk-v5');`で参照されます。

### 事前準備

1. [COSコンソール](https://console.cloud.tencent.com/cos4)にログインし、バケットを作成し、Bucket（バケット名）とRegion（地域名称）を取得します。
2. 管理コンソールの[暗号鍵管理](https://console.cloud.tencent.com/capi)でプロジェクトのSecretIdとSecretKeyを取得します。

#### 署名の計算

署名計算がフロントエンドで行われると、SecretIdとSecretKeyを公開しますので、署名計算プロセスをバックエンドにて実現します。フロントエンドは、ajaxを介してバックエンドから一時暗号鍵を取得し、正式配置のときにバックエンドに当サイトの権限チェックを追加してください。

ここに、PHPとNode.jsの[署名例](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/)を提供します。他の言語は、一時暗号鍵を使用します。詳細については、[一時暗号鍵の生成および使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

## クイックスタート

### 初期化

```js
var cos = new COS({
    // ForcePathStyle: true, // 大量のバケットを使用した場合、サフィックスのマッチングでドメイン名を有効にすることで、ホワイトリストに構成されたドメイン名の数を減らすことができます。リクエストときに地域のドメイン名を使用します
    getAuthorization: function (options, callback) {
        // 署名を非同時的に取得します
        wx.request({
            url: 'https://example.com/sts.php',
            data: {
                Method: options.Method,
                Key: options.Key
            },
            dataType: 'text',
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    ExpiredTime: data.expiredTime, // SDKがExpiredTime時間前にgetAuthorizationを再び呼び出すことはしません
                });
            }
        });
    }
});
```

初期化方法の詳細については、[demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-sdk.js)例を参照してください。

### バケットの作成

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
}, function (err, data) {
    console.log(err || data);
});
```

>!ミニプログラムにバケットを作成する必要があるが、バケット名が未知の場合、バケット名をドメイン名のホワイトリストに構成できません。関連する処理措置については、[よくある質問](https://cloud.tencent.com/document/product/436/30746#.E5.B0.8F.E7.A8.8B.E5.BA.8F.E9.87.8C.E8.AF.B7.E6.B1.82.E5.A4.9A.E4.B8.AA.E5.9F.9F.E5.90.8D.EF.BC.8C.E6.88.96.E8.80.85.E5.AD.98.E5.82.A8.E6.A1.B6.E5.90.8D.E7.A7.B0.E4.B8.8D.E7.A1.AE.E5.AE.9A.EF.BC.8C.E6.80.8E.E4.B9.88.E8.A7.A3.E5.86.B3.E7.99.BD.E5.90.8D.E5.8D.95.E9.85.8D.E7.BD.AE.E5.92.8C.E9.99.90.E5.88.B6.E9.97.AE.E9.A2.98.EF.BC.9F)を参照してください。

### バケットリストの照合

```js
cos.getService(function (err, data) {
    console.log(err || data);
});
```

### アップデートオブジェクト

ミニプログラムアップロードAPI wx.uploadFileは、POSTリクエストのみをサポートします。SDKアップロードファイルは、postObjectAPIを使用します。ミニプログラムがアップロードファイルAPIのみを使用するとき、SDKを参照しないことをおすすめします。簡単な例[demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js)を参照してください。

```js
// まずはファイルを選択し、一時的なパスを取得します
wx.chooseImage({
    count: 1, // デフォルトは9
    sizeType: ['original'], // 元画像か圧縮画像を指定できます。デフォルトは元画像です
    sourceType: ['album', 'camera'], // 参照元としてアルバムかカメラを指定できます。デフォルトは両方です
    success: function (res) {
        var filePath = res.tempFiles[0].path;
        var filename = filePath.substr(filePath.lastIndexOf('/') + 1);
        cos.postObject({
            Bucket: 'examplebucket-1250000000',
            Region: 'ap-beijing',
            Key: filename,
            FilePath: filePath,
            onProgress: function (info) {
                console.log(JSON.stringify(info));
            }
        }, function (err, data) {
            console.log(err || data);
        });
    }
});
```

### オブジェクトリストの照合

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Prefix: 'exampledir/',
}, function (err, data) {
    console.log(err || data);
});
```

### オブジェクトUrlの取得

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.png',
}, function (err, data) {
    console.log(err || data.Url);
});
```

### テキスト内容をオブジェクトにアップロードします

テキスト内容のアップロードは、putObject APIによって実行されます。putObject APIの呼び出す実際はwx.request APIを呼び出します。

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.txt',
    Body: 'hello',
    onProgress: function (info) {
        console.log(JSON.stringify(info));
    }
}, function (err, data) {
    console.log(err || data);
});
```

### オブジェクトのテキスト内容の読取り

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.txt',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### オブジェクトの削除

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.png',
}, function (err, data) {
    console.log(err || data.Body);
});
```

## FAQ
ミニプログラムSDKの使用中に質問がある場合、[よくある質問](https://cloud.tencent.com/document/product/436/30746#.E5.B0.8F.E7.A8.8B.E5.BA.8F.E9.87.8C.E8.AF.B7.E6.B1.82.E5.A4.9A.E4.B8.AA.E5.9F.9F.E5.90.8D.EF.BC.8C.E6.88.96.E8.80.85.E5.AD.98.E5.82.A8.E6.A1.B6.E5.90.8D.E7.A7.B0.E4.B8.8D.E7.A1.AE.E5.AE.9A.EF.BC.8C.E6.80.8E.E4.B9.88.E8.A7.A3.E5.86.B3.E7.99.BD.E5.90.8D.E5.8D.95.E9.85.8D.E7.BD.AE.E5.92.8C.E9.99.90.E5.88.B6.E9.97.AE.E9.A2.98.EF.BC.9F)ドキュメントのミニプログラム部分を参照してください。


## 関連ドキュメント

完全なドキュメントは作成中です。現在、ミニプログラムはシャードに関するAPIをサポートしません。アップロード、ダウンロードに関する機能を使用する必要がある場合、[ソースコード](https://github.com/tencentyun/cos-wx-sdk-v5)と[demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js)を参照してください。その他のAPIドキュメントについては、JavaScript SDKの[APIドキュメント](https://cloud.tencent.com/document/product/436/12260)を参照してください。

