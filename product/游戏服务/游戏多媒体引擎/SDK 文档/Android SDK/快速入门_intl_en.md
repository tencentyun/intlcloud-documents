This document helps Android developers debug and integrate APIs for Tencent Cloud's Game Multimedia Engine (GME). 


## How to Use
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15210).


| Important API | Description |
| ------------- |-------------|
| Init | Initializes GME |
| Poll | Triggers event callback |
| EnterRoom | Enters a room |
| EnableMic | Enables the microphone |
| EnableSpeaker | Enables the speaker |

>**Notes:**
- Before using GME, please perform project configuration. Otherwise, the SDK will not take effect.
- After a GME API is called successfully, QAVError.OK will be returned with a value of 0.		
- GME APIs should be called in the same thread.
- Authentication is needed before entering a room. Look for the authentication section in the related documentation for more information.		
- The Poll API should be called periodically to trigger event callback.
- Look for the callback message list for callback information.
- Device related operations can only be done after entering a room.

## Integration Directions

### 1. Get a Singleton
To use the voice feature, get the ITMGContext object first.

#### Function Prototype 

```
public static ITMGContext GetInstance(Context context)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| context | Context | Application's context object |


#### Sample Code

```
import com.tencent.TMG.ITMGContext; 
TMGContext.getInstance(this);
```

### 2. Initialize the SDK
For more information on getting parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).

SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.

>You must initialize the SDK before entering a room.
#### Function prototype

```
ITMGContext public int Init(String sdkAppId, String openID)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | String | The SdkAppId obtained from the Tencent Cloud Console |
| openID | String | The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000. |

#### Sample Code 
```
ITMGContext.GetInstance(this).Init(sdkAppId, openId);
```

### 3. Trigger Event Callback
The Poll API should be called periodically to trigger event callback.
#### Function Prototype

```
ITMGContext int Poll()
```
#### Sample Code
```
ITMGContext.GetInstance(this).Poll();
```

### 4. Authentication Info
The AuthBuffer is generated for encryption and authentication. For relevant backend deployment, please see [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    
When obtaining authentication for offline voice, the room ID parameter must be null.

#### Function Prototype
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| appId    		|int   		| sdkAppId from Tencent Cloud Console		|
| roomId    		|String   		|room ID, up to 127 chars (the room ID of offline voice must be null)|
| openID    	|String 	|user identifier					|
| key    		|string 	|secret key from Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme)				|


####  Sample Code  
```
import com.tencent.av.sig.AuthBuffer;//Header file
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,identifier, key);
```


### 5. Enter a room
When you enter a room with the generated authentication credentials, you receive a callback indicating ITMG_MAIN_EVENT_TYPE_ENTER_ROOM.  
- By default, Microphone and speaker will not be enabled after you enter the room.
- The API Init should be called before the API EnterRoom.

#### Function Prototype
```
ITMGContext public abstract int  EnterRoom(String roomId, int roomType, byte[] authBuffer)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | String | room ID, which is limited to 127 characters |
| roomType | int | audio type of the room |
| authBuffer | byte[] | authentication key |

For more information on room's audio types, see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Sample Code  
```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

### 6. Callback for entering a room
The ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received after a user enters a room. The action of this event should be implemented in the OnEvent function.
Reference code for the callback setting:

```
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```
Reference code for the callback processing:
#### Sample code  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	 //Receive the event of entering the room successfully.
        }
	}
```

### 7. Enable/Disable the microphone
This API is used to enable/disable the microphone. By default, microphone and speaker will not be enabled after a user enters a room.

#### Function prototype  
```
ITMGContext public void EnableMic(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | boolean | To enable the microphone, set this parameter to true, otherwise set it to false. |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```


### 8. Enable/Disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype  
```
ITMGContext public void EnableSpeaker(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled |boolean | To disable the speaker, set this parameter to false, otherwise set it to true. |

#### Sample code  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

