## Overview

The SDK for .NET provides APIs for getting object URLs and pre-signed request URLs as well as those for calculating signatures.

## Getting an object URL 

```C#
string GetAccessURL(CosRequest request);
```

## Signature calculation

```C#
string GenerateSign(string method, string path, Dictionary<string, string> queryParameters, Dictionary<string, string> headers, long signDurationSecond);
```

## Obtaining a pre-signed URL for requests 

```C#
string GenerateSignURL(PreSignatureStruct preSignatureStruct);
```

#### Parameter description

| Parameter Name | Type | Description |
| ------------------ | ---------------------------- | ------------------------------- |
| request            | CosRequest                   | Request object                        |
| preSignatureStruct | PreSignatureStruct           | Pre-signed URL instance |
| method            | string                   | HTTP request method                        |
| path | string | HTTP request path, i.e., the object key |
| headers            | `Dictionary<string, string>` | Signature request header |
| queryParameters | `Dictionary<string, string>` | Signature request parameter  |
| signDurationSecond | long                         | Signature's validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value should be 60          |

#### `PreSignatureStruct` structure description

Get the corresponding pre-signed request URL is obtained through the PreSignatureStruct object to send requests.

| Parameter Name | Type | Description |
| ------------------ | ---------------------------- | ---------------------------------- |
| appid              | string                       | Tencent Cloud account APPID                   |
| bucket             | string                       | Bucket                             |
| region             | string                       | Bucket region                     |
| method             | string                       | HTTP request method                      |
| isHttps            | bool                         | <li>true: HTTPS request<br><li>false: HTTP request |
| key                | string                       | Object key                             |
| headers            | `Dictionary<string, string>` | Signature request header |
| queryParameters | `Dictionary<string, string>` | Signature request parameter  |
| signDurationSecond | long                         | Signature's validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value should be 60          |

## Sample request

#### Example for uploading requests

[//]: # (.cssg-snippet-get-presign-upload-url)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000") // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Sets the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  preSignatureStruct.appid = "1250000000";// APPID of your Tencent Cloud account
  preSignatureStruct.region = "COS_REGION"; // Bucket region
  preSignatureStruct.bucket = "examplebucket-1250000000"; // Bucket
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "PUT"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generates an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; // Request signature duration is 600s
  preSignatureStruct.headers = null;// Header in the signature that needs to be verified
  preSignatureStruct.queryParameters = null; // URL request parameters in the signature that need to be verified

  // Pre-signed URL for upload (signed URL calculated with the permanent key method)
  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct);

  string srcPath = @"temp-source-file";// Absolute path to the local file
  PutObjectRequest request = new PutObjectRequest(null, null, srcPath);
  // Set the pre-signed URL for upload request
  request.RequestURLWithSign = requestSignURL;
  // Set progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  PutObjectResult result = cosXml.PutObject(request);
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

#### Samples for downloading requests

[//]: # (.cssg-snippet-get-presign-download-url)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000") // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Sets the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  PreSignatureStruct preSignatureStruct = new PreSignatureStruct();
  preSignatureStruct.appid = "1250000000";// APPID of your Tencent Cloud account
  preSignatureStruct.region = "COS_REGION"; // Bucket region
  preSignatureStruct.bucket = "examplebucket-1250000000"; // Bucket
  preSignatureStruct.key = "exampleobject"; // Object key
  preSignatureStruct.httpMethod = "GET"; // HTTP request method
  preSignatureStruct.isHttps = true; // Generates an HTTPS request URL
  preSignatureStruct.signDurationSecond = 600; // Request signature duration is 600s
  preSignatureStruct.headers = null;// Header in the signature that needs to be verified
  preSignatureStruct.queryParameters = null; // URL request parameters in the signature that need to be verified

  string requestSignURL = cosXml.GenerateSignURL(preSignatureStruct); 

  // Pre-signed URL for download request (signed URL calculated with the permanent key method)
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Specifies the name of the file to be saved locally
  GetObjectRequest request = new GetObjectRequest(null, null, localDir, localFileName);
  // Set the pre-signed download request URL
  request.RequestURLWithSign = requestSignURL;
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
```
