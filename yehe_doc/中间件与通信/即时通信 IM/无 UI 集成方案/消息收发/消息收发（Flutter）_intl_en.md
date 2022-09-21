## Message Classification
IM messages are classified by message destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type       | API Keyword  | Description                                                                                                                                                          |
| ------------------ | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| One-to-one message | C2CMessage   | Also called C2C message. When sending a one-to-one message, you must specify the `UserID` of the message recipient, and only the recipient can receive this message. |
| Group message      | GroupMessage | When sending a group message, you must specify the `groupID` of the target group, and all users in this group can receive this message.                              |

IM messages can also be classified by content into text messages, custom (signaling) messages, image messages, video messages, voice messages, file messages, location messages, combined messages, and group tips.

| Message Type     | API Keyword   | Description                                                                                                                                                                                                                               |
| ---------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text message     | TextElem      | It refers to a common text message.                                                                                                                                                                                                       |
| Custom message   | CustomElem    | It is a section of binary buffer and often used to transfer custom signaling in your application.                                                                                                                                         |
| Image message    | ImageElem     | When the IM SDK sends an original image, it automatically generates two images in different sizes. The three images are called the original image, large image, and thumbnail.                                                            |
| Video message    | VideoElem     | A video message contains a video file and an image.                                                                                                                                                                                       |
| Voice message    | SoundElem     | It supports displaying a red dot upon playback of the voice message.                                                                                                                                                                      |
| File message     | FileElem      | A file message cannot exceed 100 MB.                                                                                                                                                                                                      |
| Location message | LocationElem  | A location message contains three fields: location description, longitude, and latitude.                                                                                                                                                  |
| Combined message | MergerElem    | Up to 300 messages can be combined.                                                                                                                                                                                                       |
| Group tip        | GroupTipsElem | A group tip is often used to carry a system notification in a group, such as a notification indicating the following: a member joins or leaves the group; the group description is modified; or the profile of a group member is changed. |

## Sending and Receiving Simple Messages
There are two categories of messages in the IM Flutter SDK: simple messages and rich media messages. The first category is introduced here. V2TIMManager.getMessageManager() provides a set of APIs for sending and receiving simple messages. You can directly use these APIs to send and receive text messages and custom (signaling) messages. This is not recommended for an SDK of v3.6.0 or later. In this case, you are advised to use rich media messages in the following two steps: create the corresponding [V2TimMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html), and then call the [sendMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html) API.  

Simple messages:

There are two types of simple messages in the IM Flutter SDK: [text messages (V2TimTextElem)](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimTextElem.html) and [custom messages (V2TimCustomElem)](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimCustomElem.html). However, the following APIs for sending simple messages are not recommended for an SDK of v3.6.0 or later.

- [sendC2CTextMessage](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/sendC2CTextMessage.html) (not recommended for v3.6.0 or later) 
- [sendGroupTextMessage](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/sendGroupTextMessage.html) (not recommended for v3.6.0 or later) 
- [sendC2CCustomMessage](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/sendC2CCustomMessage.html) (not recommended for v3.6.0 or later) 
- [sendGroupCustomMessage](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/sendGroupCustomMessage.html) (not recommended for v3.6.0 or later) 

### Sending text and signaling messages
Recommended message sending method (take sending text messages as an example):

```dart
    V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createTextMessage(text: "The text to create");
    String id = createMessage.data!.id!; // The message creation ID returned

    V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .sendMessage(
            id: id, // Pass in the message creation ID to
            receiver: "The userID of the destination user",
            groupID: "The groupID of the destination group",
            );
```
After `createMessage` is complete, a message creation ID will be returned. You just need to pass in this ID to `sendMessage` to send the message. `sendMessage` is a common method for all types of messages. You need to specify either `receiver` or `groupID` and leave the other empty.

>! You can first call `createMessage` and then call `sendMessage` to send C2C custom (signaling) messages. A custom message is essentially a section of binary buffer, and is often used to transfer custom signaling in your app.  In addition, the IM Flutter SDK has encapsulated another signaling for you (to be introduced later).

### Receiving text and signaling messages
You can listen for simple text and signaling messages with [addSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/addSimpleMsgListener.html). To listen for complex messages such as images, videos, and voices, call [addAdvancedMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html) defined in v2TIMManager.getMessageManager().

>? Do not mix up [addSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/addSimpleMsgListener.html) and [addAdvancedMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html) to avoid logic bugs.

### Typical example: Sending and receiving on-screen comments
In the live streaming scenario, it is a common way of communication to send or receive on-screen comments in an audio-video group. This can be easily implemented.

1. An anchor calls [createGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/createGroup.html) to create an audio-video group (AVChatRoom) and records the group ID in the list of live rooms.
2. The audience select an anchor they like, and call [joinGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/joinGroup.html) to join the AVChatRoom created by this anchor.
3. A message sender calls [createTextMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextMessage.html) and [sendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) to send text messages as on-screen comments.
4. A message recipient calls [addSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/addSimpleMsgListener.html) to register a simple message listener, and use the listener callback function [onRecvGroupTextMessage](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSimpleMsgListener/V2TimSimpleMsgListener/onRecvGroupTextMessage.html) to obtain text messages.

"FlyHeart" is an instruction. To configure the "FlyHeart" feature for a live room, perform the steps below:
1. Define a custom message type, such as a JSON string `{ "command": "favor", "value": 101 }`.
2. Call [createCustomMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html) and [sendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) to send messages, and call [onRecvGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a46b48869e411b41c25a98211d951335c) to receive messages.

## Sending and Receiving Rich Media Messages
Image, video, voice, file, and location messages are called rich media messages.
- To send a rich media message, create a [V2TimMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html) object with the `create` function, and call the `send` API.
- To receive a rich media message, first check `elemType` and perform secondary parsing on `Elem` obtained based on `elemType`.

### Sending rich media messages
The following takes an image message as an example to describe the process of sending a rich media message.
1. The message sender calls [createImageMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createImageMessage.html) to create an image message, and gets the ID of the message object [V2TimMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html) (please note that this ID is not `messageId`).
2. The sender calls the [sendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) API to pass in the ID of the message object created to send the message.

### Receiving rich media messages
1. The recipient calls the [addAdvancedMsgListener](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html) API to set the advanced message listener.
2. The recipient obtains the image message [V2TIMMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html) by listening for the callback of [onRecvNewMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnRecvNewMessageCallback.html).
3. The recipient parses `elemType` in [V2TIMMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html), and performs secondary parsing based on the message type to obtain the content of `Elem` in the message.

### Typical example: Sending and receiving image messages
The sender creates and sends an image message.
```dart
// Create an image message
    V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createImageMessage(
              imagePath: image.path,
              fileName: 'test.png',
              fileContent: fileContent, // Required for the web
            );
// Get the returned ID
    String id = createMessage.data!.id!;
// Pass in ID to send the message
    V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .sendMessage(
            id: id,
            receiver: "The userID of the destination user",
            groupID: "The groupID of the destination group",
         );
```

The recipient recognizes an [image message](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_image_elem/V2TimImageElem-class.html) and parses the original image, large image, and thumbnail in the message.
```dart
  // For v3.9.0 or later, you can include V2TIM_IMAGE_TYPE to get enumerated values.
  static const V2_TIM_IMAGE_TYPES = {
    'ORIGINAL': 0,
    'BIG': 1,
    'SMALL': 2,
  };


 void onRecvNewMessage(V2TimMessage message) {
	int elemType = message.elemType;
	 V2TimImage? img;
    // Priority: thumbnail, large image, and original image
    img = message.imageElem!.imageList?.firstWhere(
        (e) => e!.type == V2_TIM_IMAGE_TYPES['ORIGINAL'],
        orElse: () => null);
    img = message.imageElem!.imageList?.firstWhere(
        (e) => e!.type == V2_TIM_IMAGE_TYPES['BIG'],
        orElse: () => null);
    img = message.imageElem!.imageList?.firstWhere(
        (e) => e!.type == V2_TIM_IMAGE_TYPES['SMALL'],
        orElse: () => null);
    if (img == null) {
     // ....
    }
    // ....
}
```


## Sending and Receiving Group @ Messages
For a group @ message, the sender can listen for the input of the @ character in the text box and call the group member selection interface. After selection is completed, the text box displays the content in the format of `"@A @B @C......"`, and then the sender can continue to edit the message content and send the message. On the group chat list of the recipient’s conversation interface, the identifier `"someone@me"` or `"@all members"` will be displayed to remind the user that the user was mentioned by someone in the group.
>? Currently, only text @ messages are supported.


### Sending group @ messages
1. The sender listens for the text box on the chat interface and launches the group member selection interface. After selection is completed, the IDs and nicknames of the selected members are returned. The ID is used to construct the message object [V2TimMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html), and the nickname is to be displayed in the text box.
2. The sender calls [createTextAtMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextAtMessage.html) of v2TIMManager.getMessageManager() to create a text @ message and gets the message object [V2TimMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html).
3. The sender calls the [sendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) API to send the @ message object created.

### Receiving group @ messages
1. During conversation loading and update, call the [OnConversationChangedCallback](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html) API of [V2TIMConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html) to get the @ list of the conversation. In the future, `getGroupAtInfoList` will be available for manually getting the `atInfoList`.
2. Obtain the @ data type with the [atType](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupAtInfo.html#attype) API of the [V2TIMGroupAtInfo](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_group_at_info/V2TimGroupAtInfo-class.html) object on the list, and update it to the @ information of the current conversation.

### Typical examples: sending and receiving group @ messages
- **Sending a group @ message**:
The sender creates and sends a group @ message:
```dart
// Obtain the IDs of group members
List<String> atUserList = ['AT_ALL_TAG',"userID of John"]; // @ all and @ John
// Create a group @ message

    V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createTextAtMessage(
              text: text,
              atUserList: atUserList,
            );
    String id = createMessage.data!.id!;
    V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .sendMessage(
            id: id,
            receiver: "Recipient",
            groupID: "The groupID of the target group",
           );
```

- **Receiving a group @ message**:
  During conversation loading and update (when calling [OnConversationChangedCallback](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html)), get the group @ data list:
```dart
   // For v3.9.0 or later, you can include V2TIM_IMAGE_TYPE to get enumerated values.
    var arInfoType = {
      "TIM_AT_UNKNOWN": 0, // Error status
      "TIM_AT_ME": 1,  // @ me
      "TIM_AT_ALL": 2,// @ all
      "TIM_AT_ALL_AT_ME": 3 // @ all and separately @ me
    };

		// Obtain the group @ data list
     getInfoList(V2TimConversation conversation) {
        List<V2TimGroupAtInfo?>? atInfoList =
           conversation.groupAtInfoList;
           if (atInfoList == null || atInfoList.isNotEmpty) {
              return [];
            } else {
                  return atInfoList;
            }
        }

```

## Sending and Receiving Combined Messages
To implement the Combine and Forward feature similar to that in WeChat, it is necessary to create a combined message according to the original message list, and then send the combined message to the peer end. After the peer end receives the combined message, it will parse out the original message list. A title and abstracts are required to display the combined message. See the figures below.

<table>
   <tr>
      <th width="0px" style="text-align:center">Combine and forward</td>
      <th width="0px" style="text-align:center">Display combined messages</td>
      <th width="0px" style="text-align:center">Tap to download combined messages and display the combined message list</td>
   </tr>
  <tr>
      <td style="text-align:center"><img style="width:190px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/bbcb11b926d78bb1f58ed2ed2c662b8e.png" /></td>
      <td style="text-align:center"><img style="width:190px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/05837ee23cf9de96ec914ef965a852d5.png" /></td>
      <td style="text-align:center"><img style="width:190px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8e8f5eddd8b9386b3af9728f0edfb30f.png" /></td>
   </tr>
</table>


- **Sending a combined message**
Usually, when we receive a combined message, the chat UI will look like this:

| Chat History of Vinson and Lynx                                                           | Title     |
| ----------------------------------------------------------------------------------------- | --------- |
| Vinson: When is the new version of SDK scheduled to go online?                            | abstract1 |
| Lynx: Next Monday. The specific time depends on the system test result in these two days. | abstract2 |
| Vinson: OK                                                                                | abstract3 |

The chat UI will display only the title and abstract information of the combined message, and the combined message list will be displayed only when the user taps the combined message. To create a combined message, it is necessary to set not only the combined message list, but also the title and abstract information. The implementation process is as follows:
1. Call the [createMergerMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createMergerMessage.html) API to create a combined message.
2. Call the [sendMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html) API to send this combined message.

- **Receiving a combined message**
When receiving a combined message [V2TIMMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html), use the [V2TIMMergerElem](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html) API for combining message elements to get [title](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html#a864916a91d453e2124c12e0ccbb66550) and [abstractList](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_merger_elem/V2TimMergerElem/abstractList.html) and display them on the UI. When a user taps a combined message, call the [downloadMergerMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html#af34d8228a9842875652a726f24ac3d30) API to download the combined message list and display it on the UI.


### Typical examples: sending and receiving combined messages
- **Sending a combined message**
The sender creates and sends a combined message.
```dart
  /// Combine and forward
  sendMergerMessage(
      {required List<V2TimConversation> conversationList, // To forward messages of multiple conversations at one time
      required String title,
      required List<String> abstractList,
      required List<String> multiSelectedMessageList}) async {
    for (var conversation in conversationList) {
      final convID = conversation.groupID ?? conversation.userID ?? "";
      final convType = conversation.type;
      // The msgId list of messages to send
      final List<String> msgIDList = multiSelectedMessageList;

      final mergerMessageInfo = await _messageService.createMergerMessage(
          msgIDList: msgIDList,
          title: title,
          abstractList: abstractList,
          compatibleText: "The current version does not support this message");
      final messageInfo = mergerMessageInfo!.messageInfo;
      if (messageInfo != null) {
        // Send mergeMessage
        V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin
            .v2TIMManager
            .getMessageManager()
            .sendMessage(
              id: mergerMessageInfo.id!,
              receiver: convType == ConvType.c2c ? convID : "",
              groupID: convType == ConvType.group ? convID : "",
            );
      }
    }
  }
```

- **Receiving a combined message**
The recipient receives and parses a combined message:
```dart

 void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.elemType == MessageElemType.V2TIM_ELEM_TYPE_MERGER) {
		// Get the combined message elements
		V2TimMergerElem mergerElem = messageItem.mergerElem!,
		// Get the title
		String title = mergerElem.title;
		// Get the abstract list
		List<String> abstractList = mergerElem.abstractList;
		// Download the combined message list when the user taps the combined message
		// ...
		};
}

	// Tap mergeMessage to download mergeMessage
  handleTap(BuildContext context, String msgID) async {
    final res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .downloadMergerMessage(msgID: msgID);
    final mergerMessageList = res.data;
    if (mergerMessageList != null) {
   // ....
    }
  }
```

## Sending Messages Excluded from the Unread Count
Normally, both one-to-one chat messages and group messages you send are included in the unread count. You can get the unread message count of a conversation via the [unreadCount](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#unreadcount) API of the conversation object [V2TIMConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html). If you need to send messages that are excluded from the unread count, such as tips and control messages, send them as follows:

```dart
    V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createTextMessage(text: "text");
    String id = createMessage.data!.id!;
	// Set the marking of messages excluded from the unread count
    createMessage.data?.messageInfo?.isExcludedFromUnreadCount = true;
    V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .sendMessage(
            id: id,
            receiver:  "userID",
            groupID:  "groupID",
            );
```


## Sending Messages Excluded from the Conversation lastMsg

In certain scenarios, if you need to send messages that are excluded from `lastMsg` of a conversation, send them as follows:

```dart
// Create the message object
    V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createTextMessage(text: "Your text");
    String id = createMessage.data!.id!;
	// Set the marking of messages excluded from the unread count
    createMessage.data?.messageInfo?.setExcludedFromLastMessage = true; // Set the marking of changes
    V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .sendMessage(
            id: id,
            receiver:  "userID",
            groupID: "groupID",
            );
```

## Sending Targeted Group Messages


A targeted group message is a message sent only to specified members in a group. You can send it as follows:

> ? This feature is available in v3.9.0 or later:
>
>- This feature requires the Flagship Edition package.
>- The original message object for creating a targeted group message cannot be a group @ message.
>- The targeted group message feature is not available for Community and AVChatRoom groups.
>- By default, targeted group messages are excluded from the unread count of the group conversation.

## Setting Offline Push
When the recipient's app is killed, the IM SDK cannot receive new messages through the normal network connection. In this scenario, the offline push service provided by mobile phone vendors must be used to notify the recipient of new messages. We recommend new users use the offline push of TPNS (see [Offline Push](https://intl.cloud.tencent.com/document/product/1047/39156) for details).

### Setting the title and content for offline push
When sending a message, you can set the title and content for offline push in the **offlinePushInfo** field of the [sendMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html) API.

```dart
// Create and send a text message to groupA, and customize the title and content for offline push
    V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createTextMessage(text: text);
    String id = createMessage.data!.id!;
    createMessage.data?.messageInfo?.isExcludedFromUnreadCount = true;
    // Set the notification title and content
    OfflinePushInfo offlinePushInfo =
        OfflinePushInfo(title: "offline_title", desc: "offline_desc");
    V2TimValueCallback<V2TimMessage> res =
        await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(
              id: id,
              receiver: receiver.length > 0 ? receiver.first : "",
              groupID: groupID.length > 0 ? groupID.first : "",
              offlinePushInfo: offlinePushInfo
            );
```

### Tapping a pushed message to go to the corresponding chat window
To implement this feature, the sender needs to set the extended field `ext` of the offline push object `offlinePushInfo` when sending a message. When the recipient opens the app, the recipient can get `ext` by using the method for obtaining custom content provided by the corresponding mobile phone vendor, and then go to the corresponding chat window based on the content of `ext`.

The following example assumes that Denny sends a message to Vinson.
Sender: Denny needs to set `ext` before sending a message.

```dart
// Denny sets `offlinePushInfo` and specifies `ext` before sending a message
    V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createTextMessage(text: text);
    String id = createMessage.data!.id!;
    
    // Set the notification title, content, and extension
    OfflinePushInfo offlinePushInfo =
        OfflinePushInfo(title: "offline_title", 
		desc: "offline_desc", 
		ext: json.encode({"action": "jump to denny"})
		);
    
	V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .sendMessage(
            id: id,
            receiver:  "userID",
            groupID:  "groupID",
            offlinePushInfo: offlinePushInfo);
```


## Setting onlineUserOnly for Message Receiving Only When Users Are Online
In some scenarios, you may want that messages sent can only be received by online users or that a recipient is not aware of the messages when the recipient is offline. For this purpose, set `onlineUserOnly` to `true` when calling [sendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html). After the setting, the messages sent differ from common messages in the following ways:
- Messages cannot be stored offline, which means the recipient cannot receive messages unless the recipient is online.
- Multi-device roaming of messages is unavailable. This means that messages received on one terminal (read or not) cannot be received on any other terminal.
- Messages cannot be stored locally. That is, these messages cannot be retrieved from the local historical messages in the cloud.

>? This parameter can be used to display Typing in some scenarios.

## Setting "Mute Notifications" for Message Receiving
The SDK supports the following types of message receiving options:

- V2TIM_RECEIVE_MESSAGE: Messages will be received when the user is online, and offline push notifications will be received when the user is offline.
- V2TIM_NOT_RECEIVE_MESSAGE: Messages will not be received regardless of the online or offline status.
- V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE: Messages will be received when the user is online, and offline push notifications will not be received when the user is offline.

You can call the [setC2CReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/setC2CReceiveMessageOpt.html) API to set the Mute Notifications option for one-to-one messages and call [setGroupReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/setGroupReceiveMessageOpt.html) to set the Mute Notifications option for group messages.


## Recalling Messages

The sender can call the [revokeMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/revokeMessage.html) API to recall a message sent successfully. By default, the sender can recall a message that is sent within 2 minutes. You can change the time limit for message recall. For operation details, see [Message recall settings](https://intl.cloud.tencent.com/document/product/1047/34419).
Message recall requires cooperation of the UI code at the recipient side. When the sender recalls a message, the recipient will receive a message recall notification [onRecvMessageRevoked](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_callbacks/OnRecvMessageRevokedCallback.html) that contains the `msgID` of the recalled message. Based on this `msgID`, you can identify the message that has been recalled and change the corresponding message bubble to the "Message recalled" state on the UI.

### The sender recalls a message

 ```dart
 V2TimCallback res =
        await TencentImSDKPlugin.v2TIMManager.getMessageManager().revokeMessage(msgID: msgID,);
 ```

### The recipient learns that the message is recalled

1. Call [addAdvancedMsgListener](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html) to set the advanced message listener.
2. Call [onRecvMessageRevoked](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnRecvMessageRevokedCallback.html) to receive the message recall notifications.

```dart

 void onRecvMessageRevoked(String msgID) {
	// msgList is the message list on the current chat interface
	for (V2TIMMessage msg in msgList) {
		if (msg.msgID == msgID) {
				// msg is the recalled message. You need to change the corresponding message bubble state on the UI.
		}
	}
}
```

## Marking Unread Messages as Read
### Marking unread messages in a conversation as read
The recipient can call [markC2CMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html) and [markGroupMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html) to respectively mark unread messages of a C2C conversation and of a group conversation as read, and call back [onConversationChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html) to notify the UI to update.
### Quickly marking unread messages of all conversations as read
The recipient can call [markAllMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markAllMessageAsRead.html) to quickly mark unread messages of all conversations as read, and call back [onConversationChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html) to notify the UI to update.

## Adding Read Receipts for Messages
In the one-to-one chat scenario, when the recipient calls the [markC2CMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html) API to mark an incoming message as read, the message sender will receive a read receipt, indicating that the recipient has read the message.

>? Currently, the read receipt feature is available only in one-to-one chats and unavailable in group chats. Although there is a [markGroupMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html) API for group messages, no read receipts will be sent to a group message sender.

### The recipient marks messages as read

 ```dart
 // Mark messages coming from Haven as read
    V2TimCallback res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .markC2CMessageAsRead(
          userID: "haven_userID",
        );
 ```

### The sender learns that the messages are read
The event notification of the message receipt is located in the advanced message listener [V2TimAdvancedMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimAdvancedMsgListener/V2TimAdvancedMsgListener-class.html). To learn that the message is already read, the sender must call [addAdvancedMsgListener](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html) to set the listener. Then, the sender can receive a read receipt from the recipient through the callback of [onRecvC2CReadReceipt](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimAdvancedMsgListener/V2TimAdvancedMsgListener/onRecvC2CReadReceipt.html).

```dart
void onRecvC2CReadReceipt(List<V2TimMessageReceipt> receiptList) {
	// The sender may receive multiple read receipts at a time. Therefore, the array callback mode is used here.
	for (V2TimMessageReceipt  receipt in receiptList) {
		// Message recipient
		String userID = receipt.userID;
		// Time of the read receipt. A message is considered as read if the timestamp in the chat window is not later than `timestamp` here.
		int timestamp = receipt.timestamp;
	}
}
```

## Viewing Historical Messages
You can call [getC2CHistoryMessageList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CHistoryMessageList.html) to obtain historical messages of one-to-one chats, and call [getGroupHistoryMessageList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupHistoryMessageList.html) to obtain historical messages of group chats. If the current device is properly connected to the network, the IM SDK pulls historical messages from the server by default. If the network connection is unavailable, the IM SDK directly reads historical messages from the local database.

### Pulling historical messages by page
The IM SDK supports the feature of pulling historical messages by page. The number of messages pulled per page cannot be too large; otherwise, the pulling speed is affected. We recommend you pull 20 messages per page.
The following example assumes that historical messages of `groupA` are pulled by page, and the number of messages per page is 20. The sample code is as follows:

```dart
// The value `null` of `lastMsg` is passed in for the first pulling, indicating that starting from the latest message, a total of 20 messages are pulled
    V2TimValueCallback<List<V2TimMessage>> res = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .getGroupHistoryMessageList(
          groupID: "groupID",
          count: 20,
        );
    List<V2TimMessage> msgList = res.data ?? [];
    if (msgList.isNotEmpty) {
      lastMsgID = msgList[msgList.length - 1].msgID;
      V2TimValueCallback<List<V2TimMessage>> nextRes = await TencentImSDKPlugin
          .v2TIMManager
          .getMessageManager()
          .getGroupHistoryMessageList(
            groupID: "groupID",
            count: 20,
            lastMsgID: lastMsgID,
          );
		  // ...
    }
```

In actual scenarios, pulling by page is often triggered by your swipe operation. Each time when you swipe on the message list, pulling by page is triggered once. However, the principle is similar to the preceding sample code. In either case, `lastMsg` specifies the start message for pulling, and `count` specifies the number of messages pulled each time.

### Precautions
- The storage period of historical messages is as follows:<ul style="margin:0;"><li>Trial edition: free storage for 7 days, no extension supported. </li><li>Pro edition: free storage for 7 days, extension supported. </li><li>Flagship edition: free storage for 30 days, extension supported. </li></ul>It is a value-added service to extend the storage period of historical messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. For information about billing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.
- Only the meeting group (corresponding to the ChatRoom of the earlier version) supports pulling historical messages of members **before they join the group**.
- Messages in the AVChatRoom do not support local storage and multi-device roaming. Therefore, the [getGroupHistoryMessageList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupHistoryMessageList.html) API does not work on an AVChatRoom.

## Deleting Messages
You can call the [deleteMessages](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessages.html) API to delete historical messages. Historical messages cannot be recovered after deletion.

## Setting Message Permissions
### Allowing message sending and receiving only among friends
By default, the IM SDK does not prevent message sending and receiving among strangers. If you wish that one-to-one messages can be sent or received only among friends, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

### Not receiving messages from a specific user
To avoid receiving messages from a specific user, you can add the user to the blocklist or set the Mute Notifications option for messages from the user. After setting the Mute Notifications option, you can change the [Mute Notifications status](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a90a89f5b4855dad72b784101667998c5). For the IM SDK for Flutter, call `ReceiveMsgOptEnum` to complete the setting.
**Adding a user to the blocklist:**
Call the [addToBlackList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addToBlackList.html) API to add a user to the blocklist.
By default, the user will not be aware of this blocking operation, and the messages sent to you will still be displayed as sent successfully (in fact, you will not receive the messages). If you want a user in the blocklist to know that his/her messages are not sent, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message to you.
**Setting "Mute Notifications" for messages from a specified user: **
Call the [setC2CReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/setC2CReceiveMessageOpt.html) API to set the message receiving option to `ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE`.

### Rejecting messages from a specified group

Call [setGroupReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/setGroupReceiveMessageOpt.html) API to set the message receiving option to `ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE`.
For SDKs of other versions, call the `setReceiveMessageOpt` API to set the group message receiving option to `ReceiveMsgOptEnum.V2TIM_GROUP_NOT_RECEIVE_MESSAGE`.



## FAQs
### 1. Why am I receiving duplicate messages?
Check the service logic as follows:
- Check whether [addSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/addSimpleMsgListener.html) and [addAdvancedMsgListener](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html) are mixed up. If yes, when text or custom messages are received, both listeners trigger a callback, resulting in duplicate messages.
- Check whether the same listener object is added repeatedly (currently, repeated listening is available). If a listener object is no longer needed, call the corresponding [removeSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/removeSimpleMsgListener.html) or [removeAdvancedMsgListener](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/removeAdvancedMsgListener.html) API to remove the unnecessary listener.

### 2. Why do the read receipts become invalid after the app is uninstalled and then reinstalled?
In the one-to-one chat scenario, if the recipient calls [markC2CMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/markC2CMessageAsRead.html) to mark a message as read, the read receipt received by the sender contains `timestamp`. Based on `timestamp`, the SDK determines whether the recipient reads the message. Currently, `timestamp` is stored locally and will be lost when the app is reinstalled.

### 3. How can I parse a message containing multiple `Elem` objects?
1. Use the `Message` object to parse the first `Elem` object.
2. Use [nextElem](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_elem/V2TIMElem/nextElem.html) of the first `Elem` object to get the next `Elem` object. If the next `Elem` object exists, an `Elem` object instance will be returned. Otherwise, `null` will be returned.
```dart

 onRecvNewMessage(V2TimMessage msg) {
	// View the first Elem object
	int elemType = msg.elemType;
	if (elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT) {
		// Text message
		V2TIMTextElem v2TIMTextElem = msg.textElem;
		String text = v2TIMTextElem.text;
		// Check whether v2TIMTextElem is followed by more Elem objects
		V2TIMElem elem = v2TIMTextElem.nextElem;
		while (elem != null) {
			// Identify the Elem type. Here, take V2TIMCustomElem as an example.
			if (elem is V2TIMCustomElem) {
				
				String? data = customElem?.data;
			}
			// Continue to check whether the current Elem is followed by more Elem objects
			elem = nextElem;
		}
		// If Elem is null, all Elem objects have been parsed.
	}
}
```

[](id:msgAnalyze)
### 4. How are different types of messages parsed?
It is complex to parse a message. We provide the [sample code](https://github.com/tencentyun/TIMSDK/blob/master/Flutter/Demo/im_discuss/lib/pages/conversion/component/common_content.dart) for parsing different types of messages. You can copy the code to your project, and perform secondary development based on your actual needs.
