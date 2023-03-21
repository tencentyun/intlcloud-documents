## Overview

With group attributes, you can manage the seats of audio chat rooms. When a user mics on, you can set a group attribute to manage the information of the user. When the user mics off, you can delete the group attribute. Other members can get the list of group attributes to display the seat list.

>!
> - Starting from v2.14.0, this feature is supported only by audio-video groups (AVChatRoom).
>- Starting from v2.25.0, this feature is supported by audio-video groups (AVChatRoom), public groups (Public), meeting groups (Meeting), work groups (Work), and community groups (Community).

The group attribute feature has the following characteristics:
1. You can configure up to 16 group attributes. The size of each group attribute can be up to 4 KB, and the total size of all group attributes can be up to 16 KB.
2. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs together can be called by a logged-in user up to ten times every five seconds in the SDK, and the 2996 error code will be called back if the limit is exceeded.
3. The `getGroupAttributes` API can be called by a logged-in user 20 times every five seconds in the SDK, and the 2996 error code will be called back if the limit is exceeded.
4. When you modify group attributes for the first time after each successful login, call `getGroupAttributes` to pull the latest group attributes before you initiate the modification operation again.
5. When multiple users modify the same group attributes at the same time, only the first user can execute successfully, and other users will receive the 10056 error code. After receiving this error code, please call `getGroupAttributes` to update the locally stored group attributes to the latest before you initiate the modification operation.
6. Before you use this feature in an audio-video group (AVChatRoom) after successful login, you need to call the [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) API to join the audio-video group. For a public group (Public), meeting group (Meeting), work group (Work), and community group (Community), you do not need to join the group again.

### Initializing group attributes

**API**

<dx-codeblock>
:::  js

tim.initGroupAttributes(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID | String | Group ID |
| groupAttributes | Object | Group attributes |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.initGroupAttributes({
  groupID: 'group1',
  groupAttributes: { key1: 'value1', key2: 'value2' }
});
promise.then(function(imResponse) { // Initialized successfully
  console.log(imResponse.data.groupAttributes); // Group attributes initialized successfully
}).catch(function(imError) { // Initialization failed
  console.warn('initGroupAttributes error:', imError); // Error information
});

:::
</dx-codeblock>

### Setting group attributes

**API**

<dx-codeblock>
:::  js

tim.setGroupAttributes(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID | String | Group ID |
| groupAttributes | Object | Group attributes |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.setGroupAttributes({
  groupID: 'group1',
  groupAttributes: { key1: 'value1', key2: 'value2' }
});
promise.then(function(imResponse) { // Set successfully
  console.log(imResponse.data.groupAttributes); // Group attributes set successfully
}).catch(function(imError) { // Setting failed
  console.warn('setGroupAttributes error:', imError); // Error information
});

:::
</dx-codeblock>


### Deleting group attributes

>! To delete specified group attributes (key-value pairs), pass in a non-empty array for `keyList`. To delete all group attributes, pass in an empty array for `keyList`.

**API**

<dx-codeblock>
:::  js

tim.deleteGroupAttributes(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID | String | Group ID |
| keyList | Array | List of keys of the group attributes  |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Delete the `key-value` of the specified group attributes
let promise = tim.deleteGroupAttributes({
  groupID: 'group1',
  keyList: ['key1', 'key2']
});
promise.then(function(imResponse) { // Deleted successfully
  console.log(imResponse.data.keyList); // List of group attributes deleted successfully
}).catch(function(imError) { // Deletion failed
  console.warn('deleteGroupAttributes error:', imError); // Error information
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Delete all group attributes
let promise = tim.deleteGroupAttributes({
  groupID: 'group1',
  keyList: []
});
promise.then(function(imResponse) { // Deleted successfully
  console.log(imResponse.data.keyList); // List of group attributes deleted successfully
}).catch(function(imError) { // Deletion failed
  console.warn('deleteGroupAttributes error:', imError); // Error information
});

:::
</dx-codeblock>

### Getting group attributes

>!To get specified group attributes, pass in a non-empty array for `keyList`. To get all group attributes, pass in an empty array for `keyList`.

**API**

<dx-codeblock>
:::  js

tim.getGroupAttributes(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID | String | Group ID |
| keyList | Array | List of keys of the group attributes  |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Get specified group attributes
let promise = tim.getGroupAttributes({
  groupID: 'group1',
  keyList: ['key1', 'key2']
});
promise.then(function(imResponse) { // Got successfully
  console.log(imResponse.data.groupAttributes); // Specified group attributes
}).catch(function(imError) { // Getting failed
  console.warn('getGroupAttributes error:', imError); // Error information
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Get all group attributes
let promise = tim.getGroupAttributes({
  groupID: 'group1',
  keyList: []
});
promise.then(function(imResponse) { // Got successfully
  console.log(imResponse.data.groupAttributes); // All group attributes
}).catch(function(imError) { // Getting failed
  console.warn('getGroupAttributes error:', imError); // Error information
});

:::
</dx-codeblock>


### Listening for a group attribute update event

<dx-codeblock>
:::  js

let onGroupAttributesUpdated = function(event) {
   const groupID = event.data.groupID // Group ID
   const groupAttributes = event.data.groupAttributes //Updated group properties
   console.log(event.data);
};
tim.on(TIM.EVENT.GROUP_ATTRIBUTES_UPDATED, onGroupAttributesUpdated);

:::
</dx-codeblock>
