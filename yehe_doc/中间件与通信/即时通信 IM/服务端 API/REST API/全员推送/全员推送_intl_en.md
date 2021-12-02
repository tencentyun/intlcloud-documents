## Feature Description
- This API can be used to push messages to all users.
- This API can be used to push messages by user attribute.
- This API can be used to push messages by user tag.
- When the admin pushes messages, the message sender displayed to the recipients is the admin.
- When the admin specifies an account to push messages to other accounts, the sender displayed to the recipients is not the admin but the account specified by the admin.
- This API supports offline storage of messages, but not message roaming.
- It takes time to push messages to all users. The required time depends on the number of accounts. Typically, it is within 1 minute.

## API Calling Description
**Only users with Flagship Edition accounts can apply for this feature. You can submit a ticket to apply for this feature. If we determine that this feature suits your needs, we will approve your application. After your application is approved, the feature will be enabled 48 hours later.**

### Sample request URL
```
https://xxxxxx/v4/all_member_push/im_push?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json
```


### Request parameters

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/all_member_push/im_push | Request API |
| usersig | Signature generated in the app admin account. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| identifier | The value must be the app admin account. |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| random | A random 32-bit unsigned integer |
| contenttype | The value is always `json`. |

### Calling frequency
This API supports push to all users, push by attribute, and push by tag. By default, it can be called up to 100 times per day, and the interval between two pushes must be greater than 1s. If you have special requirements, such as raising the frequency limit, describe your requirements in the ticket.

### Sample requests
- **Pushing messages to all users**
The admin pushes messages to all users.
```
{
	"From_Account": "admin",
    "MsgRandom": 56512,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```
The admin specifies an account to push messages to all users. (In this example, the sender account is `xiaoming`.)
```
{
	"From_Account": "xiaoming",
    "MsgRandom": 3674128,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```
The admin specifies an account to push messages to all users and sets the offline push information.
```
{
	"From_Account": "xiaoming",
    "MsgRandom": 3674128,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ],
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Desc": "Content to push offline",
        "Ext": "Passthrough content",
        "AndroidInfo": {
            "Sound": "android.mp3"
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1, // If this field is left as default or is set to `0`, the message is counted. If this field is set to `1`, the message is not counted, that is, the icon number in the upper-right corner does not increase.
            "Title":"apns title", // APNs title
            "SubTitle":"apns subtitle", // APNs subtitle
            "Image":"www.image.com" // Image URL
        }
    }
}
```
The admin pushes messages to all users and retains the messages offline for 120s.
```
{
	"From_Account": "admin",
    "MsgRandom": 21302570,
    "MsgLifeTime": 120,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```
- **Pushing messages by user tag**
The admin pushes messages to users tagged with "A shares" and "B shares".
```
{
	"From_Account": "admin",
	"MsgRandom": 214,
	"Condition": {
		"TagsAnd": ["A shares","B shares"]
	},
	"MsgBody": [
		{
			"MsgType": "TIMTextElem",
			"MsgContent": {
				"Text": "hi, beauty"
			}
		}
	]
}
```
The admin pushes messages to users tagged with "A shares" or "B shares".
```
{
	"From_Account": "admin",
	"MsgRandom": 103698523,
	"Condition": {
		"TagsOr": ["A shares","B shares"]
	},
	"MsgBody": [
		{
			"MsgType": "TIMTextElem",
			"MsgContent": {
				"Text": "hi, beauty"
			}
		}
	]
}
```
The admin pushes messages to users tagged with "A shares" and "B shares" and retains the messages offline for 120s.
```
{
	"From_Account": "admin",
	"MsgRandom": 124032,
	"MsgLifeTime": 120,
	"Condition": {
		"TagsOr": ["A shares","B shares"]
	},
	"MsgBody": [
		{
			"MsgType": "TIMTextElem",
			"MsgContent": {
				"Text": "hi, beauty"
			}
		}
	]
}
```
- **Pushing messages by user attribute**
The admin pushes messages to Shenzhen Platinum Premier users.
```
{
	"From_Account": "admin",
    "MsgRandom": 389475,
    "Condition": {
        "AttrsAnd": {
            "Membership Level": "Platinum Premier members",
            "city": "Shenzhen"
        }
    },
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```
The admin pushes messages to users in Shenzhen or male users.
```
{
	"From_Account": "admin",
    "MsgRandom": 9657,
    "Condition": {
        "AttrsOr": {
            "sex": "M",
            "city": "Shenzhen"
        }
    },
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```
The admin pushes messages to Shenzhen Platinum Premier users and retains the messages offline for 120s.
```
{
	"From_Account": "admin",
    "MsgRandom": 9312457,
	"MsgLifeTime": 120,
    "Condition": {
        "AttrsAnd": {
            "Membership Level": "Platinum Premier users",
            "city": "Shenzhen"
        }
    },
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```


### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---|
| Condition | Object | No | Valid values:<ul style="margin:0;"><li >AttrsOr<li >AttrsAnd<li >TagsOr<li>TagsAnd</ul>`AttrsOr` and `AttrsAnd` can coexist, and `TagsOr` and `TagsAnd` can coexist. However, tag conditions and attribute conditions cannot coexist. If no condition is specified, messages are pushed to all users. |
| MsgRandom | Integer | Yes | Random number of the message, which is generated by the random function and used to deduplicate push tasks. Push requests must have unique random numbers within a seven-day period. Otherwise, they are regarded as the same push task. If an error is returned when you call the push API, you can use the same message random number for a retry. |
| MsgBody | Array | Yes | Message body. For more information on the message format, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). Note that `MsgBody` is an array that can contain multiple message elements. |
| MsgType | String | Yes | TIM message object type. Valid values: <ul style="margin:0;"><li >`TIMTextElem` (text message) <li >`TIMLocationElem` (location message) <li >`TIMFaceElem` (emoji message) <li >`TIMCustomElem` (custom message) <li >`TIMSoundElem` (voice message) <li >`TIMImageElem` (image message) <li >`TIMFileElem` (file message) <li >`TIMVideoFileElem` (video message) |
| MsgContent | Object | Yes | Different message object types (`MsgType`) have different formats (`MsgContent`). For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| MsgLifeTime | Integer | No | Offline message storage duration, in seconds. The maximum duration is 604800 seconds (7 days). The default value is 0, which indicates that messages are not stored offline. |
| From_Account | String | No | Account of the message sender |
| AttrsOr | Object | No | A set of attribute conditions connected by OR. Note that attribute conditions and tag conditions cannot be used at the same time. |
| AttrsAnd | Object | No | A set of attribute conditions connected by AND. Note that attribute conditions and tag conditions cannot be used at the same time. |
| TagsOr | Object | No | A set of tag conditions connected by OR. A tag is a string of no more than 50 bytes. Note that attribute conditions and tag conditions cannot be used at the same time. The number of tags in `TagsOr` cannot exceed 10. |
| TagsAnd | Object | No | A set of tag conditions connected by AND. A tag is a string of no more than 50 bytes. Note that attribute conditions and tag conditions cannot be used at the same time. The number of tags in `TagsAnd` cannot exceed 10. |
| OfflinePushInfo | Object | No | The information to be pushed offline. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response

```
{
    "ActionStatus":"OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "TaskId": "1400123456_144115212910570789_4155518400_15723514"
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code |
| ErrorInfo | String | Error information |
| TaskId | String | Push task ID |

## Error Codes
Unless a network error (such as error 502) occurs, the HTTP return code for this API is always 200. **`ErrorCode` and `ErrorInfo` in the response represent the actual error code and error information.** For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
|---------|---------|
| 90001 | Failed to parse the JSON format. Check whether the JSON request meets JSON specifications. |
| 90002 | The `MsgBody` field in the JSON request does not meet message format requirements or it is not an array. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90005 | The `MsgRandom` field is missing in the JSON request or it is not an integer. |
| 90007 | The `MsgBody` field in the JSON request is not an array. Change it to an array. |
| 90009 | The request requires app admin permissions. |
| 90010 | The JSON request does not meet message format requirements. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90020 | The tag length exceeds the limit (the maximum length allowed is 50 bytes). |
| 90022 | `TagsOr` and `TagsAnd` in the push conditions contain repeated tags. |
| 90024 | Pushes are too frequent. The interval between two pushes must be greater than 1s. |
| 90026 | Incorrect offline message storage period. The value cannot exceed 7 days. |
| 90032 | The number of tags in the push conditions exceeds 10, or the number of tags in the tag adding request exceeds 10. |
| 90033 | Invalid attribute. |
| 90039 | Message push by attribute and message push by tag are mutually exclusive. |
| 90040 | A tag in the push conditions is null. |
| 90045 | The feature of pushing to all users is not enabled. |
| 90047 | The number of pushes exceeds the daily quota (default quota: 100). |
| 91000 | Internal service error. Try again. |

## Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/all_member_push/im_push) to debug this API.

References
- [API for Pushing to All Users](https://intl.cloud.tencent.com/document/product/1047/37165) 
- [Setting Application Attribute Names](https://intl.cloud.tencent.com/document/product/1047/37167) 
- [Getting Application Attribute Names](https://intl.cloud.tencent.com/document/product/1047/37168) 
- [Setting User Attributes](https://intl.cloud.tencent.com/document/product/1047/37170)  
- [Deleting User Attributes](https://intl.cloud.tencent.com/document/product/1047/37171)  
- [Getting User Attributes](https://intl.cloud.tencent.com/document/product/1047/37169)  
- [Adding User Tags](https://intl.cloud.tencent.com/document/product/1047/37173)  
- [Getting User Tags](https://intl.cloud.tencent.com/document/product/1047/37172)  
- [Deleting User Tags](https://intl.cloud.tencent.com/document/product/1047/37174)  
- [Deleting All Tags of a User](https://intl.cloud.tencent.com/document/product/1047/37175)  
