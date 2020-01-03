macOSを使う開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを手軽に実行できるように、ここで、macOSでの開発に向けるクイックアクセス技術ドキュメントについて説明させていただきます。

GMEクイックスタートドキュメントには、最も重要なアクセスインターフェイスに関する内容のみが提供されています、より詳細なインターフェイスについては、[関連インターフェイスドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)をご参照ください。


|重要インターフェース     | インターフェースの意味|
| ------------- |:-------------:|
|InitEngine           |GMEを初期化します|
|Poll    |イベントコールバックをトリガーします|
|EnterRoom |入室します  |
|EnableMic |マイクをオンにします |
|EnableSpeaker|スピーカーをオンにします |

>
- GMEを利用する前にプロジェクトを構成してください。構成しないと、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKになり、値は0になります。
- GMEのインターフェースの呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには、認証が必要です。このドキュメント認証に関する内容を参照してください。
- GMEは周期的にPollインターフェースを呼び出して、イベントのコールバックをトリガーする必要があります。
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、先に入室に成功する必要があります。
- エラーコードの詳細について、「エラーコード」(https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。


## クイックアクセスの手順
### 1、シングルトンを取得する
音声機能を使用する場合、先にITMGContextオブジェクトを取得する必要があります。

####  関数のプロトタイプ 

```
ITMGContext ITMGDelegate <NSObject>
```
####  サンプルコード  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```



### 2、SDKを初期化する
パラメータの取得について、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースでは、Tencent CloudコンソールからのSDKAppID番号をパラメータとして、さらにopenIdを付け加える必要があります。このopenIdはユーザーの一意な識別子です。ルールはApp開発者によって定められ、App内で重複することがなければ問題がありません（現在はINT64のみをサポートしています）。
>入室するには、先にSDKを初期化する必要があります。
####  関数のプロトタイプ

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openId
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |NSString  |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |NSString  |openIdはInt64型のみをサポートします（stringに変換され、渡されます）。この値は10000以下にならなく、ユーザーを標識する値です|

####  サンプルコード 


```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```
### 3、イベントコールバックをトリガーする
updateの中で、Pollを周期的に呼び出すことで、イベントコールバックをトリガーすることができます。
####  関数のプロトタイプ

```
ITMGContext -(void)Poll
```
####  サンプルコード
```
[[ITMGContext GetInstance] Poll];
```

### 4、認証情報
AuthBufferを生成し、関連機能の暗号化と認証に使用します。関連バックグラウンドのデプロイについては、[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
オフライン音声取得の認証を行うとき、ルーム番号のパラメータをnullに設定する必要があります。

####  関数のプロトタイプ
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int    |Tencent CloudコンソールからのsdkAppId番号です|
| roomId    |NSString  |ルーム番号は最大127文字までをサポートします（オフライン音声ルーム番号パラメータをnullに設定する必要があります）|
| openID  |NSString    |ユーザー標識です|
| key    |NSString    |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|


####  サンプルコード  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```
### 5、入室する
生成された認証情報を使って入室する場合、メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMのコールバックを受信します。入室した際に、マイクとスピーカーはデフォルトでオフになっています。戻り値がAV_OKの場合、成功したことを示します。
####  関数のプロトタイプ
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId |NSString|ルーム番号は最大127文字までサポートします|
| roomType |int|ルームのオーディオタイプです|
| authBuffer    |NSData    |認証コードです|

ルームのオーディオタイプについては、「音質選択」(https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 6、入室イベントのコールバック
入室してから、メッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMを送信し、OnEvent関数で判断します。

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```
コールバック処理の関連参照コード

####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
           	 / /入室成功イベントを受信した
        }
            break;
	}
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|

### 7、マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使用されます。入室する際、マイクとスピーカーはデフォルトでオフになっています。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |マイクをオンにする場合、渡されたパラメータはYESであり、マイクをオフにする場合、パラメータはNOです|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```


### 8、スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使用されます。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |スピーカーをオフにする場合、渡されたパラメータはNOであり、スピーカーをオンにする場合、パラメータはYESです|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```


