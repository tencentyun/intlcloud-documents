## Message Classification
IM messages are classified by message destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| C2C message | C2CMessage | When sending a C2C message, you must specify the UserID of the message recipient, and only the recipient can receive this message. |
| Group message | GroupMessage | When sending a group message, you must specify the groupID of the target group, and all users in this group can receive this message. |

IM messages can also be classified by content into text messages, custom (signaling) messages, image messages, video messages, voice messages, file messages, location messages, and group tips.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| Text message | TextElem | It refers to a common text message. Sensitive words in text messages will be filtered out in the IM service. If a message containing sensitive words is sent, the 80001 error code is returned. |
| Custom message | CustomElem | It is a section of the binary buffer, which is often used to transfer custom signaling in your app. Its content is not filtered for sensitive words. |
| Image message | ImageElem | When the IM SDK sends an original image, it automatically generates two thumbnails in different sizes. The three images are called the original image, large image, and thumbnail, respectively. |
| Video message | VideoElem | A video message contains a video file and a thumbnail. |
| Voice message | SoundElem | The feature of displaying a red dot upon playback of the voice message is supported. |
| File message | FileElem | The maximum size of a file message is 100 MB. |
| Location message | LocationElem | A location message contains three fields: location description, longitude, and latitude. |
| Group tip | GroupTipsElem | A group tip is often used to carry a system notification in a group, for example, a notification indicating that a member joins or quits the group, the group description is modified, or the profile of a group member is changed. |

## Sending and Receiving a Simple Message
[V2TIMManager.h](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html) provides a set of simple APIs for sending and receiving messages. Although these APIs can be used to send or receive text messages and custom (signaling) messages, they are easy to use and only a few minutes are needed to complete interfacing.

### Sending text and signaling messages (simplified APIs)
To send text messages, call [sendC2CTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618) or  [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7). Text messages will be filtered by IM for sensitive words. If a message containing sensitive words is sent, the 80001 error code is returned.
To send C2C custom (signaling) messages, call [sendC2CCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90) or [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65). A custom message is essentially a section of the binary buffer, and is often used to transfer custom signaling in your app. Its content is not filtered for sensitive words.

### Receiving text and signaling messages (simplified APIs)
To listen to simple text and signaling messages, call [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68). To listen to complex image, video, and voice messages, call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) defined in [V2TIMManager + Message.h](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html).

>! Do not use [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) together with [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a). Otherwise, logic bugs may occur.

### Typical example: sending and receiving on-screen comments in a livestreaming group
In the livestreaming scenario, it is a common way of communication to send or receive on-screen comments in a livestreaming group. This can be easily implemented through the simple message APIs.

1. The anchor can call [createGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) to create a livestreaming group (AVChatRoom) and record the group ID in the list of rooms in "Broadcasting" state.
2. A viewer can select an anchor that he/she likes, and call [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) to join the AVChatRoom created by this anchor.
3. The message sender can call [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7) to send a group text message as the on-screen comment.
4. The message recipient can call [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) to register a simple message listener, and use the listener callback function [onRecvGroupTextMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMSimpleMsgListener-p.html) to obtain text messages.

"FlyHeart" is an instruction. To configure the "FlyHeart" feature for an AVChatRoom, perform the steps below:
1. Define a custom message type, for example, a JSON string ` { "command": "favor", "value": 101 }`.
2. Call [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65) to send a message, and call [onRecvGroupCustomMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMSimpleMsgListener-p.html#ad01776119c059bff49b804c8152c70d9) to receive the message.

## Sending and Receiving Rich Media Messages
Image, video, voice, file, and location messages are called rich media messages. Compared with simple messages, it is more complex to send or receive rich media messages.
- Before sending a rich media message, use the `create` function to create a [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) object. Then, call the corresponding `send` API to send this message.
- When receiving the rich media message, check `elemType` and perform secondary parsing on `Elem` obtained based on `elemType`.


### Sending rich media messages
The following takes an image message as an example to describe the process of sending a rich media message.
1. The sender calls [createImageMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) to create an image message and obtain the [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) message object.
2. The sender calls [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) to send the previously created message object.

### Receiving rich media messages

1. The recipient calls [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) to set the advanced message listener.
2. The recipient obtains the [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) image message through the [onRecvNewMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) listener callback.
3. The recipient parses `elemType` in [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html, and performs secondary parsing based on the message type to obtain the content of `Elem` in the message.

### Typical example: sending and receiving image messages
The sender creates and sends an image message.
```
// Obtain the local image path.
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// Create an image message.
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
// Send the image message.
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil 
priority:V2TIM_PRIORITY_DEFAULT 
onlineUserOnly:NO offlinePushInfo:nil progress:^(uint32_t progress) {
   // Image upload progress (0-100)
} succ:^{
   // The image message is successfully sent.
} fail:^(int code, NSString *msg) {
   // The image message fails to be sent.
}];
```

The recipient identifies the image message, and parses the message to obtain the original image, large image, and thumbnail contained in the message.
```
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
  if (msg.elemType == V2TIM_ELEM_TYPE_IMAGE) {
    V2TIMImageElem *imageElem = msg.imageElem;
    // An image message contains an image in three different sizes: original image, large image, and thumbnail. (The SDK automatically generates the large image, and thumbnail.)
    - A large image is an image obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 720 pixels.
    - A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 198 pixels.
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
                // The image already exists.
        }
    }
  }
}
```

>? For more information on the message parsing sample code, see [FAQs > 5. How can I parse different types of messages](#msgAnalyze).

## Sending and Receiving Group @ Messages

For a group @ message, the sender can listen to the input of the @ character in the input bar and call the group member selection interface. After selection is completed, the format `"@A @B @C......"` is displayed in the input box, and then the sender can continue to edit the message content and send the message. On the group chat list of the recipient’s conversation interface, the identifier `"someone@me"` or `"@all members"` will be displayed to remind the user that the user was mentioned by someone in the group.

>? Currently, only text @ messages are supported.

### Sending group @ messages

1. The sender listens to the text input box on the chat interface and launches the group member selection interface. After selection is completed, the ID and nickname of the selected member are returned. The ID is used to construct the message object [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html), and the nickname is displayed in the text box.
2. The sender calls [createTextAtMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#aaebbd8ed9b9766d01f996ec722744346) of [V2TIMManager+Message](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html) to create an @ text message and obtain the message object [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html).
3. The sender calls [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) to send the previously created @ message object.

### Receiving group @ messages

1. During conversation loading and update, the [groupAtInfolist](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a5659c29a54304e89e61c25c2b073f8da) API of [V2TIMConversation](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html) needs to be called to obtain the @ data list of the conversation.
2. Through the [atType](http://doc.qcloudtrtc.com/im/interfaceV2TIMGroupAtInfo.html#a1486d853fd6f8ae074714ec8059f7621) API of the [V2TIMGroupAtInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMGroupAtInfo.html) object on the list, the @ data type is obtained and updated to the @ information of the current conversation.

### Typical examples: sending and receiving group @ messages

- **Sending a group @ message:**
The sender creates a group @ message and sends it:

```objective-c
// Obtain the ID data of the @ group member.
TUITextMessageCellData *text = (TUITextMessageCellData *)data;
NSMutableArray<NSString *> *atUserList = text.atUserList;

// Create a group @ message.
V2TIMMessage *atMsg = [[V2TIMManager sharedInstance] createTextAtMessage:text.content atUserList:atUserList];

// Send the group @ message.
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
// Obtain the group @ data list.
NSArray<V2TIMGroupAtInfo *> *atInfoList = conversation.groupAtInfolist;

// Parse the @ type (@me, @all members, @me, and @all members).
BOOL atMe = NO;         // Whether it’s @me
BOOL atAll = NO;        // Whether it’s @all members
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


## Setting APNs Offline Push (offlinePushInfo)

When the recipient's app is killed or when the recipient switches to the backend, the IM SDK cannot receive new messages through the normal network connection. In this scenario, the APNs service provided by Apple must be used to notify the recipient of new messages. For more information, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).

### Setting the title and voice for APNs Offline Push
When sending messages, you can use the **offlinePushInfo** field in the [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) API to set the title and voice for APNs offline push.

```
// Create and send an image message to groupA, and customize the title and voice for offline push.
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// Create an image message.
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
// Customize the title and voice for offline push. `01.caf` is a sample file, which must be linked to the Xcode project. Here, you only need to enter the file name with the extension.
pushInfo.title = @"Customize the title displayed";
pushInfo.iOSSound = @"01.caf";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:nil groupID:@"groupA" priority:V2TIM_PRIORITY_DEFAULT 
onlineUserOnly:NO offlinePushInfo:pushInfo progress:^(uint32_t progress) {
} succ:^{
    // The message is sent successfully.
} fail:^(int code, NSString *msg) {
    // The message failed to be sent.
}];
```

### Clicking a pushed message to go to the corresponding chat window
To implement this feature, the sender needs to set `ext`, which is the extended field of the offline push object `offlinePushInfo`, when sending a message. When the recipient opens the app, the recipient can obtain `ext` through the `didReceiveRemoteNotification` system callback, and then go to the corresponding chat window based on the content of `ext`.

The following example assumes that Denny sends a message to Vinson.
- Sender: Denny needs to set `ext` before sending a message.
```
// Denny sets `offlinePushInfo` and specifies `ext` before sending a message.
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"Text message"];
V2TIMOfflinePushInfo *info = [[V2TIMOfflinePushInfo alloc] init];
info.ext = @"jump to denny";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"vinson" groupID:nil priority:V2TIM_PRIORITY_DEFAULT
onlineUserOnly:NO offlinePushInfo:info progress:^(uint32_t progress) {
} succ:^{
} fail:^(int code, NSString *msg) {
}];
```

Recipient: although Vinson's app is not online, it can still receive an APNs offline message notification. When Vinson clicks this notification, the app is started.
<pre><code><span class="hljs-comment">// Vinson receives the following callback after starting the app.</span>
<span class="hljs-selector-tag">-</span> (void)<span class="hljs-selector-tag">application</span><span class="hljs-selector-pseudo">:(UIApplication</span> *)<span class="hljs-selector-tag">application</span> <span class="hljs-selector-tag">didReceiveRemoteNotification</span><span class="hljs-selector-pseudo">:(NSDictionary</span> *)<span class="hljs-selector-tag">userInfo</span> 
<span class="hljs-selector-tag">fetchCompletionHandler</span><span class="hljs-selector-pseudo">:(void</span> (^)(UIBackgroundFetchResult result))<span class="hljs-selector-tag">completionHandler</span> {
    <span class="hljs-comment">// Parse `desc`, which is the extended field for online push.</span>
    <span class="hljs-selector-tag">if</span> ([userInfo[@<span class="hljs-string">"ext"</span>] <span class="hljs-attribute">isEqualToString</span>:@<span class="hljs-string">"jump to denny"</span>]) {
        <span class="hljs-comment">// Go to the chat window with Denny.</span>
    }
}</code></pre>

## Setting onlineUserOnly so that Messages Can Be Received Only Online

In some scenarios, you may wish that sent messages can only be received by online users, that is, a recipient is not aware of the message when the recipient is offline. For this purpose, you can set 
`onlineUserOnly` to `YES` when calling [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a6ea32e6c119c1d771ee1123c5fb2dbae). After the setting, the sent messages differ from common messages in the following ways:
- Messages cannot be stored offline. That is, the recipient cannot receive messages unless he/she is online.
- Messages do not support multi-device roaming. That is, if the recipient has received messages on one terminal, these messages cannot be received on any other terminal no matter whether these messages are read or not.
- Messages cannot be stored locally. That is, these messages cannot be retrieved from the local history messages in the cloud.

**Typical example: displaying "The other party is typing...**
In the one-to-one chat scenario, you can call [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) to send the "I am typing..." message. When the recipient receives this message, "The other party is typing..." is displayed on the UI. The sample code is as follows:
```
// Sending the "I am typing..." message to userA.
NSString *customStr = @"{\"command\": \"textInput\"}";
NSData *customData = [customStr dataUsingEncoding:NSUTF8StringEncoding];
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createCustomMessage:customData];
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:YES offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // The message is sent successfully.
} fail:^(int code, NSString *msg) {
    // The message failed to be sent.
}];

```

## Recalling Messages
The sender can call the [revokeMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a) API to recall a successfully sent message. By default, the sender can recall a message that is sent within 2 minutes. You can change the time limit for message recall. For detailed operations, see [Message recall settings](https://intl.cloud.tencent.com/document/product/1047/34419)。
Message recall requires cooperation of the UI code at the recipient side. When the sender recalls a message, the recipient will receive a message recall notification, [onRecvMessageRevoked](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html). This notification contains the `msgID` of the recalled message. Based on this `msgID`, you can identify the message that has been recalled and change the corresponding message bubble to the "Message recalled" state on the UI.

### The sender recalls a message

```
[[V2TIMManager sharedInstance] revokeMessage:msg succ:^{
     // The message is successfully recalled.
} fail:^(int code, NSString *msg) {
     // The message fails to be recalled.
}];
```

### The recipient learns that the message is recalled
1. Call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) to set the advanced message listener.
2. Call [onRecvMessageRevoked](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) to receive the message recall notification.

```
- (void)onRecvMessageRevoked:(NSString *)msgID {
      // `msgList` is the message list on the current chat window.
      for(V2TIMMessage *msg in msgList){
         if ([msg.msgID isEqualToString:msgID]) {
             // `msg` is the recalled message. You need to change the corresponding message bubble state on the UI.
         }
     }
 }
```

## Adding Read Receipts for Messages
In the one-to-one chat scenario, when the recipient calls the [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) API to mark an incoming message as read, the message sender will receive a read receipt, indicating that the recipient has read his/her message.

>! Currently, only one-to-one chats support the read receipt feature, and group chats do not support this feature. Although the [markGroupMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) API is also available in group chats, the group message senders currently cannot receive any read receipts.

### The recipient marks messages as read

```
// Mark messages coming from Haven as read.
[[V2TIMManager sharedInstance] markC2CMessageAsRead:@"haven" succ:^{
} fail:^(int code, NSString *msg) {
}];
```

### The sender learns that the messages are read
The event notification of the message receipt is located in the advanced message listener [V2TIMAdvancedMsgListener](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html). To learn that a message is already read, the sender must call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) to set the listener. Then, the sender can receive a read receipt from the recipient through the [onRecvC2CReadReceipt](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) callback.

```
- (void)onRecvC2CReadReceipt:(NSArray<V2TIMMessageReceipt *> *)receiptList {
      // The sender may receive multiple read receipts at a time. Therefore, the array callback mode is used here.
      for (V2TIMMessageReceipt *receipt in receiptList) {
          // Message receiver
          NSString * receiver = receipt.userID;
          // Time of the read receipt. A message is considered as read if the timestamp in the chat window is not later than `timestamp` here.
          time_t timestamp = receipt.timestamp;
      }
}
@end
```

## Viewing History Messages
You can call [getC2CHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e) to obtain history messages of one-to-one chats, or call [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) to obtain history messages of group chats. If the network connection of the current device is normal, the IM SDK pulls history messages from the server by default. If the network connection is unavailable, the IM SDK directly reads history messages from the local database.

### Pulling history messages by page
The IM SDK supports the feature of pulling history messages by page. The number of messages pulled per page cannot be too large; otherwise, the pulling speed is affected. We recommend that you pull 20 messages per page.
The following example assumes that history messages of `groupA` are pulled by page, and the number of messages per page is 20. The sample code is as follows:

```
// The value `nil` of `lastMsg` is passed in for the first pulling, indicating that starting from the latest message, a total of 20 messages are pulled.
[[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 
lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Messages that are pulled by page are listed from new to old by default.
    if (msgs.count > 0) {
        // Obtain the start message for the next pulling by page.
        V2TIMMessage *lastMsg = msgs.lastObject;
	    // Pull the remaining 20 messages.
        [[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 
				lastMsg:lastMsg succ:^(NSArray<V2TIMMessage *> *msgs) {
            // Message pulling is completed.
        } fail:^(int code, NSString *msg) {
            // Messages fail to be pulled.
        }];
    }
} fail:^(int code, NSString *msg) {
    // Messages fail to be pulled.
}];
```

In actual scenarios, pulling by page is often triggered by your swipe operation. Each time when you swipe on the message list, pulling by page is triggered once. However, the principle is similar to the preceding sample code. In either case, `lastMsg` specifies the start message for pulling, and `count` specifies the number of messages pulled each time.

### Precautions
- The storage period of history messages is as follows:<ul style="margin:0;"><li>Trial edition: free storage for 7 days, no extension supported. </li><li>Pro edition: free storage for 7 days, extension supported. </li><li>Flagship edition: free storage for 30 days, extension supported.</li></ul>It is a value-added service to extend the storage period of history messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. For more information about billing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.
- Only the meeting group (corresponding to the ChatRoom of the earlier version) supports pulling history messages of members **before members join the group**.
- Messages in the AVChatRoom do not support local storage and multi-device roaming. Therefore, the [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) API does not take effect on an AVChatRoom.

## Deleting Messages
You can call the [deleteMessages](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e394ea720ecdc10d497b63b6f2b22c4) API to delete historical messages. After deletion, historical messages cannot be recovered.

## Setting Message Permissions
### Allowing message sending and receiving only among friends
By default, the IM SDK does not prevent message sending and receiving among strangers. If you wish that C2C messages can be sent or received only among friends, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

### Blocking messages from a specified user
If you want to block messages from a specified user, call the [addToBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) API to add this user to the blocklist.
When a user is added to the blocklist, the user does not know that he/she is in the blocklist by default. That is, after this user sends a message, the prompt still indicates that the message is sent successfully, but in fact the recipient will not receive the message. If you want a user in the blocklist to know that his/her message fails to be sent, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

### Blocking messages from a specified group
To block messages from a specified group, you can call the [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4974b44d56778b1d5a3df613bee09c87) API to set the group message receiving option to the `V2TIM_GROUP_NOT_RECEIVE_MESSAGE` state.

## Filtering Sensitive Words
Text messages sent by the IM SDK are filtered by IM for sensitive words. If a sent text message contains sensitive words, the IM SDK will return the 80001 error code.


## FAQs
### 1. Why am I receiving duplicate messages?
- Check whether [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) is used together with [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a). If yes, when text or custom messages are received, both listeners trigger callback, and consequently duplicate messages are received.
- Check whether the same listener object is added repeatedly. If a listener object is no longer needed, call the corresponding [removeSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a8f6f9900006bf7ad5bd9bdb8ba0914eb) or [removeAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a77ec89edbdf500431cbda5ee7aa50920) API to remove this listener.

### 2. Why do the read receipts become invalid after the app is uninstalled and then reinstalled?
In the one-to-one chat scenario, if the recipient calls [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) to mark a message as read, the read receipt received by the sender contains `timestamp`. Based on `timestamp`, the SDK determines whether the other party reads the message. Currently, `timestamp` is stored locally, and will be lost when the app is reinstalled.

### 3. How is a message containing multiple `Elem` objects parsed?
To reduce the message complexity, the SDK API 2.0 no longer supports creation of a message containing multiple `Elem` objects. If you receive a message containing multiple `Elem` objects from the API of an earlier version, perform the steps below:
1. Parse the first `Elem` object as usual.
2. Use the [nextElem](http://doc.qcloudtrtc.com/im/interfaceV2TIMElem.html) method of the first `Elem` object to obtain the next `Elem` object. If the next `Elem` object exists, the `Elem` object instance is returned. Otherwise, `nil` is returned.

```
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // View the first `Elem` object.
    if (msg.elemType == V2TIM_ELEM_TYPE_TEXT) {
        V2TIMTextElem *textElem = msg.textElem;
        NSString *text = textElem.text;
        NSLog(@"Text information: %@", text);
        // Check whether `textElem` is followed by more `Elem` objects.
        V2TIMElem *elem = textElem.nextElem;
        while (elem != nil) {
            // Identify the Elem type.
            if ([elem isKindOfClass:[V2TIMCustomElem class]]) {
                V2TIMCustomElem *customElem = (V2TIMCustomElem *)elem;
                NSData *customData = customElem.data;
                NSLog(@"Custom information: %@",customData);
            }
            // Continue to check whether current `Elem` is followed by more `Elem` objects.
            elem = elem.nextElem;
        }
        // If `elem` is `nil`, all `Elem` objects have been parsed.
    }
}
```

<span id ="msgAnalyze"></span>
### 4. How are different types of messages parsed?
It is complex to parse a message. We provide the [sample code](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKitDemo/TUIKitDemo/SampleCode/message.m) for parsing different types of messages. You can copy the code to your project, and perform secondary development based on your actual needs.

