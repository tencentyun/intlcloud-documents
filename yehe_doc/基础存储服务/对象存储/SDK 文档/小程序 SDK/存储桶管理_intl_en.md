## Overview

This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, bucket policies, tag management, versioning, and cross-region replication.

**Cross-origin Access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Bucket Policies**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting bucket policies | Sets permission policies for a specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying bucket policies | Queries the permission policies of a specified bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting bucket policies | Deletes the permission policies of a specified bucket |

**Tag Management**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes specified bucket tags |

**Versioning**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region Replication**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Cross-origin Access

### Setting Cross-origin Access Configuration

#### Feature Description

This API (PUT Bucket cors) is used to configure the cross-origin resource sharing (CORS) permission of a bucket. You can make the configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has the permission to use this API and can grant such permission to other users..

#### Sample

```js
cos.putBucketCors({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    CORSRules: [{
        "AllowedOrigin": ["*"],
        "AllowedMethod": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "AllowedHeader": ["*"],
        "ExposeHeader": ["ETag", "x-cos-acl", "x-cos-version-id", "x-cos-delete-marker", "x-cos-server-side-encryption"],
        "MaxAgeSeconds": "5"
    }]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| CORSRules | List of all the information on CORS configuration | ObjectArray | No |
| - ID | Configures the rule ID; optional | String | No |
| - AllowedMethods | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | StringArray | Yes |
| - AllowedOrigins | Allowed source origin. Wildcard `*` is supported. Format: `protocol://domain name[:port number]`. <br>Example: `http://www.qq.com`.  | StringArray | Yes |
| - AllowedHeaders | Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported | StringArray | No |
| - ExposeHeaders  | Sets the user-defined header information from the server side that the browser can receive | StringArray | No |
| - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin resource sharing (CORS, a W3C standard) configuration of a bucket. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

#### Sample

```js
cos.getBucketCors({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "CORSRules": [{
        "MaxAgeSeconds": "5",
        "AllowedOrigins": ["*"],
        "AllowedHeaders": ["*"],
        "AllowedMethods": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "ExposeHeaders": ["ETag", "Content-Length", "x-cos-acl", "x-cos-version-id", "x-cos-request-id", "x-cos-delete-marker", "x-cos-server-side-encryption"]
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - CORSRules | List of all the information on CORS configuration | ObjectArray |
| - - AllowedMethods | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | StringArray |
| - - AllowedOrigins | Allowed source origin. Wildcard `*` is supported. Format: `protocol://domain name[:port number]`. <br>Example: `http://www.qq.com`. | StringArray |
| - - AllowedHeaders | Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported | StringArray |
| - - ExposeHeaders  | Sets the user-defined header information from the server side that the browser can receive | StringArray |
| - - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String |
| - - ID | Configures the rule ID | String |

### Deleting Cross-origin Access Configuration

> 
>
> 1. If you delete the cross-origin access configuration of the current bucket, all cross-origin access requests will fail. Please proceed with caution.
> 2. It is not recommended to use this method in a browser.

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of a bucket.

#### Sample

```js
cos.deleteBucketCors({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

#### Sample

```js
cos.getBucketLocation({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - LocationConstraint | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String |

## Lifecycle

### Setting Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle management configuration for a bucket.

#### Samples

Sample 1. Transition objects to Standard_IA storage class 30 days after upload

```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
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

Sample 2. Transition objects with the specified directory prefix `dir/` to archive storage class 90 days after upload

```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
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

Sample 3. Delete objects 180 days after upload

```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
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

Sample 4. Delete parts 30 days after upload

```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| LifecycleConfiguration | Specifies lifecycle rules | Object | Yes |
| - Rules | Header information returned by the request | ObjectArray | Yes |
| - - ID | Unique rule ID | String | Yes |
| - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String | Yes |
| - - Filter | Specifies filters | String | Yes |
| - - - Prefix | Object prefix to be matched by the rule | String | No |
| - - Transition | Indicates to transition the objects | Object | No |
| - - - Days | Specifies the number of days between the object upload date and the rule effective date. This parameter can only be a positive integer | Object | Yes |
| - - - StorageClass | Storage class to which the objects are transitioned; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object | No |
| - - Expiration | Indicates to delete the objects | Object | No |
| - - - Days | Specifies the number of days between the object upload date and the rule effective date. This parameter can only be a positive integer | Object | Yes |
| - - AbortIncompleteMultipartUpload | Indicates to delete the parts | Object | No |
| - - - Days | Specifies the number of days between the object upload date and the rule effective date. This parameter can only be a positive integer | Object | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration of a bucket.

#### Sample

```js
cos.getBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

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
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Rules | Header information returned by the request | ObjectArray |
| - - ID | Unique rule ID | String |
| - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String |
| - - Filter | Specifies filters | String |
| - - - Prefix | Object prefix to be matched by the rule | String |
| - - Transition | Indicates to transition the objects | Object |
| - - - Days | Specifies the number of days between the object upload date and the rule effective date. This parameter can only be a positive integer | Object |
| - - - StorageClass | Storage class to which the objects are transitioned; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object |
| - - Expiration | Indicates to delete the objects | Object |
| - - - Days | Specifies the number of days between the object upload date and the rule effective date. This parameter can only be a positive integer | Object |
| - - AbortIncompleteMultipartUpload | Indicates to delete the parts | Object |
| - - - Days | Specifies the number of days between the object upload date and the rule effective date. This parameter can only be a positive integer | Object |

### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle management configuration of a bucket.

#### Sample

```js
cos.deleteBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Bucket Policies

### Setting Bucket Policies

#### Feature Description

This API (PUT Bucket policy) is used to set permission policies for a specified bucket.

#### Sample

```js
cos.putBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
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
            "Resource": ["qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"],
        }]
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Policy | Permission policy. For more information, see [Cloud Access Management Practices > Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469#.E8.AE.BF.E9.97.AE.E7.AE.A1.E7.90.86.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) | Object | Yes |
| - version | Version number, which is always 2.0 | ObjectArray | Yes |
| - statement | List of permission policy statements | ObjectArray | Yes |
| - - effect | Effect; enumerated values: `allow`, `deny` | String | Yes |
| - - principal | Identity information | ObjectArray | Yes |
| - - - qcs | ID string. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`. <br>100000000001 is a root account, while 100000000011 is a sub-account | String | Yes |
| - - action | List of actions subject to the policy. Wildcard `*` is supported | StringArray | Yes |
| - - resource | List of resource identification strings. <br>Format: `qcs::cos:<Region>:uid/<AppId>:<ShortBucketName>/*`.<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray | Yes   |
| - - condition | List of allowed or denied resources, which is a string | ObjectArray | No |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket Policies

#### Feature Description

This API (GET Bucket policy) is used to query the permission policies of a specified bucket.

#### Sample

```js
cos.getBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Sample Response

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - Policy | Permission policy. For more information, see [Cloud Access Management Practices > Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469#.E8.AE.BF.E9.97.AE.E7.AE.A1.E7.90.86.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) | Object |
| - - version | Version number, which is always 2.0 | ObjectArray |
| - - statement | List of permission policy statements | ObjectArray |
| - - - effect | Effect; enumerated values: `allow`, `deny` | String |
| - - - principal | Identity information | ObjectArray |
| - - - - qcs | ID string. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`. <br>100000000001 is a root account, while 100000000011 is a sub-account | String |
| - - - action | List of actions subject to the policy. Wildcard `*` is supported | StringArray |
| - - - resource | List of resource identification strings. <br>Format: `qcs::cos:<Region>:uid/<AppId>:<ShortBucketName>/*`.<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray |
| - - - condition | List of allowed or denied resources, which is a string | ObjectArray |

### Deleting Bucket Policies

#### Feature Description

This API (DELETE Bucket policy) is used to delete the permission policies of a specified bucket.

#### Sample

```js
cos.deleteBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Tag Management

### Setting Bucket Tags

#### Feature Description

This API (PUT Bucket tagging) is used to set tags for an existing bucket.

#### Sample

```js
cos.putBucketTagging({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Tagging: {
        "Tags": [
            {"Key": "k1", "Value": "v1"},
            {"Key": "k2", "Value": "v2"}
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Tagging | Tag information | Object | Yes |
| - Tags | Tag information | ObjectArray | Yes |
| - - Key | Tag name | String | Yes |
| - - Value | Tag value | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket Tags

#### Feature Description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Sample

```js
cos.getBucketTagging({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "Tags": [
        {"Key": "k1", "Value": "v1"},
        {"Key": "k2", "Value": "v2"}
    ],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Tags | Tag information | ObjectArray |
| - - Key | Tag name | String |
| - - Value | Tag value | String |

### Deleting Bucket Tags

#### Feature Description

This API (DELETE Bucket tagging) is used to delete specified bucket tags.

#### Sample

```js
cos.deleteBucketTagging({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Versioning

### Setting Versioning

#### Feature Description

This API (PUT Bucket versioning) is used to set versioning for a bucket.

#### Sample

```js
cos.putBucketVersioning({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',     /* Required */
    VersioningConfiguration: {
        Status: "Enabled"
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| VersioningConfiguration | Defines the versioning configuration of the bucket | Object | Yes |
| - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning configuration of a bucket.

#### Sample

```js
cos.getBucketVersioning({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',     /* Required */
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - VersioningConfiguration | Versioning configuration of the bucket | Object |
| - - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String |

## Cross-region Replication

### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket.

#### Sample

```js
cos.putBucketReplication({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',     /* Required */
    ReplicationConfiguration: { /* Required */
        Role: "qcs::cam::uin/100000000001:uin/100000000001",
        Rules: [{
            ID: "1",
            Status: "Enabled",
            Prefix: "sync/",
            Destination: {
                Bucket: "qcs::cos:ap-chengdu:appid/1250000000:backup",
                StorageClass: "Standard",
            }
        }]
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ReplicationConfiguration | Defines cross-region replication rules | Object | Yes |
| - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object | No |
| - Rules | List of specific replication rules | ObjectArray | Yes |
| - - ID | Job ID | String | No |
| - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String | Yes |
| - - Prefix | Prefix of the objects to be replicated | String | No |
| - - Destination | Prefix of the objects to be replicated | Object | Yes |
| - - - Bucket | Destination bucket for the replication. <br>Format: `qcs::cos:<Region>:appid/<AppId>:<ShortBucketName>`<br>Example: `qcs::cos:ap-chengdu:appid/1250000000:backup` | Object | Yes |
| - - - StorageClass | Storage class after the replication; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rules of a specified bucket.

#### Sample

```js
cos.getBucketReplication({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
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
                "Bucket": "qcs::cos:ap-chengdu:appid/1250000000:backup",
                "StorageClass": "Standard"
            }
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - ReplicationConfiguration | Cross-region replication rule | Object |
| - - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object |
| - - Rules | List of specific replication rules | ObjectArray |
| - - - ID | Job ID | String |
| - - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String |
| - - - Prefix | Prefix of the objects to be replicated | String |
| - - - Destination | Prefix of the objects to be replicated | Object |
| - - - - Bucket | Destination bucket for the replication. <br>Format: `qcs::cos:&lt;Region>:appid/&lt;AppId>:&lt;ShortBucketName>`.<br>Example: `qcs::cos:ap-chengdu:appid/1250000000:backup` | Object      |
| - - - - StorageClass | Storage class after the replication; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object |

## Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rules of a bucket.

#### Sample

```js
cos.deleteBucketReplication({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
