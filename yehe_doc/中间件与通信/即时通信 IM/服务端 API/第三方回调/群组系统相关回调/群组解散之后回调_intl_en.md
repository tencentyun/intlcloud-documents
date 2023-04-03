## Feature Overview

This callback allows you to view the group disbanding status in real time on the backend. You can record the group disbanding information in real time, for example, by recording a log or syncing the information to another system.

## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user disbands a group on the client.
- The app admin disbands a group through the RESTful API.

## Callback Triggering Timing

This callback will be triggered after a group is disbanded.

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
| CallbackCommand | Fixed value: `Group.CallbackAfterGroupDestroyed`.            |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackAfterGroupDestroyed", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "Owner_Account": "leckie", // Group owner
    "Name": "MyFirstGroup", // Group name
    "MemberList" : [ //Members of the group to be disbanded
        {
            "Member_Account": "leckie"
        },
        {
            "Member_Account": "peter"
        },
        {
            "Member_Account": "bob"
        }
    ],
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field           | Type    | Description                                                  |
| --------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand | String  | Callback command                                             |
| GroupId         | String  | ID of the group to be disbanded                              |
| Type            | String  | Type of the group to be disbanded (for more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)), such as `Public` |
| Owner_Account   | String  | `UserID` of the group owner                                  |
| MemberList      | Array   | List of members of the group to be disbanded. This field will not be returned for communities. |
| EventTime       | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

A response is sent after the app backend records the group disbanding information.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Required | Error code. We recommend you set it to `0`. This callback is used to notify users of the topic deletion. The error code value of the user doesn't affect the deletion process. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Disbanding a Group](https://intl.cloud.tencent.com/document/product/1047/34896)
