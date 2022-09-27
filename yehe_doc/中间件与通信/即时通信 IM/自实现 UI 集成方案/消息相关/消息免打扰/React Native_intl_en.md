## Feature Description

You can set the message receiving option for a **one-to-one or group chat** to implement the notification muting feature.
The IM SDK supports the following three message receiving options as defined in `V2TIMReceiveMessageOpt`:

| Message Receiving Option                                       | Feature Description                                     |
| -------------------------------------------------- | -------------------------------------------- |
| ReceiveMsgOptEnum.V2TIM_RECEIVE_MESSAGE            | Messages will be received when the user is online, and offline push notifications will be received when the user is offline.   |
| ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE        | Messages will not be received no matter whether the user is online or offline.                       |
| ReceiveMsgOptEnum.V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE | Messages will be received when the user is online, and offline push notifications will not be received when the user is offline. |

Different `V2TIMReceiveMessageOpt` options can be used to implement group message notification muting:
**No messages will be received.**
After the message receiving option is set to `V2TIM_NOT_RECEIVE_MESSAGE`, no one-to-one or group messages will be received, and the conversation list will not be updated.

**Messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**

1. The message receiving option is set to `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE`.
2. When the receiver receives a new one-to-one or group message and needs to update the conversation list, it can get the unread count through the `unreadCount` ([TS](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_ui/latest/models_V2_tim_topic_info/V2TimTopicInfo/unreadCount.html)) in the `V2TIMConversation` of the conversation.
3. The receiver displays a badge rather than the unread count when identifying the message receiving option as `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE` based on the `recvOpt` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimConversation.html#recvOpt)) in `V2TIMConversation`.

> ? As this method requires the unread count feature, it applies only to work groups (Work) and public groups (Public). For more information on group types, see Group Overview.

## Setting the Message Receiving Option for a One-to-One Chat

Call the `setC2CReceiveMessageOpt` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#setC2CReceiveMessageOpt)) to set the message receiving option for a one-to-one chat.
You can use the `userIDList` parameter to specify up to 30 users at a time.

> ! This API can be called up to 5 times every second.

Below is the sample code:

```javascript
// Set not to receive messages no matter whether the user is online or offline

TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .setC2CReceiveMessageOpt(
    ["user1", "user2"],
    ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE
  );
```

## Getting the Message Receiving Option for a One-to-One Chat

Call the `getC2CReceiveMessageOpt` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#getC2CReceiveMessageOpt)) to get the message receiving option for a one-to-one chat.

Below is the sample code:

```javascript
const messageOpt = await TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .getC2CReceiveMessageOpt(["user1", "user2"]);
messageOpt.data.forEach((element) => {
  // Message receiving option
  element.c2CReceiveMessageOpt;
  element.userID;
});
```

## Setting the Message Receiving Option for a Group Chat

Call the `setGroupReceiveMessageOpt` API ([TS](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_ui/latest/im_flutter_plugin_platform_ui/ImFlutterPlatform/setGroupReceiveMessageOpt.html)) to set the message receiving option for a group chat.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager.getMessageManager().setGroupReceiveMessageOpt(groupID: "groupID", opt: ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE);
```

## Getting the Message Receiving Option for a Group Chat

Call the `getGroupsInfo` API ([TS](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_ui/latest/im_flutter_plugin_platform_ui/ImFlutterPlatform/setGroupReceiveMessageOpt.html)) to get the `V2TIMGroupInfo` group profile object list. Here, the `recvOpt` field indicates the message receiving option for the group chat.

Below is the sample code:

```javascript
const groups = await TencentImSDKPlugin.v2TIMManager.getGroupManager().getGroupsInfo(groupIDList: ['groupID']);
  groups.data.forEach((element) => {
    // Get the message receiving option of the group
    element.groupInfo.recvOpt;
  });
```


