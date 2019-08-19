## Overview
This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |

## Cross-origin Access
### Setting Cross-origin Access Configuration

#### Feature Description

This API is used to set the cross-origin access configuration information of the specified bucket.

#### Method Prototype
```C#
PutBucketCORSResult PutBucketCORS(PutBucketCORSRequest request);

void PutBucketCORS(PutBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
	PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Set the cross-origin access configuration
	COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = new COSXML.Model.Tag.CORSConfiguration.CORSRule();
	corsRule.id = "corsconfigureId";
	corsRule.maxAgeSeconds = 6000;
	corsRule.allowedOrigin = "http://intl.cloud.tencent.com";

	corsRule.allowedMethods = new List<string>();
	corsRule.allowedMethods.Add("PUT");

	corsRule.allowedHeaders = new List<string>();
	corsRule.allowedHeaders.Add("Host");

	corsRule.exposeHeaders = new List<string>();
	corsRule.exposeHeaders.Add("x-cos-meta-x1");

	request.SetCORSRule(corsRule);

	// Execute the request
	PutBucketCORSResult result = cosXml.PutBucketCORS(request);
	// Request succeeded
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	// Request failed
 	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	// Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
// Async method
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
// Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);

// Set the cross-origin access configuration
COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = new COSXML.Model.Tag.CORSConfiguration.CORSRule();
corsRule.id = "corsconfigureId";
corsRule.maxAgeSeconds = 6000;
corsRule.allowedOrigin = "http://intl.cloud.tencent.com";

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
		// Request succeeded
		PutBucketCORSResult result = cosResult as PutBucketCORSResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
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

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|corsRule|SetCORSRule| Sets the cross-origin access configuration of a bucket |CORSConfiguration.CORSRule|
|signStartTimeSecond|SetSign| Starting time of the signature's validity period |long|
|durationSecond|SetSign| Signature's validity period |long|
|headerKeys|SetSign| Whether the signature verifies the header |`List<string>`|
|queryParameterKeys|SetSign| Whether the signature verifies the query parameter in the request URL |`List<string>`|

#### Return Result Descriptions
The result of the request is returned through PutBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

### Querying Cross-origin Access Configuration

#### Feature Description

This API is used to query the cross-origin access configuration information of the specified bucket.

#### Method Prototype
```C#
GetBucketCORSResult GetBucketCORS(GetBucketCORSRequest request);

void GetBucketCORS(GetBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
	GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	GetBucketCORSResult result = cosXml.GetBucketCORS(request);
	// Request succeeded
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	// Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	// Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
// Async method
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
// Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
// Execute the request
cosXml.GetBucketCORS(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		GetBucketCORSResult result = cosResult as GetBucketCORSResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
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

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|signStartTimeSecond|SetSign| Starting time of the signature's validity period |long|
|durationSecond|SetSign| Signature's validity period |long|
|headerKeys|SetSign| Whether the signature verifies the header |`List<string>`|
|queryParameterKeys|SetSign| Whether the signature verifies the query parameter in the request URL |`List<string>`|

#### Return Result Descriptions
The result of the request is returned through GetBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
|corsConfiguration|[CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CORSConfiguration.cs)| Returns the cross-origin resource sharing configuration information of a bucket |

### Deleting Cross-origin Access Configuration

#### Feature Description

This API is used to delete the cross-origin access configuration of the specified bucket.

#### Method Prototype
```C#
DeleteBucketCORSResult DeleteBucketCORS(DeleteBucketCORSRequest request);

void DeleteBucketCORS(DeleteBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
	DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	DeleteBucketCORSResult result = cosXml.DeleteBucketCORS(request);
	// Request succeeded
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	// Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	// Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
// Async method
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
// Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
// Execute the request
cosXml.DeleteBucketCORS(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		DeleteBucketCORSResult result = cosResult as DeleteBucketCORSResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
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

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|signStartTimeSecond|SetSign| Starting time of the signature's validity period |long|
|durationSecond|SetSign| Signature's validity period |long|
|headerKeys|SetSign| Whether the signature verifies the header |`List<string>`|
|queryParameterKeys|SetSign| Whether the signature verifies the query parameter in the request URL |`List<string>`|

#### Return Result Descriptions
The result of the request is returned through DeleteBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |


## Lifecycle
### Setting Lifecycle

#### Feature Description

This API is used to set the lifecycle configuration information of the specified bucket.

#### Method Prototype
```shell
PutBucketLifecycleResult PutBucketLifecycle(PutBucketLifecycleRequest request);

void PutBucketLifecycle(PutBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
	PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Set the lifecycle
	COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
	rule.id = "lfiecycleConfigureId";
	rule.status = "Enabled"; //Enabled，Disabled

	rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
	rule.filter.prefix = "2/";

	// Specify part deletion upon expiry
	rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
	rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

	request.SetRule(rule);

	// Execute the request
	PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
	// Request succeeded
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	// Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	// Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
// Async method
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
// Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
// Set the lifecycle
COSXML.Model.Tag.LifecycleConfiguration.Rule rule = new COSXML.Model.Tag.LifecycleConfiguration.Rule();
rule.id = "lfiecycleConfigureId";
rule.status = "Enabled"; //Enabled，Disabled

rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
rule.filter.prefix = "2/";

rule.abortIncompleteMultiUpload = new COSXML.Model.Tag.LifecycleConfiguration.AbortIncompleteMultiUpload();
rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

request.SetRule(rule);

// Execute the request
cosXml.PutBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		PutBucketLifecycleResult result = cosResult as PutBucketLifecycleResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
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

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|rule|SetRule| Sets the lifecycle configuration of a bucket |LifecycleConfiguration.Rule|
|signStartTimeSecond|SetSign| Starting time of the signature's validity period |long|
|durationSecond|SetSign| Signature's validity period |long|
|headerKeys|SetSign| Whether the signature verifies the header |`List<string>`|
|queryParameterKeys|SetSign| Whether the signature verifies the query parameter in the request URL |`List<string>`|

#### Return Result Descriptions
The result of the request is returned through PutBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |


### Querying Lifecycle

#### Feature Description

This API is used to query the lifecycle of the specified bucket.

#### Method Prototype
```shell
GetBucketLifecycleResult GetBucketLifecycle(GetBucketLifecycleRequest request);

void GetBucketLifecycle(GetBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
	GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
	// Request succeeded
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	// Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	// Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
// Async method
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
// Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
// Execute the request
cosXml.GetBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		 GetBucketLifecycleResult result = cosResult as GetBucketLifecycleResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
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

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|signStartTimeSecond|SetSign| Starting time of the signature's validity period |long|
|durationSecond|SetSign| Signature's validity period |long|
|headerKeys|SetSign| Whether the signature verifies the header |`List<string>`|
|queryParameterKeys|SetSign| Whether the signature verifies the query parameter in the request URL |`List<string>`|

#### Return Result Descriptions
The result of the request is returned through GetBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
|lifecycleConfiguration|[LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LifecycleConfiguration.cs)| Returns the lifecycle configuration information of a bucket |


### Deleting Lifecycle

#### Feature Description

This API is used to delete the lifecycle of the specified bucket.

#### Method Prototype
```shell
DeleteBucketLifecycleResult DeleteBucketLifecycle(DeleteBucketLifecycleRequest request);

void DeleteBucketLifecycle(DeleteBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
	DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
	// Request succeeded
	Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{	
	// Request failed
	Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
	// Request failed
	Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

/**
// Async method
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
// Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
// Execute the request
cosXml.DeleteBucketLifecycle(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		DeleteBucketLifecycleResult result = cosResult as DeleteBucketLifecycleResult;
		Console.WriteLine(result.GetResultInfo());

	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{
		// Request failed
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

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|signStartTimeSecond|SetSign| Starting time of the signature's validity period |long|
|durationSecond|SetSign| Signature's validity period |long|
|headerKeys|SetSign| Whether the signature verifies the header |`List<string>`|
|queryParameterKeys|SetSign| Whether the signature verifies the query parameter in the request URL |`List<string>`|

#### Return Result Descriptions
The result of the request is returned through DeleteBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |


## Versioning
### Setting Versioning

#### Feature Description

This API is used to set the versioning feature of the specified bucket.

#### Method Prototype
```
PutBucketVersioningResult PutBucketVersioning(PutBucketVersioningRequest request);
void PutBucketVersioning(PutBucketVersioningRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

```
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketVersioningRequest request = new PutBucketVersioningRequest(bucket);
// Set the validity period of the signature
//request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
request.IsEnableVersionConfig(true); // true: enable versioning; false: suspend versioning
// Use the sync method
try {
    PutBucketVersioningResult result = cosXml.PutBucketVersioning(request);
	Console.WriteLine(result.GetResultInfo());
} catch (COSXML.CosException.CosClientException clientEx) {
   Console.WriteLine("CosClientException: " + clientEx.Message);
} catch (COSXML.CosException.CosServerException serverEx) {
   Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
// Use the async callback to request
cosXml.PutBucketVersioning(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		PutBucketVersioningResult result = cosResult as PutBucketVersioningResult;
		Console.WriteLine(result.GetResultInfo());
	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| isEnable | Whether to enable versioning. true: enable; false: suspend | bool |
| signStartTimeSecond | Starting time of the signature's validity period                 | long           |
| durationSecond      | Signature's validity period                     | long           |
| headerKeys          | Whether the signature verifies the header                | `List<string>` |
| queryParameterKeys  | Whether the signature verifies the query parameter in the request URL    | `List<string>` |


#### Return Result Descriptions
The result of the request is returned through PutBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Querying Versioning

#### Feature Description

This API is used to query the versioning information of the specified bucket.

#### Method Prototype
```
GetBucketVersioningResult GetBucketVersioning(GetBucketVersioningRequest request);
void GetBucketVersioning(GetBucketVersioningRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketVersioningRequest request = new GetBucketVersioningRequest(bucket);

// Use the sync method
try {
    GetBucketVersioningResult result = cosXml.GetBucketVersioning(request);
	Console.WriteLine(result.GetResultInfo());
} catch (COSXML.CosException.CosClientException clientEx) {
   Console.WriteLine("CosClientException: " + clientEx.Message);
} catch (COSXML.CosException.CosServerException serverEx) {
   Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

// Use the async callback to request
cosXml.GetBucketVersioning(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		GetBucketVersioningResult result = cosResult as GetBucketVersioningResult;
		Console.WriteLine(result.GetResultInfo());
	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| signStartTimeSecond | Starting time of the signature's validity period                 | long           |
| durationSecond      | Signature's validity period                     | long           |
| headerKeys          | Whether the signature verifies the header                | `List<string>` |
| queryParameterKeys  | Whether the signature verifies the query parameter in the request URL    | `List<string>` |


#### Return Result Descriptions
The result of the request is returned through GetBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
|versioningConfiguration|[VersioningConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/VersioningConfiguration.cs)| Versioning configuration information |

> If the operation failed, the system throws a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API is used to set the cross-region replication rule of the specified bucket.

#### Method Prototype

```
PutBucketReplicationResult PutBucketReplication(PutBucketReplicationRequest request);
void PutBucketReplication(PutBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

```
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
string ownerUin = "ownerUin"; // Initiator ID, i.e., OwnerUin 
string subUin = "SubUin"; // Initiator ID: SubUin 
PutBucketReplicationRequest request = new PutBucketReplicationRequest(bucket);
// Set the replication
putBucketReplicationRequest.setReplicationConfigurationWithRole(ownerUin, subUin);
PutBucketReplicationRequest.RuleStruct ruleStruct = new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Mark the name of the specific rule
ruleStruct.isEnable = true; // Mark whether the rule takes effect: true: yes; false: no
ruleStruct.appid = "1250000000"; // appid
ruleStruct.region = Region.AP_Beijing.getRegion(); // Region information of the destination bucket
ruleStruct.bucket = "bucketName"; // bucketName excluding '-appid' 
ruleStruct.prefix = "34"; // Prefix matching policy
List<PutBucketReplicationRequest.RuleStruct> ruleStructs = new List<PutBucketReplicationRequest.RuleStruct>();
ruleStructs.Add(ruleStruct);
request.SetReplicationConfiguration(ownerUin, subUin, ruleStructs);

// Use the sync method
try {
    PutBucketReplicationResult result = cosXml.PutBucketReplication(request);
	Console.WriteLine(result.GetResultInfo());
} catch (COSXML.CosException.CosClientException clientEx) {
   Console.WriteLine("CosClientException: " + clientEx.Message);
} catch (COSXML.CosException.CosServerException serverEx) {
   Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

// Use the async callback to request
cosXml.PutBucketReplication(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		PutBucketReplicationResult result = cosResult as PutBucketReplicationResult;
		Console.WriteLine(result.GetResultInfo());
	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| ownerUin  | Initiator ID: OwnerUin | string |
| subUin  | Initiator ID: SubUin    | string |
| ruleStruct  | Whether the signature verifies the query parameter in the request URL | RuleStruct |
| signStartTimeSecond | Starting time of the signature's validity period                 | long           |
| durationSecond      | Signature's validity period                     | long           |
| headerKeys          | Whether the signature verifies the header                | `List<string>` |
| queryParameterKeys  | Whether the signature verifies the query parameter in the request URL    | `List<string>` |


#### Return Result Descriptions
The result of the request is returned through PutBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Querying Cross-region Replication

#### Feature Description

This API is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype
```
GetBucketReplicationResult GetBucketReplication(GetBucketReplicationRequest request);
void GetBucketReplication(GetBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketReplicationRequest request = new GetBucketReplicationRequest(bucket);

// Use the sync method
try {
    GetBucketReplicationResult result = cosXml.GetBucketReplication(request);
	Console.WriteLine(result.GetResultInfo());
} catch (COSXML.CosException.CosClientException clientEx) {
   Console.WriteLine("CosClientException: " + clientEx.Message);
} catch (COSXML.CosException.CosServerException serverEx) {
   Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

// Use the async callback to request
cosXml.GetBucketReplication(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		GetBucketReplicationResult result = cosResult as GetBucketReplicationResult;
		Console.WriteLine(result.GetResultInfo());
	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| signStartTimeSecond | Starting time of the signature's validity period                 | long           |
| durationSecond      | Signature's validity period                     | long           |
| headerKeys          | Whether the signature verifies the header                | `List<string>` |
| queryParameterKeys  | Whether the signature verifies the query parameter in the request URL    | `List<string>` |

#### Return Result Descriptions
The result of the request is returned through GetBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
|replicationConfiguration|[ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ReplicationConfiguration.cs)| Cross-region configuration information |


> If the operation failed, the system throws a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Deleting Cross-region Replication

#### Feature Description

This API is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype
```
DeleteBucketReplicationResult DeleteBucketReplication(DeleteBucketReplicationRequest request);
void DeleteBucketReplication(DeleteBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request
```
string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketReplicationRequest request = new DeleteBucketReplicationRequest(bucket);

// Use the sync method
try {
    DeleteBucketReplicationResult result = cosXml.DeleteBucketReplication(request);
	Console.WriteLine(result.GetResultInfo());
} catch (COSXML.CosException.CosClientException clientEx) {
   Console.WriteLine("CosClientException: " + clientEx.Message);
} catch (COSXML.CosException.CosServerException serverEx) {
   Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

// Use the async callback to request
cosXml.DeleteBucketReplication(request, 
	delegate(COSXML.Model.CosResult cosResult)
	{
		// Request succeeded
		DeleteBucketReplicationResult result = cosResult as DeleteBucketReplicationResult;
		Console.WriteLine(result.GetResultInfo());
	}, 
	delegate(COSXML.CosException.CosClientException clientEx, COSXML.CosException.CosServerException serverEx)
	{	
		// Request failed
		if (clientEx != null)
		{
			Console.WriteLine("CosClientException: " + clientEx.Message);
		}
		else if (serverEx != null)
		{
			Console.WriteLine("CosServerException: " + serverEx.GetInfo());
		}
	});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| signStartTimeSecond | Starting time of the signature's validity period                 | long           |
| durationSecond      | Signature's validity period                     | long           |
| headerKeys          | Whether the signature verifies the header                | `List<string>` |
| queryParameterKeys  | Whether the signature verifies the query parameter in the request URL    | `List<string>` |


#### Return Result Descriptions
The result of the request is returned through DeleteBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) exception.
