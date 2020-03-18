
>!This document applies to TRTC SDK for Web v4.x.x.

## Error Code Definitions

| Key                         | Error Code | Description                   |
| --------------------------- | ------ | ---------------------- |
| INVALID_PARAMETER           | 0x1000 | Invalid parameter               |
| INVALID_OPERATION           | 0x1001 | Invalid operation               |
| SIGNAL_CAHNNEL_SETUP_FAILED | 0x4001 | Failed to establish the signaling channel       |
| SIGNAL_CHANNEL_ERROR        | 0x4002 | Error with the signaling channel           |
| ICE_TRANSPORT_ERROR         | 0x4003 | Error with the ICE transport connection |
| JOIN_ROOM_FAILED            | 0x4004 | Failed to enter the room               |
| CREATE_OFFER_FAILED         | 0x4005 | Failed to create an SDP offer    |
| CLIENT_BANNED               | 0x4040 | The user was kicked out of the room         |
| SERVER_TIMEOUT              | 0x4041 | Media transmission service timed out       |
| SUBSCRIPTION_TIMEOUT        | 0x4042 | Remote stream subscription timed out         |
| UNKOWN                      | 0xFFFF | Unknown error               |

## Account Errors

| Error Code | Type | Description                                                         |
| :----- | :------- | :----------------------------------------------------------- |
| 70001  | Account system | `userSig` has expired. Please try to generate a signature again. If the signature expires immediately after generation, please check whether the validity period is too short or entered as 0 mistakenly |
| 70002  | Account system | The length of `userSig` is 0. Please check whether the signature is correctly calculated. Access `sign_src` to get the plain source code for signature calculation and verify the parameters to make sure that the signature is correctly calculated |
| 70003  | Account system | `userSig` verification failed. Please check whether the content of `userSig` has been truncated for reasons such as insufficient buffer length |
| 70004  | Account system | `userSig` verification failed. Please check whether the content of `userSig` has been truncated for reasons such as insufficient buffer length |
| 70005  | Account system | `userSig` verification failed. Please use a tool to check whether the generated `userSig` is correct      |
| 70006  | Account system | `userSig` verification failed. Please use a tool to check whether the generated `userSig` is correct      |
| 70007  | Account system | `userSig` verification failed. Please use a tool to check whether the generated `userSig` is correct      |
| 70008  | Account system | `userSig` verification failed. Please use a tool to check whether the generated `userSig` is correct      |
| 70009  | Account system | Failed to verify `userSig` by using the business public key. Please check whether the private key used by the generated `userSig` matches `sdkAppId` |
| 70010  | Account system | `userSig` verification failed. Please use a tool to check whether the generated `userSig` is correct      |
| 70013  | Account system | `userId` in `userSig` is different from that in the request. Please check whether the `userId` set in login is the same as that in `userSig` |
| 70014  | Account system | `sdkAppId` in `userSig` is different from that in the request. Please check whether the `sdkAppId` set in login is the same as that in `userSig`|
| 70015  | Account system | The verification method for this `sdkAppId` and account type was not found. Please check whether account integration has been performed |
| 70016  | Account system | The length of the pulled public key is 0. Please check whether the public key has been uploaded. If the public key was just uploaded again, please try again in 10 minutes  |
| 70017  | Account system | Internal verification of third-party credential timed out. Please try again |
| 70018  | Account system | Internal verification of third-party credential failed                                       |
| 70019  | Account system | The credential field is empty for HTTPS-based verification. Please correctly set `userSig`        |
| 70020  | Account system | `sdkAppId` was not found. Please check whether this parameter has been configured in Tencent Cloud |
| 70052  | Account system | Invalid `userSig`. Please generate a new one and try again|
| 70101  | Account system | Empty request packet                                               |
| 70102  | Account system | Incorrect request packet account type                                           |
| 70103  | Account system | Incorrect phone number format                                             |
| 70104  | Account system | Incorrect email address format                                                 |
| 70105  | Account system | Incorrect TLS account format                                             |
| 70106  | Account system | Invalid account format type                                             |
| 70107  | Account system | `userId` was not registered                                             |
| 70113  | Account system | Invalid quantity for batch operation                                               |
| 70114  | Account system | Restricted due to security reasons                                               |
| 70115  | Account system | The `uin` is not the one of the developer of the corresponding `sdkAppId`                           |
| 70140  | Account system | `sdkAppId` does not match `acctype`                                   |
| 70145  | Account system | Incorrect account type                                                 |
| 70169  | Account system | Internal error. Please try again                                           |
| 70201  | Account system | Internal error. Please try again                                           |
| 70202  | Account system | Internal error. Please try again                                           |
| 70203  | Account system | Internal error. Please try again                                           |
| 70204  | Account system | `sdkAppId` has no matching `acctype`                                 |
| 70205  | Account system | Failed to find `acctype`. Please try again                                    |
| 70206  | Account system | Invalid quantity for batch operation in the request                                        |
| 70207  | Account system | Internal error. Please try again                                           |
| 70208  | Account system | Internal error. Please try again                                           |
| 70209  | Account system | Failed to get the developer's `uin`                                      |
| 70210  | Account system | The `uin` in the request is not the one of the developer                                    |
| 70211  | Account system | Invalid `uin` in the request                                              |
| 70212  | Account system | Internal error. Please try again                                           |
| 70213  | Account system | Failed to access internal data. Please try again                                   |
| 70214  | Account system | Internal credential verification failed                                             |
| 70221  | Account system | Invalid login status. Please use `UserSig` to authenticate again                        |
| 70222  | Account system | Internal error. Please try again                                           |
| 70225  | Account system | Internal error. Please try again                                           |
| 70231  | Account system | Internal error. Please try again                                           |
| 70236  | Account system | `user signature` verification failed                                     |
| 70308  | Account system | Internal error. Please try again                                           |
| 70346  | Account system | Credential verification failed                                               |
| 70347  | Account system | Credential verification failed due to expiration |
| 70348  | Account system | Internal error. Please try again                                           |
| 70362  | Account system | Internal timeout. Please try again                                           |
| 70401  | Account system | Internal error. Please try again                                           |
| 70402  | Account system | Invalid parameter. Please check whether the required fields are all set and parameter settings meet the requirements |
| 70403  | Account system | The initiator of this operation is not the application admin and does not have the permission                      |
| 70050  | Account system | This account is temporarily prohibited from login due to excessive login failures and retries. Please check whether the credential is correct and retry after 1 minute |
| 70051  | Account system | Blacklisted account                                           |
