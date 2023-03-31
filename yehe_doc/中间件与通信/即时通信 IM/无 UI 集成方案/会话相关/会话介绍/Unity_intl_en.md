## Conversation
When a user creates a one-to-one or group chat, a conversation will be created.
In the Tencent Cloud IM SDK, the conversation class is `ConvInfo`. You can use the conversation management class APIs to display/update the conversation list, update the unread count, pin a conversation to the top, make a conversation draft, and mute message notifications.

## Conversation Class
The conversation class is `ConvInfo` ([Details](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html)), which defines the following content:

| Attribute                | Definition                                      | Description                                                  |
| ------------------------ | ----------------------------------------------- | ------------------------------------------------------------ |
| conv_type                | Conversation type                               | See the definition of `TIMConvType`, which can be `C2C` or `Group`. |
| conv_id                  | Unique conversation ID                          | It is in the format of `c2c_userID` for a one-to-one chat or `group_groupID` for a group chat. |
| conv_active_time         | Time when a conversation was activated          |                                                              |
| conv_is_has_lastmsg      | Whether the conversation has the last message   |                                                              |
| conv_show_name           | Displayed conversation name                     | The name of a group conversation is displayed in the following order of priority: group name > group ID; <br>The name of a one-to-one conversation is displayed in the following order of priority: friend remarks of the message receiver > nickname of the message receiver > `userID` of the message receiver. |
| conv_unread_num          | Unread message count of the conversation        | It is invalid and defaults to `0` for an audio-video group (AVChatRoom). |
| conv_recv_opt            | Message receiving option                        | See the definition of `TIMReceiveMessageOpt`.                |
| conv_last_msg            | Last message in the conversation                | For detailed directions, see [ConvGetConvInfo(List<ConvParam>, ValueCallback<String>)](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvGetConvInfo.html). |
| conv_group_at_info_array | List of @ information in the group conversation | Generally, it is used to display the notifications of "someone@me" and "@all". |
| conv_draft               | Draft information                               | The draft information can be set by calling the `ConvSetDraft` API. For more information, see [ConvSetDraft(String, TIMConvType, DraftParam)](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvSetDraft.html). |
| conv_is_has_draft        | Whether there is a conversation draft           |                                                              |
| conv_is_pinned           | Whether to pin the conversation to the top      | For detailed directions, see [ConvPinConversation](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvPinConversation.html). |

## Conversation Storage Policy
There is no limit on the number of locally stored conversations.
Up to 100 conversations can be stored in the cloud. To increase this limit, upgrade to the Ultimate edition. Then you can set the limit to 500 in the console.

Up to 100 conversations can be stored in the cloud. To increase this limit, upgrade to the Ultimate edition. Then you can set the limit to 500 in the console:

![](https://qcloudimg.tencent-cloud.cn/raw/ba00871ad091df6fbe7cbf0ceb0e7607.png)

If the information of a conversation has not been updated for a long time, the conversation can be stored in the cloud for up to seven days. To extend the conversation storage period, [contact us](https://console.cloud.tencent.com/workorder/category) for application.

Locally stored conversations may not always be consistent with those stored in the cloud. If the user does not call the `ConvDelete` API to delete the local conversations, the conversations will always exist. However, up to 100 conversations can be stored in the cloud, and if the information of a conversation has not been updated for a long time, the conversation can be stored in the cloud for up to seven days. Therefore, local conversations displayed on different terminals may differ.
