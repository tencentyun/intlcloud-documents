## Overview
You can implement the feature of combining and forwarding messages in the following steps:
1. Create a combined message based on the list of original messages.
2. Send the combined message to the receiver.
3. The receiver receives the combined message and parses the list of original messages.

## Combined Message
### Creating and sending a combined message

A combined message can be created by setting the message list along with the combined message title and digest. The process is as follows:
1. Create a combined message by setting the list of original messages as well as the combined message title and digest.
<table>
<thead>
<tr>
<th>Attribute</th>
<th>Definition</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>merge_elem_message_array</td>
<td>List of original messages</td>
<td>List of original messages to be combined and forwarded</td>
</tr>
<tr>
<td>merge_elem_title</td>
<td>Title</td>
<td>Title of the combined message, such as "Chat History of xixiyah and Hello" as shown above</td>
</tr>
<tr>
<td>merge_elem_abstract_array</td>
<td>Digest list</td>
<td>Digest list of the combined message as shown above. The original message digests need to be displayed for the combined message, which will be unfolded after the user clicks the cell.</td>
</tr>
<tr>
<td>merge_elem_compatible_text</td>
<td>Compatibility text message</td>
<td>If the early SDK versions do not support the combined message, the user will receive a text message with the content `merge_elem_compatible_text` by default.</td>
</tr>
</tbody></table>
2. Sample code for creating and sending a combined message:
<dx-codeblock>
:::  c#
// List of messages to be forwarded, which can contain combined messages but not group tips
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_Group,
   message_elem_array = new List<Elem>{
    new Elem
   {
     elem_type = TIMElemType.kTIMElem_Merge,
     merge_elem_title = "Chat History of user1 and user2", // Title of the combined message
     merge_elem_message_array = new List<Message>
     {
      message1,
      message2
     },
     merge_elem_abstract_array = new List<string>
     {
      "user1:hello", "user2:hello" // Digest list of the combined message
     },
     merge_elem_compatible_text = "The current version does not support the message" // Compatibility text of the combined message. If the early SDK version does not support the combined message, the user will receive a text message with the content `compatibleText` by default.
   }},
};
StringBuilder messageId = new StringBuilder(128);
TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_Group, message, messageId, (int code, string desc, string json_param, string user_data)=>{
 // Async message sending result
});
:::
</dx-codeblock>




### Receiving a combined message

#### Adding a listener
The receiver calls the `AddRecvNewMsgCallback` API ([details](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/AddRecvNewMsgCallback.html)) to add a message listener.
We recommend it be called early, such as after the chat page is initialized, to ensure timely message receiving in the application.

Sample code:


```c#
TencentIMSDK.AddRecvNewMsgCallback((List<Message> messages, string user_data)=>{
  foreach(Message message in messages)
  {
    foreach (Elem elem in message.message_elem_array)
    {
      // There is a next message
      if (elem.elem_type == TIMElemType.kTIMElem_Merge)
      {
      }
    }
  }
})
```


#### Parsing a message
After the listener is added, the receiver will receive the combined message `Message` in `RecvNewMsgCallback`.
You can use the combined message element to get the `merge_elem_title` and `merge_elem_abstract_array` for UI display.
Then, when the user clicks the combined message, you can call the `MsgDownloadMergerMessage` API ([details](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDownloadMergerMessage.html)) to download the combined message list for UI display.

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
To forward a single message, create a message identical to the original message first, and then call the `MsgSendMessage` API ([details](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSendMessage.html)) to send the message.
