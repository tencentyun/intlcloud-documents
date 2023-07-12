## Feature Description

If you have configured a moderation callback address, after file moderation is completed, the backend will call back the moderation result in JSON format to the callback address. You can perform subsequent file processing operations based on the callback content.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/NSJC438_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.jpeg)

## Callback Content Description

The response body returns **application/json** data. The following contains all the nodes:

```plaintext
{
  "EventName": "ReviewDocument",
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
    "PageSegment": {
      "Results": [
      {
        "Url": "",
        "Text": "",
        "PageNumber": 0,
        "SheetNumber": 0,
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
| :----------------- | :----------------------------- | :----- |
| JobsDetail         | Job result details.         | Object |
| EventName          | Job type: ReviewDocument. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Code               | Error code, which will be returned only if `State` is `Failed`. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). | String |
| Message            | Error message, which will be returned only if `State` is `Failed`. | String |
| JobId              | Moderation job ID. | String |
| DataId             | The original content will be returned if the `DataId` parameter is set when the job is submitted, which can contain up to 512 bytes. | String  |
| State              | Status of the moderation job. Valid values: `Submitted`, `Success`, `Failed`, `Auditing`. | String |
| Label              | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, and `Ads`. | String  |
| Suggestion         | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), `2` (suspiciously sensitive, with human review recommended). | Integer |
| CreationTime       | Creation time of the moderation job. | String |
| Object | If the moderated file is a file stored in COS, this field indicates its filename. | String |
| Url             | The URL of the file to be moderated, which will be returned if `Url` is selected during job creation. | String |
| PageCount | File moderation converts a file to images for moderation. This field indicates the total number of generated images. | Integer |
| Labels | This field is used to return the hit moderation scenes and corresponding results. | Object |
| PageSegment | Specific moderation result of each image after the file is converted to images. | Object |
| ForbidState        | If you set automatic freezing, this field indicates the status of the file. `0`: Not frozen; `1`: Frozen, `2`: File moved. | Integer |
| CosHeaders         | The custom header content set when the resource is uploaded to COS. If it is not set, it will not be returned. It is in a map structure, where `key` is the custom header name and `value` is the content.      | Object  | No       |
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

`PageSegment` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :------------------------------------------- | :---- |
| Results            | Detailed moderation result of each image after the file is converted to images. | Array |

`Results` has the following sub-nodes:

| Node Name (Keyword) | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------ |
| Url                | After the file is converted to images, you can view the image content at this URL. It must be a standard URL. Note: Each URL is valid for two hours. If you need to view the data after two hours, initiate a new query request. | String |
| Text | This field is used to return the OCR text recognition result of the current image. It will be returned only if text content detection is enabled in the moderation policy. | String |
| PageNumber | Number of images, which is usually the number of pages in the file. | Integer |
| SheetNumber | If the moderated file is a spreadsheet, this field indicates the number of sheets. | Integer |
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
| SubLabel           | This field indicates the specific sub-tag hit by the moderation job; for example, `SexBehavior` is a sub-tag under the `Porn` tag. Note: This field may return null, indicating that no specific sub-tags are hit. | String  |
| OcrResults | This field represents the detailed OCR result, including the text coordinate information and text recognition result. It will be returned if there is non-compliant content. | Array |
| LibResults         | This field returns results based on recognition against the risk library. Note: This field will not be returned if no samples in the risk library are hit. | Container Array |

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

## Samples

```plaintext
{
  "EventName": "ReviewDocument",
  "JobsDetail": {
    "JobId": "xxxxxx",
    "State": "Success",
    "CreationTime": "2021-08-10T21:01:10+08:00",
    "Url": "http://test.com/test.doc",
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
    "PageSegment": {
      "Results": [
      {
        "Url": "http://audit-125000000.cos.ap-chongqing.myqcloud.com/1.jpg",
        "Text": "",
        "PageNumber": 1,
        "SheetNumber": 0,
        "Label": "Normal",
        "Suggestion": 0,
        "PornInfo": {
          "HitFlag": 0,
          "Score": 0,
          "SubLabel": ""
        },
        "AdsInfo": {
          "HitFlag": 0,
          "Score": 0,
          "SubLabel": ""
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
