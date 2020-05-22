## Feature Description

The app backend can use this callback to monitor the login or logout behavior of users in real time, including:
- User login (TCP connection establishment)
- User logout or network disconnection (TCP connection disconnection)
- App heartbeat timeout (app is abnormally killed in the backend or crashes)

## Precautions

- To enable this callback, you must configure the callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is the SDKAppID of the app.
- For more information on other security considerations, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354).
 

## Trigger Scenarios

- A user initiates a login request through the client.
- A user initiates a logout request through the client.
- The backend process is killed on the client, or the CVM detects that the client is disconnected from the network.
- The client experiences a heartbeat timeout, including client crash and heartbeat timeout detected by the CVM 400 seconds after the network is disconnected.


## Trigger Conditions

This callback occurs after the IM CVM receives a TCP connection establishment or disconnection packet from the client or fails to receive successive heartbeat packets.

## API Description
### Example request URL

In the following example, the callback URL configured for the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | The callback URL. |
| SdkAppid | The SDKAppID assigned by the IM console when an application is created. |
| CallbackCommand | This parameter has a fixed value of State.StateChange. |
| contenttype | The value is fixedly set to JSON. |
| ClientIP | The client IP address, such as 127.0.0.1. |
| OptPlatform | The client platform. For more information on the value, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocol](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Example request packet

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
| Action | String | The user login or logout behavior. Login indicates that a TCP connection is established, Logout indicates that the TCP connection is disconnected, and Disconnect indicates that the network is disconnected. |
| To_Account | String | The UserID of a user. |
| Reason | String | The reason for triggering user login or logout.<ul style="margin:0;"><li>Login reason: Register, which indicates that a TCP connection is established with the app.</li><li>Logout reason: Unregister, which indicates that the app user deregisters the account and disconnects the TCP connection.</li><li>Disconnect reason: <ul style="margin:0;"><li>LinkClose: IM detects that the TCP connection with the app is disconnected, for example, the app is killed, or the client sends a TCP FIN or RST packet. </li><li>TimeOut: IM detects that the app heartbeat packet times out and regards that the TCP connection is disconnected. The heartbeat timeout time is 400s. For example, the client network is disconnected, and the client does not send the TCP FIN or RST packet and cannot send heartbeat packets. </li></ul></li></ul>|

### Example response packet

```
{
    "ActionStatus":"OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### Response packet fields

| Field | Type | Property | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: succeeded. 1: failed. |
| ErrorInfo | String | Required | The error information. |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Online Status Management](https://intl.cloud.tencent.com/document/product/1047/33518)
