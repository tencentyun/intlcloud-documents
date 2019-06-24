## 概要

このドキュメントでは、オブジェクトの簡単な操作、パート操作などの他の操作に関連するAPI概要およびSDKサンプルコードを紹介します。

**簡単な操作**

| API                                                          | 操作名         | 操作説明                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://cloud.tencent.com/document/product/436/7734) | オブジェクトリストの取得   | バケット内のオブジェクトリストを取得します                    |
| [PUT Object](https://cloud.tencent.com/document/product/436/7749) | オブジェクトのアップロード       | オブジェクト（ファイル/オブジェクト）をバケットにアップロードします     |
| [POST Object](https://cloud.tencent.com/document/product/436/14690) | フォームによるオブジェクトのアップロード   | フォームリクエストを使用してオブジェクトをアップロードします                      |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | オブジェクトのメタデータの取得 | オブジェクトのメタ情報を取得します                  |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | オブジェクトの取得       | オブジェクト（ファイル/オブジェクト）をローカルにダウンロードします        |
| [Options Object](https://cloud.tencent.com/document/product/436/8288) | プリフライトリクエストのクロスオリジン構成 | プリフライトリクエストを使用して、実際のクロスオリジンリクエストを送信できるかどうかを確認します  |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | オブジェクトコピーの設定   | ファイルをターゲットパスにコピーします                        |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | 単一オブジェクトの削除   | バケットで指定されたオブジェクト（ファイル/オブジェクト）を削除します |

**パート操作**

| API                                                          | 操作名         | 操作説明                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | マルチパートアップロードの照合   | 実行中のパートアップロードの情報を照合します         |
| [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746) | マルチパートアップロードの初期化 | マルチパートアップロードのアップロード操作を初期化します     |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | パートのアップロード       | ファイルをマルチパートアップロードします                         |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | パートのコピー       | 既存のオブジェクトを新しいオブジェクトのパートにコピーします             |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | アップロード済みパートの照合   | 特定のマルチパートアップロード操作でのアップロード済みパートを照合します   |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | マルチパートアップロードの完成   | ファイル全体のマルチパートアップロードを完成します               |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | マルチパートアップロードの終了   | 1つのマルチパートアップロード操作を終了し、アップロードされたパートを削除します |

**他の操作**

| API                                                          | 操作名       | 操作説明                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
|[POST Object restore](https://cloud.tencent.com/document/product/436/12633) | アーカイブオブジェクトの回復 | アーカイブタイプのオブジェクトを取り戻し、アクセスします                      |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | オブジェクトACLの設定 | バケットのオブジェクト（ファイル/オブジェクト）のACLを設定します |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | オブジェクトACLの取得 | オブジェクト（ファイル/オブジェクト）のACLを取得します           |

## 簡単な操作

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

/**
//非同期方法
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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

| パラメータ名            | 設定方法 | 説明                               | タイプ           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 構築方法 | バケット名、フォーマット：BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 署名の有効期間の開始時間                 | long           |
| durationSecond      | SetSign  | 署名の有効期間の長さ                     | long           |
| headerKeys          | SetSign  | 署名のheaderを検証するかどうか                | `List<string>` |
| queryParameterKeys  | SetSign  | 署名のリクエストURL内の照合パラメータを検証するかどうか    | `List<string>` |

#### 戻り結果の説明

GetBucketResultを介してリクエスト結果を返します。

| メンバー変数   | タイプ                                                         | 説明                                                      |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| httpCode   | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| listBucket | [ListBucket](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListBucket.cs) | バケットのオブジェクトリスト情報を返します                                  |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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

/**
//非同期方法
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string srcPath = @"F:\exampleobject";  //ローカルファイルの絶対パス
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

| パラメータ名            | 設定方法               | 説明                                                         | タイプ                        |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 構築方法               | バケット名、フォーマット：BucketName-APPID                           | string                      |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string                      |
| srcPath             | 構築方法               | COSにアップロードするためのローカルファイルの絶対パス                          | string                      |
| data                | 構築方法               | COSにアップロードするためのbyte数                                  | byte[]                      |
| progressCallback    | SetCosProgressCallback | アップロード進行コールバックを設定します                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                | 署名の有効期間の開始時間                                           | long                        |
| durationSecond      | SetSign                | 署名の有効期間の長さ                                               | long                        |
| headerKeys          | SetSign                | 署名のheaderを検証するかどうか                                           | `List<string>`              |
| queryParameterKeys  | SetSign                | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>`              |

#### 戻り結果の説明

PutObjectResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ   | 説明                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int    | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| eTag     | string | オブジェクトのeTagを返します                                          |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### フォームによるオブジェクトのアップロード

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
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string srcPath = @"F:\exampleobject"；//ローカルファイルの絶対パス
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string srcPath = @"F:\exampleobject";  //ローカルファイルの絶対パス
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

| パラメータ名            | 設定方法               | 説明                                                         | タイプ                        |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 構築方法               | バケット名、フォーマット：BucketName-APPID                           | string                      |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string                      |
| srcPath             | 構築方法               | COSにアップロードするためのローカルファイルの絶対パス                          | string                      |
| data                | 構築方法               | COSにアップロードするためのbyte数                                  | byte[]                      |
| progressCallback    | SetCosProgressCallback | アップロード進行コールバックを設定します                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                | 署名の有効期間の開始時間                                           | long                        |
| durationSecond      | SetSign                | 署名の有効期間の長さ                                               | long                        |
| headerKeys          | SetSign                | 署名のheaderを検証するかどうか                                          | `List<string>`              |
| queryParameterKeys  | SetSign                | 署名のリクエストURL内の照合パラメータを検証するかどうか                               | `List<string>`              |

#### 戻り結果の説明

PostObjectResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ   | 説明                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int    | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| eTag     | string | オブジェクトのeTagを返します                                          |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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

| パラメータ名            | 設定方法              | 説明                                                         | タイプ           |
| ------------------- | --------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法              | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| signStartTimeSecond | SetSign               | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign               | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign               | 署名のheaderを検証するかどうか                                          | `List<string>` |
| queryParameterKeys  | SetSign               | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>` |

#### 戻り結果の説明

HeadObjectResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ   | 説明                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int    | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| eTag     | string | オブジェクトのeTagを返します                                          |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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

/**
//非同期方法
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

| パラメータ名            | 設定方法               | 説明                                                         | タイプ                        |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 構築方法               | バケット名、フォーマット：BucketName-APPID                           | string                      |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string                      |
| localDir            | 構築方法               | オブジェクトをローカルにダウンロードして保存する絶対フォルダパス                           | string                      |
| localFileName       | 構築方法               | オブジェクトをローカルにダウンロードして保存するファイル名                                   | string                      |
| progressCallback    | SetCosProgressCallback | ダウンロード進行コールバックを設定します                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                | 署名の有効期間の開始時間                                           | long                        |
| durationSecond      | SetSign                | 署名の有効期間の長さ                                               | long                        |
| headerKeys          | SetSign                | 署名のheaderを検証するかどうか                                           | `List<string>`              |
| queryParameterKeys  | SetSign                | 署名のリクエストURL内の照合パラメータを検証するかどうか                                | `List<string>`              |

#### 戻り結果の説明

GetObjectResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ   | 説明                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int    | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| eTag     | string | オブジェクトのeTagを返します                                            |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### 簡単なコピー

あるオブジェクトを別のオブジェクトにコピーします（Put Object Copy）。

#### 方法のプロトタイプ

```C#
CopyObjectResult CopyObject(CopyObjectRequest request);

void CopyObject(CopyObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string sourceAppid = "1253960454"; //アカウントappid
	string sourceBucket = "source-1253960454"; //"ソースオブジェクトが位置するバケット
	string sourceRegion = "ap-beijing"; //ソースオブジェクトのバケットが位置する地域
	string sourceKey = "exampleobject"; //ソースオブジェクト鍵
	//ソースオブジェクトの属性を構築します
	COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "copy_exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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
string sourceKey = "exampleobject"; //ソースオブジェクト鍵
//ソースオブジェクトの属性を構築します
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "copy_exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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

| パラメータ名            | 設定方法                 | 説明                                                         | タイプ                 |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket              | 構築方法                 | バケット名、フォーマット：BucketName-APPID                           | string               |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string               |
| copySource          | SetCopySource            | コピーのデータソースパスの説明                                         | CopySourceStruct     |
| metaDataDirective   | SetCopyMetaDataDirective | ソースファイルのメタデータをコピーするか、それともソースファイルのメタデータをアップデートするか                 | CosMetaDataDirective |
| signStartTimeSecond | SetSign                  | 署名の有効期間の開始時間                                           | long                 |
| durationSecond      | SetSign                  | 署名の有効期間の長さ                                               | long                 |
| headerKeys          | SetSign                  | 署名のheaderを検証するかどうか                                          | `List<string>`       |
| queryParameterKeys  | SetSign                  | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>`       |

#### 戻り結果の説明

CopyObjectResultを介してリクエスト結果を返します。

| メンバー変数   | タイプ                                                         | 説明                                                       |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode   | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs) | 正常にコピーされたオブジェクト情報を返します                                     |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### オプションリクエスト

##### 機能説明

プリフライトリクエストのクロスオリジン構成を取得します（Options Object）。

#### 方法のプロトタイプ

```C#
OptionObjectResult OptionObject(OptionObjectRequest request);

void OptionObject(OptionObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string origin = "http://cloud.tencent.com";
	string accessMthod = "PUT";
	OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	OptionObjectResult result = cosResult as OptionObjectResult;
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string origin = "http://cloud.tencent.com";
string accessMthod = "PUT";
OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.DeleteObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		OptionObjectResult result = cosResult as OptionObjectResult;
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

| パラメータ名            | 設定方法                           | 説明                                                         | タイプ           |
| ------------------- | ---------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法                           | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath             | COSにストレージされたオブジェクトtの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| origin              | 構築方法またはSetOrigin              | シミュレートクロスオリジンアクセスのリクエストソースドメイン名                                   | string         |
| accessMthod         | 構築方法またはSetAccessControlMethod | シミュレートクロスオリジンアクセスのHTTPリクエスト方法                                 | string         |
| signStartTimeSecond | SetSign                            | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign                            | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign                            | 署名のheaderを検証するかどうか                                           | `List<string>` |
| queryParameterKeys  | SetSign                            | 署名のリクエストURL内の照合パラメータを検証するかどうか                                | `List<string>` |

#### 戻り結果の説明

DeleteObjectResultを介してリクエスト結果を返します。

| メンバー変数                        | タイプ           | 説明                                                       |
| ------------------------------- | -------------- | ---------------------------------------------------------- |
| httpCode                        | int            | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| accessControlAllowHeaders       | `List<string>` | クロスオリジンアクセスで許可されるリクエストヘッダー                                     |
| accessControlAllowMethods       | `List<string>` | クロスオリジンアクセスで許可されるHTTPリクエスト方法                               |
| accessControlAllowExposeHeaders | `List<string>` | クロスオリジンアクセスで許可されるカスタムリクエストヘッダー                                     |
| accessControlMaxAge             | long           | オプションリクエストの結果を取得する有効期間                               |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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

/**
//非同期方法
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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

| パラメータ名            | 設定方法               | 説明                                                         | タイプ           |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法               | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| signStartTimeSecond | SetSign                | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign                | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign                | 署名のheaderを検証するかどうか                                          | `List<string>` |
| queryParameterKeys  | SetSign                | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>` |

#### 戻り結果の説明

DeleteObjectResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ | 説明                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

## パート操作

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
	string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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
string bucket = "examplebucket-1250000000"; //フォーマット：BucketName-APPID
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

| パラメータ名            | 設定方法 | 説明                               | タイプ           |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket              | 構築方法 | バケット名、フォーマット：BucketName-APPID | string         |
| signStartTimeSecond | SetSign  | 署名の有効期間の開始時間                 | long           |
| durationSecond      | SetSign  | 署名の有効期間の長さ                     | long           |
| headerKeys          | SetSign  | 署名のheaderを検証するかどうか                | `List<string>` |
| queryParameterKeys  | SetSign  | 署名のリクエストURL内の照合パラメータを検証するかどうか    | `List<string>` |

#### 戻り結果の説明

ListMultiUploadsResultを介してリクエスト結果を返します。

| メンバー変数             | タイプ                                                         | 説明                                                       |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode             | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| listMultipartUploads | [ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListMultipartUploads.cs) | バケット内のすべての実行中のパートアップロードの情報を返します                   |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### オブジェクトのマルチパートアップロード

オブジェクトのマルチパートアップロードに含まれる操作：

- オブジェクトのマルチパートアップロード：マルチパートアップロードを初期化し、パートをアップロードし、すべてのパートのアップロードを完了させます。
- マルチパートアップロードの再開：アップロードされたパートを照合し、パートをアップロードし、すべてのパートのアップロードを完了させます。
- アップロードされたパートを削除します。

### <span id = "INIT_MULIT_UPLOAD">マルチパートアップロードの初期化</span>

##### 機能説明

マルチパートアップロードを初期化し、対応するuploadIdを取得します（Initiate Multipart Upload）。

#### 方法のプロトタイプ

```C#
InitMultipartUploadResult InitMultipartUpload(InitMultipartUploadRequest request);

void InitMultipartUpload(InitMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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

| パラメータ名            | 設定方法               | 説明                                                         | タイプ           |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法               | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| signStartTimeSecond | SetSign                | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign                | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign                | 署名のheaderを検証するかどうか                                          | `List<string>` |
| queryParameterKeys  | SetSign                | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>` |

#### 戻り結果の説明

InitMultipartUploadResultを介してリクエスト結果を返します。

| メンバー変数            | タイプ                                                         | 説明                                                       |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode            | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| initMultipartUpload | [InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/InitiateMultipartUpload.cs) | オブジェクトのマルチパートアップロードを初期化した後に得られたuploadIdを返します                        |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### <span id = "LIST_MULIT_UPLOAD">アップロードされたパートの照合</span>

##### 機能説明

指定uploadIdのアップロードされたパートを照合します（List Parts）。

#### 方法のプロトタイプ

```C#
ListPartsResult ListParts(ListPartsRequest request);

void ListParts(ListPartsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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

| パラメータ名            | 設定方法                | 説明                                                         | タイプ           |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法                | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath  | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| uploadId            | 構築方法またはSetUploadId | 指定されたマルチパートアップロードのuploadIdの識別                                  | string         |
| signStartTimeSecond | SetSign                 | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign                 | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign                 | 署名のheaderを検証するかどうか                                          | `List<string>` |
| queryParameterKeys  | SetSign                 | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>` |

#### 戻り結果の説明

ListPartsResultを介してリクエスト結果を返します。

| メンバー変数  | タイプ                                                         | 説明                                                       |
| --------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode  | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| listParts | [ListParts](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListParts.cs) | 指定されたuploadIdのマルチパートアップロードにおけるアップロードされたパートの情報を返します               |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### <span id = "MULIT_UPLOAD_PART">パートのアップロード</span>

パートをアップロードします（Upload Part）。

#### 方法のプロトタイプ

```C#
UploadPartResult UploadPart(UploadPartRequest request);

void UploadPart(UploadPartRequest, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
	int partNumber = 1; //パートの番号、1からの自然数にする必要があります
	string srcPath = @"F:\exampleobject"; //ローカルファイルの絶対パス
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
int partNumber = 1; //パートの番号、1からの自然数にする必要があります
string srcPath = @"F:\exampleobject"; //ローカルファイルの絶対パス
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

| パラメータ名            | 設定方法                  | 説明                                                         | タイプ                        |
| ------------------- | ------------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket              | 構築方法                  | バケット名、フォーマット：BucketName-APPID                           | string                      |
| key                 | 構築方法またはSetCosPath  | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string                      |
| uploadId            | 構築方法またはSetUploadId | 指定されたマルチパートアップロードのuploadIdの識別                                  | string                      |
| partNumber          | 構築方法またはSetPartNumber | 指定されたパートの番号を識別し、>=1でなければなりません                               | int                         |
| srcPath             | 構築方法                  | COSにアップロードするためのローカルファイルの絶対パス                          | string                      |
| data                | 構築方法                  | COSにアップロードするためのbyte数                                  | byte[]                      |
| progressCallback    | SetCosProgressCallback    | アップロード進行コールバックを設定します                                             | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign                   | 署名の有効期間の開始時間                                           | long                        |
| durationSecond      | SetSign                   | 署名の有効期間の長さ                                               | long                        |
| headerKeys          | SetSign                   | 署名のheaderを検証するかどうか                                          | `List<string>`              |
| queryParameterKeys  | SetSign                   | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>`              |

#### 戻り結果の説明

UploadPartResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ   | 説明                                                       |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int    | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| eTag     | string | パートでアップロードされたオブジェクトのeTagを返します                                            |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### <span id = "COMPLETE_MULIT_UPLOAD"> すべてのパートのアップロードの完了</span>

##### 機能説明

すべてのマルチパートアップロードの完了を実現します（Complete Multipart Upload）。

#### 方法のプロトタイプ

```C#
CompleteMultipartUploadResult CompleteMultiUpload(CompleteMultipartUploadRequest request);

void CompleteMultiUpload(CompleteMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
	CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, key, uploadId);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//partNumberに従ってアップロードされたパートを昇順に設定する必要があります
	request.SetPartNumberAndETag(1, "partNumber1 eTag");
	//リクエストを実行します
	CompleteMultipartUploadResult result = cosXml.CompleteMultiUpload(request);
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, key, uploadId);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//partNumberに従ってアップロードされたパートを昇順に設定する必要があります
request.SetPartNumberAndETag(1, "partNumber1 eTag");
//リクエストを実行します
cosXml.CompleteMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		CompleteMultipartUploadResult result = result as CompleteMultipartUploadResult;
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

| パラメータ名            | 設定方法                | 説明                                                         | タイプ                       |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------------------- |
| bucket              | 構築方法                | バケット名、フォーマット：BucketName-APPID                           | string                     |
| key                 | 構築方法またはSetCosPath  | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string                     |
| uploadId            | 構築方法またはSetUploadId | 指定されたマルチパートアップロードのuploadIdの識別                                  | string                     |
| partNumber          | SetPartNumberAndETag    | 指定されたパートの番号、>=1でなければなりません                              | int                        |
| eTag                | SetPartNumberAndETag    | 指定されたパートがアップロードされた後に返されたeTagの識別                             | string                     |
| partNumberAndETags  | SetPartNumberAndETag    | パートの番号とパートがアップロードされた後に返されたeTagの識別                            | `Dictionary<int, string> ` |
| signStartTimeSecond | SetSign                 | 署名の有効期間の開始時間                                           | long                       |
| durationSecond      | SetSign                 | 署名の有効期間の長さ                                               | long                       |
| headerKeys          | SetSign                 | 署名のheaderを検証するかどうか                                          | `List<string>`             |
| queryParameterKeys  | SetSign                 | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>`             |

#### 戻り結果の説明

CompleteMultipartUploadResultを介してリクエスト結果を返します。

| メンバー変数       | タイプ                                                         | 説明                                                       |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode       | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| CompleteResult | [CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CompleteResult.cs) | すべてのパートのアップロード成功情報を返します                                 |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

### <span id = "ABORT_MULIT_UPLOAD"> アップロードされたパートの削除 </span>

##### 機能説明

1つのマルチパートアップロードを破棄し、かつアップロードされたパートを削除します（Abort Multipart Upload）。

#### 方法のプロトタイプ

```C#
AbortMultipartUploadResult AbortMultiUpload(AbortMultipartUploadRequest request);

void AbortMultiUpload(AbortMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
	AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//リクエストを実行します
	AbortMultipartUploadResult result = cosXml.AbortMultiUpload(request);
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
string uploadId ="xxxxxxxx"; //マルチパートアップロードを初期化した後に返されたuploadId
AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//リクエストを実行します
cosXml.AbortMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		AbortMultipartUploadResult result = result as AbortMultipartUploadResult;
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

| パラメータ名            | 設定方法                | 説明                                                         | タイプ           |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法                | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath  | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| uploadId            | 構築方法またはSetUploadId | 指定されたマルチパートアップロードのuploadIdの識別                                  | string         |
| signStartTimeSecond | SetSign                 | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign                 | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign                 | 署名のheaderを検証するかどうか                                          | `List<string>` |
| queryParameterKeys  | SetSign                 | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>` |

#### 戻り結果の説明

AbortMultipartUploadResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ | 説明                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

## 他の操作

### アーカイブされたオブジェクトの回復 

##### 機能説明

アーカイブされたオブジェクトを回復します（POST Object restore）。

#### 方法のプロトタイプ

```C#
RestoreObjectResult RestoreObject(RestoreObjectRequest request);

void RestoreObject(RestoreObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

####　リクエスト例

```C#
try
{
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//回復時間
	request.SetExpireDays(3);
	request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);

	//リクエストを実行します
	RestoreObjectResult result = cosXml.RestoreObject(request);
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//回復時間
request.SetExpireDays(3);
request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);
//リクエストを実行します
cosXml.RestoreObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//リクエスト成功
		RestoreObjectResult result = cosResult as RestoreObjectResult;
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

| パラメータ名            | 設定方法               | 説明                                                         | タイプ                  |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------- |
| bucket              | 構築方法               | バケット名、フォーマット：BucketName-APPID                           | string                |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string                |
| days                | SetExpireDays          | 一時コピーの有効期間を設定します                                       | int                   |
| tier                | SetTier                | データを回復する時、Tierは、CASがサポートするExpedited、Standard、Bulkの3つの回復タイプに指定できます | RestoreConfigure.Tier |
| signStartTimeSecond | SetSign                | 署名の有効期間の開始時間                                           | long                  |
| durationSecond      | SetSign                | 署名の有効期間の長さ                                               | long                  |
| headerKeys          | SetSign                | 署名のheaderを検証するかどうか                                          | `List<string>`        |
| queryParameterKeys  | SetSign                | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>`        |

#### 戻り結果の説明

RestoreObjectResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ | 説明                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
	PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
	//署名の有効期間を設定します
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//プライベート読み書き権限を設定します 
	request.SetCosACL(CosACL.PRIVATE); 
	//アカウント1131975903に読み取り権限を付与します 
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount(); 
	readAccount.AddGrantAccount("1131975903", "1131975903"); 
	request.SetXCosGrantRead(readAccount);
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
//署名の有効期間を設定します
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//プライベート読み書き権限を設定します 
request.SetCosACL(CosACL.PRIVATE); 
//アカウント1131975903に読み取り権限を付与します 
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount(); 
readAccount.AddGrantAccount("1131975903", "1131975903"); 
request.SetXCosGrantRead(readAccount);
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

| パラメータ名            | 設定方法                                                  | 説明                                                         | タイプ           |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法                                                  | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath                                    | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| cosAcl              | SetCosAcl                                                 | バケットのACL権限を設定します                                          | string         |
| grandtAccout        | SetXCosGrantReadまたはSetXCosGrantWriteまたはSetXCosReadWrite | ユーザーに読み書き権限を付与します                                             | GrantAccount   |
| signStartTimeSecond | SetSign                                                   | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign                                                   | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign                                                   | 署名のheaderを検証するかどうか                                          | `List<string>` |
| queryParameterKeys  | SetSign                                                   | 署名のリクエストURL内の照合パラメータを検証するかどうか                               | `List<string>` |

#### 戻り結果の説明

PutObjectACLResultを介してリクエスト結果を返します。

| メンバー変数 | タイプ | 説明                                                       |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

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
	string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
	string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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
string bucket = "examplebucket-1250000000"; //バケット、フォーマット：BucketName-APPID
string key = "exampleobject"; //バケット内のオブジェクトの位置、オブジェクト鍵と呼ばれます
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

| パラメータ名            | 設定方法               | 説明                                                         | タイプ           |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket              | 構築方法               | バケット名、フォーマット：BucketName-APPID                           | string         |
| key                 | 構築方法またはSetCosPath | COSにストレージされたオブジェクトの[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324) | string         |
| signStartTimeSecond | SetSign                | 署名の有効期間の開始時間                                           | long           |
| durationSecond      | SetSign                | 署名の有効期間の長さ                                               | long           |
| headerKeys          | SetSign                | 署名のheaderを検証するかどうか                                          | `List<string>` |
| queryParameterKeys  | SetSign                | 署名のリクエストURL内の照合パラメータを検証するかどうか                              | `List<string>` |

#### 戻り結果の説明

GetObjectACLResultを介してリクエスト結果を返します。

| メンバー変数            | タイプ                                                         | 説明                                                       |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode            | int                                                          | HTTP Code、[200，300)の場合は操作が成功したことを示し、そうでない場合は操作が失敗したことを示します |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs) | オブジェクトのアクセス制御リスト情報を返します                               |

> ?操作が失敗すると、システムは、[CosClientException](https://cloud.tencent.com/document/product/436/32874#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8)または[CosServerException](https://cloud.tencent.com/document/product/436/32874#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8)異常をスローします。

