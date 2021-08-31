## Sending Messages

### Sending common messages

<b>Obtain a conversation</b>: conversations are classified into conversations with an individual user and conversations with a group. To send or receive messages in a conversation, you first need to obtain the conversation by specifying the conversation type (C2C conversation or group conversation) and the peer's identifier (the peer's account or group ID). To obtain a conversation, call `getConversation` of `TIMManager`.

**Prototype:**

```
/**
 * Obtain a conversation.
 * @param type Conversation type
 * @param peer Peer in the conversation. For a C2C conversation, use the peer's account identifier. For a group conversation, use the group ID.
 * @return Conversation instance
 */
public TIMConversation getConversation(TIMConversationType type, String peer)
```

**Example:**

```
// Obtain a C2C conversation.
String peer = "sample_user_1";  // Obtain the conversation with user "sample_user_1".
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.C2C,    // Conversation type: C2C conversation
        peer);                      // Peer's account // Peer's ID
 
// Obtain a group conversation.
String groupId = "TGID1EDABEAEO";  // Obtain the conversation with group "TGID1LTTZEAEO".
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.Group,      //Conversation type: group conversation
        groupId);                       // Group ID
```

<b>Send messages: </b>after `TIMConversation` is obtained using `TIMManager`, you can send messages and obtain cached messages for the conversation. For more information about the interpretation of messages in the IM SDK, see [Introduction to IM SDK Objects](https://intl.cloud.tencent.com/document/product/1047/34301). In the IM SDK, a message is a `TIMMessage` object. A `TIMMessage` can contain multiple `TIMElem`, and each `TIMElem` can be a text or an image. That is, a message can contain multiple texts and images.

![](https://main.qcloudimg.com/raw/5b109b81e56ac31a6c73ca6053a342ff.png)

To send messages, use the `sendMessage` method of `TIMConversation`.

**Prototype:**

```
/**
 * Send a message.
 * @param msg Message
 * @param callback Callback
 */
public void sendMessage(@NonNull TIMMessage msg, @NonNull TIMValueCallBack<TIMMessage> callback)
```

### Sending text messages

A text message is defined by `TIMTextElem`. **`The TIMTextElem` member methods are as follows:**

```
// Obtain the text content.
java.lang.String    getText()

// Set the text content. 'text' passes the text message to send.
void    setText(java.lang.String text)
```

**Example:**

```
// Construct a message.
TIMMessage msg = new TIMMessage();

// Add the text content.
TIMTextElem elem = new TIMTextElem();
elem.setText("a new msg");

// Add 'elem' to the message.
if(msg.addElement(elem) != 0) {
   Log.d(tag, "addElement failed");
   return;
}

// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending image messages

An image message is defined by `TIMImageElem`, which is a subclass of `TIMElem`. That is, the content of an image message includes one or more images. To send an image, add `TIMImageElem` to `TIMMessage` and send the image along with the message.

>! `path` does not support file paths starting with `file://`. Therefore, the `file://` prefix must be removed.

<b>The `TIMImageElem` member methods are as follows:</b>

```
/**
 * Obtain the list of images contained in `elem`. It can be called when the IM SDK fetches `elem`.
 * @return elem List of images contained in `elem`
 */
public ArrayList<TIMImage> getImageList()

/**
 * Obtain the local file path of the original image. This method is valid only for message senders.
 * @return Local file path
 */
public String getPath()

/**
 * Set the file path of the original image to be sent.
 * @param path File path of the original image
 */
public void setPath(String path)

/**
 * Obtain the image quality level.
 * @return Image quality level. 0: original image. 1: highly compressed image (small image). 2: high-resolution image (large image).
 */
public int getLevel()

/**
 * Set the image quality level.
 * @param level 0: original image. 1: highly compressed image (small image), default value. 2: high-resolution image (large image).
 */
public void setLevel(int level)

/**
 * Cancel image upload.
 * @return Whether image upload was canceled
 */
public boolean cancelUploading()

/**
 * Obtain the ID of the image upload task. The returned value of this API is valid after `sendMessage` is called.
 * @return ID of the image upload task
 */
public int getTaskId()

/**
 * Obtain the image type.
 * @return Image type
 */
public int getImageFormat()
```

To send an image, you only need to set `path`, which is the image path. After the image is sent successfully, you can call `getImageList` to obtain all image types. `TIMImage` stores the image type, size, width, and height. To download the binary data of the image, call `getImage`.

**`The TIMImage` member methods are as follows:**

```
/**
 * Obtain an image.
 * @param path Image storage path
 * @param cb Callback
 */
public void getImage(@NonNull final String path, @NonNull final TIMCallBack cb)

/**
 * Obtain the image type.
 * @return Image type
 */
public TIMImageType getType()

/**
 * Obtain the UUID.
 * @return UUID, which can be used as the unique key for caching
 */
public String getUuid()

/**
 * Obtain the image size.
 * @return Image size.
 */
public long getSize()

/**
 * Obtain the image height.
 * @return Image height.
 */
public long getHeight()

/**
 * Obtain the image width.
 * @return Image width
 */
public long getWidth()

/**
 * Obtain the image URL.
 * @return Image URL
 */
public String getUrl()

```

**Example:**


```
// Construct a message.
TIMMessage msg = new TIMMessage();

// Add an image.
TIMImageElem elem = new TIMImageElem();
elem.setPath(Environment.getExternalStorageDirectory() + "/DCIM/Camera/1.jpg");
 
// Add `elem` to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the list of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```
### Sending emoji messages

An emoji message is defined by `TIMFaceElem`. The IM SDK does not provide emoji packages. Developers can use `index` to store the index entries of the emojis in their emoji packages. Alternatively, they can directly use `data` to store emoji binary data and the string `key`. Using either method, users can customize emojis. The IM SDK only passes them through.

**`The TIMFaceElem` member methods are as follows:**

```
/**
 * Obtain an emoji index.
 * @return Emoji index
 */
public int getIndex()

/**
 * Set the emoji index.
 * @param index Emoji index
 */
public void setIndex(int index)

/**
 * Obtain custom emoji data.
 * @return Custom emoji data
 */
public byte[] getData()

/**
 * Set custom emoji data.
 * @param data Custom emoji data
 */
public void setData(byte[] data)
```

**Example:**

```
// Construct a message.
TIMMessage msg = new TIMMessage();

// Add an emoji.
TIMFaceElem elem = new TIMFaceElem();
elem.setData(sampleByteArray); // Custom byte[]
elem.setIndex(10);   // Custom emoji index
 
// Add `elem` to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```


### Sending audio messages

An audio message is defined by `TIMSoundElem`, where `data` stores audio data. For audio data, you need to provide the audio length in seconds.

>!
> - A message can contain only one audio `Elem`. If you attempt to add multiple audio `Elem` objects, the `AddElem` function returns Error 1 and the audio `Elem` objects cannot be added.
> - Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects may not be sorted in the order that they are sent. 
> - `path` does not support file paths starting with `file://`. The `file://` prefix must be removed.

<b>The `TIMSoundElem` member methods are as follows:</b>

```
/**
 * Download and save an audio file to the specified path.
 *
 * @param path Specified storage path
 * @param progressCb Download progress callback
 * @param cb Callback
 */
 public void getSoundToFile(@NonNull final String path, final TIMValueCallBack<ProgressInfo> progressCb, @NonNull final TIMCallBack cb) 

/**
 * Obtain the path of the audio file to be sent. This method is valid only for message senders.
 * @return Audio file path
 */
public String getPath()

/**
 * Set the path of the audio file to be uploaded. (If the file path is specified, the audio file in the specified file path will be uploaded first.)
 * @param path Audio file path
 */
public void setPath(String path)

/**
 * Obtain the UUID.
 * @return uuid
 */
public String getUuid()

/**
 * Obtain the length of binary data.
 * @return Length of binary data
 */
public long getDataSize()

/**
 * Obtain the audio length.
 * @return Audio length
 */
public long getDuration()

/**
 * Set the audio length.
 * @param duration Audio length
 */
public void setDuration(long duration)

/**
 * Obtain the ID of the audio upload task. The returned value of this API is valid after `sendMessage` is called.
 * @return ID of the audio file upload task
 */
public int getTaskId()

```

**Example:**

```
// Construct a message.
TIMMessage msg = new TIMMessage();

// Add an audio file.
TIMSoundElem elem = new TIMSoundElem();
elem.setPath(filePath); // Enter the audio file path.
elem.setDuration(20);  // Enter the audio length.
 
// Add `elem` to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```
### Sending location messages

A location message is defined by `TIMLocationElem`, where `desc` stores the location description information, and `longitude` and `latitude` represent the location longitude and latitude, respectively.

<b>The `TIMLocationElem` member methods are as follows:</b>

```
/**
 * Obtain the location description.
 * @return Location description
 */
public String getDesc()

/**
 * Set the location description.
 * @param desc Location description
 */
public void setDesc(String desc)

/**
 * Obtain the longitude.
 * @return Longitude
 */
public double getLongitude()

/**
 * Set the longitude.
 * @param longitude Longitude
 */
public void setLongitude(double longitude)

/**
 * Obtain the latitude.
 * @return Latitude
 */
public double getLatitude()

/**
 * Set the latitude.
 * @param latitude Latitude
 */
public void setLatitude(double latitude)
```

**Example:**


```
// Construct a message.
TIMMessage msg = new TIMMessage();

// Add location information.
TIMLocationElem elem = new TIMLocationElem();
elem.setLatitude(113.93);   // Set the latitude.
elem.setLongitude(22.54);   // Set the longitude.
elem.setDesc("Tencent Building");

// Add 'elem' to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }
    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending file messages

A file message is defined by `TIMFileElem`. You can also view additional information such as the file name.

>!
> - Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects may not be sorted in the order that they are sent. 
> - `path` does not support file paths starting with `file://`. The `file://` prefix must be removed.
> - The maximum file size is 28 MB.

<b>The `TIMFileElem` member methods are as follows:</b>

```
/**
 * Download and save a file to the specified path.
 * @param path Specified storage path
 * @param callback Callback
 */
public void getToFile(@NonNull final String path, @NonNull TIMCallBack callback)

/**
 * Obtain the UUID.
 * @return UUID, which can be used as the unique key for caching
 */
public String getUuid()

/**
 * Obtain the file size.
 * @return File size
 */
public long getFileSize()

/**
 * Obtain the file name.
 * @return File name
 */
public String getFileName()

/**
 * Set the file name when sending the file.
 * @param fileName File name
 */
public void setFileName(String fileName)

/**
 * Obtain the path of the uploaded file. This method is valid only for message senders.
 * @return File path
 */
public String getPath()

/**
 * Set the path of the file to be uploaded. (If the file path is specified, the file in the specified file path will be uploaded first.)
 * @param path File path
 */
public void setPath(String path)

/**
 * Obtain the ID of the file upload task. The returned value of this API is valid after `sendMessage` is called.
 * @return ID of the file upload task
 */
public int getTaskId()
```

**Example:**

```
// Construct a message.
TIMMessage msg = new TIMMessage();

// Add the file content.
TIMFileElem elem = new TIMFileElem();
elem.setPath(filePath); // Set the file path.
elem.setFileName("myfile.bin"); // Set the file name for displaying the message.
 
// Add `elem` to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending custom messages

Developers can customize the message format and content when built-in message types cannot meet their special needs. The IM SDK only passes through custom messages. If iOS APNs push notifications are required, a push text description to be displayed needs to be provided. A custom message is defined by `TIMCustomElem`, where 'data' stores the binary data of the message, its format is defined by developers, and `desc` stores the description text. A message can contain multiple custom `Elem` objects, which can be mixed with other `Elem` objects. In offline push scenarios, the `desc` of each `Elem` are stacked and delivered.

<b>The `TIMCustomElem` member methods are as follows:</b>

```
/**
 * Obtain the custom data.
 * @return Custom data
 */
public byte[] getData()

/**
 * Set the custom data.
 * @param data Custom data
 */
public void setData(byte[] data)

/**
 * Obtain custom description.
 * @return Custom description
 */
public String getDesc()

/**
 * Set the custom description.
 * @param desc Custom description
 */
public void setDesc(String desc)

/**
 * Obtain the `ext` field pushed by the backend.
 * @return ext
 */
public byte[] getExt()

/**
 * Set the `ext` field pushed by the backend.
 * @param ext The `ext` field pushed by the backend
 */
public void setExt(byte[] ext)

/**
 * Obtain the custom sound.
 * @return Custom sound data
 */
public byte[] getSound()

/**
 * Set custom sound data.
 * @param data Custom sound data
 */
public void setSound(byte[] data)
```

The following example shows how to add an XML message, where the specific display is determined by the developer. **Example:**

```
// Construct a message.
TIMMessage msg = new TIMMessage();
 
// Custom XML message
String sampleXml = "<!--?xml version='1.0' encoding="utf-8"?-->testTitlethis is custom msgtest msg body";
 
// Add custom content to `TIMMessage`.
TIMCustomElem elem ＝ new TIMCustomElem();
elem.setData(sampleXml.getBytes());      // Custom byte[]
elem.setDesc("this is one custom message"); // Custom description
 
// Add `elem` to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending short video messages

A short video message is defined by `TIMVideoElem`, which is a subclass of `TIMElem`. These messages can contain video snapshots and content. To send a short video, add `TIMVideoElem` to `TIMMessage` and send the video along with the message.

**`TIMVideoElem` prototype:**

```
/**
 * Obtain the ID of the short video upload task. The returned value of this API is valid after `sendMessage` is called.
 *
 * @return ID of the short video upload task
 */
public long getTaskId() {
    return this.taskId;
}

/**
 * Set short video information when sending the message.
 *
 * @param video Short video information. For more information, see {@link TIMVideo}.
 */
public void setVideo(TIMVideo video) {
    this.video = video;
}

/**
 * Obtain video information.
 *
 * @return Video information. For more information, see {@link TIMVideo}.
 */
public TIMVideo getVideoInfo() {
    return this.video;
}

/**
 * Set the video file path when sending the message.
 *
 * @param path Video file path
 */
public void setVideoPath(String path) {
    this.videoPath = path;
}

/**
 * Obtain the video file path.
 *
 * @return Video file path
 */
public String getVideoPath() {
    return this.videoPath;
}

/**
 * Set short video snapshot information when sending the message.
 *
 * @param snapshot Short video snapshot information. For more information, see {@link TIMSnapshot}.
 */
public void setSnapshot(TIMSnapshot snapshot) {
    this.snapshot = snapshot;
}

/**
 * Obtain video snapshot information.
 *
 * @return Video snapshot information. For more information, see {@link TIMSnapshot}.
 */
public TIMSnapshot getSnapshotInfo() {
    return this.snapshot;
}

/**
 * Set the short video snapshot file path when sending the message.
 *
 * @param path Short video snapshot file path
 */
public void setSnapshotPath(String path) {
    this.snapshotPath = path;
}

/**
 * Obtain the short video snapshot file path.
 *
 * @return Short video snapshot file path
 */
public String getSnapshotPath() {
    return this.snapshotPath;
}
```

**Parameter description:**

Parameter | Description
---|---
taskId | The upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress.
videoPath | The path of the local video to be sent.
video | The video information. Set the `type` and `duration` parameters when sending the message.
snapshotPath | The local snapshot path of the short video to be sent.
snapshot | The snapshot information. Set the `type` and `duration` parameters when sending the message.

The following example shows how to send a short video message. **Example:**

```
// Construct a message.
TIMMessage msg = new TIMMessage();

// Construct a short video object.
TIMVideoElem ele = new TIMVideoElem();

TIMVideo video = new TIMVideo();
video.setDuaration(duration / 1000); // Set the video length.
video.setType("mp4"); // Set the video file type.

TIMSnapshot snapshot = new TIMSnapshot(); 
snapshot.setWidth(width); // Set the video snapshot width.
snapshot.setHeight(height); // Set the video snapshot height.

ele.setSnapshot(snapshot);
ele.setVideo(video);
ele.setSnapshotPath(imgPath);
ele.setVideoPath(videoPath);

 
// Add `elem` to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

// Send a message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {// Callback for sending a message
    @Override
    public void onError(int code, String desc) {// Failed to send the message.
        // 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {// Succeeded in sending the message.
        Log.e(tag, "SendMsg ok");
    }
});
```


### 'Elem' order 

Currently, file and audio `Elem` objects might not be transferred in the order that they are added. Other `Elem` objects are transferred in the order that they are added. However, we recommend that you do not heavily rely on the `Elem` object sequence when processing elements. Instead, you should process `Elem` objects by type to prevent process crashes when exceptions occur.


### Online messages

In some scenarios, you need to send online messages, which can only be received when a user is online. If the user is not online when the messages are sent, the user will not see them upon the next login. Online messages can be used for notifications. However, online messages will not be stored or included in the unread count. The API for sending online messages is similar to `sendMessage`.

>! In versions earlier than 2.5.3, online messages apply only to C2C conversations. In version 2.5.3 or later, online messages apply to group conversations, excluding audio-video chat rooms (AVChatRoom) and broadcasting chat rooms (BChatRoom).

```
* Send an online message (the server does not save the message).
public void sendOnlineMessage(TIMMessage msg, TIMValueCallBack<TIMMessage> callback)
```

### Forwarding messages

You can call `copyFrom` of `TIMMessage` to easily copy the content of another message to the current message and resend the message to other contacts.

**Prototype:**
```
/**
 * Copy the message content to the current message, including `elem`, `priority`, `online`, and `offlinePushInfo`.
 * @param srcMsg Source message
 * @return true Copied successfully
 */
public boolean copyFrom(@NonNull TIMMessage srcMsg)
```


## Receiving Messages

To be notified of new messages, you need to register the new message notification callback `TIMMessageListener`. If you have logged in to the IM console, the IM SDK uses the `onNewMessages` callback to send new messages. For more information about how to register the new message notification callback, see [New Message Notification](https://intl.cloud.tencent.com/document/product/1047/36255#.E6.96.B0.E6.B6.88.E6.81.AF.E9.80.9A.E7.9F.A5).

>! Messages obtained using `onNewMessages` may not be unread messages. They can also be messages that have not been displayed locally. For example, when messages have been read on another client, messages of recent contacts can be pulled to obtain the latest messages in conversations. If these latest messages are not stored locally, they are sent using this method. After a user logs in, the IM SDK gets C2C offline messages. To avoid missing message notifications, the user needs to register new message notifications before login.
The `onNewMessage` callback is also used to send group system messages, relationship chain changes, and friend profile changes.

### Parsing messages

After receiving a message, use `getElem` to obtain all `Elem` nodes in `TIMMessage`. **The following is the prototype for traversing `Elem` nodes:**

```
// Obtain message elements.
TIMElem getElement(int i)

// Obtain the number of elements.
int getElementCount()
```

**Example:**

```
TIMMessage msg = /* Message */

for(int i = 0; i < msg.getElementCount(); ++i) {
	TIMElem elem = msg.getElement(i);

	// Obtain the type of the current element.
	TIMElemType elemType = elem.getType();
	Log.d(tag, "elem type: " + elemType.name());
	if (elemType == TIMElemType.Text) {
		// Process text messages.
	} else if (elemType == TIMElemType.Image) {
		// Process image messages.
	}//...Process more messages.
}
```


### Receiving image messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMElemType.Image` type are image message nodes. To obtain all image specifications, including the original image, large image, and thumbnail, use `getImageList` of `TIMImageElem`. Each specification is stored in a `TIMImage` object.

```
/**
 * Obtain the list of images contained in `Elem`. It can be called when the IM SDK fetches `Elem`.
 * @return elem List of images contained in `elem`
 */
public ArrayList<TIMImage> getImageList()
```

**`TIMImage`:**

After receiving a message, use `imageList` to obtain all image specifications, which are `TIMImage` objects. After obtaining `TIMImage`, reserve a place based on the image size and use `getImage` to download images of different specifications for display.

>! Developers need to cache the downloaded data. The IM SDK downloads data from the server each time it calls `getImage`. We recommend that you use the `uuid` of an image as the `key` to store images.

**Image specifications:** each image has three specifications, including Original (original image), Large (large image), and Thumb (thumbnail).

- **Original image:** the original image sent by a user, whose dimensions and size remain unchanged.
- **Large image:** an image obtained after the original image is proportionally compressed. The height or width of the compressed image, whichever is smaller, is equal to 720 pixels.
- **Thumbnail:** an image obtained after the original image is proportionally compressed. The height or width of the compressed image, whichever is smaller, is equal to 198 pixels.

>- If the size of the original image is less than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
>- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
>- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When a user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is downloaded when the user taps the thumbnail.
>- When an image is displayed on a tablet or PC, we recommend that the large image be displayed directly and the original image be downloaded when a user taps or clicks the large image due to the high resolution and availability of a Wi-Fi or wired network.

**Example:**

```
// Traverse the element list of a message.
for(int i = 0; i < msg.getElementCount(); ++i) {
    TIMElem elem = msg.getElement(i);
    if (elem.getType() == TIMElemType.Image) {
        // Image element
        TIMImageElem e = (TIMImageElem) elem;
        for(TIMImage image : e.getImageList()) {

            // Obtain the image type, size, width, and height.
            Log.d(tag, "image type: " + image.getType() +
                    " image size " + image.getSize() +
                    " image height " + image.getHeight() +
                    " image width " + image.getWidth());

            image.getImage(path, new TIMCallBack() {
                    @Override
                    public void onError(int code, String desc) {// Failed to obtain the image.
						// 'code' (error code) and 'desc' (error description) can be used to locate the cause of the request failure.
						// For more information about the meaning of error codes, see the Error Code table.
						Log.d(tag, "getImage failed. code: " + code + " errmsg: " + desc);
                    }

                    @Override
                    public void onSuccess() {// Request succeeded, and the parameter is the image data.
						//doSomething
						Log.d(tag, "getImage success.");
                    }
                });
        }
    }
}
```

### Receiving audio messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMElemType.Sound` type are audio message nodes. When the message is received, reserve a place based on the audio length and use `getSoundToFile` to download audio resources. The `getSoundToFile` API downloads the data from the server. To cache or store the data, use `uuid` as the `key` to store the audio file externally. The IM SDK does not store resource files.

**Prototype:**

```
/**
 * Download and save an audio file to the specified path.
 *
 * @param path Specified storage path
 * @param progressCb Download progress callback
 * @param cb Callback
 */
 public void getSoundToFile(@NonNull final String path, final TIMValueCallBack<ProgressInfo> progressCb, @NonNull final TIMCallBack cb) 
```

**Audio message read status:** you can use [custom message fields](https://intl.cloud.tencent.com/document/product/1047/36401#.E6.B6.88.E6.81.AF.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5) to determine whether an audio message has been played. For example, the value 0 of `customInt` indicates that the audio message has not been played, and the value 1 indicates that the audio message has been played. When a user taps Play, `customInt` is set to 1. The following prototype shows how to set `customInt`, and the default value is 0.

**Prototype:**
```
public void setCustomInt(int value)
```


### Receiving file messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMFileElem` type are file message nodes.

<b>The `TIMFileElem` member methods are as follows:</b>

```
// Download and save a file to the specified path.
void getToFile(String path, TIMCallBack callback)

// Obtain the file name.
java.lang.String    getFileName()

// Obtain the file size.
long    getFileSize()

// Obtain the UUID.
java.lang.String    getUuid()

// Set the file name.
void    setFileName(java.lang.String fileName)
```

You can choose to display only the file size and name of a received file message and use `getToFile` to download the file from the server each time. To cache or store the data, use `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.

**Prototype:**

```
/**
 * Download and save a file to the specified path.
 * @param path Specified storage path
 * @param callback Callback
 */
public void getToFile(@NonNull final String path, @NonNull TIMCallBack callback)
```

### Receiving short video messages
After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMVideoElem` type are short video message nodes. Use the `TIMVideo` and `TIMSnapshot` objects to obtain the video and snapshot content. After receiving `TIMVideoElem`, download the video file and snapshot file through the APIs defined in the `video` and `snapshot` properties. To cache or store the data, use `uuid` as the `key` to store the files externally. The IM SDK does not store resource files.

<b>The `TIMVideo` member methods are as follows:</b>

```

/**
 * Obtain the video.
 *
 * @param path Video storage path
 * @param cb Callback
 * @deprecated
 */
getVideo(@NonNull final String path, @NonNull final TIMCallBack cb);

/**
 * Obtain the video.
 *
 * @param path Video storage path
 * @param progressCb Download progress callback
 * @param cb Callback
 */
void getVideo(@NonNull final String path, final TIMValueCallBack<ProgressInfo> progressCb, @NonNull final TIMCallBack cb)

/**
 * Obtain the video size.
 *
 * @return Video size
 */
long getSize();

/**
* Obtain the UUID of the video file.
*
* @return UUID, which can be used as the unique key for caching
*/
String getUuid();

/**
 * Obtain the video length.
 *
 * @return Video length
 */
long getDuaration();

/**
 * Obtain the video file type.
 *
 * @return Video file type
 */
String getType(); 
```

<b>The `TIMSnapshot` member methods are as follows:</b>
```
/**
 * Obtain the snapshot.
 *
 * @param path Snapshot storage path
 * @param progressCb Download progress callback
 * @param cb Callback
 */
void getImage(final String path, final TIMValueCallBack<ProgressInfo> progressCb, final TIMCallBack cb);

/**
 * Obtain the snapshot.
 *
 * @param path Snapshot storage path
 * @param cb Callback
 * @deprecated
 */
void getImage(final String path, final TIMCallBack cb);

/**
 * Obtain the snapshot width.
 *
 * @return Snapshot width
 */
long getWidth();

/**
 * Obtain the snapshot height.
 *
 * @return Snapshot height
 */
long getHeight();

/**
 * Obtain the snapshot size.
 *
 * @return Snapshot size
 */
long getSize();

/**
 * Obtain the snapshot file type.
 *
 * @return Snapshot file type
 */
String getType();

/**
 * Obtain the UUID of the snapshot file.
 *
 * @return UUID, which can be used as the unique key for caching
 */
String getUuid(); 
```

**Parsing process for short video messages:**
The new message receipt callback is used as an example. First, determine whether the message has `TIMVideoElem` based on the element type. If yes, the message is a short video message. In this case, run the following code to parse it.

```
TIMMessage timMsg = msg.getTIMMessage();
final TIMVideoElem videoEle = (TIMVideoElem) timMsg.getElement(0);
final TIMVideo video = videoEle.getVideoInfo();
final TIMSnapshot shotInfo = videoEle.getSnapshotInfo();
final String path = ”/xxx/“ + videoEle.getSnapshotInfo().getUuid(); // Storage path of the received snapshot
final String videoPath = ”/xxx/“ + video.getUuid(); // Storage path of the received video
videoEle.getSnapshotInfo().getImage(path, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
        Log.e(tag, "Failed to download the snapshot, code = " + code + ", errorinfo = " + desc);
    }

    @Override
    public void onSuccess() {
        Log.d(tag, "Succeeded in downloading the snapshot");
    }
});

video.getVideo(videoPath, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
	Log.e(tag, "Failed to download the short video, code = " + code + ", errorinfo = " + desc);
    }

    @Override
    public void onSuccess() {
        Log.d(tag, "Succeeded in downloading the short video");
    }
});
```

## Message Properties

You can obtain message properties using the `TIMMessage` member methods.

### Checking whether a message has been read

Use `isRead` of `TIMMessage` to check whether a message has been read, which is determined by the [Unread Count](https://intl.cloud.tencent.com/document/product/1047/34324) on the app side. The prototype for checking whether a message has been read is as follows:

**Prototype:**
```
public boolean isRead()
```

### Message status

To obtain the status of the current message, such as sending, sent successfully, failed to send, or deleted, use the `status` method of `TIMMessage`. For deleted messages, use the UI to determine the status and hide the messages accordingly.
```
// Sending
TIMMessageStatus.Sending

// Sent successfully
TIMMessageStatus.SendSucc

// Failed to send
TIMMessageStatus.SendFail

// Deleted
TIMMessageStatus.HasDeleted

// Recalled
TIMMessageStatus.HasRevoked
```

### Checking whether a message was sent by oneself

To determine whether a message was sent by you yourself, use the `isSelf` method of `TIMMessage`. This method is available when the message is displayed on the interface. The following shows the prototype for determining whether a message was sent by yourself.

**Prototype:**
```
public boolean isSelf()
```

### Message sender and related profile

To obtain the sender's ID, use the `getSender` method of `TIMMessage`.
For one-to-one chat messages, use the `getConversation` method of `TIMMessage` to obtain the corresponding conversation and use `getPeer` to obtain the recipient and the recipient's profile.
For group chat messages, use `getSenderProfile` and `getSenderGroupMemberProfile` to obtain the sender's profile and the profile of the group to which the sender belongs. To get custom fields, [set the fields to be pulled](https://intl.cloud.tencent.com/document/product/1047/36271) before logging in to the IM SDK.
 >! This field obtains the user profile and writes it to the message body when the message is sent. If the user profile is updated, this field will not change unless new messages are generated.
 > You can obtain profiles only from received group messages.

```
/**
 * Obtain the message sender.
 * @return Message sender
 */
public String getSender()

/**
 * Obtain the sender profile.
 *
 * In version 4.4.716, this information is returned through a callback.
 *
 * @param callBack Callback
 */
public void getSenderProfile( TIMValueCallBack < TIMUserProfile > callBack )

/**
 * Obtain the sender's profile in the group, which is only available for received group messages (may be empty if the sender is yourself).
 *
 * @return Sender's profile in the group. "null" indicates that no profile was obtained or the message is not a group message. Currently, only the user, nameCard, role, and customInfo fields can be obtained. To obtain other fields, use `getGroupMembers` of `TIMGroupManager`.
 */
public TIMGroupMemberInfo getSenderGroupMemberProfile()
```


### Message time

To obtain the message time, use the `timestamp` method of `TIMMessage`. **This time is the server time, not the local time.** When you create a message, this time is calibrated based on the server time and will be changed to the accurate server time after the message is successfully sent.

```
// Timestamp generated for the message by the server
public long timestamp()
```

### Message ID

There are two types of message IDs. One is `msgId`, which is created when a message is generated. If `msgId` is used, messages may conflict with messages generated by other users, and therefore a time dimension needs to be added. Messages generated within 10 minutes can be distinguished by `msgId`. The other is `uniqueId`, which is generated after a message is sent successfully and is globally unique. Both types of message IDs must be checked in the same conversation.

```
// Obtain the message ID.
public String getMsgId()

// Obtain the uniqueId of the message.
public long getMsgUniqueId()
```

### Custom message field

Developers can add custom fields to messages, such as the custom integer and custom binary data fields, and can customize different effects based on these two fields. For example, custom fields can be used to determine whether an audio message has been played. Note that these custom fields are only stored locally and not synchronized to the server. You will not obtain them after switching to another client.

```
// Set the custom integer, which is 0 by default.
public void setCustomInt(int value)

// Obtain the value of the custom integer.
public int getCustomInt()

// Set the custom data content, which is "". by default.
public void setCustomStr(String str)

// Obtain the value of the custom data content.
public String getCustomStr()
```

### Message priority

Livestreaming scenarios involve the like and red packet features. Like messages have a lower priority than red packet messages. You can use `TIMCustomElem` to define the message content, and use different APIs to define the message priority when sending a message.
>! Message priorities apply only to group messages.

```
// Set the message priority.
public void setPriority(TIMMessagePriority priority)

// Obtain the message priority.
public TIMMessagePriority getPriority()
```


### Read receipt

The IM SDK provides the read receipt feature for **C2C messages**. You can enable this feature using `enableReadReceipt` of `TIMUserConfig`. After this feature is enabled, the IM SDK will send read receipts to the message sender when [sending message read reports](https://intl.cloud.tencent.com/document/product/1047/34324).

To register a read receipt listener, use `setMessageReceiptListener` of `TIMUserConfig`. To check whether the current message has been read by the recipient, use `isPeerReaded` of `TIMMessage`.

**Prototype:**

```
/**
 * Enable the read receipt feature. Then, read receipts will be sent to the message sender when message read reports are reported. This feature applies only to C2C conversations.
 */
public void enableReadReceipt()

/**
 * Set the read receipt listener.
 * @param receiptListener Read receipt listener
 */
public void setMessageReceiptListener(TIMMessageReceiptListener receiptListener)

/**
 * Check whether the recipient has read the message. (This feature applies only to C2C messages.)
 * @return true: read by the recipient. false: not read by the recipient.
 */
public boolean isPeerReaded()
```

### Message sequence number

To obtain the sequence number of the current message, use `getSeq` of `TIMMessage`.

```
/**
 * Obtain the sequence number of the current message.
 * @return Sequence number of the current message
 */
public long getSeq()
```

### Message random number

To obtain the random number of the current message, use `getRand` of `TIMMessage`.

```
/**
 * Obtain the random number of the current message.
 * @return Random number of the current message
 */
public long getRand()
```

### Message query parameters

In the IM SDK, a message is identified by a `{seq, rand, timestamp, isSelf}` quad, which represents the query parameters of the message. To obtain query parameters of the current message, use `getMessageLocator` of `TIMMessage`.

```
/**
 * Obtain the query parameters of the current message.
 * @return Query parameters of the current message
 */
public TIMMessageLocator getMessageLocator()
```

## Conversation Operations

### Obtaining all conversations

Use `getConversationList` of `TIMManager` to obtain the current number of conversations and all local conversations.
>! The SDK continuously updates the conversation list internally. The update will be sent back to the caller using `TIMRefreshListener.onRefresh`. **Call `getConversationList` after `onRefresh`** to update the conversation list.

**Prototype:**

```
/**
 * Obtain all conversations.
 * @return Conversation list
 */
public List<TIMConversation> getConversationList()
```

**Example:**

```
List<TIMConversation> list = TIMManager.getInstance().getConversationList();
```

### Recent contact roaming

By default, after the user logs in to the IM SDK, the IM SDK enables recent contact roaming and obtains the last message of each conversation.

### Obtaining local messages in a conversation

The IM SDK stores messages locally. To obtain these messages, use `getLocalMessage` of `TIMConversation`. This is an asynchronous method, and a callback needs to be set to obtain message data. **For a C2C conversation, offline messages will be obtained automatically after login. For a group conversation, when recent contacts roaming is enabled, only the last message is obtained after login, and roaming messages can be obtained using `getMessage`.**

 >! For resource messages such as image and audio messages, the message body only contains descriptive information, and additional APIs are required to download data. For more information, see Parsing Messages. The actual data downloaded is not cached, and must be cached by the caller.


**Prototype:**

```
/**
 * Obtain only the local chat history.
 * @param count Number of messages as of the last message
 * @param lastMsg Last message that was obtained. "null" indicates the latest message.
 * @param callback Callback that returns the list of obtained messages
 */
public void getLocalMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack<List<TIMMessage>> callback)
```

**Example:**

```
// Obtain a conversation extension instance.
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.Group, groupId);

// Obtain all messages of this conversation.
con.getLocalMessage(10, // Obtain the last 10 messages in this conversation.
        null, // The start message from which messages are obtained is not specified. In this case, the operation starts from the latest message.
        new TIMValueCallBack<List<TIMMessage>>() {// Callback API
    @Override
    public void onError(int code, String desc) {// Failed to obtain the messages.
        // "code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "get message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(List<TIMMessage> msgs) {// Succeeded in obtaining messages.
        // Traverse the obtained messages.
        for(TIMMessage msg : msgs) {
            lastMsg = msg;
            // The message timestamp can be obtained through `timestamp()`. `isSelf()` indicates whether the message was sent by yourself.
            Log.e(tag, "get msg: " + msg.timestamp() + " self: " + msg.isSelf() + " seq: " + msg.getSeq());
        }
    }
});
```

### Obtaining roaming messages in a conversation

For group conversations, a user can obtain roaming messages after login. For C2C conversations, the user can obtain roaming messages after the roaming service is enabled. To obtain roaming messages, use `getMessage` of `TIMConversation`. If local messages are continuous, they are obtained directly, instead of over the network. If local messages are not continuous, missing messages need to be obtained over the network.

 >! For resource messages such as image and audio messages, the message body only contains descriptive information, and additional APIs are required to download data, which can participate in message parsing. The actual data downloaded is not cached, and must be cached by the caller.

**Prototype:**

```
/**
 * Obtain the chat history.
 * @param count Number of messages as of the last message
 * @param lastMsg Last message that was obtained
 * @param callback Callback that returns the list of obtained messages
 */
public void getMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack< List<TIMMessage> > callback)
```

**Example:**

```
// Obtain a conversation extension instance.
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.Group, groupId);

// Obtain all messages of this conversation.
con.getMessage(10, // Obtain the last 10 message in this conversation.
        null, // The start message from which messages are obtained is not specified. In this case, the operation starts from the latest message.
        new TIMValueCallBack<List<TIMMessage>>() {// Callback API
    @Override
    public void onError(int code, String desc) {// Failed to obtain the messages.
        // "code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        // For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "get message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(List<TIMMessage> msgs) {// Succeeded in obtaining messages.
        // Traverse the obtained messages.
        for(TIMMessage msg : msgs) {
            lastMsg = msg;
            // The message timestamp can be obtained through `timestamp()`. `isSelf()` indicates whether the message was sent by yourself.
            Log.e(tag, "get msg: " + msg.timestamp() + " self: " + msg.isSelf() + " seq: " + msg.msg.seq());

        }
    }
});
```


### Deleting conversations

While deleting a conversation, the IM SDK also deletes the local and roaming messages of this conversation, and the deleted conversation and messages cannot be recovered.

**Prototype:**

```
/**
 * Delete a conversation stored locally and on the server, as well as all messages of this conversation that are stored locally and on the server.
 *
 * @param type Conversation type
 * @param peer Peer in the conversation. For a C2C conversation, use the peer's account identifier. For a group conversation, use the group ID.
 * @return true: deleted successfully. false: failed to delete.
 */
public boolean deleteConversation(TIMConversationType type, String peer)

```

The following example shows how to delete the C2C conversation with user1. **Example:**

```
TIMManager.getInstance().deleteConversation(TIMConversationType.C2C, "user1");
```

### Synchronously obtaining the last message of a conversation

The UI displays the last messages from users in the recent contact list. The IM SDK provides the `getLastMsg` API in `TIMConverstion` to synchronously obtaining the last message of a conversation, allowing the user to obtain and display the last message. **This feature requires a network connection. If recent contacts are disabled, the last message of a conversation cannot be obtained after login and before new messages are received.** Messages obtained using this API include deleted messages, which need to be blocked by the app. To obtain multiple recent messages, use `getMessage`.

**Prototype:**

```
/**
 * Obtain the last message from the cache.
 * @return Last message. "null" is returned if the conversation is invalid.
 */
public TIMMessage getLastMsg()

/**
 * Obtain the chat history.
 * @param count Number of messages as of the last message
 * @param lastMsg Last message that was obtained
 * @param callback Callback that returns the list of obtained messages
 */
public void getMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack< List<TIMMessage> > callback)
```


### Setting conversation drafts

The IM SDK provides the conversation draft feature. Developers can call APIs of `TIMConversation` to perform draft-related operations.

>!
> - Drafts are only valid locally. Users cannot see their drafts after switching devices or clearing the data.
> - Drafts are stored in a local database and can be obtained after users log in again.

**Prototype:**

```
/**
 * Set a draft.
 * @param Draft content. If it is null, the draft is canceled.
 */
public void setDraft(TIMMessageDraft draft)

/**
 * Obtain the draft.
 * @return Draft content
 */
public TIMMessageDraft getDraft()

/**
 * Check whether a draft is created for the current conversation.
 * @return true: yes. false: no.
 */
public boolean hasDraft()
```

**`TIMMessageDraft` is described as follows:**

```
/**
 * Obtain the list of message elements in a draft.
 * @return List of message elements
 */
public List<TIMElem> getElems()

/**
 * Set message elements in a draft.
 * @param elem Message elements to be added to the draft
 */
public void addElem(TIMElem elem)

/**
 * Obtain user-defined data in a draft.
 * @return User-defined data
 */
public byte[] getUserDefinedData()

/**
 * Set user-defined data in a draft.
 * @param userDefinedData User-defined data
 */
public void setUserDefinedData(byte[] userDefinedData)

/**
 * Obtain the edit time of a draft.
 * @return Edit time of the draft
 */
public long getTimestamp()
```
### Deleting messages of a conversation

The IM SDK allows you to delete the local and roaming messages of a conversation, and deleted messages cannot be recovered.


**Prototype:**
```
/**
 * Delete the local and roaming messages of the current conversation.
 * 
 * While deleting the local historical messages, this API also deletes the roaming messages stored on the server. After the IM SDK is uninstalled and then re-installed, these roaming messages cannot be pulled again. Note that:
 *  1. Up to 30 messages can be deleted at a time.
 *  2. The API can be called only one time per second.
 *  3. If this account has been used to pull roaming messages on other devices, and the API is called to delete these messages, these messages still exist on those devices. In short, message deletion cannot be synchronized across multiple terminals.
 */
public void deleteMessages(List<TIMMessage> messages, TIMCallBack callback)
```

### Searching for local messages

The IM SDK allows users to search for messages based on given parameters. Currently, only exact search is available, and fuzzy search is not supported. Developers can use the `findMessages` method of `TIMConversation` to search for messages.


```
/**
 * Search for messages based on given parameters.
 * @param locators Message search parameters
 * @param cb Callback, which returns matching messages
 */
public void findMessages(@NonNull List<TIMMessageLocator> locators, TIMValueCallBack<List<TIMMessage>> cb)
```

`TIMMessageLocator` can be obtained using the `getMessageLocator` method of `TIMMessage`.

**Prototype:**

```
/**
 * Obtain the locator of the current message.
 * @return Locator of the current message
 */
public TIMMessageLocator getMessageLocator()
```

### Recalling messages

Starting from version 3.1.0, the IM SDK provides an API to recall messages. To recall sent messages, call the `revokeMessage` API of `TIMConversation`.

>!
> - The API applies only to C2C and group conversations, and not to onlineMessages, AVChatRooms, or BChatRooms.
> - By default, only messages that were sent within the last 2 minutes can be recalled.

**Prototype:**

```
/**
 * Recall a message. (This API applies only to C2C and group conversations, and not to onlineMessages, AVChatRooms, or BChatRooms.)
 * @param msg Message to be recalled
 * @param cb Callback
 * @since 3.1.0
 */
public void revokeMessage(@NonNull TIMMessage msg, @NonNull TIMCallBack cb)
```

After a message is recalled, other members in the group or the peer in the C2C conversation will receive a message recall notification. In addition, the message recall notification listener `TIMMessageRevokeListener` notifies the upper-layer app. You can configure the message recall notification listener before login using `setMessageRevokedListener` of `TIMUserConfig`. For more information, see [User Configuration](https://intl.cloud.tencent.com/document/product/1047/36255).

**Prototype:**

```
/**
 * Message recall notification listener
 * @since 3.1.0
 */
public interface TIMMessageRevokedListener extends IMBaseListener {
    /**
     * Message recall notification
     * @param locator Locator of the recalled message
     */
     void onMessageRevoked(TIMMessageLocator locator);
}

```

After receiving a message recall notification, use the `checkEquals` method of `TIMMessage` to check whether the current message has been recalled by the sender and then refresh the UI when necessary.

**Prototype:**

```
/**
 * Compare the current message with the message specified by the given locator to check whether they are the same message.
 * @param locator Message locator
 * @return true: yes. false: no
 * @since 3.1.0
 */
public boolean checkEquals(@NonNull TIMMessageLocator locator)

```

## System Messages

In addition to C2C conversations and group conversations, system message is another conversation type (TIMConversationType). System messages are notifications that are sent by the system backend for various events. These messages cannot be sent by users. Currently, there are two types of system messages: relationship chain system messages and group system messages.

- The system sends a relationship chain change message when a user adds you as a friend or deletes you from his or her friend list. The developer can then update the friend list. For more information, see [System Notifications for Relationship Chain Changes](https://intl.cloud.tencent.com/document/product/1047/34332).
- When the group profile is modified, for example, due to a change to the group name or group members, the system sends a group event message in the group. The developer can choose whether to display the message and, at the same time, refresh the group profile or group members. For more information, see [Group Event Messages](https://intl.cloud.tencent.com/document/product/1047/36271#.E7.BE.A4.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF).
- When the group admin removes a member from the group or invites a user to join the group, the system sends a group system message to the user. For more information, see [Group System Messages](https://intl.cloud.tencent.com/document/product/1047/36271#.E7.BE.A4.E7.B3.BB.E7.BB.9F.E6.B6.88.E6.81.AF).


## Setting Backend Message Notification Bar Reminders

When the IM SDK is running in the background, it can continue to receive message notifications. If the program is running in the background, you can present new messages to users in the form of system notification bar reminders. New messages can be displayed in the notification bar on the top of the screen, in the notification center, or on the lock screen. See the following example for the implementation method:

**Example:**

```
NotificationManager mNotificationManager = (NotificationManager) context.getSystemService(context.NOTIFICATION_SERVICE);
NotificationCompat.Builder mBuilder = new NotificationCompat.Builder(context);
Intent notificationIntent = new Intent(context, MainActivity.class);
notificationIntent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP| Intent.FLAG_ACTIVITY_SINGLE_TOP);
PendingIntent intent = PendingIntent.getActivity(context, 0, notificationIntent, 0);
mBuilder.setContentTitle(senderStr)// Set the notification bar title.
            .setContentText(contentStr)
            .setContentIntent(intent) // Set the notification bar click intent.
            .setNumber(++pushNum) // Set the number of notifications in a collection.
            .setTicker(senderStr+":"+contentStr) // The notification appears in the notification bar for the first time with a rising animation effect.
            .setWhen(System.currentTimeMillis())// Generation time of the notification, which is displayed in the notification information. It is normally the time obtained by the system.                  
            .setDefaults(Notification.DEFAULT_ALL)// The simplest and most consistent way to add sound, flash, and vibration effects to notifications is to use the current default settings. The `defaults` properties can be used in combination.                        
            .setSmallIcon(R.drawable.ic_launcher);// Set the small icon for notifications.
Notification notify = mBuilder.build();
notify.flags |= Notification.FLAG_AUTO_CANCEL;
mNotificationManager.notify(pushId, notify);
```
