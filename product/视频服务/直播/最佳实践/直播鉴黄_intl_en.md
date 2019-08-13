
To activate LVB porn detection, you need to activate LVB screencapturing first in the [LVB Console](https://cloud.tencent.com/document/product/267/20386) or through the LVB screencapturing and porn detection API. This document mainly describes how to implement LVB porn detection through the API.

## Activating LVB Porn Detection
As the LVB porn detection feature is based on LVB screencapturing, you have to activate LVB screencapturing first before you can activate LVB porn detection in the following steps:

#### 1. Create a porn detection-enabled LVB screencapturing template
Call CreateLiveSnapshotTemplate to create a porn detection-enabled LVB screencapturing template by setting PornFlag to 1.

#### 2. Create a porn detection-enabled LVB screencapturing rule
Call CreateLiveSnapshotRule to create a porn detection-enabled LVB screencapturing rule and associate the LVB screencapturing template ID created in step 1 to the AppId, DomainName, AppName, and StreamName of the live stream that needs to be detected for porn.

#### 3. Start a live broadcast and start porn detection
After a porn detection-enabled LVB screencapturing rule is created, the porn detection feature will be automatically enabled for new live broadcasts. If you want to enable porn detection for a live broadcast in progress, you need to stop and then restart it.

## Getting the LVB Porn Detection Result
After LVB porn detection is enabled, you can configure the registered callback domain name in the porn detection callback template to have the LVB backend call back the porn detection result.

>! By default, only suspicious results but not normal ones will be called back.

The steps are as follows:
#### 1. Create an LVB porn detection callback template
Call CreateLiveCallbackTemplate to set the PornCensorshipNotifyUrl parameter to your domain name and create an LVB porn detection callback template.

#### 2. Create an LVB porn detection callback rule

Call CreateLiveCallbackRule to create a porn detection-enabled LVB screencapturing rule and associate the LVB screencapturing template ID created in last step to the AppId, DomainName, AppName, and StreamName of the live stream that needs porn detection callback.

#### 3. Get the porn detection result

The LVB backend sends the porn detection result to your registered domain name through an HTTP POST request where the result is stored in the HTTP body in JSON format. You can determine whether the live broadcast is pornographic by the confidence field alone.
>! It is recommended to use the confidence of an image to judge whether it is pornographic. If the confidence is above 83, it can be considered a suspected image. As the detection system cannot achieve 100% accuracy, there may be false positives or false negatives, and human confirmation is recommended.

The complete protocol is as follows:

| **Parameter** | **Required ** | **Data Type** | **Description** |
| --- | --- | --- | --- |
| tid | Yes | Number | Alert policy ID; video content alert: 20001 |
| streamId | No | String | Stream name |
| channelId | No | string | Channel ID |
| img | Yes | string | Link to the alerted image |
| type | Yes | Array | Image type. 1: pornographic; 2: sexy; 3-9: others |
| confidence | Yes | Number | Confidence of the detected pornographic image in the range of 0-100, which is an overall score of normalScore, hotScore, and pornScore. If the confidence is greater than 83, the image is considered a suspected image |
| normalScore | Yes | Number | Normal score of the image |
| hotScore | Yes | Number | Sexy score of the image |
| pornScore | Yes | Number | Pornographic score of the image |
| level | No | Number | Image level |
| ocrMsg | No | string | OCR information of the image (if any) |
| screenshotTime | Yes | Number | Screencaptured time |
| sendTime | Yes | Number | Request send time (UNIX timestamp) |
| abductionRisk | No | Array | An array containing the AbductionRisk structure |
| faceDetails | No | Array | An array containing the face attribute (faceDetail) structure |
| gameDetails | No | Object | Game details |

AbductionRisk description

| **Parameter** | **Required ** | **Data Type** | **Description** |
| --- | --- | --- | --- |
| level | Yes | Number | Risk level in the range of 0-4. The higher the number, the higher the risk. 3 and 4 indicate maliciousness and should be handled |
| type | Yes | Number | Risk type. 20002: porn |

faceDetail description

| **Parameter Name* | **Required ** | **Type** | **Description** |
| --- | --- | --- | --- |
| gender | No | Number | Gender [0 (female) - 100 (male)] |
| age | No | Number | Age |
| expression | No | Number | Expression [0 (normal) - 50 (smile) - 100 (laugh)] |
| beauty | No | Number | Charm [0 - 100] |
| x | No | Number | x coordinate of the top-left corner of the face frame |
| y | No | Number | y coordinate of the top-left corner of the face frame |
| width | No | Number | Face frame width |
| height | No | Number | Face frame height |

gameDetails description

| **Parameter Name* | **Required ** | **Type** | **Description** |
| --- | --- | --- | --- |
| battlegrounds | No | Object | PUBG information |
| gameList | No | Array | Game list |

gameList

| **Parameter Name* | **Required ** | **Type** | **Description** |
| --- | --- | --- | --- |
| name | No | String | Game name |
| confidence | No | Number | Probability |

In addition, the HTTP header contains the `TPD-SecretID` and `TPD-CallBack-Auth` fields which can be used for user authentication.
Signature calculation: ``Signature = base64_encode(hash_hmac('SHA1', $Body, $SecretKey, true))``, where SecretKey is the SecretKey corresponding to the SecretId.

**Below is a sample request:**
HTTP Header:
```
TPD-SecretID : SecretId

TPD-CallBack-Auth: Signature

TPD-CallBack-Version : version
```

HTTP Body:

```
{

"ocrMsg":"",

"type":[2],

"confidence":0,

"normalScore":6,

"hotScore":93,

"pornScore":0,

"screenshotTime":1534087026,

"level":0,

"img": "[http://XXXXXX-1234567890.file.myqcloud.com/2018-12-12/XTEST-screenshot-23-17-06-368x640.jpg](http://XXXXXX-1234567890.file.myqcloud.com/2018-12-12/XTEST-screenshot-23-17-06-368x640.jpg)",

"abductionRisk":[],

"faceDetails":[],

"sendTime":1534087026,

"tid":20001,

"streamId":"TEST_169787468",

"channelId":"TEST_169787468"

}
```

## Disabling LVB Porn Detection

LVB porn detection can be disabled by deleting or modifying the screencapturing rule or template. Both deletion and modification are effective only for new live broadcasts. If you want to disable LVB porn detection for a live broadcast that has already started, you have to stop and then restart it.

#### 1. Delete or modify the porn detection-enabled screencapturing rule

 - Call DeleteLiveSnapshotRule to delete the corresponding LVB screencapturing rule under DomainName, AppName, and StreamName by template ID.
 - Call ModifyLiveSnapshotRule to change the corresponding LVB screencapturing template ID under AppName and StreamName to the ID of an LVB screencapturing template with porn detection disabled.

#### 2. Delete or modify the porn detection-enabled screencapturing template

Call ModifyLiveSnapshotTemplate to set the porn detection flag of the LVB screencapturing template to 0.
