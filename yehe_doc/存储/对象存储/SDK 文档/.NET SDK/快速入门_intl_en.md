## Relevant Resources

- Download the XML SDK for .NET source code [here](https://github.com/tencentyun/qcloud-sdk-dotnet).
- For the SDK APIs and their parameters, please see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com).
- Find the complete sample code [here](https://github.com/tencentyun/cos-snippets/tree/master/dotnet).
- Download the XML SDK for .NET [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-dotnet/latest/qcloud-sdk-dotnet.zip).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).

## Step 1. Integrate the SDK

#### Environmental dependency

The .NET SDK is developed based on .NET Standard 2.0.

- For Windows users: Install .NET Core 2.0 or above or .NET Framework 4.6.1 or above. 
- For Linux/Mac users: Install .NET Core 2.0 or above.

#### Installing SDK

You can install the SDK using NuGet by adding the following to the `csproj` file in your project:

```xml
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.*" />
```

If .NET CLI is used instead, run the following command:

```sh
dotnet add package Tencent.QCloud.Cos.Sdk
```

## Step 2. Initiate COS services

The section below describes how to perform basic COS operations with the SDK for .NET, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object.


>?For more information on the meanings of parameters such as `SecretId`, `SecretKey`, and `Bucket` contained herein and how to get them, please see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).

Namespaces commonly used in this SDK include:

```C#
using COSXML;
using COSXML.Auth;
using COSXML.Model.Object;
using COSXML.Model.Bucket;
using COSXML.CosException;
```

Before making any COS requests, always instantiate the following 3 objects: `CosXmlConfig`, `QCloudCredentialProvider`, and `CosXmlServer`.

- `CosXmlConfig` provides an API to configure the SDK.
- `QCloudCredentialProvider` provides an API to set the key information.
- `CosXmlServer` provides APIs for COS operations.

>?The initialization samples below use temporary keys. For more information on how to generate and use them, please see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048).

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

### 2. Provide access credentials.

The SDK supports three types of access credentials: permanent keys, updated temporary keys, and unchanging temporary keys.

**Type 1: permanent key**

```cs
String secretId = "COS_SECRETID"; // "SecretId of your TencentCloud API key"
String secretKey = "COS_SECRETKEY"; // "SecretKey of your TencentCloud API key"
long durationSecond = 600;          // Validity period of each request signature in seconds
QCloudCredentialProvider cosCredentialProvider = new DefaultQCloudCredentialProvider(
  secretId, secretKey, durationSecond);
```

**Type 2: updated temporary key**

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
    String tmpSecretId = "COS_SECRETID"; // "SecretId of the temporary key";
    String tmpSecretKey = "COS_SECRETKEY"; // "SecretKey of the temporary key";
    string tmpToken = "COS_TOKEN"; // "Token of the temporary key";
    long tmpStartTime = 1546860702;// Start time in seconds of the temporary key's validity period
    long tmpExpiredTime = 1546862502;// End time in seconds of the temporary key's validity period
    // Call the API to update the key.
    SetQCloudCredential(tmpSecretId, tmpSecretKey, 
      String.Format("{0};{1}", tmpStartTime, tmpExpiredTime), tmpToken);
  }
}

QCloudCredentialProvider cosCredentialProvider = new CustomQCloudCredentialProvider();
```

**Type 3: unchanging temporary key (not recommended)**

Note that your request may fail if you use an expired temporary key from a previous request.

```cs
String tmpSecretId = "COS_SECRETID"; // "SecretId of the temporary key";
String tmpSecretKey = "COS_SECRETKEY"; // "SecretKey of the temporary key";
string tmpToken = "COS_TOKEN"; // "Token of the temporary key";
long tmpExpireTime = 1546862502;// End time in seconds of the temporary key's validity period
QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(
  tmpSecretId, tmpSecretKey, tmpExpireTime, tmpToken);
```

### 3. Initialize CosXmlServer.

We recommend you use `CosXmlConfig` and `QCloudCredentialProvider` to initialize the `CosXmlServer` service class as a **singleton** in your program.

```cs
CosXml cosXml = new CosXmlServer(config, cosCredentialProvider);
```

## Step 3. Access COS

### Creating bucket
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  // Execute the request.
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

### Querying bucket list
```cs
try
{
  GetServiceRequest request = new GetServiceRequest();
  // Execute the request.
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

### Uploading object
```cs
// Initialize TransferConfig.
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.
String srcPath = @"temp-source-file";// Absolute path to the local file

// Upload an object.
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
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Execute the request.
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

### Downloading object

```cs
// Initialize TransferConfig.
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local folder
string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved in the local file system.

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
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  // Execute the request.
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
