## Feature Overview

This callback allows you to view a group member's request to invite another user to join the group on the app backend in real time. You can directly block such request on the app backend.

## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user sends a request to invite another user to join the group on the client.
- The app admin adds a user to a group through the RESTful API.

## Callback Triggering Timing

This callback will be triggered before the IM backend adds the target user to the group (or after the friendship verification is passed, if relationship chain hosting is involved and friendship verification is configured in IM for the app).

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
| CallbackCommand | Fixed value: `Group.CallbackBeforeInviteJoinGroup`           |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |


### Sample request

```
 {
    "CallbackCommand": "Group.CallbackBeforeInviteJoinGroup",
    "GroupId": "@TGS#2J4SZEAEL",
    "Type": "Public",
    "Operator_Account": "leckie",
    "DestinationMembers": [
        {
            "Member_Account": "jared"
        },
        {
            "Member_Account": "leckie"
        }
    ],
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field              | Type    | Description                                                  |
| ------------------ | ------- | ------------------------------------------------------------ |
| CallbackCommand    | String  | Callback command                                             |
| GroupId            | String  | Group ID                                                     |
| Type               | String  | Type of the group to be created (for more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)), such as `Public`. |
| Operator_Account   | String  | `UserID` of the request sender                               |
| DestinationMembers | Array   | Set of `UserID` values of the group                          |
| EventTime          | Integer | Event trigger timestamp in milliseconds                      |

### Sample response
#### Allowing all users to join the group

The app backend allows all users identified in all requests to join the group.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // It indicates to allow further processing the group join request.
}
```

#### Blocking certain members from joining the group

The app backend blocks certain users identified in the requests from being invited to the group. The identifiers of such users are returned in `RefusedMembers_Account`.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "RefusedMembers_Account": [ // List of users who refused to join the group
        "jared"
    ]
}
```

### Response fields

| Field                  | Type    | Required | Description                                                  |
| ---------------------- | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus           | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode              | Integer | Yes      | Error code. `0` indicates to allow further processing the group join request; `1` indicates to reject the request. If you want to use the specified error code to reject a group join request, you need to pass in `ErrorCode` and `ErrorInfo` to the client, with `ErrorCode` in the range of [10100, 10200]. |
| ErrorInfo              | String  | Yes      | Error information                                            |
| RefusedMembers_Account | Array   | No       | List of IDs of users who refused to join the group.          |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Adding Group Members](https://intl.cloud.tencent.com/document/product/1047/34921)
