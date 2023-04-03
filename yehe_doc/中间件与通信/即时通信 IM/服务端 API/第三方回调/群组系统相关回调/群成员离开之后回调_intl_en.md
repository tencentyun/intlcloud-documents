## Feature Overview

This callback allows you to view the group leaving status of users on the app backend. You can record the group leaving information of users in real time, for example, by recording a log or syncing the information to another system.

## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user leaves the group on the client.
- An app user removes a group member from the group on the client.
- The app admin deletes a group member through the RESTful API.

## Callback Triggering Timing

This callback will be triggered after a user leaves the group or is removed from the group by the group owner/admin.

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
| CallbackCommand | Fixed value: `Group.CallbackAfterMemberExit`.                |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackAfterMemberExit", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
    "ExitType": "Kicked", // Group leaving mode. Valid values: `Kicked` (a member is removed from the group); `Quit` (a member leaves the group).
    "Operator_Account": "leckie", // Operator
    "ExitMemberList": [ // List of members who left the group
        {
            "Member_Account": "jared"
        },
        {
            "Member_Account": "tommy"
        }
    ],
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field            | Type    | Description                                                  |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | Callback command                                             |
| GroupId          | String  | ID of the group that generates group messages                |
| Type             | String  | Type of the group that generates group messages, such as `Public`. For details, see **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| ExitType         | String  | Group leaving mode. Valid values: `Kicked` (a member is removed from the group); `Quit` (a member leaves the group). |
| Operator_Account | String  | `UserID` of the user leaving the group                       |
| ExitMemberList   | Array   | List of members leaving the group                            |
| EventTime        | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

A response is returned after the app backend syncs the data.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Ignore the response result
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates to allow ignoring the response result. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Callback After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372)
- [Callback for Online and Offline Status of Audio-Video Group Members](https://intl.cloud.tencent.com/document/product/1047/48734)
- RESTful API: [Deleting Group Members](https://intl.cloud.tencent.com/document/product/1047/34949)
