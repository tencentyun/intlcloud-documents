Windowsを使う開発者がTencent Cloud Gaming Multimedia Engineの製品APIに対するデバッグ・アクセスを行いやすいように、ここで、Windowsでの開発に向けるアクセス技術ドキュメントについて説明させていただきます。

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
- GMEのインターフェースを成功に呼び出した後に、戻り値はAV_OKで、数値は0です。
- GMEのインターフェース呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには、認証が必要です、ドキュメントの認証部分の内容を参照してください。
- GMEは周期的にPollインターフェースを呼び出し、イベントのコールバックをトリガーします。
- GMEのコールバック情報については、コールバックメッセージリストを参照してください。
- デバイスを操作するには、先に入室に成功する必要があります。
- エラーコードの詳細については、[エラーコード](https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください

## リアルタイム音声のフローチャート
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 関連インターフェースの初期化
初期化される前に、SDKは未初期化段階にあります、リアルタイム音声とオフライン音声を利用するには、インターフェースInitによりSDKを初期化する必要があります。
- 利用問題については、[一般的な問題](https://intl.cloud.tencent.com/document/product/607/30254)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |


### シングルトンの取得
GME SDKはシングルトンの形式で提供されます、すべての呼び出しはITMGContextから始まり、ITMGDelegateによりアプリケーションにコールバック・パスバックされるため、一番初めに構成する必要があります。    
####  関数のプロトタイプ 

```
QAVSDK_API ITMGContext* QAVSDK_CALL ITMGContextGetInstance();
```
####  サンプルコード  

```
ITMGContext* m_pTmgContext;
m_pTmgContext = ITMGContextGetInstance();
```


### メッセージの送信
インターフェースなどは、Delegate方式でアプリケーションにコールバック通知を送信します、メッセージタイプはITMG_MAIN_EVENT_TYPEを参考してください、Windowsプラットフォームにおけるdataはjson文字列の形であり、具体的なkey-valueは、説明ドキュメントに参考してください。

####  サンプルコード  
```
//関数の実現：
class Callback : public SetTMGDelegate 
{
	virtual void OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data)
	{
  		switch(eventType)
  		{
   			//メッセージタイプを判断し処理します
  		}
 	}
}

Callback*  p = new Callback ();
m_pTmgContext->SetTMGDelegate(p);
```

### SDKの初期化

パラメータの取得については、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースはTencent CloudコンソールからのSDKAppID番号をパラメータとする必要があります、また、openIdも必要です、このopenIdはユーザーの唯一の標識です。ルールはApp開発者により設定され、Appでは重複しなければよいです（現在、INT64のみを対応しています）。
>入室するには、SDKを先に初期化する必要があります。
>
>####  関数のプロトタイプ

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |char*   |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |char*   |openIdはInt64形式のみ（char*に変換し渡される）をサポートし、10000以上である必要があり、ユーザーの標識に使われています |

####  サンプルコード 


```
#define SDKAPPID3RD "1400089356"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```
### イベントコールバックのトリガー
updateの中で、Pollを周期的に呼び出すことで、イベントのコールバックをトリガーすることができます。
####  関数のプロトタイプ

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}
    
public:    	
	virtual void Poll()= 0;
}

```
####  サンプルコード
```
//ヘッダファイルにおける宣言

//コードの実現
void TMGTestScene::update(float delta)
{
    ITMGContextGetInstance()->Poll();
}
```

### システムの一時停止
システムにPauseイベントが発生したとき、エンジンに通知を出し、Pauseを実行する必要があります。
####  関数のプロトタイプ

```
ITMGContext int Pause()
```

### システムリカバー
システムにResumeイベントが発生したとき、エンジンに通知を出し、Resumeを実行する必要があります。Resumeインターフェースはリアルタイム音声のみをリカバーします。
####  関数のプロトタイプ

```
ITMGContext int Resume()
```



### SDKの未初期化
SDKを未初期化にし、初期化以前の状態にします。アカウントを切り替えるとき、SDKを未初期化にする必要があります。
####  関数のプロトタイプ

```
ITMGContext int Uninit()
```
####  サンプルコード
```
ITMGContext* context = ITMGContextGetInstance();
context->Uninit();
```

## リアルタイム音声ルームの関連インターフェース
リアルタイム音声通話を行うには、初期化してから、SDKの入室インタフェースを呼び出し、入室する必要があります。
利用上の問題については、[リアルタイム音声の関連問題](https://intl.cloud.tencent.com/document/product/607/30257)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|GenAuthBuffer    |初期化認証です|
|EnterRoom   |入室します|
|IsRoomEntered   |入室していますか|
|ExitRoom |退室します|
|ChangeRoomType |ユーザールームのオーディオタイプを修正します|
|GetRoomType |ユーザールームのオーディオタイプを取得します|


### 認証情報
関連機能の暗号化と認証に使われるAuthBufferを生成します、関連バックグラウンドのデプロイについては[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
オフライン音声取得の認証を行うとき、ルーム番号のパラメータをnullに設定しなければなりません。

####  関数のプロトタイプ
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent CloudコンソールからのsdkAppId番号です|
| strRoomID    |char*     |ルーム番号であり、最大は127バイトをサポートします（オフライン音声ルーム番号のパラメータは、nullに設定しなければならない）|
| strOpenID  |char*     |ユーザー標識です|
| key    |string |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|
|strAuthBuffer|char*    |返されたauthbuffです|
| bufferLength   |int    |渡されたauthbuffの長さで、500であることを推奨します|


####  サンプルコード  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```



### 入室
生成された認証情報を使って入室した場合、メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMのコールバックを受信します。入室に際し、マイクとスピーカーはデフォルトでオフになっています。戻り値がAV_OKの場合、入室に成功したことを示しています。
通常音声で入室し、範囲音声に対するサービス面はニーズがない場合は、通常入室のインターフェースを使用します。詳細については、 [範囲音声](https://intl.cloud.tencent.com/document/product/607/17972)をご参照ください。

####  関数のプロトタイプ
```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomID| char*    |ルーム番号であり、最大127バイトまでをサポートします|
| roomType |ITMGRoomType|ルームのオーディオタイプです|
| authBuffer    |char*     |認証コードです|
| buffLen   |int   |認証コードの長さです|

ルームのオーディオタイプについては、[音質選択](https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

## 入室イベントのコールバック
入室してからは、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージを送信し、OnEvent関数において判断します。

####  サンプルコード  
```

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

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|-------------|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|


### 入室しているかの判断
このインターフェースを呼び出すことで、入室しているかを判断できます、戻り値はbool型です。
####  関数のプロトタイプ  
```
ITMGContext virtual bool IsRoomEntered()
```
####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();
```

### 退室
このインターフェースを呼び出すことで、ルームから退出できます。このインターフェースは非同期であり、戻り値AV_OKの意味は、非同期送信が成功したことです。

>アプリケーション中に退室してからまたすぐ入室する場合、インターフェースの呼び出しに際し、開発者はExitRoomのコールバックRoomExitComplete通知を待つ必要がなく、インターフェースを直接に呼び出せばよいです。

####  関数のプロトタイプ  
```
ITMGContext virtual int ExitRoom()
```
####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
```

### 退室のコールバック
退室してからは、ITMG_MAIN_EVENT_TYPE_EXIT_ROOMというメッセージのコールバックが発生します。
####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		//処理します
		break;
		}
	}
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|


### ユーザールームのオーディオタイプの変更
このインターフェースは、ユーザールームのオーディオタイプの変更に使われています、その結果は、コールバックイベントをご参照ください、イベントタイプはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。
####  関数のプロトタイプ  
```
IITMGContext TMGRoom public void ChangeRoomType((ITMG_ROOM_TYPE roomType)
```


|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomtype    |ITMGRoomType    |切り替えたいルームタイプです、ルームのオーディオタイプについては、EnterRoomインターフェースをご参照ください|

####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```


### ユーザールームのオーディオタイプの取得
このインターフェースはユーザールームのオーディオタイプを取得するインターフェイスであり、戻り値はルームのオーディオタイプです、戻り値が0であることは、ユーザールームのオーディオタイプの取得にエラーが発生したことを示します、ルームのオーディオタイプについてはEnterRoomインターフェースをご参照ください。

####  関数のプロトタイプ  
```
IITMGContext TMGRoom public  int GetRoomType()
```

####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->GetRoomType();
```


### ルームタイプ設定完了のコールバック
ルームタイプの設定が完了したあと、コールバックのイベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEであり、返されるパラメータはresult、error_infoとnew_room_typeです、new_room_typeは次の情報を示しており、OnEvent関数においてイベントメッセージを判断します。

|イベントのサブタイプ     | 代表的パラメータ   |意味|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |入室に際し、固有のオーディオタイプはルームタイプと不一致であるため、入室したルームのオーディオタイプに変更されました|
| ITMG_ROOM_CHANGE_EVENT_START|2|入室済みで、オーディオタイプ切り替え中であることを示しています（例えば、ChangeRoomTypeインターフェースを呼び出してからオーディオタイプを切り替えます）|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|入室済みで、オーディオタイプは切り替え済みであることを示しています|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|ルームメンバーが ChangeRoomTypeインターフェースを呼び出し、ルームのオーディオタイプの切り替えをリクエストしていることを示しています|


####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//ルームタイプイベントの処理
	 }
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


### メンバー状態の変更
このイベントについては、状態変更があった時にのみ通知され、変更がない場合は通知されません。リアルタイムにメンバー状態を取得する必要がある場合は、上位レイヤーが通知を受ける時にキャッシュしてください、イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEであり、そのうちdataはevent_idとuser_listの二つの情報を含んでおり、OnEvent関数においてイベントメッセージを判断します。
オーディオイベントの通知は閾値があり、その閾値を超えた場合にのみ通知します。2秒を超えてもオーディオパケットを受信していない場合にのみ、「メンバーがオーディオパケットの送信を停止しました」という通知を送信します。

|event_id     | 意味         |アプリケーション側のメンテナンス内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |メンバーが入室しました|アプリケーション側でメンバーリストを更新します|
|ITMG_EVENT_ID_USER_EXIT    |メンバーが退室しました|アプリケーション側でメンバーリストを更新します|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |メンバーがオーディオパケットを送信しています|アプリケーション側で通信メンバーのリストを更新します|
|ITMG_EVENT_ID_USER_NO_AUDIO    |メンバーがオーディオパケットの送信を停止しました|アプリケーション側で通信メンバーのリストを更新します|

####  サンプルコード  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//処理します
		//開発者はパラメータを解析し、情報eventIDと user_listを取得しました
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //メンバーが入室しました
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //メンバーが退室しました
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //メンバーがオーディオパケットを送信しています
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //メンバーがオーディオパケットの送信を停止しました
			    break;
 		    default:
			    break;
		    }
		break;
		}
	}
}
```

### 品質監視イベント
品質監視イベントです、イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYであり、返されるパラメータはweight、flossとdelayです、次の情報を示しており、OnEvent関数においてイベントメッセージを判断します。

|パラメータ     | 意味        |
| ------------- |-------------|
|weight    |範囲は1～5であり、 数値5は極めて高い音質であり、 数値1はほとんど使えないほどの低い音質です、0はデフォルト値であり、意味はありません|
|floss    |パケットロス率です|
|delay    |オーディオ到達のディレー時間（ms）です|




### メッセージの詳細

|メッセージ     | メッセージの意味   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |オーディオ・ビデオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオ・ビデオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネット環境などの原因により、ルームの接続が切れました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|イベントタイプ変更イベントです|

### メッセージの対応するDataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


## リアルタイム音声のオーディオインターフェース
SDKを初期化し入室してから、ルーム内でリアルタイム音声の関連インターフェースを呼び出すことができます。
ユーザーインターフェースでマイク/スピーカーのボタンをオン/オフにする場合は、次の方式を推奨します。
- 大部分のゲームAppに対しては、EnableMicとEnableSpeakerインターフェースを呼び出すことを推奨します、これは常にEnableAudioCaptureDevice/EnableAudioSendとEnableAudioPlayDevice/EnableAudioRecvインターフェースの両方を同時に呼び出すことに相当します。
- ほかのタイプのモバイル端末App（例えばソーシャルApp）で採集デバイスをオン/オフするのは、デバイス全体の（採集と再生）リスタートにつながっているため、AppがBGMを再生している場合、BGMの再生も中断されます。上がり/下りの制御方式によりマイクをオン/オフにするのは、再生デバイスの稼働を中断することがありません。具体的な呼び出し方式は、入室する時にEnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true)を一回呼び出し、マイクのオン/オフをクリックする時は、EnableAudioSend/Recのみを呼び出すことによりオーディオストリームを送信/受信するかどうかをコントロールします。
- 採集デバイスまたは再生デバイスのみを単独にリリースしたい場合は、インターフェースEnableAudioCaptureDeviceとEnableAudioPlayDeviceをご参照ください。
- pauseを呼び出しオーディオエンジンを一時停止し、resumeを呼び出しオーディオエンジンをリカバーします。



|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|GetMicListCount           |マイクデバイスの数を取得します|
|GetMicList          |マイクデバイスを列挙します|
|GetSpeakerListCount          |スピーカーデバイスの数を取得します|
|GetSpeakerList          |スピーカーデバイスを列挙します|
|SelectMic          |マイクデバイスを選びます|
|SelectSpeaker    |スピーカーデバイスを選びます|
|EnableMic    |マイクをオン/オフにします|
|GetMicState    |マイクの状態を取得します|
|EnableAudioCaptureDevice    |採集デバイスをオン/オフにします|
|IsAudioCaptureDeviceEnabled    |採集デバイスの状態を取得します|
|EnableAudioSend    |オーディオの上りをオン/オフにします|
|IsAudioSendEnabled    |オーディオの上り状態を取得します|
|GetMicLevel    |マイクのリアルタイムボリュームを取得します|
|GetSendStreamLevel|オーディオの上りのリアルタイムボリュームを取得します|
|SetMicVolume    |マイクのボリュームを設定します|
|GetMicVolume    |マイクのボリュームを取得します|
|EnableSpeaker|スピーカーをオン/オフにします |
|GetSpeakerState    |スピーカーの状態を取得します|
|EnableAudioPlayDevice    |再生デバイスをオン/オフにします|
|IsAudioPlayDeviceEnabled    |再生デバイスの状態を取得します|
|EnableAudioRecv    |オーディオの下りをオン/オフにします|
|IsAudioRecvEnabled    |オーディオの下りの状態を取得します|
|GetSpeakerLevel    |スピーカーのリアルタイムボリュームを取得します|
|GetRecvStreamLevel|ほかのルームメンバーのリアルタイムの下りボリュームを取得します|
|SetSpeakerVolume    |スピーカーのボリュームを設定します|
|GetSpeakerVolume    |スピーカーのボリュームを取得します|
|EnableLoopBack    |インイヤ・モニタリングをオン/オフにします|



### マイクデバイスの数の取得
このインターフェースは、マイクデバイスの数の取得に使われています。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicListCount()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### マイクデバイスの列挙
このインターフェースは、GetMicListCountインターフェースと連携して、マイクの列挙に使われています。

#### 関数のプロトタイプ 
```
ITMGAudioCtrl virtual int GetMicList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    |TMGAudioDeviceInfo   |デバイスリストです|
| nCount    |int     |取得したマイクデバイスの数です|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);
```



### マイクデバイスの選択
このインターフェースは、マイクデバイスの選択に使われています。「DEVICEID_DEFAULT」をパラメータとして渡し、またはこのインターフェースを呼び出しないの場合、システムのデフォルトデバイスが選択されます。デバイスIDは、GetMicListの返信リストから取得します。

####  関数のプロトタイプ  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| pMicID    |char*      |マイクデバイスID|

####  サンプルコード  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```

### マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使われています。入室に際し、マイクとスピーカーはデフォルトでオフになっています。
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |マイクをオンにする場合、渡されたパラメータはtrueであり、マイクをオフにする場合、パラメータはfalseです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### マイク状態の取得
このインターフェースはマイク状態の取得に使われています、戻り値0はマイクをオフにする状態であり、戻り値1はマイクをオンにする状態です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicState()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```

### 採集デバイスのオン/オフ
このインターフェースは、採集デバイスのオン/オフに使われています。入室に際し、デバイスはデフォルトでオフになっています。
- このインターフェースは、入室後にのみ呼び出すことができます、退室した後に、デバイスは自動的にオフになります。
- モバイル端末では、採集デバイスをオンにするのは一般的に権限申請やボリュームタイプ調整等の操作を伴っています。

####  関数のプロトタイプ  
```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |採集デバイスをオンにする場合、渡されたパラメータはtrueであり、採集デバイスをオフにする場合、パラメータはfalseです|

####  サンプルコード

```
採集デバイスをオンにします
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### 採集デバイス状態の取得
このインターフェースは、採集デバイス状態の取得に使われています。
####  関数のプロトタイプ

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```
####  サンプルコード

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### オーディオ上りのオン/オフ
このインターフェースは、オーディオ上りのオン/オフに使われています。採集デバイスがオンになっている場合は、採集されたオーディオデータを送信します。採集デバイスがオフになっている場合は、ミュート状態が続きます。採集デバイスのオン/オフは、インターフェースEnableAudioCaptureDeviceをご参照ください。

####  関数のプロトタイプ

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |オーディオ上りをオンにする場合、渡されるパラメータはtrueであり、オーディオ上りをオフにする場合、パラメータはfalseです|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### オーディオ上り状態の取得
このインターフェースは、オーディオ上り状態の取得に使われています。
####  関数のプロトタイプ  
```
ITMGContext virtual bool IsAudioSendEnabled()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();
```

### マイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使われ、戻り値がint型です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicLevel()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### オーディオ上りのリアルタイムボリュームの取得
このインターフェースは、オーディオ上りのリアルタイムボリュームの取得に使われています、その戻り値はint型であり、数値範囲は0～100です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSendStreamLevel()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

### マイクボリュームの設定
このインターフェースは、マイクボリュームの設定に使われています。パラメータvolumeはマイクボリュームの設定に使われ、値が0の場合はミュートを示し、値が100の場合はボリュームの増減がないことを示しています、デフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int SetMicVolume(int vol)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int      |ボリューム設定で、範囲は0～200です|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);
```
###  マイクボリュームの取得
このインターフェースは、マイクボリュームの取得に使われています。戻り値はint型の値であり、戻り値は101である場合は、インターフェースSetMicVolumeを呼び出したことがないことを示します。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicVolume()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
```

### スピーカーデバイスの数の取得
このインターフェースは、スピーカーデバイスの数の取得に使われています。

####  関数のプロトタイプ  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()
```
####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();
```

### スピーカーデバイスの列挙
このインターフェースは、GetSpeakerListCountインターフェースと連携しスピーカーデバイスの列挙に使われています。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    |TMGAudioDeviceInfo    |デバイスリスト|
| nCount   |int     |取得したスピーカーデバイスの数です|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);
```

### スピーカーデバイスの選択
このインターフェースは、再生デバイスの選択に使われています。「DEVICEID_DEFAULT」をパラメータとして渡し、またはこのインターフェースを呼び出しないの場合、システムのデフォルト再生デバイスが選択されます。デバイスIDは、GetSpeakerListの返信リストから取得します。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| pSpeakerID    |char*      |スピーカーデバイスのIDです|

####  サンプルコード  
```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);
```

### スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使われています。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable   |bool       |スピーカーをオフにする場合、パラメータはfalseであり、スピーカーをオンにする場合、渡すパラメータはtrueです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### スピーカー状態の取得
このインターフェースは、スピーカー状態の取得に使われています。戻り値が0の場合、スピーカがオフ状態であり、戻り値が1の場合、スピーカーがオンになっています、戻り値が2の場合、スピーカーが稼働中です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerState()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```



### 再生デバイスのオン/オフ
このインターフェースは、再生デバイスをオン/オフにすることに使われています。

####  関数のプロトタイプ  
```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool        |再生デバイスをオフにする場合、渡されるパラメータはfalseであり、再生デバイスをオンにする場合、パラメータはtrueです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### 再生デバイスの状態の取得
このインターフェースは、再生デバイスの状態の取得に使われています。
####  関数のプロトタイプ

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()
```
####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### オーディオ下りのオン/オフ
このインターフェースは、オーディオ下りのオン/オフに使われています。再生デバイスがオンになっている場合は、ほかのルームメンバーのオーディオデータが再生されます。再生デバイスがオフになっている場合は、ミュート状態が続きます。再生デバイスのオン/オフは、インターフェースEnableAudioPlayDeviceをご参照ください。

####  関数のプロトタイプ  

```
ITMGContext virtual int EnableAudioRecv(bool enable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |オーディオ下りをオンにする場合、渡されるパラメータはtrueであり、オーディオ下りをオフにする場合、パラメータはfalseです|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### オーディオ下り状態の取得
このインターフェースは、オーディオ下り状態の取得に使われています。
####  関数のプロトタイプ  
```
ITMGContext virtual bool IsAudioRecvEnabled() 
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
```

### スピーカーのリアルタイムボリュームの取得
このインターフェースはスピーカーのリアルタイムボリュームの取得に使われています。戻り値はint型の値であり、スピーカーのリアルタイムボリュームを示します。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerLevel()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### ほかのルームメンバーの下りリアルタイムボリュームの取得
このインターフェースは、ほかのルームメンバーの下りリアルタイムボリュームを取得することに使われています。その戻り値はint型であり、数値範囲は1～100です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |char*       |ほかのルームメンバーのopenIdです|

####  サンプルコード  
```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### スピーカーボリュームの設定
このインターフェースは、スピーカーボリュームの設定に使われています。
パラメータvolumeはスピーカーボリュームの設定に使われ、値が0の場合はミュートを示し、値が100の場合はボリュームの増減がないことを示しています、デフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int        |0～200の範囲でボリュームを設定します|

####  サンプルコード  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### スピーカーボリュームの取得

このインターフェースは、スピーカーボリュームの取得に使われています。戻り値はint型の値であり、スピーカーボリュームを示しています、戻り値が101の場合は、インターフェースSetSpeakerVolumeを呼び出したことがないことを示します。
Levelはリアルタイムボリュームであり、Volumeはスピーカーボリュームであり、最終音声ボリュームはLevel*Volume%となります。例えば、リアルタイムボリュームが100で、Volumeが60である場合、最終音声ボリュームも60となります。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
```


### インイヤ・モニタリングの起動
このインターフェースは、インイヤ・モニタリングの起動に使われています。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool         |起動するかどうかを設定します|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);
```


## オフラインボイスツーテキスト変換のフローチャート
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## オフライン音声
初期化される前に、SDKは未初期化段階にあります、リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
利用上の問題については、[オフライン音声関連問題](https://intl.cloud.tencent.com/document/product/607/30257)をご参照ください。

## 関連インターフェースの初期化

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
|StartRecording|録音を開始します||
|StartRecordingWithStreamingRecognition|ストリーミング録音を開始にします|
|PauseRecording|録音を一時停止します|
|ResumeRecording|録音を継続します|
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
|GetFileSize |音声ファイルのサイズ|
|GetVoiceFileDuration|音声ファイル時間|
|SpeechToText |ボイステキスト変換|

### 認証の初期化
SDKを初期化してから認証の初期化を呼び出します、authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースをご参照ください。
####  関数のプロトタイプ  
```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |char*                    |認証|
| authBufferLen    |int                |認証の長さ|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```

### 音声メッセージの最大時間の制限
音声メッセージの最大時間を制限します、最大は60秒をサポートします。

####  関数のプロトタイプ

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |音声の長さであり、単位はmsです|

####  サンプルコード  
```
int msTime = 10;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```


### 録音の起動
このインターフェースは、録音の起動に使われています。ボイスツーテキスト変換などの機能を使用するには、まず録音ファイルをアップロードする必要があります。
####  関数のプロトタイプ  
```
ITMGPTT virtual int StartRecording(const char* fileDir)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileDir    |char*                      |音声の保存パス|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StartRecording(fileDir);
```

### 録音起動のコールバック
録音起動が完了後のコールバックは呼び出し関数OnEventです、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡されるパラメータにresultとfile_pathの二つの情報が含まれています。

#### エラーコード
|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|4097   |パラメータは空です|コードのインターフェースパラメータが正しいかどうかを確認します|
|4098   |初期化にエラーが発生しました|デバイスが占用されているか、権限が正常であるかどうか、正常に初期化しているかを確認します|
|4099   |録音中です|正しいタイミングでSDKの録音機能を利用することを確保します|
|4100   |オーディオデータを採集していません|マイクデバイスが正常であるかどうかを確認します|
|4101   |録音に際し、録音ファイルへのアクセスにエラーが発生しました|ファイルが存在していること、及びそのパスの正当性を確保します|
|4102   |マイク権限を取得していないため、エラーが発生しました|SDKを使うには、マイク権限を取得する必要があるため、対応するエンジンまたはプラットフォームのSDKプロジェクト構成ドキュメントをご参照ください|
|4103   |録音時間が短いため、エラーが発生しました|第一、録音の制限長さの単位がミリ秒であるため、パラメータが正確であるかどうかを確認します。第二、録音するには、その長さは1000ミリ秒以上である必要があります|
|4104   |録音を起動していません|録音の起動インターフェースを呼び出しているかどうかを確認します|

####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
		{
		//処理します
		break;
		}
	}
}
```

### ストリーミングAutomatic Speech Recognitionの起動
このインターフェースは、ストリーミングAutomatic Speech Recognitionの起動に使われています、コールバックにおいて、音声はリアルタイムに文字に変換されて返されるため、言語を指定し識別することができるし、音声から識別した情報を指定した言語に翻訳してから返すこともできます。

####  関数のプロトタイプ  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*|音声の保存パス|
| speechLanguage    |char*                     |指定する文字に識別するための言語パラメータです、パラメータは [ボイスツーテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translateLanguage    |char*                     |指定する文字に翻訳するための言語パラメータです、パラメータは [ボイスツーテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください（このパラメータは現時点で使えないため、speechLanguageと同じパラメータを入力してください）|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```

### ストリーミングAutomatic Speech Recognition起動のコールバック
ストリーミングAutomatic Speech Recognitionが起動した後のコールバックは呼び出し関数OnEventです。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。渡されるパラメータは次の四つの情報を含んでいます。

|メッセージ名     | 意味         |
| ------------- |:-------------:|
| result    |ストリーミングAutomatic Speech Recognitionが成功しているかどうかを判断するためのリターンコードです|
| text    |ボイステキスト変換ことにより識別のテキストです|
| file_path |録音を保存するローカルパスです|
| file_id |録音のバックグラウンドにおけるurlアドレスです|

#### エラーコード

|エラーコード     | 意味         |処理方式|
| ------------- |:-------------:|:-------------:|
|32775|ストリーミングボイスツーテキスト変換は失敗しましたが、録音は成功しました|UploadRecordedFileインターフェースを呼び出し録音をアップロードしてから、SpeechToTextインターフェースを呼び出しボイステキスト変換を行います|
|32777|ストリーミングボイスツーテキスト変換が失敗しましたが、録音は成功し、アップロードされました|返された情報にはアップロードされたバックグラウンドurlアドレスが含まれているため、SpeechToTextインターフェースを呼び出しボイステキスト変換を行います|
|32786  |ストリーミングボイスツーテキスト変換が失敗しました|ストリーミング録音中です、ストリーミング録音インターフェースからの実行結果をお待ちください|

####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
		{
		//処理します
		break;
		}
	}
}
```

### 録音の一時停止
このインターフェースは、録音の一時停止に使われています。録音を再開するには、ResumeRecordingインターフェースを呼び出してください。

####  関数のプロトタイプ  
```
ITMGPTT virtual int PauseRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->PauseRecording();
```

### 録音の再開
このインターフェースは、録音の再開に使われています。

####  関数のプロトタイプ  
```
ITMGPTT virtual int ResumeRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();
```

### 録音の停止
このインターフェースは、録音の停止に使われています。このインターフェースが非同期インターフェースであるため、録音を停止した後には録音完了のコールバックがあります、コールバックが成功した後に、録音ファイルが利用できるようになります。
####  関数のプロトタイプ  
```
ITMGPTT virtual int StopRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```



### 録音のキャンセル
録音をキャンセルするにはこのインターフェースを呼び出します。キャンセルした後にはコールバックがありません。
####  関数のプロトタイプ  
```
ITMGPTT virtual int CancelRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```

### オフライン音声マイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使われています、戻り値はint型であり、数値範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetMicLevel()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetMicLevel();
```

### オフライン音声の録音ボリュームの設定
このインターフェースは、オフライン音声の録音ボリュームの設定に使われ、数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int SetMicVolume(int vol)
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);
```

### オフライン音声の録音ボリュームの取得
このインターフェースは、オフライン音声の録音ボリュームの取得に使われています。その戻り値はint型であり、数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetMicVolume()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();
```


### スピーカーのリアルタイムボリュームの取得
このインターフェースは、スピーカーのリアルタイムボリュームの取得に使われています。戻り値はint型であり、数値範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetSpeakerLevel()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```

### オフライン音声の再生ボリュームの設定
このインターフェースは、オフライン音声の再生ボリュームの設定に使われ、数値範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int SetSpeakerVolume(int vol)
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);
```

### オフライン音声の再生ボリュームの取得
このインターフェースは、オフライン音声の再生ボリュームの取得に使われ、数値範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetSpeakerVolume()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerVolume();
```




### 音声ファイルのアップロード
このインターフェースは、音声ファイルのアップロードに使われています。
####  関数のプロトタイプ  
```
ITMGPTT virtual int UploadRecordedFile(const char* filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |アップロードする音声のパス|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```


### 音声をアップロードした後のコールバック
音声をアップロードした後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡されたパラメータは、result、file_pathとfile_idという三つの情報を含んでいます。

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|8193   |アップロードに際し、録音ファイルへのアクセスにエラーが発生しました|ファイルが存在しており、及びそのパスの正当性を確認します|
|8194   |サインの認証に失敗し、エラーが発生しました|認証キーが正しいかどうか、オフライン音声を初期化しているかどうかを確認します|
|8195   |ネット環境のエラーです|デバイスのネット環境は外部ネットワークに正常にアクセスできるかどうかを確認します|
|8196   |アップロードパラメータの取得に際し、ネット環境のエラーが発生しました|認証が正しいかどうか、デバイスのネット環境は外部ネットワークに正常にアクセスできるかどうかを確認します|
|8197   |アップロードパラメータの取得に際し、リターンパケットのデータは空です|認証が正しいかどうか、デバイスのネット環境は外部ネットワークに正常にアクセスできるかどうかを確認します|
|8198   |アップロードパラメータの取得に際し、リターンパケットの解析に失敗しました|認証が正しいかどうか、デバイスのネット環境は外部ネットワークに正常にアクセスできるかどうかを確認します|
|8200   |appinfoを設定していません|applyインターフェースを呼び出しているかどうか、入力されたパラメータが空であるかどうかを確認します|

####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
		{
		//処理します
		break;
		}
	}
}
```


### 音声ファイルのダウンロード
このインターフェースは、音声ファイルのダウンロードに使われています。
####  関数のプロトタイプ  
```
ITMGPTT virtual int DownloadRecordedFile(const char* fileId, const char* filePath) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileId  |char*   |ファイルのurlパス|
| filePath |char*  |ファイルのローカル保存パス|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```


### 音声ファイルをダウンロードした後のコールバック
音声ファイルをダウンロードした後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|12289  |ファイルのダウンロードに際し、ファイルへのアクセスにエラーが発生しました    |ファイルパスの正当性を確認します|
|8194   |サインの認証に失敗しました|認証キーが正しいかどうか、オフライン音声を初期化しているかどうかを確認します|
|12291  |ネットストレージシステムに異常が発生しました    |サーバーによる音声ファイルの取得は失敗しました、インターフェースパラメータ fileid が正しいかどうか、ネット環境が正常であるかどうか、cosファイルが存在しているかどうかを確認します|
|12292  |サーバーのファイルシステムにエラーが発生しました    |デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうか、サーバーに当該ファイルがあるかどうかを確認します|
|12293  |ダウンロードパラメータの取得に際し、HTTPネットに失敗が発生しました|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|12294   |ダウンロードパラメータの取得に際し、リターンパケットのデータは空です|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|12295   |ダウンロードパラメータの取得に際し、リターンパケットの解析に失敗しました|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|12297   |appinfoを設定していません|認証キーが正しいであるかどうか、オフライン音声を初期化しているかどうかを確認します|


####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE:
		{
		//処理します
		break;
		}
	}
}
```



### 音声の再生
このインターフェースは、音声の再生に使われています。
####  関数のプロトタイプ  
```
ITMGPTT virtual int PlayRecordedFile(const char* filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |ファイルパス|

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|20485  |再生は開始されていません|ファイルがあるかどうか、及びファイルパスの正当性を確保します|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```


### 音声再生のコールバック
音声再生のコールバックは、イベントメッセージがITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡すパラメータはresultとfile_pathの二つの情報を含んでいます。

## エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|20481  |初期化にエラーが発生しました|デバイスが占用されているか、権限が正常であるかどうか、正常に初期化されているかを確認します|
|20482  |再生中に再生を中断し、次の音声を再生しようとしましたが、失敗しました（正常な場合は中断できます）|コードのロジックが正しいかどうかを確認します|
|20483  |パラメータは空です|コードのインターフェースパラメータが正しいかどうかを確認します|
|20484  |内部エラーです|プレイヤーの初期化エラー、デコードエラーなどの場合は、このエラーコードが発生するため、ログを参照して問題を特定する必要があります|

####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
		{
		//処理します
		break;
		}
	}
}
```




### 音声再生の停止
このインターフェースは、音声再生の停止に使われています。音声の再生を停止しても、再生完了のコールバックが発生できます。
####  関数のプロトタイプ  
```
ITMGPTT virtual int StopPlayFile()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```



### 音声ファイルのサイズの取得
このインターフェースを介し、音声ファイルのサイズを取得します。
####  関数のプロトタイプ  
```
ITMGPTT virtual int GetFileSize(const char* filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |音声ファイルのパス|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);
```

### 音声ファイルの長さの取得
このインターフェースは、音声ファイルの長さの取得に使われ、その単位はミリ秒です。
####  関数のプロトタイプ  
```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |音声ファイルのパス|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```


### 指定の音声ファイルを文字に識別
このインターフェースは、指定の音声ファイルを文字に識別することに使われています。

####  関数のプロトタイプ  
```
ITMGPTT virtual void SpeechToText(const char* fileID)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |char*                      |音声ファイルのurl|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```



### 指定の音声ファイルを文字に翻訳（指定言語）
このインターフェースは、言語を指定し識別することができるし、音声から識別した情報を指定された言語に翻訳してから戻すこともできます。

####  関数のプロトタイプ  
```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |char*                     |音声ファイルのurl|
| speechLanguage    |char*                     |指定文字を識別するための言語パラメータです。パラメータは[ボイスーテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translateLanguage    |char*                     |指定文字に翻訳するための言語パラメータです。パラメータは[ボイスーテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは現時点で無効であるめ、speechLanguageと同じパラメータを入力する必要があります）|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### コールバックの識別
指定された音声ファイルを文字に識別することのコールバックです。そのイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡すパラメータはresult、file_pathとtextという三つの情報を含まれます、そのうち、textは識別されたテキストです。

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|32769  |内部エラーです|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。|
|32770   |ネットワークにエラーが発生しました|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|32772  |リターンパケットの解析に失敗しました|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。|
|32774   |appinfoを設定していません|認証キーが正しいであるかどうか、オフライン音声を初期化しているかどうかを確認します|
|32776  |authbufferの認証に失敗しました|authbufferが正しいかどうかを確認します|
|32784  |ボイスツーテキスト変換のパラメータにエラーが発生しました|コードのインターフェースパラメータfileidが空であるかどうかを確認します|
|32785  |ボイスツーテキスト変換の翻訳にエラーが発生しました|オフライン音声バックグラウンドのエラーです、ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。|

####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
		{
		//処理します
		break;
		}
	}
}
```



## 高級API

### 診断情報の取得
オーディオ・ビデオ通信のリアルタイム通信品質の関連情報を取得します。このインターフェースは、主にリアルタイムの通信品質の確認、問題の調査に使われています、セールス側としては、これを無視しても構いません。
####  関数のプロトタイプ
```
ITMGRoom virtual const char* GetQualityTips()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```


### バージョン番号の取得
####  関数のプロトタイプ

```
ITMGContext virtual const char* GetSDKVersion()
```



####  サンプルコード  

```
ITMGContextGetInstance()->GetSDKVersion();
```




### ログのプリントレベルの設定
ログのプリントレベルの設定に使われています。デフォルトレベルを維持することを推奨します。
####  関数のプロトタイプ
```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

|パラメータ     | タイプ         |意味|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|ログの書き込むレベルを設定します。TMG_LOG_LEVEL_NONEは書き込まないことを示します|
|levelWrite|ITMG_LOG_LEVEL|ログのプリントレベルを設定します。TMG_LOG_LEVEL_NONEはプリントしないことを示します|



|ITMG_LOG_LEVEL|意味|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0|ログをプリントしません|
|TMG_LOG_LEVEL_ERROR=1|エラーログをプリントします（デフォルト）|
|TMG_LOG_LEVEL_INFO=2|ヒントログをプリントします|
|TMG_LOG_LEVEL_DEBUG=3|開発デバッグログをプリントします|
|TMG_LOG_LEVEL_VERBOSE=4|高頻度ログをプリントします|

####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### プリントするログのパスの設定
プリントするログのパスの設定に使われています。
デフォルトのパスは：

| フラットフォーム    | パス        |
| ------------- |:-------------:|
|Windows 	|%appdata%\Tencent\GME\ProcessName|
|iOS    		|Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android	|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

####  関数のプロトタイプ
```
ITMGContext virtual int SetLogPath(const char* logDir) 
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| logDir    |char*    |パス|

####  サンプルコード  

```
cosnt char* logDir = ""//パスのカスタマイズ設定

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

### オーディオデータブラックリストへの追加
特定のIDをオーディオデータブラックリストに追加します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |char*       |ブラックリストに追加するIDです|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);
```

### オーディオデータブラックリストからの削除
特定のIDをオーディオデータブラックリストから削除します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |char*       |ブラックリストから削除されたいIDです|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
```


## コールバックメッセージ

### メッセージリスト：

|メッセージ    | メッセージの意味  |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |オーディオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネット環境などの原因により、ルームの接続が切れました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|イベントタイプ変更イベントです|
|ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    |マイクが新規追加しました|
|ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    |マイクが紛失しました|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE|スピーカーが新規追加しました|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE|スピーカーが紛失しました|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH|伴奏が終了しました|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE|ルームメンバーが更新しました|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE|PTTの録音が完成しました|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE|PTTがアップロードされました|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|PTTがダウンロードされました|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE|PTTの再生が完了しました|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|音声の文字転換が完成しました|

### Dataリスト：

|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|result; error_info  			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    	|result; error_info; sub_event_type; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE|result; error_info  |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"スピーカー (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    |result; error_info  |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"スピーカー (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    |result; error_info  |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"マイク (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    |result; error_info |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"マイク (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    		|user_list;  event_id			|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE 	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|result; text;file_id		|{"file_id":"","text":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE|result; file_path; text;file_id|{"file_id":"","file_path":","text":"","result":0}|
