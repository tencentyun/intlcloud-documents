## Overview

This document provides an overview of SDK code samples related to generating pre-signed object URLs.

>?
> - You are advised to use a temporary key to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> - For more information about how to get a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
> 


## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Generating a Pre-Signed Object URL

#### Sample code 1. Generate a pre-signed URL

[//]: # (.cssg-snippet-get-presign-download-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  // For details about how to get the APPID, visit https://console.cloud.tencent.com/developer.
  preSignatureStruct.appid = "1250000000";
  // Bucket region. For the abbreviations of COS regions, visit https://intl.cloud.tencent.com/zh/document/product/436/6224.
  preSignatureStruct.region = "COS_REGION"; 
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  preSignatureStruct.bucket = "examplebucket-1250000000";
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "GET"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generate an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; // Request signature duration is 600s
  preSignatureStruct.headers = null;// Header in the signature that needs to be verified
  preSignatureStruct.queryParameters = null; // URL request parameters in the signature that need to be verified

  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); 

  // Pre-signed URL for download request (signed URL calculated with the permanent key method)
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Filename of the local file
  GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
  // Set the pre-signed URL for download requests
  request.RequestURLWithSign = requestSignURL;
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
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
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectPresignUrl.cs).
>

#### Sample code 2. Generate a pre-signed upload URL

[//]: # (.cssg-snippet-get-presign-upload-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  // For details about how to get the APPID, visit https://console.cloud.tencent.com/developer.
  preSignatureStruct.appid = "1250000000";
  // Bucket region. For the abbreviations of COS regions, visit https://intl.cloud.tencent.com/zh/document/product/436/6224.
  preSignatureStruct.region = "COS_REGION";
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  preSignatureStruct.bucket = "examplebucket-1250000000";
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "PUT"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generate an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; // Request signature duration is 600s
  preSignatureStruct.headers = null;// Header in the signature that needs to be verified
  preSignatureStruct.queryParameters = null; // URL request parameters in the signature that need to be verified

  // Pre-signed URL for upload (signed URL calculated with the permanent key method)
  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct);

  string srcPath = @"temp-source-file";// Absolute path of the local file
  PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
  // Set the pre-signed URL for the upload request
  request.RequestURLWithSign = requestSignURL;
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
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
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectPresignUrl.cs).
>


#### Sample code 3. Generate a pre-signed URL with `Host` in the signature

[//]: # (.cssg-snippet-get-presign-download-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  // For details about how to get the APPID, visit https://console.cloud.tencent.com/developer.
  preSignatureStruct.appid = "1250000000";
  // Bucket region. For the abbreviations of COS regions, visit https://intl.cloud.tencent.com/zh/document/product/436/6224.
  preSignatureStruct.region = "COS_REGION"; 
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  preSignatureStruct.bucket = "examplebucket-1250000000";
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "GET"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generate an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; // Request signature duration is 600s
  preSignatureStruct.signHost = true; // Whether to include `Host` in the request signature. It is recommended to include `Host` in the signature to avoid unauthorized requests. Note that if `Host` is included in the signature, the `Host` request header must also be carried in the actual request.
  preSignatureStruct.headers = null;// Header in the signature that needs to be verified
  preSignatureStruct.queryParameters = null; // URL request parameters in the signature that need to be verified

  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); 
  Console.WriteLine("requestUrl is:" + requestSignURL);

  // Pre-signed URL for download request (signed URL calculated with the permanent key method)
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Filename of the local file
  GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
  // Set the pre-signed URL for download requests
  request.RequestURLWithSign = requestSignURL;
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
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
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Sample code 4. Generate a pre-signed URL with request parameters in the signature

[//]: # (.cssg-snippet-get-presign-download-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  // For details about how to get the APPID, visit https://console.cloud.tencent.com/developer.
  preSignatureStruct.appid = "1250000000";
  // Bucket region. For the abbreviations of COS regions, visit https://intl.cloud.tencent.com/zh/document/product/436/6224.
  preSignatureStruct.region = "COS_REGION"; 
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  preSignatureStruct.bucket = "examplebucket-1250000000";
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "GET"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generate an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; // Request signature duration is 600s
  preSignatureStruct.signHost = true; // Whether to include `Host` in the request signature. It is recommended to include `Host` in the signature to avoid unauthorized requests. Note that if `Host` is included in the signature, the `Host` request header must also be carried in the actual request.
  preSignatureStruct.headers = null;// Headers in the signature that need to be verified
  string ci_params = "imageMogr2/thumbnail/!50p";
  preSignatureStruct.queryParameters = new Dictionary<string, string>(); // Request parameters in the URL in the signature that need to be verified. Take a CI image processing request as an example.
  preSignatureStruct.queryParameters.Add(ci_params, null);

  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); 
  Console.WriteLine("requestUrl is:" + requestSignURL);

  // Pre-signed URL for download request (signed URL calculated with the permanent key method)
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Filename of the local file
  GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
  // Set the pre-signed URL for download requests
  request.RequestURLWithSign = requestSignURL;
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
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
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

