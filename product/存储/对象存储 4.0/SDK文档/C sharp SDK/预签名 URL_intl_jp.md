## 概要
C# SDKは、オブジェクトURLを取得し、署名を計算し、リクエストの事前署名付きURLを取得するためのAPIを提供します。

## オブジェクトのURLの取得 
```C#
string GetAccessURL(CosRequest request);
```
## 署名の計算
```C#
string GenerateSign(string method, string path, Dictionary<string, string> queryParameters, Dictionary<string, string> headers, long signDurationSecond)；
```
## リクエストの事前署名付きURLの取得 
```C#
string GenerateSignURL(PreSignatureStruct preSignatureStruct);
```
### パラメータの説明
|パラメータ名|タイプ|説明|
|-----|-----|----|
|request|CosRequest|リクエストオブジェクト|
|preSignatureStruct|PreSignatureStruct|事前署名付きURLの例|
|method|string|HTTPリクエスト方法|
|path|string|HTTPリクエストパス、すなわち、オブジェクト鍵|
|headers|`Dictionary<string, string>`|署名のheaderを検証するかどうか|
|queryParameters|`Dictionary<string, string>`|署名のリクエストURL内の照合パラメータを検証するかどうか|
|signDurationSecond|long|署名の有効期間（単位：秒）|

### PreSignatureStruct 構造体の説明
PreSignatureStructオブジェクトを介して、対応する事前署名付きリクエストURLを取得し、リクエストを送信します。

|パラメータ名|タイプ|説明|
|-----|-----|----|
|appid|string|Tencent CloudアカウントAPPID|
|bucket|string|バケット|
|region|string|バケットが位置する地域|
|method|string|HTTPリクエスト方法|
|isHttps|bool|true：HTTPSリクエスト、false：HTTPリクエスト|
|key|string|オブジェクト鍵|
|headers|`Dictionary<string, string>`|署名のheaderを検証するかどうか|
|queryParameters|`Dictionary<string, string>`|署名のリクエストURL内の照合パラメータを検証するかどうか|
|signDurationSecond|long|署名の有効期間（単位：秒）|

## ##永続暗号鍵による事前署名リクエストの例

### アップロードリクエストの例
```C#
try
{
	//CosXmlを永続暗号鍵で初期化します
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //接続タイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.SetReadWriteTimeoutMs(40000)  //読み書きタイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.IsHttps(true)  //デフォルトのhttpsリクエストを設定します
	.SetAppid("1250000000")  //Tencent CloudアカウントのアカウントアイデンティティAPPIDを設定します
	.SetRegion("ap-beijing")  //デフォルトのバケット地域を設定します
	.SetDebugLog(true)  //ログを表示します
	.Build();  //CosXmlConfigオブジェクトを作成します
	string secretId = "COS_SECRETID"; //"クラウドAPI暗号鍵SecretId"；
	string secretKey = "COS_SECRETKEY"; //"クラウドAPI暗号鍵SecretKey"；
	long durationSecond = 600;  //secretKey有効期間（単位：秒）
	QCloudCredentialProvider cosCredentialProvider  =  new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent CloudアカウントAPPID
	preSignatureStruct.region = "ap-beijing"; //バケット地域
	preSignatureStruct.bucket = "examplebucket-1250000000"; //バケット
	preSignatureStruct.key = "exampleobject"; //オブジェクト鍵
	preSignatureStruct.httpMethod = "PUT"; //httpリクエスト方法
	preSignatureStruct.isHttps = true; //httpsリクエストURLを作成します
	preSignatureStruct.signDurationSecond = 600; //リクエスト署名有効期間は600sです
	preSignatureStruct.headers = null；//署名において検証する必要があるheader
	preSignatureStruct.queryParameters = null; //署名において検証する必要があるURL内のリクエストパラメータ
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //アップロードリクエストの事前署名付きURL（永続暗号鍵で計算された署名付きURL）

	string srcPath = @"F:\exampleobject"；//ローカルファイルの絶対パス
	PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
	//アップロードリクエストの事前署名付きURLを設定します
	request.RequestURLWithSign = requestSignURL;
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
```

### ダウンロードリクエストの例
```C#
try
{
	//CosXmlを永続暗号鍵で初期化します
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //接続タイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.SetReadWriteTimeoutMs(40000)  //読み書きタイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.IsHttps(true)  //デフォルトのhttpsリクエストを設定します
	.SetAppid("1250000000")  //Tencent CloudアカウントのアカウントアイデンティティAPPIDを設定します
	.SetRegion("ap-beijing")  //デフォルトのバケット地域を設定します
	.SetDebugLog(true)  //ログを表示します
	.Build();  //CosXmlConfigオブジェクトを作成します
	string secretId = "COS_SECRETID"; //"クラウドAPI暗号鍵SecretId"；
	string secretKey = "COS_SECRETKEY"; //"クラウドAPI暗号鍵SecretKey"；
	long durationSecond = 600;  //secretKey有効期間（単位：秒）
	QCloudCredentialProvider cosCredentialProvider  =  new DefaultQCloudCredentialProvider(secretId, secretKey, 600);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent CloudアカウントAPPID
	preSignatureStruct.region = "ap-beijing"; //バケット地域
	preSignatureStruct.bucket = "examplebucket-1250000000"; //バケット
	preSignatureStruct.key = "exampleobject"; //オブジェクト鍵
	preSignatureStruct.httpMethod = "GET"; //httpリクエスト方法
	preSignatureStruct.isHttps = true; //httpsリクエストURLを作成します
	preSignatureStruct.signDurationSecond = 600; //リクエスト署名有効期間は600sです
	preSignatureStruct.headers = null；//署名において検証する必要があるheader
	preSignatureStruct.queryParameters = null; //署名において検証する必要があるURL内のリクエストパラメータ
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //リクエストの事前署名付きURL（永続暗号鍵で計算された署名付きURL）
	
	string localDir = @"F:\"；//ローカルの指定されたフォルダにダウンロードします
	string localFileName = "exampleobject"; //ローカルに保存されたファイル名を指定します
	GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
	//ダウンロードリクエストの事前署名付きURLを設定します
	request.RequestURLWithSign = requestSignURL;
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


## 一時暗号鍵によるリクエストの事前署名の例

### アップロードリクエストの例
```C#
try
{
	//CosXmlを一時暗号鍵で初期化します
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //接続タイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.SetReadWriteTimeoutMs(40000)  //読み書きタイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.IsHttps(true)  //デフォルトのhttpsリクエストを設定します
	.SetAppid("1250000000")  //Tencent CloudアカウントのアカウントアイデンティティAPPIDを設定します
	.SetRegion("ap-beijing")  //デフォルトのバケット地域を設定します
	.SetDebugLog(true)  //ログを表示します
	.Build();  //CosXmlConfigオブジェクトを作成します
	string tmpSecretId = "COS_SECRETID"; //"一時暗号鍵SecretId"；
	string tmpSecretKey = "COS_SECRETKEY"; //"一時暗号鍵SecretKey"；
	string tmpToken = "COS_TOKEN"; //"一時暗号鍵token"；
	long tmpExpireTime = 1546862502；//一時暗号鍵の有効期間の終了時間
	QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent CloudアカウントAPPID
	preSignatureStruct.region = "ap-beijing"; //バケット地域
	preSignatureStruct.bucket = "examplebucket-1250000000"; //バケット
	preSignatureStruct.key = "exampleobject"; //オブジェクト鍵
	preSignatureStruct.httpMethod = "PUT"; //httpリクエスト方法
	preSignatureStruct.isHttps = true; //httpsリクエストURLを作成します
	preSignatureStruct.signDurationSecond = 600; //リクエスト署名有効期間は600sです
	preSignatureStruct.headers = null；//署名において検証する必要があるheader
	preSignatureStruct.queryParameters = null; //署名において検証する必要があるURL内のリクエストパラメータ
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //アップロードリクエストの事前署名付きURL（一時暗号鍵で計算された署名付きURL）

	string srcPath = @"F:\exampleobject"；//ローカルファイルの絶対パス
	PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
	//アップロードリクエストの事前署名付きURLを設定します
	request.RequestURLWithSign = requestSignURL;
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
```

### ダウンロードリクエストの例
```C#
try
{
	//CosXmlを一時暗号鍵で初期化します
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //接続タイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.SetReadWriteTimeoutMs(40000)  //読み書きタイムアウト時間をミリ秒単位で設定し、デフォルトは45000msです
	.IsHttps(true)  //デフォルトのhttpsリクエストを設定します
	.SetAppid("1250000000")  //Tencent CloudアカウントのアカウントアイデンティティAPPIDを設定します
	.SetRegion("ap-beijing")  //デフォルトのバケット地域を設定します
	.SetDebugLog(true)  //ログを表示します
	.Build();  //CosXmlConfigオブジェクトを作成します
	string tmpSecretId = "COS_SECRETID"; //"一時暗号鍵SecretId"；
	string tmpSecretKey = "COS_SECRETKEY"; //"一時暗号鍵SecretKey"；
	string tmpToken = "COS_TOKEN"; //"一時暗号鍵token"；
	long tmpExpireTime = 1546862502；//一時暗号鍵の有効期間の終了時間
	QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent CloudアカウントAPPID
	preSignatureStruct.region = "ap-beijing"; //バケット地域
	preSignatureStruct.bucket = "examplebucket-1250000000"; //バケット
	preSignatureStruct.key = "exampleobject"; //オブジェクト鍵
	preSignatureStruct.httpMethod = "GET"; //httpリクエスト方法
	preSignatureStruct.isHttps = true; //httpsリクエストURLを作成します
	preSignatureStruct.signDurationSecond = 600; //リクエスト署名有効期間は600sです
	preSignatureStruct.headers = null；//署名において検証する必要があるheader
	preSignatureStruct.queryParameters = null; //署名において検証する必要があるURL内のリクエストパラメータ
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //リクエストの事前署名付きURL（一時暗号鍵で計算された署名付きURL）
	
	string localDir = @"F:\"；//ローカルの指定されたフォルダにダウンロードします
	string localFileName = "exampleobject"; //ローカルに保存されたファイル名を指定します
	GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
	//ダウンロードリクエストの事前署名付きURLを設定します
	request.RequestURLWithSign = requestSignURL;
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

