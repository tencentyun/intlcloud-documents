## Overview

This document provides an overview of SDK code samples related to generating pre-signed object URLs.

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Generating a Pre-Signed Object URL

#### Sample 1. Generating a pre-signed upload URL

[//]: # (.cssg-snippet-get-presign-upload-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  preSignatureStruct.appid = "1250000000";// APPID of your Tencent Cloud account
  preSignatureStruct.region = "COS_REGION"; // Bucket region
  preSignatureStruct.bucket = "examplebucket-1250000000"; // Bucket
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "PUT"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generate an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; //The duration of a request signature is 600 s
  preSignatureStruct.headers = null;// Headers to verify in the signature
  preSignatureStruct.queryParameters = null; // URL request parameters to verify in the signature

  // A pre-signed URL for upload (calculated with your permanent key)
  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct);

  string srcPath = @"temp-source-file";// Absolute path to the local file
  PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
  // Set the pre-signed URL for upload requests
  request.RequestURLWithSign = requestSignURL;
  // Set progress callback
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectPresignUrl.cs).

#### Sample 2. Generating a pre-signed download URL

[//]: # (.cssg-snippet-get-presign-download-url)
```cs
try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  preSignatureStruct.appid = "1250000000";// APPID of your Tencent Cloud account
  preSignatureStruct.region = "COS_REGION"; // Bucket region
  preSignatureStruct.bucket = "examplebucket-1250000000"; // Bucket
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "GET"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generate an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; //The duration of a request signature is 600 s
  preSignatureStruct.headers = null;// Headers to verify in the signature
  preSignatureStruct.queryParameters = null; // URL request parameters to verify in the signature

  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); 

  // Pre-signed URL for download requests (calculated with your permanent key)
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally
  GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
  // Set the pre-signed URL for download requests
  request.RequestURLWithSign = requestSignURL;
  // Set progress callback
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectPresignUrl.cs).

