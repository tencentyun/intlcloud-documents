サーバーでのビデオアップロードのシナリオを実現させるために、VODではNode SDKを提供しています。アップロードのフローは、[サーバーからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33912)をご参照ください。

## 統合方式

### npmを使用してインストール
```
npm i vod-node-sdk --save
```

### ソースコードパッケージによるインストール
プロジェクトの中でnpmツールを使用して依存管理を行なっていない場合は、ソースコードを直接ダウンロードし、プロジェクトの中にインポートして使用することができます。

* [Githubからアクセス](https://github.com/tencentyun/vod-node-sdk)
* [クリックしてNode.js SDKをダウンロード](https://github.com/tencentyun/vod-node-sdk/archive/master.zip)

##  シンプルビデオアップロード
### アップロードオブジェクトの初期化
Tencent Cloud APIキーを使用して、VodUploadClientインスタンスを初期化します。

```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
```

### アップロードリクエストのオブジェクト作成
```
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
```

### アップロードの呼び出し
アップロードメソッドを呼び出して、アクセスポイントリージョンおよびアップロードリクエストを渡し、コールバック方式によって戻ってきた情報を取得します。
```
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // サービス異常の処理
        console.log(err)
    } else {
        // アップロード成功後の情報の取得
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

>?アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。

## 高度な機能
### カバーの付加
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.CoverFilePath = "/data/file/Wildlife-cover.png";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // サービス異常の処理
        console.log(err)
    } else {
        // アップロード成功後の情報の取得
        console.log(data.FileId);
        console.log(data.MediaUrl);
        console.log(data.CoverUrl);
    }
});
```

### タスクフローの指定
まず、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058)、およびテンプレートに対する命名を行います。タスクフロー時に、このタスクフローテンプレート名を使用して`Procedure`パラメータを設定すれば、アップロード成功後、タスクフローを自動的に実行することができます。
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.Procedure = "Your Procedure Name";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // サービス異常の処理
        console.log(err)
    } else {
        // アップロード成功後の情報の取得
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### サブアプリケーションのアップロード
[サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)IDを渡します。アップロード成功後、リソースは具体的なサブアプリケーションにのみ属します。
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.SubAppId = 101;
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // サービス異常の処理
        console.log(err)
    } else {
        // アップロード成功後の情報の取得
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### ストレージリージョンの指定
[コンソール](https://console.cloud.tencent.com/vod)で目標ストレージリージョンがアクティブ化されているか確認します。アクティブ化されていない場合は、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)を参考とすることができます。最後に、`StorageRegion`の属性によって、ストレージリージョンの [英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を設定します。
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.StorageRegion = "ap-chongqing";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // サービス異常の処理
        console.log(err)
    } else {
        // アップロード成功後の情報の取得
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### 一時的な証明書の使用によるアップロード
一時的な証明書の関連キー情報を渡し、一時的な証明書を使用して身分を検証し、アップロードします。
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("Credentials TmpSecretId", "Credentials TmpSecretKey", "Credentials Token");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // サービス異常の処理
        console.log(err)
    } else {
        // アップロード成功後の情報の取得
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### アダプティブビットレートストリーミング（ABS）ファイルのアップロード

このSDKでアップロードをサポートするABS形式のパッケージにはHLSとDASHがあります。manifest（M3U8またはMPD）で引用するメディアファイルは、必ず相対パスとし（URLおよび絶対パスは不可）、同時にmanifestと同じクラスのディレクトリまたは下の階層のディレクトリに置く必要があります（`../`は使用不可）。SDKのアップロードインターフェースを呼び出す時に、`MediaFilePath`パラメータにmanifest パスを入力すると、SDKが関連するメディアファイルリストを解析し、一緒にアップロードします。

```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/prog_index.m3u8";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // サービス異常の処理
        console.log(err)
    } else {
        // アップロード成功後の情報の取得
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

## インターフェースの説明
アップロードクライアントクラス`VodUploadClient`

| 属性名      | 属性説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| secretId   | Tencent Cloud APIキーID。        | String | はい    |
| secretKey | Tencent Cloud API Key。 | String  | はい    |

アップロードリクエストクラス`VodUploadRequest`

| 属性名      | 属性説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath   | アップロード予定のメディアファイルパス。ローカルパス（ユーザーサーバー上のパス）にする必要があります。URLはサポートしていません。| String | はい    |
| MediaType   | アップロード予定のメディアファイルタイプ。選択可能なタイプの詳細は、[ビデオアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760)をご参照ください。MediaFilePathに拡張子が付いている場合は入力不要です。        | String | いいえ    |
| MediaName   | アップロード後のメディアの名前。入力しない場合は、デフォルトでMediaFilePathのファイル名を採用します。      | String | いいえ    |
| CoverFilePath   | アップロード予定のカバーファイルパス。ローカルパス（ユーザーサーバー上のパス）にする必要があります。URLはサポートしていません。| String | いいえ    |
| CoverType   | アップロード予定のカバーファイルタイプ。選択可能なタイプの詳細は、[ビデオアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760)をご参照ください。CoverFilePathに拡張子が付いている場合は入力不要です。        | String | いいえ    |
| Procedure   | アップロード後に自動的に実行させたいタスクフロー名。このパラメータは、タスクフローの作成（[API方式](https://intl.cloud.tencent.com/zh/document/product/266/33897) または[コンソール方式](https://console.cloud.tencent.com/vod/video-process/taskflow)）時にユーザーが指定します。具体的な内容は、[タスクフロー概要](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。        | String | いいえ    |
| ExpireTime   | メディアファイルの‘’。表記形式はISO 8601規格に準拠します。詳細については、[ISO日時表記形式の説明](https://intl.cloud.tencent.com/document/product/266/11732)をご参照ください。        | String | いいえ    |
| ClassId   | カテゴリーID。メディアのカテゴリー管理に使用します。[カテゴリー作成](https://intl.cloud.tencent.com/document/product/266/35325) インターフェースによってカテゴリーを作成し、カテゴリーIDを取得することができます。        | Integer | いいえ    |
| SourceContext   | ソースコンテキスト。ユーザーリクエスト情報のパススルーに使用します。アップロードコールバックインターフェースは、このフィールドの値を戻します。最長250文字。        | String | いいえ    |
| SubAppId   | VOD [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)ID。サブアプリケーションの中のリソースにアクセスしたい場合は、このフィールドにサブアプリケーションIDを入力します。アクセスしない場合、このフィールドは入力不要です。        | Integer | いいえ    |
| StorageRegion   | ストレージリージョン。ストレージを予定/希望するリージョンを指定します。このフィールドにはストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を入力します。        | String | いいえ    |

アップロードレスポンスクラス`VodUploadResponse`

| 属性名      | 属性説明                   | タイプ      |
| --------- | ---------------------- | ------- |
| FileId   | メディアファイルの一意の標識。         | String |
| MediaUrl | メディア再生アドレス。   | String  |
| CoverUrl | メディアカバーアドレス。  | String  |
| RequestId | 一意のリクエストID。リクエストごとに返されます。問題を特定する時はその回のリクエストのRequestIdを提供する必要があります。  | String  |

アップロードメソッド`VodUploadClient.upload(String region, VodUploadRequest request, function callback)`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| region   | アクセスポイントリージョン。どのリージョンのVODサーバーにリクエストするかであり、ストレージリージョンとは異なります。具体的な内容は、サポートする[リージョンリスト](https://intl.cloud.tencent.com/document/product/266/34113)をご参照ください。       | String | はい    |
| request   | アップロードリクエスト。      | VodUploadRequest | はい    |
| callback   | アップロード完了コールバック関数。        | function | はい    |

アップロード完了コールバック関数`function(err, data)`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| err   | エラー情報。       | Exception | はい    |
| data   | アップロードレスポンスの結果。       | VodUploadResponse | はい    |

## エラーコードリスト

| ステータスコード         | 意味               |
| ----------- | ----------------- |
| InternalError       | 内部エラー。  |
| InvalidParameter.ExpireTime       | パラメータ値のエラー：期限。  |
| InvalidParameterValue.CoverType       | パラメータ値のエラー：カバーのタイプ。      |
| InvalidParameterValue.MediaType       | パラメータ値のエラー：メディアタイプ。            |
| InvalidParameterValue.SubAppId       | パラメータ値のエラー：サブアプリケーションID。               |
| InvalidParameterValue.VodSessionKey       | パラメータ値のエラー：VODセッション。               |
| ResourceNotFound       | リソースが存在しません。               |
