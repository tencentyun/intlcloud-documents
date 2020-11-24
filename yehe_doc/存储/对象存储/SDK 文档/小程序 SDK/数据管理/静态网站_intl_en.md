## Overview
This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting static website configuration | Sets static website configuration on an existing bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration on a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration from a bucket |


## Setting Static Website Configuration

#### API description

This API is used to configure an existing bucket as a static website.

#### Sample request 

[//]: # (.cssg-snippet-put-bucket-website)
```js
cos.putBucketWebsite({
    Bucket: 'examplebucket-1250000000',                               /* Required */
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
| Bucket | Name of the bucket for which to set static website configuration in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| WebsiteConfiguration | Static website configuration, including index document, error document, protocol conversion and redirect rule | Object | Yes |
| - IndexDocument    | Index document                                                     | Object      | Yes   |
| - - Suffix   | Specifies an index document                                                       | String      | Yes   |
| - ErrorDocument    | Error document                                                     | Object      | No   |
| - - Key   | Specifies general error response                                                       | String      | No   |
| - RedirectAllRequestsTo    | Redirects all requests                                                     | Object      | No   |
| - - Protocol | Specifies the site-wide redirect protocol. Only HTTPS is supported | String | No |
| - RoutingRules    | Sets up to 100 redirect rules                                                      | ObjectArray      | No   |
| - - Condition   | Specifies the condition that must be met for a redirect to apply. Redirects can be applied based on either prefix match or error codes.                                                       | Object      | No   |
| - - - HttpErrorCodeReturnedEquals   | Specifies the redirect error code. Only 4XX status codes are supported. This has a higher priority than `ErrorDocument`. | String | No |
| - - - KeyPrefixEquals | Specifies the object key prefix to replace with the specified “folder/” for the redirect  | String | No |
| - - Redirect   | Specifies the replacement rule for redirects that meet the condition                                                       | Object      | No   |
| - - - ReplaceKeyWith | Specifies the content that is used to replace the entire key | String | No |
| - - - ReplaceKeyPrefixWith | Specifies the content that is used to replace the key prefix. This is allowed only when the condition is `KeyPrefixEquals`. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |

## Querying Static Website Configuration

#### API description

This API is used to query the static website configuration associated with a bucket.

#### Sample request 

[//]: # (.cssg-snippet-get-bucket-website)
```js
cos.getBucketWebsite({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

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
| Bucket | Name of the bucket for which to query static website configuration in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------- | ----------- |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - WebsiteConfiguration | Static website configuration, including index document, error document, protocol conversion and redirect rules | Object | 
| - - IndexDocument    | Index document                                                     | Object      | 
| - - - Suffix   | Specifies an index document                                                       | String      | 
| - - ErrorDocument    | Error document                                                     | Object      | 
| - - - Key   | Specifies general error response                                                       | String      | 
| - - RedirectAllRequestsTo    | Redirects all requests                                                     | Object      | 
| - - - Protocol | Specifies the site-wide redirect protocol. Only HTTPS is supported. | String | 
| - - RoutingRules    | Sets up to 100 redirect rules                                                      | ObjectArray      |
| - - - Condition   | Specifies the condition that must be met for a redirect to apply. Redirects can be applied based on either prefix match or error codes.                                                       | Object      | 
| - - - - HttpErrorCodeReturnedEquals   | Specifies the redirect error code. Only 4XX status codes are supported. This has a higher priority than `ErrorDocument`. | String | 
| - - - - KeyPrefixEquals | Specifies the object key prefix to replace with the specified “folder/” for the redirect | String | 
| - - - Redirect   | Specifies the replacement rule for redirects that meet the condition                                                       | Object      | 
| - - - - ReplaceKeyWith | Specifies the content that is used to replace the entire key | String | 
| - - - - ReplaceKeyPrefixWith | Specifies the content that is used to replace the key prefix. This is allowed only when the condition is `KeyPrefixEquals`. | String | 



## Deleting Static Website Configuration

#### API description

This API is used to delete the static website configuration from a bucket.

#### Sample request 

[//]: # (.cssg-snippet-delete-bucket-website)
```js
cos.deleteBucketWebsite({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket from which to delete the static website configuration in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
