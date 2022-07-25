## Feature Description

This callback allows you to view the online and offline status (such as record logs) of an audio-video group in real time or sync the information to other systems on the app backend.

## Notes

- The feature can be used after you [upgrade](https://www.tencentcloud.com/document/product/1047/34577) to Ultimate Edition and enable the **List of online audio-video group members** feature in **Group feature configuration** in the console.
- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- App users abnormally exit after entering the audio-video group, and the network is disconnected for over 20s.
- App users abnormally exit after entering the audio-video group and go online after the network is disconnected for over 20s.

## Callback Triggering Timing

After a user enters the audio-video group, the `Offline` event is triggered due to heartbeat timeout caused by network disconnection, and the `Online` event is triggered when the user goes online 20s after the timeout. If the user logs in with multiple devices and joins the same audio-video group concurrently, the `Offline` event will be triggered when all the devices go offline concurrently. The `Online` event will be triggered when any device goes back online (only one `Online` event will be triggered even if multiple devices go back online).

## API Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL |
| SdkAppid | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackOnMemberStateChange`. |
| contenttype | Fixed value: `JSON`. |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackOnMemberStateChange", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "EventType": "Offline", // Event type: Offline (disconnected); Online (reconnected)
    "MemberList": [ // List of members who left the group
        {
            "Member_Account": "jared"
        },
        {
            "Member_Account": "tommy"
        }
    ]
}
```

### Request fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| GroupId | String | ID of the group that generates group messages |
| EventType | String | Event type: Offline (disconnected); Online (reconnected) |
| MemberList | Array | List of members triggering the event |

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

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Yes | Request result. OK: succeeded; FAIL: failed. |
| ErrorCode | Integer | Yes | Error code. The value `0` indicates to allow ignoring the response result. |
| ErrorInfo    | String  | Yes | Error information                                       |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Deleting Group Members](https://intl.cloud.tencent.com/document/product/1047/34949)


