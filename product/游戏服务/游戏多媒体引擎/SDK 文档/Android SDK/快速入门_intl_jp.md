Android開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでAndroid開発のためのクイック導入文書を紹介します。


## フローチャート
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)


GMEクイックスタートドキュメントは最も重要な導入APIを提供します。APIの詳細については、[関連APIドキュメント](https://cloud.tencent.com/document/product/607/15210)を参照してください。


|重要なAPI     | APIの意味|
| ------------- |-------------|
|Init    				|GMEの初期化 	|
|Poll    				|イベントコールバックのトリガ	|
|EnterRoom	 		|ルームに参加  			|
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

### 1. シングルトンの取得
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

### 2. SDKの初期化
パラメータの取得については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはアプリ開発者によって定められ、アプリ内で繰り返さないようにします（現在INT64のみ対応）。
>!SDKを初期化してから、ルームに参加できます。
####  関数プロトタイプ

```
ITMGContext public int Init(String sdkAppId, String openID)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  |Tencent CloudコンソールからのSdkAppId番号				|
| openID    		|String  |OpenIDはInt64型（string型に変換して渡す）のみをサポートします。10000以上で、ユーザー識別用 |

####  サンプルコード 
```
ITMGContext.GetInstance(this).Init(sdkAppId, openId);
```

### 3. イベントコールバックのトリガ
updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。
####  関数プロトタイプ

```
ITMGContext int Poll()
```
####  サンプルコード
```
ITMGContext.GetInstance(this).Poll();
```

### 4. ルームへの参加
生成した認証情報を用いてルームに参加するとき、コールバックとしてメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMが受信されます。
- ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。
- EnterRoom APIを呼び出す前に、Init APIを呼び出す必要があります。

####  関数プロトタイプ
```
ITMGContext public abstract void  EnterRoom(String roomId, int roomType, byte[] authBuffer)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId 	|String		|ルームID、127文字まで入力可能|
| roomType 	|int		|ルームオーディオタイプ		|
| authBuffer	|byte[]	|認証コード				|

ルームオーディオタイプについては、[音質選択](https://cloud.tencent.com/document/product/607/18522)を参照してください。

#### サンプルコード  
```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

### 5. ルーム参加イベントのコールバック
ルームに参加した後、コールバックがあります。メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMです。
コールバックの関連参照コードを設定します。

```
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```
コールバック処理の関連参照コード。
####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	 //ルーム参加完了イベント受信
        }
	}
```

### 6. マイクのオン/オフ
このAPIはマイクのオン/オフに使用されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。

####  関数プロトタイプ  
```
ITMGContext public void EnableMic(boolean isEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |マイクをオフにする必要があれば、渡されたパラメータはfalseです。マイクをオンにすれば、パラメータはtrueです|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```


### 7. スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。

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


## 認証について
### 認証情報
関連機能の暗号化と認証に使用されるAuthBufferを生成します。関連バックグラウンド配置については、[認証暗号鍵](https://cloud.tencent.com/document/product/607/12218)を参照してください。    
- このAPIの戻り値はByte[]型です。
- オフラインボイスが認証を取得するときに、ルームIDパラメータをnullに入力する必要があります。

####  関数プロトタイプ
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    		|int   		|Tencent CloudコンソールからのsdkAppId番号|
| roomId    		|String   	|ルームID、127文字まで入力可能（オフラインボイスのルームIDパラメータにはnullを入力することが必要）|
| openID    	|String 	|ユーザーID|
| key    		|string 	|Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme)からの暗号鍵|
 

####  サンプルコード  
```
import com.tencent.av.sig.AuthBuffer;//ヘッダファイル
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), Integer.parseInt(strRoomID),identifier, key);
```



