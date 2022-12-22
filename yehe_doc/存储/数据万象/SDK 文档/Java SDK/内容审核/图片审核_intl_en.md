## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation.

| API | Description |
| ------------- |  ---------------------- |
| [Moderating single image](https://intl.cloud.tencent.com/document/product/1045/49320) |  Scans existing data stored in COS for pornographic, illegal, and advertising images. |
| [Batch moderating images](https://intl.cloud.tencent.com/document/product/1045/49321) |  Moderates multiple images in batches. |


## Single Image Moderation

#### Feature description

The existing data scan feature of image moderation leverages CI's persistent processing API to scan existing data stored in COS for pornographic, illegal, and advertising images.

#### Method prototype

```java
ImageAuditingResponse imageAuditing(ImageAuditingRequest request);
```


#### Sample request

```java
//1. Create a job request object
ImageAuditingRequest request = new ImageAuditingRequest();
//2. Add request parameters as detailed in the API documentation
//2.1 Set the request bucket
request.setBucketName("examplebucket-1250000000");
//2.2 Set the moderation type
request.setDetectType("porn,ads");
//2.3 Set the image location in the bucket
request.setObjectKey("1.png");
//3. Call the API to get the job response object
ImageAuditingResponse response = client.imageAuditing(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required |
| ------------------ |-------------------------------------------------------- | --------- | ---- |
| ObjectKey          | Name of the image file in the COS bucket. The COS bucket is specified by `Host`. For example, if the file is `img.jpg` in the `test` directory in the `examplebucket-1250000000` bucket in Beijing, then `Host` is `examplebucket-1250000000.cos.ap-beijing.myqcloud.com`, and `ObjectKey` is `test/img.jpg`. | String | No |
| bizType           | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). You can get `bizType` in the console. If `bizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `bizType` is not specified, the default moderation policy will be used automatically. | String | No       |
| detectType        | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `bizType` parameter. | String | No       |
| detectUrl         | You can enter a `detectUrl` value to moderate an image accessible over the public network. If `detectUrl` is not specified, the backend will moderate by `ObjectKey` by default. If `detectUrl` is specified, the backend will moderate by `detectUrl`, and there will be no need to enter `ObjectKey`. Sample `detectUrl`: `http://www.example.com/abc.jpg`. | String | No       |
| interval           | For GIF image moderation, you can use this parameter to configure the frame capturing interval. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int | No |
| maxFrames         | The maximum number of frames to be captured for GIF image moderation, which must be greater than 0. The default value is `5`, indicating to capture five frames at most. | Int | No |
| largeImageDetect | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and image compression fees will be charged. For large animated images such as GIF, the compression time is long, which may cause the moderation to fail due to timeout. | Int | No |
| dataId | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| async | Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.  | Int    | No       |
| callback | The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect for async moderation. Addresses starting with `http://` or `https://` are supported, such as  `http://www.callback.com`.  | String | No |


#### Response description

- Success: An `ImageAuditingResponse` instance is returned upon success, which contains the moderation result.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

Content of the `ImageAuditingResponse` object after it is converted to JSON:
```json
{
    "requestId":"NjJkOTI3YTJfNGNhY2ZhMDlfOWJhOV9hZ*****",
    "jobId":"si461d9f9608de11ed9b3d525400b*****",
    "object":"1.png",
    "compressionResult":"0",
    "result":"0",
    "label":"Normal",
    "category":"",
    "subLabel":"",
    "score":"42",
    "text":"",
    "state":"Success",
    "pornInfo":{
        "code":"0",
        "msg":"OK",
        "hitFlag":"0",
        "score":"0",
        "label":"",
        "ocrResults":{
            "text":"",
            "keywords":""
        },
        "category":""
    }
}
```

The response body is as described below:

| Parameter | Type | Description |
| ----------------- | --------- | ------------------------------------------------------------ |
| DataId            | String    | Image ID. The original content will be returned in the moderation result, which can contain up to 512 bytes.        |
| JobId             | String    | Image moderation job ID.                                          |
| State             | String    | Status of the moderation job. Valid value: `Success`. |
| Object            | String    | The name of the image stored in the COS bucket, which will be returned if `ObjectKey` is selected during job creation.  |
| Url               | String    | The URL of the image file, which will be returned if `detect-url` is selected during job creation.                    |
| CompressionResult | Int   | Whether the image is compressed. Valid values: `0` (no), `1` (yes).        |
| Result            | Int       | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), and `2` (suspiciously sensitive, with human review recommended). |
| Label             | String    | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, `Ads`, and other types of unsafe or inappropriate content. |
| Category          | String    | This field is a subset of `Label`, indicating the specific moderation category hit; for example, `Sexy` presents the sexy category in the `Porn` tag. |
| SubLabel          | String    | Second-level tag hit by the image.                                       |
| Score      | Int         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. |
| Text              | String    | The specific text content recognized by OCR in the image, which will be returned if text content detection is enabled in the moderation policy.    |
| PornInfo          | Container | The moderation result of the **pornographic information** moderation scene.                             |
| AdsInfo           | Container | The moderation result of the **advertising information** moderation scene.                         |

The moderation information (`PornInfo` and `AdsInfo`) has the following sub-nodes:

| Parameter | Type | Description |
| ---------- | --------------- | ------------------------------------------------------------ |
| Code       | Int             | Error code. `0` indicates a success, while other numbers correspond to different errors. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| Msg        | String          | The specific error message, which will be `OK` if the moderation result is normal. |
| HitFlag    | Int         | The moderation result returned for the moderation scene. Returned values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).   |
| Score      | Int         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. A value in the range of 0–60, 61–90, or 91–100 means the image is normal, suspiciously sensitive, or sensitive respectively. For example, `Porn 99` means that the content is very likely to be pornographic.  |
| Label      | String          | This field indicates the overall result tag of the screenshot, which may be `SubLabel`, a person name, etc. |
| Category          | String    | This field is a subset of `Label`, indicating the specific moderation category hit; for example, `Sexy` presents the sexy category in the `Porn` tag. |
| SubLabel   | String          | This field indicates the specific sub-tag hit by the moderation job; for example, `SexBehavior` is a sub-tag under the `Porn` tag. </br>Note: This field may return null, indicating that no specific sub-tags are hit. |
| OcrResults | Container Array | This field represents the detailed OCR result, including the text recognition result and hit keyword. It will be returned if there is non-compliant content. |
| LibResults | Container Array | This field returns results based on recognition against the risk library. </br>Note: This field will not be returned if no samples in the risk library are hit. |

`LibResults` has the following sub-nodes:

| Parameter | Type | Description |
| -------- | ------- | ------------------------------------------------------- |
| ImageId  | String  | This field represents the hit image sample ID in the risk library.                       |
| Score    | String | This field returns the confidence under the current tag. Value range: 0–100.  The higher the value, the more likely the image hits a sample in the risk library.  For example, `Porn 99` means that the content is very likely to hit a pornographic sample in the library. |

`OcrResults` has the following sub-nodes:

| Parameter | Type | Description |
| -------- | ------------ | ------------------------------------------------------------ |
| Text     | String       | The specific text content recognized by OCR in the image.                            |
| Keywords | Array        | Keywords hit by the current moderation scene.  |
| Location | Container    | This parameter is used to return the position (X and Y coordinates of the top-left corner, length, width, and rotation angle) of the OCR detection frame in the image for quick location of the recognized text. |

| Parameter | Type | Description |
| :----- | :---- | :----------------------------------------------------------- |
| X      | Float | This parameter is used to return the pixel position of the **abscissa (X) of the top-left corner** of the detection frame. It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Y      | Float | This parameter is used to return the pixel position of the **ordinate of the top-left corner** (Y) of the detection frame. It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Width  | Float | This parameter is used to return the **width of the detection frame** (the length starting from the top-left corner and extending to the right on the X axis). It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Height | Float | This parameter is used to return the **height of the detection frame** (the length starting from the top-left corner and extending down the Y axis). It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Rotate | Float | This parameter is used to return the **rotation angle of the detection frame**. Valid values: **0–360** (**degrees**), and the direction is **counterclockwise rotation**. This parameter can be combined with the `X` and `Y` coordinate parameters to uniquely determine the specific position of the detection frame. |

## Batch Image Moderation

#### Feature description

The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files.

#### Method prototype

```java
BatchImageAuditingResponse batchImageAuditing(BatchImageAuditingRequest request);
```


#### Sample request

```java
//1. Create a job request object
BatchImageAuditingRequest request = new BatchImageAuditingRequest();
//2. Add request parameters as detailed in the API documentation
//2.1 Set the request bucket
request.setBucketName("examplebucket-1250000000");
//2.2 Add the request content
List<BatchImageAuditingInputObject> inputList = request.getInputList();
BatchImageAuditingInputObject input = new BatchImageAuditingInputObject();
input.setObject("1.jpg");
input.setDataId("DataId");
inputList.add(input);

input = new BatchImageAuditingInputObject();
input.setUrl("https://examplebucket-1250000000.cos.ap-chongqing.myqcloud.com/1.png");
input.setDataId("DataId");
inputList.add(input);

//2.2 Set the moderation type
request.getConf().setDetectType("all");
//3. Call the API to get the job response object
BatchImageAuditingResponse response = client.batchImageAuditing(request);
List<BatchImageJobDetail> jobList = response.getJobList();
```


#### Parameter description

`request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------------------- | :-------- | :--- |
| Request | None | Batch image moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :-------------------------------------------------- | :-------------- | :--- |
| Input | Request | Content to be moderated. If there are multiple images, pass in multiple `Input` structures. | Container Array | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :--- |
| Object | Request.Input | Name of the image file stored in the COS bucket; for example, if the file is `image.jpg` in the `test` directory, then the filename is `test/image.jpg`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url | Request.Input | Full URL of the image file, such as `http://a-1250000.cos.ap-shanghai.myqcloud.com/image.jpg`. Either `Object` or `Url` can be selected at a time. | String | No |
| Interval | Request.Input | Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int | No |
| MaxFrames | Request.Input | The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0. | Int | No |
| DataId | Request.Input | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| LargeImageDetect | Request.Input | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. </br>Note: Images up to 32 MB in size can be compressed, and compression fees will be charged.  | Int | No |
| UserInfo | Request.Input | Business field. | Container | No |


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

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Async | Request.Conf | Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.  | Integer | No |
| Callback | Request.Conf | The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect for async moderation. Addresses starting with `http://` or `https://` are supported, such as  `http://www.callback.com`.  | String | No |

>!
> - Moderation through `Object` is a private network operation and will not generate public network traffic.
> - Moderation through `Url` will generate public network traffic with regard to the origin where the image resides.
> 

#### Response description

- Success: A `BatchImageAuditingResponse` instance is returned upon success, which contains the moderation result.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

Content of the `ImageAuditingResponse` object after it is converted to JSON:
```json
{
  "requestId":"NjJkOTJjMjVfMTIwNjUzMDlfNDg5OF8*****",
  "jobList":[
    {
      "dataId":"DataId",
      "jobId":"sif6423b8008e011ed9b3d525400*****",
      "category":"",
      "label":"Normal",
      "result":"0",
      "object":"1.jpg",
      "score":"0",
      "subLabel":"",
      "text":"",
      "code":"",
      "message":"",
      "url":"",
      "compressionResult":"0",
      "pornInfo":{
        "code":"0",
        "msg":"OK",
        "hitFlag":"0",
        "score":"45",
        "label":"",
        "keywords":"",
        "count":"",
        "subLabel":"",
        "ocrResults":{
          "text":"",
          "keywords":""
        },
        "category":""
      },
      "adsInfo":{
        "code":"0",
        "msg":"OK",
        "hitFlag":"0",
        "score":"0",
        "label":"",
        "keywords":"",
        "count":"",
        "subLabel":"",
        "ocrResults":{
          "text":"",
          "keywords":""
        },
        "category":""
      },
      "userInfo":{
        "tokenId":"",
        "nickname":"",
        "deviceId":"",
        "appId":"",
        "room":"",
        "ip":"",
        "type":"",
        "receiveTokenId":"",
        "gender":"",
        "level":"",
        "role":""
      },
      "ocrResults":{
        "text":"",
        "keywords":""
      }
    },
    {
      "dataId":"DataId",
      "jobId":"sif640a3c108e011ed9b3d525400*****",
      "category":"",
      "label":"Normal",
      "result":"0",
      "object":"",
      "score":"42",
      "subLabel":"",
      "text":"",
      "code":"",
      "message":"",
      "url":"https://demo-1234567890.cos.ap-chongqing.myqcloud.com/1.png",
      "compressionResult":"0",
      "pornInfo":{
        "code":"0",
        "msg":"OK",
        "hitFlag":"0",
        "score":"0",
        "label":"",
        "keywords":"",
        "count":"",
        "subLabel":"",
        "category":"",
        "ocrResults":{
          "text":"",
          "keywords":""
        }
      },
      "adsInfo":{
        "code":"0",
        "msg":"OK",
        "hitFlag":"0",
        "score":"0",
        "label":"",
        "keywords":"",
        "count":"",
        "subLabel":"",
        "category":"",
        "ocrResults":{
          "text":"",
          "keywords":""
        }
      },
      "userInfo":{
        "tokenId":"",
        "nickname":"",
        "deviceId":"",
        "appId":"",
        "room":"",
        "ip":"",
        "type":"",
        "receiveTokenId":"",
        "gender":"",
        "level":"",
        "role":""
      },
      "ocrResults":{
        "text":"",
        "keywords":""
      }
    }
  ]
}
```

The response body is as described below:

`Response` has the following sub-nodes:

| Parameter | Type | Description |
| :--------- | :-------------- | :----------------------------------------------------------- |
| JobsDetail | Array | Image moderation result.                                               |
| RequestId  | String          | The ID automatically generated by the server for a request when the request is sent, which can help locate problems faster. |

`JobsDetail` has the following sub-nodes:

| Parameter | Type | Description |
| :---------------- | :-------- | :----------------------------------------------------------- |
| Code              | String    | Error code, which will be returned only in case of a failure. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| Message           | String    | Error message, which will be returned only in case of a failure.        |
| DataId            | String    | Image ID. The original content will be returned in the moderation result, which can contain up to 512 bytes.        |
| JobId             | String    | Moderation job ID.                                          |
| State             | String    | Status of the moderation job. Valid values: `Success`, `Failed`. |
| Object            | String    | The name of the image file stored in the COS bucket, which will be returned if `Object` is selected during job creation.  |
| Url               | String    | The URL of the image file, which will be returned if `Url` is selected during job creation.                    |
| CompressionResult | Integer   | Whether the image is compressed. Valid values: `0` (no), `1` (yes).        |
| Label             | String    | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, `Ads`. |
| Result            | Integer   | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), and `2` (suspiciously sensitive, with human review recommended). | 
| Score      | Integer         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. |
| Category          | String    | Moderation type hit by the image.                                     |
| SubLabel          | String    | Second-level tag hit by the image.                                       |
| Text              | String    | The specific text content recognized by OCR in the image, which will be returned if text content detection is enabled in the moderation policy.    |
| PornInfo          | Container | The moderation result of the **pornographic information** moderation scene.                             |
| AdsInfo           | Container | The moderation result of the **advertising information** moderation scene.                         |
| UserInfo          | Container | `UserInfo` set in the request, which will be returned as-is.                                 |
| ListInfo          | Container | Blocklist/Allowlist status of the account.                                           |

The moderation information (such as `PornInfo` and `AdsInfo`) has the following sub-nodes:

| Parameter | Type | Description |
| :--------- | :-------------- | :----------------------------------------------------------- |
| Code       | Integer         | Error code for individual moderation scenes. 0: Succeeded; other values: Failed. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| Msg        | String          | The specific error message, which will be `OK` if the moderation result is normal. |
| HitFlag    | Integer         | The moderation result returned for the moderation scene. Returned values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).   |
| Score      | Integer         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. |
| Label      | String          | The overall result tag of the image, which may be `SubLabel`, a person name, etc. |
| Category          | String    | This field is a subset of `Label`, indicating the specific moderation category hit; for example, `Sexy` presents the sexy category in the `Porn` tag. |
| SubLabel   | String          | Second-level tag of the image.                                           |
| OcrResults | Container Array | This field represents the detailed OCR result, including the text coordinate information and text recognition result. It will be returned if there is non-compliant content. |
| LibResults | Container Array | This field returns results based on recognition against the risk library. Note: This field will not be returned if no samples in the risk library are hit. |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :----------------- | :----------- | :--------------------------- |
| ImageId  | String  | This field represents the hit image sample ID in the risk library.                       |
| Score              | Integer      | This field returns the confidence under the current tag. Value range: 0–100.  The higher the value, the more likely the image hits a sample in the risk library.  For example, `Porn 99` means that the content is very likely to hit a pornographic sample in the library. |

`OcrResults` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :----------------- | :----------- | :--------------------------- |
| Text               | String       | Sensitive OCR text content   |
| Keywords           | String Array | Sensitive words in the text content       |

`UserInfo` has the following sub-nodes (same as `UserInfo` in the request):

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

| Node Name (Keyword) | Type | Description |
| :---------------- | :-------------- | :------------------------------------------------------ |
| ListResults       | Container Array | Results in all hit lists. |

`ListResults` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :---------------- | :------ | :------------------------------------------------------ |
| ListType          | String | Type of the hit list. Valid values: `0` (allowlist), `1` (blocklist). |
| ListName          | String  | Name of the hit list.                                 |
| Entity            | String  | Entity hit in the list.                         |
