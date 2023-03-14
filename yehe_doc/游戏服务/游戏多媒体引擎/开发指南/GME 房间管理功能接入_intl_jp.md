ここでは、開発者がルーム管理サービスに素早くアクセスできるように、ルーム管理サービスのユースケースとアクセスの流れについて紹介します。

## 機能の説明
クライアントルーム管理インターフェースにより、ルームメンバーの管理、ルームメンバーのマイクのオン・オフ管理を簡単に実現することができます。


## 運用シーン

例えば、人狼ゲームのシナリオでは、ホストとしてEnableMicで他のプレイヤーのマイクオンをコントロールできます。あるプレイヤーが「死亡」し、ルームの音声を聞いたりマイクを操作して話す必要がない場合、ForbidUserOperationインターフェースを介してそのプレイヤーのデバイス操作を禁止します。


##  前提条件
- **リアルタイムボイスサービスが既に有効にされました**：[音声サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入を含みます。詳細については、[Native SDKクイックスタート](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイックスタート](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイックスタート](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。


<dx-alert infotype="explain" title="">
この機能はH5 SDKではサポートされていません。
</dx-alert>



## 導入プロセス
###　クラス名：ITMGRoomManager

GMEルーム管理機能は、ルームに入ってから呼び出し、ルーム内のメンバーの状態のみを変更できます。
すべてのインターフェースの結果は`ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR`を介してコールバックされます。コールバックの詳細は[コールバック処理](#test1)をご参照ください。

###　インターフェースリスト


| タイプ | インターフェース | 
|---------|---------|
| 収集制御 |EnableMic、 EnableAudioCaptureDevice、EnableAudioSend | 
| 再生制御 |EnableSpeaker、 EnableAudioPlayDevice、EnableAudioRecv | 
| 機器状態の取得 |GetMicState、 GetSpeakerState | 
| 敏感なインターフェース |ForbidUserOperation | 

##　収集管理の関連インターフェース

収集管理インターフェースには、**マイク管理**、**オーディオ上り管理**および**収集ハードウェアデバイス管理**があります。マイク管理は、オーディオ上り管理に収集ハードウェア・デバイス管理を加えることに相当します。オーディオデータの上り下りとハードウェアデバイスの管理を区別するのは、収集デバイスをオンまたはオフにすると、デバイス全体（収集と再生）の再起動に伴い、AppがBGMを再生している場合、BGMの再生が中断されるためです。上り・下りを制御することで、再生デバイスを中断することなくマイクをオン/オフに切り替えることができます。

###　マイク管理

このインターフェースを呼び出して、ルームにいるユーザーのマイクをオンまたはオフにします。呼び出しが成功すると、そのユーザーのマイクはオフまたはオンになります。
EnableMicはEnableAudioSendとEnableAudioCaptureDeviceを同時に呼び出すことに相当します。

####  関数のプロトタイプ

<dx-codeblock>
::: Android java
public abstract int EnableMic(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableMic:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | YES：ユーザーのマイクをオンにします。NO：ユーザーのマイクをオフにします |
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |


#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_MIC_OP。

###　オーディオ上り管理

このインターフェースを呼び出して、ルーム内のユーザーのオーディオ上りをオンまたはオフにします。呼び出しが成功すると、そのユーザーのオーディオ上りはオフまたはオンになりますが、マイクの収集には影響しません。

####  関数のプロトタイプ


<dx-codeblock>
::: Android java
public abstract int EnableAudioSend(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioSend:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | --------------------------------------------------- |
| enable     | BOOL      |YES：ユーザーの上りをオンにします。NO：ユーザーの上りをオフにします　|
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |

#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP。

###　オーディオ収集ハードウェアデバイスの管理

このインターフェースを呼び出して、ルーム内のユーザーのオーディオ収集ハードウェアデバイスをオンまたはオフにします。呼び出しが成功すると、そのユーザーのオーディオ収集ハードウェアデバイスはオフまたはオンになりますが、上りには影響しません。

####  関数のプロトタイプ

<dx-codeblock>
::: Android java
public abstract int EnableAudioCaptureDevice(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>

| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      |YES：ユーザーのオーディオ収集ハードウェアデバイスをオンにします。NO：ユーザーのオーディオ収集ハードウェアデバイスをオフにします |
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |

#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_CAPTURE_OP。

##　再生管理の関連インターフェース

再生管理インターフェースには、**スピーカー管理**、**音声下り管理**および**再生ハードウェアデバイス管理**があります。このうち、スピーカ管理は、音声下り管理に再生ハードウェアデバイス管理を加えることに相当します。オーディオデータの上り下りとハードウェアデバイスの管理を区別するのは、収集デバイスをオンまたはオフにすると、デバイス全体（収集と再生）の再起動に伴い、AppがBGMを再生している場合、BGMの再生が中断されるためです。上り・下りを制御することで、再生デバイスを中断することなくマイクをオン/オフに切り替えることができます。

###　スピーカー管理

このインターフェースを呼び出して、ルーム内のユーザーのスピーカーをオンまたはオフにします。呼び出しが成功すると、そのユーザーのスピーカーがオフまたはオンになり、室内のオーディオ音が聞こえるようになります。
EnableSpeakerはEnableAudioRecvとEnableAudioPlayDeviceを同時に呼び出すことに相当します。

####  関数のプロトタイプ

<dx-codeblock>
::: Android java
public abstract int EnableSpeaker(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableSpeaker:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | ------------------------------------------------------- |
| enable     | BOOL      | YES ：ユーザーのスピーカーをオンにします。NO：ユーザーのスピーカーをオフにします |
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |

#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_SPEAKER_OP。

###　音声下り管理

このインターフェースを呼び出して、ルーム内のユーザーのオーディオ下りをオンまたはオフにします。呼び出しが成功すると、そのユーザーのオーディオ下りはオフまたはオンになりますが、再生デバイスには影響しません。

####  関数のプロトタイプ

<dx-codeblock>
::: Android java
public abstract int EnableAudioRecv(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioRecv:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | YES ：ユーザーのオーディオ下りをオンにします。NO：ユーザーのオーディオ下りをオフにします |
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |

#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_AUDIO_REC_OP。


###　オーディオ再生ハードウェアデバイスの管理

このインターフェースを呼び出して、ルーム内のユーザーのオーディオ再生ハードウェアデバイスをオンまたはオフにします。呼び出しが成功すると、そのユーザーのオーディオ再生ハードウェアデバイスがオフまたはオンになりますが、下りには影響しません。

####  関数のプロトタイプ

<dx-codeblock>
::: Android java
public abstract int EnableAudioPlayDevice(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)EnableAudioPlayDevice:(BOOL)enabled Receiver:(NSString *)receiverID;
:::
</dx-codeblock>


| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| enable     | BOOL      |YES ：ユーザーのオーディオ再生ハードウェアデバイスをオンにします。NO：ユーザーのオーディオ再生ハードウェアデバイスをオフにします　|
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |

#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_PLAY_OP。

##　メンバー状態取得インターフェース

###　特定のユーザーのマイク状態を取得

このインターフェースを呼び出して、ルーム内のメンバーのマイク状態を取得します。

####  関数のプロトタイプ

<dx-codeblock>
::: Android java
public abstract int GetMicState(String receiverID);
:::
::: iOS c++
-(QAVResult)GetMicState:(NSString *)receiverID;
:::
</dx-codeblock>


| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | ------------------- |
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |


#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_GET_MIC_STATE。

###　特定のユーザーのスピーカー状態を取得

このインターフェースを呼び出して、ルーム内のメンバーのスピーカー状態を取得します。

####  関数のプロトタイプ

<dx-codeblock>
::: Android java
public abstract int GetSpeakerState(String receiverID);
:::
::: iOS c++
-(QAVResult)GetSpeakerState:(NSString *)receiverID;
:::
</dx-codeblock>


#### コールバック

コールバックパラメータはITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE。


###　特定のメンバーのマイクやスピーカー操作を禁止

メンバーがルームに入ると、デフォルトでマイクとスピーカーの操作が許可されます。このインターフェースを呼び出すと、ルームのメンバーがマイクとスピーカーを操作できなくなります。この機能は、メンバーがルームを出ると無効になります。

<dx-codeblock>
::: Android java
public  abstract int ForbidUserOperation(boolean isEnabled,String receiverID);
:::
::: iOS c++
-(QAVResult)ForbidUserOperation:(BOOL)enable Receiver:(NSString *)receiverID;
:::
</dx-codeblock>

| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | --------- | ----------------------------------------------------------- |
| enable     | BOOL      | YES：ユーザーによるデバイスの操作を禁止します。NO：ユーザーによるデバイスの操作を許可します |
| receiverID | NSString* | 対象ユーザーのOpenIdを入力します                                     |

#### コールバック

コールバックパラメータはITMG_ROOM_MANAGERMENT_FOBIN_OP。

<span id="test1"></span>
##　コールバック処理

GMEの他のコールバックと同様に、ルーム管理のコールバックもOnEventで処理されます。イベント名は`ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR`で、イベントは次のような構造体を返します。

#### コールバックパラメータ

| パラメータ          | タイプ                    | 意味                                                  |
| ------------ | -------- | -------------------------------------------------------- |
| SenderID     | NSString | イベント送信者IDです。自分のOpenIdと同じ場合は、自端からのコマンド送信となります　|
| ReceiverID   | NSString | イベント受信者IDです。自分のOpenIdと同じ場合は、自端からのコマンド送信となります　|
| OperateType  | NSNumber | イベントのタイプ                                                 |
| Result       | NSNumber | イベントの結果です。0は成功                                        |
| OperateValue | NSNumber | 命コマンドの詳細                                                 |

#### OperateType

| 数値 | イベントタイプ                               | 意味                       |
| ---- | -------------------------------------- | -------------------------- |
| 0    | ITMG_ROOM_MANAGEMENT_CAPTURE_OP        | 収集デバイスハードウェアコールバックの制御       |
| 1    | ITMG_ROOM_MANAGEMENT_PLAY_OP           | 再生デバイスハードウェアコールバックの制御       |
| 2    | ITMG_ROOM_MANAGEMENT_AUDIO_SEND_OP     | 上りコールバックの制御               |
| 3    | ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP      | 下りコールバックの制御               |
| 4    | ITMG_ROOM_MANAGEMENT_MIC_OP            | マイクコールバックの制御             |
| 5    | ITMG_ROOM_MANAGEMENT_PLAY_OP           | スピーカーコールバックの制御             |
| 6    | ITMG_ROOM_MANAGEMENT_GET_MIC_STATE     | マイクの状態を取得します             |
| 7    | ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE | スピーカーの状態を取得します             |
| 8    | ITMG_ROOM_MANAGERMENT_FOBIN_OP         | マイクおよびスピーカーイベントの操作を禁止します |

#### OperateValue

| メンバー      | 意味                     |
| --------- | ------------------------ |
| boolValue |  0：オフコマンド；1：オンコマンド |


####  サンプルコード


<dx-codeblock>
::: Android java
 public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
 if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR== type) {

            ArrayList<String> operatorArr = new ArrayList<String>();
            operatorArr.add("収集");
            operatorArr.add("再生");
            operatorArr.add("上り");
            operatorArr.add("下り");
            operatorArr.add("上り収集");
            operatorArr.add("下り再生");
            operatorArr.add("mic状態");
            operatorArr.add("spk状態");
            operatorArr.add("mic/speak操作禁止");

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
                    Toast.makeText(getActivity(), String.format("id:%sへの%s操作、結果:%s", ReceiverID, operatorArr.get(OperateType), OperateValue ? "オン" : "オフ"), Toast.LENGTH_LONG).show();
                }else{
                    Toast.makeText(getActivity(), String.format("id:%sへの%s%s操作、結果:%d", ReceiverID, operatorArr.get(OperateType), OperateValue ? "オン" : "オフ", Result), Toast.LENGTH_LONG).show();
                }

            } else if (ReceiverID.equals(identifier)||ReceiverID.equals("ALL")) {
                if (Result == 0) {
                    switch (OperateType) {
                        case ITMGContext.ITMG_ROOM_MANAGEMENT_CAPTURE_OP:
                        {
                            if (!OperateValue) {
                                mSwitchCapture.setChecked(OperateValue);
                            }else{
                                AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  //オブジェクト作成
                                dialog.setTitle("機器収集をオンにしますか");
                                dialog.setMessage("");
                                dialog.setCancelable(false);
                                dialog.setPositiveButton("オン", new DialogInterface.OnClickListener() {
                                    //OKボタンのクリックイベントを設定
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        mSwitchCapture.setChecked(true);
                                        ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableAudioCaptureDevice(true);
                                    }
                                });
                                dialog.setNegativeButton("オフ", new DialogInterface.OnClickListener() {
                                    //キャンセルボタンのクリックイベントを設定
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
                            }else{
                                AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  //オブジェクト作成
                                dialog.setTitle("上りをオンにしますか");
                                dialog.setMessage("");
                                dialog.setCancelable(false);
                                dialog.setPositiveButton("オン", new DialogInterface.OnClickListener() {
                                    //OKボタンのクリックイベントを設定
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        mSwitchSend.setChecked(true);
                                        ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableAudioSend(true);
                                    }
                                });
                                dialog.setNegativeButton("オフ", new DialogInterface.OnClickListener() {
                                    //キャンセルボタンのクリックイベントを設定
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
                             }else{
                                 AlertDialog.Builder dialog = new AlertDialog.Builder (getActivity());  //オブジェクト作成
                                 dialog.setTitle("収集と上りをオンにしますか");
                                 dialog.setMessage("");
                                 dialog.setCancelable(false);
                                 dialog.setPositiveButton("オン", new DialogInterface.OnClickListener() {
                                     //OKボタンのクリックイベントを設定
                                     @Override
                                     public void onClick(DialogInterface dialog, int which) {
                                         mSwitchCapture.setChecked(true);
                                         mSwitchSend.setChecked(true);
                                         ITMGContext.GetInstance(getActivity()).GetAudioCtrl().EnableMic(true);
                                     }
                                 });
                                 dialog.setNegativeButton("オフ", new DialogInterface.OnClickListener() {
                                     //キャンセルボタンのクリックイベントを設定
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
                    Toast.makeText(getActivity(), String.format("id:%sからの%s操作、結果:%s",SenderID,operatorArr.get(OperateType),OperateValue?"オン":"オフ"), Toast.LENGTH_LONG).show();
                }
                else if (OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_SPEAKER_OP || OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_AUDIO_REC_OP|| OperateType == ITMGContext.ITMG_ROOM_MANAGEMENT_PLAY_OP|| OperateType == ITMGContext.ITMG_ROOM_MANAGERMENT_FOBIN_OP){
                    Toast.makeText(getActivity(), String.format("id:%sからの%s%s操作、結果:%d",SenderID,operatorArr.get(OperateType),OperateValue?"オン":"オフ",Result), Toast.LENGTH_LONG).show();
                } else if (OperateValue == false) {
                    Toast.makeText(getActivity(), String.format("id:%sからの%s%s操作、結果:%d",SenderID,operatorArr.get(OperateType),OperateValue?"オン":"オフ",Result), Toast.LENGTH_LONG).show();
                }
            }
 }
:::
::: iOS c++
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    [self showLog:log];
    NSLog(@"====%@====", log);
    switch (eventType) {
		case ITMG_MAIN_EVNET_TYPE_ROOM_MANAGEMENT_OPERATOR:
        {
            NSArray *operatorArr = @[@"収集",@"再生",@"上り",@"下り",@"上り収集",@"下り再生",@"メンバー追放",@"mic状態",@"spk状態",@"禁止操作mic/speak"];
			// _openId
            NSString *SenderID = [data objectForKey:@"SenderID"];
            NSString *ReceiverID = [data objectForKey:@"ReceiverID"];
            NSNumber *OperateType = [data objectForKey:@"OperateType"];
            NSNumber *Result = [data objectForKey:@"Result"];
            NSNumber *OperateValue = [data objectForKey:@"OperateValue"];
            
            ///自分が出したコマンド
            if ([SenderID isEqualToString:_openId]) {
                if (OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_MIC_STATE || OperateType.intValue == ITMG_ROOM_MANAGEMENT_GET_SPEAKER_STATE) {
                          NSString *alterString = [NSString stringWithFormat:@"id:%@への%@操作、結果:%@",ReceiverID,operatorArr[OperateType.intValue],OperateValue.boolValue?@"オン":@"オフ"];
                                             UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"ルーム管理操作" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                             [alert show];
                }
                else
                {
                    NSString *alterString = [NSString stringWithFormat:@"id:%@への%@%@操作、結果:%@",ReceiverID,OperateValue.boolValue?@"オン":@"オフ",operatorArr[OperateType.intValue],Result];
                               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"ルーム管理操作" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                               [alert show];
                }
           
                
            } 
			else if([ReceiverID isEqualToString:_openId] ){ //他人からのコマンド
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
                        NSString *alterString = [NSString stringWithFormat:@"id:%@からの%@操作、結果:%@",SenderID,operatorArr[OperateType.intValue],OperateValue.boolValue?@"オン":@"オフ"];
                                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"ルーム管理操作" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                [alert show];
                    }
                else{
                    	NSString *alterString = [NSString stringWithFormat:@"id:%@からの%@%@操作、結果:%@",SenderID,OperateValue.boolValue?@"オン":@"オフ",operatorArr[OperateType.intValue],Result];
                              UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"ルーム管理操作" message:alterString delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                              [alert show];
                	}
            	}
			}
    	}
        break;
}
:::
</dx-codeblock>

