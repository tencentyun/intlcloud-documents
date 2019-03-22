iOS開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでiOS開発のためのクイック導入文書を紹介します。


## フローチャート
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)

GMEクイックスタートドキュメントは最も重要な導入APIを提供します。APIの詳細については、[関連APIドキュメント](https://cloud.tencent.com/document/product/607/15221)を参照してください。


|重要なAPI     | APIの意味|
| ------------- |:-------------:|
|InitEngine    				       	|GMEの初期化 	|
|Poll    		|イベントコールバックのトリガ	|
|SetDefaultAudienceAudioCategory 	|バックグラウンド設定|
|EnterRoom	 	|ルームに参加  		|
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
ITMGContext ITMGDelegate <NSObject>
```
####  サンプルコード  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```



### 2. SDKの初期化
パラメータの取得については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはアプリ開発者によって定められ、アプリ内で繰り返さないようにします（現在INT64のみ対応）。
SDKを初期化してから、ルームに参加できます。
####  関数プロトタイプ

```
ITMGContext -(void)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    	|NSString  |Tencent CloudコンソールからのSdkAppId番号				|
| openID    		|NSString  |OpenIDはInt64型（string型に変換して渡す）のみをサポートし、10000以上で、ユーザー識別用 |

####  サンプルコード 
```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```

### 3. イベントコールバックのトリガ
updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。
####  関数プロトタイプ

```
ITMGContext -(void)Poll
```
####  サンプルコード
```
[[ITMGContext GetInstance] Poll];
```

### 4. ルームへの参加
生成した認証情報を用いてルームに参加するとき、コールバックとしてメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMが受信されます。
- ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。
- EnterRoom APIを呼び出す前に、InitEngine APIを呼び出す必要があります。

####  関数プロトタイプ
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId 	|NSString		|ルームID、127文字まで入力可能|
| roomType 	|int		|ルームオーディオタイプ		|
| authBuffer	|NSData	|認証コード				|

ルームオーディオタイプについては、[音質選択](https://cloud.tencent.com/document/product/607/18522)を参照してください。

####  サンプルコード  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 5. ルーム参加イベントのコールバック
ルームに参加した後、コールバックがあります。メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMです。
コールバックの関連参照コードを設定します。

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```
コールバック処理の関連参照コード。
####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
            //ルーム参加完了イベント受信
        }
            break;
     }
}
```

### 6. マイクのオン/オフ
このAPIはマイクのオン/オフに使用されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。

####  関数プロトタイプ  
```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |マイクをオンにする必要があれば、渡されたパラメータはYESとなります。マイクをオフにすれば、パラメータはNOとなります|

####  サンプルコード   
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```


### 7. スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。

####  関数プロトタイプ 
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |スピーカーをオフにする必要があれば、渡されたパラメータはNOとなります。スピーカーをオンにすれば、パラメータはYESとなります|

####  サンプルコード
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```


## 認証について
### 認証情報
AuthBufferを生成し、関連機能の暗号化と認証に使用されます。関連バックグラウンド配置については、[GME暗号鍵ドキュメント](https://cloud.tencent.com/document/product/607/12218)を参照してください。オフラインボイスで認証を取得したとき、ルームIDパラメータにはnullを入力することが必要です。
このAPIの戻り値はNSData型です。

####  関数プロトタイプ
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId identifier:(NSString*)identifier key:(NSString*)key;
+ @end
```
|パラメータ    | タイプ         |意味|
| ------------- |:-------------:|-------------|
| appId    		|int   		|Tencent CloudコンソールからのSdkAppId番号		|
| roomId    		|NSString  	|ルームID、127文字まで入力可能（オフラインボイスのルームIDパラメータにはnullを入力することが必要）	|
| identifier  		|NSString    	|ユーザーID								|
| key    			|NSString    	|Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme)からの暗号鍵					|



#### サンプルコード  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```

