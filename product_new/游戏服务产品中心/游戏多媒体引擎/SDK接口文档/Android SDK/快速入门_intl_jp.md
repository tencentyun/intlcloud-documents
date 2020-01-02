Androidを使う開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを手軽に実行できるように、ここで、Android開発に向けるクイックアクセスドキュメントについて説明させていただきます。



GMEクイックスタートドキュメントには、最も重要なアクセスインターフェイスに関する内容のみが提供されています。より詳細なインターフェイスについては、[関連インターフェイスドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)をご参照ください。

|重要インターフェース     | インターフェースの意味|
| ------------- |:-------------:|
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|EnterRoom |入室します  |
|EnableMic |マイクをオンにします |
|EnableSpeaker|スピーカーをオンにします |

>
- GMEを利用する前にプロジェクトを構成してください。構成しないと、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKであり、値は0です。
- GMEのインターフェース呼び出しは同じスレッドで行う必要があります。
- GMEで入室するには、認証が必要です。このドキュメントの認証に関する内容をご参照ください。
- GMEは周期的にPollインターフェースを呼び出し、イベントのコールバックをトリガーする必要があります。
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、先に入室に成功する必要があります。
- エラーコードの詳細について、「エラーコード」(https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。

## クイックアクセスの手順

### 1、シングルトンを取得する
音声機能を使用する場合、先にITMGContextオブジェクトを取得する必要があります。
####  関数のプロトタイプ 

```
public static ITMGContext GetInstance(Context context)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| context    |Context |アプリケーションのコンテキストオブジェクトです|


####  サンプルコード  

```
import com.tencent.TMG.ITMGContext; 
TMGContext.getInstance(this);
```

### 2、SDKを初期化する

パラメータの取得については、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースでは、Tencent CloudコンソールからのSDKAppID番号をパラメータとして、さらにopenIdを付け加える必要があります。このopenIdはユーザーの一意な識別子です。ルールはApp開発者によって定めらおれ、app内で重複することがなければ問題がありません（現在はINT64のみをサポートしています）。
>入室するには、先にSDKを初期化する必要があります。
####  関数のプロトタイプ

```
ITMGContext public int Init(String sdkAppId, String openId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |String  |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |String  |openIdはInt64型のみをサポートする（stringに変換されて渡されます）。openIdは10000より大きくする必要があり、ユーザーの識別に使用されます|

####  サンプルコード 


```
ITMGContext.GetInstance(this).Init(sdkAppId, openId);
```
### 3、イベントコールバックをトリガーする
updateでPollを周期的に呼び出すことで、イベントコールバックをトリガーすることができます。

####  関数のプロトタイプ

```
ITMGContext int Poll()
```
####  サンプルコード
```
ITMGContext.GetInstance(this).Poll();
```

### 4、認証情報
AuthBufferを生成し、関連機能の暗号化と認証に使用されます。関連バックグラウンドのデプロイについては、[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
オフライン音声の認証を取得する時、ルーム番号のパラメータはnullに設定する必要があります。

####  関数のプロトタイプ
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent CloudコンソールからのsdkAppId番号です|
| roomId    |string   |ルーム番号は最大127文字をサポートします（オフライン音声のルーム番号のパラメータはnullに設定する必要があります）|
| openID    |string |ユーザー標識です|
| key    |string |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|


####  サンプルコード  
```
import com.tencent.av.sig.AuthBuffer;//ヘッダーファイル
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,identifier, key);
```


### 5、入室する
生成された認証情報を使って入室した場合、メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMであるコールバックを受信できます。入室する際に、マイクとスピーカーはデフォルトでオフになっています。戻り値がAV_OKである場合、成功したことを示します。

####  関数のプロトタイプ
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId|string    |ルーム番号は最大127文字をサポートします|
| roomType |int|ルームのオーディオタイプです|
| authBuffer |Byte[] |認証コードです|

ルームのオーディオタイプについては、「音質選択」(https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

### 6、入室イベントのコールバック
入室してから、メッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMを送信します、OnEvent関数で判断します。
コールバックに関する参照コードを設定します。

```
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```
コールバック処理の関連参照コード
####  サンプルコード  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	 / /入室成功イベントを受信した
        }
	}
```

### 7、マイクのをオン/オフ
このインターフェースは、マイクのオン/オフに使用されます。入室する際、マイクとスピーカーはデフォルトでオフになっています。

####  関数のプロトタイプ  
```
ITMGContext public int EnableMic(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled   |boolean     |マイクをオンにする場合、渡されたパラメータはtrueであり、マイクをオフにする場合、パラメータはfalseになります|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```


### 8、スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使用されます。

####  関数のプロトタイプ  
```
ITMGContext public int EnableSpeaker(boolean isEnabled)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |スピーカーをオフにする場合、渡されたパラメータはfalseであり、スピーカーをオンにすると、パラメータはtrueになります|

####  サンプルコード  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

