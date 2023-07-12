## Feature Description

If you have configured a moderation callback address, the backend will call back the moderation result in JSON format to that address after webpage moderation is completed. You can perform subsequent file processing operations based on the callback content.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/NSJC438_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.jpeg)

## Callback Content Description

The response body returns **application/json** data. The following contains all the nodes:

```plaintext
{
  "EventName": "ReviewHtml",
  "JobsDetail": {
    "JobId": "6666666666666666666666666666666666",
    "State": "Success",
    "CreationTime": "",
    "Url": "",
    "Label": "Normal",
    "Suggestion": 0,
    "PageCount": 1,
    "Labels": {
      "PornInfo": {
        "HitFlag": 0,
        "Score": 0
      },
      "AdsInfo": {
        "HitFlag": 0,
        "Score": 0
      }
    },
    "ImageResults": {
      "Results": [
      {
        "Url": "",
        "Text": "",
        "Label": "Normal",
        "Suggestion": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0,
          "SubLabel": "",
          "OcrResults": [{
            "Text": "",
            "Keywords":["",""],
            "Location": {
              "X": 0,
              "Y": 0,
              "Width": 0,
              "Height": 0,
              "Rotate": 0
            }
          }]
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0,
          "SubLabel": ""
        }
      }
      ]
    },
    "TextResults": {
      "Results": [
      {
        "Text": "",
        "Label": "Normal",
        "Suggestion": 0,
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
      ]
    },
    "BucketId": "examplebucket-1250000000",
    "Region": "ap-chongqing",
    "ForbidState": 0,
    "CosHeaders": {
        "x-cos-meta-id": "666666"
    }
  }
}
```

The nodes are as described below:

| Node Name (Keyword) | Description | Type |
| :----------------- | :------------------------- | :----- |
| JobsDetail         | Job result details.         | Object |
| EventName          | Job type: ReviewHtml. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Code               | Error code, which will be returned only if `State` is `Failed`. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). | String |
| Message            | Error message, which will be returned only if `State` is `Failed`. | String |
| JobId              | Moderation job ID. | String |
| DataId             | This field will return the original content if the `DataId` parameter is configured during job submission, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business. | String |
| State              | Status of the moderation job. Valid values: `Submitted`, `Success`, `Failed`, `Auditing`. | String |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, and `Ads`. | String  |
| Suggestion         | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| CreationTime       | Creation time of the moderation job. | String |
| Url             | The URL of the webpage to be moderated, which will be returned if `Url` is selected during job creation. | String |
| PageCount          | Webpage moderation submits the image links and text in the webpage for separated moderation. This field indicates the total number of links and text pages submitted for moderation. | Integer |
| Labels | This field is used to return the hit moderation scenes and corresponding results. | Object |
| ImageResults       | Image moderation result of the webpage.                                       | Object  |
| TextResults        | Text moderation result of the webpage.                                       | Object  |
| HighlightHtml      | Highlighted HTML webpage content containing non-compliant keywords, which will be returned if `ReturnHighlightHtml` is specified in the request. | String |
| UserInfo           | Business field. This field will not exist if `UserInfo` is not set during job creation.                     | Object |
| ListInfo           | Blocklist/Allowlist status of the account.                                           | Container |

`Labels` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------- | :----- |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Returned values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Score              | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic.  | Integer |

`ImageResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :--------------------- | :---- |
| Results            | Image moderation result of the webpage. | Array |

`Results` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Url                | URL of the moderated image on the webpage, at which you can view the image. It must be a standard URL. | String |
| Text | This field is used to return the OCR text recognition result of the current image. It will be returned only if text content detection is enabled in the moderation policy. | String |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, and `Ads`. | String  |
| Suggestion         | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Returned values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Score              | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. Generally, a value in the range of 0–60, 61–90, or 91–100 means the image is normal, suspiciously sensitive, or sensitive respectively. For example, `Porn 99` means that the content is very likely to be pornographic. | Integer |
| Category           | This field indicates the specific moderation category hit; for example, `Sexy` presents the sexy category in the `Porn` tag. It may be null, indicating that no category is hit or there is no relevant category. | String |
| SubLabel           | This field indicates the specific sub-tag hit by the moderation job; for example, `SexBehavior` is a sub-tag under the `Porn` tag. </br>Note: This field may return null, indicating that no specific sub-tags are hit.  | String  |
| OcrResults | This field represents the detailed OCR result, including the text coordinate information and text recognition result. It will be returned if there is non-compliant content. | Array |
| LibResults         | This field returns results based on recognition against the risk library. </br>Note: This field will not be returned if no samples in the risk library are hit. | Container Array |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----- |
| ImageId            | This field represents the hit image sample ID in the risk library.                       | String  |
| Score              | This field returns the confidence under the current tag. Value range: 0–100.  The higher the value, the more likely the image hits a sample in the risk library.  For example, `Porn 99` means that the content is very likely to hit a pornographic sample in the library.  | Integer |

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

`TextResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :--------------------- | :---- |
| Results            | Text moderation result of the webpage. | Array |

`Results` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Text               | Text on the webpage is divided into segments for moderation, each of which contains 10,000 UTF-8 characters. This parameter returns the text content of the current segment. | String  |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, and `Ads`. | String  |
| Suggestion         | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo           | The moderation result of the **pornographic information** moderation scene.                           | Object  |
| AdsInfo            | The moderation result of the **advertising information** moderation scene.                       | Object  |

`PornInfo` and `AdsInfo` have the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| HitFlag            | The moderation result returned for the moderation scene. Returned values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).     | Integer |
| Score              | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. | Integer |
| Keywords           | Keywords hit in the current moderation scene. Multiple keywords are separated by comma. | String |
| LibResults         | This field returns results based on recognition against the risk library. </br>Note: This field will not be returned if no samples in the risk library are hit. | Container Array |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----- |
| LibType            | Type of the hit risk library. Valid values: `1` (preset blocklist/allowlist library), `2` (custom risk library). | Integer      |
| LibName            | Name of the hit risk library.                                           | String       |
| Keywords           | Keywords hit in the library. There may be multiple returned values representing multiple hit keywords. | String Array |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :--------------------- | :-------------------------------------------------- | :----- | :------- |
| TokenId            | Request.Input.UserInfo | Account information, which can contain up to 128 bytes.           | String | No       |
| Nickname           | Request.Input.UserInfo | Nickname information, which can contain up to 128 bytes.           | String | No       |
| DeviceId           | Request.Input.UserInfo | Device information, which can contain up to 128 bytes.           | String | No       |
| AppId              | Request.Input.UserInfo | Unique app ID, which can contain up to 128 bytes.           | String | No       |
| Room               | Request.Input.UserInfo | Room ID information, which can contain up to 128 bytes.           | String | No       |
| IP                 | Request.Input.UserInfo | IP address information, which can contain up to 128 bytes.           | String | No       |
| Type               | Request.Input.UserInfo | Business type, which can contain up to 128 bytes.           | String | No       |
| ReceiveTokenId     | Request.Input.UserInfo | User account to receive messages, which can contain up to 128 bytes.           | String | No       |
| Gender             | Request.Input.UserInfo | Gender information, which can contain up to 128 bytes.           | String | No       |
| Level              | Request.Input.UserInfo | Level information, which can contain up to 128 bytes.           | String | No       |
| Role               | Request.Input.UserInfo | Role information, which can contain up to 128 bytes.           | String | No       |

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

## Samples

```plaintext
{
  "EventName": "ReviewHtml",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "2021-08-10T21:01:10+08:00",
    "Url": "http://test.com/test.html",
    "Label": "Normal",
    "Suggestion": 0,
    "PageCount": 2,
    "Labels": {
      "PornInfo": {
        "HitFlag": 0,
        "Score": 0
      },
      "AdsInfo": {
        "HitFlag": 0,
        "Score": 0
      }
    },
    "ImageResults": {
      "Results": [
      {
        "Url": "http://xxx.xxx.com/a.jpg",
        "Text": "",
        "Label": "Normal",
        "Suggestion": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0,
          "SubLabel": "",
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0,
          "SubLabel": ""
        }
      }
      ]
    },
    "TextResults": {
      "Results": [
      {
        "Text": "xxxxxxx",
        "Label": "Normal",
        "Suggestion": 0,
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
      ]
    },
    "BucketId": "examplebucket-1250000000",
    "Region": "ap-chongqing",
    "ForbidState": 0,
    "CosHeaders": {
        "x-cos-meta-id": "xxxx"
    }
  }
}
```

