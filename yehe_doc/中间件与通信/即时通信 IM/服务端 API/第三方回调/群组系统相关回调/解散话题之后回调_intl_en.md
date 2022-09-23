## Feature Description

This callback allows you to view the deletion status of a topic in real time on the application backend. Specifically, you can view the real-time log of the topic deletion or sync the information to other systems.

## Notes

- To enable this callback, you must configure a callback URL. This callback and the callback after group deletion use the same switch. For detailed directions, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- The application user deletes a topic on the client.
- The application admin deletes a topic through the RESTful API.

## Callback Triggering Timing

It will be triggered after a topic is deleted.

## API Call Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```json
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL |
| SdkAppid | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackAfterTopicDestroyed`. |
| contenttype | Fixed value: `JSON`. |
| ClientIP | Client IP, such as 127.0.0.1 |
| OptPlatform | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```json
{
    "CallbackCommand": "Group.CallbackAfterTopicDestroyed", // Callback command
    "GroupId": "@TGS#_@TGS#cQVLVHIM62CJ", // Group ID of the deleted topic
    "Type": "Community", 	// Group type
    "TopicIdList":[		// List of the deleted topics
       "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",
       "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic_1"
    ]
}
```

### Request fields

| Object | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| GroupId | String | Group of the deleted topic |
| Type | String | Group type of the deleted topic. Here, it is `Community`. |
| TopicIdList | String | List of the deleted topics |

### Sample response
The application backend records the topic deletion information and sends the callback response packet.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | Request result. OK: succeeded; FAIL: failed. |
| ErrorCode | Integer | Required | Error code. We recommend you set it to `0`. This callback is used to notify users of the topic deletion. The error code value of the user doesn't affect the deletion process. |
| ErrorInfo    | String  | Required | Error message |




## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Deleting Topic](https://intl.cloud.tencent.com/document/product/1047/49470)

