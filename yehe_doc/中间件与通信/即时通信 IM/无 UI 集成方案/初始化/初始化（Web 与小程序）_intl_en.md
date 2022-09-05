## Creating an SDK Instance
### Web project
<pre>
import TIM from 'tim-js-sdk';
// COS SDK for sending messages such as images and files
import COS from "cos-js-sdk-v5";

let options = {
  SDKAppID: 0 // Replaces 0 with the SDKAppID of your IM app during access.
};
// Creates an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Sets the SDK log level for output. For details on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // We recommend that you use the common level during access as it covers an extensive range of logs.
// tim.setLogLevel(1); // Sets the release level, at which the SDK outputs important information. We recommend that you use this level in the production environment.

// Registers the COS SDK plug-in.
tim.registerPlugin({'cos-js-sdk': COS});
</pre>

### Mini program project
<pre>
import TIM from 'tim-wx-sdk';
// COS SDK for sending messages such as images and files
import COS from "cos-wx-sdk-v5";

let options = {
  SDKAppID: 0 // Replaces 0 with the SDKAppID of your IM app during access.
};
// Creates an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Sets the SDK log level for output. For details on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // We recommend that you use the common level during access as it covers an extensive range of logs.
// tim.setLogLevel(1); // Sets the release level, at which the SDK outputs important information. We recommend that you use this level in the production environment.

// Registers the COS SDK plug-in.
tim.registerPlugin({'cos-wx-sdk': COS});
</pre>

## Setting the Log Level
<pre>
// Sets the SDK log level for output. For details on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0);
</pre>

## Binding Events
<pre>
// Events that are listened for, for example:
tim.on(TIM.EVENT.SDK_READY, function(event) {
  // The notification stating that offline message and conversation list synchronization is completed is received. The access side can call APIs that require authentication such as sendMessage.
  // event.name - TIM.EVENT.SDK_READY
});

tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
  // New one-to-one chat, group chat, group tips, and group system push notification messages are received. Traverse event.data to obtain message list data and render it to the interface.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - Array that stores Message objects - [Message]
});

tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // The message recall notification is received.
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - Array that stores Message objects - [Message] - Value of the isRevoked attribute of each Message object is true
});

tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, function(event) {
  // The conversation list refreshment notification is received. Traverse event.data to obtain conversation list data and render it to the interface.
  // event.name - TIM.EVENT.CONVERSATION_LIST_UPDATED
  // event.data - Array that stores Conversation objects - [Conversation]
});

tim.on(TIM.EVENT.GROUP_LIST_UPDATED, function(event) {
  // The group list refreshment notification is received. Traverse event.data to obtain group list data and render it to the interface.
  // event.name - TIM.EVENT.GROUP_LIST_UPDATED
  // event.data - Array that stores Group objects - [Group]
});

tim.on(TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED, function(event) {
  // The new group system notification is received.
  // event.name - TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED
  // event.data.type - Types of group system notifications. For more information, see the <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload"> description of operationType enumerated values</a> for GroupSystemNoticePayload.
  // event.data.message - Message object, which can render event.data.message.content to the interface
});

tim.on(TIM.EVENT.PROFILE_UPDATED, function(event) {
  // The user or friend profile change notification is received.
  // event.name - TIM.EVENT.PROFILE_UPDATED
  // event.data - Array that stores Profile objects - [Profile]
});

tim.on(TIM.EVENT.BLACKLIST_UPDATED, function(event) {
  // The blacklist update notification is received.
  // event.name - TIM.EVENT.BLACKLIST_UPDATED
  // event.data - Array that stores userIDs - [userID]
});

tim.on(TIM.EVENT.ERROR, function(event) {
  // The SDK error notification is received. The error code and error message can be obtained.
  // event.name - TIM.EVENT.ERROR
  // event.data.code - Error code
  // event.data.message - Error message
});

tim.on(TIM.EVENT.SDK_NOT_READY, function(event) {
  // The notification stating that the SDK enters the not ready state is received. In this case, the SDK cannot work normally.
  // event.name - TIM.EVENT.SDK_NOT_READY
});

tim.on(TIM.EVENT.KICKED_OUT, function(event) {
  // The forcible logout notification is received.
  // event.name - TIM.EVENT.KICKED_OUT
  // event.data.type - Reason for forcible logout, for example:
  //    - TIM.TYPES.KICKED_OUT_MULT_ACCOUNT Forced logout due to multi-instance login
  //    - TIM.TYPES.KICKED_OUT_MULT_DEVICE Forced logout due to multi-client login
  //    - TIM.TYPES.KICKED_OUT_USERSIG_EXPIRED Forced logout due to signature expiration
});
</pre>

For more information on the initialization process and the use of APIs, see [SDK Initialization](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html).
