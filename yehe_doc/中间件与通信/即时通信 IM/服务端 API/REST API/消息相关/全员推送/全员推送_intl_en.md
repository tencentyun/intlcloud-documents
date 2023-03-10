Pushing to all users is an excellent tool for application user operations. It not only supports sending specific content to all users, but also can send personalized content to specific user groups based on tags and attributes, such as member events, and regional notifications. This helps effectively attract, convert, and activate new users.
## Feature Overview
- This API can be used to push messages to all users.
- This API can be used to push messages by user attribute.
- This API can be used to push messages by user tag.
- When the admin pushes messages, the message sender displayed to the recipients is the admin.
- When the admin specifies an account to push messages to other accounts, the sender displayed to the recipients is not the admin but the account specified by the admin.
- This API supports offline storage of messages, but not message roaming.
- It takes time to push messages to all users. The required time depends on the number of accounts. Typically, it is within one minute.
- This API allows you to push messages only to online users by setting the `MsgLifeTime` parameter to `0`.
>?The "pushing to all users" feature is only available on the IM Ultimate edition. To use it, [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

## API Call Description
The feature of pushing to all users is available only to users with Ultimate edition accounts. See [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322) to apply for this feature. The feature will be enabled **48 hours** after your application is approved.

### Sample request URL
```
https://xxxxxx/v4/all_member_push/im_push?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json
```
### Request parameters

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>Chinese mainland: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com`<li>Silicon Valley: `adminapiusa.im.qcloud.com` |
| v4/all_member_push/im_push | Request API |
| usersig | Signature generated in the app admin account. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| identifier | The app administration account. |
| sdkappid | The `SDKAppID` assigned by the IM console when an app is created |
| random | A random 32-bit unsigned integer |
| contenttype | The value is always `json`. |

### Calling frequency
This API includes pushing to all and by attribute and tag. By default, it can be called 100 times every day. The interval between two pushes must be greater than one second.

### Sample request
- **Pushing messages to all users**
The admin pushes messages to all users and retains the messages offline for 120 seconds.
```
{
	"From_Account": "admin",
    "MsgRandom": 56512,
    "MsgLifeTime": 120,
    "MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
                "Text": "hi, beauty"
            }
        }
    ]
}
```
The admin specifies an account for pushing to all users and retains the messages offline for 120 seconds. In the sample, the sender account is `xiaoming`:
```
{
	"From_Account": "xiaoming",
    "MsgRandom": 3674128,
    "MsgLifeTime": 120,
    "MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
                "Text": "hi, beauty"
            }
        }
    ]
}
```
The admin specifies an account for pushing to all users, sets offline push information, and retains the messages offline for 120 seconds.
```
{
	"From_Account": "xiaoming",
    "MsgRandom": 3674128,
    "MsgLifeTime": 120,
    "MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
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
            "BadgeMode": 1, // If this field is left as default or is set to `0`, the message is counted. If this field is set to `1`, the message is not counted, that is, the badge counter in the upper-right corner does not increase.
            "Title":"apns title", // APNs title
            "SubTitle":"apns subtitle", // APNs subtitle
            "Image":"www.image.com" // Image URL
        }
    }
}
```
The admin pushes messages to all users and retains the messages offline for 120 seconds.
```
{
	"From_Account": "admin",
    "MsgRandom": 21302570,
    "MsgLifeTime": 120,
    "MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
                "Text": "hi, beauty"
            }
        }
    ]
}
```
- **Pushing messages by user tag**
The admin pushes messages to users tagged with "Stock A" and "Stock B" and retains the messages offline for 120 seconds.
```
{
	"From_Account": "admin",
	"MsgRandom": 214,
    "MsgLifeTime": 120,
	"Condition":{
		"TagsAnd": ["Stock A","Stock B"]
	},
	"MsgBody":[
		{
			"MsgType": "TIMTextElem",
			"MsgContent":{
				"Text": "hi, beauty"
			}
		}
	]
}
```
The admin pushes messages to users tagged with "Stock A" and "Stock B" and retains the messages offline for 120 seconds.
```
{
	"From_Account": "admin",
	"MsgRandom": 124032,
	"MsgLifeTime": 120,
	"Condition":{
		"TagsOr": ["Stock A","Stock B"]
	},
	"MsgBody":[
		{
			"MsgType": "TIMTextElem",
			"MsgContent":{
				"Text": "hi, beauty"
			}
		}
	]
}
```
- **Pushing messages by user attribute**
The admin pushes messages to Shenzhen Platinum Premier users and retains the messages offline for 120 seconds.
```
{
	"From_Account": "admin",
    "MsgRandom": 389475,
    "MsgLifeTime": 120,
    "Condition":{
        "AttrsAnd": {
            "Membership Level": "Platinum Premier members",
            "city": "Shenzhen"
        }
    },
    "MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
                "Text": "hi, beauty"
            }
        }
    ]
}
```
The admin pushes messages to Shenzhen Platinum Premier users and retains the messages offline for 120 seconds.
```
{
	"From_Account": "admin",
    "MsgRandom": 9312457,
	"MsgLifeTime": 120,
    "Condition":{
        "AttrsAnd": {
            "Membership Level": "Platinum Premier users",
            "city": "Shenzhen"
        }
    },
    "MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
                "Text": "hi, beauty"
            }
        }
    ]
}
```


### Request fields

| Field | Type | Attribute | Description |
|---------|---------|---------|---|
| Condition | Object | Optional | Valid values:<ul style="margin:0;"><li >AttrsOr<li >AttrsAnd<li >TagsOr<li>TagsAnd</ul>`AttrsOr` and `AttrsAnd` can coexist, and `TagsOr` and `TagsAnd` can coexist. However, tag conditions and attribute conditions cannot coexist. If no condition is specified, messages are pushed to all users. |
| MsgRandom | Integer | Required | Random number (32-bit unsigned integer) of the message. It is used by the backend for message deduplication within a second. Make sure a random number is entered. |
| MsgBody | Array | Required | Message body. For more information on the message format, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). Note that `MsgBody` is an array that can contain multiple message elements. |
| MsgType | String | Required | TIM message object type. Valid values: <ul style="margin:0;"><li >`TIMTextElem` (text message) <li >`TIMLocationElem` (location message) <li >`TIMFaceElem` (emoji message) <li >`TIMCustomElem` (custom message) <li >`TIMSoundElem` (voice message) <li >`TIMImageElem` (image message) <li >`TIMFileElem` (file message) <li >`TIMVideoFileElem` (video message) |
| MsgContent | Object | Required | Different message object types (`MsgType`) have different formats (`MsgContent`). For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| MsgLifeTime | Integer | Optional | Offline message storage duration, in seconds. The maximum duration is 604,800 seconds (7 days). The default value is 0, which indicates that messages are not stored offline and will be pushed only to online users. |
| From_Account | String | Optional | Account of the message sender |
| AttrsOr | Object | Optional | A set of attribute conditions connected by OR. Note that attribute conditions and tag conditions cannot be used at the same time. |
| AttrsAnd | Object | Optional | A set of attribute conditions connected by AND. Note that attribute conditions and tag conditions cannot be used at the same time. |
| TagsOr | Array  |Optional| Union of tag conditions. A tag is a string of up to 50 bytes. Note that attribute conditions and tag conditions cannot be used at the same time. The `TagsOr` condition can contain up to ten tags. |
| TagsAnd | Array |Optional | Intersection of tag conditions. A tag is a string of up to 50 bytes. Note that attribute conditions and tag conditions cannot be used at the same time. The `TagsAnd` condition can contain up to ten tags.|
| OfflinePushInfo | Object | Optional | The information to be pushed offline. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "TaskId": "1400123456_144115212910570789_4155518400_15723514"
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: Successful; `FAIL`: Failed |
| ErrorCode | Integer | Error code |
| ErrorInfo| String | Error message |
| TaskId | String | Push task ID |

## Error Codes
Unless a network error (such as error 502) occurs, the HTTP return code for this API is always 200. **`ErrorCode` and `ErrorInfo` in the response represent the actual error code and error message.** For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
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
| 90024 | Pushes are too frequent. The interval between two pushes must be greater than 1 second. |
| 90026 | Incorrect offline message storage period. The value cannot exceed 7 days. |
| 90032 | The number of tags in the push conditions exceeds 10, or the number of tags in the tag adding request exceeds 10. |
| 90033 | Invalid attribute. |
| 90039 | Message push by attribute and message push by tag are mutually exclusive. |
| 90040 | A tag in the push conditions is null. |
| 90045 | The feature of pushing to all users is not enabled. |
| 90047 | The number of pushes exceeds the daily quota (default quota: 100). |
| 91000 | Internal service error. Try again. |

## API Debugging Tool
Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/#/v4/openim/admin_msgwithdraw?locale=en-US) to debug this API.

## References
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
