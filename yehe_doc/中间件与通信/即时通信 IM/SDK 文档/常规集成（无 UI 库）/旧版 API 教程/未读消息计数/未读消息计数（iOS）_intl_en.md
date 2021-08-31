## Unread Messages

**Unread messages** are messages that have not been read by users. This does not indicate whether the recipient has read the message. The `isReaded` method of `TIMMessage` identifies whether or not the messages are read. To show the correct unread count, developers need to explicitly call read reports to tell the app whether a message is read. For example, you can set the configuration so that all messages are read when the user enters the chat interface. For chat rooms, the server does not save the unread count. The unread count becomes zero after login and the unread count is synced with the server.

```
@interface TIMMessage : NSObject
/**
 *  Read or unread
 *
 *  @return TRUE: read. FALSE: unread.
 */
- (BOOL)isReaded;
@end
```

## Getting the Current Unread Count

The unread count of the current conversation can be obtained through the `getUnReadMessageNum` method of `TIMConversation`. For chat rooms, the server does not save the unread count. The unread count becomes zero after login and the unread count is synced with the server.

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

When the user reads messages in a conversation, a read report is sent, and the IM SDK sets all messages before the last read message as read. 

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Configure read messages.
 *
 *  @param readed The most recent read message in the conversation. Nil indicates reporting the latest messages.
 *
 *  @param succ  The success callback.
 *  @param fail  The failure callback.
 *
 *  @return 0  Successful
 */
- (int)setReadMessage:(TIMMessage*)readed succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
readed | The last read message in the conversation. The IM SDK marks messages earlier than the last read message as read.
succ | The success callback
fail | The failure callback

The following example sets all messages in a C2C (one-to-one) conversation as read. 
**Example:**

```
TIMConversation * conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS_002"];
[conversation setReadMessage:nil succ:nil fail:nil];
```



## Disabling Auto Reports

In the event of single-client login, the default setting is sufficient. For better performance, the IM SDK pulls unread messages to local storage, and the server deletes the unread messages by default. Unread messages pulled on a previous client are invisible to clients switched to later. For a single client, the unread count is correct. If you want unread messages to appear on multiple clients, you can disable auto reports **before initializing TIMManager**. IM does not perform read reports for users. **After auto reports is disabled, developers need to explicitly call `setReadMessage`**.

```
@interface TIMUserConfig: NSObject
/**
 *  Disable auto reports (effective for loaded message extension package).
 */
@property(nonatomic,assign) BOOL disableAutoReport;
@end
```

## Multi-client Read Synchronization

This feature is introduced on 2.0 and later versions. In the event of multi-client login, unread count synchronization notifications are delivered by the server. The IM SDK updates the unread count locally and tells the user to update conversations. This feature must be set before **TIMManager login**.

**Prototype:**

```
@protocol TIMRefreshListener <NSObject>
@optional
/**
 *  Refresh some conversations, including multi-client read reports synchronization.
 *
 *  @param conversations The Conversation (TIMConversation*) list.
 */
- (void)onRefreshConversations:(NSArray*)conversations;
@end
@interface TIMUserConfig : NSObject
/**
 **  The conversation refresh listener for unread count and read synchronization (effective for loaded message extension package).
 */
@property(nonatomic,retain) id<TIMRefreshListener> refreshListener;
@end
```

