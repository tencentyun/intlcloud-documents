## Creating an SDK Instance

### Web project

<pre><code><span class="hljs-keyword">import</span> TIM <span class="hljs-keyword">from</span> <span class="hljs-string">'tim-js-sdk'</span>;
<span class="hljs-comment">// The Tencent Cloud IM upload plugin is required to send messages such as images and files.</span>
<span class="hljs-keyword">import</span> TIMUploadPlugin <span class="hljs-keyword">from</span> <span class="hljs-string">'tim-upload-plugin'</span>;

<span class="hljs-keyword">let</span> options = {
  <span class="hljs-attr">SDKAppID</span>: <span class="hljs-number">0</span> <span class="hljs-comment">// Replace `0` with the `SDKAppID` of your IM app during connection.</span>
};
<span class="hljs-comment">// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.</span>
<span class="hljs-keyword">let</span> tim = TIM.create(options); <span class="hljs-comment">// The SDK instance is usually represented by `tim`.</span>

<span class="hljs-comment">// Set the SDK log output level. For more information on each level, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setLogLevel">setLogLevel API Description</a>.</span>
tim.setLogLevel(<span class="hljs-number">0</span>); <span class="hljs-comment">// Common level. You are advised to use this level during connection as it covers more logs.</span>
<span class="hljs-comment">// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.</span>

<span class="hljs-comment">// Register the Tencent Cloud IM upload plugin.</span>
tim.registerPlugin({<span class="hljs-string">'tim-upload-plugin'</span>: TIMUploadPlugin});</code></pre>


### Mini Program project

<pre><code><span class="hljs-keyword">import</span> TIM <span class="hljs-keyword">from</span> <span class="hljs-string">'tim-wx-sdk'</span>;
<span class="hljs-comment">// The Tencent Cloud IM upload plugin is required to send messages such as images and files.</span>
<span class="hljs-keyword">import</span> TIMUploadPlugin <span class="hljs-keyword">from</span> <span class="hljs-string">'tim-upload-plugin'</span>;


<span class="hljs-keyword">let</span> options = {
  <span class="hljs-attr">SDKAppID</span>: <span class="hljs-number">0</span> <span class="hljs-comment">// Replace `0` with the `SDKAppID` of your IM app during connection.</span>
};
<span class="hljs-comment">// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.</span>
<span class="hljs-keyword">let</span> tim = TIM.create(options); <span class="hljs-comment">// The SDK instance is usually represented by `tim`.</span>

<span class="hljs-comment">// Set the SDK log output level. For more information on each level, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setLogLevel">setLogLevel API Description</a>.</span>
tim.setLogLevel(<span class="hljs-number">0</span>); <span class="hljs-comment">// Common level. You are advised to use this level during connection as it covers more logs.</span>
<span class="hljs-comment">// tim.setLogLevel(1); //  Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.</span>

<span class="hljs-comment">// Register the Tencent Cloud IM upload plugin.</span>
tim.registerPlugin({<span class="hljs-string">'tim-upload-plugin'</span>: TIMUploadPlugin});</code></pre>




## Setting the Log Level

<pre><code><span class="hljs-comment">// Set the SDK log output level. For more information on each level, see <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setLogLevel">setLogLevel API Description</a>.</span>
<span class="hljs-selector-tag">tim</span><span class="hljs-selector-class">.setLogLevel</span>(<span class="hljs-number">0</span>);</code></pre>



## Binding Events


```
// Listened-to events, for example:
tim.on(TIM.EVENT.SDK_READY, function(event) {
  // A notification is received, indicating that the offline message and conversation lists are synchronized successfully. The access side can call APIs that require authentication, such as `sendMessage`.
  // event.name - TIM.EVENT.SDK_READY
});

tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
  // A newly pushed one-to-one message, group message, group tip, or group system notification is received. You can traverse `event.data` to obtain the message list and render it to the UI.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - An array that stores the Message objects - [Message]
});

tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // The message recall notification is received.
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - An array that stores the Message objects - [Message] - The `isRevoked` value of each Message object is `true`.
});

tim.on(TIM.EVENT.MESSAGE_READ_BY_PEER, function(event) {
  // SDK has received a notification indicating that the opposite end has read the message. This is the read receipt. Before using it, you need to upgrade the SDK version to V2.7.0 or higher. Only one-to-one conversations are supported.
  // event.name - TIM.EVENT.MESSAGE_READ_BY_PEER
  // event.data - event.data - An array that stores the Message objects - [Message] - The `isPeerRead` value of each Message object is `true`.
});

tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, function(event) {
  // A conversation list update notification is received. You can traverse `event.data` to obtain the conversation list and render it to the UI.
  // event.name - TIM.EVENT.CONVERSATION_LIST_UPDATED
  // event.data - An array that stores the Conversation objects - [Conversation]
});

tim.on(TIM.EVENT.GROUP_LIST_UPDATED, function(event) {
  // A group list update notification is received. You can traverse `event.data` to obtain the group list and render it to the UI.
  // event.name - TIM.EVENT.GROUP_LIST_UPDATED
  // event.data - An array that stores the Group objects - [Group]
});

tim.on(TIM.EVENT.PROFILE_UPDATED, function(event) {
  // A notification is received, indicating that your own profile or your friend's profile is updated.
  // event.name - TIM.EVENT.PROFILE_UPDATED
  // event.data - An array that stores the Profile objects - [Profile]
});

tim.on(TIM.EVENT.BLACKLIST_UPDATED, function(event) {
  // A blocklist update notification is received.
  // event.name - TIM.EVENT.BLACKLIST_UPDATED
  // event.data - An array that stores userIDs - [userID]
});

tim.on(TIM.EVENT.ERROR, function(event) {
  // An SDK error notification is received. The error code and error message can be obtained from this notification.
  // event.name - TIM.EVENT.ERROR
  // event.data.code - Error code
  // event.data.message - Error message
});

tim.on(TIM.EVENT.SDK_NOT_READY, function(event) {
  // An SDK not ready notification is received. At this time, the SDK cannot function normally.
  // event.name - TIM.EVENT.SDK_NOT_READY
});

tim.on(TIM.EVENT.KICKED_OUT, function(event) {
  // A kicked offline notification is received.
  // event.name - TIM.EVENT.KICKED_OUT
  // event.data.type - Reason for being kicked offline, such as:
  //    - TIM.TYPES.KICKED_OUT_MULT_ACCOUNT: kicked offline due to multi-instance login.
  //    - TIM.TYPES.KICKED_OUT_MULT_DEVICE: kicked offline due to multi-device login.
  //    - TIM.TYPES.KICKED_OUT_USERSIG_EXPIRED: kicked offline due to UserSig expiration (supported from V2.4.0). 
});

 tim.on(TIM.EVENT.NET_STATE_CHANGE, function(event) { 
  //  The network status changes (supported from V2.5.0). 
  // event.name - TIM.EVENT.NET_STATE_CHANGE 
  // event.data.state indicates the current network status. The enumerated values are described as follows: 
  //     \- TIM.TYPES.NET_STATE_CONNECTED: already connected to the network 
  //     \- TIM.TYPES.NET_STATE_CONNECTING: connecting. This often occurs when the SDK must reconnect due to network jitter. The prompt "The current network is unstable" or "Connecting..." can be displayed at the access side based on this status. 
  //    \- TIM.TYPES.NET_STATE_DISCONNECTED: disconnected. The prompt "The current network is unavailable" can be displayed at the access side based on this status. The SDK will continue to try to reconnect. If the user network recovers, the SDK will automatically synchronize messages.  
});

// Start to log in to the SDK. 
tim.login({userID: 'your userID', userSig: 'your userSig'}); 
```

The `options` parameter is of the `Object` type:

| Name | Type | Description |
| --------- | -------- | ----------- |
| `options` | `Object` | App configuration |

`options` includes the following attribute value:

| Name | Type | Description |
| ---------- | -------- | ----------------------- |
| `SDKAppID` | `Number` | `SDKAppID` of the IM app |

For more information on how to initialize the SDK and use APIs, see [SDK Initialization](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html).

## Login

You can send and receive messages in the IM console only after logging in to the IM SDK. To log in to the IM SDK, you need to provide information such as the UserID and UserSig. For more information, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). After successful login, to call APIs that require authentication, such as [sendMessage](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#sendMessage), you must wait until the SDK enters the ready state. You can obtain the status of the SDK by listening to events. For more information, see [TIM.EVENT.SDK_READY](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.SDK_READY).

>!By default, multi-instance login is not supported. If you use an account that has been logged in on another page to log in on the current page, the account may be forcibly logged out on the other page, which will trigger the `TIM.EVENT.KICKED_OUT` event. You can proceed accordingly after detecting the event through listening. An example of listening for multi-instance login is shown below:

```javascript
let onKickedOut = function (event) {
  console.log(event.data.type); // mutipleAccount (The same account that is used to log in on multiple pages on the same device is forcibly logged out.)
};
tim.on(TIM.EVENT.KICKED_OUT, onKickedOut);
```

To support multi-instance login (allowing the use of the same account to log in concurrently on multiple pages), log in to the [IM console](https://console.cloud.tencent.com/im) and click **Feature Configuration** -> **Login and Messages**. In the drop-down list next to **Login and Messages**, select the corresponding `SDKAppID`. Then, in the **Login settings** module, click **Edit** and use the drop-down list next to **Online Web Instances** to configure the number of instances. The configuration will take effect within 5 minutes.

**API**

```javascript
tim.login(options);
```

**Request parameters**

| Name | Type | Description |
| ------- | ------ | ------------------------------------------------------------ |
| UserID | String | The ID of the user. |
| UserSig | String | The password with which the user logs in to the IM console. It is essentially the ciphertext generated by encrypting information such as the UserID.<br/>For the detailed generation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |

**Response**

This API returns a `Promise` object.

**Example**

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Login succeeds.
  if (imResponse.data.repeatLogin === true) {
    // Indicates that the account has logged in and that the current login will be a repeated login. This feature is supported from V2.5.1.
    console.log(imResponse.data.errorInfo);
  }
}).catch(function(imError){
  console.warn('login error:', imError); // Information about the login failure.
});
```



## Logout

 This API is used to log out of the IM console. It is usually called when you switch between accounts. This API clears the login status of the current account and all the data in the memory. 

>!
>- When calling this API, the instance publishes the [SDK_NOT_READY](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.SDK_NOT_READY) event. In this case, the instance is automatically logged out and cannot receive or send messages.
>- Assume that the value of the **Online Web Instances** configured in the [IM console](https://console.cloud.tencent.com/im) is greater than 1, and the same account has been used to log in to instances `a1` and `a2` (including a Mini Program instance). After `a1.logout()` is executed, `a1` is automatically logged out and cannot receive or send messages, whereas `a2` is not affected.
>- Assume that the **Online Web Instances** is set to 2, and your account has been used to log in to instances `a1` and `a2`. When you use this account to log in to instance `a3`, either `a1` or `a2` will be forcibly logged out. In most cases, the instance that first entered the login state is forcibly logged out. This is called **kicked offline due to multi-instance login**. If `a1` is forcibly logged out, a logout process is executed within `a1` and the [KICKED_OUT](https://web.sdk.qcloud.com/im/doc/zh-cn/module-EVENT.html#.KICKED_OUT) event is triggered. The access side can listen to this event and redirect to the login page when the event is triggered. At this time, `a1` is forcibly logged out, whereas instances `a2` and `a3` can continue to run properly.

**API**

```js
tim.logout();
```

**Request parameters**

N\/A

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMResponse). `IMResponse.data` is a null object, indicating that logout succeeded.
- The callback parameter of `catch` is [IMError](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMError).

**Example**

```js
let promise = tim.logout();
promise.then(function(imResponse) {
  console.log(imResponse.data); // Logout succeeds.
}).catch(function(imError){
  console.warn('logout error:', imError);
});
```

