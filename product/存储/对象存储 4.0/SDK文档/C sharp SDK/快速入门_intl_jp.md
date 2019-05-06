## ダウンロードおよびインストール

### 関連するリソース
- COSのXML C# SDKソースコードのダウンロードアドレス：[ XML C# SDK ](https://github.com/tencentyun/qcloud-sdk-dotnet)。
- 例示的なDemoのダウンロードアドレス：[ COS XML C# SDKの例](https://github.com/tencentyun/qcloud-sdk-dotnet-demo)。
- COSのXML C# SDK DLLファイルのダウンロードアドレス：[COS XML DLLライブラリー](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/libs)。

### 環境依存関係
- COS XML C# SDKソースコードは.NET 4.0に基づいて開発され、newtonsoft.jsonライブラリーに依存します。
- Windows：.NET 2.0以上のバージョン、Visual Studio 2010以上のバージョンをインストールします。 
- Linux/Mac：Mono 3.12以上のバージョンをインストールします。

### SDKインストール
SDKに含まれるDLLライブラリーファイルはCOSXML.dllとNewtonsoft.Json.dllであり、以下の方式でSDKをインストールできます：

- DLL参照方式
	[SDK開発パッケージ](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/libs)を取得し、その中のDLLファイルをプロジェクトにインポートします。
- プロジェクト導入方式
	 [ソースコード](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/QCloudCSharpSDK)を取得し、プロジェクトとしてインポートします。
- Nuget参照方式
	NugetパッケージマネージャからTencent.QCloud.Cos.Sdkを見つけ、クリックしてインストールします。

## 使用開始
以下、COS C# SDKを使用してクライアントの初期化、バケットの作成、バケットリストの照合、オブジェクトのアップロード、オブジェクトリストの照合、オブジェクトのダウンロードおよびオブジェクトの削除などの基本操作を完了させる方法について紹介します。

### 初期化

COSサービスに関連するいかなるリクエストを実行する前に、`CosXmlConfig、QCloudCredentialProvider、CosXmlServer`の3つのオブジェクトをインスタンス化する必要があります。そのうち：
- `CosXmlConfig`はSDK構成APIを提供します。
- `QCloudCredentialProvider`は暗号鍵情報設定APIを提供します。
- `CosXmlServer`はCOS APIサービスを操作する様々なAPIを提供します。

```C#
//CosXmlConfigを初期化します 
string appid = "1250000000";//Tencent CloudアカウントのアカウントアイデンティティAPPIDを設定します
string region = "ap-beijing"; //デフォルトのバケット地域を設定します
CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //接続タイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.SetReadWriteTimeoutMs(40000)  //読み書きタイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.IsHttps(true)  //デフォルトのhttpsリクエストを設定します
	.SetAppid(appid)  //Tencent CloudアカウントのアカウントアイデンティティAPPIDを設定します
	.SetRegion(region)  //デフォルトのバケット地域を設定します
	.SetDebugLog(true)  //ログを表示します
	.Build();  //CosXmlConfigオブジェクトを作成します

//QCloudCredentialProviderを初期化し、SDKには永続暗号鍵、一時暗号鍵、カスタマイズの3つの方式が提供されます 
QCloudCredentialProvider cosCredentialProvider  =  null;

//方式1、永続暗号鍵
string secretId = "COS_SECRETID"; //"クラウドAPI暗号鍵SecretId"；
string secretKey = "COS_SECRETKEY"; //"クラウドAPI暗号鍵SecretKey"；
long durationSecond = 600;  //secretKey有効期間（単位：秒）
cosCredentialProvider = new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);

//方式2、一時暗号鍵
string tmpSecretId = "COS_SECRETID"; //"一時暗号鍵SecretId"；
string tmpSecretKey = "COS_SECRETKEY"; //"一時暗号鍵SecretKey"；
string tmpToken = "COS_TOKEN"; //"一時暗号鍵token"；
long tmpExpireTime = 1546862502；//一時暗号鍵の有効期間の終了時間
cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);

//方式3、暗号鍵情報をカスタム方式で提供し、QCloudCredentialProviderを継承し、GetQCloudCredentials()方法を上書きします
public class MyQCloudCredentialProvider : QCloudCredentialProvider
{
	public override QCloudCredentials GetQCloudCredentials()
	{
		string secretId = "COS_SECRETID"; //暗号鍵SecretId
		string secretKey = "COS_SECRETKEY"; //暗号鍵SecretKey
		string keyTime = "暗号鍵の有効期間"; //1546862502;1546863102
		return new QCloudCredentials(secretId, secretKey, keyTime);
	}

	public override void Refresh()
	{
		//暗号鍵情報をアップデートします
	}
}
cosCredentialProvider = new MyQCloudCredentialProvider();

//CosXmlServerを初期化します
CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

```

### バケットの作成
```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット名、フォーマット：BucketName-APPID
	PutBucketRequest request = new PutBucketRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	PutBucketResult result = cosXml.PutBucket(request);
	//リクエスト成功
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
	//リクエスト失敗
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//リクエスト失敗
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

```

### バケットリストの照合
```C#
try
{
	GetServiceRequest request = new GetServiceRequest();
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	GetServiceResult result = cosXml.GetService(request);
	//リクエスト成功
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
	//リクエスト失敗
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{	
	//リクエスト失敗
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### アップデートオブジェクト
```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string srcPath = @"F:\exampleobject"；//ローカルファイルの絶対パス
	PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//進行コールバックを設定します
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//リクエストを実行します
	PutObjectResult result = cosXml.PutObject(request);
	//リクエスト成功
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//リクエスト失敗
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//リクエスト失敗
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

**//大容量ファイルの場合はマルチパートアップロード()を使用する必要があり、以下の例に示すように、SDKにカプセル化されたTransferManagerとCOSXMLUploadTaskクラスを参照してください**
TransferManager transferManager = new TransferManager(cosXml, new TransferConfig());
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, null, key);
uploadTask.SetSrcPath(srcPath);
uploadTask.progressCallback = delegate (long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
};
uploadTask.successCallback = delegate (CosResult cosResult) 
{
	COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = cosResult as COSXML.Transfer.COSXMLUploadTask.UploadTaskResult;
	Console.WriteLine(result.GetResultInfo());
};
uploadTask.failCallback = delegate (CosClientException clientEx, CosServerException serverEx) 
{
	if (clientEx != null)
	{
		Console.WriteLine("CosClientException: " + clientEx.Message);
	}
	if (serverEx != null)
	{
		Console.WriteLine("CosServerException: " + serverEx.GetInfo());
	}
};
transferManager.Upload(uploadTask);

```

### オブジェクトリストの照合
```C#
try
{
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
	GetBucketRequest request = new GetBucketRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	GetBucketResult result = cosXml.GetBucket(request);
	//リクエスト成功
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
	//リクエスト失敗
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//リクエスト失敗
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### ダウンロード対象
```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string localDir = @"F:\"；//ローカルの指定されたフォルダにダウンロードします
	string localFileName = "exampleobject"; //ローカルに保存されたファイル名を指定します
	GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//進行コールバックを設定します
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//リクエストを実行します
	GetObjectResult result = cosXml.GetObject(request);
	//リクエスト成功
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//リクエスト失敗
 	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//リクエスト失敗
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### オブジェクトの削除
```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	DeleteObjectResult result = cosXml.DeleteObject(request);
	//リクエスト成功
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//リクエスト失敗
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//リクエスト失敗
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

