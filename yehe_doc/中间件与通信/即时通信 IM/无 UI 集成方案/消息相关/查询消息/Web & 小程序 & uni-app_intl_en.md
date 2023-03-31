## Feature Description

You can call [findMessages](https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage) to query a local message by `messageID`.
1. Only local messages can be queried, for example, received messages or historical messages pulled by API.
2. Audio-video group (AVChatRoom) messages cannot be queried, as they are not saved locally.

>! This API is supported by v2.18.0 or later.

**API**

<dx-codeblock>
:::  js

tim.findMessage(messageID);

:::
</dx-codeblock>

**Parameter**

| Name      | Type   | Description |
| --------- | ------ | ----------- |
| messageID | String | Message ID  |

**Returned value**

Message instance [Message](https://web.sdk.qcloud.com/im/doc/en//Message.html) or `null`.

**Sample**

<dx-codeblock>
:::  js

// Find the message. This API is supported by v2.18.0 or later.
let message = tim.findMessage('144115217363870632-1647417469-77069006');
if (message) {
  // Read the attributes of `message`, such as `readReceiptInfo`
}

:::
</dx-codeblock>