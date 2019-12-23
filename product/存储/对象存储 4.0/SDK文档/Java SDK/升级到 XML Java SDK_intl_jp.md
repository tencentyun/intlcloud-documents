JSON Java SDKとXML Java SDKのドキュメントを詳しく比較すると、単なる増分アップデートではないことがわかります。XML Java SDKは、アーキテクチャ、可用性およびセキュリティが大幅に向上し、かつ使いやすさ、ロバスト性およびパフォーマンスが大幅に改善されました。XML Java SDKにアップグレードする場合、以下のガイドを参照して、Java SDKのアップグレードを完了してください。

## 機能比較

| 機能       | XML Java SDK         | JSON Java SDK                         |
| -------- | :------------: | :------------------:    |
| ファイルのアップロード | ローカルファイル、バイトストリーム、入力ストリームのアップロードをサポートします<br>デフォルトでは、アップロードを上書きします<br>アップロードモードを知的に判断します：簡単なアップロードは最大5GBをサポートします<br>マルチパートアップロードは最大48.82TB（50,000GB）をサポートします| ローカルファイルのアップロードのみをサポートします<br>上書きするかどうかを選択できます<br>簡単なアップロードかシャードアップロードかを手動で選択する必要があります。<br>簡単なアップロードは最大20MBをサポートします<br>シャードアップロードは最大64GBをサポートします|
| ファイルの削除 | 一括削除をサポートします | 単一ファイルの削除のみをサポートします |
| バケット基本操作 | バケットの作成<br>バケットの取得<br>バケットの削除   | サポートしません |
| バケットACL操作 | バケットACLの設定<br>バケットACLの設定を取得します<br>バケットACLの設定を削除します   | サポートしない |
| バケットライフサイクル | バケットライフサイクルを作成します<br>バケットライフサイクルを取得します<br>バケットライフサイクルを削除します | サポートしません |
| ディレクトリ操作 | APIを独立に提供しません   | ディレクトリを作成します<br>ディレクトリを照合します<br>ディレクトリを削除します |

## アップグレード手順
以下の手順に従ってJava SDKをアップグレードしてください。

**1. Java SDKのアップデート**

XML Java SDKは、[maven](https://mvnrepository.com/artifact/com.qcloud/cos_api)セントラルリポジトリで公開され、mavenの依存関係自動管理方式で導入することをお勧めします。

mavenプロジェクトのpom.xmlファイルに以下の依存関係を追加します：

```xml
<!-- https://mvnrepository.com/artifact/com.qcloud/cos_api -->
<dependency>
    <groupId>com.qcloud</groupId>
    <artifactId>cos_api</artifactId>
    <version>5.x.x</version>
</dependency>

```

当然のことながら、[maven](https://mvnrepository.com/artifact/com.qcloud/cos_api)セントラルリポジトリで対応するバージョンのjarパッケージを直接的にダウンロードして、プロジェクトに手動で追加することもできます。


**2. バケット名称と可能な地域の略称の変更

XML Java SDKのバケット名称と可能な地域の略称はJSON Java SDKのものとは異なるため、ユーザーは対応して変更する必要があります。

**バケット**

XML SDKバケット名称は、ユーザーカスタマイズ文字列とAPPIDという2つの部分で構成され、両者はハイフン「-」でつなぎます。
例えば、 `examplebucket-1250000000`、そのうち、 `examplebucket` はユーザーカスタマイズ文字列であり、`1250000000` はAPPIDです。

>？APPIDはTencent Cloudアカウントのアカウントタグの1つであり、クラウドリソースを関連付けるために使用されます。ユーザーがTencentクラウドアカウントの申し込みに成功すると、システムは自動的にAPPIDをユーザーに割り当てます。[Tencent Cloudコンソール](https://console.cloud.tencent.com/)【アカウント情報】でAPPIDを確認できます。

バケットを設定し、以下のサンプルコードを参照してください。

```java
COSCredentials cred = new BasicCOSCredentials("COS_SECRETID", "COS_SECRETKEY");
// 新しい地域名を使用し、利用可能な地域のリストを公式Webサイトのドキュメントから取得でき、また以下のXML SDKとJSON SDKの地域比較表を参照できます。
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
COSClient cosclient = new COSClient(cred, clientConfig);
// バケットの名称はappidを含む必要があります
String bucketName = "examplebucket-1250000000";

// 以下は、このバケットにファイルをアップロードする例です
String key = "docs/exampleobject.doc";
File localFile = new File("src/test/resources/len10M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// ストレージタイプを設定し、デフォルトでは、標準（standard）、低頻度（standard_ia）です。
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
	PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
	// putobjectResultはファイルのetagを返します
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
	e.printStackTrace();
} catch (CosClientException e) {
	e.printStackTrace();
}

// クライアントの閉鎖
cosclient.shutdown();

```

**バケットのAvailability Zoneの略称Region**
XML SDKのバケットの可能な地域の略称が変化し、異なる地域のJSON SDKとXML SDKにおける異なる対応関係については、以下の表を参照してください：

| 地域       | XML SDK地域略称         | JSON SDK地域略称                         |
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

`COSClient`を初期化する時、バケットが位置する地域の略称を`ClientConfig`に設定します：

```java
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
COSClient cosclient = new COSClient(cred, clientConfig);

```

**3. APIの変更
XML SDKにアップグレードした後、一部操作のAPIが変更されました。実際のニーズに合わせて変更してください。同時に、SDKをより使いやすくするためにAPIをカプセル化しました。詳細については、例と[APIドキュメント](https://cloud.tencent.com/document/product/436/12263)を参照してください）。

APIには主に以下の変化があります：

**1）独立のディレクトリAPIがありません**

XML SDKでは、個別のディレクトリAPIは提供されなくなりました。COSにはフォルダとディレクトリの概念はありません。COSでは、オブジェクト`project/a.txt`のアップロードによってprojectフォルダは作成されません。ユーザーの使用習慣を満たすために、COSはコンソールやCOS browserなどのグラフィカルツールに「フォルダ」または「ディレクトリ」の表示方法をシミュレートします。具体的にはキー値が`project/`で、中身が空のオブジェクトを作成することで、従来のフォルダをシミュレートする表示方法で実現します。

たとえば、アップロードオブジェクト`project/doc/a.txt`、区切り記号`/`は「フォルダ」の表示方法をシミュレートし、コンソールに「フォルダ」projectとdocが表示されます。docはprojectの下位レベルの「フォルダ」で、a.txtファイルが含まれています。

したがって、適用シナリオは単にファイルをアップロードするだけの場合は、最初にフォルダを作成ずに、直接アップロードすることができます。適用シナリオにフォルダの概念がある場合、フォルダの作成機能を提供する必要があります。パスは`／`で終わる0KBのファイルをアップロードできます。これにより、GetBucket APIを呼び出すときにこのファイルをフォルダとして扱うことができます。

**2）TransferManager**

XML Java SDKにおいて、アップロード、ダウンロードおよびレプリケーション操作をカプセル化し、`TransferManager`と命名します。APIの設計および伝送パフォーマンスを最適化するので、直接使用することをお勧めします。

`TransferManager`の主な特性は以下のとおりです：

- アップロードおよびダウンロードプロセスの一時停止と回復をサポートします。
- ファイルサイズに応じて簡単なアップロードまたはシャードアップロードのみを選択できることをサポートし、ユーザーは該判断限界を設定できます。
- タスクステータスのリスニングをサポートします。

`TransferManager`でアップロードするサンプルコード：

```java
TransferManager transferManager = new TransferManager(cosclient, threadPool);

String key = "docs/exampleobject.doc";
File localFile = new File("src/test/resources/len30M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
try {
    // 非同期結果Uploadを返し、waitForUploadResultを同期的に呼び出してuploadの終了を待つことができ、成功した場合、UploadResultを返し、失敗した場合、異常をスローします。
    Upload upload = transferManager.upload(putObjectRequest);
    Thread.sleep(10000);
    // タスクを一時停止します
    PersistableUpload persistableUpload = upload.pause();
    // アップロードを回復します
    upload = transferManager.resumeUpload(persistableUpload);
    // アップロードの進行状況を表示できます
    showTransferProgress(upload);
    // アップロードタスクの完了を待ちます
    UploadResult uploadResult = upload.waitForUploadResult();
    System.out.println(uploadResult.getETag());

    // アップロードタスクのキャンセルもサポートします
    transferManager.cancel();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

ransferManager.shutdownNow();
cosclient.shutdown();

```

**3）署名アルゴリズムの変化**

通常は手動で署名を計算する必要がないが、SDKの署名をフロントエンドに返却して使用する場合、署名アルゴリズムの変化に注意してください。署名につき、単回と複数回署名の区別がなくなり、一方、署名の有効期の設定により安全性を確保するようになります。詳しいアルゴリズムについては、[XML署名のリクエスト](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください。

**4）新しいAPI**

XML Java SDKには、APIが新規追加され、ニーズに応じて呼び出すことができます。以下を含みます：

* createBucket、GetBucket（List Objects）、ListBucketsなどのバケット操作。
* getBucketAcl、setBucketAclなどのバケットACL操作。
* setBucketLifecycleConfiguration、getBucketLifecycleConfiguration、deleteBucketLifecycleConfigurationなどのバケットライフサイクル操作。

より多くの詳細については、[Java SDK Interface Documentation](https://cloud.tencent.com/document/product/436/12263)を参照してください。

