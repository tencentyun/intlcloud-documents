## 概要

本ドキュメントはオブジェクトのアップロード操作に関連するAPI概要およびSDKサンプルコードを提供します。

**簡単な操作**

| API                                                          | 操作名         | 操作説明                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | オブジェクトのシンプルアップロード       | 1つのオブジェクトをバケットにアップロードします     |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | オブジェクトのフォームアップロード   | フォームを使用してアップロードオブジェクトをリクエストします                      |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 	追加オブジェクトのアップロード  |	ブロック追加の方式を使用してオブジェクトをアップロードします   |

**マルチパート操作**

| API                                                          | 操作名         | 操作説明                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | マルチパートアップロードの照会   | 進行中のマルチパートアップロード情報を照会します          |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | マルチパートアップロードの初期化 | マルチパートアップロードを初期化する操作です     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | マルチパートのアップロード       | オブジェクトをマルチパートアップロードします                        |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | マルチパートのコピー       | 他のオブジェクトをマルチパートにコピーします             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | アップロードされたブロックの照会   | 特定のマルチパートアップロード操作でアップロードされたブロックを照会します   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | マルチパートアップロードの完了   | ファイル全体のマルチパートアップロードが完了しました               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | マルチパートアップロードの終了   | マルチパートアップロード操作を終了してすでにアップロードしたブロックを削除します |


## 高度なインターフェース（推奨）

高度なAPIはクラスTransferManagerによって各シンプルなインターフェースをカプセル化することで、より操作が簡単なインターフェースを提供します。内部でスレッドプールを使用し、ユーザーのリクエストを同時に受け入れて処理するため、ユーザーは複数のタスクを送信した後に非同期でタスクを実行することも選択できます。

TransferManagerインスタンスは同時に実行できます。ここでは1つのプロセスに1つのTransferManagerインスタンスだけを作成することをお勧めします。このインスタンスによって高度なインターフェースを呼び出すことができない場合、さらにこのインスタンスを閉じることを選択します。


### 機能説明

高度なインターフェースはシンプルアップロード、マルチパートアップロードのインターフェースをカプセル化し、ファイルサイズに応じてインテリジェントにアップロード方式を選択し、同時にレジューム、アップロード時の進捗の表示などの機能をサポートします。

>?
> - マルチパート閾値はシンプルアップロードを使用するかマルチパートアップロードを使用するかの区分に使用され、閾値はユーザー自身による設定をサポートします。デフォルトは5MBです。
> - マルチパートのサイズはユーザー自身による設定をサポートしています。デフォルトは1MBです。
> - ストリームタイプのアップロードでは、マルチパート閾値より小さいまたはContent-Lengthヘッダーが指定されていないアップロードの場合、高度なインターフェースはシンプルアップロードを選択することができます。
> - ストリームタイプのアップロードでは、マルチパート閾値より大きくContent-Lengthヘッダーが指定されたアップロードの場合、高度なインターフェースはマルチパートアップロードを選択することができます。
> - ファイルタイプのアップロードでは、マルチパート閾値より小さいファイルの場合、高度なインターフェースはシンプルアップロードを選択することができます。マルチパート閾値より大きいファイルの場合、高度なインターフェースはマルチパートアップロードを選択することができます。
> - ファイルタイプのマルチパートアップロードでは、高度なインターフェースは複数のスレッド複数のブロックを同時にアップロードします。
> - マルチパートアップロードに対して、高度なアップロードインターフェースは進捗を取得する機能を提供しています。具体的な内容は次の例をご参照ください。
> 

### TransferManagerの作成

高度なインターフェースの操作を使用する前に、まずTransferManagerのインスタンスを作成する必要があります。

```java
// TransferManagerインスタンスを作成します。このインスタンスは後で高度なインターフェースを呼び出すために使用されます
TransferManager createTransferManager() {
    // COSClientインスタンスを作成します。これはCOSサービスにアクセスする基本的なインスタンスです。
    // コードの詳細はこちらをご覧ください: 簡単な操作 -> COSClientの作成
    COSClient cosClient = createCOSClient();

    // スレッドプールのサイズをカスタマイズします。クライアントとCOSネットワークが十分（例えばTencent CloudのCVMを使用する、同一リージョンでCOSをアップロードする）な状況で、16または32に設定することをお勧めします。これによって十分にネットワークリソースを利用することができます
    // パブリックネットワーク伝送を使用しており、ネットワーク帯域幅の品質が低い状況では、この値を小さくすることをお勧めします。それによってネットワーク速度が遅いため、リクエストがタイムアウトすることを回避します。
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // threadpoolを渡します。スレッドプールを渡さない場合、デフォルトではTransferManager内にシングルスレッドのスレッドプールを生成します。
    TransferManager transferManager = new TransferManager(cosClient, threadPool);

    // 高度なインターフェースの設定項目を設定します
    // マルチパートアップロード閾値とマルチパートサイズはそれぞれ5MBおよび1MBです
    TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
    transferManagerConfiguration.setMultipartUploadThreshold(5*1024*1024);
    transferManagerConfiguration.setMinimumUploadPartSize(1*1024*1024);
    transferManager.setConfiguration(transferManagerConfiguration);

    return transferManager;
}
```

### パラメータの説明

TransferManagerConfigurationクラスは高度なインターフェースの設定情報を記録するために使用され、その主なメンバー説明は次のとおりです。

|  メンバー名 | 設定方法            | 説明                                                         | タイプ           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize   | set 方法 | マルチパートアップロードのブロックサイズ、単位：バイト（Byte）、デフォルトは5MB | long         |
| multipartUploadThreshold   | set 方法 | この値以上の場合、同時にファイルをマルチパートアップロードします。単位：バイト（Byte）、デフォルトは5MB | long         |
| multipartCopyThreshold         | set 方法 | この値以上の場合、同時にファイルをマルチパートコピーします。単位：バイト（Byte）、デフォルトは5GB | long           |
| multipartCopyPartSize        | set 方法 | マルチパートコピーするブロックサイズ、単位：バイト（Byte）、デフォルトは100MB           | long    |

### TransferManagerを閉じる

TransferManagerのインスタンスによって高度なインターフェースを呼び出さないと確定した後は、インスタンスをシャットダウンして、リソースの漏洩を防止してください。

```java
void shutdownTransferManager(TransferManager transferManager) {
    // 指定パラメータがtrueの場合、TransferManager内部のCOSClientインスタンスは同時にシャットダウンします。
    // 指定パラメータがfalseの場合、 TransferManager内部のCOSClientインスタンスはシャットダウンされません。
    transferManager.shutdownNow(true);
}
```

### ローカルファイルのアップロード

アップロードするソースはローカルのファイルです。

#### 方法原型

```java
// オブジェクトのアップロード
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### リクエスト例

```java
// 高度なインターフェースを使用するにはまずこのプロセスにTransferManagerインスタンスが存在することを確認する必要があります。ない場合は作成してください
// コードの詳細はこちらをご覧ください：高度なインターフェース ->TransferManagerの作成
TransferManager transferManager = createTransferManager();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// ローカルファイルパス
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

//オブジェクトのカスタムHeadersを設定する必要がある場合は、次のコードを参照することができます。不要な場合は以下の行を省略することができます。オブジェクトのカスタムHeadersの詳細な情報はhttps://cloud.tencent.com/document/product/436/13361をご参照ください
ObjectMetadata objectMetadata = new ObjectMetadata();

//Content-Type、Cache-Control、Content-Disposition、Content-Encoding、Expiresの5つのカスタムHeadersを設定する場合は、objectMetadata.setHeader()を使用することをお勧めします
objectMetadata.setHeader(key, value);
//“x-cos-meta-[拡張子のカスタマイズ]” をこのようなカスタムHeaderに設定する場合は、以下を推奨します
Map<String, String> userMeta = new HashMap<String, String>();
userMeta.put("x-cos-meta-[拡張子のカスタマイズ]", "value");
objectMetadata.setUserMetadata(userMeta);

putObjectRequest.withMetadata(objectMetadata);

try {
    // 高度なインターフェースは非同期結果のUploadを返します
    // waitForUploadResultメソッドを同期的に呼び出してアップロードの完了を待ち、成功するとUploadResultを返し、 失敗するとエラーがスローされます
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでTransferManagerインスタンスを使用しないと確定してから、これを閉じます
// コードの詳細はこちらをご覧ください：高度なインターフェース -> TransferManagerを閉じる
shutdownTransferManager(transferManager);
```

#### パラメータの説明

| パラメータ名         | 説明         | タイプ             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードリクエスト | PutObjectRequest |

Request メンバー説明：

| Request メンバー | 設定方法              | 説明                                                         | タイプ           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | コンストラクタまたはset方法 | バケットの命名形式はBucketName-APPIDです。詳細は[命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String         |
| key          | コンストラクタまたはset方法 | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` で、オブジェクトキーがdoc/picture.jpgの場合は、 [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String         |
| file         | コンストラクタまたはset方法 | ローカルファイル                                                     | File           |
| input        | コンストラクタまたはset方法 | 入力ストリーム                                                       | InputStream    |
| metadata     | コンストラクタ又はset方法 | ファイルのメタデータ                                                 | ObjectMetadata |
|trafficLimit | set 方法| オブジェクトのアップロードにトラフィック制御を行うために使用します。単位：bit/s、デフォルトではトラフィックの制御は行いません | Int|いいえ|

#### 戻り値

- 成功：Uploadが返され、アップロードが終了したかどうかを確認でき、同期してアップロードが終了するのを待つことができます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

UploadのwaitForUploadResult()メソッドを呼び出すことによって取得したオブジェクトのアップロード情報はクラスUploadResult内に記録されます。クラスUploadResult の主要メンバー説明は次のとおりです。

| メンバー名   | 説明                                                         | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名形式はBucketName-APPIDです。詳細は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String |
| key        | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br/>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` では、オブジェクトキーはdoc/picture.jpgです。詳細については [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String  |
| requestId  | リクエスト Id                                                       | String |
| dateStr    | 現在のサーバー側の時間                                               | String |
| versionId  | バケットのバージョン管理機能が有効な場合は、オブジェクトのバージョン番号Idを返します                      | String |
| crc64Ecma  | サーバーがオブジェクトの内容に基づいて計算したCRC64                           | String |

### アップロードストリームのタイプ

アップロードのソースはInputStreamタイプ（およびそのサブタイプ）のストリームインスタンスです。

#### 方法原型

```java
// オブジェクトのアップロード
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### リクエスト例

```java
// 高度なインターフェースを使用するにはまずこのプロセスにTransferManagerインスタンスが存在することを確認する必要があります。ない場合は作成してください
// コードの詳細はこちらをご覧ください：高度なインターフェース ->TransferManagerの作成
TransferManager transferManager = createTransferManager();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";

// ここではByteArrayInputStreamを作成することを例としていますが、実際にはここではアップロードしようとする InputStreamタイプのストリームである必要があります
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// アップロードのストリームの正確なストリーム長が取得できる場合は、必ずcontent-lengthを入力することをお勧めします
// 確実に取得することができない場合は、以下の行を省略することができますが、同時に高度なインターフェースもマルチパートアップロードを使用することはできません
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    // 高度なインターフェースは非同期結果のUploadを返します
    // waitForUploadResultメソッドを同期的に呼び出してアップロードの完了を待ち、成功するとUploadResultを返し、 失敗するとエラーがスローされます
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでTransferManagerインスタンスを使用しないと確定してから、これを閉じます
// コードの詳細はこちらをご覧ください：高度なインターフェース -> TransferManagerを閉じる
shutdownTransferManager(transferManager);
```

#### パラメータの説明

| パラメータ名         | 説明         | タイプ             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードリクエスト | PutObjectRequest |

Request メンバー説明：

| Request メンバー | 設定方法              | 説明                                                         | タイプ           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | コンストラクタまたはset方法 | バケットの命名形式はBucketName-APPIDです。詳細は[命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String         |
| key          | コンストラクタまたはset方法 | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` で、オブジェクトキーがdoc/picture.jpgの場合は、 [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String         |
| file         | コンストラクタまたはset方法 | ローカルファイル                                                     | File           |
| input        | コンストラクタまたはset方法 | 入力ストリーム                                                       | InputStream    |
| metadata     | コンストラクタ又はset方法 | ファイルのメタデータ                                                 | ObjectMetadata |
|trafficLimit | set 方法| オブジェクトのアップロードにトラフィック制御を行うために使用します。単位：bit/s、デフォルトではトラフィックの制御は行いません | Int|いいえ|

#### 戻り値

- 成功：Uploadが返され、アップロードが終了したかどうかを確認でき、同期してアップロードが終了するのを待つことができます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

UploadのwaitForUploadResult()メソッドを呼び出すことによって取得したオブジェクトのアップロード情報はクラスUploadResult内に記録されます。クラスUploadResult の主要メンバー説明は次のとおりです。

| メンバー名   | 説明                                                         | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名形式はBucketName-APPIDです。詳細は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String |
| key        | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br/>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` では、オブジェクトキーはdoc/picture.jpgです。詳細については [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String  |
| requestId  | リクエスト Id                                                       | String |
| dateStr    | 現在のサーバー側の時間                                               | String |
| versionId  | バケットのバージョン管理機能が有効な場合は、オブジェクトのバージョン番号Idを返します                      | String |
| crc64Ecma  | サーバーがオブジェクトの内容に基づいて計算したCRC64                           | String |

### アップロードの進捗の表示

>? マルチパートアップロードを使用したインターフェースのみアップロードの進捗を表示することができます。
>

アップロードの進捗を表示するにはまず独自のアップロードの進捗を出力する関数が必要です。この関数内でインターフェースを呼び出すことによってアップロードに成功したサイズを取得して現在の進捗を計算します。

#### 方法原型

```java
// オブジェクトのアップロード
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### リクエスト例

```java
// 以下の例を参考に、実際の状況を組み合わせて調整してください
void showTransferProgress(Transfer transfer) {
    // ここでのTransferは非同期アップロード結果Uploadの親クラスです
    System.out.println(transfer.getDescription());

    // transfer.isDone() アップロードが完了しているかどうかを照会します
    while (transfer.isDone() == false) {
        try {
            // 2秒ごとに1回進捗を取得します
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }

        TransferProgress progress = transfer.getProgress();
        long sofar = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("upload progress: [%d / %d] = %.02f%%\n", sofar, total, pct);
    }

    // 完成Completed、または失敗Failed
    System.out.println(transfer.getState());
}
```

アップロードファイルを組み合わせたサンプルコードは次のとおりです。

```java
// 高度なインターフェースを使用するにはまずこのプロセスにTransferManagerインスタンスが存在することを確認する必要があります。ない場合は作成してください
// コードの詳細はこちらをご覧ください：高度なインターフェース ->TransferManagerの作成
TransferManager transferManager = createTransferManager();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// ローカルファイルパス
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // 高度なインターフェースは非同期結果のUploadを返します
    Upload upload = transferManager.upload(putObjectRequest);
    // アップロードが終了するまで、アップロードの進捗を出力します
    showTransferProgress(upload);
    // 発生する可能性があるエラーを捕捉します
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでTransferManagerインスタンスを使用しないと確定してから、これを閉じます
// コードの詳細はこちらをご覧ください：高度なインターフェース -> TransferManagerを閉じる
shutdownTransferManager(transferManager);
```

#### 取得の進捗の説明

uploadによってこのクラスのgetProgressは TransferProgressクラスを取得できます。このクラスの以下の3つの方法によってアップロードの進捗を取得します。説明は次のとおりです。

| 方法名                 | 説明                | タイプ    |
| ----------------------- | ------------------ | -----   |
| getBytesTransferred     | すでにアップロードしたバイトを取得する   | long   |
| getTotalBytesToTransfer | 総ファイルのバイト数を取得する  | long   |
| getPercentTransferred   | すでにアップロードしたバイトのパーセンテージを取得する  | double |

#### パラメータの説明

| パラメータ名         | 説明         | タイプ             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードリクエスト | PutObjectRequest |

Request メンバー説明：

| Request メンバー | 設定方法              | 説明                                                         | タイプ           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | コンストラクタまたはset方法 | バケットの命名形式はBucketName-APPIDです。詳細は[命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String         |
| key          | コンストラクタまたはset方法 | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` で、オブジェクトキーがdoc/picture.jpgの場合は、 [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String         |
| file         | コンストラクタまたはset方法 | ローカルファイル                                                     | File           |
| input        | コンストラクタまたはset方法 | 入力ストリーム                                                       | InputStream    |
| metadata     | コンストラクタ又はset方法 | ファイルのメタデータ                                                 | ObjectMetadata |
|trafficLimit | set 方法| オブジェクトのアップロードにトラフィック制御を行うために使用します。単位：bit/s、デフォルトではトラフィックの制御は行いません | Int|いいえ|

#### 戻り値

- 成功：Uploadが返され、アップロードが終了したかどうかを確認でき、同期してアップロードが終了するのを待つことができます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

UploadのwaitForUploadResult()メソッドを呼び出すことによって取得したオブジェクトのアップロード情報はクラスUploadResult内に記録されます。クラスUploadResult の主要メンバー説明は次のとおりです。

| メンバー名   | 説明                                                         | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名形式はBucketName-APPIDです。詳細は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String |
| key        | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br/>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` では、オブジェクトキーはdoc/picture.jpgです。詳細については [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String  |
| requestId  | リクエスト ID                                                       | String |
| dateStr    | 現在のサーバー側の時間                                               | String |
| versionId  | 当バケットのバージョン管理機能が有効な場合は、オブジェクトのバージョン番号IDを返します                      | String |
| crc64Ecma  | サーバーがオブジェクトの内容に基づいて計算したCRC64                           | String |

### アップロードの一時停止、継続およびキャンセル

高度なインターフェースを使用するとアップロードタスクを一時停止し、その後アップロードを継続するか、またはアップロードタスクを直接取り消すことができます。

> ?
> - ストリーミングアップロードは一時停止、継続およびキャンセルができません。
> - シンプルアップロードは一時停止、継続およびキャンセルができません。
> - 暗号化アップロードは一時停止、継続およびキャンセルができません。

#### 方法原型

```java
// オブジェクトのアップロード
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### リクエスト例

```java
// 高度なインターフェースを使用するにはまずこのプロセスにTransferManagerインスタンスが存在することを確認する必要があります。ない場合は作成してください
// コードの詳細はこちらをご覧ください：高度なインターフェース -> サンプルコード：TransferManagerの作成
TransferManager transferManager = createTransferManager();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// ローカルファイルパス
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // 高度なインターフェースは非同期結果のUploadを返します
    Upload upload = transferManager.upload(putObjectRequest);
    // 3秒待機して、一部をアップロードします
    Thread.sleep(3000);
    // アップロードを一時停止し、PersistableUploadインスタンスを取得して、その後の復元に使用します
    PersistableUpload persistableUpload = upload.pause();
    // 複雑な一時停止と継続の方法：
    // PersistableUploadインスタンスもserializeによってシリアル化後に保存し、その後さらにdeserializeによって逆シリアル化することでアップロードを再開することができます
    // persistableUpload.serialize(out);
    // アップロードの継続
    upload = transferManager.resumeUpload(persistableUpload);
    // 発生する可能性があるエラーを捕捉します
    UploadResult uploadResult = upload.waitForUploadResult();

    // または直接今回のアップロードを取り消します
    // upload.abort();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでTransferManagerインスタンスを使用しないと確定してから、これを閉じます
// コードの詳細はこちらをご覧ください：高度なインターフェース -> サンプルコード：TransferManagerを閉じる
shutdownTransferManager(transferManager);
```

#### パラメータの説明

| パラメータ名         | 説明         | タイプ             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードリクエスト | PutObjectRequest |

Request メンバー説明：

| Request メンバー | 設定方法              | 説明                                                         | タイプ           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | コンストラクタまたはset方法 | バケットの命名形式はBucketName-APPIDです。詳細は[命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String         |
| key          | コンストラクタまたはset方法 | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` で、オブジェクトキーがdoc/picture.jpgの場合は、 [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String         |
| file         | コンストラクタまたはset方法 | ローカルファイル                                                     | File           |
| input        | コンストラクタまたはset方法 | 入力ストリーム                                                       | InputStream    |
| metadata     | コンストラクタ又はset方法 | ファイルのメタデータ                                                 | ObjectMetadata |
|trafficLimit | set 方法| オブジェクトのアップロードにトラフィック制御を行うために使用します。単位：bit/s、デフォルトではトラフィックの制御は行いません | Int|いいえ|

#### 戻り値

- 成功：Uploadが返され、アップロードが終了したかどうかを確認でき、同期してアップロードが終了するのを待つことができます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

UploadのwaitForUploadResult()メソッドを呼び出すことによって取得したオブジェクトのアップロード情報はクラスUploadResult内に記録されます。クラスUploadResult の主要メンバー説明は次のとおりです。

| メンバー名   | 説明                                                         | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名形式はBucketName-APPIDです。詳細は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください| String |
| key        | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br/>例えば、オブジェクトのアクセスドメイン名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` では、オブジェクトキーはdoc/picture.jpgです。詳細については [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String  |
| requestId  | リクエスト ID                                                       | String |
| dateStr    | 現在のサーバー側の時間                                               | String |
| versionId  | 当バケットのバージョン管理機能が有効な場合は、オブジェクトのバージョン番号IDを返します                      | String |
| crc64Ecma  | サーバーがオブジェクトの内容に基づいて計算したCRC64                           | String |

### ローカルディレクトリのアップロード

TransferManagerインスタンスローカルのディレクトリからファイルを読み取ってCOSにアップロードする機能をパッケージ化します。この機能はディレクトリ構造を破壊せずに、ファイルをアップロードできます。同時に、ディレクトリ下のファイルを別のディレクトリにアップロードするように指定することもできます。

>? 再帰的なディレクトリのアップロードをサポートしていますが、アップロードするディレクトリが大きすぎる場合、アップロードが遅くなるまたは輻輳が長くなる可能性があります。再帰的なディレクトリのアップロードが必要な場合は、小容量のディレクトリをアップロードすることをお勧めします（例：1024個以上のファイルがある）。大容量のディレクトリをアップロードする必要がある場合は、複数の小さなディレクトリに分割して段階的に呼び出すことをお勧めします。
>

#### 方法原型

```java
public MultipleFileUpload uploadDirectory(String bucketName, String virtualDirectoryKeyPrefix,
            File directory, boolean includeSubdirectories);
```

#### リクエスト例

```java
// 高度なインターフェースを使用するにはまずこのプロセスにTransferManagerインスタンスが存在することを確認する必要があります。ない場合は作成してください
// コードの詳細はこちらをご覧ください：高度なインターフェース -> サンプルコード：TransferManagerの作成
TransferManager transferManager = createTransferManager();
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";

// ファイルをbucketにアップロードした後のプレフィックスディレクトリを設定します。“”と設定すると、bucketのルートディレクトリにアップロードすることを表します
String cos_path = "/prefix";
// アップロードしようとするフォルダの絶対パスです
String dir_path = "/path/to/localdir";
// ディレクトリ下のサブディレクトリを再帰的にアップロードするかどうかを表します。trueの場合、サブディレクトリ下のファイルもアップロードされ、cosにディレクトリ構造が保持されます
Boolean recursive = false;

try {
    // 非同期結果Uploadを返し、waitForUploadResultを同期的に呼び出してuploadの終了を待ち、成功するとUploadResultが返され、失敗するとエラーがスローされます.
    MultipleFileUpload upload = transferManager.uploadDirectory(bucketName, cos_path, new File(dir_path), recursive);

    // アップロードの進捗を確認することが選択できます。この関数については、高度なインターフェース -> アップロードファイル -> アップロードの進捗の表示をご参照ください
    showTransferProgress(upload);

    // またはブロックして完了を待つ
    upload.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでTransferManagerインスタンスを使用しないと確定してから、これを閉じます
// コードの詳細はこちらをご覧ください：高度なインターフェース -> サンプルコード：TransferManagerを閉じる
shutdownTransferManager(transferManager);
```

#### パラメータの説明

| パラメータ名                   | 説明                  | タイプ             |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | cos上のbucket       | GetObjectRequest |
| virtualDirectoryKeyPrefix | cos上のobjectのプレフィックス   | String           |
| directory                 | アップロードしようとするフォルダの絶対パス  | File             |
| includeSubDirectory       | アップロードサブディレクトリを再帰的にアップロードするかどうか       | Boolean          |

#### 戻り値

- 成功：MultipleFileUploadを返しアップロードが終了したかどうかを確認することができます。同期してアップロードが終了するのを待つこともできます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

## 簡単な操作

簡単な操作はCOSClientタイプによってリクエストを送信します。簡単な操作を使用する前に必ずCOSClientインスタンスを作成する必要があります。

COSClientインスタンスは同時に実行できて安全です。ここでは1つのプロセスに1つのCOSClientインスタンスだけを作成し、このインスタンスがリクエストを送信しなくなった場合は、このインスタンスのシャットダウンを選択することをお勧めします。

### COSClientの作成

COSのインターフェースを呼び出す前に、まず COSClientのインスタンスを作成する必要があります。

```java
// COSClientインスタンスを作成し、このインスタンスはその後リクエストの呼び出しに使用されます
COSClient createCOSClient() {
    // ユーザーのID情報を設定します。
    // SECRETIDおよびSECRETKEYについてはCAMコンソールhttps://console.cloud.tencent.com/cam/capiにログインし、確認および管理を行ってください
    String secretId = "SECRETID";
    String secretKey = "SECRETKEY";
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // ClientConfigにはその後COSをリクエストするクライアント設定が含まれています：
    ClientConfig clientConfig = new ClientConfig();

    // bucketのリージョンの設定
    // COS_REGIONは https://cloud.tencent.com/document/product/436/6224をご参照ください
    clientConfig.setRegion(new Region("COS_REGION"));

    // リクエストプロトコル、httpまたはhttpsの設定
    // 5.6.53およびそれ以前のバージョンは、httpsプロトコルを使用する設定をお勧めします
    // 5.6.54およびそれ以降のバージョンです。デフォルトはhttpsを使用します
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // オプションで、以下の設定が可能です。

    // socketの読み取りタイムアウトを設定します。デフォルトは30sです
    clientConfig.setSocketTimeout(30*1000);
    // 接続確立のタイムアウトを設定します。デフォルトは30sです
    clientConfig.setConnectionTimeout(30*1000);

    // 必要であれば、httpプロキシ、ip およびportを設定します
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // cosクライアントを生成します。
    return new COSClient(cred, clientConfig);
}
```

### 一時キーを使用したCOSClientの作成

一時キーを使用してCOSをリクエストする場合は、一時キーを使用してCOSClientを作成する必要があります。
このSDKは一時キーを生成できません。追加の操作を使用して生成する必要があります。 [一時キーの生成](https://intl.cloud.tencent.com/document/product/436/14048)をご参照ください。

```java

// COSClientインスタンスを作成し、このインスタンスはその後リクエストの呼び出しに使用されます
COSClient createCOSClient() {
    // ここではすでに一時キーを取得したという結果が必要です。
    // 一時キーの生成は https://intl.cloud.tencent.com/document/product/436/14048をご参照ください
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // ClientConfigにはその後COSをリクエストするクライアント設定が含まれています：
    ClientConfig clientConfig = new ClientConfig();

    // bucketのリージョンの設定
    // COS_REGIONは https://cloud.tencent.com/document/product/436/6224をご参照ください
    clientConfig.setRegion(new Region("COS_REGION"));

    // リクエストプロトコル、httpまたはhttpsの設定
    // 5.6.53およびそれ以前のバージョンは、httpsプロトコルを使用する設定をお勧めします
    // 5.6.54およびそれ以降のバージョンです。デフォルトはhttpsを使用します
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // オプションで、以下の設定が可能です。

    // socketの読み取りタイムアウトを設定します。デフォルトは30sです
    clientConfig.setSocketTimeout(30*1000);
    // 接続確立のタイムアウトを設定します。デフォルトは30sです
    clientConfig.setConnectionTimeout(30*1000);

    // 必要であれば、httpプロキシ、ip およびportを設定します
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // cosクライアントを生成します。
    return new COSClient(cred, clientConfig);
}
```

### ローカルファイルのアップロード

アップロードするソースはローカルのファイルです。

#### 方法原型

```java
// 方法1  ローカルファイルをCOSにアップロードする
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 方法2  入力ストリームをCOSにアップロードする
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// 方法3  以上の2つの方法のパッケージは、例えばcontent-type、 content-dispositionなどのより粒度の細かいパラメータ制御をサポートしています
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// ローカルファイルパス
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでCOSClientインスタンスを使用しないことを確認した後、これを閉じます
cosClient.shutdown();
```

#### パラメータの説明

| パラメータ名         | 説明         | タイプ             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードリクエスト | PutObjectRequest |

Request メンバー説明：

| Request メンバー | 設定方法&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   | 説明                                                         | タイプ   | 入力必須 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | コンストラクタまたはset方法 | Bucket の命名形式がBucketName-APPIDの場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String          | はい|
| key          | コンストラクタまたはset方法 | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br>例えば、オブジェクトのアクセスドメイン名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`で、オブジェクトキーがdoc/picture.jpgの場合は、 [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324) をご参照ください | String         | はい|
| file         | コンストラクタまたはset方法 | ローカルファイル                                                     | File           |いいえ|
| input        | コンストラクタまたはset方法 | 入力ストリーム                                                       | InputStream    | いいえ|
| metadata     | コンストラクタまたはset方法 | オブジェクトのメタデータ                                                 | ObjectMetadata | いいえ|
|trafficLimit | set 方法| オブジェクトのアップロードにトラフィック制御を行うために使用します。単位：bit/s、デフォルトではトラフィックの制御は行いません | Int|いいえ|

ObjectMetadataクラスはオブジェクトのメタ情報を記録するために使用されます。その主なメンバー説明は次のとおりです。

| メンバー名        | 説明                                                | タイプ                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | キャッシュのタイムアウト時間は、 HTTPレスポンスヘッダー内のExpiresフィールドの値です | Date                |
| ongoingRestore  | アーカイブストレージタイプからこのオブジェクトを復元中                        | Boolean             |
| userMetadata    | プレフィックスがx-cos-meta-のユーザーカスタムメタ情報               | Map&lt;String, String&gt; |
| metadata        | ユーザーカスタムメタ情報以外のその他ヘッダー                    | Map&lt;String, String&gt; |
| restoreExpirationTime  | アーカイブオブジェクトのコピーを復元する有効期限  | Date |

#### 結果説明を返す

- 成功：PutObjectResultには、ファイルのeTagなどの情報が含まれます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

PutObjectResultクラスは結果情報を返すために使用されます。その主なメンバー説明は次のとおりです。

| メンバー名        | 説明                                                | タイプ                |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | リクエストID | String                |
| dateStr  | 現在のサーバー側の時間                        | String             |
| versionId    | バージョン管理のバケットが有効な場合は、オブジェクトのバージョン番号IDを返します              | String |
| eTag        | シンプルアップロードインターフェースはオブジェクトのMD5 値を返します。例：09cba091df696af91549de27b8e7d0f6、**注意：リクエストレスポンスヘッダー領域のETagの値には二重引用符がありますが、ここで解析した文字列のeTag値には二重引用はありません** | String |
|crc64Ecma| サーバーがオブジェクトの内容に基づいて計算した CRC64| String |

### アップロードストリームのタイプ

アップロードのソースはInputStreamタイプ（およびそのサブタイプ）のストリームインスタンスです。

#### 方法原型

```java
// 方法1  ローカルファイルをCOSにアップロードする
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 方法2  入力ストリームをCOSにアップロードする
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// 方法3  以上の2つの方法のパッケージは、例えばcontent-type、 content-dispositionなどのより粒度の細かいパラメータ制御をサポートしています
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";

// ここではByteArrayInputStreamを作成することを例としていますが、実際にはここではアップロードしようとする InputStreamタイプのストリームである必要があります
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// アップロードのストリームの正確なストリーム長が取得できる場合は、必ずcontent-lengthを入力することをお勧めします
// 確実に取得することができない場合は、以下の行を省略することができますが、同時に高度なインターフェースもマルチパートアップロードを使用することはできません
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでCOSClientインスタンスを使用しないことを確認した後、これを閉じます
cosClient.shutdown();
```

#### パラメータの説明

| パラメータ名         | 説明         | タイプ             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードリクエスト | PutObjectRequest |

Request メンバー説明：

| Request メンバー | 設定方法&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   | 説明                                                         | タイプ   | 入力必須 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | コンストラクタまたはset方法 | Bucket の命名形式がBucketName-APPIDの場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String          | はい|
| key          | コンストラクタまたはset方法 | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br>例えば、オブジェクトのアクセスドメイン名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`で、オブジェクトキーがdoc/picture.jpgの場合は、 [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324) をご参照ください | String         | はい|
| file         | コンストラクタまたはset方法 | ローカルファイル                                                     | File           |いいえ|
| input        | コンストラクタまたはset方法 | 入力ストリーム                                                       | InputStream    | いいえ|
| metadata     | コンストラクタまたはset方法 | オブジェクトのメタデータ                                                 | ObjectMetadata | いいえ|
|trafficLimit | set 方法| オブジェクトのアップロードにトラフィック制御を行うために使用します。単位：bit/s、デフォルトではトラフィックの制御は行いません | Int|いいえ|

ObjectMetadataクラスはオブジェクトのメタ情報を記録するために使用されます。その主なメンバー説明は次のとおりです。

| メンバー名        | 説明                                                | タイプ                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | キャッシュのタイムアウト時間は、 HTTPレスポンスヘッダー内のExpiresフィールドの値です | Date                |
| ongoingRestore  | アーカイブストレージタイプからこのオブジェクトを復元中                        | Boolean             |
| userMetadata    | プレフィックスがx-cos-meta-のユーザーカスタムメタ情報               | Map&lt;String, String&gt; |
| metadata        | ユーザーカスタムメタ情報以外のその他ヘッダー                    | Map&lt;String, String&gt; |
| restoreExpirationTime  | アーカイブオブジェクトのコピーを復元する有効期限  | Date |

#### 結果説明を返す

- 成功：PutObjectResultには、ファイルのeTagなどの情報が含まれます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

PutObjectResultクラスは結果情報を返すために使用されます。その主なメンバー説明は次のとおりです。

| メンバー名        | 説明                                                | タイプ                |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | リクエストID | String                |
| dateStr  | 現在のサーバー側の時間                        | String             |
| versionId    | バージョン管理のバケットが有効な場合は、オブジェクトのバージョン番号IDを返します              | String |
| eTag        | シンプルアップロードインターフェースはオブジェクトのMD5 値を返します。例：09cba091df696af91549de27b8e7d0f6、**注意：リクエストレスポンスヘッダー領域のETagの値には二重引用符がありますが、ここで解析した文字列のeTag値には二重引用はありません** | String |
|crc64Ecma| サーバーがオブジェクトの内容に基づいて計算した CRC64| String |

### ディレクトリの作成

COS自身にはディレクトリの概念はありませんが、'/' で分割されたオブジェクトのパスを仮想フォルダとみなすことができます。

>?
> - ディレクトリが必要な場合は、直接必要なディレクトリにファイルをアップロードすれば、ディレクトリは自動的に作成されます。例：/dir/example.txtのようなファイルをアップロードすると、/dirのディレクトリが自動生成されます。このような状況については本ページのローカルファイルのアップロードをご参照ください。
> 

下にファイルがないディレクトリが必要な場合は、次の方法を使用します：空のストリームを '/' が末尾のパスにアップロードします。このようにして仮想のディレクトリを作成します。

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// ここで作成するディレクトリのパスを指定します
String key = "/example/dir/";

// ここでは空のByteArrayInputStreamを作成することを例とします
byte data[] = new byte[0];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// このプロセスでCOSClientインスタンスを使用しないことを確認した後、これを閉じます
cosClient.shutdown();
```

### 追加オブジェクトのアップロード

段階的に追加する方式によるオブジェクトのアップロード。

#### 方法原型

```java
public AppendObjectResult appendObject(AppendObjectRequest appendObjectRequest)
        throws CosServiceException, CosClientException
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();

// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";

// ここでは追加アップロードするのはこの2つのファイル内の内容であると仮定します
File part1File = new File("/path/to/part1File");
File part2File = new File("/path/to/part2File");

try {
    AppendObjectRequest appendObjectRequest = new AppendObjectRequest(bucketName, key, part1File);
    appendObjectRequest.setPosition(0L);
    AppendObjectResult appendObjectResult = cosClient.appendObject(appendObjectRequest);
    long nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);

    appendObjectRequest = new AppendObjectRequest(bucketName, key, part2File);
    appendObjectRequest.setPosition(nextAppendPosition);
    appendObjectResult = cosClient.appendObject(appendObjectRequest);
    nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// クライアントを閉じる
cosClient.shutdown();
```

#### パラメータの説明

| パラメータ名         | 説明         | タイプ             |
| -------------------- | ------------ | ---------------- |
| appendObjectRequest | ファイルのアップロードリクエストの追加 | AppendObjectRequest |

AppendObjectRequest メンバー説明：

| Request メンバー | 設定方法   | 説明                                                         | タイプ   | 入力必須かどうか |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | コンストラクタまたはset方法 | Bucket の命名形式がBucketName-APPIDの場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String          | はい|
| key          | コンストラクタまたはset方法 | オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。<br>例えば、オブジェクトのアクセスドメイン名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`で、オブジェクトキーがdoc/picture.jpgの場合は、 [オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324) をご参照ください | String         | はい|
| localfile    | コンストラクタまたはset方法 | ローカルファイル                                                     | File           |いいえ|
| input        | コンストラクタまたはset方法 | 入力ストリーム                                                       | InputStream    | いいえ|
| metadata     | コンストラクタまたはset方法 | オブジェクトのメタデータ                                                 | ObjectMetadata | いいえ|
|trafficLimit | set 方法| オブジェクトのアップロードにトラフィック制御を行うために使用します。単位：bit/s、デフォルトではトラフィックの制御は行いません | Int|いいえ|
| position | set 方法| 追加操作の開始位置です。単位：byte | Long | はい |

#### 結果説明を返す

- 成功：AppendObjectResult。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

AppendObjectResultクラスは結果情報を返すために使用されます。その主なメンバー説明は次のとおりです。

| メンバー名        | 説明                                                | タイプ                |
| --------------- | --------------------------------------------------- | ------------------- |
| metadata | リターンヘッダー | ObjectMetadata               |
| nextAppendPosition| 次に追加する位置 | Long |

### オブジェクトのフォームアップロード

フォームリクエストを使用したオブジェクトのアップロードです。

#### フォームアップロードを構成するform body

フォームパラメータに基づいて、アップロードの最初の form body部分を構築します

```java
String buildPostObjectBody(String boundary, Map<String, String> formFields, String filename, String contentType) {
    StringBuffer stringBuffer = new StringBuffer();
    for(Map.Entry entry: formFields.entrySet()) {
        // boundary行を追加します。行頭は--で始まります
        stringBuffer.append("--").append(boundary).append("\r\n");
        // フィールド名
        stringBuffer.append("Content-Disposition: form-data; name=\""
                + entry.getKey() + "\"\r\n\r\n");
        // フィールド値
        stringBuffer.append(entry.getValue() + "\r\n");
    }
    // boundary行を追加します。行頭は--で始まります
    stringBuffer.append("--").append(boundary).append("\r\n");
    // ファイル名
    stringBuffer.append("Content-Disposition: form-data; name=\"file\"; "
            + "filename=\"" + filename + "\"\r\n");
    // ファイルタイプ
    stringBuffer.append("Content-Type: " + contentType + "\r\n\r\n");
    return stringBuffer.toString();
}
```

#### ローカルファイルのアップロード

```java
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// COS_REGIONは https://cloud.tencent.com/document/product/436/6224をご参照ください
String endpoint = "cos.{COS_REGION}.myqcloud.com";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// SECRETIDおよびSECRETKEYについてはCAMコンソールにログインして確認および管理を行ってください
String secretId = "AKIDXXXXXXXX";
String seretKey = "1A2Z3YYYYYYYYYY";

String localFilePath = "/path/to/localFile";
String contentType = "image/jpeg";

long startTimestamp = System.currentTimeMillis() / 1000;
long endTimestamp = startTimestamp +  30 * 60;
String endTimestampStr = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'").format(endTimestamp * 1000);

String keyTime = startTimestamp + ";" + endTimestamp;
String boundary = "----WebKitFormBoundaryZBPbaoYE2gqeB21N";

// フォームのbodyフィールド値を設定します
Map<String, String> formFields = new HashMap<>();
formFields.put("q-sign-algorithm", "sha1");
formFields.put("key", key);
formFields.put("q-ak", secretId);
formFields.put("q-key-time", keyTime);

// policyの構築は，次のドキュメントをご参照ください: https://intl.cloud.tencent.com/document/product/436/14690
String policy = "{\n" +
        "    \"expiration\": \"" + endTimestampStr + "\",\n" +
        "    \"conditions\": [\n" +
        "        { \"bucket\": \"" + bucketName + "\" },\n" +
        "        { \"q-sign-algorithm\": \"sha1\" },\n" +
        "        { \"q-ak\": \"" + secretId + "\" },\n" +
        "        { \"q-sign-time\":\"" + keyTime + "\" }\n" +
        "    ]\n" +
        "}";

// policyはbase64の後にフォームに入れる必要があります
String encodedPolicy = new String(Base64.encodeBase64(policy.getBytes()));
// policyを設定します
formFields.put("policy", encodedPolicy);
// エンコード後のpolicyおよびsecretKeyに基づいて署名を計算します
COSSigner cosSigner = new COSSigner();
String signature = cosSigner.buildPostObjectSignature(seretKey,
        keyTime, policy);
// 署名を設定します
formFields.put("q-signature", signature);

// 以上のフォームパラメータに基づいて、最初のbody部分を構築します
String formBody = buildPostObjectBody(boundary, formFields,
        localFilePath, contentType);

HttpURLConnection conn = null;
try {
    String urlStr = "http://" + bucketName + "." + endpoint;
    URL url = new URL(urlStr);
    conn = (HttpURLConnection) url.openConnection();
    conn.setRequestMethod("POST");
    conn.setRequestProperty("User-Agent", VersionInfoUtils.getUserAgent());
    conn.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
    conn.setDoOutput(true);
    conn.setDoInput(true);

    OutputStream out = new DataOutputStream(conn.getOutputStream());
    // フォームを書き込む最初の部分
    out.write(formBody.getBytes());

    // ファイル内容を出力ストリーム内に書き込みます
    File file = new File(localFilePath);
    DataInputStream in = new DataInputStream(new FileInputStream(file));
    int readBytes;
    byte[] bytes = new byte[4096];
    while ((readBytes = in.read(bytes)) != -1) {
        out.write(bytes, 0, readBytes);
    }
    in.close();

    // 最後の区切り符号を追加します。行頭と行末はいずれも--です
    byte[] endData = ("\r\n--" + boundary + "--\r\n").getBytes();
    out.write(endData);
    out.flush();
    out.close();

    // レスポンスヘッダー部を読み取ります
    for (Map.Entry<String, List<String>> entries : conn.getHeaderFields().entrySet()) {
        String values = "";
        for (String value : entries.getValue()) {
            values += value + ",";
        }
        if(entries.getKey() == null) {
            System.out.println("reponse line:" +  values );
        } else {
            System.out.println(entries.getKey() + ":" +  values );
        }
    }
} catch (Exception e) {
    e.printStackTrace();
    throw e;
} finally {
    if (conn != null) {
        conn.disconnect();
    }
}
```

## マルチパート操作

マルチパート操作は大きなファイルのアップロード時に、一連のブロックを使用するため、大きなファイルのアップロードの所要時間が長くなり、さまざまな中断を引き起こす可能性があるという問題を改善しました。

>? アップロードしようとするファイルまたはストリームを完全に取得できる場合は、高度なインターフェースを使用することをお勧めします。
>

### 操作フロー

#### マルチパートアップロードのフロー

1. マルチパートアップロードを初期化し（Initiate Multipart Upload）し、UploadIdを取得します
2. UploadId アップロードパート（Upload Part）を使用します
3. マルチパートアップロード（Complete Multipart Upload）が完了しました

#### 段階的にアップロードを継続するプロセス

1. UploadIdが記録されていない場合は、まずマルチパートアップロードタスク（List Multipart Uploads）を照会し、対応するファイルのUploadIdを取得する必要があります
2. UploadIdを使用してアップロード済みのブロックを一覧表示します（List Parts）
3. UploadIdを使用してアップロード残りのブロックをアップロードします（Upload Part）
4. マルチパートアップロードを完了します（Complete Multipart Upload）

#### マルチパートアップロードを終了するプロセス

1. UploadIdが記録されていない場合は、マルチパートアップロードタスク（List Multipart Uploads）を照会し、対応するファイルのUploadIdを取得する必要があります
2. マルチパートアップロード操作を終了し、アップロード済みのブロックを削除します（Abort Multipart Upload）

### マルチパートアップロードの初期化

マルチパートアップロード操作を初期化し、対応するuploadIdを取得してその後の操作に使用します。

#### 方法原型

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";

InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);

// マルチパートアップロードのプロセスでは、ブロックの初期化のみによってファイルアップロード後のmetadataを指定することができます
// 必要なヘッダーはここで指定できます
ObjectMetadata objectMetadata = new ObjectMetadata();
request.setObjectMetadata(objectMetadata);

try {
    InitiateMultipartUploadResult initResult = cosClient.initiateMultipartUpload(request);
    // uploadidを取得します
    String uploadId = initResult.getUploadId();
    System.out.println(uploadId);
} catch (CosServiceException e) {
    throw e;
} catch (CosClientException e) {
    throw e;
}
```

#### パラメータの説明

| パラメータ名                       | 説明 | タイプ                           |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | リクエスト | InitiateMultipartUploadRequest |

Request メンバー説明：

| パラメータ名   | 設定方法            | 説明                                                         | タイプ   |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | コンストラクタまたはset方法 | Bucket の命名形式がBucketName-APPID の場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String |
| key        | コンストラクタまたはset方法 |COSにマルチパートアップロードパス、 [オブジェクトキー]を指定します(https://intl.cloud.tencent.com/document/product/436/13324)。例えばオブジェクトキーはfolder/picture.jpgです  | String |

#### 結果説明を返す

- 成功：InitiateMultipartUploadResultを返します。今回のマルチパートアップロードを示すuploadIdが含まれます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

### マルチパートアップロードタスクの照会

マルチパートアップロードタスク（List Multipart Uploads）を照会し、現在実行中のすべてのアップロードタスクを取得し、その中から処理する必要があるuploadIdを探します。

#### 方法原型

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";

// 照会する必要があるマルチパートアップロードタスクに対応するkey
String targetKey = "targetKey";

ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
// 1回のリクエストで最大いくつ一覧表示するか
listMultipartUploadsRequest.setMaxUploads(100);
// 照会する必要があるマルチパートアップロードタスクの目標プレフィックスを設定し、直接照会する必要があるkeyを設定します
listMultipartUploadsRequest.setPrefix("targetKey");

MultipartUploadListing multipartUploadListing = null;

boolean found = false;

do {
    multipartUploadListing = cosClient.listMultipartUploads(listMultipartUploadsRequest);
    List<MultipartUpload> multipartUploads = multipartUploadListing.getMultipartUploads();

    for (MultipartUpload mUpload : multipartUploads) {
        if (mUpload.getKey().equals(targetKey)) {
            System.out.println(mUpload.getUploadId());
            found = true;
            break;
        }
    }

    if (found) {
        break;
    }

} while (multipartUploadListing.isTruncated());

if (!found) {
    System.out.printf("do not found upload task with key: %s\n", targetKey);
}
```

#### パラメータの説明

| パラメータ名                    | 説明 | タイプ                        |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | リクエスト | ListMultipartUploadsRequest |

Request メンバー説明：

| パラメータ名       | 説明                                                         | タイプ   |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName     | Bucket の命名形式がBucketName-APPIDの場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String |
| keyMarker      | エントリーの一覧表示をこのKey値から開始                                      | String |
| delimiter      | デリミタは符号で、Prefixがある場合、Prefixからdelimiterまでの間の同じパスをグループ化し、Common Prefixとして定義します。次に全てのCommon Prefixを一覧表示します。Prefixがない場合、パスの起点から開始します | String |
| prefix         | 返されるObject keyは必ずPrefixをプレフィックスとして限定します。prefix照会を使用する際には、返されるkeyにPrefixが含まれることに注意して使用してください | String |
| uploadIdMarker | エントリーの一覧表示をこのUploadId値から開始します                                 | String |
| maxUploads     | 返される最大のmultipart数を設定します。有効値は1から1000です                 | String |
| encodingType   | 規定の戻り値のコーデック。選択可能な値：url                            | String |

#### 結果説明を返す

- 成功：MultipartUploadListingを返し、マルチパートアップロード中の情報が含まれます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

### アップロードパート

オブジェクトのアップロードパート（Upload Part）。

#### 方法原型

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// uploadIdは1回のマルチパートアップロードタスクの一意のIDです。マルチパートアップロードの初期化またはマルチパートアップロードタスクの照会によって取得します
String uploadId = "exampleuploadid";

// 各マルチパートアップロードの後に戻り値etagが取得できます。保存して最後にブロックをマージする時に使用します
List<PartETag> partETags = new LinkedList<>();

// アップロードデータ、 ここで10個1Mのブロックデータをアップロードします
for (int i = 1; i <= 10; i++) {
    byte data[] = new byte[1024 * 1024];
    // ここではByteArrayInputStreamを作成することを例としていますが、実際にはここではアップロードしようとする InputStreamタイプのストリームである必要があります
    long inputStreamLength = 1024 * 1024;
    byte data[] = new byte[inputStreamLength];
    InputStream inputStream = new ByteArrayInputStream(data);

    UploadPartRequest uploadPartRequest = new UploadPartRequest();
    uploadPartRequest.setBucketName(bucketName);
    uploadPartRequest.setKey(key);
    uploadPartRequest.setUploadId(uploadId);
    uploadPartRequest.setInputStream(inputStream(data));
    // ブロックの長さを設定する
    uploadPartRequest.setPartSize(data.length);
    // アップロードしようとするブロック番号を設定します。1から始まります
    uploadPartRequest.setPartNumber(i);

    try {
        UploadPartResult uploadPartResult = cosClient.uploadPart(uploadPartRequest);
        PartETag partETag = uploadPartResult.getPartETag();
        partETags.add(partETag);
    } catch (CosServiceException e) {
        throw e;
    } catch (CosClientException e) {
        throw e;
    }
}

System.out.println(partETags);
```

#### パラメータの説明

| パラメータ名          | 説明 | タイプ              |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | リクエスト | UploadPartRequest |

Request メンバー説明：

| パラメータ名    | 設定方法 | 説明                                                         | タイプ        |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | set 方法  | Bucket の命名形式は BucketName-APPIDです。 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String      |
| key         | set 方法  | COSにマルチパートアップロードパス、 [オブジェクトキー]を指定します(https://intl.cloud.tencent.com/document/product/436/13324)。例えばオブジェクトキーは folder/picture.jpgです | String      |
| uploadId    | set 方法  | 指定されたマルチパートアップロードのuploadIdを識別します                                  | String      |
| partNumber  | set 方法  | 指定ブロックの番号を識別します。必ず >= 1です                                | int         |
| inputStream | set 方法  | マルチパートアップロードされる入力ストリーム                                           | InputStream |
|trafficLimit| set 方法| アップロードパートにトラフィック制御を行うために使用します，単位：bit/s、デフォルトではトラフィックの制御は行いません  | Int|

#### 結果説明を返す

- 成功：UploadPartResultを返します。アップロードパートのeTag情報が含まれています。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

#### リターンパラメータ説明

UploadPartResultクラスは結果情報を返すために使用されます。その主なメンバー説明は次のとおりです。

| メンバー名        | 説明                                                | タイプ                |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | 指定ブロックの番号を識別します | String                |
| eTag        | アップロードパートのMD5値を返します                   | String |
|crc64Ecma| サーバーがマルチパートの内容に基づいて計算したCRC64| String |

### アップロード済みのブロックを照会する

特定のマルチパートアップロード操作でアップロードされたブロック（List Parts）を照会します。

#### 方法原型

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// uploadIdは1回のマルチパートアップロードタスクの一意のIDです。マルチパートアップロードの初期化またはマルチパートアップロードタスクの照会によって取得します
String uploadId = "exampleuploadid";

// アップロード済みのセグメント情報を保存するために使用されます
List<PartETag> partETags = new LinkedList<>();

PartListing partListing = null;
ListPartsRequest listPartsRequest = new ListPartsRequest(bucketName, key, uploadId);
do {
    try {
        partListing = cosClient.listParts(listPartsRequest);
    } catch (CosServiceException e) {
        throw e;
    } catch (CosClientException e) {
        throw e;
    }

    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }

    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());
```

#### パラメータの説明

| パラメータ名         | 設定方法            | 説明                                                         | タイプ   |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName       | コンストラクタまたはset方法 | Bucketの命名形式がBucketName-APPIDの場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String |
| key              | コンストラクタまたはset方法 | オブジェクト名                                                   | String |
| uploadId         | コンストラクタまたはset方法 | 今回照会するマルチパートアップロードのuploadId                               | String |
| maxParts         | set 方法            | 1回に返す最大のエントリー数、デフォルトは1000                             | String |
| partNumberMarker | set 方法            | デフォルトはUTF-8バイナリーでエントリーを順次一覧表示し、すべてのエントリーの一覧表示はmarkerから開始  | String |
| encodingType     | set 方法            | 規定の戻り値のコーデック                                         | String |

#### 結果説明を返す

- 成功：PartListingを返し、各ブロックのETagと番号、および次のlistの起点markerが含まれます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

### マルチパートアップロードの完了

ファイル全体のマルチパートアップロード（Complete Multipart Upload）が完了しました。

>? マルチパートアップロードが完了すると、マルチパートアップロードタスクは削除され、タスクに対応するuploadIdは無効になります。
>

#### 方法原型

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// uploadIdは1回のマルチパートアップロードタスクの一意のIDです。マルチパートアップロードの初期化またはマルチパートアップロードタスクの照会によって取得します
String uploadId = "exampleuploadid";

// アップロード済みのセグメント情報を保存します。実際の状況では、この内容はマルチパートアップロードのインターフェースから取得します
List<PartETag> partETags = new LinkedList<>();

// セグメントアップロードが終了してから、completeを呼び出してセグメントアップロードを完了させます
CompleteMultipartUploadRequest completeMultipartUploadRequest =
        new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
try {
    CompleteMultipartUploadResult completeResult =
            cosClient.completeMultipartUpload(completeMultipartUploadRequest);
    System.out.println(completeResult.getRequestId());
} catch (CosServiceException e) {
    throw e;
} catch (CosClientException e) {
    throw e;
}

// cosClientを使用しない場合は、これを閉じます
cosClient.shutdown();
```

#### パラメータの説明

| パラメータ名   | 設定方法&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 説明                                                         | タイプ              |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | コンストラクタまたはset方法 | Bucketの命名形式がBucketName-APPID の場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String            |
| key        | コンストラクタまたはset方法 | COSのパスへのマルチパートアップロード、すなわち[オブジェクトキー](https://intl.cloud.tencent.com/document/product/436/13324)を指定します。例えばオブジェクトキーは folder/picture.jpgです | String            |
| uploadId   | コンストラクタまたはset方法 | 指定されたマルチパートアップロードの uploadId を識別します                                  | String            |
| partETags  | コンストラクタまたはset方法 | ブロックの番号およびアップロードで返されたeTagを識別します                            | List&lt;PartETag&gt; |

#### 結果説明を返す

- 成功：CompleteMultipartUploadResultを返し、完了したオブジェクトのeTag情報が含まれます。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、 [トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。

### マルチパートアップロードの終了

マルチパートアップロード操作を終了し、アップロード済みのブロックを削除します（Abort Multipart Upload）。

>? マルチパートアップロードが終了した後、マルチパートアップロードタスクおよびすでにアップロードしたブロックは全て削除され、対応するuploadIdは無効になります。
>

#### 方法原型

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### リクエスト例

```java
// COSインターフェースを呼び出す前にこのプロセスにCOSClientインスタンスが存在することを確認する必要があります。存在しない場合は作成してください
// コードの詳細はこちらをご参照ください：簡単な操作 -> COSClientの作成
COSClient cosClient = createCOSClient();
// バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式でなければなりません
String bucketName = "examplebucket-1250000000";
// オブジェクトキー（Key）はオブジェクトのバケット内での固有識別子です。
String key = "exampleobject";
// uploadIdは1回のマルチパートアップロードタスクの一意のIDです。マルチパートアップロードの初期化またはマルチパートアップロードタスクの照会によって取得します
String uploadId = "exampleuploadid";

AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
try {
    cosClient.abortMultipartUpload(abortMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// cosClientを使用しない場合は、これを閉じます
cosClient.shutdown();
```

#### パラメータの説明

| パラメータ名   | 設定方法            | 説明                                                         | タイプ   |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | コンストラクタまたはset方法 | Bucketの命名形式がBucketName-APPIDの場合は、 [命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください | String |
| key        | コンストラクタまたはset方法 | COSのパスへのマルチパートアップロード、すなわち [オブジェクトキー]です(https://intl.cloud.tencent.com/document/product/436/13324)します。例えばオブジェクトキーはfolder/picture.jpgです | String |
| uploadId   | コンストラクタまたはset方法 | 指定されたマルチパートアップロードのuploadIdを識別します                                  | String |

#### 結果説明を返す

- 成功：戻り値なし。
- 失敗：エラーが発生すると（例えば身分認証の失敗）、CosClientExceptionまたはCosServiceExceptionの異常をスローします。詳細については、[トラブルシューティング](https://intl.cloud.tencent.com/document/product/436/31537)をご参照ください。
