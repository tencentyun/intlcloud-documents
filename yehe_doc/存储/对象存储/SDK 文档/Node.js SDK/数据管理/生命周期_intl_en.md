## Overview

This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

## Setting a Lifecycle

#### Feature

This API (PUT Bucket lifecycle) is used to set lifecycle configuration on a bucket.

#### Request samples

Sample 1. Transition objects to Standard_IA storage class 30 days after upload

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "1",
        "Status": "Enabled",
        "Filter": {},
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 2. Transition objects with the specified directory prefix `dir/` to ARCHIVE storage class 90 days after upload

[//]: # (.cssg-snippet-put-bucket-lifecycle-archive)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "2",
        "Filter": {
            "Prefix": "dir/",
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 3. Remove the delete markers of expired files 180 days after upload

[//]: # (.cssg-snippet-put-bucket-lifecycle-expired)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "3",
        "Status": "Enabled",
        "Filter": {},
        "Expiration": {
            "Days": "180"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 4. Delete parts uploaded incompletely 30 days after upload

[//]: # (.cssg-snippet-put-bucket-lifecycle-cleanAbort)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "4",
        "Status": "Enabled",
        "Filter": {},
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 5. Transition a historical version to ARCHIVE 30 days after it is generated

[//]: # (.cssg-snippet-put-bucket-lifecycle-historyArchive)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "5",
        "Status": "Enabled",
        "Filter": {},
        "NoncurrentVersionTransition": {
            "NoncurrentDays": "30",
            "StorageClass": 'ARCHIVE'
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                       | Description                                                     | Type        | Required |
| -------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                           | Bucket for which the lifecycle is configured. Format: BucketName-APPID  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Rules | List of specific lifecycle rules | ObjectArray | Yes |
| - ID | Unique rule ID | String | Yes |
| - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String | Yes |
| - Filter | Specifies the filter | Object | Yes |
| - - - Prefix | Object prefix to be matched by the rule | String | No |
| - Transition | Transition attributes in the rule, indicating when the COS storage class is transitioned to Standard_IA or Archive | Object | No  |
| - - Days | Specifies the number of days after the last modified date of the object that the rule’s action occurs. The valid value of this field is a non-negative integer up to 3,650. | Number | Yes |
| - - StorageClass | Indicates the storage class of transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| - NoncurrentVersionTransition | Specifies the transition attributes of a historical object version | ObjectArray | No |
| - - NoncurrentDays | Indicates the historical object version is transitioned after the number of days determined by this value | Number | Yes |
| - - StorageClass | Indicates the storage class of transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. | String | Yes |
| - Expiration | Rule expiration attributes | Object | No |
| - - ExpiredObjectDeleteMarker | Deletes the delete marker of expired object. Enumerated values: `true` and `false`. It cannot be specified with `Days` at the same time. | Boolean | Yes |
| - - Days | Specifies the number of days after the last modified date of the object that the rule’s deletion action occurs. It cannot be specified with `ExpiredObjectDeleteMarker` at the same time. | Number | Yes |
| - AbortIncompleteMultipartUpload | Indicates to delete the parts uploaded incompletely | Object | No |
| - - DaysAfterInitiation | Parts are deleted after the number of days determined by this value, which starts from the file upload time and must be a positive integer. | Number | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Querying a Lifecycle

#### Feature

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration of a bucket.

#### Request samples

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```js
cos.getBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Response samples

```json
{
    "Rules": [{
        "ID": "1",
        "Filter": "",
        "Status": "Enabled",
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }, {
        "ID": "2",
        "Filter": {
            "Prefix": "dir/"
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }, {
        "ID": "3",
        "Filter": "",
        "Status": "Enabled",
        "Expiration": {
            "Days": "180"
        }
    }, {
        "ID": "4",
        "Filter": "",
        "Status": "Enabled",
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }, {
        "ID": "5",
        "Filter": "",
        "Status": "Enabled",
        "NoncurrentVersionTransition:": {
            "NoncurrentDays": "30",
            "StorageClass": "ARCHIVE"
        }
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which the lifecycle is queried. Format: BucketName-APPID  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Rules | List of specific lifecycle rules | ObjectArray |
| - - ID | Unique rule ID | String |
| - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String |
| - - Filter | Specifies the filter | Object |
| - - - Prefix | Key prefix to be matched with the rule | String |
| - - Transition | Transition attributes in the rule, indicating when the COS storage class is transitioned to Standard_IA or Archive | ObjectArray |
| - - - Days | Specifies the number of days after the last modified date of the object that the rule’s action occurs. The valid value of this field is a non-negative integer up to 3,650. | Number |
| - - - StorageClass | Indicates the storage class of transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| - - NoncurrentVersionTransition | Specifies historical version object conversion attributes | ObjectArray |
| - - - NoncurrentDays | Indicates the historical object version is transitioned after the number of days determined by this value | Number |
| - - - StorageClass | Indicates the storage class of transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| - - Expiration | Rule expiration attributes | Object |
| - - - ExpiredObjectDeleteMarker | Deletes the delete marker of expired object. Enumerated values: `true` and `false`. It cannot be specified with `Days` at the same time. | Boolean |
| - - - Days | Specifies the number of days after the last modified date of the object that the rule’s deletion action occurs. It cannot be specified with `ExpiredObjectDeleteMarker` at the same time. | Number |
| - - AbortIncompleteMultipartUpload | Indicates to delete the parts uploaded incompletely | Object |
| - - - DaysAfterInitiation | Parts are deleted after the number of days determined by this value, which starts from the file upload time and must be a positive integer | Number |

## Deleting a Lifecycle

#### Feature

This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket.

#### Request samples

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```js
cos.deleteBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which the lifecycle is deleted. Format: BucketName-APPID  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
