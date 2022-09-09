## Feature Description

The IM SDK on v6.3 or later provides the user status management feature. Each user has two statuses:

* General status. It is preset in the SDK and cannot be modified.
* Custom status. It can be customized and modified by users. For example, it can be set to "Listening to music" or "On the call".

> ? User status is relevant to the current user but not the device. If an account is logged in on multiple devices at the same time, the status cannot be queried or set by device.

The general user status is available in the following three types:
* Online (ONLINE): The current user has logged in and can receive and send messages.
* Offline (OFFLINE): The user didn't call `logout` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0398924fa1b62a8f5cc9b51673273b48) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f)) to log out, and the persistent connection is disconnected. In general, the user can receive offline push messages.
* Not logged in (UNLOGINED): The user hasn't logged in since registration or has called `logout` to log out.

Keep the following in mind in terms of the offline status:
1. An account will be in the offline status if the application is killed or the network is disconnected abnormally (such as due to 4G/Wi-Fi switch or a weak signal in an elevator) when the application is being logged in.
2. An account will be in the offline status if the application process is killed after the user logs in to the application and clicks the Home button to enter the background. An account will be in the online status if the application process is kept alive in the background.
3. Switching between the online and offline statuses relies on the TCP persistent connection between the IM SDK and the backend. If the client is in airplane mode, the network is completely disconnected, or if not supported by certain device vendors, TCP FIN or RST packets may fail to be sent, and the offline status cannot be switched to immediately. As the backend cannot receive heartbeat packets, it will set the current user status to offline 400 seconds later.

> ! 
>
> - Some of the following features are supported only by the Ultimate edition. Make sure that you have purchased it before use.
> - You need to enable user status in the [IM console](https://console.cloud.tencent.com/im) for some of the following features. Make sure that you have enabled it before use.

[](id:set)

## Setting the Custom Status
Call the `setSelfStatus` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7520045679f1493c890f2b3b5eee7b84) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a7d771431a61635888bdc4def438c4328)) to set a user's own custom status through the `customStatus` field.
If you have called `addIMSDKListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2f0297e96d365013e7923275ce2a5d4e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac569656a58908afba491710a8cb3c8d9)) to add a SDK listener, the `onUserStatusChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94251d1971d7b6692b3278ed0d42b73e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#a8b086c14a9505990c7f5ac053bf45cd6)) will be triggered after the field is set successfully. For more information, see [Status Change Notification](#notify).

The following describes how to clear the custom status:
1. When calling the `setSelfStatus` API, you can leave the `customStatus` field empty to clear the status.
2. When the SDK notices that the current account is in the offline status, it will automatically clear the custom status and trigger the status change notification.

> ? 
> 1. To call `setSelfStatus`, you don't need to upgrade to the Ultimate edition or enable the feature in the console.
> 2. This API can be called an unlimited number of times.

API prototype:
<dx-tabs>
::: Android
```java
/**
 *  API 5.4 for setting a user's own status is supported by the SDK on v6.3 or later.
 *
 *  @param status Custom status to be set
 *
 *  @note Note that this API can only be used to set a user's own custom status, that is, `V2TIMUserStatus.customStatus`.
 */
public abstract void setSelfStatus(V2TIMUserStatus status, V2TIMCallback callback);
```
:::
::: iOS and macOS
```objectivec
/**
 *  API 5.4 for setting a user's own status is supported by the SDK on v6.3 or later.
 *
 *  @param status Custom status to be set
 *
 *  @note Note that this API can only be used to set a user's own custom status, that is, `V2TIMUserStatus.customStatus`.
 */
- (void)setSelfStatus:(V2TIMUserStatus *)status succ:(V2TIMSucc)succ fail:(V2TIMFail)fail;
```
:::
</dx-tabs>

`V2TIMUserStatus` parameter description:

| Field         | Description       | Required | Remarks                           |
| ------------ | ---------- | -------- | ------------------------------ |
| userID       | User ID    | No       | It is read-only and cannot be set.                 |
| statusType   | General status   | No       | It is read-only and cannot be set.                 |
| customStatus | Custom status | No       | When this field is left empty, the custom status will be cleared. |


Sample code:
<dx-tabs>
::: Android
```java
V2TIMUserStatus status = new V2TIMUserStatus();
boolean clearStatus = true;
if (clearStatus) {
  	status.setCustomStatus(null);
} else {
  	status.setCustomStatus("listening music");
}
V2TIMManager.getInstance().setSelfStatus(status, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i(TAG, "setSelfStatus success, CustomStatus is " + customStr);
    }

    @Override
    public void onError(int code, String desc) {
        Log.e(TAG, "setSelfStatus error code = " + code + ",des = " + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMUserStatus *status = [[V2TIMUserStatus alloc] init];
BOOL clearStatus = YES;
if (clearStatus) {
	  status.customStatus = nil;
} else {
  	status.customStatus = @"listening music";
}
[V2TIMManager.sharedInstance setSelfStatus:status succ:^{
	
} fail:^(int code, NSString *desc) {
}];
```
:::
</dx-tabs>


[](id:get)
## Querying the User Status
Call the `getUserStatus` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2428c7f87859dd85bed1730ad8d3b92a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#abe44a4c51c686248d483674d77d71053)) to query the status of the user or another user. The API will return the general status and custom status of the queried user.

API prototype:
<dx-tabs>
::: Android

```java
/**
 *  API 5.3 for querying a user's status is supported only by the SDK on v6.3 or later.
 *
 *  @param userIDList User ID to be obtained
 *
 *  @note Note:
 *  - To query a user's custom status, the user only needs to pass in the `userID`.
 *  - When user statuses are batch queried, the API will return only the statuses that were queried successfully. If the query failed for all the users, the API will report an error.
 */
public abstract void getUserStatus(List<String> userIDList, V2TIMValueCallback<List<V2TIMUserStatus>> callback);
```
:::
::: iOS and macOS
```objectivec
/**
 *  API 5.3 for querying a user's status is supported only by the SDK on v6.3 or later.
 *
 *  @param userIDList User ID to be obtained
 *
 *  @note Note:
 *  - To query a user's custom status, the user only needs to pass in the `userID`.
 *  - When user statuses are batch queried, the API will return only the statuses that were queried successfully. If the query failed for all the users, the API will report an error.
 */
- (void)getUserStatus:(NSArray *)userIDList succ:(V2TIMUserStatusListSucc)succ fail:(V2TIMFail)fail;
```
:::
</dx-tabs>

Parameter:

| Field       | Definition                 | Required | Description                                 |
| ---------- | -------------------- | -------- | ------------------------------------ |
| userIDList | List of IDs of the users to be queried | Yes       | Users only need to pass in their own ID to query their own status. |

[](id:getMyselfStatus)
### Querying a user's own status
Users can set `userIDList` to their own `userID` to query their own status.

> ? 
> 1. To allow users to query their own status, you don't need to upgrade to the Ultimate edition or enable the feature in the console.
> 2. This API can be called an unlimited number of times.

Sample code:
<dx-tabs>
::: Android
```java
String myId = V2TIMManager.getInstance().getLoginUser();
if (myId == null || myId.isEmpty()) {
    // Log in first
    return;
}
List<String> ids = Arrays.asList(myId);
V2TIMManager.getInstance().getUserStatus(ids, new V2TIMValueCallback<List<V2TIMUserStatus>>() {
    @Override
    public void onSuccess(List<V2TIMUserStatus> v2TIMUserStatuses) {
	// Queried the user's own status successfully
    }

    @Override
    public void onError(int code, String desc) {
	// Failed to query the user's own status
    }
});
```
:::
::: iOS and macOS
```objectivec
NSString *myId = V2TIMManager.sharedInstance.getLoginUser;
if (myId == nil || myId.length == 0) {
    // Log in first
    return;
}
[V2TIMManager.sharedInstance getUserStatus:@[myId] succ:^(NSArray<V2TIMUserStatus *> *result) {
    // Queried the user's own status successfully
} fail:^(int code, NSString *desc) {
    // Failed to query the user's own status
}];
```
:::
</dx-tabs>

[](id:getOthersStatus)
### Querying the status of another user
A user can set `userIDList` to the list of the `userID` values of other users to query their statuses.

To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

To use this feature, you need to enable **Set user status query and status change notification** in the [IM console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `getUserStatus` is called.

![](https://qcloudimg.tencent-cloud.cn/raw/56bd5984c43961f2ac62b45468d72441.png)



> ? By default, this API can be called 20 times every five seconds, and the statuses of up to 500 users can be queried at a time.

Sample code:
<dx-tabs>
::: Android
```java
List<String> ids = Arrays.asList("userid1", "userid2", "userid3");
V2TIMManager.getInstance().getUserStatus(ids, new V2TIMValueCallback<List<V2TIMUserStatus>>() {
    @Override
    public void onSuccess(List<V2TIMUserStatus> v2TIMUserStatuses) {
	// Queried the status successfully
    }

    @Override
    public void onError(int code, String desc) {
	// Failed to query the status
    }
});
```
:::
::: iOS and macOS
```objectivec
[V2TIMManager.sharedInstance getUserStatus:@[@"userid1", @"userid2", @"userid3"] succ:^(NSArray<V2TIMUserStatus *> *result) {
    // Queried the status successfully
} fail:^(int code, NSString *desc) {
    // Failed to query the status
}];
```
:::
</dx-tabs>


[](id:subscribe)
## Subscribing to the User Status
Call the `subscribeUserStatus` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9c6deb154d0042d5472ec55cfe0962bb) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20e6cbe409549e0d2ff62be76914e0b3)) to subscribe to the status of the specified user. By default, the IM SDK supports subscribing to the statuses of up to 200 users. After this limit is exceeded, the earliest subscribed user statuses will be removed.
When the user status (including general status and custom status) subscribed to changes, the status change notification can be received in the `onUserStatusChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94251d1971d7b6692b3278ed0d42b73e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#a8b086c14a9505990c7f5ac053bf45cd6)).

API features:

1. This API doesn't support subscribing to a user's own status, which can be obtained in the `onUserStatusChanged` callback. For more information, see [Status Change Notification](#notify).

2. This API supports subscribing to the status of a friend, which will occupy the quota of 200 mentioned above.
   * To get the changes in the statuses of all of a user's friends, you don't need to call this API, and you can enable automatic notifications of friends' statuses in the [IM console](https://console.cloud.tencent.com/im), after which a status change notification can be received in the `onUserStatusChanged` callback.
   
   * To get the changes in the statuses of some of a user's friends, you can only call `subscribeUserStatus` for subscription, after which a status change notification can be received in the `onUserStatusChanged` callback.


To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

To use this feature, you need to enable **Set user status query and status change notification** in the [IM console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `subscribeUserStatus` is called.


> ? By default, this API can be called 20 times every five seconds, and the statuses of up to 100 users can be subscribed to at a time.

API prototype:
<dx-tabs>
::: Android
```java
/**
 *  API 5.5 for subscribing to a user's status is supported by the SDK on v6.3 or later.
 *
 *  @param userIDList ID of the user to be subscribed to
 *
 *  @note Note:
 *   - After the status of a user is subscribed to successfully, when the user's status (including the online status and custom status) changes, the change can be obtained in the `@onUserStatusChanged` callback.
 *   - To enable users to subscribe to the status of their contacts, you only need to enable the feature in the console and don't need to call this API.
 *   - This API doesn't support subscribing to a user's own status, which can be obtained in the `@onUserStatusChanged` callback.
 *   - The number of user statuses that can be subscribed to is limited. After this limit is exceeded, the earliest subscribed user statuses will be automatically removed.
 */
public abstract void subscribeUserStatus(List<String> userIDList, V2TIMCallback callback);
```
:::
::: iOS and macOS
```objectivec
/**
 *  API 5.5 for subscribing to a user's status is supported by the SDK on v6.3 or later.
 *
 *  @param userIDList ID of the user to be subscribed to
 *
 *  @note Note:
 *   - After the status of a user is subscribed to successfully, when the user's status (including the online status and custom status) changes, the change can be obtained in the `@onUserStatusChanged` callback.
 *   - To enable users to subscribe to the status of their contacts, you only need to enable the feature in the console and don't need to call this API.
 *   - This API doesn't support subscribing to a user's own status, which can be obtained in the `@onUserStatusChanged` callback.
 *   - The number of user statuses that can be subscribed to is limited. After this limit is exceeded, the earliest subscribed user statuses will be automatically removed.
 */
- (void)subscribeUserStatus:(NSArray *)userIDList succ:(V2TIMSucc)succ fail:(V2TIMFail)fail;
```
:::
</dx-tabs>

Sample code:
<dx-tabs>
::: Android
```java
List<String> useridList = Arrays.asList("userid1", "userid2", "userid3");
V2TIMManager.getInstance().subscribeUserStatus(useridList, new V2TIMCallback() {
    @Override
    public void onSuccess() {
		// Subscribed to the status successfully
    }

    @Override
    public void onError(int code, String desc) {
		// Failed to subscribe to the status
    }
});
```
:::
::: iOS and macOS
```objectivec
[V2TIMManager.sharedInstance subscribeUserStatus:@[@"userid1", @"userid2", @"userid3"] succ:^ {
		// Subscribed to the status successfully
} fail:^(int code, NSString *desc) {
		// Failed to subscribe to the status
}];
```
:::
</dx-tabs>

[](id:unsubscribe)
## Unsubscribing from the User Status
To stop receiving notifications of changes in user statuses, call the `unsubscribeUserStatus` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9254db13bd53dc48a04d05ba5f116d39) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a3780734bb50398ebe65155c3223542f0)) to unsubscribe from the user status or clear the subscription list.
If you don't want the subscription list to be cleared manually, after the account goes offline or is logged out, the IM SDK will clear it after a certain period of time by default.

To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

To use this feature, you need to enable **Set user status query and status change notification** in the [IM console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `unsubscribeUserStatus` is called.

> ? By default, this API can be called 20 times every five seconds, and the statuses of up to 100 users can be unsubscribed from at a time.

API prototype:
<dx-tabs>
::: Android
```java
/**
 *  API 5.6 for unsubscribing from a user's status is supported by the SDK on v6.3 or later.
 *
 *  @note
 *   - When `userIDList` is left empty or set to `nil`, it indicates to unsubscribe from all the current subscribed user statuses.
 */
public abstract void unsubscribeUserStatus(List<String> userIDList, V2TIMCallback callback);
```
:::
::: iOS and macOS
```objectivec
/**
 *  API 5.6 for unsubscribing from a user's status is supported by the SDK on v6.3 or later.
 *
 *  @note
 *   - When `userIDList` is left empty or set to `nil`, it indicates to unsubscribe from all the current subscribed user statuses.
 */
- (void)unsubscribeUserStatus:(NSArray *)userIDList succ:(V2TIMSucc)succ fail:(V2TIMFail)fail;
```
:::
</dx-tabs>

Sample code:
<dx-tabs>
::: Android
```java
List<String> useridList = Arrays.asList("userid1", "userid2", "userid3");
V2TIMManager.getInstance().unsubscribeUserStatus(useridList, new V2TIMCallback() {
    @Override
    public void onSuccess() {
		// Unsubscribed from the status successfully
    }

    @Override
    public void onError(int code, String desc) {
		// Failed to unsubscribe from the status
    }
});
```
:::
::: iOS
```objectivec
[V2TIMManager.sharedInstance unsubscribeUserStatus:@[@"userid1", @"userid2", @"userid3"] succ:^ {
		// Unsubscribed from the status successfully
} fail:^(int code, NSString *desc) {
		// Failed to unsubscribe from the status
}];
```
:::
</dx-tabs>


[](id:notify)
## Status Change Notification
Depending on the user type, status changes can be divided into three types:
1. Change in a user's own status.
2. Change in a friend's status.
3. Change in a non-friend user's status.

Notifications of the above three types of status changes are returned in the `onUserStatusChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94251d1971d7b6692b3278ed0d42b73e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#a8b086c14a9505990c7f5ac053bf45cd6)).
Callback prototype:
<dx-tabs>
::: Android

```java
/**
 * User status change notification
 *
 * @note Notification receiving:
 * 1. This callback will be triggered if a subscribed user status (including online status and custom status) changes.
 * 2. This callback will be triggered when a friend's status changes after notifications of friends' statuses are enabled in the IM console, even if the status has not been subscribed to.
 * 3. This callback will be sent to all the devices when an account is logged in on them and the custom status is changed on one of them.
 */
public void onUserStatusChanged(List<V2TIMUserStatus> userStatusList){}
```
:::
::: iOS and macOS
```objectivec
/**
 * User status change notification
 *
 * @note Notification receiving:
 * 1. This callback will be triggered if a subscribed user status (including online status and custom status) changes.
 * 2. This callback will be triggered when a friend's status changes after notifications of friends' statuses are enabled in the IM console, even if the status has not been subscribed to.
 * 3. This callback will be sent to all the devices when an account is logged in on them and the custom status is changed on one of them.
 */
- (void)onUserStatusChanged:(NSArray<V2TIMUserStatus *> *)userStatusList;
```
:::
</dx-tabs>

Although all the status notifications are returned in the `onUserStatusChanged` callback, they are triggered in different ways for different user types.

### Notification of a change in a user's own status
If you have called `addIMSDKListener` to add an SDK listener, after a user's own status is set successfully, when the status changes, the `onUserStatusChanged` callback will be triggered, where the user can get the latest own status.

### Notification of a change in a friend's status
1. If you have enabled automatic notifications of friends' statuses in the [IM console](https://console.cloud.tencent.com/im), when the status of a user's friend changes, the `onUserStatusChanged` callback will be automatically triggered, where the latest status of the friend can be obtained.

2. If you don't enable automatic notifications of friends' statuses and want to get friends' status changes, you need to call `subscribeUserStatus` to subscribe to friends' statuses. When a friend's status changes, the `onUserStatusChanged` callback will be automatically triggered.


> ! To use `subscribeUserStatus`, you need to purchase the Ultimate edition and enable the feature in the console. For more information, see [Subscribing to the User Status](#subscribe).

3. If you neither enable automatic notifications of friends' statuses nor call `subscribeUserStatus` to subscribe to friends' statuses, changes in friends' statuses cannot be obtained.

### Change in a non-friend user's status
To get the change in a non-friend user's status, you can only call `subscribeUserStatus` to subscribe to the status. When the user's status changes, the `onUserStatusChanged` callback will be triggered, where the user can get the latest status of the non-friend user.

> ! To use `subscribeUserStatus`, you need to purchase the Ultimate edition and enable the feature in the console. For more information, see [Subscribing to the User Status](#subscribe).

Sample code:
<dx-tabs>
::: Android
```java
private void initListener() {
    V2TIMSDKListener v2TIMSDKListener = new V2TIMSDKListener() {
        @Override
        public void onUserStatusChanged(List<V2TIMUserStatus> userStatusList) {
            String myID = V2TIMManager.getInstance().getLoginUser();
            for (V2TIMUserStatus item : userStatusList) {
                if (item.getUserID().equals(myID)) {
                    // The user's own status changed.
                } else {
                    // The status of another user changed.
                }
            }
        }
    };
    V2TIMManager.getInstance().addIMSDKListener(v2TIMSDKListener);
}
```
:::
::: iOS and macOS
```objectivec
// Add a listener
[V2TIMManager.sharedInstance addIMSDKListener:self];

// Notification callback
- (void)onUserStatusChanged:(NSArray<V2TIMUserStatus *> *)userStatusList {
    NSString *myID = V2TIMManager.sharedInstance.getLoginUser;
    for (V2TIMUserStatus *userStatus in userStatusList) {
        if ([userStatus.userID isEqualToString:myID]) {
            // The user's own status changed.
        } else {
            // The status of another user changed.
        }
    }
}
```
:::
</dx-tabs>

> ? The user status can not only be obtained through `onUserStatusChanged` as described above, but also be queried as instructed in [Querying the User Status](get).

### Multi-client sync of status change notifications
If you have enabled multi-client login (for more information, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419)), an account can be logged in on different clients. When the status of the user logged in on one of the clients changes, the backend will send the `onUserStatusChanged` notification ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94251d1971d7b6692b3278ed0d42b73e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#a8b086c14a9505990c7f5ac053bf45cd6)) to other logged-in clients.

[](id:limit)

## API Restrictions

### Plan restrictions
* You don't need to upgrade to the Ultimate edition to use the `setSelfStatus` API.
* You don't need to upgrade to the Ultimate edition to use the `getUserStatus` API to query a user's own status.
* You need to upgrade to the Ultimate edition to use the `getUserStatus` API to query another user's status.
* You need to upgrade to the Ultimate edition to use the `subscribe` / `unsubscribe` API.


### API call frequency limit
* The `setSelfStatus` API can be called an unlimited number of times.
* The `getUserStatus` API is used to query a user's own status and can be called an unlimited number of times.
* By default, the `getUserStatus` API can be called 20 times every five seconds if used to query the status of another user, and the statuses of up to 500 users can be queried at a time.
* By default, the `subscribe` API can be called 20 times every five seconds, and the statuses of up to 100 users can be subscribed to at a time.
* By default, the `unsubscribe` API can be called 20 times every five seconds, and up to 100 users can be unsubscribed from at a time.



## FAQs

### What should I do if error code 72001 is reported when I call the subscribe/unsubscribe API?

Error code 72001 indicates that the feature is not enabled in the console. You need to log in to the [IM console](https://console.cloud.tencent.com/im) and enable the feature.


