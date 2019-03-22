Unreal Engine開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでUnreal Engine開発のための導入技術文書を紹介します。

>?このドキュメントはGME SDKバージョン2.4に対応します。

## 使用フローチャート
### リアルタイムボイスフローチャート
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)
### オフラインボイスのボイステキスト変換フローチャート
![](https://main.qcloudimg.com/raw/4c875d05cd2b4eaefba676d2e4fc031d.png)


### GMEの使用に関する重要事項

|重要なAPI     | APIの意味|
| ------------- |:-------------:|
|Init		    		|GMEの初期化 	|
|Poll    			|イベントコールバックのトリガ	|
|EnterRoom	 		|ルームに参加  		|
|EnableMic	 		|マイクをオンにする 	|
|EnableSpeaker			|スピーカーをオンにする 	|

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


### 準備作業
GMEの導入には、まず、ヘッダファイルtmg_sdk.hを取り込む必要があります。ヘッダファイルのクラスはITMGDelegateを継承してメッセージの転送とコールバックを実行します。
#### サンプルコード  
```
#include "tmg_sdk.h"

class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public ITMGDelegate
{
public:
...
private:
...
｝
```


### シングルトンの設定
EnterRoom関数を呼び出す前に、まずITMGContextを取得して構成する必要があります。すべての呼び出しはITMGContextから始め、ITMGDelegateによってコールバックしてアプリケーションに渡します。

#### サンプルコード
```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```


### メッセージの渡し
APIクラスは、Delegateメソッドを使用してコールバック通知をアプリケーションに送信します。メッセージタイプはITMG_MAIN_EVENT_TYPEを参照してください。dataはWindowsプラットフォームでは、json文字列フォーマットです。key-valueの詳細については、説明ドキュメントを参照してください。

#### サンプルコード 

```
//関数実装：
//UEDemoLevelScriptActor.h:
class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public SetTMGDelegate
{
public:
	void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//UEDemoLevelScriptActor.cpp:
void AUEDemoLevelScriptActor::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data){
	//ここでeventTypeを判断、操作する
}
```

### SDKの初期化
パラメータの取得については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはアプリ開発者によって定められ、アプリ内で繰り返さないようにします（現在INT64のみ対応）。
SDKを初期化してから、ルームに参加できます。
#### 関数プロトタイプ 

```
ITMGContext virtual void Init(const char* sdkAppId, const char* openId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    	|char*   	|Tencent CloudコンソールからのsdkAppId番号					|
| openID    	|char*   	|OpenIDはInt64型（string型に変換して渡す）のみをサポートします。10000以上で、ユーザー識別用 	|

#### サンプルコード  

```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```


### イベントコールバックのトリガ

Tickで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。
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
//ヘッダファイルでの宣言
virtual void Tick(float DeltaSeconds);

//コード実装
void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) 
{   
ITMGContextGetInstance()->Poll();
}
```


### システム一時停止

システムでPauseイベントが発生したら、Pauseを実行するようエンジンに通知する必要があります。
#### 関数プロトタイプ

```
ITMGContext int Pause()
```

### システム回復
システムでResumeイベントが発生したら、Resumeを実行するようエンジンに通知する必要があります。
#### 関数プロトタイプ

```
ITMGContext  int Resume()
```



### SDKの逆初期化
SDKを逆初期化し、初期化されていない状態に入ります。アカウントの切り替えには、逆初期化が必要です。

#### 関数プロトタイプ 
```
ITMGContext int Uninit()

```
#### サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->Uninit();
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
QAVSDK_AUTHBUFFER_API int QAVSDK_AUTHBUFFER_CALL QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| dwSdkAppID    			|int   		|Tencent CloudコンソールからのsdkAppId番号		|
| strRoomID    		|char*     |ルームID、127文字まで入力可能（オフラインボイスのルームIDパラメータにはnullを入力することが必要）|
| strOpenID  		|char*     	|ユーザーID|
| strKey    			|char*	    	|Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme)からの暗号鍵					|
|strAuthBuffer		|char*	    	|返されたauthbuff							|
| bufferLength   		|int    		|渡されるauthbuffの長さです。推奨値は500です					|



#### サンプルコード  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```


### ルーム参加
生成した認証情報を用いてルームに参加するとき、コールバックとしてメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMが受信されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。戻り値がAV_OKの場合は成功です。
一般ボイスでルームに参加し、業務上で範囲ボイスのニーズがない場合は、一般のルーム参加APIが使用されます。詳細情報については、[範囲ボイス](https://cloud.tencent.com/document/product/607/17972)を参照してください。

#### 関数プロトタイプ

```
ITMGContext virtual int EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//一般ルーム参加API
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId			| char*    		|ルームID、127文字まで入力可能	|
| roomType 			|ITMG_ROOM_TYPE	|ルームオーディオタイプ		|
| authBuffer    		|char*     	|認証コード			|
| buffLen   			|int   		|認証コードの長さ		|

ルームオーディオタイプについては、[音質選択](https://cloud.tencent.com/document/product/607/18522)を参照してください。


#### サンプルコード  

```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);//一般ボイスルーム参加サンプルコード
```




### ルーム参加イベントのコールバック
ルームに参加した後、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージが送信され、OnEvent関数で判断します。
#### コード説明
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

### ルームに参加したかの判断
このAPIの呼び出しによってルームに参加したかを判断できます。戻り値はBOOL型です。
#### 関数プロトタイプ  
```
ITMGContext virtual bool IsRoomEntered()
```
#### サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();
```

### ルーム退出
このAPIの呼び出しによって現在のルームから退出できます。これは非同期APIであり、戻り値がAV_OKの場合、非同期配信が完了したことを意味します。

> アプリケーション内にルームから退出後すぐにルールに参加するシナリオがある場合、開発者はAPI呼び出しフローで、ExitRoomのRoomExitCompleteコールバック通知を待つ必要がなく、APIを直接呼び出すことが可能です。

#### 関数プロトタイプ  

```
ITMGContext virtual int ExitRoom()
```
#### サンプルコード  

```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
```

### ルーム退出コールバック
ルームから退出した後、コールバックがあります。メッセージがITMG_MAIN_EVENT_TYPE_EXIT_ROOMです。
#### サンプルコード  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		//処理
		break;
		}
	}
}
```

### ユーザールームオーディオタイプの変更
このAPIは、ユーザールームのオーディオタイプを変更するために使用されます。結果については、コールバックイベントを参照してください。イベントタイプはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。
#### 関数プロトタイプ  
```
IITMGContext TMGRoom public void ChangeRoomType((ITMG_ROOM_TYPE roomType)
```


|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomType    |ITMG_ROOM_TYPE    |切り替えたいルームタイプ。ルームオーディオタイプについては、EnterRoom APIを参照してください|

#### サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```


### ユーザールームオーディオタイプの取得
このAPIはユーザールームオーディオタイプの取得に使用され、戻り値はルームのオーディオタイプです。戻り値が0の場合、ユーザールームオーディオタイプの取得にエラーが発生したことを示します。ルームオーディオタイプについては、EnterRoom APIを参照してください。

#### 関数プロトタイプ  
```
IITMGContext TMGRoom public  int GetRoomType()
```

#### サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->GetRoomType();
```


### ルームタイプ設定完了コールバック
ルームタイプが設定された後、コールバックのイベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。返されたパラメータはresult、error_info、およびnew_room_typeです。new_room_typeによって表示される情報は以下の通りです。OnEvent関数でイベントメッセージを判断します。

|イベントサブタイプ     | 代表パラメータ   |意味|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM		|1 	|ルームに参加する過程で、持っているオーディオタイプが、ルームのタイプと一致しないため、そのルームのオーディオタイプに変更されたことを意味します	|
| ITMG_ROOM_CHANGE_EVENT_START			|2	|既にルームに参加し、オーディオタイプの切り替えが開始したことを意味します（例えば、ChangeRoomType APIを呼び出してから、オーディオタイプが切り替われます）|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE		|3	|既にルームに参加し、オーディオタイプの切り替えが完了したことを意味します|
| ITMG_ROOM_CHANGE_EVENT_REQUEST			|4	|ルームメンバーがChangeRoomType APIを呼び出し、ルームオーディオタイプの切り替えをリクエストすることを意味します|	


#### サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//ルームタイプイベントを処理
	 }
}
```

### メンバー状態の変更
このイベントは、状態が変化すると通知されるが、状態が変化しないと通知されません。リアルタイムにメンバー状態を取得する必要があれば、上位が通知を受けたときにバッファに保存してください。イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEです。dataには、event_idとuser_listという2つの情報が含まれ、OnEvent関数でevent_idメッセージを判断します。
オーディオイベントの通知にはしきい値があり、このしきい値を越えると通知が送信されます。オーディオパケットが2秒以上受信されないと、「オーディオパケットの送信を停止したメンバーがいる」というメッセージが送信されます。

|event_id     | 意味         |保守内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|ルームに参加したメンバーがいる			|アプリケーション側でメンバーリストを保守		|
|ITMG_EVENT_ID_USER_EXIT    				|ルームから退出したメンバーがいる			|アプリケーション側でメンバーリストを保守		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|オーディオパケットを送信したメンバーがいる		|アプリケーション側で通話メンバーリストを保守	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|オーディオパケットの送信を停止したメンバーがいる	|アプリケーション側で通話メンバーリストを保守	|

#### サンプルコード  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
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

|API     | APIの意味   |
| ------------- |:-------------:|
|GetMicListCount    				       	|マイクデバイス数量の取得|
|GetMicList    				      	|マイクデバイスの列挙|
|GetSpeakerListCount    				      	|スピーカーデバイス数量の取得|
|GetSpeakerList    				      	|スピーカーデバイスの列挙|
|SelectMic    				      	|マイクデバイスの選択|
|SelectSpeaker    				|スピーカーデバイスの選択|
|EnableMic    						|マイクのオン/オフ|
|GetMicState    						|マイク状態の取得|
|EnableAudioCaptureDevice    		|収集デバイスのオン/オフ		|
|IsAudioCaptureDeviceEnabled    	|収集デバイス状態の取得	|
|EnableAudioSend    				|オーディオ上りリンクのオン/オフ	|
|IsAudioSendEnabled    				|オーディオ上りリンク状態の取得	|
|GetMicLevel    						|マイクリアルタイム音量の取得	|
|SetMicVolume    					|マイク音量の設定		|
|GetMicVolume    					|マイク音量の取得		|
|EnableSpeaker    					|スピーカーのオン/オフ |
|GetSpeakerState    				|スピーカー状態の取得|
|EnableAudioPlayDevice    			|再生デバイスのオン/オフ		|
|IsAudioPlayDeviceEnabled    		|再生デバイス状態の取得	|
|EnableAudioRecv    					|オーディオ下りリンクのオン/オフ	|
|IsAudioRecvEnabled    				|オーディオ下りリンク状態の取得	|
|GetSpeakerLevel    					|スピーカーリアムタイム音量の取得	|
|SetSpeakerVolume    				|スピーカー音量の設定		|
|GetSpeakerVolume    				|スピーカー音量の取得		|
|EnableLoopBack    					|インイヤーモニターのオン/オフ			|


### SNS系アプリの呼び出しフロー図
![](https://main.qcloudimg.com/raw/53598680491501ab5a144e87ba932ccc.png)


### マイクデバイス数量の取得
このAPIは、マイクデバイス数量を取得するために使用されます。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetMicListCount()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### マイクデバイスの列挙
このAPIは、マイクデバイスを列挙するために使用されます。GetMicListCount APIと組み合わせて使用されます。

#### 関数プロトタイプ 
```
ITMGAudioCtrl virtual int GetMicList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    	|TMGAudioDeviceInfo   	|デバイスリスト		|
| nCount    		|int     		|マイクデバイス数量の取得	|

#### サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);
```



### マイクデバイスの選択
このAPIは、マイクデバイスを選択するために使用されます。「DEVICEID_DEFAULT」を呼び出さなくて、渡さないと、システムのデフォルトデバイスが選択されます。デバイスIDはGetMicListリターンリストから取得されます。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| pMicID    |char*      |マイクデバイスID|

#### サンプルコード  
```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```

### マイクのオン/オフ
このAPIはマイクのオン/オフに使用されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。
EnableMic = EnableAudioCaptureDevice + EnableAudioSend。
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


### マイク状態の取得
このAPIはマイク状態の取得に使用されます。戻り値0はマイクオフ状態で、戻り値1はマイクオン状態。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetMicState()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```


### 収集デバイスのオン/オフ
このAPIは収集デバイスのオン/オフに使用されます。ルームに参加するときに、デバイスがデフォルトでオフです。
- このAPIは、ルームに参加した後にのみ呼び出すことができます。ルームから退出した後デバイスは自動的にオフになります。
- モバイル側で、収集デバイスをオンにすると、通常に権限申請、音量タイプの調整などが必要です。

#### 関数プロトタイプ  
```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |収集デバイスをオンにする必要があれば、渡されたパラメータはtrueです。収集デバイスをオフにすれば、パラメータはfalseです|

#### サンプルコード

```
収集デバイスをオンにします
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### 収集デバイス状態の取得
このAPIは収集デバイス状態の取得に使用されます。
#### 関数プロトタイプ

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```
#### サンプルコード

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### オーディオ上りリンクのオン/オフ
このAPIはオーディオ上りリンクのオン/オフに使用されます。収集デバイスがオンの場合、収集されたオーディオデータが送信されます。収集デバイスがオフの場合、音声なしのままとなります。収集デバイスのオン/オフについては、API EnableAudioCaptureDeviceを参照してください。

#### 関数プロトタイプ

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| bEnable    |bool     |オーディオ上りリンクをオンにする必要があれば、渡されたパラメータはtrueです。オーディオ上りリンクをオフにすれば、パラメータはfalseです|

#### サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### オーディオ上りリンク状態の取得
このAPIはオーディオ上りリンク状態の取得に使用されます。
#### 関数プロトタイプ  
```
ITMGContext virtual bool IsAudioSendEnabled()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();
```

### マイクリアルタイム音量の取得
このAPIはマイクリアルタイム音量の取得に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetMicLevel()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### マイク音量の設定
このAPIはマイク音量の設定に使用されます。パラメータvolumeはマイク音量の設定に使用され、数値が0の場合はミュート状態を示し、100の場合は音量が変更されないことを示します。デフォルト数値は100です。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int SetMicVolume(int vol)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int      |音量設定、範囲0～200|

#### サンプルコード  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);
```

### マイク音量の取得
このAPIはマイク音量の取得に使用され、戻り値はint型の数値です。戻り値が101の場合、API SetMicVolumeを呼び出したことがないことを意味します。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetMicVolume()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
```

### スピーカーデバイス数量の取得
このAPIは、スピーカーデバイス数量を取得するために使用されます。

#### 関数プロトタイプ  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()
```
#### サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();
```

### スピーカーデバイスの列挙
このAPIは、スピーカーデバイスを列挙するために使用されます。GetSpeakerListCount APIと組み合わせて使用されます。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    	|TMGAudioDeviceInfo    	|デバイスリスト		|
| nCount   		|int     		|スピーカーデバイス数量の取得	|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);
```

### スピーカーデバイスの選択
このAPIは、再生デバイスを選択するために使用されます。「DEVICEID_DEFAULT」を呼び出さなくて、渡さないと、システムのデフォルト再生デバイスが選択されます。デバイスIDはGetSpeakerListリターンリストから取得されます。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| pSpeakerID    |char*      |スピーカーデバイスID|

#### サンプルコード  
```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);
```

### スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
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

### スピーカー状態の取得
このAPIはスピーカー状態の取得に使用されます。戻り値0はスピーカーオフ状態、戻り値1はスピーカーオン状態、戻り値2はスピーカーデバイス動作中を示します。


#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerState()
```

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```

再生デバイスのオン/オフ
このAPIは再生デバイスのオン/オフに使用されます。

#### 関数プロトタイプ  
```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool        |再生デバイスをオフにする必要があれば、渡されたパラメータはfalseです。再生デバイスをオンにすれば、パラメータはtrueです|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### 再生デバイス状態の取得
このAPIは再生デバイス状態の取得に使用されます。
#### 関数プロトタイプ

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()
```
#### サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### オーディオ下りリンクのオン/オフ
このAPIはオーディオ下りリンクのオン/オフに使用されます。再生デバイスがオンになっているとき、ルーム内の他の人のオーディオデータを再生します。再生デバイスがオフになっているとき、音声なしのままとなります。再生デバイスのオン/オフについては、API EnableAudioPlayDeviceを参照してください。

#### 関数プロトタイプ  

```
ITMGContext virtual int EnableAudioRecv(bool enable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool     |オーディオ下りリンクをオンにする必要があれば、渡されたパラメータはtrueです。オーディオ下りリンクをオフにすれば、パラメータはfalseです|

#### サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### オーディオ下りリンク状態の取得
このAPIはオーディオ下りリンク状態の取得に使用されます。
#### 関数プロトタイプ  
```
ITMGContext virtual bool IsAudioRecvEnabled() 
```

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
```

### スピーカーリアムタイム音量の取得
このAPIはスピーカーリアムタイム音量の取得に使用されます。戻り値はint型で、スピーカーのリアルタイム音量を表示します。
#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerLevel()
```

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### スピーカー音量の設定
このAPIはスピーカー音量の設定に使用されます。
パラメータvolumeはスピーカー音量の設定に使用され、数値が0の場合はミュート状態を示し、100の場合は音量が変更されないことを示します。デフォルト数値は100です。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int        |音量設定、範囲0～200|

#### サンプルコード  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### スピーカー音量の取得
このAPIはスピーカー音量の取得に使用されます。戻り値はint型の数値でスピーカー音量を示します。戻り値が101の場合、API SetSpeakerVolumeを呼び出したことがないことを意味します。
Levelはリアルタイム音量で、Volumeはスピーカーの音量です。最終音声の音量はLevel*Volume%に相当します。例えば、リアルタイム音量数値が100の場合、このときのVolumeの数値が60で、最終に出た音声の数値も60です。

#### 関数プロトタイプ  
```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
```


### インイヤーモニターの起動
このAPIはインイヤーモニターの起動に使用されます。
#### 関数プロトタイプ  
``` 
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |bool         |起動要否を設定する|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);
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
ITMGAudioEffectCtrl virtual int StartAccompany(const char* filePath, bool loopBack, int loopCount, int msTime) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------
| filePath    	|char* 	|伴奏再生パス						|
| loopBack  	|bool	|ミキシング有無の送信。通常trueに設定されます。つまり、他人にも伴奏が聞こえる	|
| loopCount	|int 	|ループ数。数値は-1であれば無限ループを示す				|
| msTime	|int   	|遅延時間						|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StartAccompany(filePath,true,-1,0);
```

### 伴奏再生のコールバック
伴奏再生の開始が完了した後、コールバック関数はOnEventを呼び出し、イベントメッセージはITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISHです。OnEvent関数でイベントメッセージを判断します。
#### サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
	   	}
		...
        case ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH:
		{
		//処理
		break;
		}
	}
}
```

### 伴奏再生の停止
このAPIを呼び出して、伴奏の再生を停止します。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int StopAccompany(int duckerTime)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| duckerTime	|int             |フェード時間|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAccompany(0);
```

### 伴奏の再生が完了したか
再生が完了したとき、戻り値はtrue、再生が完了していないとき、戻り値はfalse。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual bool IsAccompanyPlayEnd()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->IsAccompanyPlayEnd();
```

### 伴奏再生の一時停止
このAPIを呼び出して、伴奏の再生を一時停止します。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int PauseAccompany()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAccompany();
```

### 伴奏再生の再開
このAPIは伴奏再生の再開に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int ResumeAccompany()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAccompany();
```

### 自分が伴奏を聞こえるかどうかの設定
このAPIは、自分が伴奏を聞こえるかどうかを設定するために使用されます。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyPlay(bool enable)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|--------------|
| enable    |bool             |聞こえるか|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyPlay(false);
```

### 他人にも伴奏が聞こえるかどうかの設定
他人にも伴奏が聞こえるかどうかを設定します。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyLoopBack(bool enable)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|--------------|
| enable    |bool             |聞こえるか|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyLoopBack(false);
```

### 伴奏音量の設定
伴奏音量を設定します。デフォルト値は100です。数値が100以上の場合、音量は増加し、数値が100以下の場合、音量は減少します。値範囲は0～200です。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int SetAccompanyVolume(int vol)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int             |音量値|

#### サンプルコード  
```
int vol=100;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyVolume(vol);
```

### 伴奏再生音量の取得
このAPIは伴奏音量の取得に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int GetAccompanyVolume()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyVolume();
```

### 伴奏再生進捗の取得
伴奏の再生進捗を取得するには、次の2つのAPIを使用します。注意：Current/Total =現在のループ回数、Current％Total =現在のループ再生位置。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int GetAccompanyFileTotalTimeByMs()
ITMGAudioEffectCtrl virtual int GetAccompanyFileCurrentPlayedTimeByMs()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileTotalTimeByMs();
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileCurrentPlayedTimeByMs();
```

### 再生進捗の設定
このAPIは再生進捗の設定に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int SetAccompanyFileCurrentPlayedTimeByMs(unsigned int time)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| time    |int                |再生進捗、ミリ秒単位|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyFileCurrentPlayedTimeByMs(time);
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
ITMGAudioEffectCtrl virtual int PlayEffect(int soundId,  const char* filePath, bool loop, double pitch, double pan, double gain)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId  	|int        	|効果音ID						|
| filePath    	|char*     	|効果音パス						|
| loop    		|bool  	|繰り返し再生の要否						|
| pitch    	|double	|再生頻度。デフォルトが1.0です。値が小さいほど、再生速度は遅くなり、時間は長くなります		|
| pan    		|double	|チャンネル、値の範囲は-1.0～1.0です。-1.0は左チャンネルのみがオンになっていることを意味します	|
| gain    		|double	|音量ゲイン。値の範囲は0.0～1.0です。デフォルトが1.0です		|

#### サンプルコード  
```
double pitch = 1.0;
double pan = 0.0;
double gain = 0.0;
ITMGContextGetInstance()->GetAudioEffectCtrl()->PlayEffect(soundId,filepath,true,pitch,pan,gain);
```

### 効果音再生の一時停止
このAPIは効果音再生の一時停止に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int PauseEffect(int soundId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseEffect(soundId);
```

### すべての効果音再生の一時停止
このAPIを呼び出して、すべての効果音を一時停止
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int PauseAllEffects()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAllEffects();
```

### 効果音再生の再開
このAPIは効果音再生の再開に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int ResumeEffect(int soundId)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeEffect(soundId);
```

### すべての効果音再生の再開
このAPIを呼び出して、すべての効果音の再生を再開します。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int ResumeAllEffects()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAllEffects();
```

### 効果音再生の停止
このAPIは効果音再生の停止に使用されます。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int StopEffect(int soundId)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int                    |効果音ID|

#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopEffect(soundId);
```

### すべての効果音再生の停止
このAPIを呼び出して、すべての効果音の再生を停止します。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int StopAllEffects()
```


#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAllEffects();
```



### ボイス変更特効
このAPIを呼び出して、ボイス変更特効を設定します。
#### 関数プロトタイプ 

```
TMGAudioEffectCtrl int setVoiceType(int type)
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
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```

### カラオケ特別効果音
このAPIを呼び出して、カラオケ特別効果音を設定します。
####  関数プロトタイプ  
```
TMGAudioEffectCtrl int SetKaraokeType(int type)
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
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetKaraokeType(0);
```



### 効果音再生音量の取得
効果音再生の音量を取得します。リニア音量で、デフォルト値は100です。数値が100以上の場合、音量は増加し、数値が100以下の場合、音量は減少します。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int GetEffectsVolume()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetEffectsVolume();
```

### 効果音再生音量の設定
このAPIを呼び出して、効果音の再生音量を設定します。
#### 関数プロトタイプ  
```
ITMGAudioEffectCtrl virtual int SetEffectsVolume(int volume)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int                    |音量値|

#### サンプルコード  
```
int volume=1;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetEffectsVolume(volume);
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
ITMGPTT virtual void ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |char*                    |認証|
| authBufferLen    |int                |認証長さ|

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```

### ボイスメッセージ最大時間の制限
ボイスメッセージの最大長さを制限し、最大60秒。
#### 関数プロトタイプ

```
ITMGPTT virtual void SetMaxMessageLength(int msTime)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |ボイス時間、単位はms|
 
#### サンプルコード  
```
int msTime = 10;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```

### 録音の起動
このAPIは録音の起動に使用されます。ボイスのテキスト変換操作を実行する前に、録音ファイルをアップロードする必要があります。
#### 関数プロトタイプ  
```
ITMGPTT virtual void StartRecording(const char* fileDir)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileDir    |char*                      |ボイスの保存パス|

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StartRecording(fileDir);
```

### 録音起動のコールバック
録音の起動が完了した後、コールバックはOnEvent関数を呼び出します。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETEです。OnEvent関数でイベントメッセージを判断します。

#### サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
		{
		//処理
		break;
		}
	}
}

```

### ストリーミングボイス認識の起動
このAPIはストリーミングボイス認識の起動に使用されます。その同時にコールバックには、リアルタイムのボイス変換テキストが返されます。言語を指定して認識することができ、ボイスで認識された情報を指定された言語に翻訳して返すこともできます。

#### 関数プロトタイプ  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    	|char*	|ボイスの保存パス	|
| speechLanguage    |char*                     |指定したテキストの言語パラメータに識別します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください|
| translateLanguage    |char*                     |指定したテキストの言語パラメータに翻訳します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください。（このパラメータは一時的に無効です。speechLanguageと同じのパラメータを入力してください）|

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### ストリーミングボイス認識起動のコールバック
ストリーミングボイス認識の起動が完了した後、コールバックはOnEvent関数を呼び出します。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETEです。OnEvent関数でイベントメッセージを判断します。渡されたパラメータには、次の4つの情報が含まれています。

|メッセージ名称     | 意味         |
| ------------- |:-------------:|
| result    	|ストリーミングボイス認識が完了したかどうかを判断するための戻りコード			|
| text    		|ボイステキスト変換で認識されたテキスト	|
| file_path 	|録音を保存するローカルアドレス		|
| file_id 		|バックグラウンドでの録音のURLアドレス	|

|エラーコード     | 意味         |処理方法|
| ------------- |:-------------:|:-------------:|
|32775	|ストリーミングボイステキスト変換に失敗しましたが、録音に成功しました	|UploadRecordedFile APIを呼び出して録音をアップロードしてから、SpeechToText APIを呼び出して、ボイステキスト変換操作を行います
|32777	|ストリーミングボイステキスト変換に失敗しましたが、録音とアップロードに成功しました	|返された情報には、アップロードに成功したバックグラウンドURLアドレスが含まれています。SpeechToText APIを呼び出して、ボイステキスト変換操作を行います

#### サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
		{
		//処理
		break;
		}
	}
}

```

### 録音の停止
このAPIは録音の停止に使用されます。このAPIは非同期APIで、記録を停止すると、録音完成のコールバックが送信されます。成功した場合のみ、録音ファイルを利用できます。
#### 関数プロトタイプ 

```
ITMGPTT virtual int StopRecording()
```

#### サンプルコード 

```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```

### 録音のキャンセル
このAPIを呼び出して、録音をキャンセルします。キャンセルした後、コールバックが送信されません。
#### 関数プロトタイプ  

```
ITMGPTT virtual int CancelRecording()
```

#### サンプルコード 

```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```

### オフラインボイスマイクリアルタイム音量の取得
このAPIはマイクリアルタイム音量の取得に使用されます。戻り値はint型で、戻り値の範囲は0から100です。

#### 関数プロトタイプ  
```
ITMGPTT virtual int GetMicLevel()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetMicLevel();
```


### スピーカーリアムタイム音量の取得
このAPIはスピーカーリアルタイム音量の取得に使用されます。戻り値はint型で、戻り値の範囲は0から100です。

#### 関数プロトタイプ  
```
ITMGPTT virtual int GetSpeakerLevel()
```

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```





### ボイスファイルのアップロード
このAPIはボイスファイルのアップロードに使用されます。
#### 関数プロトタイプ 

```
ITMGPTT virtual void UploadRecordedFile(const char* filePath)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |ボイスのアップロードパス|

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```

### ボイスアップロード完成のコールバック
ボイスのアップロードが完了した後、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETEです。OnEvent関数でイベントメッセージを判断します。

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
		{
		//処理
		break;
		}
	}
}
```

### ボイスファイルのダウンロード
このAPIはボイスファイルのダウンロードに使用されます。
#### 関数プロトタイプ  

```
ITMGPTT virtual void DownloadRecordedFile(const char* fileId, const char* filePath) 
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileId  		|char*   	|ファイルのURLパス	|
| filePath 	|char*  	|ファイルのローカル保存パス	|

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```

### ボイスファイルダウンロード完了のコールバック
ボイスのダウンロードが完了した後、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE:
		{
		//処理
		break;
		}
	}
}
```

### ボイスの再生
このAPIはボイスの再生に使用されます。
#### 関数プロトタイプ  
```
ITMGPTT virtual void PlayRecordedFile(const char* filePath)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |ファイルパス|

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```

### ボイス再生のコールバック
ボイス再生のコールバック。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
		{
		//処理
		break;
		}
	}
}
```

### ボイス再生の停止
このAPIはボイス再生の停止に使用されます。
#### 関数プロトタイプ  
```
ITMGPTT virtual int StopPlayFile()
```

#### サンプルコード  

```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```

### ボイスファイルサイズの取得
このAPIによって、ボイスファイルのサイズを取得します。
#### 関数プロトタイプ  

```
ITMGPTT virtual int GetFileSize(const char* filePath)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |ボイスファイルのパス|

#### サンプルコード  

```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);
```

### ボイスファイル時間の取得
このAPIはボイスファイル時間の取得に使用され、単位はミリ秒です。
#### 関数プロトタイプ  

```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |ボイスファイルのパス|

#### サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```



### 指定ボイスファイルのテキスト認識
このAPIは指定されたボイスファイルをテキストに認識するために使用されます。
#### 関数プロトタイプ  

```
ITMGPTT virtual void SpeechToText(const char* fileID)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |char*                      |ボイスファイルURL|

#### サンプルコード  

```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```

### 指定ボイスファイルのテキスト翻訳（指定言語）
このAPIは指定されたボイスファイルを指定言語のテキストに翻訳するために使用されます。


####  関数プロトタイプ  
```
ITMGPTT virtual void SpeechToText(String fileID,String speechLanguage,String translateLanguage)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |char*                     |ボイスファイルURL|
| speechLanguage    |char*                     |指定したテキストの言語パラメータに識別します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください|
| translatelanguage    |char*                  |指定したテキストの言語パラメータに翻訳します。パラメータについては、[ボイステキスト変換の言語パラメータ参照リスト](https://cloud.tencent.com/document/product/607/30282)を参照してください。（このパラメータは一時的に無効です。入力したパラメータはspeechLanguageと一致する必要があります）|

####  サンプルコード  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```


### 認識コールバック
指定されたボイスファイルをテキストに認識するコールバック。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETEです。OnEvent関数でイベントメッセージを判断します。
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
		{
		//処理
		break;
		}
	}
}
```


## 高度なAPI

### 診断情報の取得
音声テレビ通話のリアルタイムの通話品質に関する情報を取得します。このAPIは、主にリアルタイムの通話品質の確認、トラブルシューティングなどに使用され、サービス側で無視してもかまいません。
#### 関数プロトタイプ  

```
ITMGRoom virtual const char* GetQualityTips()
```
#### サンプルコード  

```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```


### バージョン番号の取得
分析のために、SDKバージョン番号を取得します。
#### 関数プロトタイプ
```
ITMGContext virtual const char* GetSDKVersion()
```
#### サンプルコード  
```
ITMGContextGetInstance()->GetSDKVersion();
```

### プリントするログレベルの設定
プリントするログレベルの設定に使用されます。デフォルトのレベルにすることをお勧めします。
#### 関数プロトタイプ
```
ITMGContext virtual void SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

|パラメータ| タイプ|意味|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|ログ書き込みのレベルを設定します。TMG_LOG_LEVEL_NONEは書き込まないことを意味します|
|levelPrint|ITMG_LOG_LEVEL|プリントするログレベルを設定します。TMG_LOG_LEVEL_NONEはプリントしないことを意味します|


|ITMG_LOG_LEVEL|意味|
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0		|ログをプリントしない			|
|TMG_LOG_LEVEL_ERROR=1		|エラーログをプリント（デフォルト）	|
|TMG_LOG_LEVEL_INFO=2			|プロンプトログをプリント		|
|TMG_LOG_LEVEL_DEBUG=3		|開発デバッグログをプリント	|
|TMG_LOG_LEVEL_VERBOSE=4		|高頻度ログをプリント		|

#### サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->SetLogLevel(0,true,true);
```

### プリントするログのパスの設定
プリントするログのパスを設定するために使用されます。
デフォルトパス：

|プラットフォーム     |パス        |
| ------------- |:-------------:|
|Windows 	|%appdata%\Tencent\GME\ProcessName|
|iOS    		|Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android	|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### 関数プロトタイプ

```
ITMGContext virtual void SetLogPath(const char* logDir) 
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| logDir    		|char*    		|パス|

#### サンプルコード  

```
cosnt char* logDir = ""//自分でパスを設定
ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

### オーディオデータのブラックリストに追加
あるIDをオーディオデータブラックリストに追加します。戻り値が0の場合、呼び出し成功を表します。
#### 関数プロトタイプ  

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |char*       |ブラックリストに追加するID|

#### サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);
```

### オーディオデータのブラックリストから削除
あるIDをオーディオデータブラックリストから削除します。戻り値が0の場合、呼び出成功を表します。
#### 関数プロトタイプ  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |char*       |ブラックリストから削除するID|

#### サンプルコード  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
```


## コールバックメッセージ

#### メッセージリスト：

|メッセージ     | メッセージの意味   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|ボイスルーム参加のメッセージ		|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|ボイスルーム退出のメッセージ		|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT		|ネットワークなどによるルーム切断のメッセージ	|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE		|ルームタイプ変更イベント		|
|ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    	|マイクデバイス追加のメッセージ		|
|ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    	|マイクデバイス紛失のメッセージ		|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE	|スピーカーデバイス追加のメッセージ		|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE	|スピーカーデバイス紛失のメッセージ		|
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
