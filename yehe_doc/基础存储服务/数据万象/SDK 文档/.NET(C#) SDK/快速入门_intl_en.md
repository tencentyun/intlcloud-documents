## Resources

- Download the XML .NET SDK source code [here](https://github.com/tencentyun/qcloud-sdk-dotnet).
- Download XML .NET SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-dotnet/latest/qcloud-sdk-dotnet.zip).
- For the SDK APIs and their parameters, see [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com).
- Find the complete code [here](https://github.com/tencentyun/cos-snippets/tree/master/dotnet).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
- For SDK FAQs, see [.NET (C#) SDK FAQs](https://intl.cloud.tencent.com/document/product/436/40773).


>? If you encounter errors such as non-existent functions or methods when using the SDK, you can update the SDK to the latest version and try again.
>


## Step 1. Integrate the SDK

#### Environmental dependencies

The .NET SDK is developed based on .NET Standard 2.0.

- Windows: Install .NET Core 2.0 or above or .NET Framework 2.0 or above. 
- For Linux/Mac users: Install .NET Core 2.0 or above.

#### Installing the SDK

You can install the SDK using NuGet by adding the following to the `csproj` file in your project:

```xml
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.*" />
```

If .NET CLI is used instead, run the following command:

```sh
dotnet add package Tencent.QCloud.Cos.Sdk
```

If you develop for the target framework .Net Framework 4.0 or below, please download [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) and use `COSXML-Compatible.dll`.

In your Visual Studio project, click **Project** > **Add Reference** > **Browse** > **COSXML-Compatible.dll** to add the .NET(C#) SDK.

>? The compatible package does not support features such as advanced upload and download. For details, see [Backward Compatibility](https://intl.cloud.tencent.com/document/product/436/42378).
>


## Step 2. Initialize COS Services

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


The section below describes how to perform basic COS operations with the .NET SDK, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object.


>? For the definition of terms such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
>

Namespaces commonly used in this SDK include:

```C#
using COSXML;
using COSXML.Auth;
using COSXML.Model.Object;
using COSXML.Model.Bucket;
using COSXML.CosException;
```

Before making any COS requests, always instantiate the following 3 objects: `CosXmlConfig`, `QCloudCredentialProvider`, and `CosXmlServer`.

- `CosXmlConfig` provides an API to configure SDK.
- `QCloudCredentialProvider` provides an API to set the key information.
- `CosXmlServer` provides APIs to perform operations on COS API services.

>? The initialization sample below uses a temporary key. For more information about how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

### 1. Initialize a COS service

```cs
// Initialize CosXmlConfig. 
string appid = "1250000000";// Set the APPID of your Tencent Cloud account.
string region = "COS_REGION"; // Set the default bucket region.
CosXmlConfig config = new CosXmlConfig.Builder()
  .IsHttps(true)  // Set HTTPS as default request method.
  .SetRegion(region)  // Set the default bucket region.
  .SetDebugLog(true)  // Display logs.
  .Build();  // Create a CosXmlConfig object.
```

### 2. Provide access credentials

The SDK supports three types of access credentials: updated temporary keys, unchanging temporary keys, and permanent keys.

**Type 1: updated temporary key**

Since temporary keys are short term, you can obtain new ones using the following method:

```cs
public class CustomQCloudCredentialProvider : DefaultSessionQCloudCredentialProvider
{

  // Even if you do not already have a current temporary key, you can still use this method.
  public CustomQCloudCredentialProvider(): base(null, null, 0L, null) {
    ;
  }

  public override void Refresh()
  {
    //... First, request a temporary key from Tencent Cloud.
    string tmpSecretId = "SECRET_ID"; // SecretId of a temporary key. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
    string tmpSecretKey = "SECRET_KEY"; // SecretKey of a temporary key. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
    string tmpToken = "COS_TOKEN"; // Token of a temporary key. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
    long tmpStartTime = 1546860702;// Start time in seconds of the temporary key’s validity period
    long tmpExpireTime = 1546862502;// End time in seconds of the temporary key’s validity period
    // Call the API to update the key
    SetQCloudCredential(tmpSecretId, tmpSecretKey, 
      String.Format("{0};{1}", tmpStartTime, tmpExpiredTime), tmpToken);
  }
}

QCloudCredentialProvider cosCredentialProvider = new CustomQCloudCredentialProvider();
```

**Type 2: unchanging temporary key (not recommended)**

>! This method is not recommended as a request may fail if the temporary key has expired at the time of request.
>

```cs
string tmpSecretId = "SECRET_ID"; // “SecretId of the temporary key”;
string tmpSecretKey = "SECRET_KEY"; // “SecretKey of the temporary key”;
string tmpToken = "COS_TOKEN"; // “Token of the temporary key”;
long tmpExpireTime = 1546862502;// End time in seconds of the temporary key’s validity period
QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(
  tmpSecretId, tmpSecretKey, tmpExpireTime, tmpToken);
```

**Type 3: permanent key (not recommended)**

```cs
string secretId = Environment.GetEnvironmentVariable("SECRET_ID"); // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
string secretKey = Environment.GetEnvironmentVariable("SECRET_KEY"); // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
long durationSecond = 600;          // Validity period of each request signature in seconds
QCloudCredentialProvider cosCredentialProvider = new DefaultQCloudCredentialProvider(
  secretId, secretKey, durationSecond);
```

### 3. Initialize CosXmlServer

Use `CosXmlConfig` and `QCloudCredentialProvider` to initialize the `CosXmlServer` service class. We recommend you use the service class as a **singleton** in your project.

```cs
CosXml cosXml = new CosXmlServer(config, cosCredentialProvider);
```

## Step 3. Access COS

### Creating a bucket
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  // Execute the request
  PutBucketResult result = cosXml.PutBucket(request);
  // Request succeeded
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

### Querying the bucket list
```cs
try
{
  GetServiceRequest request = new GetServiceRequest();
  // Execute the request
  GetServiceResult result = cosXml.GetService(request);
  // Get the list of all buckets.
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

### Uploading an object
```cs
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
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
} catch (Exception e){
    Console.WriteLine("CosException: " + e);
}
```

### Querying objects

```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
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
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Downloading an object

```cs
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
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
} catch (Exception e){
    Console.WriteLine("CosException: " + e);
}
```

### Deleting an object

```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  // Execute the request
  DeleteObjectResult result = cosXml.DeleteObject(request);
  // Request succeeded
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
