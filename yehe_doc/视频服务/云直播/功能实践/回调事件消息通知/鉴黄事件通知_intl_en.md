Live porn detection takes real-time screenshots of suspiciously porn video images in live streams and stores them in COS. The porn detection callback is used to push the information of detected porn images, including their types, scores, and screenshot time points. You need to configure the server address for receiving porn detection callback messages in the callback template and bind the template to the push domain name. When a porn detection event is triggered by a live stream, the Tencent Cloud CSS backend will call back the porn image information to the configured receiving server.

This document describes the parameters in callback message notifications sent by Tencent Cloud CSS after a porn detection callback event is triggered.

## Notes
- You need to understand how to configure callbacks and how you will receive messages via Tencent Cloud CSS before reading this document. For more information, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080).
- By default, only questionable results of porn detection will be called back.
- We recommend you use the `label` of an image to determine whether it is pornographic. As the detection results are not 100% accurate and there may be false positives or false negatives, you can confirm them manually if necessary.

## Screencapturing Event Parameters
### Event type parameters

| Event Type | Parameter Value           |
| :------- | :------------- |
| Live porn detection | event_type = 317 |


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
| Parameter       | Required | Data Type | Description    |
| ---------- | ---------- | ---------- | --------------------------- |
| streamId       | No         | String       | Stream name    |
| channelId | No | String | Channel ID |
| img | Yes | String | URL to the alerted image |
| type | Yes | Array | Returns the maliciousness label with the highest priority in the detection result (labelResults), which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. The returned values are numbers as follows: <ul style="margin:0"><li/>0: normal<li/>1–8: indicates different types in order from `hotScore` to `adScore`; for example, 1: pornographic, 6: abusive; 8: advertising, and so on</ul> |
| score | required | Array | The score of `type` |
| hotScore    | Yes         | Number       | The confidence score of the “sexy” label                                       |
| pornScore    | Yes         | Number       | The confidence score of the “porn” label                                         |
| illegalScore   |  Yes         | Number       | The confidence score of the “illegal” label    |
| polityScore    |  Yes         | Number       | The confidence score of the “politically sensitive” label                                |
| terrorScore    |  Yes        | Number       |  The confidence score of the “terrorism information” label |
| abuseScore |  Yes     | Number | The confidence score of the “abusive” label |
| teenagerScore | Yes     | Number | The confidence score of the “inappropriate for teenagers” label  |
| adScore | Yes     | Number | The confidence score of the “advertisement” label |
| ocrMsg         | No         | String       | OCR text (if applicable)                         |
| suggestion | Yes     | string | Recommended result. Valid values: <ul style="margin:0"><li/>`Block`: to block<li/>`Review`: to review again<li/>`Pass`: to pass</ul>     |
| label | Yes | String | Supplementary text description of the returned value of the parameter `type`, such as `Normal` for the returned value **0**, `Abuse` for **6**, and `Ad` for **8**. |
| subLabel | Yes     | string | Sub-label name. An empty string will be returned when no sub-label is matched.       |
| labelResults | No     | Array of [LabelResult](#labelresult)  | The results of recognition by the categorization model, such as porn, sexy, terrorism, rule violations, etc. |
| objectResults | No     | Array of [ObjectResult](#objectresult) | The results of recognition by the object detection model, such as political entities, advertisements and logos, QR code, etc. |
| ocrResults | No    | Array of [OcrResult](#ocrresult) | The OCR-based text moderation results, including the OCR text information and moderation details |
| libResults | No     | Array of [LibResult](#libresult) | The results of recognition by the inappropriate image library |
| screenshotTime | Yes         | Number       | Screenshot time              |
| sendTime       | Yes         | Number       | The time the request was sent in Unix timestamp format  |
| similarScore   | No   | Number  | Image similarity score   |
| stream_param   | No         | String       | Push parameter                              |
| app   | No | String | Push domain name   |
| appid  | No | Number |  Application ID |
| appname        | No        | String       | Push path  |

 

#### LabelResult
The result of recognition by the classification model

| Name | Type | Description |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String            | The scenario recognized by the model, such as advertisement, porn, and harmful contents, etc.     |
| Suggestion | String                                       | Returns the operation suggestion for the current maliciousness label. When you get the determination result, the returned value indicates the action suggested by the system. We recommend you handle different types of violations and suggestions according to your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| label | String | Supplementary text description of the returned value of the callback message parameter `type`, such as `Normal` for the returned value **0**, `Abuse` for **6**, and `Ad` for **8**. |
| SubLabel   | String | Sub-label name                                                   |
| Score      | Integer | The confidence score of the label                                         |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | Details of the sub-labels determined by the categorization model                                 |

#### LabelDetailItem

The sub-label determined by the categorization model

| Name | Type | Description |
| -------- | -------- | --------------------------- |
| Id       | Integer  | Serial number  |
| name | String | Sub-label name |
| Score    | Integer  | Sub-label confidence score. Value range: 0-100 |


#### ObjectResult

Detailed results of object detection

| Name | Type | Description |
| ---------- | --------------------- | --------------------- |
| Scene      | String                                 | The object detection result, such as QR code, logo, and image OCR, etc. |
| Suggestion | String                                       | Returns the operation suggestion for the current maliciousness label. When you get the determination result, the returned value indicates the action suggested by the system. We recommend you handle different types of violations and suggestions according to your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| label | String | Supplementary text description of the returned value of the callback message parameter `type`, such as `Normal` for the returned value **0**, `Abuse` for **6**, and `Ad` for **8**. |
| SubLabel   | String | Sub-label name |
| Score      | Integer | The confidence score of the sub-label for its scenario. Value range: 0-100 |
| DealNames | Array of String | Object list |
| Details    | Array of [ObjectDetail](#objectdetail) | Details of the object detection results |

#### ObjectDetail

Details of the object detection result. If the objects to be detected are political figures, advertisements and logos, QR codes or human faces, the details will contain names, values, and confidence scores for the labels of the model’s detection box, as well as the location of the detection box.

| Name | Type | Description |
| -------- | -------- | -------- |
| Id       | Integer  | Serial number  |
| Name | String | Label name |
| Value    | String   | Label value. <ul style="margin:0"><li/>When the scenario is `Ad`, `Value` will be a URL. For example, `Name` is `QrCode`, and `Value` is `http//abc.com/aaa`.<br><li/> When the scenario is `FaceAttribute`, `Value` will be a human face attribute value. For example, `Name` is `Age`, and `Value` is `18`. </ul>|
| Score    | Integer  |Confidence score. Value range: 0-100 |
| Location | [Location](#location) | Location of the detection box |

#### Location

Coordinates and other information of the detection box

| Name | Type | Description |
| -------- | -------- | ---------------- |
| X        | Float    | X-coordinate of the detection box’s upper left corner  |
| Y        | Float    | Y-coordinate of the detection box’s upper left corner     |
| Width    | Float    | Width of the detection box            |
| Height   | Float    | Height of the detection box            |
| Rotate   | Float    | Rotation angle of the detection box |

#### OcrResult

Details of the OCR detection result

| Name | Type | Description |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String                                   | Recognition scenario. Default value: `OCR` (OCR-based image recognition)  |
| Suggestion | String                                       | Returns the operation suggestion for the maliciousness label with the highest priority. When you get the determination result, the returned value indicates the action suggested by the system. We recommend you handle different types of violations and suggestions according to your business needs. Returned values:<ul style="margin:0"><li/>Block<li/>Review<li/>Pass</ul> |
| label | String | Supplementary text description of the returned value of the callback message parameter `type`, such as `Normal` for the returned value **0**, `Abuse` for **6**, and `Ad` for **8**. |
| SubLabel   | String | Sub-label name |
| Score      | Integer | The confidence score of the sub-label for its scenario. Value range: 0-100 |
| Text       | String | The text content |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | Details of the OCR result |


#### OcrTextDetail
OCR text details

| Name | Type | Description |
| -------- | --------------- | --------------- |
| Text     | String                | Recognized OCR text (containing up to **5000 bytes**) |
| label | String | Supplementary text description of the returned value of the callback message parameter `type`, such as `Normal` for the returned value **0**, `Abuse` for **6**, and `Ad` for **8**. |
| Keywords | Array of String | No | Matched keywords under this label |
| Score      | Integer | The confidence score of the returned label. Value range: 0-100                                 |
| Location | [Location](#location) | Coordinates of the OCR text |


#### LibResult
Detailed results of recognition by the inappropriate image library

| Name | Type | Description |
| ---------- | ------------------ | ------------------------------------------------------------ |
| Scene      | String                           | The result returned by the scenario recognition model. Default value: `Similar` (similar to the scenario in the library).            |
| Suggestion | String                                       | Recommended operation. You’re advised to deal with the issues with reference to the values of `Label` and `Suggestion`. Returned values: <ul style="margin:0"><li/>`Block`: to block<li/>`Review`: to review again manually <li/>`Pass`: to pass</ul> |
| label | String | Supplementary text description of the returned value of the callback message parameter `type`, such as `Normal` for the returned value **0**, `Abuse` for **6**, and `Ad` for **8**. |
| SubLabel   | String | Sub-label name |
| Score      | Integer            | The confidence score returned by the image retrieval model. Value range: 0-100 |
| Details    | Array of [LibDetail](#libdetail) |Detailed results of recognition by the inappropriate image library |

#### LibDetail
Details of recognition by the custom library/inappropriate image library

| Name | Type | Description |
| -------- | -------- | ------------------------------------------------------------ |
| Id       | Integer  | Serial number                          |
| ImageId  | String   | Image ID                                                       |
| label | String | Supplementary text description of the returned value of the callback message parameter `type`, such as `Normal` for the returned value **0**, `Abuse` for **6**, and `Ad` for **8**. |
| Tag      | String   | Custom label                           |
| Score    | Integer  | The confidence score of model recognition. Value range: 0-100    |



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







