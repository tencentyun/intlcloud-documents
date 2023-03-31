## Overview
The Chat SDK supports friend management, and users can add and delete friends and set to send messages only to friends.

### Getting the contacts
The Chat SDK supports the logic for the friend relationship chain. You can call the `getFriendList` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendList.html)) to get contacts.

Sample code:


```dart
// Obtain the contacts
V2TimValueCallback<List<V2TimFriendInfo>> friendsList = await friendshipManager.getFriendList();
```



### Adding friends
Call the `addFriend` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addFriend.html)) to add a friend.

Sample code:


```dart
// Add a two-way friend
V2TimValueCallback<V2TimFriendOperationResult> addFriend = await friendshipManager.addFriend(userID: "userID",remark:"Friend request remarks",addWording:"Remarks",addType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH);
```


The process has the following variations depending on whether friend verification is required.

#### Friend request approval is not required
1. Users A and B call `setFriendListener` to set the relationship chain listener.
2. User B specifies that friend request approval is not required (`V2TIM_FRIEND_ALLOW_ANY`) through the `allowType` field ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/User/V2TimUserFullInfo.html#allowtype)) in the `setSelfInfo` function.
3. User A can add user B as a friend successfully by calling `addFriend`, after which the `addType` of the `V2TIMFriendAddApplication` request parameter can be set to either value as needed:
   * If it is set to `V2TIM_FRIEND_TYPE_BOTH` (two-way friend), both users A and B will receive the `onFriendListAdded` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnFriendListAddedCallback.html)).
   * If it is set to `V2TIM_FRIEND_TYPE_SINGLE` (one-way friend), only user A will receive the `onFriendListAdded` callback.


#### Friend request approval is required
1. Users A and B call `setFriendListener` to set the relationship chain listener.
2. User B specifies that friend request approval is required (`V2TIM_FRIEND_NEED_CONFIRM`) through the `allowType` field in the `setSelfInfo` function. 
3. User A calls `addFriend` to request to add user B as a friend. The `resultCode` parameter in the callback for successful API call returns `30539`, indicating that the request needs to be approved by user B. In addition, both users A and B will receive the `onFriendApplicationListAdded` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnFriendApplicationListAddedCallback.html)).
4. User B will receive the `onFriendApplicationListAdded` callback. If `type` in the `V2TIMFriendApplication` parameter is `V2TIM_FRIEND_APPLICATION_COME_IN`, user B can accept or reject the request.
    - - User B calls `acceptFriendApplication` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/acceptFriendApplication.html)) to accept the friend request. If the type is `V2TIM_FRIEND_ACCEPT_AGREE` (one-way friend):
      - User A will receive the `onFriendListAdded` callback, indicating that the one-way friend was added successfully.
      - User B will receive the `onFriendApplicationListDeleted` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnFriendApplicationListDeletedCallback.html)). At this point, user B has become a friend of user A, but not vice versa.
    - User B calls `acceptFriendApplication` to accept the friend request. If the type is `V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` (two-way friend), both users A and B will receive the `onFriendListAdded` callback, indicating that they added each other as a friend successfully.
    - User B calls `refuseFriendApplication` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/refuseFriendApplication.html)) to reject the friend request, and both users will receive the `onFriendApplicationListDeleted` callback.


### Deleting friends
Call the `deleteFromFriendList` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/deleteFromFriendList.html)) to delete a friend.

Sample code:


```dart
// Two-way deletion
V2TimValueCallback<List<V2TimFriendOperationResult>> deleteres = await friendshipManager.deleteFromFriendList(deleteType: FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList:['user1']);
```



### Checking friend relationships
Call the `checkFriend` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/checkFriend.html)) to check the friend relationship.

Sample code:


```dart
// Check whether the friend relationship is one-way or two-way
V2TimValueCallback<List<V2TimFriendCheckResult>> checkres = await friendshipManager.checkFriend(checkType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList: [] );
```


### Setting to send messages to friends only
By default, Chat SDK does not check the relationship when sending one-to-one messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
If you want to implement the interaction mode of "friending before chatting", go to [Chat console](https://console.cloud.tencent.com/im) -> **Feature Configuration** -> **Login and Message** -> **Relationship Check** and enable "Check Relationship for One-to-One Messages". With this feature enabled, users can only send messages to friends, and will receive the 20009 error code from SDK when sending a message to a non-friend user.
