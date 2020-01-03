H5を使う開発者がTencent CloudのGaming Multimedia Engine製品のAPIを容易にデバッグおよびアクセスできるように、ここで、H5での開発に向けるアクセス技術ドキュメントについて説明させていただきます。


| インターフェース           | インターフェースの意味            |
|--------------|-------------------|
| Init           | インターフェースを初期化します |
| SetTMGDelegate | デリゲートを設定します           |
| EnterRoom      | 音声ルームに参加します     |
| EnableMic      | 採集デバイスをオン/オフします |
| EnableSpeaker  | 再生デバイスをオン/オフします |
|SetMicVolume    |マイクの音量を設定します|
| ExitRoom       | 音声ルームから退出します        |


>
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKであり、値は0です。
- GMEで入室するには、認証が必要です。このドキュメントにある認証に関する内容をご参照ください。
- デバイスを操作するには、先に入室に成功する必要があります。


## 関連インターフェースの初期化
初期化される前は、SDKは未初期化の状態です。入室するには、認証を初期化してから、SDKを初期化する必要があります。

### SDKの初期化
パラメータの取得について、[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
このインターフェースは、Tencent CloudコンソールからのSDKAppID番号をパラメータとして、さらにopenIdを付け加える必要があります。このopenIdはユーザーを識別するための一意のもので、ルールはApp開発者によって設定され、Appでは重複されてはなりません（現在はINT64のみをサポートします）。

>入室するには、先にSDKを初期化する必要があります。

####  関数のプロトタイプ

```
WebGMEAPI.fn.Init = function (document, SdkAppId, openId) {...}
```

|パラメータ              |意味|
| ------------- |-------------|
| document      |HTML DOM Document オブジェクトです|
| SdkAppId      |Tencent CloudコンソールからのSdkAppId番号です|
| openId      |ユーザーを識別するために開発者によって定義されたユーザーのアカウントです。10000よりも大きい必要があります|

####  サンプルコード 
```
const cSdkAppId = () => document.getElementById("input-SdkAppId").value;
const cOpenID = () => document.getElementById("input-OpenID").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### コールバックの設定
インターフェースクラスは、Delegateメソッドを使用して、アプリケーションにコールバック通知を送信します。コールバック関数をSDKに登録して、コールバック情報を受信します。 コールバック関数をSDKに登録するには、入室する前に設定する必要があります。


####  関数のプロトタイプ
```
WebGMEAPI.fn.SetTMGDelegate = function (delegate){...}
```
|パラメータ              |意味|
| ------------- |-------------|
| onEvent     |SDK コールバックイベント|

####  サンプルコード  
```
gmeAPI.SetTMGDelegate(onEvent);
```





## リアルタイム音声の関連インターフェース
リアルタイム音声通話を行うには、初期化してから、SDKの入室インタフェースを呼び出し、入室する必要があります。


### 入室
生成された認証情報を使って入室した場合、メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMのコールバックを受信します。入室した際、マイクとスピーカーはデフォルトでオフになっています。


####  関数のプロトタイプ
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
|パラメータ              |意味|
| ------------- |-------------|
| roomId |ルーム番号、最大127文字まで|
| roomType |ルームのオーディオタイプ|
| authBuffer|認証コードです。取得方法について、[プロジェクト構成](https://intl.cloud.tencent.com/document/product/607/10783)をご参照ください。|



####  サンプルコード  
```
 function bindButtonEvents() {
        $("#start_btn").click(function () {
            console.log('start!');
            //ステップ1、  AuthBufferを取得します
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
                    //ステップ2、  AuthBufferは正常に取得します
                    if (json && json.errorCode === 0) {
                        let userSig = json.userSig;
                        gmeAPI.Init(document, cSdkAppId(), cOpenID());
                        gmeAPI.SetTMGDelegate(onEvent);
                        gmeAPI.EnterRoom(cRoomNum(), 1, userSig);
                    }else{
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
入室してから、メッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMを送信し、OnEvent関数で判断します。

####  サンプルコード  
```
 onEvent = function (eventType, result) {
         if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
        {
            //正常に入室した  
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVNET_TYPE_USER_UPDATE)
        {
            app._data.downStreamInfoList = result.PeerInfo;//受信する対向側の情報について、下表をご参照ください。
            app._data.brSend = result.UploadBRSend;//音声データアップロードのビットレートです
            app._data.rtt = result.UploadRTT;//RTTをアップロードします
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM)
        {
            //正常に退室した
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT)
        {
            //ルームへの接続が切断された
        }
    };
```


受信する対向側の情報は以下の通りです。downStreamInfoList: 

|パラメータ      |意味|
| ------------- |------------|
| brRecv      |受信のビットレート|
| delay      |受信のディレー|
| jitterBufferMs      |ジッタディレー|
| jitterReceived      |受信したジッタ|


### 退室する
このインターフェースを呼び出すことで、ルームから退出できます。このインターフェースは非同期であり、退室すると、コールバックすることになります。戻り値がAV_OKの場合は、非同期送信が成功したことです。
####  関数のプロトタイプ  
```
WebGMEAPI.fn.ExitRoom = function (){...}
```
####  サンプルコード  
```
gmeAPI.ExitRoom();
```

### マイクのオン/オフ
このインターフェースは、マイクのオン/オフに使用されます。入室した際、マイクとスピーカーはデフォルトでオフになっています。

####  関数のプロトタイプ  
```
WebGMEAPI.fn.EnableMic = function (bEnable) {...}
```
|パラメータ      |意味|
| ------------- |------------|
| isEnabled　　|マイクをオンにする場合、渡されるパラメータはtrueであり、マイクをオフにする場合、パラメータはfalseです|

####  サンプルコード  
```
gmeAPI.EnableMic(false);
```



### マイク音量の設定
このインターフェースは、マイク音量の設定に使用されます。パラメータvolumeはマイク音量の設定に使用され、値が0の場合はミュートを示し、100の場合は音量が増減しないことを示します、デフォルト値は100です。

####  関数のプロトタイプ  
```
WebGMEAPI.fn.SetMicVolume = function (volume){...}
```
|パラメータ      |意味|
| -------------|-------------|
| volume    |音量の設定で、値範囲は0～100です|

####  サンプルコード  
```
gmeAPI.SetMicVolume(100);
```


### スピーカーのオン/オフ
このインターフェースは、スピーカーのオン/オフに使用されます。
####  関数のプロトタイプ  
```
WebGMEAPI.fn.EnableSpeaker = function (bEnable){...}
```
|パラメータ              |意味|
| ------------- |------------|
| isEnabled　　　　　|スピーカーをオフにする場合、渡されるパラメータはfalseであり、スピーカーをオンにする場合、パラメータはtrueです|

####  サンプルコード  
```
gmeAPI.EnableSpeaker(true);
```
