CSS porn detection takes real-time screenshots of suspiciously pornographic video images in live streams and stores them in COS. The porn detection callback is used to push the information of detected pornographic images, including their type, score, and screenshot time. You need to configure the server address for receiving porn detection callback messages in the callback template and bind the template to the push domain name. When a porn detection event is triggered by a live stream, the Tencent Cloud CSS backend will call back the pornographic image information to the configured receiving server.

This document describes the fields in callback message notifications sent by Tencent Cloud CSS after a porn detection callback event is triggered.

## Note
- You need to understand how to configure callbacks and how you will receive messages via Tencent Cloud CSS before reading this document. For more information, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080).
- By default, only questionable results of porn detection will be called back.
- We recommend you use the `[type](#type)` of an image to determine whether it is pornographic. As the detection results are not 100% accurate and there may be false positives or false negatives, you can confirm them manually if necessary.

## Screencapturing Event Parameters
### Event type parameters

| Event Type | Parameter Value           |
| :------- | :------------- |
| CSS porn detection | event_type = 317 |


### Common callback parameters

<table>
<tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Expiration time, which is the Unix timestamp when the event notification signature expires. <ul style="margin:0"><li>The default expiration time of a message notification from Tencent Cloud is 10 minutes. If the time specified by the `t` value in a message notification has elapsed, it can be determined that this notification is invalid, thereby preventing network replay attacks. <li>The format of `t` is a decimal Unix timestamp, i.e., the number of seconds that have elapsed since 00:00:00 (UTC/GMT time), January 1, 1970.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Event notification security signature sign = MD5(key + t). <br>Note: Tencent Cloud concatenates the encryption <a href="#key">key</a> and `t`, calculates the `sign` value through MD5, and places it in the notification message. When your backend server receives the notification message, it can confirm whether the `sign` is correct based on the same algorithm and then determine whether the message is indeed from the Tencent Cloud backend.</td>
</tr></table>

>? [](id:key)`key` is the callback key in **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**, which is mainly used for authentication. We recommend filling in this field to ensure data security.
![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)




### Callback message parameters
| Parameter | Required | Data Type | Description |
| ---------- | ---------- | ---------- | --------------------------- |
| streamId       | No         | String       | Stream name                                       |
| channelId | No | String | Channel ID |
| img | Yes | String | Link to the alerted image |
| type | Yes | Array | Returns the **maliciousness label with the highest priority** in the detection result (labelResults), which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Returned values: <ul style="margin:0"><li/>0: normal<li/>1: pornographic<li/>6: abusive<li/>8: advertising<li/>2–5 and 7: other offensive, unsafe, or inappropriate types of content</ul> |
| score | Yes | Array | The score of `type` |
| hotScore    | Yes         | Number       | The score for a sexy image                                       |
| pornScore    | Yes         | Number       | The score for a porn image                                         |
| illegalScore   | Yes | Number       | The score for an image with illegal content    |
| polityScore    | Yes | Number       | The score for an image with politically sensitive content                                        |
| terrorScore    | Yes | Number       | The score for an image with terrorism content|
| abuseScore    | Yes         | Number       | The score for an abusive image                                       |
| teenagerScore    | Yes         | Number       | The score for an image with content inappropriate for teenagers                                       |
| adScore    | Yes         | Number       | The score for an advertising image                                       |
| ocrMsg         | No         | String       | OCR text (if applicable)                              |
| suggestion | Yes | string | Suggestion. Valid values: <ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul>     |
| label | Yes | string | Returns the **maliciousness label with the highest priority** in the detection result (labelResults), which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Returned value: <ul style="margin:0"><li/>Normal: normal<li/>Porn: pornographic<li/>Abuse: abusive<li/>Ad: advertising<li/>Custom: other offensive, unsafe, or inappropriate types of content</ul> |
| subLabel | Yes     | string | Sub-label name. If no sub-labels are hit, an empty string will be returned              |
| labelResults | No     | Array of [LabelResult](#labelresult)  | Moderation result of the category detection model, including pornographic, sexy, terrorism, illegal, and other results |
| objectResults | No     | Array of [ObjectResult](#objectresult) | Moderation result of the object detection model, including politically sensitive object, advertising logo, QR code, and other information |
| ocrResults | No     | Array of [OcrResult](#ocrresult) | Moderation result of the OCR text, including OCR text and text moderation result details |
| libResults | No    | Array of [LibResult](#libresult) | Moderation result of the risky image library |
| screenshotTime | Yes | Number | Screenshot time |
| sendTime       | Yes        | Number       | The time the request was sent in UNIX timestamp format |
| similarScore   | No   | Number  | Image similarity score   |
| stream_param   | No         | String       | Push parameter                                                     |
| app   | No | String | Push domain name   |
| appid  | No | Number |  APPID |
| appname        | No        | String       | Push path  |

 

#### LabelResult
Hit result of the category model.

| Name | Type | Description |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String                                       | Returns the scenario identified by the model, such as advertising, pornographic, and harmful.     |
| Suggestion | String                                       | Returns the operation suggestion for the current maliciousness label. When you get the determination result, the returned value indicates the action suggested by the system. We recommend you handle different types of violations and suggestions according to your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| Label  | String | Returns the maliciousness label in the detection result. Returned values: <ul style="margin:0"><li/>Normal: normal<li/>Porn: pornographic<li/>Abuse: abusive<li/>Ad: advertising<li/>Custom: other offensive, unsafe, or inappropriate types of content</ul> |
| SubLabel   | String | Sub-label name                                                   |
| Score      | Integer | Hit score of the label model                                         |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | Sub-label hit result details of the category model                                   |

#### LabelDetailItem

Sub-label hit result details of the category model.

| Name | Type | Description |
| -------- | -------- | --------------------------- |
| Id       | Integer  | ID                        |
| Name     | String   | Sub-label name                  |
| Score    | Integer  | Sub-label score. Value range: 0–100 |


#### ObjectResult

Object detection result details.

| Name | Type | Description |
| ---------- | --------------------- | --------------------- |
| Scene      | String                                       | Returns the identified object scenario, such as QR code, logo, and image OCR.     |
| Suggestion | String                                       | Returns the operation suggestion for the current maliciousness label. When you get the determination result, the returned value indicates the action suggested by the system. We recommend you handle different types of violations and suggestions according to your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| Label      | String                                 | Returns the maliciousness label in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Returned value: <ul style="margin:0"><li/>Normal: normal<li/>Porn: pornographic<li/>Abuse: abusive<li/>Ad: advertising<li/>Custom: other offensive, unsafe, or inappropriate types of content</ul> |
| SubLabel   | String | Sub-label name |
| Score    | Integer  | Sub-label hit score of the scenario model. Value range: 0–100 |
| Names      | Array of String       | List of object names |
| Details    | Array of [ObjectDetail](#objectdetail) | Object detection result details |

#### ObjectDetail

Object detection result details. When the detection scenario is a politically sensitive object/figure, advertising logo, QR code, or face attribute, it represents the label name, label value, label score, and location information of the model detection frame.

| Name | Type | Description |
| -------- | -------- | -------- |
| Id       | Integer  | ID  |
| Name | String | Label name |
| Value | String | Label value: <ul style="margin:0"><li/>When the scenario is `Ad`, it represents the URL. For example, when `Name` is `QrCode`, `Value` will be `http//abc.com/aaa`<br><li/>When the scenario is `FaceAttribute`, it represents the face attribute information; for example, when `Name` is `Age`, `Value` will be `18` </ul>|
| Score    | Integer  | Score. Value range: 0–100 |
| Location | [Location](#location) | Detection frame coordinates |

#### Location

Coordinates.

| Name | Type | Description |
| -------- | -------- | ---------------- |
| X        | Float    | Horizontal coordinate of the top-left corner     |
| Y        | Float    | Vertical coordinate of the top-left corner     |
| Width    | Float    | Width             |
| Height   | Float    | Height             |
| Rotate   | Float    | Rotation angle of the detection frame |

#### OcrResult

Detailed OCR result.

| Name | Type | Description |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String                                   | Indicates  the recognition scenario. Default value: OCR (image OCR).              |
| Suggestion | String                                       | Returns the operation suggestion for the maliciousness label with the highest priority. When you get the determination result, the returned value indicates the action suggested by the system. We recommend you handle different types of violations and suggestions according to your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| Label      | String                                 | Returns the maliciousness label with the highest priority in the OCR detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Returned value: <ul style="margin:0"><li/>Normal: normal<li/>Porn: pornographic<li/>Abuse: abusive<li/>Ad: advertising<li/>Custom: other offensive, unsafe, or inappropriate types of content</ul> |
| SubLabel   | String | Sub-label name |
| Score    | Integer  | Sub-label hit score of the scenario model. Value range: 0–100 |
| Text       | String | Text content |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR result details |


#### OcrTextDetail
OCR text result details.

| Name | Type | Description |
| -------- | --------------- | --------------- |
| Text | String | Returns the text content recognized by OCR (up to **5,000 bytes**) |
| Label  | String | Returns the maliciousness label in the detection result. Returned values: <ul style="margin:0"><li/>Normal: normal<li/>Porn: pornographic<li/>Abuse: abusive<li/>Ad: advertising<li/>Custom: other offensive, unsafe, or inappropriate types of content</ul> |
| Keywords | Array of String | Keywords hit under the label |
| Score    | Integer  | Hit score of the label model. Value range: 0–100 |
| Location | [Location](#location) | OCR text coordinates |


#### LibResult
Blocklist/Allowlist result details.

| Name | Type | Description |
| ---------- | ------------------ | ------------------------------------------------------------ |
| Scene      | String                           | Scenario recognition result of the model. Default value: Similar                 |
| Suggestion | String                                       | Returns the operation suggestion. When you get the determination result, the returned value indicates the action suggested by the system. We recommend you handle different types of violations and suggestions according to your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| Label  | String | Returns the maliciousness label in the detection result. Returned values: <ul style="margin:0"><li/>Normal: normal<li/>Porn: pornographic<li/>Abuse: abusive<li/>Ad: advertising<li/>Custom: other offensive, unsafe, or inappropriate types of content</ul> |
| SubLabel   | String | Sub-label name |
| Score | Integer | Recognition score of the image search model. Value range: 0–100 |
| Details    | Array of [LibDetail](#libdetail) | Blocklist/Allowlist result details |

#### LibDetail
Custom list/blocklist/allowlist details.

| Name | Type | Description |
| -------- | -------- | ------------------------------------------------------------ |
| Id       | Integer  | ID                                                         |
| ImageId  | String   | Image ID                                                       |
| Label  | String | Returns the maliciousness label in the detection result. Returned values: <ul style="margin:0"><li/>Normal: normal<li/>Porn: pornographic<li/>Abuse: abusive<li/>Ad: advertising<li/>Custom: other offensive, unsafe, or inappropriate types of content</ul> |
| Tag | String | Custom label |
| Score | Integer | Model recognition score. Value range: 0–100 |



### Sample callback message
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "hotScore": 0,
        "pornScore": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "illegalScore": 0,
        "polityScore": 0,
        "similarScore": 0,
        "terrorScore": 0,
        "abuseScore": 0,
        "teenagerScore": 0,
        "adScore": 0,
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







