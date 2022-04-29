
>!This document applies to 4.x.x versions of the TRTC web SKD.

## Error Code Definitions

| Key                         | getCode | Error Code | Description                   |
|------|----|---|------------------------------|
| INVALID_PARAMETER   | 4096    | 0x1000 | Invalid parameter.<br>Suggested solution: Check whether the parameter values passed in meet the requirements. For example, check whether the correct types of values were passed in. |
| INVALID_OPERATION   | 4097    | 0x1001 | Invalid operation.<br/>Suggested solution: Check whether the API was called correctly. For example, if you call `publish` before room entry, this error will be returned. |
| NOT_SUPPORTED       | 4098    | 0x1002 | If this error is returned when you call an API, it indicates the current browser does not support the API. <ul style="margin:0"><li/>Suggested solution: Ask the user to switch to a browser supported by the SDK. For details, see [Environment and Device Check Before Calls](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html).          |
| DEVICE_NOT_FOUND    | 4099    | 0x1003 | This error is returned when the SDK attempts to capture data from the mic or camera but cannot find a mic or camera.<br>Suggested solution: Ask the user to check whether the mic or camera functions properly. We recommend you add device check logic to your project. For details, see [Environment and Device Check Before Calls](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html). |
| INITIALIZE_FAILED   | 4100    | 0x1004 | `LocalStream.initialize()` failed to capture data. For details, see [Solution](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ErrorCode.html#.INITIALIZE_FAILED).         |
| SIGNAL_CAHNNEL_SETUP_FAILED        | 16385   | 0x4001 | Failed to establish a signaling channel. The reason is often related to accounts. For details, see [Account Errors](https://intl.cloud.tencent.com/document/product/647/41665).       |
| SIGNAL_CHANNEL_ERROR        | 16386   | 0x4002 | Signaling channel error.           |
| ICE_TRANSPORT_ERROR                | 16387   | 0x4003 | ICE transport connection error. This indicates an error occurred with the audio/video transmission channel. This is usually caused by UDP port exceptions. For example, if the ports used for data transfer are blocked by a user’s computer or router firewall, this error will be returned. For the ports used for data transfer, see [Dealing with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).  |
| JOIN_ROOM_FAILED    | 16388   | 0x4004 | Failed to enter the room. For details, see [Room Entry Errors](https://intl.cloud.tencent.com/document/product/647/41665)          |
| CREATE_OFFER_FAILED         | 16389   | 0x4005 | Failed to create SDP offer.    |
| SIGNAL_CHANNEL_RECONNECTION_FAILED | 16390   | 0x4006 | Failed to reconnect WebSocket to the signaling channel.<ul style="margin:0"><li/>When WebSocket is disconnected, the SDK will try to reconnect it. If multiple retries fail, it will return this error.<li/>Suggested solution: Ask users to check their network connection and enter the room again.      |
| UPLINK_RECONNECTION_FAILED         | 16391   | 0x4007 | Upstream peer reconnection failed.<ul style="margin:0"><li/>When upstream peers are disconnected, the SDK will try to reconnect them. If multiple retries fail, it will return this error.<li/>Suggested solution: Ask users to check their network connection and publish or enter the room again.        |
| DOWNLINK_RECONNECTION_FAILED       | 16392   | 0x4008 | Downstream peer reconnection failed. <ul style="margin:0"><li/>When downstream peers are disconnected, the SDK will try to reconnect them. If multiple retries fail, it will return this error.<li/>Suggested solution: Ask users to check their network connection and enter the room again.       |
| REMOTE_STREAM_NOT_EXIST            | 16400   | 0x4010 | The remote stream does not exist.<ul style="margin:0"><li/>If user A tries to subscribe to the stream of user B, but user B has stopped publishing his or her stream, this error will be returned.<li/>This error does not need to be handled.     |
| CLIENT_BANNED       | 16448   | 0x4040 | The user was removed from the room for one of the following reasons: <ul style="margin:0"><li/>A user with the same username entered the room. **Note**: Avoid repeated room entry with the same username because it will cause an error.<li/>The account admin called a server-side API to remove the user from the room.  |
| SERVER_TIMEOUT              | 16449   | 0x4041 | Media transmission service timed out.       |
| SUBSCRIPTION_TIMEOUT        | 16450   | 0x4042 | Remote stream subscription timed out.         |
| PLAY_NOT_ALLOWED    | 16451   | 0x4043 | Autoplay blocked.<ul style="margin:0"><li/>When you call `play()`, if audio/video fails to be played due to the [autoplay policy](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes) of the browser, this error will be returned.<li/>Suggested solution: Instruct users through UI interactions to resume play via the calling of `resume()`. For details, see [Suggested Solutions for Autoplay Restrictions](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html) |
| DEVICE_AUTO_RECOVER_FAILED         | 16452   | 0x4044 | Failed to resume capturing data from the mic/camera. This is an error event for `LocalStream`.<ul style="margin:0"><li/>When a device change is detected (for example, if the camera or mic used for publishing is disconnected or reconnected), the SDK will try to resume capturing. If it fails, this error will be returned. <li/>Suggested solution: Notify users of the failure and ask them to check if their devices are disconnected or occupied by other applications.<li/>You can also add a retry button to the UI for users to manually resume capturing. |
| START_PUBLISH_CDN_FAILED           | 16453   | 0x4045 | Failed to publish to CDN.          |
| STOP_PUBLISH_CDN_FAILED            | 16454   | 0x4046 | Failed to stop publishing to CDN.          |
| START_MIX_TRANSCODE_FAILED         | 16455   | 0x4047 | Failed to start On-Cloud MixTranscoding.     |
| STOP_MIX_TRANSCODE_FAILED          | 16456   | 0x4048 | Failed to stop On-Cloud MixTranscoding.     |
| NOT_SUPPORTED_H264  | 16457   | 0x4049 | The device does not support H.264.                                         |
| SWITCH_ROLE_FAILED  | 16458   | 0x404a | Failed to switch user roles.         |
| UNKNOWN                      | 65535   | 0xFFFF | Unknown error.               |



## Account Errors

| Error Code | Type | Description                                                         |
|:--|:-----|:-------------------|
| -8     | Account system | Invalid `SDKAppID`. Check whether a valid value was passed in.              |
| 70001  | Account system | `userSig` has expired. Please generate again. If the signature expires immediately after generation, check whether the validity period is too short or set to 0. |
| 70002  | Account system | The length of `userSig` is 0. Access `sign_src` to get the source code for signature calculation and check the parameters to ensure that the signature is calculated correctly. |
| 70003  | Account system | `userSig` verification failed. Check whether `userSig` has been truncated due to short buffer length or other reasons. |
| 70004  | Account system | `userSig` verification failed. Check whether `userSig` has been truncated due to short buffer length or other reasons. |
| 70005  | Account system | `userSig` verification failed. Check whether the `userSig` generated is correct with the help of a tool.      |
| 70006  | Account system | `userSig` verification failed. Check whether the `userSig` generated is correct with the help of a tool.      |
| 70007  | Account system | `userSig` verification failed. Check whether the `userSig` generated is correct with the help of a tool.      |
| 70008  | Account system | `userSig` verification failed. Check whether the `userSig` generated is correct with the help of a tool.      |
| 70009  | Account system | Failed to verify `userSig` with the business public key. Check whether the private key and `SDKAppID` used to generate `userSig` match. |
| 70010  | Account system | `userSig` verification failed. Check whether the `userSig` generated is correct with the help of a tool.      |
| 70013  | Account system | `userId` in `userSig` is different from that in the request. Check whether the `userId` entered during login is the same as that in `userSig`. |
| 70014  | Account system | `SDKAppID` in `userSig` is different from that in the request. Check whether the `SDKAppID` entered during login is the same as that in `userSig`. |
| 70015  | Account system | No verification method was found for this `SDKAppID` and account type. Check whether account integration has been performed. |
| 70016  | Account system | The length of the public key pulled is 0. Check whether a public key has been uploaded. If it was just uploaded, try again in 10 minutes.  |
| 70017  | Account system | Internal verification of third-party ticket timed out. Try again.                      |
| 70018  | Account system | Internal verification of third-party ticket failed.                                       |
| 70019  | Account system | The ticket field for HTTPS-based verification is empty. Enter the correct `userSig`.        |
| 70020  | Account system | The application (`SDKAppID`) was not found. Make sure you have created it in Tencent Cloud. |
| 70052  | Account system | Invalid `userSig`. Generate a new one and try again.|
| 70101  | Account system | Empty request packet.                                               |
| 70102  | Account system | Invalid account type in request packet.                                           |
| 70103  | Account system | Invalid phone number format.                                             |
| 70104  | Account system | Invalid email address format.                                                 |
| 70105  | Account system | Invalid TLS account format.                                             |
| 70106  | Account system | Invalid account format type.                                             |
| 70107  | Account system | The `userId` was not registered.                                             |
| 70113  | Account system | Invalid quantity for batch operation.                                               |
| 70114  | Account system | Restricted due to security reasons.                                               |
| 70115  | Account system | The UIN does not match that of the application developer.                           |
| 70140  | Account system | `SDKAppID` and `acctype` do not match.                                   |
| 70145  | Account system | Incorrect account type.                                                 |
| 70169  | Account system | Internal error. Try again.                      |
| 70201  | Account system | Internal error. Try again.                      |
| 70202  | Account system | Internal error. Try again.                      |
| 70203  | Account system | Internal error. Try again.                       |
| 70204  | Account system | The `SDKAppID` has no matching `acctype`.                                 |
| 70205  | Account system | Failed to find `acctype`. Try again.                                    |
| 70206  | Account system | Invalid quantity for batch operation in the request.                                        |
| 70207  | Account system | Internal error. Try again.                                           |
| 70208  | Account system | Internal error. Try again.                                           |
| 70209  | Account system | Failed to get the developer's UIN.                                      |
| 70210  | Account system | The UIN in the request is not the developer’s.                                    |
| 70211  | Account system | Invalid UIN in the request.                                              |
| 70212  | Account system | Internal error. Try again.                       |
| 70213  | Account system | Failed to access internal data. Try again.                      |
| 70214  | Account system | Internal ticket verification failed.                                             |
| 70221  | Account system | Invalid login status. Verify login with `UserSig` again.                        |
| 70222  | Account system | Internal error. Try again.                                           |
| 70225  | Account system | Internal error. Try again.                       |
| 70231  | Account system | Internal error. Try again.                       |
| 70236  | Account system | Failed to verify the user signature.                                     |
| 70308  | Account system | Internal error. Try again.                      |
| 70346  | Account system | Ticket verification failed.                                               |
| 70347  | Account system | Failed to verify the ticket because it has expired. |
| 70348  | Account system | Internal error. Try again.                      |
| 70362  | Account system | Internal timeout. Try again.                       |
| 70401  | Account system | Internal error. Try again                                           |
| 70402  | Account system | Invalid parameter. Check whether all required fields are filled in and the values entered meet the requirements. |
| 70403  | Account system | The initiator is not the application admin and is not authorized to perform the operation.                      |
| 70050  | Account system | The account is temporarily locked due to multiple failed login retries. Please check whether the ticket is correct and try again in a minute. |
| 70051  | Account system | Blocked account.                                                         |

## Room Entry Errors
| Error Code | Description              |
|:--|:-----------|
| 10006 | Service is suspended due to overdue payments. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc), find the application you created, and click **Application Info** to view the status of your TRTC service. |
| -10011 | Unknown server error. Try again. |
| -10012 | `roomId` was not passed in or did not meet the requirements. To use string-type `roomId`, set `useStringRoomId` to `true` when calling `TRTC.createClient`. |
| -10013 | `userSig` authentication failed. |
| -10015 | Failed to get server node on server. Try again. |
| -10016 | Failed to create room on server. Check if the room (`roomId`) exceeded the bandwidth limit. |
| -10018 | Advanced permission control was enabled, but `client.join` did not carry `privateMapKey` or `privateMapKey` was ` `. For details, see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157). |
| -10019 | Advanced permission control was enabled, but the `privateMapKey` carried by `client.join` did not meet the requirements. For details, see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157). |
| -10020 | Server connection timed out. Try again. |

## Common Errors and Solutions
The following errors must be fixed through application-side intervention. For example, if camera access is denied, your application needs to prompt users to grant it camera access in order to be able to make video calls.


| Error Message    | Description    | Solution    |
|:--------------|:------------|:-------------|
| publish timeout     | `publish` timed out.               | Refresh and call `publish()` again.          |
| join room timeout   | Room entry timed out.    | Refresh and try again.    |
| DTLS Transport connection timeout (10s)     | DTLS transport connection timed out.    | Refresh and try again.      |
| failed to connect to remote server via websocket           | WebSocket connection failed.                                                          | Refresh and try again.                                                                                                                         |
| ICE/DTLS Transport connection failed                       | Failed to establish media transport connection.                                                     | Check your [firewall configuration](https://intl.cloud.tencent.com/document/product/647/35164).                                                             |
| previous publishing is ongoing, please avoid re-publishing | Already publishing.                                                     | Do not call `publish()` again after publishing.                                                                                                            |
| AbortError            | The device could not be accessed due to an unknown device/system error.         | Test the device before making a call.        |
| NotReadableError                                           | The device was inaccessible due to a hardware, browser or webpage error. | Handle the error according to the error message returned, and send this message to the user: “The camera/mic cannot be accessed. Please make sure that no other applications are requesting access and try again.” |
| NotFoundError         | Could not find the media (audio, video, or screen sharing) specified by the request parameter.                       | Test the device before making a call.                                                                                                              |
| NotAllowedError| The user rejected the request of the current browser instance to access the camera/mic or share the screen.| Remind the user that audio/video calls cannot be made without camera/mic access. |
| SignalChannel reconnect failed      | WebSocket was disconnected.             | Refresh and try again.      |
| duplicate publishing, please unpublish and then re-publish | Repeated `publish` calls.              | Call `unpublish()` first before `publish()`.      |
| OverconstrainedError            | The browser could not get the camera/mic.        | Make sure that the value of `cameraId/`microphoneId` is a valid non-empty string.      |
| RtcError: no valid ice candidate found                     | The TRTC Web SKD failed with regard to hole punching via Session Traversal Utilities for NAT (STUN).       | Check your [firewall configuration](https://intl.cloud.tencent.com/document/product/647/35164).                                                             |
