## Feature Description
A new custom group field is designed based on the API 2.0. It is a "group attribute".
A group attribute enables seat management in audio chat rooms. When a member mics on, a group attribute can be set to manage the member information. When the member mics off, the group attribute can be deleted. Other members can get the group attribute list to display the seat list.
Group attributes are represented by key-value pairs, and the methods are in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.

> ? Currently, the group attribute feature is available only for audio-video groups (AVChatRoom).

The group attribute has the following features:
1. Up to 16 group attributes are supported. Each group attribute can be up to 4 KB, and the total size of all the group attributes can be up to 16 KB.
2. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs can be called by a logged-in user 10 times every 5 seconds in total in the SDK, after which the error code 8511 will be returned, or 5 times every second in total on the backend, after which the error code 10049 will be returned.
3. The `getGroupAttributes` API can be called by a logged-in user 20 times every 5 seconds in the SDK.

### Initializing the group attributes
Call the `initGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a17569b57abc77adb6be9356b9eb70182) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1b3a56dfc345f1ef2a575cb36156e745)) to initialize the group attributes, and the original group attributes, if any, will be cleared first.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().initGroupAttributes("groupA", attributeMap, new V2TIMCallback() {
  @Override
  public void onSuccess() {
		// Initialized the group attributes successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to initialized the group attributes
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] initGroupAttributes:@"groupA" attributes:@{@"key1" : @"value1"} succ:^{
    // Initialized the group attributes successfully
} fail:^(int code, NSString *desc) {
    // Failed to initialized the group attributes
}];

```
:::
</dx-tabs>

### Setting the group attributes

Call the `setGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3ec31101e4763dab7a1c99a71bc3da08) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a134342ddb51d1ee83f3981ed91d26885)) to set the group attributes. If a group attribute doesn't exist, it will be automatically added.

Sample code:

<dx-tabs>
::: Android

```java
HashMap<String, String> attributeMap = new HashMap<>();
attributeMap.put("key1", "value1");
attributeMap.put("key2", "value2");
V2TIMManager.getGroupManager().setGroupAttributes("groupA", attributeMap, new V2TIMCallback() {
  @Override
  public void onSuccess() {
		// Set the group attributes successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to set the group attributes
  }
});
```
:::
::: iOS and macOS

```objectivec
[[V2TIMManager sharedInstance] setGroupAttributes:@"groupA" attributes:@{@"key1" : @"value1"} succ:^{
    // Set the group attributes successfully
} fail:^(int code, NSString *desc) {
    // Failed to set the group attributes
}];
```

:::
</dx-tabs>

### Deleting the group attributes

Call the `deleteGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a45f211bafddc58bf5e199e18a6814578) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa504ffca9492580ca27a45f78a87e2cb)) to delete a specified group attribute. If `keys` is set to `null`/`nil`, all the group attributes will be cleared.

Sample code: 

<dx-tabs>
::: Android
```java
List<String> keyList = new ArrayList<>();
keyList.add("key1");
V2TIMManager.getGroupManager().deleteGroupAttributes("groupA", keyList, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Deleted successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to delete
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] deleteGroupAttributes:@"groupA" keys:@[@"key1"] succ:^{
    // Deleted successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete
}];
```
:::
</dx-tabs>

### Getting the group attributes

Call the `getGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ade2155fb24ed1c0b8eb976e146c14e3d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac8a74db230669d1b49da47bb0895cbf9)) to get a specified group attribute. If `keys` is set to `null`/`nil`, all the group attributes will be obtained.

> ? The `getGroupAttributes` API can be called by a logged-in user 20 times every 5 seconds in the SDK.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().getGroupAttributes("groupA", null, new V2TIMValueCallback<Map<String, String>>() {
  @Override
  public void onSuccess(Map<String, String> stringStringMap) {
  	// Obtained successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to obtain
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getGroupAttributes:@"groupA" keys:nil succ:^(NSMutableDictionary<NSString *,NSString *> *groupAttributeList) {
    // Obtained successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain
}];
```
:::
</dx-tabs>

### Updating the group attributes

If you have called `addGroupListener` to add a group event listener, all the group attributes will be called back through `onGroupAttributeChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#aa390fa93bc73a0262bdddb540227dc45) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a7b76343c7ef46af4a2cd09db6d51db13)) when a group attribute is changed.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onGroupAttributeChanged(String groupID, Map<String, String> groupAttributeMap) {
  	// A group attribute was changed.
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onGroupAttributeChanged:(NSString *)groupID attributes:(NSMutableDictionary<NSString *,NSString *> *)attributes {
    // A group attribute was changed.
}
```
:::
</dx-tabs>


