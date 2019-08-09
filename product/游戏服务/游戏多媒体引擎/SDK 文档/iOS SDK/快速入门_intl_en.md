This document helps iOS developers debug and access APIs for Tencent CFor more informationloud's Game Multimedia Engine (GME).

This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15221).


|Important API     | Description|
| ------------- |:-------------:|
|InitEngine    				       	|Initializes GME 	|
|Poll    		|Triggers event callback	|
|SetDefaultAudienceAudioCategory 	|Sets background playback|
|EnterRoom	 	|Enters a room  		|
|EnableMic	 	|Enables the microphone 	|
|EnableSpeaker		|Enables the speaker 	|

>**Notes:**
- Configure the project before using GME, otherwise the SDK will not be valid.
- After a GME API is called successfully, QAVError.OK will be returned with a value of 0.
- GME APIs should be called in the same thread.
- Authentication is needed before entering a room. Refer to the authentication section in relevant documentation for more information.
- The Poll API should be called periodically to trigger event callback.
- Refer to the callback message list for callback information.
- Device related operations can only be done after entering a room.
- For error code details, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173)


## Quick Integration Directions
### 1. Get a singleton
This API is used to get the ITMGContext instance when using the voice feature.

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
For more information on getting parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.
You must initialize the SDK before entering a room.
#### Function prototype

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| sdkAppId    	|NSString  |The SdkAppId obtained from Tencent Cloud console				|
| openID    		|NSString  |The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000. |

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

### 4. Authentication information
AuthBuffer is generated for the purpose of encryption and authentication. For more information on the authentication data, refer to [GME Key](https://intl.cloud.tencent.com/document/product/607/12218).    
The room ID parameter for voice message must be set to "null".

#### Function prototype
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| appId    		|int   		|The SdkAppId obtained from the Tencent Cloud console		|
| roomId    		|NSString  	|Room ID; 127 characters maximum (The room ID parameter for voice message must be set to "null")	|
| openID  		|NSString    	|User ID								|
| key    			|NSString    	|The key obtained from the Tencent Cloud [Console](https://intl.cloud.tencent.com/login)					|


#### Sample code  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```
### 5. Enter a room
When you enter a room with the generated authentication credentials, you receive a callback indicating ITMG_MAIN_EVENT_TYPE_ENTER_ROOM. By default, microphone and speaker will not be enabled after you enter the room. If AV_OK is returned, it indicates the callback is successful.
#### Function prototype
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| roomId 	|NSString		|Room ID, maximum to 127 characters.|
| roomType 		|int			|Audio type of the room		|
| authBuffer    	|NSData    	|Authentication key						|

For the room audio type definition, refer to [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 6. Callback for entering a room
ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received after a user enters a room. The action of this event should be implemented in the OnEvent function.

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

#### Data detail
|Message     | Data         |Example|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
### 7. Enable/Disable the microphone
This API is used to enable/disable the microphone. By default, microphone and speaker will not be enabled after a user enters a room.

#### Function prototype  
```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |To enable the microphone, set this parameter to YES; otherwise, set it to NO|

#### Sample code  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```


### 8. Enable/Disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |To disable the speaker, set this parameter to NO. Otherwise set it to YES|

#### Sample code  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```



