## Feature Description

Message receiving needs to be implemented through event listening.

## Listening for an Event

>! Call this API to listen for events before calling the [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) API in order to avoid missing the events delivered by the SDK.

**API**

<dx-codeblock>
:::  js

tim.on(eventName, handler, context);

:::
</dx-codeblock>

**Parameter**

| Name      | Type           | Description                                                  |
| --------- | -------------- | ------------------------------------------------------------ |
| eventName | String         | Event name. All event names are stored in the `TIM.EVENT` variable. To view all the events, use `console.log(TIM.EVENT)`. The event list is [here](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html). |
| handler   | Function       | Event handling method. When an event is triggered, this handler will be called to handle it. |
| context   | * \| undefined | The context expected for handler execution                   |

**Returned value**

None

**Sample**

<dx-codeblock>
:::  js

let onMessageReceived = function(event) {
  // event.data - An array that stores `Message` objects - [Message]
  const messageList = event.data;
  messageList.forEach((message) => {
    if (message.type === TIM.TYPES.MSG_TEXT) {
      // Text message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.TextPayload
    } else if (message.type === TIM.TYPES.MSG_IMAGE) {
      // Image message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.ImagePayload
    } else if (message.type === TIM.TYPES.MSG_SOUND) {
      // Audio message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.AudioPayload
    } else if (message.type === TIM.TYPES.MSG_VIDEO) {
      // Video message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload
    } else if (message.type === TIM.TYPES.MSG_FILE) {
      // File message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.FilePayload
    } else if (message.type === TIM.TYPES.MSG_CUSTOM) {
      // Custom message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.CustomPayload
    } else if (message.type === TIM.TYPES.MSG_MERGER) {
      // Merged message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.MergerPayload
    } else if (message.type === TIM.TYPES.MSG_LOCATION) {
      // Geographical location message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.LocationPayload
    } else if (message.type === TIM.TYPES.MSG_GRP_TIP) {
      // Group tip message - https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload
    } else if (message.type === TIM.TYPES.MSG_GRP_SYS_NOTICE) {
      // Group system notification - https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupSystemNoticePayload
    }
  });
};
tim.on(TIM.EVENT.MESSAGE_RECEIVED, onMessageReceived);

:::
</dx-codeblock>

## Canceling Event Listening

**API**

<dx-codeblock>
:::  js

tim.off(eventName, handler, context, once);

:::
</dx-codeblock>

**Parameter**

| Name      | Type                 | Description                                                  |
| --------- | -------------------- | ------------------------------------------------------------ |
| eventName | String               | Event name. All event names are stored in the `TIM.EVENT` variable. To view all the events, use `console.log(TIM.EVENT)`. The event list is [here](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html). |
| handler   | Function             | Event handling method. When an event is triggered, this handler will be called to handle it. |
| context   | * \| undefined       | The context expected for handler execution                   |
| once      | Boolean \| undefined | Whether to unbind only once                                  |

**Returned value**

None

**Sample**

<dx-codeblock>
:::  js

let onMessageReceived = function(event) {
  // A newly pushed one-to-one message, group message, group tip, or group system notification is received. You can traverse `event.data` to get the message list and render it to the UI.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - An array that stores `Message` objects - [Message]
};
tim.off(TIM.EVENT.MESSAGE_RECEIVED, onMessageReceived);

:::
</dx-codeblock>