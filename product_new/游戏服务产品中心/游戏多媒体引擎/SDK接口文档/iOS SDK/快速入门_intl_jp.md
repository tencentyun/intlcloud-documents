iOSを使う開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを行いやすいように、ここで、iOS 開発に適用されるクイックアクセス技術ドキュメントを説明させていただきます。

GMEクイックスタートドキュメントは最も主なアクセスインターフェースに関する内容のみを提供しています。もっと詳しいなインターフェース情報は[関連するインターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)をご参照してください。


|重要インターフェース     | インターフェースの意味|
| ------------- |:-------------:|
|InitEngine           | GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|SetDefaultAudienceAudioCategory |バックグラウンドを設定します|
|EnterRoom |入室します |
|EnableMic |マイクをオンにします |
|EnableSpeaker|スピーカーをオンにします|

>
- GMEを利用する前にプロジェクトを設定してください。設定しないと、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後に、戻り値はQAVError.OKであり、数値が0です。
- GMEのインターフェース呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには認証が必要です。ドキュメントにおける認証に関する内容をご参照ください。
- GMEは周期的にPollインターフェースを呼び出し、イベントのコールバックをトリガーする必要があります。
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、先に成功に入室する必要があります。
- エラーコードの詳細について、[エラーコード](https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。


## クイックアクセスの手順
### 1、シングルトンを取得する
音声機能を利用する場合、先にITMGContextオブジェクトを取得する必要があります。

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
パラメータの取得については、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースはTencent CloudコンソールからのSDKAppID番号をパラメータとする必要があります。また、openIdも必要であり、このopenIdはユーザーの一意な識別子です。ルールはApp開発者により設定され、Appでは重複してはなりません（現在、INT64のみに対応しています）。
>入室するには、先にSDKを初期化する必要があります。
####  関数のプロトタイプ

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |NSString  |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |NSString |openIdはInt64型のみを対応します（stringに変換して渡されます）、この値は10000以上である必要があり、ユーザーの識別に使われています。|

####  サンプルコード 


```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```
### 3、イベントのコールバックをトリガーする
updateの中で、Pollを周期的に呼び出すことにより、イベントのコールバックをトリガーすることができます。
####  関数のプロトタイプ

```
ITMGContext -(void)Poll
```
####  サンプルコード
```
[[ITMGContext GetInstance] Poll];
```

### 4、認証情報
関連機能の暗号化と認証に使われるAuthBufferを生成します。関連するバックグラウンドのデプロイについては[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
オフライン音声取得の認証を行うとき、ルーム番号のパラメータをnullに設定しなければなりません。

####  関数のプロトタイプ
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    |int    |Tencent CloudコンソールからのsdkAppId番号です|
| roomId    |NSString   |ルーム番号は最大127文字まで対応しています（オフライン音声ルーム番号のパラメータをnullに設定しなければならない）|
| openID  |NSString    |ユーザーの識別子です|
| key    |NSString   |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|


####  サンプルコード  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```
### 5、入室する
生成された認証情報で入室する場合、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというコールバックのメッセージを受信します。入室に際し、デフォルトではマイクとスピーカーはオフになっています。戻り値がAV_OKの場合、成功に入室したことを示しています。
####  関数のプロトタイプ
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId|NSString |ルーム番号は最大127バイトまで対応しています|
| roomType |int|ルームオーディオタイプです|
| authBuffer    |NSData    |認証コードです|

ルームのオーディオタイプについては、[音質選択](https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 6、入室イベントのコールバック
入室してから、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージが送信され、OnEvent関数で判断します。

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
           	 / /入室成功イベントを受信しました
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
このインターフェースは、マイクのオン/オフに使われています。入室に際し、マイクとスピーカーはデフォルトでオフになっています。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled   |boolean     |マイクをオンにする場合、渡されたパラメータは YESです、マイクをオフにする場合、パラメータはNOです|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```


### 8、スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使われています。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |スピーカーをオフにする場合、渡されたパラメータはNOです、スピーカーをオンにする場合、パラメータはYESです|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```


