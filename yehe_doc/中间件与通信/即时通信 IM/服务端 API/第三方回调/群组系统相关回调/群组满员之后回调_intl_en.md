## Feature Overview

This webhook event is used by the app backend to check the status of a full group in real time. For example, when some inactive group members are removed so that new users can join the group, this webhook will be sent to the app backend.

## Notes

- To enable this webhook, you must configure a webhook URL and toggle on the corresponding protocol. For more information on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this webhook event, the Chat backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Webhook Triggering Scenarios

- An app user requests to join a group on the client.
- An app user invites another user to join a group on the client.
- The app admin adds a group member via RESTful APIs.

## Webhook Triggering Timing

This webhook is triggered when the group is full after a new member has joined, or when the group is full and a new member fails to join.

## API Calling Description

### Sample request URL

In the following sample, the webhook URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Webhook URL                                                  |
| SdkAppid        | The `SDKAppID` assigned by the Chat console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackAfterGroupFull`.                 |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Webhook Protocols** section of [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackAfterGroupFull", // Webhook command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field           | Type    | Description                             |
| --------------- | ------- | --------------------------------------- |
| CallbackCommand | String  | Webhook command                         |
| GroupId         | String  | ID of the full group                    |
| EventTime       | Integer | Event trigger timestamp in milliseconds |

### Sample response

The app backend records the group full information and sends the webhook response packet.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // The value `0` indicates that the response result is ignored.
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates that the response result is ignored. |
| ErrorInfo    | String  | Yes      | Error information                                            |


## References

- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Deleting Group Members](https://intl.cloud.tencent.com/document/product/1047/34949)
- RESTful API: [Adding Group Members](https://intl.cloud.tencent.com/document/product/1047/34921)
