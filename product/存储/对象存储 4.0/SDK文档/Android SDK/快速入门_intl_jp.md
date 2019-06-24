## クイック導入

### 導入準備

1. SDKはAndroid 2.2以上のバージョンの携帯システムをサポートします。
2. 携帯はネットワーク（GPRS、3GまたはWIFIネットワークなど）が必要です。
3. 携帯にはストレージ容量がない場合、一部の機能は正しく機能しません。
4. [COSコンソール](https://console.cloud.tencent.com/cos4/secret)からAPPID、SecretId、SecretKeyを取得します。

>?文章に記載されているSecretId、SecretKey、Bucketなどの名称の意味と取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

### 統合SDK

#### 自動統合（**推薦**）

1、プロジェクトのルートディレクトリにあるbuild.gradleファイルにmavenリポジトリを追加します：

```
allprojects {

    repositories {
        ...
        // 次のmavenリポジトリアドレスを追加します
        maven {
            url "https://dl.bintray.com/tencentqcloudterminal/maven"
        }
    }
}
```

2、アプリケーションのルートディレクトリにあるbuild.gradleに依頼を追加します：
```
dependencies {
	...
    // この行を追加します
    compile 'com.tencent.qcloud:cosxml:5.4.19'
}
```

3、アップロード、ダウンロード、およびコピー機能のみを使用する場合は、簡易SDKを使用して上記のステップ2の依存関係を以下の依存関係に変更できます：

```
dependencies {
	...
    // この行を追加します
    compile 'com.tencent.qcloud:cosxml-lite:5.4.19'
}
```

4、SDKの品質を継続的に追跡して最適化し、より良い使用体験を実現するために、SDKにTencentモバイル分析（mta）を導入しました。この機能をオフにする場合は、アプリケーションのルートディレクトリにあるbuild.gradleに依存関係を追加します：

```
dependencies {
	...
    // この行を追加します
   compile ('com.tencent.qcloud:cosxml:5.4.19'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' //mtaの報告機能をオフにします
    }
}
```

簡易SDKコードは以下のとおりです：
```
dependencies {
	...
    // この行を追加します
    compile ('com.tencent.qcloud:cosxml-lite:5.4.19'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' //mtaの報告機能をオフにします
    }
}
```
#### 手動統合

次のjarパッケージをプロジェクトにインポートしてlibsフォルダに保存する必要があります：

- cos-android-sdk.jar
- qcloud-foundation.jar
- bolts-tasks.jar
- okhttp.jar（3.9以上のバージョン）
- okio.jar（1.13.0以上のバージョン）
- mtaUtils.jar
- mid-sdk.jar
- mta-android-sdk.jar
- logUtils.aar

[COS XML Android SDK-release](https://github.com/tencentyun/qcloud-sdk-android/releases)ですべてのjarパッケージをダウンロードできます。最新のreleaseパッケージのご使用をお勧めします。

### 権限の構成

このSDKを使用するには、ネットワーク、ストレージなどに関連するいくつかのアクセス権限が必要です。AndroidManifest.xmlに次の権限宣言を追加できます（Android 5.0以上では動的な権限を取得する必要があります）：
```html
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

### 他のリソース

**ソースとサンプルプロジェクト**

COS Android SDKに関連するソースについては、 [COS Android SDK Githubアドレス](https://github.com/tencentyun/qcloud-sdk-android)を参照してください。
サンプルdemoについて、[COS Android SDKサンプルプロジェクト](https://github.com/tencentyun/qcloud-sdk-android-samples)を参照してください。

**ログアップデート**

COS Android SDKログアップデートについては、 [COS Android SDK Githubログアップデート](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md)を参照してください。

## クイックスタート

### 初期化 

COSサービスに関連するリクエストを実行する前に、CosXmlServiceオブジェクトをインスタンス化する必要があります。具体的には次の手順とおりです。

#### 構成クラスを初期化します

**CosXmlServiceConfig** はCOSサービスの構成クラスです。以下のコードを使用して初期化できます：

```
String appid = "COSのサービスAPPID";
String region = "バケットが所在する地域"; 

//CosXmlServiceConfigオブジェクトを作成し、必要に応じてデフォルトの構成パラメータを変更します
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .setDebuggable(true)
       .builder();
```

#### 承認クラスを初期化します

端末が永続暗号鍵を介して直接身元認証すると、暗号鍵が漏れる危険性があります。COS端末SDK（Android/IOS）は、一時暗号鍵を使用してリクエストの承認をサポートしているため、一時暗号鍵を返すサービスを構築するだけで、端末のCOSリクエストを承認することができます。この方法を使用することを強くお勧めします。具体的には[モバイルアプリケーション直接送信の実践](https://cloud.tencent.com/document/product/436/9068)を参照してください。

#### 一時暗号鍵による承認（推薦）

- 標準応答ボディ承認

一時暗号鍵サービスを既に構築していて、STS SDKで取得したJSONデータを一時暗号鍵サービスの応答ボディとして直接使用する場合（cossignがこの方法を使用した）、COS SDKの承認クラスを作成するために次のコードを使用できます。
```
/**
 * 承認サービスのurlアドレスを取得します
 */
URL url = null; //アプリケーションサーバー承認サービスのURLアドレス
try {
    url = new URL("your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
}

/**
 * SDKに一時暗号鍵を提供するために{@link QCloudCredentialProvider}オブジェクトを初期化します。
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
                .url(url)
                .method("GET")
                .build());
```
>!標準応答ボディ承認方式で、署名の開始時刻は携帯のローカル時間であるため、携帯のローカル時間ずれが大きい場合（10分以上）、署名エラーが発生する可能性があり、その場合は次のカスタマイズ応答ボディ承認を使用できます。

- カスタマイズ応答ボディ承認

一時暗号鍵サービスのHTTP応答ボディをカスタマイズすること、ユーザー携帯の大きいなローカル時間ずれによる誤った署名を回避するため、端末からサーバーへ返した時間を署名の開始時間として使用すること、または、他のプロトコルを使って端末とサーバーの間で通信することなど、より柔軟性を取りたい場合は、`BasicLifecycleCredentialProvider`クラスを継承してその`fetchNewCredentials()`を実現することができます：

まず、1つの `MyCredentialProvider` クラスを定義します：

```java
public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {
       
        // まず、あなたの一時暗号鍵サーバーから署名情報を含む応答を取得します
        ....
        
        // それから応答を解析して暗号鍵情報を取得します
        String tmpSecretId = ...;
        String tmpSecretKey = ...;
        String sessionToken = ...;
        long expiredTime = ...;
        
        // サーバーへ返した時間は署名の開始時刻とします
        long beginTime = ...;
         
        // todo something you want
         
        // 最後一時暗号鍵情報オブジェクトを返した 
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, beginTime, expiredTime);
    }
}
```

それから`MyCredentialProvider`インスタンスを使って、リクエストを承認します：

```
/**
 *SDKに一時暗号鍵を提供するために{@link QCloudCredentialProvider}オブジェクトを初期化します。
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();
```

#### 永続暗号鍵による承認

一時暗号鍵サービスを構築しない場合は、永続暗号鍵を使用して承認クラスを初期化できます。この方法では暗号鍵が漏れる危険性があるため、**この方法を使用しないことを強くお勧めします**。一時的なテストのために安全な環境でのみ使用することをお勧めします。

```
String secretId = "クラウドAPI暗号鍵SecretId";
String secretKey ="クラウドAPI暗号鍵SecretKey";

/**
 * SDKに一時暗号鍵を提供するために{@link QCloudCredentialProvider}オブジェクトを初期化します。
 */
QCloudCredentialProvider credentialProvider = new ShortTimeCredentialProvider(secretId,
                secretKey, 300);
```


#### COSサービスクラスを初期化します

**CosXmlService** はCOSサービスクラスです。これをさまざまなCOSサービスを操作するために使用することができます。構成クラスと承認クラスをインスタンス化した後、COSサービスクラスを容易にインスタンス化することができます。具体的なコードは以下の通りです。

````java
CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, qCloudCredentialProvider);
````

### ファイルのアップロード

**TransferManager**、**COSXMLUploadTask**は、簡単なアップロード、マルチパートアップロードAPIの非同期リクエストをカプセル化し、アップロードリクエストの一時停止、再開、キャンセル、および継続送信機能をサポートします。この方法でファイルをアップロードすることをお勧めします。サンプルコードは次のとおりです。

```java

//TransferConfigを初期化します
TransferConfig transferConfig = new TransferConfig.Builder().build();
/**
特別な要件がある場合は、次のように初期化をカスタマイズできます。ファイル >= 2Mの場合、マルチパートアップロードを有効にして、且つマルチパートアップロードのパートサイズが1Mになります。ソースファイルが5Mより大きい場合、パートコピーを有効にして、且つパートコピーのサイズが5Mになります。
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) //パートでコピーされたファイルの最小サイズを有効にするかどうか
        .setSliceSizeForCopy(5 * 1024 * 1024) //パートでコピーするときのパートサイズ
        .setDivisionForUpload(2 * 1024 * 1024) //マルチパートアップロードされたファイルの最小サイズを有効にするかどうか
        .setSliceSizeForCopy(1024 * 1024) //マルチパートアップロードするときのパートサイズ
        .build();
*/

//TransferManagerを初期化します
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "バケット名称";
String cosPath = "オブジェクト鍵"; //すなわち、cosPath = "test.txt"のフォーマットでCOSに格納されているファイルの絶対パス；
String srcPath = "ローカルファイルの絶対パス"; //例えば：srcPath=Environment.getExternalStorageDirectory().getPath() + "/test.txt";
String uploadId = null; //マルチパートアップロードを初期化するUploadIdが存在する場合、割り当て値に対応するuploadId値が継続送信に使用され、それ以外の場合、割り当て値はnullです。
//ファイルのアップロード
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
* バイト配列をアップロードする場合は、TransferManagerのupload（string、string、byte []）メソッドを呼び出して実現できます；
* byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
*/

/**
* バイトストリームをアップロードする場合は、TransferManagerのupload（String、String、InputStream）メソッドを呼び出して実現できます；
* InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
*/


//アップロード進捗のコールバックを設定します
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//返し結果のコールバックを設定します
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//タスク状態のコールバックを設定することでタスクプロセスを確認できます。
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
特殊な要件があれば、次の操作ができます：
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); //バケットが所在するキャンパスを設定します
 putObjectRequest.setNeedMD5(true); //Md5検証を起動するかどうか
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

//アップロードをキャンセルします
cosxmlUploadTask.cancel();


//アップロードを中止します
cosxmlUploadTask.pause();

//アップロードを回復します
cosxmlUploadTask.resume();

```
### ファイルのダウンロード
**TransferManager**、**COSXMLDownloadTask** は、ダウンロードAPIの非同期リクエストをカプセル化し、ダウンロードリクエストの一時停止、再開、キャンセル、およびブレークポイントのダウンロード機能をサポートします。この方法でファイルをダウンロードすることをお勧めします。サンプルコードは次のとおりです。
```java
Context applicationContext = "applicationコンテキスト"； // getApplicationContext()
String bucket = "バケット名称"; //ファイルが所在するバケット
String cosPath = "オブジェクト鍵"; //すなわち、cosPath = "test.txt"のフォーマットでファイルをCOSに格納されている絶対パス；
String savedDirPath = "ファイルをローカルフォルダパスにダウンロードします"；
String savedFileName = "ローカルにダウンロードされたファイル名"；//入力しない場合（null）、cosのファイル名と同じです
//ファイルのダウンロード
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savedDirPath, savedFileName);
//ダウンロード進捗コールバックを設定します
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//返し結果のコールバックを設定します
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//タスク状態のコールバックを設定することでタスクプロセスを確認できます。
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
特殊な要件があれば、次の操作ができます：
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
getObjectRequest.setRegion(region); //バケットが所在するキャンパスを設定します
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
*/

//ダウンロードをキャンセルします
cosxmlDownloadTask.cancel();

//ダウンロードを中止します
cosxmlDownloadTask.pause();

//ダウンロードを回復します
cosxmlDownloadTask.resume();

```
### ファイルのコピー
**TransferManager**、**COSXMLCopyTask**は、簡単なコピー、パートコピーAPIの非同期リクエストをカプセル化し、コピーリクエストの一時停止、再開、キャンセルをサポートします。この方法でファイルをコピーすることをお勧めします。サンプルコードは次のとおりです。
```java
String bucket = "バケット名称"; //ターゲットファイルのバケット
String cosPath = "オブジェクト鍵"; //すなわち、cosPath = "test.txt"のフォーマットでターゲットファイルをCOSに格納されている絶対パス；
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(
                "ソースファイルバケットが所在するappid", "ソースファイルバケット", "ソースファイルバケットが所在するキャンパス", "ソースファイルのオブジェクト鍵");//ソースファイルが所在するcosの位置説明
//ファイルのコピー
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath, copySourceStruct);
//返し結果のコールバックを設定します
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//タスク状態のコールバックを設定することでタスクプロセスを確認できます。
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });
/**
特殊な要件があれば、次の操作ができます：
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
copyObjectRequest.setRegion(region); //バケットが所在するキャンパスを設定します
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(copyObjectRequest);
*/

//コピーをキャンセルします
cosxmlCopyTask.cancel();


//コピーを中止します
cosxmlCopyTask.pause();

//コピーを再開します
cosxmlCopyTask.resume();
```

