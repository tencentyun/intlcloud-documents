## Message Class

In the Tencent Cloud Chat SDK, the message class is `Message` ([details](https://comm.qq.com/im/doc/unity/zh/types/MessageAttributes/Message.html)), which will be frequently used for message sending and receiving.

## Meanings of Message Fields

| Field                                 | Description                                                  |
| ------------------------------------- | ------------------------------------------------------------ |
| message_elem_array                    | List of elements in the message                              |
| message_conv_id                       | Conversation ID of the message                               |
| message_conv_type                     | Conversation type of the message                             |
| message_sender                        | Message sender                                               |
| message_priority                      | Message priority                                             |
| message_client_time                   | Client time                                                  |
| message_server_time                   | Server time                                                  |
| message_is_from_self                  | Whether the message sender is the current user               |
| message_platform                      | Platform from which the message is sent                      |
| message_is_read                       | Whether the message is read                                  |
| message_is_online_msg                 | Whether the message is an online message. `false` (default): Ordinary message; `true`: Online message |
| message_is_peer_read                  | Whether the message is read by the recipient                 |
| message_need_read_receipt             | Whether the message requires a read receipt (to use this feature, you need to purchase the Ultimate edition on v6.1 or later). To use this feature for group messages, go to the Chat console to set the target group type first. |
| message_status                        | Current status of the message                                |
| message_target_group_member_array     | Specifies the targeted recipients of the group message (targeted message). This field is not supported for group @ messages, community messages, or audio-video group messages. After this field is set, the message will not be included in the unread message count of the conversation. |
| message_unique_id                     | Unique ID of the message. `kTIMMsgMsgId` is recommended.     |
| message_msg_id                        | Unique message ID.                                           |
| message_rand                          | Random code of the message                                   |
| message_has_sent_receipt              | Whether a read receipt is sent (valid only for group messages) |
| message_group_receipt_read_count      | This field is an internal field and not recommended. We recommend you call `TIMMsgGetMessageReadReceipts` to get the read receipt for a group message. |
| message_group_receipt_unread_count    | This field is an internal field and not recommended. We recommend you call `TIMMsgGetMessageReadReceipts` to get the read receipt for a group message. |
| message_seq                           | Sequence number of the message                               |
| message_custom_int                    | Custom integer field, which is saved locally, will not be sent to the peer end, and will become invalid after the application is uninstalled and reinstalled |
| message_custom_str                    | Custom data field, which is saved locally, will not be sent to the peer end, and will become invalid after the application is uninstalled and reinstalled |
| message_cloud_custom_str              | Custom message data, which is saved in the cloud, will be sent to the peer end, and can still be pulled after the application is uninstalled and reinstalled |
| message_is_excluded_from_unread_count | Whether the message is excluded from the unread count of the conversation. `NO` (default): included in the unread count of the conversation; `YES`: excluded from the unread count of the conversation |
| message_is_forward_message            | Whether the message is a forwarded message                   |
| message_group_at_user_array           | List of UserIDs of users to be mentioned (@). To @all, pass in `kImSDK_MesssageAtALL`. |
| message_sender_profile                | User profile of the message sender                           |
| message_sender_group_member_info      | Information of the message sender in a group. This parameter is only valid in a group conversation. Currently, only the `kTIMGroupMemberInfoIdentifier` and `kTIMGroupMemberInfoNameCard` fields can be obtained. You are advised to obtain other fields via the `TIMGroupGetMemberInfoList` API. |
| message_offlie_push_config            | Offline push settings of the message                         |
| message_excluded_from_last_message    | Whether the message is used as the last message (`lastMessage`) in the conversation. `true`: No; `false`: Yes |

## Message Types

Chat messages are classified by message destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type       | API Keyword  | Description                                                  |
| ------------------ | ------------ | ------------------------------------------------------------ |
| One-to-one message | C2CMessage   | Also called C2C message. When sending a one-to-one message, you must specify the UserID of the message recipient, and only the recipient can receive this message. |
| Group message      | GroupMessage | When sending a group message, you must specify the groupID of the target group, and all users in this group can receive this message. |

Tencent Cloud Chat messages can also be classified by content into text messages, image messages, video messages, audio messages, file messages, location messages, combined messages, and group tip messages.

| Message Type     | API Keyword        | Description                                                  |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| Text message     | kTIMElem_Text      | Ordinary text message                                        |
| Custom message   | kTIMElem_Custom    | It is a section of binary buffer and often used to transfer custom signaling in your application. |
| Image message    | kTIMElem_Image     | When the Chat SDK sends an original image, it automatically generates two images in different sizes. The three images are called the original image, large image, and thumbnail. |
| Video message    | kTIMElem_Video     | A video message contains a video file and a thumbnail.       |
| Audio message    | kTIMElem_Sound     | It supports displaying a red dot before the playback of the audio message. |
| File message     | kTIMElem_File      | A file message cannot exceed 100 MB.                         |
| Location message | kTIMElem_Location  | A location message contains three fields: location description, longitude, and latitude. |
| Merged message   | kTIMElem_Merge     | Up to 300 messages can be combined.                          |
| Group tip        | kTIMElem_GroupTips | A group tip is often used to carry a system notification in a group, such as a notification indicating that a member joins or leaves the group, the group description is modified, or the profile of a group member is changed. |

## Message Storage Policy

Tencent Cloud Chat messages can be classified by message storage policy into two types: online messages and non-online messages.
Online messages can be received only by online users and will not be pushed when they are offline. Non-online messages can be received by users whether they are online or not.

Online messages are delivered in real time and not stored on the server or in the SDK. Therefore, they cannot be pulled from historical messages after the device is changed or the application is uninstalled and reinstalled.

>?
>
>1. All messages in an audio-video group are online messages.
>2. Messages pushed to all users are online messages.

Non-online messages are stored in the SDK and on the server. By default, they are stored on the roaming server for seven days. If you want a longer storage period, you need to purchase the value-added service. For more information on the service content and billing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

These messages, for example, all types of ordinary messages, can be pulled from historical messages after the device is changed or the application is uninstalled and reinstalled.
