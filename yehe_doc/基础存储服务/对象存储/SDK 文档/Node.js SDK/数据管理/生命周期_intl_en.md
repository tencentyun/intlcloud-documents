## Overview

This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

## Setting a lifecycle configuration

#### Feature description 

This API is used to set the lifecycle configuration of a bucket.

#### Sample request

Sample 1. Transition objects to the `Standard_IA` storage class 30 days after upload

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

Sample 2. Transition objects with the specified directory prefix `dir/` to the `ARCHIVE` storage class 90 days after upload

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

Sample 4. Delete incomplete multipart uploads 30 days after upload

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

Sample 5. Transition a past version to the `ARCHIVE` 30 days after it is generated

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
| Bucket                           | Bucket for which the lifecycle is configured in the format: BucketName-APPID  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Rules | List of specific lifecycle rules | ObjectArray | Yes |
| - ID | Unique rule ID | String | Yes |
| - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String | Yes |
| - Filter | Specifies the filter | Object | Yes |
| - - - Prefix | Object prefix to be matched by the rule | String | No |
| - Transition | Transition attributes in the rule, indicating when the COS storage class is transitioned to `Standard_IA` or `Archive` | Object | No  |
| - - Days | Specifies the number of days after which the object was last modified that the action corresponding to the rule will be executed. The value must be a non-negative integer, and a maximum of 3650 days is supported. | Number | Yes |
| - - StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| - NoncurrentVersionTransition | Specifies the transition attributes of a past object version | ObjectArray | No |
| - - NoncurrentDays | Indicates that the past object version is transitioned after the number of days determined by this value | Number | Yes |
| - - StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. | String | Yes |
| - Expiration | Rule expiration attributes | Object | No |
| - - ExpiredObjectDeleteMarker | Deletes expired object delete markers. Enumerated values: `true` and `false`. It cannot be specified with `Days` at the same time. | Boolean | Yes |
| - - Days | Specifies the number of days after which the object was last modified that the deletion action will occur. It cannot be specified with `ExpiredObjectDeleteMarker` at the same time. | Number | Yes |
| - AbortIncompleteMultipartUpload | Indicates to delete incomplete multipart uploadeds | Object | No |
| - - DaysAfterInitiation | Incomplete multipart uploads are deleted after the number of days determined by this value; the computation of this value starts from the time the file was uploaded and must be a positive integer. | Number | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Querying a lifecycle configuration

#### Feature description

This API is used to query the lifecycle management configuration of a bucket.

#### Sample request

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```js
cos.getBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

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
| Bucket | Bucket for which the lifecycle is queried in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Rules | List of specific lifecycle rules | ObjectArray |
| - - ID | Unique rule ID | String |
| - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String |
| - - Filter | Specifies the filter | Object |
| - - - Prefix | Key prefix to be matched with the rule | String |
| - - Transition | Transition attributes in the rule, indicating when the COS storage class is transitioned to `Standard_IA` or `Archive` | ObjectArray |
| - - - Days | Specifies the number of days after which the object was last modified that the action corresponding to the rule will be executed. The value must be a non-negative integer, and a maximum of 3650 days is supported. | Number |
| - - - StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| - - NoncurrentVersionTransition | Specifies the past object version transition attributes | ObjectArray |
| - - - NoncurrentDays | Indicates that the past object version is transitioned after the number of days determined by this value | Number |
| - - - StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| - - Expiration | Rule expiration attributes | Object |
| - - - ExpiredObjectDeleteMarker | Deletes expired object delete markers.. Enumerated values: `true` and `false`. It cannot be specified with `Days` at the same time. | Boolean |
| - - - Days | Specifies the number of days after which the object was last modified that the deletion action will occur. It cannot be specified with `ExpiredObjectDeleteMarker` at the same time. | Number |
| - - AbortIncompleteMultipartUpload | Indicates to delete incomplete multipart uploads incompletely | Object |
| - - - DaysAfterInitiation | Incomplete multipart uploads are deleted after the number of days determined by this value; the computation of this value starts from the time the file was uploaded and must be a positive integer | Number |

## Deleting a lifecycle configuration

#### Feature description

This API is used to query the lifecycle configuration of a bucket.

#### Sample request

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
| Bucket | Bucket for which the lifecycle is deleted in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
