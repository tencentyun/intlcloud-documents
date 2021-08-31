Based on the web (HTML5) player and [Instant Messaging (IM)](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html), the Web ILVB component encapsulates easy-to-use [APIs](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html) and provides a free and open-source [demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/TWebLive-demo.zip), allowing developers to quickly integrate and use this component.
This component is suitable for web livestreaming scenarios, such as large conferences, events, classes, and webinars as well as WeChat HTML5 livestream marketing. 


## Trying It Online
[Click here to try it out](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html) 

## References

- [TWebLive API](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647)
- [TRTC Electron API](https://intl.cloud.tencent.com/document/product/647/35141)
- Web (HTML5) Player
- [Instant Messaging (IM)](https://intl.cloud.tencent.com/document/product/1047)
- [WebIM API](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html)


## Benefits of the Web ILVB Component

#### Reduce development time and allow developers to focus on business logic

When using the Web ILVB component, developers only need to specify several parameters after downloading the [SDK](https://www.npmjs.com/package/tweblive) to implement projects that involve common features such as LVB videos, chats, likes, and gifts.

### Reduce the time required to identify and resolve issues

- In the live streaming scenario, when there are many participants and messages, in-house services can encounter performance bottlenecks (for example, they might not be able to handle highly concurrent workloads), resulting in difficult problems, including a low request success rate, message backlog, message loss, and high message latency. The Web ILVB component ensures high-concurrency and highly available IM capabilities by integrating Instant Messaging (IM), which is built on QQ’s wealth of experience in the IM field. It also provides statistics, logging, and troubleshooting features to help you quickly identify and resolve issues.
- The Web ILVB component allows you to set message priorities. For example, the priority of host messages and gift messages can be set to [high](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/module-TYPES.html#.MSG_PRIORITY_HIGH), and the priority of like messages can be set to [low](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/module-TYPES.html#.MSG_PRIORITY_LOW). When the frequency exceeds 40 messages per second in a live room, the IM backend limits the message frequency, but ensures that high-priority messages are delivered.

### Reduce project development and OPS costs

- The Web ILVB component is free and open-source, and the accompanied Web (HTML5) player is also free. IM is the only value-added service required for this solution. You can use the free Trial Edition or upgrade IM to Enterprise Edition or Flagship Edition. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1047/34349).
- AVChatRoom groups in IM support unlimited group members.
- IM server nodes provide extensive coverage, allowing users to access the service from nearby without worrying about server scaling.
- Content filtering can identify harmful content such as pornography, politics, and profanity in order to meet regulatory requirements.
- Our IM service team quickly responds to protect your projects.



## Instructions

### Step 1: Create an IM app and a group

1. [Create an app](https://intl.cloud.tencent.com/document/product/1047/34577) in the IM console and obtain the SDKAppID.
2. [Generate a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
3. [Import a single account](https://intl.cloud.tencent.com/document/product/1047/34953) (or [import multiple accounts](https://intl.cloud.tencent.com/document/product/1047/34954)) to IM.
4. Create an live streaming group (AVChatRoom group) through the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34895) or [console](https://intl.cloud.tencent.com/document/product/1047/34578).

### Step 2: Run the Web ILVB component

<pre><code class="language-javascript"><span class="hljs-comment">// npm i tweblive</span>
<span class="hljs-keyword">import</span> TWebLive <span class="hljs-keyword">from</span> <span class="hljs-string">'tweblive'</span>;

<span class="hljs-keyword">let</span> options = {
  <span class="hljs-attr">SDKAppID</span>: <span class="hljs-number">0</span>, <span class="hljs-comment">// Replace 0 with the SDKAppID of your IM app during integration.</span>
  <span class="hljs-attr">domID</span>: <span class="hljs-string">"id_test_video"</span>, <span class="hljs-comment">// ID of the web player container, such as &lt;div id="id_test_video" style="width:100%; height:auto;"&gt;&lt;/div&gt;</span>
  <span class="hljs-attr">m3u8</span>: <span class="hljs-string">"http://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8"</span>, <span class="hljs-comment">// Replace it with the actual playback URL.</span>
  <span class="hljs-attr">flv</span>: <span class="hljs-string">"http://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv"</span> <span class="hljs-comment">// Replace it with the actual playback URL.</span>
};
<span class="hljs-comment">// Create an instance.</span>
<span class="hljs-keyword">let</span> tweblive = <span class="hljs-keyword">new</span> TWebLive(options);

<span class="hljs-comment">// This is triggered when the SDK is in the ready state. The accessing side listens to this event so that it can call SDK APIs to send messages or perform other actions and use different features of the SDK.</span>
<span class="hljs-keyword">let</span> onIMReady = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
  tweblive.sendTextMessage({
    <span class="hljs-attr">roomID</span>: <span class="hljs-string">'AV1'</span>, <span class="hljs-comment">// Replace it with the ID of the joined live room.</span>
    <span class="hljs-attr">text</span>: <span class="hljs-string">'hello from TWebLive'</span>
  }).then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">res</span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'demo sendTextMessage OK'</span>, res);
  }).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">err</span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'demo sendTextMessage failed'</span>, err);
  });
}
tweblive.on(TWebLive.EVENT.IM_READY, onIMReady);

<span class="hljs-comment">// A text message from another user in the live room was received.</span>
<span class="hljs-keyword">let</span> onTextMessageReceived = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{
  event.data.forEach(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">message</span>) </span>{
    <span class="hljs-comment">// Use the nickname if any. Otherwise, use the UserID.</span>
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'demo '</span> + (message.nick || message.from) + <span class="hljs-string">' says: '</span>, message.payload.text);
  });
}
tweblive.on(TWebLive.EVENT.TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

<span class="hljs-comment">// A custom message (such as a gift or like message) from another user in the live room was received.</span>
<span class="hljs-keyword">let</span> onCustomMessageReceived = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{
  event.data.forEach(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">message</span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'demo '</span> + <span class="hljs-string">'data:'</span> + message.payload.data + <span class="hljs-string">' description:'</span> + message.payload.description + <span class="hljs-string">' extension:'</span> + message.payload.extension);
  });
}
tweblive.on(TWebLive.EVENT.CUSTOM_MESSAGE_RECEIVED, onCustomMessageReceived);

<span class="hljs-comment">// A notification of a user joining the live room was received.</span>
<span class="hljs-keyword">let</span> onRemoteUserJoin = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{
  event.data.forEach(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">message</span>) </span>{
    <span class="hljs-comment">// Use the nickname if any. Otherwise, use the userID.</span>
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'demo '</span> + (message.nick || message.payload.userIDList[<span class="hljs-number">0</span>]) + <span class="hljs-string">' joined the group'</span>);
  });
}
tweblive.on(TWebLive.EVENT.REMOTE_USER_JOIN, onRemoteUserJoin);

<span class="hljs-comment">// For more events, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html">EVENT</a>.</span>

<span class="hljs-comment">// Anonymously join a live room when not logged in. In this case, you can only receive messages and cannot send messages.</span>
tweblive.enterRoom(<span class="hljs-string">""</span>); <span class="hljs-comment">// Enter the ID of the live room to join. It corresponds to the groupID of the AVChatRoom group in IM.</span>
</code></pre>

### Step 3: Provide the live streaming source
We recommend that you use the [relayed push service](https://intl.cloud.tencent.com/document/product/647/35242) of [TRTC](https://intl.cloud.tencent.com/document/product/647/35078).
For compatibility with both computers and mobile devices, we recommend that you provide your live streaming source in both flv and hls formats.
- On browsers that support MSEs, the component will prefer flv sources as they enable lower latency and better performance.
- On browsers that do not support MSEs, the component will prefer hls sources as they work better with mobile devices, even though they increase latency somewhat.

For LVB push on Windows or Mac platforms, we strongly recommend that you use [TRTC Electron](https://github.com/tencentyun/TRTCSDK/tree/master/Electron). **Relayed push generates both flv and hls streams and integrates with IM to provide stable, reliable, and comprehensive services**.
For instructions on how to quickly enable LVB and relayed push, see [Electron](https://intl.cloud.tencent.com/document/product/647/35089).


### Step 4: Perform secondary development based on the Web ILVB component
You can further develop other business logic and features based on the Web ILVB component.




## FAQs

### 1. How can I display the nickname (nick) instead of `userID` in the notification and chat messages after joining a live room?

To display the nickname in a live room, set the nickname (skip this step if it is already set) and then join the live room.
```javascript
// Only logged-in users can change their nicknames.
tweblive.setMyProfile({ nick: "Indiana Jones" }).then(() => {
  tweblive.enterRoom(""); // Enter the ID of the live room to join. It corresponds to the groupID of the AVChatRoom group in IM.
});
```
