
GME開発者がTencent Cloud GME製品APIのデバッグと導入を容易にするために、このドキュメントではGMEユーザーカスタマイズオーディオパックにメッセージが付属される機能の使用について紹介します。

## シナリオ

GMEユーザーカスタムオーディオパックにメッセージ機能が付属することにより、開発者はGMEオーディオパックにカスタムメッセージを持ち運び、同室の人にブロードキャストするためのシグナリングとして機能することができます。


##  前提条件

- **リアルタイムボイスサービスを有効にしました：[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入が含まれます。詳細については、[Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。


## 使用制限

このインターフェースを呼び出すには、**Standard**および**High-Definition**（ITMG_ROOM_TYPE_STANDARDおよびITMG_ROOM_TYPE_HIGHQUALITY）のルームタイプが必要で、また送信側でマイクをオンにし、受信側でスピーカーをオンにする必要があります。

##　カスタムメッセージ機能の導入

### カスタムメッセージの送信

#### インターフェースのプロトタイプ


<dx-codeblock>
::: iOS 
-(int) SendCustomData:(NSData *)data repeatCout:(int)reaptCout;
:::
::: Android java
public abstract int SendCustomData(byte[] data,int repeatCout);
:::
::: Unity undefined
public abstract int SendCustomData(byte[] customdata,int repeatCout);
:::
</dx-codeblock>

#### パラメータの説明

| パラメータ   | タイプ     | 意味            |
|----------|-------|-------|
|data       |NSData * 、byte[]    |渡す情報|
|reaptCout  |int        |繰返し回数です。-1を入力すると無限回繰返し送信となります|

#### 戻り値
インターフェースの戻り値がQAV_OKの場合、成功したことを示します。

コールバックが1004を返した場合、パラメータが間違っていることを示します。パラメータが正しいかどうかを再確認することをおすすめします。1201が返された場合はルームが存在しないことを示します。ルーム番号が正しいかどうかを確認することをお勧めします。

エラーコードの詳細については、[エラーコード](https://www.tencentcloud.com/document/product/607/33223)ドキュメントをご参照ください。

####  サンプルコード

**実行ステートメント**


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
::: Android java
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
              if(ret != 0) {
                 ShowWarnning(string.Format("send customdata failed err:{0}",ret));
              }
           }
       });
}
:::
</dx-codeblock>


**コールバック**


<dx-codeblock>
::: iOS 
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    switch (eventType) {
                 case   ITMG_MAIN_EVENT_TYPE_CUSTOMDATA_UPDATE: {
            if (ITMG_CUSTOMDATA_AV_SUB_EVENT_UPDATE == ((NSNumber *)data[@"sub_type"]).intValue) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"customdata" message:[NSString stringWithFormat:@"内容:%@,from:%@ ",data[@"content"],data[@"senderid"]] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                    [alert show];
            }
        }
            break;
    }
}
:::
::: Android java
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



### カスタムメッセージの送信を停止する
このインターフェースを呼び出すとカスタムメッセージの送信を停止します。

#### インターフェースのプロトタイプ

<dx-codeblock>
::: iOS 
-(int) StopSendCustomData;
:::
::: Android java
public abstract int StopSendCustomData();
:::
::: Unity undefined
public abstract int StopSendCustomData();
:::
</dx-codeblock>


#### 戻り値

インターフェースが1003を返した場合、StopSendCustomDataが操作されたことを示します。SDKはその操作を実行中であり、再度呼び出す必要はありません。
