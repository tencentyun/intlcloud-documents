## Feature Description
The methods to manipulate group attributes are in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.

A new custom group field is designed based on the API 2.0. It is a "group attribute" that enables seat management in audio chat rooms. When a member mics on, a group attribute can be set to manage the member information. When the member mics off, the group attribute can be deleted. Other members can get the group attribute list to display the seat list.

> ? Currently, the group attribute feature is available only for audio-video groups (AVChatRoom).

The group attribute has the following features:
1. You can create, read, update and delete (CRUD) group attributes directly in the client without console configuration.
2. Up to 16 group attributes are supported. Each group attribute can be up to 4 KB in size, and the total size of all the group attributes can be up to 16 KB.
3. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs can be called by a logged-in user up to 10 times every 5 seconds in total in the SDK, after which the error code 8511 will be returned, or 5 times every second in total on the backend, after which the error code 10049 will be returned.
4. The `getGroupAttributes` API can be called by a logged-in user up to 20 times every 5 seconds in the SDK.

### Initializing the group attributes
Call the `initGroupAttributes` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/initGroupAttributes.html)) to initialize the group attributes, and the original group attributes, if any, will be cleared first.

Sample code:



```dart
// Initialize the group attributes
groupManager.initGroupAttributes(groupID: "groupID", attributes: {
    "attr1":""
  });
```


### Setting the group attributes

Call the `setGroupAttributes` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupAttributes.html)) to set the group attributes. If a group attribute doesn't exist, it will be automatically added.

Sample code:



```dart
// Set the group attributes
groupManager.setGroupAttributes(groupID: "groupID", attributes: {
    "attr1":""
  });
```


### Deleting the group attributes

Call the `deleteGroupAttributes` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/deleteGroupAttributes.html)) to delete a specified group attribute. If `keys` is `null`/`nil`, all the group attributes will be cleared.

Sample code:



```dart
// Delete the group attributes
groupManager.deleteGroupAttributes(groupID: "groupID", keys: ['attr1','attr2']);
```


### Getting the group attributes

Call the `getGroupAttributes` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupAttributes.html)) to get a specified group attribute. If `keys` is `null`/`nil`, all the group attributes will be obtained.

Sample code:



```dart
// Get the group attributes
V2TimValueCallback<Map<String, String>> attrs = await groupManager.getGroupAttributes(groupID: "groupID");
```


### Updating the group attributes

If you have called `addGroupListener` to add a group event listener, all the group attributes will be called back through `onGroupAttributeChanged` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupAttributeChangedCallback.html)) when a group attribute is changed.

Sample code:



```dart
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupAttributeChanged: (groupID, groupAttributeMap) {
    // A group attribute is changed.
  },));
```
