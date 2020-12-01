This document describes how to send and receive messages through Web and mini programs.
## Sending Messages


### Creating a text message

This API is used to create a text message. It returns a message instance. If you need to send a text message, call [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.

**API name**

```javascript
tim.createTextMessage(options)
```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Default | Description |
| ------------------ | -------- | ------------ | ------------------------------- | ------------------------------------------------------------ |
| `to` | `String` | - | - | userID or groupID of the recipient |
| `conversationType` | `String` | - | - | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (C2C conversation) and `TIM.TYPES.CONV_GROUP` (group conversation). |
| `priority` | `String` | `<optional>` | `TIM.TYPES.MSG_PRIORITY_NORMAL` | Message priority |
| `payload` | `Object` | - | - | Message content container |

`payload` has the following properties:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `text` | `String` | Text content of the message. |

**Example**

```javascript
// Send a text message. This process is the same for web applications and WeChat Mini Programs.
// 1. Create a message instance. The instance returned by the API can be displayed on the screen.
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority applicable to group chats (supported since v2.4.2). If the message sending frequency of a group exceeds the limit, the backend delivers high-priority messages first. For more information, see https://intl.cloud.tencent.com/document/product/1047/33526.
  // Valid values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, and TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    text: 'Hello world!'
  }
});
// 2. Send a message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message is sent successfully.
  console.log(imResponse);
}).catch(function(imError){
  // The message fails to be sent.
  console.warn('sendMessage error:', imError);
});
```

**Response**

This API returns a message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).



### Creating an image message

This API is used to create an image message. It returns a message instance. If you need to send an image message, call [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.

>! File objects are supported since v2.3.1. If you need to use file objects, upgrade your SDK to v2.3.1 or later.


**API**

```javascript
tim.createImageMessage(options)
```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Default | Description |
| ------------------ | ---------- | ------------ | ------------------------------- | ---------------------------------------------------------- |
| `to` | `String` | - | - | Message recipient |
| `conversationType` | `String` | - | - | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `priority` | `String` | `<optional>` | `TIM.TYPES.MSG_PRIORITY_NORMAL` | Message priority |
| `payload` | `Object` | - | - | Message content container |
| `onProgress` | `function` | - | - | Callback function used to query the upload progress |

`payload` has the following properties:

| Name | Type | Description |
| ---- | ---------------------------- | ------------------------------------------------------------ |
| file | `HTMLInputElement` or `Object` | It is used to select a DOM node or file object of the image in a web application, or the `success` callback parameter for the `wx.chooseImage` API of a WeChat Mini Program. The SDK reads the data contained in this parameter and uploads the image. |

**Web example**

<pre><code class="language-javascript"><span class="hljs-comment">// Example 1 for sending an image message in a web application - Passing into a DOM node</span>
<span class="hljs-comment">// 1. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
<span class="hljs-keyword">let</span> message = tim.createImageMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
  <span class="hljs-comment">// Message priority applicable to group chats (supported since v2.4.2). If the message sending frequency of a group exceeds the limit, the backend delivers high-priority messages first. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Message Priority and Frequency Control</a>.</span>
  <span class="hljs-comment">// Valid values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, and TIM.TYPES.MSG_PRIORITY_LOWEST</span>
  <span class="hljs-comment">// priority: TIM.TYPES.MSG_PRIORITY_NORMAL,</span>
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">file</span>: <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'imagePicker'</span>),
  },
  <span class="hljs-attr">onProgress</span>: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{ <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'file uploading:'</span>, event) }
});
<span class="hljs-comment">// 2. Send a message.</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// The message is sent successfully.</span>
  <span class="hljs-built_in">console</span>.log(imResponse);
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// The message fails to be sent.</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
});</code></pre>

<pre><code><span class="hljs-comment">// Example 2 for sending an image message in a web application - Passing in a file object</span>
<span class="hljs-comment">// Add a message input box with the ID set to "testPasteInput", for example, &lt;input type="text" id="testPasteInput" placeholder="Take a screenshot and paste it in the input box" size="30" /&gt;</span>
<span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'testPasteInput'</span>).addEventListener(<span class="hljs-string">'paste'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">e</span>) </span>{
  <span class="hljs-keyword">let</span> clipboardData = e.clipboardData;
  <span class="hljs-keyword">let</span> file;
  <span class="hljs-keyword">let</span> fileCopy;
  <span class="hljs-keyword">if</span> (clipboardData &amp;&amp; clipboardData.files &amp;&amp; clipboardData.files.length &gt; <span class="hljs-number">0</span>) {
    file = clipboardData.files[<span class="hljs-number">0</span>];
    <span class="hljs-comment">// After the image message is successfully sent, the content pointed by `file` may be cleared by the browser. If you has extra rendering requirements, copy the data in advance.</span>
    fileCopy = file.slice();
  }
  <span class="hljs-keyword">if</span> (<span class="hljs-keyword">typeof</span> file === <span class="hljs-string">'undefined'</span>) {
    <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'file is undefined. Check compatibility of the code or browser.'</span>);
    <span class="hljs-keyword">return</span>;
  }
   <span class="hljs-comment">// 1. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
  <span class="hljs-keyword">let</span> message = tim.createImageMessage({
    <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
    <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
    <span class="hljs-attr">payload</span>: {
      <span class="hljs-attr">file</span>: file
    },
    <span class="hljs-attr">onProgress</span>: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{ <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'file uploading:'</span>, event) }
  });  
  <span class="hljs-comment">// 2. Send a message.</span>
  <span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
  promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
    <span class="hljs-comment">// The message is sent successfully.</span>
    <span class="hljs-built_in">console</span>.log(imResponse);
  }).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
    <span class="hljs-comment">// The message fails to be sent.</span>
    <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
  });
});</code></pre>

**Mini Program example**

```javascript
// Send an image message in a Mini Program.
// 1. Select an image.
wx.chooseImage({
  sourceType: ['album'], // Select an image from the album.
  count: 1, // You can select only one image. The SDK does not support sending multiple images at a time.
  success: function (res) {
    // 2. Create a message instance. The instance returned by the API can be displayed on the screen.
    let message = tim.createImageMessage({
      to: 'user1',
      conversationType: TIM.TYPES.CONV_C2C,
      payload: { file: res },
      onProgress: function(event) { console.log('file uploading:', event) }
    });
    // 3. Send the image.
    let promise = tim.sendMessage(message);
    promise.then(function(imResponse) {
      // The message is sent successfully.
      console.log(imResponse);
    }).catch(function(imError){
      // The message fails to be sent.
      console.warn('sendMessage error:', imError);
    });
  }
})
```

**Response**

This API returns a message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).


### Creating a voice message

This API is used to create a voice message. It returns a message instance. If you need to send a voice message, call [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage). Currently, createAudioMessage is applicable only to WeChat Mini Programs. 

**API**

```javascript
tim.createAudioMessage(options)
```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Default | Description |
| ------------------ | -------- | ------------ | ------------------------------- | ---------------------------------------------------------- |
| `to` | `String` | - | - | Message recipient |
| `conversationType` | `String` | - | - | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `priority` | `String` | `<optional>` | `TIM.TYPES.MSG_PRIORITY_NORMAL` | Message priority |
| `payload` | `Object` | - | - | Message content container |

`payload` has the following properties:

| Name | Type | Description |
| ---- | -------- | -------------------- |
| file | `Object` | Recorded file. |

**Mini Program example**


<pre><code><span class="hljs-comment">// Example: Record a voice message by using the official WeChat RecorderManager. For more information, see <a href="https://developers.weixin.qq.com/minigame/dev/api/media/recorder/RecorderManager.start.html">RecorderManager.start(Object object)</a>.</span>
<span class="hljs-comment">// 1. Obtain the globally unique RecorderManager.</span>
<span class="hljs-keyword">const</span> recorderManager = wx.getRecorderManager();


<span class="hljs-comment">// Some parameters related to recording</span>
<span class="hljs-keyword">const</span> recordOptions = {
  <span class="hljs-attr">duration</span>: <span class="hljs-number">60000</span>, <span class="hljs-comment">// Recording duration in ms. The maximum value is 600000 ms, that is, 10 minutes.</span>
  <span class="hljs-attr">sampleRate</span>: <span class="hljs-number">44100</span>, <span class="hljs-comment">// Sample rate.</span>
  <span class="hljs-attr">numberOfChannels</span>: <span class="hljs-number">1</span>, <span class="hljs-comment">// Number of recording channels.</span>
  <span class="hljs-attr">encodeBitRate</span>: <span class="hljs-number">192000</span>, <span class="hljs-comment">// Encoding rate.</span>
  <span class="hljs-attr">format</span>: <span class="hljs-string">'aac'</span> <span class="hljs-comment">// Format of the voice message. A voice message created using this format can be used in all IM platforms, including the Android, iOS, WeChat Mini Programs, and web platforms.</span>
};

<span class="hljs-comment">// 2.1 Listen for voice recording errors.</span>
recorderManager.onError(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">errMsg</span>) </span>{
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'recorder error:'</span>, errMsg);
});
<span class="hljs-comment">// 2.2 Listen for the recording end event. After recording is completed, call createAudioMessage to create a voice message instance.</span>
recorderManager.onStop(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">res</span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'recorder stop'</span>, res);

  <span class="hljs-comment">// 4. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
  <span class="hljs-keyword">const</span> message = tim.createAudioMessage({
    <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
    <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
    <span class="hljs-attr">payload</span>: {
      <span class="hljs-attr">file</span>: res
    }
  });

  <span class="hljs-comment">// 5. Send the message.</span>
  <span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
  promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
    <span class="hljs-comment">// The message is sent successfully.</span>
    <span class="hljs-built_in">console</span>.log(imResponse);
  }).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
    <span class="hljs-comment">// The message fails to be sent.</span>
    <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
  });
});

<span class="hljs-comment">// 3. Start recording. </span>
recorderManager.start(recordOptions);</code></pre>

**Response**

This API returns a message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).

### Creating a file message

This API is used to create a file message. It returns a message instance. If you need to send a file message, call [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.

>!
>! File objects are supported since v2.3.1. If you need to use file objects, upgrade your SDK to v2.3.1 or later.
>! Since v2.4.0, the maximum size of a file to upload is 100 MB.
> WeChat Mini Programs currently do not support the selection of files. Therefore, this API is not applicable to WeChat Mini Programs.

**API**

```javascript
tim.createFileMessage(options)
```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Default | Description |
| ------------------ | ---------- | ------------ | ------------------------------- | ------------------------------------------------------------ |
| `to` | `String` | - | - | userID or groupID of the recipient |
| `conversationType` | `String` | - | - | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (C2C conversation) and `TIM.TYPES.CONV_GROUP` (group conversation). |
| `priority` | `String` | `<optional>` | `TIM.TYPES.MSG_PRIORITY_NORMAL` | Message priority |
| `payload` | `Object` | - | - | Message content container |
| `onProgress` | `function` | - | - | Callback function used to query the upload progress |

`payload` has the following properties:

| Name | Type | Description |
| ------ | ------------------ | ------------------------------------------------------------ |
| file | `HTMLInputElement` | It is used to select a DOM node or file object of the image in a web application. The SDK reads the data contained in this parameter and uploads the file. |

**Example**

<pre><code class="language-javascript"><span class="hljs-comment">// Example 1 for sending a file message in a web application - Passing in a DOM node</span>
<span class="hljs-comment">// 1. Create a file message instance. The instance returned by the API can be displayed on the screen.</span>
<span class="hljs-keyword">let</span> message = tim.createFileMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
  <span class="hljs-comment">// Message priority applicable to group chats (supported since v2.4.2). If the message sending frequency of a group exceeds the limit, the backend delivers high-priority messages first. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Message Priority and Frequency Control</a>.</span>
  <span class="hljs-comment">// Valid values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, and TIM.TYPES.MSG_PRIORITY_LOWEST</span>
  <span class="hljs-comment">// priority: TIM.TYPES.MSG_PRIORITY_NORMAL,</span>
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">file</span>: <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'filePicker'</span>),
  },
  <span class="hljs-attr">onProgress</span>: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{ <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'file uploading:'</span>, event) }
});
<span class="hljs-comment">// 2. Send a message.</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// The message is sent successfully.</span>
  <span class="hljs-built_in">console</span>.log(imResponse);
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// The message fails to be sent.</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
});</code></pre>


<pre><code><span class="hljs-comment">// Example 2 for sending a file message in a web application - Passing in a file object</span>
<span class="hljs-comment">// Add a message input box with the ID set to "testPasteInput", for example, &lt;input type="text" id="testPasteInput" placeholder="Take a screenshot and paste it in the input box" size="30" /&gt;</span>
<span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'testPasteInput'</span>).addEventListener(<span class="hljs-string">'paste'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">e</span>) </span>{
  <span class="hljs-keyword">let</span> clipboardData = e.clipboardData;
  <span class="hljs-keyword">let</span> file;
  <span class="hljs-keyword">let</span> fileCopy;
  <span class="hljs-keyword">if</span> (clipboardData &amp;&amp; clipboardData.files &amp;&amp; clipboardData.files.length &gt; <span class="hljs-number">0</span>) {
    file = clipboardData.files[<span class="hljs-number">0</span>];
    <span class="hljs-comment">// After the image message is successfully sent, the content pointed by `file` may be cleared by the browser. If you has extra rendering requirements, copy the data in advance.</span>
    fileCopy = file.slice();
  }
  <span class="hljs-keyword">if</span> (<span class="hljs-keyword">typeof</span> file === <span class="hljs-string">'undefined'</span>) {
    <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'file is undefined. Check compatibility of the code or browser.'</span>);
    <span class="hljs-keyword">return</span>;
  }
  <span class="hljs-comment">// 1. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
  <span class="hljs-keyword">let</span> message = tim.createFileMessage({
    <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
    <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
    <span class="hljs-attr">payload</span>: {
      <span class="hljs-attr">file</span>: file
    },
    <span class="hljs-attr">onProgress</span>: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{ <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'file uploading:'</span>, event) }
  });
  <span class="hljs-comment">// 2. Send a message.</span>
  <span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
  promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
    <span class="hljs-comment">// The message is sent successfully.</span>
    <span class="hljs-built_in">console</span>.log(imResponse);
  }).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
    <span class="hljs-comment">// The message fails to be sent.</span>
    <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
  });
});</code></pre>


**Response**

This API returns a message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).




### Creating a custom message

This API is used to create a custom message. It returns a message instance. If you need to send a custom message, call [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.
If the SDK does not provide the capability you need, use custom messages to customize features, for example, the dice rolling feature.

**API**

```javascript
tim.createCustomMessage(options)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Default | Description |
| ------------------ | -------- | ------------ | ------------------------------- | ------------------------------------------------------------ |
| `to` | `String` | - | - | userID or groupID of the recipient |
| `conversationType` | `String` | - | - | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (C2C conversation) and `TIM.TYPES.CONV_GROUP` (group conversation). |
| `priority` | `String` | `<optional>` | `TIM.TYPES.MSG_PRIORITY_NORMAL` | Message priority |
| `payload` | `Object` | - | - | Message content container |

`payload` has the following properties:

| Name | Type | Description |
| ------------- | -------- | -------------------- |
| `data` | `String` | Data field of the custom message |
| `description` | `String` | Description field of the custom message |
| `extension` | `String` | Extension field of the custom message |

**Example**

<pre><code class="language-javascript"><span class="hljs-comment">// Example: Implement the dice rolling feature by using a custom message.</span>
<span class="hljs-comment">// 1. Customize a random function.</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">random</span>(<span class="hljs-params">min, max</span>) </span>{
  <span class="hljs-keyword">return</span> <span class="hljs-built_in">Math</span>.floor(<span class="hljs-built_in">Math</span>.random() * (max - min + <span class="hljs-number">1</span>) + min);
}
<span class="hljs-comment">// 2. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
<span class="hljs-keyword">let</span> message = tim.createCustomMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
  <span class="hljs-comment">// Message priority applicable to group chats (supported since v2.4.2). If the message sending frequency of a group exceeds the limit, the backend delivers high-priority messages first. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Message Priority and Frequency Control</a>.</span>
  <span class="hljs-comment">// Valid values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, and TIM.TYPES.MSG_PRIORITY_LOWEST</span>
  <span class="hljs-comment">// priority: TIM.TYPES.MSG_PRIORITY_HIGH,</span>
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">data</span>: <span class="hljs-string">'dice'</span>, <span class="hljs-comment">// Identify the message as a dice message.</span>
    <span class="hljs-attr">description</span>: <span class="hljs-built_in">String</span>(random(<span class="hljs-number">1</span>,<span class="hljs-number">6</span>)), <span class="hljs-comment">// Obtain the outcome of dice rolling.</span>
    <span class="hljs-attr">extension</span>: <span class="hljs-string">''</span>
  }
});
<span class="hljs-comment">// 3. Send the message.</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// The message is sent successfully.</span>
  <span class="hljs-built_in">console</span>.log(imResponse);
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// The message fails to be sent.</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
});
</code></pre>

**Response**

This API returns a message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).


### Creating a video message

This API is used to create a video message. It returns a message instance. If you need to send a video message, call [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.

>!
>- This API requires SDK v2.2.0 or later.
>- createVideoMessage is applicable to WeChat Mini Programs and can be used in web applications if the SDK version is v2.6.0 or later.
>- You can use WeChat Mini Programs to record a video message, or select a video from your album. However, Mini Programs do not return a thumbnail of the video. To improve user experience, the SDK sets a default thumbnail for each video message during creation. If you do not wish to display the default thumbnail, skip the information related to the thumbnail during rendering.
>- To make your video messages compatible with all platforms, use [the latest TUIKit or SDK](https://intl.cloud.tencent.com/document/product/1047/33996) to develop your mobile client.  

**API**

```javascript
tim.createVideoMessage(options)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Default | Description |
| ------------------ | -------- | ------------ | ------------------------------- | ---------------------------------------------------------- |
| `to` | `String` | - | - | Message recipient |
| `conversationType` | `String` | - | - | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `priority` | `String` | `<optional>` | `TIM.TYPES.MSG_PRIORITY_NORMAL` | Message priority |
| `payload` | `Object` | - | - | Message content container |

`payload` has the following properties:

| Name | Type | Description |
| ------ | ---------------------------------- | ------------------------------------------------------------ |
| `file` | `HTMLInputElement`, `File`, or `Object` | This is used to select a DOM node or file object of the video file in a web application, or to record a video file or select a video file from the album in a WeChat Mini Program. The SDK reads and uploads the data contained in this parameter. |

**Example**


<pre><code class="language-javascript"><span class="hljs-comment">// Example of sending a video message in a Mini Program<a href="https://developers.weixin.qq.com/miniprogram/dev/api/media/video/wx.chooseVideo.html">wx.chooseVideo</a></span>
<span class="hljs-comment">// 1. Call the Mini Program API to select a video file.</span>
wx.chooseVideo({
  <span class="hljs-attr">sourceType</span>: [<span class="hljs-string">'album'</span>, <span class="hljs-string">'camera'</span>], <span class="hljs-comment">// Source of the video file, which is the album or camera</span>
  <span class="hljs-attr">maxDuration</span>: <span class="hljs-number">60</span>, <span class="hljs-comment">// Maximum duration, which is 60s</span>
  <span class="hljs-attr">camera</span>: <span class="hljs-string">'back'</span>, <span class="hljs-comment">// Rear camera</span>
  success (res) {
    <span class="hljs-comment">// 2. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
    <span class="hljs-keyword">let</span> message = tim.createVideoMessage({
      <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
      <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
      <span class="hljs-attr">payload</span>: {
        <span class="hljs-attr">file</span>: res
      },
      <span class="hljs-attr">onProgress</span>: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{ <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'video uploading:'</span>, event) }
    })
    <span class="hljs-comment">// 3. Send the message.</span>
    <span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
    promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
      <span class="hljs-comment">// The message is sent successfully.</span>
      <span class="hljs-built_in">console</span>.log(imResponse);
    }).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
      <span class="hljs-comment">// The message fails to be sent.</span>
      <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
    });
  }
})

<span class="hljs-comment">// Example of sending a video message in a web application (supported since v2.6.0):</span>
<span class="hljs-comment">// 1. Obtain the video file, and pass in the DOM node.</span>
<span class="hljs-comment">// 2. Create a message instance.</span>
<span class="hljs-keyword">const</span> message = tim.createVideoMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">file</span>: <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'videoPicker'</span>) <span class="hljs-comment">// Alternatively, use event.target.</span>
  },
  <span class="hljs-attr">onProgress</span>: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event</span>) </span>{ <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'file uploading:'</span>, event) }
});
<span class="hljs-comment">// 3. Send the message.</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// The message is sent successfully.</span>
  <span class="hljs-built_in">console</span>.log(imResponse);
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// The message fails to be sent.</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
});
</code></pre>

**Response**

This API returns a message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).

### Creating an emoji message

This API is used to create an emoji message. It returns a message instance. If you need to send an emoji message, call [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.

>! This API requires SDK v2.3.1 or later.

**API**

```javascript
tim.createFaceMessage(options)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Default | Description |
| ------------------ | -------- | -------------- | ------------------------------- | ------------------------------------------------------------ |
| `to` | `String` | - | - | userID or groupID of the recipient |
| `conversationType` | `String` | - | - | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` (C2C conversation) and `TIM.TYPES.CONV_GROUP` (group conversation). |
| `priority` | `String` | `<optional>` | `TIM.TYPES.MSG_PRIORITY_NORMAL` | Message priority |
| `payload` | `Object` | - | - | Message content container |

`payload` has the following properties:

| Name | Type | Description |
| ------- | -------- | -------------------- |
| `index` | `Number` | Emoji index, which is customized by the user |
| `data`  | `String` | Extra data |

**Example**

<pre><code class="language-javascript"><span class="hljs-comment">// Send an emoji. This process is the same for web applications and WeChat Mini Programs.</span>
<span class="hljs-comment">// 1. Create a message instance. The instance returned by the API can be displayed on the screen.</span>
<span class="hljs-keyword">let</span> message = tim.createFaceMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'user1'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_C2C,
  <span class="hljs-comment">// Message priority applicable to group chats (supported since v2.4.2). If the message sending frequency of a group exceeds the limit, the backend delivers high-priority messages first. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33526">Message Priority and Frequency Control</a>.</span>
  <span class="hljs-comment">// Valid values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, and TIM.TYPES.MSG_PRIORITY_LOWEST</span>
  <span class="hljs-comment">// priority: TIM.TYPES.MSG_PRIORITY_NORMAL,</span>
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">index</span>: <span class="hljs-number">1</span>, <span class="hljs-comment">// The number indicates the emoji index, which is customized by the user.</span>
    <span class="hljs-attr">data</span>: <span class="hljs-string">'tt00'</span> <span class="hljs-comment">// The string indicates the extra data.</span>
  }
});
<span class="hljs-comment">// 2. Send a message.</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message);
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// The message is sent successfully.</span>
  <span class="hljs-built_in">console</span>.log(imResponse);
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// The message fails to be sent.</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError);
});
</code></pre>

**Response**

This API returns a message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).


### Sending a message

This API is used to send a message. Before sending a message, call the following APIs to create a message instance and then call this API to send the message instance.

- [createTextMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage)
- [createImageMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage)
- [createAudioMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage)
- [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage)
- [createCustomMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createCustomMessage)
- [createFaceMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceVMessage)
- [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage)

>!The SDK needs to be `ready` in order to call this API to send message instances. The following events can be listened for to learn the SDK status:
- [TIM.EVENT.SDK_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_READY): this event is triggered when the SDK status is ready.
- [TIM.EVENT.SDK_NOT_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_NOT_READY): this event is triggered when the SDK status is not ready.

[TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED) must be listened for in order to receive the pushed new one-to-one messages, group messages, group notifications, or system group notifications.
Messages sent by this API do not trigger [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED). Messages sent by the same account from other clients (or through the RESTful API) trigger [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED). Offline push is applicable only to Android or iOS terminals and is not supported by web applications or WeChat Mini Programs. 

**API**

```javascript
tim.sendMessage(options)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | **Attributes** | Description |
| --------- | --------- | -------------- | ------------------------------ |
| `message` | `Message` | - | Message instance |
| `options` | `Object` | `optional` | Message sending option (message content container) |

`options` is described in the following table.

| Name | Type | **Attributes** | Description |
| ----------------- | --------- | -------------- | ------------------------------------------------------------ |
| `onlineUserOnly` | `Boolean` | `optional` | Whether the message is sent to online users only. This parameter is supported since v2.6.4. The default value is false. If this parameter is set to true, the message is not stored in the roaming server, not counted as an unread message, and not pushed to the recipient offline. It is applicable to sending of unimportant prompts or messages, such as broadcast notifications. This parameter does not apply to messages sent in an AVChatRoom. |
| `offlinePushInfo` | `Object` | `optional` | Offline push information. This parameter is supported since v2.6.4. For more information, see [Offline Push](https://intl.cloud.tencent.com/document/product/1047/33525). |

`offlinePushInfo` is described in the following table.

| Name | Type | **Attributes** | Description |
| ---------------------- | --------- | -------------- | ------------------------------------------------------------ |
| `disablePush` | `Boolean` | `optional` | true: offline push is disabled. false (default): offline push is enabled. |
| `title` | `String` | `optional`| Title of offline push. This parameter is used by both iOS and Android. |
| `description` | `String` | `optional` | Offline push content. This field will overwrite the offline push display text of the message instance. If the sent message is a custom message, this field overwrites `message.payload.description`. If both `description` and `message.payload.description` are left unspecified, the recipient cannot receive the offline push notification of the custom message. |
| `extension` | `String` | `optional` | Passthrough content of offline push |
| `ignoreIOSBadge` | `Boolean` | `optional` | Whether the badge count is ignored (applicable to iOS only). If this parameter is set to true, the unread count icon of the application will not increase when the message is received by an iOS device. |
| `androidOPPOChannelID` | `String` | `optional` | Channel ID for offline push configured on OPPO mobile phones that run Android 8.0 or later. |

**Example**

<pre><code><span class="hljs-comment">// If the recipient is offline, the message will be stored in the roaming server and pushed offline (when the recipient's application switches to the backend or the process is killed). The default title and content of offline push are kept.</span>
<span class="hljs-comment">// For more information about offline push, see <a href="https://intl.cloud.tencent.com/document/product/1047/33525">Offline Push</a>.</span>
<span class="hljs-selector-tag">tim</span><span class="hljs-selector-class">.sendMessage</span>(message);
<span class="hljs-comment">// The message sending option is supported since v2.6.4.</span>
<span class="hljs-selector-tag">tim</span><span class="hljs-selector-class">.sendMessage</span>(message, {
<span class="hljs-attribute">onlineUserOnly</span>: true<span class="hljs-comment">// If the recipient is offline, the message is neither stored in the roaming server nor pushed offline.</span>
});
<span class="hljs-comment">// The message sending option is supported since v2.6.4.</span>
<span class="hljs-selector-tag">tim</span><span class="hljs-selector-class">.sendMessage</span>(message, {
  <span class="hljs-attribute">offlinePushInfo</span>: {
    <span class="hljs-attribute">onlineUserOnly</span>: true<span class="hljs-comment">// If the recipient is offline, the message is stored in the roaming server, but is not pushed offline.</span>
  }
});
<span class="hljs-comment">// The message sending option is supported since v2.6.4.</span>
<span class="hljs-selector-tag">tim</span><span class="hljs-selector-class">.sendMessage</span>(message, {
  <span class="hljs-comment">// If the recipient is offline, the message will be stored in the roaming server and pushed offline (when the recipient's application switches to the backend or the process is killed). The title and content of offline push can be customized at the access end.</span>
  <span class="hljs-attribute">offlinePushInfo</span>: {
    <span class="hljs-attribute">title</span>: <span class="hljs-string">''</span>, <span class="hljs-comment">// Title of offline push</span>
    <span class="hljs-attribute">description</span>: <span class="hljs-string">''</span>, <span class="hljs-comment">// Content of offline push</span>
    <span class="hljs-attribute">androidOPPOChannelID</span>: <span class="hljs-string">''</span> <span class="hljs-comment">// Channel ID for offline push configured on OPPO mobile phones that run Android 8.0 or later</span>
  }
});</code></pre>


**Response**

**Type** : `Promise`

### Recalling a message

This API is used to recall a one-to-one message or a group message. If the recall is successful, the value of `isRevoked` for the message is set to `true`.

>!
>- This API requires SDK v2.4.0 or later.
>- The time limit for message recall is 2 minutes by default. You can log in to the [IM console](https://console.cloud.tencent.com/im-detail/login-message) to change this limit.
>- You can call the [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) API to pull recalled messages from the one-to-one or group message roaming list. Recalled messages are displayed based on `isRevoked` of the message object. For example, "The other party has recalled a message" can be displayed if a message is recalled during a one-to-one conversation, or "Tom has recalled a message" can be displayed if a message is recalled during a group conversation.
>- You also use a RESTful API to [recall one-to-one messages](https://intl.cloud.tencent.com/document/product/1047/35015) or [recall group messages](https://intl.cloud.tencent.com/document/product/1047/34965).

**API**

```javascript
tim.revokeMessage(options)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| --------- | --------- | ----------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Actively recall a message.
let promise = tim.revokeMessage(message);
promise.then(function(imResponse) {
  // The message is successfully recalled.
}).catch(function(imError){
  // The message fails to be recalled.
  console.warn('revokeMessage error:', imError);
});

```

```javascript
tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // The message recall notification is received. Before using this API, upgrade the SDK to v2.4.0 or later.
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - An array that stores the Message objects - [Message] - The `isRevoked` value of each Message object is `true`.
});

```

```javascript
// Obtain a message list which contains recalled messages.
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  messageList.forEach(function(message) {
    if (message.isRevoked) {
      // Handle the recalled messages.
    } else {
      // Handle common messages.
    }
  });
});

```

**Response**

**Type** : `Promise`

### Resending a message

This API is used to resend a message. When a message fails to be sent, call this API to resend the message.

**API**

```javascript
tim.resendMessage(options)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| --------- | --------- | ----------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Resend a message.
let promise = tim.resendMessage(message); // Pass in the message instance that needs to be resent.
promise.then(function(imResponse) {
  // The message is successfully resent.
  console.log(imResponse.data.message);
}).catch(function(imError){
  // The message fails to be resent.
  console.warn('resendMessage error:', imError);
});
```

**Response**

This API returns a `Promise` object:

- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the group list from `IMResponse.data.groupList`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



## Receiving Messages

### Receiving a message

For more information, see [MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).

This API is used to receive messages by means of listening for events.

**Example**

```javascript
let onMessageReceived = function(event) {
  // event.data - Array that stores the Message objects - [Message]
};
tim.on(TIM.EVENT.MESSAGE_RECEIVED, onMessageReceived);
```



### Parsing a text message

<ul><li><b>Simple version</b><br>
 If your text message contains only text, the message is rendered as `'xxxxxxx'` on the UI.</li>
<li><b>If the message contains special formatted text such as [Toothy], the formatted text is rendered as the corresponding emoji <img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">.</b>


```javascript
const emojiMap = {         // Map the formatted text to emojis.
  '[Grin]': 'emoji_0.png',
  '[Toothy]': 'emoji_1.png',
  '[Rain]': 'emoji_2.png'
}

const emojiUrl = 'http://xxxxxxxx/emoji/'   // URL of <img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">

function parseText (payload) {
  let renderDom = []
  // Text message
    let temp = payload.text
    let left = -1
    let right = -1
    while (temp !== '') {
      left = temp.indexOf('[')
      right = temp.indexOf(']')
      switch (left) {
        case 0:
          if (right === -1) {
            renderDom.push({
              name: 'text',
              text: temp
            })
            temp = ''
          } else {
            let _emoji = temp.slice(0, right + 1)
            if (emojiMap[_emoji]) {    // If you want to render text as emojis, you need to map the text to the URLs of the emojis.
              renderDom.push({
                name: 'img',
                src: emojiUrl + emojiMap[_emoji]
              })
              temp = temp.substring(right + 1)
            } else {
              renderDom.push({
                name: 'text',
                text: '['
              })
              temp = temp.slice(1)
            }
          }
          break
        case -1:
          renderDom.push({
            name: 'text',
            text: temp
          })
          temp = ''
          break
        default:
          renderDom.push({
            name: 'text',
            text: temp.slice(0, left)
          })
          temp = temp.substring(left)
          break
      }
    }
  return renderDom
}


// The final structure of renderDom is [{name: 'text', text: 'XXX'}, {name: 'img', src: 'http://xxx'}......].
// Render the array to obtain the desired UI result, for example, XXX<img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">XXX<img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">XXX[Toothy XXX].

```

</li></ul>


### Parsing system notifications

```javascript
function parseGroupSystemNotice (payload) {
  const groupName =
      payload.groupProfile.groupName || payload.groupProfile.groupID
  switch (payload.operationType) {
    case 1:
      return `${payload.operatorID} requests to join ${groupName}`
    case 2:
      return `You have successfully joined ${groupName}`
    case 3:
      return `Your request to join ${groupName} has been denied.`
    case 4:
      return `You have been removed from ${groupName} by ${payload.operatorID}`
    case 5:
      return `${groupName} has been disbanded by ${payload.operatorID}`
    case 6:
      return `${payload.operatorID} has created ${groupName}`
    case 7:
      return `${payload.operatorID} invites you to join ${groupName}`
    case 8:
      return `You have withdrawn from ${groupName}`
    case 9:
      return `${payload.operatorID} has made you an admin of ${groupName}`
    case 10:
      return `${payload.operatorID} has removed you as an admin of ${groupName}.`
    case 255:
      return 'Custom system group notification'
  }
}

```



### Parsing group notifications

```javascript
function parseGroupTipContent (payload) {
  switch (payload.operationType) {
    case this.TIM.TYPES.GRP_TIP_MBR_JOIN:
      return `${payload.userIDList.join(',')} joined the group`
    case this.TIM.TYPES.GRP_TIP_MBR_QUIT:
      return `${payload.userIDList.join(',')} left the group`
    case this.TIM.TYPES.GRP_TIP_MBR_KICKED_OUT:
      return `${payload.operatorID} removed ${payload.userIDList.join(',')} from the group`
    case this.TIM.TYPES.GRP_TIP_MBR_SET_ADMIN:
      return `The following member(s) are now admins: ${payload.userIDList.join(',')}`
    case this.TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN:
      return `The following member(s) are no longer admins: ${payload.userIDList.join(',')}`
    default:
      return '[Group notification]'
  }
}

```



## Conversation APIs

### Obtaining the message list of a conversation 

For more information, see [Conversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html).

This API is used to pull by page the message list of a specified conversation. It is called when the message list is rendered for the first time after the user joins the conversation, or when the user pulls down the list to see more messages.

**API**

```javascript
tim.getMessageList(options)

```

>!This API can be used to fetch history messages.

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Attributes | Description |
| ------------------ | -------- | ------------ | --------------------------------------------------------- |
| `conversationID` | `String` | `<optional>` | ID of the conversation, which is in the following format: C2C+userID (for a one-to-one conversation); GROUP+groupID (for a group conversation); or @TIM#SYSTEM (for a system notification). |
| `nextReqMessageID` | `String` | `<optional>` | Message ID, which is used to continue pulling messages by page. This parameter can be left unspecified the first time messages are pulled. Every time the API is called, this parameter is returned, and you need to specify it for the next pulling. |
| `count` | `Number` | `<optional>` | Number of messages to be pulled. Both the default value and maximum value are 15. This value indicates that a maximum of 15 messages can be pulled at a time. |

**Example**

```javascript
// Pull the message list for the first time when a conversation is opened.
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list.
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pulling by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});

```

```javascript
// Pull the message list for the first time when a conversation is opened.
// Pull down to see more messages.
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list.
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pulling by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});

```

**Response**

This API returns a `Promise` object:

- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the group list from `IMResponse.data.groupList`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

### Marking conversations as read

This API is used to set the unread messages of a conversation to the read state. Messages set to the read status are not counted as unread messages. This API is called when you open or switch a conversation. If this API is not called when you open or switch a conversation, the corresponding messages remain in the unread state.

**API**

```javascript
tim.setMessageRead(options)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| --------- | -------- | -------------- |
| `options` | `Object` | Message content container |

`payload` has the following properties:

| Name | Type | Description |
| ---------------- | -------- | ------------------------------------------------------------ |
| `conversationID` | `String` | ID of the conversation, which is in the following format: C2C+userID (for a one-to-one conversation); GROUP+groupID (for a group conversation); or @TIM#SYSTEM (for a system notification). |

**Example**

```javascript
// Mark all unread messages of a conversation as read.
tim.setMessageRead({conversationID: 'C2Cexample'});

```



### Obtaining the conversation list

This API is used to obtain the conversation list. It will pull the latest 100 conversations. You can call this API when you want to refresh the conversion list.

>!
>- The profile in the conversation list obtained by this API is incomplete. It contains only information such as profile photos and nicknames, which is sufficient to meet the requirements for rendering the conversation list. To query the detailed conversation profile, call [getConversationProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getConversationProfile).
>- The conversation retention time is consistent with the storage time of the last message, which is 7 days by default. That is, conversations will be stored for 7 days by default. 

**API**

```javascript
tim.getConversationList()

```

**Example**

```javascript
// Pull the conversation list.
let promise = tim.getConversationList();
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // This conversation list will overwrite the original conversation list.
}).catch(function(imError){
  console.warn('getConversationList error:', imError); // Information related to the failure to obtain the conversation list
});

```

**Response**

This API returns a `Promise` object:

- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the group list from `IMResponse.data.groupList`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



### Obtaining a conversation profile

This API is used to obtain the profile of a conversation. When you click a conversation in the conversation list, this API is called to obtain the detailed information of the conversation.

**API**

```javascript
tim.getConversationProfile(conversationID)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| ---------------- | -------- | ------------------------------------------------------------ |
| `conversationID` | `String` | ID of the conversation, which is in the following format: C2C+userID (for a one-to-one conversation); GROUP+groupID (for a group conversation); or @TIM#SYSTEM (for a system notification). |

**Example**

```javascript
let promise = tim.getConversationProfile(conversationID);
promise.then(function(imResponse) {
  // The conversation profile is successfully obtained.
  console.log(imResponse.data.conversation); // Conversation profile
}).catch(function(imError){
  console.warn('getConversationProfile error:', imError); // Information related to the failure to obtain the conversation profile
});

```

**Response**

This API returns a `Promise` object:

- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the group list from `IMResponse.data.groupList`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



### Deleting a conversation

This API is used to delete a conversation based on the conversation ID. It deletes only the conversation but not the messages. For example, if the conversation with user A is deleted, the previous chat messages will still be available next time when you initiate a conversation with user A.

**API**

```javascript
tim.deleteConversation(conversationID)

```

**Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| ---------------- | -------- | ------------------------------------------------------------ |
| `conversationID` | `String` | ID of the conversation, which is in the following format: C2C+userID (for a one-to-one conversation); GROUP+groupID (for a group conversation); or @TIM#SYSTEM (for a system notification). |

**Example**

```javascript
let promise = tim.deleteConversation('C2CExample');
promise.then(function(imResponse) {
  // The conversation is deleted successfully.
  const { conversationID } = imResponse.data;// ID of the deleted conversation
}).catch(function(imError){
  console.warn('deleteConversation error:', imError); // Information related to the failure to delete the conversation
});

```

**Response**

This API returns a `Promise` object:

- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the group list from `IMResponse.data.groupList`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).
