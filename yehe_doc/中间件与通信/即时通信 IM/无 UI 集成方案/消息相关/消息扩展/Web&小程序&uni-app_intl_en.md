
## Overview
Message extension allows you to configure keys and values for messages to implement polling, group notes, survey and other types of messages.
- For polling, create a custom message using the `createCustomMessage` API ([details](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage)), where `data` stores the polling title and options. And store the user ID of the voter and selected option(s) in the `key` and `value` of the message extension, respectively. With the selected options of users, we can calculate the polling percentage in real time.
- For group notices, create a custom message for group notification using the [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) API, where `data` stores the title of the group notice, and then store the user ID and the corresponding info in the `key` and `value` of the message extension, respectively.
- For a survey, create a custom message using the [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) API, where `data` stores the title and options of the survey, and then store the user ID and the corresponding info in the `key` and `value` of the message extension, respectively.

> ?
- To use this feature, you need to purchase the [Ultimate edition](https://buy.cloud.tencent.com/avc?from=17220).
- This feature is available only in v2.25.0 or later.
- You need to enable this feature via [Chat console](https://console.cloud.tencent.com/im) > **Feature Configuration** > **Login and Message** > **Set message extension**.
- This feature is not available for communities and audio/video groups.

### Setting message extension
Call the [setMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageExtensions) API to set a message extension. If the extension `key` already exists, modify its `value`. Otherwise, add the new key-value extension. After the message extension is set successfully, both yourself and the recipient (one-to-one) or group members (Group) will receive the [TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_UPDATED) event.

**API**

<dx-codeblock>
:::  js

tim.setMessageExtensions(message, extensions);

:::
</dx-codeblock>

**Parameters**

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| message            | Message  | Message instance |
| extensions      | Array    | List of key-value extensions of a message. If an extension `key` already exists, modify its `value`. Otherwise, add the new key-value extension. |

> ? 
> 1. The message must meet the following conditions:
 - The `isSupportExtension` attribute of the message is set to `true`.
 - The message is sent successfully.
 - The message is not a message of a community group (Community) or audio-video group (AVChatRoom).
2. The `key` and `value` of an extension can contain up to 100 B and 1 KB, respectively. You can set up to 20 extensions each time and 300 extensions for a message.
3. If multiple users set or delete the `key` of the same extension simultaneously, only the first user can operate successfully, and other users will receive the error code 23001 and the latest extension info in the setting response packet, who can set it again if necessary.
4. We recommend setting unique keys of extensions by different users to avoid conflicts in most cases. For example, the `userID` can be set as the `key` of the extension in polling, group notices and survey.

**Return values**

`Promise` object.

**Sample** 

<dx-codeblock>
:::  js

let promise = tim.setMessageExtensions(message, [{ key: 'a', value: '1' }, { key: 'b', value: '2' }]);
promise.then(function(imResponse) {
  // Set message extensions successfully
   const { extensions } = imResponse.data;
   extensions.forEach((item) => {
     const { code, key, value } = item;
     if (code === 23001) {
       // `key` conflict. Try again according to the latest extension information returned as needed.
     }
   });
}).catch(function(imError){
  // Failed to set message extensions
  console.warn('setMessageExtensions error:', imError);
});

:::
</dx-codeblock>


### Getting message extensions

Call the [getMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageExtensions) API to get the list of message extensions.

**API**

<dx-codeblock>
:::  js

tim.getMessageExtensions(message);

:::
</dx-codeblock>

**Parameters**

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| message            | Message  | Message instance |

> ? 
> The message must meet the following conditions:
- The `isSupportExtension` attribute of the message is set to `true`.
- The message is sent successfully.
- The message is not a message of a community group (Community) or audio-video group (AVChatRoom).

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getMessageExtensions(message);
promise.then(function(imResponse) {
  // Got message extensions successfully
   const { extensions } = imResponse.data;
   extensions.forEach((item) => {
     const { key, value } = item;
     // `key` - key in the message extension
     // `value` - value of the key in the message extension
   });
}).catch(function(imError){
  // Failed to get message extensions
  console.warn('getMessageExtensions error:', imError);
});

:::
</dx-codeblock>


### Deleting message extensions

Call the [deleteMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessageExtensions) API to delete message extensions. If `keyList` is not passed in, all message extensions will be cleared. After message extensions are successfully deleted, both the user and the recipient (one-to-one) or group members (Group) will receive the [TIM.EVENT.MESSAGE_EXTENSIONS_DELETED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_DELETED) event.

**API**

<dx-codeblock>
:::  js

tim.deleteMessageExtensions(message, keyList);

:::
</dx-codeblock>

**Parameters**

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| message            | Message  | Message instance |
| keyList            | Array\|undefined    | List of message extension keys |

> ? 
> 1. The message must meet the following conditions:
 - The `isSupportExtension` attribute of the message is set to `true`.
 - The message is sent successfully.
 - The message is not a message of a community group (Community) or audio-video group (AVChatRoom).
2. If multiple users set or delete the `key` of the same extension simultaneously, only the first user can operate successfully, and other users will receive the error code 23001 and the latest extension info, who can initiate the operation again if necessary.

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Delete message extension keys
let promise = tim.deleteMessageExtensions(message, ['a', 'b']);
promise.then(function(imResponse) {
   // Deleted message extensions successfully
   const { extensions } = imResponse.data;
   extensions.forEach((item) => {
     const { code, key, value } = item;
     if (code === 23001) {
       // `key` conflict. Try again according to the latest extension information returned as needed.
     }
   });
}).catch(function(imError){
  // Failed to delete message extensions
  console.warn('deleteMessageExtensions error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Clear all message extension keys
let promise = tim.deleteMessageExtensions(message);
promise.then(function(imResponse) {
   // Message extensions cleared successfully
   console.log('deleteMessageExtensions ok:', imResponse)
}).catch(function(imError){
  // Failed to clear the message extensions
  console.warn('deleteMessageExtensions error:', imError);
});

:::
</dx-codeblock>


### Updating message extensions

If you have registered the [TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_UPDATED) event in advance, and message extensions are added or updated, the SDK distributes the `TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED` event, and you can obtain the updated key-value information in the registered callback.

**Sample**

<dx-codeblock>
:::  js

let onMessageExtensionsUpdated = function(event) {
  const { messageID, extensions } = event.data;
  // `messageID` - Message ID
  // `extensions` - Message extension list
  extensions.forEach((item) => {
   const { key, value } = item;
   // `key` - key in the message extension
   // `value` - value of the key in the message extension
  });
};
tim.on(TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED, onMessageExtensionsUpdated);

:::
</dx-codeblock>

### Deleting message extensions

If you have registered the [TIM.EVENT.MESSAGE_EXTENSIONS_DELETED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_DELETED) event in advance, and message extensions are deleted, the SDK distributes the `TIM.EVENT.MESSAGE_EXTENSIONS_DELETED` event, and you can obtain the deleted `key` in the registered callback.
**Sample**

<dx-codeblock>
:::  js

let onMessageExtensionsDeleted = function(event) {
  const { messageID, keyList } = event.data;
  // `messageID` - Message ID
  // `keyList` - List of message extension keys deleted
  keyList.forEach((key) => {
   // console.log(key)
  });
};
tim.on(TIM.EVENT.MESSAGE_EXTENSIONS_DELETED, onMessageExtensionsDeleted);

:::
</dx-codeblock>
