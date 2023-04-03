## Feature Overview

This callback allows you to view users' group join requests in real time on the app backend. You can block such requests.

## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

An app user sends a group join request on the client.

## Callback Triggering Timing

It will be triggered before the IM backend adds the user sending the group join request to the group (or before the admin is notified if admin approval is required).

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `roup.CallbackBeforeApplyJoinGroup`.            |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackBeforeApplyJoinGroup", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "Requestor_Account": "jared", // Requester
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field             | Type    | Description                                                  |
| ----------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand   | String  | Callback command                                             |
| GroupId           | String  | ID of the group that generates group messages                |
| Type              | String  | Type of the group that generates group messages, such as `Public`. For details, see **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| Requestor_Account | String  | `UserID` of the requester                                    |
| EventTime         | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

#### Allowing further processing

The group join request is allowed to be further processed.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // It indicates to allow further processing the group join request.
}
```

#### Rejecting the request

The group join request is not allowed to be further processed. The user cannot join the group, and the error code `10016` is returned to the caller.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // It indicates to reject the group join request.
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. `0` indicates to allow further processing; `1` indicates to reject the request. If you want to use the specified error code to reject a group join request, you need to pass in `ErrorCode` and `ErrorInfo` to the client, with `ErrorCode` in the range of [10100, 10200]. If a group join request requires admin approval, admin approval is still required even if `0` is returned in the callback. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

[Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
