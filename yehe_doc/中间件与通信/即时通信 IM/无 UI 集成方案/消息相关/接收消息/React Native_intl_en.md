## Feature Description

- All types of messages (text, custom, and rich media messages) are listened for and received with the `addAdvancedMsgListener` API, with the callbacks defined in the protocol of `V2TimAdvancedMsgListener`.

## Setting Message Listeners

### Advanced message listener

#### Adding a listener

The receiver calls the `addAdvancedMsgListener` ([TS](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/addAdvancedMsgListener.html)) API to add the advanced message listener. It is recommended to call the API early (such as after the chat page is initialized) to ensure timely message receiving in the application.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

TencentImSDKPlugin.v2TIMManager.getMessageManager().addAdvancedMsgListener(
        {
          onRecvC2CReadReceipt: ( receiptList) {},// The one-to-one message read notification (a notification is received when the receiver calls `markC2CMessageAsRead`).
          onRecvMessageModified: ( message) {},// The message content is modified.
          onRecvMessageReadReceipts: ( receiptList) {},// The message read receipt notification (if read receipts are supported, the notification is received when the receiver calls `sendMessageReadReceipts`).
          onRecvMessageRevoked: ( messageid) {},// Received a message recall notification.
          onRecvNewMessage: ( message) {},// Received a new message.
          onSendMessageProgress: ( message,  progress) {},// The message upload progress event.
        }
);
```

#### Removing a listener

To stop receiving messages, the receiver calls `removeAdvancedMsgListener` ([TS](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/removeAdvancedMsgListener.html)) to remove the advanced message listener.

Sample code:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

// Create a listener
const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {},
    onSendMessageProgress: (message, progress) {},
  };
// Register the listener
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
// Remove the listener
TencentImSDKPlugin.v2TIMManager.getMessageManager().removeAdvancedMsgListener(listener);
```

## Receiving Text Messages

The receiver can receive a one-to-one or group text message with the advanced message listener in the following steps:

1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` ([TS](https://comm.qq.com/im/doc/RN/en/Callback/OnRecvNewMessage.html)) callback that contains the text message.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:

```javascript

import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT){
        const text = message.textElem.text;
      }
    },
    onSendMessageProgress: (message, progress) {},
  };
TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
```

## Receiving Custom Messages

The receiver can receive a custom one-to-one or group message with the advanced message listener in the following steps:

1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` ([TS](https://comm.qq.com/im/doc/RN/en/Callback/OnRecvNewMessage.html)) callback that contains the custom message.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:

```javascript
import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM){
        const text = message.textElem.text;
        const data = message.customElem.data;
        const desc = message.customElem.desc;
        const ext = message.customElem.extension;
      }
    },
    onSendMessageProgress: (message, progress) {},
  };
TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
```

## Receiving Rich Media Messages

The receiver can receive a rich media message **only with** the advanced message listener in the following steps:

1. Call the `addAdvancedMsgListener` API to set the advanced message listener.
2. Listen for the `onRecvNewMessage` ([TS](https://comm.qq.com/im/doc/RN/en/Callback/OnRecvNewMessage.html)) callback to get the `V2TimMessage` message.
3. Parse the `elemType` attribute in the `V2TIMMessage` message, and then parse the message again according to the type to get the specific content of the elements in the message.
4. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

### Image message

The image in an image message can be in three formats: original, large, and thumbnail. The latter two are automatically generated by the SDK during message sending and can be ignored.
`Large` (large image): A large image is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 720 pixels.
`Thumb` (thumbnail): A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 198 pixels.

The React Native SDK will download the image message when free, which can be directly used by you and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the image content from `V2TimMessage`:

```javascript
import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE){
        const path = message
            .imageElem.path; // Image upload path. This field applies only to the message sender who can use it to display the image on the screen in advance to optimize the experience
        message.imageElem.imageList.map(item => { // // Traverse large images, original images, and thumbnails
          // Parse the image attribute
          const height = item.height;
          const localUrl = item.localUrl;
          const size = item.size;
          const type = item.type; // Large image, thumbnail, or original image
          const url = item.url;
          const uuid = item.uuid;
          const width = item.width;
        })
      }
    },
    onSendMessageProgress: (message, progress) {},
  };
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```

### Video message

After a video message is received, a video preview is displayed on the chat page, and the video is played back after the user clicks the message.
Two steps are required:

The React Native SDK will download video messages when free, which can be directly used by you and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the video content from `V2TimMessage`:

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO) {
  // Parse the video message attributes such as thumbnail, playback address, width and height, and size
  message.videoElem.UUID;
  message.videoElem.duration;
  message.videoElem.localSnapshotUrl;
  message.videoElem.localVideoUrl;
  message.videoElem.snapshotHeight;
  message.videoElem.snapshotPath;
  // ...
}
```

### Audio message

The React Native SDK will download audio messages when free, which can be directly used by you and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the audio content from `V2TimMessage`:

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND) {
  // Parse the playback address, local address, size, and duration of the audio message.
  message.soundElem.UUID;
  message.soundElem.dataSize;
  message.soundElem.duration;
  message.soundElem.localUrl;
  message.soundElem.url;
  // ...
}
```

### File message

The React Native SDK will download file messages when free, which can be directly used by you and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the file content from `V2TimMessage`:

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE) {
  // Parse the filename, size, URL and other info of the file message
  message.fileElem.UUID;
  message.fileElem.fileName;
  message.fileElem.fileSize;
  message.fileElem.localUrl;
  message.fileElem.path;
  message.fileElem.url;
}
```

### Geographical location message

After receiving the geographical location message, the receiver can parse the latitude and longitude information directly from `locationElem`.
The following sample code demonstrates how to parse the geographical location content from `V2TimMessage`:

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION) {
  // Parse the geographical location information such as latitude, longitude, and description
  message.locationElem.desc;
  message.locationElem.latitude;
  message.locationElem.longitude;
}
```

### Emoji message

The SDK only provides a message passthrough channel for an emoji message. For message content fields, see `faceElem` ([TS](https://comm.qq.com/im/doc/RN/en/Interface/Message/V2TimFaceElem.html)), where the contents of `index` and `data` are customized by the user.

For example, the sender can set `index` to `1` and `data` to `x12345` to indicate the smile emoji.
The receiver parses the received emoji message as `1` and `x12345` and displays the message as the smile emoji according to the preset rules.

The following sample code demonstrates how to parse the emoji content from `V2TIMMessage`:

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
  message.faceElem.data;
  message.faceElem.index;
}
```

### Group tip message

Group tip messages are tips received by users other than ordinary messages in a group chat, such as "The admin removed alice from the group chat" and "bob renamed the group "xxxx"".

> ? Group tip messages apply to group members only.

There are several types of group tip messages, as stated in `V2TIMGroupTipsElem` ([TS](https://comm.qq.com/im/doc/RN/en/Interface/Message/V2TimGroupTipsElem.html)).

After receiving a group tip message, the receiver generally needs to:

1. Parse all fields in `V2TIMGroupTipsElem`.
2. Identify the message type according to `type`.
3. Merge other fields into the content for display according to the type.

Example:
`V2TIM_GROUP_TIPS_TYPE_GROUP_INFO_CHANGE` is parsed from the `type`, indicating that this is a notification of group profile change.
The receiver can get the operator information from `opMember` and the new group name from `groupChangeInfoList`.
At this point, the receiver can merge the "operator" and "new group name" to create a group tip, such as "Alice renamed the group as "group123"".

The following sample code demonstrates how to parse the tip content from `V2TIMMessage`:

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS) {
  message.groupTipsElem.groupID; // Group
  message.groupTipsElem.type; // Group tip type
  message.groupTipsElem.opMember; // Operator profile
  message.groupTipsElem.memberList; // User profile being operated
  message.groupTipsElem.groupChangeInfoList; // Group information change details
  message.groupTipsElem.memberChangeInfoList; // Group member change information
  message.groupTipsElem.memberCount; // Number of current online group members
}
```

## Receiving Messages Containing Multiple Element Objects

1. Parse the first element object from the `Message` object.
2. Get the next element object through the `nextElem` method of the first element object. If the next object exists, an element object instance is returned; otherwise, `null` is returned.

Sample code:

```javascript
if (message.textElem.nextElem != null) {
  // There is a next element
}
```


