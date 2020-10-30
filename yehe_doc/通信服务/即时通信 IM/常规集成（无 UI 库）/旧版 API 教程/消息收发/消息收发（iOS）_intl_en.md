## Sending Messages

### Sending common messages

#### Obtaining a conversation

Conversations are classified into conversations with an individual user and conversations with a group. To send or receive messages in a conversation, you need to first obtain the conversation by specifying the conversation type (C2C conversation or group conversation) and the peer's identifier (the peer's account or group ID). To obtain a conversation, call `getConversation`.
>! If the conversation is not stored locally, calls to `TIMConversation` APIs will fail. We recommend that you operate on the `TIMConversation` object after receiving the `TIMUserConfig` > `TIMRefreshListener` callback.

**Prototype:**

```
@interface TIMManager : NSObject
/**
 * Obtain a conversation.
 *
 *  @param type Conversation type. TIM_C2C indicates a one-to-one conversation, and TIM_GROUP indicates a group conversation.
 *  @param conversationId For a C2C conversation, use the peer's account identifier. For a group conversation, use the group ID.
 *
 *  @return Conversation object
 */
- (TIMConversation*)getConversation:(TIMConversationType)type receiver:(NSString*)conversationId;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | The conversation type. For a one-to-one conversation, enter TIM_C2C. For a group conversation, enter TIM_GROUP.
conversationId | The conversation identifier. For a one-to-one conversation, the receiver is the peer's account identifier. For a group conversation, the receiver is the group ID.

**Obtain the one-to-one conversation in which the other participant's `identifier` is "iOS-001":**

```
TIMConversation * c2c_conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS-001"];
```

**Obtain the group chat with a group whose group ID is "TGID1JYSZEAEQ":** 

```
TIMConversation * grp_conversation = [[TIMManager sharedInstance] getConversation:TIM_GROUP receiver:@"TGID1JYSZEAEQ"];
```

#### Sending messages

After `TIMConversation` is obtained using `TIMManager`, you can send messages and obtain cached messages for the conversation. For more information about messages in the IM SDK, see [Introduction to IM SDK Objects](https://intl.cloud.tencent.com/document/product/1047/34302). In the IM SDK, a message is a `TIMMessage` object. A `TIMMessage` can contain multiple `TIMElem` units, which can be text or images. This means a message can contain multiple text segments and images. Use the `sendMessage` method of `TIMConversation` to send messages using blocks or the protocol callback.

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
succ | The success callback.
fail | The failure callback.

### Sending text messages

A text message is defined by `TIMTextElem`.

```
@interface TIMTextElem : TIMElem {
    NSString * text;
}
```

**Example:**


>?
>- `text` passes the text message to send.
>- In the failure callback, `code` indicates the error code, and `err` indicates the error description. For more information, see [Error Codes](/doc/product/269/1671).

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

An image message is defined by `TIMImageElem`, which is a subclass of `TIMElem`. These messages can contain images. To send an image, add `TIMImageElem` to `TIMMessage` and send the image along with the message. When sending an image, you only need to set path, the image path. After the message is sent successfully, use `imageList` to obtain all image types. In addition, use `TIMUserConfig` > `TIMUploadProgressListener` to listen to the current upload progress.

**`TIMImageElem` prototype:**

```
/**
 * Store the path of the image to be sent, which must be a local path. See the following example.
 */
@interface TIMImageElem : TIMElem
/**
 * Path of the image to be sent
 */
@property(nonatomic,retain) NSString * path;
/**
 * This parameter saves all specifications of the image when it is received. Therefore, you can skip this parameter when sending a message.
 */
@property(nonatomic,retain) NSArray * imageList;
/**
 * Upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;

/**
 * Image compression level. For more information, see `TIM_IMAGE_COMPRESS_TYPE`, which applies only to the jpg format.
 */
@property(nonatomic,assign) TIM_IMAGE_COMPRESS_TYPE level;

/**
 * Image format. For more information, see `TIM_IMAGE_FORMAT`.
 */
@property(nonatomic,assign) TIM_IMAGE_FORMAT format;
@end
```

**Parameter description:**

| Parameter | Description |
|---|---|
| path | Stores the path of the image to be sent, which must be a local path. For more information, see the example of sending an image. |
| imageList | Saves all specifications of the image when it is received. Therefore, you can skip this parameter when sending a message. For more information, see the section about receiving image messages. |
| taskId | Can be used to query the upload progress when sending images. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress. |
| level | Images need to be compressed before being sent, and level represents the compression level. For more information, see `TIM_IMAGE_COMPRESS_TYPE`. |
| format | Image format. For more information, see `TIM_IMAGE_FORMAT.` |

The following example sends an image with the absolute path of `/xxx/imgPath.jpg`. **Example:**

```
/**
* Obtain the conversation with user iOS-001.
*/
TIMConversation * c2c_conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS-001"];
/**
* Construct a message.
*/
TIMMessage * msg = [[TIMMessage alloc] init];
/**
* Construct the image content.
*/
TIMImageElem * image_elem = [[TIMImageElem alloc] init];
image_elem.path = @"/xxx/imgPath.jpg";
/**
* Add the image content to the message container.
*/
[msg addElem:image_elem];
/**
* Send the message.
*/
[conversation sendMessage:msg succ:^(){  // Successful
       NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {  // Failed
       NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending emoji messages

An emoji message is defined by `TIMFaceElem`. The IM SDK does not provide an emoji package. Developers can use `index` to store the indexes of the emojis in their emoji packages. Alternatively, they can directly use `data` to store emoji binary data and the string `key`. Using both these methods, users can customize emojis. The SDK only passes them through.

```
@interface TIMFaceElem : TIMElem
/**
 * Emoji index, which can be customized by users
 */
@property(nonatomic, assign) int index;
/**
 *  Additional data, which can be customized by users
 */
@property(nonatomic,retain) NSData * data;
@end
```

**Parameter description:**

>? You only need to pass either `index` or `data`, and the IM SDK simply passes them through.

Parameter | Description
---|---
index | Emoji index, which is customized by the developer
data | Emoji binary data, which is customized by the developer

The following example sends an emoji with an index of 10. The developer must have an emoji package that contains the emoji with the index 10 at both sides. The emoji can also be identified by binary data using the `data` parameter. **Example:**

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

An audio message is defined by `TIMSoundElem`, where `data` stores audio data. For audio data, you need to provide the audio length in seconds.

>!
>- A message can contain only one audio `Elem`. If an attempt is made to add multiple audio `Elem` objects, the `AddElem` function returns error 1 and the audio `Elem` objects cannot be added.
>- Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one. Moreover, audio and file `Elem` objects may not be sorted in the order that they are sent. 

```
/**
 * Audio message Elem
 */
@interface TIMSoundElem : TIMElem
/**
 * Upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 * The path of the audio file to be uploaded. Use `getSound` to obtain the data when receiving the message.
 */
@property(nonatomic,strong) NSString * path;
/**
 * Store audio data.
 */
@property(nonatomic,retain) NSData * data;
/**
 * Internal ID of the audio message
 */
@property(nonatomic,strong) NSString * uuid;
/**
 * Audio data size
 */
@property(nonatomic,assign) int dataSize;
/**
 * Audio length in seconds, which should be set when the message is sent
 */
@property(nonatomic,assign) int second;

/**
 * Obtain the download URL of the audio file.
 *
 *  @param urlCallBack Callback for obtaining the URL
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save audio data to a file in the specified path.
 *
 * The `getSound` API downloads audio data from the server. To cache or store the data, use `uuid` as the `key` to store the audio data externally. The IM SDK does not store resource files.
 *
 *  @param path Audio storage path
 *  @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 * Save audio data to a file in the specified path (with progress callback).
 *
 * The `getSound` API downloads audio data from the server. To cache or store the data, use `uuid` as the `key` to store the audio data externally. The IM SDK does not store resource files.
 *
 *  @param path Audio storage path
 *  @param progress Audio download progress
 *  @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

| Parameter | Description |
|---|---|
| path | The file path of the audio to be uploaded. |
| uuid | The unique identifier generated after the audio is uploaded. The user can save the file based on this identifier. The IM SDK does not save resource data internally. |
| dataSize | The audio data size. |
| second | The audio data length. |

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

A location message is defined by `TIMLocationElem`, where `desc` stores the description information of the location, and `longitude` and `latitude` specify the longitude and latitude of the location, respectively.

```
@interface TIMLocationElem : TIMElem
/**
 * Description of the location, which is set when the message is sent
 */
@property(nonatomic,retain) NSString * desc;
/**
 * Latitude, which is set when the message is sent
 */
@property(nonatomic,assign) double latitude;
/**
 * Longitude, which is set when the message is sent
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

A file message is defined by `TIMFileElem`. You can also view additional information such as the file name.

>! Audio and file `Elem` objects are not always received in the order that they are added. We recommend that you determine and display `Elem` objects one by one.

```
/**
 * File message Elem
 */
@interface TIMFileElem : TIMElem
/**
 * Upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 * Path of the file to be uploaded. (If the path is specified, the file in the specified path will be uploaded first.)
 */
@property(nonatomic,strong) NSString * path;
/**
 * Internal ID of the file
 */
@property(nonatomic,strong) NSString * uuid;
/**
 * File size
 */
@property(nonatomic,assign) int fileSize;
/**
 * Display name of the file, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * filename;

/**
 * Obtain the download URL of the file.
 *
 *  @param urlCallBack Callback for obtaining the URL 
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 * Save file data to the file in the specified path.
 *
 * The `getFile` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
 *
 *  @param path File storage path
 *  @param succ Success callback, which returns data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getFile:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 * Save file data to a file in the specified path (with progress callback).
 *
 * The `getFile` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
 *
 *  @param path File storage path
 *  @param progress File download progress
 *  @param succ Success callback, which returns data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getFile:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | The file path.
data | The binary data of the file to be sent. You only need to set either `path` or `data`. We recommend that you set `path`.
filename | The file name. The IM SDK does not verify whether the file name is correct. It only passes the file name through.

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

Developers can customize the message format and content when built-in message types cannot meet their special needs. The IM SDK only passes through custom messages. If iOS APNs push notifications are required, a push text description to display needs to be provided. A custom message is defined by `TIMCustomElem`, where `data` stores the binary data of the message and developers define the data format. A message can contain multiple custom `Elem` objects, which can be mixed with other `Elem` objects. In offline push scenarios, `desc` of each `Elem` can be stacked and delivered.

```
/**
 * Custom message type
 */
@interface TIMCustomElem : TIMElem
/**
 * Custom message binary data
 */
@property(nonatomic,strong) NSData * data;
/**
 * Custom message description, which is used for display during offline push. This parameter has been deprecated. Therefore, you need to use `offlinePushInfo` of `TIMMessage` to configure the information.
 */
@property(nonatomic,strong) NSString * desc DEPRECATED_ATTRIBUTE;
/**
 * Extension field information in offline push. This parameter has been deprecated. Therefore, you need to use `offlinePushInfo` of `TIMMessage` to configure the information.
 */
@property(nonatomic,strong) NSString * ext DEPRECATED_ATTRIBUTE;
/**
 * Sound field information in offline push. This parameter has been deprecated. Therefore, you need to use `offlinePushInfo` of `TIMMessage` to configure the information.
 */
@property(nonatomic,strong) NSString * sound DEPRECATED_ATTRIBUTE;
@end
```

**Parameter description:**

Parameter | Description
---|---
data | The binary data of the custom message.

The following example adds an XML message, the display of which is determined by the developer.

**Example:**

```
// Custom XML message
NSString * xml = @"testTitlethis is custom msgtest msg body";
// Convert the message to NSData.
NSData *data = [xml dataUsingEncoding:NSUTF8StringEncoding];
TIMCustomElem * custom_elem = [[TIMCustomElem alloc] init];
[custom_elem setData:data];
TIMMessage * msg = [[TIMMessage alloc] init];
[msg addElem:custom_elem];
TIMConversation *conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"yahaha"];
[conversation sendMessage:msg succ:^(){
	NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### Sending short video messages

A short video message is defined by `TIMVideoElem`, which is a subclass of `TIMElem`. These messages can contain video snapshots and content. To send a short video, add `TIMVideoElem` to `TIMMessage` and send the video along with the message.

**`TIMVideoElem` prototype:**

```
/**
 * Short video message
 */
@interface TIMVideoElem : TIMElem
/**
 * Upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;

/**
 * Video file path, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * videoPath;

/**
 * Video information, which is set when the message is sent
 */
@property(nonatomic,strong) TIMVideo * video;

/**
 * Snapshot file path, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * snapshotPath;

/**
 * Video snapshot, which is set when the message is sent
 */
@property(nonatomic,strong) TIMSnapshot * snapshot;
@end
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
/**
* Obtain the conversation with user iOS-001.
*/
TIMConversation * c2c_conversation = [[TIMManager sharedInstance] getConversation:TIM_C2C receiver:@"iOS-001"];
/**
* Construct a message.
*/
TIMMessage * msg = [[TIMMessage alloc] init];
/**
* Construct the video content.
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
*  Add the short video content to the message container.
*/
[msg addElem:videoElem];
/**
* Send the message.
*/
[conversation sendMessage:msg succ:^(){  // Successful
       NSLog(@"SendMsg Succ");
}fail:^(int code, NSString * err) {  // Failed
       NSLog(@"SendMsg Failed:%d->%@", code, err);
}];
```

### 'Elem' order

Currently, file and audio `Elem` objects might not be transferred in the order that they are added. Other `Elem` objects are transferred in the order that they are added. However, we recommend that you do not rely heavily on the `Elem` object sequence when processing elements. Instead, you should process `Elem` objects by type to prevent process crashes when exceptions occur.

### Online messages

In some scenarios, you need to send online messages, which can only be received when a user is online. If the user is not online when the messages are sent, the user will not see them upon the next login. Online messages can be used for notifications. However, online messages will not be stored or included in the unread count. The API for sending online messages is similar to `sendMessage`.

>!
>- In versions earlier than 2.5.3, online messages apply only to C2C conversations.
>- In version 2.5.3 or later, online messages apply to group conversations, excluding audio-video chat rooms (AVChatRoom) and broadcasting chat rooms (BChatRoom).

```
@interface TIMConversation : NSObject
/**
 *  Send online message (the server does not save the message)
 *
 *  @param msg Message body
 *  @param succ Success callback
 *  @param Failure callback
 *
 *  @return 0 Success
 */
-(int) sendOnlineMessage: (TIMMessage*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

### Forwarding messages

In version 2.4.0 and later, you can use `copyFrom` of `TIMMessage` to copy the content of another message to the current message and resend it to other contacts.

**Prototype:**

```
/**
 * Message
 */
@interface TIMMessage : NSObject
/**
 * Copy properties in the message (Elem, priority, online, and offlinePushInfo).
 *
 *  @param srcMsg Source message
 *
 *  @return 0 Success
 */
- (int)copyFrom:(TIMMessage*)srcMsg;
@end
```

## Receiving Messages

To be notified of new messages, register the new message notification callback `TIMMessageListener`. If you have logged in, the IM SDK will use the `onNewMessage` callback to send new messages. Callback message content is passed using the `TIMMessage` parameter. With `TIMMessage`, you can get detailed information about messages and the corresponding conversations, such as text, audio data, and images. For more information, see [Parsing messages](#.E6.B6.88.E6.81.AF.E8.A7.A3.E6.9E.90).

>! Messages obtained using `onNewMessages` may not be unread messages. They can also be messages that have not been displayed locally. For example, when messages are already read on another client, messages of recent contacts can be pulled to obtain the last messages of conversations. If these last messages are not stored locally, they are sent using this method. After a user logs in, the IM SDK gets C2C offline messages. To avoid missing message notifications, the user needs to register new message notifications before login.
The `onNewMessage` callback is also used to send group system messages, relationship chain changes, and friend profile changes.


**Prototype:**

```
@protocol TIMMessageListener
@optional
/**
 * New message notification
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
msgs | The list of new messages. Note that multiple messages may be sent at the same time. Messages in the same conversation are sorted from old to new.

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

After receiving a message, use `getElem` to obtain all `Elem` nodes in `TIMMessage`.

**Prototype for traversing `Elem`:**

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

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMImageElem` type are image message nodes. To obtain all image specifications for display, use `imageList`.

** `TIMImageElem` prototype:**

```
**
 * Image message `Elem`
 */
@interface TIMImageElem : TIMElem
/**
 * Path of the image to be sent
 */
@property(nonatomic,retain) NSString * path;
/**
 * Save all specifications of the image, including the thumbnail, large image, and original image. Each specification is saved in a `TIMImage` object.
 */
@property(nonatomic,retain) NSArray * imageList;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | You do not need to consider this parameter when receiving messages. It has a value of nil.
imageList | Saves all specifications of the image, including the thumbnail, large image, and original image. Each specification is saved in a `TIMImage` object.

**`TIMImage`:**

After receiving a message, use `imageList` to obtain all image specifications, which are `TIMImage` objects. After obtaining `TIMImage`, reserve a place based on the image size and use `getImage` to download images of different specifications for display. **Developers need to cache the downloaded data. The IM SDK downloads data from the server each time it calls `getImage`. We recommend that you use the `uuid` of an image as the `key` to store images.**

**Prototype:**

```
@interface TIMImage : NSObject
/**
 * Image ID, which is the internal identifier. It can be used as the key for external caching.
 */
@property(nonatomic,strong) NSString * uuid;
/**
 * Image type
 */
@property(nonatomic,assign) TIM_IMAGE_TYPE type;
/**
 * Image size
 */
@property(nonatomic,assign) int size;
/**
 * Image width
 */
@property(nonatomic,assign) int width;
/**
 * Image height
 */
@property(nonatomic,assign) int height;
/**
 * Download URL
 */
@property(nonatomic, strong) NSString * url;

/**
 * Obtain the image.
 *
 * Developers need to cache the downloaded data. The IM SDK downloads data from the server each time it calls `getImage`. We recommend that you use the `uuid` of an image as the `key` to store images.
 *
 *  @param path Image storage path
 *  @param succ Success callback, which returns image data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getImage:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 * Obtain the image (with progress callback).
 *
 * Developers need to cache the downloaded data. The IM SDK downloads data from the server each time it calls `getImage`. We recommend that you use the `uuid` of an image as the `key` to store images.
 *
 *  @param path Image storage path
 *  @param progress Image download progress
 *  @param succ Success callback, which returns image data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getImage:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Image specifications:** each image has three specifications, including Original (original image), Large (large image), and Thumb (thumbnail).

- **Original image:** the original image sent by a user, whose dimensions and size remain unchanged.
- **Large image:** an image obtained after the original image is proportionally compressed. The height or width of the compressed image, whichever is smaller, is equal to 720 pixels.
- **Thumbnail:** an image obtained after the original image is proportionally compressed. The height or width of the compressed image, whichever is smaller, is equal to 198 pixels.

>?
>- If the size of the original image is less than 198 pixels, the original size is retained for the three specifications, and no compression is needed.
>- If the size of the original image falls between 198 and 720 pixels, the large image is the same as the original image, and no compression is needed.
>- When an image is displayed on a mobile phone, we recommend that the thumbnail be displayed first. When a user taps the thumbnail, the large image is downloaded. When the user taps the large image, the original image is downloaded. Alternatively, developers can choose to skip the large image so that the original image is downloaded when the user taps the thumbnail.
>- When an image is displayed on a tablet or PC, we recommend that the large image be displayed directly and the original image be downloaded when a user taps or clicks the large image due to the high resolution and availability of a Wi-Fi or wired network.

The following example fetches 10 messages from a conversation, obtains image messages, and downloads the relevant data. **Example:**

```
//The following uses the new message callback as an example to explain the process of parsing image messages.
// Path for saving the received images
NSString * pic_path = @"/xxx/imgPath.jpg";
[conversation getMessage:10 last:nil succ:^(NSArray * msgList) {  // Messages obtained successfully.
	// Traverse all messages.
	for (TIMMessage * msg in msgList) {
		// Traverse all elements in a message.
		for (int i = 0; i < msg.elemCount; ++i) {
           TIMElem *elem = [msg getElem:i];
           // Image element
			if ([elem isKindOfClass:[TIMImageElem class]]) {
				TIMImageElem * image_elem = (TIMImageElem * )elem;

				// Traverse all image specifications (Thumbnail, Large, and Original).
				NSArray * imgList = [image_elem imageList];
				for (TIMImage * image in imgList) {
					[image getImage:pic_path succ:^(){  // Received successfully.
						NSLog(@"SUCC: pic store to %@", pic_path);
					}fail:^(int code, NSString * err) {  // Failed to receive.
						NSLog(@"ERR: code=%d, err=%@", code, err);
					}];
				}
			}
		}
	}
} fail:^(int code, NSString * err) {  // Failed to receive messages.
	NSLog(@"Get Message Failed:%d->%@", code, err);
}];
```

### Receiving audio messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMElemType.Sound` type are audio message nodes. `path` indicates the audio message path specified when a message is created, and `path` is null when a message is received. When the message is received, reserve a place based on the audio length and use `getSound` to download audio resources. The `getSound` API downloads audio data from the server. To cache or store the data, use the `uuid` as the `key` to store the audio data externally. The IM SDK does not store resource files.

**Prototype:**

```
@interface TIMSoundElem : TIMElem
/**
 * Upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress.
 */
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
 * Set to audio data when sending the message, and use `getSound` to obtain data when receiving the message.
 */
@property(nonatomic,strong) NSString * path;
/**
 * Internal ID of the audio message
 */
@property(nonatomic,strong) NSString * uuid;
/**
 * Audio data size
 */
@property(nonatomic,assign) int dataSize;
/**
 * Audio length in seconds, which should be set when the message is sent
 */
@property(nonatomic,assign) int second;

/**
 * Obtain the download URL of the audio file.
 *
 *  @param urlCallBack Callback for obtaining the URL
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 *  Save audio data to a file in the specified path. 
 *
 * The `getSound` API downloads audio data from the server. To cache or store the data, use `uuid` as the `key` to store the audio data externally. The IM SDK does not store resource files.
 *
 *  @param path Audio storage path
 *  @param succ Success callback, which returns audio data
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 * Save audio data to a file in the specified path (with progress callback).
 *
 * The `getSound` API downloads audio data from the server. To cache or store the data, use `uuid` as the `key` to store the audio data externally. The IM SDK does not store resource files.
 * 
 *  @param path Audio storage path
 *  @param progress Audio download progress
 *  @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getSound:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Other parameters:**

Parameter | Description
---|---
path | Set to audio data when sending the message, and use `getSound` to obtain data when receiving the message.
uuid | The unique identifier used to facilitate caching.
dataSize | The audio file size.
second | The audio length in seconds.

**Audio message read status:** you can use [custom message fields](https://intl.cloud.tencent.com/document/product/1047/36400#.E6.B6.88.E6.81.AF.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5) to determine whether an audio message has been played. For example, a `customInt` value of 0 indicates that the audio has not been played, and a value 1 indicates that the audio has been played. After a user taps play, set `customInt` to 1.

```
@interface TIMMessage : NSObject
/**
 * Set the custom integer. The default value is 0.
 *
 *  @param param Set parameter
 *
 *  @return TRUE Set successfully.
 */
- (BOOL) setCustomInt:(int32_t) param;

/**
 * Obtain `CustomInt`.
 *
 *  @return CustomInt
 */
- (int32_t)customInt;

@end
```

### Receiving file messages

After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMFileElem` type are file message nodes. `path` is the file path entered when the message is created and is empty when GET is performed to send the message. You can choose to display only the file size and name when receiving the message and use `getFile` to download the file from the server each time. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.

**Prototype:**

```
@interface TIMFileElem : TIMElem
/**
* Upload task ID, which can be used to query the upload progress. This parameter has been deprecated. Therefore, use `TIMUploadProgressListener` instead to listen to the upload progress.
*/
@property(nonatomic,assign) uint32_t taskId DEPRECATED_ATTRIBUTE;
/**
* Path of the file to be uploaded. (If the path is specified, the file in the specified path will be uploaded first.)
*/
@property(nonatomic,strong) NSString * path;
/**
* Internal ID of the file
*/
@property(nonatomic,strong) NSString * uuid;
/**
* File size
*/
@property(nonatomic,assign) int fileSize;
/**
* Display name of the file, which is set when the message is sent
*/
@property(nonatomic,strong) NSString * filename;

/**
* Obtain the download URL of the file.
*
*  @param urlCallBack Callback for obtaining the URL
*/
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
* Save file data to the file in the specified path.
*
* The `getFile` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
*
*  @param path File storage path
*  @param succ Success callback, which returns data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getFile:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
* Save file data to a file in the specified path (with progress callback).
*
* The `getFile` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
*
*  @param path File storage path
*  @param progress File download progress
*  @param succ Success callback, which returns data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getFile:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
path | The path of the file to be uploaded.
uuid | The unique identifier used to facilitate caching.
fileSize | The file size.
filename | The display name of the file.

### Receiving short video messages
After receiving a message, use `getElem` to obtain all `Elem` nodes from `TIMMessage`. Nodes of the `TIMVideoElem` type are short video message nodes. Use the `TIMVideo` and `TIMSnapshot` objects to obtain the video and snapshot content. After receiving `TIMVideoElem`, download the video file and snapshot file through the APIs defined in the `video` and `snapshot` properties. To cache or store the data, use the `uuid` as the `key` to store the files externally. The IM SDK does not store resource files.
Prototype:

```
@interface TIMVideo : NSObject
/**
 * Internal ID of the video message, which does not need to be set
 */
@property(nonatomic,strong) NSString * uuid;
/**
 * Video file type, which is set when the message is sent
 */
@property(nonatomic,strong) NSString * type;
/**
 * Video size, which does not need to be set
 */
@property(nonatomic,assign) int size;
/**
 * Video length, which is set when the message is sent
 */
@property(nonatomic,assign) int duration;

/**
 * Obtain the download URL of the video.
 *
 *  @param urlCallBack Callback for obtaining the URL
 */
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
 * Obtain the video.
 *
 * The `getVideo` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
 *
 *  @param path Video storage path
 *  @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getVideo:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
 * Obtain the video (with progress callback).
 *
 * The `getVideo` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
 *
 *  @param path Video storage path
 *  @param progress Video download progress
 *  @param succ Success callback
 *  @param fail Failure callback, which returns the error code and error description
 */
- (void)getVideo:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;

@end

@interface TIMSnapshot : NSObject
/**
* Image ID, which does not need to be set
*/
@property(nonatomic,strong) NSString * uuid;
/**
* Snapshot file type, which is set when the message is sent
*/
@property(nonatomic,strong) NSString * type;
/**
* Image size, which does not need to be set
*/
@property(nonatomic,assign) int size;
/**
* Image width, which is set when the message is sent
*/
@property(nonatomic,assign) int width;
/**
* Image height, which is set when the message is sent
*/
@property(nonatomic,assign) int height;

/**
* Obtain the download URL of the snapshot.
*
*  @param urlCallBack Callback for obtaining the URL
*/
-(void)getUrl:(void (^)(NSString * url))urlCallBack;

/**
* Obtain the image.
*
* The `getImage` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
*
*  @param path Image storage path
*  @param succ Success callback, which returns image data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getImage:(NSString*)path succ:(TIMSucc)succ fail:(TIMFail)fail;

/**
* Obtain the image (with progress callback).
*
* The `getImage` API downloads file data from the server. To cache or store the data, use the `uuid` as the `key` to store the file externally. The IM SDK does not store resource files.
*
*  @param path Image storage path
*  @param progress Image download progress
*  @param succ Success callback, which returns image data
*  @param fail Failure callback, which returns the error code and error description
*/
- (void)getImage:(NSString*)path progress:(TIMProgress)progress succ:(TIMSucc)succ fail:(TIMFail)fail;
@end

// The following uses the new message callback as an example to explain the process of parsing short video messages.
// Path for saving the received video and snapshot
NSString * video_path = @"/xxx/video.mp4";
NSString * snapshot_path = @"/xxx/snapshot.jpg";
[conversation getMessage:10 last:nil succ:^(NSArray * msgList) {  // Messages obtained successfully.
   // Traverse all messages.
   for (TIMMessage * msg in msgList) {
     // Traverse all elements in a message.
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
} fail:^(int code, NSString * err) {  // Failed to receive messages.
    NSLog(@"Get Message Failed:%d->%@", code, err);
}];

```

## Message Properties 

### Checking whether a message has been read

Use `isRead` to check whether a message has been read, which is determined by the [Unread Count](https://intl.cloud.tencent.com/document/product/1047/34325#.E6.9C.AA.E8.AF.BB.E6.B6.88.E6.81.AF) on the app side.

```
@interface TIMMessage : NSObject
/**
 * Check whether a message has been read.
 *
 *  @return TRUE: read. FALSE: unread.
 */
-(BOOL) isReaded;
@end
```

### Message status

To obtain the status of the current message, such as sending, sent successfully, failed to send, or deleted, use `status`. For deleted messages, use the UI to determine the status and hide the messages accordingly.

```
/**
 * Message status
 */
 typedef NS_ENUM(NSInteger, TIMMessageStatus){
 /**
  * Sending
  */
 TIM_MSG_STATUS_SENDING              = 1,
 /**
  * Sent successfully
  */
 TIM_MSG_STATUS_SEND_SUCC            = 2,
 /**
  * Failed to send
  */
 TIM_MSG_STATUS_SEND_FAIL            = 3,
 /**
  * Deleted
  */
 TIM_MSG_STATUS_HAS_DELETED          = 4,
 /**
  * Imported to local storage 
  */
 TIM_MSG_STATUS_LOCAL_STORED         = 5,
 /**
  * Recalled
  */
 TIM_MSG_STATUS_LOCAL_REVOKED        = 6,
 };

@interface TIMMessage : NSObject
/**
 * Message status
 *
 *  @return TIMMessageStatus Message status
 */
-(TIMMessageStatus) status;
@end
```

### Checking whether a message was sent by oneself

To determine whether a message was sent by you yourself, use `isSelf`. This method is available when the message is displayed on the interface.

```
@interface TIMMessage : NSObject
/**
 * Check whether the user is the sender.
 *
 *  @return TRUE: message sender. FALSE: message recipient.
 */
-(BOOL) isSelf;
@end
```

### Message sender and related profile

For group messages, use the `sender` method of `TIMMessage` to obtain the sender, or use the `GetSenderProfile` and `GetSenderGroupMemberProfile` methods to obtain the sender profile and the profile of the sender's group. In versions earlier than 1.9, you can only obtain the sender profile from an online message received after `onNewMessage` is used. In version 1.9 and later, you can obtain the sender profile from any message received after `getMessage` is used (but not from local messages received before the version update). For a C2C conversation, use `getConversation` of `TIMMessage` to obtain the conversation and use `getReceiver` to obtain information on the peer in the conversation.

>! This field obtains the user profile and writes it to the message body when the message is sent. If the user profile is updated, this field will not change unless new messages are generated.

```
@interface TIMMessage : NSObject
/**
 * Obtain the sender.
 *
 *  @return Sender identifier
 */
-(NSString *) sender;
/**
 * Obtain the sender profile.
 *
 * If the sender profile is stored locally, this profile is returned synchronously in the `profileCallBack`. Otherwise, the SDK obtains the sender profile from the server and returns it asynchronously in the `profileCallBack`.
 *
 *  @param  profileCallBack Sender profile callback
 *
 */
- (void)getSenderProfile:(ProfileCallBack)profileCallBack;
/**
 * Obtain the sender profile in the group, which may be empty if the sender is the user.
 *
 *  @return Sender's profile in the group. "nil" indicates that no profile is obtained or the message is not a group message. Currently, only the `member` field can be obtained. To obtain other fields, use `TIMGroupManager+Ext.h` > `getGroupMembers`. 
 */
-(TIMGroupMemberInfo *) GetSenderGroupMemberProfile;
@end
```

### Message time

To obtain the message time, use `timestamp`. This time is the server time, not the local time. When you create a message, this time is calibrated based on the server time and will be changed to the accurate server time after the message is successfully sent.

```
@interface TIMMessage : NSObject
/**
 * Timestamp of the current message
 *
 *  @return Timestamp
 */
-(NSDate*) timestamp;
@end
```

### Message ID

There are two types of message IDs. One is `msgId`, which is created when a message is generated. If `msgId` is used, messages may conflict with messages generated by other users, and therefore a time dimension needs to be added. Messages generated within 10 minutes can be distinguished by `msgId`. The other is `uniqueId`, which is generated after a message is sent successfully and is globally unique. Both types of message IDs must be checked in the same conversation.

```
@interface TIMMessage : NSObject
/**
 * Message ID
 */
-(NSString *) msgId;
/**
 * Obtain the uniqueId of the message.
 *
 *  @return uniqueId
 */
- (uint64_t) uniqueId;
@end
```

### Custom message field

Developers can add custom fields to messages, such as the custom integer and custom binary data fields, and can customize different effects based on these two fields. For example, custom fields can be used to determine whether an audio message has been played. Note that these custom fields are only stored locally and not synchronized to the server. You will not obtain them after switching to another client.

```
@interface TIMMessage : NSObject
/**
 * Set the custom integer, which is 0 by default.
 *
 *  @param param Set parameter
 *
 *  @return TRUE Set successfully.
 */
- (BOOL) setCustomInt:(int32_t) param;
/**
 * Set the custom data content, which is "". by default.
 *
 *  @param data Set parameter
 *
 *  @return TRUE Set successfully.
 */
- (BOOL) setCustomData:(NSData*) data;
/**
 * Obtain CustomInt.
 *
 *  @return CustomInt
 */
- (int32_t) customInt;
/**
 * Obtain CustomData.
 *
 *  @return CustomData
 */
- (NSData*) customData;
@end
```

### Message priority

Livestreaming scenarios involve the like and red packet features. Like messages have a lower priority than red packet messages. You can use `TIMCustomElem` to define the message content, and define the message priority when sending a message.

>! Message priorities apply only to group messages.

```
@interface TIMMessage : NSObject
/**
 * Set the message priority.
 *
 *  @param priority Priority
 *
 *  @return TRUE Set successfully.
 */
- (BOOL) setPriority:(TIMMessagePriority)priority;
/**
 * Obtain the message priority.
 *
 *  @return Priority
 */
- (TIMMessagePriority) getPriority;
@end
```

### Read receipt

After the read receipt feature is enabled for C2C conversations, read messages are synchronized to the client when the recipient calls `setReadMessage`.

**Enable the read receipt feature:**

```
@interface TIMUserConfig : NSObject
/**
 * Enable the read receipt feature. Then, read receipts will be sent to the message sender when message read reports are reported. This feature applies only to C2C conversations.
 */
-(void) enableReadReceipt;
/**
 * Message read receipt listener
 */
@property(nonatomic,weak) id<TIMMessageReceiptListener> messageReceiptListener;
@end
```

**Prototype:**

```
@interface TIMMessage : NSObject

/**
 * Check whether the recipient has read the message. (This feature applies only to C2C messages.)
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
 * Obtain the conversation (TIMConversation*) list.
 *
 *  @return Conversation list
 */
-(NSArray*) getConversationList;
@end
```

>! The SDK continuously updates the conversation list internally. The update will be sent back to the caller using `TIMRefreshListener.onRefresh`. **Call `getConversationList` after `onRefresh`** to update the conversation list.

**Example:**

```
NSArray * conversations = [[TIMManager sharedInstance] getConversationList];
NSLog(@"current session list : %@", [conversations description])
```

### Obtaining local messages in a conversation

The IM SDK stores messages locally. To obtain these messages, use `getLocalMessage` of `TIMConversation`. This is an asynchronous method, and a callback needs to be set to obtain message data. For a C2C conversation, offline messages will be obtained automatically after login. For a group conversation, when recent contacts roaming is enabled, only the last message is obtained after login, and roaming messages can be obtained using `getMessage`. For resource messages such as image and audio messages, the message body only contains descriptive information, and additional APIs are required to download data. For more information, see [Parsing Messages](#.E6.B6.88.E6.81.AF.E8.A7.A3.E6.9E.90). The actual data downloaded is not cached, and must be cached by the caller.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 * Obtain messages in a local conversation.
 *
 *  @param count Number of messages
 *  @param last The last message
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Operation successful
 */
-(int) getLocalMessage: (int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Specifies the number of messages to obtain.
last | Specifies the last message obtained. If `last` passes `nil`, read from the latest message.
succ | The success callback.
fail | The failure callback.

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

### Obtaining roaming messages in a conversation

For group conversations, a user can obtain roaming messages after login. For C2C conversations, the user can obtain roaming messages after the roaming service is enabled. To obtain roaming messages, use `getMessage` of the IM SDK. If local messages are continuous, they are obtained directly, instead of over the network. If local messages are not continuous, missing messages need to be obtained over the network. For resource messages such as image and audio messages, the message body only contains descriptive information, and additional APIs are required to download data, which can participate in message parsing. The actual data downloaded is not cached, and must be cached by the caller.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 *  Obtain messages in a conversation.
 *
 *  @param count Number of messages
 *  @param last The last message
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Operation successful
 */
-(int) getMessage: (int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | Specifies the number of messages to obtain.
last | Specifies the last message obtained. If `last` passes `nil`, read from the latest message.
succ | The success callback.
fail | The failure callback.

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

While deleting a conversation, the IM SDK also deletes the local and roaming messages of this conversation, and the deleted conversation and messages cannot be recovered.

**Prototype:**

```
@protocol TIMManager : NSObject
/**
 *
 * When a conversation is deleted, the roaming messages of this conversation are also deleted from the local storage and backend.
 *
 *  @param type Conversation type. For more information, see the definition of `TIMConversationType` in `TIMComm.h`.
 *  @param conversationId Conversation ID
 *                        C2C: userID of the peer
 *                        GROUP: groupId of the group
 *                        SYSTEM: @""
 *
 *  @return YES: deleted successfully. NO: failed to delete.
 */
- (BOOL)deleteConversation:(TIMConversationType)type receiver:(NSString*)conversationId;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | The conversation type. For a C2C conversation, enter TIM_C2C. For a group conversation, enter TIM_GROUP.
conversationId | The conversation ID. For a C2C conversation, `receiver` is the user ID of the peer. For a group conversation, `receiver` is the group ID.

The following example deletes the C2C conversation with a friend named "iOS_002". **Example:**

```
[[TIMManager sharedInstance] deleteConversation:TIM_C2C receiver:@"iOS_002"];
```

### Synchronously obtaining the last message of a conversation

The UI displays the last messages from users in the recent contact list. In versions later than 1.9, the IM SDK provides the `getLastMsg` API to allow users to obtain and display the last messages. **This feature requires a network connection.** Messages obtained using this API contain deleted messages, which need to be blocked by the app. To obtain multiple recent messages, use `getMessage`.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 * Obtain the last message from the cache.
 *  @return Last message (TIMMessage*)
 */
- (TIMMessage*)getLastMsg;

/**
 * Obtain roaming messages of a conversation.
 *  @param count Number of messages
 *  @param last The last message. If the value of `last` is `nil`, read from the latest message.
 *  @param succ Success callback
 *  @param fail Failure callback
 *  @return 0: this operation is successful. 1: this operation failed.
 */
- (int)getMessage:(int)count last:(TIMMessage*)last succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
count | The number of messages to obtain. The maximum number is 20. 


### Setting conversation drafts

The UI displays the user’s drafts on the recent contact list. In version 2.2 or later, an API is added to allow users to set and obtain drafts. **Draft information is stored in a local database and can be obtained after login**.

**Prototype:**

```
@interface TIMMessageDraft : NSObject
/**
 * Set the custom data.
 *
 *  @param userData Custom data
 *
 *  @return 0 Success
 */
-(int) setUserData:(NSData*)userData;
/**
 * Obtain the custom data.
 *
 *  @return Custom data
 */
-(NSData*) getUserData;
/**
 * Add an `Elem`.
 *
 *  @param elem Structure of `Elem`
 *
 *  @return 0       Success
 *          1       Adding Elem is not allowed (more than two file or audio `Elem` objects).
 *          2       Unknown `Elem`
 */
-(int) addElem:(TIMElem*)elem;
/**
 *  Obtain `Elem` with the corresponding index.
 *
 *  @param index Index
 *
 *  @return The corresponding `Elem`
 */
-(TIMElem*) getElem:(int)index;
/**
 * Obtain the number of `Elem` objects.
 *
 *  @return elem Number of `Elem` objects
 */
-(int) elemCount;
/**
 * Message generated based on the draft
 *
 *  @return Message
 */
-(TIMMessage*) transformToMessage;
/**
 * Timestamp of the current message
 *
 *  @return Timestamp
 */
-(NSDate*) timestamp;
@end

@interface TIMConversation : NSObject
/**
 * Set the conversation draft.
 *
 *  @param draft Draft content
 *
 *  @return 0 Success
 */
-(int) setDraft:(TIMMessageDraft*)draft;
/**
 * Obtain the conversation draft.
 *
 *  @return Draft content. `nil` is returned if no draft is available.
 */
-(TIMMessageDraft*) getDraft;
@end
```

**Parameter description:**

Parameter | Description
---|---
draft | The draft to be set. To clear a conversation draft, pass `nil`.

### Deleting messages of a conversation

The IM SDK allows you to delete the local and roaming messages of a conversation, and deleted messages cannot be recovered.

**Prototype:**

```
@interface TIMConversation : NSObject
/**
 * Delete the local and roaming messages of the current conversation.
 *
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Operation successful
 */
- (int)deleteMessages:(NSArray<TIMMessage *>*)msgList succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
msgList | The list of messages to be deleted.
succ | The success callback.
fail | The failure callback.

### Obtaining the message corresponding to a specified local ID

IM SDK 2.5.3 provides an API to obtain the message corresponding to a specified local ID.

**Prototype:**

```
/**
 * Message
 */
@interface TIMMessage : NSObject
/**
 * Obtain the message locator.
 *
 *  @return locator
 */
- (TIMMessageLocator*) locator;
@end
@interface TIMConversation : NSObject
/**
 * Obtain messages in a conversation.
 *
 *  @param locators Message locator (TIMMessageLocator) array
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Operation successful
 */
-(int) findMessages:(NSArray*)locators succ:(TIMGetMsgSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
locators | The list of message locators (TIMMessageLocator).
succ | The success callback, which returns a list of messages.
fail | The failure callback.

### Recalling messages

Starting from version 3.1.0, the IM SDK provides an API to recall messages. To recall sent messages, call the `revokeMessage` API of `TIMConversation`.

>!
> - The API applies only to C2C and group conversations, and not to onlineMessages, AVChatRooms, or BChatRooms.
> - By default, only messages that were sent within the last 2 minutes can be recalled.

**Prototype:**

```
/**
 * Recall a message. (This API applies only to C2C and group conversations, and not to onlineMessages, AVChatRooms, or BChatRooms.)
 *  @param msg Message to be recalled
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0: this operation is successful. 1: this operation failed.
 */
- (int)revokeMessage:(TIMMessage*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
```

After a message is recalled, other members in the group or the peer in the C2C conversation will receive a message recall notification. In addition, the message recall notification listener `TIMMessageRevokeListener` notifies the upper-layer app. You can configure the message recall notification listener before login using `messageRevokeListener` of `TIMUserConfig`. For more information, see [User Configuration](https://intl.cloud.tencent.com/document/product/1047/34313).

**Prototype:**

```
@protocol TIMMessageRevokeListener <NSObject>
@optional
/**
 * Message recall notification
 *
 *  @param locator Locator of the recalled message
 */
- (void)onRevokeMessage:(TIMMessageLocator*)locator;

@end

```

After receiving a message recall notification, use the `respondsToLocator` method of `TIMMessage` to check whether the current message has been recalled by the sender and then refresh the UI when necessary.

**Prototype:**

```
/**
 * Check whether the message corresponds to the locator.
 *
 *  @param locator Message locator
 *
 *  @return YES: it is the correct message. NO: it is not the correct message.
 */
- (BOOL)respondsToLocator:(TIMMessageLocator*)locator;

```

## System Messages

In addition to C2C conversations and group conversations, system message is another conversation type (TIMConversationType). System messages are notifications that are sent by the system backend for various events. These messages cannot be sent by users. Currently, there are two types of system messages: relationship chain system messages and group system messages.

- **Relationship chain change messages:** the system sends a relationship chain change message when a user adds you as a friend or deletes you from his or her friend list. The developer can then update the friend list. For more information, see [System Notifications for Relationship Chain Changes (iOS%20SDK)](#.E5.85.B3.E7.B3.BB.E9.93.BE.E5.8F.98.E6.9B.B4.E7.B3.BB.E7.BB.9F.E9.80.9A.E7.9F.A5).

- **Group event messages:** when the group profile is modified, for example, due to a change to the group name or group members, the system sends a group event message in the group. The developer can choose whether to display the message, and at the same time refresh the group profile or group members. For more information, see [Group management - group event messages](https://intl.cloud.tencent.com/document/product/1047/36257#.E7.BE.A4.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF).

- **Group system messages:** when the group admin removes a member from the group or invites a user to join the group, the system sends a group system message to the user. For more information, see [Group management - group system messages](https://intl.cloud.tencent.com/document/product/1047/36257#.E7.BE.A4.E7.B3.BB.E7.BB.9F.E6.B6.88.E6.81.AF).

