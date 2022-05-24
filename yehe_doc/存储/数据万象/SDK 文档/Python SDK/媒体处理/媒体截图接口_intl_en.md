## Overview

This document provides an overview of APIs and SDK code samples for media screenshot.

>! The COS Python SDK version must be at least v5.1.9.11.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  Querying screenshot	 |   Query the screenshot of media file at some time point     |

>! Before using this API, make sure that the media processing feature has been enabled in the data processing section in the console; otherwise, the error `media bucket unbinded, bucket's host is unavailable` will be reported. For more information, see [Enabling Media Processing](https://intl.cloud.tencent.com/document/product/436/46275).

## Querying Screenshot

#### Feature description

This API is used to query the screenshot of a media file at some time point.

#### Method prototype

```py
def get_snapshot(Bucket, Key, Time, Width=None, Height=None, Format='jpg', Rotate='auto', Mode='exactframe', **kwargs)
```

#### Sample request
```py
response = client.get_snapshot(
    Bucket='examplebucket-1250000000',
    Key='demo.mp4',
    Time='1.5',
    Width='480',
    Format='png'
)
print(response)
response['Body'].get_stream_to_file('snapshot.jpg')
```

#### Parameter description


| Parameter | Description | Required | Type |
| ------- | ----------------------------------------------------------- | ------- | ----- |
| Bucket        | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | Yes | String     |
| Key     | Object key, which is the unique identifier of the object in the bucket. | Yes       | String   |
| Time   | Screenshot time point in seconds, which can contain a decimal point.       | Yes       | String  |
| Width | Screenshot width. Default value: 0.         | No       | String    |
| Height | Screenshot height. Default value: 0. If `width` and `height` are both `0`, the width and height of the video are used. If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | No       | String    |
| Format | Screenshot format. Valid values: jpg, png. Default value: jpg. | No | String |
| Rotate | Image rotation method. auto: Rotate automatically according to the video rotation information. off: Do not rotate. Default value: auto. | No | String |
| Mode | Frame capturing method. keyframe: Capture the last keyframe before the specified time point. exactframe: Capture the frame at a specified time point. Default value: exactframe. | No | String |
