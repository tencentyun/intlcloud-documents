## Sending Messages

### Creating text messages
This API creates text messages. It returns a message instance, which can be called when sending text messages. [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) sends the message instance.


**Name**

```javascript
tim.createTextMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient. |
| `conversationType` | `String` | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` or `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container. |

`payload` has the following properties:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `text` | `String` | Text content of the message. |



**Example**

```javascript
// Sends text messages. Compatible with web apps and Mini Programs.
// 1. Creates a message instance. The returned instance can be displayed on the screen.
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    text: 'Hello world!'
  }
});
// 2. Sends the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully.
  console.log(imResponse);
}).catch(function(imError) {
  // Message failed to send.
  console.warn('sendMessage error:', imError);
});
```

**Response**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).



### Creating image messages
This API creates image messages. It returns a message instance, which can be called when sending image messages. [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) sends the message instance.

> Support for File objects is added in v2.3.1. If you need that, upgrade your SDK to v2.3.1 or above.


**API**

```javascript
tim.createImageMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient. |
| `conversationType` | `String` | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` or `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container. |
| `onProgress` | `function` | A function used to query the upload progress. |

`payload` has the following properties:

| Name | Type | Description |
| ---- | --------------------------- | ------------------------------------------------------------ |
| file | `HTMLInputElement` or `Object` | For web apps, this is the DOM node or File object of the image. For Mini Programs, this is the parameters of the `success` callback for `wx.chooseImage`. SDK reads the data and uploads the image. |

**Web example**

```javascript
// Sends image messages using web apps.
// 1. Creates a message instance. The returned instance can be displayed on the screen.
let message = tim.createImageMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    file: document.getElementById('imagePicker'),
  },
  onProgress: function(event) { console.log('file uploading:', event) }
});
// 2. Sends the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully.
  console.log(imResponse);
}).catch(function(imError) {
  // Message failed to send.
  console.warn('sendMessage error:', imError);
});
```

**Mini Program example**

```javascript
// Sends image messages using Mini Programs.
// 1. Selects an image.
wx.chooseImage({
  sourceType: ['album'], // Select an image from an album.
  count: 1, // You can only select one image. The SDK does not allow multiple selections.
  success: function (res) {
    // 2. Creates a message instance. The returned instance can be displayed on the screen.
    let message = tim.createImageMessage({
      to: 'user1',
      conversationType: TIM.TYPES.CONV_C2C,
      payload: { file: res },
      onProgress: function(event) { console.log('file uploading:', event) }
    });
    // 3. Sends the image.
    let promise = tim.sendMessage(message);
    promise.then(function(imResponse) {
      // Message sent successfully.
      console.log(imResponse);
    }).catch(function(imError) {
      // Message failed to send.
      console.warn('sendMessage error:', imError);
    });
  }
})
```

**Response**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).


### Creating audio messages
This API creates audio messages. It returns a message instance, which can be called when sending audio messages. [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) sends the message instance. createAudioMessage is only applicable for WeChat Mini Programs.

> To make audio messages compatible with all platforms, use [the latest TUIKit or SDK](https://intl.cloud.tencent.com/document/product/1047/33996) to develop your mobile client.

**API**

```javascript
tim.createAudioMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | --------------------- |
| `to` | `String` | Message recipient. |
| `conversationType` | `String` | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` or `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container. |

`payload` has the following properties:

| Name | Type | Description |
| ---- | --------------------------- | ------------ |
| file | `Object` | Recorded audio file. |

**Mini Program example**

<pre>
// This example uses the official WeChat RecorderManager to record the audio message. Refer to <a href="https://developers.weixin.qq.com/minigame/dev/api/media/recorder/RecorderManager.start.html">RecorderManager.start(Object object)</a> for more information.
// 1. Gets the globally unique instance of RecorderManager.
const recorderManager = wx.getRecorderManager();

// Recording parameters
const recordOptions = {
  duration: 60000, // length of the audio message, in ms. Max. value: 600000 ms (10 minutes).
  sampleRate: 44100, // Sample rate
  numberOfChannels: 1, // Number of recording channels
  encodeBitRate: 192000, // Encoding bitrate
  format: 'aac' // Format of the audio message. This audio format is compatible with all IM platforms (Android, iOS, WeChat Mini Programs, and Web apps).
};

// 2.1 Listens for recording errors.
recorderManager.onError(function(errMsg) {
  console.warn('recorder error:', errMsg);
});
// 2.2 Recording finished event. After the recording is done, call createAudioMessage to create an audio message instance.
recorderManager.onStop(function(res) {
  console.log('recorder stop', res);

  // 4. Creates a message instance. The returned instance can be displayed on the screen.
  const message = tim.createAudioMessage({
    to: 'user1',
    conversationType: TIM.TYPES.CONV_C2C,
    payload: {
      file: res
    }
  });

  // 5. Sends the message.
  let promise = tim.sendMessage(message);
  promise.then(function(imResponse) {
    // Message sent successfully.
    console.log(imResponse);
  }).catch(function(imError) {
    // Message failed to send.
    console.warn('sendMessage error:', imError);
  });
});

// 3. Recording starts.
recorderManager.start(recordOptions);
</pre>

**Response**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).

### Creating file messages
This API creates file messages. It returns a message instance, which can be called when sending file messages. [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) sends the message instance.

>
> Support for File objects is added in v2.3.1. If you need that, upgrade your SDK to v2.3.1 or above.
> In v2.4.0, the max size of uploaded files was changed to 100 MB.
> WeChat Mini Programs do not support file messages. Therefore, this API does not support WeChat Mini Programs.

**API**

```javascript
tim.createFileMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `to` | `String` | Message recipient. |
| `conversationType` | `String` | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` or `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container. |
| `onProgress` | `function` | A function used to query the upload progress. |

`payload` has the following properties:

| Name | Type | Description |
| ------ | -------- | ------------ |
| file | `HTMLInputElement` | The DOM node or File object of the file. the SDK reads the data and uploads the image. |

**Example**

```javascript
// Sends a file message.
// 1. Creates a file message instance. The returned instance can be displayed on the screen.
let message = createFileMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    file: document.getElementById('filePicker'),
  },
  onProgress: function(event) { console.log('file uploading:', event) }
});
// 2. Sends the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully.
  console.log(imResponse);
}).catch(function(imError) {
  // Message failed to send.
  console.warn('sendMessage error:', imError);
});
```

**Response**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).




### Creating custom messages

This API creates custom messages. It returns a message instance, which can be called when sending custom messages. [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) sends the message instance.
If the SDK does not provide the capability you need, use custom messages to accomplish your goals. The dice-rolling feature is one such example.

**API**

```javascript
tim.createCustomMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient. |
| `conversationType` | `String` | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` or `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container. |

`payload` has the following properties:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `data` | `String` | Custom message data |
| `description` | `String` | Custom message data |
| `extension` | `String` | Custom message data |


**Example**

```javascript
// Example: use custom messages to implement dice rolling.
// 1. Defines the random function.
function random(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}
// 2. Creates a message instance. The returned instance can be displayed on the screen.
let message = tim.createCustomMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    data: 'dice', // Denotes this message is a dice message.
    description: String(random(1,6)), // Gets the outcome.
    extension: ''
  }
});
// 3. Sends the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully.
  console.log(imResponse);
}).catch(function(imError) {
  // Message failed to send.
  console.warn('sendMessage error:', imError);
});
```

**Response**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).


### Creating video messages

This API creates video messages. It returns a message instance, which can be called when sending video messages. [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) sends the message instance. `createVideoMessage` is only compatible with WeChat Mini Programs. You can use WeChat Mini Programs to record a video message, or select a video from your album. However, Mini Programs do not return a thumbnail of the video. To improve the user experience, the SDK creates a default thumbnail for each video message. If you do not wish to display the default thumbnail, skip the part that handles thumbnail creation and implement your own solution.

>
> To make your video messages compatible with all platforms, use [the latest TUIKit or SDK](https://intl.cloud.tencent.com/document/product/1047/33996) to develop your mobile client.
>- This API requires SDK v2.2.0 or above.

**API**

```javascript
tim.createVideoMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | ---------- | ---------------------------------------------------------- |
| `to` | `String` | Message recipient. |
| `conversationType` | `String` | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` or `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Video recorded, or selected from an album. |
| `onProgress` | `function` | A function used to query the upload progress. |

**Example**

```javascript
// 1. Calls Mini Program APIs to select a video. For more information, refer to https://developers.weixin.qq.com/miniprogram/dev/api/media/video/wx.chooseVideo.html.
wx.chooseVideo({
  sourceType: ['album', 'camera'], // Select a video from an album or record one.
  maxDuration: 60, // Max. video length: 60s.
  camera: 'back', // Uses the rear camera.
  success (res) {
    // 2. Creates a message instance. The returned instance can be displayed on the screen.
    let message = tim.createVideoMessage({
      to: 'user1',
      conversationType: TIM.TYPES.CONV_C2C,
      payload: {
        file: res
      },
      onProgress: function(event) { console.log('video uploading:', event) }
    })
    // 3. Sends the message.
    let promise = tim.sendMessage(message);
    promise.then(function(imResponse) {
      // Message sent successfully.
      console.log(imResponse);
    }).catch(function(imError) {
      // Message failed to send.
      console.warn('sendMessage error:', imError);
    });
  }
})
```

**Response**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).

### Creating emoji messages

This API creates emoji messages. It returns a message instance, which can be called when sending Emoji messages. [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) sends the message instance.

> This API requires SDK v2.3.1 or above.

**API**

```javascript
tim.createFaceMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient. |
| `conversationType` | `String` | Conversation type. Valid values: `TIM.TYPES.CONV_C2C` or `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container. |

`payload` has the following properties:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `index` | `Number` | Emoji index. Customized by the user. |
| `data` | `String` | Additional data. |

**Example**

```javascript
// Emoji messages are compatible with web apps and Mini Programs.
// 1. Creates a message instance. The returned instance can be displayed on the screen.
let message = tim.createFaceMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    index: 1, // Number. The index of the emoji, customized by the user.
    data: 'tt00' // String. Additional data.
  }
});
// 2. Sends the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully.
  console.log(imResponse);
}).catch(function(imError) {
  // Message failed to send.
  console.warn('sendMessage error:', imError);
});
```

**Response**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).


### Sending messages

This API sends messages. Before sending a message, call the following APIs to create a message instance and use this API to send the message instance.
- [createTextMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage)
- [createImageMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage) 
- [createAudioMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage) 
- [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage) 
- [createCustomMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createCustomMessage)
- [createFaceMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceMessage)
- [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage)

> The SDK needs to be `ready` in order to use this API to send message instances. Use the following to monitor the SDK status:
- [TIM.EVENT.SDK_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_READY): this event is triggered when the SDK status is ready.
- [TIM.EVENT.SDK_NOT_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_NOT_READY): this event is triggered when the SDK status is not ready.


To receive one-to-one chat, group chat, group notification, or system group notification messages, you need to listen for [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).
Messages sent by this API do not trigger [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED). Messages sent by the same account from other clients (or RESTful API) trigger [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).

**API**

```javascript
tim.sendMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Sends text messages. Compatible with web apps and Mini Programs.
// 1. Sends the message instance.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully.
  console.log(imResponse);
}).catch(function(imError) {
  // Message failed to send.
  console.warn('sendMessage error:', imError);
});
```

**Response**

**Type** : `Promise`

### Recalling messages

This API recalls one-to-one chat messages and group chat messages. If the recall is successful, the value of `isRevoked` for the recalled message is set to `true`.

>
>- This API requires SDK v2.4.0 or above.
>- The recall period of a message is 2 minutes by default. You can use [the IM console](https://console.cloud.tencent.com/im-detail/login-message) to change this.
>- You can use [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) to pull recalled messages from one-to-one chat or group chat message roaming lists. Clients need to properly handle recalled messages using the `isRevoked` property. For example, once a one-to-one chat message is recalled, the client can display a message stating “The other party has recalled a message”, or “Tom has recalled a message” in group chats.
>- You also use the RESTful API to [recall one-to-one chat messages](https://intl.cloud.tencent.com/document/product/1047/35015) and [group chat messages](https://intl.cloud.tencent.com/document/product/1047/34965).

**API**

```javascript
tim.revokeMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Recalls a message.
let promise = tim.revokeMessage(message);
promise.then(function(imResponse) {
  // Message recalled successfully.
}).catch(function(imError) {
  // Failed to recall the message.
  console.warn('revokeMessage error:', imError);
});
```

```javascript
// Stores recalled messages in an array.
tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - an array of Message objects - [Message] - the isRevoked property of each Message object is true.
});
```

```javascript
// Gets a message list which contains recalled messages.
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  messageList.forEach(function(message) {
    if (message.isRevoked) {
      // Handles recalled messages.
    } else {
      // Handles normal messages.
    }
  });
});
```

**Response**

**Type** : `Promise`

### Resending messages

This API resends messages. When messages fail to send, call this API to resend them.

**API**

```javascript
tim.resendMessage(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Resends a message.
let promise = tim.resendMessage(message); // Pass the message instance that needs resending.
promise.then(function(imResponse) {
  // Message successfully resent.
  console.log(imResponse.data.message);
}).catch(function(imError) {
  // Message failed to resend.
  console.warn('resendMessage error:', imError);
});
```

**Response**

This API returns `Promise` objects:
- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupList` contains the list of groups.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



## Receiving Messages

### Receiving messages

See [MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).

This API receives messages, which is achieved by listening for events:

**Example**

```javascript
let onMessageReceived = function(event) {
  // event.data - an array that stores Message objects - [Message]
};
tim.on(TIM.EVENT.MESSAGE_RECEIVED, onMessageReceived);
```



### Parsing text messages

<ul><li><b>Simple version</b><br>
 If your text message contains only normal text, then the message is rendered as-is on the UI.</li>
<li><b>If it contains special formatted text such as [Toothy], then the formatted text is rendered as the corresponding emoji <img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">.</b>

```javascript
const emojiMap = {         // Maps formatted text to emojis.
  '[Grin]': 'emoji_0.png',
  '[Toothy]': 'emoji_1.png',
  '[Rain]': 'emoji_2.png'
}

const emojiUrl = 'http://xxxxxxxx/emoji/'   // The URL of <img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">

function parseText (payload) {
  let renderDom = []
  // Text message.
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
// Renders the array to obtain the desired UI result, such as XXX<img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">XXX<img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">XXX[Toothy XXX]
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
      return `You have withdrew from ${groupName}`
    case 9:
      return `${payload.operatorID} has made you an administrator of ${groupName}`
    case 10:
      return `${payload.operatorID} has removed you as an administrators of ${groupName}.`
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
      return `The following member(s) are now administrators: ${payload.userIDList.join(',')}`
    case this.TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN:
      return `The following member(s) are no longer administrators: ${payload.userIDList.join(',')}`
    default:
      return '[Group notification]'
  }
}
```



## Conversation APIs 

### Querying the conversation message list 

See [Conversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html).

This API queries a list of messages of the specified conversation, divided into pages. It is called when the message list is rendered for the first time after the user enters the conversation, or when “pull to see more messages” is performed.

**API**

```javascript
tim.getMessageList(options)
```

> This API can be used to “fetch message history”.

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Attributes | Default | Description |
| ------------------ | -------- | -------------- | -------------- | -------------- |
| `conversationID` | `String` | - | - | Conversation ID |
| `nextReqMessageID` | `String` | - | - | Message ID used to continue fetching messages across pages. This field can be left empty the first time messages are fetched. Every time the API is called, this field is returned, and you need to specify it for continued fetching. |
| `count` | `Number` | `<optional>` | 15 | Number of messages to be fetched. The default value and maximum value are both 15. That is, a maximum of 15 messages are returned for a single fetch. |

**Example**

```javascript
// Fetch the message list for the first time when a conversation is opened.
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list.
  const nextReqMessageID = imResponse.data.nextReqMessageID; // Pass this in for the next fetch.
  const isCompleted = imResponse.data.isCompleted; // Indicates whether all messages have been fetched.
});
```

```javascript
// Fetch the message list for the first time when a conversation is opened.
// Pull to see more messages.
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list.
  const nextReqMessageID = imResponse.data.nextReqMessageID; // Pass this in for the next fetch.
  const isCompleted = imResponse.data.isCompleted; // Indicates whether all messages have been fetched.
});
```

**Response**

This API returns `Promise` objects:
- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupList` contains the list of groups.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

### Marking conversations as read

This API is used to set the unread messages of a conversation to the read status. Messages set to the read status are not counted as unread messages. This API is called when you open or switch a conversation. If this API is not called when you open or switch a conversation, the corresponding messages remain in the unread status.

**API**

```javascript
tim.setMessageRead(options)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
// Mark all unread messages of a conversation as read.
tim.setMessageRead({conversationID: 'C2Cexample'});
```



### Querying a list of conversations

This API is used to obtain the conversation list. This API will fetch the most recent 100 conversations. You can call this API when you want to refresh the conversion list.

**API**

```javascript
tim.getConversationList()
```

**Example**

```javascript
// Fetch a list of conversations.
let promise = tim.getConversationList();
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // The new conversation list. This will overwrite the old list.
}).catch(function(imError) {
  console.warn('getConversationList error:', imError); // Information related to failures to obtain the conversation list
});
```

**Response**

This API returns `Promise` objects:
- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupList` contains the list of groups.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



### Querying conversation profiles

This API is used to obtain conversation data. When you click a conversation in the conversation list, this API is called to obtain the detailed information of the conversation.

**API**

```javascript
tim.getConversationProfile(conversationID)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
let promise = tim.getConversationProfile(conversationID);
promise.then(function(imResponse) {
  // Query succeeded. 
  console.log(imResponse.data.conversation); // Conversation profile
}).catch(function(imError) {
  console.warn('getConversationProfile error:', imError); // Information related to failures to obtain the conversation data
});
```

**Response**

This API returns `Promise` objects:
- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupList` contains the list of groups.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



### Deleting conversations

This API is used for deleting a conversation based on the conversation ID. It deletes only the conversation, without deleting messages. For example, when the conversation with user A is deleted, the previous chat messages will still be available the next time you and user A initiate a conversation.

**API**

```javascript
tim.deleteConversation(conversationID)
```

**Parameters**

`options` is an `Object`, and has the following properties:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
let promise = tim.deleteConversation('C2CExample');
promise.then(function(imResponse) {
  // Conversation successfully deleted.
  const { conversationID } = imResponse.data;// ID of the conversation to be deleted.
}).catch(function(imError) {
  console.warn('deleteConversation error:', imError); // Information related to failures to delete the conversation
});
```

**Response**

This API returns `Promise` objects:
- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupList` contains the list of groups.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).
