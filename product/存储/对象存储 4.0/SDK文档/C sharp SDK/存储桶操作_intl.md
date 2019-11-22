## Introduction

This document provides an overview of APIs and SDK sample codes related to the basic operations and the access control list (ACL) for a bucket.

**Basic operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Gets the bucket list | Gets the list of all bucket under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creates a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Search for the bucket and the access to it | Determines whether the bucket and the permission to access the bucket exist |
| GET Bucket location | Gets the location information of a bucket | Gets the information on the location where a bucket locates |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deletes a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Sets a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Gets the bucket ACL | Gets the ACL of a bucket |

## Basic Operations

### Get the bucket list

#### Feature

This API (Bucket list) is used to get the list of all buckets under the specified account.

#### Method prototype

```C#
GetServiceResult GetService(GetServiceRequest request);

void GetService(GetServiceRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```
try
{
	GetServiceRequest request = new GetServiceRequest();
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	GetServiceResult result = cosXml.GetService(request);
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
GetServiceRequest request = new GetServiceRequest();
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetService(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		GetServiceResult result = cosResult as GetServiceResult;
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
| ------------------- | -------- | ------------------------------- | -------------- |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through GetServiceResult.

| Member Variable | Type | Description |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listAllMyBuckets | [ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListAllMyBuckets.cs) | The list of buckets under the specified account is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Create a bucket

#### Feature

This API (Put Bucket) is used to create a bucket.

#### Method prototype

```C#
PutBucketResult PutBucket(PutBucketRequest request);

void PutBucket(PutBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	PutBucketRequest request = new PutBucketRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	PutBucketResult result = cosXml.PutBucket(request);
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
PutBucketRequest request = new PutBucketRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.PutBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		PutBucketResult result = cosResult as PutBucketResult;
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

Request result is returned through PutBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Search for a bucket

#### Feature

This API (Head Bucket) is used to determine whether the specified bucket exists.

#### Method prototype

```C#
HeadBucketResult HeadBucket(HeadBucketRequest request);

void HeadBucket(HeadBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	HeadBucketRequest request = new HeadBucketRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	HeadBucketResult result = cosXml.HeadBucket(request);
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
HeadBucketRequest request = new HeadBucketRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.HeadBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		HeadBucketResult result = cosResult as HeadBucketResult;
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

### Get the bucket location

#### Feature

This API (Get Bucket Location) is used to get the location information of the specified bucket.

#### Method prototype

```C#
GetBucketLocationResult GetBucketLocation(GetBucketLocationRequest request);

void GetBucketLocation(GetBucketLocationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	GetBucketLocationRequest request = new GetBucketLocationRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	GetBucketLocationResult result = cosXml.GetBucketLocation(request);
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
GetBucketLocationRequest request = new GetBucketLocationRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucketLocation(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		GetBucketLocationResult result = cosResult as GetBucketLocationResult;
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

Request result is returned through GetBucketLocationResult.

| Member Variable | Type | Description |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| locationConstraint | [LocationConstraint](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LocationConstraint.cs) | The region information of the bucket is returned |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Delete a bucket

#### Feature

This API (Delete Bucket) is used to delete the specified bucket.

#### Method prototype

```C#
DeleteBucketResult DeleteBucket(DeleteBucketRequest request);

void DeleteBucket(DeleteBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	DeleteBucketRequest request = new DeleteBucketRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	DeleteBucketResult result = cosXml.DeleteBucket(request);
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
DeleteBucketRequest request = new DeleteBucketRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.DeleteBucket(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		DeleteBucketResult result = cosResult as DeleteBucketResult;
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

Request result is returned through DeleteBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

## ACL

### Set a bucket ACL

#### Feature

This API (Put Bucket ACL) is used to set an ACL for the specified bucket.

#### Method prototype

```C#
PutBucketACLResult PutBucketACL(PutBucketACLRequest request);

void PutBucketACL(PutBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	PutBucketACLRequest request = new PutBucketACLRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set private read and write permissions
	request.SetCosACL(CosACL.PRIVATE);
	//Grant the read permission to the account 1131975903
	COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
	readAccount.AddGrantAccount("1131975903", "1131975903");
	request.SetXCosGrantRead(readAccount);
	//Execute the request
	PutBucketACLResult result = cosXml.PutBucketACL(request);
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
PutBucketACLRequest request = new PutBucketACLRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set private read and write permissions
request.SetCosACL(CosACL.PRIVATE);
//Grant the read permission to the account 1131975903
COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
readAccount.AddGrantAccount("1131975903", "1131975903");
request.SetXCosGrantRead(readAccount);
//Execute the request
cosXml.PutBucketACL(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		PutBucketACLResult result = cosResult as PutBucketACLResult;
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
| ------------------- | --------------------------------------------------------- | ---------------------------------- | -------------- |
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| cosAcl | SetCosAcl | Sets the ACL permissions for the bucket | string |
| grandtAccout | SetXCosGrantRead, SetXCosGrantWrite, or SetXCosReadWrite | Grants users the read and write permissions | GrantAccount |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result

Request result is returned through PutBucketACLResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>[CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

### Get the bucket ACL

#### Feature

This API (Get Bucket ACL) is used to get the ACL of the specified bucket.

#### Method prototype

```C#
GetBucketACLResult GetBucketACL(GetBucketACLRequest request);

void GetBucketACL(GetBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example

```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	GetBucketACLRequest request = new GetBucketACLRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	GetBucketACLResult result = cosXml.GetBucketACL(request);
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
GetBucketACLRequest request = new GetBucketACLRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
cosXml.GetBucketACL(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		GetBucketACLResult result = cosResult as GetBucketACLResult;
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

Request result is returned through GetBucketACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs) | The information of the bucket ACL is returned |

> [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception occurs when the operation fails.

