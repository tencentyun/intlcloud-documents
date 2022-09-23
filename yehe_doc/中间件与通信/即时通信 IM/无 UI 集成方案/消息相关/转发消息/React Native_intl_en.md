## Feature Description

You can implement the feature of merging and forwarding messages as provided by WeChat in the following steps:

1. Create a merged message based on the list of original messages.
2. Send the merged message to the peer end.
3. The peer end receives the merged message and parses the list of original messages.

The title and digest are needed to display the merged message:

| Merge and Forward | Display of Merged Message | Click Merged Message to Download Message List for Display |
| ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| <img src="https://main.qcloudimg.com/raw/8f9a338c4e05cf1477250a5fc1a468c6.jpg" width = "300" /> | <img src="https://main.qcloudimg.com/raw/ff2afe17010e1840eae78e56d3abcf2d.jpg" width = "300" /> | <img src="https://main.qcloudimg.com/raw/a05b309924e59382dc928694d6397d20.jpg" width = "300"/> |

## Merging and Forwarding Messages

### Creating and sending a merged message

A merged message can be created by setting the message list along with the merged message title and digest. The process is as follows:

1. Call the `createMergerMessage` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#createMergerMessage)) to create a merged message. The list of original messages as well as the merged message title and digest also need to be set.

<img src="https://qcloudimg.tencent-cloud.cn/raw/27de8638efbd212c09452918db7f62ec.png" width = "450" />

| Attribute |  Description | Remarks |
| -------------- | ---------------- | -------------------------------------------------------------------------------------------------------------- |
| msgIDList | List of IDs of original messages | List of IDs of original messages to be merged and forwarded |
| title | Title | Title of the merged message, such as "Chat History of xixiyah and Hello" |
| abstractList | Digest list | Digest list of the merged message. The original message digests need to be displayed for the merged message, which will be unfolded after the user clicks the cell. |
| compatibleText | Compatibility text message | If the SDK on an early version does not support the merged message, the user will receive a text message with the content `compatibleText` by default. |

Below is the sample code for creating and sending a merged message:

```javascript
// List of messages to be forwarded, which can contain merged messages but not group tips
const msgIDList = ["msgid1", "msgid2"];
const title =  "Chat between user1 and user2";// Combined message title
const abstractList = ["user1:hello", "user2:hello"]; // Digest list of the merged message
const compatibleText = "The current version does not support the message"; // Compatibility text of the merged message. If the SDK on an early version does not support the merged message, the user will receive a text message with the content `compatibleText` by default.
const createMergerMessageResult =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createMergerMessage(
            msgIDList,
            title, // Title of the merged message
            abstractList, // Digest list of the merged message
            compatibleText,
          );
  if (createMergerMessageResult.code == 0) {
    TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(
          id: createMergerMessageResult.data.id,
          receiver: "",
          groupID: "",
        );
  }
```

### Receiving a merged message

#### Adding a listener

The receiver calls `addAdvancedMsgListener` ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#addAdvancedMsgListener)) to add the advanced message listener.
We recommend it be called early, such as after the chat page is initialized, to ensure timely message receiving in the application.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .addAdvancedMsgListener(listener);
```

#### Parsing a message

After the listener is added, the receiver will receive the merged message `V2TimMessage` in `onRecvNewMessage`.
You can use the merged message element `V2TimMergerElem` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimMergerElem.html)) to get the `title` and `abstractList` for UI display.
Then, when the user clicks the merged message, you can call the `downloadMergerMessage` ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#downloadMergerMessage)) to download the merged message list for UI display.

Below is the sample code:

```javascript
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_MERGER){
        message.mergerElem.abstractList;
        message.mergerElem.isLayersOverLimit;
        message.mergerElem.title;
        const download = await TencentImSDKPlugin.v2TIMManager.getMessageManager().downloadMergerMessage(message.msgID,);
        if(download.code == 0){
          const messageList = download.data;
        }
}
```

## Forwarding Messages One by One

To forward a single message, create a message identical to the original message through the `createForwardMessage` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#createForwardMessage)) first, and then call the `sendMessage` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#sendMessage)) to send the message.

Below is the sample code:

```javascript
// Create a message with the same elements as the original message
const createForwardMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createForwardMessage("msgid");
// Send the message to the user `denny`
  if(createForwardMessageRes.code == 0){
    TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: createForwardMessageRes.data.id, receiver: "denny", groupID: "");
  }
```


