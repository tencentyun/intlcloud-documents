## Feature Overview

This callback allows you to view the user's topic creation request on the application backend in real time. In addition, the application backend can reject the request.

## Notes

- To enable this callback, you must configure the URL. This callback and the callback before group creation use the same switch. For detailed directions, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).
- You need to [enable the topic feature in the console](https://intl.cloud.tencent.com/document/product/1047/34419) before using it.

## Callback Triggering Scenarios

- The application user creates a topic on the client.
- The application admin creates a topic through the RESTful API.

## Callback Triggering Timing

It will be triggered before the IM backend creates a topic.

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```json
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackBeforeCreateTopic`.              |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```json
{
    "CallbackCommand": "Group.CallbackBeforeCreateTopic", // Callback command
    "Operator_Account": "leckie", // Operator
    "Type": "Community", // Group type
    "Name": "MyFirstTopic" // Group name
}
```

### Request fields

| Object           | Type   | Description                                                  |
| ---------------- | ------ | ------------------------------------------------------------ |
| CallbackCommand  | String | Callback command                                             |
| Operator_Account | String | `UserID` of the operator who initiates the topic creation request |
| Type             | String | Group type of the topic. Here, it is `Community`.            |
| Name             | String | Name of the topic requested to be created                    |

### Sample response

#### Creation allowed

The user is allowed to create a topic.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Creation allowed
}
```

#### Creation refused

The user is not allowed to create a topic. No topic will be created, and the error code `10016` will be returned to the caller.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // Creation refused
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. Valid values: `0` (creation allowed); `1` (creation refused). If you want to use your own error code to refuse a user request for topic creation, you need to pass in ` ErrorCode` and `ErrorInfo` to the client, with `ErrorCode` in the range of [10100,10200]. |
| ErrorInfo    | String  | Yes      | Error message                                                |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Creating Topic](https://intl.cloud.tencent.com/document/product/1047/49471)
