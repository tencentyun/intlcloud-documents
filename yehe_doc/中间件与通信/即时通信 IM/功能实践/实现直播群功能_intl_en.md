IM livestreaming groups (AVChatRooms) have the following features:
- **Support interactive livestreaming scenarios with unlimited group members.**
- **Support content filtering to identify harmful content related to pornography, politics, and sensitive words to meet regulatory requirements.**
- Support pushing messages (group system notifications) to all online members.
- Allow users to receive messages as guests without logging in using the web client or WeChat Mini Program.
- Allow users to join a group without admin approval.

>? This document uses the SDK for the web client and WeChat Mini Program as an example. The implementation processes of other SDKs are the same with slightly different operations.

## Use Cases

#### On-screen comments for livestreaming
 A livestreaming group (AVChatRoom) supports various message types, including on-screen comments, gifts, and likes. It can easily build a good chatting and interactive experience for livestreaming. It also supports on-screen comment moderation to protect your livestreams from sensitive words.
#### Influencer marketing
 A livestreaming group (AVChatRoom), when combined with business livestreaming, supports specific message types, such as likes, inquiries, and vouchers, helping you monetize your traffic.

#### Teaching whiteboard
 A livestreaming group (AVChatRoom) provides capabilities, such as online classrooms, text messages, and pen motion sensing to support teaching scenarios, such as communication between teachers and students, pen motion saving, large classes, and small classes.

## Use limits
- [Recalling messages](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#revokeMessage) is not supported.
- The group owner cannot directly quit the group and can only achieve the same result by disbanding the group.
- Group members cannot be removed.


## Related Documentation
- [Group Management](https://intl.cloud.tencent.com/document/product/1047/33530)
- [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996)
- [Changelog (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDK Manual](https://web.sdk.qcloud.com/im/doc/zh-cn/TIM.html)
- [SDK Integration (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34309)
- [Initialization (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34314)
- [Sending and Receiving Messages (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34322)
- [Group Management (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34330)

## Instructions
<span id="Step1"></span>
### Step 1: create an app

1. Log in to the [IM console](https://console.cloud.tencent.com/im).
 >? If you already have an app, take note of the SDKAppID and go to [Step 2](#Step2).
 > A Tencent Cloud account supports a maximum of 300 IM apps. If you have reached that limit, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app before creating a new one. **Once an app is deleted, all the data and services associated with the SDKAppID are removed and cannot be recovered, so proceed with caution.**
 >
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter a name for your app and click **OK**. After the app is created, you can view the status, version, SDKAppID, creation time, and expiration time of the app on the overview page of the console.
4. Take note of the SDKAppID.

<span id="Step2"></span>
### Step 2: create a livestreaming group (AVChatRoom)
You can create a group in the console or by calling [Creating a Group](https://intl.cloud.tencent.com/document/product/1047/34895). This document creates a group in the console.


1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card.
2. In the left sidebar, select **Group Management** and click **Add Group**.
3. Enter a name for the group and the group owner ID (optional). Select **AVChatRoom** for **Group Type**.
4. Click **OK**. After the group is created, take note of the **Group ID**. `@TGS#aC72FIKG3` is used as an example here.


<span id="Step3"></span>
### Step 3: integrate the SDK
You can integrate the SDK using NPM or Script, and we recommend NPM. The example in this document uses NPM integration.

- Web project
```javascript
// Web project
npm install tim-js-sdk --save-dev
```
- Mini Program project
```javascript
// WeChat Mini Program project
npm install tim-wx-sdk --save-dev
```

>? If a problem occurs during dependency synchronization, change the NPM source and try again.
```
// Change the CNPM source.
npm config set registry http://r.cnpmjs.org/
```

<span id="Step4"></span>
### Step 4: create an SDK instance

<pre><code><span class="hljs-comment">// Create an SDK instance. The TIM.create() method returns the same instance for the same SDKAppID.</span>
<span class="hljs-keyword">let</span> options = {
  SDKAppID: <span class="hljs-number">0</span> <span class="hljs-comment">// Replace 0 with the SDKAppID of your IM application during integration.</span>
}
<span class="hljs-keyword">let</span> tim = TIM.create(options) <span class="hljs-comment">// The SDK instance is usually represented by tim.</span>
<span class="hljs-comment">// Set the SDK logging level. For more information, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html?_ga=1.43970405.1562552652.1542703643#setLogLevel">setLogLevel Description</a>.</span>
tim.setLogLevel(<span class="hljs-number">0</span>) <span class="hljs-comment">// Normal level. We recommend that you use this level during integration as it covers more logs.</span>

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.SDK_READY, function (<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// The access side can call APIs that require authentication, such as sendMessage, only after the SDK is ready. Otherwise, the calls will fail.</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.SDK_READY</span>
})

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.MESSAGE_RECEIVED, function(<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// A newly pushed one-to-one message, group message, group prompt, or group system notification is received. You can traverse `event.data` to obtain the message list and render it to the UI.</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.MESSAGE_RECEIVED</span>
  <span class="hljs-comment">// event.data - an array that stores Message objects - [Message]</span>
  <span class="hljs-keyword">const</span> length = <span class="hljs-keyword">event</span>.data.<span class="hljs-function">length
  <span class="hljs-keyword">let</span> message
  <span class="hljs-title">for</span> (<span class="hljs-params"><span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; length; i++</span>)</span> {
    <span class="hljs-comment">// For more information on the data structure of Message instances, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html">Message</a>.</span>
    <span class="hljs-comment">// Pay particular attention to the type and payload properties.</span>
    <span class="hljs-comment">// Starting from SDK v2.6.0, the nick (nickname) and avatar (profile photo URL) properties are added for group chat messages and group prompts for events, such as users joining and quitting livestreaming groups. This allows the access side to provide a better display experience.</span>
    <span class="hljs-comment">// To do this, you must first set your own nick (nickname) and avatar (profile photo URL) by calling updateMyProfile. For more information, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#updateMyProfile">updateMyProfile Description</a>.</span>
    message = <span class="hljs-keyword">event</span>.data[i]
    <span class="hljs-keyword">switch</span> (message.type) {
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_TEXT:
        <span class="hljs-comment">// A text message is received.</span>
        <span class="hljs-keyword">this</span>._handleTextMsg(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_CUSTOM:
        <span class="hljs-comment">// A custom message is received.</span>
        <span class="hljs-keyword">this</span>._handleCustomMsg(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_GRP_TIP:
        <span class="hljs-comment">// A group prompt about an event (such as when a user joins the group or a member quits the group) is received.</span>
        <span class="hljs-keyword">this</span>._handleGroupTip(message) 
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_GRP_SYS_NOTICE:
        <span class="hljs-comment">// A group system notification is received. For more information on group system notifications sent using RESTful APIs, see <a href="https://intl.cloud.tencent.com/document/product/1047/34958">Sending System Messages in a Group</a>.</span>
        <span class="hljs-keyword">this</span>._handleGroupSystemNotice(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">default</span>:
         <span class="hljs-keyword">break</span>
    }
  }
})

_handleTextMsg(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.TextPayload">TextPayload Description</a>.</span>
  console.log(message.payload.text) <span class="hljs-comment">// Text message content</span>
}

_handleCustomMsg(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.CustomPayload">CustomPayload Description</a>.</span>
  console.log(message.payload)
}

_handleGroupTip(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.GroupTipPayload">GroupTipPayload Description</a>.</span>
  <span class="hljs-keyword">switch</span> (message.payload.operationType) {
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_JOIN: <span class="hljs-comment">// A user joins the group.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_QUIT: <span class="hljs-comment">// A member quits the group.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: <span class="hljs-comment">// A member is removed from the group.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_SET_ADMIN: <span class="hljs-comment">// A member is set as an admin. </span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN: <span class="hljs-comment">// A member's admin role is canceled.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: <span class="hljs-comment">// The group profile is modified.</span>
      <span class="hljs-comment">//Starting from v2.6.0, group custom fields can be modified.</span>
      <span class="hljs-comment">// message.payload.newGroupProfile.groupCustomField </span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: <span class="hljs-comment">// The group member profile is modified. For example, the member is muted.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">default</span>:
      <span class="hljs-keyword">break</span>
  }
}

_handleGroupSystemNotice(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.GroupSystemNoticePayload">GroupSystemNoticePayload Description</a>.</span>
  console.log(message.payload.userDefinedField) <span class="hljs-comment">// User-defined field. When sending a group system notification using a RESTful API, you can get the content of the custom notification in this property value.</span>
  <span class="hljs-comment">// For more information on how to use a RESTful API to send group system notifications, see <a href="https://intl.cloud.tencent.com/document/product/1047/34958">Sending System Messages in a Group</a>.</span>
}</code></pre>

<span id="Step5"></span>
### Step 5: log in to the SDK

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Login successful.
}).catch(function(imError) {
  console.warn('login error:', imError); // Information about the login failure.
});
```

<span id="Step6"></span>
### Step 6: set your nickname and profile photo
Starting from SDK v2.6.2, the nick (nickname) and avatar (profile photo URL) properties are added for group chat messages and group prompts for events, such as joining and quitting groups in livestreaming groups. You can call [updateMyProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#updateMyProfile) to set your nickname and profile photo.

```javascript
// Starting from SDK v2.6.0, the nick (nickname) and avatar (profile photo URL) properties are added for group chat messages and group prompts for events, such as joining and quitting groups in livestreaming groups. This allows the access side to provide a better display experience. To do this, you must first set your own profile by calling updateMyProfile.
// Modify your personal standard profile.
let promise = tim.updateMyProfile({
  nick: 'My nickname',
  avatar: 'http(s)://url/to/image.jpg'
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // The profile was updated.
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information on the failure to update your profile.
});
```

<span id="Step7"></span>
### Step 7: join a group
```javascript
// An anonymous user joins the group (no login is required and the user will only receive messages after joining the group).
let promise = tim.joinGroup({ groupID: 'avchatroom_groupID'});
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: // Waiting for the admin's approval.
      break
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // Joined the group successfully.
      console.log(imResponse.data.group) // The profile of the group.
      break
    case TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: // The user is already in the group.
      break
    default:
      break
  }
}).catch(function(imError){
  console.warn('joinGroup error:', imError) // Information on the failure to join the group.
});
```

### Step 8: create a message instance and send a message
This document uses sending a text message as an example.

<pre><code class="language-javascript"><span class="hljs-comment">// Send a text message; same for the web client and WeChat Mini Program.</span>
<span class="hljs-comment">// 1. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
<span class="hljs-keyword">let</span> message = tim.createTextMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'avchatroom_groupID'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_GROUP,
  <span class="hljs-comment">// Group chat message priority (supported by v2.4.2 and later). If messages in a group exceed the frequency limit, the backend delivers high-priority messages first. For more information, please see "Message Priority and Frequency Control" in <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Group Chat Messages</a>.</span>
  <span class="hljs-comment">// Valid values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST</span>
  <span class="hljs-attr">priority</span>: TIM.TYPES.MSG_PRIORITY_NORMAL,
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">text</span>: <span class="hljs-string">'Hello world!'</span>
  }
})
<span class="hljs-comment">// 2. Send a message.</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message)
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// Sent successfully.</span>
  <span class="hljs-built_in">console</span>.log(imResponse)
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// Failed to send.</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError)
})</code></pre>


## FAQs

### 1. If I send a message in which `Message.nick` and `Message.avatar` are both empty, how can the message be processed to normally display the nickname and profile photo on the screen?

You can call [getMyProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getMyProfile) to obtain your nickname and profile photo.

### 2. How can I mute a group member in a livestreaming group?

You can use a custom message to mute a specific group member. The custom message must contain the Members_Account of the group member to be muted and the muting time. Send the custom message to the business backend by calling the [Callback Before Delivering Group Messages](https://intl.cloud.tencent.com/document/product/1047/34374). The business backend will call [Muting and Unmuting Group Members](https://intl.cloud.tencent.com/document/product/1047/34951) to mute the group member.

### 3. How can I remove a group member from a livestreaming group?

You can use a custom message to remove a specific group member. The custom message must contain the Members_Account of the group member to be removed. Set the priority of the custom message to High to prevent the message from being discarded by the backend due to the message sending frequency limit of 40 messages per second. After the SDK receives the message, it calls the [kickGroupMember API](https://intl.cloud.tencent.com/document/product/1047/36169) to remove the group member from the group.

<span id ="p4"></span>

### 4. A group member quits a livestreaming group on the Android, iOS, or PC client when the API for quitting a group is called on the WeChat Mini Program or web client. However, when the API for quitting a group is called on the Android, iOS, or PC client, the group member does not quit the livestreaming group on the WeChat Mini Program or web client. Why is this the case?

The WeChat Mini Program and web client allow users to join livestreaming groups as guests. When the API for quitting a group is called on the Android, iOS, or PC client, the WeChat Mini Program or web client will not proactively trigger the quit group operation.

- To ensure synchronized group quitting on all clients, configure the [Callback After a Group Member Drops Out](https://intl.cloud.tencent.com/document/product/1047/34373) and determine the quit platform based on the OptPlatform field. When the quit platform is Android, iOS, or PC, call [Send a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34919) to send a custom message to the group member who quits the group. The frontend screens the conversation and does not display it on the UI. After the WeChat Mini Program or web client receives the message, it calls the [quitGroup API](https://intl.cloud.tencent.com/document/product/1047/33999).
- To ensure independent group quitting on different clients, configure [Callback After a Group Member Drops Out](https://intl.cloud.tencent.com/document/product/1047/34373) and determine the quit platform based on the OptPlatform field. Call [Send a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34919) to send a custom message to the group member who quits the group. The frontend screens the conversation and does not display it on the UI. After a non-quit platform receives the message, it calls the [joinGroup API](https://intl.cloud.tencent.com/document/product/1047/36169) to join the group. To prevent multiple system notifications for joining and quitting a group, you can submit a ticket to disable system notifications for joining and quitting a group.

### 5. Why are messages lost?

Messages can be lost due to the following conditions:

- Livestreaming groups have a message sending frequency limit of 40 messages per second. You can determine whether a message is discarded due to the frequency limit based on the callbacks before and after delivering group messages. If a message receives the callback before delivering group messages but does not receive the callback after delivering group messages, the message is discarded due to the frequency limit.
- When a group member quits a livestreaming group from the WeChat Mini Program or web client, the member may also quit on the Android, iOS, or PC client. For more information, see [FAQ 4](#p4).
- If the WeChat Mini Program or web client encounters an exception, check whether your SDK version is earlier than v2.7.6. If yes, upgrade your SDK to the latest version.

If the fault persists, submit a ticket to contact us.

### 6. How can I compile statistics on likes and follows?

Customize the like or follow message type. When a user clicks the like or follow icon on the frontend to deliver a custom message, send the like or follow message to the business side by calling the [Callback Before Delivering Group Messages](https://intl.cloud.tencent.com/document/product/1047/34374). The business side counts the number of received like and follow messages and updates the data to the group profile field every 3 to 5 seconds by calling [Modify Basic Group Profiles](https://intl.cloud.tencent.com/document/product/1047/34962). The SDK calls the [getGroupsInfo API](https://intl.cloud.tencent.com/document/product/1047/36169) to count the number of like or follow messages.

### 7. How can I properly set message priorities?

To prevent important messages from being discarded, a livestreaming group provides three message priorities for all messages. The SDK preferentially obtains high priority messages. We recommend that you set the priorities of custom messages as follows:

- High: red packets, gifts, and messages for removing group members
- Normal: common text messages
- Low: likes and follows

### 8. Are there any open-source livestreaming components that can be directly used to watch videos and chat?

Yes. The code is also open-source. For more information, see [Tencent Cloud TWebLive](https://github.com/tencentyun/TWebLive).



