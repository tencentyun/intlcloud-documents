## Overview

The app backend can use this callback to view the login or logout behaviors of users in real time, including:
- User login (a TCP connection is established)
- User logout or network disconnection (a TCP connection is terminated)
- App heartbeat timeout (the app is abnormally killed or crashes)

## Notes

- To enable this callback, you must configure the callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is the SDKAppID of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).
- For native SDK enhanced edition 5.6.1200 or later and web SDK 2.14.0 or later, a forced logout due to multi-device login or multi-instance login will trigger only a Login (Register) callback. For other SDK versions, a forced logout due to multi-client login or multi-instance login will trigger both a Login (Register) callback and a Logout (Unregister) callback.

## Callback Trigger Scenarios

- A user initiates a login request through the client.
- A user initiates a logout request through the client.
- A user's client is disconnected and then connected again.
- A user proactively kills the client process, the app is killed by the operating system of the mobile phone after the user switches the app to the background, or the process exits abnormally because the app crashes. When detecting that the client is disconnected from the network, the CVM instance triggers the network disconnection callback.
- The client heartbeat times out, for example, because the network is disconnected or the network is completely unavailable. When detecting that the client heartbeat has timed out, the CVM instance triggers the network disconnection callback. The heartbeat timeout interval is 400 seconds.

## Real-Time Callbacks
### Android, iOS, and PC
In most cases, the IM CVM instance can detect the user status change and trigger a callback in real time. For example:
- When a user proactively logs in, the IM CVM instance triggers a Login (Register) callback.
- When a user proactively logs out, the IM CVM instance triggers a Logout (Unregister) callback.
- When a user proactively kills the client process or switches to the backend, or the client process is killed by the operating system of the mobile phone, the IM CVM instance triggers a Disconnect (LinkClose) callback.

Only in the following special case, the IM CVM instance detects the user status change only after the 400-second heartbeat timeout interval expires:
When the network is completely unavailable, and the client cannot even send the FIN or RST packets over TCP, the IM CVM instance triggers a Disconnect (TimeOut) callback after the 400-second heartbeat timeout interval expires. This usually occurs when the user disconnects the client from the network (for example, by enabling the airplane mode on the mobile phone) or the user enters a tunnel with no network signal.

### Web
When a user proactively logs in on the web client, the IM CVM instance triggers a Login (Register) callback in real time.

The timeliness of status change callbacks in various logout/disconnection scenarios is as follows:
- Direct page closing triggers a Disconnect (LinkClose) callback in real time.
- A network disconnection without closing the current page takes about 60 seconds to trigger a Disconnect (LinkClose) callback.
- Proactively calling the `destroy` API triggers a Logout (Unregister) callback in real time.

### Mini Program
When a user logs in on a Mini Program, the IM CVM instance triggers a Login (Register) callback in real time.

The timeliness of status change in various exit/disconnection scenarios is as follows:
- When a user clicks in the upper-right corner to exit, a Disconnect (LinkClose) callback is triggered in five seconds.
- Network disconnection (for example, enabling airplane mode on the phone) takes about 60 seconds to trigger a Disconnect (LinkClose) callback.
- Switching WeChat to the background takes about 30 seconds to trigger a Disconnect (LinkClose) callback.
- Terminating the WeChat process triggers a Disconnect (LinkClose) callback in real time.
- Proactively calling the destroy` API triggers a Logout (Unregister) callback in real time.

## API Description
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
| SdkAppid        | SDKAppID assigned by the IM console when the app is created  |
| CallbackCommand | Fixed value: State.StateChange                               |
| contenttype     | Fixed value: JSON.                                           |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of OptPlatform in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "State.StateChange",
    "EventTime": 1629883332497,
    "Info": {
        "Action": "Login",
        "To_Account": "testuser316",
        "Reason": "Register"
    },
    "KickedDevice": [
        {
            "Platform": "Windows"
        },
        {
            "Platform": "Android"
        }
    ]
}
```

### Request fields

| Field                 | Type    | Description                                                  |
| --------------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand       | String  | Callback command                                             |
| Info                  | Object  | User login or logout information                             |
| Action                | String  | User login or logout behavior. Valid values: Login (TCP connection established); Logout (TCP connection terminated); Disconnect (network disconnected) |
| To_Account            | String  | UserID of the user                                           |
| Reason                | String  | Reason for triggering user login or logout:<ul style="margin:0;"><li >Login reason: Register, which indicates that a TCP connection is established with the app or that the network is disconnected and then connected again.<li >Logout reason: Unregister, which indicates that the app user deregisters the account and terminates the TCP connection.<li >Disconnect reason: LinkClose, which indicates that IM detects that the TCP connection with the app is terminated, such as when the app is killed or the client sends a TCP FIN or RST packet. TimeOut: IM detects that the app heartbeat packet times out and determines that the TCP connection is terminated. For example, when the client network is abnormally disconnected, the client does not send the TCP FIN or RST packet and cannot send heartbeat packets. The heartbeat timeout interval is 400 seconds.<li >For the callback reasons of specific scenarios, see [Callback Trigger Scenarios](https://intl.cloud.tencent.com/document/product/1047/34357). |
| KickedDevice          | Array   | Information about other devices that are kicked offline. This field is available only when the current status change is Login (Register) and there are other devices being kicked offline. |
| KickedDevice.Platform | String  | Platform type of the device kicked offline. Valid values: iOS, `Android, Web, Windows, iPad, Mac, Linux |
| EventTime             | Integer | Timestamp when the current callback is triggered, in milliseconds. |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. OK: Successful; FAIL: Failed                 |
| ErrorCode    | Integer | Yes      | Error code. 0: The app backend processing was successful; 1: The app backend processing failed. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Online Status Management](https://intl.cloud.tencent.com/document/product/1047/33518)
