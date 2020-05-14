An audio-video chat room (AVChatRoom) has the following characteristics:
- **Suitable for interactive live video broadcasting scenarios with unlimited group members**.
- **Supports content filtering to identify harmful content related to pornography, politics, and sensitive words to meet regulatory requirements.
- Supports pushing messages (group system notifications) to all online members.
- Web and WeChat Mini Program clients allow users to receive messages as guests without logging in.
- Users can enter the group directly with no admin approval required.

## Use Cases

#### On-screen comments for live video broadcasting
 AVChatRoom makes it easy to build good chatting and interactive experience in live video broadcasting by supporting various message types including on-screen comments, gifts, and likes. The content moderation capability can protect your livestreams from sensitive words in on-screen comments.
#### Influencer marketing
 AVChatRoom, when used with business live streaming, supports messages such as likes, inquiries, and vouchers, helping you turn traffic into profit.
#### Teaching whiteboard
 AVChatRoom provides capabilities such as online classroom, text messages, and pen motion, assisting teaching scenarios such as communication between teachers and students, saving pen motion, large classes, and small classes.

## Use limits
- [Recalling messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage) is not supported.
- Group owner cannot directly quit the group and can only do so by disbanding the group.
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
### Step 1: Create an app

1. Log in to the Tencent Cloud [IM Console](https://console.cloud.tencent.com/im).
 > If you already have an app, take note of the SDKAppID and go to [step 2](#Step2).
 > A Tencent Cloud account supports a maximum of 100 IM apps. If 100 IM apps have been created, you can create a new app after [disabling](https://intl.cloud.tencent.com/document/product/1047/34540) and deleting an unwanted app. **After an app is deleted, all the data and services associated with the SDKAppID cannot be recovered. Proceed with caution.**
 >
2. Click **Add a new app**.
3. In the **Create App** dialog box, enter a name for your app and click **OK**. After the app is created, you can view the status, service version, SDKAppID, creation time and expiration time of the app on the overview page of the console.
4. Take note of the SDKAppID.

<span id="Step2"></span>
### Step 2: Create an audio-video chat room (AVChatRoom)
You can create a group from the console or by calling the [API to create a group](https://intl.cloud.tencent.com/document/product/1047/34895). This document creates a group from the console.


1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im), and then click the target app card.
2. In the left sidebar, select **Group Management** and click **Add Group**.
3. Enter a name for the group and the group owner ID (optional). For **Group type**, select **Audio-video chat room**.
4. Click **OK**. After the group is created, take note of the **Group ID** (`@TGS#aC72FIKG3` is used as an example here).


<span id="Step3"></span>
### Step 3: integrate the SDK
You can integrate the SDK using NPM or Script, though NPM is recommended. This document uses NPM integration as an example.

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

> If a problem occurs during dependency synchronization, change npm source and try again.
```
// Change cnpm source
npm config set registry http://r.cnpmjs.org/
```

<span id="Step4"></span>
### Step 4: Create an SDK instance

<pre>
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`
let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app when connecting
}
let tim = TIM.create(options) // SDK instance is usually represented by tim
// Set SDK logging level. For a detailed description of each level, please see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html?_ga=1.43970405.1562552652.1542703643#setLogLevel">setLogLevel</a>.
tim.setLogLevel(0) // Normal level. We recommend using this level during connection as it covers large amounts of logs.

tim.on(TIM.EVENT.SDK_READY, function (event) {
  // The access side can call APIs that require authentication (for example, sendMessage) only after the SDK is ready. Otherwise, you will receive a failure!
  // event.name - TIM.EVENT.SDK_READY
})

tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
  // Received new one-to-one, group, group tips, and group system notification messages that are pushed. Traverse event.data to get message list data and render it to the interface.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - an array that stores Message objects - [Message]
  const length = event.data.length
  let message
  for (let i = 0; i < length; i++) {
    // For more information on the data structure of Message instances, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message</a>.
    // Note particularly the type and payload properties.
    // Starting from v2.6.0, the nick (nickname) and avatar (profile photo URL) properties are added for AVChatRoom group chat messages and group tips on events such as joining group and quitting group, so that the access side can provide a better displaying experience.
    // To do this, you must first set your own nick (nickname) and avatar (profile photo URL) by calling updateMyProfile. See the descriptions of API <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile">updateMyProfile</a>.
    message = event.data[i]
    switch (message.type) {
      case TIM.TYPES.MSG_TEXT:
        // A text message is received.
        this._handleTextMsg(message)
        break
      case TIM.TYPES.MSG_CUSTOM
        // A custom message is received.
        this._handleCustomMsg(message)
        break
      case TIM.TYPES.MSG_GRP_TIP:
        // A group tips message (for example, joining group and quitting group) is received.
        this._handleGroupTip(message) 
        break
      case TIM.TYPES.MSG_GRP_SYS_NOTICE:
        // A group system notification is received. For group system notifications sent via RESTful APIs, see <a href="https://intl.cloud.tencent.com/document/product/1047/34958">the API for sending system notifications in a group</a>.
        this._handleGroupSystemNotice(message)
        break
      default:
         break
    }
  }
})

_handleTextMsg(message) {
  // For more information on the data structure, see the descriptions of API <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.TextPayload">TextPayload</a>.
  console.log(message.payload.text) // Text message content
}

_handleCustomMsg(message) {
  // For more information on the data structure, see the descriptions of API <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.CustomPayload">CustomPayload</a>.
  console.log(message.payload)
}

_handleGroupTip(message) {
  // For more information on the data structure, see the descriptions of API <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload">GroupTipPayload</a>.
  switch (message.payload.operationType) {
    case TIM.TYPES.GRP_TIP_MBR_JOIN: // A member joins the group.
      break
    case TIM.TYPES.GRP_TIP_MBR_QUIT: // A member quits the group.
      break
    case TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: // A member is kicked out of the group.
      break
    case TIM.TYPES.GRP_TIP_MBR_SET_ADMIN: // A member is set as admin.
      break
    case TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN: // The admin role of a member is revoked.
      break
    case TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: // Group profile is modified.
      // Modifying group custom fields is supported by v2.6.0 and higher.
      // message.payload.newGroupProfile.groupCustomField 
      break
    case TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: // Group member profile is modified. For example, a member is muted.
      break
    default:
      break
  }
}

_handleGroupSystemNotice(message) {
  // For more information on the data structure, see the descriptions of API <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload">GroupSystemNoticePayload</a>.
  console.log(message.payload.userDefinedField) // User-defined field. When sending a group system notification via RESTful APIs, you can get the content of the custom notification in this property value.
  // To send group system notifications via RESTful APIs, see the <a href="https://intl.cloud.tencent.com/document/product/1047/34958">API for sending system notifications in a group</a>.
}
</pre>

<span id="Step5"></span>
### Step 5: Join a group
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
  console.warn('joinGroup error:', imError) // Information on the failure in joining the group.
});
```

<span id="Step6"></span>
### Step 6: Log in to the SDK


```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Login succeeded.
}).catch(function(imError) {
  console.warn('login error:', imError); // Information about login failure.
});
```

### Step 7: Create a message instance and send a message
This document takes sending a text message as an example.

<pre>
// Send a text message; same for web applications and Mini Programs.
// 1. Create a message instance. The instance returned by the API can be displayed on the screen.
let message = tim.createTextMessage({
  to: 'avchatroom_groupID',
  conversationType: TIM.TYPES.CONV_GROUP,
  // Message priority applicable to group chats (supported by v2.4.2 and higher). If messages in a group exceed the frequency limit, the backend delivers high-priority messages first. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Message Priority and Frequency Control</a>.
  // Enumerated values supported: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    "Text": "hello world"
  }
})

// 2. Send the message.
let promise = tim.sendMessage(message)
promise.then(function(imResponse) {
  // Sent successfully.
  console.log(imResponse)
}).catch(function(imError) {
  // Failed to send
  console.warn('sendMessage error:', imError)
})
</pre>



