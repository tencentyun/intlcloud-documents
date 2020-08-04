## Overview

This document provides an overview of APIs and SDK code samples related to cross-region replication.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules from a bucket |

## SDK API References

For parameters and method descriptions of all SDK APIs, see [SDK API References](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Cross-Region Replication

#### API description

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
PutBucketReplicationRequest putBucketReplicationRequest =
        new PutBucketReplicationRequest(bucket);

string ownerUin = "100000000001"; //Replication initiator identifier: OwnerUin
string subUin = "100000000001"; //Replication initiator identifier: SubUin
putBucketReplicationRequest.setReplicationConfigurationWithRole(ownerUin,
        subUin);

PutBucketReplicationRequest.RuleStruct ruleStruct =
        new PutBucketReplicationRequest.RuleStruct();
//Identifies the name of a specific rule
ruleStruct.id = "replication_01";
//Identify whether to enable the rule. true: enabled; false: disabled
ruleStruct.isEnable = true;
//Destination bucket region
ruleStruct.region = "ap-beijing";
//Destination bucket
ruleStruct.bucket = "destinationbucket-1250000000";
//Prefix matching policy
ruleStruct.prefix = "dir/";
putBucketReplicationRequest.setReplicationConfigurationWithRule(ruleStruct);

cosXmlService.putBucketReplicationAsync(putBucketReplicationRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketReplicationResult putBucketReplicationResult =
                (PutBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketReplication.java).

## Querying Cross-Region Replication

#### API description

This API (GET Bucket replication) is used to query the cross-region replication rules of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
GetBucketReplicationRequest getBucketReplicationRequest =
        new GetBucketReplicationRequest(bucket);

cosXmlService.getBucketReplicationAsync(getBucketReplicationRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketReplicationResult getBucketReplicationResult =
                (GetBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketReplication.java).

## Deleting Cross-Region Replication

#### API description

This API (DELETE Bucket replication) is used to delete the cross-region replication rules from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; //Format: BucketName-APPID
DeleteBucketReplicationRequest deleteBucketReplicationRequest =
        new DeleteBucketReplicationRequest(bucket);

cosXmlService.deleteBucketReplicationAsync(deleteBucketReplicationRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                DeleteBucketReplicationResult deleteBucketReplicationResult =
                        (DeleteBucketReplicationResult) result;
            }

            @Override
            public void onFail(CosXmlRequest cosXmlRequest,
                               CosXmlClientException clientException,
                               CosXmlServiceException serviceException) {
                if (clientException != null) {
                    clientException.printStackTrace();
                } else {
                    serviceException.printStackTrace();
                }
            }
        });
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketReplication.java).

