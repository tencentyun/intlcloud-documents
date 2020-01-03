Androidを使う開発者がTencent CloudのGaming Multimedia Engine製品のAPIに対するデバッグ・アクセスを行いやすいように、ここで、Androidでの開発に向けるアクセス技術のドキュメントについて説明させていただきます。

>このドキュメントはGME sdk version：2.5に対応しています。

## GME利用上の重要事項

|重要なインターフェース     | インターフェースの意味|
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|EnterRoom |入室します  |
|EnableMic |マイクをオンにします |
|EnableSpeaker|スピーカーをオンにします |

>
- GMEを利用する前にプロジェクトを構成してください、構成しないの場合、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKであり、数値は0です。
- GMEのインターフェースの呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには、認証が必要です。本ドキュメントの認証に関する内容をご参照ください。
- GMEは周期的にPollインターフェースを呼び出して、イベントのコールバックをトリガーする必要があります。
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、先に入室に成功する必要があります。
- エラーコードの詳細について、[エラーコード](https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。

## リアルタイム音声のフローチャート
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 関連インターフェースの初期化
初期化が実施される前に、SDKは未初期化の状態です。リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
- 利用上の問題について、[一般的な問題](https://intl.cloud.tencent.com/document/product/607/30254)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |


### シングルトンの取得
音声機能を使用する場合、先にITMGContextオブジェクトを取得する必要があります。
####  関数のプロトタイプ 

```
public static ITMGContext GetInstance(Context context)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| context    |Context |アプリケーションのコンテキストオブジェクト|


####  サンプルコード  

```
import com.tencent.TMG.ITMGContext; 
TMGContext.getInstance(this);
```

### コールバックの登録
インターフェースクラスは、Delegateメソッドを使用して、アプリケーションにコールバック通知を送信します。コールバック関数をSDKに登録して、コールバック情報を受信します。

####  サンプルコード 
```
private ITMGContext.ITMGDelegate itmgDelegate = null;
```
コンストラクターでこのコールバック関数をオーバーライドして、コールバックのパラメータを処理させます。

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:| ------------- |
| type    |ITMGContext.ITMG_MAIN_EVENT_TYPE |コールバックのイベントタイプ|
| data    |Intent メッセージタイプ  |コールバックの関連情報、イベントデータ|



####  サンプルコード  
```
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```


コールバック関数をSDKに登録するには、入室する前に設定する必要があります。
####  関数のプロトタイプ 
```
ITMGContext public int SetTMGDelegate(ITMGDelegate delegate)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| delegate    |ITMGDelegate |SDK コールバック関数|

####  サンプルコード  
```
TMGContext.GetInstance(this).SetTMGDelegate(itmgDelegate);
```



### SDKの初期化

パラメータの取得について、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースは、Tencent CloudコンソールからのSDKAppID番号をパラメータとして、さらにopenIdを付け加える必要があります。このopenIdはユーザーを識別するための一意のもので、ルールはApp開発者によって設定され、App内で重複しなければよいです（現在はINT64のみをサポートします）。
>入室するには、先にSDKを初期化する必要があります。
>
>####  関数のプロトタイプ

```
ITMGContext public int Init(String sdkAppId, String openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |String  |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |String  |openIdはInt64型のみをサポートします（stringに変換されて渡される）。openIdは10000よりも大きくする必要があり、ユーザーの識別に使用されます。|

####  サンプルコード 


```
ITMGContext.GetInstance(this).Init(sdkAppId, openId);
```
### イベントコールバックをトリガーする
updateの中で、Pollを周期的に呼び出すことで、イベントコールバックをトリガーすることができます。
####  関数のプロトタイプ

```
ITMGContext int Poll()
```
####  サンプルコード
```
ITMGContext.GetInstance(this).Poll();
```

### システムの一時停止
システムにPauseイベントが発生した場合、エンジンに通知して、Pauseを実行させる必要があります。
####  関数のプロトタイプ

```
ITMGContext int Pause()
```

### システムリカバー
システムにResumeイベントが発生した場合、エンジンに通知して、Resumeを実行させる必要があります。Resumeインターフェースはリアルタイム音声のみをリカバーします。
####  関数のプロトタイプ

```
ITMGContext int Resume()
```



### SDKの未初期化
SDKを未初期化して、未初期化状態にします。アカウントを切り替えるには未初期化にする必要があります。
####  関数のプロトタイプ

```
ITMGContext int Uninit()
```
####  サンプルコード
```
ITMGContext.GetInstance(this).Uninit();
```

## リアルタイム音声ルームの関連インターフェース
リアルタイム音声通話を行うには、初期化してから、SDKの入室インタフェースを呼び出して、入室する必要があります。
利用上の問題については、[リアルタイム音声の関連問題](https://intl.cloud.tencent.com/document/product/607/30257)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|GenAuthBuffer    |認証を初期化します|
|EnterRoom   |入室します|
|IsRoomEntered   |入室していますか|
|ExitRoom |退室します|
|ChangeRoomType |ユーザールームのオーディオタイプを変更する|
|GetRoomType |ユーザールームのオーディオタイプを取得する|


### 認証情報
AuthBufferを生成し、関連機能の暗号化と認証に使用します。関連バックグラウンドのデプロイについて[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
オフライン音声取得の認証を行うとき、ルーム番号のパラメータをnullに設定する必要があります。

####  関数のプロトタイプ
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent CloudコンソールからのsdkAppId番号です|
| roomId    |string   |ルーム番号、最大127文字まで（オフライン音声ルーム番号のパラメータをnullに設定する必要があります。）|
| openID    |string |ユーザー識別です|
| key    |string |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|


####  サンプルコード  
```
import com.tencent.av.sig.AuthBuffer;//ヘッダーファイル
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,identifier, key);
```



### 入室
生成された認証情報を使って入室した場合、メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMのコールバックを受信します。入室した際に、マイクとスピーカーはデフォルトでオフになっています。戻り値がAV_OKの場合、入室に成功したことを示しています。


####  関数のプロトタイプ
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId|string    |ルーム番号、最大127文字までをサポートします|
| roomType |int|ルームのオーディオタイプです|
| authBuffer |Byte[] |認証コードです|

ルームのオーディオタイプについては、[音質選択](https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

## 入室イベントのコールバック
入室してから、メッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMを送信し、OnEvent関数において判断します。

####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	 / /入室成功イベントを受信した
        }
	}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|


### 入室したかを判断する
このインターフェースを呼び出すことで、入室したかを判断できます。戻り値はbool値です。
####  関数のプロトタイプ  
```
ITMGContext public boolean IsRoomEntered()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).IsRoomEntered();
```

### 退室
このインターフェースを呼び出すことで、ルームから退出できます。このインターフェースは非同期であり、戻り値がAV_OKの場合は、非同期送信が成功したことを示します。

>アプリケーション中に退室してから、またすぐに入室する場合、インターフェースの呼び出しでは、開発者がExitRoomのRoomExitCompleteコールバック通知を待つ必要がなく、インターフェースを直接に呼び出せばよいです。

####  関数のプロトタイプ  
```
ITMGContext public int ExitRoom()
```
####  サンプルコード  
```
ITMGContext.GetInstance().ExitRoom();
```

### 退室のコールバック
退室してからは、メッセージがITMG_MAIN_EVENT_TYPE_EXIT_ROOMのコールバックが発生します。
####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            //退室成功イベントを受信した
        }
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|


### ユーザールームのオーディオタイプの変更
このインターフェースは、ユーザールームのオーディオタイプの変更に使用されます。その結果については、コールバックイベントをご参照てください。イベントタイプはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。
####  関数のプロトタイプ  
```
IITMGContext TMGRoom public void ChangeRoomType(int nRoomType)
```


|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| nRoomType    |int    |切り替えたいルームタイプです。ルームのオーディオタイプについて、EnterRoomインターフェースをご参照ください|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetRoom().ChangeRoomType(nRoomType);
```


### ユーザールームのオーディオタイプの取得
このインターフェースはユーザールームのオーディオタイプを取得するために使用されます、戻り値はルームのオーディオタイプです。戻り値が0の場合は、ユーザールームのオーディオタイプの取得にエラーが発生したことを示します。ルームのオーディオタイプについてEnterRoomインターフェースをご参照ください。

####  関数のプロトタイプ  
```
IITMGContext TMGRoom public  int GetRoomType()
```

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetRoom().GetRoomType();
```


### ルームタイプ設定完了のコールバック
ルームタイプの設定が完了した後、コールバックのイベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEであり、返されたパラメータはresult、error_infoおよびnew_room_typeです。new_room_typeは次の情報を示し、OnEvent関数でイベントメッセージを判断します。

|イベントのサブタイプ     | 代表的パラメータ   |意味|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |入室する際に、固有のオーディオタイプがルームタイプと一致しないため、入室したルームのオーディオタイプに変更されました|
| ITMG_ROOM_CHANGE_EVENT_START|2|入室済みで、オーディオタイプ切り替え中です（例えば、ChangeRoomTypeインターフェースを呼び出してオーディオタイプを切り替えます）|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|入室済みで、オーディオタイプは切り替え済みです|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|ルームメンバーがChangeRoomTypeインターフェースを呼び出し、ルームのオーディオタイプの切り替えをリクエストしています|


####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//ルームタイプイベントの処理
	 }
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


### メンバー状態の変化
このイベントは、状態の変更があった場合にのみ通知します、変更がない場合は、通知されません。リアルタイムでメンバー状態を取得する場合は、上位層が通知を受ける時にキャッシュしてください。イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEであり、ここでは、dataにevent_idとuser_listの2つの情報が含まれており、OnEvent関数でイベントメッセージを判断します。
オーディオイベントの通知にしきい値があり、そのしきい値を超えた場合に通知します。2秒を超えてもオーディオパッケージを受信していない場合にのみ、「メンバーがオーディオパッケージの送信を停止しました」の通知を送信します。

|event_id     | 意味         |アプリケーション側のメンテナンス内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |メンバーが入室しました|アプリケーション側でメンバーリストをメンテナンスします|
|ITMG_EVENT_ID_USER_EXIT    |メンバーが退室しました|アプリケーション側でメンバーリストをメンテナンスします|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |メンバーがオーディオパッケージを送信しています|アプリケーション側で通信メンバーのリストをメンテナンスします|
|ITMG_EVENT_ID_USER_NO_AUDIO    |メンバーがオーディオパッケージの送信を停止しました|アプリケーション側で通信メンバーのリストをメンテナンスします|

####  サンプルコード  

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_USER_UPDATE == type)
        {
		//メンバー状態の更新
		int nEventID = data.getIntExtra("event_id", 0);
		String[] identifierList =data.getStringArrayExtra("user_list");
		 switch (nEventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //メンバーが入室しました
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //メンバーが退室しました
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //メンバーがオーディオパッケージを送信します
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //メンバーがオーディオパッケージの送信を停止しました
			    break;
		    default:
			    break;
 		    }
	}
}
```

### 品質監視イベント
品質監視イベントであり、イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYで、返されたパラメータはweight、flossおよびdelayです。次の情報を示し、OnEvent関数でイベントメッセージを判断します。

|パラメータ     | 意味        |
| ------------- |-------------|
|weight    |範囲は1～5であり、値5はきわめて高い音質を示し、値1は使用できないほどの低い音質を示します。値0はデフォルト値を示し、意味はありません|
|floss    |パケットロス率|
|delay    |オーディオ到達のディレー時間（ms）|




### メッセージの詳細

|メッセージ    | メッセージの意味 |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |オーディオ・ビデオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオ・ビデオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネットワークなどの原因により、ルームへの接続が切断されました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|ルームタイプ変更イベントです|

### メッセージに対応するDataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


## リアルタイム音声のオーディオインターフェース
SDKを初期化し入室した場合にのみ、ルーム内でリアルタイム音声の関連インターフェースを呼び出すことができます。
ユーザーインターフェースでマイク/スピーカーのオン/オフボタンをクリックするとき、以下の方法をお勧めします。
- 大部分のゲームAppに対しては、EnableMicとEnableSpeakerインターフェースを呼び出すことを推奨します。これは、常にEnableAudioCaptureDevice/EnableAudioSendとEnableAudioPlayDevice/EnableAudioRecvインターフェースの両方を同時に呼び出すことに相当します。
-  ほかのタイプのモバイル端末App（例えばソーシャルApp）で採集デバイスをオン/オフするのは、デバイス全体（収集と再生）のリスタートが発生します。もしAppがBGMの再生中であれば、BGMの再生も中断されます。アップリンクモードとダウンリンクモードを制御することで、再生デバイスを中断せずにマイクのオン/オフを実現することができます。呼び出し方法の詳細は、入室時にEnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true) を一回呼び出します。マイクのオン/オフをクリックするときに、EnableAudioSend/Recvのみを呼び出すことでオーディオストリームの送信/受信を実施するかどうかを制御します。
- 採集デバイスまたは再生デバイスのみをリリースする場合は、インターフェースEnableAudioCaptureDeviceとEnableAudioPlayDeviceをご参照てください。
- pauseを呼び出してオーディオエンジンを一時停止させ、resumeを呼び出してオーディオエンジンをリカバーします。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|EnableMic    |マイクをオン/オフにします|
|GetMicState    |マイクの状態を取得します|
|EnableAudioCaptureDevice    |採集デバイスをオン/オフにします|
|IsAudioCaptureDeviceEnabled    |採集デバイスの状態を取得します|
|EnableAudioSend    |オーディオの上りをオン/オフにします|
|IsAudioSendEnabled    |オーディオの上り状態を取得します|
|GetMicLevel    |マイクのリアルタイム音量を取得します|
|GetSendStreamLevel|オーディオの上りリアルタイム音量を取得します|
|SetMicVolume    |マイクの音量を設定します|
|GetMicVolume    |マイクの音量を取得します|
|EnableSpeaker|スピーカーをオン/オフにします |
|GetSpeakerState    |スピーカーの状態を取得します|
|EnableAudioPlayDevice    |再生デバイスをオン/オフにします|
|IsAudioPlayDeviceEnabled    |再生デバイスの状態を取得します|
|EnableAudioRecv    |オーディオの下りをオン/オフにします|
|IsAudioRecvEnabled    |オーディオの下り状態を取得します|
|GetSpeakerLevel    |スピーカーのリアルタイム音量を取得します|
|GetRecvStreamLevel|ほかのルームメンバーのリアルタイム下り音量を取得します|
|SetSpeakerVolume    |スピーカーの音量を設定します|
|GetSpeakerVolume    |スピーカーの音量を取得します|
|EnableLoopBack    |インイヤ・モニタリングをオン/オフにします|



### マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使われています。入室した際、マイクとスピーカーはデフォルトでオフになっています。
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  関数のプロトタイプ  
```
ITMGContext public int EnableMic(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled   |boolean     |マイクをオンにする場合、渡されるパラメータはtrueであり、マイクをオフにする場合、パラメータはfalseです|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```

### マイク状態の取得
このインターフェースはマイクの状態の取得に使用されます。戻り値0はオフの状態を示し、戻り値1はオンの状態を示します。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetMicState 
```
####  サンプルコード  
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicState();
```

### 採集デバイスのオン/オフ
このインターフェースは、採集デバイスのオン/オフに使用されます。入室した際、デバイスはデフォルトでオフになっています。
- このインターフェースは、入室後にのみ呼び出すことができます。退室した後、デバイスを自動的にオフになっています。
- 移動端末で採集デバイスをオンにすると、一般的に権限申請や音量タイプの調整などの操作が伴います。

####  関数のプロトタイプ  
```
ITMGContext public int EnableAudioCaptureDevice(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean    |採集デバイスをオンにする場合、渡されるパラメータはtrueであり、採集デバイスをオフにする場合、パラメータはfalseです|

####  サンプルコード

```
採集デバイスをオンにします
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 採集デバイス状態の取得
このインターフェースは、採集デバイス状態の取得に使用されます。
####  関数のプロトタイプ

```
ITMGContext public boolean IsAudioCaptureDeviceEnabled()
```
####  サンプルコード

```
bool IsAudioCaptureDevice =ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### オーディオ上りのオン/オフ
このインターフェースは、オーディオ上りのオン/オフに使用されます。採集デバイスがオンになっている場合は、採集したオーディオデータを送信します。採集デバイスがオフになっている場合は、ミュート状態を保持します。採集デバイスのオン/オフについては、インターフェースEnableAudioCaptureDeviceをご参照てください。

####  関数のプロトタイプ

```
ITMGContext public int EnableAudioSend(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean   |オーディオ上りをオンにする場合、渡されるパラメータはtrueであり、オーディオ上りをオフにする場合、パラメータはfalseです|

####  サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioSend(true);
```

### オーディオ上り状態の取得
このインターフェースは、オーディオ上り状態の取得に使用されます。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl boolean IsAudioSendEnabled()
```
####  サンプルコード  
```
bool IsAudioSend =  =ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioSendEnabled();
```

### マイクのリアルタイム音量の取得
このインターフェースは、マイクのリアルタイム音量の取得に使用され、戻り値がint型です。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl int GetMicLevel() 
```
####  サンプルコード  
```
int micLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicLevel();
```

### オーディオ上りのリアルタイム音量の取得
このインターフェースは、オーディオ上りのリアルタイム音量の取得に使用されます。戻り値はint型で、値の範囲は0～100です。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl int GetSendStreamLevel()
```
####  サンプルコード  
```
int Level = ITMGContext.GetInstance(this).GetAudioCtrl().GetSendStreamLevel();
```

### マイク音量の設定
このインターフェースは、マイク音量の設定に使用されます。パラメータvolumeはマイク音量の設定に使用され、値が0の場合はミュートを示し、100の場合は音量が増減しないことを示します。デフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl int SetMicVolume(int volume) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int      |音量の設定、値の範囲は0～200です。|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().SetMicVolume(volume);
```
###  マイク音量の取得
このインターフェースは、マイク音量の取得に使用されます。戻り値はint型であり、101の場合は、インターフェースSetMicVolumeを呼び出したことがなかったことを示します。

####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetMicVolume()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetMicVolume();
```

### スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使用されます。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  関数のプロトタイプ  
```
ITMGContext public int EnableSpeaker(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |スピーカーをオフにする必要がある場合、渡されるパラメータはfalseであり、スピーカーをオンにする場合、パラメータはtrueです|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

### スピーカー状態の取得
このインターフェースは、スピーカー状態の取得に使用されます。戻り値が0の場合、スピーカーがオンにし、戻り値が1の場合、スピーカーがオンになっており、戻り値が2の場合、スピーカが動作していることを示します。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetSpeakerState() 
```

####  サンプルコード  
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerState();
```



### 再生デバイスのオン/オフ
このインターフェースは、再生デバイスのオン/オフに使用されます。

####  関数のプロトタイプ  
```
ITMGContext public int EnableAudioPlayDevice(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean        |再生デバイスをオフにする場合、渡されるパラメータはfalseであり、再生デバイスをオンにする場合、渡すパラメータはtrueです|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 再生デバイスの状態の取得
このインターフェースは、再生デバイスの状態の取得に使用されます。
####  関数のプロトタイプ

```
ITMGContext public int IsAudioPlayDeviceEnabled()
```
####  サンプルコード  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### オーディオ下りのオン/オフ
このインターフェースは、オーディオ下りのオン/オフに使用されます。再生デバイスがオンになっている場合は、ほかのルームメンバーのオーディオデータを再生します。再生デバイスがオフになっている場合は、ミュート状態が保持されます。再生デバイスのオン/オフについて、インターフェースEnableAudioPlayDeviceをご参照ください。

####  関数のプロトタイプ  

```
ITMGContext public int EnableAudioRecv(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |オーディオ下りをオンにする場合、渡されるパラメータはtrueであり、オーディオ下りをオフにする場合、渡されるパラメータはfalseです|

####  サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioRecv(true);
```



### オーディオ下り状態の取得
このインターフェースは、オーディオ下り状態の取得に使用されます。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public boolean IsAudioRecvEnabled()
```

####  サンプルコード  
```
bool IsAudioRecv = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioRecvEnabled();
```

### スピーカーのリアルタイム音量の取得
このインターフェースはスピーカーのリアルタイム音量の取得に使用されます。戻り値はint型の値で、スピーカーのリアルタイム音量を示します。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetSpeakerLevel() 
```

####  サンプルコード  
```
int SpeakLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerLevel();
```

### ほかのルームメンバーの下りリアルタイム音量の取得
このインターフェースは、ほかのルームメンバーの下りリアルタイム音量の取得に使用されます。戻り値はint型で、値の範囲は1～100です。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetRecvStreamLevel(string openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |string       |ほかのルームメンバーのopenIdです|

####  サンプルコード  
```
int Level = ITMGContext.GetInstance(this).GetAudioCtrl().GetRecvStreamLevel(openId);
```

### スピーカー音量の設定
このインターフェースは、スピーカー音量の設定に使用されます。
パラメータvolumeはスピーカー音量の設定に使用され、値が0の場合はミュートを示し、100の場合は音量が増減しないことを示します、そのデフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public int SetSpeakerVolume(int volume) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int      |音量の設定、値の範囲は0～200です。|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().SetSpeakerVolume(volume);
```

### スピーカー音量の取得

このインターフェースは、スピーカー音量の取得に使用されます。戻り値はint型で、スピーカー音量を示します。戻り値が101の場合は、インターフェースSetSpeakerVolumeを呼び出したことがないことを示します。
Levelはリアルタイム音量で、Volumeはスピーカー音量で、最終的な音声音量は、Level*Volume%となります。例えば、リアルタイム音量が100で、Volumeが60の場合、最終的な音声音量も60です。

####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public int GetSpeakerVolume()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerVolume();
```


### インイヤ・モニタリングの起動
このインターフェースは、インイヤ・モニタリングの起動に使用されます。
####  関数のプロトタイプ  
```
ITMGContext TMGAudioCtrl public int EnableLoopBack(boolean enable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |boolean         |起動するかどうかを設定します|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableLoopBack(true);
```


## オフライン音声のテキスト変換のフローチャート
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## オフライン音声
初期化が実施される前に、SDKは未初期化の状態です。リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
利用上の問題について、[リアルタイム音声関連問題](https://intl.cloud.tencent.com/document/product/607/30257)をご参照ください。

## 関連インターフェースの初期化

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |


### オフライン音声関連インターフェース
|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |認証を初期化します|
|SetMaxMessageLength    |最大音声メッセージの長さを制限します|
|StartRecording|録音を開始します|
|StartRecordingWithStreamingRecognition|ストリーミング録音を開始します|
|PauseRecording|録音を一時停止します|
|ResumeRecording|録音を継続します|
|StopRecording    |録音を停止します|
|CancelRecording|録音をキャンセルします|
|GetMicLevel|オフライン音声のリアルタイムマイク音量を取得します|
|SetMicVolume|オフライン音声の録音音量を設定します|
|GetMicVolume|オフライン音声の録音音量を取得します|
|GetSpeakerLevel|オフライン音声のリアルタイムスピーカー音量を取得します  |
|SetSpeakerVolume|オフライン音声の再生音量を設定します|
|GetSpeakerVolume|オフライン音声の再生音量を取得します|
|UploadRecordedFile |音声ファイルをアップロードします|
|DownloadRecordedFile|音声ファイルをダウンロードします|
|PlayRecordedFile |音声を再生します|
|StopPlayFile|音声再生を停止します|
|GetFileSize |音声ファイルのサイズ|
|GetVoiceFileDuration|音声ファイルの長さ|
|SpeechToText |ボイスツーテキスト変換|

### 認証の初期化
SDKを初期化してから認証の初期化を呼び出します。authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースをご参照ください。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int ApplyPTTAuthbuffer(String authBuffer)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |String                    |認証|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
```

### 最大音声メッセージの長さの制限
音声メッセージの長さを制限します、最大60秒間までサポートします。

####  関数のプロトタイプ

```
ITMGContext TMGPTT public int SetMaxMessageLength(int msTime)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |音声の長さで、単位はmsです|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SetMaxMessageLength(msTime);
```


### 録音の開始
このインターフェースは、録音の開始に使用されます。ボイステキスト変換などの操作を行うには、まず録音ファイルをアップロードする必要があります。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int StartRecording(String filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                     |音声データの保存パス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().StartRecording(filePath);
```

### 録音開始のコールバック
録音開始が完了後のコールバックは関数OnEventを呼び出します、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETEであり、OnEvent関数でイベントメッセージを判断します。
渡すパラメータにはresultとfile_pathの2つの情報が含まれています。

#### エラーコード
|エラーコード値 |原因  |推奨アクション        |
|-----|------|------|
|4097   |パラメータは空です|コード中のインターフェースパラメータが正しいかどうかを確認します|
|4098   |初期化にエラーが発生しました|デバイスが占用されていないか、権限が正常であるかどうか、正常に初期化されたかを確認します|
|4099   |録音中です|適切なタイミングでSDKの録音機能を使用することを確保します|
|4100   |オーディオデータが収集されていません|マイクに異常がないかを確認します|
|4101   |録音する際に、録音ファイルへのアクセスにエラーが発生しました|ファイルが存在して、ファイルパスの正当性を確認します|
|4102   |マイク権限を取得していないため、エラーが発生しました|SDKを使用するには、マイク権限を取得する必要があるため、権限を追加するには、対象エンジンまたはプラットフォームのSDKプロジェクト構成ドキュメントをご参照ください|
|4103   |録音時間が短すぎるため、エラーが発生しました|まず、録音時間の制限単位がミリ秒であるため、パラメータが正確であるかどうかを確認します。次に、録音するには、その長さは1000ミリ秒以上である必要があります|
|4104   |録音が開始されていません|録音開始のインターフェースを呼び出したかどうかを確認します|

####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE == type)
        	{
            		### 録音開始のコールバック
        	}
}
```

### ストリーミング音声識別の開始
このインターフェースは、ストリーミング音声識別の開始に使用されます。コールバックする際に、リアルタイムで音声がテキストに変換されて返されるため、識別言語を指定できます。また、音声から識別された情報を指定の言語に翻訳してから返すことができます。

####  関数のプロトタイプ  

```
ITMGContext TMGPTT public int StartRecordingWithStreamingRecognition (String filePath)
ITMGContext TMGPTT public int StartRecordingWithStreamingRecognition(String filePath,String speechLanguage,String translateLanguage) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath|String|音声データの保存パス|
| speechLanguage    |String|指定された文字に識別するための言語パラメータです。パラメータの詳細については、 [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translateLanguage|String|指定された文字に翻訳するための言語パラメータです。パラメータの詳細については、 [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは現在使用できないため、speechLanguageと同じパラメータを入力してください）|

####  サンプルコード  
```
String  temple = getActivity().getExternalFilesDir(null).getAbsolutePath() + "/test_"+(index++)+".ptt";
ITMGContext.GetInstance(getActivity()).GetPTT().StartRecordingWithStreamingRecognition(temple,"cmn-Hans-CN","cmn-Hans-CN");
```

### ストリーミング音声識別を開始したのコールバック
ストリーミング音声識別を開始した後のコールバックは関数OnEventを呼び出します。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETEであり、OnEvent関数でイベントメッセージを判断します。渡すパラメータには次の4つの情報が含まれています。

|情報名     | 意味         |
| ------------- |:-------------:|
| result    |ストリーミング音声識別が成功したかどうかを判断するためのリターンコードです|
| text    |ボイステキスト変換で識別されたテキストです|
| file_path |録音ファイルを保存するローカルパスです|
| file_id |録音のバックグラウンドにおけるurlアドレスです|

|エラーコード     | 意味         |対処方法|
| ------------- |:-------------:|:-------------:|
|32775|ストリーミングボイスツーテキスト変換が失敗しましたが、録音が成功しました|UploadRecordedFileインターフェースを呼び出して録音をアップロードしてから、SpeechToTextインターフェースを呼び出してボイステキスト変換を行います。 |
|32777|ストリーミングボイスツーテキスト変換が失敗しましたが、録音が成功し、アップロードしました|返された情報にはアップロードしたバックグラウンドurlアドレスが含まれており、SpeechToTextインターフェースを呼び出してボイステキスト変換を行います|
|32786  |ストリーミングボイスツーテキスト変換が失敗しました|ストリーミング録音中です、ストリーミング録音インターフェースの実行結果を待ちください|

####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE == type)
        	{
            		//ストリーミング開始のコールバック
        	}
}
```

### 録音の一時停止
このインターフェースは、録音の一時停止に使用されます。録音を再開する場合は、インターフェースResumeRecordingを呼び出してください。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int PauseRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().PauseRecording();
```

### 録音の再開
このインターフェースは、録音の再開に使用されます。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int ResumeRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().ResumeRecording();
```

### 録音の停止
このインターフェースは、録音の停止に使用されます。このインターフェースが非同期インターフェースであるため、録音を停止した後には録音完了のコールバックがあります。コールバックが成功した後にのみ録音ファイルが利用可能です。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int StopRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().StopRecording();
```



### 録音のキャンセル
このインターフェースを呼び出して録音をキャンセルできます。キャンセルした後にはコールバックがありません。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int CancelRecording()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().CancelRecording();
```

### オフライン音声マイクのリアルタイム音量の取得
このインターフェースは、マイクのリアルタイム音量の取得に使用されます。戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int GetMicLevel()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetMicLevel();
```

### オフライン音声の録音音量の設定
このインターフェースは、オフライン音声の録音音量の設定に使用され、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int SetMicVolume(int vol)
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SetMicVolume(100);
```

### オフライン音声の録音音量の取得
このインターフェースは、オフライン音声の録音音量の設定に使用されます。戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int GetMicVolume()
```

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetMicVolume();
```


### スピーカーのリアルタイム音量の取得
このインターフェースは、スピーカーのリアルタイム音量の取得に使用されます。戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int GetSpeakerLevel()
```

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetSpeakerLevel();
```

### オフライン音声の再生音量の設定
このインターフェースは、オフライン音声の再生音量の設定に使用されます。値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int SetSpeakerVolume(int vol)
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SetSpeakerVolume(100);
```

### オフライン音声の再生音量の取得
このインターフェースは、オフライン音声の再生音量の取得に使用されます。戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int GetSpeakerVolume()
```

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetSpeakerVolume();
```




### 音声ファイルのアップロード
このインターフェースは、音声ファイルのアップロードに使用されます。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int UploadRecordedFile(String filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                      |アップロードする音声ファイルのパス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().UploadRecordedFile(filePath);
```


### 音声ファイルのアップロード後のコールバック
音声をアップロードした後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETEであり、OnEvent関数でイベントメッセージを判断します。
渡すパラメータには、result、file_pathとfile_idの3つの情報が含まれています。

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション     |
|-----|------|------|
|8193   |アップロードする際に、ファイルへのアクセスにエラーが発生しました|ファイルが存在しており、ファイルパスが規則に準拠していることを確認します|
|8194   |サインの認証に失敗し、エラーが発生しました|認証キーが正しいかどうか、オフライン音声を初期化したかどうかを確認します|
|8195   |ネットワークのエラーです|デバイスのネットワークが外部ネットワークに正常にアクセスできるかどうかを確認します|
|8196   |アップロードパラメータを取得する際に、ネットワークのエラーが発生しました|認証が正しいかどうか、デバイスのネットワークは外部ネットワークに正常にアクセスできるかどうかを確認します|
|8197   |アップロードパラメータを取得する際に、リターンパケットデータが空です|認証が正しいかどうか、デバイスのネットワークが外部ネットワークに正常にアクセスできるかどうかを確認します|
|8198   |アップロードパラメータを取得する際に、リターンパケットの解析に失敗しました|認証が正しいかどうか、デバイスのネットワークが外部ネットワークに正常にアクセスできるかどうかを確認します|
|8200   |appinfoが設定されていません|applyインターフェースを呼び出しているかどうか、渡されたパラメータが空であるかどうかを確認します|

####  サンプルコード

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE== type)
       	 {
           	// 音声アップロード完了のコールバック
       	 }
}
```


### 音声ファイルのダウンロード
このインターフェースは、音声ファイルのダウンロードに使用されます。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int DownloadRecordedFile(String fileID, String downloadFilePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |String                      |ファイルのurlパス|
| downloadFilePath |String                      |ファイルのローカル保存パス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().DownloadRecordedFile(url,path);
```


### 音声ファイルダウンロード完了のコールバック
音声ファイルをダウンロードした後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETEであり、OnEvent関数でイベントメッセージを判断します。

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション     |
|-----|------|------|
|12289  |ファイルをダウンロードする際に、ファイルへのアクセスにエラーが発生しました    |ファイルパスが規則に準拠しているかどうかを確認します|
|8194   |サインの認証に失敗しました|認証キーが正しいかどうか、オフライン音声を初期化したかどうかを確認します|
|12291  |ネットストレージシステムに異常が発生しました     |サーバーが音声ファイルの取得に失敗しました。インターフェースパラメータfileidが正しいか、ネットワークに異常がないか、cosファイルが存在しないかを確認します|
|12292  |サーバーのファイルシステムにエラーが発生しました    |デバイスのネットワークは外部ネットワークに正常にアクセスできるかどうか、サーバーに該当ファイルが存在するかどうかを確認します|
|12293  |ダウンロードパラメータを取得する際に、HTTPネットワークに失敗しました|デバイスのネットワークが外部ネットワークに正常にアクセスできるかどうかを確認します|
|12294   |ダウンロードパラメータを取得する際に、リターンパケットデータは空です|デバイスのネットワークは外部ネットワークに正常にアクセスできるかどうかを確認します|
|12295   |ダウンロードパラメータを取得する際に、リターンパケットの解析に失敗しました|デバイスのネットワークは外部ネットワークに正常にアクセスできるかどうかを確認します|
|12297   |appinfoが設定されていません|認証キーが正しいかどうか、オフライン音声を初期化したかどうかを確認します|


####  サンプルコード

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE== type)
        {
            //ダウンロード完了        
	}
}
```



### 音声の再生
このインターフェースは、音声の再生に使用されます。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int PlayRecordedFile(String downloadFilePath) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| downloadFilePath    |String   |ファイルのパス|

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション       |
|-----|------|------|
|20485  |再生を開始されていません|ファイルが存在するかどうか、ファイルパスが規則に準拠しているかどうかを確認します|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().PlayRecordedFile(downloadFilePath);
```


### 音声再生のコールバック
音声再生のコールバックです。イベントメッセージがITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETEであり、OnEvent関数でイベントメッセージを判断します。
渡すパラメータにはresultとfile_pathの2つの情報が含まれています。

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション          |
|-----|------|------|
|20481  |初期化にエラーが発生しました|デバイスが占用されているかどうか、権限が正常であるかどうか、正常に初期化されたかどうかを確認します|
|20482  |再生中に、再生を中断して次の音声を再生しようとしましたが、失敗しました（通常中断可能です）|コードのロジックが正しいかどうかを確認します|
|20483  |パラメータは空です|コードのインターフェースパラメータが正しいかどうかを確認します|
|20484  |内部エラーです|プレイヤー初期化のエラーやデコード失敗などによるエラーコードが発生するため、ログを参照して問題を特定する必要があります|

####  サンプルコード

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE== type)
       	 	{
			//音声再生のコールバック 
		}
}
```




### 音声再生の停止
このインターフェースは、音声再生の停止に使用されます。音声の再生を停止しても、再生完了のコールバックが発生します。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int StopPlayFile()
```

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().StopPlayFile();
```



### 音声ファイルのサイズの取得
このインターフェースを介して、音声ファイルのサイズを取得します。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int GetFileSize(String filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                     |音声ファイルのパス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetFileSize(path);
```

### 音声ファイルの長さの取得
このインターフェースは、音声ファイルの長さの取得に使用され、その単位はミリ秒です。
####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int GetVoiceFileDuration(String filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |String                     |音声ファイルのパス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().GetVoiceFileDuration(path);
```


### 指定された音声ファイルを文字に識別します
このインターフェースは、指定された音声ファイルを文字に識別するために使用されます。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int SpeechToText(String fileID)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |String                     |音声ファイル url|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID);
```



### 指定された音声ファイルを文字に翻訳します（言語指定）
このインターフェースは、指定された言語で音声ファイルを識別でき、音声から識別された情報を指定された言語に翻訳して返すこともできます。

####  関数のプロトタイプ  
```
ITMGContext TMGPTT public int SpeechToText(String fileID,String speechLanguage,String translateLanguage)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |String                     |音声ファイル url|
| speechLanguage    |String                    |指定された文字を識別するための言語パラメータです。パラメータについては、 [ボイスツーテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translateLanguage    |String                     |指定された文字に翻訳するための言語パラメータです。パラメータについては、 [ボイスツーテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照てください。（このパラメータは現在使用できないため、speechLanguageと同じパラメータを入力する必要があります）|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID,"cmn-Hans-CN","en-US");
```



### 識別のコールバック
指定された音声ファイルを文字に識別するためのコールバックです。そのイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETEであり、OnEvent関数でイベントメッセージを判断します。
渡すパラメータにはresult、file_pathとtextの3つの情報が含まれて、ここでのtextは識別されたテキストです。

#### エラーコード

|エラーコード値 |原因  |推奨ソリューション             |
|-----|------|------|
|32769  |内部エラーです|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、バックグラウンドのスタッフに対処を依頼します。|
|32770   |ネットワークで失敗が発生しました|デバイスのネットワークは外部ネットワークに正常にアクセスできるかどうかを確認します|
|32772  |リターンパケットの解析に失敗しました|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、バックグラウンドのスタッフに対処を依頼します。|
|32774   |appinfoが設定されていません|認証キーが正しいであるかどうか、オフライン音声を初期化したかどうかを確認します|
|32776  |authbufferの認証に失敗しました|authbufferが正しいであるかどうかを確認します|
|32784  |ボイスツーテキスト変換のパラメータにエラーが発生しました|コードのインターフェースパラメータfileidが空であるかどうかを確認します|
|32785  |ボイスツーテキスト変換から返された翻訳にエラーが発生しました|オフライン音声バックグラウンドのエラーです、ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、バックグラウンドのスタッフに対処を依頼します。|

####  サンプルコード

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE == type)
       	 {
            //音声ファイルを正常に識別しました       
	 }
}
```



## 高度なAPI

### バージョン番号の取得
分析するためのSDKのバージョンを取得します。
####  関数のプロトタイプ
```
ITMGContext public void GetSDKVersion()
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetSDKVersion();
```

### マイク権限の確認
マイクの権限状態を返します。
####  関数のプロトタイプ

```
ITMGContext  public abstract ITMG_RECORD_PERMISSION  CheckMicPermission()
```

#### パラメータの意味

|パラメータ|値|意味|
|---|---|---|
|ITMG_PERMISSION_GRANTED|0|マイク使用が許可されています|
|ITMG_PERMISSION_Denied|1|マイクが無効になっています|
|ITMG_PERMISSION_NotDetermined|2|ユーザーに権限を申請するための権限ボックスがポップアップされていません|
|ITMG_PERMISSION_ERROR|3|インターフェースの呼び出しエラー|

####  サンプルコード  

```
ITMGContext.GetInstance(this).CheckMicPermission();
```




### ログのプリントレベルの設定
ログのプリントレベルの設定に使用されます。デフォルトレベルを維持することをお勧めします。
####  関数のプロトタイプ
```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

|パラメータ     | タイプ         |意味|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|ログへの書き込みレベルの設定です。TMG_LOG_LEVEL_NONEは書き込まないことを示します、デフォルトはTMG_LOG_LEVEL_INFOです。|
|levelPrint|ITMG_LOG_LEVEL|ログのプリントレベルの設定です。TMG_LOG_LEVEL_NONEはプリントしないことを示します、デフォルトはTMG_LOG_LEVEL_ERRORです。|




|ITMG_LOG_LEVEL|意味|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0|ログをプリントしない|
|TMG_LOG_LEVEL_ERROR=1|エラーログをプリントします（デフォルト）|
|TMG_LOG_LEVEL_INFO=2|ヒントログをプリントします|
|TMG_LOG_LEVEL_DEBUG=3|開発デバッグログをプリントします|
|TMG_LOG_LEVEL_VERBOSE=4|高頻度のログをプリントします|

####  サンプルコード  
```
ITMGContext.GetInstance(this).SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### プリントするログのパスを設定
プリントするログのパスを設定するために使用されます。デフォルトのパスは/sdcard/Android/data/xxx.xxx.xxx/filesです。
####  関数のプロトタイプ
```
ITMGContext int SetLogPath(String logDir)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| logDir    |String   |パス|

####  サンプルコード  
```
ITMGContext.GetInstance(this).SetLogPath(path);
```


### 診断情報の取得
オーディオ・ビデオ通話のリアルタイム通信品質の関係情報を取得します。このインターフェースは、主にリアルタイムの通信品質の確認、トラブルシューティングに使用されます。セールス側は、これを無視しても構いません。
####  関数のプロトタイプ  
```
IITMGContext TMGRoom public String GetQualityTips() 
```
####  サンプルコード  
```
ITMGContext.GetInstance(this).GetRoom().GetQualityTips();
```

### オーディオデータのブラックリストへの追加
特定のIDをオーディオデータのブラックリストに追加します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |String     |ブラックリストに追加するIDです|

####  サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().AddAudioBlackList(openId);
```

### オーディオデータのブラックリストから削除
特定のIDをオーディオデータのブラックリストから削除します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(String openId)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |String     |ブラックリストから削除するIDです|

####  サンプルコード  

```
ITMGContext.GetInstance(this).GetAudioCtrl().RemoveAudioBlackList(openId);
```


## コールバックメッセージ

### メッセージリスト：

|メッセージ    | メッセージの意味  |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |オーディオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネットワークなどの原因により、ルームの接続が切断しました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|ルームタイプ変更イベント|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH|伴奏が終了しました|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE|ルームメンバーが更新されました|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE|PTTの録音が完了しました|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE|PTTをアップロードしました|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|PTTをダウンロードしました|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE|PTTの再生が完了しました|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|ボイスツーテキスト変換が完了しました|

### Dataリスト：

|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; sub_event_type; new_room_type|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE|result; error_info  |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"スピーカー (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    |result; error_info  |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"スピーカー (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    |result; error_info  |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"マイク (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    |result; error_info |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"マイク (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    |user_list;  event_id|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE |result; file_path  |{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE |result; file_path;file_id  |{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|result; file_path;file_id  |{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE |result; file_path  |{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|result; text;file_id|{"file_id":"","text":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE|result; file_path; text;file_id|{"file_id":"","file_path":","text":"","result":0}|
