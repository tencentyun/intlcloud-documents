## Introduction
C# SDK provides APIs for obtaining object URL, computing signature and obtaining pre-signed URL used for request.

## Obtaining Object URL 
```C#
string GetAccessURL(CosRequest request);
```
## Computing Signature
```C#
string GenerateSign(string method, string path, Dictionary<string, string> queryParameters, Dictionary<string, string> headers, long signDurationSecond)；
```
## Obtaining Pre-signed URL Used for Request 
```C#
string GenerateSignURL(PreSignatureStruct preSignatureStruct);
```
### Parameters
| Parameter Name | Type | Description |
|-----|-----|----|
| request | CosRequest | Request object |
| preSignatureStruct | PreSignatureStruct | Pre-signed URL example |
| method | string | HTTP request method |
| path | string | HTTP request path, i.e. ObjectKey |
| headers | `Dictionary<string, string>` | Indicates whether to verify the header for the signature |
| queryParameters | `Dictionary<string, string>` | Indicates whether to verify the query parameters in the request URL for the signature |
| signDurationSecond | long | The signature's validity period (in sec) |

### Description of the PreSignatureStruct structure
Get the corresponding pre-signed request URL through the PreSignatureStruct object to send requests.

| Parameter Name | Type | Description |
|-----|-----|----|
| appid | string | The Tencent Cloud account's APPID |
| bucket | string | Bucket |
| region | string | The region where the bucket resides |
| method | string | HTTP request method |
| isHttps | bool | true: HTTPS request; false: HTTP request |
| key | string | ObjectKey |
| headers | `Dictionary<string, string>` | Indicates whether to verify the header for the signature |
| queryParameters | `Dictionary<string, string>` | Indicates whether to verify the query parameters in the request URL for the signature |
| signDurationSecond | long | The signature's validity period (in sec) |

## Example of Using Permanent Key to Generate Pre-signed URL

### Example of a upload request
```C#
try
{
	//Initialize CosXml using permanent key
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //Set the connection timeout threshold (in ms). Defaults to 45000 ms.
	.SetReadWriteTimeoutMs(40000)  //Set the read/write timeout threshold (in ms). Defaults to 45000 ms.
	.IsHttps(true)  //Set HTTPS request as default
	.SetAppid("1250000000")  //Set the Tencent Cloud account ID: APPID
	.SetRegion("ap-beijing")  //Set a default region of bucket
	.SetDebugLog(true)  //Display logs
	.Build();  //Create a CosXmlConfig object
	string secretId = "COS_SECRETID"; //"Cloud API key SecretId"
	string secretKey = "COS_SECRETKEY"; //"Cloud API key SecretKey"
	long durationSecond = 600;  //Validity period of secretKey (in sec)
	QCloudCredentialProvider cosCredentialProvider  =  new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud account's APPID
	preSignatureStruct.region = "ap-beijing"; //Region of the bucket
	preSignatureStruct.bucket = "examplebucket-1250000000"; //Bucket
	preSignatureStruct.key = "exampleobject"; //ObjectKey
	preSignatureStruct.httpMethod = "PUT"; //HTTP request method
	preSignatureStruct.isHttps = true; //Generate HTTPS request URL
	preSignatureStruct.signDurationSecond = 600; //Validity period of request signature is 600s
	preSignatureStruct.headers = null；//The header in signature for verification
	preSignatureStruct.queryParameters = null; //The request parameters of URL in signature for verification
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //The pre-signed URL (a signature URL computed with permanent key) for upload request

	string srcPath = @"F:\exampleobject"；//Absolute path to the local file
	PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
	//Set the pre-signed URL for upload request
	request.RequestURLWithSign = requestSignURL;
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
```

### Example of a download request
```C#
try
{
	//Initialize CosXml using permanent key
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //Set the connection timeout threshold (in ms). Defaults to 45000 ms.
	.SetReadWriteTimeoutMs(40000)  //Set the read/write timeout threshold (in ms). Defaults to 45000 ms.
	.IsHttps(true)  //Set HTTPS request as default
	.SetAppid("1250000000")  //Set the Tencent Cloud account ID: APPID
	.SetRegion("ap-beijing")  //Set a default region of bucket
	.SetDebugLog(true)  //Display logs
	.Build();  //Create a CosXmlConfig object
	string secretId = "COS_SECRETID"; //"Cloud API key SecretId"
	string secretKey = "COS_SECRETKEY"; //"Cloud API key SecretKey"
	long durationSecond = 600;  //Validity period of secretKey (in sec)
	QCloudCredentialProvider cosCredentialProvider  =  new DefaultQCloudCredentialProvider(secretId, secretKey, 600);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud account's APPID
	preSignatureStruct.region = "ap-beijing"; //Region of the bucket
	preSignatureStruct.bucket = "examplebucket-1250000000"; //Bucket
	preSignatureStruct.key = "exampleobject"; //ObjectKey
	preSignatureStruct.httpMethod = "GET"; //HTTP request method
	preSignatureStruct.isHttps = true; //Generate HTTPS request URL
	preSignatureStruct.signDurationSecond = 600; //Validity period of request signature is 600s
	preSignatureStruct.headers = null；//The header in signature for verification
	preSignatureStruct.queryParameters = null; //The request parameters of URL in signature for verification
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //Pre-signed URL (a signature URL computed with permanent key) used for download request
	
	string localDir = @"F:\"；//Download to the specified local folder
	string localFileName = "exampleobject"; //Specify the name of the file stored locally
	GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
	//Set the pre-signed URL for download request
	request.RequestURLWithSign = requestSignURL;
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
```


## Example of Temporary Key for Pre-signed Request

### Example of a upload request
```C#
try
{
	//Initialize CosXml using temporary key
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //Set the connection timeout threshold (in ms). Defaults to 45000 ms.
	.SetReadWriteTimeoutMs(40000)  //Set the read/write timeout threshold (in ms). Defaults to 45000 ms.
	.IsHttps(true)  //Set HTTPS request as default
	.SetAppid("1250000000")  //Set the Tencent Cloud account ID: APPID
	.SetRegion("ap-beijing")  //Set a default region of bucket
	.SetDebugLog(true)  //Display logs
	.Build();  //Create a CosXmlConfig object
	string tmpSecretId = "COS_SECRETID"; //"Temporary key SecretId"
	string tmpSecretKey = "COS_SECRETKEY"; //"Temporary key SecretKey"
	string tmpToken = "COS_TOKEN"; //"Temporary key token"
	long tmpExpireTime = 1546862502；//Expiration timestamp of temporary key
	QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud account's APPID
	preSignatureStruct.region = "ap-beijing"; //Region of the bucket
	preSignatureStruct.bucket = "examplebucket-1250000000"; //Bucket
	preSignatureStruct.key = "exampleobject"; //ObjectKey
	preSignatureStruct.httpMethod = "PUT"; //HTTP request method
	preSignatureStruct.isHttps = true; //Generate HTTPS request URL
	preSignatureStruct.signDurationSecond = 600; //Validity period of request signature is 600s
	preSignatureStruct.headers = null；//The header in signature for verification
	preSignatureStruct.queryParameters = null; //The request parameters of URL in signature for verification
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //The pre-signed URL (a signature URL computed with temporary key) for upload request

	string srcPath = @"F:\exampleobject"；//Absolute path to the local file
	PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
	//Set the pre-signed URL for upload request
	request.RequestURLWithSign = requestSignURL;
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
```

### Example of a download request
```C#
try
{
	//Initialize CosXml using temporary key
	CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //Set the connection timeout threshold (in ms). Defaults to 45000 ms.
	.SetReadWriteTimeoutMs(40000)  //Set the read/write timeout threshold (in ms). Defaults to 45000 ms.
	.IsHttps(true)  //Set HTTPS request as default
	.SetAppid("1250000000")  //Set the Tencent Cloud account ID: APPID
	.SetRegion("ap-beijing")  //Set a default region of bucket
	.SetDebugLog(true)  //Display logs
	.Build();  //Create a CosXmlConfig object
	string tmpSecretId = "COS_SECRETID"; //"Temporary key SecretId"
	string tmpSecretKey = "COS_SECRETKEY"; //"Temporary key SecretKey"
	string tmpToken = "COS_TOKEN"; //"Temporary key token"
	long tmpExpireTime = 1546862502；//Expiration timestamp of temporary key
	QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);
	CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

	PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
	preSignatureStruct.appid = "1250000000";//Tencent Cloud account's APPID
	preSignatureStruct.region = "ap-beijing"; //Region of the bucket
	preSignatureStruct.bucket = "examplebucket-1250000000"; //Bucket
	preSignatureStruct.key = "exampleobject"; //ObjectKey
	preSignatureStruct.httpMethod = "GET"; //HTTP request method
	preSignatureStruct.isHttps = true; //Generate HTTPS request URL
	preSignatureStruct.signDurationSecond = 600; //Validity period of request signature is 600s
	preSignatureStruct.headers = null；//The header in signature for verification
	preSignatureStruct.queryParameters = null; //The request parameters of URL in signature for verification
	
	string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); //The pre-signed URL (a signature URL computed with temporary key) for download request
	
	string localDir = @"F:\"；//Download to the specified local folder
	string localFileName = "exampleobject"; //Specify the name of the file stored locally
	GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
	//Set the pre-signed URL for download request
	request.RequestURLWithSign = requestSignURL;
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
```

