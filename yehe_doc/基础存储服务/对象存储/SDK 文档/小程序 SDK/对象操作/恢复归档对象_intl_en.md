## Overview

This document provides an overview of APIs and SDK code samples for restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

## Restoring an Archived Object 

#### Feature description

The `POST Object restore` API is used to restore an archived COS object. The restored readable object is a temporary copy, for which you can set the readable status and the time to delete it through the `Days` parameter. If the time has elapsed and you haven't initiated a copy or extension operation, the temporary object will be automatically deleted. Temporary objects are only copies of the archived objects which always exist.

#### Sample code

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    RestoreRequest: {
        Days: 1,
        CASJobParameters: {
            Tier: 'Expedited'
        }
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| RestoreRequest | Container for data restoration | Object | Yes |
| - Days | Expiration time of the temporary copy | Number | Yes |
| - CASJobParameters | Container for archive job parameters | Object | Yes |
| - - Tier | Restoration mode. Valid values: `Standard` (which restores an object within 3–5 hours), `Expedited` (which restores an object within 15 minutes), `Bulk` (which restores an object within 5–12 hours). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
