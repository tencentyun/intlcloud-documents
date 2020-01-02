Unityを使う開発者たちがTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを手軽に実行できるように、Unityでの開発に向けるアクセス技術ドキュメントについて説明させていただきます。

>このドキュメントはGME sdk version：2.5に対応しています。

## GME利用上の重要事項

|重要インターフェース     | インターフェースの意味|
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|EnterRoom |入室します  |
|EnableMic |マイクをオンにします |
|EnableSpeaker|スピーカーをオンにします |

>
- GMEを利用する前にプロジェクトを設定してください、設定しないと、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKであり、数値は0です。
- GMEのインターフェースへの呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには、認証が必要です、ドキュメントの認証部分の内容を参照してください。
- GMEは周期的にPollインターフェースを呼び出して、イベントのコールバックをトリガーしています。
- GMEのコールバック情報については、コールバックメッセージリストをご参照してください。
- デバイスを操作するには、成功に入室する後が必要です。
- エラーコードの詳細について、「エラーコード」(https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。

## リアルタイム音声のフローチャート
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)

## 初期化の関連インターフェース
初期化が実施されていない場合、SDKは未初期化段階です、リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
- 利用問題について、「一般的な問題」(https://intl.cloud.tencent.com/document/product/607/30254)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |

### インスタンスの取得
QAVContext.GetInstance()の直接呼び出しでインスタンスを取得するのではなく、ITMGContextのメソッドでContextのインスタンスを取得してください。

### SDKの初期化

パラメータの取得について、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースでは、パラメータとしてTencent CloudコンソールからのSDKAppID番号と一つのユーザーを標識する一意のopenIdが必要です。ルールはApp開発者によって設定され、Appの範囲内で唯一な値（現在はINT64のみをサポートしています）です。
>入室するには、SDKを先に初期化する必要があります。
>
>####  関数のプロトタイプ

```
ITMGContext Init(string sdkAppId, string openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |String  |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |String  |openIdはInt64型のみをサポートします（stringに変換され、入力されます）、この値は10000以下にならなく、ユーザーを標識する値です|

####  サンプルコード 


```
int ret = ITMGContext.GetInstance().Init(str_appId, str_openID);
	if (ret != QAVError.OK) {
		return;
	}
```
### イベントコールバックのトリガー
updateの中で、Pollを周期的に呼び出すことで、イベントコールバックをトリガーすることができます。
####  関数のプロトタイプ

```
ITMGContext public abstract int Poll();
```
### システムの一時停止
システムにPauseイベントが発生した場合、エンジンに通知を出し、Pauseを実行させる必要があります。
####  関数のプロトタイプ

```
ITMGContext public abstract int Pause()
```

### システムリカバー
システムにResumeイベントが発生した場合、エンジンに通知を出し、Resumeを実行させる必要があります。Resumeインターフェースはリアルタイム音声のみをリカバーします。
####  関数のプロトタイプ

```
ITMGContext  public abstract int Resume()
```



### SDKの未初期化
SDKを未初期化にして、初期化以前の状態に入ります。アカウントを切り替えするとき、SDKを未初期化にする必要があります。
####  関数のプロトタイプ

```
ITMGContext public abstract int Uninit()
```





## リアルタイム音声ルームの関連インターフェース
リアルタイム音声通話を行うには、初期化してから、SDKのルーム参加のインタフェースを呼び出して、入室する必要があります。
利用上の問題について、[リアルタイム音声関連問題](https://intl.cloud.tencent.com/document/product/607/30257)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|GenAuthBuffer    |初期化認証です|
|EnterRoom   |入室します|
|IsRoomEntered   |入室していますか|
|ExitRoom |退室します|
|ChangeRoomType |ユーザールームのオーディオタイプを修正します|
|GetRoomType |ユーザールームのオーディオタイプを取得します|


### 認証情報
AuthBufferを生成し、関連機能の暗号化と認証に適用します、関連バックグラウンドのデプロイについては[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
オフライン音声取得の認証を行うとき、ルーム番号のパラメータをnullに設定する必要があります。

####  関数のプロトタイプ
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent CloudコンソールからのsdkAppId番号です|
| roomId    |string   |ルーム番号、最大127文字までサポートします（オフライン音声ルーム番号パラメータをnullに設定する必要があります）|
| openID    |string |ユーザーID|
| key    |string |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|


####  サンプルコード  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId,openID, "a495dca2482589e9");
}
```



### 入室
生成された認証情報で入室します。入室するときに、マイクとスピーカーがデフォルトでオフになっています。

範囲音声のアクセスフローについて、[範囲音声](https://intl.cloud.tencent.com/document/product/607/17972)をご参照ください。


####  関数のプロトタイプ
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId|string    |ルーム番号、最大127文字までサポートします|
| roomType |ITMGRoomType|ルームのオーディオタイプです|
| authBuffer |Byte[] |認証コードです|

ルームのオーディオタイプについては、「音質選択」(https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

## 入室する後のイベントコールバック
入室した後、委託関数を介してコールバックを行う必要があります。resultとerror_infoの二つの情報があります。

####  関数のプロトタイプ
```
委託関数：
public delegate void QAVEnterRoomComplete(int result, string error_info);
イベント関数：
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

監視処理：
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
	    ShowWarnning (string.Format ("join room failed, err:{0}, errInfo:{1}", err, errInfo));
	    return;
	}else{
	    ShowWarnning (string.Format ("現在の音声ルームid:{0}、他の端末から入室し通話してください。",roomId ));
    }
}
```

### 入室したかの判断
このインターフェースを呼び出すことで、入室したかを判断できます、戻り値はbool型です。

####  関数のプロトタイプ  
```
ITMGContext abstract bool IsRoomEntered()
```
####  サンプルコード  
```
ITMGContext.GetInstance().IsRoomEntered();
```

### 退室
このインターフェースを呼び出すことで、退室できます。このインターフェースは非同期であり、戻り値AV_OKの意味は、非同期の送信成功です。

>アプリケーション中に退室してからすぐに入室するケースがある場合、インターフェースの呼び出し時、開発者はExitRoomのコールバックRoomExitComplete通知を待つ必要がなく、インターフェースを直接に呼び出せばよいです。

####  関数のプロトタイプ  
```
ITMGContext ExitRoom()
```
####  サンプルコード  
```
ITMGContext.GetInstance().ExitRoom();
```

### 退室のコールバック
退室しコールバックを完成して、委託関数でメッセージを送信します。
####  関数のプロトタイプ  
```
委託関数：
public delegate void QAVExitRoomComplete();
イベント関数：
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```
####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
監視処理：
void OnExitRoomComplete(){
    //退室した後の処理
}
```

### ユーザールームのオーディオタイプの取得
このインターフェースはユーザールームのオーディオタイプを取得するインターフェイスであり、戻り値はルームのオーディオタイプです、戻り値は0であることは、ユーザールームのオーディオタイプの取得にエラーが発生したことを示しています、。ルームのオーディオタイプについてEnterRoomインターフェースをご参照ください。

####  関数のプロトタイプ  
```
ITMGContext ITMGRoom public  int GetRoomType()
```

####  サンプルコード  
```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### ユーザールームのオーディオタイプの変更
このインターフェースはユーザールームのオーディオタイプを変更するインターフェイスです。
####  関数のプロトタイプ  
```
ITMGContext ITMGRoom public void ChangeRoomType(ITMGRoomType roomtype)
```


|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomtype    |ITMGRoomType    |切り替えたいルームタイプです、ルームのオーディオタイプについて、EnterRoomインターフェースをご参照ください|

####  サンプルコード  
```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```



### ルームのオーディオタイプのコールバックの変更
ルームのタイプを主動的に設定します、ルームタイプを設定した後、委託関数で修正完了の関連情報を渡します。

|戻ったパラメータ     | 意味  |
| ------------- |:-------------:|
| result    |0 は成功です|
| error_info    |失敗の場合、関連エラーメッセージが伝送されます|

```
委託関数：
public delegate void QAVOnChangeRoomtypeCallback(int result, string error_info);

イベント関数：
public abstract event QAVCallback OnChangeRoomtypeCallback; 
```

####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().OnChangeRoomtypeCallback += new QAVOnChangeRoomtypeCallback(OnChangeRoomtypeCallback);
監視処理：
void OnChangeRoomtypeCallback(int result, string error_info){
    //ルームタイプ設定完了後の処理
}
```

### ルームタイプ変更の通知
ユーザーまたはルーム内の他のユーザーは主動的にルームタイプを変更する場合、ルームタイプの変更がありましたら、このコールバック関数が呼び出されます。ルームタイプの変更がこのコールバック関数でサービス層に通知されています、戻り値はルームのタイプであり、詳細についてEnterRoomインターフェースをご参照ください。
```
委託関数：
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

イベント関数：
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```
####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
監視処理：
void OnRoomTypeChangedEvent(int roomtype){
    //ルームタイプ変更後の処理
}
```



### メンバー状態の変化
このイベントは状態が変化した場合のみ通知され、状態変化がない場合は通知されません。メンバーの状態をリアルタイムに取得するには、上位レベルで通知を受けたとき、キャッシュしてください。イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEであり，その中にevent_id、countとopenIdListがありまして，イベントメッセージがOnEvent関数で判断されています。
オーディオイベントの通知に、一つの閾値があります、この閾値を越える場合のみ、通知が送信されます。オーディオパケットを受信しない時間は2秒以上になる場合のみ、「あるメンバーがオーディオパケットの送信を停止した」のメッセージが通知されます。

|event_id     | 意味         |アプリケーション側のメンテナンス内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |あるメンバーが入室しました|アプリケーション側でメンバーリストをメンテナンスします|
|ITMG_EVENT_ID_USER_ENTER    |あるメンバーが退室しました|アプリケーション側でメンバーリストをメンテナンスします|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |あるメンバーはオーディオパケットを送信しています|アプリケーション側で通話メンバーリストをメンテナンスします|
|ITMG_EVENT_ID_USER_NO_AUDIO    |あるメンバーはオーディオパケットの送信を停止しました|アプリケーション側で通話メンバーリストをメンテナンスします|

####  サンプルコード
```
委託関数：
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
イベント関数：
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

イベントを監視します。
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
監視処理：
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
    // 処理します

		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //あるメンバーは入室しました
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //あるメンバーは退室しました
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //あるメンバーはオーディオパケットを送信しています
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //あるメンバーはオーディオパケットの送信を停止しました
			    break;
		  
		    default:
			    break;
 		    }
		break;
}

```


### 品質監視イベント
品質監視イベントです。イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYです、戻ったパラメータはweight、floss  とdelayです、それぞれの意味は以下です、イベントメッセージがOnEvent関数で判断されています。

|パラメータ     | 意味         |
| ------------- |-------------|
|weight    |範囲は1-5です。数値5の意味は音質スコアが最高です、数値1の意味は音質スコアが最悪であり、ほとんど利用不可です。数値0は初期値であり、意味がありません|
|floss    |パケットロス率です|
|delay    |オーディオ送達遅延時間（ms）です|


## リアルタイム音声オーディオインターフェース
SDKを初期化した後に入室します、リアルタイムオーディオ音声関連インターフェースを呼び出すには、入室するのが必要です。
ユーザーインターフェースでマイク/スピーカーのオン/オフボタンをクリックするとき、以下の方式をお勧めします。
- ほとんどのゲームAppでは、EnableMicとEnableSpeakerインターフェイスを呼び出すことをお勧めします。これらのインターフェイスは、常にEnableAudioCaptureDevice / EnableAudioSendインターフェイスとEnableAudioPlayDevice / EnableAudioRecvインターフェイスを同時に呼び出す必要があります。
- ソーシャルAppなど他のタイプの移動端末Appのほう、採集デバイスをオンまたはオフにすると、デバイス全体（採集と再生）のリスタートが発生します。もしAppがこのタイミングでBGMの再生中であれば、BGMの再生も中断されます。アップリンクモードとダウンリンクモードを制御することで、再生デバイスを中断せずにマイクのオン/オフを実現することができます。具体的な方法は、入室する時EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true) を呼び出します、マイクのオン/オフをクリックするときに、EnableAudioSend/Recvを呼び出すことでオーディオストリームの送信/受信を実施するかを制御します。
- 採集または再生デバイスを別々にリリースするには、インターフェースEnableAudioCaptureDeviceとEnableAudioPlayDeviceをご参照ください。
- pauseを呼び出してオーディオエンジンを一時停止します、resumeを呼び出してオーディオエンジンをリカバーします。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|EnableMic    |マイクをオン/オフにします|
|GetMicState    |マイク状態を取得します|
|EnableAudioCaptureDevice    |採集デバイスをオン/オフにします|
|IsAudioCaptureDeviceEnabled    |採集デバイスの状態を取得します|
|EnableAudioSend    |オーディオの上がりをオン/オフにします|
|IsAudioSendEnabled    |オーディオの上がり状態を取得します|
|GetMicLevel    |マイクのリアルタイムボリュームを取得します|
|GetSendStreamLevel|オーディオの上がりのリアルタイムボリュームを取得します|
|SetMicVolume    |マイクのボリュームを設定します|
|GetMicVolume    |マイクのボリュームを取得します|
|EnableSpeaker    |スピーカーをオン/オフにします |
|GetSpeakerState    |スピーカーの状態を取得します|
|EnableAudioPlayDevice    |再生デバイスをオン/オフにします|
|IsAudioPlayDeviceEnabled    |再生デバイスの状態を取得します|
|EnableAudioRecv    |オーディオの下りをオン/オフにします|
|IsAudioRecvEnabled    |オーディオの下り状態を取得します|
|GetSpeakerLevel    |スピーカーのリアルタイムボリュームを取得します|
|GetRecvStreamLevel|ほかのルームメンバのリアルタイム下りボリュームを取得します|
|SetSpeakerVolume    |スピーカーのボリュームを設定します|
|GetSpeakerVolume    |スピーカーのボリュームを取得します|
|EnableLoopBack    |インイヤ・モニタリングをオン/オフにします|



### マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使用されます。入室する時、マイクとスピーカーはデフォルトでオフになっています。
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  関数のプロトタイプ  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled   |boolean     |マイクをオンにします場合、渡すパラメータはtrueであり、マイクをオフにします場合、パラメータはfalseです|

####  サンプルコード  
```
マイクをオンにします
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### マイク状態の取得
このインターフェースはマイクの状態の取得に使用されます、戻り値0はオフ状態で、戻り値1はオン状態を表します。
####  関数のプロトタイプ  
```
ITMGAudioCtrl GetMicState()
```
####  サンプルコード  
```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### 採集デバイスのオン/オフ
このインターフェースは、採集デバイスのオン/オフに使用されます。入室する時、デバイスはデフォルトでオフになっています。
- このインターフェースは、入室した後にのみ呼び出すことができます、退室した後、デバイスは自動的にオフになります。
- モバイル端末における採集デバイスの起動は一般的に、権限申請やボリュームタイプの調整を伴っています。

####  関数のプロトタイプ  
```
ITMGAudioCtrl int EnableAudioPlayDevice(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |採集デバイスをオンにします場合、渡すパラメータはtrueであり、採集デバイスをオフにします場合、パラメータはfalseです|

####  サンプルコード

```
採集デバイスをオンにします
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 採集デバイス状態の取得
このインターフェースは、採集デバイス状態の取得に使用されます。
####  関数のプロトタイプ

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```
####  サンプルコード

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### オーディオ送信のオン/オフ
このインターフェースは、オーディオ送信のオン/オフに使用されます。採集デバイスがオンになっている場合は、採集したオーディオデータを送信します。採集デバイスがオフになっている場合は、ミュート状態が続きます。採集デバイスのオン/オフは、インターフェースEnableAudioCaptureDeviceをご参照ください。

####  関数のプロトタイプ

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |オーディオ送信をオンにする場合、渡すパラメータはtrueであり、オーディオ送信をオフにする場合、パラメータはfalseです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### オーディオ送信状態の取得
このインターフェースは、オーディオ送信状態の取得に使用されます。
####  関数のプロトタイプ  
```
ITMGAudioCtrl bool IsAudioSendEnabled()
```
####  サンプルコード  
```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### マイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使用され、戻り値がint型です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl int GetMicLevel
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### オーディオ送信のリアルタイムボリュームの取得
このインターフェースは、オーディオ送信のリアルタイムボリュームの取得に使用され、戻り値はint型であり、戻り値の範囲は0～100です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl int GetSendStreamLevel()
```
####  サンプルコード  
```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### マイクボリュームの設定
このインターフェースは、マイクボリュームの設定に使用されます。パラメータvolumeはマイクボリュームの設定に使用され、値が0の場合はミュートを示し、100の場合はボリュームが増減しないこと示します。そのデフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGAudioCtrl SetMicVolume(int volume)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int      |ボリューム設定で、値の範囲は0～200です。|

####  サンプルコード  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```
###  マイクボリュームの取得
このインターフェースは、マイクボリュームの取得に使用されます。戻り値はint型であり、101である場合は、インターフェースSetMicVolumeを呼び出したことがないを示します。

####  関数のプロトタイプ  
```
ITMGAudioCtrl GetMicVolume()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

### スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使用されます。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  関数のプロトタイプ  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |スピーカーをオフにする場合、渡すパラメータはfalseであり、スピーカーをオンにする場合、パラメータはtrueです|

####  サンプルコード  
```
スピーカーをオンにします。
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### スピーカー状態の取得
このインターフェースは、スピーカー状態の取得に使用されます。戻り値が0の場合、スピーカーがオフになっており、戻り値が1の場合、スピーカーがオンになっており、戻り値が2の場合、スピーカーが稼働中であることを示します。
####  関数のプロトタイプ  
```
ITMGAudioCtrl GetSpeakerState()
```

####  サンプルコード  
```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### 再生デバイスのオン/オフ
このインターフェースは、再生デバイスのオン/オフに使用されます。

####  関数のプロトタイプ  
```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |再生デバイスをオフにする場合、渡すパラメータはfalseであり、再生デバイスをオンにする場合、パラメータはtrueです|

####  サンプルコード  
```
再生デバイスをオンにします。
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 再生デバイスの状態の取得
このインターフェースは、再生デバイスの状態の取得に使用されます。
####  関数のプロトタイプ

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```
####  サンプルコード  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### オーディオ受信のオン/オフ
このインターフェースは、オーディオ受信のオン/オフに使用されます。再生デバイスがオンになっている場合は、ほかのルームメンバーのオーディオデータを再生します。再生デバイスがオフになっている場合は、ミュート状態が続きます。再生デバイスのオン/オフは、インターフェースEnableAudioPlayDeviceをご参照ください。

####  関数のプロトタイプ  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |オーディオ受信をオンにする場合、渡すパラメータはtrueであり、オーディオ受信をオフにする場合、パラメータはfalseです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### オーディオ受信状態の取得
このインターフェースは、オーディオ受信状態の取得に使用されます。
####  関数のプロトタイプ  
```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

####  サンプルコード  
```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### スピーカーのリアルタイムボリュームの取得
このインターフェースはスピーカーのリアルタイムボリュームの取得に使用されます。戻り値はint型であり、スピーカーのリアルタイムボリュームを示します。
####  関数のプロトタイプ  
```
ITMGAudioCtrl GetSpeakerLevel()
```

####  サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### ルームのほかのメンバーのリアルタイム受信ボリュームの取得
このインターフェースは、ルームのほかのメンバーのリアルタイム受信ボリュームの取得に使用されます、戻り値はint型であり、値の範囲は1～100です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |string       |ルームのほかのメンバーのopenIdです|

####  サンプルコード  
```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### スピーカーボリュームの設定
このインターフェースは、スピーカーボリュームの設定に使用されます。
パラメータvolumeはスピーカーボリュームの設定に使用され、値が0の場合はミュートを示し、100の場合はボリュームが増減しないことを示します、デフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int      |ボリューム設定で、値の範囲は0～200です|

####  サンプルコード  
```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### スピーカーボリュームの取得

このインターフェースは、スピーカーボリュームの取得に使用されます。戻り値はint型であり、スピーカーのボリュームを示します、戻り値が101の場合は、インターフェースSetSpeakerVolumeを呼び出したことがないを示します。
Levelはリアルタイムボリュームで、Volumeはスピーカーボリュームで、最終の音声ボリュームは、Level*Volume%となります。例えば、リアルタイムボリューム数値が100で、Volumeが数値60である場合、最終の音声ボリューム数値も60です。

####  関数のプロトタイプ  
```
ITMGAudioCtrl GetSpeakerVolume()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```


### インイヤ・モニタリングの起動
このインターフェースは、インイヤ・モニタリングの起動に使用されます。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool         |起動するかどうかを設定します|

####  サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### デバイス占用とリリースイベントのコールバック
ルームで、デバイスの占用またはリリースが発生すると、このコールバックが呼び出されます、委託関数でイベントの関連情報を渡します。

```
委託関数：
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
イベント関数：
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| deviceType    |int       |1は採集デバイスを示し、2は再生デバイスを示します|
| deviceId    |string |デバイスGUIDであり、デバイスを標識することに使用されます、Windows側とMac側のみで有効です|
| openOrClose    |bool  |採集デバイス/再生デバイスを占用またはリリースします|


|パラメータ     | 数値         |意味|
| ------------- |:-------------:|-------------|
| AUDIODEVICE_CAPTURE    |1       |採集デバイスを示します|
| AUDIODEVICE_PLAYER    |2 |再生デバイスを示します|

####  サンプルコード  

```
イベントを監視します。
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
監視処理：
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    //デバイス占用とリリースイベント関連のコールバック処理
}
```

## オフライン音声のテキスト変換のフローチャート
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## オフライン音声
初期化が実施されていない場合、SDKは未初期化段階です、リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要が有ります。
利用上の問題について、[オフライン音声関連問題](https://intl.cloud.tencent.com/document/product/607/30258)をご参照ください。

## 初期化の関連インターフェース

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |


### オフライン音声の関連インターフェース
|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |認証の初期化です|
|SetMaxMessageLength    |音声メッセージの最大時間を制限します|
|StartRecording|録音を開始します|
|StartRecordingWithStreamingRecognition|ストリーミング録音を開始します|
|PauseRecording|録音を一時停止します|
|ResumeRecording|録音をリカバーします|
|StopRecording    |録音を停止します|
|CancelRecording|録音をキャンセルします|
|GetMicLevel|オフライン音声のリアルタイムマイクボリュームを取得します|
|SetMicVolume|オフライン音声の録音ボリュームを設定します|
|GetMicVolume|オフライン音声の録音ボリュームを取得します|
|GetSpeakerLevel|オフライン音声のリアルタイムスピーカーボリュームを取得します  |
|SetSpeakerVolume|オフライン音声の再生ボリュームを設定します|
|GetSpeakerVolume|オフライン音声の再生ボリュームを取得します|
|UploadRecordedFile |音声ファイルをアップロードします|
|DownloadRecordedFile|音声ファイルをダウンロードします|
|PlayRecordedFile |音声を再生します|
|StopPlayFile|音声再生を停止します|
|GetFileSize |音声ファイルのサイズです|
|GetVoiceFileDuration|音声ファイルの音声時間の長さです|
|SpeechToText |ボイステキスト変換です|

### 認証の初期化
SDKを初期化してから認証の初期化を呼び出します、authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースをご参照ください。
####  関数のプロトタイプ  
```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |byte[]                   |認証|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```

### 音声メッセージの最大時間の制限
音声メッセージの音声時間の長さを制限します、最大は60秒をサポートします。

####  関数のプロトタイプ

```
ITMGPTT int SetMaxMessageLength(int msTime)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |音声の長さで、単位はmsです|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(60000); 
```


### 録音の起動
このインターフェースは、録音の起動に使用されます。ボイスツーテキスト変換などの機能を使用するには、録音ファイルを先にアップロードする必要があります。
####  関数のプロトタイプ  
```
ITMGPTT int StartRecording(string fileDir)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileDir    |string                      |音声データの保存パスです|

####  サンプルコード  
```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```

### 録音開始のコールバック
録音完成のコールバックであり、委託関数でメッセージを渡します。
####  関数のプロトタイプ  
```
委託関数：
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
イベント関数：
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |string                      |codeが0の場合は、録音が完了したことを示します|
| filepath    |string                      |録音データの保存パスです|

#### エラーコード
|エラーコード値 |原因  |推奨ソリューション       |
|-----|------|------|
|4097   |パラメータは空です|コードのインターフェースパラメータが正しいかどうかを確認します|
|4098   |初期化にエラーが発生しました|デバイスが占用されているか、権限が正常であるかどうか、正常に初期化されているかを確認します|
|4099   |録音中です|正確な時点でSDKの録音機能を使用するようにしてください|
|4100   |オーディオデータを採集していません|マイクデバイスが正常であるかどうかを確認します|
|4101   |録音時、録音ファイルへのアクセスにエラーが発生しました|ファイルが存在しており、そのパスの正当性を確認します|
|4102   |マイク権限を取得していないため、エラーが発生しました|SDKを使用するには、マイク権限を取得する必要があるため、該当のエンジンまたはプラットフォームのSDKプロジェクト構成ドキュメントをご参照ください|
|4103   |録音時間が短いため、エラーが発生しました|第一、録音の制限長さの単位がミリ秒であるため、パラメータが正確であるかどうかを確認します。第二、録音するには、その長さは1000ミリ秒以上である必要があります|
|4104   |録音を起動していません|録音の起動インターフェースを呼び出しているかどうかを確認します|

####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete +=  new QAVRecordFileCompleteCallback (OnRecordFileComplete);
監視処理：
void OnRecordFileComplete(int code, string filepath){
    //録音コールバックの起動
}
```

### ストリーミングAutomatic Speech Recognitionの起動
このインターフェースは、ストリーミングAutomatic Speech Recognitionの起動に使用されます、コールバックにおいて、ボイスはリアルタイムにテキスト変換されて返されるため、言語を指定して識別し、または音声から識別した情報を指定の言語に翻訳してから返すことができます。

####  関数のプロトタイプ  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string translateLanguage,string translateLanguage) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath|String|音声データの保存パスです|
| speechLanguage    |String|指定文字として識別するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください|
| translateLanguage|String|指定文字として翻訳するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください（このパラメータは現在使用できないため、speechLanguageと同じパラメータを入力してください）|

####  サンプルコード  
```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```

### ストリーミングAutomatic Speech Recognitionのコールバックの起動
ストリーミングAutomatic Speech Recognition完了後のコールバック起動で、委託関数でメッセージを渡します。
```
委託関数：
public delegate void QAVStreamingRecognitionCallback(int code, string fileid, string filepath, string result);
イベント関数：
public abstract event QAVStreamingRecognitionCallback OnStreamingSpeechComplete;
```

|メッセージ名前     | 意味         |
| ------------- |:-------------:|
| code    |ストリーミングAutomatic Speech Recognitionが成功したかを判断するリターンコードです|
| result    |ボイステキスト変換の結果テキストです|
| filepath |録音を保存するローカルパスです|
| fileid |録音はバックグラウンドにおけるurlアドレスです|

|エラーコード     | 意味         |対応方法|
| ------------- |:-------------:|:-------------:|
|32775|ストリーミングボイステキスト変換が失敗しましたが、録音が成功しました|UploadRecordedFileインターフェースを呼び出して録音をアップロードしてから、SpeechToTextインターフェースを呼び出してボイステキスト変換を行います|
|32777|ストリーミングボイステキスト変換が失敗しましたが、録音が成功し、アップロードしました|返された情報にはアップロードしたバックグラウンドurlアドレスが含まれているため、SpeechToTextインターフェースを呼び出してボイステキスト変換を行います|

####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
監視処理：
void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
    // ストリーミングAutomatic Speech Recognitionのコールバックの起動
}

```

### 録音の一時停止
このインターフェースは、録音の一時停止に使用されます。録音を継続する場合は、インターフェースResumeRecordingを呼び出してください。

####  関数のプロトタイプ  
```
ITMGPTT int PauseRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().PauseRecording();
```

### 録音の継続
このインターフェースは、録音の継続実行に使用されます。

####  関数のプロトタイプ  
```
ITMGPTT int ResumeRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().ResumeRecording();
```


### 録音の停止
このインターフェースは、録音の停止に使用されます。このインターフェースが非同期インターフェースであるため、録音を停止した後には録音完了のコールバックがあります、録音が成功してから、録音ファイルが利用できます。
####  関数のプロトタイプ  
```
ITMGPTT int StopRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```



### 録音のキャンセル
このインターフェースを呼び出して録音をキャンセルします。キャンセルした後、コールバックがありません。
####  関数のプロトタイプ  
```
ITMGPTT int CancelRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

### オフライン音声のマイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使用されます、戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT int GetMicLevel()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();
```


### オフライン音声の録音ボリュームの設定
このインターフェースは、オフライン音声の録音ボリュームの設定に使用され、その値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT int SetMicVolume(int vol)
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().SetMicVolume(100);
```

### オフライン音声の録音ボリュームの取得
このインターフェースは、オフライン音声の録音ボリュームの取得に使用されます。その戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT int GetMicVolume()
```

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().GetMicVolume();
```
### スピーカーのリアルタイムボリュームの取得
このインターフェースは、スピーカーのリアルタイムボリュームの取得に使用されます。戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT int GetSpeakerLevel()
```

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();
```



### オフライン音声の再生ボリュームの設定
このインターフェースは、オフライン音声の再生ボリュームの設定に使用され、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT int SetSpeakerVolume(int vol)
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().SetSpeakerVolume(100);
```

### オフライン音声の再生ボリュームの取得
このインターフェースは、オフライン音声の再生ボリュームの取得に使用され。その戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT int GetSpeakerVolume()
```

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerVolume();
```

### 音声ファイルのアップロード
このインターフェースは、音声ファイルのアップロードに使用されます。
####  関数のプロトタイプ  
```
ITMGPTT int UploadRecordedFile (string filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |string                      |音声データのアップロードパスです|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```


### 音声のアップロードが完了した後のコールバック
音声のアップロード完了後のコールバックであり、委託関数でメッセージを渡します。
####  関数のプロトタイプ
```
委託関数：
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
イベント関数：
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合は、録音が完了したことを示します|
| filepath    |string                      |録音データの保存パスです|
| fileid    |string                      |ファイルのurlパスです|

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション       |
|-----|------|------|
|8193   |アップロード時、ファイルへのアクセスにエラーが発生しました|ファイルが存在しており、そのパスの正当性を確認します|
|8194   |サインの認証に失敗し、エラーが発生しました|認証キーが正しいかどうか、オフライン音声が初期化されているかどうかを確認します|
|8195   |ネット環境のエラーです|デバイスのネット環境はインターネットに正常にアクセスできるかどうかを確認します|
|8196   |アップロードパラメータの取得時、ネット環境のエラーが発生しました|認証が正しいかどうか、デバイスのネット環境はインターネットに正常にアクセスできるかどうかを確認します|
|8197   |アップロードパラメータの取得時、返されたパケットのデータは空です|認証が正しいかどうか、デバイスのネット環境はインターネットに正常にアクセスできるかどうかを確認します|
|8198   |アップロードパラメータの取得時、返されたパケットの解析に失敗しました|認証が正しいかどうか、デバイスのネット環境はインターネットに正常にアクセスできるかどうかを確認します|
|8200   |appinfoが設定されていません|applyインターフェースを呼び出しているかどうか、入力したパラメータが空であるかどうかを確認します|

####  サンプルコード
```
イベントを監視します。
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete +=new QAVUploadFileCompleteCallback (OnUploadFileComplete);
監視処理：
void OnUploadFileComplete(int code, string filepath, string fileid){
    // 音声をアップロードした後のコールバック
}
```


### 音声ファイルのダウンロード
このインターフェースは、音声ファイルのダウンロードに使用されます。
####  関数のプロトタイプ  
```
ITMGPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |string                       |ファイルのurlパスです|
| downloadFilePath    |string                       |ファイルのローカル保存パスです|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```


### 音声ファイルのダウンロードが完了した後のコールバック
音声ファイルダウンロード完了後のコールバックであり、委託関数でメッセージを渡します。
####  関数のプロトタイプ  
```
委託関数：
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
イベント関数：
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合は、録音が完了したことを示します|
| filepath    |string                      |録音データの保存パスです|
| fileid    |string                      |ファイルのurlパス|

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション       |
|-----|------|------|
|12289  |ファイルのダウンロード時、ファイルへのアクセスにエラーが発生しました    |ファイルパスが合法かどうかを確認します|
|12290   |サインの認証に失敗しました|認証キーが正しいかどうか、オフライン音声が初期化されているかどうかを確認します|
|12291  |ネットストレージシステムに異常が発生しました    |サーバーによる音声ファイルの取得が失敗しました、インターフェースパラメータfileidが正しいかどうか、ネット環境が正常であるかどうか、cosファイルが存在しているかどうかをご確認ください|
|12292  |サーバーのファイルシステムにエラーが発生しました    |デバイスのネット環境はインターネットに正常にアクセスできるかどうか、サーバーに該当ファイルがあるかどうかを確認します|
|12293  |ダウンロードパラメータの取得時、HTTPネットに失敗が発生しました|デバイスのネット環境はインターネットに正常にアクセスできるかどうかを確認します|
|12294   |ダウンロードパラメータの取得時、返されたパケットのデータは空です|デバイスのネット環境はインターネットに正常にアクセスできるかどうかを確認します|
|12295   |ダウンロードパラメータの取得時、返されたパケットの解析に失敗しました|デバイスのネット環境はインターネットに正常にアクセスできるかどうかを確認します|
|12297   |appinfoが設定されていません|認証キーが正しいであるかどうか、オフライン音声が初期化されているかどうかを確認します|



####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete +=new QAVDownloadFileCompleteCallback(OnDownloadFileComplete);
監視処理：
void OnDownloadFileComplete(int code, string filepath, string fileid){
    // 音声ファイルをダウンロードした後のコールバック
}
```



### 音声の再生
このインターフェースは、音声の再生に使用されます。
####  関数のプロトタイプ  
```
ITMGPTT PlayRecordedFile (string downloadFilePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| downloadFilePath    |string                       |ファイルのパスです|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```


### 音声再生のコールバック
音声再生のコールバックであり、委託関数でメッセージを渡します。
####  関数のプロトタイプ  
```
委託関数：
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
イベント関数：
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合は、録音が完了したことを示します|
| filepath    |string                      |録音データの保存パスです|

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション       |
|-----|------|------|
|20481  |初期化にエラーが発生しました|デバイスが占用されているか、権限が正常であるかどうか、正常に初期化されているかを確認します|
|20482  |再生中で、再生を停止して次の音声を再生しようとしましたが失敗しました（普通には停止可能です）|コードのロジックが正しいかどうかを確認します|
|20483  |パラメータは空です|コードのインターフェースパラメータが正しいかどうかを確認します|
|20484  |内部エラーです|プレイヤー初期化のエラー、デコードエラーなどを示すエラーコードであるため、ログを参照して問題を確定する必要があります|


####  サンプルコード  
```
イベントを監視します。
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete +=new  QAVPlayFileCompleteCallback(OnPlayFileComplete);
監視処理：
void OnPlayFileComplete(int code, string filepath){
    // 音声再生のコールバック
}
```




### 音声再生の停止
このインターフェースは、音声再生の停止に使用されます。音声の再生を停止しても、再生完了のコールバックがあります。
####  関数のプロトタイプ  
```
ITMGPTT int StopPlayFile()
```

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```



### 音声ファイルのサイズの取得
このインターフェースを介して、音声ファイルのサイズを取得します
####  関数のプロトタイプ  
```
ITMGPTT GetFileSize(string filePath) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |string                      |音声ファイルのパスです|

####  サンプルコード  
```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### 音声ファイルの音声時間の長さの取得
このインターフェースは、音声ファイルの音声時間の長さの取得に使用され、長さの単位はミリ秒です。
####  関数のプロトタイプ  
```
ITMGPTT int GetVoiceFileDuration(string filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |string                      |音声ファイルのパスです|

####  サンプルコード  
```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```


### 指定の音声ファイルを文字に識別
このインターフェースは、指定の音声ファイルを文字に識別するために使用されます。

####  関数のプロトタイプ  
```
ITMGPTT int SpeechToText(String fileID)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |string                      |音声ファイルのurlです|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```



### 指定の音声ファイルを文字に翻訳（指定言語）
このインターフェースは、言語を指定して識別し、音声から識別した情報を指定の言語に翻訳してから返すことができます。

####  関数のプロトタイプ  
```
ITMGPTT int SpeechToText(String fileID,String language)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |String                     |音声ファイルのurlです|
| speechLanguage    |String                    |指定文字として識別するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translatelanguage    |String                    |指定文字として翻訳するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは現在使用できないため、speechLanguageと同じパラメータを入力する必要があります）|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```



### 識別のコールバック
指定の音声ファイルをテキストに識別し、委託関数でメッセージを渡します。
####  関数のプロトタイプ  
```
委託関数：
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
イベント関数：
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合は、録音が完了したことを示します|
| fileid    |string                     |音声ファイルのurlです|
| result    |string                      |転換で得たテキストです|

####  サンプルコード
```
イベントを監視します。
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += new QAVSpeechToTextCallback(OnSpeechToTextComplete);
監視処理：
void OnSpeechToTextComplete(int code, string fileid, string result){
    // 識別のコールバック
}
```



## 高度なAPI

### バージョンの取得
分析を行うために、SDKのバージョンを取得します。
####  関数のプロトタイプ
```
ITMGContext  abstract string GetSDKVersion()
```
####  サンプルコード  
```
ITMGContext.GetInstance().GetSDKVersion();
```





### ログのプリントレベルの設定
ログのプリントレベルの設定に使用されます。デフォルトレベルを維持することを推奨します。
####  関数のプロトタイプ
```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

|パラメータ| タイプ|意味|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|ログの書き込むレベルの設定で、TMG_LOG_LEVEL_NONEは書き込まないことを示します、デフォルトはTMG_LOG_LEVEL_INFOです。|
|levelPrint|ITMG_LOG_LEVEL|ログのプリントレベルの設定で、TMG_LOG_LEVEL_NONEはプリントしないことを示します、デフォルトはTMG_LOG_LEVEL_ERRORです。|



|ITMG_LOG_LEVEL|意味|
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0|ログをプリントしません|
|TMG_LOG_LEVEL_ERROR=1|エラーログをプリントします（デフォルト）|
|TMG_LOG_LEVEL_INFO=2|ヒントログをプリントします|
|TMG_LOG_LEVEL_DEBUG=3|開発デバッグログをプリントします|
|TMG_LOG_LEVEL_VERBOSE=4|高い頻度のログをプリントします|

####  サンプルコード  
```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### プリントするログのパスの設定
プリントするログのパスの設定に使用されます。
デフォルトのパスは：

| フラットフォーム     |パス        |
| ------------- |-------------|
|Windows |%appdata%\Tencent\GME\ProcessName|
|iOS    |Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

####  関数のプロトタイプ
```
ITMGContext  SetLogPath(string logDir)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| logDir    |NSString   |パスです|

####  サンプルコード  
```
ITMGContext.GetInstance().SetLogPath(path);
```


### 診断情報の取得
オーディオ・ビデオ通信のリアルタイム通信品質の関係情報を取得します。このインターフェースは、主にリアルタイムの通信品質の確認、問題の調査に使用されます、セールス側としては、これを無視しても構いません。
####  関数のプロトタイプ  
```
ITMGRoom GetQualityTips()
```
####  サンプルコード  
```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### オーディオデータブラックリストに追加
特定のIDをオーディオデータブラックリストに追加します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |NSString      |ブラックリストに追加するidです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (id);
```

### オーディオデータブラックリストから削除
特定のIDをオーディオデータブラックリストから削除します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |NSString      |ブラックリストから削除するidです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (id);
```

