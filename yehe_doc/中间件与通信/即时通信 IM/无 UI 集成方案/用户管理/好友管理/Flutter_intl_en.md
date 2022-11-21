## Feature Description
The IM SDK supports friend management, and users can add and delete friends and set to send messages only to friends.

### Getting contacts
The IM SDK supports the logic for the friend relationship chain. You can call the `getFriendList` API ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/getFriendList.html)) to get contacts.

Sample code:


```dart
// Get contacts
V2TimValueCallback<List<V2TimFriendInfo>> friendsList = await friendshipManager.getFriendList();
```



### Adding a friend
Call the `addFriend` API ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/addFriend.html)) to add a friend.

Sample code:


```dart
// Add a two-way friend
V2TimValueCallback<V2TimFriendOperationResult> addFriend = await friendshipManager.addFriend(userID: "userID",remark:"Friend request remarks",addWording:"Remarks",addType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH);
```


The process has the following variations depending on whether friend verification is required.

#### Option 1. Friend request approval is not required
1. Users A and B call `setFriendListener` to set the relationship chain listener.

2. User B specifies that friend request approval is not required (`V2TIM_FRIEND_ALLOW_ANY`) through the `allowType` field ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_user_full_info/V2TimUserFullInfo/allowType.html)) in the `setSelfInfo` function.

3. User A can add user B as a friend successfully by calling `addFriend`, after which the `addType` of the `V2TIMFriendAddApplication` request parameter can be set to either value as needed:
   * If it is set to `V2TIM_FRIEND_TYPE_BOTH` (two-way friend), both users A and B will receive the `onFriendListAdded` callback ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendListAdded.html)).
   * If it is set to `V2TIM_FRIEND_TYPE_SINGLE` (one-way friend), only user A will receive the `onFriendListAdded` callback.


#### Option 2. Friend request approval is required
1. Users A and B call `setFriendListener` to set the relationship chain listener.

2. User B specifies that friend request approval is required (`V2TIM_FRIEND_NEED_CONFIRM`) through the `allowType` field in the `setSelfInfo` function. 
   
3. User A calls `addFriend` to request to add user B as a friend. The `resultCode` parameter in the callback for successful API call returns `30539`, indicating that the request needs to be approved by user B. In addition, both users A and B will receive the `onFriendApplicationListAdded` callback ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListAdded.html)).
   
4. User B will receive the `onFriendApplicationListAdded` callback. If `type` in the `V2TIMFriendApplication` parameter is `V2TIM_FRIEND_APPLICATION_COME_IN`, user B can accept or reject the request.
    - User B calls `acceptFriendApplication` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/acceptFriendApplication.html)) to accept the friend request. If the type is `V2TIM_FRIEND_ACCEPT_AGREE` (one-way friend):
      - User A will receive the `onFriendListAdded` callback, indicating that the one-way friend was added successfully.
      - User B will receive the `onFriendApplicationListDeleted` callback ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListDeleted.html)). At this point, user B has become a friend of user A, but not vice versa.
    - User B calls `acceptFriendApplication` to accept the friend request. If the type is `V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` (two-way friend), both users A and B will receive the `onFriendListAdded` callback, indicating that they added each other as a friend successfully.
    - User B calls `refuseFriendApplication` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/refuseFriendApplication.html)) to reject the friend request, and both users will receive the `onFriendApplicationListDeleted` callback.


### Deleting a friend
Call the `deleteFromFriendList` API ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/deleteFromFriendList.html)) to delete a friend.

Sample code:


```dart
// Delete a two-way friend
V2TimValueCallback<List<V2TimFriendOperationResult>> deleteres = await friendshipManager.deleteFromFriendList(deleteType: FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList:['user1']);
```



### Checking the friend relationship
Call the `checkFriend` API ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/checkFriend.html)) to check the friend relationship.

Sample code:


```dart
// Check whether the friend relationship is one-way or two-way
V2TimValueCallback<List<V2TimFriendCheckResult>> checkres = await friendshipManager.checkFriend(checkType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList: [] );
```


### Setting to send messages to friends only
By default, IM SDK does not check the relationship when sending one-to-one messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
To implement "adding a friend before sending a message", you can log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After it is enabled, a user can send messages only to friends. If the user sends a message to a non-friend user, the SDK will report error code 20009.



