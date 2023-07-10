## Overview

This document provides an overview of APIs and SDK code samples related to custom domains.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Custom Domains

#### Description

This API (PUT Bucket domain) is used to set a custom domain for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-domain)
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  
  DomainConfiguration domain = new DomainConfiguration();
  domain.rule = new DomainConfiguration.DomainRule();
  domain.rule.Name = "www.qq.com";
  domain.rule.Status = "ENABLED";
  domain.rule.Type = "WEBSITE";
  
  PutBucketDomainRequest request = new PutBucketDomainRequest(bucket, domain);   
  // Execute the request
  PutBucketDomainResult result = cosXml.PutBucketDomain(request);
  
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketDomain.cs).

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Description

This API (GET Bucket domain) is used to query the custom domain set for a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-domain)
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  GetBucketDomainRequest request = new GetBucketDomainRequest(bucket);   
  // Execute the request
  GetBucketDomainResult result = cosXml.GetBucketDomain(request);
  
  // Request succeeded
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketDomain.cs).


#### Response parameters

<table>
<thead>
<tr>
<th>Parameter Name</th>
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

