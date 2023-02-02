본문은 개발자가 Game Multimedia Engine(GME)용 API를 쉽게 디버그하고 통합할 수 있도록 해주는 사용자 정의 오디오 포워딩 라우팅 사용에 대한 자세한 설명을 제공합니다.


## 시나리오

**시나리오 설명: 두 명의 친구가 팀을 이루어 작은 팀을 구성한 후 그들은 세 명의 낯선 사람을 연결하여 큰 팀을 구성합니다. 그들은 큰 팀에서는 모든 구성원의 목소리를 듣고 싶어하지만 작은 팀에서는 서로만 이야기합니다.**

이는 맞춤형 오디오 라우팅 기능으로 달성할 수 있습니다. 여기서는 5명의 사용자가 모두 동일한 음성 대화방에 입장합니다. 그런 다음 오디오 라우팅 API 설정을 통해 플레이어가 2인 팀 또는 전체 방에서 음성을 듣도록 설정할 수 있을 뿐만 아니라 2인 팀 또는 전체 방에서 들리도록 설정할 수 있습니다.

오디오 규칙 거리: SetServerAudioRouteSendOperateType(AUDIO_ROUTE_SEND_WHITE_LIST,"2인 팀 list",ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE,"2인 팀 list");
이런 식으로 오디오는 목록에 있는 플레이어에게만 전송되고 3인 팀에서만 수신됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/819dd334b2ba7af9f2813f2d6f28aea2.png)


## 전제 조건

- **실시간 음성 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK에 액세스**: 핵심 API 및 음성 채팅 API에 대한 액세스를 포함합니다. 자세한 내용은 [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.
- GME의 음성 채팅 기능을 이용하여 성공적으로 음성방에 입장하였고, 마이크(EnableMic)와 스피커(EnableSpeaker)를 켰습니다.


## 오디오 포워딩 라우팅에 액세스


### 오디오 포워딩 규칙 설정

이 API는 오디오 포워딩 규칙을 설정하는 데 사용되며 성공적인 방 입장 콜백에서 호출됩니다. 호출된 후 이 API는 이 방 입장에 적용되며 방을 나간 후에는 유효하지 않습니다.


<dx-alert infotype="notice" title="주의">
음소거 기능인 AddBlackList는 로컬에서 적용되며 사용자 지정 오디오 라우팅보다 우선 순위가 높습니다. 예를 들어 A가 SetServerAudioRouteSendOperateType을 통해 B의 음성만 들리도록 설정했지만 AddBlackList를 호출하여 B를 음소거하면 A는 B의 음성을 듣지 않습니다.
</dx-alert>




#### API 프로토타입

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


#### 유형 설명

**ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE**

오디오 전송 규칙을 설정합니다. 전송 규칙에 따라 전송 효과가 달라집니다.

| 전송 유형                       | 효과                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_SEND_TO_ANYONE | 로컬 오디오는 백엔드로 업스트림으로 전송되지만 백엔드는 아무에게도 포워딩하지 않습니다. 이는 로컬을 음소거하는 것과 같습니다. 현재 OpenIDForSend 매개변수는 유효하지 않습니다. null만 입력하면 됩니다. |
| AUDIO_ROUTE_SEND_TO_ALL        | 로컬 오디오는 모든 사람에게 업스트림으로 전송됩니다. 현재 OpenIDForSend 매개변수는 유효하지 않습니다. null만 입력하면 됩니다. |
| AUDIO_ROUTE_SEND_BLACK_LIST    | 로컬 오디오는 업스트림으로 전송되며 매개변수 OpenIDForSend에서 제공하는 블록리스트에 있는 사람에게 포워딩되지 않습니다. |
| AUDIO_ROUTE_SEND_WHITE_LIST    | 로컬 오디오는 업스트림으로 전송되고 OpenIDForSend 매개변수에서 제공하는 얼로우리스트에 있는 사람에게 포워딩됩니다. |
>?
- 전달된 유형이 AUDIO_ROUTE_NOT_SEND_TO_ANYONE 또는 AUDIO_ROUTE_SEND_TO_ALL인 경우 OpenIDForSend 매개변수가 적용되지 않습니다. null만 입력하면 됩니다.
- 전달된 유형이 AUDIO_ROUTE_SEND_BLACK_LIST인 경우 OpenIDForSend 매개변수가 블록리스트가 됩니다. 최대 10명까지 지원됩니다.
- 전달된 유형이 AUDIO_ROUTE_SEND_WHITE_LIST인 경우 OpenIDForSend 매개변수가 얼로우리스트가 됩니다. 최대 10명까지 지원됩니다.
>

**ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE**

오디오 수신 규칙을 설정합니다. 다른 수신 규칙에 대해 다른 수신 효과가 있습니다.

| 수신 유형                         | 효과                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_RECV_FROM_ANYONE | 로컬은 오디오를 수신하지 않으며 이는 방에서 스피커를 비활성화하는 것과 같습니다. 현재 OpenIDForSend 매개변수는 유효하지 않습니다. null만 입력하면 됩니다. |
| AUDIO_ROUTE_RECV_FROM_ALL        | 로컬은 모든 사람의 오디오를 수신합니다. 현재 OpenIDForSend 매개변수는 유효하지 않습니다. null만 입력하면 됩니다. |
| AUDIO_ROUTE_RECV_BLACK_LIST      | 로컬은 블록리스트에 있는 사람들의 오디오를 수신하지 않습니다. 블록리스트는 OpenIDForSend 매개변수로 제공됩니다. |
| AUDIO_ROUTE_RECV_WHITE_LIST      | 로컬은 얼로우리스트에 있는 사람들의 오디오만 수신합니다. 얼로우리스트는 OpenIDForSend 매개변수로 제공됩니다. |

>?
- 전달된 유형이 AUDIO_ROUTE_NOT_RECV_FROM_ANYONE 또는 AUDIO_ROUTE_RECV_FROM_ALL인 경우 OpenIDForSend 매개변수가 적용되지 않습니다.
- 전달된 유형이 AUDIO_ROUTE_RECV_BLACK_LIST인 경우 OpenIDForSend 매개변수가 블록리스트가 됩니다. 최대 10명까지 지원됩니다.
- 전달된 유형이 AUDIO_ROUTE_RECV_WHITE_LIST인 경우 OpenIDForSend 매개변수가 얼로우리스트가 됩니다. 최대 10명까지 지원됩니다.
>

#### 반환값

반환된 QAV_OK 값은 호출이 성공했음을 나타냅니다.
- 콜백이 1004를 반환하면 매개변수가 잘못된 것입니다. 매개변수를 확인하십시오.
- 콜백이 1001을 반환하면 작업이 반복되었음을 의미합니다.
- 콜백이 1201을 반환하면 방이 존재하지 않는다는 의미입니다. 방 번호가 맞는지 확인하십시오.
콜백이 10001 및 1005를 반환하면 API를 다시 호출하십시오.

반환된 결과에 대한 자세한 설명은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/40105)를 참고하십시오. 


#### 예시 코드

 **실행 문**
```
@synthesize _sendListArray;
@synthesize _recvListArray;

int ret =  [[[ITMGContext GetInstance] GetRoom] SetServerAudioRouteSendOperateType:SendType  SendList:_sendListArray RecvOperateType:RecvType RecvList:_recvListArray];
if (ret != QAV_OK) {
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"audioroute 목록 업데이트 실패" message:[NSString stringWithFormat:@"에러 코드:%d",ret] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
    [alert show];
}
```
**콜백**
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString* log =[NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    switch (eventType) {
                case ITMG_MAIN_EVENT_TYPE_SERVER_AUDIO_ROUTE_EVENT:{
            {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"audioroute 업데이트" message:[NSString stringWithFormat:@"결과:%@,sub_type: %@ errorinof: %@", data[@"result"],data[@"sub_type"],data[@"error_info"]] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                              [alert show];
            }
        }
        default:
            break;
    }
}
```


### 오디오 포워딩 규칙 가져오기

이 API는 오디오 포워딩 규칙을 가져오는 데 사용됩니다. 호출된 후 API는 규칙을 반환하고 전달된 배열 매개변수는 해당 규칙의 openId를 반환합니다.

#### API 프로토타입

```
//iOS API
-(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE)GetCurrentSendAudioRoute:(NSMutableArray *) OpenIDForSend;
-(ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE)GetCurrentRecvAudioRoute:(NSMutableArray *)OpenIDForRecv;
//Unity API
public abstract ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE GetCurrentSendAudioRoute(List<string> OpenIDforSend);
public abstract ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE GetCurrentRecvAudioRoute(List<string> OpenIDforRecve);
```


#### 반환 규칙

**ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE**

| 전송 유형                       | 효과                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_SEND_TO_ANYONE | 로컬 오디오는 백엔드로 업스트림으로 전송되지만 백엔드는 아무에게도 포워딩하지 않습니다. 이는 로컬을 음소거하는 것과 같습니다. |
| AUDIO_ROUTE_SEND_TO_ALL        | 로컬 오디오는 모든 사람에게 업스트림으로 전송됩니다.                                   |
| AUDIO_ROUTE_SEND_BLACK_LIST    | 로컬 오디오는 업스트림으로 전송되며 블록리스트에 있는 사람에게 포워딩되지 않습니다.                             |
| AUDIO_ROUTE_SEND_WHITE_LIST    | 로컬 오디오는 업스트림으로 전송되어 얼로우리스트에 있는 사람들에게 포워딩됩니다.                             |
|AUDIO_ROUTE_RECV_INQUIRE_ERROR |가져오는 동안 오류가 발생했습니다. 로컬이 방에 들어왔는지, SDK가 초기화되었는지 확인하십시오.

**ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE**

| 수신 유형                         | 효과                                           |
| -------------------------------- | ---------------------------------------------- |
| AUDIO_ROUTE_NOT_RECV_FROM_ANYONE | 로컬은 오디오를 수신하지 않으며 이는 방에서 스피커를 비활성화하는 것과 같습니다. |
| AUDIO_ROUTE_RECV_FROM_ALL        | 로컬은 모든 사람의 오디오를 수신합니다.                           |
| AUDIO_ROUTE_RECV_BLACK_LIST      | 로컬은 블록리스트에 있는 사람들의 오디오를 수신하지 않습니다.                 |
| AUDIO_ROUTE_RECV_WHITE_LIST      | 로컬은 얼로우리스트에 있는 사람들의 오디오만 수신합니다.                 |
|AUDIO_ROUTE_RECV_INQUIRE_ERROR |가져오는 동안 오류가 발생했습니다. 로컬이 방에 들어왔는지, SDK가 초기화되었는지 확인하십시오.

>!`SetServerAudioRouteSendOperateType` API에서 `AUDIO_ROUTE_RECV_INQUIRE_ERROR`를 사용하지 마십시오.



