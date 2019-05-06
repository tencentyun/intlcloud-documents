COS XML C＃SDK操作が成功した場合は各APIに対応するタイプを返し、失敗した場合はCosClientExceptionと
 CosServerExceptionをスローします。そのうち、CosClientExceptionは、パラメータが空であり、ネットワーク接続が失敗したなど、クライアント異常を表します；CosServerExceptionは、存在しないファイルにアクセスし、ファイルへのアクセス権限がないなど、サーバーが要件を満たさないクライアントのリクエストを処理する時に返したエラーを表します。詳細については、[SDK異常説明]（#COS_EXCEPTION）を参照してください。

SDKでは、各APIリクエストのために同期と非同期という2つのリクエスト方法を提供します。

## Service APIの説明

### バケットリストの取得

##### 機能説明

指定されたアカウント内のすべてのバケットリスト（Bucket list）を取得するために使用されます。

#### 方法のプロトタイプ
```C#
GetServiceResult GetService(GetServiceRequest request);

void GetService(GetServiceRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
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

/**
//非同期方法
GetServiceRequest request = new GetServiceRequest();
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetService(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		GetServiceResult result = cosResult as GetServiceResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetServiceResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|listAllMyBuckets|[ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListAllMyBuckets.cs)|指定されたアカウント内のバケットリストの情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

## Bucket API説明

### バケットの作成

##### 機能説明

バケットを作成します（Put Bucket）。

#### 方法のプロトタイプ
```C#
PutBucketResult PutBucket(PutBucketRequest request);

void PutBucket(PutBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
PutBucketRequest request = new PutBucketRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.PutBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		PutBucketResult result = cosResult as PutBucketResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
PutBucketResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットの削除

##### 機能説明

指定されたバケットを削除します（Delete Bucket）。

#### 方法のプロトタイプ
```C#
DeleteBucketResult DeleteBucket(DeleteBucketRequest request);

void DeleteBucket(DeleteBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	DeleteBucketRequest request = new DeleteBucketRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	DeleteBucketResult result = cosXml.DeleteBucket(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
DeleteBucketRequest request = new DeleteBucketRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.DeleteBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		DeleteBucketResult result = cosResult as DeleteBucketResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
DeleteBucketResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットの検索

##### 機能説明

指定されたバケットが存在するかどうかを検索します（Head Bucket）。

#### 方法のプロトタイプ
```C#
HeadBucketResult HeadBucket(HeadBucketRequest request);

void HeadBucket(HeadBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	HeadBucketRequest request = new HeadBucketRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	HeadBucketResult result = cosXml.HeadBucket(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
HeadBucketRequest request = new HeadBucketRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.HeadBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		HeadBucketResult result = cosResult as HeadBucketResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
HeadBucketResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトリストの取得

##### 機能説明

指定されたバケット内のすべてのオブジェクト（Object List）を取得します。

#### 方法のプロトタイプ
```C#
GetBucketResult GetBucket(GetBucketRequest request);

void GetBucket(GetBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
GetBucketRequest request = new GetBucketRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		GetBucketResult result = cosResult as GetBucketResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetBucketResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|listBucket|[ListBucket](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListBucket.cs)|バケットのオブジェクトリスト情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケット地域の取得

##### 機能説明

指定されたバケットが位置する地域の情報を取得します（Get Bucket Location）。

#### 方法のプロトタイプ
```C#
GetBucketLocationResult GetBucketLocation(GetBucketLocationRequest request);

void GetBucketLocation(GetBucketLocationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	GetBucketLocationRequest request = new GetBucketLocationRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	GetBucketLocationResult result = cosXml.GetBucketLocation(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
GetBucketLocationRequest request = new GetBucketLocationRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucketLocation(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		GetBucketLocationResult result = cosResult as GetBucketLocationResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetBucketLocationResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|locationConstraint|[LocationConstraint](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LocationConstraint.cs)|バケットの地域情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします


### バケットACLの設定

##### 機能説明

指定されたバケットのアクセス制御リスト（ACL）を設定します（Put Bucket ACL）。

#### 方法のプロトタイプ
```C#
PutBucketACLResult PutBucketACL(PutBucketACLRequest request);

void PutBucketACL(PutBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	PutBucketACLRequest request = new PutBucketACLRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//プライベート読み書き権限を設定します
	request.SetCosACL(CosACL.PRIVATE);
	//アカウント1131975903に読み取り権限を付与します
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
	readAccount.AddGrantAccount("1131975903", "1131975903");
	request.setXCosGrantRead(readAccount);
	//リクエストを実行します
	PutBucketACLResult result = cosXml.PutBucketACL(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
PutBucketACLRequest request = new PutBucketACLRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//プライベート読み書き権限を設定します
request.SetCosACL(CosACL.PRIVATE);
//アカウント1131975903に読み取り権限を付与します
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
readAccount.AddGrantAccount("1131975903", "1131975903");
request.setXCosGrantRead(readAccount);
//リクエストを実行します
cosXml.PutBucketACL(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		PutBucketACLResult result = cosResult as PutBucketACLResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|cosAcl|SetCosAcl|バケットのACL権限を設定します|string|
|grandtAccout|SetXCosGrantReadまたはSetXCosGrantWriteまたはSetXCosReadWrite|ユーザーに読み書き権限を付与します|GrantAccount|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
PutBucketACLResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットACLの取得

##### 機能説明

指定されたバケットのアクセス制御リスト（ACL）を取得します（Get Bucket ACL）。

#### 方法のプロトタイプ
```C#
GetBucketACLResult GetBucketACL(GetBucketACLRequest request);

void GetBucketACL(GetBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	GetBucketACLRequest request = new GetBucketACLRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	GetBucketACLResult result = cosXml.GetBucketACL(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
GetBucketACLRequest request = new GetBucketACLRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucketACL(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		GetBucketACLResult result = cosResult as GetBucketACLResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetBucketACLResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|accessControlPolicy|[AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs)|バケットのアクセス制御リストの情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットのクロスオリジンアクセス構成の設定

##### 機能説明

指定されたバケットのクロスオリジンアクセス構成情報（CORS）を設定します（Put Bucket CORS）。

#### 方法のプロトタイプ
```C#
PutBucketCORSResult PutBucketCORS(PutBucketCORSRequest request);

void PutBucketCORS(PutBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//クロスオリジンアクセス構成CORSを設定します
	COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = new COSXML.Model.Tag.CORSConfiguration.CORSRule();
	corsRule.id = "corsconfigureId";
	corsRule.maxAgeSeconds = 6000;
	corsRule.allowedOrigin = "http://cloud.tencent.com";

	corsRule.allowedMethods = new List<string>();
	corsRule.allowedMethods.Add("PUT");

	corsRule.allowedHeaders = new List<string>();
	corsRule.allowedHeaders.Add("Host");

	corsRule.exposeHeaders = new List<string>();
	corsRule.exposeHeaders.Add("x-cos-meta-x1");

	request.SetCORSRule(corsRule);

	//リクエストを実行します
	PutBucketCORSResult result = cosXml.PutBucketCORS(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);

//クロスオリジンアクセス構成CORSを設定します
COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = new COSXML.Model.Tag.CORSConfiguration.CORSRule();
corsRule.id = "corsconfigureId";
corsRule.maxAgeSeconds = 6000;
corsRule.allowedOrigin = "http://cloud.tencent.com";

corsRule.allowedMethods = new List<string>();
corsRule.allowedMethods.Add("PUT");

corsRule.allowedHeaders = new List<string>();
corsRule.allowedHeaders.Add("Host");

corsRule.exposeHeaders = new List<string>();
corsRule.exposeHeaders.Add("x-cos-meta-x1");

request.SetCORSRule(corsRule);

cosXml.PutBucketCORS(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		PutBucketCORSResult result = cosResult as PutBucketCORSResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|corsRule|SetCORSRule|バケットのクロスオリジンアクセス構成を設定します|CORSConfiguration.CORSRule|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
PutBucketCORSResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットのクロスオリジンアクセス構成の取得

##### 機能説明

指定されたバケットのクロスオリジンアクセス構成情報（CORS）を取得します（Get Bucket CORS）。

#### 方法のプロトタイプ
```C#
GetBucketCORSResult GetBucketCORS(GetBucketCORSRequest request);

void GetBucketCORS(GetBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	GetBucketCORSResult result = cosXml.GetBucketCORS(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.GetBucketCORS(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		GetBucketCORSResult result = cosResult as GetBucketCORSResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetBucketCORSResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|corsConfiguration|[CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CORSConfiguration.cs)|バケットのクロスオリジンリソース共有構成の情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットのクロスオリジンアクセス構成の削除

##### 機能説明

指定されたバケットのクロスオリジンアクセス構成(CORS)を削除します（Delete Bucket CORS）。

#### 方法のプロトタイプ
```C#
DeleteBucketCORSResult DeleteBucketCORS(DeleteBucketCORSRequest request);

void DeleteBucketCORS(DeleteBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	DeleteBucketCORSResult result = cosXml.DeleteBucketCORS(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.DeleteBucketCORS(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		DeleteBucketCORSResult result = cosResult as DeleteBucketCORSResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
DeleteBucketCORSResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします


### バケットのライフサイクルの設定

##### 機能説明

指定されたバケットのライフサイクル構成情報（Lifecycle）を設定します（Put Bucket LifeCycle）。

#### 方法のプロトタイプ
```C#
PutBucketLifecycleResult PutBucketLifecycle(PutBucketLifecycleRequest request);

void PutBucketLifecycle(PutBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//lifecycleを設定します
	COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
	rule.id = "lfiecycleConfigureId";
	rule.status = "Enabled"; //Enabled，Disabled

	rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
	rule.filter.prefix = "2/";

	//指定されたパートの期限切れ削除操作
	rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
	rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

	request.SetRule(rule);

	//リクエストを実行します
	PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//lifecycleを設定します
COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
rule.id = "lfiecycleConfigureId";
rule.status = "Enabled"; //Enabled，Disabled

rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
rule.filter.prefix = "2/";

rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

request.SetRule(rule);

//リクエストを実行します
cosXml.PutBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		PutBucketLifecycleResult result = cosResult as PutBucketLifecycleResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|rule|SetRule|バケットのライフサイクル構成を設定します|LifecycleConfiguration.Rule|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
PutBucketLifecycleResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットのライフサイクルの取得

##### 機能説明

指定されたバケットのライフサイクル（Lifecycle）を取得します(Get Bucket Lifecycle)。

#### 方法のプロトタイプ
```C#
GetBucketLifecycleResult GetBucketLifecycle(GetBucketLifecycleRequest request);

void GetBucketLifecycle(GetBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.GetBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		 GetBucketLifecycleResult result = cosResult as GetBucketLifecycleResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetBucketLifecycleResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|lifecycleConfiguration|[LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LifecycleConfiguration.cs)|バケットのライフサイクル構成情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### バケットのライフサイクルの削除

##### 機能説明

指定されたバケットのライフサイクル（Lifecycle）を削除します（Delete Bucket Lifecycle）。

#### 方法のプロトタイプ
```C#
DeleteBucketLifecycleResult DeleteBucketLifecycle(DeleteBucketLifecycleRequest request);

void DeleteBucketLifecycle(DeleteBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.DeleteBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		DeleteBucketLifecycleResult result = cosResult as DeleteBucketLifecycleResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
DeleteBucketLifecycleResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### マルチパートアップロードの照合

##### 機能説明

指定されたバケット内の実行中のマルチパートアップロードを照合します（List Multipart Uploads）。

#### 方法のプロトタイプ
```C#
ListMultiUploadsResult ListMultiUploads(ListMultiUploadsRequest request);

void ListMultiUploads(ListMultiUploadsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //フォーマット：bucketname-appid
	ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	ListMultiUploadsResult result = cosXml.ListMultiUploads(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //フォーマット：bucketname-appid
ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.ListMultiUploads(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		ListMultiUploadsResult result = cosResult as ListMultiUploadsResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
ListMultiUploadsResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|listMultipartUploads|[ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListMultipartUploads.cs)|バケット内のすべての実行中のマルチパートアップロードの情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

## Object API説明

### オブジェクトの簡単なアップロード

##### 機能説明

指定されたバケットにオブジェクトをアップロードします（Put Object）。

#### 方法のプロトタイプ
```C#
PutObjectResult PutObject(PutObjectRequest request);

void PutObject(PutObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string srcPath = @"F:\test.txt"；//ローカルファイルパス
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string srcPath = @"F:\test.txt";  //ローカルファイルパス
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//進行コールバックを設定します
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//リクエストを実行します
cosXml.PutObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		PutObjectResult result = cosResult as PutObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|srcPath|構築方法|COSにアップロードするためのローカルファイルの絶対パス|string|
|data|構築方法|COSにアップロードするためのbyte数|byte[]|
|progressCallback|SetCosProgressCallback|アップロード進行コールバックを設定します|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
PutObjectResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|eTag|string|オブジェクトのeTagを返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトのマルチパートアップロード

オブジェクトのマルチパートアップロードに含まれる操作：

オブジェクトのマルチパートアップロード：マルチパートアップロードを初期化し、パートをアップロードし、すべてのパートのアップロードを完了させます。

マルチパートアップロードの再開：アップロードされたパートを照合し、パートをアップロードし、すべてのパートのアップロードを完了させます。

アップロードされたパートを削除します。

#### <span id = "INIT_MULIT_UPLOAD">マルチパートアップロードの初期化</span>

##### 機能説明

マルチパートアップロードを初期化し、対応するuploadIdを取得します（Initiate Multipart Upload）。

##### 方法のプロトタイプ
```C#
InitMultipartUploadResult InitMultipartUpload(InitMultipartUploadRequest request);

void InitMultipartUpload(InitMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
	//リクエスト成功
	string uploadId = result.initMultipartUpload.uploadId; //後続のマルチパートアップロードに使用されるuploadId
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.InitMultipartUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		InitMultipartUploadResult result = cosResult as InitMultipartUploadResult;
		string uploadId = result.initMultipartUpload.uploadId; //後続のマルチパートアップロードに使用されるuploadId
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

##### 戻り結果の説明
InitMultipartUploadResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|initMultipartUpload|[InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/InitiateMultipartUpload.cs)|オブジェクトのマルチパートアップロードを初期化した後に得られたuploadIdを返します |

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

#### <span id = "LIST_MULIT_UPLOAD">アップロードされたパートの照合</span>

##### 機能説明

指定uploadIdのアップロードされたパートを照合します（List Parts）。

##### 方法のプロトタイプ
```C#
ListPartsResult ListParts(ListPartsRequest request);

void ListParts(ListPartsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
	ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	ListPartsResult result = cosXml.ListParts(request);
	//リクエスト成功
	//アップロードされたパートを列挙します
	List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.ListParts(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		ListPartsResult result = cosResult as ListPartsResult;
		//アップロードされたパートを列挙します
		List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	 {	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|構築方法またはSetUploadId|指定されたマルチパートアップロードのuploadIdの識別 |string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

##### 戻り結果の説明
ListPartsResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|listParts|[ListParts](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListParts.cs)|指定されたuploadIdのマルチパートアップロードにおけるアップロードされたパートの情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

#### <span id = "MULIT_UPLOAD_PART">パートのアップロード</span>

パートをアップロードします（Upload Part）。

##### 方法のプロトタイプ
```C#
UploadPartResult UploadPart(UploadPartRequest request);

void UploadPart(UploadPartRequest, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
	int partNumber = 1; //パートの番号、1からの自然数にする必要があります
	string srcPath = @"F:\test.txt"; //ローカルファイルパス
	UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, uploadId, srcPath);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//進行コールバックを設定します
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {0:##.##}%",  completed * 100.0 / total));
	});
	//リクエストを実行します
	UploadPartResult result = cosXml.UploadPart(request);
	//リクエスト成功
	//返されたパートのeTagを取得し、後続のCompleteMultiUploadsに使用します
	string eTag = result.eTag;
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
int partNumber = 1; //パートの番号、1からの自然数にする必要があります
string srcPath = @"F:\test.txt"; //ローカルファイルパス
UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, uploadId, srcPath);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//進行コールバックを設定します
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {0:##.##}%",  completed * 100.0 / total));
});
//リクエストを実行します
cosXml.UploadPart(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		UploadPartResult result = cosResult as UploadPartResult;
		//返されたパートのeTagを取得し、後続のCompleteMultiUploadsに使用します
		string eTag = result.eTag;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|構築方法またはSetUploadId|指定されたマルチパートアップロードのuploadIdの識別 |string|
|partNumber|構築方法またはSetPartNumber|指定されたパートの番号、>=1でなければなりません|int|
|srcPath|構築方法|COSにアップロードするためのローカルファイルの絶対パス|string|
|data|構築方法|COSにアップロードするためのbyte数|byte[]|
|progressCallback|SetCosProgressCallback|アップロード進行コールバックを設定します|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

##### 戻り結果の説明
UploadPartResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|eTag|string|オブジェクトのパートのeTagを返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

#### <span id = "COMPLETE_MULIT_UPLOAD">すべてのパートのアップロードの完了</span>

##### 機能説明

すべてのパートのアップロードの完了を実現します（Complete Multipart Upload）。

##### 方法のプロトタイプ
```C#
CompleteMultiUploadResult CompleteMultiUpload(CompleteMultiUploadRequest request);

void CompleteMultiUpload(CompleteMultiUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
	CompleteMultiUploadRequest request = new CompleteMultiUploadRequest(bucket, key, uploadId);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//partNumberに従ってアップロードされたパートを昇順に設定する必要があります
	request.SetPartNumberAndETag(1, "partNumber1 eTag");
	//リクエストを実行します
	CompleteMultiUploadResult result = cosXml.CompleteMultiUpload(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
CompleteMultiUploadRequest request = new CompleteMultiUploadRequest(bucket, key, uploadId);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//partNumberに従ってアップロードされたパートを昇順に設定する必要があります
request.SetPartNumberAndETag(1, "partNumber1 eTag");
//リクエストを実行します
cosXml.CompleteMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		CompleteMultiUploadResult result = result as CompleteMultiUploadResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
   {	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|構築方法またはSetUploadId|指定されたマルチパートアップロードのuploadIdの識別 |string|
|partNumber|SetPartNumberAndETag|指定されたパートの番号、>=1でなければなりません|int|
|eTag|SetPartNumberAndETag|指定されたパートがアップロードれた後に返されたeTagの識別|string|
|partNumberAndETags|SetPartNumberAndETag|パートの番号とシャー度パートがアップロードされた後に返されたeTagの識別|`Dictionary<int, string> `|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

##### 戻り結果の説明
CompleteMultiUploadResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|completeMultipartUpload|[CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CompleteMultipartUploadResult.cs)|すべてのパートのアップロード成功情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

#### <span id = "ABORT_MULIT_UPLOAD">アップロードされたパートの削除</span>

##### 機能説明

1つのマルチパートアップロードを破棄し、かつアップロードされたパートを削除します（Abort Multipart Upload）。

##### 方法のプロトタイプ
```C#
AbortMultiUploadResult AbortMultiUpload(AbortMultiUploadRequest request);

void AbortMultiUpload(AbortMultiUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
	AbortMultiUploadRequest request = new AbortMultiUploadRequest(bucket, key, uploadId);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	AbortMultiUploadResult result = cosXml.AbortMultiUpload(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
AbortMultiUploadRequest request = new AbortMultiUploadRequest(bucket, key, uploadId);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.AbortMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		AbortMultiUploadResult result = result as AbortMultiUploadResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|uploadId|構築方法またはSetUploadId|指定されたマルチパートアップロードのuploadIdの識別 |string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

##### 戻り結果の説明
AbortMultiUploadResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### Postによるオブジェクトのアップロード

##### 機能説明

フォームを使用してオブジェクトをアップロードします（Post Object）。

#### 方法のプロトタイプ
```C#
PostObjectResult PostObject(PostObjectRequest request);

void PostObject(PostObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string srcPath = @"F:\test.txt"；//ローカルファイルパス
	PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//進行コールバックを設定します
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//リクエストを実行します
	PostObjectResult result = cosXml.PostObject(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string srcPath = @"F:\test.txt";  //ローカルファイルパス
PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//進行コールバックを設定します
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//リクエストを実行します
cosXml.PostObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		PostObjectResult result = cosResult as PostObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|srcPath|構築方法|COSにアップロードするためのローカルファイルの絶対パス|string|
|data|構築方法|COSにアップロードするためのbyte数|byte[]|
|progressCallback|SetCosProgressCallback|アップロード進行コールバックを設定します|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
PostObjectResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|eTag|string|オブジェクトのeTagを返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトの検索

##### 機能説明

バケットには指定されたオブジェクトが存在するかどうかを照合します（Head Object）。

#### 方法のプロトタイプ
```C#
HeadObjectResult HeadObject(HeadObjectRequest request);

void HeadObject(HeadObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	HeadObjectRequest request = new HeadObjectRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	HeadObjectResult result = cosXml.HeadObject(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
HeadObjectRequest request = new HeadObjectRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.HeadObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		HeadObjectResult result = cosResult as HeadObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
HeadObjectResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|eTag|string|オブジェクトのeTagを返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### ダウンロード対象

##### 機能説明

オブジェクトをローカルにダウンロードします（Get Object）。

#### 方法のプロトタイプ
```C#
GetObjectResult GetObject(GetObjectRequest request);

void GetObject(GetObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string localDir = @"F:\"；//ローカルの指定されたフォルダにダウンロードします
	string localFileName = "test.txt"; //ローカルに保存されたファイル名を指定します
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string localDir = @"F:\"；//ローカルの指定されたフォルダにダウンロードします
string localFileName = "test.txt"; //ローカルに保存されたファイル名を指定します
GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//進行コールバックを設定します
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//リクエストを実行します
cosXml.GetObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		GetObjectResult result = cosResult as GetObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|localDir|構築方法|オブジェクトをローカルにダウンロードして保存する絶対フォルダパス|string|
|localFileName|構築方法|オブジェクトをローカルにダウンロードして保存するファイル名|string|
|progressCallback|SetCosProgressCallback|ダウンロード進行コールバックを設定します|Callback.OnProgressCallback|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetObjectResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|eTag|string|オブジェクトのeTagを返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトのコピー

オブジェクトのコピー操作は、簡単なコピー（1M～5Gに適する）、パートコピー（5Gなどの大容量ファイルのコピーに適する）を含みます。

##### 簡単なコピー

あるオブジェクトを別のオブジェクトにコピーします（Put Object Copy）。

##### 方法のプロトタイプ
```C#
CopyObjectResult CopyObject(CopyObjectRequest request);

void CopyObject(CopyObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### リクエスト例
```C#
try
{
	string sourceAppid = "1253960454"; //アカウントappid
	string sourceBucket = "source-1253960454"; //"ソースオブジェクトが位置するバケット
	string sourceRegion = "ap-beijing"; //ソースオブジェクトのバケットが位置する地域
	string sourceKey = "test.txt"; //ソースオブジェクト鍵
	//ソースオブジェクトの属性を構築します
	COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "copy_test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	CopyObjectRequest request =  new CopyObjectRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//コピーソースを設定します
	request.SetCopySource(copySource);
	//コピーするか、それともアップデートするかを設定し、ここではコピーします
	request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
	//リクエストを実行します
	CopyObjectResult result = cosXml.CopyObject(request);
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

/**
//非同期方法
string sourceAppid = "1253960454"; //アカウントappid
string sourceBucket = "source-1253960454"; //"ソースオブジェクトが位置するバケット
string sourceRegion = "ap-beijing"; //ソースオブジェクトのバケットが位置する地域
string sourceKey = "test.txt"; //ソースオブジェクト鍵
//ソースオブジェクトの属性を構築します
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "copy_test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
CopyObjectRequest request =  new CopyObjectRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//コピーソースを設定します
request.SetCopySource(copySource);
//コピーするか、それともアップデートするかを設定し、ここではコピーします
request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
//リクエストを実行します
cosXml.CopyObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		CopyObjectResult result = cosResult as CopyObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|copySource|SetCopySource|コピーのデータソースパスの説明|CopySourceStruct|
|metaDataDirective|SetCopyMetaDataDirective|ソースファイルのメタデータをコピーするか、それともソースファイルのメタデータをアップデートするか|CosMetaDataDirective|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

##### 戻り結果の説明
CopyObjectResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|copyObject|[CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs)|正常にコピーされたオブジェクト情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

##### パートコピー

オブジェクトのパートコピー操作は以下を含みます：
1、マルチパートアップロードを初期化し、uploadIdを取得し、詳細については、[InitMultipartUpload](#INIT_MULIT_UPLOAD)を参照してください；
2、uploadIdに従ってパートコピーを実行します；
3、すべてのパートのコピーを完了させ、詳細については、[CompleteMultiUpload](#COMPLETE_MULIT_UPLOAD)を参照してください。

##### 方法のプロトタイプ
```C#
UploadPartCopyResult PartCopy(UploadPartCopyRequest request);

void PartCopy(UploadPartCopyRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

##### リクエスト例
```C#
try
{
	string sourceAppid = "1253960454"; //アカウントappid
	string sourceBucket = "source-1253960454"; //"ソースオブジェクトが位置するバケット
	string sourceRegion = "ap-beijing"; //ソースオブジェクトのバケットが位置する地域
	string sourceKey = "test.txt"; //ソースオブジェクト鍵
	//ソースオブジェクトの属性を構築します
	COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "copy_test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId = "1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 "； //マルチパートアップロードを初期化したuploadId
	int partNumber = 1; // partNumber >= 1
	UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, partNumber, uploadId);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//コピーソースを設定します
	request.SetCopySource(copySource);
	//パートのコピーを設定します
	request.SetCopyRange(0, 1024 * 1024);
	//リクエストを実行します
	UploadPartCopyResult result = cosXml.PartCopy(request);
	//リクエスト成功
	//返されたパートのeTagを取得し、CompleteMultiUploadに使用します
	string eTag = result.copyObject.eTag;
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

/**
//非同期方法
string sourceAppid = "1253960454"; //アカウントappid
string sourceBucket = "source-1253960454"; //"ソースオブジェクトが位置するバケット
string sourceRegion = "ap-beijing"; //ソースオブジェクトのバケットが位置する地域
string sourceKey = "test.txt"; //ソースオブジェクト鍵
//ソースオブジェクトの属性を構築します
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "copy_test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId = "1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 "； //マルチパートアップロードを初期化したuploadId
int partNumber = 1; // partNumber >= 1
UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, partNumber, uploadId);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//コピーソースを設定します
request.SetCopySource(copySource);
//コピーするか、それともアップデートするかを設定し、ここではコピーします
request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
//リクエストを実行します
cosXml.PartCopy(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		UploadPartCopyResult getObjectResult = result as UploadPartCopyResult;
		//返されたパートのeTagを取得し、CompleteMultiUploadに使用します
		string eTag = result.copyObject.eTag;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|partNumber|構築方法|パートの番号、partNumber >= 1|int|
|uploadId|構築方法|パートコピーのuploadIdの識別 |string|
|copySource|SetCopySource|コピーのデータソースパスの説明|CopySourceStruct|
|start|SetCopyRange|コピーされたコンテンツの範囲の開始位置|long|
|end|SetCopyRange|コピーされたコンテンツの範囲の終了位置|long|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

##### 戻り結果の説明
UploadPartCopyResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|copyObject|[CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs)|正常にコピーされたオブジェクトのパート情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトの削除

##### 機能説明

指定されたオブジェクトを削除します（Delete Object）。

#### 方法のプロトタイプ
```C#
DeleteObjectResult DeleteObject(DeleteObjectRequest request);

void DeleteObject(DeleteObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.DeleteObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		DeleteObjectResult getObjectResult = result as DeleteObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
DeleteObjectResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトの一括削除

##### 機能説明

指定されたバケット内の複数オブジェクトを削除します（Delete Multi Objects）。

#### 方法のプロトタイプ
```C#
DeleteMultiObjectResult DeleteMultiObjects(DeleteMultiObjectRequest request);

void DeleteMultiObjects(DeleteMultiObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//戻り結果の形式を設定します
	request.SetDeleteQuiet(false);
	//複数オブジェクトを削除します
	List<string> keys = new List<string>();
	keys.Add("test1.txt");
	keys.Add("test2.txt");
	request.SetObjectKeys(keys);
	//リクエストを実行します
	DeleteMultiObjectResult result = cosXml.DeleteMultiObjects(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//戻り結果の形式を設定します
request.SetDeleteQuiet(false);
//複数オブジェクトを削除します
List<string> keys = new List<string>();
keys.Add("test1.txt");
keys.Add("test2.txt");
request.SetObjectKeys(keys);

//リクエストを実行します
cosXml.DeleteMultiObjects(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		DeleteMultiObjectResult result = cosResult as DeleteMultiObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|quiet|SetDeleteQuiet|戻り結果一括アップロードモードを設定し、True：各keyの削除状況を返し、False：削除に失敗したkeyの状況だけを返します|bool|
|key|SetDeleteKey|COS上のオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)を削除する必要があります|string|
|versionId|SetDeleteKey|COS上のオブジェクトの指定されたバージョンを削除する必要があります|string|
|keys|SetObjectKeys|COS上のオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)の集合を削除する必要があります|`List<string>`|
|versionIdAndKey|SetObjectKeys|COS上のオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)と指定されたバージョンの集合を削除する必要があります|Dictionary<string, string>|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
DeleteMultiObjectResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|deleteResult|[DeleteResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/DeleteResult.cs)|オブジェクト一括削除情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトACLの設定

##### 機能説明

オブジェクトアクセス制御リスト（ACL）を設定します（Put Object ACL）。

#### 方法のプロトタイプ
```C#
PutObjectACLResult PutObjectACL(PutObjectACLRequest request);

void PutObjectACL(PutObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//プライベート読み書き権限を設定します 
	request.SetCosACL(CosACL.PRIVATE); 
	//アカウント1131975903に読み取り権限を付与します 
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount(); 
	readAccount.AddGrantAccount("1131975903", "1131975903"); 
	request.setXCosGrantRead(readAccount);
	//リクエストを実行します
	PutObjectACLResult result = cosXml.PutObjectACL(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//プライベート読み書き権限を設定します 
request.SetCosACL(CosACL.PRIVATE); 
//アカウント1131975903に読み取り権限を付与します 
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount(); 
readAccount.AddGrantAccount("1131975903", "1131975903"); 
request.setXCosGrantRead(readAccount);
//リクエストを実行します
cosXml.PutObjectACL(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		PutObjectACLResult result = cosResult as PutObjectACLResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|cosAcl|SetCosAcl|バケットのACL権限を設定します|string|
|grandtAccout|SetXCosGrantReadまたはSetXCosGrantWriteまたはSetXCosReadWrite|ユーザーに読み書き権限を付与します|GrantAccount|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
PutObjectACLResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

### オブジェクトACLの取得

##### 機能説明

オブジェクトアクセス制御リスト（ACL）を取得します（Get Object ACL）。

#### 方法のプロトタイプ
```C#
GetObjectACLResult GetObjectACL(GetObjectACLRequest request);

void GetObjectACL(GetObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例
```C#
try
{
	string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
	string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	GetObjectACLResult result = cosXml.GetObjectACL(request);
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

/**
//非同期方法
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.GetObjectACL(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		GetObjectACLResult result = cosResult as GetObjectACLResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//リクエスト失敗
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
});
*/
```

#### パラメータ説明
|パラメータ名|設定方法|説明|タイプ|
|-----|-----|-----|------|
| bucket|構築方法|バケット名、フォーマット：bucketname-appid|string|
|key|構築方法またはSetCosPath|COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)|string|
|signStartTimeSecond|SetSign|署名の有効期間の開始時間|long|
|durationSecond|SetSign|署名の有効期間の長さ|long|
|headerKeys|SetSign|署名のheaderを検証するかどうか|`List<string>`|
|queryParameterKeys|SetSign|署名のリクエストURL内の照合パラメータを検証するかどうか|`List<string>`|

#### 戻り結果の説明
GetObjectACLResultを介してリクエスト結果を返します。

|メンバー変数|タイプ|説明|
|-----|-----|----|
|httpCode|int|HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します|
|accessControlPolicy|[AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs)|オブジェクトのアクセス制御リスト情報を返します|

> 操作が失敗した場合は[CosClientException](#COS_CLIENT_EXCEPTION)または[CosServerException](#COS_SERVER_EXCEPTION)異常をスローします

## 高度なAPI 

### 高度なAPIによるファイルのアップロード（推奨）

**TransferManager**、**COSXMLUploadTask** は簡単なアップロードおよびマルチパートアップロードAPIの非同期リクエストをカプセル化します
```go
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string srcPath = @"F:\test.txt"; //ファイルのローカル位置
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, null, key)
{	
	//進行コールバック
	successCallback = delegate (CosResult cosResult)
	{
		Console.WriteLine(String.Format("progress ={0:##.##}%",completed * 100.0 / total));
	},
	//コールバック成功
	successCallback = delegate (CosResult cosResult)
	{
		COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = cosResult as COSXML.Transfer.COSXMLUploadTask.UploadTaskResult;
		Console.WriteLine(result.GetResultInfo());
	},
	//コールバック失敗
	failCallback = delegate (CosClientException clientEx, CosServerException serverEx)
	{
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	}
};
//アップロードソースを設定します
long offset = 0; //ソースファイルの0位置から開始します
long  sendContentLength  =  -1; //ファイル全体をアップロードします（または一部のコンテンツをアップロードし、sendContentLength > -1）
uploadTask.SetSrcPath(srcPath, offset, sendContentLength);
//リクエストを実行します
transferManager.Upload(uploadTask);
```

### 高度なAPIによるファイルのダウンロード（推奨）

**TransferManager**、**COSXMLDownloadTask**はダウンロードAPIの非同期リクエストをカプセル化します
```go
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string localDir = @"F:\"; //ファイルをローカルにダウンロードして保存するフォルダパス
string localFileNmae = "test.txt"; //ファイルをローカルにダウンロードするフォルダ名
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, null, key, localDir, localFileName)
{	
	//進行コールバック
	successCallback = delegate (CosResult cosResult)
	{
		Console.WriteLine(String.Format("progress ={0:##.##}%",completed * 100.0 / total));
	},
	//コールバック成功
	successCallback = delegate (CosResult cosResult)
	{
		COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = cosResult as COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult;
		Console.WriteLine(result.GetResultInfo());
	},
	//コールバック失敗
	failCallback = delegate (CosClientException clientEx, CosServerException serverEx)
	{
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	}
};

//リクエストを実行します
transferManager.Download(downloadTask);
```

### 高度なAPIによるファイルのコピー（推奨）

**TransferManager**、**COSXMLCopyTask**は簡単なコピーおよびパートコピーAPIの非同期リクエストをカプセル化します
```go
string sourceAppid = "1253960454"; //アカウントappid
string sourceBucket = "source-1253960454"; //"ソースオブジェクトが位置するバケット
string sourceRegion = "ap-beijing"; //ソースオブジェクトのバケットが位置する地域
string sourceKey = "test.txt"; //ソースオブジェクト鍵
//ソースオブジェクトの属性を構築します
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);
string bucket = "test-1253960454"; //バケット、フォーマット：bucketname-appid
string key = "copy_test.txt"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
COSXMLCopyTask copyTask = new COSXMLCopyTask(bucket, null, key, copySource)
{	
	//コールバック成功
	successCallback = delegate (CosResult cosResult)
	{
		COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = cosResult as COSXML.Transfer.COSXMLCopyTask.CopyTaskResult;
		Console.WriteLine(result.GetResultInfo());
	},
	//コールバック失敗
	failCallback = delegate (CosClientException clientEx, CosServerException serverEx)
	{
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	}
};
//リクエストを実行します
transferManager.Copy(copyTask);
```

## <span id="COS_EXCEPTION">SDK異常説明</span>

SDKの中で、APIを呼び出してCOSオブジェクトの操作に失敗した場合、CosXmlClientExceptionまたはCosXmlServiceException異常をスローします。

### <span id="COS_CLIENT_EXCEPTION"> [CosXmlClientException](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/CosException/CosClientException.cs) </span>

クライアント異常は、クライアントの原因でサーバーとの正常な対話を完了できないことによる失敗（例えば、クライアントがサーバーに接続できず、サーバーから返されたデータを解決できず、ローカルファイルの読み取りにIO異常が発生した）を指すために使用されます。
CosClientExceptionはSystem.ApplicationExceptionから統合され、使用方法はSystem.ApplicationExceptionと同じであり、同時に追加のメンバーerrorCodeを添加し、以下に示すとおりです：

|メンバー|説明|タイプ|
| ---- | ---- | ---- |
|errorCode|クライアントエラーコード、例えば、10000はパラメータ検証が失敗したことを表します|int|


### <span id="COS_SERVER_EXCEPTION"> [CosXmlServiceException](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/CosException/CosServerException.cs) </span>

CosServerExceptionサービス異常は、対話が正常に達成できるが、操作が失敗したシナリオを表すために使用されます。例えば、クライアントは存在しないバケットにアクセスし、存在しないファイルを削除し、ある操作を実行する権限がなく、サーバーに異常があるなどです。
CosServerExceptionは、サーバーから返されたステータスコード、requesttid、エラーの詳細などを含みます。異常をキャプチャした後、必要なトラブルシューティング要因を含む異常全体を印刷することをお勧めします。以下は、異常メンバー変数の説明です：

| メンバー   | 説明 | タイプ |
| ------------ | ---------------------------------------- | --------- |
| requestId    | リクエストIDであり、リクエストを表すために使用され、トラブルシューティングに非常に重要です。| string    |
| statusCode   | 応答のステータスコードであり、4xxはクライアントによるリクエストの失敗を指し、5xxはサーバー異常による失敗です。[COSエラー情報](https://cloud.tencent.com/document/product/436/7730)を参照してください。 | string    |
| errorCode | リクエストが失敗した時にボディにより返されたError Codeについて、[COSエラー情報](https://cloud.tencent.com/document/product/436/7730)を参照してください。| string |
| errorMessage | リクエストが失敗した時にボディにより返されたError Messageについて、[COSエラー情報](https://cloud.tencent.com/document/product/436/7730)を参照してください。| string |

