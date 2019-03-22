Windows開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでWindows開発のためのクイック導入文書を紹介します。


## フローチャート
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)


GMEクイックスタートドキュメントは最も重要な導入APIを提供します。APIの詳細については、[関連APIドキュメント](https://cloud.tencent.com/document/product/607/15232)を参照してください。


|重要なAPI     | APIの意味|
| ------------- |-------------|
|Init   				|GMEの初期化 	|
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

#### サンプルコード  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### 2. SDKの初期化
パラメータの取得については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはアプリ開発者によって定められ、アプリ内で繰り返さないようにします（現在INT64のみ対応）。
SDKを初期化してから、ルームに参加できます。
#### 関数プロトタイプ

```
ITMGContext virtual void Init(const char* sdkAppId, const char* openId)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    	|char*  	|Tencent CloudコンソールからのSdkAppId番号					|
| openID    		|char*   	|OpenIDはInt64型（string型に変換して渡す）のみをサポートします。10000以上で、ユーザー識別用 	|

#### サンプルコード 
```
#define SDKAPPID3RD "1400035750"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```

### 3. イベントコールバックのトリガ
updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。
#### 関数プロトタイプ

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}
    
public:    	
	virtual void Poll()= 0;
}
```
#### サンプルコード
```
ITMGContextGetInstance()->Poll();
```

### 4. ルームへの参加
生成した認証情報を用いてルームに参加するとき、コールバックとしてメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMが受信されます。
- ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。
- EnterRoom APIを呼び出す前に、Init APIを呼び出す必要があります。

#### 関数プロトタイプ
```
ITMGContext virtual int EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//一般ルーム参加API
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId			| char*    		|ルームID、127文字まで入力可能	|
| roomType 			|ITMG_ROOM_TYPE	|ルームオーディオタイプ	|
| authBuffer    		|char*    				|認証コード			|
| buffLen   			|int   				|認証コードの長さ		|

ルームオーディオタイプについては、[音質選択](https://cloud.tencent.com/document/product/607/18522)を参照してください。

#### サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 5. ルーム参加イベントのコールバック
ルームに参加した後、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージが送信され、OnEvent関数で判断します。
#### サンプルコード  
```


//実装コード
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
		}
	}
}
```

### 6. マイクのオン/オフ
このAPIはマイクのオン/オフに使用されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual void EnableMic(bool bEnabled)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |マイクをオンにする必要があれば、渡されたパラメータはtrueです。マイクをオフにすれば、パラメータはfalseです		|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```


### 7. スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual void EnableSpeaker(bool enabled)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable   		|bool       	|スピーカーをオフにする必要があれば、渡されたパラメータはfalseです。スピーカーをオンにすれば、パラメータはtrueです	|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```


## 認証について
### 認証情報
関連機能の暗号化と認証に使用されるAuthBufferを生成します。関連バックグラウンド配置については、[認証暗号鍵](https://cloud.tencent.com/document/product/607/12218)を参照してください。  
オフラインボイスが認証を取得するときに、ルームIDパラメータをnullに入力する必要があります。

#### 関数プロトタイプ
```
QAVSDK_AUTHBUFFER_API int QAVSDK_AUTHBUFFER_CALL QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| dwSdkAppID    			|int   		|Tencent CloudコンソールからのsdkAppId番号		|
| strRoomID    		|char*     |ルームID、127文字まで入力可能（オフラインボイスのルームIDパラメータにはnullを入力することが必要）|
| strOpenID  		|char*    		|ユーザーID								|
| strKey    			|char*	    	|Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme)からの暗号鍵					|
|strAuthBuffer		|char*	    	|返されたauthbuff							|
| buffLenght   		|int    		|渡されるauthbuffの長さです。推奨値は500です					|



#### サンプルコード  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```




