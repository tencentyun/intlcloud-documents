## Download and Installation

### Related resources
- Download XML C# SDK source code of COS from: [XML C# SDK](https://github.com/tencentyun/qcloud-sdk-dotnet).
- Download Demo from: [COS XML C# SDK Demo](https://github.com/tencentyun/qcloud-sdk-dotnet-demo).
- Download XML C# SDK DLL files　of COS from:[COS XML DLL Library](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/libs).

### Environment dependencies
- The COS XML C# SDK source code is developed based on .NET 4.0 and relies on the newtonsoft.json library.
- Windows: Install NET 2.0 or above, and Visual Studio 2010 or above. 
- Linux/Mac: Install Mono 3.12 or above.

### Install SDK
DLL library files included in the SDK are COSXML.dll and Newtonsoft.Json.dll. You can install SDK by the following ways:

- Reference DLL
	Obtain the [SDK package](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/libs), and import the DLL files into the project.
- Reference Project
	 Obtain the [source code](https://github.com/tencentyun/qcloud-sdk-dotnet/tree/master/QCloudCSharpSDK), and import it as a project.
- Reference Nuget
	Find Tencent.QCloud.Cos.Sdk in NuGet Package Manager and click to install it.

## Getting Started
The following describes how to use COS C# SDK to perform a basic operation, such as initializing the client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

### Initialization

Before executing any request related to COS services, instantiate 3 objects: `CosXmlConfig, QCloudCredentialProvider, and CosXmlServer`.
- `CosXmlConfig` provides an API to configure SDK.
- `QCloudCredentialProvider` provides an API to set the key information.
- `CosXmlServer` provides APIs to perform operations on COS API services.

```C#
//Initialize CosXmlConfig 
string appid = "1250000000";//Set the Tencent Cloud account ID: APPID
string region = "ap-beijing"; //Set a default region of bucket
CosXmlConfig config = new CosXmlConfig.Builder()
	.SetConnectionTimeoutMs(60000)  //Set the connection timeout threshold (in ms). Defaults to 45000 ms.
	.SetReadWriteTimeoutMs(40000)  //Set the read/write timeout threshold (in ms). Defaults to 45000 ms.
	.IsHttps(true)  //Set HTTPS request as default
	.SetAppid(appid)  //Set the Tencent Cloud account ID: APPID
	.SetRegion(region)  //Set a default region of bucket
	.SetDebugLog(true)  //Display logs
	.Build();  //Create a CosXmlConfig object

//Initialize QCloudCredentialProvider. SDK supports computing a signature using permanent key, temporary key, and custom method. 
QCloudCredentialProvider cosCredentialProvider  =  null;

//Method 1: Permanent key
string secretId = "COS_SECRETID"; //"Cloud API key SecretId"
string secretKey = "COS_SECRETKEY"; //"Cloud API key SecretKey"
long durationSecond = 600;  //Validity period of secretKey (in sec)
cosCredentialProvider = new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);

//Method 2: Temporary key
string tmpSecretId = "COS_SECRETID"; //"Temporary key SecretId"
string tmpSecretKey = "COS_SECRETKEY"; //"Temporary key SecretKey"
string tmpToken = "COS_TOKEN"; //"Temporary key token"
long tmpExpireTime = 1546862502；//Expiration timestamp of temporary key
cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId,tmpSecretKey,tmpExpireTime,tmpToken);

//Method 3: Key information is provided by using custom method. You need to inherit QCloudCredentialProvider and override the GetQCloudCredentials() method.
public class MyQCloudCredentialProvider : QCloudCredentialProvider
{
	public override QCloudCredentials GetQCloudCredentials()
	{
		string secretId = "COS_SECRETID"; //Key SecretId
		string secretKey = "COS_SECRETKEY"; //Key SecretKey
		string keyTime = "Validity period of key"; //1546862502;1546863102
		return new QCloudCredentials(secretId, secretKey, keyTime);
	}

	public override void Refresh()
	{
		//Update key information
	}
}
cosCredentialProvider = new MyQCloudCredentialProvider();

//Initialize CosXmlServer
CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);

```

### Create a bucket
```C#
try
{
	string bucket = "examplebucket-1250000000"; //Bucket name. Format: BucketName-APPID
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

```

### Query the bucket list
```C#
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
```

### Upload an object
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

**//Large files are uploaded in parts(). See TransferManager and COSXMLUploadTask encapsulated in the SDK, as shown below:**
TransferManager transferManager = new TransferManager(cosXml, new TransferConfig());
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, null, key);
uploadTask.SetSrcPath(srcPath);
uploadTask.progressCallback = delegate (long completed, long total)
{
	Console.WriteLine(String.Format("progress = {1:##.##}%", completed * 100.0 / total));
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

### Query the object list
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
```

### Download an object
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
```

### Delete an object
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
```

