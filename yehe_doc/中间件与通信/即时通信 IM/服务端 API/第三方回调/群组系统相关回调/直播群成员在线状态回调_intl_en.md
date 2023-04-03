## Feature Overview

This webhook allows you to view the online and offline status (such as record logs) of an audio-video group in real time or synchronize the information to other systems on the app backend. This wehhook synchronizes only the online and offline events. To monitor the group joining and leaving events, see [After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372) and [After a User Leaves a Group](https://intl.cloud.tencent.com/document/product/1047/34373).

## Reminders

- To use this webhook, you need to purchase the [Ultimate edition](https://buy.cloud.tencent.com/avc?from=17473) and enable the **List of online audio-video group members** feature on the **Group feature configuration** page in the console. After the feature is enabled in the console, the list of the latest 1,000 online members of an audio-video group will be stored and the list can be pulled on clients. If the feature is disabled in the console, the list cannot be pulled on clients, and only the list of the 30 latest group members can be pulled.
- To enable this webhook, you must configure a webhook URL and toggle on the corresponding protocol. For more information on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this webhook event, the Chat backend initiates an HTTP POST request to the app backend.
- After receiving the webhook request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Webhook Triggering Scenarios

- App users abnormally exit after entering the audio-video group, and the network is disconnected for over 20 seconds.
- App users abnormally exit after entering the audio-video group and go online after the network is disconnected for over 20 seconds.

## Webhook Triggering Timing

After a user enters the audio-video group, the `Offline` event is triggered due to heartbeat timeout caused by network disconnection, and the `Online` event is triggered when the user goes online 20s after the timeout. If the user logs in with multiple devices and joins the same audio-video group concurrently, the `Offline` event will be triggered when all the devices go offline concurrently. The `Online` event will be triggered when any device goes back online (only one `Online` event will be triggered even if multiple devices go back online).

## API Calling Description

### Sample request URL

In the following sample, the webhook URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | The `SDKAppID` assigned by the Chat console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackOnMemberStateChange`.            |
| contenttype     | Fixed value: `JSON`.                                         |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackOnMemberStateChange", // Webhook command
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

| Field           | Type   | Description                                              |
| --------------- | ------ | -------------------------------------------------------- |
| CallbackCommand | String | Webhook command                                          |
| GroupId         | String | ID of the group that generates group messages            |
| EventType       | String | Event type: Offline (disconnected); Online (reconnected) |
| MemberList      | Array  | List of members triggering the event                     |

### Sample response

A response is returned after the app backend synchronizes the data.

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
- [After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372)
- [After a User Leaves a Group](https://intl.cloud.tencent.com/document/product/1047/34373)
