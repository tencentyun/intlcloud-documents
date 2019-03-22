		
Unity開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでUnity開発のためのクイック導入文書を紹介します。		
		
		
## フローチャート		
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)		
		
						
GMEクイックスタートドキュメントは最も重要な導入APIを提供します。APIの詳細については、[関連APIドキュメント](https://cloud.tencent.com/document/product/607/15228)を参照してください。			


|重要なAPI     | APIの意味|
| ------------- |:-------------:|
|Init    		|GMEの初期化 	|
|Poll    		|イベントコールバックのトリガ	|
|EnterRoom	 	|ルームに参加  		|
|EnableMic	 		|マイクをオンにする 		|
|EnableSpeaker		|スピーカーをオンにする 		|

>**説明：**			
- GMEのAPIが正常に呼び出された後、戻り値はQAVError.OKで、値は0です。		
- 同じスレッドで、GMEのAPIを呼び出す必要があります。
- GMEによるルームへの参加は認証が必要です。ドキュメントの認証関連部分を参照してください。		
- GMEは定期的にPoll APIを呼び出してイベントコールバックをトリガする必要があります。
- GMEのコールバック情報は、コールバックメッセージリストを参照します。
- デバイスの操作はルームに参加した後に行われます。
## クイック導入手順


### 1. SDKの初期化
パラメータの取得については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。		
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはアプリ開発者によって定められ、アプリ内で繰り返さないようにします（現在INT64のみ対応）。
SDKを初期化してから、ルームに参加できます。

#### 関数プロトタイプ
```
IQAVContext Init(string sdkAppID, string openID)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  |Tencent CloudコンソールからのSdkAppId番号						|
| openID    	|String  |OpenIDはInt64型（string型に変換して渡す）のみをサポートします。10000以上で、ユーザー識別用 	|

#### サンプルコード  
```
int ret = IQAVContext.GetInstance().Init(str_appId, str_userId);
	if (ret != QAVError.OK) {
		return;
	}
```

### 2. イベントコールバックのトリガ
updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。
#### 関数プロトタイプ

```
ITMGContext public abstract int Poll();
```

### 3. ルームへの参加
生成した認証情報を用いてルームに参加します。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。


#### 関数プロトタイプ
```
ITMGContext EnterRoom(string roomID, int roomType, byte[] authBuffer)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomID		|string    	|ルームID、127文字まで入力可能					|
| roomType 	|ITMGRoomType		|ルームオーディオタイプ		|
| authBuffer 	|Byte[] 	|認証コード					|

ルームオーディオタイプについては、[音質選択](https://cloud.tencent.com/document/product/607/18522)を参照してください。
  
#### サンプルコード  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### 4. ルーム参加イベントのコールバック
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

リスニングして処理：
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

### 5. マイクのオン/オフ
このAPIはマイクのオン/オフに使用されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。

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


### 6. スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。
#### 関数プロトタイプ  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |スピーカーをオフにする必要があれば、渡されたパラメータはfalseです。スピーカーをオンにすれば、パラメータはtrueです|

#### サンプルコード  
```
スピーカーをオンにする
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

## 認証について
### 認証情報

関連機能の暗号化と認証に使用されるAuthBufferを生成します。関連バックグラウンド配置については、[認証暗号鍵](https://cloud.tencent.com/document/product/607/12218)を参照してください。          
オフラインボイスが認証を取得するときに、ルームIDパラメータをnullに入力する必要があります。
このAPIの戻り値はByte[]型です。
#### 関数プロトタイプ

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    		|int   		|Tencent CloudコンソールからのSdkAppId番号		|
| roomId    		|string   		|ルームID、127文字まで入力可能					|
| openId    	|String 	|ユーザーID					|
| key    		|string 	|Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme)からの暗号鍵				|

#### サンプルコード  

```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId, userId, "a495dca2482589e9");
}
```


