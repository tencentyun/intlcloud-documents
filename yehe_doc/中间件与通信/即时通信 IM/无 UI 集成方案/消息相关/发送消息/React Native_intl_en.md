## Feature Description
* It supports sending text, custom, and rich media messages, all of which belong to the `Message` type.

## Key API Description
The `MsgSendMessage` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgSendMessage_System_String_com_tencent_imsdk_unity_enums_TIMConvType_com_tencent_imsdk_unity_types_Message_System_Text_StringBuilder_com_tencent_imsdk_unity_callback_ValueCallback_com_tencent_imsdk_unity_types_Message__)) is one of the most core APIs for message sending. It supports sending messages of all types.

The API is as described below:

<table ><thead ><tr>
<th >Type</th><th >Name</th><th >Description</th></tr>

</thead><tbody ><tr>
<td>System.String</td>
<td>conv_id</td>
<td>Conversation ID</td>
</tr>

<tr>
<td>TIMConvType</td>
<td>conv_type</td>
<td>Conversation type</td>
</tr>

<tr>
<td>Message</td>
<td>message</td>
<td>Message</td>
</tr>

<tr>
<td>System.Text.StringBuilder</td>
<td>message_id</td>
<td>Message ID</td>
</tr>

<tr>
<td>ValueCallback<message > | ValueCallback<string ></string></message></td>
<td>callback</td>
<td>Async callback</td>
</tr>

</tbody>
</table>



## Sending a Text Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_Text,
              text_elem_content =  "This is an ordinary text message"
            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, 						string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```

## Sending an Image Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_Image,
              image_elem_orig_path =  "/Users/xxx/xxx.png", // Absolute file path
              image_elem_level = TIMImageLevel.kTIMImageLevel_Orig // Send the original image
            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```

## Sending an Audio Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_Sound,
              sound_elem_file_path =  "/Users/xxx/xxx.mp3", // Absolute file path
              sound_elem_file_size = 10  // Audio duration

            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```

## Sending a Video Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_Video,
              video_elem_video_path =  "/Users/xxx/xxx.mp4", // Absolute file path
              video_elem_video_type = "mp4",  // Video type
              video_elem_video_duration = 10, // Video duration
              video_elem_image_path = "Absolute path of the local video thumbnail file"
            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```

## Sending a File Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_File,
              file_elem_file_path =  "/Users/xxx/xxx.x", // Absolute file path
              file_elem_file_name = "Filename",
            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```

## Sending a Location Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_Location,
              location_elem_desc =  "Shennan Boulevard, Nanshan District, Shenzhen",// Location information digest
              location_elem_longitude = 34, // Longitude
              location_elem_latitude = 20 // Latitude
            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```

## Sending an Emoji Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_Face,
              face_elem_index = 0,
              face_elem_buf = ""
            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```

## Sending a Custom Message

```c#
public static void MsgSendMessage() {
        string conv_id = ""; // The ID of a one-to-one message is the `UserID`, and that of a group message is the `GroupID`.
        Message message = new Message
        {
          message_conv_id = conv_id,
          message_conv_type = TIMConvType.kTIMConv_C2C, // It is `TIMConvType.kTIMConv_Group` for a group message.
          message_elem_array = new List<Elem>
          {
            new Elem
            {
              elem_type = TIMElemType.kTIMElem_Custom,
              custom_elem_data = "",
              custom_elem_desc = "",
              custom_elem_ext = ""
            }
          }
        };
        StringBuilder messageId = new StringBuilder(128);

        TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, string json_param, string user_data)=>{
          // Async message sending result
        });
  			// The message ID `messageId` returned when the message is sent
}
```



