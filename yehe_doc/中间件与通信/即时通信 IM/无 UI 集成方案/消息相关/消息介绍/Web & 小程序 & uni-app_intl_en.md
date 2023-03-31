## Message Class

In the IM SDK, [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html) indicates the message object that is used to describe the attributes of a message, such as type, content, and conversation ID.

| Attribute        | Type    | Default Value                 | Description                                                  |
| ---------------- | ------- | ----------------------------- | ------------------------------------------------------------ |
| ID               | String  | -                             | Message ID. Starting from v2.18.0, the rule for concatenating the message ID is `${senderTinyID}-${clientTime}-${random}`, which is the same as that for concatenating the message ID of native IM. |
| type             | String  | -                             | Message type. Valid values:<br/><li>TIM.TYPES.MSG_TEXT --- text message</li><li>TIM.TYPES.MSG_IMAGE --- image message</li><li>TIM.TYPES.MSG_AUDIO --- audio message</li><li>TIM.TYPES.MSG_VIDEO --- video message</li><li>TIM.TYPES.MSG_FILE --- file message</li><li>TIM.TYPES.MSG_CUSTOM --- custom message</li><li>TIM.TYPES.MSG_MERGER --- merged message (supported by v2.10.1 or later)</li><li>TIM.TYPES.MSG_LOCATION --- location message (supported by v2.15.0 or later)</li><li>TIM.TYPES.MSG_GRP_TIP --- group tip message</li><li>TIM.TYPES.MSG_GRP_SYS_NOTICE --- group system notification</li> |
| payload          | Object  | -                             | Message content. Valid values:<br/><li>[Text](https://web.sdk.qcloud.com/im/doc/en/Message.html#.TextPayload)</li><li>[Image](https://web.sdk.qcloud.com/im/doc/en/Message.html#.ImagePayload)</li><li>[Audio](https://web.sdk.qcloud.com/im/doc/en/Message.html#.AudioPayload)</li><li>[Video](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload)</li><li>[File](https://web.sdk.qcloud.com/im/doc/en/Message.html#.FilePayload)</li><li>[Custom](https://web.sdk.qcloud.com/im/doc/en/Message.html#.CustomPayload)</li><li>[Merged (supported by v2.10.1 or later)](https://web.sdk.qcloud.com/im/doc/en/Message.html#.MergerPayload)</li><li>[Geographical location (supported by v2.15.0 or later)](https://web.sdk.qcloud.com/im/doc/en/Message.html#.LocationPayload)</li><li>[Group tip](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)</li><li>[Group system notification](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupSystemNoticePayload) |
| conversationID   | String  | -                             | Conversation ID of the message                               |
| conversationType | String  | -                             | Conversation type of the message. Valid values:<br/><li>TIM.TYPES.CONV_C2C --- C2C (one-to-one) conversation</li><li>TIM.TYPES.CONV_GROUP --- group conversation</li><li>TIM.TYPES.CONV_SYSTEM --- system conversation</li> |
| to               | String  | -                             | `userID` of the receiver                                     |
| from             | String  | -                             | `userID` of the sender. It is set to the ID of the currently logged-in user by default when a message is sent. |
| flow             | String  | -                             | Message flow.<br/><li>in --- the received message </li><li>out --- the sent message</li> |
| time             | Number  | -                             | Message timestamp in seconds                                 |
| status           | String  | -                             | Message status.<br/><li>unSend --- not sent</li><li>success --- sent successfully</li><li>fail --- failed to send |
| isRevoked        | Boolean | false                         | Whether the message is a recalled message. `true` indicates yes. This attribute is supported by v2.4.0 or later. |
| priority         | String  | TIM.TYPES.MSG_PRIORITY_NORMAL | Message priority. This attribute applies to group chats and is supported by v2.4.2 or later. |
| nick             | String  | -                             | Nickname of the message sender. This attribute is supported by v2.6.0 or later for audio-video groups (AVChatRoom) and needs to be set by calling the [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile) API in advance. |
| avatar           | String  | -                             | Profile photo address of the message sender. This attribute is supported by v2.6.0 or later for audio-video groups (AVChatRoom) and needs to be set by calling the [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile) API in advance. |
| isPeerRead       | Boolean | false                         | Whether the one-to-one message is read by the receiver. `true` indicates yes. This attribute is supported by v2.7.0 or later. |
| nameCard         | String  | -                             | Group name card of the sender that sends a non-audio-video group message. This attribute is supported by v2.9.0 or later. It can also be called the nickname of the message sender in the group and needs to be set by calling the [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard) API in advance. |
| atUserList       | Array   | -                             | This field stores the `userID` values of the group members who are mentioned in the group message. It is supported by v2.9.0 or later. |
| cloudCustomData  | String  | -                             | Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later. |
| isDeleted        | Boolean | false                         | Whether the message is a deleted message. `true` indicates yes. This attribute is supported by v2.12.0 or later. |
| isModified       | Boolean | false                         | Whether the message is a modified message. `true` indicates yes (supported by v2.12.1 or later). |
| needReadReceipt  | Boolean | false                         | Whether a read receipt is needed. `true` indicates yes. This attribute is supported by v2.18.0 or later and applies only to group messages. To use it, you need to purchase the Ultimate edition package. |
| readReceiptInfo  | Object  | -                             | Message read receipt information (supported by v2.18.0 or later).<br/><li>readCount --- count of the messages that are read, which can be queried by calling [getMessageReadReceiptList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList) API; to query the group members who read the message, call the [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList).</li><li>unreadCount --- count of the messages that are not read, which can be queried by calling the [getMessageReadReceiptList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList) API. |

|      |      |      |      |
| --- |  --- | --- | --- |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |