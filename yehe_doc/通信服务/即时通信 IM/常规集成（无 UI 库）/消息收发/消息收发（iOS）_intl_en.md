## Sending Messages

### Sending common messages

#### Getting a conversation

A conversation refers to a conversation with a user or a group. To send or receive messages in a one-to-one or group conversation, you need to first get the conversation by specifying the conversation type (one-to-one or group) and the other participant’s identifier (the other participant’s account or group ID). Use `getConversation` to get a conversation.
> If the conversation is not stored locally, calls to TIMConversation APIs will fail. We recommend that you operate on the TIMConversation object after receiving the TIMUserConfig -> TIMRefreshListener callback.

**Prototype:**

```
@interface TIMManager : NSObject
/**
 *  Get a conversation
 *
 *  @param type Type of the conversation. TIM_C2C indicates a one-to-one chat and TIM_GROUP indicates a group chat.
 *  @param conversationId For a C2C conversation, use the other participant’s identifier, and for a GROUP conversation, use the group ID.
 *
 *  @return A Conversation object
 */
- (TIMConversation*)getConversation:(TIMConversationType)type receiver:(NSString*)conversationId;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | Conversation type. For a one-to-one chat, enter TIM_C2C, and for a group chat, enter TIM_GROUP.
conversationId | Conversation identifier. For a one-to-one chat, receiver is the other participant’s identifier. For a group chat, receiver is the group ID.

**Get the one-to-one conversation in which the other participant’s `identifier` is “iOS-001”:**

```
TIMConversation * c2c_conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS-001"];
```

**Get the group conversation with the group ID of “TGID1JYSZEAEQ”:** 

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
msg | The message.
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
>- text passes the text message to send.
>- In the failure callback, code indicates the error code (see [Error Codes](/doc/product/269/1671) for more information), and err indicates the error description.

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

An image message is defined by `TIMImageElem`, which is a subclass of `TIMElem`. These messages can contain image content. Sending an image means adding `TIMImageElem` to `TIMMessage` and sending it along with the message. When sending an image, you only need to set `path`, the image path. You can get all image types through `imageList` after the message is sent successfully. In addition, use `TIMUserConfig -> TIMUploadProgressListener` to listen to the current upload progress.

**`TIMImageElem` prototype:**

```
/**
 *  Store the path of the image to send, which must be a local path. See the following example.
 */
@interface TIMImageElem : TIMElem
/**
 *  The path of the image to send
 */
@property(nonatomic,retain) NSString * path;
/**
 *  This parameter saves all specifications of the image when it is received. You do not need to consider it when sending the message
 */
@property(nonatomic,retain) NSArray * imageList;
/**
 * Upload task ID, which can be used to query the upload progress. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;

/**
 *  Image compression level. See TIM_IMAGE_COMPRESS_TYPE for more information (applies to jpg format only).
 */
@property(nonatomic,assign) TIM_IMAGE_COMPRESS_TYPE level;

/**
 *  Image format. See TIM_IMAGE_FORMAT for more information.
 */
@property(nonatomic,assign) TIM_IMAGE_FORMAT format;
@end
```

**Parameter description:**

| Parameter | Description |
|---|---|
| path | Stores the path of the image to send, which must be a local path. See the example of sending an image. |
| imageList | Saves all specifications of the image when it is received. You do not need to consider it when sending the message. See the section about receiving image messages. |
| taskId | Can be used to query the upload progress when sending images. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress. |
| level | Images need to be compressed before being sent, and level represents the compression level. See the definition of TIM_IMAGE_COMPRESS_TYPE for more information. |
| format | Image format. See TIM_IMAGE_FORMAT for more information. |

The following example sends an image with the absolute path of `/xxx/imgPath.jpg`. **Example:**

```
/**
*  Get the one-to-one conversation with the same user iOS-001
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
[conversation sendMessage:msg succ:^(){  //Successful
       NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {  //Failed
       NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending emoji messages

An emoji message is defined by `TIMFaceElem`. The IM SDK does not provide an emoji package. Developers can use `index` to store the indexes of the emojis they have in their emoji packages. Alternatively, users can directly use `data` to store emoji binary data and the string `key`. Either way, users can customize emojis. The SDK is only responsible for passing them through.

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

>You only need to pass index or data. The IM SDK is responsible for passing the information through.

Parameter | Description
---|---
index | Emoji index, which is customized by the developer
data | Emoji binary data, which is customized by the developer

The following example sends an emoji with an index of 10. The developer must have an emoji package at both sides with an emoji with the index 10. The emoji can also be identified by binary data through data. **Example:**

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

An audio message is defined by `TIMSoundElem`, where `data` stores audio data, for which you need to provide the audio length in seconds.

>
>- A message can contain only one audio `Elem`. If multiple audio `Elem` objects are added, the `AddElem` function returns error 1 and the audio elements will not be added.
>- Audio and file `Elem` objects are not always received in the order they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects are not guaranteed to be sorted in the order they are sent. 

```
/**
 *  Audio message Elem
 */
@interface TIMSoundElem : TIMElem
/**
 *  Upload task ID, which can be used to query the upload progress. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 *  The path to the audio file to upload. Use getSound to get the data when receiving the message
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
 *  Get the download URL of the audio file
 *
 *  @param urlCallBack Get the URL callback
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save audio data to the specified file
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 *
 *  @param path Audio storage path
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Save audio data to the specified file (with progress callback)
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 *
 *  @param path Audio storage path
 *  @param progress Audio download progress
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

| Parameter | Description |
|---|---|
| path | The file path of the audio to upload. |
| uuid | The unique identifier generated after the audio is uploaded. The user can save the file based on this identifier. The IM SDK does not save resource data internally. |
| dataSize | Audio data size. |
| second | Audio length. |

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

A location message is defined by `TIMLocationElem`, where `desc` stores the description information of the location. `longitude` and `latitude` represent the longitude and latitude of the location respectively.

```
@interface TIMLocationElem : TIMElem
/**
 *  Description of the location, which should be set when sending the message
 */
@property(nonatomic,retain) NSString * desc;
/**
 *  The latitude, which should be set when sending the message
 */
@property(nonatomic,assign) double latitude;
/**
 *  The longitude, which should be set when sending the message
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

> Audio and file `Elem` objects are not always received in the order they are added. We recommend that you determine and display `Elem` objects one by one.

```
/**
 *  File message Elem
 */
@interface TIMFileElem : TIMElem
/**
 *  Upload task ID, which can be used to query the upload progress. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 *  The path of the file to upload (If the path is set, the file will be uploaded first)
 */
@property(nonatomic,strong) NSString * path;
/**
 *  The internal ID of the file
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
 *  Get the download URL of the file
 *
 *  @param urlCallBack Get the URL callback 
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save file data to the specified file
 *
 *  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
 *
 *  @param path File storage path
 *  @param succ Success callback, which returns data
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getFile:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Save file data to the specified file (with progress callback)
 *
 *  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
 *
 *  @param path File storage path
 *  @param progress File download progress
 *  @param succ Success callback, which returns data
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getFile:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | File path.
data | The binary data of the file to send. You only need to set path or data. We recommend using path.
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

### Custom message sending APIs

Custom messages are messages whose format and content are defined by developers when the built-in message types cannot meet their special needs. The IM SDK is only responsible for passing custom messages through. If iOS APNs push notifications are required, you need to provide a push text description for display. A custom message is defined by `TIMCustomElem`, where `data` stores the binary data of the message, and the data format is defined by the developer. A message can contain multiple custom `Elem` objects which can be mixed with other `Elem` objects. In the case of offline `Push`, the `desc` of each `Elem` is put in a stack and delivered.

```
/**
 *  Custom message type
 */
@interface TIMCustomElem : TIMElem
/**
 *  Custom message binary data
 */
@property(nonatomic,strong) NSData * data;
/**
 *  Custom message description, which is used for display during offline push. This parameter has been disused, so please use offlinePushInfo in TIMMessage to configure this information.
 */
@property(nonatomic,strong) NSString * desc DEPRECATED_ATTRIBUTE;
/**
 *  Extension field information in offline push. This parameter has been disused, so please use offlinePushInfo in TIMMessage for configuration.
 */
@property(nonatomic,strong) NSString * ext DEPRECATED_ATTRIBUTE;
/**
 *  Sound field information in offline push. This parameter has been disused, so please use offlinePushInfo in TIMMessage to configure the information.
 */
@property(nonatomic,strong) NSString * sound DEPRECATED_ATTRIBUTE;
@end
```

**Parameter description:**

Parameter | Description
---|---
data | Binary data of the custom message.

The following example adds an XML-based message, the display of which is determined by the developer. **Example:**

```
// Custom message using XML protocol
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

A short video message is defined by `TIMVideoElem`, which is a subclass of `TIMElem`. These messages can contain video snapshots and content. In this case, sending a short video is actually adding `TIMVideoElem` to `TIMMessage` and sending it along with the message.

**`TIMVideoElem` prototype:**

```
/**
 *  Short video message
 */
@interface TIMVideoElem : TIMElem
/**
 *  Upload task ID, which can be used to query the upload progress. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress.
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
taskId | Upload task ID, which can be used to query the upload progress. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress.
videoPath | Path of the local video to be sent
video | Video information. Sets the type and duration parameters when sending the message.
snapshotPath | Path of the local snapshot of the short video to be sent
snapshot | Snapshot information. Sets the type, width, and height when sending the message.

The following example shows how to send a short video message. **Example:**

```
/**
*  Get the one-to-one conversation with the same user iOS-001
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
videoElem.snapshotPath = @"/xxx/snapshotPath.jpg";
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
[conversation sendMessage:msg succ:^(){  //Successful
       NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {  //Failed
       NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Elem order

Currently, the file and sound elements are not necessarily transferred in the sequence that they are added. Other elements are transferred in the sequence that they are added. However, we do not recommend you rely heavily on the element sequence when processing elements. Instead, you should process elements, one by one, by type to prevent process crashes when exceptions occur.

### Online messages

In some scenarios, you need to send online messages, which can only be received when the user is online. If not online when the messages are sent, the user will not see them after the next login. Online messages can be used as notifications. Moreover, online messages will not be stored nor included in the unread count. The API for sending online messages is similar to `sendMessage`.

>
>- Versions earlier than 2.5.3 only support one-to-one messages.
>- Version 2.5.3 and higher support group messages (AVChatRoom and BChatRoom types are currently not supported).

```
@interface TIMConversation : NSObject
/**
 *  Send online message (the server does not save the message)
 *
 *  @param msg  Message body
 *  @param succ  Success callback
 *  @param fail   Failure callback
 *
 *  @return 0 Successful
 */
-(int) sendOnlineMessage: (TIMMessage*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

### Forwarding messages

In version 2.4.0 and higher, you can use `copyFrom` in `TIMMessage` to copy the content of another message to the current message and resend it to contacts.

**Prototype:**

```
/**
 *  Message
 */
@interface TIMMessage : NSObject
/**
 *  Copy properties in the message (Elem, priority, online, and offlinePushInfo)
 *
 *  @param srcMsg Source message
 *
 *  @return 0 Successful
 */
- (int)copyFrom:(TIMMessage*)srcMsg;
@end
```

## Receiving Messages

If you need to be notified of new messages, you only need to register the new message notification callback `TIMMessageListener`. If you have logged in, the IM SDK throws new messages through `onNewMessage` in the callback. Callback message content is passed through the `TIMMessage` parameter. With `TIMMessage`, you can get detailed information about messages and the corresponding conversations, such as text, audio data, and images. For more information, see [Parsing messages](#.E6.B6.88.E6.81.AF.E8.A7.A3.E6.9E.90).

> Messages thrown through `onNewMessage` are not necessarily unread messages. They can also be messages that have not been displayed locally, such as when messages are read on another client and pulling recent contacts obtains the last messages of conversations. If not stored locally, these messages are thrown by this method. After the user logs in, the IM SDK pulls offline messages. To avoid missing message notifications, you need to register new message notifications before login.
Group system messages, relationship chain changes, and friend profile changes will also be thrown through the callback `onNewMessage`.


**Prototype:**

```
@protocol TIMMessageListener
@optional
/**
 *  New message notification
 *
 *  @param msgs List of new messages, an array of TIMMessage types
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
msgs | A list of new messages. Note that multiple messages may be thrown out. Messages in the same conversation are sorted from old to new.

The following example sets a message callback notification and prints new messages when they arrive. **Example:**

```
@interface TIMMessageListenerImpl : NSObject
- (void)onNewMessage:(NSArray*) msgs;
@end
@implementation TIMMessageListenerImpl
- (void)onNewMessage:(NSArray*) msgs {
    NSLog(@"NewMessages: %@", msgs);
}
@end
TIMMessageListenerImpl * impl = [[TIMMessageListenerImpl alloc] init];
[[TIMManager sharedInstance] addMessageListener:impl];
```

### Parsing messages

After receiving messages, you can get all `Elem` nodes from `TIMMessage` through `getElem.

**Prototype of traversing `Elem`:**

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

After receiving messages, the recipient can get all `Elem` nodes from `TIMMessage` through `getElem`. Nodes of the `TIMImageElem` type are message nodes. The specifications of the image can be obtained through `imageList` for display purposes.

** `TIMImageElem` prototype:**

```
**
 *  Image message Elem
 */
@interface TIMImageElem : TIMElem
/**
 *  The path of the image to send
 */
@property(nonatomic,retain) NSString * path;
/**
 *  Save all specifications of the image. Currently, up to three types of specifications can be saved: thumbnail, large image, and original image. Each specification is saved in a TIMImage object.
 */
@property(nonatomic,retain) NSArray * imageList;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | You do not need to consider this parameter when receiving messages. It has a value of nil.
imageList | Saves all specifications of the image. Currently, up to three types of specifications can be saved: thumbnail, large image, and original image. Each specification is saved in a TIMImage object.

**`TIMImage` description:**

When receiving the message, get all image specifications through `imageList`. These specifications are `TIMImage` data. After getting `TIMImage`, reserve a place using the image size and download images of different specifications through `getImage` for display. **The downloaded data needs to be cached by the developer. The IM SDK downloads the data again from the server every time it calls `getImage`. We recommend that you use the `uuid` of images as the `key` to store images.**

**Prototype:**

```
@interface TIMImage : NSObject
/**
 *  Image ID, which is the internal identifier. It can be used as the key for external caching.
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
 *  The download URL
 */
@property(nonatomic, strong) NSString * url;

/**
 *  Get the image
 *
 *  The downloaded data needs to be cached by the developer. The IM SDK downloads the data again every time it calls getImage. We recommend that you use the uuid of images as the key to store images.
 *
 *  @param path Image storage path
 *  @param succ Success callback which returns image data
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getImage:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Get the image (with progress callback)
 *
 *  The downloaded data needs to be cached by the developer. The IM SDK downloads the data again every time it calls getImage. We recommend that you use the uuid of images as the key to store images.
 *
 *  @param path Image storage path
 *  @param progress Image download progress
 *  @param succ Success callback which returns image data
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getImage:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Image specifications:** every image has three specifications, including Original (original image), Large (large image), and Thumb (thumbnail).

- **Original image:** the original image sent by the user, whose dimensions and size remain unchanged.
- **Large image:** an image obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 720 pixels.
- **Thumbnail:** an image obtained after the original image is proportionally compressed. After the compression, the smaller one of the height and width is equal to 198 pixels.

>
>- If the size of the original image is smaller than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
>- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
>- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When the user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is directly downloaded when the user taps the thumbnail.
>- When an image is displayed on a tablet or PC, due to the high resolution and availability of a Wi-Fi or wired network, we recommend that the large image be displayed directly, and the original image be downloaded when the user taps or clicks the large image.

The following example fetches 10 messages from a conversation, gets image messages, and downloads relevant data. **Example:**

```
//Here, we use the new message receipt callback as an example. The following shows the process of parsing image messages
//The path to which the received images are saved
NSString * pic_path = @"/xxx/imgPath.jpg";
[conversation getMessage:10 last:nil succ:^(NSArray * msgList) {  //Got the messages successfully
	//Traverse all messages
	for (TIMMessage * msg in msgList) {
		//Traverse all elements in a message
		for (int i = 0; i < msg.elemCount; ++i) {
           TIMElem *elem = [msg getElem:i];
           //Image element
			if ([elem isKindOfClass:[TIMImageElem class]]) {
				TIMImageElem * image_elem = (TIMImageElem * )elem;

				//Traverse all image specifications (Thumbnail, Large, Original)
				NSArray * imgList = [image_elem imageList];
				for (TIMImage * image in imgList) {
					[image getImage:pic_path succ:^(){  //Received successfully
						NSLog(@"SUCC: pic store to %@", pic_path);
					}fail:^(int code, NSString * err) {  //Failed to receive
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

After receiving a message, the recipient can get all `Elem` nodes from `TIMMessage` through `getElem`. `TIMSoundElem` represents audio message nodes. `path` is the audio information when creating the message and is empty when receiving the message. Reserve a place using the audio length when receiving the message and download audio through `getSound`, which downloads from the server every time. If developers need to cache or store the data, use `uuid` as the `key` to store the audio file externally. The IM SDK does not store resource files.

**Prototype:**

```
@interface TIMSoundElem : TIMElem
/**
 *  Upload task ID, which can be used to query the upload progress. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 *  Set to audio data when sending the message, and use getSound to get the data when receiving the message
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
 *  Get the download URL of the audio file
 *
 *  @param urlCallBack Get the URL callback
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save audio data to the specified file 
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 *
 *  @param path Audio storage path
 *  @param succ Success callback which returns audio data
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Save audio data to the specified file (with progress callback)
 *
 *  getSound downloads audio data from the server every time. If developers need to cache or store the data, use uuid as the key to store the audio file externally. The IM SDK does not store resource files.
 * 
 *  @param path Audio storage path
 *  @param progress Audio download progress
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Other parameters:**

Parameter | Description
---|---
path | Set to audio data when sending the message, and use getSound to get the data when receiving the message.
uuid | The unique identifier for easy caching.
dataSize | Audio file size.
second | Audio length in seconds.

**The read status of the audio message:** whether the audio has been played. Use message custom fields to implement this feature. For example, for `customInt`, a value of 0 means not played and a value of 1 means played. In this case, set `customInt` to 1 after the user clicks to play the audio.

```
@interface TIMMessage : NSObject
/**
 *  Set custom integer. The default value is 0.
 *
 *  @param param Set parameter
 *
 *  @return TRUE Setting successful
 */
- (BOOL) setCustomInt:(int32_t) param;

/**
 *  Get CustomInt
 *
 *  @return CustomInt
 */
- (int32_t)customInt;

@end
```

### Receiving file messages

After receiving a message, the recipient can get all `Elem` nodes from `TIMMessage` through `getElem`. `TIMFileElem` represents a file message node. `path` is the file path entered when creating the message and is empty when GET is performed for the message. You can choose to display only the file size and display name when receiving the message and download the file through `getFile`, which downloads from the server every time. To cache or store the data, the developer can use `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.

**Prototype:**

```
@interface TIMFileElem : TIMElem
/**
*  Upload task ID, which can be used to query the upload progress. This parameter has been disused, so please use TIMUploadProgressListener to listen to the upload progress.
*/
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
*  The path of the file to upload (If the path is set, the file will be uploaded first)
*/
@property(nonatomic,strong) NSString * path;
/**
*  The internal ID of the file
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
*  Get the download URL of the file
*
*  @param urlCallBack Get the URL callback
*/
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
*  Save file data to the specified file
*
*  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
*
*  @param path File storage path
*  @param succ Success callback, which returns data
*  @param fail     Failure callback, which returns the error code and error description
*/
- (void)getFile:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
*  Save file data to the specified file (with progress callback)
*
*  getFile downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the file externally. The IM SDK does not store resource files.
*
*  @param path File storage path
*  @param progress File download progress
*  @param succ Success callback, which returns data
*  @param fail     Failure callback, which returns the error code and error description
*/
- (void)getFile:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | The path of the file to upload.
uuid | The unique ID for easy caching.
fileSize | File size.
filename | Display name of the file.

### Receiving short video messages
After receiving a message, the recipient can get all Elem nodes from TIMMessage through getElem. The node of the TIMVideoElem type is a file message node, and the video and snapshot are obtained through TIMVideo and TIMSnapshot objects. After receiving TIMVideoElem, download the video file and snapshot file through the APIs defined in the video and snapshot properties. To cache or store the data, developers can use uuid as the key to store the files externally. The IM SDK does not store resource files.
Prototype:

```
@interface TIMVideo : NSObject
/**
 *  Internal ID of the video message, no need to set it
 */
@property(nonatomic,strong) NSString * uuid;
/**
 *  Video file type, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * type;
/**
 *  Video size, no need to set it
 */
@property(nonatomic,assign) int size;
/**
 *  Video length, which is set when the message is sent
 */
@property(nonatomic,assign) int duration;

/**
 *  Get the download URL of the video
 *
 *  @param urlCallBack Get the URL callback
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Get the video
 *
 *  getVideo downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the files externally. The IM SDK does not store resource files.
 *
 *  @param path The path to which the video is saved
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getVideo:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 *  Get the video (with progress callback)
 *
 *  getVideo downloads file data from the server every time. If developers need to cache or store the data, use uuid as the key to store the files externally. The IM SDK does not store resource files.
 *
 *  @param path The path to which the video is saved
 *  @param progress Video download progress
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)getVideo:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;

@end

@interface TIMSnapshot : NSObject
/**
*  Image ID, no need to set it
*/
@property(nonatomic,strong) NSString * uuid;
/**
*  Snapshot file type, which is set when the message is sent
*/
@property(nonatomic,strong) NSString * type;
/**
*  Image size, no need to set it
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
*  Get the download URL of the snapshot
*
*  @param urlCallBack Get the URL callback
*/
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
*  Get the image
*
*  getImage downloads file data from the server each time. If developers need to cache or store the data, use uuid as the key to store the image externally. The IM SDK does not store resource files.
*
*  @param path Image storage path
*  @param succ Success callback which returns image data
*  @param fail     Failure callback, which returns the error code and error description
*/
- (void)getImage:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
*  Get the image (with progress callback)
*
*  getImage downloads file data from the server each time. If developers need to cache or store the data, use uuid as the key to store the image externally. The IM SDK does not store resource files.
*
*  @param path Image storage path
*  @param progress Image download progress
*  @param succ Success callback which returns image data
*  @param fail     Failure callback, which returns the error code and error description
*/
- (void)getImage:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end

//Here, we use the new message receipt callback as an example. The following shows the process of parsing short video messages
//The path to which the received video and snapshot are saved
NSString * video_path = @"/xxx/video.mp4";
NSString * snapshot_path = @"/xxx/snapshot.jpg";
[conversation getMessage:10 last:nil succ:^(NSArray * msgList) {  //Got the messages successfully
   //Traverse all messages
   for (TIMMessage * msg in msgList) {
     //Traverse all elements in a message
     for (int i = 0; i < msg.elemCount; ++i) {
         TIMElem *elem = [msg getElem:i];
         if ([elem isKindOfClass:[TIMVideoElem class]]) {
              TIMVideoElem * video_elem = (TIMVideoElem * )elem;
              [video_elem.video getVideo:video_path succ:^()｛
                  NSLog(@"Video file downloaded successfully");
              ｝ fail:^(int code, NSString * err) {
                  NSLog(@"Failed to download the video file:%@ %d", err, code);
              }];
              [video_elem.snapshot getImage:snapshot_path succ:^() {
                  NSLog(@"Snapshot downloaded successfully");
              } fail:^(int code, NSString * err) {
                  NSLog(@"Failed to download the video snapshot:%@ %d", err, code);
              }];
         }
     }
} fail:^(int code, NSString * err) {  //Failed to receive messages
    NSLog(@"Get Message Failed:%d->%@", code, err);
}];

```

## Message Properties 

### Checking whether a message is read

Determine whether a message is read through the message property `isReaded`. The read status depends on the read reports from the app.

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

### Message status

You can get the status of the current message through the `status` method, such as sending, sent successfully, failed to send, and deleted. For deleted messages, use the UI to determine the status and hide them.

```
/**
 *  Message status
 */
 typedef NS_ENUM(NSInteger, TIMMessageStatus){
 /**
  *  Sending message
  */
 TIM_MSG_STATUS_SENDING              = 1,
 /**
  *  Message sent successfully
  */
 TIM_MSG_STATUS_SEND_SUCC            = 2,
 /**
  *  Failed to send message
  */
 TIM_MSG_STATUS_SEND_FAIL            = 3,
 /**
  *  Message has been deleted
  */
 TIM_MSG_STATUS_HAS_DELETED          = 4,
 /**
  *  Message imported to local storage 
  */
 TIM_MSG_STATUS_LOCAL_STORED         = 5,
 /**
  *  Message has been recalled
  */
 TIM_MSG_STATUS_LOCAL_REVOKED        = 6,
 };

@interface TIMMessage : NSObject
/**
 *  Message status
 *
 *  @return TIMMessageStatus Message status
 */
-(TIMMessageStatus) status;
@end
```

### Whether a message was sent by oneself

Determine whether a message was sent by oneself through the message property `isSelf`. This is available when displayed on the interface.

```
@interface TIMMessage : NSObject
/**
 *  Sender?
 *
 *  @return TRUE: message sender. FALSE: message recipient.
 */
-(BOOL) isSelf;
@end
```

### Message sender and related profile

For group messages, use the `sender` method of `TIMMessage` to get the sender, or use the `GetSenderProfile` and `GetSenderGroupMemberProfile` methods to get the user’s profile and the profile of the group of which the user is a member. In versions earlier than 1.9, you can only get user profiles from online messages thrown by `onNewMessage`. In version 1.9 and higher, you can get profiles from messages obtained through `getMessage` (but not from local messages that were received before updating the version). For one-to-one messages, get the corresponding conversation through `getConversation` of `TIMMessage` and the other participant in the conversation through `getReceiver`.

> This field obtains the user profile and writes it to the message body when the message is sent. If there are user profile updates in the future, this field does not change unless new messages are generated.

```
@interface TIMMessage : NSObject
/**
 *  Get the sender
 *
 *  @return Sender identifier
 */
-(NSString *) sender;
/**
 *  Get the sender’s profile
 *
 *  If stored locally, the sender’s profile is returned synchronously in the profileCallBack callback. Otherwise, the SDK pulls the sender’s profile from the server and returns it asynchronously in the profileCallBack callback.
 *
 *  @param  profileCallBack Sender profile callback
 *
 */
- (void)getSenderProfile:(ProfileCallBack)profileCallBack;
/**
 *  Get the sender’s profile in the group (may be empty if the sender is the user)
 *
 *  @return The sender’s profile in the group. “nil” indicates that no profile is obtained or the message is not a group message. Currently, the only field that can be obtained is member. To get other fields, use TIMGroupManager+Ext.h -> getGroupMembers. 
 */
-(TIMGroupMemberInfo *) GetSenderGroupMemberProfile;
@end
```

### Message time

The message time can be obtained through the message property `timestamp`. This time is the server time, not the local time. During the creation of a message, the time is adjusted based on the server time, and will be changed to the accurate server time after the message is sent successfully.

```
@interface TIMMessage : NSObject
/**
 *  Timestamp of the current message
 *
 *  @return The timestamp
 */
-(NSDate*) timestamp;
@end
```

### Deleting messages

Currently, deleting messages on the server is not supported. You can only delete messages in local storage. Messages deleted with this method are not really deleted but only marked as deleted. Calling `getMessage` does not return the messages marked as deleted when the app is not uninstalled.

```
@interface TIMMessage : NSObject
/**
 *  Delete message. Note that this only changes the status.
 *
 *  @return TRUE Successful
 */
-(BOOL) remove;
@end
```

### Message IDs

There are two types of message IDs. One is `msgId` which is created when the message is generated. As this ID may conflict with messages generated by other users, a time dimension needs to be added. Messages generated within 10 minutes are considered distinguishable by `msgId`. The other is `uniqueId` which is generated after the message is sent successfully. IDs generated with this method are globally unique. These two methods both need to be used for judgment in a conversation.

```
@interface TIMMessage : NSObject
/**
 *  Message ID
 */
-(NSString *) msgId;
/**
 *  Get message’s uniqueId
 *
 *  @return uniqueId
 */
- (uint64_t) uniqueId;
@end
```

### Message custom fields

Developers can add custom fields to messages, such as custom integer and custom binary data. You can customize different effects based on these two fields. For example, you can determine whether an audio message has been played. Note that these custom fields are only stored locally and not synced to the server. You will not get them after switching to another client.

```
@interface TIMMessage : NSObject
/**
 *  Set custom integer. The default value is 0.
 *
 *  @param param Set parameter
 *
 *  @return TRUE Setting successful
 */
- (BOOL) setCustomInt:(int32_t) param;
/**
 *  Set custom data content. The default is "".
 *
 *  @param data Set parameter
 *
 *  @return TRUE Setting successful
 */
- (BOOL) setCustomData:(NSData*) data;
/**
 *  Get CustomInt
 *
 *  @return CustomInt
 */
- (int32_t) customInt;
/**
 *  Get CustomData
 *
 *  @return CustomData
 */
- (NSData*) customData;
@end
```

### Message priorities

Live streaming scenarios have Like and Red Packet features. Like messages have a lower priority than Red Packet messages. Use `TIMCustomElem` to define the message content and define the message priority when sending the message.

> Valid for group messages only

```
@interface TIMMessage : NSObject
/**
 *  Set message priority
 *
 *  @param priority Priority
 *
 *  @return TRUE Setting successful
 */
- (BOOL) setPriority:(TIMMessagePriority)priority;
/**
 *  Get the priority of the message
 *
 *  @return Priority
 */
- (TIMMessagePriority) getPriority;
@end
```

### Read receipts

For one-to-one messages, after the user enables the read receipts feature, read messages are synced to the client when the recipient calls `setReadMessage`.

**Enable read receipts feature:**

```
@interface TIMUserConfig : NSObject
/**
 *  After the read receipts feature is enabled, read receipts will be sent to the recipient when reporting read messages. This feature is only valid for one-to-one conversations.
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
@interface TIMManager : NSObject

/**
 *  Get conversation (TIMConversation*) list
 *
 *  @return Conversation list
 */
-(NSArray*) getConversationList;
@end
```

> The SDK will update the conversation list internally. After each update, a callback will be initiated via `TIMRefreshListener.onRefresh`. Please **call `getConversationList` after `onRefresh`** to update the conversation list.

**Example:**

```
NSArray * conversations = [[TIMManager sharedInstance] getConversationList];
NSLog(@"current session list : %@", [conversations description])
```

### Obtaining local messages in a conversation

The IM SDK stores messages locally, which can be obtained through `getLocalMessage` of `TIMConversation`. This is an asynchronous method, requiring callback to get message data. For one-to-one chats, offline messages can be obtained after login. For group chats, only the latest message is obtained after logging in with recent contacts roaming enabled and using `getMessage` to get roaming messages. For resource messages, such as image and audio messages, the message body only contains descriptive information. Additional APIs are needed to download data. For more information, please see [Parsing Messages](#.E6.B6.88.E6.81.AF.E8.A7.A3.E6.9E.90). After data is downloaded, the real data is not cached. The caller must cache the data.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Get messages in a local conversation
 *
 *  @param count The number of messages
 *  @param last  The last message
 *  @param succ Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 This operation was successful
 */
-(int) getLocalMessage: (int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Specifies the number of messages to get.
last | Specifies the last message obtained. If last passes nil, read from the latest message.
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

For group chats, the user gets roaming messages after login. For C2C chats, the user can get roaming messages after the roaming service is enabled. Roaming messages are obtained through the `getMessage` API of the IM SDK. If local messages are continuous, they are obtained directly. Otherwise, the missing messages will need to be obtained over the network. For resource messages, such as image and audio messages, the message body only contains descriptive information. Additional APIs are needed to download data. For more information, please see the section about parsing messages. After data is downloaded, the real data is not cached. The caller must cache the data.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Get messages in a conversation
 *
 *  @param count The number of messages
 *  @param last  The last message
 *  @param succ Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 This operation was successful
 */
-(int) getMessage: (int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Specifies the number of messages to get.
last | Specifies the last message obtained. If last passes nil, read from the latest message.
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

There are two methods to delete a conversation, each of which applies to different scenarios. One is to delete the conversation and save all messages and the other is to delete the conversation together with all its messages. Note that, for group chats, `getMessage` pulls roaming messages. Therefore, it is possible that messages are deleted successfully but roaming messages can still be pulled. If you do not need to pull roaming messages, you can use `getLocalMessage` to get messages, or use `getMessage` to pull a specified number of messages, such as a certain number of unread messages. `deleteConversation` deletes the conversation only and `deleteConversationAndMessages` deletes the conversation and all its messages.

**Prototype:**

```
@protocol TIMManager : NSObject
/**
 *  Delete conversation
 *
 *  @param type Type of the conversation. TIM_C2C indicates a one-to-one chat and TIM_GROUP indicates a group chat.
 *  @param receiver    User identifier or group ID
 *
 *  @return TRUE: deleted successfully. FALSE: failed to delete.
 */
-(BOOL) deleteConversation:(TIMConversationType)type receiver:(NSString*)receiver;
/**
 *  Delete a conversation and its messages
 *
 *  @param type Type of the conversation. TIM_C2C indicates a one-to-one chat and TIM_GROUP indicates a group chat.
 *  @param receiver    User identifier or group ID
 *
 *  @return TRUE: deleted successfully. FALSE: failed to delete.
 */
-(BOOL) deleteConversationAndMessages:(TIMConversationType)type receiver:(NSString*)receiver;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | Conversation type. For a one-to-one chat, enter TIM_C2C, and for a group chat, enter TIM_GROUP.
receiver | Conversation identifier. For a one-to-one chat, receiver is the other participant’s identifier. For a group chat, receiver is the group ID.

The following example deletes the C2C conversation with a friend named “iOS_002”. **Example:**

```
[[TIMManager sharedInstance] deleteConversation:TIM_C2C receiver:@"iOS_002"];
```

### Synchronously obtaining the last message of a conversation

The UI displays the last messages of the user on the recent contact list. A sync API `getLastMsg` was added in version 1.9 and later to allow users to get and display the last messages. **This feature requires a network connection**. Getting messages through this API does not filter out messages in the deleted status, which need to be blocked at the app level. To get multiple recent messages, call `getMessage`.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Get the last message from cache
 *  @return The last message (TIMMessage*)
 */
- (TIMMessage*)getLastMsg;

/**
 *  Get the roaming messages of a conversation
 *  @param count The number of messages
 *  @param last  The last message. If the value of last is nil, read from the latest message.
 *  @param succ Success callback
 *  @param fail  Failure callback
 *  @return 0: this operation is successful. 1: this operation failed.
 */
- (int)getMessage:(int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Number of messages to be obtained. The maximum number is 20. 


### Setting conversation drafts

The UI displays the user’s drafts on the recent contact list. An API to set and get drafts was added to version 2.2 and later to allow users to set conversation drafts. **Draft information is stored in a local database and can be obtained after login**.

**Prototype:**

```
@interface TIMMessageDraft : NSObject
/**
 *  Configure custom data
 *
 *  @param userData Custom data
 *
 *  @return 0 Successful
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
 *  @return 0       Successful
 *          1       Adding Elem is not allowed (file or audio exceeds two Elem)
 *          2       Unknown Elem
 */
-(int) addElem:(TIMElem*)elem;
/**
 *  Get the Elem for the corresponding index
 *
 *  @param index The index
 *
 *  @return Returns the corresponding Elem
 */
-(TIMElem*) getElem:(int)index;
/**
 *  Get the number of Elem
 *
 *  @return elem Quantity
 */
-(int) elemCount;
/**
 *  The message corresponding to the draft
 *
 *  @return The message
 */
-(TIMMessage*) transformToMessage;
/**
 *  Timestamp of the current message
 *
 *  @return The timestamp
 */
-(NSDate*) timestamp;
@end

@interface TIMConversation : NSObject
/**
 *  Set conversation draft
 *
 *  @param draft Draft content
 *
 *  @return 0 Successful
 */
-(int) setDraft:(TIMMessageDraft*)draft;
/**
 *  Get conversation draft
 *
 *  @return Draft content; returns nil if no draft
 */
-(TIMMessageDraft*) getDraft;
@end
```

**Parameter description:**

Parameter | Description
---|---
draft | The draft to be set. To clear a conversation draft, pass nil.

### Deleting local conversation messages

The IM SDK allows you to delete local conversation messages while keeping the conversation. **The IM SKD pulls the messages from the server again the next time it pulls messages for group conversations**.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Delete local conversation messages
 *
 *  @param succ Success callback
 *  @param fail  Failure callback
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

### Getting the message corresponding to a specified local ID

IM SDK 2.5.3 provides an API to get the message corresponding to a specified local ID.

**Prototype:**

```
/**
 * Message
 */
@interface TIMMessage : NSObject
/**
 *  Get message locator
 *
 *  @return locator
 */
- (TIMMessageLocator*) locator;
@end
@interface TIMConversation : NSObject
/**
 *  Get messages in a conversation
 *
 *  @param locators An array of message locators (TIMMessageLocator)
 *  @param succ Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 This operation was successful
 */
-(int) findMessages:(NSArray*)locators succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
locators | List of message locators (TIMMessageLocator).
succ | The success callback, which returns a list of messages.
fail | Failure callback

### Recalling messages

Starting with version 3.1.0, the IM SDK provides an API to recall messages. You can recall sent messages by calling the `revokeMessage` API of `TIMConversation`.

>
> - The API works for C2C and group conversations, but not onlineMessage, AVChatRoom, and BChatRoom.
> - By default, messages that were sent within the last 2 minutes can be recalled.

**Prototype:**

```
/**
 > - Message recalling works for C2C and group conversations, but not onlineMessage, AVChatRoom, and BChatRoom.
 *  @param msg   The recalled message
 *  @param succ Success callback
 *  @param fail  Failure callback
 *
 *  @return 0: this operation is successful. 1: this operation failed.
 */
- (int)revokeMessage:(TIMMessage*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
```

After a message is recalled, other members in the group or the other participant in the C2C conversation receives a message recall notification. In addition, the message recall notification listener `TIMMessageRevokeListener` notifies the upper-layer app. You can configure the message recall notification listener before login through `messageRevokeListener` of `TIMUserConfig`. For more information, see [User Configuration](https://intl.cloud.tencent.com/document/product/1047/34313).

**Prototype:**

```
@protocol TIMMessageRevokeListener <NSObject>
@optional
/**
 *  Message recall notification
 *
 *  @param locator The identifier of the recalled message
 */
- (void)onRevokeMessage:(TIMMessageLocator*)locator;

@end

```

After receiving a message recall notification, you can use the `respondsToLocator` method in `TIMMessage` to check whether the current message has been recalled by the sender, and then refresh the UI when necessary.

**Prototype:**

```
/**
 *  Whether the message corresponds to the locator
 *
 *  @param locator Message locator
 *
 *  @return YES: it is the correct message. NO: it is not the correct message.
 */
- (BOOL)respondsToLocator:(TIMMessageLocator*)locator;

```

## System Messages

In addition to C2C chat and group chat messages, system message is another conversation type (TIMConversationType). System messages are notification messages sent by the system backend for various events and cannot be sent by users. Currently, there are two types of system messages: relationship chain system messages and group system messages.

- **Relationship chain change system messages:** when the user has a friend request or is deleted by a contact, the system sends a change notification and the developer can refresh the friend list. For more information, please see Relationship chain change system notifications.

- **Group event messages:** when a group profile changes, such as changes to the group name or group members, the system sends a group event message in the group. The developer can choose whether to display the message or not and can refresh the group profile or group members at the same time. For more information, see Group management - group event messages.

- **Group system messages:** when a group member is removed from the group by a group admin or non-members are invited to the group, the system sends group system messages to users. For more information, see Group management - group system messages.
