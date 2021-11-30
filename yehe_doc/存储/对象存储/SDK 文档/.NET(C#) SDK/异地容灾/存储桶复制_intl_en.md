## Overview

This document provides an overview of APIs and SDK code samples related to bucket copying.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-bucket replication | Sets a cross-bucket replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-bucket replication | Queries the cross-bucket replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-bucket replication | Deletes a cross-bucket replication rule of a bucket |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Cross-Bucket Replication

#### API description

This API is used to set a cross-bucket replication rule for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-replication)
```cs
// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
string ownerUin = "100000000001"; //Replication initiator identifier: OwnerUin
string subUin = "100000000001"; //Replication initiator identifier: SubUin
PutBucketReplicationRequest request = new PutBucketReplicationRequest(bucket);
// Set replication
PutBucketReplicationRequest.RuleStruct ruleStruct = 
  new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Identifies the replication rule
ruleStruct.isEnable = true; // Indicates whether the rule is enabled. true: enabled; false: not enabled
ruleStruct.appid = "1250000000"; //APPID
ruleStruct.region = "ap-beijing"; // Destination bucket region
ruleStruct.bucket = "destinationbucket-1250000000"; // Format: BucketName-APPID
ruleStruct.prefix = "34"; // Prefix matching policy
List<PutBucketReplicationRequest.RuleStruct> ruleStructs = 
  new List<PutBucketReplicationRequest.RuleStruct>();
ruleStructs.Add(ruleStruct);
request.SetReplicationConfiguration(ownerUin, subUin, ruleStructs);

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

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReplication.cs).

## Querying Cross-Bucket Replication

#### API description

This API is used to query the cross-bucket replication rule of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-replication)
```cs
// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
GetBucketReplicationRequest request = new GetBucketReplicationRequest(bucket);
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

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReplication.cs).

## Deleting Cross-Bucket Replication

#### API description

This API is used to delete the cross-bucket replication rule set for a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-replication)
```cs
// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
DeleteBucketReplicationRequest request = new DeleteBucketReplicationRequest(bucket);
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

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReplication.cs).

