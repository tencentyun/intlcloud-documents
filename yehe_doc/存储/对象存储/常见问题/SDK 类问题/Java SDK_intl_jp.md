### クライアント側のネットワークは正常なのに、HTTPでのCOSアクセスが非常に遅かったり、Connection resetのエラーが発生したりします。どのように対処すればよいですか。
一部の地域ではキャリアがCOSのドメイン名をハイジャックする可能性がありますので、COSへのアクセスはできる限りHTTPSで行ってください。

### SDKをインポートして実行すると、java.lang.NoSuchMethodErrorというエラーが表示されましたが、どのように対処すればよいですか。

原因：一般的にはJARパッケージの競合発生によるものです。例えば、ユーザーのプロジェクト内のhttpclientライブラリ内のJARパッケージのバージョンにはメソッドAがなく、一方でSDKが依存するJARパッケージではメソッドAを使用する場合などです。この場合、実行時のロード順序の問題により、ユーザーのプロジェクト内のhttpclientライブラリをロードし、実行する際にNoSuchMethodErrorのエラーがスローされます。
解決方法：
方法1：プロジェクト内のNoSuchMethodErrorの原因となるパッケージのバージョンを、SDKのpom.xmlにある対応するライブラリのバージョンと一致させます。
方法2：cos-java-sdkをcos_api-bundleに切り替えます。この方法ではcos-java-sdkのすべての依存関係が独立してインストールされるため、より多くの容量を占有します。
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### Java SDKのデフォルトのタイムアウト時間はどのくらいですか。

Java SDKのデフォルトの接続タイムアウト時間は45000ms、デフォルトの読み取り/書き込みタイムアウト時間は45000msです。SDKのSetConnectionTimeoutMsメソッドおよびSetReadWriteTimeoutMsを使用して調整できます。

### Java SDKのアップロード速度が遅く、ログにはIOExceptionが頻繁にプリントされますが、どのように対処すればよいですか。

原因と対処方法は次のとおりです。

1. まず、パブリックネットワークでCOSにアクセスしているかどうかを確認します。現在同一リージョンのCVMによるCOSへのアクセスはプライベートネットワークを使用します（プライベートネットワークドメイン名が解決されるIPは10、100、169のネットワークセグメントです。COSドメイン名に関しては[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください）。パブリックネットワークを使用している場合は、出口帯域幅が小さくないか、または他のプログラムによって帯域幅リソースが占有されていないかを確認します。
2. 本番環境におけるログレベルがDEBUGではないことを確認します。INFOログの使用をお勧めします。
3. 現時点でシンプルアップロードの速度は10MBに達することが可能で、高度なAPIは同時実行数32の状況下での速度が60MBに達することが可能です。これらの値より速度が著しく低い場合は、上記の2点をご参照ください。
4. WARNログにプリントされたIOExceptionを無視できる場合、SDKはリトライを行います。IOExceptionの原因はネットワーク速度が遅すぎるためである可能性があります。対処方法については1と2をご参照ください。

### ファイルアップロードリクエストパスに「+」が含まれ、Code: 403  SignatureDoesNotMatchのエラーが発生しましたが、どのように対処すればよいですか。
考えられる原因：ユーザーのJava環境のhttpclientバージョンによって起こったurlencodeエンコードエラー。
解決方法：次の方法で解決することをお勧めします。
方法1：httpclientバージョン4.5.3を使用します。
```
<groupId>org.apache.httpcomponents</groupId>
       <artifactId>httpclient</artifactId>
 <version>4.5.3</version> 
```

方法2：cos-java-sdkをcos_api-bundleに切り替えます。この方法ではcos-java-sdkのすべての依存関係が独立してインストールされるため、より多くの容量を占有します。
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### Java SDKを使用中に、ある依存バージョンが低すぎるというエラーが発生しましたが、どのように対処すればよいですか。
原因：ユーザーのJava環境の依存バージョンとJava SDKが必要とする依存バージョンが競合している。
解決方法:
方法1：表示に従って、対応する依存関係を必要なバージョンにアップグレードします。
方法2：cos-java-sdkをcos_api-bundleに切り替えます。この方法ではcos-java-sdkのすべての依存関係が独立してインストールされるため、より多くの容量を占有します。
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### SDKでディレクトリを作成するにはどうすればよいですか。

COSのファイルとディレクトリはどちらもオブジェクトであり、ディレクトリは`/`で終わるオブジェクトに過ぎません。ファイルを作成する際は、ディレクトリを作成する必要はありません。オブジェクトキーが`xxx/yyy/zzz.txt`のファイルを作成する場合は、keyを`xxx/yyy/zzz.txt`に設定するだけでよく、`xxx/yyy/`というオブジェクトを作成する必要はありません。コンソール上で表示する際は、`/`で区切ることでディレクトリの階層のように表示することも可能です。ただし、これらのディレクトリオブジェクトは存在しないものです。ディレクトリオブジェクトを作成したい場合は、次のサンプルコードを使用することができます。

```java
String bucketName = "examplebucket-1250000000";
String key = "folder/images/";
// ディレクトリオブジェクトとは末尾が/の空ファイルであり、長さが0のbyteストリームがアップロードされます
InputStream input = new ByteArrayInputStream(new byte[0]);
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest =
new PutObjectRequest(bucketName, key, input, objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### SDKでHTTPSを使用するにはどうすればよいですか。

SDKの関連設定はすべてClientConfigクラスの中に一括保存されており、サンプルコードは次のとおりです。

```java
// ユーザーID情報(secretId, secretKey)を初期化します
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// bucketのリージョンを設定します。COSリージョンの略称についてはhttps://intl.cloud.tencent.com/document/product/436/6224をご参照ください
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// httpsの使用を設定します
clientConfig.setHttpProtocol(HttpProtocol.https);
// cosクライアントを生成します
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDKでプロキシを使用するにはどうすればよいですか。

プロキシを使用してアクセスする必要があるCOSのクライアントは、ClientConfigクラスでプロキシIP（またはドメイン名）およびポートを設定できます。サンプルコードは次のとおりです。

```java
// ユーザーID情報(secretId, secretKey)を初期化します
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// bucketのリージョンを設定します。COSリージョンの略称についてはhttps://intl.cloud.tencent.com/document/product/436/6224をご参照ください
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// プロキシの使用を設定します(IPとポートを同時に設定する必要があります)
// プロキシIPを設定します(ドメイン名を入れることもできます)
clientConfig.setHttpProxyIp("192.168.2.3");
// プロキシポートを設定します
clientConfig.setHttpProxyPort(8080);
// cosクライアントを生成します
COSClient cosClient = new COSClient(cred, clientConfig);
```

### カスタムEndpointBuilderを設定するにはどうすればよいですか。
APIリクエストのEndpointを指定する必要があるかもしれないケースの場合、EndpointBuilderインターフェースの中のbuildGeneralApiEndpointおよびbuildGetServiceApiEndpointの中の2つの関数を実装し、それぞれ一般APIリクエストおよびGETServiceリクエストが指定するリモートEndpointとする必要があります。使用例は次のとおりです。
```
// ステップ1：EndpointBuilderインターフェースの中の2つの関数を実装します
class SelfDefinedEndpointBuilder implements EndpointBuilder {
    @Override
    public String buildGeneralApiEndpoint(String bucketName) {
        return String.format("%s.%s", bucketName, "mytest.com");
    }

    @Override
    public String buildGetServiceApiEndpoint() {
        return "service.mytest.com";
    }
}

// ステップ2：クライアントを初期化します
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
SelfDefinedEndpointBuilder selfDefinedEndpointBuilder = new SelfDefinedEndpointBuilder();
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
clientConfig .setEndpointBuilder(selfDefinedEndpointBuilder);
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDKのアップロード、ダウンロード、一括削除などの操作において、使用するkey値にはプレフィックス`/`を追加する必要がありますか。
COSのkey値にはプレフィックス`/`を付ける必要はありません。例えば、オブジェクトのkey値をexampleobjectに設定してアップロードしたオブジェクトは、URL： `http://cos.ap-guangzhou.myqcloud.com/exampleobject`によってアクセスすることができます。
>!一括削除するリクエストの中には、プレフィックスが`/`のkeyを入れないでください。オブジェクトの削除に失敗する場合があります。


### COSでJava SDKを使用してアップロードを行った際に、please make sure bucket name must contain legal appid when appid is missing. example: bucektname-1250000000というエラーが発生しましたが、どのように対処すればよいですか。

COS Java SDKの旧バージョンは、例えば125で始まるAPPIDのみをサポートしています。ご使用中のAPPIDが130で始まるものの場合は、SDKを最新バージョンに更新することをお勧めします。Java SDKのダウンロードとインストールについては[Java SDKドキュメント](https://intl.cloud.tencent.com/document/product/436/10199)をご参照ください。

### COS Java SDKを使用して大容量ファイルをアップロードするにはどうすればよいですか。

Java SDKを使用して5Gより大きなファイルをアップロードする場合は、[高度なアップロードインターフェース](https://intl.cloud.tencent.com/document/product/436/31534)の使用をお勧めします。高度なアップロードインターフェースはユーザーファイルの長さおよびデータタイプに応じて、シンプルアップロードまたはマルチパートアップロード方式を自動的に選択します。

### Java SDKでファイルアップロードの進捗状況を取得するにはどうすればよいですか。

進捗状況を取得したい場合は、[高度なアップロード](https://intl.cloud.tencent.com/document/product/436/31534)インターフェースを使用し、UploadのメソッドgetProgress()を呼び出してアップロードの進捗状況を示すTransferProgressクラスを取得することをお勧めします。

### Java SDKはローカルファイルのCRC64の計算をサポートしていますか。

COS Java SDK自体はローカルファイルのcrc64の計算をサポートしていません。業務側での実現が必要な場合は、[Java issues](https://github.com/tencentyun/cos-java-sdk-v5/issues/63)を参照して回答をお探しください。

### Java SDKで検証した、COSから返されたCRC64が21ビットであった場合、ローカルで計算したCRC64と比較するにはどうすればよいですか。

JavaのLongは20桁の数字しかサポートしていません。次の比較方法をご参照ください。

```java
CRC64 localCRC = new CRC64();
// ローカルのcrc64を計算します
localCRC.update();
//...

// COSから返されたCRCをLongに変換します
cosCRC = crc64ToLong(strCOSCRC);

// 比較します
if (cosCRC == localCRC.getValue()) {
   xxx
}

// COSから返されたCRC64を1つのJava内のLongに変換します
long crc64ToLong(String crc64) {
   if (crc64.charAt(0) == '-') {
       return negativeCrc64ToLong(crc64);
   }else{
       return positiveCrc64ToLong(crc64);
   }
}

long positiveCrc64ToLong(String strCrc64) {
   BigInteger crc64 = new BigInteger(strCrc64);
   BigInteger maxLong = new BigInteger(Long.toString(Long.MAX_VALUE));

   int maxCnt = 0;

   while (crc64.compareTo(maxLong) > 0) {
       crc64 = crc64.subtract(maxLong);
       maxCnt++;
   }

   return crc64.longValue() + Long.MAX_VALUE * maxCnt;
}

long negativeCrc64ToLong(String strCrc64) {
   BigInteger crc64 = new BigInteger(strCrc64);
   BigInteger minLong = new BigInteger(Long.toString(Long.MIN_VALUE));

   int minCnt = 0;

   while (crc64.compareTo(minLong) < 0) {
       crc64 = crc64.subtract(minLong);
       minCnt++;
   }

   return crc64.longValue() + Long.MIN_VALUE * minCnt;
}
```

### Java SDKは長時間接続を使用できますか。

Java SDKはデフォルトで長時間接続を使用します。

### Java SDKを使用して、指定のディレクトリのすべてのパスを取得すると同時に、パスがファイルかフォルダかを判断するにはどうすればよいですか。

Java SDKの[オブジェクトリストの照会](https://intl.cloud.tencent.com/document/product/436/10199#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)機能を使用して、バケット内のオブジェクトをリストアップすることができます。**prefixパラメータを使用すると、ディレクトリのプレフィックスを指定できます**。



