## Feature Description
To group friends into categories such as "Classmates at university" and "Coworkers", call the following APIs.

## Friend List

### Creating a friend list
Call the `createFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a8b33edab15ae7d179e4e2d885e7d2b7d)) to create a friend list.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().createFriendGroup("Friends at university", userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // Friend list created successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to create the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Create a friend list
[[V2TIMManager sharedInstance] createFriendGroup:@"Friends at university" userIDList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // Friend list created successfully
} fail:^(int code, NSString *desc) {
    // Failed to create the friend list
}];
```
:::
</dx-tabs>

### Deleting a friend list
Call the `deleteFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7)) to delete a friend list. This will not delete the friends.

Sample code:
<dx-tabs>
::: Android
```java
List<String> friendGroupList = new ArrayList<>();
friendGroupList.add("Friends at university");
V2TIMManager.getFriendshipManager().deleteFriendGroup(friendGroupList, new V2TIMCallback() {
  @Override
  public void onSuccess() {
    // Friend list deleted successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to delete the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Delete a friend list
[[V2TIMManager sharedInstance] deleteFriendGroup:@[@"Friends at university"] succ:^{
    // Friend list deleted successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete the friend list
}];
```
:::
</dx-tabs>

### Renaming a friend list
Call the `renameFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0)) to rename a friend list.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getFriendshipManager().renameFriendGroup("Friends at university", "Friends in high school", new V2TIMCallback() {
  @Override
  public void onSuccess() {
    // Friend list name changed successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to rename the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Rename a friend list
[[V2TIMManager sharedInstance] renameFriendGroup:@"Friends at university" newName:@"Friends in high school" succ:^{
    // Friend list name changed successfully
} fail:^(int code, NSString *desc) {
    // Failed to rename the friend list
}];
```
:::
</dx-tabs>

### Getting a friend list
Call the `getFriendGroupList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229)) to get a friend list.

Sample code:
<dx-tabs>
::: Android
```java
List<String> friendGroups = new ArrayList<>();
friendGroups.add("Friends at university");
V2TIMManager.getFriendshipManager().getFriendGroups(friendGroups, new V2TIMValueCallback<List<V2TIMFriendGroup>>() {
  @Override
  public void onSuccess(List<V2TIMFriendGroup> v2TIMFriendGroups) {
    // Friend list obtained successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to obtain the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Get a friend list
[[V2TIMManager sharedInstance] getFriendGroupList:@[@"Friends at university"] succ:^(NSArray<V2TIMFriendGroup *> *groups) {
    // Friend list obtained successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the friend list
}];
```
:::
</dx-tabs>

### Adding a friend to a list
Call the `addFriendsToFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d)) to add a friend to a list.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().addFriendsToFriendGroup("Friends at university", userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // Added successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to add the friend to the group
  }
});
```
:::
::: iOS and macOS
```objectivec
// Add a friend to a list
[[V2TIMManager sharedInstance] addFriendsToFriendGroup:@"Friends at university" userIDList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // Added successfully
} fail:^(int code, NSString *desc) {
    // Failed to add the friend to the group
}];
```
:::
</dx-tabs>

### Removing a friend from a list
Call the `deleteFriendsFromFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359)) to remove a friend from a list. This will only remove the friend from the list and will not delete the friend.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().deleteFriendsFromFriendGroup("Friends at university", userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // Removed successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to remove the friend
  }
});
```
:::
::: iOS and macOS
```objectivec
// Remove a friend from a list
[[V2TIMManager sharedInstance] deleteFriendsFromFriendGroup:@"Friends at university" userIDList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // Removed successfully
} fail:^(int code, NSString *desc) {
    // Failed to remove the friend
}];
```
:::
</dx-tabs>


