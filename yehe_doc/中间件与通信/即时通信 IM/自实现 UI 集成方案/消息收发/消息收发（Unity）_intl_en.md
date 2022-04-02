## Message Classification

IM messages are classified by message destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| One-to-one message | C2CMessage | Also called C2C message. When sending a one-to-one message, you must specify the UserID of the message recipient, and only the recipient can receive this message. |
| Group message | GroupMessage | When sending a group message, you must specify the groupID of the target group, and all users in this group can receive this message. |

IM messages can also be classified by content into text messages, image messages, video messages, voice messages, file messages, location messages, combined messages, and group tips.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| Text message | kTIMElem_Text | It refers to a common text message. Sensitive words of text messages will be filtered out in the IM service. If a message containing sensitive words is sent, the 80001 error code is returned. |
| Custom message | kTIMElem_Custom | It is a section of binary buffer and often used to transfer custom signaling in your application. Its content is not filtered for sensitive words. |
| Image message | kTIMElem_Image | When the IM SDK sends an original image, it automatically generates two images in different sizes. The three images are called the original image, large image, and thumbnail. |
| Video message | kTIMElem_Video | A video message contains a video file and an image. |
| Voice message | kTIMElem_Sound | The SDK supports displaying a red dot upon playback of the voice message. |
| File message | kTIMElem_File | A file message cannot exceed 100 MB. |
| Location message | kTIMElem_Location | A location message contains three fields: location description, longitude, and latitude. |
| Combined message | kTIMElem_Merge | Up to 300 messages can be combined. |
| Group tip | kTIMElem_GroupTips | A group tip is often used to carry a system notification in a group, such as a notification indicating that a member joins or leaves the group, the group description is modified, or the profile of a group member is changed. |

## Sending Text Messages

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a C2C message is the UserID, and that of a group message is the GroupID.
        Message message = new Message();
        message.message_conv_id = conv_id;
        message.message_conv_type = TIMConvType.kTIMConv_C2C;// For a group message, this value is TIMConvType.kTIMConv_Group.
        List<Elem> messageElems = new List<Elem>(); 
        Elem textMessage = new Elem(); // Create a message
        textMessage.elem_type = TIMElemType.kTIMElem_Text;
        textMessage.text_elem_content = "This is a text message";
        messageElems.Add(textMessage);
        message.message_elem_array = messageElems;
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID messageId returned when the message is sent
}
```

## Sending Image Messages

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a C2C message is the UserID, and that of a group message is the GroupID.
        Message message = new Message();
        message.message_conv_id = conv_id;
        message.message_conv_type = TIMConvType.kTIMConv_C2C;// For a group message, this value is TIMConvType.kTIMConv_Group.
        List<Elem> messageElems = new List<Elem>(); 
        Elem imageMessage = new Elem(); // Create a message
        imageMessage.elem_type = TIMElemType.kTIMElem_Image;
        imageMessage.image_elem_orig_path = "/Users/xxx/xxx.png"; // Absolute path to the file
  			imageMessage.image_elem_level = TIMImageLevel.kTIMImageLevel_Orig; // Send an original image
        messageElems.Add(imageMessage);
        message.message_elem_array = messageElems;
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID messageId returned when the message is sent
}
```

## Getting Message Sending Progress

```c#
TencentIMSDK.SetMsgElemUploadProgressCallback((Message message, int index, int cur_size, int total_size, string user_data)=>{
	// message represents the message being sent.
  // index represents the number of the file being uploaded.
  // cur_size represents the size (in MB) of the file being uploaded.
  // total_size represents the total size of all files being uploaded.
})
```

## Receiving Messages

```c#
// Register a message receiving listener
TencentIMSDK.RecvNewMsgCallback((List<Message> message, string user_data)=>{

})
```

## Meanings of Message Fields

| Field                                 | Meaning                                                       |
| ------------------------------------- | ------------------------------------------------------------ |
| message_elem_array                    | List of elements in the message                                             |
| message_conv_id                       | Conversation ID of the message                                              |
| message_conv_type                     | Conversation type of the message                                             |
| message_sender                        | Message sender                                                 |
| message_priority                      | Message priority                                                   |
| message_client_time                   | Client time                                                   |
| message_server_time                   | Server time                                                   |
| message_is_from_self                  | Whether the message sender is the current user                                             |
| message_platform                      | Platform that sends the message                                               |
| message_is_read                       | Whether the message is read                                                 |
| message_is_online_msg                 | Whether the message is an online message. `false` (default): common message; `true`: message that disappears after being viewed |
| message_is_peer_read                  | Whether the message is read by the peer of the conversation                                       |
| message_status                        | Current status of the message                                                 |
| message_unique_id                     | Unique ID of the message. `kTIMMsgMsgId` is recommended.                        |
| message_msg_id                        | Unique ID of the message                                               |
| message_rand                          | Random code of the message                                                 |
| message_seq                           | Sequence number of the message                                                     |
| message_custom_int                    | Custom integer field (saved locally, will not be sent to the peer end, and will become invalid after the app is uninstalled and reinstalled) |
| message_custom_str                    | Custom data field (saved locally, will not be sent to the peer end, and will become invalid after the app is uninstalled and reinstalled) |
| message_cloud_custom_str | Custom message data (saved in the cloud, will be sent to the peer end, and can still be pulled after the app is uninstalled and reinstalled) |
| message_is_excluded_from_unread_count | Whether the message is excluded from the unread count of the conversation. `NO` (default): included in the unread count of the conversation; `YES`: excluded from the unread count of the conversation |
| message_is_forward_message            | Whether the message is a forwarded message                                              |
| message_group_at_user_array | UserID list of users that need to be mentioned (@). If you need to @all, pass in `kImSDK_MesssageAtALL`. |
| message_sender_profile                | User profile of the message sender                                       |
| message_sender_group_member_info      |Information of the message sender in a group. This parameter is only valid in a group conversation. Currently, only the `kTIMGroupMemberInfoIdentifier` and `kTIMGroupMemberInfoNameCard` fields can be obtained. You are advised to obtain other fields via the `TIMGroupGetMemberInfoList` API. |
| message_offlie_push_config            | Offline push settings of the message                                           |
| message_excluded_from_last_message    | Whether the current message is used as the last message (`lastMessage`) of the conversation. `true`: no; `false`: yes      |

