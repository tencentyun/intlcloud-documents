An audio-video chat room (AVChatRoom) has the following characteristics:
- **Suitable for interactive live video broadcasting scenarios with unlimited group members**.
- **Supports content filtering to identify harmful content related to pornography, politics, and profanity to meet regulatory requirements.
- Supports pushing messages (group system notifications) to all online members.
- Allows users to receive messages as guests without logging in using the web client or WeChat Mini Program.
- Users can enter the group directly with no admin approval required.

> This document uses the SDK for the web client and WeChat Mini Programs as an example. The implementation processes of other SDKs are the same with slightly different operations.

## Use Cases

#### On-screen comments for live video broadcasting
 An AVChatRoom makes it easy to build a good chatting and interactive experience for live video broadcasting by supporting various message types including on-screen comments, gifts, and likes. The content moderation capability can protect your livestreams from profanity in on-screen comments.
#### Influencer marketing
 An AVChatRoom, when combined with business live streaming, supports messages such as likes, inquiries, and vouchers, helping you turn traffic into profit.

#### Teaching whiteboard
 An AVChatRoom provides capabilities such as online classroom, text messages, and pen motion, assisting teaching scenarios such as communication between teachers and students, pen motion saving, large classes, and small classes.

## Use Limits
- [Recalling messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage) is not supported.
- The group owner cannot directly quit the group and can only achieve the same result by disbanding the group.
- Group members cannot be removed.


## Related Documentation
- [Group Management](https://intl.cloud.tencent.com/document/product/1047/33530)
- [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996)
- [Changelog (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDK Manual](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html)
- [SDK Integration (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34309)
- [Initialization (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34314)
- [Login (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34318)
- [Sending and Receiving Messages (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34322)
- [Group Management (Web & Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34330)

## Instructions
<span id="Step1"></span>
### Step 1: create an app

1. Log in to the [IM Console](https://console.cloud.tencent.com/im).
 >If you already have an app, take note of the SDKAppID and go to [step 2](#Step2).
 >A Tencent Cloud account supports a maximum of 100 IM apps. If you have reached that limit, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app before creating a new one. **Once an app is deleted, all the data and services associated with the SDKAppID are removed and cannot be recovered, so proceed with caution.**
 >
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter a name for your app and click **OK**. After the app is created, you can view the status, version, SDKAppID, creation time, and expiry time of the app on the overview page of the console.
4. Take note of the SDKAppID.

<span id="Step2"></span>
### Step 2: create an audio-video chat room (AVChatRoom)
You can create a group from the console or by calling the [API to create a group](https://intl.cloud.tencent.com/document/product/1047/34895). This document creates a group from the console.


1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im) and click the target app card.
2. In the left sidebar, select **Group Management** and click **Add Group**.
3. Enter a name for the group and the group owner ID (optional). For **Group Type**, select **Audio-video chat room**.
4. Click **OK**. After the group is created, take note of the **Group ID** (`@TGS#aC72FIKG3` is used as an example here).


<span id="Step3"></span>
### Step 3: integrate the SDK
You can integrate the SDK using NPM or Script, though we recommend NPM. The example in this document uses NPM integration.

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

>If a problem occurs during dependency synchronization, change the npm source and try again.
```
// Change cnpm source
npm config set registry http://r.cnpmjs.org/
```

<span id="Step4"></span>
### Step 4: create an SDK instance

<pre><code><span class="hljs-comment">// Create an SDK instance. The TIM.create() method returns the same instance for the same SDKAppID.</span>
<span class="hljs-keyword">let</span> options = {
  SDKAppID: <span class="hljs-number">0</span> <span class="hljs-comment">// Replace 0 with the SDKAppID of your IM app during integration.</span>
}
<span class="hljs-keyword">let</span> tim = TIM.create(options) <span class="hljs-comment">// The SDK instance is usually represented by tim.</span>
<span class="hljs-comment">// Set the SDK log output level. For a detailed description of each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html?_ga=1.43970405.1562552652.1542703643#setLogLevel">setLogLevel</a>.</span>
tim.setLogLevel(<span class="hljs-number">0</span>) <span class="hljs-comment">// Normal level. We recommend that you use this level during integration as it covers more logs.</span>

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.SDK_READY, function (<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// The accessing side can call APIs that require authentication only after the SDK is ready. Otherwise, the calls will fail.</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.SDK_READY</span>
})

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.MESSAGE_RECEIVED, function(<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// A newly pushed one-to-one message, group message, group tips message, or group system notification is received. You can traverse event.data to get the message list and render it to the UI.</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.MESSAGE_RECEIVED</span>
  <span class="hljs-comment">// event.data - an array that stores Message objects - [Message]</span>
  <span class="hljs-keyword">const</span> length = <span class="hljs-keyword">event</span>.data.<span class="hljs-function">length
  <span class="hljs-keyword">let</span> message
  <span class="hljs-title">for</span> (<span class="hljs-params"><span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; length; i++</span>)</span> {
    <span class="hljs-comment">// For more information on the data structure of Message instances, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message</a>.</span>
    <span class="hljs-comment">// Pay particular attention to the type and payload properties.</span>
    <span class="hljs-comment">// Starting from v2.6.0, the nick (nickname) and avatar (profile photo URL) properties are added for AVChatRoom group chat messages and group tips for events such as joining a group and quitting a group. This allows the accessing side to provide a better display experience.</span>
    <span class="hljs-comment">// To do this, you must first set your own nick (nickname) and avatar (profile photo URL) by calling updateMyProfile. See <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile">updateMyProfile</a>.</span>
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
        <span class="hljs-comment">// A group tips message about an event (such as when member joins the group or a member quits the group) is received.</span>
        <span class="hljs-keyword">this</span>._handleGroupTip(message) 
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_GRP_SYS_NOTICE:
        <span class="hljs-comment">// A group system notification is received. For group system notifications sent via RESTful APIs, see <a href="https://intl.cloud.tencent.com/document/product/1047/34958">the API for sending system notifications in a group</a>.</span>
        <span class="hljs-keyword">this</span>._handleGroupSystemNotice(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">default</span>:
         <span class="hljs-keyword">break</span>
    }
  }
})

_handleTextMsg(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.TextPayload">TextPayload</a>.</span>
  console.log(message.payload.text) <span class="hljs-comment">// Text message content.</span>
}

_handleCustomMsg(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.CustomPayload">CustomPayload</a>.</span>
  console.log(message.payload)
}

_handleGroupTip(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload">GroupTipPayload</a>.</span>
  <span class="hljs-keyword">switch</span> (message.payload.operationType) {
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_JOIN: <span class="hljs-comment">// Member joins the group.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_QUIT: <span class="hljs-comment">// Member quits the group.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: <span class="hljs-comment">// Member is removed from the group.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_SET_ADMIN: <span class="hljs-comment">// Member is set as admin.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN: <span class="hljs-comment">// Member’s admin role is canceled.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: <span class="hljs-comment">// Group profile is modified.</span>
      <span class="hljs-comment">// Modifying group custom fields is supported by v2.6.0 and later.</span>
      <span class="hljs-comment">// message.payload.newGroupProfile.groupCustomField </span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: <span class="hljs-comment">// Group member profile is modified. For example, a member is muted.</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">default</span>:
      <span class="hljs-keyword">break</span>
  }
}

_handleGroupSystemNotice(message) {
  <span class="hljs-comment">// For more information on the data structure, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload">GroupSystemNoticePayload</a>.</span>
  console.log(message.payload.userDefinedField) <span class="hljs-comment">// User-defined field. When sending a group system notification via RESTful APIs, you can get the content of the custom notification in this property value.</span>
  <span class="hljs-comment">// To send group system notifications via RESTful APIs, see the <a href="https://intl.cloud.tencent.com/document/product/1047/34958">API for sending system notifications in a group</a>.</span>
}</code></pre>

<span id="Step5"></span>
### Step 5: log in to the SDK

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Login succeeded.
}).catch(function(imError) {
  console.warn('login error:', imError); // Information about login failure.
});
```

<span id="Step6"></span>
### Step 6: set your nickname and profile photo
SDK version 2.6.2 and higher add nick (nickname) and avatar (profile photo URL) for group chat messages and group notifications such as joining and leaving groups in audio-video chat rooms. You can call [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile) to set your nickname and profile photo.

```javascript
// Starting from SDK version 2.6.0, nick (nickname) and avatar (profile photo URL) are added for group chat messages and group notifications such as joining and leaving groups in audio-video chat rooms. This allows the accessing side to provide a better user experience. To do this, you must first set your own profile by calling updateMyProfile.
// Modify your personal standard profile.
let promise = tim.updateMyProfile({
  nick: 'My nickname',
  avatar: 'http(s)://url/to/image.jpg'
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // The profile is updated.
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
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: // Waiting for the admin’s approval.
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

<pre><code class="language-javascript"><span class="hljs-comment">// Send a text message; same for the web client and WeChat Mini Programs.</span>
<span class="hljs-comment">// 1. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
<span class="hljs-keyword">let</span> message = tim.createTextMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'avchatroom_groupID'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_GROUP,
  <span class="hljs-comment">// Group chat message priority (supported by v2.4.2 and higher). If messages in a group exceed the rate limit, the backend delivers high-priority messages first. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Message Priority and Frequency Control</a>.</span>
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



