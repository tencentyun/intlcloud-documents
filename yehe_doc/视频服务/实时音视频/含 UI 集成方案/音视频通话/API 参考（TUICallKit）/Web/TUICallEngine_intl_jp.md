## TUICallEngine APIの概要

TUICallEngine APIはオーディオビデオ通話コンポーネントの**UIインターフェースがない**ものです。

## APIの概要

| API                                                          | 説明                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [createInstance](#createinstance) | TUICallEngineインスタンスの作成（シングルトンモード） |
| [destroyInstance](#destroyinstance) | TUICallEngineインスタンスの破棄（シングルトンモード） |
| [on](#on)    | イベントの監視                            |
| [off](#off)  | イベント監視のキャンセル                        |
| [login](#login) | ログインインターフェース                            |
| [logout](#logout) | ログアウトインターフェース                            |
| [setSelfInfo](#setselfInfo) | ユーザーニックネームおよびプロフィール画像の設定                  |
| [call](#call) | C2C通話への招待                         |
| [groupCall](#groupcall) | グループチャット通話への招待                        |
| [accept](#accept) | 通話応答                            |
| [reject](#reject) | 通話拒否                            |
| [hangup](#hangup) | 通話終了                            |
| [switchCallMediaType](#switchcallmediatype) | 現在の通話タイプの切り替え                    |
| [startRemoteView](#startremoteview) | リモート画面レンダリングの起動                    |
| [stopRemoteView](#stopremoteview) | リモート画面レンダリングの停止                    |
| [startLocalView](#startlocalview) | ローカル画面レンダリングの起動                    |
| [stopLocalView](#stoplocalview) | ローカル画面レンダリングの停止                    |
| [openCamera](#opencamera) | カメラの起動                          |
| [closeCamara](#closecamara) | カメラの終了                          |
| [openMicrophone](#openmicrophone) | マイクをオンにする                          |
| [closeMicrophone](#closemicrophone) | マイクをオフにする                          |
| [setVideoQuality](#setvideoquality) | ビデオ画質の設定                        |
| [getDeviceList](#getdevicelist) | デバイスリストの取得                        |
| [switchDevice](#switchdevice) | カメラまたはマイクデバイスの切り替え              |

## APIの詳細

### createInstance

TUICallEngineのシングルトンを作成します。



```swift
const tuiCallEngine = TUICallEngine.createInstance({
    SDKAppID: 0, // アクセス時に、0をIMアプリケーションのSDKAppIDに置き換える必要があります
    tim: tim         // timパラメータはサービス内にすでに存在するTIMインスタンスに使用され、TIMインスタンスの一意性を保証します
});
```

**パラメータは下表に示すとおりです**

| パラメータ     | タイプ   | 意味                  |
| -------- | ------ | --------------------- |
| SDKAppID | Number | IMアプリケーションのSDKAppID |
| tim      | Any    | TIMインスタンス（オプション）      |

### destroyInstance

TUICallEngineのシングルトンを破棄します。



```swift
tuiCallEngine.destroyInstance().then(() => {
    //success
}).catch(error => {
    console.warn('destroyInstance error:', error);
});
```

### on

イベントを監視します。



```swift
let onError = function(error) {
    console.log(error);
};
tuiCallEngine.on(TUICallEvent.ERROR, onError, this);
```

**パラメータは下表に示すとおりです**

| パラメータ      | タイプ     | 意味                         |
| --------- | -------- | ---------------------------- |
| eventName | String   | イベント名                       |
| callback  | function | イベント応答コールバック                 |
| context   | Any      | callback実行希望時のコンテキスト |

### off

イベントの監視をキャンセルします。



```swift
let onError = function(error) {
    console.log(error);
};
tuiCallEngine.off(TUICallEvent.ERROR, onError, this);
```

**パラメータは下表に示すとおりです**

| パラメータ      | タイプ     | 意味                         |
| --------- | -------- | ---------------------------- |
| eventName | String   | イベント名                       |
| callback  | function | イベント応答コールバック                 |
| context   | Any      | callback実行希望時のコンテキスト |

### login

インターフェースにログインします。



```swift
let promise = tuiCallEngine.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('login error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ    | タイプ   | 意味                                                         |
| ------- | ------ | ------------------------------------------------------------ |
| userID  | String | 現在のユーザーID。文字列タイプでは、アルファベット（a-z および A-Z）、数字（0-9）、ハイフン（-）、アンダーバー（_）のみ使用できます |
| userSig | String | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 [UserSigの計算方法](https://www.tencentcloud.com/document/product/647/35166)をご参照ください。 |

### logout

インターフェースからログアウトします。



```swift
let promise = tuiCallEngine.logout();
promise.then(() => {
    //success
}).catch(error => {
    console.warn('logout error:', error);
});
```

### setSelfInfo

ユーザーニックネームおよびプロフィール画像を設定します。



```swift
let promise = tuiCallEngine.setSelfInfo({
    nickName: 'video', 
    avatar:'http(s)://url/to/image.jpg'
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('setSelfInfo error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ     | タイプ   | 意味     |
| -------- | ------ | -------- |
| nickName | String | ニックネーム     |
| avatar   | String | プロフィール画像のアドレス |

### call

C2Cの通話に招待します。被招待者はTUICallEvent.INVITEDイベントを受信します。

>! オフラインプッシュは端末（AndroidまたはiOS)にのみ適用され、Webではサポートされません。



```javascript
let promise = tuiCallEngine.call({
    userID: 'user1', 
    type: 1, 
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('call error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ   | タイプ   | 意味                            |
| ------ | ------ | ------------------------------- |
| userID          | String | 被招待者のuserID  |
| type   | Number | 0-不明、1-音声通話、2-ビデオ通話 |

### groupCall

IMグループの通話に招待します。被招待者は`EVENT.INVITED`イベントを受信します。

>! オフラインプッシュは端末（AndroidまたはiOS)にのみ適用され、Webではサポートされません。



```javascript
let promise = tuiCallEngine.groupCall({
    userIDList: ['user1', 'user2'], 
    type: 1, 
    groupID: 'IMグループID', 
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('groupCall error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ                                                         | タイプ   | 意味                                                    |
| ------------------------------------------------------------ | ------ | ------------------------------------------------------- |
| userIDList                                                   | Array  | 招待リスト                                                |
| type                                                         | Number | 0-不明、1-音声通話、2-ビデオ通話                         |
| groupID                                                      | String | IMグループ                                                 |
| timeout                                                      | String | タイムアウト時間(オプション)                                          |
| roomID                                                       | String | ルームID(オプション)                                           |
| [offlinePushInfo](#offlinePushInfo) | Object | メッセージのオフラインプッシュをカスタマイズします（オプションです。tsignalingバージョンは>= 0.8.0が必要です） |

#### offlinePushInfo

| パラメータ                 | タイプ   | 意味                                                   |
| -------------------- | ------ | ------------------------------------------------------- |
| title                | string | オフラインプッシュタイトル（オプション）                                    |
| description          | string | オフラインプッシュコンテンツ（オプション）                                    |
| androidOPPOChannelID | string | オフラインプッシュのためのOPPO携帯（システム8.0以上）のチャンネルIDを設定します（オプション） |
| extension            | string | オフラインプッシュパススルーコンテンツ（オプション）（tsignalingバージョン >= 0.9.0）    |

### accept

被招待者として`TUICallEvent.INVITED` イベントのコールバックを受信した場合は、このインターフェースを呼び出して通話に応答することができます。



```javascript
tuiCallEngine.on(TUICallEvent.INVITED, () => {
    tuiCallEngine.accept().promise.then(() => {
        //success
    }).catch(error => {
        console.warn('accept error:', error);
    });
});
```

### reject

現在の通話を拒否します。着呼側として`TUICallEvent.INVITED `のコールバックを受信した場合は、この関数を呼び出して通話を拒否することができます。



```javascript
tuiCallEngine.on(TUICallEvent.INVITED, () => {
    tuiCallEngine.reject().then(() => {
        //success
    }).catch(error => {
        console.warn('reject error:', error);
    });
});
```

### hangup

現在の通話を終了します。通話中である場合は、この関数を呼び出して通話を終了できます。

通話中にこのインターフェースを呼び出せば、通話を終了することができます

ダイヤルしていない状態では、通話をキャンセルするために用いることができます



```javascript
tuiCallEngine.hangup().then(() => {
     //success
 }).catch(error => {
        console.warn('hangup error:', error);
 });
```

### switchCallMediaType

現在の通話タイプを切り替えます。

1v1通話中のみ使用をサポートします

ERRORイベントの監視に失敗しました。code：60001



```javascript
// 1は音声通話、2はビデオ通話を意味します
tuiCallEngine.switchCallMediaType(2).then(() => {
  //success
}).catch(error => {
  console.warn('switchCallMediaType error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ         | タイプ   | 意味                   |
| ------------ | ------ | ---------------------- |
| newMediaType | Number | 1-音声通話、2-ビデオ通話 |

### startRemoteView

リモート画面のレンダリングを起動します。



```javascript
let promise = tuiCallEngine.startRemoteView({
    userID: 'user1', 
    videoViewDomID: 'video_1',
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('startRemoteView error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ           | タイプ   | 意味                               |
| -------------- | ------ | ---------------------------------- |
| userID         | String | ユーザーID                            |
| videoViewDomID | String | このユーザーデータはこのdom idノードにレンダリングされます |

### stopRemoteView

リモート画面のレンダリングを停止します



```javascript
tuiCallEngine.stopRemoteView({userID: 'user1'});
```

**パラメータは下表に示すとおりです**

| パラメータ   | タイプ   | 意味   |
| ------ | ------ | ------ |
| userID | String | ユーザーid |

### startLocalView

ローカル画面のレンダリングを起動します



```javascript
let promise = tuiCallEngine.startLocalView({
    userID: 'user1', 
    videoViewDomID: 'video_1'
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('startLocalView error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ           | タイプ   | 意味                               |
| -------------- | ------ | ---------------------------------- |
| userID         | String | ユーザーID                            |
| videoViewDomID | String | このユーザーデータはこのdom idノードにレンダリングされます |

### stopLocalView

ローカル画面のレンダリングを停止します



```javascript
let promise = tuiCallEngine.stopLocalView({userID: 'user1'});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('stopLocalView error:', error)
});
```

**パラメータは下表に示すとおりです**

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID         | String | ユーザーID    |

### openCamera

カメラをオンにする



```javascript
tuiCallEngine.openCamera().then(() => {
    //success
}).catch(error => {
    console.warn('openCamera error:', error);
});
```

### closeCamara

カメラをオフにします。



```javascript
tuiCallEngine.closeCamera().then(() => {
    //success
}).catch(error => {
    console.warn('closeCamara error:', error);
});
```

### openMicrophone

マイクをオンにします



```javascript
tuiCallEngine.openMicrophone().then(() => {
    //success
}).catch(error => {
    console.warn('openMicrophone error:', error);
});
```

### closeMicrophone

マイクをオフにします。



```javascript
tuiCallEngine.closeMicrophone().then(() => {
    //success
}).catch(error => {
    console.warn('closeMicrophone error:', error);
});
```

### setVideoQuality

ビデオの画質を設定します。



```javascript
const profile = '720p';
tuiCallEngine.setVideoQuality(profile).then(() => {
    //success
}).catch(error => {
    console.warn('setVideoQuality error:', error)
});    // ビデオ画質を720pに設定します     
```

**パラメータは下表に示すとおりです**

| ビデオProfile | 解像度（幅 x 高さ） |
| ------------ | ----------------- |
| 480p         | 640 × 480         |
| 720p         | 1280 × 720        |
| 1080p        | 1920 × 1080       |

### getDeviceList

デバイスリストを取得します。



```javascript
tuiCallEngine.getDeviceList("camera").then((devices) => {
    console.log(devices);
}).catch(error => {
    console.warn('getDeviceList error:', error);
});
```

**パラメータは下表に示すとおりです**

| パラメータ       | タイプ   | 意味                                  |
| ---------- | ------ | ------------------------------------- |
| deviceType | String | 'camera'-カメラ、'microphones'-マイク |

### switchDevice

カメラまたはマイクデバイスを切り替えます。



```javascript
let promsie = tuiCallEngine.switchDevice({
    deviceType: 'video', 
    deviceId: cameras[0].deviceId
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('switchDevice error:', error)
});
```

**パラメータは下表に示すとおりです**

| パラメータ       | タイプ   | 意味                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| deviceType | String | 切り替えたいデバイスタイプ　'video'カメラ'audio'マイク               |
| deviceId   | String | 切り替えたいデバイスID　カメラデバイスIDはgetCameras()で取得します<li/>マイクデバイスIDはgetMicrophones()で取得します |

 
