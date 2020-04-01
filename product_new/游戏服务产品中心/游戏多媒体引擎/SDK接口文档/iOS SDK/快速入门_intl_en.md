This document describes how to get started with the GME APIs for iOS.

This document only describes the most important APIs to help you get started with GME. For more information on APIs, please see the [API documentation](https://intl.cloud.tencent.com/document/product/607/15210).


| Important API | Description |
| ------------- |:-------------:|
|InitEngine    				       	| Initializes GME 	|
|Poll    		| Triggers event callback	|
|SetDefaultAudienceAudioCategory 	| Sets background playback volume level |
|EnterRoom	 	| Enters room  		|
|EnableMic	 	| Enables mic 	|
|EnableSpeaker		| Enables speaker 	|

>
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- Authentication is required for room entry in GME. For more information, please see the authentication section in relevant documentation.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For GME callback messages, please see the callback message list.
- Operation on devices should be performed after successful room entry.
- For detailed error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173).


## Directions for Quick Access
### 1. Get a singleton
To use the voice feature, get the `ITMGContext` object first.

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
For more information on how to get parameters, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782).
This API requires the `SDKAppID` from the Tencent Cloud Console and the `openId` as parameters. The `openId` uniquely identifies a user with the rules stipulated by the application developer and must be unique in the application (currently, only INT64 is supported).
>The SDK must be initialized so that a room can be entered.
#### Function prototype

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId    	|NSString  | `AppId` from the Tencent Cloud Console 				|
| openId    		|NSString  | `OpenID` can only be in Int64 type (converted to string) with a value greater than 10,000, which is used to identify the user. |


#### Sample code 

```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```

### 3. Trigger event callback
Event callbacks can be triggered by periodically calling the `Poll` API in `update`.
#### Function prototype

```
ITMGContext -(void)Poll
```
#### Sample code
```
[[ITMGContext GetInstance] Poll];
```

### 4. Authenticate
Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    
To get authentication for voice messaging and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId    		|int   		| `AppId` from the Tencent Cloud Console.		|
| roomId    		|NSString  	| Room ID, which can contain up to 127 characters (for voice messaging and speech-to-text feature, enter `null`). 	|
| openID  		|NSString    	| User ID, which is the same as `openID` during initialization. 								|
| key    			|NSString    	| Permission key from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme). 					|


#### Sample code  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```
### 5. Enter a room
When a client enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.
#### Function prototype
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId 	|NSString		| Room ID, which can contain up to 127 characters |
| roomType 		|int			| Room audio type		|
| authBuffer    	|NSData    	| Authentication key						|

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 6. Receive callback for room entry
After the client enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function.

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```
Sample code for processing the callback:
#### Sample code  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
           	 // Receive the event of successful room entry
        }
            break;
	}
}
```

#### Data details
| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|


### 7. Enable/Disable the mic
This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.

#### Function prototype  
```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable the mic, set this parameter to `YES`; otherwise, set it to `NO`. |

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
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       | To disable the speaker, set this parameter to `NO`; otherwise, set it to `YES`. |

#### Sample code  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```


