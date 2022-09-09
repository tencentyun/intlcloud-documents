## Feature Description
To block a user's messages, add the user to the blocklist.

## Blocklist
### Blocking a user
Call the `addToBlackList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c)) to add a user to the blocklist, that is, block the user.
If you have called `addFriendListener` to add a listener, blocking a user will trigger the `onBlackListAdded` callback.

> ? If users A and B are friends, after either user A or user B is blocked by the other user, the two-way friend relationship will be terminated, and they cannot start a conversation with or send a friend request to each other.

By default, a blocked user does not know that he/she is "blocked". After the user sends a message, the error code indicating that he/she has been blocked will not be returned.
To have the "You have been blocked by the user" error message returned after a blocked user sends a message, you can log in to the [IM console](https://console.cloud.tencent.com/im) and disable **Blocklist Check** as shown below. Then the SDK will report error code 20007 after a blocked user sends a message.
<img src="https://qcloudimg.tencent-cloud.cn/raw/168404f5f3ed977ff05f5d93444aa65e.png" style="zoom:80%;"/>

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().addToBlackList(userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // User blocked successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to block the user
  }
});

// Listen for the notification of a user added to the blocklist
V2TIMManager.getFriendshipManager().addFriendListener(new V2TIMFriendshipListener() {
  @Override
  public void onBlackListAdd(List<V2TIMFriendInfo> infoList) {
    // A user was added to the blocklist.
  }
});
```
:::
::: iOS and macOS
```objectivec
// Block a user
[[V2TIMManager sharedInstance] addToBlackList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // User blocked successfully
} fail:^(int code, NSString *desc) {
    // Failed to block the user
}];

// Listen for the notification of a user added to the blocklist
[[V2TIMManager sharedInstance] addFriendListener:self];
- (void)onBlackListAdded:(NSArray<V2TIMFriendInfo *>*)infoList {
    // A user was added to the blocklist.
}
```
:::
</dx-tabs>

### Unblocking a user
Call `deleteFromBlackList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3dcd8f1c70dceafa94ab48796c2f26aa) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aa7e69a67185eaca658ba429cf6309a5f)) to remove a user from the blocklist, after which the user can send a friend request and start a conversation.
If you have called `addFriendListener` to add a listener, unblocking a user will trigger the `onBlackListDeleted` callback.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().deleteFromBlackList(userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // User unblocked successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to unblock the user
  }
});

// Listen for the notification of a user removed from the blocklist
V2TIMManager.getFriendshipManager().addFriendListener(new V2TIMFriendshipListener() {
  @Override
  public void onBlackListDeleted(List<String> userList) {
    // A user was removed from the blocklist.
  }
});
```
:::
::: iOS and macOS
```objectivec
// Unblock a user
[[V2TIMManager sharedInstance] deleteFromBlackList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // User unblocked successfully
} fail:^(int code, NSString *desc) {
    // Failed to unblock the user
}];

// Listen for the notification of a user removed from the blocklist
[[V2TIMManager sharedInstance] addFriendListener:self];
- (void)onBlackListDeleted:(NSArray*)userIDList {
    // A user was removed from the blocklist.
}

```
:::
</dx-tabs>

### Getting the blocklist
Call `getBlackList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6269df2d96c910648ab2f0c43e1931c6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a0d854d64c8ae936014a8424d55508fa3)) to view how many users have been blocked and manage them.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getFriendshipManager().getBlackList(new V2TIMValueCallback<List<V2TIMFriendInfo>>() {
  @Override
  public void onSuccess(List<V2TIMFriendInfo> v2TIMFriendInfos) {
    // Blocklist obtained successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to obtain the blocklist
  }
});
```
:::
::: iOS and macOS
```objectivec
// Get the blocklist
[[V2TIMManager sharedInstance] getBlackList:^(NSArray<V2TIMFriendInfo *> *infoList) {
    // Blocklist obtained successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the blocklist
}];
```
:::
</dx-tabs>


