## Overview

This document provides an overview of APIs and SDK code samples related to cross-region replication.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rules for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Setting cross-region replication rules

#### Feature description

This API is used to set the cross-region replication rules for a bucket.

> Buckets must have version control enabled to use cross-region replication.

#### Sample request

[//]: # (.cssg-snippet-put-bucket-replication)
```js
cos.putBucketReplication({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    ReplicationConfiguration: { /*Required*/
        Role: "qcs::cam::uin/100000000001:uin/100000000001",
        Rules: [{
            ID: "1",
            Status: "Enabled",
            Prefix: "sync/",
            Destination: {
                Bucket: "qcs::cos:ap-beijing::destinationbucket-1250000000",
                StorageClass: "Standard",
            }
        }]
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Source bucket in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ReplicationConfiguration | Defines cross-region replication rules | Object | Yes |
| - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object | No |
| - Rules | List of specific replication rules | ObjectArray | Yes |
| - - ID | Identifies the ID of a specific rule | String | No |
| - - Status | Identifies whether the rule is in effect. Enumerated values: Enabled, Disabled | String | Yes |
| - - Prefix | Prefix matching policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | String      | No   |
| - - Destination | Destination bucket information | Object | Yes |
| - - - Bucket             | Destination bucket name in the format: `qcs::cos:<Region>::<BucketName-APPID>`<br>Example: `qcs::cos:ap-beijing::destinationbucket-1250000000` | Object      | Yes   |
| - - - StorageClass | Storage class of the copied object; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Querying cross-region replication rules

#### Feature description

This API is used to query the cross-region replication rules of a bucket.

#### Sample request

[//]: # (.cssg-snippet-get-bucket-replication)
```js
cos.getBucketReplication({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "ReplicationConfiguration": {
        "Role": "qcs::cam::uin/100000000001:uin/100000000001",
        "Rules": {
            "ID": "1",
            "Status": "Enabled",
            "Prefix": "sync/",
            "Destination": {
                "Bucket": "qcs::cos:ap-beijing::destinationbucket-1250000000",
                "StorageClass": "Standard"
            }
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format: `BucketName-APPID`. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - ReplicationConfiguration | Cross-region replication rule | Object |
| - - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object |
| - - Rules | List of specific replication rules | ObjectArray |
| - - - ID | Identifies the ID of a specific rule | String |
| - - - Status | Identifies whether the rule is in effect. Enumerated values: Enabled, Disabled | String |
| - - - Prefix    | Prefix matching policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | String |
| - - - Destination | Destination bucket information | Object |
| - - - - Bucket             | Destination bucket name in the format: `qcs::cos:<Region>::<BucketName-APPID>`<br>Example: `qcs::cos:ap-beijing::destinationbucket-1250000000` | Object      |
| - - - - StorageClass | Storage class of the copied object; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object |


## Deleting cross-region replication rules

#### Feature description

This API is used to delete the cross-region replication rules of a bucket.

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-replication)
```js
cos.deleteBucketReplication({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format: `BucketName-APPID`. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
