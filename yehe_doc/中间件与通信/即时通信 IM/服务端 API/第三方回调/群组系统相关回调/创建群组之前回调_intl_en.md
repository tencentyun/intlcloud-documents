## Overview

This webhook event is used by the app backend to check users' group creation requests in real time. The app backend can also reject the requests.

## Notes

- To enable this webhook, you must configure a webhook URL and toggle on the corresponding protocol. For more information on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this webhook event, the Chat backend initiates an HTTP POST request to the app backend.
- After receiving the webhook request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Webhook Triggering Scenarios

- The app user creates a group on the client.
- The app admin creates a group through the RESTful API.

## Webhook Triggering Timing

It will be triggered before the Chat backend creates a group.

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
| CallbackCommand | Fixed value: `Group.CallbackBeforeCreateGroup`.              |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Webhook Protocols** section of [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackBeforeCreateGroup", // Webhook command
    "Operator_Account": "leckie", // Operator
    "Owner_Account": "leckie", // Group owner
    "Type": "Public", // Group type
    "Name": "MyFirstGroup", // Group name
    "CreateGroupNum": 123, // Number of groups of the same type that the user has created
    "MemberList": [ // List of initial members
        {
            "Member_Account": "bob"
        },
        {
            "Member_Account": "peter"
        }
    ],
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds
}
```

### Request fields

| Object           | Type    | Description                                                  |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | Webhook command                                              |
| Operator_Account | String  | `UserID` of the operator who initiates the group creation request |
| Owner_Account    | String  | `UserID` of the owner of the group requested to be created   |
| Type             | String  | Type of the group that generates group messages, such as `Public`. For details, see **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| Name             | String  | Name of the group requested to be created                    |
| CreateGroupNum   | Integer | Number of groups of the same type that the user has created  |
| MemberList       | Array   | List of initial members of the group requested to be created |
| EventTime        | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

#### Creation allowed

The user is allowed to create a group.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Creation allowed
}
```

#### Creation disallowed

The user is not allowed to create a group. No group will be created, and the error code `10016` will be returned to the caller.

```
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
| ErrorCode    | Integer | Yes      | Error code returned. `0`: Allows group creation; `1`: Forbids group creation. If the business side wants to use a custom error code to forbid a user to create a group and send `ErrorCode` and `ErrorInfo` to the client, ensure that the value of `ErrorCode` is set within the range of [10100, 10200]. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Creating a Group](https://intl.cloud.tencent.com/document/product/1047/34895)
