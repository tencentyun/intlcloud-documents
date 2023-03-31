## Feature Description
A user's conversation list usually contains multiple conversations. If there is a new message in one of the conversations, a badge needs to be displayed in the list cell to indicate the unread count.
After the user clicks to enter the conversation and goes back to the conversation list, the unread count is cleared, and the badge disappears.
In some applications, the total unread count of all the conversations is calculated and displayed at the bottom tab of the conversation list.

This document describes how to implement the conversation unread count notification feature.

## Getting the Total Unread Count of All the Conversations
In general cases, to get the total unread count of all the conversations, you can traverse the conversation list to get the `ConvInfo` information of each conversation and add the `conv_unread_num` values of all the `ConvInfo` objects to get the final result and display it on the UI.
The IM SDK provides the `ConvGetTotalUnreadMessageCount` API to query the total unread count of all the conversations.
When the total unread count changes, the SDK will notify you of the latest total unread count through the `SetConvTotalUnreadMessageCountChangedCallback` callback.


Below are detailed steps.

### Getting the total unread count
Call `ConvGetTotalUnreadMessageCount` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_ConvGetTotalUnreadMessageCount_com_tencent_imsdk_unity_callback_ValueCallback_com_tencent_imsdk_unity_types_GetTotalUnreadNumberResult__)) to get the total unread count of all the conversations and update it on the UI.

Sample code:


```c#
// Get the total unread count
TIMResult res = TencentIMSDK.ConvGetTotalUnreadMessageCount((int code, string desc, GetTotalUnreadNumberResult unread, string user_data)=>{
 // Process the async logic
});
```


### Notification of a change in the total unread count

Call `SetConvTotalUnreadMessageCountChangedCallback` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_SetConvTotalUnreadMessageCountChangedCallback_com_tencent_imsdk_unity_callback_ConvTotalUnreadMessageCountChangedCallback_)) to add a conversation listener to receive notifications of a change in the total unread count.

Sample code:


```c#
TencentIMSDK.SetConvTotalUnreadMessageCountChangedCallback((int total_unread_count, string user_data)=>{
 // Process the callback logic
});
```


## Clearing the Conversation Unread Count
After the user clicks to enter a conversation and goes back to the conversation list, the unread count needs to be cleared, after which the badge in the conversation list needs to disappear.
The IM SDK provides three APIs to clear the unread count for different conversation types:
* `MsgReportReaded` is used to clear the unread count of a **one-to-one** conversation.
* `MsgSendMessageReadReceipts` is used to clear the unread count of a **group** conversation.
* `MsgMarkAllMessageAsRead` is used to clear the unread count of **all** the conversations.

Below are detailed steps.
### One-to-one chat
Call `MsgReportReaded` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgReportReaded_System_String_com_tencent_imsdk_unity_enums_TIMConvType_com_tencent_imsdk_unity_types_Message_com_tencent_imsdk_unity_callback_NullValueCallback_)) to clear the unread count of a specified one-to-one conversation.

Sample code:


```c#
// `message` can be set to `null`. In that case, the timestamp of the latest message (if any) in the conversation or the current time is used as the read timestamp for reporting. If a message needs to be specified, the timestamp of this specified message is used as the read timestamp for reporting. We recommend you use the message JSON content in the message array obtained from the received new message or the message JSON content located by the message locator; otherwise, repeated message JSON content will be constructed.
TIMResult res = TencentIMSDK.MsgReportReaded(conv_id, TIMConvType TIMConvType.kTIMConv_C2C, null, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```

After `MsgReportReaded` is called successfully:
1. If the caller has called `SetConvEventCallback` to add a conversation listener, it will receive the `ConvEventCallback` callback and update the UI.
2. The sender will receive the `MsgReadedReceiptCallback` callback that contains the timestamp when the conversation unread count is cleared.


### Group chat
Call `MsgSendMessageReadReceipts` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgSendMessageReadReceipts_System_Collections_Generic_List_com_tencent_imsdk_unity_types_Message__com_tencent_imsdk_unity_callback_NullValueCallback_)) to clear the unread count of a specified group conversation.

Sample code:


```c#
TIMResult res = TencentIMSDK.MsgSendMessageReadReceipts(msg_array, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```

After `MsgReportReaded` is called successfully:
1. If the caller has called `SetConvEventCallback` to add a conversation listener, it will receive the `ConvEventCallback` callback and update the UI.
2. The sender will receive the `MsgReadedReceiptCallback` callback that contains the timestamp when the conversation unread count is cleared.

### All conversations
Call `MsgMarkAllMessageAsRead` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgMarkAllMessageAsRead_com_tencent_imsdk_unity_callback_NullValueCallback_)) to clear the unread count of all the conversations.


Sample code:


```c#
TIMResult res = TencentIMSDK.MsgMarkAllMessageAsRead((int code, string desc, string user_data)=>{
 // Process the async logic
});
```


After `MsgMarkAllMessageAsRead` is called successfully, if the caller has called `SetConvEventCallback` to add a conversation listener, it will receive the `ConvEventCallback` callback and update the UI.

Sample code:

```c#
TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
 // Process the callback logic
});
```
