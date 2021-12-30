
To enable porn detection during live streaming, you need to enable screencapturing either in the [CSS console](https://intl.cloud.tencent.com/document/product/267/31072) or via APIs. This document describes how to implement porn detection via APIs.

## Enabling Porn Detection
As the porn detection feature is based on screencapturing, you have to enable screencapturing first before you can enable porn detection. The steps are as follows:

### 1. Create a screencapturing template with porn detection enabled
Call [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834), setting `PornFlag` to `1` to create a screencapturing template with porn detection enabled.

### 2. Create a screencapturing rule
Call [CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835) to create a screencapturing rule, binding the ID of the screencapturing template created in step 1 with the target `AppId`, `DomainName`, `AppName`, and `StreamName`.

### 3. Start live streaming
After you create a screencapturing rule with porn detection enabled, the porn detection feature will be automatically enabled for new streams. If you want to enable porn detection for an ongoing stream, you need to stop and restart the stream.

## Getting Porn Detection Result
After porn detection is enabled, you can configure a registered domain name in the porn detection callback template to receive callbacks of porn detection results.
>! By default, only questionable results will be called back.

### 1. Create a porn detection callback template
Call [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815), setting `PornCensorshipNotifyUrl` to your domain name to create a porn detection callback template.
### 2. Create a porn detection callback rule

Call [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) to create a porn detection callback rule, binding the ID of the porn detection callback template created in step 1 to the target `AppId`, `DomainName`, and `AppName`.

### 3. Get the porn detection result
The CSS backend sends the porn detection result to your registered domain name through an HTTP POST request where the result is stored in the HTTP body in JSON format. You can determine whether the live streaming is pornographic by checking the `type` field.
>!We recommend you use the `type` of an image to determine whether it is pornographic. As the detection system cannot achieve 100% accuracy, there may be false positives or false negatives, and human confirmation is recommended.  

#### The complete protocol is as follows:
| Parameter       | Required | Data Type | Description    |
| -------- | -------- | -------- | -------- |
| streamId       | No         | String       | Stream name    |
| channelId      | No         | String       | Channel ID                                                      |
| img            | Yes         | String       | Link to the alerted image                                               |
| type    | Yes     | Array    | Categories of negative labels with the highest priority in the detection result. For details, see the description of `label`. |
| score | Yes | Array | Scores of `type` |
| ocrMsg         | No         | String       | OCR result (if any)                         |
| suggestion | Yes | String | Suggestion. Valid values: <ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul>     |
| label       | Yes     | String   | Negative label with the highest priority in the detection result (`LabelResults`). This is the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. |
| subLabel    | Yes     | String   | Sub-label under the negative label with the highest priority in the detection result, such as porn - sexual acts. If no content is sub-labeled, this field will be empty. |
| labelResults   | No     | [Array of LabelResult](#labelresult)   | Negative label hit details of the category model, including the detected porn content, ads, terrorism content, and politically sensitive content <br>Note: **This field may return `null`, indicating that no valid values can be obtained.** |
| objectResults  | No     | [Array of ObjectResult](#objectresult) | Detection result of the object model, including label name, hit score, coordinates, scenario, and suggested operation regarding objects, advertising logos, QR codes, etc. For details, see the description of the data structure of `ObjectResults`. <br> Note: **This field may return `null`, indicating that no valid values can be obtained.** |
| ocrResults     | No     | [Array of OcrResult](#ocrresult)    | OCR result, including text coordinates, recognized text, suggested operation, etc. For details, see the description of the data structure of `OcrResults`.<br> Note: **This field may return `null`, indicating that no valid values can be obtained.** |
| libResults | No    | [Array of LibResult](#libresult) | Blocklist/Allowlist moderation result  |
| screenshotTime | Yes         | Number       | Screenshot time              |
| sendTime       | Yes         | Number       | Time when the request was sent, in Unix timestamp format  |
| stream_param   | No         | String       | Push parameters                              |
| app   | No | String | Push domain name   |
| appid  | No | Number |  Application ID |
| appname        | No        | String       | Push path  |

 

#### LabelResult
Hit result of the category model

| Parameter | Type | Description |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String                                       | Scenario identified by the model, such as advertising, pornographic, and harmful     |
| Suggestion | String                                       | Operation suggested by the system for the current negative label. We recommend you handle different types of violations and suggestions based on your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| label | String   | Negative label in the detection result |
| SubLabel   | String | Sub-label name |
| Score      | Integer | Hit score of the label model                                         |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | Sub-label hit details of the category model                                   |

#### LabelDetailItem

Sub-label hit details of the category model

| Parameter | Type | Description |
| -------- | -------- | ----- |
| Id       | Integer  | ID                        |
| Name     | String   | Sub-label name                  |
| Score    | Integer  | Sub-label score. Value range: 0-100 |


#### ObjectResult

Object detection result

| Parameter| Type | Description |
| ---------- | --------------------- | --------------------- |
| Scene      | String                                       | Object scenario identified, such as QR code, logo, and OCR     |
| Suggestion | String                                       | Operation suggested by the system for the current negative label. We recommend you handle different types of violations and suggestions based on your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| label | String   | Negative label in the detection result |
| SubLabel   | String | Sub-label name |
| Score    | Integer  | Sub-label hit score of the scenario model. Value range: 0-100 |
| Names      | Array of String       | List of object names |
| Details    | Array of [ObjectDetail](#objectdetail) | Object detection details |

#### ObjectDetail

Object detection details. When the detection scenario is object, advertising logo, or QR code, it returns the label name, label value, label score, and location information of the detection frame.

| Parameter | Type | Description |
| -------- | -------- | -------- |
| Id    | Integer    | ID of the object identified    |
| Name     | String     | Object label identified   |
| Value    | String     | Value or content of the object label identified. For example, if the label is QR code (`QrCode`), this parameter is the URL of the QR code. |
| Score    | Integer    | Hit score of the object label. Value range: 0-100. For example, `QrCode 99` indicates a high likelihood that the content is a QR code. |
| Location | [Location](#location) | Coordinates (of the top-left corner), dimensions, and rotation of the object detection frame |

#### Location

Coordinates and other information of the detection frame

| Parameter | Type | Description |
| -------- | -------- | ---------------- |
| X        | Float    | Horizontal coordinate of the top-left corner     |
| Y        | Float    | Vertical coordinate of the top-left corner     |
| Width    | Float    | Width             |
| Height   | Float    | Height             |
| Rotate   | Float    | Rotation angle of the detection frame |

#### OcrResult

OCR result

| Parameter| Type | Description |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String                                   | Recognition scenario. Default value: OCR              |
| Suggestion | String                                       | Operation suggested by the system for the negative label with the highest priority. We recommend you handle different types of violations and suggestions based on your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| label | String   | Negative label in the detection result |
| SubLabel   | String | Sub-label name |
| Score    | Integer  | Sub-label hit score of the scenario model. Value range: 0-100 |
| Text       | String | Text |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR details |


#### OcrTextDetail
OCR details

| Parameter | Type | Description |
| -------- | --------------- | --------------- |
| Text | String | Text recognized (up to **5,000 bytes**) |
| label | String   | Negative label in the detection result |
| Keywords | Array of String | Keywords hit under the label |
| Score    | Integer  | Hit score of the label model. Value range: 0-100 |
| Location | [Location](#location) | OCR text coordinates |


#### LibResult
Blocklist/Allowlist result

| Parameter| Type | Description |
| ---------- | ------------------ | ------------------ |
| Scene      | String                           | Scenario recognition result of the model. Default value: Similar                 |
| Suggestion | String                                       | Operation suggested by the system. We recommend you handle different types of violations and suggestions based on your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| label | String   | Negative label in the detection result |
| SubLabel   | String | Sub-label name |
| Score | Integer | Recognition score of the image search model. Value range: 0-100 |
| Details    | Array of [LibDetail](#libdetail) | Blocklist/Allowlist details |

#### LibDetail
Custom list or blocklist/allowlist details

| Parameter | Type | Description |
| -------- | -------- | ------------------ |
| Id       | Integer  | ID                        |
| ImageId  | String   | Image ID                                                       |
| label | String   | Negative label in the detection result |
| Tag | String | Custom label |
| Score | Integer | Model recognition score. Value range: 0-100 |



#### Sample callback message
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "suggestion": "Block",
        "label": "Porn",
        "subLabel": "PornHigh",
        "labelResults": [{
                "HitFlag": 0,
                "Scene": "Illegal",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 1,
                "Scene": "Porn",
                "Suggestion": "Block",
                "Label": "Porn",
                "SubLabel": "PornHigh",
                "Score": 99,
                "Details": [{
                        "Id": 0,
                        "Name": "PornHigh",
                        "Score": 99
                }, {
                        "Id": 1,
                        "Name": "WomenChest",
                        "Score": 99
                }]
        }, {
                "HitFlag": 0,
                "Scene": "Sexy",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "Terror",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }],
        "objectResults": [{
                "HitFlag": 0,
                "Scene": "QrCode",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "MapRecognition",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "PolityFace",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }],
        "ocrResults": [{
                "HitFlag": 0,
                "Scene": "OCR",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Text": "",
                "Details": []
        }],
        "streamId": "teststream",
        "channelId": "teststream",
        "stream_param": "txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
        "app": "5000.myqcloud.com",
        "appname": "live",
        "appid": 10000,
        "event_type": 317,
        "sign": "ac920c3e66**********78cf1b5de2c63",
        "t": 1615860427
}
:::
</dx-codeblock>



## Disabling Porn Detection

You can disable porn detection by deleting the screencapturing rule or modifying the screencapturing template. Both the deletion and modification are effective only for new live streams. If you want to disable porn detection for an ongoing live stream, you have to stop and restart the stream.

### 1. Delete the screencapturing rule

Call [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833), passing in the `DomainName`, `AppName`, and `StreamName` bind to the screencapturing template ID to delete the screencapturing rule.

### 2. Modify the screencapturing template

Call [ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828), setting `PornFlag` to `0.
