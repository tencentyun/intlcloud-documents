## 概要

Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。Unity開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでUnity開発のための導入技術文書を紹介します。

## 使用フローチャート
### リアルタイムボイスフローチャート
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)
### オフラインボイスのボイステキスト変換フローチャート
![](https://main.qcloudimg.com/raw/4c875d05cd2b4eaefba676d2e4fc031d.png)


### GMEの使用に関する重要事項

|重要なAPI     | APIの意味|
| ------------- |:-------------:|
|Init    		|GMEの初期化 	|
|Poll    		|イベントコールバックのトリガ	|
|EnterRoom	 	|ルームに参加  		|
|EnableMic	 	|マイクをオンにする 	|
|EnableSpeaker		|スピーカーをオンにする	|

>**説明：**
- GMEのAPIが正常に呼び出された後、戻り値はQAVError.OKで、値は0です。
- 同じスレッドで、GMEのAPIを呼び出す必要があります。
- GMEによるルームへの参加は認証が必要です。ドキュメントの認証関連部分を参照してください。
- GMEは定期的にPoll APIを呼び出してイベントコールバックをトリガする必要があります。
- GMEのコールバック情報は、コールバックメッセージリストを参照します。
- デバイスの操作はルームに参加した後に行われます。
- このドキュメントはGME SDKバージョン2.3に対応します。


## 関連APIの初期化
初期化する前には、SDKは初期化されていない状態で、初期化が認証された上、SDKを初期化してから、ルームに参加可能となります。

|API     | APIの意味   |
| ------------- |:-------------:|
|Init    	|GMEの初期化	|
|Poll    	|イベントコールバックのトリガ	|
|Pause   	|システム一時停止	|
|Resume 	|システム回復	|
|Uninit    	|GMEの逆初期化 	|

### インスタンス取得
QAVContext.GetInstance()ではなく、ITMGContextメソッドを用いてContextインスタンスを取得してください。

### SDKの初期化
パラメータの取得については、ドキュメント[ゲームマルチメディアエンジン（GME）導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはApp開発者によって定められ、App内で繰り返さないようにします（現在INT64のみ対応）。
SDKを初期化してから、ルームに参加できます。

#### 関数プロトタイプ
```
ITMGContext Init(string sdkAppID, string openID)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  |Tencent CloudコンソールからのSdkAppId番号						|
| openID    	|String  |OpenIDはInt64型（string型に変換して渡す）のみをサポートします。10000以上で、ユーザー識別用 	|

#### サンプルコード  
```
int ret = ITMGContext.GetInstance().Init(str_appId, str_userId);
	if (ret != QAVError.OK) {
		return;
	}
```

### イベントコールバックのトリガ
updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。
#### 関数プロトタイプ

```
ITMGContext public abstract int Poll();
```
### システム一時停止
システムでPauseイベントが発生したら、Pauseを実行するようエンジンに通知する必要があります。
#### 関数プロトタイプ

```
ITMGContext public abstract int Pause()
```

### システム回復
システムでResumeイベントが発生したら、Resumeを実行するようエンジンに通知する必要があります。
#### 関数プロトタイプ

```
ITMGContext  public abstract int Resume()
```






### SDKの逆初期化
SDKを逆初期化し、初期化されていない状態に入ります。アカウントの切り替えには、逆初期化が必要です。
#### 関数プロトタイプ

```
ITMGContext public abstract int Uninit()
```





## リアルタイムボイスルーム関連API
初期化後、SDKでルーム参加を呼び出しルームに参加してから、リアルタイムに音声電話をかけるようになります。

|API     | APIの意味   |
| ------------- |:-------------:|
|GenAuthBuffer    	|認証の初期化|
|EnterRoom   		|ルーム参加|
|EnterTeamRoom   	|チームボイスルームに参加する|
|IsRoomEntered   	|ルームに参加したか|
|ExitRoom 		|ルーム退出|
|ChangeRoomType 	|ユーザールームオーディオタイプの変更|
|GetRoomType 		|ユーザールームオーディオタイプの取得|



### 認証情報
関連機能の暗号化と認証に使用されるAuthBufferを生成します。関連バックグラウンド配置については、[GME暗号鍵ドキュメント](https://cloud.tencent.com/document/product/607/12218)を参照してください。    
オフラインボイスが認証を取得するときに、ルーム番号パラメータをnullに入力する必要があります。
このAPIの戻り値はByte[]型です。
#### 関数プロトタイプ
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    		|int   		|Tencent CloudコンソールからのSdkAppId番号		|
| roomId    		|string   		|ルーム番号、127文字まで入力可能（オフラインボイスのルーム番号パラメータにはnullを入力することが必要）|
| openId    	|String 	|ユーザーID					|
| key    		|string 	|Tencent Cloud[コンソール](https://console.cloud.tencent.com/gamegme)からの暗号鍵				|



#### サンプルコード  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId, userId, "a495dca2482589e9");
}
```

### ルーム参加
生成した認証情報を用いてルームに参加します。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。ルーム参加のタイムアウトが30秒になるとコールバックが受信されます。

範囲ボイス導入の詳細については、[GME範囲ボイス](https://cloud.tencent.com/document/product/607/17972)を参照してください。


#### 関数プロトタイプ
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId		|string    	|ルーム番号、127文字まで入力可能					|
| roomType 	|ITMGRoomType		|ルームオーディオタイプ		|
| authBuffer 	|Byte[] 	|認証コード					|

- ルームオーディオタイプについては、[音質選択](https://cloud.tencent.com/document/product/607/18522)を参照してください。

> サンプルコード  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### ルーム参加イベントのコールバック
ルームに参加した後、デリゲート関数を通じてコールバックを実行する必要があります。resultとerror_infoが含まれます。
#### 関数プロトタイプ
```
デリゲート関数：
public delegate void QAVEnterRoomComplete(int result, string error_info);
イベント関数：
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### サンプルコード
```
イベントのリスニング：
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

リスニング処理：
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
	    ShowWarnning (string.Format ("join room failed, err:{0}, errInfo:{1}", err, errInfo));
	    return;
	}else{
	    ShowWarnning (string.Format ("現在のボイスルームid:{0}、別の終端からこのルームに参加して通話をしてください",roomId ));
    }
}
```

### ルームに参加したかの判断
このAPIの呼び出しによってルームに参加したかを判断できます。戻り値はBOOL型です。
#### 関数プロトタイプ  
```
ITMGContext abstract bool IsRoomEntered()
```
#### サンプルコード  
```
ITMGContext.GetInstance().IsRoomEntered();
```

### ルーム退出
このAPIの呼び出しによって現在のルームから退出できます。これは非同期APIであり、戻り値がAV_OKの場合、非同期配信が完了したことを意味します。

#### 関数プロトタイプ  
```
ITMGContext ExitRoom()
```
#### サンプルコード  
```
ITMGContext.GetInstance().ExitRoom();
```

### ルーム退出コールバック
ルームから退出するとコールバックが完了し、デリゲートでメッセージを渡します。
#### 関数プロトタイプ  
```
デリゲート関数：
public delegate void QAVExitRoomComplete();
イベント関数：
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```
#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
リスニング処理：
void OnExitRoomComplete(){
    //ルーム退出後の処理
}
```

### ユーザールームオーディオタイプの取得
このAPIはユーザールームオーディオタイプの取得に使用され、戻り値はルームのオーディオタイプです。戻り値が0の場合、ユーザールームオーディオタイプの取得にエラーが発生したことを示します。ルームオーディオタイプについては、EnterRoom APIを参照してください。

#### 関数プロトタイプ  
```
ITMGContext ITMGRoom public  int GetRoomType()
```

#### サンプルコード  
```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### ユーザールームオーディオタイプの変更
このAPIはユーザールームオーディオタイプの変更に使用されます。
#### 関数プロトタイプ  
```
ITMGContext ITMGRoom public void ChangeRoomType(ITMGRoomType roomtype)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomtype    |ITMGRoomType    |切り替えたいルームタイプ。ルームオーディオタイプについては、EnterRoom APIを参照してください|

#### サンプルコード  
```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```



### ルームオーディオタイプ変更のコールバック
ルームのタイプを自発的に設定します。ルームのタイプを設定した後、デリゲートで変更された関連メッセージを渡します。

|返されたパラメータ    | 意味  |
| ------------- |:-------------:|
| result    |0は成功を示す|
| error_info    |失敗した場合、関連エラー情報を渡す|

```
デリゲート関数：
public delegate void QAVOnChangeRoomtypeCallback(int result, string error_info);

イベント関数：
public abstract event QAVCallback OnChangeRoomtypeCallback; 
```
#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().OnChangeRoomtypeCallback += new QAVOnChangeRoomtypeCallback(OnChangeRoomtypeCallback);
リスニング処理：
void OnChangeRoomtypeCallback(){
    //ルームタイプ設定完了後の処理
}
```

### ルームタイプ変化通知
ユーザーは自発的にルームタイプを変更したか、またはルーム内の他のユーザーはルームタイプを変更したか、ルームのタイプが変化した場合、このコールバック関数は呼び出されます。このコールバック関数を通じてサービス側にルームタイプの変化を通知し、ルームタイプを戻します。EnterRoom APIを参照してください。
```
デリゲート関数：
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

イベント関数：
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```
#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
リスニング処理：
void OnRoomTypeChangedEvent(){
    //ルームタイプ変更後の処理
}
```


	
### メンバー状態の変更
このイベントは、状態が変化すると通知されるが、状態が変化しないと通知されません。リアルタイムにメンバー状態を取得する必要があれば、上位が通知を受けたときにバッファに保存してください。イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEです。パラメータintentには、event_idとuser_listという2つの情報が含まれ、OnEvent関数でイベントメッセージを判断します。
オーディオイベントの通知にはしきい値があり、このしきい値を越えると通知が送信されます。オーディオパケットが2秒以上受信されないと、「オーディオパケットの送信を停止したメンバーがいる」というメッセージが送信されます。

|event_id     | 意味         |アプリケーション側の保守内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|ルームに参加したメンバーがいる			|アプリケーション側でメンバーリストを保守		|
|ITMG_EVENT_ID_USER_EXIT    				|ルームから退出したメンバーがいる			|アプリケーション側でメンバーリストを保守		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|オーディオパケットを送信したメンバーがいる		|アプリケーション側で通話メンバーリストを保守	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|オーディオパケットの送信を停止したメンバーがいる	|アプリケーション側で通話メンバーリストを保守	|

#### サンプルコード  
```
デリゲート関数：
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
イベント関数：
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

イベントのリスニング：
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
リスニング処理：
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
    //処理
		//開発者はパラメータに対して分析して、event_idおよびuser_listの情報を取得します
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //ルームに参加したメンバーがいる
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //ルームから退出したメンバーがいる
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //オーディオパケットを送信したメンバーがいる
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //オーディオパケットの送信を停止したメンバーがいる
			    break;
		  
		    default:
			    break;
 		    }
		break;
}

```


### 品質監視イベント
品質監視イベント、イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYです。返されたパラメータはweight、floss、およびdelayです。表示される情報は以下の通りです。OnEvent関数でイベントメッセージを判断します。

|パラメータ     | 意味         |
| ------------- |-------------|
|weight    				|範囲は1～50で、数値50の音質評点は優秀、数値1の音質評点は不可で、ほとんど使えません。数値0は初期値（意味なし）を示します|
|floss    				|パケットロス率|
|delay    		|オーディオ届け遅延時間（ms）|


## リアルタイムボイスオーディオAPI
SDKが初期化された後にルームに参加します。ルーム内に限り、リアルタイムオーディオボイスに関連するAPIを呼び出すことができます。
**呼び出しシナリオ**

ユーザーインターフェースでマイク/スピーカーのオン/オフボタンをクリックする場合は、次のようにお勧めします。
- ほとんどのゲームAppに対して、EnableMic APIおよびEnbaleSpeaker APIを呼び出すことをお勧めします。常にEnableAudioCaptureDevice/EnableAudioSend APIとEnableAudioPlayDevice/EnableAudioRecv APIを同時に呼び出すことと同等です。
- ソーシャルタイプのAppなど、他のタイプのモバイルAppでは収集デバイスをオンまたはオフすると、デバイス全体（収集と再生）が再起動します。このときAppがBGMを再生している場合、BGMの再生も中断されます。マイクのオン/オフは、再生デバイスを中断せずに、上りリンクと下りリンクを制御することによって達成されます。具体的な呼び出し方法：ルームに参加するときに、EnableAudioCaptureDevice(true) && EnabledAudioPlayDevice(true)を1回呼び出します。マイクのオン/オフを切り替えるときに、EnableAudioSend/Recvのみを呼び出して、オーディオストリームの送受信を制御します。
- 収集デバイスまたは再生デバイスを個別にリリースする場合、EnableAudioCaptureDevice APIおよびEnableAudioPlayDevice APIを参照してください。
- pauseを呼び出して、オーディオエンジンを一時停止し、resumeを呼び出して、オーディオエンジンを再開します。

|API     | APIの意味   |
| ------------- |:-------------:|
|EnableMic    						|マイクのオン/オフ|
|GetMicState    						|マイク状態の取得|
|EnableAudioCaptureDevice    		|収集デバイスのオン/オフ		|
|IsAudioCaptureDeviceEnabled    	|収集デバイス状態の取得	|
|EnableAudioSend    				|オーディオ上りリンクのオン/オフ	|
|IsAudioSendEnabled    				|オーディオ上りリンク状態の取得	|
|GetMicLevel    						|マイクリアルタイム音量の取得	|
|SetMicVolume    					|マイク音量の設定		|
|GetMicVolume    					|マイク音量の取得		|
|EnableSpeaker    					|スピーカーのオン/オフ|
|GetSpeakerState    					|スピーカー状態の取得	|
|EnableAudioPlayDevice    			|再生デバイスのオン/オフ		|
|IsAudioPlayDeviceEnabled    		|再生デバイス状態の取得	|
|EnableAudioRecv    					|オーディオ下りリンクのオン/オフ	|
|IsAudioRecvEnabled    				|オーディオ下りリンク状態の取得	|
|GetSpeakerLevel    					|スピーカーリアムタイム音量の取得	|
|SetSpeakerVolume    				|スピーカー音量の設定		|
|GetSpeakerVolume    				|スピーカー音量の取得		|
|EnableLoopBack    					|インイヤーモニターのオン/オフ			|



### マイクのオン/オフ
このAPIはマイクのオン/オフに使用されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。
EnableMic = EnableAudioCaptureDevice + EnableAudioSend。
#### 関数プロトタイプ  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |マイクをオンにする必要があれば、渡されたパラメータはtrueです。マイクをオフにすれば、パラメータはfalseです|

#### サンプルコード  
```
マイクをオンにする
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### マイク状態の取得
このAPIはマイク状態の取得に使用されます。戻り値0はマイクオフ状態で、戻り値1はマイクオン状態。
#### 関数プロトタイプ  
```
ITMGAudioCtrl GetMicState()
```
#### サンプルコード  
```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### 収集デバイスのオン/オフ
このAPIは収集デバイスのオン/オフに使用されます。ルームに参加するときに、デバイスがデフォルトでオフです。
- このAPIは、ルームに参加した後にのみ呼び出すことができます。ルームから退出した後デバイスは自動的にオフになります。
- モバイル側で、収集デバイスをオンにすると、通常に権限申請、音量タイプの調整などが必要です。

#### 関数プロトタイプ  
```
ITMGAudioCtrl int EnableAudioPlayDevice(bool isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |収集デバイスをオンにする必要があれば、渡されたパラメータはtrueです。収集デバイスをオフにすれば、パラメータはfalseです|

#### サンプルコード  
```
収集デバイスをオンにします
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 収集デバイス状態の取得
このAPIは収集デバイス状態の取得に使用されます。

#### 関数プロトタイプ  
```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```
#### サンプルコード

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### オーディオ上りリンクのオン/オフ
このAPIはオーディオ上りリンクのオン/オフに使用されます。収集デバイスがオンの場合、収集されたオーディオデータが送信されます。収集デバイスがオフの場合、音声なしのままとなります。収集デバイスのオン/オフについては、API EnableAudioCaptureDeviceを参照してください。

#### 関数プロトタイプ

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |オーディオ上りリンクをオンにする必要があれば、渡されたパラメータはtrueです。オーディオ上りリンクをオフにすれば、パラメータはfalseです|

#### サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### オーディオ上りリンク状態の取得
このAPIはオーディオ上りリンク状態の取得に使用されます。
#### 関数プロトタイプ  

```
ITMGAudioCtrl bool IsAudioSendEnabled()
```
#### サンプルコード  
```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### マイクリアルタイム音量の取得
このAPIはマイクリアルタイム音量の取得に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioCtrl -(int)GetMicLevel
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### マイク音量の設定
このAPIはマイク音量の設定に使用されます。パラメータvolumeはマイク音量の設定に使用され、数値が0の場合はミュート状態を示し、100の場合は音量が変更されないことを示します。デフォルト数値は100です。

#### 関数プロトタイプ  
```
ITMGAudioCtrl SetMicVolume(int volume)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int      |音量設定、範囲0～200|

#### サンプルコード  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```

### マイク音量の取得
このAPIはマイク音量の取得に使用され、戻り値はint型の数値です。戻り値が101の場合、API SetMicVolumeを呼び出したことがないことを意味します。

#### 関数プロトタイプ  
```
ITMGAudioCtrl GetMicVolume()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

### スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### 関数プロトタイプ  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |スピーカーをオフにする必要があれば、渡されたパラメータはfalseです。スピーカーをオンにすれば、パラメータはtrueです|

#### サンプルコード  
```
スピーカーをオンにする
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```


### スピーカー状態の取得
このAPIはスピーカー状態の取得に使用されます。戻り値0はスピーカーオフ状態、戻り値1はスピーカーオン状態、戻り値2はスピーカーデバイス動作中を示します。
#### 関数プロトタイプ  
```
ITMGAudioCtrl GetSpeakerState()
```

#### サンプルコード  
```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```


再生デバイスのオン/オフ
このAPIは再生デバイスのオン/オフに使用されます。
#### 関数プロトタイプ  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        再生デバイスをオフにする必要があれば、渡されたパラメータはfalseです。再生デバイスをオンにすれば、パラメータはtrueです|

#### サンプルコード

```
再生デバイスをオンにする
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```


### 再生デバイス状態の取得
このAPIは再生デバイス状態の取得に使用されます。
#### 関数プロトタイプ

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```
#### サンプルコード

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### オーディオ下りリンクのオン/オフ
このAPIはオーディオ下りリンクのオン/オフに使用されます。再生デバイスがオンになっているとき、ルーム内の他の人のオーディオデータを再生します。再生デバイスがオフになっているとき、音声なしのままとなります。再生デバイスのオン/オフについては、API EnableAudioPlayDeviceを参照してください。

#### 関数プロトタイプ  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |オーディオ下りリンクをオンにする必要があれば、渡されたパラメータはtrueです。オーディオ下りリンクをオフにすれば、パラメータはfalseです|

#### サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```

### オーディオ下りリンク状態の取得
このAPIはオーディオ下りリンク状態の取得に使用されます。
#### 関数プロトタイプ  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```
#### サンプルコード  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```


### スピーカーリアムタイム音量の取得
このAPIはスピーカーリアムタイム音量の取得に使用されます。戻り値はint型で、スピーカーのリアルタイム音量を表示します。
#### 関数プロトタイプ  
```
ITMGAudioCtrl GetSpeakerLevel()
```

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### スピーカー音量の設定
このAPIはスピーカー音量の設定に使用されます。
パラメータvolumeはスピーカー音量の設定に使用され、数値が0の場合はミュート状態を示し、100の場合は音量が変更されないことを示します。デフォルト数値は100です。

#### 関数プロトタイプ  
```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int        |音量設定、範囲0～200|

#### サンプルコード

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### スピーカー音量の取得
このAPIはスピーカー音量の取得に使用されます。戻り値はint型の数値でスピーカー音量を示します。戻り値が101の場合、API SetSpeakerVolumeを呼び出したことがないことを意味します。
Levelはリアルタイム音量で、Volumeはスピーカーの音量です。最終音声の音量はLevel * Volume%に相当します。例えば、リアルタイム音量数値が100の場合、このときのVolumeの数値が60で、最終に出た音声の数値も60です。

#### 関数プロトタイプ  
```
ITMGAudioCtrl GetSpeakerVolume()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```


### インイヤーモニターの起動
このAPIはインイヤーモニターの起動に使用されます。
#### 関数プロトタイプ  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool         |起動要否を設定する|

#### サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### デバイス使用とリリースイベントのコールバック
ルーム内で、デバイス使用とデバイスリリースをするときにコールバックが実行され、デリゲートによってイベントの関連メッセージを渡します。

```
デリゲート関数：
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
イベント関数：
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| deviceType    	|int       	|1は収集デバイスを、2は再生デバイスを表す							|
| deviceId   	 	|string 	|デバイスGUIDです。デバイス識別に使用され、Windows端末とMac端末のみに有効	|
| openOrClose    |bool  	|収集デバイス/再生デバイスの使用またはリリース							|


|パラメータ    | 数値         |意味|
| ------------- |:-------------:|-------------|
| AUDIODEVICE_CAPTURE    	|1       	|収集デバイスを表す|
| AUDIODEVICE_PLAYER   	 	|2 			|再生デバイスを表す|

#### サンプルコード  

```
イベントのリスニング：
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
リスニング処理：
void QAVAudioDeviceStateCallback(){
    //デバイス使用とリリースイベント関連コールバック処理
}
```


## リアルタイムボイス伴奏関連API
|API     | APIの意味   |
| ------------- |:-------------:|
|StartAccompany    				       |伴奏再生の開始|
|StopAccompany    				   	|伴奏再生の停止|
|IsAccompanyPlayEnd				|伴奏の再生が完了したか|
|PauseAccompany    					|伴奏再生の一時停止|
|ResumeAccompany					|伴奏再生の再開|
|SetAccompanyVolume 				|伴奏音量の設定|
|GetAccompanyVolume				|伴奏再生音量の取得|
|SetAccompanyFileCurrentPlayedTimeByMs 				|再生進捗の設定|

### 伴奏再生の開始
このAPIを呼び出して、伴奏の再生を開始します。m4a、wav、およびmp3という3つのフォーマットをサポートします。このAPIを呼び出すと、音量がリセットされます。
#### 関数プロトタイプ  
```
IQAVAudioEffectCtrl int StartAccompany(string filePath, bool loopBack, int loopCount, int duckerTimeMs)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |string            |伴奏再生パス|
| loopBack    |bool          |ミキシング有無の送信。通常trueに設定されます。つまり、他人にも伴奏が聞こえる	|
| loopCount	|int          |ループ数。数値は-1であれば無限ループを示す							|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StartAccompany(filePath,true,loopCount,duckerTimeMs);
```

### 伴奏再生のコールバック
伴奏再生終了時のコールバックです。デリゲートでメッセージを渡します。
#### 関数プロトタイプ  
```
デリゲート関数：
public delegate void QAVAccompanyFileCompleteHandler(int code, string filepath);
イベント関数：
public abstract event QAVAccompanyFileCompleteHandler OnAccompanyFileCompleteHandler;
```
#### サンプルコード
```
イベントのリスニング：
ITMGContext.GetInstance().GetAudioEffectCtrl().OnAccompanyFileCompleteHandler += new QAVAccompanyFileCompleteHandler(OnAccomponyFileCompleteHandler);
リスニング処理：
void OnAccomponyFileCompleteHandler(int code, string filepath){
    //伴奏再生のイベントコールバック
}
```

### 伴奏再生の停止
このAPIを呼び出して、伴奏の再生を停止します。
#### 関数プロトタイプ  
```
IQAVAudioEffectCtrl int StopAccompany(int duckerTimeMs)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| duckerTimeMs    |int             |フェード時間|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StopAccompany(duckerTimeMs);
```

### 伴奏の再生が完了したか
再生が完了したとき、戻り値はtrue、再生が完了していないとき、戻り値はfalse。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl bool IsAccompanyPlayEnd();
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().IsAccompanyPlayEnd();
```


### 伴奏再生の一時停止
このAPIを呼び出して、伴奏の再生を一時停止します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int PauseAccompany()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PauseAccompany();
```



### 伴奏再生の再開
このAPIは伴奏再生の再開に使用されます。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int ResumeAccompany()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().ResumeAccompany();
```

### 自分が伴奏を聞こえるかどうかの設定
このAPIは、自分が伴奏を聞こえるかどうかを設定するために使用されます。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int EnableAccompanyPlay(bool enable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool             |聞こえるか|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().EnableAccompanyPlay(true);
```

### 他人にも伴奏が聞こえるかどうかの設定
他人にも伴奏が聞こえるかどうかを設定します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int EnableAccompanyLoopBack(bool enable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool             |聞こえるか|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().EnableAccompanyLoopBack(true);
```


### 伴奏音量の設定
伴奏音量を設定します。デフォルト値は100です。数値が100以上の場合、音量は増加し、数値が100以下の場合、音量は減少します。値範囲は0～200です。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int SetAccompanyVolume(int vol)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int             |音量値|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetAccompanyVolume(vol);
```

### 伴奏再生音量の取得
このAPIは伴奏音量の取得に使用されます。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl abstract int GetAccompanyVolume()
```
#### サンプルコード  
```
string currentVol = "VOL: " + ITMGContext.GetInstance().GetAudioEffectCtrl().GetAccompanyVolume();
```

### 伴奏再生進捗の取得
伴奏の再生進捗を取得するには、次の2つのAPIを使用します。注意：Current/Total =現在のループ回数、Current％Total =現在のループ再生位置。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl abstract uint GetAccompanyFileTotalTimeByMs()
IQAAudioEffectCtrl abstract int GetAccompanyFileCurrentPlayedTimeByMs()
```
#### サンプルコード  
```
Sstring current = "Current: " + ITMGContext.GetInstance().GetAudioEffectCtrl().GetAccompanyFileCurrentPlayedTimeByMs() + " ms";
string total = "Total: " + ITMGContext.GetInstance().GetAudioEffectCtrl().GetAccompanyFileTotalTimeByMs() + " ms";
```


### 再生進捗の設定
このAPIは再生進捗の設定に使用されます。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl abstract uint SetAccompanyFileCurrentPlayedTimeByMs(uint time)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| time    |uint                |再生進捗、ミリ秒単位|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetAccompanyFileCurrentPlayedTimeByMs(time);
```


## リアルタイムボイス効果音関連API
|API     | APIの意味   |
| ------------- |:-------------:|
|PlayEffect    		|効果音の再生|
|PauseEffect    	|効果音再生の一時停止|
|PauseAllEffects	|すべての効果音の一時停止|
|ResumeEffect    	|効果音再生の再開|
|ResumeAllEffects	|すべての効果音再生の再開|
|StopEffect 		|効果音再生の停止|
|StopAllEffects		|すべての効果音再生を停止|
|SetVoiceType 		|ボイス変更特効|
|SetKaraokeType 		|カラオケ特別効果音|
|GetEffectsVolume	|効果音再生音量の取得|
|SetEffectsVolume 	|効果音再生音量の設定|

### 効果音の再生
このAPIは効果音の再生に使用されます。パラメータ内の効果音IDはApp側で管理される必要があり、IDは1回の独立した再生イベントを表します。この再生はこのIDで制御できます。ファイルはm4a、wav、およびmp3という3つのフォーマットをサポートします。
#### 関数プロトタイプ  

```
IQAAudioEffectCtrl int PlayEffect(int soundId, string filePath, bool loop = false, double pitch = 1.0f, double pan = 0.0f, double gain = 1.0f)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    	|int      	|効果音ID|
| filePath    	|string 	|効果音パス|
| loop    		|bool   	|繰り返し再生の要否|
| pitch    	|double	|未使用フィールド|
| pan    		|double	|未使用フィールド|
| gain    		|double	|未使用フィールド|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PlayEffect(soundId,filePath,true,1.0,0,1.0);
```

### 効果音再生の一時停止
このAPIは効果音再生の一時停止に使用されます。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int PauseEffect(int soundId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PauseEffect(soundId);
```

### すべての効果音再生の一時停止
このAPIを呼び出して、すべての効果音を一時停止します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int PauseAllEffects()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PauseAllEffects();
```

### 効果音再生の再開
このAPIは効果音再生の再開に使用されます。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int ResumeEffect(int soundId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().ResumeEffect(soundId);
```



### すべての効果音再生の再開
このAPIを呼び出して、すべての効果音の再生を再開します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int ResumeAllEffects()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().ResumeAllEffects();
```

### 効果音再生の停止
このAPIは効果音再生の停止に使用されます。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int StopEffect(int soundId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StopEffect(soundId);
```

### すべての効果音再生の停止
このAPIを呼び出して、すべての効果音の再生を停止します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int StopAllEffects()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StopAllEffects(); 
```

### ボイス変更特効
このAPIを呼び出して、ボイス変更特効を設定します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl int setVoiceType(int type)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| type    |int                    |ローカル側のボイス変更タイプを示す|



|タイプパラメータ     |パラメータ例|意味|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  		|0	|原音			|
| ITMG_VOICE_TYPE_LOLITA    				|1	|ロリ			|
| ITMG_VOICE_TYPE_UNCLE  				|2	|おじさん			|
| ITMG_VOICE_TYPE_INTANGIBLE    			|3	|ファンタジー			|
| ITMG_VOICE_TYPE_DEAD_FATBOY  			|4	|デブ			|
| ITMG_VOICE_TYPE_HEAVY_MENTA			|5	|ヘビーメタル			|
| ITMG_VOICE_TYPE_DIALECT 				|6	|外国人			|
| ITMG_VOICE_TYPE_INFLUENZA 				|7	|風邪			|
| ITMG_VOICE_TYPE_CAGED_ANIMAL 			|8	|絶望			|
| ITMG_VOICE_TYPE_HEAVY_MACHINE		|9	|ヘビーマシン			|
| ITMG_VOICE_TYPE_STRONG_CURRENT		|10	|強電流			|
| ITMG_VOICE_TYPE_KINDER_GARTEN			|11	|幼稚園			|
| ITMG_VOICE_TYPE_HUANG 					|12	|ミニオン			|


#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().setVoiceType(0);
```

### カラオケ特別効果音
このAPIを呼び出して、カラオケ特別効果音を設定します。
####  関数プロトタイプ  
```
IQAAudioEffectCtrl int SetKaraokeType(int type)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| type    |int                    |ローカル側のボイス変更タイプを示す|


|タイプパラメータ     |パラメータ例|意味|
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL 		|0	|原音			|
|ITMG_KARAOKE_TYPE_POP 				|1	|流行			|
|ITMG_KARAOKE_TYPE_ROCK 			|2	|ロック			|
|ITMG_KARAOKE_TYPE_RB 				|3	|ヒップホップ			|
|ITMG_KARAOKE_TYPE_DANCE 			|4	|舞曲			|
|ITMG_KARAOKE_TYPE_HEAVEN 			|5	|ファンタジー			|
|ITMG_KARAOKE_TYPE_TTS 				|6	|ボイス合成		|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetKaraokeType(0);
```




### 効果音再生音量の取得
効果音再生の音量を取得します。リニア音量で、デフォルト値は100です。数値が100以上の場合、音量は増加し、数値が100以下の場合、音量は減少します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl  int GetEffectsVolume()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().GetEffectsVolume();
```


### 効果音再生音量の設定
このAPIを呼び出して、効果音の再生音量を設定します。
#### 関数プロトタイプ  
```
IQAAudioEffectCtrl  int SetEffectsVolume(int volume)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int                    |音量値|

#### サンプルコード  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetEffectsVolume(volume);
```







## オフラインボイス
オフラインボイスおよびテキスト変換機能を使用するには、最初にSDKを初期化する必要があります。

|API     | APIの意味   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |認証の初期化	|
|SetMaxMessageLength    |ボイスメッセージ最大時間の制限	|
|StartRecording		|録音の起動		|
|StartRecordingWithStreamingRecognition		|ストリーミング録音の起動		|
|StopRecording    	|録音の停止		|
|CancelRecording	|録音のキャンセル		|
|UploadRecordedFile 	|ボイスファイルのアップロード		|
|DownloadRecordedFile	|ボイスファイルのダウンロード		|
|PlayRecordedFile 	|ボイスの再生		|
|StopPlayFile		|ボイス再生の停止		|
|GetFileSize 		|ボイスファイルのサイズ		|
|GetVoiceFileDuration	|ボイスファイルの時間		|
|SpeechToText 		|ボイスのテキスト認識			|

### 認証の初期化
認証初期化は、SDKの初期化後に呼び出されます。authBufferの取得については、上記のリアルタイムボイス認証情報APIを参照してください。
#### 関数プロトタイプ  
```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |byte[]                   |認証|

#### サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```

### ボイスメッセージ最大時間の制限
ボイスメッセージの最大長さを制限し、最大60秒。
#### 関数プロトタイプ  
```
ITMGPTT int SetMaxMessageLength(int msTime)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |ボイス時間、単位はms|

#### サンプルコード  

```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(60000); 
```


### 録音の起動
このAPIは録音の起動に使用されます。ボイスのテキスト変換操作を実行する前に、録音ファイルをアップロードする必要があります。
#### 関数プロトタイプ  
```
ITMGPTT int StartRecording(string fileDir)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileDir    |string                      |ボイスの保存パス|

#### サンプルコード  
```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```

### 録音起動のコールバック
録音完了時のコールバックです。デリゲートでメッセージを渡します。
#### 関数プロトタイプ  
```
デリゲート関数：
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
イベント関数：
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |string                      |codeが0の場合、記録完了|
| filepath    |string                      |記録用保存アドレス|

#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete += mInnerHandler;
リスニング処理：
void mInnerHandler(int code, string filepath){
    //録音起動のコールバック
}
```

### ストリーミングボイス認識の起動
このAPIはストリーミングボイス認識の起動に使用されます。その同時にコールバックには、リアルタイムのボイス変換テキストが返されます。ストリーミング認識は中国語と英語のみをサポートします。

#### 関数プロトタイプ  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string language)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    	|String	|ボイスの保存パス	|
| language    |String                     |パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください|

#### サンプルコード  
```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN");
```

### ストリーミングボイス認識起動のコールバック
ストリーミングボイス認識起動完了後のコールバックはデリゲートでメッセージを渡します。
```
デリゲート関数：
public delegate void QAVStreamingRecognitionCallback(int code, string fileid, string filepath, string result);
イベント関数：
public abstract event QAVStreamingRecognitionCallback OnStreamingSpeechComplete;
```

|メッセージ名称     | 意味         |
| ------------- |:-------------:|
| code    	|ストリーミングボイス認識が完了したかどうかを判断するための戻りコード		|
| result    		|ボイステキスト変換で認識されたテキスト	|
| filepath 	|録音を保存するローカルアドレス		|
| fileid 		|バックグラウンドでの録音のURLアドレス	|

|エラーコード     | 意味         |処理方法|
| ------------- |:-------------:|:-------------:|
|32775	|ストリーミングボイステキスト変換に失敗しましたが、録音に成功しました	|UploadRecordedFile APIを呼び出して録音をアップロードしてから、SpeechToText APIを呼び出して、ボイステキスト変換操作を行います
|32777	|ストリーミングボイステキスト変換に失敗しましたが、録音とアップロードに成功しました	|返された情報には、アップロードに成功したバックグラウンドURLアドレスが含まれています。SpeechToText APIを呼び出して、ボイステキスト変換操作を行います

#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete += mInnerHandler;
リスニング処理：
void mInnerHandler(int code, string fileid, string filepath, string result){
    //ストリーミングボイス認識起動のコールバック
}

```
### 録音の停止
このAPIは録音の停止に使用されます。このAPIは非同期APIで、記録を停止すると、録音完成のコールバックが送信されます。成功した場合のみ、録音ファイルを利用できます。
#### 関数プロトタイプ  
```
ITMGPTT int StopRecording()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```

### 録音のキャンセル
このAPIを呼び出して、録音をキャンセルします。キャンセルした後、コールバックが送信されません。
#### 関数プロトタイプ  

```
IQAVPTT int CancelRecording()
```
#### サンプルコード  

```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

### ボイスファイルのアップロード
このAPIはボイスファイルのアップロードに使用されます。
#### 関数プロトタイプ  

```
IQAVPTT int UploadRecordedFile (string filePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |string                      |ボイスのアップロードパス|

#### サンプルコード

```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```


### ボイスアップロード完成のコールバック
ボイスアップロード完了のコールバックです。デリゲートでメッセージを渡します。
#### 関数プロトタイプ  
```
デリゲート関数：
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
イベント関数：
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合、記録完了|
| filepath    |string                      |記録用保存アドレス|
| fileid    |string                      |ファイルのURLパス|

#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete += mInnerHandler;
リスニング処理：
void mInnerHandler(int code, string filepath, string fileid){
    //ボイスアップロード完成のコールバック
}
```


### ボイスファイルのダウンロード
このAPIはボイスファイルのダウンロードに使用されます。
#### 関数プロトタイプ  

```
IQAVPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |string                       |ファイルのURLパス|
| downloadFilePath    |string                       |ファイルのローカル保存パス|

#### サンプルコード

```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```


### ボイスファイルダウンロード完了のコールバック
ボイスファイルダウンロード完了のコールバックです。デリゲートでメッセージを渡します。
#### 関数プロトタイプ  
```
デリゲート関数：
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
イベント関数：
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合、記録完了|
| filepath    |string                      |記録用保存アドレス|
| fileid    |string                      |ファイルのURLパス|

#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete += mInnerHandler;
リスニング処理：
void mInnerHandler(int code, string filepath, string fileid){
    //ボイスファイルダウンロード完了のコールバック
}
```



### ボイスの再生
このAPIはボイスの再生に使用されます。
#### 関数プロトタイプ  
```
IQAVPTT PlayRecordedFile (string downloadFilePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| downloadFilePath    |string                       |ファイルパス|

#### サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```


### ボイス再生のコールバック
ボイスファイル再生のコールバックです。デリゲートでメッセージを渡します。
#### 関数プロトタイプ  
```
デリゲート関数：
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
イベント関数：
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合、記録完了|
| filepath    |string                      |記録用保存アドレス|

#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete += mInnerHandler;
リスニング処理：
void mInnerHandler(int code, string filepath){
    //ボイス再生のコールバック
}
```




### ボイス再生の停止
このAPIはボイス再生の停止に使用されます。
#### 関数プロトタイプ  
```
IQAVPTT int StopPlayFile()
```

#### サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```



### ボイスファイルサイズの取得
このAPIによって、ボイスファイルのサイズを取得します。
#### 関数プロトタイプ  
```
IQAVPTT GetFileSize(string filePath) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |string                      |ボイスファイルのパス|

#### サンプルコード  
```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### ボイスファイル時間の取得
このAPIはボイスファイル時間の取得に使用され、単位はミリ秒です。
#### 関数プロトタイプ  
```
IQAVPTT int GetVoiceFileDuration(string filePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |string                      |ボイスファイルのパス|

#### サンプルコード  
```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```


### 指定ボイスファイルのテキスト認識
このAPIは指定されたボイスファイルをテキストに認識するために使用されます。

#### 関数プロトタイプ  

```
IQAVPTT int SpeechToText(String fileID)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |string                      |ボイスファイルURL|

#### サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```

### 指定ボイスファイルのテキスト認識（指定言語）
このAPIは指定されたボイスファイルを指定言語のテキストに認識するために使用されます。

####  関数プロトタイプ  
```
IQAVPTT int SpeechToText(String fileID,String language)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |String                     |ボイスファイルURL|
| language    |String                     |パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください|

####  サンプルコード  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN");
```


### 認識コールバック
指定したボイスファイルをテキストに認識し、デリゲートでメッセージを渡します。
#### 関数プロトタイプ  
```
デリゲート関数：
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
イベント関数：
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| code    |int                       |codeが0の場合、記録完了|
| fileid    |string                      |ボイスファイルURL	|
| result    |string                      |変換されたテキスト結果|

#### サンプルコード  
```
イベントのリスニング：
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += mInnerHandler;
リスニング処理：
void mInnerHandler(int code, string fileid, string result){
    //認識コールバック
}
```
## 高度なAPI
### バージョン番号の取得
分析のために、SDKバージョン番号を取得します。
#### 関数プロトタイプ
```
ITMGContext  abstract string GetSDKVersion()
```
#### サンプルコード  
```
ITMGContext.GetInstance().GetSDKVersion();
```





### プリントするログレベルの設定
プリントするログレベルの設定に使用されます。
#### 関数プロトタイプ
```
ITMGContext  SetLogLevel(int logLevel, bool enableWrite, bool enablePrint)
```


|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| logLevel    		|int   		|プリントするログのレベル			|
| enableWrite    	|bool   		|ファイル書込み要否、デフォルトははい	|
| enablePrint    	|bool   		|コンソール書込み要否、デフォルトははい	|



|ITMG_LOG_LEVEL|意味|
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0		|ログをプリントしない			|
|TMG_LOG_LEVEL_ERROR=1		|エラーログをプリント（デフォルト）	|
|TMG_LOG_LEVEL_INFO=2			|プロンプトログをプリント		|
|TMG_LOG_LEVEL_DEBUG=3		|開発デバッグログをプリント	|
|TMG_LOG_LEVEL_VERBOSE=4		|高頻度ログをプリント		|

#### サンプルコード  
```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_NONE,true,true);
```

### プリントするログのパスの設定
プリントするログのパスを設定するために使用されます。
デフォルトパス：

|プラットフォーム     |パス        |
| ------------- |-------------|
|Windows 	|%appdata%\Tencent\GME\ProcessName|
|iOS    		|Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android	|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### 関数プロトタイプ
```
ITMGContext  SetLogPath(string logDir)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------
| logDir    		|NSString   		|パス|

#### サンプルコード  
```
ITMGContext.GetInstance().SetLogPath(path);
```
### 診断情報の取得
音声テレビ通話のリアルタイムの通話品質に関する情報を取得します。このAPIは、主にリアルタイムの通話品質の確認、トラブルシューティングなどに使用され、サービス側で無視してもかまいません。
#### 関数プロトタイプ  
```
IQAVRoom GetQualityTips()
```
#### サンプルコード  
```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### オーディオデータのブラックリストに追加
あるIDをオーディオデータブラックリストに追加します。戻り値が0の場合、呼び出し失敗を表します。
#### 関数プロトタイプ  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(string openId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |NSString      |ブラックリストに追加するID|

#### サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (id);
```

### オーディオデータのブラックリストから削除
あるIDをオーディオデータブラックリストから削除します。戻り値が0の場合、呼び出し失敗を表します。
#### 関数プロトタイプ  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |NSString      |ブラックリストから削除するID|

#### サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (id);
```


