## Overview

If you have configured a moderation callback address, after text moderation is completed, the backend will call back the moderation result in JSON format to the callback address. You can perform subsequent file processing operations based on the callback content.

The callback content is divided into simple callback (Simple) and detailed callback (Detail).

![](https://qcloudimg.tencent-cloud.cn/raw/b3e99f1b4436ff487601671962732bd4.jpeg)


## Callback Content Description

### Simple callback (Simple)

The callback notification adopts the `POST` method of HTTP, with the `X-Ci-Content-Version: Simple` header.

The response body returns **application/json** data. The following contains all the nodes:

```plaintext
{
   "code": 0,
   "data": {
       "forbidden_status": 0,
       "event": "ReviewText",
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

The nodes are described as follows:

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :------ | :------- |
| code | Error code. 0: moderation succeeded; other values: moderation failed. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). | Integer | Yes |
| message | Error message. | String | Yes |
| data | Details of the text moderation result. | Object | Yes |

`data` is as described below:

| Parameter | Description | Type | Required |
| :--------------- | :----------------------------------------------------------- | :------ | :------- |
| trace_id | Unique ID. If the job is an async job created through an API, this value is the `JobId` returned by the API. | String | Yes |
| url | Full URL of the moderated text. | String | Yes |
| event | Triggered event, which is fixed at `ReviewText` here. | String | Yes |
| result | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer | Yes |
| forbidden_status | If you set auto-freezing, this field indicates the frozen status of the text. `0`: not frozen, `1`: frozen, `2`: file moved. | Integer | Yes |
| cos_headers      | The custom header content set when the resource is uploaded. If it is not set, it will not be returned.       | Object  | No       |
| porn_info        | The moderation result of the **pornographic information** moderation scene.                           | Object  | No       |
| ads_info         | The moderation result of the **advertising information** moderation scene.                       | Object  | No       |
| abuse_info       | The moderation result of the **abusive information** moderation scene.                           | Object  | No       |
| illegal_info     | The moderation result of the **illegal information** moderation scene.                           | Object  | No       |
| data_id          | The original content will be returned if the `DataId` parameter is set when the job is submitted, which can contain up to 512 bytes. | String  | No       |

`xx_info` is as described below:

| Parameter | Description | Type | Required |
| :------- | :------------------------------------------------------ | :------ | :------- |
| hit_flag | The moderation result returned for the moderation scene. Return values: **0** (normal), **1** (confirmed as a violation of the current scene), and **2** (suspected as a violation of the current scene).     | Integer | Yes       |
| label | Hit keyword. | String | Yes |
| count | The number of sensitive text segments that hit the moderation scene. | Integer | Yes |

### Detail callback (Detail)

The callback notification adopts the `POST` method of HTTP, with the `X-Ci-Content-Version: Detail` header.

The response body returns **application/json** data. The following contains all the nodes:

```plaintext
{
  "EventName": "ReviewText",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "",
    "Object": "",
    "Label": "Normal",
    "Result": 0,
    "SectionCount": 1,
    "PornInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "AdsInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "IllegalInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "AbuseInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "Section": [
      {
        "StartByte": 0,
        "Label": "Normal",
        "Result": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Keywords": ""
        },
        "IllegalInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Keywords": ""
        },
        "AbuseInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Keywords": ""
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Keywords": ""
        }
      }
    ],
    "BucketId": "",
    "Region": "ap-chongqing",
    "ForbidState": 0,
    "CosHeaders": {
        "x-cos-meta-id": "xxxxx"
    }
  }
}
```

The nodes are described as follows:

| Node Name (Keyword)         | Description                               | Type   |
| :----------------- | :--------------------------- | :----- |
| JobsDetail         | Job result details.         | Object |
| EventName          | Job type: ReviewText. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Code               | Error code, which will be returned only if `State` is `Failed`. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). | String |
| Message            | Error message, which will be returned only if `State` is `Failed`. | String |
| JobId              | ID of the text moderation job. | String |
| DataId             | The original content will be returned if the `DataId` parameter is set when the job is submitted, which can contain up to 512 bytes. | String  |
| State              | Status of the moderation job. Valid values: `Submitted`, `Success`, `Failed`, `Auditing`. | String |
| CreationTime       | Creation time of the moderation job. | String |
| Object             | The name of the text file to be moderated, which will be returned if `Object` is selected during job creation. | String |
| Content            | The Base64-encoded text content to be moderated, which will be returned if `Content` is selected during job creation. | String  |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Return values: `Normal`, `Porn`, `Ads`, `Illegal`, and `Abuse`. | String  |
| Result             | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |
| IllegalInfo        | The moderation result of the **illegal information** moderation scene.                           | Object  |
| AbuseInfo          | The moderation result of the **abusive information** moderation scene.                           | Object  |
| SectionCount      | The text moderation feature divides the text into segments for moderation, each of which contains 10,000 UTF-8 characters. This parameter indicates the number of segments. | Integer |
| Section            | Moderation result for each text segment.                                   | Array   |
| BucketId           | Name of the bucket of the created moderation job.                             | String  |
| Region             | Bucket region.                                           | String  |
| ForbidState        | If you set automatic freezing, this field indicates the status of the text. `0`: not frozen; `1`: frozen, `2`: file moved. | Integer |
| CosHeaders         | The custom header content set when the resource is uploaded to COS. If it is not set, it will not be returned. It is in a map structure, where `key` is the custom header name and `value` is the content.      | Object  | No       |
| UserInfo           | Business field.                                              | Container       |
| ListInfo           | Blocklist/Allowlist status of the account.                                           | Container |

`PornInfo`, `AdsInfo`, `IllegalInfo`, and `AbuseInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :------------------------------------------------------ | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Return values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Count              | The number of text segments that hit this moderation scene.                              | Integer |

`Section` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| StartByte | The starting position of the segment in the text (for example, 10 represents the 11th UTF-8 character). This value starts from 0. | Integer |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Return values: `Normal`, `Porn`, `Ads`, `Illegal`, and `Abuse`. | String  |
| Result             | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |
| IllegalInfo        | The moderation result of the **illegal information** moderation scene.                           | Object  |
| AbuseInfo          | The moderation result of the **abusive information** moderation scene.                           | Object  |

`PornInfo`, `AdsInfo`, `IllegalInfo`, and `AbuseInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Return values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Score              | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. Generally, a value in the range of 0–60, 61–90, or 91–100 means that the image is normal, suspiciously sensitive, or sensitive respectively. For example, `Porn 99` means that the content is very likely to be pornographic. | Integer |
| Keywords           | Keywords hit in the current moderation scene. Multiple keywords are separated by commas. | String |
| LibResults         | This field returns results based on recognition against the risk library. Note: This field will not be returned if no samples in the risk library are hit. | Container Array |
| SubLabel           | The specific sub-tag hit by the moderation job; for example, `SexBehavior` is a sub-tag under the `Porn` tag. Note: This field may return null, indicating that no specific sub-tags are hit. | String  |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----- |
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

| Node Name (Keyword) | Description | Type |
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
       "event":"ReviewText",
       "forbidden_status": 0,
       "porn_info": {
           "hit_flag": 0,
           "label": "",
           "count": 0
       },
       "result": 0,
       "trace_id": "ixzt90jl2dfscxxxxxxxxxxxxxxxxx",
       "url": "https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.txt",
       "cos_headers": {
           "x-cos-meta-id": "xxxxxx"
       }
   },
   "message": "success"
}
```

#### Sample 2: Detailed callback (Detail)

```plaintext
{
  "EventName": "ReviewText",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "2021-08-10T21:01:08+08:00",
    "Object": "1.txt",
    "Label": "Normal",
    "Result": 0,
    "SectionCount": 1,
    "PornInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "AdsInfo": {
      "HitFlag": 0,
      "Count": 0
    },
    "Section": [
      {
        "StartByte": 0,
        "Label": "Normal",
        "Result": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Keywords": ""
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0,
          "Keywords": ""
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

