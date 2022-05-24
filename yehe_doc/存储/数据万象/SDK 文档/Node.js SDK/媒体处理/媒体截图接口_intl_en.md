## Overview

This document provides an overview of APIs and SDK code samples for media screenshot.

>! The COS Node.js SDK version must be at least v2.11.2.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  Querying screenshot	 |   Query the screenshot of media file at some time point     |


## Querying Screenshot

#### Feature description

This API is used to query the screenshot of a media file at some time point.

>! Before using this API, make sure that the media processing feature has been enabled in the data processing section in the console; otherwise, the error `media bucket unbinded, bucket's host is unavailable` will be reported.

#### Sample code
```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
cos.request({
    Bucket: config.Bucket,
    Region: config.Region,
    Method: 'GET',
    Key: 'test.mp4',  /* Media file in bucket (required) */
    Query: {
        'ci-process': 'snapshot', /** Fixed value (required) */
        time: 1, /** Screenshot time point in seconds (required) */
        // width: 0, /** Screenshot width (optional) */
        // height: 0, /** Screenshot height (optional) */
        // format: 'jpg', /** Screenshot format (optional). Valid values: jpg; png. Default value: jpg */
        // rotate: 'auto', /** Image rotation method (optional). Default value: auto */
        // mode: 'exactframe', /** Frame capturing method (optional). Default value: exactframe */
    },
    RawBody: true,
},
function(err, data){
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ci-process | Operation type, which is fixed at `snapshot`. | String | Yes |
| time   | Screenshot time point in seconds.                                        | Number | Yes   |
| width | Screenshot width. Default value: 0.	 | Number | No |
| height | Screenshot height. Default value: 0. If `width` and `height` are both `0`, the width and height of the video are used. If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | Number | No |
| format | Screenshot format. Valid values: jpg; png. Default value: jpg.	 | String | No |
| rotate | Image rotation method. auto: Rotate automatically according to the video rotation information. off: Do not rotate. Default value: auto. | String       | No |
| mode   | Frame capturing method. keyframe: Capture the last keyframe before the specified time point. exactframe: Capture the frame at a specified time point. Default value: exactframe.  | String       | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers. | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers. | Object |
| - RequestId | Unique ID of the request. | String |
| - Body       | Returned file content, which is in string format by default.                           | String  |
