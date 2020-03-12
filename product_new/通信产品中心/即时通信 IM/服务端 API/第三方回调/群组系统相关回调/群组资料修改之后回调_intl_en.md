## Feature Description
The app backend uses this callback to monitor changes to group information (including the group name, group introduction, group notification, profile photo, and group-specific custom fields) in real time, including recording the changes of group information in real time (for example, recording a log or synchronizing the changes to other systems).

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

### Content that may trigger the callback

Group information includes [basic group information](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E5.9F.BA.E7.A1.80.E8.B5.84.E6.96.99) and [group-specific custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81).
Currently, this callback may be triggered when the group name, group introduction, group notification, or profile photo URL is modified. This callback is not triggered when other basic group information is modified.

### Callback triggering scenarios

- An app user modifies group information through a client.
- The app admin modifies group information through a RESTful API.

## Callback Triggering Time

The callback is triggered after basic group information is modified.

## API Description

### Request URL example

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | The callback URL. |
| SdkAppid | The SDKAppID assigned by the IM console when an app is created. |
| CallbackCommand | The value is fixed to Group.CallbackAfterGroupInfoChanged. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet examples
#### Modifying part of basic group information

If part of basic group information is modified, the request packet contains only the basic group information fields that have been modified.

```
{
    "CallbackCommand": "Group.CallbackAfterGroupInfoChanged", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "Operator_Account": "leckie", // Operator
    "Notification": "NewNotification" // Modified group announcement
}
```

#### Modifying part of group-specific custom fields

If part of group-specific custom fields are modified, the request packet contains only the group-specific custom fields that have been modified.

```
{
    "CallbackCommand": "Group.CallbackAfterGroupInfoChanged", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "Operator_Account": "leckie", // Operator
    "UserDefinedDataList": [ // Modified group-specific custom fields
        {
            "Key": "UserDefinedKey2", // Key of the custom field
            "Value": "UserDefinedValue2" // Value of the custom field
        }
    ]
}
```

#### Modifying both basic group information and group-specific custom fields

```
{
    "CallbackCommand": "Group.CallbackAfterGroupInfoChanged", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "Operator_Account": "leckie", // Operator
    "Name": "NewGroupName", // Changed group name
    "Introduction": "NewIntroduction", // Modified group introduction
    "Notification": "NewNotification", // Modified group announcement
    "FaceUrl": "NewFaceUrl", // Changed group profile photo URL
    "UserDefinedDataList": [ // Modified group-specific custom fields
        {
            "Key": "UserDefinedKey1", // Key of the custom field
            "Value": "UserDefinedValue1" // Value of the custom field
        },
        {
            "Key": "UserDefinedKey2",
            "Value": "UserDefinedValue2"
        },
        {
            "Key": "UserDefinedKey3",
            "Value": "UserDefinedValue3"
        }
    ]
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | The callback command. |
| GroupId | String | The ID of the group whose information is modified. |
| Type | String | The type of the group whose information is modified, such as Private, Public, or ChatRoom. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). |
| Operator_Account | String | The identifier of the operator. |
| Name | String | The changed group name. |
| Introduction | String | The modified group introduction. |
| Notification | String | The modified group announcement. |
| FaceUrl | String | The changed group profile photo URL. |
| UserDefinedDataList | Array | The modified group-specific custom fields. |

### Response packet example

After recording group information changes, the app backend sends a callback response packet.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Ignore the result in the response
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. The 0 value indicates that the result in the response is ignored. |
| ErrorInfo | String | Required | Error information. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Modifying group basic information](https://intl.cloud.tencent.com/document/product/1047/34962)
