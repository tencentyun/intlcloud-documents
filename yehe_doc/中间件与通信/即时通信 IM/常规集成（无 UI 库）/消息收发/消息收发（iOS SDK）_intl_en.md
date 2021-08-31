## Sending Messages

### Sending common messages

#### Obtaining a conversation

A conversation refers to a conversation with a user or a group. To send or receive messages in a one-to-one or group conversation, you need to first obtain the conversation by specifying the conversation type (one-to-one chat or group chat) and the peer’s identifier (the peer’s account or group ID). Use `getConversation` to obtain a conversation.
>If the conversation is not stored locally, calls to TIMConversation APIs will fail. We recommend that you operate the TIMConversation object after receiving the TIMUserConfig > TIMRefreshListener callback.

**Prototype:**

```
@interface TIMManager : NSObject
/**
 *  Obtain a conversation
 *
 *  @param type Type of the conversation. TIM_C2C indicates the one-to-one chat, and TIM_GROUP indicates the group chat.
 *  @param conversationId For a C2C conversation, use the peer’s identifier. For a GROUP conversation, use the group ID.
 *
 *  @return A conversation object
 */
- (TIMConversation*)getConversation:(TIMConversationType)type receiver:(NSString*)conversationId;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | Conversation type. For a one-to-one chat, enter TIM_C2C. For a group chat, enter TIM_GROUP.
conversationId | Conversation identifier. For a one-to-one chat, the receiver is the peer’s identifier. For a group chat, the receiver is the group ID.

**Obtain the one-to-one conversation in which the peer’s `identifier` is "iOS-001":**

```
TIMConversation * c2c_conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS-001"];
```

**Obtain the group conversation with the group whose ID is "TGID1JYSZEAEQ":** 

```
TIMConversation * grp_conversation = [[TIMManager sharedInstance] getConversation:TIM_GROUP receiver:@"TGID1JYSZEAEQ"];
```

#### Sending messages

After getting a `TIMConversation` instance through `TIMManager`, you can send messages and get cached messages for the conversation. See [IM SDK Basic Concepts](https://intl.cloud.tencent.com/document/product/1047/34302) for an explanation of Message in the IM SDK. In the IM SDK, a message is a `TIMMessage` object. A `TIMMessage` can contain multiple `TIMElem` units, which can be text or images. This means a message can contain multiple text segments and images. Use the `sendMessage` method of `TIMConversation` to send messages through blocks or the `protocol` callback.

![](https://main.qcloudimg.com/raw/6bf979993ac8490ce53f68256e05ef01.png)


**Prototype:**

```
@interface TIMConversation : NSObject
-(int) sendMessage: (TIMMessage*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
--- | ---
msg | Message
succ | Success callback
fail | Failure callback

### Sending text messages

A text message is defined by `TIMTextElem`.

```
@interface TIMTextElem : TIMElem {
    NSString * text;
}
```

**Example:**


>
>- "text" passes the text message to be sent.
>- In the failure callback, "code" indicates the error code (see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348) for more information), and "err" indicates the error description.

```
TIMTextElem * text_elem = [[TIMTextElem alloc] init];

[text_elem setText:@"this is a text message"];

TIMMessage * msg = [[TIMMessage alloc] init];
[msg addElem:text_elem];

[conversation sendMessage:msg succ:^(){
	NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending image messages

An image message is defined by `TIMImageElem`, which is a subclass of `TIMElem`. Image messages can contain image content. In this case, sending an image is actually adding `TIMImageElem` to `TIMMessage` and sending it along with the message. When sending an image, you only need to set `path`, that is, the image path. You can obtain all image types through `imageList` after the message is sent successfully. In addition, use TIMUploadProgressListener` to monitor the current upload progress.

**`TIMImageElem` prototype:**

```
/**
 *  Store the path of the image to be sent, which must be a local path. See the following example.
 */
@interface TIMImageElem : TIMElem
/**
 *  Path of the image to be sent
 */
@property(nonatomic,retain) NSString * path;
/**
 *  This parameter saves all specifications of the image when it is received. You do not need to consider it when sending the message.
 */
@property(nonatomic,retain) NSArray * imageList;
/**
 * ID of the upload task, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress instead.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;

/**
 *  Image compression level. For more information, see TIM_IMAGE_COMPRESS_TYPE (only valid for the jpg format).
 */
@property(nonatomic,assign) TIM_IMAGE_COMPRESS_TYPE level;

/**
 *  Image format. For more information, see TIM_IMAGE_FORMAT.
 */
@property(nonatomic,assign) TIM_IMAGE_FORMAT format;
@end
```

**Parameter description:**

| Parameter | Description |
|---|---|
| path | Path of the image to be sent, which must be a local path. For reference, see the example of sending an image. |
| imageList | Saves all specifications of the image when it is received. You do not need to consider it when sending the message. For reference, see the section about receiving image messages. |
| taskId | This can be used to query the upload progress during image sending. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress instead. |
| level | Images need to be compressed before being sent, and "level" represents the compression level. For more information, see the definition of TIM_IMAGE_COMPRESS_TYPE. |
| format | Image format. For more information, see TIM_IMAGE_FORMAT. |

The following example shows how to send an image with the absolute path of `/xxx/imgPath.jpg`. **Example:**

```
/**
*  Obtain the one-to-one conversation with the same user iOS-001
*/
TIMConversation * c2c_conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS-001"];
/**
*  Construct a message
*/
TIMMessage * msg = [[TIMMessage alloc] init];
/**
*  Construct image content
*/
TIMImageElem * image_elem = [[TIMImageElem alloc] init];
image_elem.path = @"/xxx/imgPath.jpg";
/**
*  Add image content to the message container
*/
[msg addElem:image_elem];
/**
*  Send the message
*/
[conversation sendMessage:msg succ:^(){  //Sent the message successfully
       NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {  //Failed to send the message
       NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending emoji messages

An emoji message is defined by `TIMFaceElem`. The IM SDK does not provide emoji packages. Developers can use `index` to store the index entries of the emojis in their emoji packages. Alternatively, users can directly use `data` to store emoji binary data and the string `key`. In either way, users can customize emojis, and the SDK is only responsible for passing them through.

```
@interface TIMFaceElem : TIMElem
/**
 *  Emoji index, which can be customized by the user
 */
@property(nonatomic, assign) int index;
/**
 *  Additional data, which can be customized by the user
 */
@property(nonatomic,retain) NSData * data;
@end
```

**Parameter description:**

>You only need to pass in "index" or "data", and the IM SDK is responsible for passing the data through.

Parameter | Description
---|---
index | Emoji index, which is customized by the developer
data | Emoji binary data, which is customized by the developer

The following example shows how to send an emoji with the index of 10. The developer must have emoji packages at both sides, and the index specifies the emoji with index 10. The emoji can also be identified by binary data through "data". **Example:**

```
TIMFaceElem * face_elem = [[TIMFaceElem alloc] init];

[face_elem setIndex:10];

TIMMessage * msg = [[TIMMessage alloc] init];
[msg addElem:face_elem];

[conversation sendMessage:msg succ:^(){
	NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending audio messages

An audio message is defined by `TIMSoundElem`, where `data` stores audio data. To use this object, you need to provide the audio length in seconds.

>
>- A message can contain only one audio `Elem`. If multiple audio `Elem` objects are added, the `AddElem` function returns error 1 and the audio elements will not be added.
>- Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects are not guaranteed to be sorted in the order that they are sent. 

```
/**
 *  Audio message Elem
 */
@interface TIMSoundElem : TIMElem
/**
 *  ID of the upload task, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress instead.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 *  Path of the audio file to be uploaded. Use getSound to obtain the data when receiving the message.
 */
@property(nonatomic,strong) NSString * path;
/**
 *  Store audio data
 */
@property(nonatomic,retain) NSData * data;
/**
 *  Internal ID of the audio message
 */
@property(nonatomic,strong) NSString * uuid;
/**
 *  Audio data size
 */
@property(nonatomic,assign) int dataSize;
/**
 *  Audio length in seconds, which should be set when sending the message
 */
@property(nonatomic,assign) int second;

/**
 *  Obtain the download URL of the audio file
 *
 *  @param urlCallBack Get the URL callback
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save audio data to the specified file
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 *
 *  @param path Storage path of the audio file
 * @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Save audio data to the specified file (with the progress callback)
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 *
 *  @param path Storage path of the audio file
 *  @param progress Audio download progress
 * @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

| Parameter | Description |
|---|---|
| path | Path of the audio file to be uploaded |
| uuid | Unique identifier generated after the audio file is uploaded. Users can save the file based on this identifier, and the IM SDK does not save resource data internally. |
| dataSize | Audio data size |
| second | Audio length |

**Example:**

```
TIMSoundElem * sound_elem = [[TIMSoundElem alloc] init];
[sound_elem setPath:@"./xxx.mp3"];
[sound_elem setSecond:10];
TIMMessage * msg = [[TIMMessage alloc] init];
[msg addElem:sound_elem];
[conversation sendMessage:msg succ:^(){
	NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending location messages

A location message is defined by `TIMLocationElem`, where `desc` stores the description information of the location, and `longitude` and `latitude` represent the longitude and latitude of the location respectively.

```
@interface TIMLocationElem : TIMElem
/**
 *  Description of the location, which should be set when sending the message
 */
@property(nonatomic,retain) NSString * desc;
/**
 *  Latitude, which should be set when sending the message
 */
@property(nonatomic,assign) double latitude;
/**
 *  Longitude, which should be set when sending the message
 */
@property(nonatomic,assign) double longitude;
@end
```

**Example:**

```
NSString *desc= @"Tencent Building";
TIMLocationElem * location_elem = [[TIMLocationElem alloc] init];
[location_elem setDesc:desc];
[location_elem setLatitude:113.93];
[location_elem setLongitude:22.54];
TIMMessage * msg = [[TIMMessage alloc] init];
[msg addElem:location_elem];
[conversation sendMessage:msg succ:^(){
	NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending file messages

A file message is defined by `TIMFileElem`. You can also view additional information such as the file display name.

> Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one.

```
/**
 *  File message Elem
 */
@interface TIMFileElem : TIMElem
/**
 *  ID of the upload task, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress instead.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 *  Path of the file to be uploaded (if the path is set, the file will be uploaded first)
 */
@property(nonatomic,strong) NSString * path;
/**
 *  Internal ID of the file
 */
@property(nonatomic,strong) NSString * uuid;
/**
 *  File size
 */
@property(nonatomic,assign) int fileSize;
/**
 *  Display name of the file, which should be set when sending the message
 */
@property(nonatomic,strong) NSString * filename;

/**
 *  Obtain the download URL of the file
 *
 *  @param urlCallBack Obtain the URL callback 
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save file data to the specified file
 *
 *  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
 *
 * @param path Storage path of the file
 * @param succ Success callback, which returns data
 * @param fail Failure callback, which returns the error code and error description
 */
- (void)getFile:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Save file data to the specified file (with the progress callback)
 *
 *  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
 *
 * @param path Storage path of the file
 * @param progress File download progress
 * @param succ Success callback, which returns data
 * @param fail Failure callback, which returns the error code and error description
 */
- (void)getFile:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | File path
data | Binary data of the file to be sent. You only need to set "path" or "data". We recommend that you us "path".
filename | File name. The IM SDK does not verify that the file name is correct, but only passes it through.

**Example:**

```
TIMFileElem * file_elem = [[TIMFileElem alloc] init];
[file_elem setPath:./xxx/a.txt];
[file_elem setFilename:@"a.txt"];
TIMMessage * msg = [[TIMMessage alloc] init];
[msg addElem:file_elem];
[conversation sendMessage:msg succ:^(){
	NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending custom messages

A custom message is a message whose format and content are defined by developers when built-in message types cannot meet their special needs. The IM SDK is only responsible for passing custom messages through. If iOS APNs push notifications are required, you need to provide a push text description for display. A custom message is defined by `TIMCustomElem`, where `data` stores the binary data of the message and the data format is defined by the developer. A message can contain multiple custom `Elem` objects, which can be mixed with other `Elem` objects. In the case of offline `Push`, the `desc` of each `Elem` are put in a stack and delivered.

```
/**
 *  Custom message type
 */
@interface TIMCustomElem : TIMElem
/**
 *  Binary data of the custom message
 */
@property(nonatomic,strong) NSData * data;
/**
 *  Custom message description, which is used for display in offline push. This parameter has been deprecated, and you can use offlinePushInfo in TIMMessage to configure this information.
 */
@property(nonatomic,strong) NSString * desc DEPRECATED_ATTRIBUTE;
/**
 *  Extension field information in offline push. This parameter has been deprecated, and you can use offlinePushInfo in TIMMessage to configure this information.
 */
@property(nonatomic,strong) NSString * ext DEPRECATED_ATTRIBUTE;
/**
 *  Sound field information in offline push. This parameter has been deprecated, and you can use offlinePushInfo in TIMMessage to configure this information.
 */
@property(nonatomic,strong) NSString * sound DEPRECATED_ATTRIBUTE;
@end
```

**Parameter description:**

Parameter | Description
---|---
data | Binary data of the custom message

The following example shows how to add an XML-based message, the display of which is determined by the developer. **Example:**

```
// Custom message using the XML protocol
NSString * xml = @"testTitlethis is custom msgtest msg body";
// Convert to NSData
NSData *data = [xml dataUsingEncoding:NSUTF8StringEncoding];
TIMCustomElem * custom_elem = [[TIMCustomElem alloc] init];
[custom_elem setData:data];
TIMMessage * msg = [[TIMMessage alloc] init];
[msg addElem:custom_elem];
[conversation sendMessage:msg succ:^(){
	NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending short video messages

A short video message is defined by `TIMVideoElem`, which is a subclass of `TIMElem`. Short video messages can contain video snapshots and content. In this case, sending a short video is actually adding `TIMVideoElem` to `TIMMessage` and sending it along with the message.

**`TIMVideoElem` prototype:**

```
/**
 *  Short video message
 */
@interface TIMVideoElem : TIMElem
/**
 *  ID of the upload task, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;

/**
 *  Video file path, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * videoPath;

/**
 *  Video information, which is set when the message is sent
 */
@property(nonatomic,strong) TIMVideo * video;

/**
 *  Snapshot file path, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * snapshotPath;

/**
 *  Video snapshot, which is set when the message is sent
 */
@property(nonatomic,strong) TIMSnapshot * snapshot;
@end
```

**Parameter description:**

Parameter | Description
---|---
taskId | ID of the upload task, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress.
videoPath | Path of the local video to be sent
video | Video information. Sets the "type" and "duration" parameters when sending the message.
snapshotPath | Path of the local snapshot of the short video to be sent
snapshot | Snapshot information. Sets the "type", "width", and "height" parameters when sending the message.

The following example shows how to send a short video message. **Example:**

```
/**
*  Obtain the one-to-one conversation with the same user iOS-001
*/
TIMConversation * c2c_conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS-001"];
/**
*  Construct a message
*/
TIMMessage * msg = [[TIMMessage alloc] init];
/**
*  Construct video content
*/
TIMVideoElem * videoElem = [[TIMVideoElem alloc] init];
videoElem.videoPath = @"/xxx/videoPath.mp4";
videoElem.video = [[TIMVideo alloc] init];
videoElem.video.type = @"mp4";
videoElem.video.duration = 10;
videoElem.snapshotPath = @"/xxx/snapshotPath.jgp";
videoElem.snapshot = [[TIMSnapshot alloc] init];
videoElem.snapshot.type = @"jpg";
videoElem.snapshot.width = 100;
videoElem.snapshot.height = 200;
/**
*  Add short video content to the message container
*/
[msg addElem:videoElem];
/**
*  Send the message
*/
[conversation sendMessage:msg succ:^(){  //Sent the message successfully
       NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {  //Failed to send the message
       NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Elem order

Currently, the file and sound elements are not necessarily transferred in the order that they are added. Other elements are transferred in the order that they are added. However, we recommend that you do not heavily rely on the element sequence when processing elements. Instead, you should process elements by type to prevent process crashes when exceptions occur.

### Online messages

In some scenarios, you need to send online messages, which can only be received when the user is online. If not online when the messages are sent, the user will not see them after the next login. Online messages can be used as notifications. Online messages will not be stored nor included in the unread count. The API for sending online messages is similar to `sendMessage`.

>
>- Versions earlier than 2.5.3 only support one-to-one chat messages.
>- Version 2.5.3 and later support group messages (the AVChatRoom and BChatRoom types are currently not supported.)

```
@interface TIMConversation : NSObject
/**
 *  Send the online message (the server does not save the message)
 *
 *  @param msg Message body
 * @param succ Success callback
 @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
-(int) sendOnlineMessage: (TIMMessage*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

### Forwarding messages

In version 2.4.0 and later, you can use `copyFrom` in `TIMMessage` to copy the content of another message to the current message and resend it to contacts.

**Prototype:**

```
/**
 *  Message
 */
@interface TIMMessage : NSObject
/**
 *  Copy properties in the message, including ELem, priority, online, and offlinePushInfo
 *
 *  @param srcMsg Source message
 *
 *  @return 0 Succeeded
 */
- (int)copyFrom:(TIMMessage*)srcMsg;
@end
```

## Receiving Messages

In most cases, users need to be notified of new messages. For this purpose, you only need to register the new message notification callback `TIMMessageListener`. If the user is logged in, the IM SDK throws new messages through this method. Note that messages thrown through `onNewMessages` are not necessarily unread messages. Instead, they can also be messages that have not been displayed locally, such as when messages are read on another client and pulling recent contacts obtains the last messages of conversations. If not stored locally, these messages are thrown by this method. After the user logs in, the IM SDK pulls C2C offline messages. To avoid missing message notifications, you need to register new message notifications before login. The content of messages that are called back is passed through the parameter `TIMMessage`. With `TIMMessage`, you can obtain detailed information about messages and conversations, such as message text, audio data, and images. For more information, see [Parsing Messages](#parsing-messages).

**Prototype:**

```
@protocol TIMMessageListener
@optional
/**
 *  New message notification
 *
 *  @param msgs List of new messages, which is an array of TIMMessage types
 */
- (void)onNewMessage:(NSArray*) msgs;
@end

@interface TIMManager : NSObject
- (int)addMessageListener:(id<TIMMessageListener>)listener;
@end
```

**Parameter description:**

Parameter | Description
---|---
msgs | List of new messages. Note that multiple messages may be thrown out. Messages in the same conversation are sorted from old to new.

The following example shows how to set a message callback notification and print new messages when they arrive. **Example:**

```
@interface TIMMessageListenerImpl : NSObject
- (void)onNewMessage:(TIMMessage*) msg;
@end
@implementation TIMMessageListenerImpl
@synthesize onMessage;
- (void)onNewMessage:(NSArray*) msgs {
    NSLog(@"NewMessages: %@", msgs);
}
@end
TIMMessageListenerImpl * impl = [[TIMMessageListenerImpl alloc] init];
[[TIMManager sharedInstance] addMessageListener:impl];
```

### Parsing messages

After receiving messages, you can obtain all `Elem` nodes from `TIMMessage` through `getElem`.

**Prototype of traversing `Elems`:**

```
@interface TIMMessage : NSObject
-(int) elemCount;
-(TIMElem*) getElem:(int)index;
@end
```

**Example:**

```
TIMMessage * message = /* Message */
int cnt = [message elemCount];
for (int i = 0; i < cnt; i++) {
 TIMElem * elem = [message getElem:i];
 if ([elem isKindOfClass:[TIMTextElem class]]) {
     TIMTextElem * text_elem = (TIMTextElem * )elem;
 }
 else if ([elem isKindOfClass:[TIMImageElem class]]) {
     TIMImageElem * image_elem = (TIMImageElem * )elem;
 }
}
```

### Receiving image messages

After receiving messages, the recipient can obtain all `Elem` nodes from `TIMMessage` through `getElem`. Nodes of the `TIMImageElem` type are message nodes. The specifications of the image can be obtained through `imageList` for display purposes.

** `TIMImageElem` prototype:**

```
**
 *  Image message Elem
 */
@interface TIMImageElem : TIMElem
/**
 *  Path of the image to be sent
 */
@property(nonatomic,retain) NSString * path;
/**
 *  Save all the specifications of the image. Currently, up to three types of specifications can be saved: thumbnail, large image, and original image. Each specification is saved in a TIMImage object.
 */
@property(nonatomic,retain) NSArray * imageList;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | You do not need to consider this parameter when receiving messages. Its value is nil.
imageList | Saves all the specifications of the image. Currently, up to three types of specifications can be saved: thumbnail, large image, and original image. Each specification is saved in a TIMImage object.

**`TIMImage` description:**

When receiving the message, obtain all image specifications through `imageList`. These specifications are `TIMImage` data. After obtaining `TIMImage`, reserve a place by using the image size and download images of different specifications through `getImage` for display. **The downloaded data needs to be cached by the developer. The IM SDK downloads the data again from the server every time it calls `getImage`. We recommend that you use the `uuid` of images as the `key` to store images.**

**Prototype:**

```
@interface TIMImage : NSObject
/**
 *  Image ID, which is the internal identifier and can be used as the key for external caching.
 */
@property(nonatomic,strong) NSString * uuid;
/**
 *  Image type
 */
@property(nonatomic,assign) TIM_IMAGE_TYPE type;
/**
 *  Image size
 */
@property(nonatomic,assign) int size;
/**
 *  Image width
 */
@property(nonatomic,assign) int width;
/**
 *  Image height
 */
@property(nonatomic,assign) int height;
/**
 *  Download URL
 */
@property(nonatomic, strong) NSString * url;

/**
 *  Obtain the image
 *
 *  The downloaded data needs to be cached by the developer. The IM SDK downloads the data again every time it calls getImage. We recommend that you use the uuid of images as the key to store images.
 *
 *  @param path Storage path of the image
 *  @param succ Success callback, which returns image data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getImage:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Obtain the image (with the progress callback)
 *
 *  The downloaded data needs to be cached by the developer. The IM SDK downloads the data again every time it calls getImage. We recommend that you use the uuid of images as the key to store images.
 *
 *  @param path Storage path of the image
 *  @param progress Image download progress
 *  @param succ Success callback, which returns image data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getImage:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Image specifications:** each image has three specifications, which are Original (original image), Large (large image), and Thumb (thumbnail).

- **Original image:** the original image sent by the user, whose dimensions and size remain unchanged.
- **Large image:** an image obtained after the original image is proportionally compressed. After the compression, the height or width of the resulting image, whichever is smaller, is equal to 720 pixels.
- **Thumbnail:** an image obtained after the original image is proportionally compressed. After the compression, the height or width of the resulting image, whichever is smaller, is equal to 198 pixels.

>
>- If the size of the original image is less than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
>- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
>- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When the user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is directly downloaded when the user taps the thumbnail.
>- When an image is displayed on a tablet or PC, due to the high resolution and availability of a Wi-Fi or wired network, we recommend that the large image be displayed directly, and the original image be downloaded when the user taps or clicks the large image.

The following example fetches 10 messages from a conversation, obtains image messages, and downloads relevant data. **Example:**

```
//Here, we use the new message receipt callback as an example. The following shows the process of parsing image messages.
//Storage path of the received images
NSString * pic_path = @"/xxx/imgPath.jpg";
[conversation getMessage:10 last:nil succ:^(NSArray * msgList) {  //Obtained the messages successfully
	//Traverse all messages
	for (TIMMessage * msg in msgList) {
		//Traverse all elements in a message
		for (int i = 0; i < msg.elemCount; ++i) {
           TIMElem *elem = [msg getElem:i];
           //Image element
			if ([elem isKindOfClass:[TIMImageElem class]]) {
				TIMImageElem * image_elem = (TIMImageElem * )elem;

				//Traverse all image specifications (Thumbnail, Large, and Original)
				NSArray * imgList = [image_elem imageList];
				for (TIMImage * image in imgList) {
					[image getImage:pic_path succ:^(){  //Received the image successfully
						NSLog(@"SUCC: pic store to %@", pic_path);
					}fail:^(int code, NSString * err) {  //Failed to receive the image
						NSLog(@"ERR: code=%d, err=%@", code, err);
					}];
				}
			}
		}
	}
} fail:^(int code, NSString * err) {  //Failed to receive messages
	NSLog(@"Get Message Failed:%d->%@", code, err);
}];
```

### Receiving audio messages

After receiving a message, the recipient can obtain all `Elem` nodes from `TIMMessage` through `getElem`. `TIMSoundElem` represents audio message nodes. `path` is the audio information when creating the message and is empty when receiving the message. Reserve a place by using the audio length when receiving the message and download audio through `getSound`, which downloads from the server every time. If developers need to cache or store the data, use `uuid` as the `key` to store the audio file externally. The IM SDK does not store resource files.

**Prototype:**

```
@interface TIMSoundElem : TIMElem
/**
 *  ID of the upload task, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 *  Set to audio data when sending the message, and use getSound to obtain the data when receiving the message
 */
@property(nonatomic,strong) NSString * path;
/**
 *  Internal ID of the audio message
 */
@property(nonatomic,strong) NSString * uuid;
/**
 *  Audio data size
 */
@property(nonatomic,assign) int dataSize;
/**
 *  Audio length in seconds, which should be set when sending the message
 */
@property(nonatomic,assign) int second;

/**
 *  Obtain the download URL of the audio file
 *
 *  @param urlCallBack Obtain the URL callback
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save audio data to the specified file 
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 *
 *  @param path Storage path of the audio file
 *  @param succ Success callback, which returns audio data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Save audio data to the specified file (with the progress callback)
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 * 
 *  @param path Storage path of the audio file
 *  @param progress Audio download progress
 * @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Other parameters:**

Parameter | Description
---|---
path | Set to audio data when sending the message, and use getSound to obtain the data when receiving the message
uuid | Unique identifier for easy caching
dataSize | Audio file size
second | Audio length in seconds

**The read state of the audio message:** whether the audio file has been played. Use [message custom fields](https://intl.cloud.tencent.com/document/product/1047/34321) to implement this feature. For example, for `customInt`, a value of 0 means not played and a value of 1 means played. In this case, set `customInt` to 1 after the user taps to play the audio file.

```
@interface TIMMessage : NSObject
/**
 *  Set the custom integer, which defaults to 0
 *
 *  @param param Set the parameter
 *
 *  @return TRUE Set successfully
 */
- (BOOL) setCustomInt:(int32_t) param;

/**
 *  Obtain CustomInt
 *
 *  @return CustomInt
 */
- (int32_t)customInt;

@end
```

### Receiving file messages

After receiving a message, the recipient can obtain all `Elem` nodes from `TIMMessage` through `getElem`. `TIMFileElem` represents a file message node. `path` is the file path that is entered when creating the message and is empty when GET is performed for the message. You can choose to display only the file size and display name when receiving the message and download the file through `getFile`, which downloads from the server every time. To cache or store the data, the developer can use `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.

**Prototype:**

```
@interface TIMFileElem : TIMElem
/**
*  ID of the upload task, which can be used to query the upload progress. This parameter has been deprecated, and you can use TIMUploadProgressListener to monitor the upload progress.
*/
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
*  Path of the file to be uploaded (if the path is set, the file will be uploaded first)
*/
@property(nonatomic,strong) NSString * path;
/**
*  Internal ID of the file
*/
@property(nonatomic,strong) NSString * uuid;
/**
*  File size
*/
@property(nonatomic,assign) int fileSize;
/**
*  Display name of the file, which should be set when sending the message
*/
@property(nonatomic,strong) NSString * filename;

/**
*  Obtain the download URL of the file
*
*  @param urlCallBack Obtain the URL callback
*/
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
*  Save file data to the specified file
*
*  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
*
* @param path Storage path of the file
* @param succ Success callback, which returns data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getFile:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
*  Save file data to the specified file (with the progress callback)
*
*  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
*
* @param path Storage path of the file
* @param progress File download progress
* @param succ Success callback, which returns data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getFile:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | Path of the file to be uploaded
uuid | Unique ID for easy caching
fileSize | File size
filename | Display name of the file

### Receiving short video messages
After receiving a message, the recipient can obtain all Elem nodes from TIMMessage through getElem. The node of the TIMVideoElem type is a file message node, and the video and snapshot are obtained through the TIMVideo and TIMSnapshot objects. After receiving TIMVideoElem, download the video file and snapshot file through the APIs defined in the video and snapshot properties. To cache or store the data, developers can use uuid as the key to store the files externally. The IM SDK does not store resource files.
Prototype:

```
@interface TIMVideo : NSObject
/**
 *  Internal ID of the video message, which does not need to be set
 */
@property(nonatomic,strong) NSString * uuid;
/**
 *  Video file type, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * type;
/**
 *  Video size, which does not need to be set
 */
@property(nonatomic,assign) int size;
/**
 *  Video length, which is set when the message is sent
 */
@property(nonatomic,assign) int duration;

/**
 *  Obtain the download URL of the video
 *
 *  @param urlCallBack Obtain the URL callback
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Obtain the video
 *
 *  getVideo downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the files externally. The IM SDK does not store resource files.
 *
 *  @param path Storage path of the video
 * @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getVideo:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Obtain the video (with the progress callback)
 *
 *  getVideo downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the files externally. The IM SDK does not store resource files.
 *
 *  @param path Storage path of the video
 *  @param progress Video download progress
 * @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getVideo:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;

@end

@interface TIMSnapshot : NSObject
/**
*  Image ID, which does not need to be set
*/
@property(nonatomic,strong) NSString * uuid;
/**
*  Snapshot file type, which is set when the message is sent
*/
@property(nonatomic,strong) NSString * type;
/**
*  Image size, which does not need to be set
*/
@property(nonatomic,assign) int size;
/**
*  Image width, which is set when the message is sent
*/
@property(nonatomic,assign) int width;
/**
*  Image height, which is set when the message is sent
*/
@property(nonatomic,assign) int height;

/**
*  Obtain the download URL of the snapshot
*
*  @param urlCallBack Obtain the URL callback
*/
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
*  Obtain the image
*
*  getImage downloads file data from the server each time. If developers need to cache or store the data, use uuid as the key to store the image externally. The IM SDK does not store resource files.
*
*  @param path Storage path of the image
*  @param succ Success callback, which returns image data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getImage:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
*  Obtain the image (with the progress callback)
*
*  getImage downloads file data from the server each time. If developers need to cache or store the data, use uuid as the key to store the image externally. The IM SDK does not store resource files.
*
*  @param path Storage path of the image
*  @param progress Image download progress
*  @param succ Success callback, which returns image data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getImage:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end

//Here, we use the new message receipt callback as an example. The following shows the process of parsing short video messages.
//Storage path of the received video and snapshot
NSString * video_path = @"/xxx/video.mp4";
NSString * snapshot_path = @"/xxx/snapshot.jpg";
[conversation getMessage:10 last:nil succ:^(NSArray * msgList) {  //Obtained the messages successfully
   //Traverse all messages
   for (TIMMessage * msg in msgList) {
     //Traverse all elements in a message
     for (int i = 0; i < msg.elemCount; ++i) {
         TIMElem *elem = [msg getElem:i];
         if ([elem isKindOfClass:[TIMVideoElem class]]) {
              TIMVideoElem * video_elem = (TIMVideoElem * )elem;
              [video_elem.video getVideo:video_path succ:^()｛
                  NSLog(@"Downloaded the video file successfully");
              ｝ fail:^(int code, NSString * err) {
                  NSLog(@"Failed to download the video file:%@ %d", err, code);
              }];
              [video_elem.snapshot getImage:snapshot_path succ:^() {
                  NSLog(@"Downloaded the snapshot successfully");
              } fail:^(int code, NSString * err) {
                  NSLog(@"Failed to download the snapshot:%@ %d", err, code);
              }];
         }
     }
} fail:^(int code, NSString * err) {  //Failed to receive messages
    NSLog(@"Get Message Failed:%d->%@", code, err);
}];

```

## Message Properties 

### Whether a message is read

Determine whether a message is read through the message property `isReaded`. The read state depends on [read reports](https://intl.cloud.tencent.com/document/product/1047/34325) from the app.

```
@interface TIMMessage : NSObject
/**
 *  Read or unread
 *
 *  @return TRUE: read. FALSE: unread.
 */
-(BOOL) isReaded;
@end
```

### Message states

You can obtain the state of the current message through the `status` method, such as sending, sent successfully, failed to send, and deleted. For deleted messages, use the UI to determine the state and hide them.

```
/**
 *  Message state
 */
 typedef NS_ENUM(NSInteger, TIMMessageStatus){
 /**
  **  Message is being sent
  */
 TIM_MSG_STATUS_SENDING              = 1,
 /**
  **  Sent the message successfully
  */
 TIM_MSG_STATUS_SEND_SUCC            = 2,
 /**
  *  Failed to send the message
  */
 TIM_MSG_STATUS_SEND_FAIL            = 3,
 /**
  *  Message has been deleted
  */
 TIM_MSG_STATUS_HAS_DELETED          = 4,
 /**
  *  Message has been imported to local storage 
  */
 TIM_MSG_STATUS_LOCAL_STORED         = 5,
 /**
  *  Message has been recalled
  */
 TIM_MSG_STATUS_LOCAL_REVOKED        = 6,
 };

@interface TIMMessage : NSObject
/**
 *  Message state
 *
 *  @return TIMMessageStatus Message state
 */
-(TIMMessageStatus) status;
@end
```

### Whether a message was sent by yourself

Determine whether a message was sent by yourself through the message property `isSelf`, which is available when displayed on the interface.

```
@interface TIMMessage : NSObject
/**
 *  Whether the sender is yourself
 *
 *  @return TRUE: message sender. FALSE: message recipient
 */
-(BOOL) isSelf;
@end
```

### Message sender and the related profile

For group messages, use the `sender` method of `TIMMessage` to obtain the sender, or use the `GetSenderProfile` and `GetSenderGroupMemberProfile` methods to obtain the user’s profile and the profile of the belonging group of the user. In versions earlier than 1.9, you can only obtain user profiles from online messages thrown by `onNewMessage`. In version 1.9 and later, you can obtain profiles from messages obtained through `getMessage` (but not from local messages that were received before updating the version). For one-to-one chat messages, obtain the corresponding conversation through `getConversation` of `TIMMessage` and the peer in the conversation through `getReceiver`.

>This field obtains the user profile and writes it to the message body when the message is sent. If there are user profile updates in the future, this field does not change unless new messages are generated.

```
@interface TIMMessage : NSObject
/**
 *  Obtain the sender
 *
 *  @return Sender’s identifier
 */
-(NSString *) sender;
/**
 *  Obtain the sender’s profile
 *
 *  If stored locally, the sender’s profile is returned synchronously in the profileCallBack callback. Otherwise, the SDK pulls the sender’s profile from the server and returns it asynchronously in the profileCallBack callback.
 *
 *  @param  profileCallBack Sender profile callback
 *
 */
- (void)getSenderProfile:(ProfileCallBack)profileCallBack;
/**
 *  Obtain the sender’s profile in the group (may be empty if the sender is yourself)
 *
 *  @return Sender’s profile in the group. "nil" indicates that no profile is obtained or the message is not a group message. Currently, the only field that can be obtained is "member". To obtain other fields, use TIMGroupManager+Ext.h -> getGroupMembers. 
 */
-(TIMGroupMemberInfo *) GetSenderGroupMemberProfile;
@end
```

### Message time

The message time can be obtained through the message property `timestamp`. This time is the server time, but not the local time. When you create a message, the time is adjusted based on the server time and will be changed to the accurate server time after the message is sent successfully.

```
@interface TIMMessage : NSObject
/**
 *  Timestamp of the current message
 *
 *  @return Timestamp
 */
-(NSDate*) timestamp;
@end
```

### Deleting messages

Currently, deleting messages on the server is not supported. You can only delete messages in local storage. Messages deleted with this method are not physically deleted but only marked as deleted. Calling `getMessage` does not return the messages marked as deleted when the app is not uninstalled.

```
@interface TIMMessage : NSObject
/**
 *  Delete the message. Note that this only changes its state.
 *
 *  @return TRUE Succeeded
 */
-(BOOL) remove;
@end
```

### Message IDs

There are two types of message IDs. One is `msgId`, which is created when the message is generated. As this ID may conflict with messages generated by other users, a time dimension needs to be added. Messages generated within 10 minutes are considered distinguishable by `msgId`. The other identifier is `uniqueId`, which is generated after the message is sent successfully. IDs generated with this method are globally unique. These two methods need to be determined in the same conversation.

```
@interface TIMMessage : NSObject
/**
 *  Message ID
 */
-(NSString *) msgId;
/**
 *  Obtain the uniqueId of the message
 *
 *  @return uniqueId
 */
- (uint64_t) uniqueId;
@end
```

### Message custom fields

Developers can add custom fields to messages, such as the custom integer and custom binary data. You can customize different effects based on these two fields. For example, you can determine whether an audio message has been played. Note that these custom fields are only stored locally and not synchronized to the server. You will not obtain them after switching to another client.

```
@interface TIMMessage : NSObject
/**
 *  Set the custom integer, which defaults to 0
 *
 *  @param param Set the parameter
 *
 *  @return TRUE Set successfully
 */
- (BOOL) setCustomInt:(int32_t) param;
/**
 *  Set custom data content, which defaults to ""
 *
 *  @param data Set the parameter
 *
 *  @return TRUE Set successfully
 */
- (BOOL) setCustomData:(NSData*) data;
/**
 *  Obtain CustomInt
 *
 *  @return CustomInt
 */
- (int32_t) customInt;
/**
 *  Obtain CustomData
 *
 *  @return CustomData
 */
- (NSData*) customData;
@end
```

### Message priorities

Live streaming scenarios involve the like and red packet features. Like messages have a lower priority than red packet messages. Use `TIMCustomElem` to define message content and define the message priority when sending the message.

>This is valid for group messages only.

```
@interface TIMMessage : NSObject
/**
 *  Set the message priority
 *
 *  @param priority Priority
 *
 *  @return TRUE Set successfully
 */
- (BOOL) setPriority:(TIMMessagePriority)priority;
/**
 *  Obtain the priority of the message
 *
 *  @return Priority
 */
- (TIMMessagePriority) getPriority;
@end
```

### Read receipts

For one-to-one chat messages, after the user enables the read receipt feature, read messages are synchronized to the client when the recipient calls `setReadMessage`.

**Enable the read receipt feature:**

```
@interface TIMUserConfig : NSObject
/**
 *  After the read receipt feature is enabled, read receipts will be sent to the recipient when reporting read messages. This feature is only valid for one-to-one conversations.
 */
-(void) enableReadReceipt;
/**
 *  Message read receipt listener
 */
@property(nonatomic,weak) id<TIMMessageReceiptListener> messageReceiptListener;
@end
```

**Prototype:**

```
@interface TIMMessage : NSObject

/**
 *  Whether the recipient has read the message (valid for C2C messages only)
 *
 *  @return TRUE: read. FALSE: unread.
 */
-(BOOL) isPeerReaded;
@end
```

## Conversation Operations

### Obtaining all conversations

```
@interface TIMMessage : NSObject

/**
 *  Obtain the conversation (TIMConversation*) list
 *
 *  @return Conversation list
 */
-(NSArray*) getConversationList;
@end
```

**Example:**

```
NSArray * conversations = [[TIMManager sharedInstance] getConversationList];
NSLog(@"current session list : %@", [conversations description])
```

### Obtaining local messages in a conversation

The IM SDK stores messages locally, which can be obtained through `getLocalMessage` of `TIMConversation`. This is an asynchronous method, which requires callback to obtain message data. For one-to-one chats, offline messages can be obtained after login. For group chats, only the last message is obtained after logging in with roamed recent contacts enabled and using `getMessage` to obtain roaming messages. For resource messages, such as image and audio messages, the message body only contains descriptive information. Additional APIs are required to download data. For more information, see [Parsing Messages](#parsing-messages). After data is downloaded, the data is not cached, but the caller must cache the data.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Obtain messages in a local conversation
 *
 *  @param count Obtain the number of messages
 *  @param last Last message
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 This operation was successful
 */
-(int) getLocalMessage: (int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Specifies the number of messages to obtain.
last | Specifies the obtained last message. If "last" is nil, read from the latest message.
succ | Success callback
fail | Failure callback

**Example:**

```
[conversation getLocalMessage:10 last:nil succ:^(NSArray * msgList) {
	for (TIMMessage * msg in msgList) {
		if ([msg isKindOfClass:[TIMMessage class]]) {
			NSLog(@"GetOneMessage:%@", msg);
		}
	}
}fail:^(int code, NSString * err) {
	NSLog(@"Get Message Failed:%d->%@", code, err);
}];
```

### Obtaining conversation roaming messages

For group chats, the user obtains roaming messages after login. For C2C chats, the user can obtain roaming messages after the roaming service is enabled. Roaming messages are obtained through the `getMessage` API of the IM SDK. If local messages are continuous, they are obtained directly. Otherwise, missing messages need to be obtained over the network. For resource messages, such as image and audio messages, the message body only contains descriptive information. Additional APIs are required to download data. For more information, see the section about parsing messages. After data is downloaded, the data is not cached, but the caller must cache the data.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Obtain messages in a conversation
 *
 *  @param count Obtain the number of messages
 *  @param last Last message
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 This operation was successful
 */
-(int) getMessage: (int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Specifies the number of messages to obtain.
last | Specifies the obtained last message. If "last" is nil, read from the latest message.
succ | Success callback
fail | Failure callback

**Example:**

```
[conversation getMessage:10 last:nil succ:^(NSArray * msgList) {
	for (TIMMessage * msg in msgList) {
		if ([msg isKindOfClass:[TIMMessage class]]) {
			NSLog(@"GetOneMessage:%@", msg);
		}
	}
}fail:^(int code, NSString * err) {
	NSLog(@"Get Message Failed:%d->%@", code, err);
}];
```

### Deleting conversations

There are two methods to delete a conversation, each of which applies to different scenarios. One is to delete the conversation and save all messages, and the other is to delete the conversation together with all its messages. Note that, for group chats, `getMessage` pulls roaming messages. Therefore, it is possible that messages are deleted successfully but roaming messages can still be pulled. If you do not need to pull roaming messages, you can use `getLocalMessage` to obtain messages, or use `getMessage` to pull a specified number of messages, such as a certain number of unread messages. `deleteConversation` deletes the conversation only, and `deleteConversationAndMessages` deletes the conversation and all its messages.

**Prototype:**

```
@protocol TIMManager : NSObject
/**
 *  Delete a conversation
 *
 *  @param type Type of the conversation. TIM_C2C indicates the one-to-one chat, and TIM_GROUP indicates the group chat.
 *  @param receiver User identifier or group ID
 *
 *  @return TRUE: deleted successfully. FALSE: failed to delete.
 */
-(BOOL) deleteConversation:(TIMConversationType)type receiver:(NSString*)receiver;
/**
 *  Delete a conversation and its messages
 *
 *  @param type Type of the conversation. TIM_C2C indicates the one-to-one chat, and TIM_GROUP indicates the group chat.
 *  @param receiver User’s identifier or group ID
 *
 *  @return TRUE: deleted successfully. FALSE: failed to delete.
 */
-(BOOL) deleteConversationAndMessages:(TIMConversationType)type receiver:(NSString*)receiver;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | Conversation type. For a one-to-one chat, enter TIM_C2C. For a group chat, enter TIM_GROUP.
receiver | Conversation identifier. For a one-to-one chat, the receiver is the peer’s identifier. For a group chat, the receiver is the group ID.

The following example shows how to delete the C2C conversation with a friend named "iOS_002". **Example:**

```
[[TIMManager sharedInstance] deleteConversation:TIM_C2C receiver:@"iOS_002"];
```

### Synchronously obtaining the last message of a conversation

The UI displays the last messages of the user on the recent contacts screen. The synchronization API `getLastMsg` was added in version 1.9 and later to allow users to obtain and display the last messages. **This feature requires a network connection**. Obtaining messages through this API does not filter messages in the deleted state, which need to be blocked at the app level. To obtain multiple recent messages, call `getMessage`.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Obtain the last message from cache
 *  @return Last message (TIMMessage*)
 */
- (TIMMessage*)getLastMsg;

/**
 *  Obtain the roaming messages of a conversation
 *  @param count Obtain the number of messages
 *  @param last Last message. If "last" is nil, read from the latest message.
 *  @param succ Success callback
 *  @param fail Failure callback
 *  @return 0: this operation was successful. 1: this operation failed.
 */
- (int)getMessage:(int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Number of messages to obtain, which is 20 at the maximum 


### Setting conversation drafts

The UI displays the draft of the user on the recent contacts screen. An API to set and obtain drafts was added in version 2.2 and later to allow users to set conversation drafts. **Draft information is stored in a local database and can be obtained after login**.

**Prototype:**

```
@interface TIMMessageDraft : NSObject
/**
 *  Set custom data
 *
 *  @param userData Custom Data
 *
 *  @return 0 Succeeded
 */
-(int) setUserData:(NSData*)userData;
/**
 *  Obtain custom data
 *
 *  @return Custom data
 */
-(NSData*) getUserData;
/**
 *  Add Elem
 *
 *  @param elem Elem structure
 *
 *  @return 0      Succeeded
 *          1       Adding Elem is not allowed (file or audio or more than two Elems)
 *          2       Unknown Elem
 */
-(int) addElem:(TIMElem*)elem;
/**
 *  Obtain the Elem for the corresponding index
 *
 * @param index Index
 *
 * @return Return the corresponding Elem
 */
-(TIMElem*) getElem:(int)index;
/**
 *  Obtain the number of Elems
 *
 *  @return elem Quantity
 */
-(int) elemCount;
/**
 *  Message corresponding to the draft
 *
 *  @return Message
 */
-(TIMMessage*) transformToMessage;
/**
 *  Timestamp of the current message
 *
 *  @return Timestamp
 */
-(NSDate*) timestamp;
@end

@interface TIMConversation : NSObject
/**
 *  Set the conversation draft
 *
 *  @param draft Draft content
 *
 *  @return 0 Succeeded
 */
-(int) setDraft:(TIMMessageDraft*)draft;
/**
 *  Obtain the conversation draft
 *
 *  @return Draft content, and nil is returned if no draft exists
 */
-(TIMMessageDraft*) getDraft;
@end
```

**Parameter description:**

Parameter | Description
---|---
draft | Draft to be set. To clear a conversation draft, pass in nil.

### Deleting local conversation messages

The IM SDK allows you to delete local conversation messages while keeping the conversation. **The IM SKD pulls the messages from the server again the next time it pulls messages for group conversations**.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Delete local conversation messages
 *
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 This operation was successful
 */
-(int) deleteLocalMessage:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
succ | Success callback
fail | Failure callback

### Obtaining messages with specified local IDs

IM SDK 2.5.3 provides an API to obtain the message corresponding to a specified local ID.

**Prototype:**

```
/**
 *  Message
 */
@interface TIMMessage : NSObject
/**
 *  Obtain the message locator
 *
 *  @return locator
 */
- (TIMMessageLocator*) locator;
@end
@interface TIMConversation : NSObject
/**
 *  Obtain messages in a conversation
 *
 *  @param locators Array of message locators (TIMMessageLocator)
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 This operation was successful
 */
-(int) findMessages:(NSArray*)locators succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
locators | List of message locators (TIMMessageLocator)
succ | Success callback, which returns the list of messages
fail | Failure callback

### Recalling messages

Starting with version 3.1.0, the IM SDK provides an API to recall messages. You can recall the messages that have been sent by calling the `revokeMessage` API of `TIMConversation`.

>
> - The API works for C2C and group conversations, but not onlineMessage, AVChatRoom, and BChatRoom.
> - By default, messages that were sent within the last 2 minutes can be recalled.

**Prototype:**

```
/**
 > - Message recall works for C2C and group conversations, but not onlineMessage, AVChatRoom, and BChatRoom.
 *  @param msg Recalled message
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0: this operation was successful. 1: this operation failed.
 */
- (int)revokeMessage:(TIMMessage*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
```

After a message is recalled, other members in the group or the peer in the C2C conversation receives a message recall notification. In addition, the message recall notification listener `TIMMessageRevokeListener` notifies the upper-layer app. You can configure the message recall notification listener before login through `messageRevokeListener` of `TIMUserConfig`. For more information, see [User Configuration](https://intl.cloud.tencent.com/document/product/1047/34313).

**Prototype:**

```
@protocol TIMMessageRevokeListener <NSObject>
@optional
/**
 *  Message recall notification
 *
 *  @param locator Identifier of the recalled message
 */
- (void)onRevokeMessage:(TIMMessageLocator*)locator;

@end

```

After receiving a message recall notification, you can use the `respondsToLocator` method in `TIMMessage` to check whether the current message has been recalled by the sender, then refresh the UI when necessary.

**Prototype:**

```
/**
 *  Whether the message corresponds to the locator
 *
 *  @param locator Message locator
 *
 *  @return YES: it is the right message. NO: it is not the right message.
 */
- (BOOL)respondsToLocator:(TIMMessageLocator*)locator;

```

## System Messages

In addition to C2C chat and group chat, system messages is also a conversation type (TIMConversationType). System messages are notification messages sent by the system backend for various events and cannot be sent by users. Currently, there are two kinds of system messages: relationship chain system messages and group system messages.

- **Relationship chain change system messages:** when the user has a friend request or is deleted by a contact, the system sends a change notification and the developer can refresh the friend list. For more information, see [Relationship Chain Change System Notifications](https://intl.cloud.tencent.com/zh/document/product/1047/34332#.E5.85.B3.E7.B3.BB.E9.93.BE.E5.8F.98.E6.9B.B4.E7.B3.BB.E7.BB.9F.E9.80.9A.E7.9F.A5).

- **Group event messages:** when a group profile is modified, such as changes to the group name or group members, the system sends a group event message in the group. The developer can choose whether to display the message or not and can refresh the group profile or group members at the same time. For more information, see [Group Management - Group Event Messages](https://intl.cloud.tencent.com/document/product/1047/34329).

- **Group system messages:** when the group owner is removed or non-members are invited to the group, the system sends a group system message to users. For more information, see [Group Management - Group System Messages](https://intl.cloud.tencent.com/document/product/1047/34329).
