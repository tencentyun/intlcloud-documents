## Feature Description
You **must** initialize the IM SDK before using its features.

## Initialization
You can initialize the SDK in the following steps:
1. Prepare an `SDKAppID`.
2. Call `TIM.create` to initialize the SDK.
3. Add an SDK event listener.

The detailed steps are as follows.

### Preparing an SDKAppID
To perform the initialization, you must have a correct `SDKAppID`.
The `SDKAppID` uniquely identifies a Tencent Cloud IM account. We recommend you apply for a new `SDKAppID` for each application. Messages are naturally isolated and cannot communicate between different `SDKAppID` values.
In the [IM console](https://console.cloud.tencent.com/im), you can view all your `SDKAppID` values, and you can click **Create Application** to create an `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/0f985a6fa6ac7f6a8c278ae021da7b12.png)

### Calling the initialization API
After performing the above steps, you can call [TIM.create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) to initialize the SDK.

**API**

<dx-codeblock>
:::  js

 TIM.create(options);

:::
</dx-codeblock>

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name     | Type    | Description                                                  |
| -------- | ------- | ------------------------------------------------------------ |
| SDKAppID | Number  | `SDKAppID` of the IM app                                     |
| oversea  | Boolean | If your app needs to be used outside the Chinese mainland, set this property to `true`. Then, the SDK will use a domain name outside the Chinese mainland to avoid interference. |


**Sample**

<dx-codeblock>
:::  js

// SDK v2.11.2 and later versions support WebSocket, and we recommend you integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
import TIM from 'tim-js-sdk';
import TIMUploadPlugin from 'tim-upload-plugin';

let options = {
  SDKAppID: 0 // Replace 0 with the `SDKAppID` of your IM application when connecting.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by `tim`.

// Set the SDK log output level. For more information on each level, see <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Common level. We recommend you use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. We recommend you use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

:::
</dx-codeblock>

### Listening on events

**Sample**

<dx-codeblock>
:::  js

// This event is triggered when the SDK enters the `ready` status. When detecting this event during listening, you can call SDK APIs such as the message sending API to use various features of the SDK.
let onSdkReady = function(event) {
  let message = tim.createTextMessage({ to: 'user1', conversationType: 'C2C', payload: { text: 'Hello world!' }});
  tim.sendMessage(message);
};
tim.on(TIM.EVENT.SDK_READY, onSdkReady);

// This event is triggered when the SDK enters the `not ready` status. In this case, you cannot use SDK features such as message sending. To use them, you need to call the `login` API to drive the SDK into the `ready` status.
let onSdkNotReady = function(event) {
  // To use features such as message sending, you need to drive the SDK to enter the `ready` status and then call the login API again as follows:
  // tim.login({userID: 'your userID', userSig: 'your userSig'});
};
tim.on(TIM.EVENT.SDK_NOT_READY, onSdkNotReady);

// This event is triggered when the SDK receives a newly pushed one-to-one message, group message, group tip, or group system message. When this event occurs, you can traverse event.data to obtain the message list and render it to the UI.
let onMessageReceived = function(event) {
  // event.data - An array that stores Message objects - [Message]
};
tim.on(TIM.EVENT.MESSAGE_RECEIVED, onMessageReceived);

// This event is triggered when the SDK receives a notification for message modifications. When this event occurs, the message sender can traverse event.data to obtain the message list and update the content of the message with the same ID on the UI.
let onMessageModified = function(event) {
  // event.data - An array that stores modified Message objects - [Message]
};
tim.on(TIM.EVENT.MESSAGE_MODIFIED, onMessageModified);

// This event is triggered when the SDK receives a notification indicating that messages are recalled. When this event occurs, the access side can traverse event.data to obtain data of the message recall list and render the recalled messages to the UI. For example, The peer end has recalled a message can be displayed if a message is recalled during a one-to-one conversation, and "XXX has recalled a message" can be displayed if a message is recalled during a group conversation.
let onMessageRevoked = function(event) {
  // event.data - An array that stores Message objects - [Message] - The `isRevoked` attribute value of each Message object is `true`.
};
tim.on(TIM.EVENT.MESSAGE_REVOKED, onMessageRevoked);

// This event is triggered when the SDK receives a notification (read receipt) indicating that the peer end has read the message. When this event occurs, the access side can traverse event.data to obtain data of the message recall list and render the recalled messages to the UI. For example, for a one-to-one conversation, the status of the message sent by the current party can be changed from Unread to Read.
let onMessageReadByPeer = function(event) {
  // event.data - An array that stores the Message objects - [Message] - The `isPeerRead` value of each Message object is `true`.
};
tim.on(TIM.EVENT.MESSAGE_READ_BY_PEER, onMessageReadByPeer);

// The SDK receives the read receipt of the group message (supported from v2.18.0).
let onMessageReadReceiptReceived = function(event) {
  // event.data - An array that stores message read receipt information
  const readReceiptInfoList = event.data;
  readReceiptInfoList.forEach((item) => {
    const { groupID, messageID, readCount, unreadCount } = item;
    const message = tim.findMessage(messageID);
    if (message) {
      if (message.readReceiptInfo.unreadCount === 0) {
        // Read by all
      } else {
        // message.readReceiptInfo.readCount - Latest read count of the message
        // To query which group members have read the message, call the [getGroupMessageReadMemberList] API.
      }
    }
  });
};
tim.on(TIM.EVENT.MESSAGE_READ_RECEIPT_RECEIVED, onMessageReadReceiptReceived);

// This event is triggered when the conversation list is updated. event.data is an array that stores the Conversation objects.
let onConversationListUpdated = function(event) {
  console.log(event.data); // Array that stores Conversation instances
};
tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, onConversationListUpdated);

// This event is triggered when the SDK group list is updated. The access side can traverse event.data to obtain the group list and render it to the UI.
let onGroupListUpdated = function(event) {
   console.log(event.data);// Array that stores Group instances
};
tim.on(TIM.EVENT.GROUP_LIST_UPDATED, onGroupListUpdated);

This event is triggered when group properties are updated. The access side can traverse event.data to obtain the updated group properties (supported from v2.14.0).
let onGroupAttributesUpdated = function(event) {
   const groupID = event.data.groupID // Group ID
   const groupAttributes = event.data.groupAttributes // Updated group attributes
   console.log(event.data);
};
tim.on(TIM.EVENT.GROUP_ATTRIBUTES_UPDATED, onGroupAttributesUpdated);

// This event is triggered when a topic is created (supported from v2.19.1).
let onTopicCreated = function(event) {
  const groupID = event.data.groupID // Group ID of the topic
  const topicID = event.data.topicID // Topic ID
  console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_CREATED, onTopicCreated);

// This event is triggered when a topic is deleted (supported from v2.19.1).
let onTopicDeleted = function(event) {
  const groupID = event.data.groupID // Group ID of the topic
  const topicIDList = event.data.topicIDList // List of deleted topic IDs
  console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_DELETED, onTopicDeleted);

// This event is triggered when a topic profile is updated (supported from v2.19.1).
let onTopicUpdated = function(event) {
   const groupID = event.data.groupID // Group ID of the topic
   const topic = event.data.topic // Topic profile
   console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_UPDATED, onTopicUpdated);

// This event is triggered when the profile of the current user or profiles of friends are changed. event.data is an array that stores Profile objects.
let onProfileUpdated = function(event) {
  console.log(event.data); // Array that stores Profile objects
};
tim.on(TIM.EVENT.PROFILE_UPDATED, onProfileUpdated);

// This event is triggered when the SDK blocklist is updated.
let onBlacklistUpdated = function(event) {
  console.log(event.data); // Your blocklist. The value is an array that stores `userID` values.
};
tim.on(TIM.EVENT.BLACKLIST_UPDATED, onBlacklistUpdated);

// This event is triggered when the contact is updated.
let onFriendListUpdated = function(event) {
  console.log(event.data);
}
tim.on(TIM.EVENT.FRIEND_LIST_UPDATED, onFriendListUpdated);

// This event is triggered when the friend list is updated.
let onFriendGroupListUpdated = function(event) {
  console.log(event.data);
}
tim.on(TIM.EVENT.FRIEND_GROUP_LIST_UPDATED, onFriendGroupListUpdated);

// FRIEND_APPLICATION_LIST_UPDATED
let onFriendApplicationListUpdated = function(event) {
  // friendApplicationList - Friend request list - [FriendApplication]
  // unreadCount - Number of unread friend requests
  const { friendApplicationList, unreadCount } = event.data;
  // Friend requests received by you (friend requests that are sent to you by others)
  const applicationSentToMe = friendApplicationList.filter((friendApplication) => friendApplication.type === TIM.TYPES.SNS_APPLICATION_SENT_TO_ME);
  // Friend requests sent by you (friend requests that you send to others)
  const applicationSentByMe = friendApplicationList.filter((friendApplication) => friendApplication.type === TIM.TYPES.SNS_APPLICATION_SENT_BY_ME);
};
tim.on(TIM.EVENT.FRIEND_APPLICATION_LIST_UPDATED, onFriendApplicationListUpdated);

// This event is triggered when the current user is kicked offline.
let onKickedOut = function(event) {
  console.log(event.data.type);
  // TIM.TYPES.KICKED_OUT_MULT_ACCOUNT (The user is forcibly logged out because the same account logs in from multiple webpages on the web client.)
  // TIM.TYPES.KICKED_OUT_MULT_DEVICE (The user is forcibly logged out because the same account logs in from multiple terminals.)
  // TIM.TYPES.KICKED_OUT_USERSIG_EXPIRED (The signature expired.)
  // TIM.TYPES.KICKED_OUT_REST_API (The user is forcibly logged out by the RESTful API, which is supported since v2.20.0/)
};
tim.on(TIM.EVENT.KICKED_OUT, onKickedOut);

// This event is triggered when the network status changes.
let onNetStateChange = function(event) {
  // Supported from v2.5.0
  // event.data.state indicates the current network status. The enumerated values are described as follows:
  // TIM.TYPES.NET_STATE_CONNECTED: Already connected to the network
  // TIM.TYPES.NET_STATE_CONNECTING: Connecting. This often occurs when the SDK must reconnect due to network jitter. The message "The current network is unstable" or "Connecting..." can be displayed at the access side based on this status.
  // TIM.TYPES.NET_STATE_DISCONNECTED: Disconnected. The message "The current network is unavailable" can be displayed at the access side based on this status. The SDK will continue to try to reconnect. If the user network recovers, the SDK will automatically synchronize messages.
};
tim.on(TIM.EVENT.NET_STATE_CHANGE, onNetStateChange);

:::
</dx-codeblock>


## Uninitialization

Terminate the SDK instance. The SDK will log out, disconnect the WebSocket persistent connection, and then release resources.

<dx-codeblock>
:::  js

tim.destroy();

:::
</dx-codeblock>
