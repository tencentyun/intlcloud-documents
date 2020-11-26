

This document describes how to manage GME chat rooms using Objective-C in iOS. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to request the required libraries.

## Project Configuration

Import the GME SDK, and then set “ImSDK.framework” to **Embed&Sign** as shown below.
- **XCode10:**
![](https://main.qcloudimg.com/raw/55bded873ffc3f5f7e95043c3e77aee3.png)
- **XCode11:**
![](https://main.qcloudimg.com/raw/dbb4d0fcebc2f71685969af3d9950bf1.png)

## ITMGRoomManager

GME chat room management can be used only when there are one or more members in a room, and only to modify the status of a room member.
All the callbacks for API responses are processed through `ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR`. For callback details, please see [Processing Callbacks](#test1).

```
@interface ITMGRoomManager :NSObject
```

## Capture Management APIs

The capture management APIs are used to manage the **microphone**, **audio upstreaming** and **capture device** separately. Managing the microphone is equivalent to managing both the audio upstreaming and capture device. The APIs are designed to avoid problems where the background music may stop playing due to the otherwise unified management of both the capture and playback devices.

### Microphone management

This API (EnableMic) is used to enable/disable the microphone for a user in a chat room.
Calling `EnableMic` is equivalent to calling both `EnableAudioSend` and `EnableAudioCaptureDevice`.

#### Function prototype
```
-(QAVResult)EnableMic:(BOOL)enable Receiver:(NSString *)receiverID;
```
| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | <li> YES: enables the microphone for a user<li>NO: disables the microphone for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_MIC_OP.

### Audio upstreaming management

This API (EnableAudioSend) is used to enable/disable audio upstreaming for a user in a chat room but will not affect the microphone capture.

#### Function prototype

```
-(QAVResult)EnableAudioSend:(BOOL)enable Receiver:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | --------------------------------------------------- |
| enable     | BOOL      | <li> YES: enables audio upstreaming for a user<li>NO: disables audio upstreaming for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP.

### Capture hardware management

This API (EnableAudioCaptureDevice) is used to enable/disable the audio capture device for a user in a chat room but will not affect audio upstreaming.

#### Function prototype

```
-(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      | <li>YES: enables the audio capture device for a user<li>NO: disables the audio capture device for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_CAPTURE_OP.

## Playback Management APIs

The playback management APIs are used to manage the **speaker**, **audio downstreaming** and **playback device** separately. Managing the speaker is equivalent to managing both the audio downstreaming and playback device. The APIs are designed to avoid problems where the background music may stop playing due to the otherwise unified management of both the capture and playback devices.

### Speaker management

This API (EnableSpeaker) is used to enable/disable the speaker for a user to hear the sound in a chat room.
Calling `EnableSpeaker` is equivalent to calling both `EnableAudioRecv` and `EnableAudioPlayDevice`.

#### Function prototype

```
-(QAVResult)EnableSpeaker:(BOOL)enable Receiver:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | <li>YES: enables the speaker for a user<li>NO: disables the speaker for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_SPEAKER_OP.

### Audio downstreaming management

This API (EnableAudioRecv) is used to enable/disable audio downstreaming for a user but will not affect the playback device.

#### Function prototype

```
-(QAVResult)EnableAudioRecv:(BOOL)enabled Receiver:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | <li> YES: enables audio downstreaming for a user<li>NO: disables audio downstreaming for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP.


### Playback device management

This API (EnableAudioPlayDevice) is used to enable/disable the audio playback device for a user but will not affect audio downstreaming.

#### Function prototype

```
-(QAVResult)EnableAudioPlayDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      | <li>YES: enables the audio playback device for a user<li>NO: disables the audio playback device for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_PLAY_OP.

## APIs for Obtaining the User Status

### Obtaining the microphone status

This API is used to obtain the microphone status for a user in a chat room.

#### Function prototype

```
-(QAVResult)GetMicState:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | ------------------- |
| receiverID | NSString* | Specifies the OpenId of the user                                    |


#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_GET_MIC_STATE.

### Obtaining the speaker status

This API is used to obtain the speaker status for a user in a chat room.

#### Function prototype

```
-(QAVResult)GetSpeakerState:(NSString *)receiverID;
```

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE.


## Other APIs

### API for removing users

This API is used to remove a user from a chat room.

```
-(QAVResult)KickOut:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | ------------------- |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_KICKOUT_OP.

### API for disabling the microphone/speaker for a user

Each user that enters a chat room can use their microphone and speaker by default. Calling this API will have the microphone and speaker disabled for a user until he or she exits the room.

```
-(QAVResult)ForbidUserOperation:(BOOL)enable Receiver:(NSString *)receiverID;
```

| Parameter | Type | Description |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | <li>YES: enables the microphone/speaker for a user<li>NO: disables the microphone/speaker for a user|
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGERMENT_FOBIN_OP.

<span id="test1"></span>
## Processing Callbacks

Like all the other GME callbacks, the chat room management callbacks are processed using `OnEvent` with an event named `ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR`. This event returns a parameter structure as shown below:

#### Callback parameters

| Parameter | Type | Description |
| ------------ | -------- | -------------------------------------------------------- |
| SenderID     | NSString | ID of the event sender. If it’s the same as your own OpenId, the sender is your client  |
| ReceiverID   | NSString | ID of the event receiver. If it’s the same as your own OpenId, the receiver is your client |
| OperateType  | NSNumber | Event type                                                 |
| Result   | NSNumber | Event result. `0` indicates success                                        |
| OperateValue | NSNumber | Callback details                                                |

#### OperateType

| Value | Event Type                              | Description                       |
| ---- | -------------------------------------- | -------------------------- |
| 0    | ITMG_ROOM_MANAGEMENT_CAPTURE_OP        | Callback for controlling the capture device       |
| 1    | ITMG_ROOM_MANAGEMENT_PLAY_OP           | Callback for controlling the playback device    |
| 2    | ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP     | Callback for controlling audio upstreaming      |
| 3    | ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP      | Callback for controlling audio downstreaming              |
| 4    | ITMG_ROOM_MANAGEMENT_MIC_OP            | Callback for controlling the microphone         |
| 5    | ITMG_ROOM_MANAGEMENT_PLAY_OP           | Callback for controlling the speaker             |
| 6    | ITMG_ROOM_MANAGEMENT_KICKOUT_OP        | Removes a user from a chat room     |
| 7    | ITMG_ROOM_MANAGEMENT_GET_MIC_STATE     | Obtains the microphone status         |
| 8    | ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE | Obtains the speaker status         |
| 9    | ITMG_ROOM_MANAGERMENT_FOBIN_OP         | Disables the microphone and speaker |

#### OperateValue

| Member      | Description                     |
| --------- | ------------------------ |
| boolValue | <li>0: disable<li>1: enable |


#### Sample code

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString* log =[NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    [self showLog:log];
    NSLog(@"====%@====",log);
    switch (eventType) {
		case ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR:
        {
            NSArray *operatorArr = @[@"capture",@"play back",@"upstream",@"downstream",@"capture and upstream",@"play back and downstream",@"remove user",@"mic status",@"speaker status",@"disable mic/speaker"];
			// _openId
            NSString *SenderID = [data objectForKey:@"SenderID"];
            NSString *ReceiverID = [data objectForKey:@"ReceiverID"];
            NSNumber *OperateType = [data objectForKey:@"OperateType"];
            NSNumber *Result = [data objectForKey:@"Result"];
            NSNumber *OperateValue = [data objectForKey:@"OperateValue"];
            
            // Request sent
            if ([SenderID isEqualToString:_openId]) {
                if (OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_MIC_STATE || OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE) {
                          NSString *alterString = [NSString stringWithFormat:@"%@ request sent to id:%@; result :%@",ReceiverID,operatorArr[OperateType.intValue],OperateValue.boolValue?@"enable":@"disable"];
                                             UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"room management operation" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                             [alert show];
                }
                else
                {
                    NSString *alterString = [NSString stringWithFormat:@"%@%@ request sent to id:%@; result :%@", ReceiverID,OperateValue.boolValue?@"enable":@"disable",operatorArr[OperateType.intValue],Result];
                               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"room management operation" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                               [alert show];
                }
           
                
            } 
			else if([ReceiverID isEqualToString:_openId] ){ // Request received
            	if (Result.intValue == 0) {
                	switch (OperateType.intValue) {
                        case ITMG_ROOM_MANAGEMENT_CAPTURE_OP:{
                            [_micSwitch setOn:OperateValue.boolValue animated:true];
                        }
                            break;
                        case ITMG_ROOM_MANAGEMENT_PLAY_OP:{
                            [_speakerSwitch setOn:OperateValue.boolValue animated:true];
                            }
                            break;
                        case ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP:{
                            [_sendSwitch setOn:OperateValue.boolValue animated:true];
                        }
                            break;
                        case ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP:{
                            [_recvSwitch setOn:OperateValue.boolValue animated:true];
                        }
                            break;
                        case ITMG_ROOM_MANAGEMENT_MIC_OP:{
                        [_micSwitch setOn:OperateValue.boolValue animated:true];
                        [_sendSwitch setOn:OperateValue.boolValue animated:true];
                        }
                            break;
                        case ITMG_ROOM_MANAGEMENT_SPEAKER_OP:{
                        [_speakerSwitch setOn:OperateValue.boolValue animated:true];
                        [_recvSwitch setOn:OperateValue.boolValue animated:true];
                            
                        }
                            break;
                        default:
                            break;
                    }
                
                if (OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_MIC_STATE || OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE) {
                        NSString *alterString = [NSString stringWithFormat:@"%@ request received from id:%@; result :%@",SenderID,operatorArr[OperateType.intValue],OperateValue.boolValue?@"enable":@"disable"];
                                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"room management operation" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                [alert show];
                    }
                else{
                    	NSString *alterString = [NSString stringWithFormat:@"%@%@ request received from id:%@; result :%@",SenderID,OperateValue.boolValue?@"enable":@"disable",operatorArr[OperateType.intValue],Result];
                              UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"room management operation" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                              [alert show];
                	}
            	}
			}
    	}
        break;
}
```
