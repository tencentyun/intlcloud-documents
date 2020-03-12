## Feature Description

The app backend can use this callback to monitor the login or logout behaviors of users in real time, including:
- User login (establishment of a TCP connection)
- User logout or user network disconnection (disconnection of the TCP connection)
- App heartbeat timeout (app is unexpectedly killed by the backend or crashes)

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).
- A large number of heartbeat timeout packets (for example, when the app crashes or is killed by the backend) may incur. The developer’s backend service needs to monitor the server performance when responding to the callback.

## Callback Triggering Scenarios

- A user initiates a login request through the client.
- A user initiates a logout request through the client.
- The backend process is killed on the client, or the CVM detects that the client is disconnected from the network.
- The client experiences a heartbeat timeout, including client crash and heartbeat timeout detected by the CVM 400 seconds after the network is disconnected.


## Callback Triggering Time

The callback is triggered after the IM CVM receives a TCP connection establishment or TCP connection end packet, or after the IM CVM fails to receive successive heartbeat packets.

## API Description
### Request URL example

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | The callback URL. |
| SdkAppid | The SDKAppID assigned by the IM console when an app is created. |
| CallbackCommand | The value is fixed to State.StateChange. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

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
| Info | Object | User login or logout information. |
| Action | String | The user login or logout behavior. Login: login (establishment of a TCP connection). Logout: logout (termination of the TCP connection). Disconnect: network disconnection (disconnection of the TCP connection). |
| To_Account | String | The user’s identifier. |
| Reason | String | The reason for triggering user login or logout. <br>The Login reason is Register, that is, the app establishes a TCP connection. <br>The Logout reason is Unregister, that is, the TCP connection is terminated due to the de-registration of the app user. <br>The Disconnect reasons are: LinkClose (IM detects that the app’s TCP connection is terminated, for example, the app is killed or the client sends a TCP FIN or RST packet) and TimeOut (IM detects an app heartbeat timeout and determines that the TCP connection is lost, for example, the client is unexpectedly disconnected from the network and cannot send a TCP FIN or RST packet or heartbeat packets.) |

### Response packet example

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: the app backend processing succeeded. 1: the app backend processing failed. |
| ErrorInfo | String | Required | Error information. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Online status management](https://intl.cloud.tencent.com/document/product/1047/33518)
