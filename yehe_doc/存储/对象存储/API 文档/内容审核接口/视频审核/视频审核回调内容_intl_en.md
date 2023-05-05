## Feature Overview

If you have configured a moderation callback address, after video moderation is completed, the backend will call back the moderation result in JSON format to the callback address. You can perform subsequent file processing operations based on the callback content.

The callback content is divided into simple callback (Simple) and detailed callback (Detail).

![](https://staticintl.cloudcachetci.com/yehe/backend-news/QLJ4586_PRELIM__%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.jpeg)

## Callback Content Description

### Simple callback (Simple)

The callback notification adopts the `POST` method of HTTP, with the `X-Ci-Content-Version: Simple` header.

The response body returns **application/json** data. The following contains all the nodes:

```plaintext
{
   "code": 0,
   "data": {
       "event":"ReviewVideo",
       "forbidden_status": 0,
       "porn_info": {
           "hit_flag": 0,
           "label": "",
           "count": 0
       },
       "result": 0,
       "trace_id": "test_trace_id",
       "url": "test_url",
       "cos_headers": {
           "x-cos-meta-xx": "xx"
       }
   },
   "message": "Test request when setting callback url"
}
```

The nodes are as described below:

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :------ | :------- |
| code | Error code. 0: moderation succeeded; other values: moderation failed. For more information, see [Error Codes](https://www.tencentcloud.com/document/product/1045/33700). | Integer | Yes |
| message | Error message. | String | Yes |
| data | Details of the video moderation result. | Object | Yes |

`data` is as described below:

| Parameter | Description | Type | Required |
| :--------------- | :----------------------------------------------------------- | :------ | :------- |
| trace_id | Request ID. If the job is an async job created through an API, this value is the `JobId` returned by the API. | String | Yes |
| url | Full URL of the moderated video. | String | Yes |
| event | Triggered event, which is fixed at `ReviewVideo` here. | String | Yes |
| result | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer | Yes |
| forbidden_status | If you set automatic freezing, this field indicates the frozen status of the video. `0`: not frozen, `1`: frozen, `2`: file moved. | Integer | Yes |
| cos_headers      | The custom header content set when the resource is uploaded. If it is not set, it will not be returned.       | Object  | No       |
| porn_info        | The moderation result of the **pornographic information** moderation scene.                           | Object  | No       |
| ads_info         | The moderation result of the **advertising information** moderation scene.                       | Object  | No       |
| data_id          | The original content will be returned if the `DataId` parameter is set when the job is submitted, which can contain up to 512 bytes. | String  | No       |

`xx_info` is as described below:

| Parameter | Description | Type | Required |
| :------- | :------------------------------------------------------ | :------ | :------- |
| hit_flag | The moderation result returned for the moderation scene. Return values: **0** (normal), **1** (confirmed as a violation of the current scene), and **2** (suspected as a violation of the current scene).     | Integer | Yes       |
| label | Hit label name, which is empty currently. | String | Yes |
| count | The number of sensitive screenshots that hit the moderation scene. | Integer | Yes |

### Detail callback (Detail)

The callback notification adopts the `POST` method of HTTP, with the `X-Ci-Content-Version: Detail` header.

The response body returns **application/json** data. The following contains all the nodes:

```plaintext
{
  "EventName": "ReviewVideo",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "",
    "Object": "",
    "Label": "Normal",
    "Result": 0,
    "SnapshotCount": 1,
    "PornInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "AdsInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "Snapshot": [
      {
        "Url": "",
        "Text": "",
        "SnapshotTime": 0,
        "Label": "Normal",
        "Result": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Label": "",
          "SubLabel": ""
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Label": "",
          "SubLabel": ""
        }
      }
    ],
    "AudioSection": [
      {
        "Url": "",
        "Text": "",
        "OffsetTime": 0,
        "Duration": 30000,
        "Label": "Normal",
        "Result": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0
        }
      }
    ],
    "BucketId": "examplebucket-1250000000",
    "Region": "ap-chongqing",
    "ForbidState": 0,
    "CosHeaders": {
        "x-cos-meta-id": "xxx"
    }
  }
}
```

The nodes are as described below:

| Node Name (Keyword) | Description                        | Type   |
| :----------------- | :-------------------------- | :----- |
| JobsDetail         | Job result details.         | Object |
| EventName          | Job type: ReviewVideo. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Code               | Error code, which will be returned only if `State` is `Failed`. For more information, see [Error Codes](https://www.tencentcloud.com/document/product/1045/33700). | String |
| Message            | Error message, which will be returned only if `State` is `Failed`. | String |
| JobId              | Moderation job ID. | String |
| DataId | The original content will be returned if the `DataId` parameter is set when the job is submitted, which can contain up to 512 bytes. | String |
| State              | Status of the video moderation job. Valid values: `Submitted`, `Snapshoting`, `Success`, `Failed`, `Auditing`. | String |
| CreationTime       | Creation time of the video moderation job. | String |
| Object             | The name of the video file to be moderated, which will be returned if `Object` is selected during job creation. | String |
| Url             | The URL of the video file to be moderated, which will be returned if `Url` is selected during job creation. | String |
| SnapshotCount      | The total number of video screenshots. In the callback where the live stream status is `Auditing`, this field indicates the number of screenshots included in the callback. | Integer |
| Label              | This field is used to return the **maliciousness label with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Return values: `Normal`, `Porn`, and `Ads`. | String  |
| Result             | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |
| Snapshot           | This field is used to return the result of video image moderation. | Array |
| AudioSection       | This field is used to return the result of video sound moderation. If no audio is detected, it will not be returned. | Array |
| BucketId           | Name of the bucket of the created moderation job.                             | String  |
| Region             | Bucket region.                                           | String  |
| ForbidState        | If you set automatic freezing, this field indicates the status of the video. `0`: not frozen; `1`: frozen, `2`: file moved. | Integer |
| CosHeaders         | The custom header content set when the resource is uploaded to COS. If it is not set, it will not be returned. It is in a map structure, where `key` is the custom header name and `value` is the content.      | Object  | No       |
| UserInfo           | Business field. This field will not exist if `UserInfo` is not set during job creation.                     | Object |
| Type               | Moderation type. `live_video` will be returned for live stream moderation.                          | String    |
| ListInfo           | Blocklist/Allowlist status of the account.                                          | Object  |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :------------------------------------------------------ | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Return values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Count              | The number of screenshots that hit this moderation scene.                              | Integer |

`Snapshot` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Url | URL of the current video screenshot, at which you can view the screenshot. It must be a standard URL. </br>Note: Each URL is valid for 2 hours. If you need to view the data after 2 hours, initiate a new query request. | String |
| SnapshotTime       | This field is used to return the time where the current screenshot is in the video in milliseconds, such as 5000 (i.e., 5000 milliseconds after the video starts). For live stream moderation, this field returns the timestamp of the current screenshot in milliseconds, such as 1649387157000. | Integer |
| Text | This field is used to return the OCR text recognition result of the current screenshot. It will be returned only if text content detection is enabled in the moderation policy. | String |
| Label              | This field is used to return the **maliciousness label with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Return values: `Normal`, `Porn`, and `Ads`. | String  |
| Result             | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | Whether the moderation type is hit. Valid values: `0` (miss), `1` (hit), `2` (suspected). | Integer |
| Score              | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. | Integer |
| Label | This field indicates the overall result label of the screenshot, which may be `SubLabel`, a person name, etc. | String |
| Category           | This field indicates the specific moderation category hit; for example, `Sexy` represents the sexy category in the `Porn` label. It may be null, indicating that no category is hit or there is no relevant category. | String |
| SubLabel           | This field indicates the specific sub-label hit by the moderation job; for example, `SexBehavior` is a sub-label under the `Porn` label. </br>Note: This field may return null, indicating that no specific sub-labels are hit. | String |
| OcrResults | This field represents the detailed OCR result, including the text coordinate information and text recognition result. It will be returned if there is non-compliant content. | Array |
| LibResults         | This field returns results based on recognition against the risk library. Note: This field will not be returned if no samples in the risk library are hit. | Object Array |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----- |
| ImageId            | This field represents the hit image sample ID in the risk library.                       | String  |
| Score              | This field returns the confidence under the current label. Value range: 0–100.  The higher the value, the more likely the image hits a sample in the risk library. For example, `Porn 99` means that the content is very likely to hit a pornographic sample in the library. | Integer |

`OcrResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----- |
| Text | The specific text content recognized by OCR in the image. | String |
| Keywords           | Keywords hit by the current moderation scene.  | Array  |
| Location           | This parameter is used to return the position (X and Y coordinates of the top-left corner, length, width, and rotation angle) of the OCR detection frame in the image for quick location of the recognized text. | Object |

`ObjectResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----- |
| Name               | This field is used to return the name of the recognized object, such as person name.                 | String |
| Location           | This parameter is used to return the position (X and Y coordinates of the top-left corner, length, width, and rotation angle) of the recognition result in the image for you to quickly locate information. | Object |

`Location` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :---- |
| X                  | This parameter is used to return the pixel position of the **abscissa (X) of the top-left corner** of the detection frame. It can be combined with other parameters to uniquely determine the size and position of the detection frame. | Float |
| Y                  | This parameter is used to return the pixel position of the **ordinate of the top-left corner** (Y) of the detection frame. It can be combined with other parameters to uniquely determine the size and position of the detection frame. | Float |
| Height             | This parameter is used to return the **height of the detection frame** (the length starting from the top-left corner and extending down the Y axis). It can be combined with other parameters to uniquely determine the size and position of the detection frame. | Float |
| Width              | This parameter is used to return the **width of the detection frame** (the length starting from the top-left corner and extending to the right on the X axis). It can be combined with other parameters to uniquely determine the size and position of the detection frame. | Float |
| Rotate             | This parameter is used to return the **rotation angle of the detection frame**. Valid values: **0–360** (**degrees**), and the direction is **counterclockwise rotation**. This parameter can be combined with the `X` and `Y` coordinate parameters to uniquely determine the specific position of the detection frame. | Float |

`AudioSection` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Url | URL of the current video sound segment, at which you can get the content of the segment. It must be a standard URL. </br>Note: Each URL is valid for 2 hours. If you need to view the data after 2 hours, initiate a new query request. | String |
| Text | This field is used to return the ASR text recognition result of the current video sound segment. | String |
| OffsetTime         | This field is used to return the time where the current sound segment is in the video in milliseconds, such as 5000 (i.e., 5000 milliseconds after the video starts). For live stream moderation, this field returns the timestamp of the current sound segment in milliseconds, such as 1649387157000. | Integer |
| Duration | The duration of the current video sound segment in milliseconds. | Integer |
| Label              | This field is used to return the **maliciousness label with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Return values: `Normal`, `Porn`, and `Ads`. | String  |
| Result | Recognition result for reference. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | Whether the moderation type is hit. Valid values: `0` (miss), `1` (hit), `2` (suspected). | Integer |
| Score              | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. | Integer |
| Category           | This field indicates the specific hit moderation type. </br>Note: This field may return null.      | String          |
| Keywords           | Keywords hit by the current moderation scene. Nothing will be returned if there is none.  | Array  |
| LibResults         | This field returns results based on recognition against the risk library. </br>Note: This field will not be returned if no samples in the risk library are hit. | Container Array |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----- |
| LibType            | Type of the hit risk library. Valid values: `1` (preset blocklist/allowlist library), `2` (custom risk library). | Integer      |
| LibName            | Name of the hit risk library. | String |
| Keywords           | Keywords hit in the library. There may be multiple returned values representing multiple hit keywords. | String Array |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword)  | Description                                                         | Type   | Required |
| :----------------- | :-------------------------------------------------- | :----- | :------- |
| TokenId            | Account information, which can contain up to 128 bytes.           | String | No       |
| Nickname           | Nickname information, which can contain up to 128 bytes.           | String | No       |
| DeviceId           | Device information, which can contain up to 128 bytes.           | String | No       |
| AppId              | Unique app ID, which can contain up to 128 bytes.           | String | No       |
| Room               | Room ID information, which can contain up to 128 bytes.           | String | No       |
| IP                 | IP address information, which can contain up to 128 bytes.           | String | No       |
| Type               | Business type, which can contain up to 128 bytes.           | String | No       |
| ReceiveTokenId     | User account to receive messages, which can contain up to 128 bytes.           | String | No       |
| Gender             | Gender information, which can contain up to 128 bytes.           | String | No       |
| Level              | Level information, which can contain up to 128 bytes.           | String | No       |
| Role               | Role information, which can contain up to 128 bytes.           | String | No       |

`ListInfo` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :---------------- | :------------------------------------------------------ | :----- |
| ListResults        | Results in all hit lists. | Container Array |

`ListResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :---------------- | :------------------------------------------------------ | :----- |
| ListType           | Type of the hit list. Valid values: `0` (allowlist), `1` (blocklist). | Integer |
| ListName           | Name of the hit list.                                 | String  |
| Entity             | Entity hit in the list.                         | String  |

## Examples

#### Sample 1: Simple callback (Simple)

```plaintext
{
   "code": 0,
   "data": {
       "event":"ReviewVideo",
       "forbidden_status": 0,
       "porn_info": {
           "hit_flag": 0,
           "label": "",
           "count": 0
       },
       "result": 0,
       "trace_id": "vxzt90jl2dfscxxxxxxxxxxxxxxxxx",
       "url": "https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/video.mp4",
       "cos_headers": {
           "x-cos-meta-id": "666666"
       }
   },
   "message": "success"
}
```

#### Sample 2: Detailed callback (Detail)

```plaintext
{
  "EventName": "ReviewVideo",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "2021-08-10T21:01:10+08:00",
    "Object": "1.mp4",
    "Label": "Normal",
    "Result": 0,
    "SnapshotCount": 1,
    "PornInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "AdsInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "Snapshot": [
      {
        "Url": "https://video-1250000000.cos.ap-chongqing.myqcloud.com/test/0.jpg",
        "Text": "",
        "SnapshotTime": 41,
        "Label": "Normal",
        "Result": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Label": "",
          "SubLabel": ""
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Label": "",
          "SubLabel": ""
        }
      }
    ],
    "AudioSection": [
      {
        "Url": "https://audio-1250000000.cos.ap-guangzhou.myqcloud.com/0.mp3",
        "Text": "",
        "OffsetTime": 0,
        "Duration": 30000,
        "Label": "Normal",
        "Result": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0
        }
      }
    ],
    "BucketId": "examplebucket-1250000000",
    "Region": "ap-chongqing",
    "ForbidState": 0,
    "CosHeaders": {
        "x-cos-meta-id": "xxxx"
    }
  }
}
```

