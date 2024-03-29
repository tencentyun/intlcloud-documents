
## Feature Overview
This API allows the app admin to import topic data without triggering callbacks or delivering notifications. When your app needs to be migrated to Chat from another instant messaging system, you can use this API to import existing topic data.

## API Calling Description
### Applicable group types

| Group Type | Support for This RESTful API |
|-----------|------------|
| Private | No |
| Public | No |
| ChatRoom | No |
| AVChatRoom | No |
| Community | This API applies only to topic-enabled communities. |

These are the preset group types in Chat. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
>?To use the topic feature, you need to go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), choose **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**, enable the community feature and then enable the topic feature.


### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/import_topic?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters
The following table describes only the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<br><li>China: `console.tim.qq.com`</li><li>Singapore: `adminapisgp.im.qcloud.com`</li><li>Seoul: `adminapikr.im.qcloud.com`</li><li>Frankfurt: `adminapiger.im.qcloud.com`</li><li>Mumbai: `adminapiind.im.qcloud.com`</li><li>Silicon Valley: `adminapiusa.im.qcloud.com`</li> |
| v4/group_open_http_svc/import_topic | Request API                             |
| sdkappid | SDKAppID assigned by the Chat console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype | Request format. The value is fixed to `json`. |

### Maximum call frequency

200 calls per second

### Sample request

- **Basic format**
Specify the group to which the topic to import belongs. You can use `CreateTime` to specify the topic creation time.
```
{
  "GroupId": "@TGS#_@TGS#cBZXAIIM62CV",     // (Required) ID of the group to which the topic to import belongs
  "TopicName": "test_topic3",           // (Optional) Topic name
  "CreateTime": 1448357837              // (Optional) Topic creation time
}
```
- **Specifying other optional fields**
Specify optional fields such as `Introduction` and `Notification`.
```
{
    "Type": "Community", // (Optional) Type of the group to which the topic belongs, which should be `Community`
    "GroupId": "@TGS#_@TGS#cBZXAIIM62CV",     // (Required) ID of the group to which the topic to import belongs
    "TopicName": "test_topic3",           // (Optional) Topic name
    "Introduction": "This is topic Introduction", // (Optional) Topic introduction
    "Notification": "This is topic Notification", // (Optional) Topic notification
    "FaceUrl": "http://this.is.face.url",
    "CreateTime": 1448357837 // (Optional) Topic creation time. If this field is not specified, the default creation time is the request time.
}
```


### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| Type | String | No  | Type of the group to which the topic belongs. Currently, only a Community group is supported. |
| GroupId  | String | Yes | ID of group to which the topic to import belongs.           |
| TopicId | String | No | To simplify topic IDs and make them easy to remember, Tencent Cloud allows apps to customize topic IDs during topic creation through RESTful APIs. For details, see [here](https://intl.cloud.tencent.com/document/product/1047/33529#customize). |
| TopicName | String | Yes | Topic name, whose maximum length is 30 bytes. This field is UTF-8-encoded, and one Chinese character occupies three bytes. |
| From_Account | uint64 | No | User account that wants to create the topic. |
| CustomString | String | No |Custom string, which can contain up to 3,000 bytes, encoded in UTF-8. |
| FaceUrl | String | No | URL of the topic profile photo, whose maximum length is 100 bytes. |
| Notification | String | No | Topic notice, whose maximum length is 300 bytes. This field is UTF-8-encoded, and one Chinese character occupies three bytes. |
| Introduction | String | No | Topic introduction, whose maximum length is 240 bytes. This field is UTF-8-encoded, and one Chinese character occupies three bytes. |
| CreateTime | Integer | No | Topic creation time |

### Sample response
- **Basic format**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "TopicId": "@TGS#_@TGS#cBZXAIIM62CV@TOPIC#_@TOPIC#cTCCCIIM62CW"
}
```

- **Specifying other optional fields**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "TopicId": "@TGS#_@TGS#cBZXAIIM62CV@TOPIC#_@TOPIC#c5CCCIIM62CW"
}
```


### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: Successful; other values: Failed |
| ErrorInfo | String | Error information |
| TopicId | String | Topic ID after successful creation, which is assigned by the Chat backend or specified by users. |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
|---------|---------|
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | Insufficient operation permissions. Check the request parameters based on the error message. |
| 10010 | The current group does not exist or has been deleted. |
| 10015 | The requested group ID is invalid. Check the request parameter based on the error message. |
| 10021 | The topic ID is already in use. Specify another topic ID. |
| 10037 | The number of prepaid topics created exceeds the limit. Delete some of the topics or upgrade your service. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). |
|11000|The current group does not support the community topic feature. To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577) and [enable it in the console](https://intl.cloud.tencent.com/document/product/1047/34419).|
| 80001  | Failed to pass the security check. Check the request parameters based on the error message.                   |
| 80005 | Failed to pass the security check: Security check timed out. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/#/group_open_http_svc/import_group) to debug this API.

## References

- Creating a topic ([v4/million_group_open_http_svc/create_topic](https://intl.cloud.tencent.com/document/product/1047/49471))
- Deleting a topic ([v4/million_group_open_http_svc/destroy_topic](https://intl.cloud.tencent.com/document/product/1047/49470))
- Importing a group profile ([v4/group_open_http_svc/import_group](https://intl.cloud.tencent.com/document/product/1047/34967))

