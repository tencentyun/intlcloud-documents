## Overview

This document provides an overview of APIs and SDK code samples related to cross-region replication.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication rule | Sets a cross-region replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication rule | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication rule | Deletes a cross-region replication rule from a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Cross-Region Replication Rule

#### API description 

This API is used to set a cross-region replication rule for a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-replication)
```cs
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
string ownerUin = "100000000001"; //Replication initiator identifier: OwnerUin
string subUin = "100000000001"; //Replication initiator identifier: SubUin
PutBucketReplicationRequest request = new PutBucketReplicationRequest(bucket);
// Set replication
PutBucketReplicationRequest.RuleStruct ruleStruct = 
  new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Identify the replication rule
ruleStruct.isEnable = true; // Indicates whether the rule is enabled. true: enabled; false: not enabled
ruleStruct.appid = "1250000000"; // APPID
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketInventory.cs).

## Querying Cross-Region Replication Rule

#### API description 

This API is used to query the cross-region replication rule of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-replication)
```cs
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketReplicationRequest request = new GetBucketReplicationRequest(bucket);
try
{
  GetBucketReplicationResult result = cosXml.GetBucketReplication(request);
  // Bucket’s cross-region replication configuration
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketInventory.cs).

## Deleting Cross-Region Replication Rule

#### API description 

This API is used to delete the cross-region replication rule from a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-replication)
```cs
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketInventory.cs).

