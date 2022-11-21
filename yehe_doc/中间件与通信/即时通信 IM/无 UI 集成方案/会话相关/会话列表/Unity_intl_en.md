## Feature Description
After a user logs in to the application, the list of recent conversations can be displayed to make it easy to locate the target conversation.
The conversation list is as follows:
<img src="https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/res/RPReplay_Final0511.gif" alt="" style="zoom:40%;" />

The conversation list features include getting the conversation list and processing the conversation list update.
This section describes how to implement such features.

## Getting the Conversation List
You can call `ConvGetConvList` ([Details](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvGetConvList.html)) to get the conversation list. This API pulls locally cached conversations. If any server conversation is updated, the SDK will automatically sync the update and notify you in the `TIMConvEventCallback` callback.

User conversations are returned in a list that stores `ConvInfo` objects.

Sample code:


```c#
TIMResult res = TencentIMSDK.ConvGetConvList((int code, string desc, List<ConvInfo> info_list, string user_data)=>{
 // Process the async logic
});
```


## Updating the Conversation List
After the IM SDK is logged in successfully, the user goes online, or the network is disconnected and reconnected, the IM SDK will automatically update the conversation list.
You can get the updated conversation list in the following steps:
1. Add a conversation listener.
2. Receive and process conversation changes.
3. Remove the conversation listener. This step is optional and can be performed as needed.

### Adding a conversation listener
Call `SetConvEventCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetConvEventCallback.html)) to add a conversation listener to receive conversation change events.

Sample code:

```c#
TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
 // Process the callback logic
});
```


You can listen for the event in `TIMConvEvent` ([Details](https://comm.qq.com/im/doc/unity/en/enums/TIMConvEvent.html)) to get the notification of a conversation list change.

Currently, the IM SDK supports the following conversation change events:

| Event                | Description                   | Suggestion                                                                                                               |
| -------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| kTIMConvEvent_Add    | A new conversation was added. | Re-sort the conversations when the user receives a one-to-one message from a new colleague or is invited to a new group. |
| kTIMConvEvent_Del    | A conversation was deleted.   | Trigger this event when the user deletes a conversation.                                                                 |
| kTIMConvEvent_Update | A conversation was updated.   | Trigger this event when the unread count of a conversation changes or a new message is received.                         |
| kTIMConvEvent_Start  | A conversation was started.   |                                                                                                                          |
| kTIMConvEvent_Finish | A conversation was ended.     |                                                                                                                          |


### Removing a conversation listener
Pass in `null` for `SetConvEventCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetConvEventCallback.html)) to remove a conversation listener to stop receiving conversation change events.
This step is optional and can be performed as needed.

Sample code:


```c#
TencentIMSDK.SetConvEventCallback(null);
```



### Sending a message without updating the conv_last_msg
On the UI of conversation list, it is usually necessary to display the preview and send time of the latest message in each conversation. In this case, you can use `conv_last_msg` of `ConvInfo` as the data source for implementation. However, in some cases, if you don't want some messages (such as system tips) to be displayed as the latest message in a conversation, you can set `message_excluded_from_last_message` to `false`/`no` when calling `MsgSendMessage`.

For directions on how to send a message, see [MsgSendMessage(String, TIMConvType, Message, StringBuilder, ValueCallback<Message>)](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessage.html).





