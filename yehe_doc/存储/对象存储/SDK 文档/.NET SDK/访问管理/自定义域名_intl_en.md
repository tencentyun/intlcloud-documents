## Overview

This document provides an overview of APIs and SDK code samples related to custom endpoints.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom endpoint | Sets a custom endpoint for a bucket |
| GET Bucket domain    | Querying a custom endpoint | Queries the custom endpoint of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Custom Endpoint

#### API description 

This API is used to configure a custom endpoint for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-domain)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  
  DomainConfiguration domain = new DomainConfiguration();
  domain.rule = new DomainConfiguration.DomainRule();
  domain.rule.Name = "www.qq.com";
  domain.rule.Status = "ENABLED";
  domain.rule.Type = "WEBSITE";
  
  PutBucketDomainRequest request = new PutBucketDomainRequest(bucket, domain);   
  // Execute the request
  PutBucketDomainResult result = cosXml.PutBucketDomain(request);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketDomain.cs).

#### Error codes

The following describes some common errors that may occur when making requests using this API.

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The endpoint record already exists, and forced overwrite is not specified in the request; OR the endpoint record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The endpoint is a domain name without ICP filing in the Chinese mainland                          |

## Querying a Custom Endpoint

#### API description 

This API is used to query the custom endpoint of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-domain)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketDomainRequest request = new GetBucketDomainRequest(bucket);   
  // Execute the request
  GetBucketDomainResult result = cosXml.GetBucketDomain(request);
  
  // Request successful
  Console.WriteLine(result.domainConfiguration);
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketDomain.cs).


#### Response parameters

<table>
<thead>
<tr>
<th>Parameter Name</td>
<th>Description</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">x-cos-domain-txt-verification</td>
<td>Endpoint verification information. This field is an MD5 checksum of a character string in the format: <code>cos[Region][BucketName-APPID][BucketCreateTime]</code>, where `Region` is the bucket region and `BucketCreateTime` is the time the bucket was created in GMT format</td>
<td>String</td>
</tr>
</tbody></table>

