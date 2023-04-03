## Feature Overview

This callback allows you to view the messages of group member join on the application backend in real time. Specifically, it notifies the application backend of group join so that the app can sync data as necessary.

## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user sends a request to join the group on the client, and the request is approved.
- An app user successfully invites another user to join the group on the client.
- The app admin adds a user to a group through the RESTful API.

## Callback Triggering Timing

- This callback will be triggered after a user requests to join a group and successfully joins the group.
- This callback will be triggered after a user is invited by another member and successfully joins the group.
- This callback will be triggered after a user is added to a group by the app admin through the RESTful API.

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
| CallbackCommand | Fixed value: `Group.CallbackAfterNewMemberJoin`.             |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackAfterNewMemberJoin", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "JoinType": "Apply", // Group joining mode. Valid values: `Apply` (group join upon request); `Invited` (group join by invitation).
    "Operator_Account": "leckie", // Operator
    "NewMemberList": [ // List of new members in the group
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
| GroupId          | String  | Group ID                                                     |
| Type             | String  | Type of the group to be created (for more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)), such as `Public`. |
| JoinType         | String  | Group joining mode. Valid values: `Apply` (group join upon request); Invited (group join by invitation). |
| Operator_Account | String  | `UserID` of the request sender                               |
| NewMemberList    | Array   | Set of `UserID` values of new group members                  |
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
| ActionStatus | String  | Yes      | Request result. `OK`: successful; `FAIL`: failed             |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates to allow ignoring the response result. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Callback After a User Leaves a Group](https://intl.cloud.tencent.com/document/product/1047/34373)
- [Callback for Online and Offline Status of Audio-Video Group Members](https://intl.cloud.tencent.com/document/product/1047/48734)
- RESTful API: [Adding Group Members](https://intl.cloud.tencent.com/document/product/1047/34921)
