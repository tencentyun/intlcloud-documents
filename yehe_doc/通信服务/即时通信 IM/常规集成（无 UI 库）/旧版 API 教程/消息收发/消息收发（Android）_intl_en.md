
Send messages

### Sending common messages

**Obtain a conversation:** conversations are classified into conversations with a user or a group. To send or receive messages in a conversation, you need to first obtain the conversation by specifying the conversation type (one-to-one chat or group chat) and the peer's identifier (the peer's account or group ID). To obtain a conversation, use `getConversation` of `TIMManager`.

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
//Obtain a one-to-one chat.
String peer = "sample_user_1";  //Obtain the conversation with user "sample_user_1".
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.C2C,    // Conversation type: one-to-one chat
        peer);                      //Peer's account//Peer's ID
 
//Obtain a group chat.
String groupId = "TGID1EDABEAEO";  //Obtain the conversation with group "TGID1LTTZEAEO".
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.Group,      //Conversation type: group chat
        groupId);                       //Group ID
```

**Send messages:** After `TIMConversation` is obtained using `TIMManager`, you can send messages and obtain cached messages for the conversation. For more information about the interpretation of messages in the IM SDK, see [Introduction to IM SDK Objects](https://intl.cloud.tencent.com/document/product/1047/34301). In the IM SDK, a message is a `TIMMessage` object. A `TIMMessage` can contain multiple `TIMElem` units, which can be text or images. That is, a message can contain multiple text segments and images.

![](https://main.qcloudimg.com/raw/5b109b81e56ac31a6c73ca6053a342ff.png)

To send messages, use the `sendMessage` method of `TIMConversation`.

**Prototype:**

```
/**
 * Send messages.
 * @param msg Message
 * @param callback Callback
 */
public void sendMessage(@NonNull TIMMessage msg, @NonNull TIMValueCallBack<TIMMessage> callback)
```

### Sending text messages

A text message is defined by `TIMTextElem`. **The member methods of `TIMTextElem` are as follows:**

```
//Obtain text content.
java.lang.String    getText()

//Set text content. 'text' passes the text message to send.
void    setText(java.lang.String text)
```

**Example:**

```
// Construct a message
TIMMessage msg = new TIMMessage();

//Add text content.
TIMTextElem elem = new TIMTextElem();
elem.setText("a new msg");

//Add elem to the message.
if(msg.addElement(elem) != 0) {
   Log.d(tag, "addElement failed");
   return;
}

//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending image messages

An image message is defined by `TIMImageElem`, which is a subclass of `TIMElem`. These messages can contain images. To send an image, add `TIMImageElem` to `TIMMessage` and send the image along with the message.

> `path` does not support file paths starting with `file://`. Therefore, the `file://` prefix must be removed.

**The member methods of `TIMImageElem` are as follows:**

```
/**
 * Obtain the list of images contained in Elem. It can be called when the IM SDK fetches Elem.
 * @return List of images contained in elem
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
 * @return Whether image upload is canceled
 */
public boolean cancelUploading()

/**
 * Obtain the ID of the image upload task. The returned value of this API is valid after sendMessage is called.
 * @return ID of the image upload task
 */
public int getTaskId()

/**
 * Obtain the image type.
 * @return Image type
 */
public int getImageFormat()
```

To send an image, you only need to set `path`, which is the image path. After the image is sent successfully, you can use `getImageList` to obtain all image types. `TIMImage` stores the image type, size, width, and height. To download binary data of the image, use `getImage`.

**The member methods of `TIMImage` are as follows:**

```
/**
 * Obtain the image.
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
 * Obtain uuid.
 * @return uuid, which can be used as the unique key for caching
 */
public String getUuid()

/**
 * Obtain the image size.
 * @return Image size
 */
public long getSize()

/**
 * Obtain the image height.
 * @return Image height
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
// Construct a message
TIMMessage msg = new TIMMessage();

//Add an image.
TIMImageElem elem = new TIMImageElem();
elem.setPath(Environment.getExternalStorageDirectory() + "/DCIM/Camera/1.jpg");
 
//Add elem to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the list of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```
### Sending emoji messages

An emoji message is defined by `TIMFaceElem`. The IM SDK does not provide emoji packages. Developers can use `index` to store index entries of emojis in their emoji packages. Alternatively, they can directly use `data` to store emoji binary data and the string key. Either way, users can customize the emojis, and the IM SDK only passes them through.

**The member methods of `TIMFaceElem` are as follows:**

```
/**
 * Obtain the emoji index.
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
// Construct a message
TIMMessage msg = new TIMMessage();

//Add an emoji.
TIMFaceElem elem = new TIMFaceElem();
elem.setData(sampleByteArray); //Custom byte[]
elem.setIndex(10);   //Custom emoji index
 
//Add elem to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```


### Sending audio messages

An audio message is defined by `TIMSoundElem`, where `data` stores audio data. For audio data, you need to provide the audio length in seconds.

>
> - A message can contain only one audio `Elem`. If multiple audio `Elem` objects are added, the `AddElem` function returns error 1 and the audio elements will not be added.
> - Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects may not be sorted in the order that they are sent. 
> - `path` does not support file paths starting with `file://`. The `file://` prefix must be removed.

**The member methods of `TIMSoundElem` are as follows:**

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
 * Set the path of the audio file to be uploaded. (If the file path is set, the audio file in the set file path will be uploaded first.)
 * @param path Audio file path
 */
public void setPath(String path)

/**
 * Obtain uuid.
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
 * Obtain the ID of the audio upload task. The returned value of this API is valid after sendMessage is called.
 * @return ID of the audio upload task
 */
public int getTaskId()

```

**Example:**

```
// Construct a message
TIMMessage msg = new TIMMessage();

//Add an audio file.
TIMSoundElem elem = new TIMSoundElem();
elem.setPath(filePath); //Enter the audio file path.
elem.setDuration(20);  //Enter the audio length.
 
//Add elem to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```
### Sending location messages

A location message is defined by `TIMLocationElem`, where `desc` stores the location description information, and `longitude` and `latitude` represent the location longitude and latitude, respectively.

**The member methods of `TIMLocationElem` are as follows:**

```
/**
 * Obtain location description.
 * @return Location description
 */
public String getDesc()

/**
 * Set location description.
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
// Construct a message
TIMMessage msg = new TIMMessage();

//Add location information.
TIMLocationElem elem = new TIMLocationElem();
elem.setLatitude(113.93);   //Set the latitude.
elem.setLongitude(22.54);   //Set the longitude.
elem.setDesc("Tencent Building");

//Add elem to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }
    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending file messages

A file message is defined by `TIMFileElem`. You can also view additional information such as the file display name.

>
> - Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects may not be sorted in the order that they are sent. 
> - `path` does not support file paths starting with `file://`. The `file://` prefix must be removed.
> - The maximum file size is 28 MB.

**The member methods of `TIMFileElem` are as follows:**

```
/**
 * Download and save a file to the specified path.
 * @param path Specified storage path
 * @param callback Callback
 */
public void getToFile(@NonNull final String path, @NonNull TIMCallBack callback)

/**
 * Obtain uuid.
 * @return uuid, which can be used as the unique key for caching
 */
public String getUuid()

/**
 * Obtain the file size.
 * @return File size
 */
public long getFileSize()

/**
 * Obtain the file display name.
 * @return File name
 */
public String getFileName()

/**
 * Set the file display name when sending the file.
 * @param fileName File name
 */
public void setFileName(String fileName)

/**
 * Obtain the path of the uploaded file. This method is valid only for message senders.
 * @return File path
 */
public String getPath()

/**
 * Set the path of the file to be uploaded. (If the file path is set, the file in the set file path will be uploaded first.)
 * @param path File path
 */
public void setPath(String path)

/**
 * Obtain the ID of the file upload task. The returned value of this API is valid after sendMessage is called.
 * @return ID of the file upload task
 */
public int getTaskId()
```

**Example:**

```
// Construct a message
TIMMessage msg = new TIMMessage();

//Add file content.
TIMFileElem elem = new TIMFileElem();
elem.setPath(filePath); //Set the file path.
elem.setFileName("myfile.bin"); //Set the file name for displaying the message.
 
//Add elem to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending custom messages

Developers can customize the message format and content when built-in message types cannot meet their special needs. The IM SDK only passes through custom messages. If iOS APNs push notifications are required, a push text description to be displayed needs to be provided. A custom message is defined by `TIMCustomElem`, where 'data' stores the binary data of the message, developers define the data format, and `desc` stores the description text. A message can contain multiple custom `Elem` objects, which can be mixed with other `Elem` objects. In offline push scenarios, the `desc` of each `Elem` is stacked and delivered.

**The member methods of `TIMCustomElem` are as follows:**

```
/**
 * Obtain custom data.
 * @return Custom data
 */
public byte[] getData()

/**
 * Set custom data.
 * @param data Custom data
 */
public void setData(byte[] data)

/**
 * Obtain custom description.
 * @return Custom description
 */
public String getDesc()

/**
 * Set custom description.
 * @param desc Custom description
 */
public void setDesc(String desc)

/**
 * Obtain the ext field pushed by the backend.
 * @return ext
 */
public byte[] getExt()

/**
 * Set the ext field pushed by the backend.
 * @param ext The ext field pushed by the backend.
 */
public void setExt(byte[] ext)

/**
 * Obtain a custom sound.
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
// Construct a message
TIMMessage msg = new TIMMessage();
 
//Custom message using the XML protocol
String sampleXml = "<!--?xml version='1.0' encoding="utf-8"?-->testTitlethis is custom msgtest msg body";
 
//Add custom content to TIMMessage.
TIMCustomElem elem ＝ new TIMCustomElem();
elem.setData(sampleXml.getBytes());      //Custom byte[]
elem.setDesc("this is one custom message"); //Custom description
 
//Add elem to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending short video messages

A short video message is defined by `TIMVideoElem`, which is a subclass of `TIMElem`. These messages can contain video snapshots and content. To send a short video, add `TIMVideoElem` to `TIMMessage` and send the video along with the message.

**`TIMVideoElem` prototype:**

```
/**
 * Obtain the ID of the short video upload task. The returned value of this API is valid after sendMessage is called.
 *
 * @return ID of the short video upload task
 */
public long getTaskId() {
    return this.taskId;
}

/**
 * Set short video information when sending the message.
 *
 * @param video Short video information. For more information, please see {@link TIMVideo}.
 */
public void setVideo(TIMVideo video) {
    this.video = video;
}

/**
 * Obtain video information.
 *
 * @return Video information. For more information, please see {@link TIMVideo}.
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
 * @param snapshot Short video snapshot information. For more information, please see {@link TIMSnapshot}.
 */
public void setSnapshot(TIMSnapshot snapshot) {
    this.snapshot = snapshot;
}

/**
 * Obtain video snapshot information.
 *
 * @return Video snapshot information. For more information, please see {@link TIMSnapshot}.
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

| Parameter | Description |
---|---
taskId | The upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Use TIMUploadProgressListener to listen to the upload progress.
videoPath | The path of the local video to send.
video | The video information. Set the type and duration parameters when sending the message.
snapshotPath | The local snapshot path of the short video to send.
snapshot | The snapshot information. Set the type, width, and height when sending the message.

The following example shows how to send a short video message. **Example:**

```
// Construct a message
TIMMessage msg = new TIMMessage();

//Construct a short video object.
TIMVideoElem ele = new TIMVideoElem();

TIMVideo video = new TIMVideo();
video.setDuaration(duration / 1000); //Set the video length.
video.setType("mp4"); // Set the video type.

TIMSnapshot snapshot = new TIMSnapshot(); 
snapshot.setWidth(width); // Set the video snapshot width.
snapshot.setHeight(height); // Set the video snapshot height.

ele.setSnapshot(snapshot);
ele.setVideo(video);
ele.setSnapshotPath(imgPath);
ele.setVideoPath(videoPath);

 
//Add elem to the message.
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

//Send the message.
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//The message was sent successfully.
        Log.e(tag, "SendMsg ok");
    }
});
```


### Elem order 

Currently, file and audio `Elem` objects may not be transferred in the order that they are added. Other `Elem` objects are transferred in the order that they are added. However, we recommend that you do not rely heavily on the `Elem` object sequence when processing elements. Instead, you should process elements by type to prevent process crashes when exceptions occur.


### Online messages

In some scenarios, you need to send online messages, which can only be received when a user is online. If the user is not online when the messages are sent, the user will not see them after the next login. Online messages can be used as notifications. However, online messages will not be stored nor included in the unread count. The API for sending online messages is similar to `sendMessage`.

> In versions earlier than 2.5.3, online messages apply only to one-to-one chats. In version 2.5.3 and later, online messages apply to group chats, excluding audio-video chat rooms (AVChatRoom) and broadcasting chat rooms (BChatRoom groups)

```
//Send an online message (the server does not save the message).
public void sendOnlineMessage(TIMMessage msg, TIMValueCallBack<TIMMessage> callback)
```

### Forwarding messages

You can use `copyFrom` of `TIMMessage` to easily copy the content of another message to the current message and resend the message to contacts.

**Prototype:**
```
/**
 * Copy message content to the current message, including elem, priority, online, and offlinePushInfo.
 * @param srcMsg Source message
 * @return true Copied successfully
 */
public boolean copyFrom(@NonNull TIMMessage srcMsg)
```


## Receiving Messages

To be notified of new messages, register the new message notification callback `TIMMessageListener`. If you have logged in, the IM SDK will use the `onNewMessages` callback to send new messages. For more information about how to register the new message notification callback, see New Message Notification.

> Messages obtained using `onNewMessages` may not be unread messages. They can also be messages that have not been displayed locally. For example, when messages are read on another client and the last messages of conversations obtained by getting recent contacts are not stored locally, these messages are sent using this method. After a user logs in, the IM SDK gets C2C offline messages. To avoid missing message notifications, the user needs to register new message notifications before login.
The `onNewMessage` callback is also used to send group system messages, relationship chain changes, and friend profile changes.

### Parsing messages

After receiving a message, use `getElem` to obtain all `Elem` nodes in `TIMMessage`. **The following is the prototype for traversing `Elem` nodes:**

```
//Obtain message elements.
TIMElem getElement(int i)

//Obtain the number of elements.
int getElementCount()
```

**Example:**

```
TIMMessage msg = /* Message */

for(int i = 0; i < msg.getElementCount(); ++i) {
	TIMElem elem = msg.getElement(i);

	//Obtain the type of the current element.
	TIMElemType elemType = elem.getType();
	Log.d(tag, "elem type: " + elemType.name());
	if (elemType == TIMElemType.Text) {
		//Process text messages.
	} else if (elemType == TIMElemType.Image) {
		//Process image messages.
	}//...Process more messages.
}
```


### Receiving image messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMElemType.Image` type are image message nodes. To obtain all image specifications, including the original image, large image, and thumbnail, use `getImageList` of `TIMImageElem`. Each specification is stored in a `TIMImage` object.

```
/**
 * Obtain the list of images contained in Elem. It can be called when the IM SDK fetches Elem.
 * @return List of images contained in elem
 */
public ArrayList<TIMImage> getImageList()
```

**`TIMImage`:**

After receiving a message, use imageList to obtain all image specifications, which are `TIMImage` objects. After obtaining `TIMImage`, reserve a place based on the image size and use `getImage` to download images of different specifications for display.

> Developers cache the downloaded data. The IM SDK downloads data from the server each time it calls `getImage`. We recommend that you use the `uuid` of an image as the `key` to store images.

**Image specifications:** each image has three specifications, Original (original image), Large (large image), and Thumb (thumbnail).

- **Original image:** the original image sent by a user, whose dimensions and size remain unchanged.
- **Large image:** an image obtained after the original image is proportionally compressed. The height or width of the compressed image, whichever is smaller, is equal to 720 pixels.
- **Thumbnail:** an image obtained after the original image is proportionally compressed. The height or width of the compressed image, whichever is smaller, is equal to 198 pixels.

>- If the size of the original image is less than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
>- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
>- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When a user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is downloaded when the user taps the thumbnail.
>- When an image is displayed on a tablet or PC, we recommend that the large image be displayed directly and the original image be downloaded when a user taps or clicks the large image due to the high resolution and availability of a Wi-Fi or wired network.

**Example:**

```
//Traverse the element list of a message.
for(int i = 0; i < msg.getElementCount(); ++i) {
    TIMElem elem = msg.getElement(i);
    if (elem.getType() == TIMElemType.Image) {
        //Image element
        TIMImageElem e = (TIMImageElem) elem;
        for(TIMImage image : e.getImageList()) {

            //Obtain the image type, size, width, and height.
            Log.d(tag, "image type: " + image.getType() +
                    " image size " + image.getSize() +
                    " image height " + image.getHeight() +
                    " image width " + image.getWidth());

            image.getImage(path, new TIMCallBack() {
                    @Override
                    public void onError(int code, String desc) {//Failed to obtain the image.
						//"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
						//For more information about the meaning of error codes, see the Error Code table.
						Log.d(tag, "getImage failed. code: " + code + " errmsg: " + desc);
                    }

                    @Override
                    public void onSuccess() {//Request succeeded, and the parameter is image data.
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

**Audio message read status:** You can use custom message fields to determine whether an audio message has been played. For example, the value 0 of `customInt` indicates that the audio has been played, and the value 1 indicates that the audio has not been played. After a user taps play, set `customInt` to 1. The following shows set custom integers, and the default value is 0.

**Prototype:**
```
public void setCustomInt(int value)
```


### Receiving file messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMFileElem` type are file message nodes.

**The member methods of `TIMFileElem` are as follows:**

```
//Download and save the file to the specified path.
void getToFile(String path, TIMCallBack callback)

//Obtain the file name.
java.lang.String    getFileName()

//Obtain the file size.
long    getFileSize()

//Obtain uuid.
java.lang.String    getUuid()

//Set the file name.
void    setFileName(java.lang.String fileName)
```

You can choose to display only the file size and display name of a received file message and use `getToFile` to download the file from the server each time. To cache or store the data, use `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.

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
After receiving a message, use getElem to obtain all Elem nodes from TIMMessage. Nodes of the TIMVideoElem type are short video message nodes. Use the TIMVideo and TIMSnapshot objects to obtain the video and snapshot content. After receiving TIMVideoElem, download the video file and snapshot file through the APIs defined in the video and snapshot properties. To cache or store the data, use `uuid` as the `key` to store the files externally. The IM SDK does not store resource files.

**The member methods of `TIMVideo` are as follows:**

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
* Obtain the uuid of the video file.
*
* @return uuid, which can be used as the unique key for caching
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

**The member methods of `TIMSnapshot` are as follows:**
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
 * Obtain the uuid of the snapshot file.
 *
 * @return uuid, which can be used as the unique key for caching
 */
String getUuid(); 
```

**Parsing process for short video messages:**
The new message receipt callback is used as an example. First, determine whether the message has TIMVideoElem based on the element type. If yes, it is a short video message. In this case, run the following code to parse it.

```
TIMMessage timMsg = msg.getTIMMessage();
final TIMVideoElem videoEle = (TIMVideoElem) timMsg.getElement(0);
final TIMVideo video = videoEle.getVideoInfo();
final TIMSnapshot shotInfo = videoEle.getSnapshotInfo();
final String path = ”/xxx/“ + videoEle.getSnapshotInfo().getUuid(); //Storage path of the received snapshot
final String videoPath = ”/xxx/“ + video.getUuid(); //Storage path of the received video
videoEle.getSnapshotInfo().getImage(path, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
        Log.e(tag, "Failed to download the snapshot, code = " + code + ", errorinfo = " + desc);
    }

    @Override
    public void onSuccess() {
        Log.d(tag, "Downloaded the snapshot successfully");
    }
});

video.getVideo(videoPath, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
	Log.e(tag, "Failed to download the short video, code = " + code + ", errorinfo = " + desc);
    }

    @Override
    public void onSuccess() {
        Log.d(tag, "Downloaded the short video successfully");
    }
});
```

## Message Properties

Message properties can be obtained using the member methods of `TIMMessage`.

### Checking whether a message has been read

Use `isRead` of `TIMMessage` to check whether a message has been read, which is determined by the [Unread Count](https://intl.cloud.tencent.com/document/product/1047/34324) on the app side. The message read prototype is as follows:

**Prototype:**
```
public boolean isRead()
```

### Message status

To obtain the status of the current message, such as sending, sent successfully, failed to send, and deleted, use the `status` method of `TIMMessage`. For deleted messages, use the UI to determine the status and hide them.
```
//Sending
TIMMessageStatus.Sending

//Sent successfully
TIMMessageStatus.SendSucc

//Failed to send
TIMMessageStatus.SendFail

//Deleted
TIMMessageStatus.HasDeleted

//Recalled
TIMMessageStatus.HasRevoked
```

### Checking whether a message was sent by oneself

To determine whether a message was sent by you yourself, use the `isSelf` method of `TIMMessage`. This method is available when it is displayed on the interface. The following shows the prototype for determining whether a message was sent by yourself.

**Prototype:**
```
public boolean isSelf()
```

### Message sender and related profile

To obtain the sender's ID, use the `getSender` method of `TIMMessage`.
**For one-to-one chat messages**, use the `getConversation` method of `TIMMessage` to obtain the corresponding conversation and use `getPeer` to obtain the recipient and the recipient's profile.
**For group chat messages**, use `getSenderProfile` and `getSenderGroupMemberProfile` to obtain the sender's profile and the profile of the group to which the sender belongs. To get custom fields, [set the fields to be pulled](https://intl.cloud.tencent.com/document/product/1047/34328) before logging in to the IM SDK.
 > This field obtains the user profile and writes it to the message body when the message is sent. If the user profile is updated, this field will not change unless new messages are generated.
 > You can obtain profiles only from received group messages.

```
/**
 * Obtain the message sender.
 * @return Message sender
 */
public String getSender()

/**
 * Obtain the sender's profile.
 *
 * Version 4.4.716 returns this information through a callback.
 *
 * @param callBack Callback
 */
public void getSenderProfile( TIMValueCallBack < TIMUserProfile > callBack )

/**
 * Obtain the sender's profile in the group, which is only available for received group messages (may be empty if the sender is yourself).
 *
 * @return Sender's profile in the group. "null" indicates that no profile was obtained or the message is not a group message. Currently, only the user, nameCard, role, and customInfo fields can be obtained. To obtain other fields, use getGroupMembers of TIMGroupManager.
 */
public TIMGroupMemberInfo getSenderGroupMemberProfile()
```


### Message time

To obtain the message time, use the `timestamp` method of `TIMMessage`. **This time is the server time, not the local time**. When you create a message, this time is calibrated based on the server time and will be changed to the accurate server time after the message is successfully sent.

```
//Timestamp generated for the message by the server
public long timestamp()
```

### Deleting messages

Currently, you cannot delete messages on the server and can only delete messages in local storage. To delete messages, use the `remove` method of `TIMMessage`. After the messages are deleted, using `getMessage` to get messages will not return the deleted messages.

```
/**
 * Mark a message as deleted.
 * @return Succeeded or failed
 */
public boolean remove()
```

### Message IDs

There are two types of message IDs. One is `msgId`, which is created when a message is generated. As this ID may conflict with messages generated by other users, a time dimension needs to be added. Messages generated within 10 minutes can be distinguished by `msgId`. The other is `uniqueId`, which is generated after a message is sent successfully and is globally unique. These two methods both need to be used for judgment in a conversation.

```
//Obtain the message ID.
public String getMsgId()

//Obtain the uniqueId of the message.
public long getMsgUniqueId()
```

### Custom message fields

Developers can add custom fields to messages, such as the custom integer and custom binary data fields, and can customize different effects based on these two fields. For example, custom fields can be used to determine whether an audio message has been played. Note that these custom fields are only stored locally and not synchronized to the server. You will not obtain them after switching to another client.

```
//Set the custom integer, which defaults to 0.
public void setCustomInt(int value)

//Obtain the custom integer value.
public int getCustomInt()

//Set custom data content, which defaults to "".
public void setCustomStr(String str)

//Obtain the value of the custom data content.
public String getCustomStr()
```

### Message priorities

Livestreaming scenarios involve the like and red packet features. Like messages have a lower priority than red packet messages. Use `TIMCustomElem` to define the message content and the message priority when the message is sent.
> Message priorities apply only to group messages.

```
//Set the message priority.
public void setPriority(TIMMessagePriority priority)

//Obtain the message priority.
public TIMMessagePriority getPriority()
```


### Read receipts

The IM SDK provides the read receipt feature for **C2C messages**, which can be enabled using `enableReadReceipt` of `TIMUserConfig`. After this feature is enabled, read receipts will be sent to the message sender when reporting [message read reports](https://intl.cloud.tencent.com/document/product/1047/34324).

To register a read receipt listener, use `setMessageReceiptListener` of `TIMUserConfig`. To check whether the current message has been read by the recipient, use `isPeerReaded` of `TIMMessage`.

**Prototype:**

```
/**
 * After the read receipt feature is enabled, read receipts will be sent to the message sender when read messages are reported. This feature applies only to one-to-one chats.
 */
public void enableReadReceipt()

/**
 * Set the read receipt listener.
 * @param receiptListener Read receipt listener
 */
public void setMessageReceiptListener(TIMMessageReceiptListener receiptListener)

/**
 * Check whether the recipient has read the message (applies only to C2C messages).
 * @return true: read by the recipient. false: not read by the recipient.
 */
public boolean isPeerReaded()
```

### Message sequence numbers

To obtain the sequence number of the current message, use `getSeq` of `TIMMessage`.

```
/**
 * Obtain the sequence number of the current message.
 * @return Sequence number of the current message
 */
public long getSeq()
```

### Message random numbers

To obtain the random number of the current message, use `getRand` of `TIMMessage`.

```
/**
 * Obtain the random number of the current message.
 * @return Random number of the current message
 */
public long getRand()
```

### Message query parameters

In the IM SDK, a specific message is identified by a `{seq, rand, timestamp, isSelf}` quad, which is called the query parameters of the message. To obtain query parameters of the current message, use `getMessageLocator` of `TIMMessage`.

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
> The SDK continuously updates the conversation list internally. The update will be sent back to the caller using `TIMRefreshListener.onRefresh`. **Call `getConversationList` after `onRefresh`** to update the conversation list.

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

By default, the IM SDK obtains recent contacts when roaming and the last message of each conversation after a user logs in.

### Obtaining local messages in a conversation

The IM SDK stores messages locally. To obtain these messages, use `getLocalMessage` of `TIMConversation`. This is an asynchronous method, and a callback needs to be set to obtain message data. **For one-to-one chats, offline messages will be obtained automatically after login. For group chats, only the last message is obtained after you log in with recent contacts roaming enabled, and roaming messages can be obtained using `getMessage`**.

 > Note:
 > For resource messages such as image and audio messages, the message body only contains descriptive information, and additional APIs are required to download data. For more information, please see the section about parsing messages. Downloaded data is not cached. The caller must cache the data.


**Prototype:**

```
/**
 * Obtain only the local chat history.
 * @param count Number of messages as of the last message
 * @param lastMsg Obtained last message. "null" indicates the latest message.
 * @param callback Callback that returns the list of obtained messages
 */
public void getLocalMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack<List<TIMMessage>> callback)
```

**Example:**

```
//Obtain a conversation extension instance.
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.Group, groupId);

//Obtain all messages of this conversation.
con.getLocalMessage(10, //Obtain the last 10 messages in this conversation.
        null, //The message starting from which messages are obtained is not specified. In this case, the operation starts from the last message.
        new TIMValueCallBack<List<TIMMessage>>() {//Callback API
    @Override
    public void onError(int code, String desc) {//Failed to obtain the messages.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "get message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(List<TIMMessage> msgs) {//Obtained messages successfully.
        //Traverse obtained messages.
        for(TIMMessage msg : msgs) {
            lastMsg = msg;
            //The message timestamp can be obtained through timestamp(). isSelf() indicates whether the message was sent by yourself.
            Log.e(tag, "get msg: " + msg.timestamp() + " self: " + msg.isSelf() + " seq: " + msg.getSeq());
        }
    }
});
```

### Obtaining roaming messages in a conversation

For group chats, a user can obtain roaming messages after login. For C2C chats, the user can obtain roaming messages after the roaming service is enabled. To obtain roaming messages, use `getMessage` of `TIMConversation`. If local messages are continuous, they are obtained directly. Otherwise, missing messages need to be obtained over the network.

 > For resource messages such as image and audio messages, the message body only contains descriptive information. Therefore, additional APIs are required to download data. For more information, please see the section about parsing messages. Downloaded data is not cached. The caller must cache the data.

**Prototype:**

```
/**
 * Obtain the chat history.
 * @param count Number of messages as of the last message
 * @param lastMsg Obtained last message
 * @param callback Callback that returns the list of obtained messages
 */
public void getMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack< List<TIMMessage> > callback)
```

**Example:**

```
//Obtain a conversation extension instance.
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.Group, groupId);

//Obtain all messages of this conversation.
con.getMessage(10, //Obtain the last 10 message in this conversation.
        null, //The message starting from which messages are obtained is not specified. In this case, the operation starts from the last message.
        new TIMValueCallBack<List<TIMMessage>>() {//Callback API
    @Override
    public void onError(int code, String desc) {//Failed to obtain the messages.
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For more information about the meaning of error codes, see the Error Code table.
        Log.d(tag, "get message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(List<TIMMessage> msgs) {//Obtained messages successfully.
        //Traverse obtained messages.
        for(TIMMessage msg : msgs) {
            lastMsg = msg;
            //The message timestamp can be obtained through timestamp(). isSelf() indicates whether the message was sent by yourself.
            Log.e(tag, "get msg: " + msg.timestamp() + " self: " + msg.isSelf() + " seq: " + msg.msg.seq());

        }
    }
});
```


### Deleting conversations

`TIMManager` in the IM SDK provides two methods to delete conversations in different scenarios. One is to delete the conversation and retain all messages, and the other is to delete the conversation together with all its messages.

>
> - After local messages of C2C conversations are deleted, you cannot obtain the message history before the C2C conversations are deleted.
> - After local messages of group conversations are deleted, `getMessage` can be used to get roaming messages. Therefore, it is possible that the message history before the conversation is deleted can still be pulled after messages are deleted successfully. If you do not need to get roaming messages, use `getLocalMessage` to obtain messages or use `getMessage` to get a specified number of messages, such as a certain number of unread messages.

**Prototype:**

```
/**
 * Delete conversation cache.
 * @param type Conversation type
 * @param peer Peer in the conversation. For a C2C conversation, use the peer's account identifier. For a group conversation, use the group ID.
 * @return true: succeeded. false: failed.
 */
public boolean deleteConversation(TIMConversationType type, String peer)


/**
 * Delete conversation cache and local messages related to this conversation.
 * @param type Conversation type
 * @param peer Peer in the conversation. For a C2C conversation, use the peer's account identifier. For a group conversation, use the group ID.
 * @return true: succeeded. false: failed.
 */
public boolean deleteConversationAndLocalMsgs(TIMConversationType type, String peer)
```

The following example shows how to delete the C2C conversation with the user named hello. **Example:**

```
TIMManager.getInstance().deleteConversation(TIMConversationType.C2C, "hello");
```

### Synchronously obtaining the last message of a conversation

The UI displays the last messages from users in the recent contact list. The IM SDK provides the `getLastMsg` API to synchronize the latest messages from conversations, allowing users to obtain and display the last messages. **This feature requires a network connection. If recent contacts are disabled, the latest messages cannot be obtained after login and before new messages are received**. Messages obtained using this API contain deleted messages, which need to be blocked by the app. To obtain multiple recent messages, use `getMessage`.

**Prototype:**

```
/**
 * Obtain the last message from cache.
 * @return Last message. "null" is returned if the conversation is invalid.
 */
public TIMMessage getLastMsg()

/**
 * Obtain the chat history.
 * @param count Number of messages as of the last message
 * @param lastMsg Obtained last message
 * @param callback Callback that returns the list of obtained messages
 */
public void getMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack< List<TIMMessage> > callback)
```


### Setting conversation drafts

The IM SDK provides the conversation draft feature. Developers can call APIs of `TIMConversation` to perform draft-related operations.

>
> - Drafts are only valid locally. Users cannot see their drafts after switching devices or clearing the data.
> - Draft information is stored in a local database and can be obtained after users log in again.

**Prototype:**

```
/**
 * Set a draft.
 * @param draft Draft content. If it is null, the draft is canceled.
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

**The following describes `TIMMessageDraft`:**

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
### Deleting local messages of a conversation

The IM SDK allows you to clear the local chat history while retaining the conversation. To do this, call `deleteLocalMessage` of `TIMConversation`.

> After the local message history of a group conversation is deleted, locally deleted historic messages can still be pulled through roaming.


**Prototype:**
```
/**
 * Batch delete all the historical messages of a conversation.
 * @param callback Callback
 */
public void deleteLocalMessage(@NonNull TIMCallBack callback)
```

### Searching for local messages

The IM SDK allows you to search for messages based on given parameters. Currently, only exact search is available, and fuzzy search is not supported. Developers can use the `findMessages` method of `TIMConversation` to search for messages.


```
/**
 * Search for messages based on given parameters.
 * @param locators Message search parameters
 * @param cb Callback, which returns hit messages
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

>
> - The API applies only to C2C and group conversations, not to onlineMessages, AVChatRooms, or BChatRooms.
> - By default, only messages that were sent within the last 2 minutes can be recalled.

**Prototype:**

```
/**
 * Message recalling applies only to C2C and group conversations, not to onlineMessages, AVChatRooms, or BChatRooms.
 * @param msg Message to be recalled
 * @param cb Callback
 * @since 3.1.0
 */
public void revokeMessage(@NonNull TIMMessage msg, @NonNull TIMCallBack cb)
```

After a message is recalled, other members in the group or the other participant in the C2C conversation will receive a message recall notification. In addition, the message recall notification listener `TIMMessageRevokeListener` notifies the upper-layer app. You can configure the message recall notification listener before login using `setMessageRevokedListener` of `TIMUserConfig`. For more information, see [User Configuration](https://intl.cloud.tencent.com/document/product/1047/34312).

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
 * Compare the current message with the message specified by the given locator to check whether they refer to the same message.
 * @param locator Message locator
 * @return true: yes. false: no.
 * @since 3.1.0
 */
public boolean checkEquals(@NonNull TIMMessageLocator locator)

```

## System Messages

In addition to C2C chat and group chat messages, another conversation type (TIMConversationType) is system messages. System messages are notifications sent by the system backend for various events and that cannot be sent by users. Currently, there are two types of system messages: relationship chain system messages and group system messages.

- The system sends relationship chain change messages when a user adds you as a friend or deletes you from his or her friend list. The developer can then update the friend list. For more information, see [System Notifications for Relationship Chain Changes](https://intl.cloud.tencent.com/document/product/1047/34332).
- When the group profile is modified, such as by a change to the group name or group members, the system sends a group event message in the group. The developer can choose whether to display the message and can refresh the group profile or group members at the same time. For more information, see [Group Event Messages](https://intl.cloud.tencent.com/document/product/1047/34328#.E7.BE.A4.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF).
- When the group admin removes a member from the group or invites a user to the group, the system sends a group system message to users. For more information, see [Group System Messages](https://intl.cloud.tencent.com/document/product/1047/34328#.E7.BE.A4.E7.B3.BB.E7.BB.9F.E6.B6.88.E6.81.AF).


## Setting Backend Message Notification Bar Reminders

When the IM SDK is running in the background, it can continue to receive message notifications. If the program is running in the background, you can present new messages to users in the form of a system notification bar reminders. New messages can be displayed in the notification bar on the top of the interface, in the notification center, or on the lock screen. See the following example for the implementation method:

**Example:**

```
NotificationManager mNotificationManager = (NotificationManager) context.getSystemService(context.NOTIFICATION_SERVICE);
NotificationCompat.Builder mBuilder = new NotificationCompat.Builder(context);
Intent notificationIntent = new Intent(context, MainActivity.class);
notificationIntent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP| Intent.FLAG_ACTIVITY_SINGLE_TOP);
PendingIntent intent = PendingIntent.getActivity(context, 0, notificationIntent, 0);
mBuilder.setContentTitle(senderStr)//Set the notification bar title.
            .setContentText(contentStr)
            .setContentIntent(intent) //Set the notification bar click intent.
            .setNumber(++pushNum) //Set the number of notifications in a collection.
            .setTicker(senderStr+":"+contentStr) //The notification appears in the notification bar for the first time with a rising animation effect
            .setWhen(System.currentTimeMillis())//Generation time of the notification, which is displayed in the notification information. It is normally the time obtained by the system.                  
            .setDefaults(Notification.DEFAULT_ALL)//The simplest and most consistent way to add sounds, flashing, and vibration to notifications is to use the current default settings. To do this, use the defaults property, which can be used in combination.                        
            .setSmallIcon(R.drawable.ic_launcher);//Set the small icon for notifications.
Notification notify = mBuilder.build();
notify.flags |= Notification.FLAG_AUTO_CANCEL;
mNotificationManager.notify(pushId, notify);
```
