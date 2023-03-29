
This document provides a detailed description of using custom audio package attached with message that makes it easy for developers to debug and integrate the APIs for Game Multimedia Engine (GME).

## Overview

The feature of custom audio package attached with message allows you to attach custom messages in the GME audio package as a signaling broadcast to users in the same room.


## Prerequisites

- **You have activated the voice chat service**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- **You have integrated the GME SDK**, including core APIs and voice chat APIs. For more information, see [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), and [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545).


## Use Limits

Calling this API must meet two requirements: the room type should be [Standard or HD](https://www.tencentcloud.com/document/product/607/18522) (ITMG_ROOM_TYPE_STANDARD or ITMG_ROOM_TYPE_HIGHQUALITY); The mic of the sender and the speaker of the receiver are both on.

## Integrating Custom Message Feature

### Sending custom messages

#### API prototype


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

#### Parameter description

| Parameter | Type | Description |
|----------|-------|-------|
|data       |NSData *, byte[]   |Message to be delivered|
|reaptCout  |int        |Repeat times, fill in -1 for unlimited repetitive sending|

#### Returned values
A returned value of QAV_OK indicates the call is successful.

Callback returning 1004 indicates parameter error, please check parameter. Returning 1201 indicates non-existent room, please check room number.

For more error codes, see [Error Codes](https://www.tencentcloud.com/document/product/607/33223).

#### Sample code

**Executed statements**


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
    if(ret != 0){
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


**Callback**


<dx-codeblock>
::: iOS 
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString* log =[NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    switch (eventType) {
                 case   ITMG_MAIN_EVENT_TYPE_CUSTOMDATA_UPDATE: {
            if (ITMG_CUSTOMDATA_AV_SUB_EVENT_UPDATE == ((NSNumber *)data[@"sub_type"]).intValue) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"customdata" message:[NSString stringWithFormat:@"content:%@,from:%@ ",data[@"content"],data[@"senderid"]] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
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



### Stopping sending custom messages
Call this API to stop sending custom messages

#### API prototype

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


#### Returned values

If the API returns error code 1003, `StopSendCustomData` is being performed by the SDK, so there is no need to call it again.
