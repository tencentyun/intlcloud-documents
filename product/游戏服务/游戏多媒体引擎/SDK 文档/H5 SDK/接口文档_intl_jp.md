## 概要

Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。H5開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここではH5開発のための導入技術文書を紹介します。

### GME H5 API使用目次

| API           | 意味            |
|--------------|-------------------|
| Init           | APIの初期化         |
| SetTMGDelegate | デリゲートの設定           |
| EnterRoom      | ボイスルーム参加       |
| EnableMic      | 収集デバイスのオン/オフ |
| EnableSpeaker  | 再生デバイスのオン/オフ |
| SetMicVolume   | マイク音量の設定      |
| ExitRoom       | ボイスルーム退出        |


**説明**

**GMEのAPIが正常に呼び出された後、戻り値はQAVError.OKで、値は0です。**

**GMEによるルームへの参加は認証が必要です。ドキュメントの認証関連部分を参照してください。**

**デバイスの操作はルームに参加した後に行われます。**


## 関連APIの初期化
初期化する前には、SDKは初期化されていない状態で、初期化が認証された上、SDKを初期化してから、ルームに参加可能となります。

## SDKの初期化
パラメータの取得については、[ゲームマルチメディアエンジン（GME）導入ガイド](/GME%20Introduction.md)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはApp開発者によって定められ、App内で繰り返さないようにします（現在INT64のみ対応）。
SDKを初期化してから、ルームに参加できます。
#### 関数プロトタイプ

```
WebGMEAPI.fn.Init = function (document, sdkAppId, openId) {...}
```

|パラメータ    |意味|
| ------------- |-------------|
| document    	  |		HTML DOM Documentオブジェクト	|
| sdkAppId    		  |Tencent CloudコンソールからのSdkAppId番号	|
| openId    		  |開発者によって定義されたユーザー識別用ユーザーアカウント。10000より大きくする必要があります|

#### サンプルコード 
```
const cSdkAppId = () => document.getElementById("input-sdkappid").value;
const cOpenID = () => document.getElementById("input-openid").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### コールバックの設定
APIクラスは、Delegateメソッドを使用してコールバック通知をアプリケーションに送信します。コールバック関数をSDKに登録して、コールバック情報を受け取ります。
ルームに参加する前に、コールバック関数をSDKに登録する必要があります。

#### 関数プロトタイプ
```
WebGMEAPI.fn.SetTMGDelegate = function (delegate){...}
```
|パラメータ             |意味|
| ------------- |-------------|
| onEvent     |SDKコールバックイベント|

#### サンプルコード  
```
gmeAPI.SetTMGDelegate(onEvent);
```





## リアルタイムボイス関連API
初期化後、SDKでルーム参加を呼び出しルームに参加してから、リアルタイムに音声電話をかけるようになります。
認証の取得については、[準備作業ドキュメント](./H5%20SDK%20Project%20Configuration.md)を参照してください。

### ルーム参加
生成した認証情報を用いてルームに参加するとき、コールバックとしてメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMが受信されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。
認証については、プロジェクト構成を参照してください。

#### 関数プロトタイプ
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
|パラメータ    |意味|
| ------------- |-------------|
| roomId 	|ルーム番号、127文字まで入力可能|
| roomType 	|ルームオーディオタイプ|
| authBuffer	|認証コード|



|オーディオタイプ|意味|推奨コンソールサンプリングレートの設定|適用シナリオ|
|-------|---|----|----------------|------|
| ITMG_ROOM_TYPE_FLUENCY			|スムーズな音質	|1|音質に特に要望がない場合は、16Kのサンプリングレートで十分。					|スムーズさを優先に、超低遅延リアルタイムボイスで、FPS、MOBA等のようなゲーム内のボイスシナリオに適用されます。	|					
| ITMG_ROOM_TYPE_STANDARD			|標準音質	|2|音質に対する要望に基づき、16k/48kのサンプリングレートを選択可能。				|時間遅延が適当な良好音質で、人狼殺、ボードゲーム等、カジュアルゲームのリアルタイム通話シナリオに適用されます。	|						
| ITMG_ROOM_TYPE_HIGHQUALITY		|高音質	|3|最良の効果を保証するため、コンソールで48kサンプリングレートの高音質構成に設定するのをお勧めます。	|時間遅延が大きな超高音質で、音楽やダンスのゲームおよびボイスソーシャルAPPに適用されます。音楽再生、オンラインカラオケ等、高音質シナリオに適用されます。	|

- 音量タイプや利用シナリオに特別な要望があれば、カスタマサービスまでご連絡してください。
- コンソールのサンプリングレート設定はゲームのボイス効果に直接影響を与えますので、[コンソール](https://console.cloud.tencent.com/gamegme)にてサンプリングレートの設定がプロジェクトの利用シナリオに一致しているかを再確認してください。


#### サンプルコード  
```
 function bindButtonEvents() {
        $("#start_btn").click(function () {
            console.log('start!');
            //ステップ1：AuthBufferを取得します
            var FetchSigCgi = 'http://134.175.146.244:10005/';
            $.ajax({
                type: "POST",
                url: FetchSigCgi,
                dataType: 'json',
                data: {
                    sdkappid: cSdkAppId(),
                    roomid: cRoomNum(),
                    openid: cOpenID(),
                },
                success: function (json) {
                    //ステップ2：AuthBufferを取得しました
                    if (json && json.errorCode === 0) {
                        let userSig = json.userSig;
                        gmeAPI.Init(document, cSdkAppId(), cOpenID());
                        gmeAPI.SetTMGDelegate(onEvent);
                        gmeAPI.EnterRoom(cRoomNum(), 1, userSig);
                    } else {
                        console.error(json);
                    }
                },
                error: function (err) {
                    console.error(err);
                }
            });
        });
```

### イベントコールバック
ルームに参加した後、ITMG_MAIN_EVENT_TYPE_ENTER_ROOMというメッセージが送信され、OnEvent関数で判断します。

#### サンプルコード  
```
 onEvent = function (eventType, result) {
         if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
        {
            //ルーム参加に成功
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVNET_TYPE_USER_UPDATE)
        {
            app._data.downStreamInfoList = result.PeerInfo;//受信したピア情報。下表を参照
            app._data.brSend = result.UploadBRSend;//アップロードビットレート
            app._data.rtt = result.UploadRTT;//アップロードRTT
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM)
        {
            //ルーム退出に成功
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT)
        {
            //ルーム接続切断
        }
    };
```


受信したピア情報は次の通りです。downStreamInfoList： 

|パラメータ      |意味|
| ------------- |------------|
| brRecv      |受信したビットレート|
| delay      |受信した遅延|
| jitterBufferMs      |ジッタ遅延|
| jitterReceived      |jitter受信|


### ルーム退出
このAPIの呼び出しによって現在のルームから退出できます。非同期APIとして、ルーム退出後にコールバックが実行され、戻り値はAV_OKの場合、非同期配信が完了したことを意味します。
#### 関数プロトタイプ  
```
WebGMEAPI.fn.ExitRoom = function (){...}
```
#### サンプルコード  
```
gmeAPI.ExitRoom();
```

### マイクのオン/オフ
このAPIはマイクのオン/オフに使用されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。

#### 関数プロトタイプ  
```
WebGMEAPI.fn.EnableMic = function (bEnable) {...}
```
|パラメータ      |意味|
| ------------- |------------|
| isEnabled      |マイクをオンにする必要があれば、渡されたパラメータはtrueです。マイクをオフにすれば、パラメータはfalseです|

#### サンプルコード  
```
gmeAPI.EnableMic(false);
```



### マイク音量の設定
このAPIはマイク音量の設定に使用されます。パラメータvolumeはマイク音量の設定に使用され、数値が0の場合はミュート状態を示し、100の場合は音量が変更されないことを示します。デフォルト数値は100です。

#### 関数プロトタイプ  
```
WebGMEAPI.fn.SetMicVolume = function (volume){...}
```
|パラメータ    |意味|
| -------------|-------------|
| volume    |0～100の範囲で音量を設定|

#### サンプルコード  
```
gmeAPI.SetMicVolume(100);
```


### スピーカーのオン/オフ
このAPIはスピーカーのオン/オフに使用されます。
#### 関数プロトタイプ  
```
WebGMEAPI.fn.EnableSpeaker = function (bEnable){...}
```
|パラメータ             |意味|
| ------------- |------------|
| isEnabled           |スピーカーをオフにする必要があれば、渡されたパラメータはfalseです。スピーカーをオンにすれば、パラメータはtrueです|

#### サンプルコード  
```
gmeAPI.EnableSpeaker(true);
```

