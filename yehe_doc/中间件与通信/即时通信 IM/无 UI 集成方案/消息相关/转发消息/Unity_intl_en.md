## Feature Description
You can implement the feature of merging and forwarding messages in the following steps:
1. Create a merged message based on the list of original messages.
2. Send the merged message to the receiver.
3. The receiver receives the merged message and parses the list of original messages.

The title and digest are needed to display the merged message, as shown below:

| Merge and Forward                                                                                       | Display of Merged Message                                                                               | Click Merged Message to Download Message List for Display                                              |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/cb970fdd471cdd668b5ce31d188970fd.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/2304c7ea1e29de702f99d96e52a9739c.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/f2c81dc8df0064cf8202d06a79f7af16.png" width = "300"/> |


## Merging and Forwarding Messages
### Creating and sending a merged message

A merged message can be created by setting the message list along with the merged message title and digest. The process is as follows:
1. Create a merged message by setting the list of original messages as well as the merged message title and digest.

<img src="https://qcloudimg.tencent-cloud.cn/raw/dbc9a0f199effcf6d865b6497ec185f3.png" width = "450" />

| Attribute                  | Description                | Remarks                                                                                                                                                                            |
| -------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| merge_elem_message_array   | List of original messages  | List of original messages to be merged and forwarded                                                                                                                               |
| merge_elem_title           | Title                      | Title of the merged message, such as "Chat History of xixiyah and Hello" as shown above                                                                                            |
| merge_elem_abstract_array  | Digest list                | Digest list of the merged message as shown above. The original message digests need to be displayed for the merged message, which will be unfolded after the user clicks the cell. |
| merge_elem_compatible_text | Compatibility text message | If the SDK on an early version does not support the merged message, the user will receive a text message with the content `merge_elem_compatible_text` by default.                 |

Sample code for creating and sending a merged message:


```c#
// List of messages to be forwarded, which can contain merged messages but not group tips
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_Group,
   message_elem_array = new List<Elem>{
    new Elem
   {
     elem_type = TIMElemType.kTIMElem_Merge,
     merge_elem_title = "Chat History of user1 and user2", // Title of the merged message
     merge_elem_message_array = new List<Message>
     {
      message1,
      message2
     },
     merge_elem_abstract_array = new List<string>
     {
      "user1:hello", "user2:hello" // Digest list of the merged message
     },
     merge_elem_compatible_text = "The current version does not support the message", // Compatibility text of the merged message. If the SDK on an early version does not support the merged message, the user will receive a text message with the content `compatibleText` by default.
   }},
};
StringBuilder messageId = new StringBuilder(128);
TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_Group, message, messageId, (int code, string desc, string json_param, string user_data)=>{
 // Async message sending result
});
```



### Receiving a merged message

#### Adding a listener
The receiver calls `AddRecvNewMsgCallback` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_AddRecvNewMsgCallback_com_tencent_imsdk_unity_callback_RecvNewMsgCallback_com_tencent_imsdk_unity_callback_RecvNewMsgStringCallback_)) to add a message listener.
We recommend it be called early, such as after the chat page is initialized, to ensure timely message receiving in the application.

Sample code:


```c#
TencentIMSDK.AddRecvNewMsgCallback((List<Message> messages, string user_data)=>{
  foreach(Message message in messages)
  {
    foreach (Elem elem in message.message_elem_array)
    {
      // There is a next element
      if (elem.elem_type == TIMElemType.kTIMElem_Merge)
      {
      }
    }
  }
})
```


#### Parsing a message
After the listener is added, the receiver will receive the merged message `Message` in `RecvNewMsgCallback`.
You can use the merged message element to get the `merge_elem_title` and `merge_elem_abstract_array` for UI display.
Then, when the user clicks the merged message, you can call the `MsgDownloadMergerMessage` API ([c#](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgDownloadMergerMessage.html)) to download the merged message list for UI display.

Sample code:


```c#
if(elem.TIMElemType == TIMElemType.kTIMElem_Merge){
   elem.merge_elem_abstract_array;
   elem.merge_elem_layer_over_limit;
   elem.merge_elem_title;
   TIMResult res = TencentIMSDK.MsgDownloadMergerMessage(message, (int code, string desc, List<Message> messages, string user_data)=>{
    // Process the async logic
   });
}
```



## Forwarding Messages One by One
To forward a single message, create a message identical to the original message first, and then call the `MsgSendMessage` API ([c#](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessage.html)) to send the message.






