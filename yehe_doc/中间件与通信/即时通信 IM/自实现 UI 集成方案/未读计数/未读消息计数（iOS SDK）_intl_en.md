## Unread Messages

**Unread messages** are messages that have not been read by users. This does not indicate whether the recipient has actually read the messages. The `isReaded` method of `TIMMessage` identifies whether messages are read or not. To display the correct unread count, developers need to explicitly call read reports to notify the app whether a message is read. For example, you can mark all messages as read when the user enters the chat UI. For ChatRoom groups, the server does not save the unread count. The unread count becomes zero after login is completed and being synced with the server.

```
@interface TIMMessage : NSObject
/**
 *  Read or unread
 *
 *  @return TRUE: read, FALSE: unread
 */
- (BOOL)isReaded;
@end
```

## Obtaining the Current Unread Count

The unread count of the current conversation can be obtained through the `getUnReadMessageNum` method of `TIMConversation`. For ChatRoom groups, the server does not save the unread count. The unread count becomes zero after login is completed and being synced with the server.

**Prototype:**

```
@interface TIMConversation : NSObject
- (int)getUnReadMessageNum;
@end
```

**Example:**

```
TIMConversation * conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS_002"];
[conversation getUnReadMessageNum]; 
```

## Read Reports 

When the user reads a message in a conversation, a read report is sent, and the IM SDK sets all messages before the last read message as read. 

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Configure read messages
 *
 *  @param readed Indicates the last read message in the conversation. Nil indicates reporting the latest messages.
 *
 * @param succ Callback upon success
 @param fail Callback upon failure
 *
 *  @return 0 Indicate success
 */
- (int)setReadMessage:(TIMMessage*)readed succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
readed | The last read message in the conversation. The IM SDK marks messages earlier than the last read message as read.
succ | The callback upon success.
fail | The callback upon failure.

The following example sets all messages in C2C (one-to-one chat) conversations as read. **Example:**

```
TIMConversation * conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS_002"];
[conversation setReadMessage:nil succ:nil fail:nil];
```



## Disabling Auto Reporting

In the event of single-client login, the default setting is sufficient. For better performance, the IM SDK pulls unread messages to local storage, and the server deletes the unread messages by default. Unread messages that were pulled on a previous client are invisible to clients to be switched to later. For a single client, the unread count is correct. If you want unread messages to appear on multiple clients, you can disable auto reporting **before initializing TIMManager**. IM does not perform read reporting for users. **After auto reporting is disabled, developers need to explicitly call `setReadMessage`**.

```
@interface TIMUserConfig: NSObject
/**
 * Disable auto reporting (valid for the extension package for loaded messages)
 */
@property(nonatomic,assign) BOOL disableAutoReport;
@end
```

## Multi-Client Read Synchronization

This feature is introduced to version 2.0 and later. In the event of multi-client login, unread count synchronization notifications are delivered by the server. The IM SDK updates the unread count locally and notifies the user to update conversations. This feature must be set before **TIMManager login**.

**Prototype:**

```
@protocol TIMRefreshListener <NSObject>
@optional
/**
 *  Refresh some conversations, including synchronizing multi-client read reports
 *
 *  @param conversations Conversation (TIMConversation*) list
 */
- (void)onRefreshConversations:(NSArray*)conversations;
@end
@interface TIMUserConfig : NSObject
/**
 **  Conversation refreshment listener (for the unread count and read synchronization) (valid for the extension package for loaded messages)
 */
@property(nonatomic,retain) id<TIMRefreshListener> refreshListener;
@end
```

