This document provides an overview that makes it easy for Mac developers to debug and integrate the APIs for Game Multimedia Engine.


## How to Use
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)


This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://cloud.tencent.com/document/product/607/18739).


| Important API | Description |
| ------------- |:-------------:|
| InitEngine | Initializes GME |
|Poll    		| Triggers event callback	|
|EnterRoom	 	| Enters a room  		|
| EnableMic | Enables the microphone |
| EnableSpeaker | Enables the speaker |

>**Notes:**
- When a GME API is called successfully, QAVError.OK is returned, and the value is 0.
- GME APIs are called in the same thread.
- The request for entering a room via GME API should be authenticated. For more information, see authentication section in relevant documentation.
- The Poll API is called periodically for GME to trigger event callback.
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
For more information on how to obtain parameters, see [Integration Guide](https://cloud.tencent.com/document/product/607/10782).
This API should contain SdkAppId and openId. The SdkAppId is obtained from the Tencent Cloud console, and the openId is used to uniquely identify a user. The setting rule for openId can be customized by App developers, and this ID must be unique in an App (only INT64 is supported).
SDK must be initialized before a user can enter a room.
#### Function prototype

```
ITMGContext -(void)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | NSString | The SdkAppId obtained from the Tencent Cloud Console |
| openID | NSString | The OpenID only supports Int64 type(should be converted to String type for passing the api argument). It is used to identify the user and the value should be greater than 10000.|

#### Sample code 
```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```

### 3. Trigger event callback
Event callbacks can be triggered by periodically calling Poll in "update".
#### Function prototype

```
ITMGContext -(void)Poll
```
#### Sample code
```
[[ITMGContext GetInstance] Poll];
```

### 4. Enter a room
When you enter a room with the generated authentication information, the ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received as a callback.
- Microphone and speaker are not enabled by default after a user enters the room.
- The API InitEngine should be called before the API EnterRoom.

#### Function prototype
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | NSString | Room ID, which is limited to 127 characters |
| roomType | int | Audio type of the room |
| authBuffer | NSData | Authentication key |

For more information about room's audio types, see [Sound Quality Selection](https://cloud.tencent.com/document/product/607/18522).
  
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
            //Receive the event of entering the room successfully.
        }
            break;
     }
}
```

### 6. Enable/Disable the microphone
This API is used to enable/disable the microphone. Microphone and speaker are not enabled by default after a user enters a room.

#### Function prototype  
```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | boolean | To disable the microphone, set this parameter to NO, otherwise set it to YES. |

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
This API is used to generate AuthBuffer for encryption and authentication. For more information on deployment at backend, see [Authentication Key](https://cloud.tencent.com/document/product/607/12218). To obtain authentication for voice message, the room ID parameter must be set to null.    
A value of type NSData is returned by this API.

#### Function prototype
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId | int | The SdkAppId obtained from the Tencent Cloud Console |
| roomId | NSString  | Room ID, which is limited to 127 characters (The room ID parameter for voice message must be set to null) |
| openID | NSString   | User ID |
| key | NSString   | The key obtained from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme) |



#### Sample code  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```

