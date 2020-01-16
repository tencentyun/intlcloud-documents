Cocos2Dを使う開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを行いやすいように、ここで、Cocos2D 開発に適用されるクイックアクセス技術ドキュメントを説明させていただきます。


GME クイックスタートドキュメンテートは最も主なアクセスインターフェースに関する内容のみを提供しています、 もっと詳しいなインターフェース情報は[関連するインターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)をご参照ください。


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
- GMEのインターフェース呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには認証が必要です。ドキュメントにおける認証部分の内容をご参照ください。
- GMEは周期的にPollインターフェースを呼び出し、イベントのコールバックをトリガーする必要があります。
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、先に成功に入室する必要があります。
- エラーコードの詳細については、[エラーコード](https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。


## クイックアクセスの手順
### 1、シングルトンを取得する
音声機能を使用する場合、先にITMGContextオブジェクトを取得する必要があります。

####  サンプルコード  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### 2、 SDKを初期化する
パラメータの取得については、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースはTencent CloudコンソールからのSDKAppID番号をパラメータとする必要があります。また、openIdも必要であり、このopenIdはユーザーの一意な識別子です。ルールはApp開発者により設定され、Appで重複してはなりません（現在、INT64のみに対応しています）。
>入室するには、SDKを先に初期化する必要があります。
####  関数のプロトタイプ

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openID)
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |char*   |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |char*   |openIdはInt64型のみ（string*に変換して渡されます）をサポートし、10000以上である必要があり、ユーザーの識別に使われています |

####  サンプルコード 


```
#define SDKAPPID3RD "1400035750"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```
### 3、イベントのコールバックをトリガーする
updateの中で、Pollを周期的に呼び出すことにより、イベントのコールバックをトリガーすることができます。
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
ITMGContextGetInstance()->Poll();
```


### 4、認証情報
関連機能の暗号化と認証に使われるAuthBufferを生成します。関連するバックグラウンドのデプロイについては[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。  
オフライン音声取得の認証を行うときに、ルーム番号のパラメータをnullに設定しなければなりません。

####  関数のプロトタイプ
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent CloudコンソールからのsdkAppId番号です|
| strRoomID    |char*     |ルーム番号は最大127バイトまで可能です（オフライン音声ルーム番号のパラメータは、nullに設定しなければならない）|
| strOpenID  |char*     |ユーザーの識別子です|
| key    |string |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|
|strAuthBuffer|char*    |戻された authbuffです|
| bufferLength   |int    |渡されたauthbuffの長さは500であることを推奨します|



####  サンプルコード  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```


### 5、入室する
生成された認証情報をで入室する場合、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージのコールバックを受信します。入室に際し、デフォルトではマイクとスピーカーはオフになっています。戻り値がAV_OKの場合、入室に成功したことを示しています。
- 入室に際し、デフォルトではマイクとスピーカーはオフになっています。
-  EnterRoomインターフェースを呼び出す前に先にInitインターフェースを呼び出す必要があります。

####   関数のプロトタイプ
```
ITMGContext virtual int EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//一般入室インターフェース
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomID| char*    |ルーム番号は最大127バイトまで可能です|
| roomType |ITMGRoomType|ルームのオーディオタイプです|
| authBuffer    |char*     |認証コードです|
| buffLen   |int   |認証コードの長さです|

ルームのオーディオタイプについては、[音質選択](https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 6、入室イベントのコールバック
入室してから、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージが送信され、OnEvent関数で判断します。

####  サンプルコード  
```

void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
		}
	}
}
```

### 7、マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使われています。入室に際し、デフォルトではマイクとスピーカーはオフになっています。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual void EnableMic(bool bEnabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |マイクをオンにする場合、渡されたパラメータはtrueです、マイクをオフにする場合、パラメータはfalseです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```


### 8、スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使われています。

####  関数のプロトタイプ  
```
ITMGAudioCtrl virtual void EnableSpeaker(bool enabled)
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable   |bool       |スピーカーをオフにする場合、渡されたパラメータはfalseです、スピーカーをオンにする場合、パラメータはtrueです|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```



