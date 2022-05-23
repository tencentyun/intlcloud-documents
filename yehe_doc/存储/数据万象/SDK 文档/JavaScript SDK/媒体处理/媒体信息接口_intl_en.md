## Overview

This document provides an overview of APIs and SDK code samples for media information.

>! The COS JavaScript SDK version must be at least v1.3.1.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   Querying file information | Queries media file information      |


## Querying File Information

#### Feature description

This API is used to query the information of a media file.

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
        'ci-process': 'videoinfo' /** Fixed value (required) */
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key                        | Fixed value: mediabucket. | String   | Yes   |
| ci-process | Operation type, which is fixed at `videoinfo`.                                          | String | Yes   |

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
| - Response       | Response result. | Object |
| - - MediaInfo       | Media details.	 | Object |
| - - - Stream             | Stream information.   | Object |
| - - - - Video              |  Video information. | Container |
| - - - - - Index              | Stream number.                  | Number    |
| - - - - - CodecName          | Codec format name.              | String |
| - - - - - CodecLongName      | Detailed name of the codec format        | String |
| - - - - - CodecTimeBase      | Codec timebase.                    | String |
| - - - - - CodecTagString     | Codec tag name.                  | String |
| - - - - - CodecTag           | Codec tag.                    | String |
| - - - - - Profile            | Video codec profile.                | String |
| - - - - - Height             | Video height in px.             | Number    |
| - - - - - Width              | Video width in px.             | Number    |
| - - - - - HasBFrame          | Whether B-frames exist. 1: yes; 0: no. | Number    |
| - - - - - RefFrames          | Number of reference frames for video codec.        | Number    |
| - - - - - Sar                | Sample aspect ratio.                  | String |
| - - - - - Dar                | Display aspect ratio.                  | String |
| - - - - - PixFormat          | Pixel format.                    | String |
| - - - - - FieldOrder         | Field order.                     | String |
| - - - - - Level              | Video codec level.                | Number    |
| - - - - - Fps                | Video frame rate.                    | Number    |
| - - - - - AvgFps             | Average frame rate.                    | String |
| - - - - - Timebase           | Timebase.                        | String |
| - - - - - StartTime          | Video start time in seconds.      | Number  |
| - - - - - Duration           | Video duration in seconds.          | Number  |
| - - - - - Bitrate            | Bitrate in Kbps.         | Number  |
| - - - - - NumFrames          | Total number of frames.                      | Number    |
| - - - - - Language           | Language.                         | String |
| - - - - Audio              |  Audio information. | Container |
| - - - - - Index              | Stream number.                  | Number    |
| - - - - - CodecName          | Codec format name.              | String |
| - - - - - CodecLongName      | Detailed name of the codec format. | String |
| - - - - - CodecTimeBase      | Codec timebase.             | String |
| - - - - - CodecTagString     | Codec tag name.           | String |
| - - - - - CodecTag           | Codec tag.             | String |
| - - - - - SampleFmt          | Sample format.             | String |
| - - - - - SampleRate         | Sample rate.               | Number    |
| - - - - - Channel            | Number of channels.             | Number    |
| - - - - - ChannelLayout      | Channel layout.             | String |
| - - - - - Timebase           | Timebase.                 | String |
| - - - - - StartTime          | Audio start time in seconds. | Number  |
| - - - - - Duration           | Audio duration in seconds.     | Number  |
| - - - - - Bitrate            | Bitrate in Kbps.    | Number  |
| - - - - - Language           | Language.                 | String |
| - - - - Subtitle           |  Subtitles information. | Container |
| - - - - - Index              | Stream number.                | Number    |
| - - - - - Language           | Language. `und` indicates no query result. | String |
| - - - Format             | Format information. | Object |
| - - - - NumStream          | Number of streams (including videos, audios, and subtitles). | Number    |
| - - - - NumProgram         | Number of programs.                                  | Number    |
| - - - - FormatName         | Container format name.                                | String |
| - - - - FormatLongName     | Detailed name of the container format.                          | String |
| - - - - StartTime          | Start time in seconds.                          | Number  |
| - - - - Duration           | Duration in seconds.                              | Number  |
| - - - - Bitrate            | Bitrate in Kbps.                         | Number    |
| - - - - Size               | Size in bytes.                           | Number    |