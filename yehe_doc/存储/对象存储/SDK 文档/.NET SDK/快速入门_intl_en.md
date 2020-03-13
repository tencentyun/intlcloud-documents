## Download and installation

#### Relevant Resources
- Source code of COS XML .NET SDK: [COS XML .NET SDK](https://github.com/tencentyun/qcloud-sdk-dotnet).

#### Environmental Requirements
COS XML .NET SDK is developed based on .NET Standard 2.0.

- Windows: Install .NET Core 2.0 or above or .NET Framework 4.6.1 or above. 
- Linux/Mac: Install .NET Core 2.0 or above.

### Installing SDKs

We provide a way to integrate Nuget, which can add to the `csproj` file of your project:

```
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.*" />
```

If .NET CLI is used, run the following command for installation:

```shell
dotnet add package Tencent.QCloud.Cos.Sdk
```

You can also manually download the SDK [here](https://github.com/tencentyun/qcloud-sdk-dotnet/releases).

## Getting Started
The section below describes how to perform basic operations with COS .NET SDK, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.


>- For definitions of SecretID, SecretKey, Bucket and other terms, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).

Namespaces commonly used in SDKs include:

```C#
using COSXML;
using COSXML.Auth;
using COSXML.Model.Object;
using COSXML.Model.Bucket;
using COSXML.CosException;
```

### Initialization

Before executing any COS requests, instantiate 3 objects: ` CosXmlConfig, QCloudCredentialProvider, and CosXmlServer`.
- `CosXmlConfig` provides an API to configure SDK.
- `QCloudCredentialProvider` provides an API to set the key information.
- `CosXmlServer` provides APIs to perform operations on COS API services.

> For more information on how to generate and use the temporary keys used in the initialization samples below, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

[//]: # (.cssg-snippet-global-init)
```C#
// Initialize CosXmlConfig 
string appid = "1250000000";// Set the APPID of your Tencent Cloud account
string region = "COS_REGION"; // Set the default bucket region
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid(appid)  // Set the APPID of your Tencent Cloud account
  .SetRegion(region)  // Set the default bucket region
  .SetDebugLog(true)  // Show the log
  .Build();  // Create a CosXmlConfig object

// Initialize QCloudCredentialProvider. COS SDK supports 3 different methods, using permanent key, temporary key, and a custom method.
QCloudCredentialProvider cosCredentialProvider = null;

// Method 1: Permanent Key
String secretId = "COS_SECRETID"; // "TencentCloud API key SecretId";
String secretKey = "COS_SECRETKEY"; // "Enter the SecretKey of your TencentCloud API key";
long durationSecond = 600;          // Validity period of the request signature in seconds
cosCredentialProvider = new DefaultQCloudCredentialProvider(secretId, secretKey, durationSecond);

// Method 2: Temporary Key
String tmpSecretId = "COS_SECRETID"; // "Temporary key SecretId";
String tmpSecretKey = "COS_SECRETKEY"; // "Temporary key SecretKey";
string tmpToken = "COS_TOKEN"; //"Temporary key token";
long tmpExpireTime = 1546862502;// End of the validity period of the temporary key
cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(tmpSecretId, tmpSecretKey, 
  tmpExpireTime, tmpToken);

// Initialize CosXmlServer
CosXmlServer cosXml = new CosXmlServer(config, cosCredentialProvider);
```
[//]: # (.cssg-snippet-global-init-custom-credential-provider)
```C#
// Method 3: The key is provided via a custom method. You need to inherit QCloudCredentialProvider and override the GetQCloudCredentials() method.
public class MyQCloudCredentialProvider : QCloudCredentialProvider
{
  public override QCloudCredentials GetQCloudCredentials()
  {
    String secretId = "COS_SECRETID"; // Permanent key SecretId
    String secretKey ="COS_SECRETKEY"; // Permanent key SecretKey
    // Validity period of the key, accurate to the second. E.g., 1546862502;1546863102
    string keyTime = "SECRET_STARTTIME;SECRET_ENDTIME"; 
    return new QCloudCredentials(secretId, secretKey, keyTime);
  }

  public override void Refresh()
  {
    // Overrides the key. Callback is performed automatically when the key expires.
  }
}
```

### Creating a Bucket
[//]: # (.cssg-snippet-put-bucket)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  PutBucketResult result = cosXml.PutBucket(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Querying Bucket List
[//]: # (.cssg-snippet-get-service)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  GetServiceRequest request = new GetServiceRequest();
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  GetServiceResult result = cosXml.GetService(request);
  // Get a list of all buckets
  List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Uploading an Object
[//]: # (.cssg-snippet-put-object)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string srcPath = @"temp-source-file";// Absolute path to the local file
  if (!File.Exists(srcPath)) {
    // If a target file do not exist, create a temporary file for testing
    File.WriteAllBytes(srcPath, new byte[1024]);
  }

  PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  PutObjectResult result = cosXml.PutObject(request);
  // Object etag
  string eTag = result.eTag;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Querying Object List
[//]: # (.cssg-snippet-get-bucket)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Get the object in a/
  request.SetPrefix("a/");
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // bucket information
  ListBucket info = result.listBucket;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Downloading an Object
[//]: # (.cssg-snippet-get-object)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Specify the file name of the file to be saved locally
  GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  GetObjectResult result = cosXml.GetObject(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}

// Download the returned bytes data
try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.

  GetObjectBytesRequest request = new GetObjectBytesRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  GetObjectBytesResult result = cosXml.GetObject(request);
  // Get content
  byte[] content = result.content;
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Delete an object
[//]: # (.cssg-snippet-delete-object)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  DeleteObjectResult result = cosXml.DeleteObject(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```
