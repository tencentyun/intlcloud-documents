## Feature Description
You can merge and forward messages in the following steps:
1. Create a merged message based on the list of original messages.
2. Send the merged message to the receiver.
3. The receiver receives the merged message and parses the list of original messages.

The title and digest are needed to display the merged message, as shown below:

| Merge and Forward                                            | Display of Merged Message                                    | Click Merged Message to Download Message List for Display    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/cb970fdd471cdd668b5ce31d188970fd.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/2304c7ea1e29de702f99d96e52a9739c.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/f2c81dc8df0064cf8202d06a79f7af16.png" width = "219"/> |

## Creating a Merged Message

This API is used to create a merged message. It returns a message instance, which can be sent by calling the [sendMessage](https://web.sdk.qcloud.com/im/doc/en//SDK.html#sendMessage) API when you need to send a merged message.

>!
>- This API is supported by v2.10.1 or later.
>- Unable to merge messages that failed to be sent. If the message list contains a message that failed to be sent, the API will report an error.

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
| abstractList   | String | Digest list. You can set digest information in different formats for different message types, for example, in the `sender:text` format for a text message, in the `sender:[image]` format for an image message, or in the `sender:[file]` format for a file message. |
| compatibleText | String | Compatibility text. If the early SDK version does not support the merged message, the user will receive a text message with the content `${compatibleText}` by default. This field is required. |

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
  // Message sent successfully
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

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html).

**Sample**

<dx-codeblock>
:::  js

let forwardMessage = tim.createForwardMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: message, // Message instance for the received or sent message
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
});
// 2. Send the message.
let promise = tim.sendMessage(forwardMessage);
promise.then(function(imResponse) {
  // Message sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>