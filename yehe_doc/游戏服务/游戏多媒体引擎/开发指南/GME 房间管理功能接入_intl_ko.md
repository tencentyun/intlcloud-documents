이 문서는 방 관리 기능의 사용 사례와 기능에 빠르게 연결하는 방법을 설명합니다.

## 기능 소개
클라이언트 방 관리 API를 사용하여 방 구성원 및 구성원 마이크 켜짐/꺼짐 상태를 쉽게 관리할 수 있습니다.


## 사용 사례

예를 들어 Werewolf의 호스트는 EnableMic를 사용하여 다른 플레이어가 마이크를 사용하도록 제어할 수 있습니다. 플레이어가 ‘죽었고’ 회의실 구성원의 말을 듣거나 마이크와 대화할 필요가 없는 경우 호스트는 ForbidUserOperation API를 사용하여 플레이어가 장치를 조작하지 못하도록 금지합니다.


## 전제 조건
- **음성 채팅 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK에 액세스**: 핵심 API 및 음성 채팅 API에 대한 액세스를 포함합니다. 자세한 내용은 [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858), [Unity SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44544), [Unreal SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.


<dx-alert infotype="explain" title="">
이 기능은 H5용 SDK에서 지원되지 않습니다.
</dx-alert>



## 연결 프로세스
### 클래스 이름: ITMGRoomManager

GME 채팅방 관리는 방에 1명 이상의 구성원이 있을 때만 사용할 수 있으며, 방 구성원의 상태를 수정하는 경우에만 사용할 수 있습니다.
API 응답에 대한 모든 콜백은 `ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR`를 통해 처리됩니다. 콜백에 대한 자세한 내용은 [콜백 처리](#test1)를 참고하십시오.

### API 목록


| 유형 | API | 
|---------|---------|
| 캡처 제어 |EnableMic, EnableAudioCaptureDevice, EnableAudioSend | 
| 재생 제어 |EnableSpeaker, EnableAudioPlayDevice, EnableAudioRecv | 
| 장치 상태 획득 |GetMicState, GetSpeakerState | 
| 민감한 API |ForbidUserOperation | 

## 캡처 관리 API

캡처 관리 API는 **마이크**, **오디오 업스트림** 및 **캡처 장치**를 개별적으로 관리하는 데 사용됩니다. 마이크를 관리하는 것은 오디오 업스트림 및 캡처 장치를 모두 관리하는 것과 같습니다. 오디오 업/다운스트림과 하드웨어 장치 관리를 구분하는 이유는, 캡처 장치를 활성화 또는 비활성화하면 전체 장치(캡처 및 재생)가 다시 시작되므로, 만약 이 때 App에서 배경 음악이 재생되고 있었다면 재생이 중지되기 때문입니다. API는 캡처 및 재생 장치의 통합 관리로 인해 배경 음악 재생이 중지될 수 있는 문제를 방지하도록 설계되었습니다.

### 마이크 관리

이 API(EnableMic)는 채팅방에서 사용자의 마이크를 활성화/비활성화하는 데 사용됩니다.
EnableMic를 호출하는 것은 EnableAudioSend 및 EnableAudioCaptureDevice를 모두 호출하는 것과 같습니다.

#### 함수 프로토타입

<dx-codeblock>
::: Android  java
public abstract int EnableMic(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableMic:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| 매개변수       | 유형          | 설명                                                    |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | YES: 사용자의 마이크를 활성화합니다, NO: 사용자의 마이크를 비활성화합니다 |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다                                     |


#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_MIC_OP입니다.

### 오디오 업스트림 관리

이 API(EnableAudioSend)는 채팅방에서 사용자의 오디오 업스트림을 활성화/비활성화하는 데 사용되지만 마이크 캡처에는 영향을 미치지 않습니다.

#### 함수 프로토타입


<dx-codeblock>
::: Android  java
public abstract int EnableAudioSend(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioSend:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| 매개변수       | 유형      | 설명                                                |
| ---------- | --------- | --------------------------------------------------- |
| enable     | BOOL      |YES: 사용자에 대해 업스트림을 활성화합니다, NO: 사용자에 대해 업스트림을 비활성화합니다 |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다                                 |

#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP입니다.

### 장치 관리 캡처

이 API(EnableAudioCaptureDevice)는 채팅방에서 사용자의 오디오 캡처 장치를 활성화/비활성화하는 데 사용되지만 오디오 업스트림에는 영향을 미치지 않습니다.

#### 함수 프로토타입

<dx-codeblock>
::: Android  java
public abstract int EnableAudioCaptureDevice(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>

| 매개변수       | 유형      | 설명                                                         |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      |YES: 사용자의 오디오 캡처 장치를 활성화합니다, NO: 사용자의 오디오 캡처 장치를 비활성화합니다 |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다                                          |

#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_CAPTURE_OP입니다.

## 재생 관리 API

재생 관리 API는 **스피커**, **오디오 다운스트림** 및 **재생 장치**를 개별적으로 관리하는 데 사용됩니다. 스피커를 관리하는 것은 오디오 다운스트림 및 재생 장치를 모두 관리하는 것과 같습니다. 오디오 업/다운스트림과 하드웨어 장치 관리를 구분하는 이유는, 캡처 장치를 활성화 또는 비활성화하면 전체 장치(캡처 및 재생)가 다시 시작되므로, 만약 이 때 App에서 배경 음악이 재생되고 있었다면 재생이 중지되기 때문입니다. API는 캡처 및 재생 장치의 통합 관리로 인해 배경 음악 재생이 중지될 수 있는 문제를 방지하도록 설계되었습니다.

### 스피커 관리

이 API(EnableSpeaker)는 사용자가 채팅방에서 소리를 들을 수 있도록 스피커를 활성화/비활성화하는 데 사용됩니다.
EnableSpeaker를 호출하는 것은 EnableAudioRecv 및 EnableAudioPlayDevice를 모두 호출하는 것과 같습니다.

#### 함수 프로토타입

<dx-codeblock>
::: Android  java
public abstract int EnableSpeaker(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableSpeaker:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| 매개변수       | 유형      | 설명                                                    |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | YES: 사용자를 위해 스피커를 활성화합니다, NO: 사용자의 스피커를 비활성화합니다 |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다                                     |

#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_SPEAKER_OP입니다.

### 오디오 다운스트림 관리

이 API(EnableAudioRecv)는 사용자를 위해 오디오 다운스트림을 활성화/비활성화하는 데 사용되지만 재생 장치에는 영향을 미치지 않습니다.

#### 함수 프로토타입

<dx-codeblock>
::: Android  java
public abstract int EnableAudioRecv(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioRecv:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| 매개변수       | 유형      | 설명                                                        |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | YES: 사용자를 위해 오디오 다운스트림을 활성화합니다, NO: 사용자에 대해 오디오 다운스트림을 비활성화합니다 |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다                                         |

#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP입니다.


### 재생 장치 관리

이 API(EnableAudioPlayDevice)는 사용자의 오디오 재생 장치를 활성화/비활성화하는 데 사용되지만 오디오 다운스트림에는 영향을 미치지 않습니다.

#### 함수 프로토타입

<dx-codeblock>
::: Android  java
public abstract int EnableAudioPlayDevice(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioPlayDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| 매개변수       | 유형      | 설명                                                         |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      |YES: 사용자의 오디오 재생 장치를 활성화합니다, NO: 사용자의 오디오 재생 장치를 비활성화합니다 |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다                                          |

#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_PLAY_OP입니다.

## 사용자 상태를 가져오기 위한 API

### 마이크 상태 가져오기

이 API는 채팅방에서 사용자의 마이크 상태를 가져오는 데 사용됩니다.

#### 함수 프로토타입

<dx-codeblock>
::: Android  java
public abstract int GetMicState(String receiverID);
:::
::: iOS c++
-(QAVResult)GetMicState:(NSString *)receiverID;
:::
</dx-codeblock>


| 매개변수       | 유형      | 설명                |
| ---------- | --------- | ------------------- |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다 |


#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_GET_MIC_STATE입니다.

### 스피커 상태 가져오기

이 API는 채팅방에서 사용자의 스피커 상태를 가져오는 데 사용됩니다.

#### 함수 프로토타입

<dx-codeblock>
::: Android  java
public abstract int GetSpeakerState(String receiverID);
:::
::: iOS c++
-(QAVResult)GetSpeakerState:(NSString *)receiverID;
:::
</dx-codeblock>


#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE입니다.


### 사용자의 마이크/스피커 비활성화

채팅방에 입장하는 각 사용자는 기본적으로 마이크와 스피커를 사용할 수 있습니다. 이 API를 호출하면 사용자가 방을 나갈 때까지 마이크와 스피커가 비활성화됩니다.

<dx-codeblock>
::: Android  java
public  abstract int ForbidUserOperation(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)ForbidUserOperation:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>

| 매개변수       | 유형      | 설명                                                        |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | YES: 사용자의 장치를 비활성화합니다, NO: 사용자에 대해 장치를 활성화합니다 |
| receiverID | NSString* | 사용자의 OpenId를 지정합니다                                         |

#### 콜백

콜백 매개변수는 ITMG_ROOM_MANAGERMENT_FOBIN_OP입니다.

<span id="test1"></span>
## 콜백 처리

다른 모든 GME 콜백과 마찬가지로 채팅방 관리 콜백은 `ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR`라는 이벤트와 함께 OnEvent를 사용하여 처리됩니다. 이 이벤트는 아래와 같이 매개변수 구조를 반환합니다.

#### 콜백 매개변수

| 매개변수         | 유형     | 설명                                                     |
| ------------ | -------- | -------------------------------------------------------- |
| SenderID     | NSString | 이벤트 발신자의 ID입니다. 자신의 OpenId와 같으면 발신자는 클라이언트입니다 |
| ReceiverID   | NSString | 이벤트 수신자의 ID입니다. 자신의 OpenId와 동일한 경우 수신자는 클라이언트입니다 |
| OperateType  | NSNumber | 이벤트 유형                                                 |
| Result       | NSNumber | 이벤트 결과. 0: 성공                                        |
| OperateValue | NSNumber | 콜백 세부 정보                                                 |

#### OperateType

| 값 | 이벤트 유형                               | 설명                       |
| ---- | -------------------------------------- | -------------------------- |
| 0    | ITMG_ROOM_MANAGEMENT_CAPTURE_OP        | 캡처 장치 제어 콜백       |
| 1    | ITMG_ROOM_MANAGEMENT_PLAY_OP           | 재생 장치 제어 콜백       |
| 2    | ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP     | 오디오 업스트림 제어 콜백               |
| 3    | ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP      | 오디오 다운스트림 제어 콜백               |
| 4    | ITMG_ROOM_MANAGEMENT_MIC_OP            | 마이크 제어 콜백             |
| 5    | ITMG_ROOM_MANAGEMENT_PLAY_OP           | 스피커 제어 콜백             |
| 6    | ITMG_ROOM_MANAGEMENT_GET_MIC_STATE     | 마이크 상태 가져오기             |
| 7    | ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE | 스피커 상태 가져오기             |
| 8    | ITMG_ROOM_MANAGERMENT_FOBIN_OP         | 마이크와 스피커 비활성화 |

#### OperateValue

| 구성원      | 설명                     |
| --------- | ------------------------ |
| boolValue |  0: 비활성화, 1: 활성화 |


#### 예시 코드


<dx-codeblock>
::: Android  java
 public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
 if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR== type) {

            ArrayList<String> operatorArr = new ArrayList<String>();
            operatorArr.add("캡처");
            operatorArr.add("재생");
            operatorArr.add("업스트림");
            operatorArr.add("다운스트림");
            operatorArr.add("캡처 및 업스트림");
            operatorArr.add("재생 및 다운스트림");
            operatorArr.add("mic 상태");
            operatorArr.add("spk 상태");
            operatorArr.add("mic/speak 비활성화");

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
                    Toast.makeText(getActivity(), String.format("id:%s에게 발송한 %s 작업, 결과:%s", ReceiverID, operatorArr.get(OperateType), OperateValue ? "on" : "off"), Toast.LENGTH_LONG).show();
                } else  {
                    Toast.makeText(getActivity(), String.format("id:%s에게 발송한 %s%s 작업, 결과:%d", ReceiverID, operatorArr.get(OperateType), OperateValue ? "on" : "off", Result), Toast.LENGTH_LONG).show();
                }

            } else if (ReceiverID.equals(identifier)||ReceiverID.equals("ALL")) {
                if (Result == 0) {
                    switch (OperateType) {
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_CAPTURE_OP:
                        {
                            if (!OperateValue) {
                                mSwitchCapture.setChecked(OperateValue);
                            } else  {
                                AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  //객체 생성
                                dialog.setTitle("장치 캡처 활성화 여부");
                                dialog.setMessage("");
                                dialog.setCancelable(false);
                                dialog.setPositiveButton("On", new DialogInterface.OnClickListener() {
                                    //확인 버튼의 클릭 이벤트 설정
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        mSwitchCapture.setChecked(true);
                                        ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableAudioCaptureDevice(true);
                                    }
                                });
                                dialog.setNegativeButton("Off", new DialogInterface.OnClickListener() {
                                    //취소 버튼의 클릭 이벤트 설정
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
                                AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  //객체 생성
                                dialog.setTitle("업스트림 활성화 여부");
                                dialog.setMessage("");
                                dialog.setCancelable(false);
                                dialog.setPositiveButton("On", new DialogInterface.OnClickListener() {
                                    //확인 버튼의 클릭 이벤트 설정
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        mSwitchSend.setChecked(true);
                                        ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableAudioSend(true);
                                    }
                                });
                                dialog.setNegativeButton("Off", new DialogInterface.OnClickListener() {
                                    //취소 버튼의 클릭 이벤트 설정
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
                                 AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  //객체 생성
                                 dialog.setTitle("캡처 및 업스트림 활성화 여부");
                                 dialog.setMessage("");
                                 dialog.setCancelable(false);
                                 dialog.setPositiveButton("On", new DialogInterface.OnClickListener() {
                                     //확인 버튼의 클릭 이벤트 설정
                                     @Override
                                     public void onClick(DialogInterface dialog, int which) {
                                         mSwitchCapture.setChecked(true);
                                         mSwitchSend.setChecked(true);
                                         ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableMic(true);
                                     }
                                 });
                                 dialog.setNegativeButton("Off", new DialogInterface.OnClickListener() {
                                     //취소 버튼의 클릭 이벤트 설정
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
                    Toast.makeText(getActivity(), String.format("id:%s(으)로부터 %s 작업 수신, 결과:%s",SenderID,operatorArr.get(OperateType),OperateValue?"on":"off"), Toast.LENGTH_LONG).show();
                }
                else if (OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_SPEAKER_OP || OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP|| OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_PLAY_OP|| OperateType == ITMGContext.ITMG_ROOM_MANAGERMENT_FOBIN_OP){
                    Toast.makeText(getActivity(), String.format("id:%s(으)로부터 %s%s 작업 수신,결과:%d",SenderID,operatorArr.get(OperateType),OperateValue?"on":"off",Result), Toast.LENGTH_LONG).show();
                } else if (OperateValue == false) {
                    Toast.makeText(getActivity(), String.format("id:%s(으)로부터 %s%s 작업 수신, 결과:%d",SenderID,operatorArr.get(OperateType),OperateValue?"on":"off",Result), Toast.LENGTH_LONG).show();
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
            NSArray *operatorArr = @[@"캡처",@"재생",@"업스트림",@"다운스트림",@"캡처 및 업스트림",@"재생 및 다운스트림",@"구성원 제거",@"mic 상태",@"spk 상태",@"mic/speak 비활성화"];
			// _openId
            NSString *SenderID = [data objectForKey:@"SenderID"];
            NSString *ReceiverID = [data objectForKey:@"ReceiverID"];
            NSNumber *OperateType = [data objectForKey:@"OperateType"];
            NSNumber *Result = [data objectForKey:@"Result"];
            NSNumber *OperateValue = [data objectForKey:@"OperateValue"];
            
            //자신이 전송한 명령
            if ([SenderID isEqualToString:_openId]) {
                if (OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_MIC_STATE || OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE) {
                          NSString *alterString = [NSString stringWithFormat:@"id:%@에게 발송한 %@ 작업, 결과:%@",ReceiverID,operatorArr[OperateType.intValue],OperateValue.boolValue?@"on":@"off"];
                                             UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"방 관리 작업" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                             [alert show];
                }
                else
                {
                    NSString *alterString = [NSString stringWithFormat:@"id:%@에게 발송한 %@%@작업, 결과:%@",ReceiverID,OperateValue.boolValue?@"on":@"off",operatorArr[OperateType.intValue],Result];
                               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"방 관리 작업" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                               [alert show];
                }
           
                
            } 
			else if([ReceiverID isEqualToString:_openId] ){ //다른 사람이 전송한 명령
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
                        NSString *alterString = [NSString stringWithFormat:@"id:%@(으)로부터 %@작업 수신, 결과:%@",SenderID,operatorArr[OperateType.intValue],OperateValue.boolValue?@"on":@"off"];
                                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"방 관리 작업" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                [alert show];
                    }
                else{
                    	NSString *alterString = [NSString stringWithFormat:@"id:%@(으)로부터 %@%@ 작업 수신, 결과:%@",SenderID,OperateValue.boolValue?@"on":@"off",operatorArr[OperateType.intValue],Result];
                              UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"방 관리 작업" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                              [alert show];
                	}
            	}
			}
    	}
        break;
}
:::
</dx-codeblock>

