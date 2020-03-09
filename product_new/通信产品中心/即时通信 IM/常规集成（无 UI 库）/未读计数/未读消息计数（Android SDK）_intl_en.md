
## Unread Messages

Unread messages are messages that have not been reported as read by users. This does not indicate whether the recipient has actually read the messages. To use this feature, you need to enable read receipts. For more information, see [Read Receipts](https://cloud.tencent.com/document/product/269/9232#.E5.B7.B2.E8.AF.BB.E5.9B.9E.E6.89.A7). The `isRead` method of `TIMMessage` identifies whether a message is read or not. To display the correct unread count, developers need to explicitly call read reports to notify the IM SDK whether the messages have been read. For example, you can mark all messages as read when the user enters the chat UI.

>For ChatRoom groups, the server does not save the unread count. The unread count becomes zero after login is completed and being synchronized with the server.

**Prototype:**

```
/**
 * Check whether the message is read
 * @return Return the result of read or unread
 */
public boolean isRead()
```

## Obtaining the Current Unread Count

The unread count of the current conversation can be obtained through the `getUnReadMessageNum` method of `TIMConversation`.

>For ChatRoom groups, the server does not save the unread count. The unread count becomes zero after login is completed and being synced with the server.

**Prototype:**

```
/**
 * Obtain the unread count
 * @return Unread count
 */
public long getUnreadMessageNum()
```

**Example:**

```
//Obtain the conversation extension instance
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.C2C, peer);
//Obtain the conversation unread count
long num = con.getUnreadMessageNum();
Log.d(tag, "unread msg num: " + num);
```

## Read Reports

When the user reads a message in a conversation, a read report is sent, and IM SDK sets all messages before the last read message as read. The API for read reports is `setReadMessage` in `TIMConversation`.

**Prototype:**

```
/**
 * Mark all messages before this message as read
 * @param msg Indicates the last read message. Passing null marks all messages in the conversation as read.
 * @param callback Callback
 */
public void setReadMessage(TIMMessage msg, TIMCallBack callback) 
```

**Example:**

```
//Report read one-to-one chat conversations
String peer = "sample_user_1";  //Obtain the conversation with user "sample_user_1"
TIMConversation conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.C2C,    //Conversation type: one-to-one chat
        peer);                      //Conversation peer’s account
//Mark all messages in this conversation as read
conversation.setReadMessage(null, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "setReadMessage failed, code: " + code + "|desc: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "setReadMessage succ");
	}
});
 
//Report read group chat conversations
String groupId = "TGID1EDABEAEO";  //Obtain the conversation with group "TGID1LTTZEAEO"
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.Group,      //Conversation type: group chat
        groupId);                       //Group ID
//Mark the message represented by lastMsg and all previous messages as read
conversation.setReadMessage(lastMsg, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "setReadMessage failed, code: " + code + "|desc: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "setReadMessage succ");
	}
});
```

>The methods for setting one-to-one and group chats as read are the same, with the only difference being the conversation type.

## Synchronizing Read Reports Across Multiple Clients

In the event of multi-client login, unread count synchronization notifications are delivered by the server. The IM SDK updates the unread count locally and notifies the user to update conversations. Notifications initiate callback through the `onRefreshConversation` API in `TIMRefreshListener`. Users who require multi-client synchronization can perform relevant synchronization through this API. For more information, see [Conversation Refreshment](https://cloud.tencent.com/document/product/269/9229#.E4.BC.9A.E8.AF.9D.E5.88.B7.E6.96.B0.E7.9B.91.E5.90.AC).

**Prototype:**

```
/**
 * Refresh some conversations, including synchronizing multi-client read reports
 * @param conversations List of conversations to be refreshed
 */
public void onRefreshConversation(List<TIMConversation> conversations);
```

## Disabling Auto Reporting

For better performance, the IM SDK pulls unread messages to local storage, and the server deletes the unread messages by default. Unread messages that were previously pulled on another client are invisible to clients to be switched to later, even if auto read reporting is disabled. For a single client, the unread count is correct. If you want unread messages to appear on multiple clients, you can call the `disableAutoReport` method in `TIMUserConfig` to disable auto reporting. IM does not perform read reporting for users after auto reporting is disabled.

>
> - After auto reporting is disabled, developers need to explicitly call `setReadMessage` to perform read reporting.
> - This must be set before login for the setting to take effect.


**Prototype:**

```
/**
 * Configure whether to enable read reporting, which is enabled by default, and set this before login.
 * @param disableAutoReport true: disabled, false: enabled
 */
public TIMUserConfig disableAutoReport(boolean disableAutoReport) 
```

