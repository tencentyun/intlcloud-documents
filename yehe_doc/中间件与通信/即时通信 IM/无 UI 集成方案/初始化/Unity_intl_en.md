## Feature Description
You **must** initialize the IM SDK before using its features.
In most scenarios, you need to initialize the IM SDK only once during the application lifecycle.


## Initialization
You can initialize the SDK in the following steps:
1. Prepare a `SDKAppID`.
2. Set the `SdkConfig`.
3. Set the SDK event listener.
4. Call `InitSDK` to initialize the SDK.

The detailed steps are as follows.

[](id:SDKAppID)
### Preparing a SDKAppID
To perform the initialization, you must have a correct `SDKAppID`.
The `SDKAppID` uniquely identifies a Tencent Cloud IM account. We recommend you apply for a new `SDKAppID` for each application. Messages are naturally isolated and cannot communicate between different `SDKAppID` values.
In the [IM console](https://console.cloud.tencent.com/im), you can view all your `SDKAppID` values, and you can click **Create Application** to create a `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/be7102b9af71190a1ee2194909e461f1.png)


[](id:SDKConfig)
### Setting the SdkConfig

Before initializing the SDK, you need to initialize the [SdkConfig](https://comm.qq.com/im/doc/unity/en/types/SDKSetConfigAttributes/SdkConfig.html) object, which is used to set the local SDK cache and log position.

You need to configure the storage path of the IM runtime logs and data.

### sdk_config_config_file_path

It is the storage path of the local IM data.
>!The application needs read-write access to this path.

### sdk_config_log_file_path

It is the storage path of the IM logs.
>!The application needs read-write access to this path.

### Calling the initialization API
After performing the above steps, you can call `InitSDK` ([c#](https://comm.qq.com/im/doc/unity/en/api/IMSDKInit/Init.html)) to initialize the SDK.

Below is the sample code:

```c#
public static void Init() {
        int sdkappid = 0; // Get the `SDKAppID` from the IM console
        SdkConfig sdkConfig = new SdkConfig();

        sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";

        sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";

        TIMResult res = TencentIMSDK.Init(long.Parse(sdkappid), sdkConfig);
}
```

### Registering a SDK global event listener
After the initialization, SDK will throw such events as connection status and login ticket expiration through the `NetworkStatusListenerCallback`, `UserSigExpiredCallback`, and other callbacks.
We recommend you register a global event listener immediately after calling `initSDK` and perform logic processing in such callbacks.

The callbacks are as described below:

| Event Callback                             | Description                                                                  |
| ------------------------------------------ | ---------------------------------------------------------------------------- |
| RecvNewMsgCallback                         | Callback for receiving a new message                                         |
| MsgReadedReceiptCallback                   | Callback for a message read receipt                                          |
| MsgRevokeCallback                          | Callback for recalling a message                                             |
| MsgElemUploadProgressCallback              | Callback for the upload progress of a message element                        |
| GroupTipsEventCallback                     | Callback for a group system message                                          |
| GroupAttributeChangedCallback              | Callback for a group attribute change                                        |
| ConvTotalUnreadMessageCountChangedCallback | Callback for a change in the unread message count of a conversation          |
| NetworkStatusListenerCallback              | Callback for listening on the network connection status                      |
| KickedOfflineCallback                      | Callback for being kicked offline                                            |
| UserSigExpiredCallback                     | Callback for ticket expiration                                               |
| OnAddFriendCallback                        | Callback for adding a friend                                                 |
| OnDeleteFriendCallback                     | Callback for deleting a friend                                               |
| UpdateFriendProfileCallback                | Callback for updating the profile of a friend                                |
| FriendAddRequestCallback                   | Callback for a friend request                                                |
| FriendApplicationListDeletedCallback       | Callback for deleting a friend request                                       |
| FriendApplicationListReadCallback          | Callback for reading a friend request                                        |
| FriendBlackListAddedCallback               | Callback for adding a friend to the blocklist                                |
| FriendBlackListDeletedCallback             | Callback for removing a friend from the blocklist                            |
| LogCallback                                | Log callback                                                                 |
| MsgUpdateCallback                          | Callback for a message update                                                |
| MsgGroupMessageReadMemberListCallback      | Callback for getting the list of group members who have read a group message |

>! If you receive the `UserSigExpiredCallback` callback, the `UserSig` that you use for login has expired. In this case, you need to use a new `UserSig` to log in again. If you continue to use the expired `UserSig`, the IM SDK will be in an infinite login loop.

### Uninitialization
Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, you don't need to uninitialize the IM SDK before exiting the application.
However, you can uninitialize the IM SDK in special cases, for example, only after you enter a specific UI and no longer use it after exiting the UI.

You can perform the uninitialization by calling the uninitialization API `unInitSDK` ([c#](https://comm.qq.com/im/doc/unity/en/api/IMSDKInit/Uninit.html)).

Below is the sample code:

```c#
// Uninitialize the SDK
TencentIMSDK.Uninit();
```
## Notes
`res` is the result returned when the SDK is called. When it is `TIMResult.TIM_SUCC = 0`, the API is called successfully.

After the SDK is initialized successfully, you need to add the required event listener to avoid missing messages.

[](id:qa)

## FAQs

[](id:qa1)

### 1. You must initialize the IM SDK before using the login, message, group, conversation, relationship chain and profile, and signaling features.


