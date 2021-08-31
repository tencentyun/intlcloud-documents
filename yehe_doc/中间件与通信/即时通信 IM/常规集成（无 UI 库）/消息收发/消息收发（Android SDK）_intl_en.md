## Sending Messages

### Sending common messages

**Obtain a conversation:** a conversation refers to a conversation with a user or a group. To send or receive messages in a one-to-one or group conversation, you need to first obtain the conversation by specifying the conversation type (one-to-one chat or group chat) and the peer’s identifier (the peer’s account or group ID). Use `getConversation` in `TIMManager` to obtain a conversation.

**Prototype:**

```
/**
 * Obtain a conversation
 * @param type Conversation type
 * @param peer The peer in the conversation. For a C2C conversation, use the peer’s identifier. For a group conversation, use the group ID.
 * @return A conversation instance
 */
public TIMConversation getConversation(TIMConversationType type, String peer)
```

**Example:**

```
//Obtain a one-to-one conversation
String peer = "sample_user_1";  //Obtain the conversation with user "sample_user_1"
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.C2C,    //Conversation type: one-to-one chat
        peer);                      //User account of the peer in the conversation//Peer’s ID
 
//Obtain a group conversation
String groupId = "TGID1EDABEAEO";  //Obtain the conversation with group "TGID1LTTZEAEO"
conversation = TIMManager.getInstance().getConversation(
        TIMConversationType.Group,      //Conversation type: group chat
        groupId);                       //Group ID
```

**Sending messages:** after obtaining a `TIMConversation` instance through `TIMManager`, you can send messages and obtain the cached messages of the conversation. See [Introduction to IM SDK Objects](https://intl.cloud.tencent.com/document/product/1047/34301) for the explanation of a message in the IM SDK. In the IM SDK, a message is a `TIMMessage` object. A `TIMMessage` object can contain multiple `TIMElem` objects, which can be text segments or images. That is, a message can contain multiple text segments and images.

![](https://main.qcloudimg.com/raw/5b109b81e56ac31a6c73ca6053a342ff.png)

To send messages, use the `sendMessage` method of `TIMConversation`.

**Prototype:**

```
/**
 * Send a message
 * @param msg Message
 * @param callBack Callback
 */
public void sendMessage(@NonNull TIMMessage msg, @NonNull TIMValueCallBack<TIMMessage> callback)
```    

### Sending text messages

A text message is defined by `TIMTextElem`. **The member methods of `TIMTextElem` are as follows:**

```
//Obtain text content
java.lang.String    getText()

//Set text content, and the text message to be sent is passed by ‘text’
void    setText(java.lang.String text)
```

**Example:**

```
//Construct a message
TIMMessage msg = new TIMMessage();

//Add text content
TIMTextElem elem = new TIMTextElem();
elem.setText("a new msg");

//Add elem to the message
if(msg.addElement(elem) != 0) {
   Log.d(tag, "addElement failed");
   return;
}

//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending image messages

An image message is defined by `TIMImageElem`, which is a subclass of `TIMElem`. Image messages can contain images. In this case, sending an image is actually adding `TIMImageElem` to `TIMMessage` and sending it along with the message.

>`path` does not support file paths starting with `file://`. Therefore, the `file://` prefix must be removed.

**The member methods of `TIMImageElem` are as follows:**

```
/**
 * The following method can be called when the IM SDK fetches elem to obtain the image list from elem.
 * @return List of images contained in elem
 */
public ArrayList<TIMImage> getImageList()

/**
 * Obtain the local file path of the original image. This method is only valid for message senders.
 * @return Local file path
 */
public String getPath()

/**
 * Set the file path of the original image to be sent
 * @param path File path of the original image
 */
public void setPath(String path)

/**
 * Obtain the image quality level
 * @return Image quality level. 0: original image. 1: highly compressed image (small image). 2: high-resolution image (large image).
 */
public int getLevel()

/**
 * Set the image quality level
 * @param level 0: original image. 1: highly compressed image (small image). 2: high-resolution image (large image).
 */
public void setLevel(int level)

/**
 * Cancel image upload
 * @return Whether canceling the image upload succeeded
 */
public boolean cancelUploading()

/**
 * Obtain the ID of the image upload task. The returned value of this API is valid after sendMessage is called.
 * @return ID of the image upload task
 */
public int getTaskId()

/**
 * Obtain the image type
 * @return Image type
 */
public int getImageFormat()
```

To send an image, you only need to set `path`, that is, the image path. After the image is sent successfully, you can obtain all image formats through `getImageList`. `TIMImage` stores the format, size, width, and height of the image. The binary data of the image can be downloaded through `getImage`.

**The member methods of `TIMImage` are as follows:**

```
/**
 * Obtain the image
 * @param path Image storage path
 * @param cb Callback
 */
public void getImage(@NonNull final String path, @NonNull final TIMCallBack cb)

/**
 * Obtain the image type
 * @return Image type
 */
public TIMImageType getType()

/**
 * Obtain uuid
 * @return uuid, which can be used as the unique key for caching
 */
public String getUuid()

/**
 * Obtain the image size
 * @return Image size
 */
public long getSize()

/**
 * Obtain the image height
 * @return Image height
 */
public long getHeight()

/**
 * Obtain the image width
 * @return Image width
 */
public long getWidth()

/**
 * Obtain the image URL
 * @return Image URL
 */
public String getUrl()

```

**Example:**


```
//Construct a message
TIMMessage msg = new TIMMessage();

//Add an image
TIMImageElem elem = new TIMImageElem();
elem.setPath(Environment.getExternalStorageDirectory() + "/DCIM/Camera/1.jpg");
 
//Add elem to the message
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the list of error codes, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```
### Sending emoji messages

An emoji message is defined by `TIMFaceElem`. The IM SDK does not provide emoji packages. Developers can use `index` to store the index entries of the emojis in their emoji packages. Alternatively, they can directly use `data` to store emoji binary data and the string key. In either way, users can customize the emojis, and the IM SDK is only responsible for passing them through.

**The member methods of `TIMFaceElem` are as follows:**

```
/**
 * Obtain the emoji index
 * @return Emoji index
 */
public int getIndex()

/**
 * Set the emoji index
 * @param index Emoji index
 */
public void setIndex(int index)

/**
 * Obtain emoji custom data
 * @return Emoji custom data
 */
public byte[] getData()

/**
 * Set emoji custom data
 * @param data Emoji custom data
 */
public void setData(byte[] data)
```

**Example:**

```
//Construct a message
TIMMessage msg = new TIMMessage();

//Add an emoji
TIMFaceElem elem = new TIMFaceElem();
elem.setData(sampleByteArray); //Custom byte[]
elem.setIndex(10);   //Custom emoji index
 
//Add elem to the message
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```


### Sending audio messages

An audio message is defined by `TIMSoundElem`, where `data` stores audio data, for which you need to provide the audio length in seconds.

>
> - A message can contain only one audio `Elem`. If multiple audio `Elem` objects are added, the `AddElem` function returns error 1 and the audio elements will not be added.
> - Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects are not guaranteed to be sorted in the order that they are sent. 
>`path` does not support file paths starting with `file://`. The `file://` prefix must be removed.

**The member methods of `TIMSoundElem` are as follows:**

```
/**
 * Download and save an audio file to the specified path
 * @param path Specified storage path
 * @param callback Callback
 */
public void getSoundToFile(@NonNull final String path, @NonNull TIMCallBack callback)

/**
 * Obtain the path of the audio file to be sent. This method is only valid for message senders.
 * @return Audio file path
 */
public String getPath()

/**
 * Set the path of the audio file to be uploaded (if the file path is set, the audio file will be uploaded first)
 * @param path Audio file path
 */
public void setPath(String path)

/**
 * Obtain uuid
 * @return uuid
 */
public String getUuid()

/**
 * Obtain the length of binary data
 * @return Length of binary data
 */
public long getDataSize()

/**
 * Obtain the audio length
 * @return Audio length
 */
public long getDuration()

/**
 * Set the audio length
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
//Construct a message
TIMMessage msg = new TIMMessage();

//Add an audio file
TIMSoundElem elem = new TIMSoundElem();
elem.setPath(filePath); //Enter the audio file path
elem.setDuration(20);  //Enter the audio length
 
//Add elem to the message
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```
### Sending location messages

A location message is defined by `TIMLocationElem`, where `desc` stores the descriptive information of the location, and `longitude` and `latitude` represent the longitude and latitude of the location respectively.

**The member methods of `TIMLocationElem` are as follows:**

```
/**
 * Obtain location description
 * @return Location description
 */
public String getDesc()

/**
 * Set location description
 * @param desc Location description
 */
public void setDesc(String desc)

/**
 * Obtain the longitude
 * @return Longitude
 */
public double getLongitude()

/**
 * Set the longitude
 * @param longitude Longitude
 */
public void setLongitude(double longitude)

/**
 * Obtain the latitude
 * @return Latitude
 */
public double getLatitude()

/**
 * Set the latitude
 * @param latitude Latitude
 */
public void setLatitude(double latitude)
```

**Example:**


```
//Construct a message
TIMMessage msg = new TIMMessage();

//Add location information
TIMLocationElem elem = new TIMLocationElem();
elem.setLatitude(113.93);   //Set the latitude
elem.setLongitude(22.54);   //Set the longitude
elem.setDesc("Tencent Builiding");

//Add elem to the message
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }
    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending file messages

A file message is defined by `TIMFileElem`. You can also view additional information such as the file display name.

>
> - Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects are not guaranteed to be sorted in the order that they are sent. 
>`path` does not support file paths starting with `file://`. The `file://` prefix must be removed.
> - The maximum file size is 28 MB.

**The member methods of `TIMFileElem` are as follows:**

```
/**
 * Download and save a file to the specified path
 * @param path Specified storage path
 * @param callback Callback
 */
public void getToFile(@NonNull final String path, @NonNull TIMCallBack callback)

/**
 * Obtain uuid
 * @return uuid, which can be used as the unique key for caching
 */
public String getUuid()

/**
 * Obtain the file size
 * @return File size
 */
public long getFileSize()

/**
 * Obtain the file display name
 * @return File name
 */
public String getFileName()

/**
 * Set the file display name when sending the file
 * @param fileName File name
 */
public void setFileName(String fileName)

/**
 * Obtain the path of the uploaded file. This method is only valid for the sender.
 * @return File path
 */
public String getPath()

/**
 * Set the path of the file to be uploaded (if the file path is set, the file will be uploaded first)
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
//Construct a message
TIMMessage msg = new TIMMessage();

//Add file content
TIMFileElem elem = new TIMFileElem();
elem.setPath(filePath); //Set the file path
elem.setFileName("myfile.bin"); //Set the file name for displaying the message
 
//Add elem to the message
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending custom messages

A custom message is the message whose format and content are defined by developers when built-in message types cannot meet their special needs. The IM SDK is only responsible for passing through custom messages. If iOS APNs push notifications are required, you need to provide a push text description for display. A custom message is defined by `TIMCustomElem`, where ‘data’ stores the binary data of the message and the data format is defined by the developer, while `desc` stores the description text. A message can contain multiple custom `Elem` objects, which can be mixed with other `Elem` objects. In the case of offline push, the `desc` of each `Elem` are stored in a stack and delivered.

**The member methods of `TIMCustomElem` are as follows:**

```
/**
 * Obtain custom data
 * @return Custom data
 */
public byte[] getData()

/**
 * Set custom data
 * @param data Custom data
 */
public void setData(byte[] data)

/**
 * Obtain custom description
 * @return Custom description
 */
public String getDesc()

/**
 * Set custom description
 * @param desc Custom description
 */
public void setDesc(String desc)

/**
 * Obtain the ext field of the corresponding backend push
 * @return ext
 */
public byte[] getExt()

/**
 * Set the ext field of the corresponding backend push
 * @param ext ext field of the corresponding backend push
 */
public void setExt(byte[] ext)

/**
 * Obtain a custom sound
 * @return Data of the custom sound
 */
public byte[] getSound()

/**
 * Set the data of the custom sound
 * @param data Data of the custom sound
 */
public void setSound(byte[] data)
```

The following example shows how to add an XML-based message, the display of which is determined by the developer. **Example:**

```
//Construct a message
TIMMessage msg = new TIMMessage();
 
// Custom message using the xml protocol
String sampleXml = "<!--?xml version='1.0' encoding="utf-8"?-->testTitlethis is custom msgtest msg body";
 
//Add custom content to TIMMessage
TIMCustomElem elem ＝ new TIMCustomElem();
elem.setData(sampleXml.getBytes());      //Custom byte[]
elem.setDesc("this is one custom message"); //Custom description
 
//Add elem to the message
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}
//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```

### Sending short video messages

A short video message is defined by `TIMVideoElem`, which is a subclass of `TIMElem`. These messages can contain video snapshots and content. In this case, sending a short video is actually adding `TIMVideoElem` to `TIMMessage` and sending it along with the message.

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
 * Set short video information when sending the message
 *
 * @param video Short video information, see {@link TIMVideo} for details
 */
public void setVideo(TIMVideo video) {
    this.video = video;
}

/**
 * Obtain video information
 *
 * @return Video information, see {@link TIMVideo} for details
 */
public TIMVideo getVideoInfo() {
    return this.video;
}

/**
 * Set the video file path when sending the message
 *
 * @param path Video file path
 */
public void setVideoPath(String path) {
    this.videoPath = path;
}

/**
 * Obtain the video file path
 *
 * @return Video file path
 */
public String getVideoPath() {
    return this.videoPath;
}

/**
 * Obtain short video snapshot information when sending the message
 *
 * @param snapshot Short video snapshot information, see {@link TIMSnapshot} for details
 */
public void setSnapshot(TIMSnapshot snapshot) {
    this.snapshot = snapshot;
}

/**
 * Obtain video snapshot information
 *
 * @return Video snapshot information, see {@link TIMSnapshot} for details
 */
public TIMSnapshot getSnapshotInfo() {
    return this.snapshot;
}

/**
 * Set the short video snapshot file path when sending the message
 *
 * @param path Short video snapshot file path
 */
public void setSnapshotPath(String path) {
    this.snapshotPath = path;
}

/**
 * Obtain the short video snapshot file path
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
taskId | Upload task ID, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress instead.
videoPath | Path of the local video to be sent
video | Video information. Sets the type and duration parameters when sending the message.
snapshotPath | Path of the local snapshot of the short video to be sent
snapshot | Snapshot information. Sets the type, width, and height when sending the message.

The following example shows how to send a short video message. **Example:**

```
//Construct a message
TIMMessage msg = new TIMMessage();

//Construct a short video object
TIMVideoElem ele = new TIMVideoElem();

TIMVideo video = new TIMVideo();
video.setDuaration(duration / 1000); //Set the video length
video.setType("mp4"); // Set the video format

TIMSnapshot snapshot = new TIMSnapshot(); 
snapshot.setWidth(width); // Set the video snapshot width
snapshot.setHeight(height); // Set the video snapshot height

ele.setSnapshot(snapshot);
ele.setVideo(video);
ele.setSnapshotPath(imgPath);
ele.setVideoPath(videoPath);

 
//Add elem to the message
if(msg.addElement(elem) != 0) {
    Log.d(tag, "addElement failed");
    return;
}

//Send the message
conversation.sendMessage(msg, new TIMValueCallBack<TIMMessage>() {//Callback for sending a message
    @Override
    public void onError(int code, String desc) {//Failed to send the message
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "send message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(TIMMessage msg) {//Sent the message successfully
        Log.e(tag, "SendMsg ok");
    }
});
```


### Elem order 

Currently, the file and audio `Elems` are not necessarily transferred in the order that they are added. Other `Elems` are transferred in the order that they are added. However, we recommend that you do not heavily rely on the element sequence when processing elements. Instead, you should process elements by type to prevent process crashes when exceptions occur.


### Online messages

In some scenarios, you need to send online messages, which can only be received when the user is online. If not online when the messages are sent, the user will not see them after the next login. Online messages can be used as notifications. Moreover, online messages will not be stored nor included in the unread count. The API for sending online messages is similar to `sendMessage`.

>Versions earlier than 2.5.3 support only one-to-one chat messages. Version 2.5.3 and later support group chat messages (AVChatRoom and BChatRoom groups are currently not supported.)

```
//Send the online message (the server does not save the message)
public void sendOnlineMessage(TIMMessage msg, TIMValueCallBack<TIMMessage> callback)
```

### Forwarding messages

Through the `copyFrom` API in `TIMMessage`, you can easily copy the content of another message and resend it to contacts.

**Prototype:**
```
/**
 * Copy message content to the current message, including elem, priority, online, and offlinePushInfo
 * @param srcMsg Source message
 * @return true Copied successfully
 */
public boolean copyFrom(@NonNull TIMMessage srcMsg)
```


## Receiving Messages

In most cases, users need to be notified of new messages. For this purpose, you only need to register the new message notification callback `TIMMessageListener`. If the user is logged in, the IM SDK throws new messages through `onNewMessages` in the callback. For information on how to register the callback, see [New Message Notifications](https://intl.cloud.tencent.com/document/product/1047/34312).

>Messages thrown through `onNewMessages` are not necessarily unread messages. Instead, they can also be messages that have not been displayed locally, such as when messages are read on another client and pulling recent contacts obtains the last messages of conversations. If not stored locally, these messages are thrown by this method. After the user logs in, the IM SDK pulls C2C offline messages. To avoid missing message notifications, you need to register new message notifications before login.

### Parsing messages

After receiving a message, you can use `getElem` to obtain all `Elem` nodes in `TIMMessage`. **The following is the prototype for traversing `Elems`:**

```
//Obtain message elements
TIMElem getElement(int i)

//Obtain the number of elements
int getElementCount()
```

**Example:**

```
TIMMessage msg = /* Message */

for(int i = 0; i < msg.getElementCount(); ++i) {
	TIMElem elem = msg.getElement(i);

	//Obtain the type of the current element
	TIMElemType elemType = elem.getType();
	Log.d(tag, "elem type: " + elemType.name());
	if (elemType == TIMElemType.Text) {
		//Process text messages
	} else if (elemType == TIMElemType.Image) {
		//Process image messages
	}//...Process more messages
}
```


### Receiving image messages

After receiving a message, the recipient can obtain all `Elem` nodes from `TIMMessage` through `getElem`. Nodes of the `TIMElemType.Image` type are image nodes. Use `getImageList` in `TIMImageElem` to obtain all the specifications of the image. Currently, there are up to three specifications: original image, large image, and thumbnail. Each specification is stored in a `TIMImage` object.

```
/**
 * Can be called when the IM SDK fetches Elem. Obtain the image list from Elem.
 * @return List of images contained in elem
 */
public ArrayList<TIMImage> getImageList()
```

**`TIMImage`:**

Obtain all image specifications through imageList when receiving the message. The obtained data is the `TIMImage` data. After obtaining `TIMImage`, reserve a place by using the image size and download the images of different specifications through `getImage` in order to display the images.

>The downloaded data needs to be cached by the developer. The IM SDK downloads the data from the server again every time it calls `getImage`. We recommend that you use the `uuid` of images as the `key` to store images.

**Image specifications:** every image has three specifications, which are Original (original image), Large (large image), and Thumb (thumbnail).

- **Original image:** the original image sent by the user, whose dimensions and size remain unchanged.
- **Large image:** an image obtained after the original image is proportionally compressed. After the compression, the height or width of the resulting image, whichever is smaller, is equal to 720 pixels.
- **Thumbnail:** an image obtained after the original image is proportionally compressed. After the compression, the height or width of the resulting image, whichever is smaller, is equal to 198 pixels.

>- If the size of the original image is less than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
>- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
>- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When the user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is directly downloaded when the user taps the thumbnail.
>- When an image is displayed on a tablet or PC, due to the high resolution and availability of a Wi-Fi or wired network, we recommend that the large image be displayed directly, and the original image be downloaded when the user taps or clicks the large image.

**Example:**

```
//Traverse the element list of a message
for(int i = 0; i < msg.getElementCount(); ++i) {
    TIMElem elem = msg.getElement(i);
    if (elem.getType() == TIMElemType.Image) {
        //Image element
        TIMImageElem e = (TIMImageElem) elem;
        for(TIMImage image : e.getImageList()) {

            //Obtain the image type, size, width, and height
            Log.d(tag, "image type: " + image.getType() +
                    " image size " + image.getSize() +
                    " image height " + image.getHeight() +
                    " image width " + image.getWidth());

            image.getImage(path, new TIMCallBack() {
                    @Override
                    public void onError(int code, String desc) {//Failed to obtain the image
						//"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
						//For the meaning of the error code, see the error code table.
						Log.d(tag, "getImage failed. code: " + code + " errmsg: " + desc);
                    }

                    @Override
                    public void onSuccess() {//Request succeeded, and the parameter is image data
						//doSomething
						Log.d(tag, "getImage success.");
                    }
                });
        }
    }
}
```

### Receiving audio messages

After receiving a message, the recipient can obtain all `Elem` nodes from `TIMMessage` through `getElem`. Nodes of the `TIMElemType.Sound` type are audio nodes. When the message is received, reserve a place by using the audio length and download audio resources through `getSoundToFile`. The `getSoundToFile` API downloads the data from the server. To cache or store the data, developers can use `uuid` as the `key` to store the audio file externally. The IM SDK does not store resource files.

**Prototype:**

```
/**
 * Download and save an audio file to the specified path
 * @param path Specified storage path
 * @param callback Callback
 */
public void getSoundToFile(@NonNull final String path, @NonNull TIMCallBack callback)
```

**The read state of the audio message:** whether the audio file has been played. Use [message custom fields](https://intl.cloud.tencent.com/document/product/1047/34320) to implement this feature. For example, for `customInt`, a value of 0 means not played and a value of 1 means played. In this case, set `customInt` to 1 after the user clicks to play the audio. The following sets a custom integer and the default value is 0.

**Prototype:**
```
public void setCustomInt(int value)
```


### Receiving file messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`, where `TIMFileElem` represents a file message node.

**The member methods of `TIMFileElem` are as follows:**

```
//Download and save the file to the specified path
void getToFile(String path, TIMCallBack callback)

//Obtain the file name
java.lang.String    getFileName()

//Obtain the file size
long    getFileSize()

//Obtain uuid
java.lang.String    getUuid()

//Set the file name
void    setFileName(java.lang.String fileName)
```

You can choose to display only the file size and display name when the message arrives and download the file from the server through `getToFile` each time. To cache or store the data, developers can use `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.

**Prototype:**

```
/**
 * Download and save a file to the specified path
 * @param path Specified storage path
 * @param callback Callback
 */
public void getToFile(@NonNull final String path, @NonNull TIMCallBack callback)
```

### Receiving short video messages
After receiving a message, the recipient can obtain all Elem nodes from TIMMessage through getElem. Nodes of the TIMVideoElem type are file message nodes, and the video and snapshot are obtained through the TIMVideo and TIMSnapshot objects. After receiving TIMVideoElem, download the video file and snapshot file through the APIs defined in the video and snapshot attributes. To cache or store the data, developers can use UUID as the key to store the files externally. The IM SDK does not store resource files.

**The member methods of `TIMVideo` are as follows:**

```

/**
 * Obtain the video
 *
 * @param path Storage path of the video
 * @param cb Callback
 * @deprecated
 */
getVideo(@NonNull final String path, @NonNull final TIMCallBack cb);

/**
 * Obtain the video
 *
 * @param path Storage path of the video
 * @param progressCb Download progress callback
 * @param cb Callback
 */
void getVideo(@NonNull final String path, final TIMValueCallBack<ProgressInfo> progressCb, @NonNull final TIMCallBack cb)

/**
 * Obtain the video size
 *
 * @return Return the video size
 */
long getSize();

/**
* Obtain the UUID of the video file
*
* @return uuid, which can be used as the unique key for caching
*/
String getUuid();

/**
 * Obtain the video length
 *
 * @return Video length
 */
long getDuaration();

/**
 * Obtain the type of the video file
 *
 * @return Return the video type
 */
String getType(); 
```

**The member methods of `TIMSnapshot` are as follows:**
```
/**
 * Obtain the snapshot
 *
 * @param path Storage path of the snapshot
 * @param progressCb Download progress callback
 * @param cb Callback
 */
void getImage(final String path, final TIMValueCallBack<ProgressInfo> progressCb, final TIMCallBack cb);

/**
 * Obtain the snapshot
 *
 * @param path Storage path of the snapshot
 * @param cb Callback
 * @deprecated
 */
void getImage(final String path, final TIMCallBack cb);

/**
 * Obtain the snapshot width
 *
 * @return Snapshot width
 */
long getWidth();

/**
 * Obtain the snapshot height
 *
 * @return Snapshot height
 */
long getHeight();

/**
 * Obtain the snapshot size
 *
 * @return Return the snapshot size
 */
long getSize();

/**
 * Obtain the type of the snapshot file
 *
 * @return Return the video type
 */
String getType();

/**
 * Obtain the uuid of the snapshot file
 *
 * @return uuid, which can be used as the unique key for caching
 */
String getUuid(); 
```

**Parsing process for short video messages:**
Here, we will use the new message receipt callback as an example. First, you need to determine whether it has TIMVideoElem through the element type. If yes, it is a short video message and you need to run the following code to parse it.

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

Message properties can be obtained through the member methods of `TIMMessage`.

### Checking whether a message is read

You can check whether a message is read through the `isRead` method of `TIMMessage`. Whether a message is read or not depends on the [read reports](https://intl.cloud.tencent.com/document/product/1047/34324#.E5.B7.B2.E8.AF.BB.E4.B8.8A.E6.8A.A5) implemented by the app. The prototype for determining the message read state is as follows:

**Prototype:**
```
public boolean isRead()
```

### Message states

You can obtain the state of the current message through the `status` method of `TIMMessage`, such as sending, sent successfully, failed to send, and deleted. For deleted messages, use the UI to determine the state and hide them.
```
//Sending…
TIMMessageStatus.Sending

//Sent successfully
TIMMessageStatus.SendSucc

//Failed to send
TIMMessageStatus.SendFail

//Deleted
TIMMessageStatus.HasDeleted

//Message is recalled
TIMMessageStatus.HasRevoked
```

### Checking whether a message was sent by yourself

Determine whether a message was sent by yourself through the `isSelf` method of `TIMMessage`. This method is available when displayed on the interface. The following shows the prototype for determining whether a message was sent by yourself.

**Prototype:**
```
public boolean isSelf()
```

### Message sender and the related profile

The sender’s ID can be obtained through the `getSender` method of `TIMMessage`.
**For one-to-one chat messages:** you can obtain the corresponding conversation through the `getConversation` method of `TIMMessage`, as well as the recipient and the recipient’s profile through `getPeer`.
**For group chat messages:** you can obtain the sender’s profile and the profile of the sender’s belonging group through `getSenderProfile` and `getSenderGroupMemberProfile`. To pull custom fields, you need to [set the fields to be pulled](https://intl.cloud.tencent.com/document/product/1047/34328) before logging in to the IM SDK.
 >This field obtains the user profile and writes it to the message body when the message is sent. If there are user profile updates in the future, this field does not change unless new messages are generated.
 >You can only obtain profiles from received group messages.

```
/**
 * Obtain the message sender
 * @return Message sending user
 */
public String getSender()

/**
 * Obtain the sender’s profile
 *
 * Version 4.4.716 returns this information through a callback
 *
 * @param callBack Callback
 */
public void getSenderProfile( TIMValueCallBack < TIMUserProfile > callBack )

/**
 * Obtain the sender’s profile in the group, which is only available from received group messages (may be empty if the sender is yourself)
 *
 * @return Sender’s profile in the group. "null" indicates that no profile is obtained or the message is not a group message. Currently, the fields that can be obtained include user, nameCard, role, and customInfo. To obtain other fields, use TIMGroupManager > getGroupMembers.
 */
public TIMGroupMemberInfo getSenderGroupMemberProfile()
```


### Message time

The message time can be obtained through the `timestamp` method of `TIMMessage`. **This time is the server time, but not the local time**. When you create a message, this time is adjusted based on the server time and will be changed to the accurate server time after the message is successfully sent.

```
//Timestamp generated for the message by the server
public long timestamp()
```

### Deleting messages

Currently, deleting messages on the server is not supported. You can only delete messages in local storage. To delete messages, use the `remove` method of `TIMMessage`. After the messages are deleted, pulling messages through `getMessage` does not return the deleted messages.

```
/**
 * Mark the message as deleted
 * @return Succeeded or failed
 */
public boolean remove()
```

### Message IDs

There are two types of message IDs. One is `msgId`, which is created when the message is generated. As this ID may conflict with messages generated by other users, a time dimension needs to be added. Messages generated within 10 minutes are considered distinguishable by `msgId`. The other identifier is `uniqueId`, which is generated after the message is sent successfully. IDs generated with this method are globally unique. These two methods need to be determined in the same conversation.

```
//Obtain the message ID
public String getMsgId()

//Obtain the uniqueId of the message
public long getMsgUniqueId()
```

### Message custom fields

Developers can add custom fields to messages, such as custom integer and custom binary data. You can customize different effects based on these two fields. For example, you can determine whether an audio message has been played. Note that these custom fields are only stored locally and not synchronized to the server. You will not obtain them after switching to another client.

```
//Set the custom integer, which defaults to 0.
public void setCustomInt(int value)

//Obtain the custom integer value
public int getCustomInt()

//Set custom data content, which defaults to ""
public void setCustomStr(String str)

//Obtain the value of the custom data content
public String getCustomStr()
```

### Message priorities

Live streaming scenarios involve the like and red packet features. Like messages have a lower priority than red packet messages. Use `TIMCustomElem` to define the message content and define the message priority through a different API when sending the message.
>Valid for group messages only

```
//Set the message priority
public void setPriority(TIMMessagePriority priority)

//Obtain the message priority
public TIMMessagePriority getPriority()
```


### Read receipts

The IM SDK provides the read receipt feature for **C2C messages**, which can be enabled through `enableReadReceipt` in `TIMUserConfig`. After the feature is enabled, read receipts will be sent to the recipient when reporting [message read reports](https://intl.cloud.tencent.com/document/product/1047/34324#.E5.B7.B2.E8.AF.BB.E4.B8.8A.E6.8A.A5).

You can register the read receipt listener through `setMessageReceiptListener` in `TIMUserConfig`, and query whether the current message has been read by the recipient through `isPeerReaded` in `TIMMessage`.

**Prototype:**

```
/**
 * After the read receipt feature is enabled, read receipts will be sent to the recipient when reporting message read reports. This feature is only valid for one-to-one conversations.
 */
public void enableReadReceipt()

/**
 * Set the read receipt listener
 * @param receiptListener Read receipt listener
 */
public void setMessageReceiptListener(TIMMessageReceiptListener receiptListener)

/**
 * Whether the recipient has read the message (valid for C2C messages only)
 * @return true: read by the recipient. false: not read by the recipient.
 */
public boolean isPeerReaded()
```

### Message sequence numbers

Obtain the sequence number of the current message through `getSeq` of `TIMMessage`.

```
/**
 * Obtain the sequence number of the current message
 * @return Sequence number of the current message
 */
public long getSeq()
```

### Message random numbers

The random number of the current message can be obtained through `getRand` in `TIMMessage`.

```
/**
 * Obtain the random number of the current message
 * @return Random number of the current message
 */
public long getRand()
```

### Message query parameter

In the IM SDK, a specific message is identified by a `{seq, rand, timestamp, isSelf}` quad, which is called the query parameter of messages. The query parameter of the current message can be obtained from the current message through `getMessageLocator` in `TIMMessage`.

```
/**
 * Obtain the query parameter of the current message
 * @return Query parameter of the current message
 */
public TIMMessageLocator getMessageLocator()
```

## Conversation Operations

### Obtaining all conversations

Obtain the number of current conversations through `getConversationList` of `TIMManager` to obtain all local conversations.

**Prototype:**

```
/**
 * Obtain all conversations
 * @return List of conversations
 */
public List<TIMConversation> getConversationList()
```

**Example:**

```
List<TIMConversation> list = TIMManager.getInstance().getConversationList();
```

### Roamed recent contacts

By default, the IM SDK obtains roamed recent contacts and the last message for each conversation after the user logs in.

### Obtaining local messages in a conversation

The IM SDK stores messages locally. These messages can be obtained through `getLocalMessage` of `TIMConversation`. This is an asynchronous method, which requires a callback to obtain message data. **For one-to-one chats, offline messages will be obtained automatically after login. For group chats, only the last message is obtained after you log in with roamed recent contacts enabled, and roaming messages can be obtained through `getMessage`**.

 > Note:
 > For resource messages such as image and audio messages, the message body only contains descriptive information, and additional APIs are required to download data. For more information, see the section about parsing messages. After data is downloaded, the data is not cached. Instead, the caller must cache the data.


**Prototype:**

```
/**
 * Obtain only the local chat history
 * @param count Number of messages starting from the last message and going backward
 * @param lastMsg Last obtained message. If null, it is a new message.
 * @param callback Callback that returns the list of obtained messages
 */
public void getLocalMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack<List<TIMMessage>> callback)
```

**Example:**

```
//Obtain a conversation extension instance
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.Group, groupId);

//Obtain all the messages of this conversation
con.getLocalMessage(10, //Obtain the last 10 messages in this conversation
        null, //The message starting from which to obtain messages is not specified. In this case, the operation starts from the last message.
        new TIMValueCallBack<List<TIMMessage>>() {//Callback API
    @Override
    public void onError(int code, String desc) {//Failed to obtain the messages
        //The API returns "code" (error code) and "desc" (error description), which can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "get message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(List<TIMMessage> msgs) {//Obtained messages successfully
        //Traverse the obtained messages
        for(TIMMessage msg : msgs) {
            lastMsg = msg;
            //The message timestamp can be obtained through timestamp(). isSelf() indicates whether the message was sent by yourself.
            Log.e(tag, "get msg: " + msg.timestamp() + " self: " + msg.isSelf() + " seq: " + msg.msg.seq());

        }
    }
});
```

### Obtaining conversation roaming messages

For group chats, the user obtains roaming messages after login. For C2C chats, the user can obtain roaming messages after the roaming service is enabled. Roaming messages are obtained through `getMessage` of `TIMConversation`. If local messages are continuous, they are obtained directly. Otherwise, missing messages need to be obtained over the network.

 >For resource messages such as image and audio messages, the message body only contains descriptive information. Therefore, additional APIs are required to download data. For more information, see the section about parsing messages. After data is downloaded, the data is not cached. Instead, the caller must cache the data.

**Prototype:**

```
/**
 * Obtain the chat history
 * @param count Number of messages starting from the last message and going backward
 * @param lastMsg Last obtained message
 * @param callback Callback that returns the list of obtained messages
 */
public void getMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack< List<TIMMessage> > callback)
```

**Example:**

```
//Obtain a conversation extension instance
TIMConversation con = TIMManager.getInstance().getConversation(TIMConversationType.Group, groupId);

//Obtain all the messages of this conversation
con.getMessage(10, //Obtain the last 10 message in this conversation
        null, //The message starting from which to obtain messages is not specified. In this case, the operation starts from the last message.
        new TIMValueCallBack<List<TIMMessage>>() {//Callback API
    @Override
    public void onError(int code, String desc) {//Failed to obtain the messages
        //The API returns "code" (error code) and "desc" (error description), which can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.d(tag, "get message failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(List<TIMMessage> msgs) {//Obtained messages successfully
        //Traverse obtained messages
        for(TIMMessage msg : msgs) {
            lastMsg = msg;
            //The message timestamp can be obtained through timestamp(). isSelf() indicates whether the message was sent by yourself.
            Log.e(tag, "get msg: " + msg.timestamp() + " self: " + msg.isSelf() + " seq: " + msg.msg.seq());

        }
    }
});
```


### Deleting conversations

`TIMManager` in the IM SDK provides two methods to delete a conversation, each of which applies to different scenarios. One of both methods is to delete the conversation and save all messages, and the other is to delete the conversation together with all its messages.

>
> - For C2C conversations, after local messages are deleted, you cannot obtain the message history before the conversation is deleted.
> - For group conversations, after local messages are deleted, `getMessage` still pulls roaming messages. Therefore, it is possible that messages are deleted successfully, but the message history before the conversation is deleted can still be pulled. If you do not need to pull roaming messages, you can use `getLocalMessage` to obtain messages, or use `getMessage` to pull a specified number of messages, such as a certain number of unread messages.

**Prototype:**

```
/**
 * Delete conversation cache
 * @param type Conversation type
 * @param peer Peer in the conversation. For a C2C conversation, use the peer’s identifier. For a group conversation, use the group ID.
 * @return true: succeeded. false: failed.
 */
public boolean deleteConversation(TIMConversationType type, String peer)


/**
 * Delete conversation cache and local messages related to this conversation
 * @param type Conversation type
 * @param peer Peer in the conversation. For a C2C conversation, use the peer’s identifier. For a group conversation, use the group ID.
 * @return true: succeeded. false: failed.
 */
public boolean deleteConversationAndLocalMsgs(TIMConversationType type, String peer)
```

The following example shows how to delete the C2C conversation with the user named hello. **Example:**

```
TIMManager.getInstance().deleteConversation(TIMConversationType.C2C, "hello");
```

### Synchronously obtaining the last message of a conversation

The UI displays the last messages from the user on the recent contact list. The IM SDK provides a `getLastMsg` API to synchronize the latest messages from conversations, allowing users to obtain and display the last messages. **This feature requires a network connection. If recent contacts are disabled, the latest messages cannot be obtained after login and before new messages arrive**. Obtaining messages through this API does not filter messages in the deleted state, which need to be blocked at the app level. To obtain multiple recent messages, call `getMessage`.
 
**Prototype:**

```
/**
 * Obtain the last message from cache
 * @return Last message. "nul" is returned if the conversation is invalid.
 */
public TIMMessage getLastMsg()

/**
 * Obtain the chat history
 * @param count Number of messages starting from the last message and going backward
 * @param lastMsg Last obtained message
 * @param callback Callback that returns the list of obtained messages
 */
public void getMessage(int count, TIMMessage lastMsg, @NonNull TIMValueCallBack< List<TIMMessage> > callback)
```


### Setting conversation drafts

The IM SDK provides the conversation draft feature. Developers can perform draft-related operations through APIs in `TIMConversation`.

>
> - Drafts are only valid locally, which means you cannot see your drafts after switching devices or clearing the data.
> - Draft information is stored in a local database and can be obtained after users log in again.
 
**Prototype:**

```
/**
 * Set a draft
 * @param draft Draft content. If null, the draft is canceled.
 */
public void setDraft(TIMMessageDraft draft)

/**
 * Obtain the draft
 * @return Return draft content
 */
public TIMMessageDraft getDraft()

/**
 * Check whether a draft is created for this conversation
 * @return true: yes. false: no.
 */
public boolean hasDraft()
```

**The following describes `TIMMessageDraft`:**

```
/**
 * Obtain the list of message elements in a draft
 * @return List of message elements
 */
public List<TIMElem> getElems()

/**
 * Set message elements in a draft
 * @param elem Message elements to be added to the draft
 */
public void addElem(TIMElem elem)

/**
 * Obtain user-defined data in a draft
 * @return User-defined data
 */
public byte[] getUserDefinedData()

/**
 * Set user-defined data in a draft
 * @param userDefinedData User-defined data
 */
public void setUserDefinedData(byte[] userDefinedData)

/**
 * Obtain the edit time of a draft
 * @return Edit time of the draft
 */
public long getTimestamp()
```
### Deleting the local messages of a conversation

The IM SDK allows you to clear the local chat history while retaining the conversation. To do this, call `deleteLocalMessage` of `TIMConversation`.

>For group conversations, the deleted local message history can still be pulled through roaming.


**Prototype:**
```
/**
 * Batch delete all the historical messages of this conversation
 * @param callback Callback
 */
public void deleteLocalMessage(@NonNull TIMCallBack callback)
```

### Searching for local messages

The IM SDK allows you to search for messages based on given parameters. Currently, only exact search is available, but fuzzy search is not supported. Developers can call the `findMessages` method in `TIMConversation` to search for messages.


```
/**
 * Search messages based on given parameters
 * @param locators Message search parameters
 * @param cb Callback, which returns hit messages
 */
public void findMessages(@NonNull List<TIMMessageLocator> locators, TIMValueCallBack<List<TIMMessage>> cb)
```

`TIMMessageLocator` can be obtained through the `getMessageLocator` method in `TIMMessage`.

**Prototype:**

```
/**
 * Obtain the locator of the current message
 * @return Locator of the current message
 */
public TIMMessageLocator getMessageLocator()
```

### Recalling messages

Starting with version 3.1.0, the IM SDK provides an API to recall messages. You can recall sent messages by calling the `revokeMessage` API of `TIMConversation`.

>
> - The API works for C2C and group conversations, but not onlineMessage, AVChatRoom, and BChatRoom.
> - By default, messages that were sent within the last 2 minutes can be recalled.

**Prototype:**

```
/**
 > - Message recalling works for C2C and group conversations, but not onlineMessage, AVChatRoom, and BChatRoom.
 * @param msg Message to be recalled
 * @param cb Callback
 * @since 3.1.0
 */
public void revokeMessage(@NonNull TIMMessage msg, @NonNull TIMCallBack cb)
```

After a message is recalled, other members in the group or the peer in the C2C conversation receives a message recall notification. In addition, the message recall notification listener `TIMMessageRevokeListener` notifies the upper-layer app of this. You can configure the message recall notification listener before login through `setMessageRevokedListener` of `TIMUserConfig`. For more information, see [User Configuration](https://intl.cloud.tencent.com/document/product/1047/34312#.E7.94.A8.E6.88.B7.E9.85.8D.E7.BD.AE).

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

After receiving a message recall notification, you can use the `checkEquals` method in `TIMMessage` to check whether the current message has been recalled by the sender and then refresh the UI when necessary.

**Prototype:**

```
/**
 * Compare the current message with the given locator to check whether they refer to the same message
 * @param locator Message locator
 * @return true: yes. false: no.
 * @since 3.1.0
 */
public boolean checkEquals(@NonNull TIMMessageLocator locator)

```

## System Messages

In addition to C2C chat and group chat messages, system message is another conversation type (TIMConversationType). System messages are notification messages sent by the system backend for various events and cannot be sent by users. Currently, there are two types of system messages: relationship chain system messages and group system messages.

- Relationship chain change system messages: when the user has a friend request or is deleted by a contact, the system sends a change notification, and the developer can refresh the friend list. For more information, see [Relationship Chain Change System Notifications](https://intl.cloud.tencent.com/document/product/1047/34332#.E5.85.B3.E7.B3.BB.E9.93.BE.E5.8F.98.E6.9B.B4.E7.B3.BB.E7.BB.9F.E9.80.9A.E7.9F.A5).
- When the group profile is modified, such as a change to the group name or group members, the system sends a group event message in the group. The developer can choose whether to display the message or not and can refresh the group profile or group members at the same time. For more information, see [Group Event Messages](https://intl.cloud.tencent.com/document/product/1047/34328#.E7.BE.A4.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF).
- When the group owner is removed or non-members are invited to the group, the system sends a group system message to users. For more information, see [Group System Messages](https://intl.cloud.tencent.com/document/product/1047/34328#.E7.BE.A4.E7.B3.BB.E7.BB.9F.E6.B6.88.E6.81.AF).


## Setting Background Message Notification Bar Reminders

When the IM SDK is running in the background, it can continue to receive message notifications when online. If the program is running in the background, you can present new messages to the user in the form of a system notification bar reminder. New messages can be displayed in the notification bar on the top, in the notification center, or on the lock screen. See the following example for the implementation method:

**Example:**

```
NotificationManager mNotificationManager = (NotificationManager) context.getSystemService(context.NOTIFICATION_SERVICE);
NotificationCompat.Builder mBuilder = new NotificationCompat.Builder(context);
Intent notificationIntent = new Intent(context, MainActivity.class);
notificationIntent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP| Intent.FLAG_ACTIVITY_SINGLE_TOP);
PendingIntent intent = PendingIntent.getActivity(context, 0, notificationIntent, 0);
mBuilder.setContentTitle(senderStr)//Set the notification bar title
            .setContentText(contentStr)
            .setContentIntent(intent) //Set the notification bar click intent
            .setNumber(++pushNum) //Set the number of notifications in a collection
            .setTicker(senderStr+":"+contentStr) //Notification appears in the notification bar for the first time with a rising animation effect
            .setWhen(System.currentTimeMillis())//Generation time of the notification, which is displayed in the notification information. It is normally the time obtained by the system.                  
            .setDefaults(Notification.DEFAULT_ALL)//The simplest and most consistent way to add sounds, flashing, and vibration to notifications is to use current default settings. To do this, use the defaults property, which can be used in combination.                        
            .setSmallIcon(R.drawable.ic_launcher);//Set the small icon for notifications
Notification notify = mBuilder.build();
notify.flags |= Notification.FLAG_AUTO_CANCEL;
mNotificationManager.notify(pushId, notify);
```
