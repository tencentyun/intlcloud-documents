macOSを使う開発者がTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを行いやすいように、ここで、macOSでの開発に向けるアクセス技術ドキュメントについて説明させていただきます。

>このドキュメントはGME sdk version：2.5に対応しています。

## GME利用上の重要事項

|重要インターフェース     | インターフェースの意味|
| ------------- |:-------------:|
|InitEngine           |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|EnterRoom |入室します  |
|EnableMic |マイクをオンにします |
|EnableSpeaker|スピーカーをオンにします |

>
- GMEを利用する前にプロジェクトを設定してください、設定しないと、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKであり、値は0です。
- GMEのインターフェース呼び出しは、同じスレッドで行う必要があります。
- GMEで入室するには、認証が必要です。ドキュメントにおける認証部分の内容をご参照ください。
- GMEは周期的にPollインターフェースを呼び出し、イベントのコールバックをトリガーします。
- GMEのコールバック情報については、コールバックメッセージリストをご参照ください。
- デバイスを操作するには、先に入室に成功する必要があります。
- エラーコードの詳細については、「エラーコード」(https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。

## リアルタイム音声のフローチャート
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 関連インターフェースの初期化
初期化される前に、SDKは未初期化段階にあります。リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
- 利用問題については、「一般的な問題」(https://intl.cloud.tencent.com/document/product/607/30254)をご参照ください。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|InitEngine           |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |

### シングルトンの取得
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

###メッセージング
インターフェース類はDelegate方式でアプリケーションにコールバック通知を送信します、メッセージタイプはITMG_MAIN_EVENT_TYPEをご参照ください。メッセージの内容は辞書であり、コールバックの情報の受信に使われています。
####  関数のプロトタイプ

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```



####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
		switch (eventType) {
			//eventTypeの判断
			}
	}
```





### SDKの初期化

パラメータの取得については、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースはTencent CloudコンソールからのSDKAppID番号をパラメータとする必要があります。また、openIdも必要です、このopenIdはユーザーの唯一の標識です。ルールはApp開発者により設定され、Appでは重複されてはなりません（現在、INT64のみに対応しています）。
>入室するには、SDKを先に初期化する必要があります。
>
>####  関数のプロトタイプ

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openId
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| sdkAppId    |NSString  |Tencent CloudコンソールからのsdkAppId番号です|
| openId    |NSString  |openIdはInt64のみをサポートします（stringに変換され、渡されます）。この値は10000以上である必要があり、ユーザーを識別に使用されます。|

####  サンプルコード 


```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```
### イベントのコールバックをトリガーする
updateの中で、Pollを周期的に呼び出すことで、イベントのコールバックをトリガーすることができます。
####  関数のプロトタイプ

```
ITMGContext -(void)Poll
```
####  サンプルコード
```
[[ITMGContext GetInstance] Poll];
```

### システムの一時停止
システムにPauseイベントが発生した場合、エンジンに通知を出し、Pauseを実行させる必要があります。
####  関数のプロトタイプ

```
ITMGContext -(QAVResult)Pause
```

### システムリカバー
システムにResumeイベントが発生した場合、エンジンに通知を出し、Resumeを実行させる必要があります。Resumeインターフェースはリアルタイム音声のみをリカバーします。
####  関数のプロトタイプ

```
ITMGContext -(QAVResult)Resume
```



### SDKの未初期化
SDKを未初期化にして、未初期化状態にします。アカウントを切り替えるには、SDKを未初期化にする必要があります。
####  関数のプロトタイプ

```
ITMGContext -(void)Uninit
```
####  サンプルコード
```
[[ITMGContext GetInstance] Uninit];
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
関連機能の暗号化と認証に使われるAuthBufferを生成します。関連バックグラウンドのデプロイについては[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    
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
| roomId    |NSString  |ルーム番号であり、最大127文字までサポートします（オフライン音声ルーム番号パラメータをnullに設定しなければなりません）|
| openID  |NSString    |ユーザー識別です|
| key    |NSString    |Tencent Cloud [コンソール](https://console.cloud.tencent.com/gamegme) からのキーです|


####  サンプルコード  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```



### 入室
生成された認証情報で入室した場合、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージがのコールバックを受信します。入室に際し、マイクとスピーカーはデフォルトでオフになっています。戻り値がAV_OKの場合、入室が成功したことを示しています。


####  関数のプロトタイプ
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| roomId |NSString|ルーム番号であり、最大127文字までサポートします|
| roomType |int|ルームオーディオタイプです|
| authBuffer    |NSData    |認証コードです|

ルームのオーディオタイプについては、「音質選択」(https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。


####  サンプルコード  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

## 入室イベントのコールバック
入室してから、メッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMを送信し、OnEvent関数において判断されます。

####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
           	 / /入室成功イベントの受信
        }
            break;
	}
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|


### 入室しているかの判断
このインターフェースを呼び出すことで、入室しているかを判断できます。戻り値はbool型です。
####  関数のプロトタイプ  
```
ITMGContext -(BOOL)IsRoomEntered
```
####  サンプルコード  
```
[[ITMGContext GetInstance] IsRoomEntered];
```

### 退室
このインターフェースを呼び出すことで、ルームから退出できます。このインターフェースは非同期であり、戻り値AV_OKの意味は、非同期送信が成功したことです。

>アプリケーション中に退室してからまたすぐ入室する場合、インターフェースを呼び出す際に、開発者はExitRoomのコールバックRoomExitComplete通知を待つ必要がなく、インターフェースを直接に呼び出せばよいです。

####  関数のプロトタイプ  
```
ITMGContext -(int)ExitRoom
```
####  サンプルコード  
```
[[ITMGContext GetInstance] ExitRoom];
```

### 退室のコールバック
退室してからは、メッセージがITMG_MAIN_EVENT_TYPE_EXIT_ROOMのコールバックが発生します。
####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM：
        {
            //退室成功イベントの受信
        }
            break;
    }
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|


### ユーザールームのオーディオタイプの変更
このインターフェースは、ユーザールームのオーディオタイプの変更に使われています。その結果は、コールバックイベントをご参照ください。イベントタイプはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。
####  関数のプロトタイプ  
```
ITMGContext GetRoom -(void)ChangeRoomType:(int)nRoomType
```


|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| nRoomType    |int    |切り替えたいルームタイプです。ルームのオーディオタイプについては、EnterRoomインターフェースをご参照ください|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetRoom ]ChangeRoomType:_roomType];
```


### ユーザールームのオーディオタイプの取得
このインターフェースはユーザールームのオーディオタイプを取得するために使用されます、戻り値はルームのオーディオタイプです。戻り値が0であることは、ユーザールームのオーディオタイプの取得にエラーが発生したことを示しています、ルームのオーディオタイプについてはEnterRoomインターフェースをご参照ください。

####  関数のプロトタイプ  
```
ITMGContext GetRoom -(int)GetRoomType
```

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetRoom ]GetRoomType];
```


### ルームタイプ設定完了のコールバック
ルームタイプの設定が完了したあと、コールバックのイベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEであり、返されるパラメータはresult、error_infoとnew_room_typeです。new_room_typeは次の情報を示しており、OnEvent関数においてイベントメッセージを判断します。

|イベントのサブタイプ     | 代表的パラメータ   |意味|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |入室に際し、固有のオーディオタイプはルームタイプと不一致であるため、入室するルームのオーディオタイプに変更されました|
| ITMG_ROOM_CHANGE_EVENT_START|2|入室済みで、オーディオタイプ切り替え中です（例えば、ChangeRoomTypeインターフェースを呼び出してからオーディオタイプを切り替えます）|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|入室済みで、オーディオタイプは切り替え済みです|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|ルームメンバーが ChangeRoomTypeインターフェースを呼び出し、ルームのオーディオタイプの切り替えをリクエストします|


####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
 		case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
			//処理
	 }
    }
}
```

#### Dataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


### メンバー状態の変更
このイベントについては、状態の変更があった時にのみ通知されます、変更がない場合は、通知されません。リアルタイムにメンバー状態を取得する必要がある場合は、上位レイヤーが通知を受信した時にキャッシュしてください。イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEであり、そのうちdataはevent_idとuser_listの二つの情報を含んでおり、OnEvent関数においてイベントメッセージを判断します。
オーディオイベントの通知はしきい値があり、そのしきい値を超えた場合に通知されます。2秒を超えてもオーディオパケットを受信していない場合にのみ、「メンバーがオーディオパケットの送信を停止しました」という通知を送信します。

|event_id     | 意味         |アプリケーション側のメンテナンス内容|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |メンバーが入室しました|アプリケーション側でメンバーリストをメンテナンスします|
|ITMG_EVENT_ID_USER_EXIT    |メンバーが退室しました|アプリケーション側でメンバーリストをメンテナンスします|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |メンバーがオーディオパケットを送信しています|アプリケーション側で通信メンバーのリストをメンテナンスします|
|ITMG_EVENT_ID_USER_NO_AUDIO    |メンバーがオーディオパケットの送信を停止しました|アプリケーション側で通信メンバーのリストをメンテナンスします|

####  サンプルコード  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//処理
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
			    //メンバーがオーディオパケットを送信します
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //メンバーがオーディオパケットの送信を停止しました
			    break;
 		    }
		break;
		}
    }
}
```

### 品質モニタニングイベント
品質モニタニングイベントであり、イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYで、返されるパラメータはweight、flossとdelayであり、次の情報を示しており、OnEvent関数においてイベントメッセージを判断します。

|パラメータ     | 意味        |
| ------------- |-------------|
|weight    |範囲は1～5であり、値5は極めて高い音質であり、値1は使えないほどの低い音質です。0はデフォルト値であり、意味がありません|
|floss    |パケットロス率です|
|delay    |オーディオ到達のディレー時間（ms）です|




### メッセージの詳細

|メッセージ    | メッセージの意味   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |オーディオ・ビデオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオ・ビデオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネットワークなどの原因により、ルームの接続が切れました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|ルームタイプ変更イベントです|

### メッセージに対応するDataの詳細
|メッセージ     | Data         |例|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


## リアルタイム音声のオーディオインターフェース
SDKを初期化し入室してから、ルーム内でリアルタイム音声の関連インターフェースを呼び出すことができます。
ユーザーインターフェースでマイク/スピーカーのボタンをオン/オフにする場合は、次の方式をお薦めします。
- 大部分のゲームAppに対しては、EnableMicとEnableSpeakerインターフェースを呼び出すことをお薦めします。これは、常にEnableAudioCaptureDevice/EnableAudioSendとEnableAudioPlayDevice/EnableAudioRecvインターフェースの両方を同時に呼び出すことに相当します。
- その他のモバイル端末App（例えばソーシャルApp）では、採集デバイスのオン/オフは、デバイス全体の（採集と再生）リスタートを伴っています。AppがBGMを再生している場合、BGMの再生も停止されます。上り/下りをコントロールすることによりマイクをオン/オフにするのは、再生デバイスの稼働を中断することがありません。具体的な呼び出し方式は、入室する時にEnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true)を一回呼び出し、マイクのオン/オフをクリックする時は、EnableAudioSend/Recのみを呼び出しオーディオストリームを送信/受信するかどうかをコントロールします。
- 採集デバイスまたは再生デバイスのみをリリースする場合は、インターフェースEnableAudioCaptureDeviceとEnableAudioPlayDeviceをご参照ください。
- pauseを呼び出しオーディオエンジンを一時的に停止し、resumeを呼び出しオーディオエンジンをリカバーします。

|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
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
|GetRecvStreamLevel|ほかのルームメンバーのリアルタイム下りボリュームを取得します|
|SetSpeakerVolume    |スピーカーのボリュームを設定します|
|GetSpeakerVolume    |スピーカーのボリュームを取得します|
|EnableLoopBack    |インイヤ・モニタリングをオン/オフにします|



### マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使われています。入室に際し、マイクとスピーカーはデフォルトでオフになっています。
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableMic:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled   |boolean     |マイクをオンにする場合、渡されるパラメータはtrueであり、マイクをオフにする場合、パラメータはfalseです|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```

### マイク状態の取得
このインターフェースはマイクの状態の取得に使われています。戻り値0はオフ状態を示し、戻り値1はオン状態を示しています。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetMicState
```
####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicState];
```

### 採集デバイスのオン/オフ
このインターフェースは、採集デバイスのオン/オフに使われています。入室に際し、デバイスはデフォルトでオフになっています。
- このインターフェースは、入室後にのみ呼び出すことができます。退室した後、デバイスは自動的にオフになります。
- モバイル端末における採集デバイスの起動は、一般的に権限申請やボリュームタイプの調整を伴っています。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |BOOL     |採集デバイスをオンにする場合、渡されるパラメータはYESであり、採集デバイスをオフにする場合、パラメータはNOです|

####  サンプルコード

```
採集デバイスをオンにします
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioCaptureDevice:enabled];
```

### 採集デバイス状態の取得
このインターフェースは、デバイス状態の取得に使われています。
####  関数のプロトタイプ

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioCaptureDeviceEnabled
```
####  サンプルコード

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];
```

### オーディオ上りのオン/オフ
このインターフェースは、オーディオ上りのオン/オフに使われています。採集デバイスがオンになっている場合は、採集したオーディオデータを送信します。採集デバイスがオフになっている場合は、ミュート状態が続きます。採集デバイスのオン/オフは、インターフェースEnableAudioCaptureDeviceをご参照ください。

####  関数のプロトタイプ

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioSend:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |BOOL     |オーディオ上りをオンにする場合、渡されるパラメータはYESであり、オーディオ上りをオフにする場合、パラメータはNOです|

####  サンプルコード  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioSend:enabled];
```

### オーディオ上り状態の取得
このインターフェースは、オーディオ上り状態の取得に使われています。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(BOOL)IsAudioSendEnabled
```
####  サンプルコード  
```
BOOL IsAudioSend =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];
```

### マイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使われ、戻り値がint型です。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetMicLevel
```
####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];
```

### オーディオ上りのリアルタイムボリュームの取得
このインターフェースは、オーディオ上りのリアルタイムボリュームの取得に使われています。その戻り値はint型であり、数値範囲が0～100です。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetSendStreamLevel()
```
####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSendStreamLevel];
```

### マイクボリュームの設定
このインターフェースは、マイクボリュームの設定に使われています。パラメータvolumeはマイクボリュームの設定に使われ、値が0の場合はミュートを示し、100の場合はボリュームの増減がないことを示しています、そのデフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(QAVResult)SetMicVolume:(int) volume
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int      |ボリューム設定で、数値範囲が0～200です。|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];
```
###  マイクボリュームの取得
このインターフェースは、マイクボリュームの取得に使われています。戻り値はint型であり、戻り値は101である場合は、インターフェースSetMicVolumeを呼び出したことがないことを示しています。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int) GetMicVolume
```
####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];
```

### スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使われています。
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |スピーカーをオフにする場合、渡されるパラメータはNOであり、スピーカーをオンにする場合、パラメータはYESです|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```

### スピーカー状態の取得
このインターフェースは、スピーカー状態の取得に使われています。戻り値が0の場合、スピーカーがオフにし、戻り値が1の場合、スピーカーがオンにし、戻り値が2の場合、スピーカーが稼働していることを示します。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerState
```

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerState];
```



### 再生デバイスのオン/オフ
このインターフェースは、再生デバイスのオン/オフに使われています。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioPlayDevice:(BOOL)enabled
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enabled    |BOOL        |再生デバイスをオフにする場合、渡されるパラメータはNOであり、再生デバイスをオンにする場合、パラメータはYESです|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioPlayDevice:enabled];
```

### 再生デバイスの状態の取得
このインターフェースは、再生デバイスの状態の取得に使われています。
####  関数のプロトタイプ

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioPlayDeviceEnabled
```
####  サンプルコード  

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];
```

### オーディオ下りのオン/オフ
このインターフェースは、オーディオ下りのオン/オフに使われています。再生デバイスがオンになっている場合は、ほかのルームメンバーのオーディオデータを再生します。再生デバイスがオフになっている場合は、ミュート状態が続きます。再生デバイスのオン/オフは、インターフェースEnableAudioPlayDeviceをご参照ください。

####  関数のプロトタイプ  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioRecv:(BOOL)enabled
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enabled    |BOOL     |オーディオ下りをオンにする場合、渡されるパラメータはYESであり、オーディオ下りをオフにする場合、パラメータはNOです|

####  サンプルコード  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioRecv:enabled];
```



### オーディオ下り状態の取得
このインターフェースは、オーディオ下り状態の取得に使われています。
####  関数のプロトタイプ  
```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

####  サンプルコード  
```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];
```

### スピーカーのリアルタイムボリュームの取得
このインターフェースはスピーカーのリアルタイムボリュームの取得に使われています。戻り値はint型であり、スピーカーのリアルタイムボリュームを示しています。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerLevel
```

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];
```

### ほかのルームメンバーの下りリアルタイムボリュームの取得
このインターフェースは、ほかのルームメンバーの下りリアルタイムボリュームの取得に使われています。その戻り値はint型であり、数値範囲が1～100です。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetRecvStreamLevel:(NSString*) openID 
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openID    |NSString       |ほかのルームメンバーのopenIdです|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetRecvStreamLevel:(NSString*) openId
```

### スピーカーボリュームの設定
このインターフェースは、スピーカーボリュームの設定に使われています。
パラメータvolumeはスピーカーボリュームの設定に使われ、値が0の場合はミュートを示し、100の場合はボリュームの増減がないことを示しています。そのデフォルト値は100です。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(QAVResult)SetSpeakerVolume:(int)vol
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int        |ボリューム設定で、範囲は0～200です|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];
```

### スピーカーボリュームの取得

このインターフェースは、スピーカーボリュームの取得に使われています。戻り値はint型であり、スピーカーボリュームを示します。戻り値が101の場合は、インターフェースSetSpeakerVolumeを呼び出したことがないことを示しています。
Levelはリアルタイムボリュームで、Volumeはスピーカーボリュームで、最終の音声ボリュームは、Level*Volume%となります。例えば、リアルタイムボリュームが100で、Volumeが60である場合、最終の音声ボリュームも60です。

####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerVolume
```
####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerVolume];
```


### インイヤ・モニタリングの起動
このインターフェースは、インイヤ・モニタリングの起動に使われています。
####  関数のプロトタイプ  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableLoopBack:(BOOL)enable
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| enable    |boolean         |起動するかどうかを設定します|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableLoopBack:YES];
```


## オフライン音声のテキスト変換のフローチャート
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## オフライン音声
初期化される前に、SDKは未初期化段階にあります。リアルタイム音声とオフライン音声を利用するには、インターフェースInitでSDKを初期化する必要があります。
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
|StartRecording|録音します|
|StartRecordingWithStreamingRecognition|ストリーミング録音します|
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
|GetFileSize |音声ファイルのサイズです|
|GetVoiceFileDuration|音声ファイルの長さです|
|SpeechToText |ボイステキスト変換です|

### 認証の初期化
SDKを初期化してから認証の初期化を呼び出します。authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースをご参照ください。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| authBuffer    |NSData*                    |認証|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]ApplyPTTAuthbuffer:(NSData *)authBuffer];
```

### 音声メッセージの長さの制限
音声メッセージの長さを制限します、最大は60秒をサポートします。

####  関数のプロトタイプ

```
ITMGContext GetPTT -(QAVResult)SetMaxMessageLength:(int)msTime
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| msTime    |int                    |音声の長さで、単位はmsです|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]SetMaxMessageLength:(int)msTime];
```


### 録音の開始
このインターフェースは、録音の開始に使われています。ボイステキスト変換などの機能を使用するには、先に録音ファイルをアップロードする必要があります。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(int)StartRecording:(NSString*)fileDir
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileDir    |NSString                     |音声データの保存パスです|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]StartRecording:path];
```

### 録音開始のコールバック
録音開始が完了後のコールバックは関数OnEventを呼び出します、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡されるパラメータはresultとfile_pathの二つの情報を含んでいます。

## エラーコード
|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|4097   |パラメータは空です|コードにおけるインターフェースパラメータが正しいかどうかを確認します|
|4098   |初期化にエラーが発生しました|デバイスが占用されているか、権限が正常であるかどうか、正常に初期化されているかを確認します|
|4099   |録音中です|適切なタイミングでSDKの録音機能を使うことを確保します|
|4100   |オーディオデータを採集していません|マイクが正常であるかどうかを確認します|
|4101   |録音に際し、録音ファイルへのアクセスにエラーが発生しました|ファイルが存在していること、及びファイルパスの正当性を確保します|
|4102   |マイク権限を取得していないため、エラーが発生しました|SDKを使用するには、マイク権限を取得する必要があります。権限の追加については、当該エンジン又はプラットフォームのSDKプロジェクト構成ドキュメントをご参照ください|
|4103   |録音時間が短いため、エラーが発生しました|まず、録音の制限長さの単位がミリ秒であるため、パラメータが正確であるかどうかを確認します。次に、録音の長さは1000ミリ秒以上である必要があります|
|4104   |録音を開始していません|録音の開始インターフェースを呼び出しているかどうかを確認します|

####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE：
        {
	    //録音のコールバック
        }
            break;
    }
}
```

### ストリーミング音声識別の開始
このインターフェースは、ストリーミング音声識別の開始に使われています。コールバックにおいて、ボイスはリアルタイムでテキストに変換されて返されるため、言語を指定し識別することができるし、音声から識別した情報を指定した言語に翻訳してから返すこともできます。

####  関数のプロトタイプ  

```
ITMGContext GetPTT -(void) StartRecordingWithStreamingRecognition(const NSString* filePath)
ITMGContext GetPTT -(void) StartRecordingWithStreamingRecognition(const NSString* filePath,const NSString*speechLanguage,const NSString*translateLanguage)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |NSString* |音声データの保存パスです|
| speechLanguage    |NSString*                     |指定された文字に識別するための言語パラメータです。パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translateLanguage    |NSString*                     |指定された文字に翻訳するための言語パラメータです。パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは現時点使えないため、speechLanguageと同じパラメータを入力してください）|

####  サンプルコード  
```
[[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:recordfilePath  speechLanguage:@"cmn-Hans-CN" translateLanguage:@"cmn-Hans-CN"];
```

### ストリーミング音声識別を開始したのコールバック
ストリーミング音声識別を開始した後のコールバックは関数OnEventを呼び出します。イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。渡されるパラメータは次の4つの情報が含まれています。

|情報名     | 意味         |
| ------------- |:-------------:|
| result    |ストリーミング音声識別が成功しているかどうかを判断するためのリターンコードです|
| text    |ボイステキスト変換で識別したテキストです|
| file_path |録音を保存するローカルパスです|
| file_id |録音のバックグラウンドにおけるurlアドレスです|

|エラーコード     | 意味         |対処方法|
| ------------- |:-------------:|:-------------:|
|32775|ストリーミングボイスツーテキスト変換は失敗しましたが、録音は成功しました|UploadRecordedFileインターフェースを呼び出し録音をアップロードしてから、SpeechToTextインターフェースを呼び出しボイステキスト変換を行います|
|32777|ストリーミングボイスツーテキスト変換は失敗しましたが、録音は成功し、アップロードしました|返された情報にはアップロードしたバックグラウンドurlアドレスが含まれているため、SpeechToTextインターフェースを呼び出してボイステキスト変換を行います|

####  サンプルコード  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE：
        {
	    //ストリーミング音声識別のコールバック
        }
            break;
    }
}
```
### 録音の一時停止
このインターフェースは、録音の一時停止に使われています。録音を再開する場合は、インターフェースResumeRecordingを呼び出してください。

####  関数のプロトタイプ  
```
ITMGContext GetPTT int PauseRecording()
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]PauseRecording;
```

### 録音の再開
このインターフェースは、録音の再開に使われています。

####  関数のプロトタイプ  
```
ITMGContext GetPTT int ResumeRecording()
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]ResumeRecording;
```


### 録音の停止
このインターフェースは、録音の停止に使われています。このインターフェースが非同期インターフェースであるため、録音を停止した後には録音完了のコールバックがあります。コールバックが成功してから、録音ファイルが利用できるようになります。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(QAVResult)StopRecording
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]StopRecording];
```



### 録音のキャンセル
このインターフェースを呼び出し録音をキャンセルします。キャンセルした後にはコールバックがありません。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(QAVResult)CancelRecording
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]CancelRecording];
```

### オフライン音声マイクのリアルタイムボリュームの取得
このインターフェースは、マイクのリアルタイムボリュームの取得に使われています。戻り値はint型であり、数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGContext GetPTT -(QAVResult)GetMicLevel
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]GetMicLevel];
```

### オフライン音声の録音ボリュームの設定
このインターフェースは、オフライン音声の録音ボリュームの設定に使われ、その数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGContext GetPTT int SetMicVolume:(int) vol
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]SetMicVolume:100];
```

### オフライン音声の録音ボリュームの取得
このインターフェースは、オフライン音声の録音ボリュームの取得に使われています。その戻り値はint型であり、数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGContext GetPTT int GetMicVolume()
```

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]GetMicVolume];
```


### スピーカーのリアルタイムボリュームの取得
このインターフェースは、スピーカーのリアルタイムボリュームの取得に使われています。戻り値はint型であり、数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGContext GetPTT -(QAVResult)GetSpeakerLevel
```

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerLevel];
```

### オフライン音声の再生ボリュームの設定
このインターフェースは、オフライン音声の再生ボリュームの設定に使われ、数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGContext GetPTT int SetSpeakerVolume:(int) vol
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]SetSpeakerVolume:100];
```

### オフライン音声の再生ボリュームの取得
このインターフェースは、オフライン音声の再生ボリュームの設定に使われ、数値範囲が0～100です。

####  関数のプロトタイプ  
```
ITMGContext GetPTT int GetSpeakerVolume()
```

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerVolume];
```




### 音声ファイルのアップロード
このインターフェースは、音声ファイルのアップロードに使われています。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(void)UploadRecordedFile:(NSString*)filePath 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |NSString                      |音声データのアップロードパス|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]UploadRecordedFile:path];
```


### 音声をアップロードした後のコールバック
音声をアップロードした後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
## エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|8193   |アップロードに際し、録音ファイルへのアクセスにエラーが発生しました|ファイルが存在していること、及びファイルパスの正当性を確保します|
|8194   |サインの認証に失敗し、エラーが発生しました|認証キーが正しいかどうか、オフライン音声を初期化しているかどうかを確認します|
|8195   |ネット環境のエラーです|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|8196   |アップロードパラメータの取得に際し、ネット環境のエラーが発生しました|認証が正しいかどうか、デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|8197   |アップロードパラメータの取得に際し、リターンパケットのデータは空です|認証が正しいかどうか、デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|8198   |アップロードパラメータの取得に際し、リターンパケットの解析に失敗しました|認証が正しいかどうか、デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|8200   |appinfoを設定していません|applyインターフェースを呼び出しているかどうか、渡されたパラメータが空であるかどうかを確認します|

####  サンプルコード

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE：
        {
	    //音声をアップロードしました
        }
            break;
    }
}
```


### 音声ファイルのダウンロード
このインターフェースは、音声ファイルのダウンロードに使われています。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(void)DownloadRecordedFile:(NSString*)fileId downloadFilePath:(NSString*)downloadFilePath 
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |NSString                      |ファイルのurlパス|
| downloadFilePath |NSString                      |ファイルのローカル保存パス|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]DownloadRecordedFile:fileIdpath downloadFilePath:path];
```


### 音声ファイルをダウンロードした後のコールバック
音声ファイルをダウンロードした後のイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡されるパラメータは、result、file_pathとfile_idの三つの情報を含んでいます。
## エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|12289  |ファイルのダウンロードに際し、ファイルへのアクセスにエラーが発生しました    |ファイルパスの正当性を確認します|
|8194   |サインの認証に失敗しました|認証キーが正しいかどうか、オフライン音声を初期化しているかどうかを確認します|
|12291  |ネットストレージシステムに異常が発生しました    |サーバーによる音声ファイルの取得が失敗しました、インターフェースパラメータ fileid が正しいかどうか、ネット環境が正常であるかどうか、cosファイルが存在しているかどうかを確認ください|
|12292  |サーバーのファイルシステムにエラーが発生しました    |デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうか、サーバーに該当ファイルがあるかどうかを確認します|
|12293  |ダウンロードパラメータの取得に際し、HTTPネットに失敗が発生しました|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|12294   |ダウンロードパラメータの取得に際し、リターンパケットのデータは空です|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|12295   |ダウンロードパラメータの取得に際し、リターンパケットの解析に失敗しました|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|12297   |appinfoを設定していません|認証キーが正しいであるかどうか、オフライン音声を初期化しているかどうかを確認します|


####  サンプルコード

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE：
        {
	    //ダウンロード完了   
        }
            break;
    }
}
```



### 音声の再生
このインターフェースは、音声の再生に使われています。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(void)PlayRecordedFile:(NSString*)downloadFilePath
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| downloadFilePath    |NSString                      |ファイルのパス|

## エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|20485  |再生が開始されていません|ファイルが存在していること、及びファイルパスの正当性を確保します|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]PlayRecordedFile:path];
```


### 音声再生のコールバック
音声再生のコールバックは、イベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡すパラメータはresultとfile_pathの二つの情報を含んでいます。

## エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|20481  |初期化にエラーが発生しました|デバイスが占用されているか、権限が正常であるかどうか、正常に初期化されているかを確認します|
|20482  |再生中で、再生を停止し次の音声を再生しようとしましたが、失敗しました（普通には停止できます）|コードのロジックが正しいかどうかを確認します|
|20483  |パラメータは空です|コードのインターフェースパラメータが正しいかどうかを確認します|
|20484  |内部エラーです|プレイヤー初期化のエラー、デコードエラーなどによるエラーコードが発生するため、ログを参照して問題を特定する必要があります|

####  サンプルコード

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE：
        {
	    //音声再生のコールバック 
        }
            break;
    }
}
```




### 音声再生の停止
このインターフェースは、音声再生の停止に使われています。音声の再生を停止しても、再生完了のコールバックが発生します。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(int)StopPlayFile
```

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]StopPlayFile];
```



### 音声ファイルのサイズの取得
このインターフェースを介して、音声ファイルのサイズを取得します。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(int)GetFileSize:(NSString*)filePath
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |音声ファイルのパスです|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]GetFileSize:path];
```

### 音声ファイルの長さの取得
このインターフェースは、音声ファイルの長さの取得に使われ、その単位はミリ秒です。
####  関数のプロトタイプ  
```
ITMGContext GetPTT -(int)GetVoiceFileDuration:(NSString*)filePath
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |音声ファイルのパスです|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]GetVoiceFileDuration:path];
```


### 指定された音声ファイルを文字に識別します
このインターフェースは、指定された音声ファイルを文字に識別するために使われています。

####  関数のプロトタイプ  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |NSString                     |音声ファイルのurlです|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID];
```



### 指定された音声ファイルを文字に翻訳します（指定言語）
このインターフェースは、言語を指定し識別することができるし、音声から識別された情報を指定された言語に翻訳してから返すこともできます。

####  関数のプロトタイプ  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID (NSString*)speechLanguage (NSString*)translateLanguage
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| fileID    |NSString*                     |音声ファイル のurlです|
| speechLanguage    |NSString*                     |指定された文字に識別するための言語パラメータです。パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。|
| translatelanguage    |NSString*                     |指定された文字に翻訳するための言語パラメータです。パラメータは [ボイステキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは現在使用できないため、speechLanguageと同じパラメータを入力する必要があります）|

####  サンプルコード  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID speechLanguage:"cmn-Hans-CN" translateLanguage:"cmn-Hans-CN"];
```



### 識別のコールバック
指定された音声ファイルを文字に識別するためのコールバックです。そのイベントメッセージはITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETEであり、OnEvent関数においてイベントメッセージを判断します。
渡すパラメータはresult、file_pathとtextの三つの情報が含まれて、そのうち、textは識別されたテキストです。

#### エラーコード

|エラーコードの値 |原因  |推奨ソリューション        |
|-----|------|------|
|32769  |内部エラーです|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。|
|32770   |ネット環境に失敗が発生しました|デバイスのネット環境では外部ネットワークに正常にアクセスできるかどうかを確認します|
|32772  |リターンパケットの解析に失敗しました|ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。|
|32774   |appinfoを設定していません|認証キーが正しいであるかどうか、オフライン音声を初期化しているかどうかを確認します|
|32776  |authbufferの認証に失敗しました|authbufferが正しいかどうかを確認します|
|32784  |ボイスツーテキスト変換のパラメータにエラーが発生しました|コードのインターフェースパラメータfileidが空であるかどうかを確認します|
|32785  |ボイスツーテキスト変換から返された翻訳にエラーが発生しました|オフライン音声バックグラウンドのエラーです。ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。|

####  サンプルコード

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
        {
	    //音声ファイルを正常に識別しました       
        }
            break;   
    }
}
```



## 高度なAPI

### バージョン番号の取得
分析を行うために、SDKのバージョンを取得します。
####  関数のプロトタイプ
```
ITMGContext  -(NSString*)GetSDKVersion
```
####  サンプルコード  
```
[[ITMGContext GetInstance] GetSDKVersion];
```

### ログのプリントレベルの設定
ログのプリントレベルの設定に使われています。デフォルトレベルを維持することをお薦めします。
####  関数のプロトタイプ
```
ITMGContext -(void)SetLogLevel:(ITMG_LOG_LEVEL)levelWrite (ITMG_LOG_LEVEL)levelPrint
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
|TMG_LOG_LEVEL_VERBOSE=4|高頻度ログをプリントします|

####  サンプルコード  
```
[[ITMGContext GetInstance] SetLogLevel:TMG_LOG_LEVEL_INFO TMG_LOG_LEVEL_INFO];
```



### プリントするログのパスの設定
ログをプリントするパスの設定に使われています。デフォルトパスは/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documentsです。
####  関数のプロトタイプ
```
ITMGContext -(void)SetLogPath:(NSString*)logDir
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| logDir    |NSString   |パス|

####  サンプルコード  
```
[[ITMGContext GetInstance] SetLogPath:Path];
```


### 診断情報の取得
オーディオ・ビデオ通信のリアルタイム通信品質の関係情報を取得します。このインターフェースは、主にリアルタイムの通信品質の確認、トラブルシューティングに使用されます。セールス側としては、これを無視しても構いません。
####  関数のプロトタイプ  
```
ITMGContext GetRoom -(NSString*)GetQualityTips
```
####  サンプルコード  
```
[[[ITMGContext GetInstance]GetRoom ] GetQualityTips];
```

### オーディオデータブラックリストへの追加
特定のIDをオーディオデータブラックリストに追加します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext GetAudioCtrl -(QAVResult)AddAudioBlackList:(NSString*)openID
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |NSString      |ブラックリストに追加するIDです|

####  サンプルコード  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] AddAudioBlackList[id]];
```

### オーディオデータブラックリストから削除
特定のIDをオーディオデータブラックリストから削除します。戻り値が0の場合は、呼び出しに成功したことを示します。
####  関数のプロトタイプ  

```
ITMGContext GetAudioCtrl -(QAVResult)RemoveAudioBlackList:(NSString*)openID
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| openId    |NSString      |ブラックリストから削除するIDです|

####  サンプルコード  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] RemoveAudioBlackList[openId]];
```


## コールバックメッセージ

### メッセージリスト：

|メッセージ    | メッセージの意味   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |オーディオルームに入室します|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |オーディオルームから退室します|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |ネット環境などの原因により、ルームの接続が切れました|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|ルームタイプ変更イベント|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH|伴奏が終了しました|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE|ルームメンバーが更新されました|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE|PTTの録音が完成しました|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE|PTTをアップロードしました|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|PTTをダウンロードしました|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE|PTTの再生が完了しました|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|ボイステキスト変換が完成しました|

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
