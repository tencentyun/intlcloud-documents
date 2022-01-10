## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer configuration | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer configuration | Queries a bucket referer allowlist or blocklist |

## Setting Bucket Referer Configuration

#### Description

This API (PUT Bucket referer) is used to set a referer allowlist/blocklist for a bucket.

#### Sample request

[//]: # ".cssg-snippet-put-bucket-referer"
```js
cos.putBucketReferer({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    RefererConfiguration: {
        Status: 'Enabled',
        RefererType: 'White-List',
        DomainList: {
            Domains: [
                '*.qq.com',
                '*.qcloud.com',
            ]
        },
        EmptyReferConfiguration: 'Allow',
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | Required |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                           | Bucket for which the bucket policy is configured in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| RefererConfiguration        | Hotlink protection configuration. For details, see [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Object      | Yes   |
| - Status     | Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`           | String | Yes   |
| - RefererType   | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String | Yes   |
| - DomainList   | List of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains.   | Object | Yes   |
| - - Domains    | Domain names in the blocklist/allowlist. Format: '*.qq.com' (one domain); ['*.qq.com', '*.qcloud.com'] (multiple domains)                              | String\Array      | Yes   |
| -  EmptyReferConfiguration | Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` (default) | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |

## Querying Bucket Referer Configuration

#### Description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Sample request

[//]: # ".cssg-snippet-get-bucket-referer"
```js
cos.getBucketReferer({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "RefererConfiguration": {
        "Status": "Enabled",
        "RefererType": "White-List",
        "DomainList": {
            "Domains": [
                "*.qq.com",
                "*.qcloud.com"
            ]
        },
        "EmptyReferConfiguration": "Allow"
    },
    "statusCode": 200,
    "headers": {},
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which the bucket policy is queried in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| --------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - RefererConfiguration        | Hotlink protection configuration. For details, see [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Object      |
| - - Status   | Whether hotlink protection is enabled. Enumerated values: `Enabled`, `Disabled` | String                                   |
| - - RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String |
| - - DomainList   | List of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains.   | Object |
| - - - Domains    | Domain names in the blocklist/allowlist                            | Array      |
| - - EmptyReferConfiguration | Whether access with an empty referer is allowed. Enumerated values: `Allow`, `Deny` (default) | String |
