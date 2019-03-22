Android開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでAndroid開発のための導入技術文書を紹介します。

>?このドキュメントはGME SDKバージョン2.4に対応します。

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


## 関連APIの初期化
初期化する前には、SDKは初期化されていない状態で、初期化が認証された上、SDKを初期化してから、ルームに参加可能となります。

|API     | APIの意味   |
| ------------- |:-------------:|
|Init    	|GMEの初期化	| 
|Poll    	|イベントコールバックのトリガ	|
|Pause   	|システム一時停止	|
|Resume 	|システム回復	|
|Uninit    	|GMEの逆初期化 	|


### シングルトンの取得
ボイス機能を使用するときは、まずITMGContextオブジェクトを取得する必要があります。
####  関数プロトタイプ 

```
public static ITMGContext GetInstance(Context context)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| context    |Context |アプリケーションコンテキストオブジェクト|


####  サンプルコード  

```
import com.tencent.TMG.ITMGContext; 
TMGContext.getInstance(this);
```

### コールバックの登録
APIクラスは、Delegateメソッドを使用してコールバック通知をアプリケーションに送信します。コールバック関数をSDKに登録して、コールバック情報を受け取ります。

####  サンプルコード 
```
private ITMGContext.ITMGDelegate itmgDelegate = null;
```
コールバックのパラメータを処理するには、構造関数でこのコールバック関数を上書きします。

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:| ------------- |
| type    	|ITMGContext.ITMG_MAIN_EVENT_TYPE 	|コールバックイベントタイプ				|
| data    	|Intentメッセージタイプ  						|コールバックの関連情報、イベントデータ	|



####  サンプルコード  
```
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```


ルームに参加する前に、コールバック関数をSDKに登録する必要があります。
####  関数プロトタイプ 
```
ITMGContext public int SetTMGDelegate(ITMGDelegate delegate)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| delegate    |ITMGDelegate |SDKコールバック関数|

####  サンプルコード  
```
TMGContext.GetInstance(this).SetTMGDelegate(itmgDelegate);
```



### SDKの初期化
パラメータの取得については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはアプリ開発者によって定められ、アプリ内で繰り返さないようにします（現在INT64のみ対応）。
>!SDKを初期化してから、ルームに参加できます。
####  関数プロトタイプ

```
ITMGContext public int Init(String sdkAppId, String openID)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  |Tencent CloudコンソールからのsdkAppId番号				|
| openID    		|String  |OpenIDはInt64型（string型に変換して渡す）のみをサポートします。10000以上で、ユーザー識別用|

####  サンプルコード 


```
ITMGContext.GetInstance(this).Init(sdkAppId, openID);
```
### イベントコールバックのトリガ
updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。
####  関数プロトタイプ

```
ITMGContext int Poll()
```
####  サンプルコード
```
ITMGContext.GetInstance(this).Poll();
```

### システム一時停止
システムでPauseイベントが発生したら、Pauseを実行するようエンジンに通知する必要があります。
####  関数プロトタイプ

```
ITMGContext int Pause()
```

### システム回復
システムでResumeイベントが発生したら、Resumeを実行するようエンジンに通知する必要があります。
####  関数プロトタイプ

```
ITMGContext int Resume()
```



### SDKの逆初期化
SDKを逆初期化し、初期化されていない状態に入ります。アカウントの切り替えには、逆初期化が必要です。
#### 関数プロトタイプ

```
ITMGContext int Uninit()
```
####  サンプルコード
```
ITMGContext.GetInstance(this).Uninit();
```

## リアルタイムボイスルーム関連API
初期化後、SDKでルーム参加を呼び出しルームに参加してから、リアルタイムに音声電話をかけるようになります。

|API     | APIの意味   |
| ------------- |:-------------:|
|GenAuthBuffer    	|認証の初期化|
|EnterRoom   		|ルーム参加|
|IsRoomEntered   	|ルームに参加したか|
|ExitRoom 		|ルーム退出|
|ChangeRoomType 	|ユーザールームオーディオタイプの変更|
|GetRoomType 		|ユーザールームオーディオタイプの取得|


### 認証情報
関連機能の暗号化と認証に使用されるAuthBufferを生成します。関連バックグラウンド配置については、[認証暗号鍵](https://cloud.tencent.com/document/product/607/12218)を参照してください。    
オフラインボイスが認証を取得するときに、ルームIDパラメータをnullに入力する必要があります。

#### 関数プロトタイプ
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    		|int   		|Tencent CloudコンソールからのsdkAppId番号		|
| roomId    		|String   		|ルームID、127文字まで入力可能（オフラインボイスのルームIDパラメータにはnullを入力することが必要）|
| openID    	|String 	|ユーザーID					|
| key    		|string 	|Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme)からの暗号鍵				|


####  サンプルコード  
```
import com.tencent.av.sig.AuthBuffer;//ヘッダファイル
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,identifier, key);
```



### ルーム参加
生成した認証情報を用いてルームに参加するとき、コールバックとしてメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMが受信されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。戻り値がAV_OKの場合は成功です。


####  関数プロトタイプ
```
ITMGContext public abstract int EnterRoom(String roomId, int roomType, byte[] authBuffer)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId 	|String		|ルームID、127文字まで入力可能|
| roomType 	|int		|ルームオーディオタイプ|
| authBuffer	|byte[]	|認証コード|

ルームオーディオタイプについては、[音質選択](https://cloud.tencent.com/document/product/607/18522)を参照してください。


####  サンプルコード  
```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

### ルーム参加イベントのコールバック
ルームに参加した後、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージが送信され、OnEvent関数で判断します。

####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	 //ルーム参加完了イベント受信
        }
	}
```


### ルームに参加したかの判断
このAPIの呼び出しによってルームに参加したかを判断できます。戻り値はBOOL型です。
####  関数プロトタイプ  
```
ITMGContext public boolean IsRoomEntered()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).IsRoomEntered();
```

### ルーム退出
このAPIの呼び出しによって現在のルームから退出できます。これは非同期APIであり、戻り値がAV_OKの場合、非同期配信が完了したことを意味します。

>！アプリケーション内にルームから退出後すぐにルールに参加するシナリオがある場合、開発者はAPI呼び出しフローで、ExitRoomのRoomExitCompleteコールバック通知を待つ必要がなく、APIを直接呼び出すことが可能です。

#### 関数プロトタイプ  
```
ITMGContext public int ExitRoom()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).ExitRoom();
```

### ルーム退出コールバック
ルームから退出した後、コールバックがあります。メッセージがITMG_MAIN_EVENT_TYPE_EXIT_ROOMです。
####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            //ルーム退出完了イベント受信
        }
}
```

### ユーザールームオーディオタイプの変更
このAPIは、ユーザールームのオーディオタイプを変更するために使用されます。結果については、コールバックイベントを参照してください。イベントタイプはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。
####  関数プロトタイプ  
```
IITMGContext TMGRoom public void ChangeRoomType(int nRoomType)
```


|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| nRoomType    |int    |切り替えたいルームタイプ。ルームオーディオタイプについては、EnterRoom APIを参照してください|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetRoom().ChangeRoomType(nRoomType);
```


### ユーザールームオーディオタイプの取得
このAPIはユーザールームオーディオタイプの取得に使用され、戻り値はルームのオーディオタイプです。戻り値が0の場合、ユーザールームオーディオタイプの取得にエラーが発生したことを示します。ルームオーディオタイプについては、EnterRoom APIを参照してください。

####  関数プロトタイプ  
```
IITMGContext TMGRoom public  int GetRoomType()
```

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetRoom().GetRoomType();
```


### ルームタイプ設定完了コールバック
ルームタイプが設定された後、コールバックのイベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。返されたパラメータはresult、error_info、およびnew_room_typeです。new_room_typeによって表示される情報は以下の通りです。OnEvent関数でイベントメッセージを判断します。

|イベントサブタイプ     | 代表パラメータ   |意味|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM		|1 	|ルームに参加する過程で、持っているオーディオタイプが、ルームのタイプと一致しないため、そのルームのオーディオタイプに変更されたことを意味します	|
| ITMG_ROOM_CHANGE_EVENT_START			|2	|既にルームに参加し、オーディオタイプの切り替えが開始したことを意味します（例えば、ChangeRoomType APIを呼び出してから、オーディオタイプが切り替われます）|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE		|3	|既にルームに参加し、オーディオタイプの切り替えが完了したことを意味します|
| ITMG_ROOM_CHANGE_EVENT_REQUEST			|4	|ルームメンバーがChangeRoomType APIを呼び出し、ルームオーディオタイプの切り替えをリクエストすることを意味します|	


####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//ルームタイプ変更後の処理
	 }
}
```

### メンバー状態の変更
このイベントは、状態が変化すると通知されるが、状態が変化しないと通知されません。リアルタイムにメンバー状態を取得する必要があれば、上位が通知を受けたときにバッファに保存してください。イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEです。パラメータintentには、event_idとuser_listという2つの情報が含まれ、OnEvent関数でイベントメッセージを判断します。
オーディオイベントの通知にはしきい値があり、このしきい値を越えると通知が送信されます。オーディオパケットが2秒以上受信されないと、「オーディオパケットの送信を停止したメンバーがいる」というメッセージが送信されます。

|event_id     | 意味         |保守内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|ルームに参加したメンバーがいる			|アプリケーション側でメンバーリストを保守		|
|ITMG_EVENT_ID_USER_EXIT    				|ルームから退出したメンバーがいる			|アプリケーション側でメンバーリストを保守		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|オーディオパケットを送信したメンバーがいる		|アプリケーション側で通話メンバーリストを保守	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|オーディオパケットの送信を停止したメンバーがいる	|アプリケーション側で通話メンバーリストを保守	|

####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_USER_UPDATE == type)
        {
		//メンバー状態のアップデート
		int nEventID = data.getIntExtra("event_id", 0);
		String[] identifierList =data.getStringArrayExtra("user_list");
		 switch (nEventID)
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
	}
}
```

### 品質監視イベント
品質監視イベント、イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYです。返されたパラメータはweight、floss、およびdelayです。表示される情報は以下の通りです。OnEvent関数でイベントメッセージを判断します。

|パラメータ     | 意味         |
| ------------- |-------------|
|weight    				|範囲は1～50で、数値50の音質評点は優秀、数値1の音質評点は不可で、ほとんど使えません。数値0は初期値（意味なし）を示します|
|floss    				|パケットロス率|
|delay    		|オーディオ届け遅延時間（ms）|




### メッセージ詳細

|メッセージ     | メッセージの意味   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				       |音声ビデオルーム参加のメッセージ|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				         	|音声ビデオルーム退出のメッセージ|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		       |ネットワークなどによるルーム切断のメッセージ|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE				|ルームタイプ変更イベント|

### メッセージに対応するData詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|



## リアルタイムボイスオーディオAPI
SDKが初期化された後にルームに参加します。ルーム内に限り、リアルタイムオーディオボイスに関連するAPIを呼び出すことができます。
ユーザーインターフェースでマイク/スピーカーのオン/オフボタンをクリックする場合は、次のようにお勧めします。
- ほとんどのゲームアプリに対して、EnableMic APIおよびEnbaleSpeaker APIを呼び出すことをお勧めします。常にEnableAudioCaptureDevice/EnableAudioSend APIとEnableAudioPlayDevice/EnableAudioRecv APIを同時に呼び出すことと同等です。
- SNS系アプリなど、他のタイプのモバイルアプリでは収集デバイスをオンまたはオフすると、デバイス全体（収集と再生）が再起動します。このときアプリがBGMを再生している場合、BGMの再生も中断されます。マイクのオン/オフは、再生デバイスを中断せずに、上りリンクと下りリンクを制御することによって達成されます。具体的な呼び出し方法：ルームに参加するときに、EnableAudioCaptureDevice(true) && EnabledAudioPlayDevice(true)を1回呼び出します。マイクのオン/オフを切り替えるときに、EnableAudioSend/Recvのみを呼び出して、オーディオストリームの送受信を制御します。
- 収集デバイスまたは再生デバイスを個別にリリースする場合、EnableAudioCaptureDevice APIおよびEnableAudioPlayDevice APIを参照してください。
- pauseを呼び出して、オーディオエンジンを一時停止し、resumeを呼び出して、オーディオエンジンを再開します。

### SNS系アプリの呼び出しフロー図
![](https://main.qcloudimg.com/raw/53598680491501ab5a144e87ba932ccc.png)


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
####  関数プロトタイプ  
```
ITMGContext public void EnableMic(boolean isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |マイクをオンにする必要があれば、渡されたパラメータはtrueです。マイクをオフにすれば、パラメータはfalseです|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```

### マイク状態の取得
このAPIはマイク状態の取得に使用されます。戻り値0はマイクオフ状態で、戻り値1はマイクオン状態。
####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl int GetMicState() 
```
####  サンプルコード  
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicState();
```

### 収集デバイスのオン/オフ
このAPIは収集デバイスのオン/オフに使用されます。ルームに参加するときに、デバイスがデフォルトでオフです。
- このAPIは、ルームに参加した後にのみ呼び出すことができます。ルームから退出した後デバイスは自動的にオフになります。
- モバイル側で、収集デバイスをオンにすると、通常に権限申請、音量タイプの調整などが必要です。

####  関数プロトタイプ  
```
ITMGContext public int EnableAudioCaptureDevice(boolean isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |収集デバイスをオンにする必要があれば、渡されたパラメータはtrueです。収集デバイスをオフにすれば、パラメータはfalseです|

#### サンプルコード

```
打开采集设备
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 収集デバイス状態の取得
このAPIは収集デバイス状態の取得に使用されます。
#### 関数プロトタイプ

```
ITMGContext public boolean IsAudioCaptureDeviceEnabled()
```
#### サンプルコード

```
bool IsAudioCaptureDevice =ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### オーディオ上りリンクのオン/オフ
このAPIはオーディオ上りリンクのオン/オフに使用されます。収集デバイスがオンの場合、収集されたオーディオデータが送信されます。収集デバイスがオフの場合、音声なしのままとなります。収集デバイスのオン/オフについては、API EnableAudioCaptureDeviceを参照してください。

#### 関数プロトタイプ

```
ITMGContext public int EnableAudioSend(boolean isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |オーディオ上りリンクをオンにする必要があれば、渡されたパラメータはtrueです。オーディオ上りリンクをオフにすれば、パラメータはfalseです|

#### サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioSend(true);
```

### オーディオ上りリンク状態の取得
このAPIはオーディオ上りリンク状態の取得に使用されます。
#### 関数プロトタイプ  
```
ITMGContext TMGAudioCtrl boolean IsAudioSendEnabled()
```
####  サンプルコード  
```
bool IsAudioSend =  =ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioSendEnabled();
```

### マイクリアルタイム音量の取得
このAPIはマイクリアルタイム音量の取得に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl int GetMicLevel() 
```
####  サンプルコード  
```
int micLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicLevel();
```

### マイク音量の設定
このAPIはマイク音量の設定に使用されます。パラメータvolumeはマイク音量の設定に使用され、数値が0の場合はミュート状態を示し、100の場合は音量が変更されないことを示します。デフォルト数値は100です。

####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl int SetMicVolume(int volume) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int      |音量設定、範囲0～200|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().SetMicVolume(volume);
```
###  マイク音量の取得
このAPIはマイク音量の取得に使用され、戻り値はint型の数値です。戻り値が101の場合、API SetMicVolumeを呼び出したことがないことを意味します。

#### 関数プロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetMicVolume()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetMicVolume();
```

### スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  関数プロトタイプ  
```
ITMGContext public void EnableSpeaker(boolean isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |スピーカーをオフにする必要があれば、渡されたパラメータはfalseです。スピーカーをオンにすれば、パラメータはtrueです|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

### スピーカー状態の取得
このAPIはスピーカー状態の取得に使用されます。戻り値0はスピーカーオフ状態、戻り値1はスピーカーオン状態、戻り値2はスピーカーデバイス動作中を示します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetSpeakerState() 
```

####  サンプルコード  
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerState();
```



再生デバイスのオン/オフ
このAPIは再生デバイスのオン/オフに使用されます。

#### 関数プロトタイプ  
```
ITMGContext public int EnableAudioPlayDevice(boolean isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean        |再生デバイスをオフにする必要があれば、渡されたパラメータはfalseです。再生デバイスをオンにすれば、パラメータはtrueです|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 再生デバイス状態の取得
このAPIは再生デバイス状態の取得に使用されます。
#### 関数プロトタイプ

```
ITMGContext public int IsAudioPlayDeviceEnabled()
```
#### サンプルコード  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### オーディオ下りリンクのオン/オフ
このAPIはオーディオ下りリンクのオン/オフに使用されます。再生デバイスがオンになっているとき、ルーム内の他の人のオーディオデータを再生します。再生デバイスがオフになっているとき、音声なしのままとなります。再生デバイスのオン/オフについては、API EnableAudioPlayDeviceを参照してください。

#### 関数プロトタイプ  

```
ITMGContext public int EnableAudioRecv(boolean isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |オーディオ下りリンクをオンにする必要があれば、渡されたパラメータはtrueです。オーディオ下りリンクをオフにすれば、パラメータはfalseです|

#### サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioRecv(true);
```



### オーディオ下りリンク状態の取得
このAPIはオーディオ下りリンク状態の取得に使用されます。
#### 関数プロトタイプ  
```
ITMGContext TMGAudioCtrl public boolean IsAudioRecvEnabled()
```

####  サンプルコード  
```
bool IsAudioRecv = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioRecvEnabled();
```

### スピーカーリアムタイム音量の取得
このAPIはスピーカーリアムタイム音量の取得に使用されます。戻り値はint型で、スピーカーのリアルタイム音量を表示します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetSpeakerLevel() 
```

####  サンプルコード  
```
int SpeakLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerLevel();
```

### スピーカー音量の設定
このAPIはスピーカー音量の設定に使用されます。
パラメータvolumeはスピーカー音量の設定に使用され、数値が0の場合はミュート状態を示し、100の場合は音量が変更されないことを示します。デフォルト数値は100です。

####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl public int SetSpeakerVolume(int volume) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int        |音量設定、範囲0～200|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().SetSpeakerVolume(volume);
```

### スピーカー音量の取得

このAPIはスピーカー音量の取得に使用されます。戻り値はint型の数値でスピーカー音量を示します。戻り値が101の場合、API SetSpeakerVolumeを呼び出したことがないことを意味します。
Levelはリアルタイム音量で、Volumeはスピーカーの音量です。最終音声の音量はLevel*Volume%に相当します。例えば、リアルタイム音量数値が100の場合、このときのVolumeの数値が60で、最終に出た音声の数値も60です。

####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetSpeakerVolume()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerVolume();
```


### インイヤーモニターの起動
このAPIはインイヤーモニターの起動に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioCtrl public int EnableLoopBack(boolean enable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |boolean         |起動要否を設定する|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableLoopBack(true);
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

####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int StartAccompany(String filePath, boolean loopBack, int loopCount) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    	|String    	|伴奏再生パス					|
| loopBack  	|boolean    	|ミキシング有無の送信。通常trueに設定されます。つまり、他人にも伴奏が聞こえる	|
| loopCount	|int    		|ループ数。数値は-1であれば無限ループを示す	|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StartAccompany(filePath,true,loopCount,duckerTimeMs);
```

### 伴奏再生のコールバック
伴奏再生の開始が完了した後、コールバック関数はOnEventを呼び出し、イベントメッセージはITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISHです。OnEvent関数でイベントメッセージを判断します。
渡されたパラメータintentには、resultとfile_pathという2つの情報が含まれています。
####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH == type)
        {
		//伴奏再生のイベントコールバック
	}
}
```

### 伴奏再生の停止
このAPIを呼び出して、伴奏の再生を停止します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int StopAccompany(int duckerTimeMs)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| duckerTimeMs    |int             |フェード時間|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StopAccompany(duckerTimeMs);
```

### 伴奏の再生が完了したか
再生が完了したとき、戻り値はtrue、再生が完了していないとき、戻り値はfalse。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public boolean IsAccompanyPlayEnd() 
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().IsAccompanyPlayEnd();
```


### 伴奏再生の一時停止
このAPIを呼び出して、伴奏の再生を一時停止します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int PauseAccompany()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PauseAccompany();
```


### 伴奏再生の再開
このAPIは伴奏再生の再開に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int ResumeAccompany()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().ResumeAccompany();
```



### 伴奏音量の設定
伴奏音量を設定します。デフォルト値は100です。数値が100以上の場合、音量は増加し、数値が100以下の場合、音量は減少します。値範囲は0～200です。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int SetAccompanyVolume(int vol)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int             |音量値|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetAccompanyVolume(Volume);
```

### 伴奏再生音量の取得
このAPIは伴奏音量の取得に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int GetAccompanyVolume()
```
####  サンプルコード  
```
string currentVol = "VOL: " + ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetAccompanyVolume();
```

### 伴奏再生進捗の取得
伴奏の再生進捗を取得するには、次の2つのAPIを使用します。注意：Current/Total =現在のループ回数、Current％Total =現在のループ再生位置。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public long GetAccompanyFileTotalTimeByMs()
ITMGContext TMGAudioEffectCtrl public long GetAccompanyFileCurrentPlayedTimeByMs()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetAccompanyFileTotalTimeByMs();
ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetAccompanyFileCurrentPlayedTimeByMs();
```


### 再生進捗の設定
このAPIは再生進捗の設定に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int SetAccompanyFileCurrentPlayedTimeByMs(long time)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| time    |long                |再生進捗、ミリ秒単位|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetAccompanyFileCurrentPlayedTimeByMs(time);
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
このAPIは効果音の再生に使用されます。パラメータ内の効果音IDはアプリ側で管理される必要があり、IDは1回の独立した再生イベントを表します。この再生はこのIDで制御できます。ファイルはm4a、wav、およびmp3という3つのフォーマットをサポートします。
#### 関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int PlayEffect(int soundId, String filePath, boolean loop) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    	|int    		|効果音ID|
| filePath    	|String		|効果音パス|
| loop    		|boolean	|繰り返し再生の要否|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PlayEffect(soundId,filePath,loop);
```


### 効果音再生の一時停止
このAPIは効果音再生の一時停止に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int PauseEffect(int soundId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PauseEffect(soundId);
```

### すべての効果音再生の一時停止
このAPIを呼び出して、すべての効果音を一時停止します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int PauseAllEffects()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PauseAllEffects();
```

### 効果音再生の再開
このAPIは効果音再生の再開に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int ResumeEffect(int soundId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().ResumeEffect(soundId);
```



### すべての効果音再生の再開
このAPIを呼び出して、すべての効果音の再生を再開します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int ResumeAllEffects()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().ResumeAllEffects();
```

### 効果音再生の停止
このAPIは効果音再生の停止に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int StopEffect(int soundId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StopEffect(soundId);
```

### すべての効果音再生の停止
このAPIを呼び出して、すべての効果音の再生を停止します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int StopAllEffects()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StopAllEffects();
```

### ボイス変更特効
このAPIを呼び出して、ボイス変更特効を設定します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl  public int setVoiceType(int type);
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| type    |int                    |ローカル側のボイス変更タイプを示す|


|タイプパラメータ     |パラメータ例|意味|
| ------------- |-------------|------------- |
|ITMG_VOICE_TYPE_ORIGINAL_SOUND  		|0	|原音			|
|ITMG_VOICE_TYPE_LOLITA    				|1	|ロリ			|
|ITMG_VOICE_TYPE_UNCLE  				|2	|おじさん			|
|ITMG_VOICE_TYPE_INTANGIBLE    			|3	|ファンタジー			|
|ITMG_VOICE_TYPE_DEAD_FATBOY  			|4	|デブ			|
|ITMG_VOICE_TYPE_HEAVY_MENTA			|5	|ヘビーメタル			|
|ITMG_VOICE_TYPE_DIALECT 				|6	|外国人			|
|ITMG_VOICE_TYPE_INFLUENZA 				|7	|風邪			|
|ITMG_VOICE_TYPE_CAGED_ANIMAL 			|8	|絶望			|
|ITMG_VOICE_TYPE_HEAVY_MACHINE			|9	|ヘビーマシン			|
|ITMG_VOICE_TYPE_STRONG_CURRENT			|10	|強電流			|
|ITMG_VOICE_TYPE_KINDER_GARTEN			|11	|幼稚園			|
|ITMG_VOICE_TYPE_HUANG 					|12	|ミニオン			|


####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().setVoiceType(0);
```

### カラオケ特別効果音
このAPIを呼び出して、カラオケ特別効果音を設定します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl  public int SetKaraokeType(int type);
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

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetKaraokeType(0);
```

### 効果音再生音量の取得
効果音再生の音量を取得します。リニア音量で、デフォルト値は100です。数値が100以上の場合、音量は増加し、数値が100以下の場合、音量は減少します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int GetEffectsVolume()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().GetEffectsVolume();
```


### 効果音再生音量の設定
このAPIを呼び出して、効果音の再生音量を設定します。
####  関数プロトタイプ  
```
ITMGContext TMGAudioEffectCtrl public int SetEffectsVolume(int volume)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int                    |音量値|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioEffectCtrl().SetEffectsVolume(Volume);
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
|GetMicLevel|オフラインボイスマイクリアルタイム音量の取得	|
|GetSpeakerLevel|オフラインボイススピーカーリアムタイム音量の取得	|
|UploadRecordedFile 	|ボイスファイルのアップロード		|
|DownloadRecordedFile	|ボイスファイルのダウンロード		|
|PlayRecordedFile 	|ボイスの再生		|
|StopPlayFile		|ボイス再生の停止		|
|GetFileSize 		|ボイスファイルのサイズ		|
|GetVoiceFileDuration	|ボイスファイルの時間		|
|SpeechToText 		|ボイスのテキスト認識		|

### 認証の初期化
認証初期化は、SDKの初期化後に呼び出されます。authBufferの取得については、上記のリアルタイムボイス認証情報APIを参照してください。
#### 関数プロトタイプ  
```
ITMGContext TMGPTT public void ApplyPTTAuthbuffer(String authBuffer)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |String                    |認証|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
```

### ボイスメッセージ最大時間の制限
ボイスメッセージの最大長さを制限し、最大60秒。

####  関数プロトタイプ

```
ITMGContext TMGPTT public void SetMaxMessageLength(int msTime)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |ボイス時間、単位はms|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SetMaxMessageLength(msTime);
```


### 録音の起動
このAPIは録音の起動に使用されます。ボイスのテキスト変換操作を実行する前に、録音ファイルをアップロードする必要があります。
####  関数プロトタイプ  
```
ITMGContext TMGPTT public void StartRecording(String filePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                     |ボイスの保存パス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().StartRecording(filePath);
```

### 録音起動のコールバック
録音の起動が完了した後、コールバックはOnEvent関数を呼び出します。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
渡されたパラメータには、resultとfile_pathという2つの情報が含まれています。

####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE == type)
        	{
            		//録音起動のコールバック
        	}
}
```

### ストリーミングボイス認識の起動
このAPIはストリーミングボイス認識の起動に使用されます。その同時にコールバックには、リアルタイムのボイス変換テキストが返されます。言語を指定して認識することができ、ボイスで認識された情報を指定された言語に翻訳して返すこともできます。

#### 関数プロトタイプ  

```
ITMGContext TMGPTT public int StartRecordingWithStreamingRecognition (String filePath)
ITMGContext TMGPTT public int StartRecordingWithStreamingRecognition(String filePath,String speechLanguage,String translateLanguage) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath			|String	|ボイスの保存パス	|
| speechLanguage    		|String	|指定したテキストの言語パラメータに識別します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください|
| translateLanguage	|String	|指定したテキストの言語パラメータに翻訳します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください。（このパラメータは一時的に無効です。speechLanguageと同じのパラメータを入力してください）|

#### サンプルコード  
```
String  temple = getActivity().getExternalFilesDir(null).getAbsolutePath() + "/test_"+(index++)+".ptt";
ITMGContext.GetInstance(getActivity()).GetPTT().StartRecordingWithStreamingRecognition(temple,"cmn-Hans-CN","cmn-Hans-CN");
```

### ストリーミングボイス認識起動のコールバック
ストリーミングボイス認識の起動が完了した後、コールバックはOnEvent関数を呼び出します。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETEです。OnEvent関数でイベントメッセージを判断します。渡されたパラメータには、次の4つの情報が含まれています。

|メッセージ名称     | 意味         |
| ------------- |:-------------:|
| result    	|ストリーミングボイス認識が完了したかどうかを判断するための戻りコード		|
| text    		|ボイステキスト変換で認識されたテキスト	|
| file_path 	|録音を保存するローカルアドレス		|
| file_id 		|バックグラウンドでの録音のURLアドレス	|

|エラーコード     | 意味         |処理方法|
| ------------- |:-------------:|:-------------:|
|32775	|ストリーミングボイステキスト変換に失敗しましたが、録音に成功しました	|UploadRecordedFile APIを呼び出して録音をアップロードしてから、SpeechToText APIを呼び出して、ボイステキスト変換操作を行います
|32777	|ストリーミングボイステキスト変換に失敗しましたが、録音とアップロードに成功しました	|返された情報には、アップロードに成功したバックグラウンドURLアドレスが含まれています。SpeechToText APIを呼び出して、ボイステキスト変換操作を行います

#### サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE == type)
        	{
            		//ストリーミング起動のコールバック
        	}
}
```


### 録音の停止
このAPIは録音の停止に使用されます。このAPIは非同期APIで、記録を停止すると、録音完成のコールバックが送信されます。成功した場合のみ、録音ファイルを利用できます。
#### 関数プロトタイプ  
```
ITMGContext TMGPTT public int StopRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().StopRecording();
```



### 録音のキャンセル
このAPIを呼び出して、録音をキャンセルします。キャンセルした後、コールバックが送信されません。
#### 関数プロトタイプ  
```
ITMGContext TMGPTT public int CancelRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().CancelRecording();
```

### オフラインボイスマイクリアルタイム音量の取得
このAPIはマイクリアルタイム音量の取得に使用されます。戻り値はint型で、戻り値の範囲は0から100です。

#### 関数プロトタイプ  
```
ITMGContext TMGPTT public int GetMicLevel()
```
#### サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetMicLevel();
```


### スピーカーリアムタイム音量の取得
このAPIはスピーカーリアルタイム音量の取得に使用されます。戻り値はint型で、戻り値の範囲は0から100です。

#### 関数プロトタイプ  
```
ITMGContext TMGPTT public int GetSpeakerLevel()
```

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetSpeakerLevel();
```






### ボイスファイルのアップロード
このAPIはボイスファイルのアップロードに使用されます。
#### 関数プロトタイプ  
```
ITMGContext TMGPTT public void UploadRecordedFile(String filePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                      |ボイスのアップロードパス|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().UploadRecordedFile(filePath);
```


### ボイスアップロード完成のコールバック
ボイスのアップロードが完了した後、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
渡されたパラメータには、result、file_path、およびfile_idという3つの情報が含まれています。
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE== type)
       	 {
           	//ボイスアップロード完成のコールバック
       	 }
}
```


### ボイスファイルのダウンロード
このAPIはボイスファイルのダウンロードに使用されます。
#### 関数プロトタイプ  
```
ITMGContext TMGPTT public void DownloadRecordedFile(String fileID, String downloadFilePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    			|String                      |ファイルのURLパス	|
| downloadFilePath 	|String                      |ファイルのローカル保存パス	|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().DownloadRecordedFile(url,path);
```


### ボイスファイルダウンロード完了のコールバック
ボイスのダウンロードが完了した後、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
渡されたパラメータには、result、file_path、およびfile_idという3つの情報が含まれています。

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE== type)
        {
            //ダウンロード成功        
	}
}
```



### ボイスの再生
このAPIはボイスの再生に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGPTT public int PlayRecordedFile(String downloadFilePath) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| downloadFilePath    |String   |ファイルパス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().PlayRecordedFile(downloadFilePath);
```


### ボイス再生のコールバック
ボイス再生のコールバック。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
渡されたパラメータには、resultとfile_pathという2つの情報が含まれています。
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE== type)
       	 	{
			//ボイス再生のコールバック 
		}
}
```




### ボイス再生の停止
このAPIはボイス再生の停止に使用されます。
####  関数プロトタイプ  
```
ITMGContext TMGPTT public int StopPlayFile()
```

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().StopPlayFile();
```



### ボイスファイルサイズの取得
このAPIによって、ボイスファイルのサイズを取得します。
####  関数プロトタイプ  
```
ITMGContext TMGPTT public int GetFileSize(String filePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                     |ボイスファイルのパス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetFileSize(path);
```

### ボイスファイル時間の取得
このAPIはボイスファイル時間の取得に使用され、単位はミリ秒です。
####  関数プロトタイプ  
```
ITMGContext TMGPTT public int GetVoiceFileDuration(String filePath)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                     |ボイスファイルのパス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetVoiceFileDuration(path);
```


### 指定ボイスファイルのテキスト認識
このAPIは指定されたボイスファイルをテキストに認識するために使用されます。

#### 関数プロトタイプ  
```
ITMGContext TMGPTT public int SpeechToText(String fileID)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |String                     |ボイスファイルURL|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID);
```



### 指定ボイスファイルのテキスト翻訳（指定言語）
このAPIは指定されたボイスファイルを指定言語のテキストに翻訳するために使用されます。

#### 関数プロトタイプ  
```
ITMGContext TMGPTT public int SpeechToText(String fileID,String speechLanguage,String translateLanguage)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |String                     |ボイスファイルURL|
| speechLanguage    |String                    |指定したテキストの言語パラメータに識別します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください|
| translatelanguage    |String                    |指定したテキストの言語パラメータに翻訳します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください。（このパラメータは一時的に無効です。入力したパラメータはspeechLanguageと一致する必要があります）|

#### サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID,"cmn-Hans-CN","en-US");
```



### 認識コールバック
指定されたボイスファイルをテキストに認識するコールバック。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
渡されたパラメータには、result、file_path、およびtextという3つの情報が含まれています。ここで、textは認識されたテキストです。
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE == type)
       	 {
            //ボイスファイル認識成功       
	 }
}
```



## 高度なAPI

### バージョン番号の取得
分析のために、SDKバージョン番号を取得します。
#### 関数プロトタイプ
```
ITMGContext public void GetSDKVersion()
```
#### サンプルコード  
```
ITMGContext.GetInstance(this).GetSDKVersion();
```

### プリントするログレベルの設定
プリントするログレベルの設定に使用されます。デフォルトのレベルにすることをお勧めします。
#### 関数プロトタイプ
```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

|パラメータ| タイプ|意味|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|ログ書き込みのレベルを設定します。TMG_LOG_LEVEL_NONEは書き込まないことを意味します|
|levelPrint|ITMG_LOG_LEVEL|プリントするログレベルを設定します。TMG_LOG_LEVEL_NONEはプリントしないことを意味します|



|ITMG_LOG_LEVEL|意味|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0		|ログをプリントしない			|
|TMG_LOG_LEVEL_ERROR=1		|エラーログをプリント（デフォルト）	|
|TMG_LOG_LEVEL_INFO=2			|プロンプトログをプリント		|
|TMG_LOG_LEVEL_DEBUG=3		|開発デバッグログをプリント	|
|TMG_LOG_LEVEL_VERBOSE=4		|高頻度ログをプリント		|

#### サンプルコード  
```
ITMGContext.GetInstance(this).SetLogLevel(1,true,true);
```



### プリントするログのパスの設定
プリントするログのパスの設定に使用します。デフォルトのパスは/sdcard/Android/data/xxx.xxx.xxx/files。
#### 関数プロトタイプ
```
ITMGContext int SetLogPath(String logDir)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| logDir    		|String   		|パス|

#### サンプルコード  
```
ITMGContext.GetInstance(this).SetLogPath(path);
```


### 診断情報の取得
音声テレビ通話のリアルタイムの通話品質に関する情報を取得します。このAPIは、主にリアルタイムの通話品質の確認、トラブルシューティングなどに使用され、サービス側で無視してもかまいません。
#### 関数プロトタイプ  
```
IITMGContext TMGRoom public String GetQualityTips() 
```
#### サンプルコード  
```
ITMGContext.GetInstance(this).GetRoom().GetQualityTips();
```

### オーディオデータのブラックリストに追加
あるIDをオーディオデータブラックリストに追加します。戻り値が0の場合、呼び出し成功を表します。
#### 関数プロトタイプ  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |String      |ブラックリストに追加するID|

#### サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().AddAudioBlackList(openId);
```

### オーディオデータのブラックリストから削除
あるIDをオーディオデータブラックリストから削除します。戻り値が0の場合、呼び出成功を表します。
#### 関数プロトタイプ  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(String openId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |String      |ブラックリストから削除するID|

#### サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().RemoveAudioBlackList(openId);
```


## コールバックメッセージ

#### メッセージリスト：

|メッセージ     | メッセージの意味   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|ボイスルーム参加のメッセージ		|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|ボイスルーム退出のメッセージ		|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT		|ネットワークなどによるルーム切断のメッセージ	|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE		|ルームタイプ変更イベント		|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH		|伴奏終了のメッセージ			|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE		|ルームメンバーアップデートのメッセージ		|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE	|PTT録音完了			|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE	|PTTアップロード完了			|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|PTTダウンロード完了			|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		|PTT再生完了			|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|ボイステキスト変換完了			|

#### Dataリスト：

|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|result; error_info			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|result; error_info  			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    	|result; error_info; sub_event_type; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"スピーカー (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"スピーカー (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"マイク (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    	|result; error_info 			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"マイク (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    		|user_list;  event_id			|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE 	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|result; text;file_id		|{"file_id":"","text":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE	|result; file_path; text;file_id		|{"file_id":"","file_path":","text":"","result":0}|

