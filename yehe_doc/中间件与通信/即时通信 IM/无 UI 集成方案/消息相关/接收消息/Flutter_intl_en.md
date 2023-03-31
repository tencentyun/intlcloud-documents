## Overview
All types of messages (text, custom, and rich media messages) are listened for and received with the `addAdvancedMsgListener` API, with the callbacks defined in the protocol of `V2TimAdvancedMsgListener`.


## Setting Message Listeners

### Advanced message listener

#### Adding a listener
The receiver calls the `addAdvancedMsgListener` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html)) to add the advanced message listener. It is recommended to call the API early (such as after the chat panel is initialized) to ensure timely message receiving in the application.

Sample code:


```dart
    // Create a message listener
    V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
      onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {
        // Callback after marking a one-to-one message as read
      },
      onRecvMessageModified: (V2TimMessage message) {
        // `msg` is the modified message object
      },
      onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {
        // Callback after marking a group message as read
        receiptList.forEach((element) {
          element.groupID;  // Group ID
          element.msgID; // Message ID
          element.readCount;// Latest group message read count
          element.unreadCount;// Latest group message unread count
          element.userID; //  ID of the other party of the one-to-one message
        });
      },
      onRecvMessageRevoked: (String messageid) {
        // Process the recalled messages among locally maintained messages
      },
      onRecvNewMessage: (V2TimMessage message) async {
        // Process a text message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT) {
          message.textElem?.text;
        }
        // Use a custom message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM) {
          message.customElem?.data;
          message.customElem?.desc;
          message.customElem?.extension;
        }
        // Use an image message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE) {
          message.imageElem
              ?.path; // Image upload path. This field applies only to the message sender who can use it to display the image on the screen in advance to optimize the experience
          message.imageElem?.imageList?.forEach((element) {
            // Traverse large images, original images, and thumbnails
            // Parse image attributes
            element?.height;
            element?.localUrl;
            element?.size;
            element?.type; // Large image, original image, or thumbnail
            element?.url;
            element?.uuid;
            element?.width;
          });
        }
        // Process a video message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO) {
          // Parse the video message attributes such as thumbnail, playback address, width and height, and size
          message.videoElem?.UUID;
          message.videoElem?.duration;
          message.videoElem?.localSnapshotUrl;
          message.videoElem?.localVideoUrl;
          message.videoElem?.snapshotHeight;
          message.videoElem?.snapshotPath;
          // ...
        }
        // Process an audio message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND) {
          // Parse the playback address, local address, size, and duration of the audio message.
          message.soundElem?.UUID;
          message.soundElem?.dataSize;
          message.soundElem?.duration;
          message.soundElem?.localUrl;
          message.soundElem?.url;
          // ...
        }
        // Process a file message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE) {
          // Parse the filename, size, URL and other info of the file message
          message.fileElem?.UUID;
          message.fileElem?.fileName;
          message.fileElem?.fileSize;
          message.fileElem?.localUrl;
          message.fileElem?.path;
          message.fileElem?.url;
        }
        // Process a location message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION) {
          // Parse the geographical location information such as latitude, longitude, and description
          message.locationElem?.desc;
          message.locationElem?.latitude;
          message.locationElem?.longitude;
        }
        // Process an emoji message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
          message.faceElem?.data;
          message.faceElem?.index;
        }
        // Process a group tip text message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS) {
          message.groupTipsElem?.groupID; // Group
          message.groupTipsElem?.type; // Group tip type
          message.groupTipsElem?.opMember; // Operator profile
          message.groupTipsElem?.memberList; // User profile being operated
          message.groupTipsElem?.groupChangeInfoList; // Group information change details
          message.groupTipsElem?.memberChangeInfoList; // Group member change information
          message.groupTipsElem?.memberCount; // Number of current online group members
        }
        // Process a combined message
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_MERGER) {
          message.mergerElem?.abstractList;
          message.mergerElem?.isLayersOverLimit;
          message.mergerElem?.title;
          V2TimValueCallback<List<V2TimMessage>> download =
              await TencentImSDKPlugin.v2TIMManager
                  .getMessageManager()
                  .downloadMergerMessage(
                    msgID: message.msgID!,
                  );
          if (download.code == 0) {
            List<V2TimMessage>? messageList = download.data;
          }
        }
        if (message.textElem?.nextElem != null) {
          // Get the next element object through the `nextElem` method of the first element object. If the next object exists, an element object instance is returned; otherwise, `null` is returned.
        }
      },
      onSendMessageProgress: (V2TimMessage message, int progress) {
        // File upload progress callback
      },
    );
    // Add an event listener for advanced messages
    TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .addAdvancedMsgListener(listener: listener);
```


#### Removing a listener
To stop receiving messages, the receiver calls `removeAdvancedMsgListener` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/removeAdvancedMsgListener.html)) to remove the advanced message listener.

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



## Receiving Text Messages

The receiver can receive a one-to-one or group text message with the advanced message listener in the following steps:
1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html)) that contains the custom message.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // Process a text message
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



## Receiving Custom Messages

The receiver can receive a custom one-to-one or group message with the advanced message listener in the following steps:
1. Call `addAdvancedMsgListener` to set the event listener.
2. Listen for the `onRecvNewMessage` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html)) that contains the custom message.
3. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.

Sample code:


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // Use a custom message
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



## Receiving Rich Media Messages
The receiver can receive a rich media message **only with** the advanced message listener in the following steps:
1. Call the `addAdvancedMsgListener` API to set the advanced message listener.
2. Listen for the `onRecvNewMessage` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html)) to get the `V2TimMessage` message.
3. Parse the `elemType` attribute in the `V2TIMMessage` message, and then parse the message again according to the type to get the specific content of the elements in the message.
4. To stop receiving messages, call `removeAdvancedMsgListener` to remove the listener. This step is optional and can be performed as needed.




### Image message

The image in an image message can be in three formats: original, large, and thumbnail. The latter two are automatically generated by the SDK during message sending and can be ignored.
`Large` (large image): A large image is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 720 pixels.
`Thumb` (thumbnail): A thumbnail is an image obtained after the original image is proportionally compressed. After the compression, the height or width (whichever is shorter) is equal to 198 pixels.

In the SDK for Flutter 5.0.4 or later, multimedia message online URLs (`url`) will not be returned when users get the message list. They need to be obtained by calling the `getMessageOnlineUrl` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html)).
In the SDK for Flutter SDK 5.0.4 or later, multimedia message local URLs (`localurl`) will no longer be returned by default. They will be returned only after you download messages successfully by calling the `downloadMessage` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html)).

The following sample code demonstrates how to parse the image content from `V2TimMessage`:



```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) async {
      // Use an image message
      if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE) {
        String path = message
            .imageElem.path; // Image upload path. This field applies only to the message sender who can use it to display the image on the screen in advance to optimize the experience
        for (var item in message.imageElem.imageList) { // Traverse large images, original images, and thumbnails
          // Parse image attributes
          int height = item.height;
          String localUrl = item.localUrl;
          int size = item.size;
          int type = item.type; // Large image, thumbnail, or original image
          String url = item.url;
          String uuid = item.uuid;
          int width = item.width;
        }
      }
      // Get the multimedia message URL
      V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
          await TencentImSDKPlugin.v2TIMManager
              .getMessageManager()
              .getMessageOnlineUrl(
                msgID: '', // Message ID
              );
      if (getMessageOnlineUrlRes.code == 0) {
        // Obtained successfully
      }

      // Download a multimedia message
      V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(
              msgID: '', // Message ID
              messageType: 3, // Message type
              imageType: 0, // Image type. This field is valid only for image messages.
              isSnapshot: false // Whether it is a video thumbnail. This field is valid only for video messages.
              );
      if (downloadMessageRes.code == 0) {
        // Download successful
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

The SDK for Flutter will download video messages when free, which can be directly used by you. Local videos and video thumbnails will be cleared when the application is uninstalled. The following sample code demonstrates how to parse video content from `V2TimMessage`:

In the SDK for Flutter 5.0.4 or later, multimedia message online URLs (`url`) will not be returned when users get the message list. They need to be obtained by calling the `getMessageOnlineUrl` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html)).
In the SDK for Flutter SDK 5.0.4 or later, multimedia message local URLs (`localurl`) will no longer be returned by default. They will be returned only after you download messages successfully by calling the `downloadMessage` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html)).


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

      // Get the multimedia message URL
      V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
          await TencentImSDKPlugin.v2TIMManager
              .getMessageManager()
              .getMessageOnlineUrl(
                msgID: '', // Message ID
              );
      if (getMessageOnlineUrlRes.code == 0) {
        // Obtained successfully
      }

      // Download a multimedia message
      V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(
              msgID: '', // Message ID
              messageType: 5, // Message type
              imageType: 0, // Image type. This field is valid only for image messages.
              isSnapshot: false // Whether it is a video thumbnail. This field is valid only for video messages.
              );
      if (downloadMessageRes.code == 0) {
        // Download successful
      }
```


### Audio message

The SDK for Flutter will download audio messages when free, which can be directly used by you and will be cleared when the application is uninstalled. The following sample code demonstrates how to parse audio content from `V2TimMessage`:

In the SDK for Flutter 5.0.4 or later, multimedia message online URLs (`url`) will not be returned when users get the message list. They need to be obtained by calling the `getMessageOnlineUrl` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html)).
In the SDK for Flutter SDK 5.0.4 or later, multimedia message local URLs (`localurl`) will no longer be returned by default. They will be returned only after you download messages successfully by calling the `downloadMessage` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html)).

```dart
    if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND){
  			// Parse the playback address, local address, size, and duration of the audio message.
        message.soundElem.UUID;
        message.soundElem.dataSize;
        message.soundElem.duration;
        message.soundElem.localUrl;
        message.soundElem.url;
        // ...
        // Get the multimedia message URL
        V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
            await TencentImSDKPlugin.v2TIMManager
                .getMessageManager()
                .getMessageOnlineUrl(
                  msgID: '', // Message ID
                );
        if (getMessageOnlineUrlRes.code == 0) {
          // Obtained successfully
        }

        // Download a multimedia message
        V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(
                msgID: '', // Message ID
                messageType: 4, // Message type
                imageType: 0, // Image type. This field is valid only for image messages.
                isSnapshot: false // Whether it is a video thumbnail. This field is valid only for video messages.
                );
        if (downloadMessageRes.code == 0) {
          // Download successful
        }
    }
```


### File message

The SDK for Flutter will download file messages when free, which can be directly used by you and will be cleared when the application is uninstalled. The following sample code demonstrates how to parse file message content from `V2TimMessage`:

In the SDK for Flutter 5.0.4 or later, multimedia message online URLs (`url`) will not be returned when users get the message list. They need to be obtained by calling the `getMessageOnlineUrl` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html)).
In the SDK for Flutter SDK 5.0.4 or later, multimedia message local URLs (`localurl`) will no longer be returned by default. They will be returned only after you download messages successfully by calling the `downloadMessage` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html)).

```dart

    if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE){
  			// Parse the filename, size, URL and other info of the file message
        message.fileElem.UUID;
        message.fileElem.fileName;
        message.fileElem.fileSize;
        message.fileElem.localUrl;
        message.fileElem.path;
        message.fileElem.url;
        // Get the multimedia message URL
        V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
            await TencentImSDKPlugin.v2TIMManager
                .getMessageManager()
                .getMessageOnlineUrl(
                  msgID: '', // Message ID
                );
        if (getMessageOnlineUrlRes.code == 0) {
          // Obtained successfully
        }

        // Download a multimedia message
        V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(
                msgID: '', // Message ID
                messageType: 6, // Message type
                imageType: 0, // Image type. This field is valid only for image messages.
                isSnapshot: false // Whether it is a video thumbnail. This field is valid only for video messages.
                );
        if (downloadMessageRes.code == 0) {
          // Download successful
        }
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

The SDK only provides a message passthrough channel for an emoji message. For message content fields, see `faceElem` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimFaceElem.html)), where the contents of `index` and `data` are customized by the user.

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

Group tip messages are tips received by users other than ordinary messages in a group chat, such as "The admin removed alice from the group chat" and "bob renamed the group "xxxx"".

> ? Group tip messages apply to group members only.

There are many types of group tip messages. For more information, see the definition of `V2TIMGroupTipsType` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Group/V2TimGroupTipsElem.html)).

After receiving a group tip message, the receiver generally needs to:
1. Parse all fields in `V2TIMGroupTipsElem`.
2. Identify the message type according to `type`.
3. Merge other fields into the content for display according to the type.

Example:
`V2TIM_GROUP_TIPS_TYPE_GROUP_INFO_CHANGE` is parsed from the `type`, indicating that this is a notification of group profile change.
The receiver can get the operator information from `opMember` and the new group name from `groupChangeInfoList`.
At this point, the receiver can merge the "operator" and "new group name" to create a group tip, such as "Alice renamed the group as "group123"".

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


## Receiving Messages Containing Multiple Element Objects

1. Parse the first element object from the `Message` object.
2. Get the next element object through the `nextElem` method of the first element object. If the next object exists, an element object instance is returned; otherwise, `null` is returned.

Sample code:


```dart
if(message.textElem.nextElem!=null){
   // There is a next message
}
```
