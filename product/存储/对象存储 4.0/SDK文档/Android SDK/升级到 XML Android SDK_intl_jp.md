JSON Android SDKとXML Android SDKのドキュメントを詳しく比較すると、単なる増分アップデートではないことがわかります。XML Android SDKは、アーキテクチャ、使いやすさ、およびセキュリティが大幅に向上し、かつ使いやすさ、ロバスト性、および伝送パフォーマンスが大幅に改善されました。XML Android SDKにアップグレードする場合は、以下のガイドに従ってSDKのアップグレードを完成してください。

## 機能比較

次の表に、JSON Android SDKとXML Android SDKの主な機能比較を示します：

| 機能       | XML Android SDK         | JSON Android SDK                         |
| -------- | :------------: | :------------------:    |
| ファイルアップロード | ローカルファイル、バイトストリーム、入力ストリームのアップロードをサポートします<br>デフォルトでは、アップロードを上書きします<br>アップロードモードを知的に判断します<br>簡単なアップロードは最大5GBをサポートします<br>マルチパートアップロードは最大48.82TB（50,000GB）をサポートします | ローカルファイルのアップロードのみをサポートします<br>上書きかどうかを選択できます<br>簡単なアップロードかマルチパートアップロードかを手動で選択する必要があります<br>簡単アップロードは最大20MBをサポートします<br>マルチパートアップロードは最大64GBをサポートします |
| ファイルの削除 | 一括削除をサポートします | 単一ファイルの削除のみをサポートします |
| バケット基本操作 | バケットの作成<br>バケットの取得<br>バケットの削除   | サポートしません |
| バケットACL操作 | バケットACLを設定します<br>バケットACLの設定を取得します<br>バケットACLの設定を削除します   | サポートしません |
| バケットライフサイクル | バケットライフサイクルを作成します<br>バケットライフサイクルを取得します<br>バケットライフサイクルを削除します | サポートしません |
| ディレクトリ操作 | APIを独立に提供しません   | ディレクトリを作成します<br>ディレクトリを照合します<br>ディレクトリを削除します |

## アップグレード手順
以下の手順に従ってAndroid SDKをアップグレードしてください。

**1. Android SDKのアップデート**

COS XML Android SDKは[Bintray](https://bintray.com)のmavenパッケージ管理コンソールでリリースされます。自動統合方法を使用してアップデートすることをお勧めします。

プロジェクトのルートディレクトリにあるbuild.gradleファイルにmavenリポジトリを追加します。コードが下記のとおりである。

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

アプリケーションのルートディレクトリにあるbuild.gradleに依頼を追加します。コードが下記のとおりである。

```
dependencies {
	...
    // この行を追加します
    compile 'com.tencent.qcloud:cosxml:5.4.+'
}
```

もちろん、手動jarパッケージ依頼を引き続き選択することができます。[COS XML Android SDK-release](https://github.com/tencentyun/qcloud-sdk-android/releases)ですべてのjarパッケージをダウンロードできます。

**2. SDK認証方式の変更**

JSON Android SDKでは、アプリケーションサーバーで自分で署名を計算し、クライアントに返してそれを使用する必要があります。XML SDKでは、新しい認証アルゴリズムが使用され、XML Android SDKで、アプリケーションサーバーで一時暗号鍵（STS）ソリューションを導入することを強くお勧めします。このソリューションでは、署名計算プロセスを理解する必要はなく、サーバーでCAMを導入し、取得した一時暗号鍵をクライアントに返してSDKに設定するだけで、SDKが暗号鍵を管理して署名を計算します。一時暗号鍵は一定期間後に自動的に無効になり、永続暗号鍵は漏洩されません。
また、異なる粒度でアクセス権限を制御することもできます。具体的な手順について、[モバイルアプリケーション直接送信の実践](https://cloud.tencent.com/document/product/436/9068)および[一時暗号鍵の生成と使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

それでもアプリケーションサーバーを使用して手動で署名を計算してから、クライアントに戻って使用する方式の場合は、署名アルゴリズムが変更されたことに注意してください。署名は単一の署名と複数の署名を区別しなくなりましたが、署名の有効期間の設定によってセキュリティを確保します。署名をアップデートするには、[XMLリクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください。

**3. SDK初期化の変更**

XML Android SDKでは、初期化APIにはいくつかの変更が発生します：

* 区別するために、`CosXmlServiceConfig`は`COSClientConfig`を代わり、`CosXmlService`は`COSClient`を代わりますが、その役割が同じです。
* 1つの有効な暗号鍵を提供するために、初期化するときに、1つの暗号鍵提供者`QCloudCredentialProvider`をインスタンス化する必要があります。一時暗号鍵のご使用をお勧めします。

**JSON SDKの初期化方式は下記のとおりです：**

```
//COSClientConfigオブジェクトを作成し、必要に応じてデフォルトの構成パラメータを変更します
COSClientConfig config = new COSClientConfig();
//キャンパスを設定します
config.setEndPoint(COSEndPoint.COS_GZ);

Context context = getApplicationContext()；
String appid =  "Tencent Cloud登録のappid";
String peristenceId = "IDを持続化します";

//COSlientオブジェクトを作成して、COSの操作を実現します
COSClient cos = new COSClient(context,appid,config,peristenceId);
```

**XML SDKの初期化方式は下記のとおりです：**

```
String appid = "1250000000";
String region = "ap-guangzhou"; 

//CosXmlServiceConfigオブジェクトを作成し、必要に応じてデフォルトの構成パラメータを変更します
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .builder();
       
/**
 * 承認サービスのurlアドレスを取得します
 */
URL url = null; 
try {
    url = new URL("your_auth_server_url"); //アプリケーションサーバー承認サービスのURLアドレス
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
                
                
CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, credentialProvider);
```


**4. バケット名称とAvailability Zoneの略称を変更します**

XML SDKのバケット名称とAvailability Zoneの略称はJSON SDKのものとは異なるため、ユーザーは対応して変更する必要があります。

**バケット**

XML Android SDKバケット名称は2つの部分で構成されています：ユーザー定義の文字列とAPPIDです。両方はハイフン「-」で接続されています。例えば、`examplebucket-1250000000`、その中で、`examplebucket`はユーザーで定義された文字列で、`1250000000`はAPPIDです。

>?APPIDはTencent CloudアカウントのアカウントIDの1つであり、クラウドリソースを関連付けるために使用されます。ユーザーがTencent Cloudアカウントの申し込みに成功すると、システムは自動的にAPPIDをユーザーに割り当てます。[Tencent Cloudコンソール](https://console.cloud.tencent.com/)を通して、【アカウント情報】でAPPIDを確認できます。

バケットを設定するとき、以下のサンプルコードを参照してください：

```
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject.doc";
String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject.doc";
//ファイルのアップロード
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
```

**バケットのAvailability Zoneの略称Region**

XML Android SDKバケットの使用可能な地域の略称が変更されました。次のグラフには、各地域のJSON SDKとXML SDKでの対応関係を示します。

| 地域       | XML Android SDK地域略称         | JSON Android SDK地域略称                         |
| -------- | ------------ | ---------------------------------------- |
| 北京1区（華北） | ap-beijing-1 | tj |
| 北京       | ap-beijing   | bj |
| 上海（華東）   | ap-shanghai  | sh |
| 広州（華南）   | ap-guangzhou | gz |
| 成都（西南）   | ap-chengdu   | cd |
| 重慶       | ap-chongqing | 無し |
| シンガポール      | ap-singapore | sgp |
| 香港       | ap-hongkong  | hk |
| トロント      | na-toronto   | ca |
| フランクフルト     | eu-frankfurt | ger |
| ムンバイ       | ap-mumbai    | 無し |
| ソウル       | ap-seoul     | 無し |
| シリコンバレー       | na-siliconvalley     | 無し |
| バージニア       | na-ashburn     | 無し |
| バンコク       | ap-bangkok     | 無し |
| モスクワ       | eu-moscow     | 無し |

初期化するとき、バケットが所在する地域の略称を`CosXmlServiceConfig`に設定してください：

```
String appid = "1250000000";
String region = "ap-guangzhou"; 

CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .builder();
```

**5. APIの変更**

XML SDKにアップグレードした後、一部操作のAPIが変更されました。実際のニーズに合わせて変更してください。SDKを使いやすくするためにAPIをカプセル化しました。詳細については、例と[APIドキュメント](https://cloud.tencent.com/document/product/436/11238)を参照してください。

API変化は以下の3点があります：

**1）独立のディレクトリAPIがありません**

XML SDKでは、独立のディレクトリAPIを提供しなくなりました。COS自体にはフォルダやディレクトリという概念がなく、COSはオブジェクトproject/a.txtをアップロードする原因で、projectフォルダを作成しません。
ユーザーの使用習慣を満たすために、COSはコンソールやCOS browserなどのグラフィカルツールに「フォルダ」または「ディレクトリ」の表示方式をシミュレートします。具体的については、鍵値がproject/で、中身が空のオブジェクトを作成することで、従来のフォルダをシミュレートする表示方法で実現します。

たえば、アップロードオブジェクトproject/doc/a.txt、区切り記号/は「フォルダ」の表示方式をシミュレートしますので、コンソールに「フォルダ」projectとdocが表示されます。ここで、docはproject下位レベルの「フォルダ」で、a.txtが含まれています。

したがって、適用シナリオが単にファイルをアップロードするだけの場合は、まずフォルダを作成せずに直接アップロードすることができます。

適用シナリオにフォルダの概念があり、フォルダを作成する機能を提供する必要がある場合は、パスが '/'で終わる0KBファイルをアップロードできます。こうすれば、`GetBucket`APIを呼び出すときにこのようなファイルをフォルダとして使うことができます。


**2）TransferManager**

XML SDKにおいて、アップロード、ダウンロードおよびコピー操作をカプセル化し、`TransferManager`と命名します。同時に設計および伝送パフォーマンスAPIのの両方を最適化しますので、直接使用することをお勧めします。`TransferManager`の主な特性は以下のとおりです：

* アップロードおよびダウンロードプロセスの一時停止と回復をサポートします。
* ファイルサイズに応じて簡単なアップロードまたはマルチパートアップロードのインテリジェントな選択をサポートし、該判断限界を設定できます。
* タスクステータスのリスニングをサポートします。

`TransferManager`でアップロードするサンプルコード：

```
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
String cosPath = "オブジェクト鍵"; //すなわち、cosPath = "exampleobject.doc"のフォーマットでCOSに格納されているファイルの絶対パス；
String srcPath = "ローカルファイルの絶対パス"; //例えば：srcPath=Environment.getExternalStorageDirectory().getPath() + "/exampleobject.doc";
String uploadId = "マルチパートアップロードのUploadId";//アップロードの再開に使用されます。マルチパートアップロードがない場合はnullになります。
//ファイルのアップロード
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
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
 putObjectRequest.setSign(600); //署名の有効期間を設定します
 putObjectRequest.setNeedMD5(true); //Md5検証を有効にするかどうか
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

//アップロードをキャンセルします
cosxmlUploadTask.cancel();


//アップロードを中止します
cosxmlUploadTask.pause();

//アップロードを回復します
cosxmlUploadTask.resume();
```

**3）新規追加されたAPI**

XML Android SDK新規追加されたAPI、必要に応じて呼び出すことができます。以下を含みます：

* バケットの操作、例えば、PutBucketRequest、GetBucketRequest、ListBucketRequestなど。
* バケットACLの操作、例えば、PutBucketACLRequest、GetBucketACLRequestなど。
* バケットのライフサイクルの操作、例えば、PutBucketLifecycleRequest、GetBucketLifecycleRequestなど。

具体的には、弊社の[Android SDK APIドキュメント](https://cloud.tencent.com/document/product/436/11238)を参照してください。

