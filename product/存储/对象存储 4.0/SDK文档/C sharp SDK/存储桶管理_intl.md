## Introduction
This document provides an overview of APIs and SDK sample codes related to the cross-origin access and lifecycle.

**Cross-origin access**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Sets the cross-origin configuration for a bucket | Sets the cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Gets cross-origin configuration | Gets the configurations on cross-origin access of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deletes cross-origin configuration | Deletes the configurations on cross-origin access of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Sets the lifecycle | Sets the configurations on the lifecycle management for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Queries the lifecycle | Queries the configurations on the lifecycle management of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deletes the lifecycle | Deletes the configurations on the lifecycle management of a bucket |

## Cross-Origin Access
### Set cross-origin configuration

#### Feature

This API (Put Bucket CORS) is used to set the configurations on cross-origin access (CORS) for a bucket.

#### Method prototype
```C#
PutBucketCORSResult PutBucketCORS(PutBucketCORSRequest request);

void PutBucketCORS(PutBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example
```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set the configurations on cross-origin access (CORS)
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

	//Execute the request
	PutBucketCORSResult result = cosXml.PutBucketCORS(request);
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
PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);

//Set the configurations on cross-origin access (CORS)
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
		//Request successful
		PutBucketCORSResult result = cosResult as PutBucketCORSResult;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| corsRule| SetCORSRule | Sets the configurations on cross-origin access for a bucket | CORSConfiguration.CORSRule |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result
Request result is returned through PutBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

### Get cross-origin configuration

#### Feature

This API (Get Bucket CORS) is used to get the configurations on cross-origin access (CORS) of a bucket.

#### Method prototype
```C#
GetBucketCORSResult GetBucketCORS(GetBucketCORSRequest request);

void GetBucketCORS(GetBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example
```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	GetBucketCORSResult result = cosXml.GetBucketCORS(request);
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
GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.GetBucketCORS(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		GetBucketCORSResult result = cosResult as GetBucketCORSResult;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result
Request result is returned through GetBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| corsConfiguration | [CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CORSConfiguration.cs) | The CORS configuration for the bucket is returned |

### Delete cross-origin configuration

#### Feature

This API (Delete Bucket CORS) is used to delete the configurations on cross-origin access (CORS) of a bucket.

#### Method prototype
```C#
DeleteBucketCORSResult DeleteBucketCORS(DeleteBucketCORSRequest request);

void DeleteBucketCORS(DeleteBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example
```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	DeleteBucketCORSResult result = cosXml.DeleteBucketCORS(request);
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
DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.DeleteBucketCORS(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		DeleteBucketCORSResult result = cosResult as DeleteBucketCORSResult;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result
Request result is returned through DeleteBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |


## Lifecycle
### Set the lifecycle

#### Feature

This API (Put Bucket LifeCycle) is used to set the lifecycle configuration for the specified bucket.

#### Method prototype
```shell
PutBucketLifecycleResult PutBucketLifecycle(PutBucketLifecycleRequest request);

void PutBucketLifecycle(PutBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example
```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Set the lifecycle
	COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
	rule.id = "lfiecycleConfigureId";
	rule.status = "Enabled"; //Enabled, Disabled

	rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
	rule.filter.prefix = "2/";

	//Specify the operation of deleting expired parts
	rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
	rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

	request.SetRule(rule);

	//Execute the request
	PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
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
PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Set the lifecycle
COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
rule.id = "lfiecycleConfigureId";
rule.status = "Enabled"; //Enabled，Disabled

rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
rule.filter.prefix = "2/";

rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

request.SetRule(rule);

//Execute the request
cosXml.PutBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		PutBucketLifecycleResult result = cosResult as PutBucketLifecycleResult;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| rule | SetRule | Sets the lifecycle configuration for a bucket | LifecycleConfiguration.Rule |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result
Request result is returned through PutBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |


### Query the lifecycle

#### Feature

This API (Get Bucket Lifecycle) is used to get the lifecycle of the specified bucket.

#### Method prototype
```shell
GetBucketLifecycleResult GetBucketLifecycle(GetBucketLifecycleRequest request);

void GetBucketLifecycle(GetBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example
```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
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
GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.GetBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		 GetBucketLifecycleResult result = cosResult as GetBucketLifecycleResult;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result
Request result is returned through GetBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| lifecycleConfiguration | [LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LifecycleConfiguration.cs) | The lifecycle configuration of the bucket is returned |


### Delete the lifecycle

#### Feature

This API (Delete Bucket Lifecycle) is used to delete the lifecycle of the specified bucket.

#### Method prototype
```shell
DeleteBucketLifecycleResult DeleteBucketLifecycle(DeleteBucketLifecycleRequest request);

void DeleteBucketLifecycle(DeleteBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Request example
```C#
try
{
	string bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
	DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
	//Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	//Execute the request
	DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
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
DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
//Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
//Execute the request
cosXml.DeleteBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		//Request successful
		DeleteBucketLifecycleResult result = cosResult as DeleteBucketLifecycleResult;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period | long |
| durationSecond | SetSign | Duration of the signature's validity period | long |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List<string>` |

#### Returned result
Request result is returned through DeleteBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

