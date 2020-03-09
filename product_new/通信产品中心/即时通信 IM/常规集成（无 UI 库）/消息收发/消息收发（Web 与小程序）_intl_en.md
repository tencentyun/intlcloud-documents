## Sending Messages

### Creating text messages
This API is used for creating text messages. It returns a message instance. When you want to send a text message, call the API [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.


**API name**

```javascript
tim.createTextMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient |
| `conversationType` | `String` | Conversation type. Possible values are `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container |

`payload` is described in the following table:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `text` | `String` | Message text content |



**Example**

```javascript
// Send a text message. This is same for web applications and mini programs.
// 1. Create a message instance. The instance returned by the API can be displayed on the screen.
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    text: 'Hello world!'
  }
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send
  console.warn('sendMessage error:', imError);
});
```

**Return**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html)



### Creating image messages
This API is used for creating image messages. It returns a message instance. When you want to send an image message, call the API [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.


**API**

```javascript
tim.createImageMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient |
| `conversationType` | `String` | Conversation type. Possible values are `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container |

The description of `payload` is shown in the following table:

| Name | Type | Description |
| ---- | --------------------------- | ------------------------------------------------------------ |
| file | `HTMLInputElement or Object` | This is used to choose the DOM node (Web), or File object (Web), or the `success` callback parameters for the WeChat Mini Program `wx.chooseImage` API for an image. The SDK reads the data and uploads an image. |

**Web example**

```javascript
// The web application sends an image message.
// 1. Create a message instance. The instance returned by the API can be displayed on the screen.
let message = tim.createImageMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    file: document.getElementById('imagePicker'),
  },
  onProgress: function(event) { console.log('file uploading:', event) }
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send
  console.warn('sendMessage error:', imError);
});
```

**Mini program example**

```javascript
// The mini program sends an image.
// 1. Select an image.
wx.chooseImage({
  sourceType: ['album'], // Select an image from an album.
  count: 1, // Select only one image. Currently, the SDK does not support sending multiple images at a time.
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
      // Sent successfully
      console.log(imResponse);
    }).catch(function(imError) {
      // Failed to send
      console.warn('sendMessage error:', imError);
    });
  }
})
```

**Return**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html)


### Creating audio messages
This API is used for creating audio message instances. It returns a message instance. To send an audio message, call the API [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance. Currently, createAudioMessage can only be used in the WeChat Mini Program environment.

> Audio messages can be sent throughout the platform. When using mobile terminals, use the [latest TUIKit or SDK](https://cloud.tencent.com/document/product/269/36887).

**API**

```javascript
tim.createAudioMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | --------------------- |
| `to` | `String` | Message recipient |
| `conversationType` | `String` | Conversation type. Possible values are `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container |

The description of `payload` is shown in the following table:

| Name | Type | Description |
| ---- | --------------------------- | ------------ |
| file | `Object` | File information obtained after recording |

**Mini program example**

<pre>
// Example: use WeChat’s official RecorderManager for recording. For more information, see <a href="https://developers.weixin.qq.com/minigame/dev/api/media/recorder/RecorderManager.start.html">RecorderManager.start(Object object)</a>.
// 1. Obtain the globally unique RecorderManager.
const recorderManager = wx.getRecorderManager();

// Some recording parameters
const recordOptions = {
  duration: 60000, // Recording duration in ms. The maximum value is 600,000 ms (10 minutes).
  sampleRate: 44100, // Sample rate
  numberOfChannels: 1, // Number of recording channels
  encodeBitRate: 192000, // Encoding bit rate
  format: 'aac' // Audio format. Audio messages created in this format can be sent throughout the IM platform (for Android, iOS, WeChat Mini Program, and web).
};

// 2.1 Monitor recording error events.
recorderManager.onError(function(errMsg) {
  console.warn('recorder error:', errMsg);
});
// 2.2 Monitor recording end events. After recording is finished, call createAudioMessage to create an audio message instance.
recorderManager.onStop(function(res) {
  console.log('recorder stop', res);

  // 4. Create a message instance. The instance returned by the API can be displayed on the screen.
  const message = tim.createAudioMessage({
    to: 'user1',
    conversationType: TIM.TYPES.CONV_C2C,
    payload: {
      file: res
    }
  });

  // 5. Send the message.
  let promise = tim.sendMessage(message);
  promise.then(function(imResponse) {
    // Sent successfully
    console.log(imResponse);
  }).catch(function(imError) {
    // Failed to send
    console.warn('sendMessage error:', imError);
  });
});

// 3. Start recording.
recorderManager.start(recordOptions);
</pre>

**Return**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html)

### Creating file messages
This API is used for creating file messages. It returns a message instance. To send a file message, call the API [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.

> Currently, WeChat Mini Programs do not support the file selection feature, so this API currently does not support WeChat Mini Programs.

**API**

```javascript
tim.createFileMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `to` | `String` | Message recipient |
| `conversationType` | `String` | Conversation type. Possible values are `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container |
| `onProgress` | `function` | Callback function for obtaining the upload progress |

`payload` is described in the following table:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `file` | `HTMLInputElement` | This is used to choose the DOM node (web) or File object (web) for a file. The SDK reads the data and uploads a file. |

**Example**

```javascript
// Send a file message.
// 1. Create a file message instance. The instance returned by the API can be displayed on the screen.
let message = createFileMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    file: document.getElementById('filePicker'),
  },
  onProgress: function(event) { console.log('file uploading:', event) }
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send
  console.warn('sendMessage error:', imError);
});
```

**Return**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html)




### Creating custom messages

This API is used for creating custom message instances. It returns a message instance. To send a custom message, call the API [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance.
When the capabilities provided by the SDK cannot meet your needs, you can use custom messages to implement customized features, such as the dice-rolling feature.

**API**

```javascript
tim.createCustomMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient |
| `conversationType` | `String` | Conversation type. Possible values are `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container |

`payload` is described in the following table:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `data` | `String` | Data field of the custom message |
| `description` | `String` | Data field of the custom message |
| `extension` | `String` | Data field of the custom message |


**Example**

```javascript
// Example: use custom messages to implement the dice-rolling feature.
// 1. Define a random function.
function random(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}
// 2. Create a message instance. The instance returned by the API can be displayed on the screen.
let message = tim.createCustomMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    data: 'dice', // Indicate whether the message is a dice-type message
    description: String(random(1,6)), // Obtain the dice number
    extension: ''
  }
});
// 3. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send
  console.warn('sendMessage error:', imError);
});
```

**Return**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html)


### Creating video messages

This API is used for creating video message instances. It returns a message instance. To send a video message, call the API [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message instance. Currently, `createVideoMessage` can only be used in the WeChat Mini Program environment. For videos recorded by WeChat Mini Programs or video files selected from the album, no video thumbnail information is returned. To improve the user experience, the SDK sets the default thumbnail information when creating a video message. If the access side does not want the default thumbnail to be displayed, it can ignore relevant thumbnail information during rendering as needed.

> Video messages can be sent throughout the platform. When using mobile terminals, use the [latest TUIKit or SDK](https://cloud.tencent.com/document/product/269/36887).

**API**

```javascript
tim.createVideoMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | ---------- | ---------------------------------------------------------- |
| `to` | `String` | Message recipient |
| `conversationType` | `String` | Conversation type. Possible values are `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Video file recorded or selected from the album
| `onProgress` | `function` | Callback function for obtaining the upload progress |

**Example**

```javascript
// 1. Call the mini program API to select a video. For details on the API, visit https://developers.weixin.qq.com/miniprogram/dev/api/media/video/wx.chooseVideo.html.
wx.chooseVideo({
  sourceType: ['album', 'camera'], // Video source. The video can be selected from an album or recorded.
  maxDuration: 60, // Maximum duration, which is 60 seconds
  camera: 'back', // Rear camera
  success (res) {
    // 2. Create a message instance. The instance returned by the API can be displayed on the screen.
    let message = tim.createVideoMessage({
      to: 'user1',
      conversationType: TIM.TYPES.CONV_C2C,
      payload: {
        file: res
      },
      onProgress: function(event) { console.log('video uploading:', event) }
    })
    // 3. Send the message.
    let promise = tim.sendMessage(message);
    promise.then(function(imResponse) {
      // Sent successfully
      console.log(imResponse);
    }).catch(function(imError) {
      // Failed to send
      console.warn('sendMessage error:', imError);
    });
  }
})
```

**Return**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html)

### Creating emoji messages

This API is used for creating emoji message instances. It returns a message instance. To send an emoji message, call the API [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) to send the message.

**API**

```javascript
tim.createFaceMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------ |
| `to` | `String` | Message recipient |
| `conversationType` | `String` | Conversation type. Possible values are `TIM.TYPES.CONV_C2C` and `TIM.TYPES.CONV_GROUP`. |
| `payload` | `Object` | Message content container |

`payload` is described in the following table:

| Name | Type | Description |
| ------ | -------- | ------------ |
| `index` | `Number` | User-defined emoji index |
| `data` | `String` | Extra data |

**Example**

```javascript
// Send an emoji message. This is same for web applications and mini programs.
// 1. Create a message instance. The instance returned by the API can be displayed on the screen.
let message = tim.createFaceMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  payload: {
    index: 1, // Index number of the emoji, which is defined by users
    data: 'tt00' // String Extra data
  }
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send
  console.warn('sendMessage error:', imError);
});
```

**Return**

Message instance [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html)


### Sending messages

This API is used for sending messages. You need to first call one of the following APIs for creating message instances to obtain a message instance and then call this API to send the message instance.
- [Create a text message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage)
- [Create an image message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage)
- [Create an audio message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage)
- [Create a video message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage)
- [Create a custom message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createCustomMessage)
- [Create an emoji message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceVMessage)
- [Create a file message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage)

> To call this API to send a message instance, the SDK needs to be in the ready state. Otherwise, the message instance cannot be sent. The SDK state can be obtained by monitoring the following events:
- [TIM.EVENT.SDK_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_READY): is triggered when the SDK is in the ready state.
- [TIM.EVENT.SDK_NOT_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_NOT_READY): is triggered when the SDK is in the not ready state.


To receive new one-to-one messages, group messages, group notification messages, and group system notification messages that are published, you need to monitor the event [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).
Messages sent by this instance do not trigger the event [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED). Messages sent by the same account from other terminals (or through a RESTful API) trigger the event [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).

**API**

```javascript
tim.sendMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Send a text message. This is same for web applications and mini programs.
// 1. Send the generated message instance.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Sent successfully
  console.log(imResponse);
}).catch(function(imError) {
  // Failed to send
  console.warn('sendMessage error:', imError);
});
```

**Return**

**Type** : `Promise`

### Recalling messages

This API is used for recalling a one-to-one chat message or group chat message. After the message is recalled, the `isRevoked` value of the message is `true`.

>
>- The default time frame for recalling a message is 2 minutes. You can set this time frame in the [console](https://console.cloud.tencent.com/im-detail/login-message).
>- The recalled message can be fetched from one-to-one chat message or group chat message roaming by calling the API [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList). The access side needs to properly handle the display of the recalled message based on the isRevoked attribute of the message object. For example, in a one-to-one conversation, it can be displayed as "The user recalled a message". In a group conversation, it can be displayed as "Tom recalled a message".
>- You can call RESTful APIs of [recalling a one-to-one chat message](https://cloud.tencent.com/document/product/269/38980) or [recalling a group chat message](https://cloud.tencent.com/document/product/269/12341) to recall a message.

**API**

```javascript
tim.revokeMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Actively recall a message
let promise = tim.revokeMessage(message);
promise.then(function(imResponse) {
  // Recalled the message successfully
}).catch(function(imError) {
  // Failed to recall the message
  console.warn('revokeMessage error:', imError);
});
```

```javascript
// Received the message recall notification
tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - Array for storing message objects - [Message] - The isRevoked value of each message object is true.
});
```

```javascript
// A message is recalled when you attempt to obtain the message list of a conversation.
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  messageList.forEach(function(message) {
    if (message.isRevoked) {
      // Process a recalled message
    } else {
      // Process a common message
    }
  });
});
```

**Return**

**Type** : `Promise`

### Resending messages

This API is used for resending messages. When a message fails to be sent, you can call this API to resend the message.

**API**

```javascript
tim.resendMessage(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `message` | `Message` | Message instance |

**Example**

```javascript
// Resend a message
let promise = tim.resendMessage(message); // Pass in the message instance to be resent
promise.then(function(imResponse) {
  // Resent successfully
  console.log(imResponse.data.message);
}).catch(function(imError) {
  // Failed to resend
  console.warn('resendMessage error:', imError);
});
```

**Return**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The group list can be obtained from `IMResponse.data.groupList`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



## Receiving Messages

### Receiving messages

See the [Message Receiving Event](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).

This API is used for receiving messages. To receive messages, you need to monitor the corresponding event:

**Example**

```javascript
let onMessageReceived = function(event) {
  // event.data - Array for storing message objects - [Message]
};
tim.on(TIM.EVENT.MESSAGE_RECEIVED, onMessageReceived);
```



### Parsing text messages

<ul><li><b>Simple version</b><br>
 If your text message contains only words, you can directly render words `'xxxxxxx'` on the UI.</li>
<li><b>The content containing [Grin] needs to be parsed into the text for <img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">.</b>

```javascript
const emojiMap = {         // Path that is matched with [Grin]
  '[Smile]': 'emoji_0.png',
  '[Grin]': 'emoji_1.png',
  '[Rain]': 'emoji_2.png'
}

const emojiUrl = 'http://xxxxxxxx/emoji/'   // Address of the image <img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">

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
            if (emojiMap[_emoji]) {    // If you need to render an emoji, you need to match the emoji [Grin] with the corresponding emoji address.
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


// The structure of renderDom at the end is [{name: 'text', text: 'XXX'}, {name: 'img', src: 'http://xxx'}......].
// By rendering the current array, you can obtain the desired UI result, for example: XXX<img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">XXX<img src="https://main.qcloudimg.com/raw/6be88c30a4552b5eb93d8eec243b6593.png"  style="margin:0;">XXX[Grin XXX].
```
</li></ul>


### Parsing system messages

```javascript
function parseGroupSystemNotice (payload) {
  const groupName =
      payload.groupProfile.groupName || payload.groupProfile.groupID
  switch (payload.operationType) {
    case 1:
      return `${payload.operatorID} applies for joining the group: ${groupName}`
    case 2:
      return `Successfully joined the group: ${groupName}`
    case 3:
      return `Application for joining the group: ${groupName} is rejected`
    case 4:
      return `Removed by ${payload.operatorID} from the group: ${groupName}`
    case 5:
      return `The group named ${groupName} has been dismissed by ${payload.operatorID}`
    case 6:
      return `${payload.operatorID} created the group: ${groupName}`
    case 7:
      return `${payload.operatorID} invites you to join the group: ${groupName}`
    case 8:
      return `You have quit the group: ${groupName}`
    case 9:
      return `You have been designated by ${payload.operatorID} as an admin of the group: ${groupName}`
    case 10:
      return `${payload.operatorID} has revoked your role as the admin of the group: ${groupName}`
    case 255:
      return 'Custom group system notification'
  }
}
```



### Parsing group notification messages

```javascript
function parseGroupTipContent (payload) {
  switch (payload.operationType) {
    case this.TIM.TYPES.GRP_TIP_MBR_JOIN:
      return `Group member: ${payload.userIDList.join(',')}, joined the group`
    case this.TIM.TYPES.GRP_TIP_MBR_QUIT:
      return `Group member: ${payload.userIDList.join(',')}, quit the group`
    case this.TIM.TYPES.GRP_TIP_MBR_KICKED_OUT:
      return `Group member: ${payload.userIDList.join(',')}, was removed by ${payload.operatorID} from the group`
    case this.TIM.TYPES.GRP_TIP_MBR_SET_ADMIN:
      return `Group member: ${payload.userIDList.join(',')}, became an admin`
    case this.TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN:
      return `Group member: ${payload.userIDList.join(',')}, was revoked from the role of admin`
    default:
      return '[Group notification message]'
  }
}
```



## Conversations

### Obtaining the message list of a conversation 

See [Conversation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html).

This API is used for fetching the message list of a specified conversation on different pages. This API needs to be called when first rendering the message list when users enter the conversation or when users "page down to view more messages".

**API**

```javascript
tim.getMessageList(options)
```

> This API can be used to "fetch historical messages".

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Attributes | Default | Description |
| ------------------ | -------- | -------------- | -------------- | -------------- |
| `conversationID` | `String` | - | - | Conversation ID |
| `nextReqMessageID` | `String` | - | - | Message ID that is used to continue fetching messages across pages. This field can be left empty the first time messages are fetched. Every time the API is called, this field is returned, and you need to specify it for continuous fetching. |
| `count` | `Number` | `<optional>` | 15 | Number of messages to be fetched. The default value and maximum value are both 15. That is, a maximum of 15 messages are returned for a single fetch. |

**Example**

```javascript
// Fetch the message list for the first time after opening a conversation
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This is used to continuously fetch messages. This field needs to be passed in to continue fetching messages across pages.
  const isCompleted = imResponse.data.isCompleted; // Indicate whether all messages have been fetched
});
```

```javascript
// Fetch the message list for the first time after opening a conversation
// You can view more messages by paging down
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This is used to continuously fetch messages. This field needs to be passed in to continue fetching messages across pages.
  const isCompleted = imResponse.data.isCompleted; // Indicate whether all messages have been fetched
});
```

**Return**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The group list can be obtained from `IMResponse.data.groupList`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

### Setting a conversation as read

This API is used to set the unread messages of a conversation as read. Messages set as read are not counted as unread messages. This API is called when you open or switch a conversation. If this API is not called when you open or switch a conversation, the corresponding messages remain in the unread state.

**API**

```javascript
tim.setMessageRead(options)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
// Report that all unread messages in a conversation have been read
tim.setMessageRead({conversationID: 'C2Cexample'});
```



### Obtaining the conversation list

This API is used to obtain the conversation list. It fetches the most recent 100 conversations. You can call this API when you want to refresh the conversion list.

**API**

```javascript
tim.getConversationList()
```

**Example**

```javascript
// Fetch the conversation list
let promise = tim.getConversationList();
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // Conversation list, which will be used to overwrite the original conversation list
}).catch(function(imError) {
  console.warn('getConversationList error:', imError); // Information about failures to obtain the conversation list
});
```

**Return**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The group list can be obtained from `IMResponse.data.groupList`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



### Obtaining conversation information

This API is used to obtain conversation information. When you click a conversation in the conversation list, this API is called to obtain the detailed information of the conversation.

**API**

```javascript
tim.getConversationProfile(conversationID)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
let promise = tim.getConversationProfile(conversationID);
promise.then(function(imResponse) {
  // Obtained successfully
  console.log(imResponse.data.conversation); // Conversation information
}).catch(function(imError) {
  console.warn('getConversationProfile error:', imError); // Information about failures to obtain the conversation information
});
```

**Return**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The group list can be obtained from `IMResponse.data.groupList`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).



### Deleting conversations

This API is used for deleting a conversation based on the conversation ID. It deletes only the conversation, without deleting messages. For example, when the conversation with user A is deleted, the previous chat messages will still be available the next time you and user A initiate a conversation.

**API**

```javascript
tim.deleteConversation(conversationID)
```

**Parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| ------------------ | -------- | -------------- |
| `conversationID` | `String` | Conversation ID |

**Example**

```javascript
let promise = tim.deleteConversation('C2CExample');
promise.then(function(imResponse) {
  // Deleted successfully
  const { conversationID } = imResponse.data;// ID of the deleted conversation
}).catch(function(imError) {
  console.warn('deleteConversation error:', imError); // Information about failures to delete the conversation
});
```

**Return**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The group list can be obtained from `IMResponse.data.groupList`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).
