
본문은 개발자가 게임 멀티미디어 엔진(GME)용 API를 쉽게 디버깅하고 통합할 수 있도록 하는 메시지와 함께 사용자 지정 오디오 패키지 사용에 대한 자세한 설명을 제공합니다.

## 시나리오

메시지가 첨부된 사용자 지정 오디오 패키지 기능을 사용하면 GME 오디오 패키지에 사용자 지정 메시지를 같은 방에 있는 사용자에게 신호 방송으로 첨부할 수 있습니다.


## 전제 조건

- **음성 채팅 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK 통합**: 핵심 API 및 음성 채팅 API를 포함합니다. 자세한 내용은 [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.


## 사용 제한

이 API를 호출하려면 두 가지 요구 사항을 충족해야 합니다. 방 유형은 **표준** 또는 **HD**(ITMG_ROOM_TYPE_STANDARD 또는 ITMG_ROOM_TYPE_HIGHQUALITY)여야 하며, 발신자의 마이크와 수신자의 스피커가 모두 켜져 있어야 합니다.

## 사용자 지정 메시지 기능 통합

### 사용자 지정 메시지 전송

#### API 프로토타입


<dx-codeblock>
::: iOS 
-(int) SendCustomData:(NSData *)data repeatCout:(int)reaptCout;
:::
::: Android  java
public abstract int SendCustomData(byte[] data,int repeatCout);
:::
::: Unity undefined
public abstract int SendCustomData(byte[] customdata,int repeatCout);
:::
</dx-codeblock>

#### 매개변수 설명

| 매개변수   | 유형     | 설명            |
|----------|-------|-------|
|data       |NSData * , byte[]    |전달할 메시지|
|reaptCout  |int        |반복 횟수, 무제한 반복 전송을 위해 -1 입력|

#### 반환된 값
반환된 QAV_OK 값은 호출이 성공했음을 나타냅니다.

1004를 반환하는 콜백은 매개변수 오류를 나타냅니다. 매개변수를 확인하십시오. 1201은 존재하지 않는 방임을 나타냅니다. 방 번호를 확인하십시오.

자세한 에러 코드는 [에러 코드](https://www.tencentcloud.com/document/product/607/33223)를 참고하십시오.

#### 예시 코드

**실행 문**


<dx-codeblock>
::: iOS 
-(IBAction)SendCustData:(UIButton*)sender {
    int ret = 0;
    NSString *typeString;
    switch (sender.tag) {
        case 1:
            ret = [[[ITMGContext GetInstance] GetRoom] SendCustomData:[NSData dataWithBytes:_shareRoomID.text.UTF8String length:_roomIdText.text.length] repeatCout:_shareOpenID.text.intValue];
            typeString = @"sendCustData";
            break;
          case 2:
            ret = [[[ITMGContext GetInstance] GetRoom] StopSendCustomData];
            typeString = @"recvCustData";
            break;
        default:
            break;
    }
    if(ret != 0) {
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"set fail" message:[NSString stringWithFormat:@"%@:errorcode :%d",typeString,ret] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
        [alert show];
    }
}
:::
::: Android  java
String strData = mEditData.getText().toString();
String repeatCount = mEditRepeatCount.getText().toString();
int nRet = ITMGContext.GetInstance(getActivity()).GetRoom().SendCustomData(strData.getBytes(), Integer.parseInt(repeatCount));
:::
::: Unity undefined
InputField SendCustom_Count_InputField = transform.Find("inroomPanel/imPanel/SendCustom_Count_InputField").GetComponent<InputField>();
InputField SendCustom_Data_InputField = transform.Find("inroomPanel/imPanel/SendCustom_Data_InputField").GetComponent<InputField>();

transform.Find("inroomPanel/imPanel/SendCustom_Btn").GetComponent<Button>().onClick.AddListener(delegate ()
       {
           string data = SendCustom_Data_InputField.text;
           string str_count = SendCustom_Count_InputField.text;
           int count = 0;
           if (int.TryParse(str_count, out count)) {
               Debug.Log(data+ count.ToString());
               byte[] byteData = Encoding.Default.GetBytes(data);
              int ret =  ITMGContext.GetInstance().GetRoom().SendCustomData(byteData, count);
              if(ret != 0 ) {
                 ShowWarnning(string.Format("send customdata failed err:{0}",ret));
              }
           }
       });
}
:::
</dx-codeblock>


**콜백**


<dx-codeblock>
::: iOS 
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString* log =[NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    switch (eventType) {
                 case   ITMG_MAIN_EVENT_TYPE_CUSTOMDATA_UPDATE: {
            if (ITMG_CUSTOMDATA_AV_SUB_EVENT_UPDATE == ((NSNumber *)data[@"sub_type"]).intValue) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"customdata" message:[NSString stringWithFormat:@"콘텐츠:%@,from:%@ ",data[@"content"],data[@"senderid"]] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                    [alert show];
            }
        }
            break;
    }
}
:::
::: Android  java
if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CUSTOMDATA_UPDATE == type) {
	int subtype  =  data.getIntExtra("sub_event",-1);
	if (subtype == 0) {
	    String content =  data.getStringExtra("content");
	    String sender = data.getStringExtra("senderid");
	    Toast.makeText(getActivity(), String.format("recv content =%s, from:%s", content, 
	        sender), Toast.LENGTH_SHORT).show();
	}
:::
::: Unity undefined
void OnEvent(int eventType,int subEventType,string data)
{
	Debug.Log (data);
	switch (eventType) {
     case (int)ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CUSTOMDATA_UPDATE:
      {
         if(subEventType == (int)ITMG_CUSTOMDATA_SUB_EVENT.ITMG_CUSTOMDATA_AV_SUB_EVENT_UPDATE) {
             _customData = JsonUtility.FromJson<CustomDataInfo>(data);
           ShowWarnning(string.Format("recve customdata {0}  from {1}",_customData.content,_customData.senderid));
         }
      }
     break;
}
:::
</dx-codeblock>



### 사용자 지정 메시지 전송 중지
사용자 지정 메시지 전송을 중지하려면 이 API를 호출하십시오.

#### API 프로토타입

<dx-codeblock>
::: iOS 
-(int) StopSendCustomData;
:::
::: Android  java
public abstract int StopSendCustomData();
:::
::: Unity undefined
public abstract int StopSendCustomData();
:::
</dx-codeblock>


### 반환된 값

API가 오류 코드 1003을 반환하면 SDK에서 StopSendCustomData를 수행하는 중이므로 다시 호출할 필요가 없습니다.
