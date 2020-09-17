LVB porn detection takes real-time screenshots of suspiciously pornographic video images in live streams and stores them in COS. The porn detection callback is used to push the information of detected pornographic images, including their type, score, and screenshot time. You need to configure the server address receiving porn detection callback messages in the callback template and associate the template with the push domain name. When a porn detection event is triggered by a live stream, the Tencent Cloud LVB backend will call back the pornographic image information to the configured receiving server.

This document describes the fields in callback message notifications sent by Tencent Cloud LVB after a porn detection callback event is triggered.

## Notes
- You need to understand how to configure the callback feature and receive callback messages on Tencent Cloud LVB before reading this document. For more information, please see [How to Receive Event Notification](https://cloud.tencent.com/document/product/267/32744).
- By default, only questionable results will be called back for LVB porn detection.
- We recommend you use the `[type](#type)` of an image to judge whether it is pornographic. As the detection results are not 100% accurate and there may be false positives or false negatives, you can confirm them manually if necessary.

## Screencapturing Event Parameter Description

### Event type parameters

| Event Type | Field Value Description           |
| :------- | :------------- |
| LVB porn detection | event_type = 317 |

### Common callback parameters

<table>
<tr><th>Field Name</th><th>Type</th><th>Description</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Expiration time, which is the Unix timestamp when the event notification signature expires. <ul style="margin:0"><li>The default expiration time of a message notification from Tencent Cloud is 10 minutes. If the time specified by the `t` value in a message notification has elapsed, it can be determined that this notification is invalid, thereby preventing network replay attacks. <li>The format of `t` is a decimal Unix timestamp, i.e., the number of seconds that has elapsed since January 01, 1970 00:00 (UTC/GMT time).</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Security signature of event notification (sign = MD5(key + t)). <br>Note: Tencent Cloud splices the encryption `<a href="#key">key</a>` and `t`, calculates the `sign` value through MD5, and places it in the notification message. After your backend server receives the notification message, it can confirm whether the `sign` is correct based on the same algorithm and then determine whether the message is indeed from the Tencent Cloud backend.</td>
</tr></table>

>? `<span id="key"></span>key` is the callback key in **Feature Template** > **[Callback Configuration](https://console.cloud.tencent.com/live/config/callback)**, which is mainly used for authentication. In order to protect the security of your data, we recommend you enter it.
>![](https://main.qcloudimg.com/raw/34b21b2d50d2aca00dd2dfa19816e8e3.png)

### Callback message parameters

| **Parameter**       | **Required** | **Data Type** | **Description**                                                     |
| :------------- | :----------- | :----------- | :----------------------------------------------------------- |
| tid            | No         | Number       | Alert policy ID. Video content alert: 20001                             |
| streamId       | No         | String       | Stream name                                                       |
| channelId      | No         | string       | Channel ID                                                      |
| img            | Yes         | string       | Link to alerted image                                                 |
| <span id="type"></span> type           | Yes         | Array        | Image type, 0: normal, 1: pornographic, 2: sexy, 3: politically sensitive, 4: illegal, 5: terrorism, 6–9: others |
| confidence     | Yes         | Number       | Confidence level of the detected pornographic image ranges from 0 to 100, which is an overall score factoring in `normalScore`, `hotScore`, and `pornScore` |
| normalScore    | Yes         | Number       | Score for normal image                                         |
| hotScore    | Yes         | Number       | Score for sexy image                                         |
| pornScore    | Yes         | Number       | Score for pornographic image                                         |
| level          | No         | Number       | Image level                                                   |
| ocrMsg         | No         | string       | OCR recognition information of image (if any)                              |
| screenshotTime | Yes         | Number       | Screenshot time                                                     |
| sendTime       | Yes         | Number       | Request sent time (UNIX timestamp)                                    |
| abductionRisk  | No         | Array        | An array containing the [AbductionRisk](#abductionrisk) structure                            |
| faceDetails    | No         | Array        | An array containing the face attribute ([faceDetail](#facedetail)) structure                     |
| [gameDetails](#gamedetails)    | No         | Object       | Game details                                                 |
| polityScore    | No         | Number       | Score for image involving politically sensitive information                                         |
| illegalScore   | No         | Number       | Score for image involving illegal information                                         |
| terrorScore    | No         | Number       | Score for image involving terrorism information                                         |
| similarScore   | No         | Number       | Score for image similarity                                               |
| stream_param   | No         | String       | Push parameter                                                     |
| app            | No         | String       | Push domain name                                                     |
| appid          | No         | Number       | APPID                                                      |
| appname        | No         | String       | Push path                                               |

#### AbductionRisk

| **Parameter** | **Required ** | **Data Type** | **Description** |
| :------- | :----------- | :----------- | :----------------------------------------------------------- |
| level    | Yes         | Number       | Risk level ranges from 0 to 4. The larger the number, the greater the risk. 3 and 4 indicate maliciousness and we recommend you deal with such images |
| type     | Yes         | Number       | Risk type. 20002: porn                                        |

#### faceDetail

| **Parameter Name* | **Required ** | **Type** | **Description** |
| :----------- | :----------- | :------- | :---------------------------------------- |
| gender       | No         | Number   | Gender [0 (female)–100 (male)]              |
| age          | No         | Number   | Age                                      |
| expression   | No         | Number   | Expression [0 (normal)–50 (smile)–100 (laugh)] |
| beauty       | No         | Number   | Attractiveness [0–100]                            |
| x            | No         | Number   | x coordinate of the top-left corner of face frame                            |
| y            | No         | Number   | y coordinate of the top-left corner of face frame                            |
| width        | No         | Number   | Face frame width                                |
| height       | No         | Number   | Face frame height                                |

#### gameDetails

| **Parameter Name* | **Required ** | **Type** | **Description** |
| :------------ | :----------- | :------- | :----------- |
| battlegrounds | No         | Object   | PUBG information |
| [gameList](#gamelist)      | No         | Array    | Game list     |

#### gameList

| **Parameter Name* | **Required ** | **Type** | **Description** |
| :----------- | :----------- | :------- | :------- |
| name         | No         | String   | Game name |
| confidence   | No         | Number   | Probability     |

### Sample callback message

HTTP Body:

```
{
    "event_type":317,
	
    "ocrMsg":"",

    "type":[2],

    "confidence":0,

    "normalScore":2,

    "hotScore":97,

    "pornScore":0,

    "screenshotTime":1575513174,

    "level":0,

    "img":"http://test-10000.cos.ap-shanghai.myqcloud.com/2019-12-05/teststream-screenshot-10-32-54-960x540.jpg",

    "abductionRisk":[ ],

    "faceDetails":[ ],

    "sendTime":1575513176,

    "illegalScore":0,

    "polityScore":0,

    "similarScore":0,

    "terrorScore":0,

    "tid":20001,

    "streamId":"teststream",

    "channelId":"teststream",

    "stream_param":"txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",

    "app":"testlive.myqcloud.com",

    "appname":"live",

    "appid":10000
}  
```




