## Overview

If you have configured a moderation callback address, after audio moderation is completed, the backend will call back the moderation result in JSON format to the callback address. You can perform subsequent file processing operations based on the callback content.

The callback content is divided into simple callback (Simple) and detailed callback (Detail).

![](https://qcloudimg.tencent-cloud.cn/raw/b3e99f1b4436ff487601671962732bd4.jpeg)

## Callback Content Description

### Simple callback (Simple)

```plaintext
{
   "code": 0,
   "data": {
       "forbidden_status": 0,
       "porn_info": {
           "hit_flag": 0,
           "label": "",
           "score": 9
       },
       "result": 0,
       "trace_id": "test_trace_id",
       "url": "test_audio",
       "cos_headers": {
           "x-cos-meta-xx": "xx"
       }
   },
   "message": "Test request when setting callback url"
}
```

The nodes are described as follows:

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :------ | :------- |
| code | Error code. 0: moderation succeeded; other values: moderation failed. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). | Integer | Yes |
| message | Error message. | String | Yes |
| data | Details of the audio moderation result. | Object | Yes |

`data` is as described below:

| Parameter | Description | Type | Required |
| :--------------- | :----------------------------------------------------------- | :------ | :------- |
| trace_id | Request ID. If the job is an async job created through an API, this value is the `JobId` returned by the API. | String | Yes |
| url | Full URL of the moderated audio. | String | Yes |
| event | Triggered event, which is fixed at `ReviewAudio` here. | String | Yes |
| result | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer | Yes |
| forbidden_status | If you set auto-freezing, this field indicates the frozen status of the audio. `0`: not frozen, `1`: frozen, `2`: file moved. | Integer | Yes |
| cos_headers      | The custom header content set when the resource is uploaded. If it is not set, it will not be returned.       | Object  | No       |
| porn_info        | The moderation result of the **pornographic information** moderation scene.                           | Object  | No       |
| ads_info         | The moderation result of the **advertising information** moderation scene.                       | Object  | No       |
| data_id          | The original content will be returned if the `DataId` parameter is set when the job is submitted, which can contain up to 512 bytes. | String  | No       |

`xx_info` is as described below:

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :------ | :------- |
| hit_flag                | Whether the moderation type is hit. Valid values: `0` (miss), `1` (hit), and `2` (suspected). | Integer | Yes |
| score    | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic.  | Integer | Yes       |
| label | Result tag of this moderation job. If a sensitive keyword is hit, the keyword will be returned in this field. | String | Yes |

### Detail callback (Detail)

The callback notification adopts the `POST` method of HTTP, with the `X-Ci-Content-Version: Detail` header.

The response body returns **application/json** data. The following contains all the nodes:

```plaintext
{
  "EventName": "ReviewAudio",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "",
    "Object": "",
    "Label": "Normal",
    "Result": 0,
    "AudioText": "       ",
    "PornInfo": {
      "HitFlag": 0,
      "Score": 0,
      "Label": ""
    },
    "AdsInfo": {
      "HitFlag": 0,
      "Score": 0,
      "Label": ""
    },
    "Section": [
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
    "BucketId": "",
    "Region": "ap-chongqing",
    "ForbidState": 0,
    "CosHeaders": {
        "x-cos-meta-id": "xxxx"
    }
  }
}
```

The nodes are described as follows:

| Node Name (Keyword) | Description                        | Type   |
| :----------------- | :-------------------------- | :----- |
| JobsDetail         | Job result details.         | Object |
| EventName          | Job type: ReviewAudio. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Code               | Error code, which will be returned only if `State` is `Failed`. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). | String |
| Message            | Error description, which will be returned only if `State` is `Failed`. | String |
| JobId              | ID of the audio moderation job. | String |
| DataId             | The original content will be returned if the `DataId` parameter is set when the job is submitted, which can contain up to 512 bytes. | String  |
| State              | Status of the audio moderation job. Valid values: Submitted, Success, Failed, Auditing. | String |
| CreationTime       | Creation time of the audio moderation job. | String |
| Object             | The name of the audio file to be moderated, which will be returned if `Object` is selected during job creation. | String |
| Url             | The URL of the audio file to be moderated, which will be returned if `Url` is selected during job creation. | String |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Return values: `Normal`, `Porn`, and `Ads`. | String  |
| SubLabel | The specific sub-tag hit by the moderation job. Note: This field may return null. | String |
| Result             | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| AudioText          | This field is used to return the recognized text content of the audio file.                 | String  |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |
| Section | When the audio is too long, it will be segmented. This field is used to return the moderation result of an audio segment, mainly including the start time and audio moderation result. | Array |
| BucketId           | Name of the bucket of the created audio moderation job.                             | String  |
| Region             | Bucket region.                                           | String  |
| ForbidState        | If you set automatic freezing, this field indicates the status of the audio. `0`: not frozen; `1`: frozen, `2`: file moved. | Integer |
| CosHeaders         | The custom header content set when the resource is uploaded to COS. If it is not set, it will not be returned. It is in a map structure, where `key` is the custom header name and `value` is the content.      | Object  | No       |
| UserInfo | Business field. This field will not exist if `UserInfo` is not set during job creation. | Object |
| ListInfo           | Blocklist/Allowlist status of the account.                                          | Object        |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Return values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Score              | Moderation result score. The higher the score, the more sensitive the content is. | Integer |
| Category           | This field indicates the specific hit moderation type. Note: This field may return null.      | String          |
| SubLabel   | The specific sub-tag hit by the moderation job. Note: This field may return null. | String |
| Label | Overall result tag of this moderation job. If a sensitive keyword is hit, the keyword will be returned in this field. | String |

`Section` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Url | URL of the current audio segment, at which you can get the content of the segment. It must be a standard URL. </br>Note: Each URL is valid for 2 hours. If you need to view the data after 2 hours, initiate a new query request. | String |
| Text | This field is used to return the ASR text recognition result of the current audio segment. | String |
| OffsetTime | This field is used to return the time where the current audio segment is in the entire audio in milliseconds, such as 5000 (i.e., 5000 milliseconds after the audio starts). | Integer |
| Duration | Duration of the current audio segment in milliseconds. | Integer |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Return values: `Normal`, `Porn`, and `Ads`. | String  |
| SubLabel   | The specific sub-tag hit by the moderation job. Note: This field may return null. | String |
| Result             | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Return values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Score              | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic.  | Integer |
| Category           | This field indicates the specific moderation category hit; for example, `Sexy` represents the sexy category in the `Porn` tag. It may be null, indicating that no category is hit or there is no relevant category. | String |
| Keywords | The sensitive keyword hit by the moderation job. Nothing will be returned if there is none. | Array |
| LibResults         | This field returns results based on recognition against the risk library. </br>Note: This field will not be returned if no samples in the risk library are hit. | Container Array |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :------------------ | :----------------------------------------------------------- | :----- |
| LibType            | Type of the hit risk library. Valid values: `1` (preset blocklist/allowlist library), `2` (custom risk library). | Integer      |
| LibName            | Name of the hit risk library.                                           | String       |
| Keywords           | Keywords hit in the library. There may be multiple return values representing multiple hit keywords. | String Array |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required |
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

| Node Name (Keyword)         | Description                               | Type   |
| :---------------- | :------------------------------------------------------ | :----- |
| ListResults        | Results in all hit lists. | Container Array |

`ListResults` has the following sub-nodes:

| Node Name (Keyword)         | Description                               | Type   |
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
       "event":"ReviewAudio",
       "forbidden_status": 0,
       "porn_info": {
           "hit_flag": 0,
           "label": "",
           "score": 9
       },
       "result": 0,
       "trace_id": "ixzt90jl2dfscxxxxxxxxxxxxxxxxx",
       "url": "https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/music.mp3",
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
  "EventName": "ReviewAudio",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "2021-08-10T21:01:08+08:00",
    "Object": "1.mp3",
    "Result": 0,
    "AudioText": "       ",
    "PornInfo": {
      "HitFlag": 0,
      "Score": 0,
      "Label": ""
    },
    "AdsInfo": {
      "HitFlag": 0,
      "Score": 0,
      "Label": ""
    },
    "Section": [
      {
        "Url": "https://audio-1250000000.cos.ap-guangzhou.myqcloud.com/0.mp3",
        "Text": "",
        "OffsetTime": 0,
        "Duration": 30000,
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

