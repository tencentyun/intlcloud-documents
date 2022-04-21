## Message Classification
IM messages are classified by message destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| One-to-one message | C2CMessage | Also called C2C message. When sending a one-to-one message, you must specify the UserID of the message recipient, and only the recipient can receive this message. |
| Group message | GroupMessage | When sending a group message, you must specify the groupID of the target group, and all users in this group can receive this message. |

IM messages can also be classified by content into text messages, custom (signaling) messages, image messages, video messages, voice messages, file messages, location messages, combined messages, and group tips.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| Custom message | CustomElem | It is a section of binary buffer and often used to transfer custom signaling in your application. |
| Image message | ImageElem | When the IM SDK sends an original image, it automatically generates two images in different sizes. The three images are called the original image, large image, and thumbnail. |
| Video message | VideoElem | A video message contains a video file and an image. |
| Voice message | SoundElem | It supports displaying a red dot upon playback of the voice message. |
| File message | FileElem | A file message cannot exceed 100 MB. |
| Location message | LocationElem | A location message contains three fields: location description, longitude, and latitude. |
| Combined message | MergerElem | Up to 300 messages can be combined. |
| Group tip | GroupTipsElem | A group tip is often used to carry a system notification in a group, such as a notification indicating the following: a member joins or leaves the group; the group description is modified; or the profile of a group member is changed. |

## Sending and Receiving Simple Messages
[V2TIMManager.h](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html) provides a set of simple APIs for sending and receiving messages. Although these APIs can only be used to send or receive text messages and custom (signaling) messages, they are easy to use and it takes only a few minutes to complete interfacing.

### Sending text and signaling messages
To send text messages, call [sendC2CTextMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a8f4eb13fbf039c0216f14f178d9f9f36) or [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a74fc1a30a7c1a292e625c5b2cf1e91f0).
To send one-to-one custom (signaling) messages, call [sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20c6ea174904a99fafebb5c1b3475b39) or [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#af8b149e054d532a8fb5ca12a7160c90f). A custom message is essentially a section of binary buffer, and is often used to transfer custom signaling in your application.

### Receiving text and signaling messages
To listen to simple text and signaling messages, call [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88). To listen to image, video, and voice messages, call [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) defined in [V2TIMManager + Message.h](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html).

>! Do not use [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) together with [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab); otherwise, logic bugs may occur.

### Typical example: Sending and receiving on-screen comments
In the livestreaming scenario, it is a common way of communication to send or receive on-screen comments in an audio-video group. This can be easily implemented through the simple message APIs.

1. The anchor can call [createGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4bada5d6a06fac04a1424ae2c597e389) to create an audio-video group (AVChatRoom) and record the group ID in the list of rooms in "Broadcasting" state.
2. A viewer can select an anchor that he/she likes, and call [joinGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a9979ed856657724d317791c723bacef5) to join the AVChatRoom created by this anchor.
3. The message sender can call [sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a74fc1a30a7c1a292e625c5b2cf1e91f0) to send a group text message as the on-screen comment.
4. The message recipient can call [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) to register a simple message listener, and use the listener callback function [onRecvGroupTextMessage](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#a3a25f772d74fd81698d087ec043d9366) to obtain text messages.

"FlyHeart" is an instruction. To configure the "FlyHeart" feature for a live room, perform the steps below:
1. Define a custom message type, such as a JSON string `{ "command": "favor", "value": 101 }`.
2. Call [sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#af8b149e054d532a8fb5ca12a7160c90f) to send a message, and call [onRecvGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#ad01776119c059bff49b804c8152c70d9) to receive the message.

## Sending and Receiving Rich Media Messages
Image, video, voice, file, and location messages are called rich media messages. Compared with sending or receiving simple messages, it is more complex to send or receive rich media messages.
- Before sending a rich media message, use the `create` function to create an object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html). Then, call the corresponding `send` API to send this message.
- When receiving the rich media message, check `elemType` and perform secondary parsing on `Elem` obtained based on `elemType`.


### Sending rich media messages
The following takes an image message as an example to describe the process of sending a rich media message.
1. The sender calls [createImageMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) to create an image message and obtain the [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html) message object.
2. The sender calls [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send the previously created message object.

### Receiving rich media messages

1. The recipient calls [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) to set the advanced message listener.
2. The recipient obtains the [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html) image message through the [onRecvNewMessage](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html) listener callback.
3. The recipient parses `elemType` in [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html), and performs secondary parsing based on the message type to obtain the content of `Elem` in the message.

### Typical example: Sending and receiving image messages
The sender creates and sends an image message.
```
// Obtain the local image path
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// Create an image message
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
// Send the image message
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil 
priority:V2TIM_PRIORITY_DEFAULT 
onlineUserOnly:NO offlinePushInfo:nil progress:^(uint32_t progress) {
   // Image upload progress (0-100)
} succ:^{
   // The image message was sent successfully
} fail:^(int code, NSString *msg) {
   // The image message failed to be sent
}];
```

The recipient identifies the image message, and parses the message to obtain the original image, large image, and thumbnail contained in the message.
```
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
  if (msg.elemType == V2TIM_ELEM_TYPE_IMAGE) {
    V2TIMImageElem *imageElem = msg.imageElem;
    // An image message contains an image in three different sizes: original image, large image, and thumbnail. The SDK automatically generates a large image and a thumbnail.
    // A large image is obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 720 pixels.
    // A thumbnail is obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 198 pixels.
    NSArray<V2TIMImage *> *imageList = imageElem.imageList;
    for (V2TIMImage *timImage in imageList) {
        NSString *uuid = timImage.uuid; // Image ID
        V2TIMImageType type = timImage.type; // Image type
        int size = timImage.size; // Image size (bytes)
        int width = timImage.width; // Image width
        int height = timImage.height; // Image height
        // Set the image download path `imagePath`. Here, `uuid` can be used as an identifier to avoid repeated download.
        NSString *imagePath = [NSTemporaryDirectory() stringByAppendingPathComponent:
                            [NSString stringWithFormat: @"testImage%@",timImage.uuid]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:imagePath]) {
                [timImage downloadImage:imagePath 
                                progress:^(NSInteger curSize, NSInteger totalSize) {
                    NSLog(@"Image download progress: curSize: %lu,totalSize:%lu",curSize,totalSize);
                } succ:^{
                    NSLog(@"Image download completed");
                } fail:^(int code, NSString *msg) {
                    NSLog(@"Image download failed: code: %d,msg:%@",code,msg);
                }];
        } else {
                // The image already exists
        }
    }
  }
}
```

>? For more information on the message parsing sample code, see [FAQs > 5. How can I parse different types of messages](#msgAnalyze).

## Sending and Receiving Group @ Messages

For a group @ message, the sender can listen to the input of the @ character in the input box and call the group member selection interface. After selection is completed, the input box displays the content in the format of `"@A @B @C......"`, and then the sender can continue to edit the message content and send the message. On the group chat list of the recipient’s conversation interface, the identifier `"someone@me"` or `"@all members"` will be displayed to remind the user that the user was mentioned by someone in the group.

>? Currently, only text @ messages are supported.

### Sending group @ messages

1. The sender listens to the text input box on the chat interface and launches the group member selection interface. After selection is completed, the ID and nickname of the selected member are returned. The ID is used to construct the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html), and the nickname is to be displayed in the text box.
2. The sender calls [createTextAtMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ad33b6f7cb849054333b18eeb1e9c187d) of [V2TIMManager+Message](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html) to create an @ text message and obtain the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html).
3. The sender calls [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send the created @ message object.

### Receiving group @ messages

1. During conversation loading and update, you need to call the [groupAtInfolist](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a5659c29a54304e89e61c25c2b073f8da) API of [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html) to obtain the @ data list of the conversation.
2. Obtain and update the @ data type to the @ information of the current conversation through the [atType](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupAtInfo.html#a1486d853fd6f8ae074714ec8059f7621) API of the [V2TIMGroupAtInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupAtInfo.html) object on the list.

### Typical examples: sending and receiving group @ messages

- **Sending a group @ message:**
The sender creates and sends a group @ message.

```objective-c
// Obtain the ID data of the @ group member
TUITextMessageCellData *text = (TUITextMessageCellData *)data;
NSMutableArray<NSString *> *atUserList = text.atUserList;

// Create a group @ message
V2TIMMessage *atMsg = [[V2TIMManager sharedInstance] createTextAtMessage:text.content atUserList:atUserList];

// Send the group @ message
[[V2TIMManager sharedInstance] sendMessage:atMsg
                                  receiver:nil
                                   groupID:@"toGroupId"
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:nil
                                  progress:nil
                                      succ:^{
    NSLog(@"group @ message is sent successfully");
}
                                      fail:^(int code, NSString *desc) {
    NSLog(@"group @ message failed to be sent");
}];
```

- **Receiving a group @ message:**
 During conversation loading and update, obtain the group @ data list, parse the current @ type, and display the prompt text based on the @ type.

```objective-c
// Obtain the group @ data list
NSArray<V2TIMGroupAtInfo *> *atInfoList = conversation.groupAtInfolist;

// Parse the @ type (@me, @all members, @me and @all members)
BOOL atMe = NO;         // Whether it's @me
BOOL atAll = NO;        // Whether it's @all members
NSString *atTipsStr = @"";
for (V2TIMGroupAtInfo *atInfo in atInfoList) {
    switch (atInfo.atType) {
        case V2TIM_AT_ME:
            atMe = YES;
            break;
        case V2TIM_AT_ALL:
            atAll = YES;
            break;
        case V2TIM_AT_ALL_AT_ME:
            atMe = YES;
            atAll = YES;
            break;
        default:
            break;
    }
}

// Based on the @ type, prompt:
if (atMe && !atAll) {
    atTipsStr = @"[someone@me]";
}
if (!atMe && atAll) {
    atTipsStr = @"[@all members]";
}
if (atMe && atAll) {
    atTipsStr = @"[someone@me][@all members]";
}
```

## Sending and Receiving Combined Messages
To implement the Combine and Forward feature similar to that in WeChat, it is necessary to create a combined message according to the original message list, and then send the combined message to the peer end. After the peer end receives the combined message, it will parse out the original message list. A title and abstracts are required to display the combined message. 

- **Sending a combined message**
Usually, when we receive a combined message, the chat UI will look like this:

| Chat History of Vinson and Lynx | Title |
|---------|---------|
| Vinson: When is the new version of SDK scheduled to go online? | abstract1 |
| Lynx: Next Monday. The specific time depends on the system test result in these two days. | abstract2 |
| Vinson: OK | abstract3 |

The chat UI will display only the title and abstract information of the combined message, and the combined message list will be displayed only when the user clicks the combined message. To create a combined message, it is necessary to set not only the combined message list, but also the title and abstract information. The implementation process is as follows:
1. Call the [createMergerMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a0f56dde34bd350dd6e829e5bff067722) API to create a combined message.
2. Call the [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) API to send the combined message.

- **Receiving a combined message**
When receiving a combined message [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html), use [V2TIMMergerElem](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMergerElem.html) to get [title](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMergerElem.html#ad39b2fbc36bb32f1287f61db3d3477a1) and [abstractList](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMergerElem.html#ad39b2fbc36bb32f1287f61db3d3477a1) for UI display. When a user clicks the combined message, call the [downloadMergerMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMergerElem.html#ad77abfe27eabf237aee7c951100e6755) API to download the combine message list for UI display.

> Only available in Enhanced Edition v5.2.210 or later.

### Typical examples: sending and receiving combined messages
- **Sending a combined message**
The sender creates and sends a combined message.

```objective-c
// List of messages to be forwarded, which can contain combined messages but not group tips
NSArray *msgs = @[message1,message2...];  
// Title of the combined message
NSString *title = @"Chat History of Vinson and Lynx";  
// Abstract list of the combined message
NSArray *abstactList = @[@"abstract1",@"abstract2",@"abstract3"]; 
// Combined messages are compatible with text. If SDKs of early versions do not support combined messages, the user will receive a text message with the content `compatibleText`.
NSString *compatibleText = @"Please upgrade to the latest version to check the combined message"; 
// Create a combined message
V2TIMMessage *mergeMessage = [[V2TIMManager sharedInstance] createMergerMessage:msgs title:title 
abstractList:abstactList compatibleText:compatibleText];
// Send the combined message to the user Denny
[[V2TIMManager sharedInstance] sendMessage:mergeMessage receiver:@"denny"  groupID:nil
 priority:V2TIM_PRIORITY_NORMAL  onlineUserOnly:NO  offlinePushInfo:nil progress:nil succ:nil fail:nil];
```

- **Receiving a combined message**
The recipient receives and parses a combined message:
```objective-c
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_MERGER) {
            // Get the combined message elements
            V2TIMMergerElem *mergerElem = msg.mergerElem;
            // Get the title
            NSString *title = mergerElem.title;
            // Get the abstract list
            NSArray *abstractList = mergerElem.abstractList;
            // Download the combined message list when the user clicks the combined message
            [msg.mergerElem downloadMergerMessage:^(NSArray<V2TIMMessage *> *msgs) {
                // Download succeeded. `msgs` is the combined message list
                for (V2TIMMessage *subMsg in msgs) {
                    // If the combined message list still contains combined messages, you can continue parsing
                    if (subMsg.elemType == V2TIM_ELEM_TYPE_MERGER) {
                        V2TIMMergerElem *mergerElem = subMsg.mergerElem;
                        // Get the title
                        NSString *title = mergerElem.title;
                        // Get the abstract list
                        NSArray *abstractList = mergerElem.abstractList;
                        // Download the combined message list when the user clicks the combined message
                        [msg.mergerElem downloadMergerMessage:nil fail:nil];
                    }
                }
            } fail:^(int code, NSString *desc) {
                // Download failed
            }];
        }
}
```


## Read Receipts for Group Messages
When sending a group message, you can set whether a message requires a read receipt. If yes, the receiver can send a read receipt only after the message is read.
>?
- Only available in Enhanced Edition v6.1.2155 or later.
- This feature requires the Flagship Edition package.
- You need to set the group types that support message receipts on the **Feature Configuration** > **Login and Message** > **Group Message Read Receipts** page in the [IM console](https://console.cloud.tencent.com/im).
  

### The sender specifies that group messages require read receipts
After creating a message, the sender specifies that the message requires a read receipt by using the [needReadReceipt](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html#a41267989ed78823270ff16faf2356bc9) field of the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html), and sends the message to the group.
```java
/// API call example
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"Group message read receipt"];
// Specify that the message requires a read receipt
message.needReadReceipt = YES;
// Send the message
[[V2TIMManager sharedInstance] sendMessage:message receiver:nil groupID:@"groupA" priority:V2TIM_PRIORITY_NORMAL onlineUserOnly:NO offlinePushInfo:nil progress:nil succ:nil fail:nil];
```

### The receiver sends the group message read receipt
When receiving a message, the receiver determines whether the message requires a read receipt by using the [needReadReceipt](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html#a41267989ed78823270ff16faf2356bc9) field of the message object [V2TIMMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html). If a read receipt is required, and the user has read the message, the receiver calls the [sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a375af7e0f3e0f0b3135ccd517de9fdd8) API to send the message read receipt.
```java
/// API call example
/// Assume that the message is read by user
if (!msg.isSelf && msg.needReadReceipt) {
    [[V2TIMManager sharedInstance] sendMessageReadReceipts:@[msg] succ:^{
        // Message read receipt sent successfully
    } fail:^(int code, NSString *desc) {
        // Failed to send the message read receipt
    }];
}
```

### The sender listens for notifications of group message read receipts
After the receiver sends a message read receipt, the sender can use the [onRecvMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#ac62bcff71b2876760e179178a91b8321) callback of [V2TIMAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html) to listen for the notifications of group message read receipts.
```java
/// API call example
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];
- (void)onRecvMessageReadReceipts:(NSArray<V2TIMGroupMessageReceipt *> *)receiptList {
    for(V2TIMMessageReceipt *receipt in receiptList) {
        // Unique ID of the message
        NSString *msgID = receipt.msgID;
        // Latest message read count
        uint64_t readCount = receipt.readCount;
        // Latest message unread count
        uint64_t unreadCount = receipt.unreadCount;
    }
}
```

### The sender proactively pulls group message read receipt information
When the sender enters the message list UI from other UIs, it pulls the message history first and then call the [getMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a69192bc43e551f34f5d483dae5e70410) API to pull message read receipt information.

```java
/// API call example
[[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    NSMutableArray *receiptMsgs = [NSMutableArray array];
    // If the message is sent by you and it requires a read receipt, the message read receipt information needs to be pulled.
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

### The sender proactively pulls the list of members who have read a group message
The sender can call the [getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aa345a87cfa4da2983f878bb5385d0b82) API to pull the list of members who have read a group message in pagination mode.

```java
/// API call example
[[V2TIMManager sharedInstance] getGroupMessageReadMemberList:message filter:V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ nextSeq:0 count:100 succ:^(NSMutableArray<V2TIMGroupMemberInfo *> *members, uint64_t nextSeq, BOOL isFinished) {
    // `members` is the list of members who have read the message pulled for the current page
    // `nextSeq` indicates the cursor position for the next page pulling
    // `isFinished` indicates whether the read member list has been fully pulled
    // If the read member list is not fully pulled, continue with the next pulling (here is only the sample code. In pagination pulling mode, the action is recommended to be triggered by UI clicking by user).
    if (!isFinished) {
        [[V2TIMManager sharedInstance] getGroupMessageReadMemberList:message filter:V2TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ nextSeq:nextSeq count:100 succ:^(NSMutableArray<V2TIMGroupMemberInfo *> *members, uint64_t nextSeq, BOOL isFinished) {
            // The read member list is pulled successfully
        } fail:^(int code, NSString *desc) {
            // Failed to pull the read member list
        }];
    }
} fail:^(int code, NSString *desc) {
    // Failed to pull the read member list
}];
```


## Read Receipts for One-to-One Messages
Currently, the one-to-one chat scenario does not support read receipts at the message level. In the scenario, when the receiver calls the [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ad7d239caa69ec7da45f52d6bb02ee19c) API to mark the conversation as read, and the sender will receive a read receipt, indicating that the peer has read the conversation. The read receipt carries the conversation read time of the receiver, and the sender can consider that all messages before this time are read by the peer.

### The receiver marks a conversation as read

```java
// Mark messages coming from Haven as read
[[V2TIMManager sharedInstance] markC2CMessageAsRead:@"haven" succ:^{
} fail:^(int code, NSString *msg) {
}];
```

### The sender listens for the notifications of conversation read receipts
The event notification of the conversation read receipt is located in the advanced message listener [V2TIMAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html). To perceive the event, the sender must call [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) to set the listener. Then, the sender can perceive the event through the [onRecvC2CReadReceipt](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html) callback.

```java
- (void)onRecvC2CReadReceipt:(NSArray<V2TIMMessageReceipt *> *)receiptList {
      // The sender may receive multiple read receipts at a time. Therefore, the array callback mode is used here.
      for (V2TIMMessageReceipt *receipt in receiptList) {
          // Message recipient
          NSString * receiver = receipt.userID;
          // Time of the read receipt. A message is considered as read if the timestamp in the chat window is not later than `timestamp` here.
          time_t timestamp = receipt.timestamp;
      }
}
@end
```

## Sending Messages Excluded from the Unread Count
Normally, when you send one-to-one chat messages and group messages, the messages are included in the unread count (you can get the unread message count of a conversation via the [unreadCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6) API of the [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html) conversation object). If you need to send messages that are excluded from the unread count, such as tips and control messages, send them as follows:

>! Only available in Enhanced Edition v5.3.425 or later.

```objective-c
// Create the message object
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"This is a signaling message"];

// Set the identifier for excluding from the unread message count
message.isExcludedFromUnreadCount = YES;

// Send the message
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:YES offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // The message was successfully sent
} fail:^(int code, NSString *msg) {
    // The message failed to be sent
}];
```

## Sending Messages Excluded from the Conversation lastMsg

In certain scenarios, if you need to send messages that are excluded from `lastMsg` of a conversation, send them as follows:

> Only available in Enhanced Edition v5.4.666 or later.

```objective-c
// Create the message object
V2TIMMessage *message = [V2TIMManager.sharedInstance createTextMessage:content];
// Set the identifier for excluding from lastMsg of the conversation
message.isExcludedFromLastMessage = YES;
// Send the message
[V2TIMManager.sharedInstance sendMessage:message receiver:@"userA" groupID:nil priority:V2TIM_PRIORITY_NORMAL onlineUserOnly:NO offlinePushInfo:nil progress:^(uint32_t progress) {
    // Sending progress
} succ:^{
    // The message was successfully sent
} fail:^(int code, NSString *desc) {
    // The message failed to be sent
}];
```

## Sending Targeted Group Messages

A targeted group message is a message sent only to specified members in a group. You can send it as follows:

```objective-c
// Create an original message object
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"This is a targeted group message"];

// Create a targeted group message object, and specify the recipients "Vinson" and "Denny"
NSMutableArray *receiverList = [NSMutableArray array];
[receiverList addObject:@"vinson"];
[receiverList addObject:@"denny"];
V2TIMMessage *targetGroupMessage = [V2TIMManager.sharedInstance createTargetedGroupMessage:message receiverList:receiverList];

// Send the targeted group message in groupA
[[V2TIMManager sharedInstance] sendMessage:targetGroupMessage receiver:nil groupID:@"groupA"
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:NO offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // The message was successfully sent
} fail:^(int code, NSString *msg) {
    // The message failed to be sent
}];
```

>?
> Only available in Enhanced Edition v6.0.1975 or later.
>- This feature requires the Flagship Edition package.
>- The original message object for creating a targeted group message cannot be a group @ message.
>- The targeted group message feature is not available for Community and AVChatRoom groups.
>- By default, targeted group messages are excluded from the unread count of the group conversation.

## Setting APNs Offline Push

When the recipient's app is killed or when the recipient switches to the backend, the IM SDK cannot receive new messages through the normal network connection. In this scenario, the APNs service provided by Apple must be used to notify the recipient of new messages. For more information, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/39157).

### Setting the title and voice for APNs offline push
When sending messages, you can use the **offlinePushInfo** field in the [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) API to set the title and voice for APNs offline push.

```
// Create and send an image message to groupA, and customize the title and voice for offline push.
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// Create an image message
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
// Customize the title and voice for offline push. `01.caf` is a sample file, which must be linked to the Xcode project. Here, you only need to enter the file name with the extension.
pushInfo.title = @"Customize the title displayed";
pushInfo.iOSSound = @"01.caf";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:nil groupID:@"groupA" priority:V2TIM_PRIORITY_DEFAULT 
onlineUserOnly:NO offlinePushInfo:pushInfo progress:^(uint32_t progress) {
} succ:^{
    // The message was successfully sent
} fail:^(int code, NSString *msg) {
    // The message failed to be sent
}];
```

### Clicking a pushed message to go to the corresponding chat window
To implement this feature, the sender needs to set the extended field `ext` of the offline push object `offlinePushInfo`, when sending a message. When the recipient opens the app, the recipient can obtain `ext` through the `didReceiveRemoteNotification` system callback, and then go to the corresponding chat window based on the content of `ext`.

The following example assumes that Denny sends a message to Vinson.
- Sender: Denny needs to set `ext` before sending a message.
```
// Denny sets `offlinePushInfo` and specifies `ext` before sending a message
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"Text message"];
V2TIMOfflinePushInfo *info = [[V2TIMOfflinePushInfo alloc] init];
info.ext = @"jump to denny";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"vinson" groupID:nil priority:V2TIM_PRIORITY_DEFAULT
onlineUserOnly:NO offlinePushInfo:info progress:^(uint32_t progress) {
} succ:^{
} fail:^(int code, NSString *msg) {
}];
```

- Recipient: although Vinson's app is not online, it can still receive an APNs offline message notification. When Vinson clicks this notification, the app is started.
<pre><code><span class="hljs-comment">// Vinson receives the following callback after starting the app.</span>
<span class="hljs-selector-tag">-</span> (void)<span class="hljs-selector-tag">application</span><span class="hljs-selector-pseudo">:(UIApplication</span> *)<span class="hljs-selector-tag">application</span> <span class="hljs-selector-tag">didReceiveRemoteNotification</span><span class="hljs-selector-pseudo">:(NSDictionary</span> *)<span class="hljs-selector-tag">userInfo</span> 
<span class="hljs-selector-tag">fetchCompletionHandler</span><span class="hljs-selector-pseudo">:(void</span> (^)(UIBackgroundFetchResult result))<span class="hljs-selector-tag">completionHandler</span> {
    <span class="hljs-comment">// Parse `desc`, which is the extended field for online push.</span>
    <span class="hljs-selector-tag">if</span> ([userInfo[@<span class="hljs-string">"ext"</span>] <span class="hljs-attribute">isEqualToString</span>:@<span class="hljs-string">"jump to denny"</span>]) {
        <span class="hljs-comment">// Go to the chat window with Denny.</span>
    }
}</code></pre>

## Setting onlineUserOnly for Message Receiving Only When Users Are Online

In some scenarios, you may wish that sent messages can only be received by online users or that a recipient is not aware of the message when the recipient is offline. For this purpose, you can set 
Set `onlineUserOnly` to `YES` when calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a6ea32e6c119c1d771ee1123c5fb2dbae). After the setting, the sent messages differ from common messages in the following ways:
- Messages cannot be stored offline, which means the recipient cannot receive messages unless the recipient is online.
- Multi-device roaming of messages is unavailable. This means that messages received on one terminal (read or not) cannot be received on any other terminal.
- Messages cannot be stored locally. That is, these messages cannot be retrieved from the local historical messages in the cloud.

**Typical example: displaying "The other party is typing..."**
In the one-to-one chat scenario, you can call [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send the "I am typing..." message. When the recipient receives this message, "The other party is typing..." is displayed on the UI. The sample code is as follows:
```
// Send the "I am typing..." message to userA
NSString *customStr = @"{\"command\": \"textInput\"}";
NSData *customData = [customStr dataUsingEncoding:NSUTF8StringEncoding];
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createCustomMessage:customData];
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:YES offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // The message was successfully sent
} fail:^(int code, NSString *msg) {
    // The message failed to be sent
}];

```

## Setting "Mute Notifications" for Message Receiving
The SDK supports the following types of message receiving options:
- V2TIM_RECEIVE_MESSAGE: Messages will be received when the user is online, and offline push notifications will be received when the user is offline.
- V2TIM_NOT_RECEIVE_MESSAGE: Messages will not be received regardless of the online or offline status.
- V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE: Messages will be received when the user is online, and offline push notifications will not be received when the user is offline.

You can call the [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ace29641a1c691bc44705b9bc8b08be37) API to set the Mute Notifications option for one-to-one messages and call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a40f3e2ada605b73a39b05a3d3144636b) API to set the Mute Notifications option for group messages.

>! Only available in Enhanced Edition v5.3.425 or later.

## Recalling Messages
The sender can call the [revokeMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a972ac3fb7744458eb0d6abd96ce35126) API to recall a successfully sent message. By default, the sender can recall a message that is sent within 2 minutes. You can change the time limit for message recall. For detailed operations, see [Message recall settings](https://intl.cloud.tencent.com/document/product/1047/34419).
Message recall requires cooperation of the UI code at the recipient side. When the sender recalls a message, the recipient will receive a message recall notification, [onRecvMessageRevoked](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html). This notification contains the `msgID` of the recalled message. Based on this `msgID`, you can identify the message that has been recalled and change the corresponding message bubble to the "Message recalled" state on the UI.

### The sender recalls a message

```
[[V2TIMManager sharedInstance] revokeMessage:msg succ:^{
     // The message was successfully recalled
} fail:^(int code, NSString *msg) {
     // The message failed to be recalled
}];
```

### The recipient learns that the message is recalled
1. Call [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) to set the advanced message listener.
2. Call [onRecvMessageRevoked](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html) to receive the message recall notification.

```
- (void)onRecvMessageRevoked:(NSString *)msgID {
      // msgList is the message list on the current chat interface
      for(V2TIMMessage *msg in msgList){
         if ([msg.msgID isEqualToString:msgID]) {
             // `msg` is the recalled message. You need to change the corresponding message bubble state on the UI.
         }
     }
 }
```

## Marking Unread Messages as Read
### Marking unread messages in a conversation as read
The recipient can call [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ad7d239caa69ec7da45f52d6bb02ee19c) or [markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a40afaf1f06edd10c90d8d67fa98c2b14), respectively, to mark incoming messages in a C2C conversation or a group conversation as read, and perform callback of [onConversationChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#a371039feea8aa04047bd3ebcf8d12931) to notify the UI to update.
### Quickly marking unread messages of all conversations as read
The recipient can call [markAllMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ab9e190495505a6fe226c9c4ed10e4eeb) to quickly mark unread messages of all conversations as read, and perform callback of [onConversationChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#a371039feea8aa04047bd3ebcf8d12931) to notify the UI to update.

> Only available in Enhanced Edition v5.8.1668 or later.

## Viewing Historical Messages
You can call [getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a63d51af9d34e0cd8011da374b7e7a786) to obtain historical messages of one-to-one chats, or call [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acc79b07f0ac1b4b29b72878850ce4ad1) to obtain historical messages of group chats. If the network connection of the current device is normal, the IM SDK pulls historical messages from the server by default. If the network connection is unavailable, the IM SDK directly reads historical messages from the local database.

### Pulling historical messages by page
The IM SDK supports the feature of pulling historical messages by page. The number of messages pulled per page cannot be too large; otherwise, the pulling speed is affected. We recommend that you pull 20 messages per page.
The following example assumes that historical messages of `groupA` are pulled by page, and the number of messages per page is 20. The sample code is as follows:

```
// The value `nil` of `lastMsg` is passed in for the first pulling, indicating that starting from the latest message, a total of 20 messages are pulled
[[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 
lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Messages that are pulled by page are listed from new to old by default
    if (msgs.count > 0) {
        // Obtain the start message for the next pulling by page
        V2TIMMessage *lastMsg = msgs.lastObject;
        // Pull the remaining 20 messages
        [[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 
                lastMsg:lastMsg succ:^(NSArray<V2TIMMessage *> *msgs) {
            // Message pulling is completed
        } fail:^(int code, NSString *msg) {
            // Failed to pull the message
        }];
    }
} fail:^(int code, NSString *msg) {
    // Failed to pull the message
}];
```

In actual scenarios, pulling by page is often triggered by your swipe operation. Each time when you swipe on the message list, pulling by page is triggered once. However, the principle is similar to the preceding sample code. In either case, `lastMsg` specifies the start message for pulling, and `count` specifies the number of messages pulled each time.

### Precautions
- The storage period of historical messages is as follows:<ul style="margin:0;"><li>Trial edition: free storage for 7 days, no extension supported. </li><li>Pro edition: free storage for 7 days, extension supported. </li><li>Flagship edition: free storage for 30 days, extension supported. </li></ul>It is a value-added service to extend the storage period of historical messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. For information about billing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.
- Only the meeting group (corresponding to the ChatRoom of the earlier version) supports pulling historical messages of members **before they join the group**.
- Messages in an audio-video group (AVChatRoom) do not support local storage and multi-device roaming. Therefore, the [getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acc79b07f0ac1b4b29b72878850ce4ad1) API does not take effect on an audio-video group.

## Deleting Messages
You can call the [deleteMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a989a11c62ba2001a6a8360d6421d9dd3) API to delete historical messages. After deletion, historical messages cannot be recovered.

## Setting Message Permissions
### Allowing message sending and receiving only among friends
By default, the IM SDK does not prevent message sending and receiving among strangers. If you wish that one-to-one messages can be sent or received only among friends, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

### Not receiving messages from a specific user 
To avoid receiving messages from a specific user, you can blocklist the user or set the Mute Notifications option for messages from the user. After setting the Mute Notifications option, you can change the [Mute Notifications status](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ae4064d7096592f71587cc9f54ea3253e).
**Adding a user to the blocklist:**
Call the [addToBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ad1de7b4712309ce4164e4db6574486f0) API to add the user to the blocklist. When the user is blocklisted, the user does not know that he/she is in the blocklist by default. That is, after this user sends a message, the prompt still indicates that the message is sent successfully, but in fact the recipient will not receive the message. If you want a user on the blocklist to know that his/her message fails to be sent, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

**Setting "Mute Notifications" for messages from a specified user: **
Call the [setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a40f3e2ada605b73a39b05a3d3144636b) API to set the message receiving option to `V2TIM_NOT_RECEIVE_MESSAGE`.

>! Only available in Enhanced Edition v5.3.425 or later.

### Rejecting messages from a specified group
For Enhanced Edition v5.3.425 or later, call the [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a40f3e2ada605b73a39b05a3d3144636b) API to set the message receiving option to `V2TIM_NOT_RECEIVE_MESSAGE`.
For SDKs of other versions, call the `setReceiveMessageOpt` API to set the message receiving option to `V2TIM_GROUP_NOT_RECEIVE_MESSAGE`.


## FAQs
### 1. Why am I receiving duplicate messages?
- Check whether [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) is used together with [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab). If yes, when text or custom messages are received, both listeners trigger callback, and consequently duplicate messages are received.
- Check whether the same listener object is added repeatedly. If a listener object is no longer needed, call the corresponding [removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b) or [removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6) API to remove this listener.

### 2. Why do the read receipts become invalid after the app is uninstalled and then reinstalled?
In the one-to-one chat scenario, if the recipient calls [markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ad7d239caa69ec7da45f52d6bb02ee19c) to mark a message as read, the read receipt received by the sender contains `timestamp`. Based on `timestamp`, the SDK determines whether the other party reads the message. Currently, `timestamp` is stored locally, and will be lost when the app is reinstalled.

### 3. How can I send a message containing multiple `Elem`?
You can call [appendElem](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMElem.html#a632f3740c4c42014dc38a4c074a700c9) after creating a `Message` object via the `Elem` member of the `Message` object to add the next `Elem` member.
Below is an example of text message + custom message:

```
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"text"];
V2TIMCustomElem *customElem = [[V2TIMCustomElem alloc] init];
customElem.data = [@"custom message" dataUsingEncoding:NSUTF8StringEncoding];
[msg.textElem appendElem:customElem];
```
### 4. How can I parse a message containing multiple `Elem` objects?
1. Use the `Message` object to parse the first `Elem` object.
2. Use the [nextElem](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMElem.html) method of the first `Elem` object to obtain the next `Elem` object. If the next `Elem` object exists, the `Elem` object instance is returned. Otherwise, `nil` is returned.

```
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // View the first Elem object
    if (msg.elemType == V2TIM_ELEM_TYPE_TEXT) {
        V2TIMTextElem *textElem = msg.textElem;
        NSString *text = textElem.text;
        NSLog(@"Text information: %@", text);
        // Check whether `textElem` is followed by more `Elem` objects
        V2TIMElem *elem = textElem.nextElem;
        while (elem != nil) {
            // Identify the `Elem` type
            if ([elem isKindOfClass:[V2TIMCustomElem class]]) {
                V2TIMCustomElem *customElem = (V2TIMCustomElem *)elem;
                NSData *customData = customElem.data;
                NSLog(@"Custom information: %@",customData);
            }
            // Continue to check whether the current Elem is followed by more Elem objects
            elem = elem.nextElem;
        }
        // If `elem` is `nil`, all `Elem` objects have been parsed
    }
}
```

[](id:msgAnalyze)
### 5. How are different types of messages parsed?
It is complex to parse a message. We provide the [sample code](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/SampleCode/MessageParser.m) for parsing different types of messages. You can copy the code to your project, and perform secondary development based on your actual needs.

### 6. Why did sending the PNG images in an Xcode project fail?

When you use a PNG image in an Xcode project to create an image message and send it, a sending failure message will be displayed. The reason is that Xcode compresses the PNG images in projects and modifies the file headers by default, and as a result, the images cannot be identified by IM. To solve the problem, configure your Xcode project as shown in the following figure.

![Image](https://main.qcloudimg.com/raw/844287d24d27a08f22cdba7272c556d9.png)
