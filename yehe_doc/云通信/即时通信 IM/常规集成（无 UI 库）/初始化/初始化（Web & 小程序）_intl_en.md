## Creating an SDK Instance
### Web project
<pre>
import TIM from 'tim-js-sdk';
// The COS SDK needed for sending messages such as images and files
import COS from "cos-js-sdk-v5";

let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`
let tim = TIM.create(options); // SDK instance is usually represented by tim

// Set SDK log level for output. For a detailed description of each level, please see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Common level, we recommended using this level during connection as it covers large amount of logs
// tim.setLogLevel(1); // Release level, for which the SDK outputs important information. We recommend using this in a production environment.

// Register COS SDK plugin
tim.registerPlugin({'cos-js-sdk': COS});
</pre>

### Mini Program project
<pre>
import TIM from 'tim-wx-sdk';
// The COS SDK needed for sending messages such as images and files
import COS from "cos-wx-sdk-v5";

let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`
let tim = TIM.create(options); // SDK instance is usually represented by tim

// Set SDK log level for output. For a detailed description of each level, please see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Common level, we recommended using this level during connection as it covers large amount of logs
// tim.setLogLevel(1); // Release level, for which the SDK outputs important information. We recommend using this in a production environment.

// Register COS SDK plugin
tim.registerPlugin({'cos-wx-sdk': COS});
</pre>

## Setting Log Level
<pre>
// Set SDK log level for output. For a detailed description of each level, please see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0);
</pre>

## Binding Events
<pre>
// Events that are listened for, for example:
tim.on(TIM.EVENT.SDK_READY, function(event) {
  // Successful offline message and conversation list synchronization notification received. The access side can call APIs that require authentication such as sendMessage.
  // event.name - TIM.EVENT.SDK_READY
});

tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
  // New one-to-one, group, group tips, and group system notification messages that are pushed received. Traverse event.data to get message list data and render it to the interface.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - an array that stores Message objects - [Message]
});

tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // The message recall notification received
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - an array of Message objects - [Message] - the isRevoked property of each Message object is true.
});

tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, function(event) {
  // Conversation list refresh notification received. Traverse event.data to get conversation list data and render it to the interface
  // event.name - TIM.EVENT.CONVERSATION_LIST_UPDATED
  // event.data - array storing conversation objects - [Conversation]
});

tim.on(TIM.EVENT.GROUP_LIST_UPDATED, function(event) {
  // Group list refresh notification received. Traverse event.data to get group list data and render it to the interface
  // event.name - TIM.EVENT.GROUP_LIST_UPDATED
  // event.data - array storing Group objects - [Group]
});

tim.on(TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED, function(event) {
  // New group system notification received
  // event.name - TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED
  // event.data.type - types of group system notifications. For more information, see the <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload"> Description of operationType enumerated values</a> for GroupSystemNoticePayload
  // event.data.message - Message objects, which can render event.data.message.content to the interface
});

tim.on(TIM.EVENT.PROFILE_UPDATED, function(event) {
  // User or friend profile change notification received
  // event.name - TIM.EVENT.PROFILE_UPDATED
  // event.data - array storing Profile objects - [Profile]
});

tim.on(TIM.EVENT.BLACKLIST_UPDATED, function(event) {
  // Blacklist update notification received
  // event.name - TIM.EVENT.BLACKLIST_UPDATED
  // event.data - array storing userIDs - [userID]
});

tim.on(TIM.EVENT.ERROR, function(event) {
  // SDK error notification received. The error code and error message can be obtained.
  // event.name - TIM.EVENT.ERROR
  // event.data.code - Error code
  // event.data.message - Error message
});

tim.on(TIM.EVENT.SDK_NOT_READY, function(event) {
  // SDK not ready notification received. In this case, the SDK cannot function normally.
  // event.name - TIM.EVENT.SDK_NOT_READY
});

tim.on(TIM.EVENT.KICKED_OUT, function(event) {
  // Force offline notification received
  // event.name - TIM.EVENT.KICKED_OUT
  // event.data.type - reason for force offline, for example:
  //    - TIM.TYPES.KICKED_OUT_MULT_ACCOUNT Force offline due to multi-instance login
  //    - TIM.TYPES.KICKED_OUT_MULT_DEVICE Force offline due to multi-client login
  //    - TIM.TYPES.KICKED_OUT_USERSIG_EXPIRED Force offline due to signature expiration
});
</pre>

For more information about the initialization process and the use of APIs, please see [SDK Initialization](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html).
