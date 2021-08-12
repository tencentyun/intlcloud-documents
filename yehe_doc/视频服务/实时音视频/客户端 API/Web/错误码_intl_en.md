
>!This document applies to TRTC SDK for Web 4.x.x.

## Error Code Definitions

| Key                         | getCode | Error Code | Description                   |
| --------------------------- | ------- | ------ | ---------------------- |
| INVALID_PARAMETER           | 4096    | 0x1000 | Invalid parameter.               |
| INVALID_OPERATION           | 4097    | 0x1001 | Invalid operation.               |
| SIGNAL_CAHNNEL_SETUP_FAILED | 16385   | 0x4001 | Failed to establish signaling channel.       |
| SIGNAL_CHANNEL_ERROR        | 16386   | 0x4002 | Signaling channel error.           |
| ICE_TRANSPORT_ERROR         | 16387   | 0x4003 | ICE transport connection error. |
| JOIN_ROOM_FAILED            | 16388   | 0x4004 | Failed to enter room.               |
| CREATE_OFFER_FAILED         | 16389   | 0x4005 | Failed to create SDP offer.    |
| CLIENT_BANNED               | 16448   | 0x4040 | User was kicked out.         |
| SERVER_TIMEOUT              | 16449   | 0x4041 | Media transmission service timed out.       |
| SUBSCRIPTION_TIMEOUT        | 16450   | 0x4042 | Remote stream subscription timed out.         |
| UNKNOWN                      | 65535   | 0xFFFF | Unknown error.               |



## Account Errors

| Error Code | Type | Description |
| :----- | :------- | :------------------------------------------------------------------------------------------------------------ |
| 70001  | Account system | `userSig` has expired. Please generate again. If the signature expires immediately after generation, check whether the validity period is too short or set to 0. |
| 70002  | Account system | The length of `userSig` is 0. Please access `sign_src` to get the source code for signature calculation and check the parameters to make sure that the signature is calculated correctly. |
| 70003  | Account system | `userSig` verification failed. Please check whether `userSig` has been truncated due to short buffer length, etc. |
| 70004  | Account system | `userSig` verification failed. Please check whether `userSig` has been truncated due to short buffer length, etc. |
| 70005  | Account system | `userSig` verification failed. Please check whether the `userSig` generated is correct with the help of a tool.      |
| 70006  | Account system | `userSig` verification failed. Please check whether the `userSig` generated is correct with the help of a tool.      |
| 70007  | Account system | `userSig` verification failed. Please check whether the `userSig` generated is correct with the help of a tool.      |
| 70008  | Account system | `userSig` verification failed. Please check whether the `userSig` generated is correct with the help of a tool.      |
| 70009  | Account system | Failed to verify `userSig` with the business public key. Please check whether the private key and `sdkAppId` used to generate `userSig` match. |
| 70010  | Account system | `userSig` verification failed. Please check whether the `userSig` generated is correct with the help of a tool.      |
| 70013  | Account system | `userId` in `userSig` is different from that in the request. Please check whether the `userId` entered during login is the same as that in `userSig`. |
| 70014  | Account system | `sdkAppId` in `userSig` is different from that in the request. Please check whether the `sdkAppId` entered during login is the same as that in `userSig`. |
| 70015  | Account system | The verification method for this `sdkAppId` and account type was not found. Please check whether account integration has been performed. |
| 70016  | Account system | The length of the public key pulled is 0. Please check whether a public key has been uploaded. If it was just uploaded, try again in 10 minutes.  |
| 70017  | Account system | Internal validation of third-party ticket timed out. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70018  | Account system | Internal validation of third-party ticket failed.                                       |
| 70019  | Account system | The ticket field for HTTPS-based validation is empty. Please enter the correct `userSig`.        |
| 70020  | Account system | `sdkAppId` was not found. Please make sure you have configured it in Tencent Cloud. |
| 70052  | Account system | Invalid `userSig`. Please generate a new one and try again.|
| 70101  | Account system | Empty request packet.                                               |
| 70102  | Account system | Incorrect account type in request packet.                                           |
| 70103  | Account system | Incorrect phone number format.                                             |
| 70104  | Account system | Incorrect email address format.                                                 |
| 70105  | Account system | Incorrect TLS account format.                                             |
| 70106  | Account system | Invalid account format type.                                             |
| 70107  | Account system | `userId` was not registered.                                             |
| 70113  | Account system | Invalid batch number.                                               |
| 70114  | Account system | Restricted for security reasons.                                               |
| 70115  | Account system | The `uin` does not match that of the `sdkAppId` developer.                           |
| 70140  | Account system | `sdkAppId` and `acctype` do not match.                                   |
| 70145  | Account system | Incorrect account type.                                                 |
| 70169  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70201  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70202  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70203  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70204  | Account system | `sdkAppId` has no matching `acctype`.                                 |
| 70205  | Account system | Failed to find `acctype`. Please try again.                                    |
| 70206  | Account system | Invalid batch number in request.                                       |
| 70207  | Account system | Internal error. Please try again.                                           |
| 70208  | Account system | Internal error. Please try again.                                           |
| 70209  | Account system | Failed to get developer's `uin`.                                      |
| 70210  | Account system | `uin` in request is not developer’s.                                   |
| 70211  | Account system | Invalid `uin` in request.                                              |
| 70212  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70213  | Account system | Failed to access internal data. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70214  | Account system | Internal ticket validation failed.                                             |
| 70221  | Account system | Invalid login status. Please authenticate your login with `UserSig` again.                        |
| 70222  | Account system | Internal error. Please try again.                                           |
| 70225  | Account system | Internal error. Please try again. If the problem persists after multiple retries, please contact TLS account support over QQ at 3268519604                      |
| 70231  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70236  | Account system | User signature verification failed.                                     |
| 70308  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70346  | Account system | Ticket validation failed.                                               |
| 70347  | Account system | Ticket expired and validation failed. |
| 70348  | Account system | Internal error. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70362  | Account system | Internal timeout. Please try again. If the problem persists after multiple retries, contact TLS account support over QQ at 3268519604.                      |
| 70401  | Account system | Internal error. Please try again.                                           |
| 70402  | Account system | Invalid parameter. Please check whether all required fields are filled in and the values entered meet the requirements. |
| 70403  | Account system | The initiator is not the application admin and is not authorized to perform the operation.                      |
| 70050  | Account system | The account is temporarily locked due to failed login and multiple retries. Please check whether the ticket is correct and try again in a minute. |
| 70051  | Account system | Blocked account. Please contact TLS account support over QQ at 3268519604.                                                        |

## Room Entry Errors
| Error Code | Message |
|:----- |:-------- |
| 10006 | Service is suspended due to overdue payments. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc), find the application you created, and click **Application Info** to view the status of your TRTC service. |
| -10011 | Unknown server error. Please try again. |
| -10012 | `roomId` not passed in or does not meet requirements. To use `roomId` in string type, set `useStringRoomId` to `true` when calling `TRTC.createClient`. |
| -10013 | `userSig` authentication failed. |
| -10015 | Failed to get server node on server. Please try again. |
| -10016 | Failed to create room on server. Check if `roomId` meets QoS requirements. |
| -10018 | After advanced permission control is enabled, `client.join` does not carry `privateMapKey` or `privateMapKey` is ` `. For details, see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157). |
| -10019 | After advanced permission control is enabled, `privateMapKey` carried by `client.join` does not meet the requirements. For details, see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157). |
| -10020 | Server connection timed out. Please try again. |

## Common Errors and Solutions
The following errors must be fixed through application-side intervention. For example, if camera access is denied, the application needs to prompt users to grant it camera access in order to be able to make video calls.


| Error Message | Reason | Solution |
| :--------------------------------------------------------- | :------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| publish timeout                                            | Publishing timed out.                                                                | Refresh and call `publish()` again.                                                                                                     |
| join room timeout                                          | Room entry timed out                                                                   | Refresh the page and try again.                                                                                                                       |
| DTLS Transport connection timeout (10s)                    | DTLS connection timed out.                                                     | Refresh and try again.                                                                                                                         |
| failed to connect to remote server via websocket           | WebSocket connection failed.                                                          | Refresh and try again.                                                                                                                         |
| ICE/DTLS Transport connection failed                       | Failed to establish media transport connection.                                                     | Check [firewall configuration](https://intl.cloud.tencent.com/document/product/647/35164).                                                             |
| previous publishing is ongoing, please avoid re-publishing | Already publishing.                                                     | Do not call `publish()` again after publishing.                                                                                                            |
| AbortError                                                 | The device was inaccessible due to an unknown device/system error.                                | Please test the device before making a call.                                                                                                               |
| NotReadableError                                           | The device was inaccessible due to a hardware, browser or webpage error. | Handle the error according to the error message returned, and send this message to the user: “The camera/mic cannot be accessed. Please make sure that no other applications are requesting access and try again.” |
| NotFoundError                                              | Unable to find the media (audio, video, or screen sharing) of the request parameter.                       | Please test the device before making a call.                                                                                                              |
| NotAllowedError                                            | The user has rejected the current browser instance’s request to access the camera/mic or share screens. | Remind the user that video calls are not possible without camera/mic access. |
| SignalChannel reconnect failed                             | WebSocket disconnected.                                                              | Refresh and try again.                                                                                                                         |
| duplicate publishing, please unpublish and then re-publish | Repeated `publish` calls.                                                                | Call `unpublish()` first before `publish()`.                                                                                                   |
| OverconstrainedError                                       | The browser could not get the `cameraId`/`microphoneId`.                                        | Make sure that the value of `cameraId/`microphoneId` is a valid non-empty string.                                                                                      |
| RtcError: no valid ice candidate found                     | TRTC SDK for desktop browsers failed with regard to hole punching via Session Traversal Utilities for NAT (STUN).                                                 | Check [firewall configuration](https://intl.cloud.tencent.com/document/product/647/35164).                                                             |
