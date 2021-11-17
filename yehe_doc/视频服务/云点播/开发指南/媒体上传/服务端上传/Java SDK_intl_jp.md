サーバーでのビデオアップロードのシナリオを実現させるために、VODではJava SDKを提供しています。アップロードのフローは、[サーバーからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33912)をご参照ください。

## 統合方式

### Maven依存によるインポート

プロジェクトのpom.xmlファイルにVOD SDKの依存を追加すれば完了です。

```
<dependency>
    <groupId>com.qcloud</groupId>
    <artifactId>vod_api</artifactId>
    <version>2.1.4</version>
</dependency>
```

### jarパッケージによるインポート

プロジェクトがMaven方式の採用で依存管理を行なっていない場合は、次の方式を採用し、各々に必要なjarパッケージをダウンロードして、プロジェクトにインポートすることができます。

| jarファイル         | 説明    |
| ------------ | ------------ |
| vod_api-2.1.4.jar | VOD SDK。 |
| jackson-annotations-2.9.0.jar,jackson-core-2.9.7.jar,jackson-databind-2.9.7.jar,gson-2.2.4.jar       | オープンソースのJSON関連ライブラリ。 |
| cos_api-5.4.10.jar            | Tencent Cloud Cloud Object StorageサービスCOS SDK。                          |
| tencentcloud-sdk-java-3.1.2.jar             | Tencent Cloud API SDK。                        |
| commons-codec-1.10.jar,commons-logging-1.2.jar,log4j-1.2.17.jar,slf4j-api-1.7.21.jar,slf4j-log4j12-1.7.21.jar           | オープンソースのログ関連ライブラリ。    |
| httpclient-4.5.3.jar,httpcore-4.4.6.jar,okhttp-2.5.0.jar,okio-1.6.0.jar | オープンソースのHTTP処理ライブラリ。                            |
| joda-time-2.9.9.jar | オープンソースの時間処理ライブラリ。                            |
| jaxb-api-2.3.0.jar | オープンソースのXML処理ライブラリ。                            |
| bcprov-jdk15on-1.59.jar | オープンソースの暗号化処理ライブラリ。                            |

[Java SDK関連jarパッケージ](https://github.com/tencentyun/vod-java-sdk/raw/master/packages/vod-sdk-jar.zip)をクリックして、ダウンロードしたjarパッケージをプロジェクトにインポートすれば、使用できます。



##  シンプルなアップロード
### アップロードクライアントオブジェクトの初期化
Tencent Cloud APIキーを使用して、VodUploadClientインスタンスを初期化します。
```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
```

### アップロードリクエストのオブジェクト作成
メディアのローカルアップロードパスを設定します。
```
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
```

### アップロードの呼び出し
アップロードメソッドを呼び出し、アクセスポイントリージョンおよびアップロードリクエストを渡します。
```
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```

>?アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。

## 高度な機能
### カバーの付加
```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
request.setCoverFilePath("/data/videos/Wildlife.jpg");
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```

### タスクフローの指定
まず、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058)、およびテンプレートに対する命名を行います。タスクフロー時に、このタスクフローテンプレート名を使用して`Procedure`パラメータを設定すれば、アップロード成功後、タスクフローを自動的に実行することができます。
```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
request.setProcedure("Your Procedure Name");
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```

### サブアプリケーションのアップロード
[サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)IDを渡します。アップロード成功後、リソースは具体的なサブアプリケーションにのみ属します。
```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
request.setSubAppId(101);
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```

### ストレージリージョンの指定
[コンソール](https://console.cloud.tencent.com/vod)で目標ストレージリージョンがアクティブ化されているか確認します。アクティブ化されていない場合は、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)を参考とすることができます。最後に、`StorageRegion`の属性によって、ストレージリージョンの [英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を設定します。
```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
request.setStorageRegion("ap-chongqing");
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```

### パート同時実行数の指定
パート同時実行数は、大きなファイルに対応するもので、複数のパートに分割すると同時にアップロードするものです。パート同時アップロードのメリットは、1個のファイルのアップロードを素早く完了させられることで、SDKはファイルのサイズを基に、通常アップロードとパートアップロードを自動的に選択します。ユーザーは、パートアップロードの各手順に気を遣う必要もなく、パートでのアップロードを実現できます。こうしてファイルの同時パート数は、`ConcurrentUploadNumber`パラメータによって指定します。
```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
request.setConcurrentUploadNumber(5);
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```

### 臨時証明書の使用によるアップロード
臨時証明書の関連キー情報を渡し、臨時証明書を使用して身分を検証し、アップロードします。
```
VodUploadClient client = new VodUploadClient("Credentials TmpSecretId", "Credentials TmpSecretKey", "Credentials Token");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```


### アップロードのプロキシ設定
アップロードのプロキシ設定では、関係するプロトコルおよびデータはいずれもプロキシ経由で処理します。開発者はプロキシの助けを借りて、ファイルを自社イントラネットからTencent Cloudにアップロードすることができます。
```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/Wildlife.wmv");
HttpProfile httpProfile = new HttpProfile();
httpProfile.setProxyHost("your proxy ip");
httpProfile.setProxyPort(8080); //your proxy port
client.setHttpProfile(httpProfile);
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
}
```

### アダプティブビットレートストリーミング（ABS）ファイルのアップロード

このSDKでアップロードをサポートするABS形式のパッケージにはHLSとDASHがあります。manifest（M3U8またはMPD）で引用するメディアファイルは、必ず相対パスとし（URLおよび絶対パスは不可）、同時にmanifestと同じクラスのディレクトリまたは下の階層のディレクトリに置く必要があります（`../`は使用不可）。SDKのアップロードインターフェースを呼び出す時に、`MediaFilePath`パラメータにmanifest パスを入力すると、SDKが関連するメディアファイルリストを解析し、一緒にアップロードします。

```
VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.setMediaFilePath("/data/videos/prog_index.m3u8");
try {
    VodUploadResponse response = client.upload("ap-guangzhou", request);
    logger.info("Upload FileId = {}", response.getFileId());
} catch (Exception e) {
    // サービスチームによるトラブルシューティング
    logger.error("Upload Err", e);
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
| ExpireTime   | メディアファイルの期限切れ時間。表記形式はISO 8601規格に準拠します。詳細については、[ISO日時表記形式の説明](https://intl.cloud.tencent.com/document/product/266/11732)をご参照ください。        | String | いいえ    |
| ClassId   | カテゴリーID。メディアのカテゴリー管理に使用します。[カテゴリー作成](https://intl.cloud.tencent.com/document/product/266/35325) インターフェースによってカテゴリーを作成し、カテゴリーIDを取得することができます。        | Integer | いいえ    |
| SourceContext   | ソースコンテキスト。ユーザーリクエスト情報のパススルーに使用します。アップロードコールバックインターフェースは、このフィールドの値を戻します。最長250文字。        | String | いいえ    |
| SubAppId   | VOD [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)ID。サブアプリケーションの中のリソースにアクセスしたい場合は、このフィールドにサブアプリケーションIDを入力します。アクセスしない場合、このフィールドは入力不要です。        | Integer | いいえ    |
| StorageRegion   | ストレージリージョン。ストレージを予定/希望するリージョンを指定します。このフィールドにはストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を入力します。        | String | いいえ    |
| ConcurrentUploadNumber   | パート同時実行数。大きなファイルを対象にパートアップロードする時に有効となります。        | Integer | いいえ    |

アップロードレスポンスクラス`VodUploadResponse`

| 属性名      | 属性説明                   | タイプ      |
| --------- | ---------------------- | ------- |
| FileId   | メディアファイルの一意の標識。        | String |
| MediaUrl | メディア再生アドレス。 | String  |
| CoverUrl | メディアカバーアドレス。 | String  |
| RequestId | 一意のリクエストID。リクエストごとに返されます。問題を特定する時はその回のリクエストのRequestIdを提供する必要があります。 | String  |

アップロードメソッド`VodUploadClient.upload(String region, VodUploadRequest request)`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| region   | アクセスポイントリージョン。どのリージョンのVODサーバーにリクエストするかであり、ストレージリージョンとは異なります。具体的な内容は、サポートする[リージョンリスト](https://intl.cloud.tencent.com/zh/document/product/266/34113#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)をご参照ください。       | String | はい    |
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
