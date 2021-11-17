サーバーでのビデオアップロードのシナリオを実現させるために、VODではPHP SDKを提供しています。アップロードのフローは、[サーバーからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33912)をご参照ください。

## 統合方式

### composerを使用してインポート
```json
{
    "require": {
        "qcloud/vod-sdk-v5": "v2.4.0"
    }
}
```

### ソースコードパッケージによるインストール
プロジェクトの中でcomposerツールを使用して依存管理を行なっていない場合は、ソースコードを直接ダウンロードし、プロジェクトの中にインポートして使用することができます。

* [Githubからアクセス](https://github.com/tencentyun/vod-php-sdk-v5)
* [クリックしてPHP SDKダウンロード](https://github.com/tencentyun/vod-php-sdk-v5/raw/master/packages/vod-sdk.zip)

vod-sdk.zipファイルをプロジェクトの中で解凍し、autoload.phpファイルをインポートすれば使用できます。

##  シンプルビデオアップロード
### アップロードオブジェクトの初期化
Tencent Cloud APIキーを使用して、VodUploadClientインスタンスを初期化します。

**composerを使用してインポート**
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;

$client = new VodUploadClient("your secretId", "your secretKey");
```

**ソースコードを使用してインポート**
```php
<?php
require 'vod-sdk-v5/autoload.php';

use Vod\VodUploadClient;

$client = new VodUploadClient("your secretId", "your secretKey");
```

### アップロードリクエストのオブジェクト作成
```
use Vod\Model\VodUploadRequest;

$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
```

### アップロードの呼び出し
アップロードメソッドを呼び出し、アクセスポイントリージョンおよびアップロードリクエストを渡します。
```
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
```

>?アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。

## 高度な機能
### カバーの付加
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->CoverFilePath = "/data/videos/Wildlife-Cover.png";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
    echo "CoverUrl -> ". $rsp->CoverUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
```

### タスクフローの指定
まず、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058)、およびテンプレートに対する命名を行います。タスクフロー時に、このタスクフローテンプレート名を使用して`Procedure`パラメータを設定すれば、アップロード成功後、タスクフローを自動的に実行することができます。
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->Procedure = "Your Procedure Name";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
```

### サブアプリケーションのアップロード
[サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)IDを渡します。アップロード成功後、リソースは具体的なサブアプリケーションにのみ属します。
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->SubAppId = 101;
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
```

### ストレージリージョンの指定
[コンソール](https://console.cloud.tencent.com/vod)で目標ストレージリージョンがアクティブ化されているか確認します。アクティブ化されていない場合は、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)をご参照ください。最後に、`StorageRegion`の属性によって、ストレージリージョンの [英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を設定します。
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->StorageRegion = "ap-chongqing";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
```

### 一時的な証明書の使用によるアップロード
一時的な証明書の関連キー情報を渡し、一時的な証明書を使用して身分を検証し、アップロードします。
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("Credentials TmpSecretId", "Credentials TmpSecretKey", "Credentials Token");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
```


### アップロードのプロキシ設定
アップロードのプロキシ設定では、関係するプロトコルおよびデータはいずれもプロキシ経由で処理します。開発者はプロキシを参照しながら、ファイルを自社インターネットかたテンセントクラウドにアップロードします。
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;
use Vod\Model\VodUploadHttpProfile;

$client = new VodUploadClient("your secretId", "your secretKey");
$uploadHttpProfile = new VodUploadHttpProfile("your proxy addr");
$client->setHttpProfile($uploadHttpProfile);
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
```

### アダプティブビットレートストリーミング（ABS）ファイルのアップロード

このSDKでアップロードをサポートするABS形式のパッケージにはHLSとDASHがあります。manifest（M3U8またはMPD）で引用するメディアファイルは、必ず相対パスとし（URLおよび絶対パスは不可）、同時にmanifestと同じクラスのディレクトリまたは下の階層のディレクトリに置く必要があります（`../`は使用不可）。SDKのアップロードインターフェースを呼び出す時に、`MediaFilePath`パラメータにmanifest パスを入力すると、SDKが関連するメディアファイルリストを解析し、一緒にアップロードされます。

```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/prog_index.m3u8";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // アップロード異常の処理
    echo $e;
}
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
| MediaFilePath   | アップロード予定のメディアファイルパス。ローカルパスにする必要があります。URLはサポートしていません。| String | はい    |
| MediaType   | アップロード予定のメディアファイルタイプ。選択可能なタイプの詳細は、[ビデオアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760)をご参照ください。MediaFilePathに拡張子が付いている場合は入力不要です。        | String | いいえ    |
| MediaName   | アップロード後のメディアの名前。入力しない場合は、デフォルトでMediaFilePathのファイル名を採用します。      | String | いいえ    |
| CoverFilePath   | アップロード予定のカバーファイルパス。ローカルパスにする必要があります。URLはサポートしていません。| String | いいえ    |
| CoverType   | アップロード予定のカバーファイルタイプ。選択可能なタイプの詳細は、[ビデオアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760)をご参照ください。CoverFilePathに拡張子が付いている場合は入力不要です。        | String | いいえ    |
| Procedure   | アップロード後に自動的に実行させたいタスクフロー名。このパラメータは、タスクフローの作成（[API方式](https://intl.cloud.tencent.com/zh/document/product/266/33897) または[コンソール方式](https://console.cloud.tencent.com/vod/video-process/taskflow)）時にユーザーが指定します。具体的な内容は、[タスクフロー概要](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。        | String | いいえ    |
| ExpireTime   | メディアファイルの期限。表記形式はISO 8601規格に準拠します。詳細については、[ISO日時表記形式の説明](https://intl.cloud.tencent.com/document/product/266/11732)をご参照ください。        | String | いいえ    |
| ClassId   | カテゴリーID。メディアのカテゴリー管理に使用します。[カテゴリー作成](https://intl.cloud.tencent.com/document/product/266/35325) インターフェースによってカテゴリーを作成し、カテゴリーIDを取得することができます。        | Integer | いいえ    |
| SourceContext   | ソースコンテキスト。ユーザーリクエスト情報のパススルーに使用します。アップロードコールバックインターフェースは、このフィールドの値を戻します。最長250文字。        | String | いいえ    |
| SubAppId   | VOD [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)ID。サブアプリケーションの中のリソースにアクセスしたい場合は、このフィールドにサブアプリケーションIDを入力します。アクセスしない場合、この項目は入力不要です。        | Integer | いいえ    |
| StorageRegion   | ストレージリージョン。ストレージを予定/希望するリージョンを指定します。このフィールドにはストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を入力します。        | String | いいえ    |

アップロードレスポンスクラス`VodUploadResponse`

| 属性名      | 属性説明                   | タイプ      |
| --------- | ---------------------- | ------- |
| FileId   | メディアファイルの一意の標識。        | String |
| MediaUrl | メディア再生アドレス。 | String  |
| CoverUrl | メディアカバーアドレス。 | String  |
| RequestId | 一時的なリクエストID。リクエストごとに返されます。問題を特定する時はその回のリクエストのRequestIdを提供する必要があります。 | String  |

アップロードメソッド`VodUploadClient.upload(String region, VodUploadRequest request)`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| region   | アクセスポイントリージョン。どのリージョンのVODサーバーにリクエストするかであり、ストレージリージョンとは異なります。具体的な内容は、サポートする[リージョンリスト](https://intl.cloud.tencent.com/zh/document/product/266/34113#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)をご参照ください。        | String | はい    |
| request   | アップロードリクエスト。        | VodUploadRequest | はい    |

## エラーコードリスト
| ステータスコード         | 意味               |
| ----------- | ----------------- |
| InternalError       | 内部エラー。 |
| InvalidParameter.ExpireTime       | パラメータ値のエラー：期限。 |
| InvalidParameterValue.CoverType       | パラメータ値のエラー：カバーのタイプ。     |
| InvalidParameterValue.MediaType       | パラメータ値のエラー：メディアタイプ。           |
| InvalidParameterValue.SubAppId       | パラメータ値のエラー：サブアプリケーションID。              |
| InvalidParameterValue.VodSessionKey       | パラメータ値のエラー：VODセッション。              |
| ResourceNotFound       | リソースがありません。              |
