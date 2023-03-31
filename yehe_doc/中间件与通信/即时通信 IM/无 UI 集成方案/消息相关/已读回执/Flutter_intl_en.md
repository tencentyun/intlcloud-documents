## Feature Description
If a message sender wants to know who has or has not read the message, the sender needs to enable the message read receipt feature.
After this feature is enabled, the sender can set whether a message requires a read receipt when sending the message; if yes, the sender will receive a receipt after the message is read by the receiver.

Read receipts are supported for both one-to-one and group messages in the same way.

> ?
> - To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8).
> - Read receipts for group messages are supported only by Flutter v3.8.0.


## Message Read Receipt
### Specifying a group type for which to support message read receipts
Log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Group Message Read Receipts**.


### Specifying that a message requires a read receipt (by the sender)
After creating a message, the sender specifies that the message requires a read receipt through the `needReadReceipt` field in `V2TimMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html#needreadreceipt)) and then sends the message to the conversation.

Sample code:


```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createCustomMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createCustomMessage(
            data: 'Typing...',
          );
// Set `needReadReceipt` to `true` when sending the message
  TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: createCustomMessageRes.data.id, receiver: "", groupID: "groupID",onlineUserOnly: true,needReadReceipt: true);
```


### Sending a message read receipt (by the receiver)
After receiving the message, the receiver determines whether the message requires a read receipt based on the `needReadReceipt` field in `V2TIMMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html#needreadreceipt)). If yes, after the user reads the message, the receiver calls the `sendMessageReadReceipts` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessageReadReceipts.html)) to send a read receipt.

Sample code:


```java
V2TimCallback sendMessageReadReceipts = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessageReadReceipts(messageIDList: ['msgids']);
  if(sendMessageReadReceipts.code == 0){
    // Succeeded
  }else{
    // Failed
  }
```


### Listening for a message read receipt notification (by the sender)
After the receiver sends a message read receipt, the sender can listen for a receipt notification through `onRecvMessageReadReceipts` in `V2TimAdvancedMsgListener` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnRecvMessageReadReceipts.html)) and update the UI based on the notification to display the message as, for example, "Read by two members".

Sample code:


```dart
onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {
      receiptList.forEach((element) { 
        element.groupID;  // Group ID
        element.msgID; // Message ID
        element.readCount;// Latest read count of the group message
        element.unreadCount;// Latest unread count of the group message
        element.userID; //  ID of the other party of the one-to-one message
      });
},
```


### Pulling message read receipt information (by the sender)
After entering the message list, the sender pulls historical messages first, and then calls the `getMessageReadReceipts` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/getMessageReadReceipts.html)) to pull the message read receipt information.

The `V2TimessageReceipt` field of the message read receipt is as described below:

| Attribute   | Definition                                            | Description                                                  |
| ----------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| msgID       | Message ID                                            | Unique message ID                                            |
| userID      | ID of the receiver                                    | If the message is a one-to-one message, this field indicates the ID of the receiver. |
| timestamp   | Time when the receiver marks the message as read      | This field is invalid when a message is read. If the message is a one-to-one message, when the receiver calls the `markC2CMessageAsRead` API to mark the message as read, the sender will receive the `onRecvC2CReadReceipt` callback which contains the `timestamp` information. |
| groupID     | Group ID                                              | If the message is a group message, this field indicates the group ID. |
| readCount   | Number of members who have read the group message     | If the message is a group message, this field indicates the number of members who have read the message. |
| unreadCount | Number of members who have not read the group message | If the message is a group message, this field indicates the number of members who have not read the message. |

Sample code:


```dart
V2TimValueCallback<List<V2TimMessageReceipt>> getMessageReadReceipts = await  TencentImSDKPlugin.v2TIMManager.getMessageManager().getMessageReadReceipts(messageIDList: []);
  if(getMessageReadReceipts.code == 0){
    getMessageReadReceipts.data.forEach((element) {
      // Parse the group message read receipt
      element.groupID;
      element.msgID;
      element.readCount;
      element.timestamp;
      element.unreadCount;
      element.userID;
    });
  }
```


### Pulling the list of members who have or have not read a group message (by the sender)
To view the list of members who have or have not read a group message, the sender can call the `getGroupMessageReadMemberList`API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/getGroupMessageReadMemberList.html)) to pull the member list by page.



```dart
V2TimValueCallback<V2TimGroupMessageReadMemberList> getGroupMessageReadMemberList = await  TencentImSDKPlugin.v2TIMManager.getMessageManager().getGroupMessageReadMemberList(messageID: "", filter: GetGroupMessageReadMemberListFilter.V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ,);

 if(getGroupMessageReadMemberList.code == 0){
   // Get the list of members who have or have not read the group message
   getGroupMessageReadMemberList.data.isFinished;
   getGroupMessageReadMemberList.data.memberInfoList;
   getGroupMessageReadMemberList.data.nextSeq;
 }
```
