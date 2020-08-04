## Message Classification
IM messages are classified by destination into two types: one-to-one messages (also called C2C messages) and group messages.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| C2C message | C2CMessage | When sending a C2C message, you must specify the UserID of the message recipient, and only the recipient can receive this message. |
| Group message | GroupMessage | When sending a group message, you must specify the groupID of the target group, and all users in this group can receive this message. |

IM messages can also be classified by content into text messages, custom (signaling) messages, image messages, video messages, voice messages, file messages, location messages, and group tips.

| Message Type | API Keyword | Description |
|---------|---------|---------|
| Text message | TextMessage | This is a common text message. Sensitive words in text messages will be filtered out by the IM service. If a message containing sensitive words is sent, the 80001 error code is returned. |
| Custom message | CustomMessage | This is a section of the binary buffer, which is often used to transfer custom signaling in your app. Its content is not filtered for sensitive words. |
| Image message | ImageElem | When the IM SDK sends an original image, it automatically generates two smaller images of different sizes. The three images are called the original image, large image, and thumbnail. |
| Video message | VideoElem | A video message contains a video file and a thumbnail. |
| Voice message | SoundElem | Voice messages can display a red dot upon playback. |
| File message | FileElem | The maximum size of a file message is 100 MB. |
| Location message | LocationElem | A location message contains three fields: location description, longitude, and latitude. |
| Group tip | GroupTipsElem | A group tip is often used to carry a system notification for a group, such as a notification indicating that a member has joined or quit the group, the group description has been modified, or the profile of a group member has been changed. |

## Sending and Receiving a Simple Message
[V2TIMManager.h](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html) provides a set of simple APIs for sending and receiving messages. Although these APIs can be used to send or receive text messages and custom (signaling) messages, they are easy to use and only a few minutes are needed to configure access.

### Sending text and signaling messages (simplified APIs)
To send text messages, call [sendC2CTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618) or [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7). Text messages will be filtered by IM for sensitive words. If a message containing sensitive words is sent, the 80001 error code is returned.
To send C2C custom (signaling) messages, call [sendC2CCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90) or [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65). A custom message is essentially a section of the binary buffer, which is often used to transfer custom signaling in your app. Its content is not filtered for sensitive words.

### Receiving text and signaling messages (simplified APIs)
To listen to simple text and signaling messages, call [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68). To listen to complex image, video, and voice messages, call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) defined in [V2TIMManager + Message.h](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html).

> Do not use [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) together with [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) as this may produce logic bugs.

### Typical example: sending and receiving on-screen comments in a livestreaming group
In the livestreaming scenario, a common way of communicating is to send and receive on-screen comments in a livestreaming group. This can be easily implemented through the simple message APIs.

1. The anchor can call [createGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) to create a livestreaming group (AVChatRoom) and record the group ID in the list of rooms in "Broadcasting" state.
2. A viewer can select an anchor that he/she likes and call [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) to join the AVChatRoom created by this anchor.
3. The message sender can call [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7) to send a group text message as an on-screen comment.
4. The message recipient can call [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) to register a simple message listener and use the listener callback function [onRecvGroupTextMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMSimpleMsgListener-p.html) to obtain text messages.

"FlyHeart" is an instruction. To configure the "FlyHeart" floating heart feature for an AVChatRoom, perform the steps below:
1. Define a custom message type, for example, a JSON string ` { "command": "favor", "value": 101 }`.
2. Call [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65) to send a message and call [onRecvGroupCustomMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMSimpleMsgListener-p.html#ad01776119c059bff49b804c8152c70d9) to receive the message.

## Sending and Receiving Rich Media Messages
Image, video, voice, file, and location messages are called rich media messages. Compared with simple messages, it is more complex to send or receive rich media messages.
- Before sending a rich media message, use the `create` function to create a [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) object. Then, call the corresponding `send` API to send this message.
- When receiving the rich media message, check `elemType` and perform secondary parsing on the `Elem` obtained based on `elemType`.


### Sending Rich Media Messages
The following takes an image message as an example to describe the process of sending a rich media message.
1. The sender calls [createImageMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) to create an image message and obtain the [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) message object.
2. The sender calls [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) to send the previously created message object.

### Receiving Rich Media Messages

1. The recipient calls [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) to set the advanced message listener.
2. The recipient obtains the [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) image message through the [onRecvNewMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) listener callback.
3. The recipient parses `elemType` in [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) and performs secondary parsing based on the message type to obtain the content of `Elem` in the message.

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
   // The image message failed to be sent.
}];
```

The recipient identifies the image message and parses the message to obtain the original image, large image, and thumbnail contained in the message.
```
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
  if (msg.elemType == V2TIM_ELEM_TYPE_IMAGE) {
    V2TIMImageElem *imageElem = msg.imageElem;
    // An image message contains an image in three different sizes: original image, large image, and thumbnail. (The SDK automatically generates the large image and thumbnail.)
    - A large image is an image obtained after the original image is proportionally compressed. After the compression, the compressed image has a height and width equal to 720 pixels.
    - A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the compressed image has a height and width equal to 198 pixels.
    NSArray<V2TIMImage *> *imageList = imageElem.imageList;
    for (V2TIMImage *timImage in imageList) {
        NSString *uuid = timImage.uuid; // Image ID
        V2TIMImageType type = timImage.type; // Image type
        int size = timImage.size; // Image size (bytes)
        int width = timImage.width; // Image width
        int height = timImage.height; // Image height
        // Set the image download path `imagePath`. Here, `uuid` can be used as an identifier to avoid repeated downloads.
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

> For more information on the message parsing sample code, see [FAQs -> 5. How can I parse different types of messages?](#msgAnalyze).

## Setting APNs Offline Push (offlinePushInfo)

When the recipient's app is killed or when the recipient switches to the backend, the IM SDK cannot receive new messages through the normal network connection. In this scenario, the APNs service provided by Apple must be used to notify the recipient of new messages. For more information, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).

### Setting the title and sound for APNs Offline Push
When sending messages, you can use the **offlinePushInfo** field in the [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) API to set the title and sound for APNs offline push.

```
// Create and send an image message to groupA, and customize the title and sound for offline push.
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// Create an image message.
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
// Customize the title and sound for offline push. `01.caf` is a sample file, which must be linked to the Xcode project. Here, you only need to enter the file name with the extension.
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

In some scenarios, you may wish that sent messages can only be received by online users. In this case, recipients are not aware of the message when they are offline. For this purpose, you can set
`onlineUserOnly` to `YES` when calling [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a6ea32e6c119c1d771ee1123c5fb2dbae). After this parameter value is set, the sent messages differ from common messages in the following ways:
- Messages cannot be stored offline. That is, the recipient cannot receive messages unless he/she is online.
- Messages do not support multi-device roaming. That is, if the recipient has received a message on one terminal, this message cannot be received on any other terminal no matter whether it has been read or not.
- Messages cannot be stored locally. That is, these messages cannot be retrieved from historical messages that are stored locally or in cloud.

** Typical example: displaying "The other party is typing..."
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
The sender can call the [revokeMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a) API to recall a successfully sent message. By default, the sender can recall a message that has been sent within 2 minutes. You can change the time limit for message recall. For specific instructions, see [Message recall settings](https://intl.cloud.tencent.com/document/product/1047/34419).
Message recall requires the support of the UI code at the recipient side. When the sender recalls a message, the recipient will receive a message recall notification, [onRecvMessageRevoked](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html). This notification contains the `msgID` of the recalled message. Based on this `msgID`, you can identify the message that has been recalled and change the corresponding message bubble to the "Message recalled" state on the UI.

### The sender recalls a message

```
[[V2TIMManager sharedInstance] revokeMessage:msg succ:^{
     // The message is successfully recalled.
} fail:^(int code, NSString *msg) {
     // The message failed to be recalled.
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

> Currently, only C2C messages support the read receipt feature, and group messages do not support this feature. Although the [markGroupMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) API is also available to group messages, the group message senders currently cannot receive any read receipts.

### The recipient marks messages as read

```
// Mark messages coming from Haven as read.
[[V2TIMManager sharedInstance] markC2CMessageAsRead:@"haven" succ:^{
} fail:^(int code, NSString *msg) {
}];
```

### The sender learns that the messages are read
The event notification of message read receipts is located in the advanced message listener [V2TIMAdvancedMsgListener](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html). To enable the sender to learn that a message has been read, call [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) to set the listener. Then, the sender can receive a read receipt from the recipient through the [onRecvC2CReadReceipt](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) callback.

```
- (void)onRecvC2CReadReceipt:(NSArray<V2TIMMessageReceipt *> *)receiptList {
      // The recipient may receive multiple read receipts at a time. Therefore, the array callback mode is used here.
      for (V2TIMMessageReceipt *receipt in receiptList) {
          // Message recipient
          NSString * receiver = receipt.userID;
          // Time of the read receipt. A message is considered as read if the timestamp in the chat window is not later than `timestamp` here.
          time_t timestamp = receipt.timestamp;
      }
}
@end
```

## Viewing Historical Messages
You can call [getC2CHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e) to obtain historical messages of one-to-one chats, or call [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) to obtain historical messages of group chats. If the network connection of the current device is normal, the IM SDK pulls historical messages from the server by default. If the network connection is unavailable, the IM SDK directly reads historical messages from the local database.

### Pulling historical messages by page
The IM SDK supports pulling historical messages by page. The number of messages pulled per page cannot be too large. Otherwise, the pulling speed will be slow. We recommend that you pull 20 messages per page.
The following example assumes that the historical messages of `groupA` are pulled by page, and the number of messages per page is 20. The sample code is as follows:

```
// The value `nil` of `lastMsg` is passed in for the first pull, indicating that a total of 20 messages are pulled starting from the most recent message
[[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20
lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Messages pulled by page are listed from new to old by default.
    if (msgs.count > 0) {
        // Obtain the start message for the next pull by page.
        V2TIMMessage *lastMsg = msgs.lastObject;
    // Pull the remaining 20 messages.
        [[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20
lastMsg:lastMsg succ:^(NSArray<V2TIMMessage *> *msgs) {
            // Message pulling is completed.
        } fail:^(int code, NSString *msg) {
            // Messages failed to be pulled.
        }];
    }
} fail:^(int code, NSString *msg) {
    // Messages failed to be pulled.
}];
```

In actual scenarios, pulling by page is often triggered when the user swipes the interface. Each time the user swipes the message list, pulling by page is triggered once. However, the principle is similar to the preceding sample code. In either case, `lastMsg` specifies the start message for pulling, and `count` specifies the number of messages pulled each time.

### Precautions
- The storage period of historical messages is as follows:<ul style="margin:0;"><li>Trial edition: free storage for 7 days, no extension supported. </li><li>Pro edition: free storage for 7 days, extension supported.</li><li>Flagship edition: free storage for 30 days, extension supported.</li></ul>Extending the storage period of historical messages is a value-added service. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. For more information about billing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.
- Only the meeting group (corresponding to the ChatRoom of the earlier version) supports pulling the historical messages of members **before members join the group**.
- Messages in the AVChatRoom do not support local storage and multi-device roaming. Therefore, the [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) API does not work for AVChatRooms.

## Deleting Messages
You can call the [deleteMessageFromLocalStorage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c) API to delete received messages locally.

### Deleting local messages

```
[[V2TIMManager sharedInstance] deleteMessageFromLocalStorage:msg succ:^{
      // Messages are deleted successfully.
} fail:^(int code, NSString *msg) {
     // Messages failed to be deleted.
}];
```

> Why are the deleted messages pulled again after the app is uninstalled and then reinstalled?
> Currently, IM supports the deletion of local messages only. When the app is reinstalled, as messages still exist in the cloud, historical messages deleted locally can still be pulled from the cloud.

### Deleting messages in the cloud
Currently, IM does not support the deletion of messages in the cloud. If messages in the cloud are deleted, a reverse mapping relationship will be set up in the cloud, affecting the overall performance of the system.


## Setting Message Permissions
### Allowing message sending and receiving only among friends
By default, the IM SDK does not prevent message sending and receiving among strangers. If you want C2C messages to be sent and received only among friends, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** -> **Login and Messages** -> **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

### Blocking messages from a specified user
If you want to block messages from a specified user, call the [addToBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) API to add this user to the blocklist.
When a user is added to the blocklist, by default, the user does not know that he/she is in the blocklist. That is, after this user sends a message, the prompt still indicates that the message was sent successfully, but in fact, the recipient will not receive the message. If you want a user in the blocklist to know that his/her message failed to be sent, you can log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** -> **Login and Messages** -> **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

### Blocking messages from a specified group
To block messages from a specified group, you can call the [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4974b44d56778b1d5a3df613bee09c87) API to set the group message receiving option to the `V2TIM_GROUP_NOT_RECEIVE_MESSAGE` state.

## Filtering Sensitive Words
Text messages sent by the IM SDK are filtered by IM for sensitive words. If a sent text message contains sensitive words, the IM SDK will return the 80001 error code.

## FAQs
### 1. Why am I receiving duplicate messages?
- Check whether [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) is used together with [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a). If yes, when text or custom messages are received, both listeners trigger callback, so duplicate messages are received.
- Check whether the same listener object is added repeatedly. If a listener object is no longer needed, call the corresponding [removeSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a8f6f9900006bf7ad5bd9bdb8ba0914eb) or [removeAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a77ec89edbdf500431cbda5ee7aa50920) API to remove this listener.

### 2. Why are deleted messages pulled again after the app is uninstalled and then reinstalled?
Currently, IM supports the deletion of local messages only. When the app is reinstalled, as messages still exist in the cloud, historical messages deleted locally can still be pulled from the cloud.

### 3. Why do read receipts become invalid after the app is uninstalled and then reinstalled?
In the one-to-one chat scenario, if the recipient calls [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) to mark a message as read, the read receipt received by the sender contains `timestamp`. Based on `timestamp`, the SDK determines whether the other party has read the message. Currently, `timestamp` is stored locally, and will be lost when the app is reinstalled.

### 4. How is a message containing multiple `Elem` objects parsed?
To reduce the message complexity, 2.0 version APIs no longer support the creation of messages containing multiple `Elem` objects. If you receive a message containing multiple `Elem` objects from an earlier version API, perform the steps below:
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
            // Continue to check whether the current `Elem` is followed by more `Elem` objects.
            elem = elem.nextElem;
        }
        // If `elem` is `nil`, all `Elem` objects have been parsed.
    }
}
```

<span id ="msgAnalyze"></span>
### 5. How are different types of messages parsed?
Message parsing is a complex process. We provide [sample code](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKitDemo/TUIKitDemo/SampleCode/message.m) for parsing different types of messages. You can copy the code to your project and perform secondary development based on your actual needs.
