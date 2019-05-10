## 概要

このドキュメントでは、バケットの基本操作とアクセス制御リスト（ACL）に関連するAPI概要およびSDKサンプルコードを紹介します。

**基本操作**

| API                                                          | 操作名             | 操作説明                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | バケットリストの取得     | 指定されたアカウント内のすべてのバケットのリストを取得します     |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | バケットの作成         | 指定されたアカウントでバケットを作成します         |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | バケットおよびその権限の検索 | バケットが存在するかどうか、アクセスする権限があるかどうかを検索します |
| [GET Bucket location](https://cloud.tencent.com/document/product/436/8275) | バケット地域情報の取得 | バケットが位置する地域の情報を取得します           |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | バケットの削除         | 指定されたアカウント内の空きバケットを削除します         |

**アクセス制御リスト（ACL）**

| API                                                          | 操作名         | 操作説明              |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | バケットACLの設定 | バケットのACL構成を設定します |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | バケットACLの取得 | バケットのACL構成を取得します |

## 基本操作

### バケットリストの取得

##### 機能説明

指定されたアカウント内のすべてのバケットリスト（Bucket list）を取得するために使用されます。

#### 方法のプロトタイプ

```C#
GetServiceResult GetService(GetServiceRequest request);

void GetService(GetServiceRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```
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

| パラメータ名            | 設定方法 | 説明                            | タイプ           |
| ------------------- | -------- | ------------------------------- | -------------- |
| signStartTimeSecond | SetSign  | 署名の有効期間の開始時間              | long           |
| durationSecond      | SetSign  | 署名の有効期間の長さ                  | long           |
| headerKeys          | SetSign  | 署名のheaderを検証するかどうか            | `List<string>` |
| queryParameterKeys  | SetSign  | 署名のリクエストURL内の照合パラメータを検証するかどうか | `List<string>` |

#### 戻り結果の説明

GetServiceResultを介してリクエスト結果を返します。

| メンバー変数        | タイプ                                                         | 説明                                                     |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode         | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| listAllMyBuckets | [ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListAllMyBuckets.cs) | 指定されたアカウント内のバケットリストの情報を返します                         |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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

| パラメータ名            | 設定方法 | 説明                               | タイプ           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 構築方法 | バケット名、フォーマット：BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 署名の有効期間の開始時間                 | long           |
| durationSecond      | SetSign  | 署名の有効期間の長さ                     | long           |
| headerKeys          | SetSign  | 署名のheaderを検証するかどうか                | `List<string>` |
| queryParameterKeys  | SetSign  | 署名のリクエストURL内の照合パラメータを検証するかどうか    | `List<string>` |

#### 戻り結果の説明

PutBucketResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ | 説明                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code、［200，300）の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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

| パラメータ名            | 設定方法 | 説明                               | タイプ           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 構築方法 | バケット名、フォーマット：BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 署名の有効期間の開始時間                 | long           |
| durationSecond      | SetSign  | 署名の有効期間の長さ                     | long           |
| headerKeys          | SetSign  | 署名のheaderを検証するかどうか                | `List<string>` |
| queryParameterKeys  | SetSign  | 署名のリクエストURL内の照合パラメータを検証するかどうか    | `List<string>` |

#### 戻り結果の説明

GetBucketLocationResultを介してリクエスト結果を返します。

| メンバー変数           | タイプ                                                         | 説明                                                     |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode           | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| locationConstraint | [LocationConstraint](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LocationConstraint.cs) | バケットの地域情報を返します                                     |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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

| パラメータ名            | 設定方法 | 説明                               | タイプ           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 構築方法 | バケット名、フォーマット：BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 署名の有効期間の開始時間                 | long           |
| durationSecond      | SetSign  | 署名の有効期間の長さ                     | long           |
| headerKeys          | SetSign  | 署名のheaderを検証するかどうか                 | `List<string>` |
| queryParameterKeys  | SetSign  | 署名のリクエストURL内の照合パラメータを検証するかどうか      | `List<string>` |

#### 戻り結果の説明

DeleteBucketResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ | 説明                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code、［200，300）の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

## アクセス制御リスト

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
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
	PutBucketACLRequest request = new PutBucketACLRequest(bucket);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//プライベート読み書き権限を設定します
	request.SetCosACL(CosACL.PRIVATE);
	//アカウント1131975903に読み取り権限を付与します
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
	readAccount.AddGrantAccount("1131975903", "1131975903");
	request.SetXCosGrantRead(readAccount);
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
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
PutBucketACLRequest request = new PutBucketACLRequest(bucket);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//プライベート読み書き権限を設定します
request.SetCosACL(CosACL.PRIVATE);
//アカウント1131975903に読み取り権限を付与します
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
readAccount.AddGrantAccount("1131975903", "1131975903");
request.SetXCosGrantRead(readAccount);
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

| パラメータ名            | 設定方法                                                  | 説明                               | タイプ           |
| ------------------- | --------------------------------------------------------- | ---------------------------------- | -------------- |
| bucket              | 構築方法                                                  | バケット名、フォーマット：BucketName-APPID | string         |
| cosAcl              | SetCosAcl                                                 | バケットのACL権限を設定します              | string         |
| grandtAccout        | SetXCosGrantReadまたはSetXCosGrantWriteまたはSetXCosReadWrite | ユーザーに読み書き権限を付与します                   | GrantAccount   |
| signStartTimeSecond | SetSign                                                   | 署名の有効期間の開始時間                 | long           |
durationSecond      | SetSign                                                   | 署名の有効期間の長さ                     | long           |
| headerKeys          | SetSign                                                   | 署名のheaderを検証するかどうか                | `List<string>` |
| queryParameterKeys  | SetSign                                                   | 署名のリクエストURL内の照合パラメータを検証するかどうか    | `List<string>` |

#### 戻り結果の説明

PutBucketACLResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ | 説明                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code、［200，300）の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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

| パラメータ名            | 設定方法 | 説明                               | タイプ           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 構築方法 | バケット名、フォーマット：BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 署名の有効期間の開始時間                 | long           |
| durationSecond      | SetSign  | 署名の有効期間の長さ                     | long           |
| headerKeys          | SetSign  | 署名のheaderを検証するかどうか                | `List<string>` |
| queryParameterKeys  | SetSign  | 署名のリクエストURL内の照合パラメータを検証するかどうか    | `List<string>` |

#### 戻り結果の説明

GetBucketACLResultを介してリクエスト結果を返します。

| メンバー変数            | タイプ                                                         | 説明                                                     |
| ------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode            | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs) | バケットのアクセス制御リスト情報を返します                             |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

