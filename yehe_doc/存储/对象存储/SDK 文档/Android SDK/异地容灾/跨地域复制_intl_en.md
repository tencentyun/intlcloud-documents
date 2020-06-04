## Overview

This document provides an overview of APIs and SDK code samples related to cross-region replication.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Setting Cross-Region Replication

#### Feature

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket.

#### Method prototype
```java
PutBucketReplicationResult putBucketReplication(PutBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketReplicationAsync(PutBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-put-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
string ownerUin = "100000000001"; //Replication initiator identifier: OwnerUin
string subUin = "100000000001"; //Replication initiator identifier: SubUin
PutBucketReplicationRequest putBucketReplicationRequest = new PutBucketReplicationRequest(bucket);
putBucketReplicationRequest.setReplicationConfigurationWithRole(ownerUin, subUin);
PutBucketReplicationRequest.RuleStruct ruleStruct = new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Identifies the replication rule
ruleStruct.isEnable = true; // Indicates if the Rule is enabled. true: enabled; false: not enabled
ruleStruct.region = "ap-beijing"; // Destination bucket region
ruleStruct.bucket = "destinationbucket-1250000000";  // Destination bucket
ruleStruct.prefix = "34"; // Prefix matching policy
putBucketReplicationRequest.setReplicationConfigurationWithRule(ruleStruct);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketReplicationRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutBucketReplicationResult putBucketReplicationResult = cosXmlService.putBucketReplication(putBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.putBucketReplicationAsync(putBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketReplicationResult putBucketReplicationResult = (PutBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo PUT Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Source bucket in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| ownerUin  |Replication initiator identifier: OwnerUin  | String |
| subUin  |Replication initiator identifier: SubUin    | String |
| ruleStruct  | Indicates whether the signature verifies the query parameters in the request URL | RuleStruct |
| queryParameterKeys |  Indicates whether to verify the query parameters in the request URL for the signature |  `Set<String>` |
| headerKeys  | Indicates whether to verify the headers for the signature | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description
The result of the request is returned through PutBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).




## Querying Cross-Region Replication

#### Feature

This API (GET Bucket replication) is used to query the cross-region replication rules of a specified bucket.

#### Method prototype
```java
GetBucketReplicationResult getBucketReplication(GetBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void getBucketReplicationAsync(GetBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-get-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketReplicationRequest getBucketReplicationRequest = new GetBucketReplicationRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketReplicationRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketReplicationResult getBucketReplicationResult = cosXmlService.getBucketReplication(getBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.getBucketReplicationAsync(getBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketReplicationResult getBucketReplicationResult = (GetBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo GET Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket for which to query cross-region replication in the format: BucketName-APPID. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| headerKeys  | Indicates whether to verify the headers for the signature | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through GetBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |
| replicationConfiguration | [ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ReplicationConfiguration.java) | The cross-region replication configuration of the bucket under the specified account is returned                    |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).


## Deleting Cross-Region Replication

#### Feature

This API (DELETE Bucket replication) is used to delete the cross-region replication rules of a bucket.

#### Method prototype
```java
DeleteBucketReplicationResult deleteBucketReplication(DeleteBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void deleteBucketReplicationAsync(DeleteBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-delete-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketReplicationRequest deleteBucketReplicationRequest = new DeleteBucketReplicationRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketReplicationRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    DeleteBucketReplicationResult deleteBucketReplicationResult = cosXmlService.deleteBucketReplication(deleteBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.deleteBucketReplicationAsync(deleteBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketReplicationResult deleteBucketReplicationResult = (DeleteBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo DELETE Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket for which to delete cross-region replication in the format: BucketName-APPID. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| headerKeys  | Indicates whether to verify the headers for the signature | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description

The result of the request is returned through DeleteBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

