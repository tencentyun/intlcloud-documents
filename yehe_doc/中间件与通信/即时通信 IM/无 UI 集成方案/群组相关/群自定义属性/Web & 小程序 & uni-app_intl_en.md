## Feature Description

A group attribute enables seat management in audio chat rooms. When a member mics on, a group attribute can be set to manage the member information. When the member mics off, the group attribute can be deleted. Other members can get the group attribute list to display the seat list.

>!
>- Currently, the group attribute feature is available only for audio-video groups (AVChatRoom).
>- This API applies only to audio-video groups (AVChatRoom). If you call this API for other types of groups, this API will return the 2641 error code.
>- Before this API is used, [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) must be called to join an audio-video group (AVChatRoom); otherwise, the error code 2642 will be returned.
>- Up to 16 group attribute keys are supported, which can contain up to 32 bytes. The size of each group attribute value can be up to 4 KB, and the total size of all group attributes (including keys and values) can be up to 16 KB.

### Initializing the group attributes

**API**

<dx-codeblock>
:::  js

tim.initGroupAttributes(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID |
| groupAttributes | Object | Group attributes |

**Returned value**

`Promise` object

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
  console.warn('initGroupAttributes error:', imError); // Failed to initialize the group attributes
});

:::
</dx-codeblock>

### Setting the group attributes

**API**

<dx-codeblock>
:::  js

tim.setGroupAttributes(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID |
| groupAttributes | Object | Group attributes |

**Returned value**

`Promise` object

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
  console.warn('setGroupAttributes error:', imError); // Failed to set the group attributes
});

:::
</dx-codeblock>


### Deleting the group attributes

>! To delete specified group attributes (`key-value`), pass in a non-empty array for `keyList`; to delete all the group attributes, pass in an empty array for `keyList`.

**API**

<dx-codeblock>
:::  js

tim.deleteGroupAttributes(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID |
| keyList | Array | List of keys of the group attributes  |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Delete the `key-value` of the specified group attributes
let promise = tim.deleteGroupAttributes({
  groupID: 'group1',
  keyList: ['key1', 'key2']
});
promise.then(function(imResponse) { // Deleted successfully
  console.log(imResponse.data.keyList); // List of the group attribute keys deleted successfully
}).catch(function(imError) { // Deletion failed
  console.warn('deleteGroupAttributes error:', imError); // Failed to delete the group attributes
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Delete all the group attributes
let promise = tim.deleteGroupAttributes({
  groupID: 'group1',
  keyList: []
});
promise.then(function(imResponse) { // Deleted successfully
  console.log(imResponse.data.keyList); // List of the group attribute keys deleted successfully
}).catch(function(imError) { // Deletion failed
  console.warn('deleteGroupAttributes error:', imError); // Failed to delete the group attributes
});

:::
</dx-codeblock>

### Getting the group attributes

>! To get specified group attributes, pass in a non-empty array for `keyList`; to get all the group attributes, pass in an empty array for `keyList`.

**API**

<dx-codeblock>
:::  js

tim.getGroupAttributes(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID |
| keyList | Array | List of keys of the group attributes  |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Get specified group attributes
let promise = tim.getGroupAttributes({
  groupID: 'group1',
  keyList: ['key1', 'key2']
});
promise.then(function(imResponse) { // Obtained successfully
  console.log(imResponse.data.groupAttributes); // Specified group attributes
}).catch(function(imError) { // Failed to obtain
  console.warn('getGroupAttributes error:', imError); // Failed to obtain the group attributes
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Get all the group attributes
let promise = tim.getGroupAttributes({
  groupID: 'group1',
  keyList: []
});
promise.then(function(imResponse) { // Obtained successfully
  console.log(imResponse.data.groupAttributes); // All the group attributes
}).catch(function(imError) { // Failed to obtain
  console.warn('getGroupAttributes error:', imError); // Failed to obtain the group attributes
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