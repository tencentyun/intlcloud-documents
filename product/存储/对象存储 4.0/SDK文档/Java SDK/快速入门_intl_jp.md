##開発前の準備

### 関連するリソース

COSのXML Java SDKリソースのダウンロードアドレス：[XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5)。

### 環境依存関係

- SDKはJDK 1.7、1.8およびそれ以降のバージョンをサポートします。
- JDKのインストール方式については、[Javaのインストールおよび構成](/ document / product / 436/10865)を参照してください。

> ?本書に記載されるSecretId、SecretKey、Bucketなどの名前の意味と取得方法について[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

### SDKインストール

SDKをインストールする方式は2つあります：Mavenインストールとソースコードインストール。

- Mavenインストール
  mavenプロジェクトにおいて、pom.xmlを使用して関連する依存関係を追加し、コンテンツは以下のとおりです：
```shell
<dependency>
            <groupId>com.qcloud</groupId>
            <artifactId>cos_api</artifactId>
            <version>5.4.10</version>
</dependency>
```

- ソースコードインストール
  [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5)からソースコードをダウンロードし、mavenを通じて導入します。例えば、eclipseであり、File -> Import -> maven -> Existing Maven Projectsを順に選択します。

### SDKのアンインストール

pom依存関係またはソースコードを削除することによりSDKをアンインストールすることができます。

## クイックスタート

### クライアントCOSClientの初期化

`COSClient`はCOS APIを呼び出すオブジェクトです。`COSClient`インスタンスを生成した後に繰り返し使用することができ、スレッドセキュリティです。最後にプログラムまたはサービスが終了した時、クライアントを閉じればよいです。

#### 恒久的なクラウドAPI暗号鍵情報による初期化

クラウドAPI暗号鍵は永続暗号鍵であり、Tencent Cloud [CAMコンソール](https://console.qcloud.com/cam/capi)により取得・生成され、大部分の適用シナリオに適しています。

Java SDKクラウドAPI暗号鍵の初期化方法は以下のとおりです。

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します。
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXX", "XXXXXXXXXXXXXXX");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
// clientConfigには、地域、https（デフォルトでは、http）、タイムアウト、プロキシなどの設定方法が含まれ、使用については、ソースコードまたはAPIドキュメントFAQの説明を参照してください。
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントの生成。
COSClient cosClient = new COSClient(cred, clientConfig);
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "mybucket-1251668577";
```

#### 一時暗号鍵による初期化

Tencent Cloud CAMサービスに一時暗号鍵を申請し、一時暗号鍵の生成および使用については、[一時暗号鍵の生成および使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

Java SDKは、一時暗号鍵をインバウンドしてクライアントを初期化することをサポートし、一時暗号鍵の初期化方法は以下のとおりです。

```java
// 1 取得された一時暗号鍵（tmpSecretId、tmpSecretKey、sessionToken）をインバウンドします
BasicSessionCredentials cred = new BasicSessionCredentials("a-demo-secretId", "a-demo-secretKey", "a-demo-session-token");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
// clientConfigには、地域、https（デフォルトでは、http）、タイムアウト、プロキシなどの設定方法が含まれ、使用については、ソースコードまたはAPIドキュメントFAQを参照してください
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントの生成
COSClient cosClient = new COSClient(cred, clientConfig);
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "mybucket-1251668577";
```

### ファイルのアップロード

ローカルファイルまたはサイズが既知となる入力ストリームコンテンツをCOSにアップロードし、20M以下の画像のような小さいファイルのアップロードに適し、最大5GBを超えないファイルのアップロードをサポートします。5GB以上のファイルであれば、マルチパートアップロードまたは高レベルAPIによるアップロードを使用してください。

- ローカルファイルの大部分が20M以上である場合、APIドキュメントの高レベルAPIによるアップロードを参照することをお勧めします。
- 同じキーのオブジェクトが既にCOSに存在する場合、アップロードする時に上書きします。
- ディレクトリオブジェクトを作成するには、COSにディレクトリが存在しないため、[APIドキュメント](https://cloud.tencent.com/document/product/436/12263#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)のFAQ部分を参照してください。
- オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)の説明を参照してください。
- アップロードした後、同じ `key`を使用して、` GetObject`APIを呼び出してファイルをローカルにダウンロードすることができ、事前署名リンクを生成し（ダウンロードする際に`GET`としてmethodを指定してください、具体的なAPIの説明については、[APIドキュメント](https://cloud.tencent.com/document/product/436/12263)を参照してください）、他の側に共有してダウンロードすることもできます。しかしながら、ファイルがプライベート読み取り権限であれば、事前署名リンクが一定の有効期間しかないことに注意してください。

サンプルコードは以下のとおりです。

```java
File localFile = new File("src/test/resources/len5M.txt");
// アップロード先のバケットを指定します
String bucketName = "demoBucket-1250000000";
// COSにアップロードされるオブジェクトキーを指定します
String key = "upload_single_demo.txt";

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### ファイルのダウンロード

ファイルをローカルにダウンロードしますか、またはファイルダウンロード入力ストリームを取得し、以下のサンプルコードを参照してください。

```java
// ダウンロード先のローカルパスを指定します
File downFile = new File("src/test/resources/mydown.txt");
// ファイルが位置するバケットを指定します
String bucketName = "demoBucket-1250000000";
// ファイルのCOS上のオブジェクトキーを指定します
String key = "upload_single_demo.txt";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### ファイルの削除

COS上の指定されたパスのファイルを削除し、コードは以下のとおりです。

```java
// ファイルが位置するバケットを指定します
String bucketName = "demoBucket-1250000000";
// ファイルのCOS上のオブジェクトキーを指定します
String key = "upload_single_demo.txt";

cosClient.deleteObject(bucketName, key);
```

### クライアントの閉鎖

cosClientを閉じ、かつHTTPで接続されたアプリケーションサーバー管理スレッドをリリースし、コードは以下のとおりです。

```
// クライアントを閉じます（アプリケーションサーバースレッドを閉じます）
cosClient.shutdown();
```

