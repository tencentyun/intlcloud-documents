		
Unityを使う開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを行いやすいように、ここで、Unity 開発に適用されるクイックアクセス技術ドキュメントを説明させていただきます。		
		
GME クイックスタートドキュメントは最も主なアクセスインターフェースに関する内容のみを提供しています。 もっと詳しいインターフェース情報は[関連するインターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)をご参照ください。
			
|重要インターフェース     | インターフェースの意味|
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|EnterRoom |入室します  |
|EnableMic |マイクをオンにします |
|EnableSpeaker|スピーカーをオンにします |

>
- GMEを利用する前にプロジェクトを設定してください。設定しないと、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKであり、数値は0です。
- GMEのインターフェース呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには認証が必要です。ドキュメントの認証部分の内容をご参照ください。
- GMEは周期的にPollインターフェースを呼び出してイベントのコールバックをトリガーする必要があります
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、先に成功に入室する必要があります。
- エラーコードの詳細については、「エラーコード」(https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。

## クイックアクセスの手順
### 1、 SDKを初期化する
パラメータの取得については、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースはTencent CloudコンソールからのSDKAppID番号をパラメータとする必要があります。また、openIdも必要であり、このopenIdはユーザーの一意な識別子です。ルールはApp開発者により設定され、Appで重複してはなりません（現在、INT64のみに対応します）。
> 入室するには、SDKを先に初期化する必要があります。
####  関数のプロトタイプ

```
ITMGContext Init(string sdkAppID, string openID)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |String  |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |String  |openIdはInt64型しか対応していません（stringに変換してから渡されます）、この値は10000以上である必要があり、ユーザーを識別するために使われています。|

####  サンプルコード 

```
int ret = ITMGContext.GetInstance().Init(str_appId, str_userId);
	if (ret != QAVError.OK) {
		return;
	}
```
### 2、イベントコールバックをトリガーする
updateの中で、Pollを周期的に呼び出すことで、イベントのコールバックをトリガーすることができます。
####  関数のプロトタイプ

```
ITMGContext public abstract int Poll();
```

### 3、認証情報
関連機能の暗号化と認証に使われるAuthBufferを生成します。関連バックグラウンドのデプロイについては[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
オフライン音声取得の認証を行うとき、ルーム番号のパラメータをnull設定しなければなりません。

####  関数のプロトタイプ
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent CloudコンソールからのsdkAppId番号です。|
| roomId    |string   |ルーム番号であり、最大127文字まで対応しています（オフライン音声ルーム番号のパラメータをnullに設定しなければならない）。|
| openID    |string |ユーザーの識別子です。|
| key    |string |Tencent Cloud  [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです。|


####  サンプルコード  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId, userId, "a495dca2482589e9");
}
```
### 4、入室する
生成された認証情報でルームに参加します。入室するときに、デフォルトではマイクとスピーカーがオフになっています。


####  関数のプロトタイプ
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId|string    |ルーム番号は最大127文字まで対応しています。|
| roomType |ITMGRoomType|ルームのオーディオタイプです。|
| authBuffer |Byte[] |認証コードです。|

ルームのオーディオタイプについては、「音質選択」(https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### 5、入室イベントのコールバック
入室した後、デリゲート関数を介しコールバックを行う必要があります。その中にresultとerror_infoの二つの情報が含まれています。
####  関数のプロトタイプ
```
デリゲート関数：
public delegate void QAVEnterRoomComplete(int result, string error_info);
イベント関数：
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

####  サンプルコード  
```
イベントをリッスンします。
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

リッスン処理：
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
	    ShowWarnning (string.Format ("join room failed, err:{0}, errInfo:{1}", err, errInfo));
	    return;
	}else{
	    ShowWarnning (string.Format ("現在の音声ルームid:{0}、ほかの端末からこのルームに参加し通話してください",roomId ));
    }
}
```

### 6、マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使われています。入室する際に、マイクとスピーカーはデフォルトでオフになっています。

####  関数のプロトタイプ  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |マイクをオンにする必要がある場合は、渡されたパラメータはtrueです、マイクをオフにする場合は、パラメータはfalseです。|

####  サンプルコード  
```
マイクをオンにします
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```


### 7、スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使われています。
####  関数のプロトタイプ  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |スピーカーをオフにする必要がある場合は、渡されたパラメータはfalseです、スピーカーをオンにする場合、パラメータはtrueです。|

####  サンプルコード  
```
スピーカーをオンにします
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

