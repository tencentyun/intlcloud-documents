## Feature Description
* The `addAdvancedMsgListener` API is used to listen for and receive all types of messages (text, custom, and rich media messages), with the callback defined in the `V2TimAdvancedMsgListener` protocol.


## Setting a Message Listener

### Advanced message listener

#### Adding a listener
The receiver calls the `addAdvancedMsgListener` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html)) to add the advanced message listener. We recommend it be called early, such as after the chat page is initialized, to ensure timely message receiving in the application.

Sample code:


```dart
TencentImSDKPlugin.v2TIMManager.getMessageManager().addAdvancedMsgListener(
        listener: V2TimAdvancedMsgListener(
          onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},// One-to-one message read notification (a notification is received when the receiver calls `markC2CMessageAsRead`)
          onRecvMessageModified: (V2TimMessage message) {},// The message content is modified
          onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},// Message read receipt notification (if read receipts are supported, the notification is received when the receiver calls `sendMessageReadReceipts`)
          onRecvMessageRevoked: (String messageid) {},// Received a message recall notification
          onRecvNewMessage: (V2TimMessage message) {},// Received a new message
          onSendMessageProgress: (V2TimMessage message, int progress) {},// Message upload progress event
        ),
);
```


#### Removing a listener
To stop receiving messages, the receiver can call `removeAdvancedMsgListener` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/removeAdvancedMsgListener.html)) to remove the advanced message listener.

Sample code:


```dart
// Create a listener
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {},
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
// Register the listener
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
// Remove the listener
TencentImSDKPlugin.v2TIMManager.getMessageManager().removeAdvancedMsgListener(listener: listener);
```



## Receiving a Text Message

The receiver can receive a one-to-one or group text message by using the advanced message listener in the following steps:
1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` callback ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnRecvNewMessageCallback.html)) to receive text messages.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // Process the text message
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT){
        String text = message.textElem.text;
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



## Receiving a Custom Message

The receiver can receive a custom one-to-one or group message by using the advanced message listener in the following steps:
1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` callback ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnRecvNewMessageCallback.html)) to receive custom messages.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // Use the custom message
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM){
        String data = message.customElem.data;
        String desc = message.customElem.desc;
        String ext = message.customElem.extension;
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



## Receiving a Rich Media Message
The receiver can receive a rich media message **only by using** the advanced message listener in the following steps:
1. Call the `addAdvancedMsgListener` API to set the advanced message listener.
2. Listen for the `onRecvNewMessage` callback ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnRecvNewMessageCallback.html)) to receive the `V2TimMessage` message.
3. Parse the `elemType` attribute in the `V2TIMMessage` message and then parse the message again according to the type to get the specific content of the elements in the message.
4. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.


### Image message

The image in an image message can be in three formats: original, large, and thumbnail. The latter two are automatically generated by the SDK during message sending and can be ignored.
Large image: A large image is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 720 pixels.
Thumbnail: A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 198 pixels.

The SDK for Flutter will download the image message when free, which can be directly used by you and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the image content from `V2TimMessage`:



```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // Use the image message
      if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE) {
        String path = message
            .imageElem.path; // Image upload path. This field applies only to the message sender who can use it to display the image on the screen in advance to optimize the experience
        for (var item in message.imageElem.imageList) { // Traverse large images, original images, and thumbnails
          // Parse the image attribute
          int height = item.height;
          String localUrl = item.localUrl;
          int size = item.size;
          int type = item.type; // Large image, thumbnail, or original image
          String url = item.url;
          String uuid = item.uuid;
          int width = item.width;
        }
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



### Video message

After a video message is received, a video preview is displayed on the chat page, and the video is played back after the user clicks the message.
Two steps are required:

The SDK for Flutter will download video messages when free, which can be directly used by you and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the video content from `V2TimMessage`:



```dart
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO){
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

The SDK for Flutter will download audio messages when free, which can be directly used by you and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the audio content from `V2TimMessage`:



```dart
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND){
  			// Parse the audio message, such as audio playback address, local address, size, and duration
        message.soundElem.UUID;
        message.soundElem.dataSize;
        message.soundElem.duration;
        message.soundElem.localUrl;
        message.soundElem.url;
        // ...
}
```


### File message

The SDK for Flutter will download file messages when free, which can be directly used by developers and will be cleared when the application is uninstalled.

The following sample code demonstrates how to parse the file content from `V2TimMessage`:



```dart

if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE){
  			// Parse the file message, such as filename, size, URL, etc. of the file message
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



```dart

if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION){
  			// Parse the geographical location information such as latitude, longitude, and description
        message.locationElem.desc;
        message.locationElem.latitude;
        message.locationElem.longitude;
}
```


### Emoji message

The SDK provides a passthrough channel only for emoji messages. For message content fields, see the definition of `faceElem` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimFaceElem.html)). Here, `index` and `data` can be customized.

For example, the sender can set `index` to `1` and `data` to `x12345` to indicate the smile emoji.
The receiver parses the received emoji message as `1` and `x12345` and displays the message as the smile emoji according to the preset rules.

The following sample code demonstrates how to parse the emoji content from `V2TIMMessage`:


```dart
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
        message.faceElem.data;
        message.faceElem.index;
}
```


### Group tip message

Group tip messages are tips received by users in addition to ordinary messages in a group chat, for example, "The admin removed Alice from the group chat" and "Bob renamed the group "xxxx"".

> ? Group tip messages will be received by only group members but not one-to-one chat parties.

There are many types of group tip messages. For more information, see the definition of `V2TIMGroupTipsType` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupTipsElem.html)).

After receiving a group tip message, the receiver generally needs to:
1. Parse each field in `V2TIMGroupTipsElem`.
2. Identify the message type according to `type`.
3. Merge other fields into the content for display according to the type.

For example:
The receiver parses `type` as `V2TIM_GROUP_TIPS_TYPE_GROUP_INFO_CHANGE`, indicating that this is a notification of group profile change.
The receiver can get the operator information from `opMember` and the modified group name from `groupChangeInfoList`.
At this point, the receiver can merge the "operator" and "modified group name" to create a group tip, such as "Alice renamed the group "group123"".

The following sample code demonstrates how to parse the tip content from `V2TIMMessage`:



```dart
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS){
        message.groupTipsElem.groupID; // Group
        message.groupTipsElem.type; // Group tip type
        message.groupTipsElem.opMember; // Operator profile
        message.groupTipsElem.memberList; // User profile being operated
        message.groupTipsElem.groupChangeInfoList; // Group information change details
        message.groupTipsElem.memberChangeInfoList; // Group member change information
        message.groupTipsElem.memberCount; // Number of current online group members
}
```


## Receiving a Message Containing Multiple Elements

1. Parse the first element object through the Message object.
2. Get the next element object through the `nextElem` method of the first element object. If the next object exists, an element object instance is returned; otherwise, `null` is returned.

Sample code:


```dart
if(message.textElem.nextElem!=null){
   // There is a next message.
}
```



