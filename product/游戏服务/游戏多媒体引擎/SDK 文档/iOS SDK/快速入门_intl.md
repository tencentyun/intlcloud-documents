This getting started article is trying to help iOS developers debug and access APIs for Tencent Cloud's Game Multimedia Engine (GME).


## How to Use
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)

This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15221).


| Important API | Description |
| ------------- |:-------------:|
| InitEngine | Initializes GME |
|Poll    		| Triggers event callback	|
| SetDefaultAudienceAudioCategory | Sets background playback |
|EnterRoom	 	| Enters a room  		|
| EnableMic | Enables the microphone |
| EnableSpeaker | Enables the speaker |

>**Notes:**
- After a GME API is called successfully, QAVError.OK will be returned with a value of 0.
- GME APIs are called in the same thread.
- The request for entering a room via GME API should be authenticated. For more information, see authentication section in relevant documentation.
- The Poll API should be called periodically to trigger event callback.
- See the callback message list for GME callback information.
- The operation on devices shall be carried out after successful entry into a room.


## Procedure for Quick Integration
### 1. Get a singleton
To use the voice feature, get the ITMGContext object first.

#### Function prototype 

```
ITMGContext ITMGDelegate <NSObject>
```
#### Sample code  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```



### 2. Initialize the SDK
For more information about getting parameters, see [Integration Guide](https://cloud.tencent.com/document/product/607/10782).

SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.

You must initialize the SDK before entering a room.

#### Function prototype

```
ITMGContext -(void)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | NSString | The SdkAppId obtained from the Tencent Cloud Console |
| openID | NSString | The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000.|

#### Sample code 
```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```

### 3. Trigger event callback
The Poll API should be called periodically to trigger event callback.
#### Function prototype

```
ITMGContext -(void)Poll
```
#### Sample code
```
[[ITMGContext GetInstance] Poll];
```

### 4. Enter a room
When you enter a room with the generated authentication credentials, you receive a callback indicating ITMG_MAIN_EVENT_TYPE_ENTER_ROOM.  
- By default, microphone and speaker will not be enabled after you enter the room.
- The API Init should be called before the API EnterRoom.

#### Function prototype
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | NSString | Room ID, which is limited to 127 characters |
| roomType | int | Audio type of the room |
| authBuffer | NSData | Authentication key |

For more information about room's audio types, see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Sample code  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 5. Callback for entering a room
A callback response is returned after a user enters the room, and the ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received.
Reference code for the callback setting:

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```
Reference code for the callback processing:
#### Sample code  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
            // Receive the event of entering the room successfully.
        }
            break;
     }
}
```

### 6. Enable/Disable the microphone
This API is used to enable/disable the microphone. By default, microphone and speaker will not be enabled after a user enters a room.

#### Function prototype  
```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | boolean | To enable the microphone, set this parameter to YES; otherwise set it to NO. |

#### Sample code   
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```


### 7. Enable/Disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | boolean | To disable the speaker, set this parameter to NO, otherwise set it to YES. |

#### Sample code
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```


## Authentication
### Authentication information
This API is used to generate AuthBuffer for encryption and authentication. For more information about deployment at the backend, see [GME Key](https://intl.cloud.tencent.com/document/product/607/12218). To obtain authentication for voice message, the room ID parameter must be set to null.
A value of type NSData is returned by this API.

#### Function prototype
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId identifier:(NSString*)identifier key:(NSString*)key;
+ @end
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId | int | The SdkAppId obtained from the Tencent Cloud Console |
| roomId | NSString | Room ID, which is limited to 127 characters (The room ID parameter for voice message must be set to null) |
| identifier | NSString | User ID |
| key | NSString | The key obtained from the Tencent Cloud [Console](https://intl.cloud.tencent.com/login)



#### Sample code  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```

