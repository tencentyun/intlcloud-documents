## Feature Description

The methods to manipulate group attributes are in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.

A new custom group field is designed based on the API 2.0. It is a "group attribute" that enables seat management in audio chat rooms. When a member mics on, a group attribute can be set to manage the member information. When the member mics off, the group attribute can be deleted. Other members can get the group attribute list to display the seat list.

> ? Currently, the group attribute feature is available only for audio-video groups (AVChatRoom).

The group attribute has the following features:

1. You can CRUD group attributes directly in the client without console configuration.
2. Up to 16 group attributes are supported. Each group attribute can be up to 4 KB, and the total size of all the group attributes can be up to 16 KB.
3. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs can be called by a logged-in user up to 10 times every 5 seconds in total in the SDK, after which the error code 8511 will be returned, or 5 times every second in total on the backend, after which the error code 10049 will be returned.
4. The `getGroupAttributes` API can be called by a logged-in user up to 20 times every 5 seconds in the SDK.

### Initializing group attributes

You can call the `initGroupAttributes` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/initGroupAttributes.html)) to initialize the group attributes, and the original group attributes, if any, will be cleared.

Below is the sample code:

```javascript
// Initialize the group attributes
groupManager.initGroupAttributes("groupID", {
  attr1: "",
});
```

### Setting group attributes

You can call the `setGroupAttributes` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/setGroupAttributes.html)) to set the group attributes. If a group attribute does not exist, it will be automatically added.

Below is the sample code:

```javascript
// Set the group attributes
groupManager.setGroupAttributes("groupID", {
  attr1: "",
});
```

### Deleting group attributes

You can call the `deleteGroupAttributes` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/deleteGroupAttributes.html)) to delete specified group attributes. If `keys` is `null`/`nil`, all the group attributes will be cleared.

Below is the sample code:

```javascript
// Delete a group attribute
groupManager.deleteGroupAttributes("groupID", ["attr1", "attr2"]);
```

### Getting group attributes

You can call the `getGroupAttributes` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/getGroupAttributes.html)) to get specified group attributes. If `keys` is `null`/`nil`, all the group attributes will be obtained.

Below is the sample code:

```javascript
// Get the group attributes
const attrs = await groupManager.getGroupAttributes("groupID");
```

### Updating group attributes

If you have called `addGroupListener` to add a group event listener, all the group attributes will be called back through `onGroupAttributeChanged` ([Details](https://comm.qq.com/im/doc/RN/en/Callback/OnGroupAttributeChanged.html)) when a group attribute is changed.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager.addGroupListener({
  onGroupAttributeChanged: (groupID, groupAttributeMap) => {
    // A group attribute is changed.
  },
});
```
