## Creating a Message

### Creating a text message

This API is used to create a text message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a text message.

**API**

<dx-codeblock>
:::  js

tim.createTextMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | `userID` or `groupID` of the message receiver                |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (one-to-one conversation), `TIM.TYPES.CONV_GROUP` (group conversation). |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name | Type   | Description          |
| ---- | ------ | -------------------- |
| text | String | Message text content |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample**

<dx-codeblock>
:::  js

// Send a text message on web
// 1. Create a message instance. The returned instance can be displayed on the screen.
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, see https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    text: 'Hello world!'
  },
  // The read receipt feature is supported for one-to-one messages by v2.20.0 or later. To use it, purchase the Ultimate edition package and set `needReadReceipt` to `true` when creating a message.
  needReadReceipt: true
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

**Response**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).


### Creating an @ message

This API is used to create an @ text message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a text message.

>!
>- This API is supported by v2.9.0 or later.
>- It applies only to group chats, and @ all members is not supported for a community and its topic.

**API**

<dx-codeblock>
:::  js

tim.createTextAtMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | `userID` or `groupID` of the message receiver                |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (one-to-ont conversation), `TIM.TYPES.CONV_GROUP` (group conversation). |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name       | Type   | Description                                                  |
| ---------- | ------ | ------------------------------------------------------------ |
| text       | String | Text content                                                 |
| atUserList | Array  | List of users that need to be mentioned (@). To mention (@) all, pass in [TIM.TYPES.MSG_AT_ALL](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_AT_ALL). For example, to mention (@) `denny` and `lucy` as well as all members, pass in ['denny', 'lucy', TIM.TYPES.MSG_AT_ALL] for `atUserList`. |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample**

<dx-codeblock>
:::  js

// Send a text message on web
// 1. Create a message instance. The returned instance can be displayed on the screen.
let message = tim.createTextAtMessage({
  to: 'group1',
  conversationType: TIM.TYPES.CONV_GROUP,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    text: '@denny @lucy @all Dinner tonight. Reply 1 if you receive this message',
    atUserList: ['denny', 'lucy', TIM.TYPES.MSG_AT_ALL] // 'denny' and 'lucy' are `userID` values, not nicknames
  },
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

### Creating an image message

This API is used to create an image message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send an image message.

>!
>- File objects can be passed in on v2.3.1 or later.
>- File messages such as images can be sent via uni-app on v2.11.2 or later.
>- WebP images are supported by v2.17.0 or later.


**API**

<dx-codeblock>
:::  js

tim.createImageMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type     | Default                       | Description                                                  |
| ---------------- | -------- | ----------------------------- | ------------------------------------------------------------ |
| to               | String   | -                             | Message receiver                                             |
| conversationType | String   | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C`, `TIM.TYPES.CONV_GROUP`. |
| priority         | String   | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object   | -                             | Message content container                                    |
| onProgress       | function | -                             | Callback function for getting the upload progress            |
| cloudCustomData  | String   | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name | Type                       | Description                                                  |
| ---- | -------------------------- | ------------------------------------------------------------ |
| file | HTMLInputElement \| Object | It is used to select a DOM node (web) or `File` object (web) of the image. The SDK reads the data contained in this parameter and uploads the image. |


**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).


**Sample for web**
<dx-codeblock>
:::  js

// Sample 1: Sending an image message on web - passing in a DOM node
// 1. Create a message instance. The returned instance can be displayed on the screen.
let message = tim.createImageMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    file: document.getElementById('imagePicker'),
  },
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
  onProgress: function(event) { console.log('file uploading:', event) }
});

// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Sample 2: Sending an image message on web - passing in a File object
// Add a message input box with the ID set to `testPasteInput`, for example, <input type="text" id="testPasteInput" placeholder="Take a screenshot and paste it in the input box" size="30" />
document.getElementById('testPasteInput').addEventListener('paste', function(e) {
  let clipboardData = e.clipboardData;
  let file;
  let fileCopy;
  if (clipboardData && clipboardData.files && clipboardData.files.length > 0) {
    file = clipboardData.files[0];
    // After the image message is sent successfully, the content pointed to by `file` may be cleared by the browser. If you have extra rendering needs, you can copy the data in advance.
    fileCopy = file.slice();
  }

  if (typeof file === 'undefined') {
    console.warn('The `file` is `undefined`. Check for the compatibility of the code or browser.');
    return;
  }

  // 1. Create a message instance. The returned instance can be displayed on the screen.
  let message = tim.createImageMessage({
    to: 'user1',
    conversationType: TIM.TYPES.CONV_C2C,
    payload: {
      file: file
    },
    onProgress: function(event) { console.log('file uploading:', event) }
  });

  // 2. Send the message.
  let promise = tim.sendMessage(message);
  promise.then(function(imResponse) {
    // The message sent successfully
    console.log(imResponse);
  }).catch(function(imError) {
    // Failed to send the message
    console.warn('sendMessage error:', imError);
  });
});

:::
</dx-codeblock>



### Creating an audio message

This API is used to create an audio message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send an audio message. 

**API**

<dx-codeblock>
:::  js

tim.createAudioMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | Message receiver                                             |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C`, `TIM.TYPES.CONV_GROUP`. |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name | Type   | Description                               |
| ---- | ------ | ----------------------------------------- |
| file | Object | File information obtained after recording |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).



### Creating a video message

This API is used to create a video message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a video message.

>!
>- This API can be used in the web environment on v2.6.0 or later.
>- The SDK supports video thumbnails [snapshotUrl](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload) on v2.17.0 or later, and uses [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin) as the upload plugin.

**API**

<dx-codeblock>
:::  js

tim.createVideoMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | Message receiver                                             |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C`, `TIM.TYPES.CONV_GROUP`. |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name | Type                               | Description                      |
| ---- | ---------------------------------- | -------------------------------- |
| file | HTMLInputElement \| File \| Object | Data field of the custom message |


**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample for web**

<dx-codeblock>
:::  js

// Sample: Sending a video message on web (supported by v2.6.0 or later)
// 1. Get the video file by passing in the DOM node.
// 2. Create a message instance.
const message = tim.createVideoMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    file: document.getElementById('videoPicker') // Alternatively, use `event.target`
  },
  onProgress: function(event) { console.log('file uploading:', event) }
});
// 3. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

**Sample for uni-app**

<dx-codeblock>
:::  js

// Send a video message via uni-app. Before using this API, upgrade your SDK to v2.16.2 or later and upgrade tim-upload-plugin to v1.0.2 or later.
// 1. Select a video.
uni.chooseVideo({
  count: 1,
  sourceType: ['camera', 'album'], // Specify whether the video is from an album or a camera. Both are included by default.
  maxDuration: 60, // Maximum duration, which is 60s
  camera: 'back', // Rear camera
  success: function(res) {
    let message = tim.createVideoMessage({
      to: 'user1',
      conversationType: TIM.TYPES.CONV_C2C,
      payload: { file: res },
      onProgress: function(event) { console.log('file uploading:', event) }
    });
    // 2. Send the message.
    let promise = tim.sendMessage(message);
    promise.then(function(imResponse) {
      // The message sent successfully
      console.log(imResponse);
    }).catch(function(imError) {
      // Failed to send the message
      console.warn('sendMessage error:', imError);
    });
  }
})

:::
</dx-codeblock>

### Creating a custom message

This API is used to create a custom message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a custom message. When the current SDK capabilities cannot meet your needs, you can customize messages.

**API**

<dx-codeblock>
:::  js

tim.createCustomMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | `userID` or `groupID` of the message receiver                |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (one-to-one conversation), `TIM.TYPES.CONV_GROUP` (group conversation). |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name        | Type   | Description                       |
| ----------- | ------ | --------------------------------- |
| data        | String | Data of the custom message        |
| description | String | Description of the custom message |
| extension   | String | Extension of the custom message   |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample**

<dx-codeblock>
:::  js

// Sample: Using a custom message to implement dice rolling
// 1. Define the random function.
function random(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}
// 2. Create a message instance. The returned instance can be displayed on the screen.
let message = tim.createCustomMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_HIGH,
  payload: {
    data: 'dice', // Used to identify the message as a dice message
    description: String(random(1,6)), // Get the outcome
    extension: ''
  }
});
// 3. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

### Creating an emoji message

This API is used to create an emoji message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send an emoji message.

**API**

<dx-codeblock>
:::  js

tim.createFaceMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | `userID` or `groupID` of the message receiver                |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (one-to-one conversation), `TIM.TYPES.CONV_GROUP` (group conversation). |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name  | Type   | Description                                  |
| ----- | ------ | -------------------------------------------- |
| index | Number | Emoji index, which is customized by the user |
| data  | String | Extra data                                   |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample**

<dx-codeblock>
:::  js

// Send an emoji message on web
// 1. Create a message instance. The returned instance can be displayed on the screen.
let message = tim.createFaceMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    index: 1, // Number. Emoji index, which is customized by the user
    data: 'tt00' // String. Extra data
  },
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>


### Creating a file message

This API is used to create a file message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a file message.

>! 
>- File objects can be passed in on v2.3.1 or later.
>- The maximum file size is adjusted to 100 MB starting from v2.4.0.
>- File messages can be sent via uni-app on v2.16.2 or later. To use this feature, upgrade [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin) to v1.0.2 or later.

**API**

<dx-codeblock>
:::  js

tim.createFileMessage(options);

:::
</dx-codeblock>


**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type     | Default                       | Description                                                  |
| ---------------- | -------- | ----------------------------- | ------------------------------------------------------------ |
| to               | String   | -                             | `userID` or `groupID` of the message receiver                |
| conversationType | String   | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (client to client conversation), `TIM.TYPES.CONV_GROUP` (group conversation). |
| priority         | String   | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object   | -                             | Message content container                                    |
| onProgress       | function | -                             | Callback function for getting the upload progress            |
| cloudCustomData  | String   | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name | Type                               | Description                                                  |
| ---- | ---------------------------------- | ------------------------------------------------------------ |
| file | HTMLInputElement \| File \| Object | It is used to select a DOM node or `File` object of the file on web, or the success callback parameter of the uni.chooseFile API. The SDK reads the data contained in this parameter and uploads the file. |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample for web**

<dx-codeblock>
:::  js

// Sample 1: Sending a file message on web - passing in a DOM node
// 1. Create a file message instance. The returned instance can be displayed on the screen.
let message = tim.createFileMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    file: document.getElementById('filePicker'),
  },
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
  onProgress: function(event) { console.log('file uploading:', event) }
});

// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Sample 2: Sending a file message on web - passing in a File object
// Add a message input box with the ID set to `testPasteInput`, for example, <input type="text" id="testPasteInput" placeholder="Take a screenshot and paste it in the input box" size="30" />
document.getElementById('testPasteInput').addEventListener('paste', function(e) {
  let clipboardData = e.clipboardData;
  let file;
  let fileCopy;
  if (clipboardData && clipboardData.files && clipboardData.files.length > 0) {
    file = clipboardData.files[0];
    // After the image message is sent successfully, the content pointed to by `file` may be cleared by the browser. If you have extra rendering needs, you can copy the data in advance.
    fileCopy = file.slice();
  }

  if (typeof file === 'undefined') {
    console.warn('The `file` is `undefined`. Check for the compatibility of the code or browser.');
    return;
  }

  // 1. Create a message instance. The returned instance can be displayed on the screen.
  let message = tim.createFileMessage({
    to: 'user1',
    conversationType: TIM.TYPES.CONV_C2C,
    payload: {
      file: file
    },
    onProgress: function(event) { console.log('file uploading:', event) }
  });

  // 2. Send the message.
  let promise = tim.sendMessage(message);
  promise.then(function(imResponse) {
    // The message sent successfully
    console.log(imResponse);
  }).catch(function(imError) {
    // Failed to send the message
    console.warn('sendMessage error:', imError);
  });
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Send a file message via uni-app. Before using this API, upgrade your SDK to v2.16.2 or later and upgrade tim-upload-plugin to v1.0.2 or later.
// 1. Select a file.
uni.chooseFile({
  count: 1,
  extension:['.zip','.doc'],
  success: function(res) {
    let message = tim.createFileMessage({
      to: 'user1',
      conversationType: TIM.TYPES.CONV_C2C,
      payload: { file: res },
      onProgress: function(event) { console.log('file uploading:', event) }
    });
    // 2. Send the message.
    let promise = tim.sendMessage(message);
    promise.then(function(imResponse) {
      // The message sent successfully
      console.log(imResponse);
    }).catch(function(imError) {
      // Failed to send the message
      console.warn('sendMessage error:', imError);
    });
  }
});

:::
</dx-codeblock>

### Creating a geographical location message

This API is used to create a geographical location message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a geographical location message.

>! This API is supported by v2.15.0 or later.

**API**

<dx-codeblock>
:::  js

tim.createLocationMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | `userID` or `groupID` of the message receiver                |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (one-to-one conversation), `TIM.TYPES.CONV_GROUP` (group conversation). |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name        | Type   | Description                              |
| ----------- | ------ | ---------------------------------------- |
| description | String | Description of the geographical location |
| longitude   | Number | Longitude                                |
| latitude    | Number | Latitude                                 |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample**

<dx-codeblock>
:::  js

// Send a geographical location message on web (supported by v2.15.0 or later)
// 1. Create a message instance. The returned instance can be displayed on the screen.
let message = tim.createLocationMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    description: 'Tencent Building, No. 10000, Shennan Boulevard, Shenzhen',
    longitude: 113.941079, // Longitude
    latitude: 22.546103 // Latitude
  }
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

### Creating a merged message

This API is used to create a merged message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a merged message.

>!
>- This API is supported by v2.10.1 or later.
>- This API does not support merging messages that failed to be sent. If the message list contains a message that failed to be sent, the API will report an error.

**API**

<dx-codeblock>
:::  js

tim.createMergerMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type   | Default                       | Description                                                  |
| ---------------- | ------ | ----------------------------- | ------------------------------------------------------------ |
| to               | String | -                             | `userID` or `groupID` of the message receiver                |
| conversationType | String | -                             | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (one-to-one conversation), `TIM.TYPES.CONV_GROUP` (group conversation). |
| priority         | String | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority                                             |
| payload          | Object | -                             | Message content container                                    |
| cloudCustomData  | String | ''                            | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |

The `payload` is as described below:

| Name           | Type   | Description                                                  |
| -------------- | ------ | ------------------------------------------------------------ |
| messageList    | Array  | Merged message list                                          |
| title          | String | Title of merged messages, for example, "Chat History of the Talent Center in the Greater Bay Area" |
| abstractList   | String | Abstract list. You can set abstract information in different formats for different message types, for example, in the `sender:text` format for a text message, in the `sender:[image]` format for an image message, or in the `sender:[file]` format for a file message. |
| compatibleText | String | Compatibility text. If the SDK on an early version does not support the merged message, the user will receive a text message with the content `${compatibleText}` by default. This field is required. |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample**

<dx-codeblock>
:::  js

// 1. Forward group messages to a one-to-one conversation.
// `message1`, `message2`, and `message3` are group messages.
let mergerMessage = tim.createMergerMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    messageList: [message1, message2, message3],
    title: 'Chat History of the Talent Center in the Greater Bay Area',
    abstractList: ['allen: 666', 'iris: [Image]', 'linda: [File]'],
    compatibleText: 'Upgrade your IM SDK to v2.10.1 or later to view this message.'
  },
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
});

// 2. Send the message.
let promise = tim.sendMessage(mergerMessage);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

## Downloading a Merged Message

This API is used to download a merged message. When the merged message sent by the sender is large in size, the SDK will store it in the cloud, and the message receiver needs to download it from the cloud before viewing it.

>! This API is supported by v2.10.1 or later.

<dx-codeblock>
:::  js

tim.downloadMergerMessage(message);

:::
</dx-codeblock>

**Parameter**

| Name    | Type    | Description      |
| ------- | ------- | ---------------- |
| message | Message | Message instance |


**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// If `downloadKey` exists, the received merged message is stored in the cloud and needs to be downloaded first.
if (message.type === TIM.TYPES.MSG_MERGER && message.payload.downloadKey !== '') {
  let promise = tim.downloadMergerMessage(message);
  promise.then(function(imResponse) {
    // After the download is successful, the SDK will update information such as `message.payload.messageList`.
    console.log(imResponse.data);
  }).catch(function(imError) {
    // Download failed
    console.warn('downloadMergerMessage error:', imError);
  });
}

:::
</dx-codeblock>

## Forwarding Messages One by One

To forward a single message, create a message identical to the original message through the [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) API first, and then call the [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) API to send the message.

>!
>- This API is supported by v2.10.1 or later.
>- It supports forwarding a single message or several messages one by one.

**API**

<dx-codeblock>
:::  js

tim.createForwardMessage(message);

:::
</dx-codeblock>

**Parameter**

| Name    | Type    | Description      |
| ------- | ------- | ---------------- |
| message | Message | Message instance |

**Sample**

<dx-codeblock>
:::  js

let forwardMessage = tim.createForwardMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: message, // The received or sent message instance
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
});
// 2. Send the message.
let promise = tim.sendMessage(forwardMessage);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

### Sending a message

This API is used to send a message. You need to call any of the following message instance creation APIs to create a message instance first before calling this API to send the message instance.

- [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage)
- [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextAtMessage)
- [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage)
- [createAudioMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage)
- [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage)
- [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage)
- [createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage)
- [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage)
- [createLocationMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createLocationMessage)
- [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage)
- [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage)

>!
>- When this API is called to send a message instance, the SDK must be in the `ready` status; otherwise, the message instance cannot be sent. The SDK status can be obtained by listening for the `TIM.EVENT.SDK_READY` event, which will be triggered when the SDK is in the `ready` status.
>TIM.EVENT.SDK_NOT_READY: Triggered when the SDK is in the `not ready` status
>- The [TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) event must be listened for in order to receive newly pushed one-to-one messages, group messages, group tips, or group system notifications.
>- Messages sent by this API will not trigger the [TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) event. Messages sent by the same account from another client (or through the RESTful API) will trigger the [TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) event.
>- Offline push applies only to Android or iOS devices but is not supported for web.
>- `onlineUserOnly` and `messageControlInfo` cannot be used together.

<dx-codeblock>
:::  js

tim.sendMessage(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name    | Type    | Description                                                  |
| ------- | ------- | ------------------------------------------------------------ |
| message | Message | Message instance                                             |
| options | Object  | Message sending option (message content container), which is optional |

The `options` is as described below:

| Name               | Type    | Description                                                  |
| ------------------ | ------- | ------------------------------------------------------------ |
| onlineUserOnly     | Boolean | This parameter is supported by v2.6.4 or later. It specifies whether the message is sent only to online users and defaults to `false`. If it is set to `true`, the message will not be stored on the roaming server, nor counted as an unread message, nor pushed to the receiver offline. It is suitable for sending unimportant tips such as broadcast notifications. This parameter is not supported when a message is sent in an audio-video group (AVChatRoom). |
| offlinePushInfo    | Object  | This parameter is supported by v2.6.4 or later. For more information, see [Offline Push](https://intl.cloud.tencent.com/document/product/1047/33525). |
| messageControlInfo | Object  | This parameter is supported by v2.16.0 or later. It is a message control configuration item. |

The `offlinePushInfo` is as described below:

| Name                 | Type    | Description                                                  |
| -------------------- | ------- | ------------------------------------------------------------ |
| disablePush          | Boolean | true: offline push is disabled; false (default): offline push is enabled. |
| title                | String  | Offline push title. This parameter is used by both iOS and Android. |
| description          | String  | Offline push content. This parameter will overwrite the offline push display text of the message instance. If the sent message is a custom message, this parameter will overwrite `message.payload.description`. If both `description` and `message.payload.description` are left empty, the receiver cannot receive the offline push notification of the custom message. |
| extension            | String  | Content passed through by offline push                       |
| ignoreIOSBadge       | Boolean | Specifies whether the badge count is ignored (applicable to iOS only). If this parameter is set to `true`, the unread message count on the application badge will not increase when the message is received by the iOS device. |
| androidOPPOChannelID | String  | Offline push channel ID for OPPO phones that run Android v8.0 or later |

The `messageControlInfo` is as described below:

| Name                    | Type    | Description                                                  |
| ----------------------- | ------- | ------------------------------------------------------------ |
| excludedFromUnreadCount | Boolean | true: `unreadCount` of the conversation is not updated (the message is stored on the roaming server); false (default) |
| excludedFromLastMessage | Boolean | true: `lastMessage` of the conversation is not updated (the message is stored on the roaming server); false (default) |

**Response**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// If the receiver is offline, the message will be stored on the roaming server and pushed offline on the precondition that the receiver's application switches to the background or the process is killed. The default title and content of offline push are kept.
// For more information on offline push, see https://intl.cloud.tencent.com/document/product/1047/33525.
tim.sendMessage(message);

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// The message sending option is supported by v2.6.4 or later.
tim.sendMessage(message, {
  onlineUserOnly: true // If the receiver is offline, the message will be neither stored on the roaming server nor pushed offline.
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// The message sending option is supported by v2.6.4 or later.
tim.sendMessage(message, {
  offlinePushInfo: {
    disablePush: true // If the receiver is offline, the message will be stored on the roaming server, but will not be pushed offline.
  }
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// The message sending option is supported by v2.6.4 or later.
tim.sendMessage(message, {
  // If the receiver is offline, the message will be stored on the roaming server and pushed offline on the precondition that the receiver's application switches to the background or the process is killed. The title and content of offline push can be customized at the access side.
  offlinePushInfo: {
    title: '', // Offline push title
    description: '', // Offline push content
    androidOPPOChannelID: '' // Offline push channel ID for OPPO phones that run Android v8.0 or later for offline push
  }
});
:::
</dx-codeblock>

<dx-codeblock>
:::  js

// The message control option is supported by v2.16.0 or later.
tim.sendMessage(message, {
  messageControlInfo: {
    excludedFromUnreadCount: true, // `unreadCount` of the conversation is not updated (the message is stored on the roaming server).
    excludedFromLastMessage: true // `lastMessage` of the conversation is not updated (the message is stored on the roaming server).
  }
});

:::
</dx-codeblock>
