サーバーでのビデオアップロードのシナリオを実現させるために、VODではC# SDKを提供しています。アップロードのフローは、[サーバーからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33912)をご参照ください。

## 統合方式

### nugetによるインストール
1. コマンドラインによるインストール：
```
dotnet add package VodSDK --version 1.0.1
```
2. Visual Studioのnugetパッケージ管理ツールによって、VodSDKを検索し、インストールします。

### ソースコードパッケージによるインストール
プロジェクトの中でnugetツールを使用していない場合は、ソースコードを直接ダウンロードし、プロジェクトの中にインポートして使用することができます。

* [Githubからアクセス](https://github.com/tencentyun/vod-dotnet-sdk)
* [クリックしてC# SDKをダウンロード](https://github.com/tencentyun/vod-dotnet-sdk/archive/master.zip)

最新のコードがダウンロードされ、解凍後、プロジェクトの作業ディレクトリ下にインストールされますので、Visual Studio 2017を使用して開き、コンパイルします。このSDKはまだ外部のパッケージに依存しているため、以下のSDKを同時にインストールする必要があります。 
- [Tencent Cloud API SDK](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
- [Cloud Object Storage SDK](https://github.com/tencentyun/qcloud-sdk-dotnet)

##  シンプルなアップロード
### アップロードクライアントオブジェクトの初期化
Tencent Cloud APIキーを使用して、VodUploadClientインスタンスを初期化します。
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
```

### アップロードリクエストのオブジェクト作成
メディアのローカルアップロードパスを設定します。
```
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
```

### アップロードの呼び出し
アップロードメソッドを呼び出し、アクセスポイントリージョンおよびアップロードリクエストを渡します。
```
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // メディアFileIdの出力
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // サービスチームによるトラブルシューティング
    Console.WriteLine(e);
}
```

>アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。

## 高度な機能
### カバーの付加
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.CoverFilePath = "/data/videos/Wildlife.jpg";
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // メディアFileIdの出力
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // サービスチームによるトラブルシューティング
    Console.WriteLine(e);
}
```

### タスクフローの指定
まず、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058)、およびテンプレートに対する命名を行います。タスクフロー時に、このタスクフローテンプレート名を使用して`Procedure`パラメータを設定すれば、アップロード成功後、タスクフローを自動的に実行することができます。
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.Procedure = "Your Procedure Name";
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // メディアFileIdの出力
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // サービスチームによるトラブルシューティング
    Console.WriteLine(e);
}
```

### サブアプリケーションのアップロード
[サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)IDを渡します。アップロード成功後、リソースは具体的なサブアプリケーションにのみ属します。
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.SubAppId = 101;
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // メディアFileIdの出力
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // サービスチームによるトラブルシューティング
    Console.WriteLine(e);
}
```

### ストレージリージョンの指定
[コンソール](https://console.cloud.tencent.com/vod)で目標ストレージリージョンがアクティブ化されているか確認します。アクティブ化されていない場合は、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)を参考とすることができます。最後に、`StorageRegion`の属性によって、ストレージリージョンの [英語の略称](https://intl.cloud.tencent.com/document/product/266/33910)を設定します。
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.StorageRegion = "ap-chongqing";
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // メディアFileIdの出力
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // サービスチームによるトラブルシューティング
    Console.WriteLine(e);
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
| SubAppId   | VOD [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)ID。サブアプリケーションの中のリソースにアクセスしたい場合は、このフィールドにサブアプリケーションIDを入力します。アクセスしない場合、このフィールドは入力不要です。        | Integer | いいえ    |
| MediaType   | アップロード予定のメディアファイルタイプ。選択可能なタイプの詳細は、[ビデオアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760#.E6.96.87.E4.BB.B6.E7.B1.BB.E5.9E.8B)をご参照ください。MediaFilePathに拡張子が付いている場合は入力不要です。        | String | いいえ    |
| MediaName   | アップロード後のメディアの名前。入力しない場合は、デフォルトでMediaFilePathのファイル名を採用します。      | String | いいえ    |
| CoverFilePath   | アップロード予定のカバーファイルパス。ローカルパスにする必要があります。URLはサポートしていません。| String | いいえ    |
| CoverType   | アップロード予定のメディアファイルタイプ。選択可能なタイプの詳細は、[ビデオアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760#.E5.B0.81.E9.9D.A2.E7.B1.BB.E5.9E.8B)をご参照ください。CoverFilePathに拡張子が付いている場合は入力不要です。        | String | いいえ    |
| Procedure   | アップロード後に自動的に実行させたいタスクフロー名。このパラメータは、タスクフローの作成（[API方式](https://intl.cloud.tencent.com/document/product/266/34167) または[コンソール方式](https://console.cloud.tencent.com/vod/video-process/taskflow)）時にユーザーが指定します。具体的な内容は、[タスクフロー概要](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81)をご参照ください。        | String | いいえ    |
| ExpireTime   | メディアファイルの期限切れ時間。表記形式はISO 8601規格に準拠します。詳細については、[ISO日時表記形式の説明](https://intl.cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F)をご参照ください。        | String | いいえ    |
| ClassId   | カテゴリーID。メディアのカテゴリー管理に使用します。カテゴリー作成インターフェースによってカテゴリーを作成し、カテゴリーIDを取得することができます。        | Integer | いいえ    |
| SourceContext   | ソースコンテキスト。ユーザーリクエスト情報のパススルーに使用します。アップロードコールバックインターフェースは、このフィールドの値を戻します。最長250文字。        | String | いいえ    |
| StorageRegion   | ストレージリージョン。ストレージを予定/希望するリージョンを指定します。このフィールドにはストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/33910)を入力します。        | String | いいえ    |

アップロードレスポンスクラス`VodUploadResponse`

| 属性名      | 属性説明                   | タイプ      |
| --------- | ---------------------- | ------- |
| FileId   | メディアファイルの一意の標識。        | String |
| MediaUrl | メディア再生アドレス。 | String  |
| CoverUrl | メディアカバーアドレス。 | String  |
| RequestId | 一意のリクエストID。リクエストごとに返されます。問題を特定する時はその回のリクエストのRequestIdを提供する必要があります。 | String  |

アップロードメソッド`VodUploadClient.Upload(String region, VodUploadRequest request)`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| region   | アクセスポイントリージョン。どのリージョンのVODサーバーにリクエストするかであり、ストレージリージョンとは異なります。具体的な内容は、サポートする[リージョンリスト](https://intl.cloud.tencent.com/document/product/266/34113#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)をご参照ください。       | String | はい    |
| request   | アップロードリクエスト。        | VodUploadRequest | はい    |

## エラーコードリスト
| ステータスコード         | 意味               |
| ----------- | ----------------- |
| InternalError       | 内部エラー。 |
| InvalidParameter.ExpireTime       | パラメータ値のエラー：期限切れ時間。 |
| InvalidParameterValue.CoverType       | パラメータ値のエラー：カバーのタイプ。     |
| InvalidParameterValue.MediaType       | パラメータ値のエラー：メディアタイプ。           |
| InvalidParameterValue.SubAppId       | パラメータ値のエラー：サブアプリケーションID。              |
| InvalidParameterValue.VodSessionKey       | パラメータ値のエラー：VODセッション。              |
| ResourceNotFound       | リソースがありません。              |
