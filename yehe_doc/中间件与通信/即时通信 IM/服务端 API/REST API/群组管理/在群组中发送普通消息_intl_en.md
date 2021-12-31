## Feature Description
 This API is used by the app admin to send ordinary messages in a group.

## API Calling Description
### Applicable group types

| Group Type ID | RESTful API Support |
|-----------|------------|
| Private | Yes. Same as Work (work group) in the new version. |
| Public | Yes |
| ChatRoom | Yes. Same as Meeting (temporary meeting group) in the new version. |
| AVChatRoom | Yes |
|Community| Yes |

These are the preset group types in IM. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/send_group_msg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/send_group_msg | Request API |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

200 calls per second

### Sample requests

- **Basic format**
The app admin sends ordinary group messages, and the sender is the app admin.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
    "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMFaceElem", // Emoji
            "MsgContent": {
                "Index": 6,
                "Data": "abc\u0000\u0001"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data",
    "OfflinePushInfo": {
        "PushFlag": 0, // Normal push
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
- **Specifying the message sender**
The app admin can specify a group member as the message sender in `From_Account`.
After receiving the message, other members will see that the message is sent from the group member specified by the app admin.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "From_Account": "leckie", // Message sender (optional)
    "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
    "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMFaceElem", // Emoji
            "MsgContent": {
                "Index": 6,
                "Data": "abc\u0000\u0001"
            }
        }
    ]
}
```

- **Specifying that messages do not trigger conversation update**
If the value of `SendMsgControl` includes `NoLastMsg`, the message does not trigger conversation update; if it includes `NoUnread`, the message is not included in the unread count. The setting takes effect only for the current message. The parameter is not available for AVChatRoom.
```
{
     "GroupId": "@TGS#2C5SZEAEF",
     "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
     "SendMsgControl":["NoLastMsg"],// Do not trigger conversation update.
     "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
         {
             "MsgType": "TIMTextElem", // Text
             "MsgContent": {
                 "Text": "red packet"
             }
         },
         {
             "MsgType": "TIMFaceElem", // Emoji
             "MsgContent": {
                 "Index": 6,
                 "Data": "abc\u0000\u0001"
             }
         }
     ]
 }
```

- **Specifying the message priority**
You can specify the message priority. The default priority is `Normal`.
There are three priority options in descending order: `High`, `Normal`, and `Low`. They are case-sensitive.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
    "MsgPriority": "High", // Message priority
    "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMFaceElem", // Emoji
            "MsgContent": {
                "Index": 6,
                "Data": "abc\u0000\u0001"
            }
        }
    ]
}
```
- **Forbidding callback for a message**
When the callback switch is turned on, users can specify `ForbidCallbackControl` to control whether to initiate callback for a single message. By default, callback is initiated.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
    "ForbidCallbackControl":[
		    "ForbidBeforeSendMsgCallback",
		    "ForbidAfterSendMsgCallback"], // Callback forbidding control options
    "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMFaceElem", // Emoji
            "MsgContent": {
                "Index": 6,
                "Data": "abc\u0000\u0001"
            }
        }
    ]
}
```
- **Sending group @ messages**
  The target @ users set in the `GroupAtInfo` field have a one-to-one and sequential correspondence to the target @ users in the message body.

  ```
      {
          "GroupId": "@TGS#2C5SZEAEF",
          "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
          "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
              {
                  "MsgType": "TIMTextElem", // Text
                  "MsgContent": {
                      "Text": "red @all @tommy @brennanli packet"
                  }
              }
          ],
          // It corresponds to @all @tommy @brennanli in the text information.
          "GroupAtInfo":[
          {
              "GroupAtAllFlag":1 // `1`: @ all ; `0`: @ a certain group member
          },
          {
              "GroupAtAllFlag":0,
              "GroupAt_Account":"tommy" // @ a specific group member
          },
          {
              "GroupAtAllFlag":0,
              "GroupAt_Account":"brennanli"
          }
  	 ]    
      }
  ```


- **Specifying messages for online delivery without offline or roaming retention**
If **OnlineOnlyFlag** in the message body is set to a value greater than `0`, the message is for online delivery only, not for offline or roaming retention (not available for AVChatRoom or BChatRoom).
```
    {
        "GroupId": "@TGS#2C5SZEAEF",
        "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
        "OnlineOnlyFlag": 1, // The message is for online delivery only (only online group members will receive it), not for offline or roaming retention.
        "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
            {
                "MsgType": "TIMTextElem", // Text
                "MsgContent": {
                    "Text": "red packet"
                }
            },
            {
                "MsgType": "TIMFaceElem", // Emoji
                "MsgContent": {
                    "Index": 6,
                    "Data": "abc\u0000\u0001"
                }
            }
        ]
    }
```


### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | ID of the group to which the message will be sent |
| Random | Integer | Yes | A 32-bit unsigned integer. If the random numbers of two messages within five minutes are the same, the later message will be discarded as a repeated message. |
| MsgPriority | String | No | Message priority |
| MsgBody | Array | Yes | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| From_Account | String | No | Message source account. If this field is not specified, the message sender is the app admin account used to call the API. Alternatively, apps can specify the message sender in this field to implement some special features. Note that if this field is specified, you must ensure that the account in this field exists. |
| OfflinePushInfo | Object | No | Information of offline push. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| ForbidCallbackControl | Array | No | Message callback forbidding option, valid only for a single message. `ForbidBeforeSendMsgCallback`: callback before sending the message is forbidden; `ForbidAfterSendMsgCallback`: callback after sending the message is forbidden. |
| OnlineOnlyFlag | Integer | No | `1`: send to online members only; `0` (default value): send to all members. This field is not valid for audio-video groups (AVChatRoom). |
| SendMsgControl | Array | No | Message sending permission, only valid for the current message. `NoLastMsg`: do not trigger conversation update; `NoUnread`: do not include the message in the unread count. |
| CloudCustomData | String | No | Custom message data. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. |

### Sample responses
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "MsgTime": 1497249503,
    "MsgSeq": 1
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. |
| ErrorInfo | String | Error information |
| MsgTime | Integer | Message sending timestamp, corresponding to the backend server time |
| MsgSeq | Integer | Message sequence number, the unique identifier of a message |

## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API.

| Error Code | Description |
|---------|---------|
| 10002 | Internal error of the server. Please retry. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. This error occurs when, for example, a member in a public group tries to remove other users from the group (only the app admin can perform this operation). |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Use a correct group ID. |
| 10016 | The app backend rejected this operation through a third-party callback. |
| 10017 | The message cannot be sent due to muting. Check whether the sender is muted. |
| 10023 | The frequency limit for message sending is reached. Try again later. |
| 80001 | Text security filtering. Check whether the message text contains restricted words. |
| 80002 | The message content is too long. Currently, the maximum message length supported is 8,000 bytes. Please adjust the message length. |

## Debugging Tool
Use the [RESTful API online debugging tool](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/group_open_http_svc/send_group_msg) to debug this API.

References

- Sending System Messages in a Group ([v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958))
- Sending One-to-One Messages to One User ([v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919))
- Sending One-to-One Messages to Multiple Users ([v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920))
- [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527)


## Possible Callbacks
 [Callback After Sending a Group Message](https://intl.cloud.tencent.com/document/product/1047/34375)
