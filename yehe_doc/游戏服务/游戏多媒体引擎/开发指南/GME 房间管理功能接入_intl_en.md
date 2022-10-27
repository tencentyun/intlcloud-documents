This document describes use cases of the room management feature and how to quickly connect to the feature.

## Overview
You can use client room management APIs to manage room members and member mic-on/off status easily.


## Use Cases

For example, the host in Werewolf can use `EnableMic` to control other players to enable their mic to speak. If a player is dead and doesn't need to listen to room members or speak with a mic, the host use the `ForbidUserOperation` API to forbid the player from manipulating devices.


## Prerequisites
- **Activated the real-time voice service**: See [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- **Accessed to GME SDK**: includes access of core APIs and Voice Chat APIs. For details, please see [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858), [Unity SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/44544), [Unreal SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/44545).


<dx-alert infotype="explain" title="">
This feature is not supported by the SDK for HTML5.
</dx-alert>



## Connection Process
### Class name: ITMGRoomManager

GME chat room management can be used only when there are one or more members in a room, and only to modify the status of a room member.
All the callbacks for API responses are processed through `ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR`. For callback details, please see [Processing Callbacks](#test1).

### API list


| Type | APIs | 
|---------|---------|
| Capturing control APIs |EnableMic, EnableAudioCaptureDevice, and EnableAudioSend | 
| Playback control APIs | EnableSpeaker, EnableAudioPlayDevice, and EnableAudioRecv | 
| Device status acquisition APIs |GetMicState and GetSpeakerState | 
| Sensitive APIs |ForbidUserOperation | 

## Capture Management APIs

The capture management APIs are used to manage the **microphone**, **audio upstreaming** and **capture device** separately. Managing the microphone is equivalent to managing both the audio upstreaming and capture device. The APIs are designed to avoid problems where the background music may stop playing due to the otherwise unified management of both the capture and playback devices.

### Mic management

This API (EnableMic) is used to enable/disable the microphone for a user in a chat room.
Calling `EnableMic` is equivalent to calling both `EnableAudioSend` and `EnableAudioCaptureDevice`.

#### Function prototype

<dx-codeblock>
::: Android  java
public abstract int EnableMic(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableMic:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | YES: Enable the mic for a user; NO: Disable the mic for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |


#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_MIC_OP.

### Audio upstreaming management

This API (EnableAudioSend) is used to enable/disable audio upstreaming for a user in a chat room but will not affect the microphone capture.

#### Function prototype


<dx-codeblock>
::: Android  java
public abstract int EnableAudioSend(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioSend:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| Parameter | Type | Description |
| ---------- | --------- | --------------------------------------------------- |
| enable     | BOOL      |YES: Enable upstreaming for a user; NO: Disable upstreaming for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP.

### Capturing device management

This API (EnableAudioCaptureDevice) is used to enable/disable the audio capture device for a user in a chat room but will not affect audio upstreaming.

#### Function prototype

<dx-codeblock>
::: Android  java
public abstract int EnableAudioCaptureDevice(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>

| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      |YES: Enable the audio capturing device for a user; NO: Disable the audio capturing device for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_CAPTURE_OP.

## Playback Management APIs

The playback management APIs are used to manage the **speaker**, **audio downstreaming** and **playback device** separately. Managing the speaker is equivalent to managing both the audio downstreaming and playback device. The APIs are designed to avoid problems where the background music may stop playing due to the otherwise unified management of both the capture and playback devices.

### Speaker management

This API (EnableSpeaker) is used to enable/disable the speaker for a user to hear the sound in a chat room.
Calling `EnableSpeaker` is equivalent to calling both `EnableAudioRecv` and `EnableAudioPlayDevice`.

#### Function prototype

<dx-codeblock>
::: Android  java
public abstract int EnableSpeaker(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableSpeaker:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | YES: Enable the speaker for a user; NO: Disable the speaker for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_SPEAKER_OP.

### Audio downstreaming management

This API (EnableAudioRecv) is used to enable/disable audio downstreaming for a user but will not affect the playback device.

#### Function prototype

<dx-codeblock>
::: Android  java
public abstract int EnableAudioRecv(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioRecv:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| Parameter | Type | Description |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | YES: Enable audio downstreaming for a user; NO: Disable audio downstreaming for a user |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP.


### Playback device management

This API (EnableAudioPlayDevice) is used to enable/disable the audio playback device for a user but will not affect audio downstreaming.

#### Function prototype

<dx-codeblock>
::: Android  java
public abstract int EnableAudioPlayDevice(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioPlayDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| Parameter | Type | Description |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      |YES: Enable the audio playback device for a user; NO: Disable the audio playback device for a user  |
| receiverID | NSString* | Specifies the OpenId of the user                                    |

#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_PLAY_OP.

## APIs for Obtaining the User Status

### Getting the mic status

This API is used to obtain the microphone status for a user in a chat room.

#### Function prototype

<dx-codeblock>
::: Android  java
public abstract int GetMicState(String receiverID);
:::
::: iOS c++
-(QAVResult)GetMicState:(NSString *)receiverID;
:::
</dx-codeblock>


| Parameter | Type | Description |
| ---------- | --------- | ------------------- |
| receiverID | NSString* | Specifies the OpenId of the user                                    |


#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_GET_MIC_STATE.

### Getting the speaker status

This API is used to obtain the speaker status for a user in a chat room.

#### Function prototype

<dx-codeblock>
::: Android  java
public abstract int GetSpeakerState(String receiverID);
:::
::: iOS c++
-(QAVResult)GetSpeakerState:(NSString *)receiverID;
:::
</dx-codeblock>


#### Callback

The callback parameter is ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE.


### API for disabling the mic/speaker for a user

Each user that enters a chat room can use their microphone and speaker by default. Calling this API will have the microphone and speaker disabled for a user until he or she exits the room.

<dx-codeblock>
::: Android  java
public  abstract int ForbidUserOperation(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)ForbidUserOperation:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>

| Parameter | Type | Description |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | YES: Disable the devices for a user; NO: Enable the devices for a user |
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
| 6    | ITMG_ROOM_MANAGEMENT_GET_MIC_STATE     | Obtains the microphone status         |
| 7    | ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE | Obtains the speaker status         |
| 8    | ITMG_ROOM_MANAGERMENT_FOBIN_OP         | Disables the microphone and speaker |

#### OperateValue

| Member      | Description                     |
| --------- | ------------------------ |
| boolValue |  0: Disable; 1: Enable |


#### Sample code


<dx-codeblock>
::: Android  java
 public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
 if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR== type) {

            ArrayList<String> operatorArr = new ArrayList<String>();
            operatorArr.add("Capture");
            operatorArr.add("Play back");
            operatorArr.add("Upstream");
            operatorArr.add("Downstream");
            operatorArr.add("Capture and upstream");
            operatorArr.add("Play back and downstream");
            operatorArr.add("Mic status");
            operatorArr.add("Speaker status");
            operatorArr.add("Disable the mic/speaker");

            String SenderID =  data.getStringExtra("SenderID");
            String ReceiverID = data.getStringExtra("ReceiverID");
            int OperateType = data.getIntExtra("OperateType",-1000);

            int Result =data.getIntExtra("Result",-1000);
            boolean OperateValue = data.getBooleanExtra("OperateValue",false);
            if (OperateType == -1000 ||Result == -1000) {
                return;
            }
            if (SenderID.equals(identifier)) {
                if (OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_GET_MIC_STATE || OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE) {
                    Toast.makeText(getActivity(), String.format("Sent ID %s the result of the %s operation: %s", ReceiverID, operatorArr.get(OperateType), OperateValue ? "on" : "off"), Toast.LENGTH_LONG).show();
                } else  {
                    Toast.makeText(getActivity(), String.format("Sent ID %s the result of the %s%s operation: %d", ReceiverID, operatorArr.get(OperateType), OperateValue ? "on" : "off", Result), Toast.LENGTH_LONG).show();
                }

            } else if (ReceiverID.equals(identifier)||ReceiverID.equals("ALL")) {
                if (Result == 0) {
                    switch (OperateType) {
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_CAPTURE_OP:
                        {
                            if (!OperateValue) {
                                mSwitchCapture.setChecked(OperateValue);
                            } else  {
                                AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  // Create an object
                                dialog.setTitle("Whether to enable device capturing");
                                dialog.setMessage("");
                                dialog.setCancelable(false);
                                dialog.setPositiveButton("On", new DialogInterface.OnClickListener() {
                                    // Set the click event of the **OK** button
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        mSwitchCapture.setChecked(true);
                                        ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableAudioCaptureDevice(true);
                                    }
                                });
                                dialog.setNegativeButton("Off", new DialogInterface.OnClickListener() {
                                    // Set the click event of the **Cancel** button
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                    }
                                });
                                dialog.show();
                            }

                        }
                            break;
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_PLAY_OP:
                        {
                            mSwitchPlayDevice.setChecked(OperateValue);
                        }
                            break;
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP:
                        {
                            if (!OperateValue) {
                                mSwitchSend.setChecked(OperateValue);
                            } else  {
                                AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  // Create an object
                                dialog.setTitle("Whether to enable upstreaming");
                                dialog.setMessage("");
                                dialog.setCancelable(false);
                                dialog.setPositiveButton("On", new DialogInterface.OnClickListener() {
                                    // Set the click event of the **OK** button
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        mSwitchSend.setChecked(true);
                                        ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableAudioSend(true);
                                    }
                                });
                                dialog.setNegativeButton("Off", new DialogInterface.OnClickListener() {
                                    // Set the click event of the **Cancel** button
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                    }
                                });
                                dialog.show();
                            }
                        }
                            break;
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP:
                         {
                             mSwitchRecv.setChecked(OperateValue);
                        }
                            break;
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_MIC_OP:
                         {
                             if (!OperateValue) {
                                 mSwitchCapture.setChecked(OperateValue);
                                 mSwitchSend.setChecked(OperateValue);
                             }  else  {
                                 AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  // Create an object
                                 dialog.setTitle("Whether to enable capturing and upstreaming");
                                 dialog.setMessage("");
                                 dialog.setCancelable(false);
                                 dialog.setPositiveButton("On", new DialogInterface.OnClickListener() {
                                     // Set the click event of the **OK** button
                                     @Override
                                     public void onClick(DialogInterface dialog, int which) {
                                         mSwitchCapture.setChecked(true);
                                         mSwitchSend.setChecked(true);
                                         ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableMic(true);
                                     }
                                 });
                                 dialog.setNegativeButton("Off", new DialogInterface.OnClickListener() {
                                     // Set the click event of the **Cancel** button
                                     @Override
                                     public void onClick(DialogInterface dialog, int which) {
                                     }
                                 });
                                 dialog.show();
                             }
                          }
                            break;
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_SPEAKER_OP:
                        {
                            mSwitchPlayDevice.setChecked(OperateValue);
                            mSwitchRecv.setChecked(OperateValue);
                        }
                            break;

                    }
                }
                if (OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_GET_MIC_STATE || OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE)
                {
                    Toast.makeText(getActivity(), String.format("Received from the ID %s the result of the %s operation: %s",SenderID,operatorArr.get(OperateType),OperateValue?"on":"off"), Toast.LENGTH_LONG).show();
                }
                else if (OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_SPEAKER_OP || OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP|| OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_PLAY_OP|| OperateType == ITMGContext.ITMG_ROOM_MANAGERMENT_FOBIN_OP){
                    Toast.makeText(getActivity(), String.format("Received from ID %s the result of the %s%s operation: %d",SenderID,operatorArr.get(OperateType),OperateValue?"on":"off",Result), Toast.LENGTH_LONG).show();
                } else if (OperateValue == false) {
                    Toast.makeText(getActivity(), String.format("Received from ID %s the result of the %s%s operation: %d",SenderID,operatorArr.get(OperateType),OperateValue?"on":"off",Result), Toast.LENGTH_LONG).show();
                }
            }
 }
:::
::: iOS c++
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
:::
</dx-codeblock>

