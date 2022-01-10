## Overview

This document provides an overview of APIs and SDK code samples related to restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

## Restoring an Archived Object 

#### Description

This API (`POST Object restore`) is used to restore an archived COS object. The restored readable object is temporary. You can set the time during which the temporary object remains readable and the time to delete it. You can use the `Days` parameter to specify the expiration time of the temporary object. If you have not performed any operation on the object, such as copying it or extending its validity period, when it expires, the temporary object will be automatically deleted. A temporary object is only a copy of the archived object. The source object continues to exist throughout this period.

#### Sample code

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| RestoreRequest | A container for data restoration | Object | Yes |
| - Days | Expiration time of the temporary copy | Number | Yes |
| - CASJobParameters | A container for the archive job parameters | Object | Yes |
| - - Tier  | Specifies the restoration mode. The following three restoration modes are supported for the ARCHIVE storage class: <ul><li>Standard: restores an object within 3-5 hours.</li><li>Expedited: restores an object within 15 minutes.</li><li>Bulk: restores an object within 5-12 hours.</li></ul>The following two restoration modes are supported for the DEEP ARCHIVE storage class:<ul><li> Standard: restores an object within 12-24 hours.</li><li>Bulk: restores an object within 24-48 hours.</li></ul> | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
