Cocos2dを使う開発者たちがTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを手軽に実行できるように、ここで、Cocos2dでの開発に向けるアクセス技術ドキュメントについて説明させていただきます。

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
- GMEのインターフェースが正常に呼び出された後、戻り値はAV_OKであり、数値は0です。
- GMEのインターフェースの呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには、認証が必要です、ドキュメントの認証部分の内容を参照してください。
- GMEは周期的にPollインターフェースを呼び出して、イベントのコールバックをトリガーする必要があります。
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、成功に入室することが必要です。
- エラーコードの詳細について、「エラーコード」(https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。

## リアルタイム音声のフローチャート
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 関連インターフェースの初期化
初期化が実施されていない場合、SDKは未初期化段階です、リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
利用問題について、「一般的な問題」(https://intl.cloud.tencent.com/document/product/607/30254)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |


### 準備作業
GMEを追加するには、まずヘッダーファイルtmg_sdk.hを導入する必要があります、ヘッダーファイルクラスは、メッセージの転送とコールバックを行うために、ITMGDelegateを継承しています。
####  サンプルコード  

```
#include "tmg_sdk.h"

class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
public:
...
private:
...
｝
```


### シングルトンの設定
EnterRoom関数を呼び出す前に、ITMGContextの取得が必要です、全ての呼び出しはITMGContextから始まることであり、ITMGDelegateによってコールバックでアプリケーションに返送されています、事前に設定する必要があります。
####  サンプルコード 
```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```


### メッセージの送信
インターフェースなどは、Delegate方式でアプリケーションにコールバック通知を送信します、メッセージタイプはITMG_MAIN_EVENT_TYPEに参考しており、Windowsプラットフォームでのdataはjson文字列の形式であり、具体的なkey-valueは、説明ドキュメントに参考してください。

####  サンプルコード  
```
//関数の実現：
//TMGTestScene.h:
class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
public:
	void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//TMGTestScene.cpp:
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	//ここで、eventTypeへの判断と操作を行います
}
```

### SDK初期化

パラメータの取得について、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースでは、パラメータとしてTencent CloudコンソールからのSDKAppID番号と一つのユーザーを標識する一意のopenIdが必要です。ルールはApp開発者によって設定され、App範囲内での唯一な値（現在はINT64のみをサポートしています）です。
>入室するには、SDKを先に初期化する必要があります。
>
>####  関数のプロトタイプ

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |char*   |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |char*   |openIdはInt64形式のみ（char*に変換して渡される）をサポートし、10000以上である必要があり、ユーザーの標識に使用されます |

####  サンプルコード 


```
#define SDKAPPID3RD "1400089356"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```
### イベントコールバックのトリガー
updateの中で、Pollを周期的に呼び出すことで、イベントコールバックをトリガーすることができます。
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
//ヘッダファイルにある宣言
class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
void update(float delta); 
}

//コードの実現
void TMGTestScene::update(float delta)
{
    ITMGContextGetInstance()->Poll();
}
```

### システムの一時停止
システムにPauseイベントが発生したとき、エンジンに通知を出し、Pauseを実行させる必要があります。
####  関数のプロトタイプ

```
ITMGContext int Pause()
```

### システムのリカバー
システムにResumeイベントが発生したとき、エンジンに通知を出し、Resumeを実行させる必要があります。Resumeインターフェースはリアルタイム音声のみをリカバーします。
####  関数のプロトタイプ

```
ITMGContext int Resume()
```



### SDKの未初期化
SDKを未初期化にして、初期化以前の状態に入ります。アカウントを切り替えするとき、SDKを未初期化にする必要があります。
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
リアルタイム音声通話を行うには、初期化してから、SDKの入室のインタフェースを呼び出して、入室する必要があります。
利用上の問題について、[リアルタイム音声関連問題](https://intl.cloud.tencent.com/document/product/607/30257)を参照してください。

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
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent CloudコンソールからのsdkAppId番号です|
| strRoomID    |char*     |ルーム番号、最大127文字までサポートします（オフライン音声ルーム番号パラメータをnullに設定する必要があります。）|
| strOpenID  |char*     |ユーザー標識です|
| key    |string |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|
|strAuthBuffer|char*    |返されたauthbuffです|
| bufferLength   |int    |渡すauthbuffの長さで、500を推奨します|


####  サンプルコード  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```



### 入室
生成された認証情報を使って入室した場合、メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMのコールバックを受信します。入室に際し、マイクとスピーカーはデフォルトでオフになっています。戻り値がAV_OKの場合、入室が成功です。
通常音声で入室し、範囲音声に対するサービス面はニーズがない場合は、通常入室するインターフェースを使用します。詳細については、 [範囲音声](https://intl.cloud.tencent.com/document/product/607/17972)をご参照ください。

####  関数のプロトタイプ
```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomID| char*    |ルーム番号で、最大127バイトまでをサポートします|
| roomType |ITMGRoomType|ルームのオーディオタイプです|
| authBuffer    |char*     |認証コードです|
| buffLen   |int   |認証コードの長さです|

ルームのオーディオタイプについては、「音質選択」(https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

## 入室イベントのコールバック
入室してからは、メッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMを送信し、OnEvent関数で当該メッセージが判断されます。

####  サンプルコード  
```

void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// 処理
		break;
		}
	}
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|-------------|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|


### 入室したかの判断
このインターフェースを呼び出すことで、入室したかを判断できます、戻り値はbool型です。
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
このインターフェースを呼び出すことで、退室できます。このインターフェースは非同期であり、戻り値AV_OKの意味は、非同期送信が成功したことです。

>アプリケーション中に退室してからすぐ入室するケースがある場合、インターフェースの呼び出しに際し、開発者はExitRoomのコールバックRoomExitComplete通知を待つ必要がなく、インターフェースを直接に呼び出せばよいです。

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
退室してから、メッセージがITMG_MAIN_EVENT_TYPE_EXIT_ROOMのコールバックが発生します。
####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		// 処理
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
このインターフェースは、ユーザールームのオーディオタイプの変更に使用されます、その結果は、コールバックイベントをご参照ください、イベントタイプはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。
####  関数のプロトタイプ  
```
IITMGContext TMGRoom public void ChangeRoomType((ITMG_ROOM_TYPE roomType)
```


|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomType    |ITMG_ROOM_TYPE    |切り替えたいルームタイプです、ルームのオーディオタイプについては、EnterRoomインターフェースをご参照ください|

####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```


### ユーザールームのオーディオタイプの取得
このインターフェースはユーザールームのオーディオタイプを取得するインターフェイスであり、戻り値はルームのオーディオタイプです。戻り値は0であることは、ユーザールームのオーディオタイプを取得する時にエラーが発生したことを示しています、ルームのオーディオタイプについてEnterRoomインターフェースをご参照ください。

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
ルームタイプの設定が完了したあと、コールバックのイベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEであり、返されるパラメータはresult、error_infoとnew_room_typeです。new_room_typeは次の情報を表し、OnEvent関数においてイベントメッセージを判断します。

|イベントのサブタイプ     | 代表的パラメータ   |意味|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |入室する時、固有のオーディオタイプはルームタイプと不一致であるため、入室するルームのオーディオタイプに変更されました|
| ITMG_ROOM_CHANGE_EVENT_START|2|入室済みで、オーディオタイプ切り替え中です（例えば、ChangeRoomTypeインターフェースを呼び出してオーディオタイプを切り替えます）|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|入室済みで、オーディオタイプは切り替え済みです|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|ルームメンバーが ChangeRoomTypeインターフェースを呼び出し、ルームのオーディオタイプの切り替えをリクエストします|


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


### メンバー状態の変化
このイベントは状態が変化した場合のみ通知され、状態変化がない場合は通知されません。リアルタイムでメンバー状態を取得する場合は、上層が通知を受ける時にキャッシュしてください、イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEであり、そのうちdataはevent_idとuser_listの二つの情報を持っており、OnEvent関数によって判断されています。
オーディオイベントの通知に、閾値があります、この閾値を越える場合のみ、通知が送信されます。オーディオパケットを受信しない時間は2秒以上になる場合のみ、「メンバーがオーディオパケットの送信を停止した」のメッセージが通知されます。

|event_id     | 意味         |アプリケーション側のメンテナンス内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |メンバーが入室した|アプリケーション側でメンバーリストを更新します|
|ITMG_EVENT_ID_USER_ENTER    |メンバーが退室した|アプリケーション側でメンバーリストを更新します|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |メンバーはオーディオパケットを送信した|アプリケーション側で通話メンバーリストを更新します|
|ITMG_EVENT_ID_USER_NO_AUDIO    |メンバーはオーディオパケットの送信を停止した|アプリケーション側で通話メンバーリストを更新します|

####  サンプルコード  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		// 処理
		//開発者はパラメータを解析し、eventIDとuser_listの情報を取得します
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //メンバーは入室しました
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //メンバーは退室しました
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //メンバーはオーディオパケットを送信しています
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //メンバーはオーディオパケットの送信を停止しました
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
品質監視イベントです、イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYです。返されるパラメータはweight、floss  とdelayです、それぞれの意味は以下です、イベントメッセージがOnEvent関数で判断されています。

|パラメータ     | 意味         |
| ------------- |-------------|
|weight    |範囲は1-5です、数値5の意味は音質スコアが最高です、数値1の意味は音質スコアが最悪であり、ほとんど利用不可です、数値0は初期値であり、意味がありません|
|floss    |パケットロス率|
|delay    |オーディオ送達遅延時間（ms）|




### メッセージの詳細

|メッセージ    | メッセージの意味   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |オーディオ・ビデオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオ・ビデオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネット環境などの原因により、ルームとの接続が切れました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|ルームタイプ変更イベントです|

### メッセージと対応するDataの詳細

|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


## リアルタイム音声のオーディオインターフェース
SDKを初期化した後に入室します、リアルタイムにオーディオ音声関連インターフェースを呼び出すには、入室が必要です。
ユーザーインターフェースでマイク・スピーカーのオン・オフボタンをクリックするとき、以下の方式をお勧めます。
- 大部分のゲームAppに対しては、EnableMicとEnableSpeakerインターフェースを呼び出すことを推奨します、これは、常にEnableAudioCaptureDevice/EnableAudioSendとEnableAudioPlayDevice/EnableAudioRecvインターフェースの両方を同時に呼び出すことに相当します。
- ソーシャルAppなど他のタイプの移動端末Appのほう、採集デバイスをオンまたはオフにすると、デバイス全体（採集と再生）のリスタートが発生します。もしAppがこのタイミングでBGMの再生中であれば、BGMの再生も中断されます。アップリンクモードとダウンリンクモードを制御することで、再生デバイスを中断せずにマイクのオン/オフを実現することができます。具体的な方法は、入室する時EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true) を呼び出します、マイクのオン/オフをクリックするときに、EnableAudioSend/Recvを呼び出すことでオーディオストリームの送信/受信を実施するかを制御します。
- 採集デバイスまたは再生デバイスのみをリリースする場合は、インターフェースEnableAudioCaptureDeviceとEnableAudioPlayDeviceをご参照ください。
- pauseを呼び出してオーディオエンジンを停止し、resumeを呼び出してオーディオエンジンをリカバーします。



|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|GetMicListCount           |マイクデバイスの数を取得します|
|GetMicList          |マイクデバイスのリストを取得します|
|GetSpeakerListCount          |スピーカーデバイスの数を取得します|
|GetSpeakerList          |スピーカーデバイスのリストを取得します|
|SelectMic          |マイクデバイスを選びます|
|SelectSpeaker    |スピーカーデバイスを選びます|
|EnableMic    |マイクをオン/オフにします|
|GetMicState    |マイクの状態を取得します|
|EnableAudioCaptureDevice    |採集デバイスをオン/オフにします|
|IsAudioCaptureDeviceEnabled    |採集デバイスの状態を取得します|
|EnableAudioSend    |オーディオの送信をオン/オフにします|
|IsAudioSendEnabled    |オーディオの送信状態を取得します|
|GetMicLevel    |マイクのリアルタイムボリュームを取得します|
|GetSendStreamLevel|オーディオの送信のリアルタイムボリュームを取得します|
|SetMicVolume    |マイクのボリュームを設定します|
|GetMicVolume    |マイクのボリュームを取得します|
|EnableSpeaker|スピーカーをオン/オフにします |
|GetSpeakerState    |スピーカーの状態を取得します|
|EnableAudioPlayDevice    |再生デバイスをオン/オフにします|
|IsAudioPlayDeviceEnabled    |再生デバイスの状態を取得します|
|EnableAudioRecv    |オーディオの受信をオン/オフにします|
|IsAudioRecvEnabled    |オーディオの受信の状態を取得します|
|GetSpeakerLevel    |スピーカーのリアルタイムボリュームを取得します|
|GetRecvStreamLevel|ルームのほかのメンバーのリアルタイム受信ボリュームを取得します|
|SetSpeakerVolume    |スピーカーのボリュームを設定します|
|GetSpeakerVolume    |スピーカーのボリュームを取得します|
|EnableLoopBack    |インイヤ・モニタリングをオン/オフにします|



### マイクデバイスの数の取得
このインターフェースは、マイクデバイスの数の取得に使用されます。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicListCount()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### マイクデバイスリストの取得
このインターフェースは、GetMicListCountインターフェースと連携して、マイクデバイスリストの取得に使用されます。

####  関数のプロトタイプ 
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
このインターフェースは、マイクデバイスの選択に使用されます。「DEVICEID_DEFAULT」をパラメータとして渡す、またはこのインターフェースをコールしないと、システムのデフォルトデバイスが選択されます。デバイスIDは、GetMicListの戻りリストから取得したものです。

####  関数のプロトタイプ  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| pMicID    |char*      |マイクデバイスのIDです|

####  サンプルコード  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```

### マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使用されます。入室する時、マイクとスピーカーはデフォルトでオフになっています。
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |マイクをオンにする場合、trueをパラメータとして渡してください。マイクをオフにする場合、falseをパラメータとして渡してください|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### マイク状態の取得
このインターフェースはマイクの状態の取得に使用されます、戻り値0はオフ状態で、戻り値1はオン状態を表します。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicState()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```

### 採集デバイスのオン/オフ
このインターフェースは、採集デバイスのオン/オフに使用されます。入室する時、デバイスはデフォルトでオフになっています。
- このインターフェースは、入室した後にのみ呼び出すことができます、退室した後、デバイスは自動的にオフになります。
- モバイル端末における採集デバイスの起動に伴い、権限申請やボリュームタイプの調整が一般的に発生しています。

####  関数のプロトタイプ  
```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |採集デバイスをオンにするには、渡すパラメータはtrueであり、採集デバイスをオフにする場合、パラメータはfalseです。|

####  サンプルコード

```
採集デバイスをオンにします
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### デバイス状態の取得
このインターフェースは、デバイス状態の取得に使用されます。
####  関数のプロトタイプ

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```
####  サンプルコード

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### オーディオ送信のオン/オフ
このインターフェースは、オーディオ送信のオン/オフに使用されます。採集デバイスがオンになっている場合は、採集したオーディオデータを送信します。採集デバイスがオフになっている場合は、ミュート状態を保持します。採集デバイスのオン/オフについては、インターフェースEnableAudioCaptureDeviceを参照してください。

####  関数のプロトタイプ

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |オーディオ送信をオンにするには、渡すパラメータはtrueであり、オーディオ送信をオフにするには、パラメータはfalseです。|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### オーディオ送信状態の取得
このインターフェースは、オーディオ送信状態の取得に使用されます。
####  関数のプロトタイプ  
```
ITMGContext virtual bool IsAudioSendEnabled()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();
```

### マイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使用され、戻り値がint型です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicLevel()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### オーディオ送信のリアルタイムボリュームの取得
このインターフェースは、オーディオ送信のリアルタイムボリュームの取得に使用されます、戻り値はint型で、値の範囲は0～100です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSendStreamLevel()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

### マイクボリュームの設定
このインターフェースは、マイクボリュームの設定に使用されます。パラメータvolumeはマイクボリュームの設定に使用され、値が0の場合はミュートを示し、値が100の場合はボリュームが増減しないことを示します、そのデフォルト値は100です。

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
このインターフェースは、マイクボリュームの取得に使用されます。戻り値はint型値であり、戻り値が101の場合は、インターフェースSetMicVolumeを呼び出したことがなかったことを示します。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetMicVolume()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
```

### スピーカーデバイスの数の取得
このインターフェースは、スピーカーデバイスの数の取得に使用されます。

####  関数のプロトタイプ  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()
```
####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();
```

### スピーカーデバイスリストの取得
このインターフェースは、GetSpeakerListCountインターフェースと連携してスピーカーデバイスのリストの取得に使用されます。

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
| ppDeviceInfoList    |TMGAudioDeviceInfo    |デバイスリストです|
| nCount   |int     |取得しているスピーカーデバイスの数です|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);
```

### スピーカーデバイスの選択
このインターフェースは、再生デバイスの選択に使用されます。「DEVICEID_DEFAULT」をパラメータとして渡し、またはこのインターフェースを呼び出していない場合、システムのデフォルトデバイスが選択されます。デバイスIDは、GetSpeakerListの戻りリストから取得したものです。

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
このインターフェースは、スピーカーのオン/オフに使用されます。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable   |bool       |スピーカーをオフにする場合、渡すパラメータはfalseであり、スピーカーをオンにする場合、渡すパラメータはtrueです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### スピーカー状態の取得
このインターフェースは、スピーカー状態の取得に使用されます。戻り値が0の場合、スピーカーがオフになっており、戻り値が1の場合、スピーカーがオンになっており、戻り値が2の場合、スピーカーデバイスが稼働中であることを示します。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerState()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```



### 再生デバイスのオン/オフ
このインターフェースは、再生デバイスのオン/オフに使用されます。

####  関数のプロトタイプ  
```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool        |再生デバイスをオフにするには、渡すパラメータはfalseであり、再生デバイスをオンにする場合、渡すパラメータはtrueです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### 再生デバイスの状態の取得
このインターフェースは、再生デバイスの状態の取得に使用されます。
####  関数のプロトタイプ

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()
```
####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### オーディオ受信のオン/オフ
このインターフェースは、オーディオ受信のオン/オフに使用されます。再生デバイスがオンになっている場合は、ルームのほかのメンバーのオーディオデータを再生します。再生デバイスがオフになっている場合は、ミュート状態を保持します。再生デバイスのオン/オフについて、インターフェースEnableAudioPlayDeviceを参照してください。

####  関数のプロトタイプ  

```
ITMGContext virtual int EnableAudioRecv(bool enable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |オーディオ受信をオンにするには、渡すパラメータはtrueであり、オーディオ受信をオフにするには、渡すパラメータはfalseです|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### オーディオ受信状態の取得
このインターフェースは、オーディオ受信状態の取得に使用されます。
####  関数のプロトタイプ  
```
ITMGContext virtual bool IsAudioRecvEnabled() 
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
```

### スピーカーのリアルタイムボリュームの取得
このインターフェースはスピーカーのリアルタイムボリュームの取得に使用されます。戻り値はint型数値で、スピーカーのリアルタイムボリュームを示します。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerLevel()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### ルームのほかのメンバーのダウンリンクリアルタイムボリュームの取得
このインターフェースは、ルームのほかのメンバーのダウンリンクリアルタイムボリュームの取得に使用されます、戻り値はint型で、値の範囲は0～100です。
####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |char*       |ルームのほかのメンバーのopenIdです|


####  サンプルコード  
```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### スピーカーボリュームの設定
このインターフェースは、スピーカーボリュームの設定に使用されます。
パラメータvolumeはスピーカーボリュームの設定に使用され、値が0の場合はミュートを示し、値が100の場合はボリュームが増減しないことを示します、そのデフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int        |ボリューム設定で、範囲は0～200です|

####  サンプルコード  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### スピーカーボリュームの取得

このインターフェースは、スピーカーボリュームの取得に使用されます。戻り値はint型値で、スピーカーボリュームを示します、戻り値が101の場合は、インターフェースSetSpeakerVolumeを呼び出したことがなかったことを示します。
Levelはリアルタイムボリュームで、Volumeはスピーカーボリュームで、最終的な音声ボリュームは、Level*Volume%となります。例えば、リアルタイムボリュームの数値が100で、Volumeの数値が60の場合、最終的な音声ボリュームも60です。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
```


### インイヤ・モニタリングの起動
このインターフェースは、インイヤ・モニタリングの起動に使用されます。
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


## オフライン音声のテキスト変換のフローチャート
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## オフライン音声
初期化が実施されていない場合、SDKは未初期化段階です、リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
利用上の問題については、[リアルタイム音声関連問題](https://intl.cloud.tencent.com/document/product/607/30258)を参照してください。

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
|GetFileSize |音声ファイルのサイズ|
|GetVoiceFileDuration|音声ファイルの時間|
|SpeechToText |ボイステキスト変換|

### 認証の初期化
SDKを初期化してから認証の初期化を呼び出します、authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースを参照してください。
####  関数のプロトタイプ  
```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |char*                    |認証です|
| authBufferLen    |int                |認証の長さです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```

### 音声メッセージの最大時間の制限
音声メッセージの最大時間を制限します、最大60秒までサポートします。

####  関数のプロトタイプ

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |音声の長さで、単位はmsです|

####  サンプルコード  
```
int msTime = 10;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```


### 録音の起動
このインターフェースは、録音の起動に使用されます。音声テキスト変換などの操作を行うには、録音ファイルを先にアップロードする必要があります。
####  関数のプロトタイプ  
```
ITMGPTT virtual int StartRecording(const char* fileDir)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileDir    |char*                      |音声の保存パスです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StartRecording(fileDir);
```

### 録音開始のコールバック
録音開始が完了後のコールバック呼び出し関数OnEventです、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETEで、OnEvent関数でイベントメッセージを判断します。
渡すパラメータにはresultとfile_pathの2つの情報が含まれています。

#### エラーコード
|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|4097   |パラメータは空です|コードのインターフェースパラメータが正しいかどうかを確認します|
|4098   |初期化にエラーが発生しました|デバイスが占用されていないか、権限が正常であるかどうか、正常に初期化されたかを確認します|
|4099   |録音中です|正しいタイミングでSDKの録音機能を使用することを確保します|
|4100   |オーディオデータが収集されていません|マイクデバイスに異常がないかを確認します|
|4101   |録音する際に、録音ファイルへのアクセスにエラーが発生しました|ファイルが存在して、ファイルパスの正当性を確認します|
|4102   |マイク権限を取得していないため、エラーが発生しました|SDKを使用するには、マイク権限を取得する必要があるため、権限を追加するには、対応エンジンまたはプラットフォームのSDKプロジェクト構成ドキュメントを参照してください|
|4103   |録音時間が短すぎるため、エラーが発生しました|まず、録音時間の制限単位がミリ秒であるため、パラメータが正確であるかどうかを確認します。次に、録音するには、その長さは1000ミリ秒以上である必要があります|
|4104   |録音が開始されていません|録音開始のインターフェースを呼び出したかどうかを確認します|

####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// 処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
		{
		// 処理
		break;
		}
	}
}
```

### ストリーミングAutomatic Speech Recognitionの起動
このインターフェースは、ストリーミングAutomatic Speech Recognitionの起動に使用されます、コールバックする際に、リアルタイムで音声がテキストに変換されて返されるため、識別言語を指定できます。また、音声から識別された情報を指定の言語に翻訳してから返すことができます。

####  関数のプロトタイプ  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*|音声の保存パスです|
| speechLanguage    |char*                     |指定文字に識別するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translateLanguage    |char*                     |指定文字に翻訳するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは現在使用できないため、speechLanguageと同じパラメータを入力してください）|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```

### ストリーミングAutomatic Speech Recognitionのコールバックの起動
ストリーミングAutomatic Speech Recognitionが完了してからのコールバック呼び出し関数OnEventを起動します、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。渡すパラメータは次の四つの情報を含んでいます。

|メッセージ名前     | 意味         |
| ------------- |:-------------:|
| result    |ストリーミングAutomatic Speech Recognitionが成功しているかどうかを判断するための戻りコードです|
| text    |ボイステキスト変換で識別したテキストです|
| file_path |録音を保存するローカルパスです|
| file_id |録音のバックグラウンドにおけるurlアドレスです|

#### エラーコード

|エラーコード     | 意味         |対応方法|
| ------------- |:-------------:|:-------------:|
|32775|ストリーミングボイステキスト変換が失敗しましたが、録音が成功しました|UploadRecordedFileインターフェースを呼び出して録音をアップロードしてから、SpeechToTextインターフェースを呼び出してボイステキスト変換します|
|32777|ストリーミングボイステキスト変換が失敗しましたが、録音が成功し、アップロードしました|返された情報にはアップロードしたバックグラウンドurlアドレスが含まれているため、SpeechToTextインターフェースを呼び出してボイステキスト変換します|
|32786  |ストリーミングボイスツーテキスト変換が失敗しました|ストリーミング録音中です、ストリーミング録音インターフェースからの実行結果をお待ちください|

####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// 処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
		{
		// 処理
		break;
		}
	}
}
```

### 録音の一時停止
このインターフェースは、録音の一時停止に使用されます。録音を再開する場合は、インターフェースResumeRecordingを呼び出してください。

####  関数のプロトタイプ  
```
ITMGPTT virtual int PauseRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->PauseRecording();
```

### 録音の継続
このインターフェースは、録音の継続実行に使用されます。

####  関数のプロトタイプ  
```
ITMGPTT virtual int ResumeRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();
```

### 録音の停止
このインターフェースは、録音の停止に使用されます。このインターフェースが非同期インターフェースであるため、録音を停止した後には録音完了のコールバックがあります、コールバックが成功してから、録音ファイルが利用できます。
####  関数のプロトタイプ  
```
ITMGPTT virtual int StopRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```



### 録音のキャンセル
このインターフェースを呼び出して録音をキャンセルします。キャンセルした後にはコールバックがありません。
####  関数のプロトタイプ  
```
ITMGPTT virtual int CancelRecording()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```

### オフライン音声のマイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使用されます。戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetMicLevel()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetMicLevel();
```

### オフライン音声の録音ボリュームの設定
このインターフェースは、オフライン音声の録音ボリュームの設定に使用され、その値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int SetMicVolume(int vol)
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);
```

### オフライン音声の録音ボリュームの取得
このインターフェースは、オフライン音声の録音ボリュームの取得に使用されます。その戻り値はintであり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetMicVolume()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();
```


### スピーカーのリアルタイムボリュームの取得
このインターフェースは、スピーカーのリアルタイムボリュームの取得に使用されます。戻り値はint型であり、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetSpeakerLevel()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```

### オフライン音声の再生ボリュームの設定
このインターフェースは、オフライン音声の再生ボリュームの設定に使用され、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int SetSpeakerVolume(int vol)
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);
```

### オフライン音声の再生ボリュームの取得
このインターフェースは、オフライン音声の再生ボリュームの取得に使用され、値の範囲は0～100です。

####  関数のプロトタイプ  
```
ITMGPTT virtual int GetSpeakerVolume()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerVolume();
```




### 音声ファイルのアップロード
このインターフェースは、音声ファイルのアップロードに使用されます。
####  関数のプロトタイプ  
```
ITMGPTT virtual int UploadRecordedFile(const char* filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |アップロードする音声のパスです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```


### 音声のアップロードが完了した後のコールバック
音声をアップロードが完了した後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETEであり、OnEvent関すにおいてイベントメッセージを判断します。
渡すパラメータは、result、file_pathとfile_idの三つの情報を含んでいます。

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|8193   |ファイルのアップロードに際し、ファイルへのアクセスにエラーが発生しました|ファイルが存在しており、そのパスの正当性を確認します|
|8194   |サインの認証に失敗し、エラーが発生しました|認証キーが正しいかどうか、オフライン音声を初期化しているかどうかを確認します|
|8195   |ネット環境のエラーです|デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|8196   |アップロードパラメータの取得に際し、ネット環境のエラーが発生しました|認証が正しいかどうか、デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|8197   |アップロードパラメータの取得に際し、返されたパケットのデータは空です|認証が正しいかどうか、デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|8198   |アップロードパラメータの取得に際し、返されたパケットの解析に失敗しました|認証が正しいかどうか、デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|8200   |appinfoを構成していません|applyインターフェースを呼び出しているかどうか、入力したパラメータが空であるかどうかを確認します|

####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// 処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
		{
		// 処理
		break;
		}
	}
}
```


### 音声ファイルのダウンロード
このインターフェースは、音声ファイルのダウンロードに使用されます。
####  関数のプロトタイプ  
```
ITMGPTT virtual int DownloadRecordedFile(const char* fileId, const char* filePath) 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileId  |char*   |ファイルのurlパスです|
| filePath |char*  |ファイルのローカル保存パスです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```


### 音声ファイルのダウンロードが完了した後のコールバック
音声ファイルをダウンロードが完了した後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETEで、OnEvent関数においてイベントメッセージを判断します。

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|12289  |ファイルのダウンロードに際し、ファイルへのアクセスにエラーが発生しました    |ファイルパスがルールに適合しているかどうかを確認します|
|8194   |サインの認証に失敗しました|認証キーが正しいかどうか、オフライン音声を初期化しているかどうかを確認します|
|12291  |ネットストレージシステムに異常が発生しました    |サーバーによる音声ファイルの取得が失敗しました、インターフェースパラメータfileidが正しいかどうか、ネット環境が正常であるかどうか、cosファイルが存在しているかどうかを確認してください|
|12292  |サーバーのファイルシステムにエラーが発生しました    |デバイスのネット環境ではインターネットに正常にアクセスできるかどうか、サーバーに該当ファイルがあるかどうかを確認します|
|12293  |ダウンロードパラメータの取得に際し、HTTPネットに失敗が発生しました|デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|12294   |ダウンロードパラメータの取得に際し、返されたパケットのデータは空です|デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|12295   |ダウンロードパラメータの取得に際し、返されたパケットの解析に失敗しました|デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|12297   |appinfoを構成していません|認証キーが正しいであるかどうか、オフライン音声を初期化しているかどうかを確認します|


####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// 処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE:
		{
		// 処理
		break;
		}
	}
}
```



### 音声の再生
このインターフェースは、音声の再生に使用されます。
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
|20485  |再生が開始されていませんん|ファイルが存在するかどうか、そのパスがルールに適合しているかどうかを確認します|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```


### 音声再生のコールバック
音声再生のコールバックは、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETEであり、OnEvent関すにおいてイベントメッセージを判断します。
渡すパラメータにはresultとfile_pathの2つの情報が含まれています。

#### エラーコード

|エラーコード値 |原因  |提案        |
|-----|------|------|
|20481  |初期化にエラーが発生しました|デバイスが占用されていないか、権限が正常であるかどうか、正常に初期化されたかを確認します|
|20482  |再生中で、再生を停止して次の音声を再生しようとしましたが、失敗しました（普通には停止可能です）|コードのロジックが正しいかどうかを確認します|
|20483  |パラメータは空です|コード中のインターフェースパラメータが正しいかどうかを確認します|
|20484  |内部エラーです|プレイヤー初期化のエラー、デコードエラーなどを表するエラーコードであるため、ログを参照して問題を確定する必要があります|

####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// 処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
		{
		// 処理
		break;
		}
	}
}
```




### 音声再生の停止
このインターフェースは、音声再生の停止に使用されます。音声の再生を停止しても、再生完了のコールバックがあります。
####  関数のプロトタイプ  
```
ITMGPTT virtual int StopPlayFile()
```

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```



### 音声ファイルのサイズの取得
このインターフェースを介して、音声ファイルのサイズを取得します
####  関数のプロトタイプ  
```
ITMGPTT virtual int GetFileSize(const char* filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |音声ファイルのパスです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);
```

### 音声ファイルの長さの取得
このインターフェースは、音声ファイルの長さの取得に使用され、その単位はミリ秒です。
####  関数のプロトタイプ  
```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |音声ファイルのパスです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```


### 指定の音声ファイルを文字に識別
このインターフェースは、指定の音声ファイルを文字に識別ために使用されます。

####  関数のプロトタイプ  
```
ITMGPTT virtual void SpeechToText(const char* fileID)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |char*                      |音声ファイルのurlです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```



### 指定の音声ファイルを文字に翻訳（指定言語）
このインターフェースは、言語を指定して識別し、音声から識別した情報を指定の言語に翻訳してから返すことができます。

####  関数のプロトタイプ  
```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |char*                     |音声ファイルのurlです|
| speechLanguage    |char*                     |指定文字に識別するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translateLanguage    |char*                     |指定文字に翻訳するための言語パラメータです、パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは現在使用できないため、speechLanguageと同じパラメータを入力する必要があります）|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### 識別のコールバック
指定の音声ファイルを文字に識別するためのコールバックです、そのイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡すパラメータはresult、file_pathとtextの三つの情報を含んでおり、そのうちのtextは識別されたテキストです。

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|32769  |内部エラーです|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決するようにバックグラウンドの操作者に連絡します。|
|32770   |ネット環境に失敗が発生しました|デバイスのネット環境ではインターネットに正常にアクセスできるかどうかを確認します|
|32772  |返されたパケットの解析に失敗しました|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決するようにバックグラウンドの操作者に連絡します。|
|32774   |appinfoを構成していません|認証キーが正しいであるかどうか、オフライン音声を初期化しているかどうかを確認します|
|32776  |authbufferの認証に失敗しました|authbufferが正しいかどうかを確認します|
|32784  |ボイスツーテキスト変換のパラメータにエラーが発生しました|コードのインターフェースパラメータfileidが空であるかどうかを確認します|
|32785  |ボイスツーテキスト変換から返された翻訳にエラーが発生しました|オフライン音声バックグラウンドのエラーです、ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決するようにバックグラウンドの操作者に連絡します。|

####  サンプルコード

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// 処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
		{
		// 処理
		break;
		}
	}
}
```



## 高度なAPI

### 診断情報の取得
オーディオ・ビデオ通信のリアルタイム通信品質の関係情報を取得します。このインターフェースは、主にリアルタイムの通信品質の確認、問題の調査に使用されます、セールス側としては、これを無視しても構いません。
####  関数のプロトタイプ
```
ITMGRoom virtual const char* GetQualityTips()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```


### バージョンの取得
####  関数のプロトタイプ

```
ITMGContext virtual const char* GetSDKVersion()
```



####  サンプルコード  

```
ITMGContextGetInstance()->GetSDKVersion();
```




### ログのプリントレベルの設定
ログのプリントレベルの設定に使用されます。デフォルトレベルを維持することを推奨します。
####  関数のプロトタイプ
```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

|パラメータ     | タイプ         |意味|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|ログの書き込むレベルの設定で、TMG_LOG_LEVEL_NONEは書き込まないことを示します|
|levelWrite|ITMG_LOG_LEVEL|ログのプリントレベルの設定で、TMG_LOG_LEVEL_NONEはプリントしないことを示します|



|ITMG_LOG_LEVEL|意味|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0|ログをプリントしません|
|TMG_LOG_LEVEL_ERROR=1|エラーログをプリントします（デフォルト）|
|TMG_LOG_LEVEL_INFO=2|ヒントログをプリントします|
|TMG_LOG_LEVEL_DEBUG=3|開発デバッグログをプリントします|
|TMG_LOG_LEVEL_VERBOSE=4|高頻度のログをプリントします|

####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### プリントするログのパスの設定
プリントするログのパスの設定に使用されます。
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
| logDir    |char*    |パスです|

####  サンプルコード  

```
cosnt char* logDir = ""//パスのカスタマイズ設定

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

### オーディオデータブラックリストに追加
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

### オーディオデータブラックリストから削除
特定のIDをオーディオデータブラックリストから削除します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |char*       |ブラックリストから削除するIDです|

####  サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
```


## コールバックメッセージ

### メッセージリスト：

|メッセージ    | メッセージの意味   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |オーディオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネット環境などの原因により、ルームとの接続が切れました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|ルームタイプ変更イベントです|
|ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    |マイクデバイスが新規追加されました|
|ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    |マイクデバイスが紛失しました|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE|スピーカーデバイスが新規追加されました|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE|スピーカーデバイスが紛失しました|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH|伴奏が終了しています|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE|ルームメンバーが更新されました|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE|PTTの録音が完成しました|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE|PTTをアップロードが完成しました|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|PTTをダウンロードが完成しました|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE|PTTの再生が完了しています|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|音声の文字転換が完成しました|

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
