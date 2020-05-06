## Overview

This document provides an overview of APIs and SDK code samples related to cross-region replication.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rules for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Setting cross-region replication

#### Feature description

This API is used to set the cross-region replication rules for a bucket.

#### Method prototype

```C#
PutBucketReplicationResult PutBucketReplication(PutBucketReplicationRequest request);
void PutBucketReplication(PutBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-replication)
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

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
string ownerUin = "100000000001"; //Replication initiator identifier: OwnerUin
string subUin = "100000000001"; //Replication initiator identifier: SubUin
PutBucketReplicationRequest request = new PutBucketReplicationRequest(bucket);
// Set replication
PutBucketReplicationRequest.RuleStruct ruleStruct = 
  new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Used to identify the name of the replication rule
ruleStruct.isEnable = true; // Indicates whether the Rule is enabled. true: enabled; false: not enabled
ruleStruct.appid = "1250000000"; // APPID
ruleStruct.region = "ap-beijing"; // Destination bucket region
ruleStruct.bucket = "destinationbucket-1250000000"; // Format: BucketName-APPID
ruleStruct.prefix = "34"; // Prefix matching policy
List<PutBucketReplicationRequest.RuleStruct> ruleStructs = 
  new List<PutBucketReplicationRequest.RuleStruct>();
ruleStructs.Add(ruleStruct);
request.SetReplicationConfiguration(ownerUin, subUin, ruleStructs);

// Use the sync method
try
{
  PutBucketReplicationResult result = cosXml.PutBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Source bucket in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| ownerUin  |Replication initiator identifier: OwnerUin  | string |
| subUin  |Replication initiator identifier: SubUin    | string |
| ruleStruct | Signature request parameter | RuleStruct |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys          | Signature request header                | `List<string>` |
| queryParameterKeys | SetSign | Signature request parameter | `List<string>` |


#### Response description
The result of the request is returned through PutBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.




## Querying cross-region replication

#### Feature description

This API is used to query the cross-region replication rules of a specified bucket.

#### Method prototype
```C#
GetBucketReplicationResult GetBucketReplication(GetBucketReplicationRequest request);
void GetBucketReplication(GetBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-replication)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000") // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Sets the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // The Secretid of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketReplicationRequest request = new GetBucketReplicationRequest(bucket);

// Use the sync method
try
{
  GetBucketReplicationResult result = cosXml.GetBucketReplication(request);
  // Bucket cross-region replication configuration
  ReplicationConfiguration conf =  result.replicationConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket for which to query cross-region replication in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys          | Signature request header                | `List<string>` |
| queryParameterKeys | SetSign | Signature request parameter | `List<string>` |

#### Response description
The result of the request is returned through GetBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
|replicationConfiguration|[ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ReplicationConfiguration.cs)|Cross-origin access configuration|


>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Deleting a cross-region replication

#### Feature description

This API is used to delete the cross-region replication rule of the specified bucket.

#### Method prototype
```C#
DeleteBucketReplicationResult DeleteBucketReplication(DeleteBucketReplicationRequest request);
void DeleteBucketReplication(DeleteBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # (.cssg-snippet-delete-bucket-replication)
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

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketReplicationRequest request = new DeleteBucketReplicationRequest(bucket);

// Use the sync method
try
{
  DeleteBucketReplicationResult result = cosXml.DeleteBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description

| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket for which to delete cross-region replication in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys          | Signature request header                | `List<string>` |
| queryParameterKeys | SetSign | Signature request parameter | `List<string>` |


#### Response description
The result of the request is returned through DeleteBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.
