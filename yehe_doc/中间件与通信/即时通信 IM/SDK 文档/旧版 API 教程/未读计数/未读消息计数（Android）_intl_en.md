
## Unread Messages

Here, unread messages are messages that have not been reported as read by users. This does not indicate whether the recipient has actually read the messages. To use this feature, you need to enable read receipts. For more information, see the **Read receipt** section in [Sending and Receiving Messages (Android)](https://intl.cloud.tencent.com/document/product/1047/36401). The `isRead` of `TIMMessage` identifies whether a message is read or not. To display the correct unread count, developers need to explicitly call read reports to notify the IM SDK whether the messages have been read. For example, you can mark all messages as read when the user enters the chat UI.

>!For chat rooms, the server does not save the unread count. The unread count becomes zero after login is completed and being synchronized with the server.


**Prototype:**

```
/**
 * Check whether the message is read.
 * @return Return the result of read or unread.
 */
public boolean isRead()
```

## Getting the Current Unread Count

You can get the unread count of the current conversation via the `getUnReadMessageNum` method of `TIMConversation`.

>!For chat rooms, the server does not save the unread count. The unread count becomes zero after login is completed and being synchronized with the server.

**Prototype:**

```
/**
 * Get the unread count.
 * @return Return the unread count.
 */
public long getUnreadMessageNum()
```

**Example:**

```
// Get the conversation extension instance.
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.C2C, peer);
// Get the conversation unread count.
long num = con.getUnreadMessageNum();
Log.d(tag, "unread msg num: " + num);
```

## Read Reporting

When a user reads a message in a conversation and a read report is sent, and IM SDK sets all messages before the last read message as read. The API for read reporting is `setReadMessage` in `TIMConversation`.

**Prototype:**

```
/**
 * Mark all messages before this message as read.
 * @param msg The last read message. Passing `null` marks all messages in the conversation as read.
 * @param callback Callback
 */
public void setReadMessage(TIMMessage msg, TIMCallBack callback) 
```

**Examples:**

```
// Report read messages in a one-to-one conversation.
String peer = "sample_user_1";  // Get the conversation with the user "sample_user_1".
TIMConversation conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.C2C,    // Conversation type: one-to-one chat
        peer);                      // Account of the other party of the conversation
// Mark all messages in this conversation as read.
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
 
// Report read messages in a group conversation.
String groupId = "TGID1EDABEAEO";  // Get the conversation of the group "TGID1LTTZEAEO".
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.Group,      //Conversation type: group chat
        groupId);                       // Group ID
// Mark the message represented by `lastMsg` and all previous messages as read.
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

>?The methods for setting messages in one-to-one and group chats as read are the same. The only difference is the conversation type.

## Synchronizing Read Reports Across Multiple Devices

In the case of multi-device login, unread count synchronization notifications are sent by the server. The IM SDK updates the unread count locally and notifies the user to update conversations. Notifications trigger callbacks through the `onRefreshConversation` API in `TIMRefreshListener`. Users who require multi-device synchronization can perform relevant synchronization through this API. For more information, see the **Conversation refresh listener** section in [Initialization (Android)](https://intl.cloud.tencent.com/document/product/1047/36255).

**Prototype:**

```
/**
 * Refresh some conversations, including synchronizing multi-device read reports.
 * @param conversations List of conversations to be refreshed
 */
public void onRefreshConversation(List<TIMConversation> conversations);
```

## Disabling Auto Reporting

For better performance, the IM SDK pulls unread messages to local storage, and the server deletes the unread messages by default. Unread messages that are previously pulled on another device are invisible to devices you switch to later, even if the read messages haven't been manually reported. For a single device, the unread count is correct. If you want unread messages to appear on multiple devices, you can disable auto reporting using the `disableAutoReport` method in `TIMUserConfig`. IM does not perform read reporting for users after auto reporting is disabled.

>!
> - After auto reporting is disabled, developers need to explicitly call `setReadMessage` to perform read reporting.
> - This must be set before login for the setting to take effect.


**Prototype:**

```
/**
 * Configure whether to enable auto read reporting, which is enabled by default, and set this before login.
 * @param disableAutoReport `true`: disabled; `false`: enabled.
 */
public TIMUserConfig disableAutoReport(boolean disableAutoReport) 
```


