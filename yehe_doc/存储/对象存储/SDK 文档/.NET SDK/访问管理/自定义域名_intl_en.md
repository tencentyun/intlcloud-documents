## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain | Querying custom domain name | Queries the custom domain name information of a bucket |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

```
PutBucketDomainResult putBucketDomain(PutBucketDomainRequest request);

void putBucketDomainAsync(PutBucketDomainRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

```
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the `APPID` of your Tencent Cloud account
  .SetRegion("ap-guangzhou") // Set the default bucket region
  .Build();

string secretId = "COS_SECRETID";   //TencentCloud API key's SecretId
string secretKey = "COS_SECRETKEY"; // TencentCloud API key's SecretKey
long durationSecond = 600;          // Validity period of each request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  
  DomainConfiguration domain = new DomainConfiguration();
  domain.rule = new DomainConfiguration.DomainRule();
  domain.rule.Name = "www.qq.com";
  domain.rule.Status = "ENABLED";
  domain.rule.Type = "WEBSITE";
  
  PutBucketDomainRequest request = new PutBucketDomainRequest(bucket, domain);   
  // Execute the request
  PutBucketDomainResult result = cosXml.putBucketDomain(request);
  
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

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket            | Bucket for which to set a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string                                      |
| Name                  | Custom domain name                                                   | string |
| Status            | Domain name status. Valid values: ENABLED, DISABLED                     | string |
| Type              | Type of bound origin server. Valid values: REST, WEBSITE                       | string |
| Replace | Forcibly overwrites existing configuration. Valid values: CNAME, TXT                    | string |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

#### Returned error code description

Some frequent special errors that may occur with this request are listed below:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | The domain name record already exists, and no forced overwriting is set in the request. Or, the domain name record does not exist, but forced overwriting is set in the request. |
| HTTP 451 Unavailable For Legal Reasons | The domain name is served in Mainland China but has no ICP filing.                          |

## Querying Custom Domain Name

#### Feature description

This API (GET Bucket domain) is used to query the custom domain name information of a bucket.

#### Method prototype

```
GetBucketDomainResult getBucketDomain(GetBucketDomainRequest request);

void getBucketDomainAsync(GetBucketDomainRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

```
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the `APPID` of your Tencent Cloud account
  .SetRegion("ap-guangzhou") // Set the default bucket region
  .Build();

string secretId = "COS_SECRETID";   //TencentCloud API key's SecretId
string secretKey = "COS_SECRETKEY"; // TencentCloud API key's SecretKey
long durationSecond = 600;          // Validity period of each request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketDomainRequest request = new GetBucketDomainRequest(bucket);   
  // Execute the request
  GetBucketDomainResult result = cosXml.getBucketDomain(request);
  
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

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket            | Bucket for which to query a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string                                      |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

#### Return parameter description


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
<td>Domain name verification information. This field is an MD5 check value, whose original string is in the following format: <code>cos[Region][BucketName-APPID][BucketCreateTime]</code>, where `Region` is the bucket region and `BucketCreateTime` is the bucket creation time in GMT</td>
<td>string</td>
</tr>
</tbody></table>
