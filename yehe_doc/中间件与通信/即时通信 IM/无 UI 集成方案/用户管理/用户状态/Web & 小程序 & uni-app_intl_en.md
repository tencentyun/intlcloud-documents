## Feature Description

The IM SDK for web on v2.21.0 or later provides the user status management feature. Each user has two statuses:

* General status. It is preset in the SDK and cannot be modified.
* Custom status. It can be customized and modified by users. For example, it can be set to "Listening to music" or "On the call".

> ? User status is relevant to the current user but not the device. If an account is logged in on multiple devices at the same time, the status cannot be queried or set by device.

The general user status is available in the following three types:
* Online ([TIM.TYPES.USER_STATUS_ONLINE](https://web.sdk.qcloud.com/im/doc/zh-cn/module-TYPES.html#.USER_STATUS_ONLINE)): The current user has logged in and can receive and send messages.
* Offline ([TIM.TYPES.USER_STATUS_OFFLINE](https://web.sdk.qcloud.com/im/doc/zh-cn/module-TYPES.html#.USER_STATUS_OFFLINE)): The offline status will not be triggered when the SDK for web is logged in/out. It will be triggered in the application with the IM SDK for React Native.
* Not logged in ([TIM.TYPES.USER_STATUS_UNLOGINED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-TYPES.html#.USER_STATUS_UNLOGINED)): The user hasn't logged in since registration or has called `logout` to log out.

> ! 
>
> - Some of the following features are supported only by the Ultimate edition. Make sure that you have purchased it before use.
> - You need to enable user status in the [IM console](https://console.cloud.tencent.com/im) for some of the following features. Make sure that you have enabled it before use.

[](id:set)
## Setting the Custom Status
Call the [setSelfStatus](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setSelfStatus) API to set a user's own custom status through the `customStatus` field. Then, notifications of a change in the user's own custom status will be received through the [TIM.EVENT.USER_STATUS_UPDATED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.USER_STATUS_UPDATED) event. For more information, see [Status Change Notification](#notify).

The following describes how to clear the custom status:
1. When calling the `setSelfStatus` API, you can leave the `customStatus` field empty to clear the status.
2. A period of time after the account logs out of the SDK for web, the IM backend will automatically clear the custom status and trigger the status change notification.

> ? 
> 1. To call `setSelfStatus`, you don't need to upgrade to the Ultimate edition or enable the feature in the console.
> 2. This API can be called an unlimited number of times.

**API**

<dx-codeblock>
:::  js

tim.setSelfStatus(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name         | Type   | Description        |
| ------------ | ------ | ------------------ |
| customStatus | String | Custom user status |


**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Set `customStatus` to the empty string `''` to clear the user's own custom status
let promise = tim.setSelfStatus({customStatus: 'xxx'});
promise.then(function(imResponse) {
  console.log(imResponse.data);
  const { userID, statusType, customStatus } = imResponse.data;
  // userID - User ID
  // statusType - User status. The enumerated values are described as follows:
  // TIM.TYPES.USER_STATUS_UNKNOWN - Unknown
  // TIM.TYPES.USER_STATUS_ONLINE - Online
  // TIM.TYPES.USER_STATUS_OFFLINE - Offline
  // TIM.TYPES.USER_STATUS_UNLOGINED - Not logged in
  // customStatus - Custom user status
}).catch(function(imError) {
  console.warn('setSelfStatus error:', imError); // Failed to set the user's own custom status
});

:::
</dx-codeblock>

[](id:get)
## Querying the User Status
Call the [getUserStatus](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getUserStatus) API to query the status of the user or another user. The API will return the general status and custom status of the queried user.

**API**

<dx-codeblock>
:::  js

tim.getUserStatus(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type  | Description                                                  |
| ---------- | ----- | ------------------------------------------------------------ |
| userIDList | Array | List of the `userID` values to be queried. Users only need to pass in their own `userID` to query their own status. |

**Returned value**

`Promise` object.

[](id:getMyselfStatus)
### Querying a user's own status
Users can set `userIDList` to their own `userID` to query their own status.

> ? 
> 1. To allow users to query their own status, you don't need to upgrade to the Ultimate edition or enable the feature in the console.
> 2. This API can be called an unlimited number of times.

**Sample**

<dx-codeblock>
:::  js

// Query the user's own status
// When `userIDList` contains only the user's own `userID`, it indicates to query only the user's own status.
let promise = tim.getUserStatus({userIDList: [`${myUserID}`]});
promise.then(function(imResponse) {
   const { successUserList } = imResponse.data;
   successUserList.forEach((item) => {
     const { userID, statusType, customStatus } = item;
     // userID - User ID
     // statusType - User status. The enumerated values are described as follows:
     // TIM.TYPES.USER_STATUS_UNKNOWN - Unknown
     // TIM.TYPES.USER_STATUS_ONLINE - Online
     // TIM.TYPES.USER_STATUS_OFFLINE - Offline
     // TIM.TYPES.USER_STATUS_UNLOGINED - Not logged in
     // customStatus - Custom user status
   });
}).catch(function(imError) {
  console.warn('getUserStatus error:', imError); // Failed to obtain the user status
});

:::
</dx-codeblock>

[](id:getOthersStatus)
### Querying the status of another user
A user can set `userIDList` to the list of the `userID` values of other users to query their statuses.

To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

To use this feature, you need to enable **Set user status query and status change notification** in the [IM console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `getUserStatus` is called.

![](https://qcloudimg.tencent-cloud.cn/raw/56bd5984c43961f2ac62b45468d72441.png)

> ? By default, this API can be called 20 times every five seconds, and the statuses of up to 500 users can be queried at a time.

**Sample**

<dx-codeblock>
:::  js

// Query the status of another user
let promise = tim.getUserStatus({userIDList: ['user0', 'user1']});
promise.then(function(imResponse) {
   const { successUserList, failureUserList } = imResponse.data;
   // List of `userID` values of the users whose statuses were queried successfully
   successUserList.forEach((item) => {
     const { userID, statusType, customStatus } = item;
     // userID - User ID
     // statusType - User status. The enumerated values are described as follows:
     // TIM.TYPES.USER_STATUS_UNKNOWN - Unknown
     // TIM.TYPES.USER_STATUS_ONLINE - Online
     // TIM.TYPES.USER_STATUS_OFFLINE - Offline
     // TIM.TYPES.USER_STATUS_UNLOGINED - Not logged in
     // customStatus - Custom user status
   });

   // List of `userID` values of the users whose statuses failed to be queried
   failureUserList.forEach((item) => {
     const { userID, code, message } = item;
     // userID - `userID` of the user whose status failed to be queried
     // code - Error code for the failed query
     // message - Error message for the failed query
   });
}).catch(function(imError) {
  console.warn('getUserStatus error:', imError); // Failed to obtain the user status
});

:::
</dx-codeblock>

[](id:subscribe)
## Subscribing to the User Status
Call the [subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#subscribeUserStatus) API to subscribe to the status of the specified user.
When the user status (including general status and custom status) subscribed to changes, the status change notification can be received through the [TIM.EVENT.USER_STATUS_UPDATED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.USER_STATUS_UPDATED) event.

API features:

1. This API doesn't support subscribing to a user's own status, which can be obtained through the [TIM.EVENT.USER_STATUS_UPDATED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.USER_STATUS_UPDATED) event. For more information, see [Status Change Notification](#notify).

2. This API supports subscribing to the status of a friend, which will occupy the subscription quota assigned by the IM backend.
   * To get the changes in the statuses of all of a user's friends, you don't need to call this API, and you can enable automatic notifications of friends' statuses in the [IM console](https://console.cloud.tencent.com/im), after which a friend status change notification can be received through the [TIM.EVENT.USER_STATUS_UPDATED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.USER_STATUS_UPDATED) callback.
   
   * To get the changes in the statuses of some of a user's friends, you can only call [subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#subscribeUserStatus) for subscription, after which a status change notification can be received through the [TIM.EVENT.USER_STATUS_UPDATED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.USER_STATUS_UPDATED) event.

     
     

To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

To use this feature, you need to enable **Set user status query and status change notification** in the [IM console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `subscribeUserStatus` is called.


> ? By default, this API can be called 20 times every five seconds, and the statuses of up to 100 users can be subscribed to at a time.

**API**

<dx-codeblock>
:::  js

tim.subscribeUserStatus(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type  | Description                                                  |
| ---------- | ----- | ------------------------------------------------------------ |
| userIDList | Array | List of `userID` values. The number of `userID` values cannot exceed 100 per request. |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.subscribeUserStatus({userIDList: ['user0', 'user1']});
promise.then(function(imResponse) {
  const { failureUserList } = imResponse.data;
   // List of `userID` values of the users whose statuses failed to be subscribed to
   failureUserList.forEach((item) => {
     const { userID, code, message } = item;
     // userID - `userID` of the user whose status failed to be queried
     // code - Error code for the failed query
     // message - Error message for the failed query
   });
}).catch(function(imError) {
  console.warn('subscribeUserStatus error:', imError); // Failed to subscribe to the user status
});

:::
</dx-codeblock>

[](id:unsubscribe)
## Unsubscribing from the User Status
To stop receiving notifications of changes in user statuses, call the [unsubscribeUserStatus](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#unsubscribeUserStatus) API to unsubscribe from the user status or clear the subscription list.
If you don't want the subscription list to be cleared manually, after the account is logged out, the IM backend will clear it after a certain period of time by default.

To use this feature, you need to upgrade to the Ultimate edition. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

To use this feature, you need to enable **Set user status query and status change notification** in the [IM console](https://console.cloud.tencent.com/im) in advance; otherwise, an error will be reported when `unsubscribeUserStatus` is called.

> ? By default, this API can be called 20 times every five seconds, and the statuses of up to 100 users can be unsubscribed from at a time.

**API**

<dx-codeblock>
:::  js

tim.unsubscribeUserStatus(options);

:::
</dx-codeblock>

**Parameter**


When the `options` parameter is `undefined`, it indicates to cancel all the current subscriptions. When it is of the `Object` type, it contains the following attribute values:

| Name       | Type  | Description                                                  |
| ---------- | ----- | ------------------------------------------------------------ |
| userIDList | Array | List of `userID` values. The number of `userID` values cannot exceed 100 per request. When `userIDList` is an empty array or `undefined`, it indicates to cancel all the current subscriptions. |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Unsubscribe from some of the current user statuses
let promise = tim.unsubscribeUserStatus({userIDList: ['user0', 'user1']});
promise.then(function(imResponse) {
  const { failureUserList } = imResponse.data;
   // List of `userID` values of the users whose statuses failed to be unsubscribed from
   failureUserList.forEach((item) => {
     const { userID, code, message } = item;
     // userID - `userID` of the user whose status failed to be queried
     // code - Error code for the failed query
     // message - Error message for the failed query
   });
}).catch(function(imError) {
  console.warn('unsubscribeUserStatus error:', imError); // Failed to unsubscribe from the user status
});

// Unsubscribe from all the current subscribed user statuses
let promise = tim.unsubscribeUserStatus();
promise.then(function(imResponse) {
  const { failureUserList } = imResponse.data;
   // List of `userID` values of the users whose statuses failed to be unsubscribed from
   failureUserList.forEach((item) => {
     const { userID, code, message } = item;
     // userID - `userID` of the user whose status failed to be queried
     // code - Error code for the failed query
     // message - Error message for the failed query
   });
}).catch(function(imError) {
  console.warn('unsubscribeUserStatus error:', imError); // Failed to unsubscribe from the user status
});

:::
</dx-codeblock>

[](id:notify)
## Status Change Notification
Depending on the user type, status changes can be divided into three types:
1. Change in a user's own status.
2. Change in a friend's status.
3. Change in a non-friend user's status.

The SDK will deliver the [TIM.EVENT.USER_STATUS_UPDATED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.USER_STATUS_UPDATED) event to notify a status change of any of the three types.

Although all the status notifications are returned in the `TIM.EVENT.USER_STATUS_UPDATED` callback, they are triggered in different ways for different user types.

### Notification of a change in a user's own status
If you have registered the [TIM.EVENT.USER_STATUS_UPDATED](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.USER_STATUS_UPDATED) event listener, when a user's own status changes, the SDK will deliver the `TIM.EVENT.USER_STATUS_UPDATED` event, where the user can get the latest own status.

### Notification of a change in a friend's status
1. If you have enabled automatic notifications of friends' statuses in the [IM console](https://console.cloud.tencent.com/im), when the status of a user's friend changes, the SDK will deliver the `TIM.EVENT.USER_STATUS_UPDATED` event, where the latest status of the friend can be obtained.

2. If you don't enable automatic notifications of friends' statuses and want to get friends' status changes, you need to call `subscribeUserStatus` to subscribe to friends' statuses. When a friend's status changes, the SDK will deliver the `TIM.EVENT.USER_STATUS_UPDATED` callback.


> ! To use `subscribeUserStatus`, you need to purchase the Ultimate edition and enable the feature in the console. For more information, see [Subscribing to the User Status](#subscribe).

3. If you neither enable automatic notifications of friends' statuses nor call `subscribeUserStatus` to subscribe to friends' statuses, changes in friends' statuses cannot be obtained.

### Change in a non-friend user's status
To get the change in a non-friend user's status, you can only call `subscribeUserStatus` to subscribe to the status. When the user's status changes, the `TIM.EVENT.USER_STATUS_UPDATED` callback will be triggered, where the user can get the latest status of the non-friend user.

> ! To use `subscribeUserStatus`, you need to purchase the Ultimate edition and enable the feature in the console. For more information, see [Subscribing to the User Status](#subscribe).


**Sample**

<dx-codeblock>
:::  js

/**
 * Notification receiving:
 * 1. This event will be triggered if a subscribed user status (including online status and custom status) changes.
 * 2. This event will be triggered when a friend's status changes after notifications of friends' statuses are enabled in the IM console, even if the status has not been subscribed to.
 * 3. This event will be sent to all the devices when an account is logged in on them and the custom status is changed on one of them.
 */
 let onUserStatusUpdated = function(event) {
    console.log(event.data);
    const userStatusList = event.data;
    userStatusList.forEach((item) => {
     const { userID, statusType, customStatus } = item;
     // userID - User ID
     // statusType - User status. The enumerated values are described as follows:
     // TIM.TYPES.USER_STATUS_UNKNOWN - Unknown
     // TIM.TYPES.USER_STATUS_ONLINE - Online
     // TIM.TYPES.USER_STATUS_OFFLINE - Offline
     // TIM.TYPES.USER_STATUS_UNLOGINED - Not logged in
     // customStatus - Custom user status
    })
 };
 tim.on(TIM.EVENT.USER_STATUS_UPDATED, onUserStatusUpdated);

:::
</dx-codeblock>

> ? The user status can not only be obtained through `TIM.EVENT.USER_STATUS_UPDATED` as described above, but also be queried as instructed in [Querying the User Status](#get).

### Multi-client and multi-instance sync of status change notifications
If you have enabled multi-client login or multi-instance login on the same platform (for more information, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419)), an account can be logged in on different clients. When the status of the user logged in on one of the clients changes, the IM backend will send the status change notification to other logged-in devices.

[](id:limit)
## API Restrictions

### Plan restrictions
* You don't need to upgrade to the Ultimate edition to use the `setSelfStatus` API.
* You don't need to upgrade to the Ultimate edition to use the `getUserStatus` API to query a user's own status.
* You need to upgrade to the Ultimate edition to use the `getUserStatus` API to query another user's status.
* You need to upgrade to the Ultimate edition to use the `subscribeUserStatus` / `unsubscribeUserStatus` API.


### API call frequency limit
* The `setSelfStatus` API can be called an unlimited number of times.
* The `getUserStatus` API is used to query a user's own status and can be called an unlimited number of times.
* By default, the `getUserStatus` API can be called 20 times every five seconds if used to query the status of another user, and the statuses of up to 500 users can be queried at a time.
* By default, the `subscribeUserStatus` API can be called 20 times every five seconds, and the statuses of up to 100 users can be subscribed to at a time.
* By default, the `unsubscribeUserStatus` API can be called 20 times every five seconds, and up to 100 users can be unsubscribed from at a time.



## FAQs

### What should I do if error code 72001 is reported when I call the subscribe/unsubscribe API?

Error code 72001 indicates that the feature is not enabled in the console. You need to log in to the [IM console](https://console.cloud.tencent.com/im) and enable the feature.
