An audio-video chat room (AVChatRoom) has the following characteristics:
- **Ideal for interactive live streams with unlimited group members**.
- **Filters harmful content related to pornography, politics, and sensitive words to meet regulatory requirements**.
- Pushes messages (group system notifications) to all online members.
- Allows users to receive messages as guests without logging in using the web client and WeChat Mini Programs.
- Allows users to join a group without needing approvals from administrators.

> This document uses the SDK for the web client and WeChat Mini Programs as an example. The implementation processes of other SDKs are the same with slightly different operations.

## Use Cases

#### On-screen comments for live stream
 Audio-video chat rooms support various message types, including on-screen comments, gifts, and likes, which builds an excellent interactive live chat experience. The content of on-screen comments can be reviewed, protecting your live streams from sensitive words.
![](https://imgcache.qq.com/open_proj/proj_qcloud_v2/gateway/product/im-new/css/img/scenes/function2.gif)
#### Streamer marketing
 Audio-video chat rooms can be used as an e-commerce channel. By providing likes, quotes, and vouchers, they help streamers monetize traffic.
 ![](https://imgcache.qq.com/open_proj/proj_qcloud_v2/gateway/product/im-new/css/img/scenes/function3.gif)
#### Online education
 Audio-video chat rooms can provide capabilities such as online classroom, text messages, and pen tracking This is perfect for use cases such as communication between teachers and students, saving pen tracks, large classes, and small classes.
 ![](https://imgcache.qq.com/open_proj/proj_qcloud_v2/gateway/product/im-new/css/img/scenes/function4.gif)

## Limits
- [Recalling messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage) is not supported.
- The group owner cannot quit the group and can only do so by disbanding the group.
- Group members cannot be removed.


## Documentation
- [Group Management](https://intl.cloud.tencent.com/document/product/1047/33530)
- [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996)
- [Changelog (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDK Manual](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html)
- [SDK Integration (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34309)
- [Initialization (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34314)
- [Login (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34318)
- [Sending and Receiving Messages (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34322)
- [Group Management (Web and Mini Programs)](https://intl.cloud.tencent.com/document/product/1047/34330)

## Instructions
<span id="Step1"></span>
### Step 1: create an app

1. Log in to the [IM console](https://console.cloud.tencent.com/im).
 > If you already have an app, record its SDKAppID and go to [Step 2](#Step2).
 > A Tencent Cloud account can create a maximum of 100 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost**. **Proceed with caution**.
 >
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter a name for your app and click **OK**. After the app is created, you can view the status, service version, SDKAppID, creation time, and expiration time of the app on the overview page of the console.
4. Record the SDKAppID.

<span id="Step2"></span>
### Step 2: create an audio-video chat room (AVChatRoom)
You can create a group in the console or by calling the [Creating a Group](https://intl.cloud.tencent.com/document/product/1047/34895) API. This article uses creating a group in the console as an example.


1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the desired app.
2. In the left sidebar, select **Group Management** and click **Add Group**.
3. Enter a name for the group and the group owner ID (optional). Select **Audio-video chat room** as the **Group Type**.
4. Click **OK**. After the group is created, record **Group ID**, for example, `@TGS#aC72FIKG3`.


<span id="Step3"></span>
### Step 3: integrate the SDK
You can use NPM or a script to integrate the SDK. NPM is the recommended method. For the purpose of this article, NPM is used.

- Web project
```javascript
// Web project
npm install tim-js-sdk --save-dev
```
- Mini program project
```javascript
// WeChat mini program project
npm install tim-wx-sdk --save-dev
```

> If a problem occurs during dependency synchronization, change the NPM source and try again.
```
// Change the cnpm source.
npm config set registry http://r.cnpmjs.org/
```

<span id="Step4"></span>
### Step 4: create an SDK instance

<pre>
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app.
}
let tim = TIM.create(options) // The SDK instance is usually named tim.
// Set the SDK log output level. For more information on log levels, refer to <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html?_ga=1.43970405.1562552652.1542703643#setLogLevel">setLogLevel</a>.
tim.setLogLevel(0) // Normal. We recommend this level during integration because it provides more details.

tim.on(TIM.EVENT.SDK_READY, function (event) {
  // Call APIs that require authentication only after SDK ready. Otherwise, API calls will fail.
  // event.name - TIM.EVENT.SDK_READY
})

tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
  // Traverse event.data to get new one-to-one chat messages, group chat messages, group notifications, and group system notifications and render them to the interface.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - an array of message objects - [Message]
  const length = event.data.length
  let message
  for (let i = 0; i < length; i++) {
    // For more information on message instance data structure, refer to <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message</a>.
    // Pay close attention to type and payload.
    // Version 2.6.0 added nick (nickname) and avatar (profile photo URL) for audio-video chat room group chat messages and group notifications (joining and leaving groups) to provide a better user experience.
    // To do this, you must first set your own nick (nickname) and avatar (profile photo URL) by calling updateMyProfile. For more information, refer to <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile">updateMyProfile</a>.
    message = event.data[i]
    switch (message.type) {
      case TIM.TYPES.MSG_TEXT:
        // Text messages.
        this._handleTextMsg(message)
        break
      case TIM.TYPES.MSG_CUSTOM
        // Custom messages.
        this._handleCustomMsg(message)
        break
      case TIM.TYPES.MSG_GRP_TIP:
        // Group notifications such as joining or leaving a group
        this._handleGroupTip(message) 
        break
      case TIM.TYPES.MSG_GRP_SYS_NOTICE:
        // Group system notifications. For more information on using RESTful APIs to send group system notifications, refer to <a href="https://intl.cloud.tencent.com/document/product/1047/34958">Sending System Messages in a Group</a>.
        this._handleGroupSystemNotice(message)
        break
      default:
         break
    }
  }
})

_handleTextMsg(message) {
  // For more information on data structure, refer to <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.TextPayload">TextPayload</a>.
  console.log(message.payload.text) // Text message content
}

_handleCustomMsg(message) {
  // For more information on data structure, refer to <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.CustomPayload">CustomPayload</a>.
  console.log(message.payload)
}

_handleGroupTip(message) {
  // For more information on data structure, refer to <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload">GroupTipPayload</a>.
  switch (message.payload.operationType) {
    case TIM.TYPES.GRP_TIP_MBR_JOIN: // Members join the group.
      break
    case TIM.TYPES.GRP_TIP_MBR_QUIT: // Members leave the group.
      break
    case TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: // Members are kicked out of the group.
      break
    case TIM.TYPES.GRP_TIP_MBR_SET_ADMIN: // Members are set as admins.
      break
    case TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN: // Members are removed as administrators.
      break
    case TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: // The group profile is modified.
      // Modifying group custom fields is supported in v2.6.0 and later.
      // message.payload.newGroupProfile.groupCustomField 
      break
    case TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: // The group member profile changed. For example, a member is muted.
      break
    default:
      break
  }
}

_handleGroupSystemNotice(message) {
  // For more information on data structure, refer to <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload">GroupSystemNoticePayload</a>.
  console.log(message.payload.userDefinedField) // User-defined field. When sending a group system notification using RESTful APIs, you can retrieve the content of the custom notification from the value of this property.
  // To send group system notifications using RESTful APIs, refer to <a href="https://intl.cloud.tencent.com/document/product/1047/34958">Sending System Messages in a Group</a>.
}
</pre>

<span id="Step5"></span>
### Step 5: log in to the SDK

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Login succeeded.
}).catch(function(imError) {
  console.warn('login error:', imError); // Information about the login failure.
});
```

<span id="Step6"></span>
### Step 6: set your nickname and profile photo
SDK 2.6.2 added nick (nickname) and avatar (profile photo URL) for group chat messages and group notifications such as joining and leaving groups in audio-video chat rooms. You can call [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile) to set your nickname and profile photo.

```javascript
// SDK 2.6.2 added nick (nickname) and avatar (profile photo URL) for group chat messages and group notifications such as joining and leaving groups in audio-video chat rooms. This allows clients to provide a better user experience. To do this, you must first set your own profile by calling updateMyProfile.
// Modify your personal standard profile.
let promise = tim.updateMyProfile({
  nick: 'My nickname',
  avatar: 'http(s)://url/to/image.jpg'
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // The profile is updated.
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information on profile update failures.
});
```

<span id="Step7"></span>
### Step 7: join a group
```javascript
// An anonymous user joins the group (no login required, and the user can only receive messages after joining the group).
let promise = tim.joinGroup({ groupID: 'avchatroom_groupID'});
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: // Waiting for the admin's approval.
      break
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // Joined the group successfully.
      console.log(imResponse.data.group) // The group profile.
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

### Step 8: create a message instance and sending a message
This article uses sending a text message as an example.

<pre><code class="language-javascript"><span class="hljs-comment">// Send a text message; same for the web client and WeChat Mini Programs.</span>
<span class="hljs-comment">// 1. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
<span class="hljs-keyword">let</span> message = tim.createTextMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'avchatroom_groupID'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_GROUP,
  <span class="hljs-comment">// Group chat message priority (supported by v2.4.2 and later). If messages in a group exceed the rate limit, the backend delivers high-priority messages first. For more information, refer to <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Message Priority and Frequency Control</a></span>
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



