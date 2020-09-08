## Features

The app backend can use this callback to monitor the login or logout behaviors of users in real time, including:
- User login (a TCP connection is established)
- User logout or network disconnection (a TCP connection is terminated)
- App heartbeat timeout (the app is abnormally killed or crashes)

## Notes

- To enable this callback, you must configure the callback URL and enable the corresponding protocol for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is the SDKAppID of the app.
- For more security considerations, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- A user initiates a login request through the client.
- A user initiates a logout request through the client.
- A user actively kills the client process, the app is killed by the operating system of the mobile phone after the user switches it to the background, or the process exits abnormally because it crashes. When it detects the client is disconnected from the network, the CVM instance triggers the network disconnection callback.
- The client heartbeat times out, for example, because the network is disconnected or the network is completely unavailable. When it detects that the client heartbeat has timed out, the CVM instance triggers the network disconnection callback. The heartbeat timeout interval is 400 seconds.

## Real-Time Callbacks
### Android, iOS, and PC
In most cases, the IM CVM instance can detect the user status change and trigger a callback in real time. For example:
- When a user logs in, the IM CVM instance triggers the Login and Register callbacks.
- When a user logs out, the IM CVM instance triggers the Logout and Unregister callbacks.
- When a user kills the client process or switches to the backend, or the client process is killed by the operating system of the mobile phone, the IM CVM instance triggers the Disconnect and LinkClose callbacks.

In the following special case, the IM CVM instance detects the status change only after the 400-second heartbeat timeout interval expires:
When the network is completely unavailable, and the client cannot even send the FIN or RST packets over TCP, the IM CVM instance triggers the Disconnect and TimeOut callbacks after the 400-second heartbeat timeout interval expires. Common scenarios include when the user disconnects the client from the network (for example, by enabling the Airplane mode on the mobile phone) or the user enters a tunnel with no network signal.

### Web
When a user logs in to the web app, the IM CVM instance can detect the login and trigger a callback in real time.
When the user network is unavailable or the user directly closes the webpage, the IM CVM instance can trigger a callback only after the 400-second heartbeat timeout interval expires.


## API Description
### Sample request URL

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Sample:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | Specifies that the request protocol is HTTPS and the request method is POST. |
| www.example.com | The callback URL. |
| SdkAppid | The SDKAppID assigned in the IM console when the app is created. |
| CallbackCommand | Fixed value: State.StateChange |
| contenttype | Fixed value: JSON |
| ClientIP | The IP address of the client, such as 127.0.0.1. |
| OptPlatform | The platform of the client. For more information about possible values, see the parameter description of the OptPlatform in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request packet

```
{
    "CallbackCommand": "State.StateChange",
    "Info": {
        "Action": "Logout",
        "To_Account": "testuser316",
        "Reason": "Unregister"
    }
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | The callback command. |
| Info | Object | The user login or logout information. |
| Action | String | The user login or logout behavior. Login indicates that a TCP connection is established, Logout indicates that the TCP connection is terminated, and Disconnect indicates that the network is disconnected. |
| To_Account | String | The UserID of a user |
| Reason | String | The reason for triggering user login or logout:<ul style="margin:0;"><li >Login reason: Register, which indicates that a TCP connection was established with the app.<li >Logout reason: Unregister, which indicates that the app user deregisters the account and terminates the TCP connection. <li >Disconnect reason: LinkClose, which indicates that IM detects that the TCP connection with the app was terminated, such as when the app is killed or the client sends a TCP FIN or RST packet. TimeOut: IM detects that the app heartbeat packet times out and determines that the TCP connection was terminated. For example, when the client network is abnormally disconnected, the client does not send the TCP FIN or RST packet and cannot send heartbeat packets. The heartbeat timeout interval is 400 seconds. <li >For the callback reasons of specific scenarios, see [Trigger Scenarios](https://intl.cloud.tencent.com/document/product/1047/34357).<li >If a user’s login request and logout request come at the same time, only the Logout + Unregister callback will be triggered, and the Login + Register callback will not be triggered. |

### Sample response packet

```
{
    "ActionStatus":"OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### Response packet fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: the app backend processing was successful. 1: the app backend processing failed. |
| ErrorInfo | String | Required | The error information. |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Online Status Management](https://intl.cloud.tencent.com/document/product/1047/33518)
