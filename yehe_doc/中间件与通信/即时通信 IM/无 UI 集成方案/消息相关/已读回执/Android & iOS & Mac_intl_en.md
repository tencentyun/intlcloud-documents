## Feature Description
If a message sender wants to know who has or has not read the message, the sender needs to enable the message read receipt feature.
After this feature is enabled, the sender can set whether a message requires a read receipt when sending the message; if yes, the sender will receive a receipt after the message is read by the receiver.

Read receipts are supported for both one-to-one and group messages in the same way.

> ?
> - To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8).
> - Read receipts for group messages are supported only by the Enhanced edition on v6.1.2155 or later.
> - Read receipts for one-to-one messages are supported only by the Enhanced edition on v6.2.2363 or later.


## Message Read Receipt
### Specifying a group type for which to support message read receipts
Log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Group Message Read Receipts**.


You don't need to configure read receipts to be sent for one-to-one messages in the console, as they are supported by default.

### Specifying that a message requires a read receipt (by the sender)
After creating a message, the sender specifies that the message requires a read receipt through the `needReadReceipt` field in `V2TIMMessage` ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a53a9afe71275a00a54f1cb02f0e5eaaa) / [iOS and macOS](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMMessage.html#a41267989ed78823270ff16faf2356bc9)) and then sends the message to the conversation.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMMessage message = V2TIMManager.getMessageManager().createTextMessage("Group message read receipt");
// Specify that the message requires a read receipt
message.setNeedReadReceipt(true);
// Send the message
V2TIMManager.getMessageManager().sendMessage(message, null, "groupA", V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
  @Override
  public void onProgress(int progress) {
  }

  @Override
  public void onSuccess(V2TIMMessage message) {
  }

  @Override
  public void onError(int code, String desc) {
  }
});
```
:::
::: iOS and macOS
```objectivec
/// Sample API call
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"Group message read receipt"];
// Specify that the message requires a read receipt
message.needReadReceipt = YES;
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message receiver:nil groupID:@"groupA" priority:V2TIM_PRIORITY_NORMAL onlineUserOnly:NO offlinePushInfo:nil progress:nil succ:nil fail:nil];
```
:::
</dx-tabs>

### Sending a message read receipt (by the receiver)
After receiving the message, the receiver determines whether the message requires a read receipt based on the `needReadReceipt` field in `V2TIMMessage`. If yes, after the user reads the message, the receiver calls the `sendMessageReadReceipts` API ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a66ec09cb444ddca989e9518d5118275d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a375af7e0f3e0f0b3135ccd517de9fdd8)) to send a message read receipt.

Sample code:
<dx-tabs>
::: Android
```java
// Suppose the user has read the `message` message
if (!message.isSelf() && message.isNeedReadReceipt()) {
  List<V2TIMMessage> messageList = new ArrayList<>();
  messageList.add(message);
  V2TIMManager.getMessageManager().sendMessageReadReceipts(messageList, new V2TIMCallback() {
    @Override
    public void onSuccess() {
      // Read receipt for the message sent successfully
    }

    @Override
    public void onError(int code, String desc) {
      // Failed to send a read receipt for the message
    }
  });
}
```
:::
::: iOS and macOS
```objectivec
/// Sample API call
/// Suppose the user has read the `msg` message
if (!msg.isSelf && msg.needReadReceipt) {
    [[V2TIMManager sharedInstance] sendMessageReadReceipts:@[msg] succ:^{
        // Read receipt for the message sent successfully
    } fail:^(int code, NSString *desc) {
        // Failed to send a read receipt for the message
    }];
}
```
:::
</dx-tabs>

### Listening for a message read receipt notification (by the sender)
After the receiver sends a message read receipt, the sender will receive the read receipt notification in `onRecvMessageReadReceipts` of `V2TIMAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a000a30bf4b1c26bd32ec9231f54ffd4d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/zh-cn/protocolV2TIMAdvancedMsgListener-p.html#ac62bcff71b2876760e179178a91b8321)) and update the UI based on the notification to display the message as, for example, "Read by two members".

Sample code:
<dx-tabs>
::: Android
```java
V2TIMAdvancedMsgListener advancedMsgListener = new V2TIMAdvancedMsgListener() {
  @Override
  public void onRecvMessageReadReceipts(List<V2TIMMessageReceipt> receiptList) {
  for (V2TIMMessageReceipt receipt : receiptList) {
    // Message ID
    String msgID = receipt.getMsgID();
    // ID of the other party of the one-to-one message
    String userID = receipt.getUserID();
    // Read status of the other party of the one-to-one message
    boolean isPeerRead = receipt.isPeerRead();
    // Latest read count of the group message
    long readCount = receipt.getReadCount();
    // Latest unread count of the group message
    long unreadCount = receipt.getUnreadCount();
    }
  }
};
V2TIMManager.getMessageManager().addAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS and macOS
```objectivec
/// Sample API call
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];
- (void)onRecvMessageReadReceipts:(NSArray<V2TIMMessageReceipt *> *)receiptList {
    for(V2TIMMessageReceipt *receipt in receiptList) {
        // Message ID
        NSString *msgID = receipt.msgID;
        // ID of the other party of the one-to-one message
        NSString * userID = receipt.userID;
        // Read status of the other party of the one-to-one message
        BOOL isPeerRead = receipt.isPeerRead;
        // Group ID
        NSString * groupID = receipt.groupID;
        // Latest read count of the group message
        uint64_t readCount = receipt.readCount;
        // Latest unread count of the group message
        uint64_t unreadCount = receipt.unreadCount;
    }
}
```
:::
</dx-tabs>

### Pulling message read receipt information (by the sender)
After entering the message list, the sender pulls historical messages first, and then calls the `getMessageReadReceipts` API ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a50e3bc679e196866057415a7c192abf6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a69192bc43e551f34f5d483dae5e70410)) to pull the message read receipt information.

The `V2TIMMessageReceipt` field of the message read receipt is as described below:

| Attribute   | Definition                                            | Description                                                  |
| ----------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| msgID       | Message ID                                            | Unique message ID                                            |
| userID      | ID of the receiver                                    | If the message is a one-to-one message, this field indicates the ID of the receiver. |
| isPeerRead  | Whether the message is read by the receiver           | If the message is a one-to-one message, this field indicates whether the message is read by the receiver. |
| timestamp   | Time when the receiver marks the message as read      | This field is invalid when a message is read. If the message is a one-to-one message, when the receiver calls the `markC2CMessageAsRead` API to mark the message as read, the sender will receive the `onRecvC2CReadReceipt` callback which contains the `timestamp` information. |
| groupID     | Group ID                                              | If the message is a group message, this field indicates the group ID. |
| readCount   | Number of members who have read the group message     | If the message is a group message, this field indicates the number of members who have read the message. |
| unreadCount | Number of members who have not read the group message | If the message is a group message, this field indicates the number of members who have not read the message. |

Sample code:
<dx-tabs>
::: Android
```java
/// Sample API call (taking a group message as an example)
V2TIMManager.getMessageManager().getGroupHistoryMessageList("groupA", 20, null, new V2TIMValueCallback<List<V2TIMMessage>>() {
  @Override
  public void onSuccess(final List<V2TIMMessage> v2TIMMessages) {
    List<V2TIMMessage> receiptMsgs = new ArrayList<>();
    // If the message sent by you requires a read receipt, the message read receipt information will need to be pulled.
    for (V2TIMMessage msg : v2TIMMessages) {
      if (msg.isSelf() && msg.isNeedReadReceipt()) {
        receiptMsgs.add(msg);
      }
    }
    V2TIMManager.getMessageManager().getMessageReadReceipts(receiptMsgs, new V2TIMValueCallback<List<V2TIMMessageReceipt>>() {
      @Override
      public void onSuccess(List<V2TIMMessageReceipt> v2TIMMessageReceipts) {
        Map<String, V2TIMMessageReceipt> messageReceiptMap = new HashMap<>();
        for (V2TIMMessageReceipt receipt : v2TIMMessageReceipts) {
          messageReceiptMap.put(receipt.getMsgID(), receipt);
        }
        for (V2TIMMessage msg : v2TIMMessages) {
          V2TIMMessageReceipt receipt = messageReceiptMap.get(msg.getMsgID());
          if (receipt != null) {
            // ID of the other party of the one-to-one message
            String userID = receipt.getUserID();
            // Read status of the other party of the one-to-one message
            boolean isPeerRead = receipt.isPeerRead();
            // Group ID
            String groupID = receipt.getGroupID();
            // Message read count. If `readCount` is `0`, no one has read the message.
            long readCount = receipt.getReadCount();
            // Message unread count. If `unreadCount` is `0`, all members have read the message.
            long unreadCount = receipt.getUnreadCount();
          }
        }
      }

      @Override
      public void onError(int code, String desc) {
        // Failed to pull the message read status
      }
    });
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to pull the message
  }
});
```
:::
::: iOS and macOS
```objectivec
/// Sample API call (taking a group message as an example)
[[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    NSMutableArray *receiptMsgs = [NSMutableArray array];
    // If the message sent by you requires a read receipt, the message read receipt information will need to be pulled.
    for (V2TIMMessage *msg in msgs) {
        if (msg.isSelf && msg.needReadReceipt) {
            [receiptMsgs addObject:msg];
        }
    }
    [[V2TIMManager sharedInstance] getMessageReadReceipts:receiptMsgs succ:^(NSArray<V2TIMMessageReceipt *> *receiptList) {
       NSMutableDictionary *param = [NSMutableDictionary dictionary];
       for (V2TIMMessageReceipt *receipt in receiptList) {
           [param setObject:receipt forKey:receipt.msgID];
       }
       for (V2TIMMessage *msg in msgs) {
           V2TIMMessageReceipt *receipt = param[msg.msgID];
           // ID of the other party of the one-to-one message
           NSString * userID = receipt.userID;
           // Read status of the other party of the one-to-one message
           BOOL isPeerRead = receipt.isPeerRead;
           // Group ID
           NSString * groupID = receipt.groupID;
           // Message read count. If `readCount` is `0`, no one has read the message.
           uint64_t readCount = receipt.readCount;
           // Message unread count. If `unreadCount` is `0`, all members have read the message.
           uint64_t unreadCount = receipt.unreadCount;
       }
    } fail:^(int code, NSString *desc) {
       // Failed to pull the message read status
    }];
} fail:^(int code, NSString *desc) {
    // Failed to pull the message
}];
```
:::
</dx-tabs>

### Pulling the list of members who have or have not read a group message (by the sender)
To view the list of members who have or have not read a group message, the sender can call the `getGroupMessageReadMemberList` API ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a93c48782f3e127e8a50aef1bf8829099) / [iOS and macOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#aa345a87cfa4da2983f878bb5385d0b82)) to pull the member list by page.

<dx-tabs>
::: Android
```java
/// Sample API call
V2TIMManager.getMessageManager().getGroupMessageReadMemberList(message, V2TIMMessage.V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ, 0, 100, new V2TIMValueCallback<V2TIMGroupMessageReadMemberList>() {
  @Override
  public void onSuccess(V2TIMGroupMessageReadMemberList v2TIMGroupMessageReadMemberList) {
    // `members` is the list of members who have read the message pulled from the current page.
    List<V2TIMGroupMemberInfo> members = v2TIMGroupMessageReadMemberList.getMemberInfoList();
    // `nextSeq` indicates the cursor position for the next pull.
    long nextSeq = v2TIMGroupMessageReadMemberList.getNextSeq();
    // `isFinished` indicates whether the list of members who have read the message has been fully pulled.
    boolean isFinished = v2TIMGroupMessageReadMemberList.isFinished();
    // If the list of members who have read the message is not fully pulled, continue with the next pull (here is only the sample code. We recommend paged pull be triggered by a user click).
    if (!isFinished) {
      V2TIMManager.getMessageManager().getGroupMessageReadMemberList(message, V2TIMMessage.V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ, nextSeq, 100, new V2TIMValueCallback<V2TIMGroupMessageReadMemberList>() {
        @Override
        public void onSuccess(V2TIMGroupMessageReadMemberList v2TIMGroupMessageReadMemberList) {
            // List of members who have read the message pulled successfully
        }

        @Override
        public void onError(int code, String desc) {
            // Failed to pull the list of members who have read the message
        }
      });
    }    
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to pull the list of members who have read the message
  }
});
```
:::
::: iOS and macOS
```objectivec
/// Sample API call
[[V2TIMManager sharedInstance] getGroupMessageReadMemberList:message filter:V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ nextSeq:0 count:100 succ:^(NSMutableArray<V2TIMGroupMemberInfo *> *members, uint64_t nextSeq, BOOL isFinished) {
    // `members` is the list of members who have read the message pulled from the current page.
    // `nextSeq` indicates the cursor position for the next pull.
    // `isFinished` indicates whether the list of members who have read the message has been fully pulled.
    // If the list of members who have read the message is not fully pulled, continue with the next pull (here is only the sample code. We recommend paged pull be triggered by a user click).
    if (!isFinished) {
        [[V2TIMManager sharedInstance] getGroupMessageReadMemberList:message filter:V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ nextSeq:nextSeq count:100 succ:^(NSMutableArray<V2TIMGroupMemberInfo *> *members, uint64_t nextSeq, BOOL isFinished) {
            // List of members who have read the message pulled successfully
        } fail:^(int code, NSString *desc) {
            // Failed to pull the list of members who have read the message
        }];
    }
} fail:^(int code, NSString *desc) {
    // Failed to pull the list of members who have read the message
}];
```
:::
</dx-tabs>
