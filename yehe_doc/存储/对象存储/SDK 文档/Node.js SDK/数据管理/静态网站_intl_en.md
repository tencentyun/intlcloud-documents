## Overview
This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration on an existing bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website | Queries the static website configuration on a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website | Deletes the static website configuration on a bucket |


## Setting a Static Website

#### Feature

This API (PUT Bucket website) is used to configure a static website for an existing bucket.

#### Request samples

```js
cos.putBucketWebsite({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    WebsiteConfiguration: {
        IndexDocument: {
            Suffix: "index.html"
        },
        ErrorDocument: {
            Key: "error.html"
        },
        RedirectAllRequestsTo: {
            Protocol: "https"
        },
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Name of the bucket which is configured as a static website. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| WebsiteConfiguration | Static website configuration, including index documents, error documents, protocol conversion, and redirect rules | Object | Yes |
| - IndexDocument    | Index document                                                     | Object      | Yes   |
| - - Suffix   | Specifies an index document                                                       | String      | Yes   |
| - ErrorDocument    | Error document                                                     | Object      | No   |
| - - Key   | Specifies general error response                                                       | String      | No   |
| - RedirectAllRequestsTo    | Redirects all requests                                                     | Object      | No   |
| - - Protocol |Specifies the site-wide redirect protocol, with only HTTPS supported. | String | No |
| - RoutingRules    | Sets up to 100 redirect rules                                                      | ObjectArray      | No   |
| - - Condition   | Specifies the redirect condition, either prefix-match or error code                                                       | Object      | No   |
| - - - HttpErrorCodeReturnedEquals   | Specifies the redirect error code. Only 4XX status codes are supported. It has a higher priority than ErrorDocument. | String | No |
| - - - KeyPrefixEquals | Specifies the prefix of the paths to be redirected | String | No |
| - - Redirect   | Specifies the replacement rule for redirects that meet the Condition                                                       | Object      | No   |
| - - - ReplaceKeyWith | Specifies the content which is used to replace the entire Key | String | No |
| - - - ReplaceKeyPrefixWith | Specifies the content which is used to replace the prefix of Key. This is allowed only when Condition is KeyPrefixEquals. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Querying Static Website

#### Feature

This API (GET Bucket website) is used to query the static website configuration associated with a bucket.

#### Request samples

```js
cos.getBucketWebsite({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "WebsiteConfiguration": {
        "IndexDocument": {
            "Suffix": "index.html"
        },
        "ErrorDocument": {
            "Key": "error.html"
        },
        "RedirectAllRequestsTo": {
            "Protocol": "https"
        },
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type          | Required |
| ------ | ------------------------ | ------ | ---- |
| Bucket | Name of the bucket which is configured as a static website. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------- | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - WebsiteConfiguration | Static website configuration, including index documents, error documents, protocol conversion, and redirect rules | Object | 
| - - IndexDocument    | Index document                                                     | Object      | 
| - - - Suffix   | Specifies an index document                                                       | String      | 
| - - ErrorDocument    | Error document                                                     | Object      | 
| - - - Key   | Specifies general error response                                                       | String      | 
| - - RedirectAllRequestsTo    | Redirects all requests                                                     | Object      | 
| - - - Protocol |Specifies the site-wide redirect protocol, with only HTTPS supported. | String | 
| - - RoutingRules    | Sets up to 100 redirect rules                                                      | ObjectArray      |
| - - - Condition   | Specifies the redirect condition, either prefix-match or error code                                                       | Object      | 
| - - - - HttpErrorCodeReturnedEquals   | Specifies the redirect error code. Only 4XX status codes are supported. It has a higher priority than ErrorDocument. | String | 
| - - - - KeyPrefixEquals | Specifies the prefix of the paths to be redirected | String | 
| - - - Redirect   | Specifies the replacement rule for redirects that meet the Condition                                                       | Object      | 
| - - - - ReplaceKeyWith | Specifies the content which is used to replace the entire Key | String | 
| - - - - ReplaceKeyPrefixWith | Specifies the content which is used to replace the prefix of Key. This is allowed only when Condition is KeyPrefixEquals. | String | 



## Deleting Static Website

#### Feature

This API (DELETE Bucket website) is used to delete the static website configuration on a bucket.

#### Request samples

```js
cos.deleteBucketWebsite({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket whose static website configuration is deleted. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
