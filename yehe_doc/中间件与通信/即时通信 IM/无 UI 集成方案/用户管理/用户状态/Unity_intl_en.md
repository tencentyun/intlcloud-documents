## Overview

The native SDK on v6.3 or later provides the user status management feature. Each user has two statuses:

* General status. It is preset in the SDK and cannot be modified.
* Custom status. It can be customized and modified by users. For example, it can be set to "Listening to music" or "On the call".

> ? User status is relevant to the current user but not the device. If an account is logged in on multiple devices at the same time, the status cannot be queried or set.

The general user status is available in the following three types:
* Online (ONLINE): The current user has logged in and can receive and send messages.
* Offline (OFFLINE): The user didn't call `logout` ([details](https://comm.qq.com/im/doc/unity/zh/api/loginOrlogout/Logout.html)) to log out, and the persistent connection is disconnected. In general, the user can receive offline push messages.
* Not logged in (UNLOGINED): The user hasn't logged in since registration or has called `logout` to log out.

Keep the following in mind in terms of the offline status:
1. An account will be in the offline status if the application is killed or the network is disconnected abnormally (such as due to 4G/Wi-Fi switch or a weak signal in an elevator) when the application is being logged in.
2. An account will be in the offline status if the application process is killed after the user logs in to the application and clicks the Home button to enter the background. An account will be in the online status if the application process is kept alive in the background.
3. Switching between the online and offline statuses relies on the TCP persistent connection between the Chat SDK and the backend. If the client is in airplane mode, the network is completely disconnected, or if not supported by certain device vendors, TCP FIN or RST packets may fail to be sent, and the offline status cannot be switched to immediately. As the backend cannot receive heartbeat packets, it will set the current user status to offline 400 seconds later.

> !
>
> - **Some of the following features** are supported only by the Ultimate edition. Make sure that you have purchased it before use.
> - You need to enable user status in the [Chat console](https://console.cloud.tencent.com/im) for **some of the following features**. Make sure that you have enabled it before use.

[](id:set)

## Setting the Custom Status
Call the `SetSelfStatus` API ([details](https://comm.qq.com/im/doc/unity/zh/api/UserApi/SetSelfStatus.html)) to set a user's own custom status through the `current_user_status` field.
If you have called `SetUserStatusChangedCallback` ([details](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetUserStatusChangedCallback.html)) to add a SDK listener, the `UserStatusChangedCallback` callback ([details](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)) will be triggered after the field is set successfully.
For how to use `UserStatusChangedCallback`, see [Status Change Notification](#notify).

The following describes how to clear the custom status:
1. When calling the `SetSelfStatus` API, you can leave the `current_user_status` field empty to clear the status.
2. When the SDK notices that the current account is in the offline status, it will automatically clear the custom status and trigger the status change notification.

> ?
> 1. To call `SetSelfStatus`, you don't need to upgrade to the Ultimate edition or enable the feature in the console.
> 2. This API can be called an unlimited number of times.

Sample code:

```c#
    // Set user status
    UserStatus status = new UserStatus
    {
      user_status_identifier = "userID",
      user_status_status_type = TIMUserStatusType.kTIMUserStatusType_Online
    };
    TIMResult res = TencentIMSDK.SetSelfStatus(status, (int code, string desc, string result, string user_data)=>{
      // Async result of the user status setting
    });
```


[](id:get)
## Querying the User Status
Call the `GetUserStatus` API ([details](https://comm.qq.com/im/doc/unity/zh/api/UserApi/GetUserStatus.html)) to query the status of the current user or another user. The API will return the general status and custom status of the queried user.

[](id:getMyselfStatus)
### Querying a user's own status
A user can call `GetUserStatus` with `identifier_array` containing only the user's own userID to query the user's own status.

> ?
> 1. To allow users to query their own status, you don't need to upgrade to the Ultimate edition or enable the feature in the console.
> 2. This API can be called an unlimited number of times.

Sample code:

```c#
  // Query user status
    TIMResult res = TencentIMSDK.GetUserStatus(new List<string> {"userID1"}, (int code, string desc, List<UserStatus> results, string user_data)=>{
      // Async result of the user status query
    });
```

[](id:getOthersStatus)
### Querying the status of another user
A user can set `identifier_array` to the list of the userIDs of other users to query their statuses.

> ?
> 1. To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
> 2. To use this feature, you need to enable **Set user status query and status change notification** in the [Chat console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `GetUserStatus` is called.
> <img src="https://qcloudimg.tencent-cloud.cn/raw/1adfc878b14e6a6a62de3a7db159b0a6.png" style="zoom:30%;"/>
> 3. By default, this API can be called 20 times every five seconds, and the statuses of up to 500 users can be queried at a time.

[](id:subscribe)
## Subscribing to the User Status
Call the `SubscribeUserStatus` API ([details](https://comm.qq.com/im/doc/unity/zh/api/UserApi/SubscribeUserStatus.html)) to subscribe to the status of the specified user. By default, the Chat SDK supports subscribing to the statuses of up to 200 users. After this limit is exceeded, the earliest subscribed user statuses will be removed.
When the user status (including general status and custom status) subscribed to changes, the status change notification can be received in the `UserStatusChangedCallback` callback ([details](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)).

API features:

1. This API doesn't support subscribing to a user's own status, which can be obtained in the `UserStatusChangedCallback` callback. For more information, see [Status Change Notification](#notify).
2. This API supports subscribing to the status of a friend, which will occupy the quota of 200 mentioned above.
 * To get the changes in the statuses of all of a user's friends, you don't need to call this API, and you can enable automatic notifications of friends' statuses in the [Chat console](https://console.cloud.tencent.com/im), after which a status change notification can be received in the `UserStatusChangedCallback` callback.
The following figure shows the switch for the automatic notification of friends' statuses.
<img src="https://qcloudimg.tencent-cloud.cn/raw/17b70799301407e46b14ca144646eb98.png" style="zoom:30%;"/>
 * To get the changes in the statuses of some of a user's friends, you can only call `SubscribeUserStatus` for subscription, after which a status change notification can be received in the `UserStatusChangedCallback` callback.

> ?
> 1. To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
> 2. To use this feature, you need to enable **Set user status query and status change notification** in the [Chat console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `SubscribeUserStatus` is called.
> <img src="https://qcloudimg.tencent-cloud.cn/raw/1adfc878b14e6a6a62de3a7db159b0a6.png" style="zoom:30%;"/>
> 3. By default, this API can be called 20 times every five seconds, and the statuses of up to 100 users can be subscribed to at a time.

Sample code:
```c#
    // Subscribe to the user status
    TIMResult res = TencentIMSDK.SubscribeUserStatus(new List<string> {"userID1"}, (int code, string desc, string result, string user_data)=>{
      // Async result of the user status subscription
    });
```

[](id:unsubscribe)
## Unsubscribing from the User Status
To stop receiving notifications of changes in user statuses, call the `UnsubscribeUserStatus` API ([details](https://comm.qq.com/im/doc/unity/zh/api/UserApi/UnsubscribeUserStatus.html)) to unsubscribe from the user status or clear the subscription list.
If you don't clear the subscription list manually, after the account goes offline or is logged out, the Chat SDK will clear it after a certain period of time by default.

The use limits of the API for unsubscribing from the user status are consistent with those of the [API for subscribing to the user status](#subscribe).

Sample code:

```c#
    // Unsubscribe from the user status
    TIMResult res = TencentIMSDK.UnsubscribeUserStatus(new List<string> {"userID1"}, (int code, string desc, string result, string user_data)=>{
      // Async result of the user status unsubscription
    });
```


[](id:notify)
## Status Change Notification
Depending on the user status type, status changes can be divided into three types:
1. Change in a user's own status.
2. Change in a friend's status.
3. Change in a non-friend user's status.

Notifications on all these status changes can be called back through the `UserStatusChangedCallback` callback ([details](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)), which is triggered in different ways for different user types.

### Notification of a change in a user's own status
If you have called SetUserStatusChangedCallback` to add an SDK listener, after a user's own status is set successfully, when the status changes, the `UserStatusChangedCallback` callback will be triggered, where the user can get the latest own status.

### Notification of a change in a friend's status
1. If you have enabled automatic notifications of friends' statuses in the [Chat console](https://console.cloud.tencent.com/im), when the status of a user's friend changes, the `UserStatusChangedCallback` callback will be automatically triggered.
2. If you don't enable automatic notifications of friends' statuses but still want to get friends' status changes, you need to call `SubscribeUserStatus` to subscribe to friends' statuses. When a friend's status changes, the `UserStatusChangedCallback` callback will be automatically triggered.
For the use limits of `SubscribeUserStatus`, refer to [Subscribing to the User Status](#subscribe).
3. If you neither enable automatic notifications of friends' statuses nor call `SubscribeUserStatus` to subscribe to friends' statuses, changes in friends' statuses cannot be obtained.

### Change in a non-friend user's status
To get the change in a non-friend user's status, you can only call `SubscribeUserStatus` to subscribe to the status. When the user's status changes, the `UserStatusChangedCallback` callback will be triggered.
For the use limits of `SubscribeUserStatus`, refer to [Subscribing to the User Status](#subscribe).

Sample code:

```c#
    // Set the user status change notification callback
    TencentIMSDK.SetUserStatusChangedCallback((List<UserStatus> json_user_status_array, string user_data)=>{
      // Process the callback logic
    });
```

### Multi-client sync of status change notifications
If you have enabled multi-device login ([details](https://intl.cloud.tencent.com/document/product/1047/34419)), an account can be logged in on different devices. When the status of the user logged in on one of the devices changes, the backend will send the `UserStatusChangedCallback` notification ([details](https://comm.qq.com/im/doc/unity/zh/callback/UserStatusChangedCallback.html)) to other logged-in devices.

[](id:limit)

## API Restrictions

### Plan restrictions
* You don't need to upgrade to the Ultimate edition to use the `SetSelfStatus` API.
* You don't need to upgrade to the Ultimate edition to use the `GetUserStatus` API to query a user's own status.
* You need to upgrade to the Ultimate edition to use the `GetUserStatus` API to query another user's status.
* You need to upgrade to the Ultimate edition to use the `SubscribeUserStatus`/`UnsubscribeUserStatus` API.


### API call frequency limit
* The `SetSelfStatus` API can be called an unlimited number of times.
* The `GetUserStatus` API is used to query a user's own status and can be called an unlimited number of times.
* By default, the `GetUserStatus` API can be called 20 times every five seconds if used to query the status of another user, and the statuses of up to 500 users can be queried at a time.
* By default, the `SubscribeUserStatus` API can be called 20 times every five seconds, and the statuses of up to 100 users can be subscribed to at a time.
* By default, the `UnsubscribeUserStatus` API can be called 20 times every five seconds, and up to 100 users can be unsubscribed from at a time.


## FAQs

### What should I do if error code 72001 is reported when I call the subscribe/unsubscribe API?

Error code 72001 indicates that the feature is not enabled in the console. You need to log in to the [Chat console](https://console.cloud.tencent.com/im) and enable the feature.
