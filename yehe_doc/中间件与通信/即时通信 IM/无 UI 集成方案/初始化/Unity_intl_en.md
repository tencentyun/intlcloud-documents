## Overview
You **must** initialize the IM SDK before using its features.
In most scenarios, you need to initialize the IM SDK only once during the application lifecycle.


## Initialization
You can initialize the SDK in the following steps:
1. Prepare an `SDKAppID`.
2. Set the `SdkConfig`.
3. Set the SDK event listener.
4. Call [`Init`](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Init.html) to initialize the SDK.

The detailed steps are as follows.

[](id:SDKAppID)
### Preparing an SDKAppID
To perform the initialization, you must have a correct `SDKAppID`.
`SDKAppID` is the unique ID that the IM service uses to identify a customer account. We recommend you apply for a new `SDKAppID` for every independent app to automatically isolate messages between `SDKAppIDs`.
You can view all `SDKAppIDs` in the [IM console](https://console.cloud.tencent.com/im) or click **Create Application** to create an `SDKAppID`.


[](id:SDKConfig)
### Setting the SdkConfig

Before initializing the SDK, you need to initialize the [SdkConfig](https://comm.qq.com/im/doc/unity/zh/types/SDKSetConfigAttributes/SdkConfig.html) object, which is used to set the local SDK cache and log position.

It is used to configure the storage path of IM running logs and data.

### sdk_config_config_file_path

Storage path of local IM data.
>! The app needs to have read-write access to this path.

### sdk_config_log_file_path

It is the storage path of the IM logs.
>! The app needs to have read-write access to this path.

### Calling the initialization API
After performing the above steps, you can call [`Init`](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Init.html) to initialize the SDK.

Sample code:

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
After the initialization, SDK will throw such events as connection status and login ticket expiration through the [`NetworkStatusListenerCallback`](https://comm.qq.com/im/doc/unity/zh/callback/NetworkStatusListenerCallback.html), [`UserSigExpiredCallback`](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html), and other callbacks.
We recommend you register a global event listener immediately after calling `initSDK` and perform logic processing in such callbacks.

The callbacks are as described below:

| Event Callback                                               | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [RecvNewMsgCallback](https://comm.qq.com/im/doc/unity/zh/callback/RecvNewMsgCallback.html) | Callback for receiving a new message                         |
| [MsgReadedReceiptCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgReadedReceiptCallback.html) | Callback for a message read receipt                          |
| [MsgRevokeCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgRevokeCallback.html) | Callback for a message recall                                |
| [MsgElemUploadProgressCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgElemUploadProgressCallback.html) | Callback for the upload progress of a message element        |
| [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/zh/callback/GroupTipsEventCallback.html) | Callback for a group system message                          |
| [GroupAttributeChangedCallback](https://comm.qq.com/im/doc/unity/zh/callback/GroupAttributeChangedCallback.html) | Callback for a group attribute change                        |
| [ConvTotalUnreadMessageCountChangedCallback](https://comm.qq.com/im/doc/unity/zh/callback/ConvTotalUnreadMessageCountChangedCallback.html) | Callback for a change in the unread message count of a conversation |
| [NetworkStatusListenerCallback](https://comm.qq.com/im/doc/unity/zh/callback/NetworkStatusListenerCallback.html) | Callback for listening for the network connection status     |
| [KickedOfflineCallback](https://comm.qq.com/im/doc/unity/zh/callback/KickedOfflineCallback.html) | Callback for being kicked offline                            |
| [UserSigExpiredCallback](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html) | Callback for ticket expiration                               |
| [OnAddFriendCallback](https://comm.qq.com/im/doc/unity/zh/callback/OnAddFriendCallback.html) | Callback for adding a friend                                 |
| [OnDeleteFriendCallback](https://comm.qq.com/im/doc/unity/zh/callback/OnDeleteFriendCallback.html) | Callback for deleting a friend                               |
| [UpdateFriendProfileCallback](https://comm.qq.com/im/doc/unity/zh/callback/UpdateFriendProfileCallback.html) | Callback for updating the profile of a friend                |
| [FriendAddRequestCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendAddRequestCallback.html) | Callback for a friend request                                |
| [FriendApplicationListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListDeletedCallback.html) | Callback for deleting a friend request                       |
| [FriendApplicationListReadCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListReadCallback.html) | Callback for reading a friend request                        |
| [FriendBlackListAddedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendBlackListAddedCallback.html) | Callback for adding a friend to the blocklist                |
| [FriendBlackListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendBlackListDeletedCallback.html) | Callback for deleting a friend from the blocklist            |
| [LogCallback](https://comm.qq.com/im/doc/unity/zh/callback/LogCallback.html) | Log callback                                                 |
| [MsgUpdateCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgUpdateCallback.html) | Callback for a message update                                |
| [MsgGroupMessageReadMemberListCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgGroupMessageReadMemberListCallback.html) | Callback for getting the list of group members who have read a group message |

>! If you receive the [`UserSigExpiredCallback`](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html) callback, the `UserSig` that you use for login has expired. In this case, you need to use the newly issued `UserSig` to log in again. If you continue to use the expired `UserSig`, the IM SDK will enter an infinite login loop.

// Uninitialization
Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, you don't need to uninitialize the IM SDK before exiting the application.
However, you can uninitialize the IM SDK in special cases, for example, only after you enter a specific UI and no longer use it after exiting the UI.

You can perform the uninitialization by calling the uninitialization API [`unInit`](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Uninit.html).

Sample code:

```c#
// Uninitialize the SDK
TencentIMSDK.Uninit();
```
## Others
It is used to display the result returned when the SDK is called. When `res` is `TIMResult.TIM_SUCC = 0`, the API call is successful.

After the SDK is successfully initialized, add required listeners to avoid missing messages.

[](id:qa)

## FAQs

[](id:qa1)

### 1. You must initialize the IM SDK before using the login, message, group, conversation, relationship chain and profile, and signaling features.
