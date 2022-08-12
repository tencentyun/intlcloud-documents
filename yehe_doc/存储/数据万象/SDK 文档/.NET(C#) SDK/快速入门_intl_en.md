## Related Resources

- Download the XML .NET SDK source code from [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet).
- Download the XML .NET SDK from [GitHub](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-dotnet/latest/qcloud-sdk-dotnet.zip).
- For SDK APIs and parameters, see [COS XML .NET SDK](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com).
- For all the code samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
- For SDK FAQs, see [.NET (C#) SDK](https://intl.cloud.tencent.com/document/product/436/40773).


>? If you encounter errors such as non-existent functions or methods when using the SDK, update the SDK to the latest version and try again.
>


## Step 1. Integrate the SDK

#### Environmental dependencies

The .NET SDK is developed based on .NET Standard 2.0.

- Windows: Install .NET Core 2.0 or later or .NET Framework 2.0 or later. 
- Linux/macOS: Install .NET Core 2.0 or later.

#### Installing SDK

You can install the SDK through NuGet by adding the following to the `csproj` file in your project:

```xml
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.*" />
```

If you use .NET CLI, run the following command:

```sh
dotnet add package Tencent.QCloud.Cos.Sdk
```

If you develop for the target framework .NET Framework 4.0 or earlier, download [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) and use the `COSXML-Compatible.dll` file.

In your Visual Studio project, click **Project** > **Add Reference** > **Browse** > **COSXML-Compatible.dll** to add the .NET(C#) SDK.

>? The compatible package does not support features such as advanced upload and download. For more information, see [Backward Compatibility](https://intl.cloud.tencent.com/document/product/436/42378).
>


## Step 2. Initialize the COS service

The section below describes how to use the COS .NET SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, or deleting an object.


>? For the definitions of terms such as `SecretId`, `SecretKey`, and bucket, see [Introduction](https://intl.cloud.tencent.com/document/product/436/7751).
>

Namespaces commonly used in this SDK include:

```C#
using COSXML;
using COSXML.Auth;
using COSXML.Model.Object;
using COSXML.Model.Bucket;
using COSXML.CosException;
```

Before executing any COS requests, you always need to instantiate the following three objects: `CosXmlConfig`, `QCloudCredentialProvider`, and `CosXmlServer`.

- `CosXmlConfig` provides an API for configuring the SDK.
- `QCloudCredentialProvider` provides an API for setting the key information.
- `CosXmlServer` provides APIs for COS operations.

>? The initialization sample below uses a temporary key. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

### 1. Initialize the service

```cs
// Initialize `CosXmlConfig`. 
string appid = "1250000000";// Set the `APPID` of your Tencent Cloud account
string region = "COS_REGION"; // Set the default bucket region
CosXmlConfig config = new CosXmlConfig.Builder()
  .IsHttps(true)  // Set HTTPS as the default request method
  .SetRegion(region)  // Set the default bucket region
  .SetDebugLog(true)  // Display logs
  .Build();  // Create a `CosXmlConfig` object
```

### 2. Provide access credentials

The SDK supports three types of access credentials: permanent keys, continuously updated temporary keys, and unchanged temporary keys.

**Option 1: Permanent key**

```cs
string secretId = "SECRET_ID"; // `SecretId` of your TencentCloud API key
string secretKey = "SECRET_KEY"; // `SecretKey` of your TencentCloud API key
long durationSecond = 600;  // Validity period of the request signature in seconds
QCloudCredentialProvider cosCredentialProvider = new DefaultQCloudCredentialProvider(
  secretId, secretKey, durationSecond);
```

**Option 2: Continuously updated temporary key**

As a temporary key expires after a certain period of time, you can get a new one in the following way:

```cs
public class CustomQCloudCredentialProvider : DefaultSessionQCloudCredentialProvider
{

  // Even if you don't already have a temporary key, you can still use this option for initialization.
  public CustomQCloudCredentialProvider(): base(null, null, 0L, null) {
    ;
  }

  public override void Refresh()
  {
    // First, request a temporary key from Tencent Cloud
    string tmpSecretId = "SECRET_ID"; // `SecretId` of the temporary key
    string tmpSecretKey = "SECRET_KEY"; // `SecretKey` of the temporary key
    string tmpToken = "COS_TOKEN"; // Token of the temporary key
    long tmpStartTime = 1546860702;// Start time of the temporary key's validity period in seconds
    long tmpExpiredTime = 1546862502;// End time of the temporary key's validity period in seconds
    // Call the API to update the key
    SetQCloudCredential(tmpSecretId, tmpSecretKey, 
      String.Format("{0};{1}", tmpStartTime, tmpExpiredTime), tmpToken);
  }
}

QCloudCredentialProvider cosCredentialProvider = new CustomQCloudCredentialProvider();
```

**Option 3: Unchanged temporary key (not recommended)**

>! This option is not recommended as a request may fail if the temporary key has expired at the time of request.
>

```cs
string tmpSecretId = "SECRET_ID"; // `SecretId` of the temporary key
string tmpSecretKey = "SECRET_KEY"; // `SecretKey` of the temporary key
string tmpToken = "COS_TOKEN"; // Token of the temporary key
long tmpExpireTime = 1546862502;// End time of the temporary key's validity period in seconds
QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(
  tmpSecretId, tmpSecretKey, tmpExpireTime, tmpToken);
```

### 3. Initialize `CosXmlServer`

Use `CosXmlConfig` and `QCloudCredentialProvider` to initialize the `CosXmlServer` service class. We recommend you use the service class as a **singleton** in your project.

```cs
CosXml cosXml = new CosXmlServer(config, cosCredentialProvider);
```

## Step 3. Access COS

### Creating bucket
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
  PutBucketRequest request = new PutBucketRequest(bucket);
  // Execute the request
  PutBucketResult result = cosXml.PutBucket(request);
  // The request succeeded.
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // The request failed.
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // The request failed.
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Querying bucket list
```cs
try
{
  GetServiceRequest request = new GetServiceRequest();
  // Execute the request
  GetServiceResult result = cosXml.GetService(request);
  // Get the list of all buckets
  List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // The request failed.
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // The request failed.
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Uploading object
```cs
// Initialize `TransferConfig`
TransferConfig transferConfig = new TransferConfig();

// Initialize `TransferManager`
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
String srcPath = @"temp-source-file";// Absolute path to the local file

// Upload an object
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath);
uploadTask.SetSrcPath(srcPath);

uploadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = await 
    transferManager.UploadAsync(uploadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

### Querying object list

```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // The data is truncated, and the next marker of the data is recorded.
    this.nextMarker = info.nextMarker;
  }
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // The request failed.
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // The request failed.
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Downloading object

```cs
// Initialize `TransferConfig`
TransferConfig transferConfig = new TransferConfig();

// Initialize `TransferManager`
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local directory
string localFileName = "my-local-temp-file"; // Filename of the local file

// Download an object
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
  localDir, localFileName);

downloadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
    transferManager.DownloadAsync(downloadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

### Deleting object

```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
  string key = "exampleobject"; // Object key
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  // Execute the request
  DeleteObjectResult result = cosXml.DeleteObject(request);
  // The request succeeded.
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // The request failed.
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // The request failed.
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```
