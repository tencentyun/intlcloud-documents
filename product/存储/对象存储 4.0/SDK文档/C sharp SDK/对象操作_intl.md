## Introduction

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations and other operations on objects.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Gets the object list | Gets the list of objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploads an object | Uploads an object (file) to the bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploads an object using a form | Uploads an object using the form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Gets object metadata | Gets the meta information of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Gets an object | Downloads an object (file) locally |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | CORS configuration for a pre-flight request | You can initiate a pre-flight request to determine whether a real request for COS can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Sets object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deletes a single object | Deletes the specified object in the bucket |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Queries multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializes multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploads parts | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copies a part | Copies an existing object to a part of a new object |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Queries uploaded parts | Queries the uploaded parts in the specific multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completes multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Terminates multipart upload | Terminates a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restores an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Sets the object ACL | Sets an ACL for an object (file) in the bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Gets the object ACL | Gets the ACL of an object (file) |

## Simple Operations

### Get the object list

#### Feature

This API (Object List) is used to get all objects in the specified bucket.

#### Method prototype

```C#
GetBucketResult GetBucket(GetBucketRequest request);

void GetBucket(GetBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	GetBucketRequest request = new GetBucketRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	GetBucketResult result = cosXml.GetBucket(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
GetBucketRequest request = new GetBucketRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		GetBucketResult result = cosResult as GetBucketResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through GetBucketResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listBucket | [ListBucket](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListBucket.cs) | The list of objects in a bucket is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Upload an object using simple upload

#### Feature

This API (Put Object) is used to upload an object to the specified bucket.

#### Method prototype

```C#
PutObjectResult PutObject(PutObjectRequest request);

void PutObject(PutObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string srcPath = @"F:\exampleobject"；//Absolute path to the local file
	PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set progress callback
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//Execute the request
	PutObjectResult result = cosXml.PutObject(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string srcPath = @"F:\exampleobject";  //Absolute path to the local file
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set progress callback
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//Execute the request
cosXml.PutObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		PutObjectResult result = cosResult as PutObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| srcPath | Construction method | Absolute path to the local file uploaded to COS | string |
| data | Construction method | The array of bytes of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through PutObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | The eTag of an object is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Upload an object using a form

#### Feature

This API (Post Object) is used to upload an object using a form.

#### Method prototype

```C#
PostObjectResult PostObject(PostObjectRequest request);

void PostObject(PostObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string srcPath = @"F:\exampleobject"；//Absolute path to the local file
	PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set progress callback
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//Execute the request
	PostObjectResult result = cosXml.PostObject(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string srcPath = @"F:\exampleobject";  //Absolute path to the local file
PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set progress callback
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//Execute the request
cosXml.PostObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		PostObjectResult result = cosResult as PostObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| srcPath | Construction method | Absolute path to the local file uploaded to COS | string |
| data | Construction method | The array of bytes of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through PostObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | The eTag of an object is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Search for an object

#### Feature

This API (Head Object) is used to query whether the specified object exists in the bucket.

#### Method prototype

```C#
HeadObjectResult HeadObject(HeadObjectRequest request);

void HeadObject(HeadObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	HeadObjectRequest request = new HeadObjectRequest(bucket, key);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	HeadObjectResult result = cosXml.HeadObject(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
HeadObjectRequest request = new HeadObjectRequest(bucket, key);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.HeadObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		HeadObjectResult result = cosResult as HeadObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through HeadObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | The eTag of an object is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Download an object

#### Feature

This API (Get Object) is used to download an object locally.

#### Method prototype

```C#
GetObjectResult GetObject(GetObjectRequest request);

void GetObject(GetObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string localDir = @"F:\"；//Download to the specified local folder
	string localFileName = "exampleobject"; //Specify the name of the file stored locally
	GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set progress callback
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
	});
	//Execute the request
	GetObjectResult result = cosXml.GetObject(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
 	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string localDir = @"F:\"；//Download to the specified local folder
string localFileName = "exampleobject"; //Specify the name of the file stored locally
GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set progress callback
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
});
//Execute the request
cosXml.GetObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		GetObjectResult result = cosResult as GetObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| localDir | Construction method | The absolute path to the folder where the file is downloaded and stored locally | string |
| localDir | Construction method | The name of the file downloaded and stored locally | string |
| progressCallback    | SetCosProgressCallback | Sets the callback for download progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through GetObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | The eTag of an object is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Simple copy

This API (Put Object Copy) is used to copy an object to another.

#### Method prototype

```C#
CopyObjectResult CopyObject(CopyObjectRequest request);

void CopyObject(CopyObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string sourceAppid = "1253960454"; //Account APPID
	string sourceBucket = "source-1253960454"; //"The bucket of the source object
	string sourceRegion = "ap-beijing"; //The region where the bucket of the source object resides
	string sourceKey = "exampleobject"; //Source ObjectKey
	//Construct source object attributes
	COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "copy_exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	CopyObjectRequest request =  new CopyObjectRequest(bucket, key);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set the copy source
	request.SetCopySource(copySource);
	//Set whether to copy or update. Copy is used here.
	request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
	//Execute the request
	CopyObjectResult result = cosXml.CopyObject(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string sourceAppid = "1253960454"; //Account APPID
string sourceBucket = "source-1253960454"; //"The bucket of the source object
string sourceRegion = "ap-beijing"; //The region where the bucket of the source object resides
string sourceKey = "exampleobject"; //Source ObjectKey
//Construct source object attributes
COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "copy_exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
CopyObjectRequest request =  new CopyObjectRequest(bucket, key);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set the copy source
request.SetCopySource(copySource);
//Set whether to copy or update. Copy is used here.
request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
//Execute the request
cosXml.CopyObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		CopyObjectResult result = cosResult as CopyObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| copySource | SetCopySource | Describes the source path of the copied data | CopySourceStruct |
| metaDataDirective | SetCopyMetaDataDirective | Indicates whether to copy or update the metadata of the source file | CosMetaDataDirective |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs) | The information of the object copied successfully is returned. |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Options request

#### Feature

This API (Options Object) is used to get the CORS configuration for a pre-flight request.

#### Method prototype

```C#
OptionObjectResult OptionObject(OptionObjectRequest request);

void OptionObject(OptionObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string origin = "http://cloud.tencent.com";
	string accessMthod = "PUT";
	OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	OptionObjectResult result = cosResult as OptionObjectResult;
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string origin = "http://cloud.tencent.com";
string accessMthod = "PUT";
OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.DeleteObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		OptionObjectResult result = cosResult as OptionObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| origin | Construction method or SetOrigin | Simulates the origin from which the request for cross-origin access is sent | string |
| accessMthod | Construction method or SetAccessControlMethod | Simulates the HTTP method of the request for cross-origin access | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| ------------------------------- | -------------- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlAllowHeaders | `List<string>` | Allowed headers of the request for CORS |
| accessControlAllowMethods | `List<string>` | Allowed HTTP methods of the request for cross-origin access |
| accessControlAllowExposeHeaders | `List<string>` | Allowed custom headers of the request for cross-domain access |
| accessControlMaxAge | long | The validity period of the results obtained by OPTIONS |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Delete an object

#### Feature

This API (Delete Object) is used to delete the specified object.

#### Method prototype

```C#
DeleteObjectResult DeleteObject(DeleteObjectRequest request);

void DeleteObject(DeleteObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	DeleteObjectResult result = cosXml.DeleteObject(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.DeleteObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		DeleteObjectResult getObjectResult = result as DeleteObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS. | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

## Multipart Operations

### Query multipart upload

#### Feature

This API (List Multipart Uploads) is used to query in-progress multipart uploads in the specified bucket.

#### Method prototype

```C#
ListMultiUploadsResult ListMultiUploads(ListMultiUploadsRequest request);

void ListMultiUploads(ListMultiUploadsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	ListMultiUploadsResult result = cosXml.ListMultiUploads(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.ListMultiUploads(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		ListMultiUploadsResult result = cosResult as ListMultiUploadsResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through ListMultiUploadsResult.

| Member Variable | Type | Description |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listMultipartUploads | [ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListMultipartUploads.cs) | The information of all in-progress multipart uploads in the bucket is returned. |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Upload an object using multipart upload

This includes the following operations:

- Upload an object in multiple parts: Initialize multipart upload, upload parts, and complete the upload of all parts.
- Resume multipart upload: Query the uploaded parts, upload parts, and complete the upload of all parts.
- Delete the uploaded parts.

### <span id = "INIT_MULIT_UPLOAD">Initialize multipart upload</span>

#### Feature

This API (Initiate Multipart Upload) is used to initialize multipart upload and get the corresponding uploadId.

#### Method prototype

```C#
InitMultipartUploadResult InitMultipartUpload(InitMultipartUploadRequest request);

void InitMultipartUpload(InitMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
	//Request successful
	string uploadId = result.initMultipartUpload.uploadId; //The uploadId required for the subsequent multipart uploads
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.InitMultipartUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		InitMultipartUploadResult result = cosResult as InitMultipartUploadResult;
		string uploadId = result.initMultipartUpload.uploadId; //The uploadId required for the subsequent multipart uploads
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS. | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through InitMultipartUploadResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| initMultipartUpload | [InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/InitiateMultipartUpload.cs) | The object's uploadId is returned when multipart upload is initialized |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### <span id = "LIST_MULIT_UPLOAD">Query uploaded parts</span>

#### Feature

This API (List Parts) is used to query the parts uploaded to the specified uploadId.

#### Method prototype

```C#
ListPartsResult ListParts(ListPartsRequest request);

void ListParts(ListPartsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
	ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	ListPartsResult result = cosXml.ListParts(request);
	//Request successful
	//List uploaded parts
	List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.ListParts(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		ListPartsResult result = cosResult as ListPartsResult;
		//List uploaded parts
		List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	 {	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| uploadId | Construction method or SetUploadId | Identifies the specified uploadId for multipart upload | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through ListPartsResult.

| Member Variable | Type | Description |
| --------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listParts | [ListParts](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListParts.cs) | The information of the parts uploaded to the specified uploadId in a multipart upload is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### <span id = "MULIT_UPLOAD_PART">Upload a part</span>

This API (Upload Part) is used to upload a part.

#### Method prototype

```C#
UploadPartResult UploadPart(UploadPartRequest request);

void UploadPart(UploadPartRequest, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
	int partNumber = 1; //Part No., which is increased by an increment of 1.
	string srcPath = @"F:\exampleobject"; //Absolute path to the local file
	UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, uploadId, srcPath);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set progress callback
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {0:##.##}%",  completed * 100.0 / total));
	});
	//Execute the request
	UploadPartResult result = cosXml.UploadPart(request);
	//Request successful
	//Get the eTag of the returned part for subsequent ompleteMultiUploads.
	string eTag = result.eTag;
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
int partNumber = 1; //Part No., which is increased by an increment of 1.
string srcPath = @"F:\exampleobject"; //Absolute path to the local file
UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, uploadId, srcPath);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set progress callback
request.SetCosProgressCallback(delegate(long completed, long total)
{
	Console.WriteLine(String.Format("progress = {0:##.##}%",  completed * 100.0 / total));
});
//Execute the request
cosXml.UploadPart(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		UploadPartResult result = cosResult as UploadPartResult;
		//Get the eTag returned when the part is uploaded for subsequent ompleteMultiUploads.
		string eTag = result.eTag;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| uploadId | Construction method or SetUploadId | Identifies the specified uploadId for multipart upload | string |
| partNumber | Construction method or SetPartNumber | Identifies the number of the specified part, which should be ≥ 1. | int |
| srcPath | Construction method | Absolute path to the local file uploaded to COS | string |
| data | Construction method | The array of bytes of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through UploadPartResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | The eTag of an object uploaded using a part is returned |

> [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### <span id = "COMPLETE_MULIT_UPLOAD">Complete the upload of all parts</span>

#### Feature

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Method prototype

```C#
CompleteMultipartUploadResult CompleteMultiUpload(CompleteMultipartUploadRequest request);

void CompleteMultiUpload(CompleteMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
	CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, key, uploadId);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set the number of each uploaded part in order, which is incremented by partNumber.
	request.SetPartNumberAndETag(1, "partNumber1 eTag");
	//Execute the request
	CompleteMultipartUploadResult result = cosXml.CompleteMultiUpload(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, key, uploadId);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set the number of each uploaded part in order, which is incremented by partNumber.
request.SetPartNumberAndETag(1, "partNumber1 eTag");
//Execute the request
cosXml.CompleteMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		CompleteMultipartUploadResult result = result as CompleteMultipartUploadResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
   {	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| uploadId | Construction method or SetUploadId | Identifies the specified uploadId for multipart upload | string |
| partNumber | SetPartNumberAndETag | Identifies the number of the specified part, which should be ≥ 1. | int |
| eTag | SetPartNumberAndETag | Identifies the eTag returned when the specified part is uploaded | string |
| partNumberAndETags | SetPartNumberAndETag | Identifies the part No. and the eTag returned when the part is uploaded | `Dictionary<int, string> ` |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through CompleteMultipartUploadResult.

| Member Variable | Type | Description |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| CompleteResult | [CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CompleteResult.cs) | The information of successful upload of all parts is returned. |

> [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### <span id = "ABORT_MULIT_UPLOAD">Delete uploaded parts</span>

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method prototype

```C#
AbortMultipartUploadResult AbortMultiUpload(AbortMultipartUploadRequest request);

void AbortMultiUpload(AbortMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
	AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	AbortMultipartUploadResult result = cosXml.AbortMultiUpload(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
string uploadId ="xxxxxxxx"; //The uploadId returned when multipart upload is initialized
AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.AbortMultiUpload(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		AbortMultipartUploadResult result = result as AbortMultipartUploadResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| uploadId | Construction method or SetUploadId | Identifies the specified uploadId for multipart upload | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through AbortMultipartUploadResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

> [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

## Other Operations

### Restore an archived object 

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method prototype

```C#
RestoreObjectResult RestoreObject(RestoreObjectRequest request);

void RestoreObject(RestoreObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Restoration time
	request.SetExpireDays(3);
	request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);

	//Execute the request
	RestoreObjectResult result = cosXml.RestoreObject(request);
	//Request successful
    Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Restoration time
request.SetExpireDays(3);
request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);
//Execute the request
cosXml.RestoreObject(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		RestoreObjectResult result = cosResult as RestoreObjectResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| days | SetExpireDays | Sets the validity period of the temporary replica | int |
| tier | SetTier | When restoring data, Tier can be specified as three types of restoration supported by CAS: Expedited, Standard, and Bulk. | RestoreConfigure.Tier |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through RestoreObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

> [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Set the object ACL

#### Feature

This API (Put Object ACL) is used to set an ACL for an object.

#### Method prototype

```C#
PutObjectACLResult PutObjectACL(PutObjectACLRequest request);

void PutObjectACL(PutObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set private read and write permissions 
	request.SetCosACL(CosACL.PRIVATE); 
	//Grant the read permission to the account 1131975903 
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount(); 
	readAccount.AddGrantAccount("1131975903", "1131975903"); 
	request.SetXCosGrantRead(readAccount);
	//Execute the request
	PutObjectACLResult result = cosXml.PutObjectACL(request);
	//Request successful
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set private read and write permissions 
request.SetCosACL(CosACL.PRIVATE); 
//Grant the read permission to the account 1131975903 
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount(); 
readAccount.AddGrantAccount("1131975903", "1131975903"); 
request.SetXCosGrantRead(readAccount);
//Execute the request
cosXml.PutObjectACL(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		PutObjectACLResult result = cosResult as PutObjectACLResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | string |
| cosAcl | SetCosAcl | Sets the ACL permissions for the bucket | string |
| grandtAccout | SetXCosGrantRead, SetXCosGrantWrite, or SetXCosReadWrite | Grants users the read and write permissions | GrantAccount |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through PutObjectACLResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

> [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Get the object ACL

#### Feature

This API (Get Object ACL) is used to get the ACL of an object.

#### Method prototype

```C#
GetObjectACLResult GetObjectACL(GetObjectACLRequest request);

void GetObjectACL(GetObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
	string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
	GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	GetObjectACLResult result = cosXml.GetObjectACL(request);
	//Request successful
    Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	//Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	//Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
//Async method
string bucket = "examplebucket-1250000000"; //Bucket. Format: BucketName-APPID
string key = "exampleobject"; //The location of the object in the bucket, i.e. ObjectKey.
GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.GetObjectACL(request,
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		GetObjectACLResult result = cosResult as GetObjectACLResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		//Request failed
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

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| key | Construction method or SetCosPath | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS. | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through GetObjectACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs) | The information of the object ACL is returned |

> [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

