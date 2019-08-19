## Overview

This document provides an overview of APIs related to cross-origin access, lifecycle, bucket policy, tag management, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Bucket policy**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for the specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying bucket policy | Queries the permission policy of the specified bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of the specified bucket |

**Tag management**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Query bucket tags | Queries the existing tags of the specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes the specified bucket tag |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |

## Cross-origin Access

### Setting Cross-origin Access Configuration

> 
>
> 1. If you want to modify the cross-origin access configuration on the frontend, the bucket should have already supported cross-origin access and you can configure it in the console. For more information, see the Getting Started documentation.
> 2. When modifying the cross-origin access configuration, be careful not to affect cross-origin access requests under the current origin.

#### Feature Description

This API (PUT Bucket cors) is used to set the cross-origin access permission of a bucket. You can implement the configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has direct permission to use this API and can grant such permission to other users.

#### Use Cases

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| CORSRules | Information list of all CORS configurations | ObjectArray | No |
| - ID | Configures the rule ID; optional | String | No |
| - AllowedMethods | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | StringArray | Yes |
| - AllowedOrigins | Allowed origin in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard * is supported | StringArray | Yes |
| - AllowedHeaders | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported | StringArray | No |
| - ExposeHeaders  | Sets custom header information from the server that the browser can receive | StringArray | No |
| - MaxAgeSeconds | Sets the validity period of the result of the OPTIONS request | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration information of a bucket. (Cross-origin resource sharing (CORS) is a W3C standard.) By default, the bucket owner has direct permission to use this API and can grant such permission to other users.

#### Use Cases

```js
cos.getBucketCors({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Return Example

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - CORSRules | Information list of all CORS configurations | ObjectArray |
| - - AllowedMethods | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | StringArray |
| - - AllowedOrigins | Allowed origin in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard * is supported | StringArray |
| - - AllowedHeaders | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported | StringArray |
| - - ExposeHeaders  | Sets custom header information from the server that the browser can receive | StringArray |
| - - MaxAgeSeconds | Sets the OPTIONS cross-origin information caching duration in seconds | String |
| - - ID | Configures the rule ID | String |

### Deleting Cross-origin Access Configuration

> 
>
> 1. Deleting the cross-domain access configuration information of the current bucket will cause all cross-origin access requests to fail. Please do so with caution.
> 2. This method is not recommended for use in a browser.

#### Feature Description

This API is used to delete the cross-origin access configuration information of a bucket.

#### Use Cases

```js
cos.deleteBucketCors({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

#### Use Cases

```js
cos.getBucketLocation({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - LocationConstraint | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String |

## Lifecycle

### Setting Lifecycle

#### Feature Description

This API is used to set the lifecycle management configuration for a bucket.

#### Use Cases

Example 1. Transition files to Standard_IA storage class 30 days after upload

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

Example 2. Transition files with the specified directory prefix `dir/` to archive storage class 90 days after upload

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

Example 3. Delete files 180 days after upload

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

Example 4. Delete parts 30 days after upload

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| LifecycleConfiguration | Specifies the lifecycle rules | Object | Yes |
| - Rules | Header information returned by the request | ObjectArray | Yes |
| - - ID | Unique ID of the rule | String | Yes |
| - - Status | Rule status; enumerated values: Enabled, Disabled | String | Yes |
| - - Filter | Specifies the filter | String | Yes |
| - - - Prefix | The object prefix to be matched by the rule | String | No |
| - - Transition | Indicates to transition the object | Object | No |
| - - - Days | Validity period of the rule in days starting from the file upload date, which must be a positive integer | Object | Yes |
| - - - StorageClass | Target storage class for object transition; enumerated values: STANDARD, STANDARD_IA; default value: STANDARD | Object | No |
| - - Expiration | Indicates to delete the object | Object | No |
| - - - Days | Validity period of the rule in days starting from the file upload date, which must be a positive integer | Object | Yes |
| - - AbortIncompleteMultipartUpload | Indicates to delete the parts | Object | No |
| - - - Days | Validity period of the rule in days starting from the file upload date, which must be a positive integer | Object | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration for a bucket.

#### Use Cases

```js
cos.getBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Return Example

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Rules | Header information returned by the request | ObjectArray |
| - - ID | Unique ID of the rule | String |
| - - Status | Rule status; enumerated values: Enabled, Disabled | String |
| - - Filter | Specifies the filter | String |
| - - - Prefix | The object prefix to be matched by the rule | String |
| - - Transition | Indicates to transition the object | Object |
| - - - Days | Validity period of the rule in days starting from the file upload date, which must be a positive integer | Object |
| - - - StorageClass | Target storage class for object transition; enumerated values: STANDARD, STANDARD_IA; default value: STANDARD | Object |
| - - Expiration | Indicates to delete the object | Object |
| - - - Days | Validity period of the rule in days starting from the file upload date, which must be a positive integer | Object |
| - - AbortIncompleteMultipartUpload | Indicates to delete the parts | Object |
| - - - Days | Validity period of the rule in days starting from the file upload date, which must be a positive integer | Object |

### Deleting Lifecycle

#### Feature Description

This API is used to delete the lifecycle management configuration of a bucket.

#### Use Cases

```js
cos.deleteBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Bucket Policy

### Setting a Bucket Policy

#### Feature Description

This API is used to set a permission policy for the specified bucket.

#### Use Cases

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Policy | Permission policy. For more information, see [Access Management Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469#policy-syntax) | Object | Yes |
| - version | Version number, which is always 2.0 | ObjectArray | Yes |
| - statement | Permission policy lifecycle list | ObjectArray | Yes |
| - - effect | Effectiveness; enumerated values: allow, deny | String | Yes |
| - - principal | Identity information | ObjectArray | Yes |
| - - - qcs | ID string in the format of qcs::cam::uin/100000000001:uin/100000000011, where 100000000001 is a root account, while 100000000011 is a sub-account | String | Yes |
| - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray | Yes |
| - - resource | List of related resource identification strings in the format of qcs::cos:&ltRegion>:uid/&ltAppId>:&ltShortBucketName>/\*, such as qcs::cos:ap-beijing:uid/1250000000:examplebucket/\* | StringArray | Yes |
| - - condition | List of allowed or disabled resources, which is a string | ObjectArray | No |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket Policy	

#### Feature Description

This API is used to query the permission policy of the specified bucket.

#### Use Cases

```js
cos.getBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Return Example

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| --------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - Policy | Permission policy. For more information, see [Access Management Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469#policy-syntax) | Object |
| - - version | Version number, which is always 2.0 | ObjectArray |
| - - statement | Permission policy lifecycle list | ObjectArray |
| - - - effect | Effectiveness; enumerated values: allow, deny | String |
| - - - principal | Identity information | ObjectArray |
| - - - - qcs | ID string in the format of qcs::cam::uin/100000000001:uin/100000000011, where 100000000001 is a root account, while 100000000011 is a sub-account | String |
| - - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray |
| - - - resource | List of related resource identification strings in the format of qcs::cos:&ltRegion>:uid/&ltAppId>:&ltShortBucketName>/\*, such as qcs::cos:ap-beijing:uid/1250000000:examplebucket/\* | StringArray |
| - - - condition | List of allowed or disabled resources, which is a string | ObjectArray |

### Deleting a Bucket Policy

#### Feature Description

This API is used to delete the permission policy of the specified bucket.

#### Use Cases

```js
cos.deleteBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Tag Management

### Setting a Bucket Tag

#### Feature Description

This API is used to set a tag for an existing bucket.

#### Use Cases

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket Tags

#### Feature Description

This API is used to query the existing tags of the specified bucket.

#### Use Cases

```js
cos.getBucketTagging({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Return Example

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Tags | Tag information | ObjectArray |
| - - Key | Tag name | String |
| - - Value | Tag value | String |

### Deleting a Bucket Tag

#### Feature Description

This API is used to delete the specified bucket tag.

#### Use Cases

```js
cos.deleteBucketTagging({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Versioning

### Setting Versioning

#### Feature Description

This API is used to set the versioning feature for a bucket.

#### Use Cases

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| VersioningConfiguration | Defines the versioning configuration information of the bucket | Object | Yes |
| - Status | Versioning status; enumerated values: Enabled, Suspended | String | No |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Versioning

#### Feature Description

This API is used to query the versioning information of a bucket.

#### Use Cases

```js
cos.getBucketVersioning({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',     /* Required */
}, function (err, data) {
    console.log(err || data);
});

```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - VersioningConfiguration | Versioning configuration information of the bucket | Object |
| - - Status | Versioning status; enumerated values: null, Enabled, Suspended | String | No |

## Cross-region Replication

### Setting Cross-region Replication

#### Feature Description

This API is used to set the cross-region replication rule for a bucket.

#### Use Cases

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
                Bucket: "qcs:id/0:cos:ap-chengdu:appid/1250000000:backup",
                StorageClass: "Standard",
            }
        }]
    }
}, function (err, data) {
    console.log(err || data);
});

```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ReplicationConfiguration | Defines the cross-region replication rule | Object | Yes |
| - Role | The role used in the replication process in the format of qcs::cam::uin/100000000001:uin/100000000011, where 100000000001 is a root account, while 100000000011 is a sub-account | Object | No |
| - Rules | List of specific replication rules | ObjectArray | Yes |
| - - ID | Task ID | String | No |
| - - Status | Rule status; enumerated values: Enabled, Disabled | String | Yes |
| - - Prefix | Prefix of the object to be copied | String | No |
| - - Destination | Prefix of the object to be copied | Object | Yes |
| - - - Bucket | Destination bucket in the format of qcs:id/0:cos:&lt;Region>:appid/&lt;AppId>:&lt;ShortBucketName>, such as qcs:id/0:cos:ap-chengdu:appid/1250000000:backup | Object | Yes |
| - - - StorageClass | Storage class after replication; enumerated values: STANDARD, STANDARD_IA; default value: STANDARD | Object | No |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Cross-region Replication

#### Feature Description

This API is used to query the cross-region replication rule of a specified bucket.

#### Use Cases

```js
cos.getBucketReplication({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Return Example

```json
{
    "ReplicationConfiguration": {
        "Role": "qcs::cam::uin/100000000001:uin/100000000001",
        "Rules": {
            "ID": "1",
            "Status": "Enabled",
            "Prefix": "sync/",
            "Destination": {
                "Bucket": "qcs:id/0:cos:ap-chengdu:appid/1250000000:backup",
                "StorageClass": "Standard"
            }
        }
    },
    "statusCode": 200,
    "headers": {}
}

```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - ReplicationConfiguration | Cross-region replication rule | Object |
| - - Role | The role used in the replication process in the format of qcs::cam::uin/100000000001:uin/100000000011, where 100000000001 is a root account, while 100000000011 is a sub-account | Object |
| - - Rules | List of specific replication rules | ObjectArray |
| - - - ID | Task ID | String |
| - - - Status | Rule status; enumerated values: Enabled, Disabled | String |
| - - - Prefix | Prefix of the object to be copied | String |
| - - - Destination | Prefix of the object to be copied | Object |
| - - - - Bucket | Destination bucket in the format of qcs:id/0:cos:&lt;Region>:appid/&lt;AppId>:&lt;ShortBucketName>, such as qcs:id/0:cos:ap-chengdu:appid/1250000000:backup | Object |
| - - - - StorageClass | Storage class after replication; enumerated values: STANDARD, STANDARD_IA; default value: STANDARD | Object |

### Deleting Cross-region Replication

#### Feature Description

This API is used to delete the cross-region replication rule of a bucket.

#### Use Cases

```js
cos.deleteBucketReplication({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
