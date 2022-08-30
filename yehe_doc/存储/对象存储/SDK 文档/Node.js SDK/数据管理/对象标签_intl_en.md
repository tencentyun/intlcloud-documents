## Overview

This document provides an overview of APIs and SDK code samples for object tagging.

| API | Operation |  Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an existing object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes the specified tags of an object. |


## Tagging Object

#### Feature description

This API is used to set a tag for an existing object.

#### Sample request

[//]: # (.cssg-snippet-put-object-tagging)
```js
cos.putObjectTagging({
    Bucket: 'examplebucket-1250000000', /* Bucket (required) */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Key: '1.png', /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
    Tags: [
        {"Key": "k1", "Value": "v1"},
        {"Key": "k2", "Value": "v2"}
    ],
    // VersionId: 'MTg0NDUwOTMyODM1MDg2MTA1xxx' /* Object version ID (optional) */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket    | Target bucket name in the format of `BucketName-APPID`  | String      | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Tags    | Tag information                                                     | ObjectArray | Yes   |
| - Key   | Tag name                                                       | String      | Yes   |
| - Value | Tag value                                                       | String      | Yes   |
| VersionId | Version ID of the object (if versioning is enabled). If this parameter is not specified, tags will be added to the latest version of the object.	  | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |

## Querying Object Tag

#### Feature description

This API is used to query the existing tags of a specified object.

#### Sample request

[//]: # (.cssg-snippet-get-object-tagging)
```js
cos.getObjectTagging({
    Bucket: 'examplebucket-1250000000', /* Bucket (required) */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Key: '1.png', /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

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

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket    | Target bucket name in the format of `BucketName-APPID`  | String      | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type        |
| ------------ | ------------------------------------------------------------ | ----------- |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - Tags       | Tag information                                                     | ObjectArray |
| - - Key      | Tag name                                                       | String      |
| - - Value    | Tag value                                                       | String      |

## Deleting Object Tag

#### Feature description

This API is used to delete the existing tags of a specified object.

#### Sample request

[//]: # (.cssg-snippet-delete-object-tagging)
```js
cos.deleteObjectTagging({
    Bucket: 'examplebucket-1250000000', /* Bucket (required) */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Key: '1.png', /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket    | Target bucket name in the format of `BucketName-APPID`  | String      | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
