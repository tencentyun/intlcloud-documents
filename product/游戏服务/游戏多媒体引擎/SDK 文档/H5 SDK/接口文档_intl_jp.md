H5開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでH5開発のための導入技術文書を紹介します。


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
- GMEのAPIが正常に呼び出された後、戻り値はQAVError.OKで、値は0です。
- GMEによるルームへの参加は認証が必要です。ドキュメントの認証関連部分を参照してください。
- デバイスの操作はルームに参加した後に行われます。


## 関連APIの初期化
初期化する前には、SDKは初期化されていない状態で、初期化が認証された上、SDKを初期化してから、ルームに参加可能となります。

### SDKの初期化
パラメータの取得については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
このAPIには、パラメータとしてTencent CloudコンソールからのSdkAppId番号と、ユーザー固有の識別子であるopenIdが必要です。ルールはアプリ開発者によって定められ、アプリ内で繰り返さないようにします（現在INT64のみ対応）。

> SDKを初期化してから、ルームに参加できます。

### 関数プロトタイプ

```
WebGMEAPI.fn.Init = function (document, SdkAppId, openId) {...}
```

|パラメータ    |意味|
| ------------- |-------------|
| document    	  |		HTML DOM Documentオブジェクト	|
| SdkAppId    		  |Tencent CloudコンソールからのSdkAppId番号	|
| openId    		  |開発者によって定義されたユーザー識別用ユーザーアカウント。10000より大きくする必要があります|

### サンプルコード 
```
const cSdkAppId = () => document.getElementById("input-SdkAppId").value;
const cOpenID = () => document.getElementById("input-OpenID").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### コールバックの設定
APIクラスは、Delegateメソッドを使用してコールバック通知をアプリケーションに送信します。コールバック関数をSDKに登録して、コールバック情報を受け取ります。ルームに参加する前に、コールバック関数をSDKに登録する必要があります。


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


### ルーム参加
生成した認証情報を用いてルームに参加するとき、コールバックとしてメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMが受信されます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。


#### 関数プロトタイプ
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
|パラメータ    |意味|
| ------------- |-------------|
| roomId 	|ルームID、127文字まで入力可能|
| roomType 	|ルームオーディオタイプ|
| authBuffer	|認証コード。取得方法は[プロジェクトの構成](https://cloud.tencent.com/document/product/607/32156)を参照してください。|



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

