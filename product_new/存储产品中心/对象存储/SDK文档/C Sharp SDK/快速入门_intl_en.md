## Download and Installation

#### Relevant Resources
- The COS XML SDK for .NET source code can be downloaded [here](https://github.com/tencentyun/qcloud-sdk-dotnet).
- The sample demo can be download [here](https://github.com/tencentyun/qcloud-sdk-dotnet-demo).

#### Environmental Dependency
- COS XML SDK for .NET: Developed based on .NET Standard 2.0.
- Windows: Install .NET Core 2.0 or above or .NET Framework 4.6.1 or above. 
- Linux/Mac: Install .NET Core 2.0 or above.

#### Adding the SDK

We provide a way to integrate Nuget, which can add to the `csproj` file of your project:

```
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.5" />
```

If .NET CLI is used, run the following command for installation:

```shell
dotnet add package Tencent.QCloud.Cos.Sdk
```

You can also manually download the SDK [here](https://github.com/tencentyun/qcloud-sdk-dotnet/releases).

#### Other Dependencies

We use Newtonsoft.Json as a third-party dependency, and if it is not automatically pulled locally, you can add it to the `csproj` file manually:

```
<PackageReference Include="Newtonsoft.Json" Version="12.0.2" />
```

## Getting Started
The section below describes how to perform basic operations in the COS SDK for .NET, such as initializing a client, creating a bucket, querying bucket list, uploading an object, querying object list, downloading an object, and deleting an object.


>
>- For the definitions of SecretId, SecretKey, Bucket and other terms, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
>- Namespaces commonly used in the SDK include `using COSXML, using COSXML.Auth, using COSXML.Model.Object, using COSXML.Model.Bucket, and using COSXML.CosException`.

### Initialization

Before executing any COS requests,  instantiate 3 objects: ` CosXmlConfig, QCloudCredentialProvider, and CosXmlServer`.
- `CosXmlConfig` provides the API for configuring the SDK.
- `QCloudCredentialProvider` provides the API for setting key information.
- `CosXmlServer` provides various COS APIs.

```C#
// Initialize CosXmlConfig 
string appid = "1250000000";// Set the APPID of your Tencent Cloud account
string region = "ap-beijing"; // Set the default bucket region
CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
	.SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
	.IsHttps(true)  // Set HTTPS as default request method
	.SetAppid(appid)  // Set the APPID of your Tencent Cloud account
	.SetRegion(region)  // Set the default bucket region
	.SetDebugLog(true)  // Show the log
	.Build();  // Create a CosXmlConfig object

// Initialize QCloudCredentialProvider. The SDK provides three methods: permanent key, temporary key, and custom 
QCloudCredentialProvider cosCredentialProvider  =  null;

// Method 1: Permanent key
string secretId = "COS_SECRETID"; //"TencentCloud API key's SecretId";
string secretKey = "COS_SECRETKEY"; //"TencentCloud API key's SecretKey";
long durationSecond = 600;  // Validity period of the secretKey in seconds
cosCredentialProvider = new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);

// Method 2: Temporary key
string tmpSecretId = "COS_SECRETID"; // "Temporary key's SecretId";
string tmpSecretKey = "COS_SECRETKEY"; // "Temporary key's SecretKey";
string tmpToken = "COS_TOKEN"; // "Temporary key's token";
long tmpExpireTime = 1546862502;// End time of validity of the temporary key
cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);

// Method 3: Custom key information, which inherits QCloudCredentialProvider and rewrites the GetQCloudCredentials() method
public class MyQCloudCredentialProvider : QCloudCredentialProvider
{
	public override QCloudCredentials GetQCloudCredentials()
	{
		string secretId = "COS_SECRETID"; // Key's SecretId
		string secretKey = "COS_SECRETKEY"; // Key's SecretKey
		string keyTime = "Validity period of the key"; //1546862502;1546863102
		return new QCloudCredentials(secretId, secretKey, keyTime);
	}

	public override void Refresh()
	{
		// Update key information
	}
}
cosCredentialProvider = new MyQCloudCredentialProvider();

// Initialize CosXmlServer
CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

```

### Creating a Bucket
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
	PutBucketRequest request = new PutBucketRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	PutBucketResult result = cosXml.PutBucket(request);
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

```

### Querying the Bucket List
```C#
try
{
	GetServiceRequest request = new GetServiceRequest();
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	GetServiceResult result = cosXml.GetService(request);
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
```

### Uploading an Object
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
	string key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
	string srcPath = @"F:\exampleobject";// Absolute path to the local file
	PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Set progress callback
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
	});
	// Execute the request
	PutObjectResult result = cosXml.PutObject(request);
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

**// Multipart upload() needs to be used for large files. For more information, see the TransferManager and COSXMLUploadTask classes encapsulated in the SDK. Below is an example:**
TransferManager transferManager = new TransferManager(cosXml, new TransferConfig());
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, null, key);
uploadTask.SetSrcPath(srcPath);
uploadTask.progressCallback = delegate (long completed, long total)
{
	Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
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

### Querying the Object List
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
	GetBucketRequest request = new GetBucketRequest(bucket);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	GetBucketResult result = cosXml.GetBucket(request);
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
```

### Downloading an Object
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
	string key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
	string localDir = @"F:\";// Download to the specified local folder
	string localFileName = "exampleobject"; // Specify the name of the file to be saved in the local file system
	GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Set progress callback
	request.SetCosProgressCallback(delegate(long completed, long total)
	{
		Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
	});
	// Execute the request
	GetObjectResult result = cosXml.GetObject(request);
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
```

### Deleting an Object
```C#
try
{
	string bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
	string key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
	DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
	// Set the validity period of the signature
	request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
	// Execute the request
	DeleteObjectResult result = cosXml.DeleteObject(request);
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
```
