This document provides a detailed description of using custom audio forwarding routing that makes it easy for developers to debug and integrate the APIs for Game Multimedia Engine (GME).


## Use Cases

**Scenario description: after two friends team up to form a small team, they match three strangers to form a large team. They want to hear the voice of all members in the large team but only talk to each other in the small team.**

This can be achieved by the custom audio routing feature. Here, all five users enter the same voice chat room. Then, through the audio routing API settings, the players can be set to hear the voice in the two-player team or the entire room, as well as to be heard by the two-player team or the entire room.

Audio rule distance: SetServerAudioRouteSendOperateType(AUDIO_ROUTE_SEND_WHITE_LIST,"two-player team list",ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE,"two-player team list");
In this way, audio will be only sent to players in the list and will be only received from the three-player team.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/KH6i143_819dd334b2ba7af9f2813f2d6f28aea2.png)


## Prerequisites

- **You have activated the voice chat service**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- **You have integrated the GME SDK**, including core APIs and voice chat APIs. For more information, see [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), and [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545).
- You have successfully entered the voice room by using GME's voice chat feature and turned on the mic (EnableMic) and speaker (EnableSpeaker).


## Accessing Audio Forwarding Routing


### Setting audio forwarding rules

This API is used to set audio forwarding rules, and it is called in the callback of successful room entry. After being called, this API will take effect for this room entry and will be invalid after room exit.


<dx-alert infotype="notice" title="Note">
The mute feature `AddBlackList` takes effect locally and has a higher priority than custom audio routing. For example, if A sets to only hear B's voice through `SetServerAudioRouteSendOperateType` but calls `AddBlackList` to mute B, then A will not hear B's voice.
</dx-alert>




#### API prototype

<dx-codeblock>
::: Unity c#
public abstract class ITMGRoom{
	public abstract int SetServerAudioRouteSendOperateType(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE Sendtype, string[] OpenIDforSend, ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE Recvtype, string[] OpenIDforRecv);
}
:::
::: C++ c++
virtual int SetServerAudioRoute(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE SendType, const char OpenIDforSend[][21], int OpenIDforSendSize, ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE RecvType,const char OpenIDforRecv[][21], int OpenIDforRecvSize) = 0;
:::
::: Android  java
public abstract int SetServerAudioRoute(ITMGContext.ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE sendType, ArrayList<String> SendList, ITMGContext.ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE recvType, ArrayList<String> RecvList);
:::
::: iOS objectc
-(int)SetServerAudioRouteSendOperateType:(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE) Sendtype  SendList:(NSArray *)OpenIDForSend  RecvOperateType:(ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE) Recvtype RecvList:(NSArray *)OpenIDForRecv;
:::
</dx-codeblock>


#### Type descriptions

**ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE**

Set audio sending rules. There will be different sending effects for the different sending rules.

| Sending Types | Effects |
| ------------------------------ | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_SEND_TO_ANYONE | The local audio is sent upstream to the backend, but the backend does not forward to anyone, which is equivalent to mute the local. At this time, the parameter OpenIDForSend is invalid. You just need to enter null. |
| AUDIO_ROUTE_SEND_TO_ALL        | The local audio is sent upstream to everyone. At this time, the parameter OpenIDForSend is invalid. You just need to enter null. |
| AUDIO_ROUTE_SEND_BLACK_LIST    | The local audio is sent upstream and will not be forwarded to people in the blocklist, which is provided by the parameter OpenIDForSend. |
| AUDIO_ROUTE_SEND_WHITE_LIST    | The local audio is sent upstream and is forwarded to people in the allowlist, which is provided by the parameter OpenIDForSend. |
>?
>- If the passed type is AUDIO_ROUTE_NOT_SEND_TO_ANYONE or AUDIO_ROUTE_SEND_TO_ALL, then the parameter OpenIDForSend does not take effect. You just need to enter null.
>- If the passed type is AUDIO_ROUTE_SEND_BLACK_LIST, the parameter OpenIDForSend will be the blocklist. Up to 10 people are supported.
>- If the passed type is AUDIO_ROUTE_SEND_WHITE_LIST, the parameter OpenIDForSend will be the allowlist. Up to 10 people are supported.


**ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE**

Set audio receiving rules. There will be different receiving effects for the different receiving rules.

| Receiving Types | Effects |
| -------------------------------- | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_RECV_FROM_ANYONE | The local does not receive any audio, which is equivalent to disable the speaker in the room. At this time, the parameter OpenIDForSend is invalid. You just need to enter null. |
| AUDIO_ROUTE_RECV_FROM_ALL        | The local receives everyone’s audio. At this time, the parameter OpenIDForSend is invalid. You just need to enter null. |
| AUDIO_ROUTE_RECV_BLACK_LIST    | The local does not receive the audio of people in the blocklist. The blocklist is provided by the parameter OpenIDForSend. |
| AUDIO_ROUTE_RECV_WHITE_LIST    | The local will only receive the audio of people in the allowlist. The allowlist is provided by the parameter OpenIDForSend. |

>?
>- If the passed type is AUDIO_ROUTE_NOT_RECV_FROM_ANYONE or AUDIO_ROUTE_RECV_FROM_ALL, the parameter OpenIDForSend does not take effect.
>- If the passed type is AUDIO_ROUTE_RECV_BLACK_LIST, the parameter OpenIDForSend will be the blocklist. Up to 10 people are supported.
>- If the passed type is AUDIO_ROUTE_RECV_WHITE_LIST, the parameter OpenIDForSend will be the allowlist. Up to 10 people are supported.


#### Returned values

A returned value of QAV_OK indicates the call is successful.
- If the callback returns 1004, it means the parameter is incorrect. Please check the parameter.
- If the callback returns 1001, it means the operation is repeated.
- If the callback returns 1201, it means the room does not exist. Please check whether the room number is correct.
- If the callback returns 10001 and 1005, please call the API again.

For more explanations of the returned result, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).


#### Sample code

 **Executed statements**
```
@synthesize _sendListArray;
@synthesize _recvListArray;

int ret =  [[[ITMGContext GetInstance] GetRoom] SetServerAudioRouteSendOperateType:SendType  SendList:_sendListArray RecvOperateType:RecvType RecvList:_recvListArray];
if (ret != QAV_OK) {
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Failed to update audioroute list" message:[NSString stringWithFormat:@"error code:%d",ret] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
    [alert show];
}
```
**Callback**
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString* log =[NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    switch (eventType) {
                case ITMG_MAIN_EVENT_TYPE_SERVER_AUDIO_ROUTE_EVENT:{
            {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Update audioroute" message:[NSString stringWithFormat:@"Result:%@,sub_type: %@ errorinof: %@", data[@"result"],data[@"sub_type"],data[@"error_info"]] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                              [alert show];
            }
        }
        default:
            break;
    }
}
```


### Obtaining audio forwarding rules

This API is used to obtain audio forwarding rules. After being called, the API returns the rule, and the passed array parameter will return the openId of the corresponding rule.

#### API prototype

```
//iOS API
-(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE)GetCurrentSendAudioRoute:(NSMutableArray *) OpenIDForSend;
-(ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE)GetCurrentRecvAudioRoute:(NSMutableArray *)OpenIDForRecv;
//Unity API
public abstract ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE GetCurrentSendAudioRoute(List<string> OpenIDforSend);
public abstract ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE GetCurrentRecvAudioRoute(List<string> OpenIDforRecve);
```


#### Returning rules

**ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE**

| Sending Types | Effects |
| ------------------------------ | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_SEND_TO_ANYONE | The local audio is sent upstream to the backend, but the backend does not forward to anyone, which is equivalent to mute the local. |
| AUDIO_ROUTE_SEND_TO_ALL | The local audio is sent upstream to everyone. |
| AUDIO_ROUTE_SEND_BLACK_LIST | The local audio is sent upstream and will not be forwarded to people in the blocklist. |
| AUDIO_ROUTE_SEND_WHITE_LIST | The local audio is sent upstream and is forwarded to people in the allowlist. |
|AUDIO_ROUTE_RECV_INQUIRE_ERROR | An error occurred during obtaining. Check whether the local has entered the room and whether the SDK has been initialized. |

**ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE**

| Receiving Types | Effects |
| -------------------------------- | ---------------------------------------------- |
| AUDIO_ROUTE_NOT_RECV_FROM_ANYONE | The local does not receive any audio, which is equivalent to turn off the speaker in the room. |
| AUDIO_ROUTE_RECV_FROM_ALL | The local receives everyone’s audio. |
| AUDIO_ROUTE_RECV_BLACK_LIST | The local does not receive the audio of people in the blocklist. |
| AUDIO_ROUTE_RECV_WHITE_LIST | The local will only receive the audio of people in the allowlist. |
|AUDIO_ROUTE_RECV_INQUIRE_ERROR | An error occurred during obtaining. Check whether the local has entered the room and whether the SDK has been initialized. |

>!Please do not use `AUDIO_ROUTE_RECV_INQUIRE_ERROR` in the `SetServerAudioRouteSendOperateType` API.



