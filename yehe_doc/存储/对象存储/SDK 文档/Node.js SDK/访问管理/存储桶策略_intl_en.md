## Overview

This document provides an overview of APIs and SDK code samples related to bucket policy.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for the specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the permission policy of the specified bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of the specified bucket |

## Setting a Bucket Policy

#### Feature

This API (PUT Bucket policy) is used to set permission policies for the specified bucket.

#### Request samples

[//]: # (.cssg-snippet-put-bucket-policy)
```js
cos.putBucketPolicy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Policy: {
        "version": "2.0",
        "Statement": [{
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/100000000001:uin/100000000001"]
            },
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"],
        }]
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | Required |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                           | Bucket for which the bucket policy is configured. Format: BucketName-APPID  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Policy | Permission policy. For more information, see [Access Management Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469) | Object | Yes |
| - version | Version number, fixed as 2.0 | String | Yes |
| - statement | List of permission policy statements | ObjectArray | Yes |
| - - effect | Effect; enumerated values: `allow`, `deny` | String | Yes |
| - - principal | Identity information | ObjectArray | Yes |
| - - - qcs | ID string <br>Format: `qcs::cam::uin/100000000001:uin/100000000011` <br>Here, 100000000001 is a root account, while 100000000011 is a sub-account | String | Yes |
| - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray | Yes |
| - - resource | List of resource identification strings. <br>Format: `qcs::cos:<Region>:uid/<AppId>:<ShortBucketName>/*`<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray | Yes |
| - - condition | Constraints; can be left blank. For details, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603). | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Querying a Bucket Policy

#### Feature

This API (GET Bucket policy) is used to query the permission policies of a specified bucket.

#### Request samples

[//]: # (.cssg-snippet-get-bucket-policy)
```js
cos.getBucketPolicy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Response samples

```json
{
    "Policy": {
        "version": "2.0",
        "Statement": [{
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/100000000001:uin/100000000001"]
            },
            "Resource": ["qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"],
            "Sid": "costs-1539833197000000307620-46518-39"
        }]
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which the permission policy is queried. Format: BucketName-APPID  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| --------------- | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - Policy | Permission policy. For more information, see [Cloud Access Management Practices > Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469) | Object |
| - - version | Version number, fixed as 2.0 | String |
| - - statement | List of permission policy statements | ObjectArray |
| - - - effect | Effect; enumerated values: `allow`, `deny` | String |
| - - - principal | Identity information | ObjectArray |
| - - - - qcs | ID string. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`. <br>100000000001 is a root account, while 100000000011 is a sub-account | String |
| - - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray |
| - - - resource | List of resource identification strings.<br>Format: `qcs::cos:<Region>:uid/<AppId>:<ShortBucketName>/*`<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray |
| - - - condition | Constraints; can be left blank. For details, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603). | ObjectArray |

## Delete a Bucket Policy

#### Feature

This API (DELETE Bucket policy) is used to delete the permission policy of the specified bucket.

>Only the Bucket owner is allowed to initiate this request. You will receive "204 No Content" if the permission policy does not exist.

#### Request samples

[//]: # (.cssg-snippet-delete-bucket-policy)
```js
cos.deleteBucketPolicy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which the permission policy is deleted. Format: BucketName-APPID  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

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
