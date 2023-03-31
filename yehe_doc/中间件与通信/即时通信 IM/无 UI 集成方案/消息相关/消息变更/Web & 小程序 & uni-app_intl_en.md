## Feature Description
This feature enables any member in a conversation to modify a successfully sent message in the conversation. The message will be synced to all the members in the conversation once modified successfully.

## Modifying a Message

This API is used to modify a message. After a user modifies a message successfully, both the user and the receiver (one-to-one) or group members (Group) will receive the [MESSAGE_MODIFIED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_MODIFIED) event.

>!
>- This API is supported by v2.20.0 or later.
>- It does not support modifying online messages or audio-video group messages. Do not modify the `random`, `sequence`, or `time` fields of a message.
>- It only supports modifying text, custom, geographical location, and emoji messages.
>- If a message is modified by another member during modification, the SDK will return the error code 2480, indicating that a conflict occurred while modifying the message.

*API**

<dx-codeblock>
:::  js

tim.modifyMessage(message);

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

// Listen for the `MESSAGE_MODIFIED` event, which will be delivered by the SDK after a message is modified successfully
let onMessageModified = function(event) {
  // event.data - An array that stores modified Message objects - [Message]
};
tim.on(TIM.EVENT.MESSAGE_MODIFIED, onMessageModified);

// Change the text content of `txtMessage` to `Hello Tencent`
txtMessage.payload.text = "Hello Tencent";

let promise = tim.modifyMessage(txtMessage);
promise.then(function(imResponse) {
  const { message } = imResponse.data;
  // Message modified successfully. `message` is the latest message.
}).catch(function(imError) {
  // Failed to modify the message
  const { code, data } = imError;
  if (code === 2480) {
    // A conflict occurred while modifying the message. `data.message` is the latest message.
  } else if (code === 2481) {
    // Audio-video group messages cannot be modified.
  } else if (code === 20026) {
    // The message does not exist.
  }
});

:::
</dx-codeblock>