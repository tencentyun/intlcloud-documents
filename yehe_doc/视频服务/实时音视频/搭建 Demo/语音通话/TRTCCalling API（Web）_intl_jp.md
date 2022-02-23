## TRTCCallingの概要

[TRTCCalling](https://www.npmjs.com/package/trtc-calling-js)コンポーネントは、Tencent CloudのTencent Real-Time Communication（TRTC）とInstant Messaging（IM）サービスの組み合わせにより構成されており、1対1および複数人でのビデオ/音声通話をサポートしています。具体的な実装プロセスについては、[リアルタイム音声通話（Web）](https://intl.cloud.tencent.com/document/product/647/38928)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。

## 環境要件
最新バージョンのChromeブラウザをご使用ください。現在、デスクトップのChromeブラウザはTRTC Web SDKをサポートしており、関連機能は比較的整っていますので、Chromeブラウザを使用して体験することをお勧めします。具体的な内容については [環境要件](https://intl.cloud.tencent.com/document/product/647/38928#.E7.8E.AF.E5.A2.83.E8.A6.81.E6.B1.82)をご参照ください。

## TRTCCalling API 

#### イベントサブスクリプション/サブスクリプションのキャンセルに関するインターフェース関数 

このコンポーネントはイベントのディスパッチに基づいて管理します。アプリケーション層は、コンポーネントからディスパッチされるイベントにインタラクティブに応じて変更することができます。

| API    | 説明         |
| ------------ | ------------ |
| [on(eventName, callback, context)](#on)   | イベントのサブスクリプション     |
| [off(eventName, callback, context)](#off) | イベントサブスクリプションの取消 |


#### SDK 基本関数

| API      | 説明 |
| ---------------------------------- | ----------------- |
| [login({userID, userSig})](#login) | IMログインインターフェース。すべての機能を使用するためには、まずログインする必要があります |
| [logout()](#logout) | インターフェースからログアウトします。ログアウトした後は、ダイヤル操作ができなくなります    |

#### 通話操作に関連するインターフェース関数

| API  | 説明         |
| ------------------------------- | ------------ |
| [call({userID, type, offlinePushInfo}))](#call)     | シングル通話の招待 |
| [groupCall({userIDList, type, groupID, offlinePushInfo})](#groupCall) | グループチャット通話の招待 |
| [accept()](#accept)          | 通話招待に応答 |
| [reject()](#reject)          | 通話招待を拒否 |
| [hangup()](#hangup)          | 現在の通話の終了 |


#### ビデオ制御に関連するインターフェース関数

| API  | 説明    |
| ------------------------------- | ---------------------- |
| [startRemoteView({userID, videoViewDomID})](#startRemoteView) | リモート画面レンダリングの起動       |
| [stopRemoteView({userID})](#stopRemoteView) | リモート画面レンダリングの停止       |
| [startLocalView({userID, videoViewDomID})](#startLocalView) | ローカル画面レンダリングの起動       |
| [stopLocalView({userID})](#stopLocalView) | ローカル画面レンダリングの停止       |
| [openCamera()](#openCamera)  | カメラの起動    |
| [closeCamera()](#closeCamera)     | カメラの停止    |
| [setMicMute(isMute)](#setMicMute)     | デバイスマイクのミュートの有無     |
| [setVideoQuality(profile)](#setVideoQuality) | ビデオ画質の設定  |
| [switchToAudioCall()](#switchToAudioCall) | ビデオ通話を音声通話へ切り替え   |
| [switchToVideoCall()](#switchToVideoCall) | 音声通話をビデオ通話へ切り替え   |
| [getCameras()](#getCameras)  | カメラデバイスリストの取得   |
| [getMicrophones()](#getMicrophones)     | マイクデバイスリストの取得   |
| [switchDevice({deviceType, deviceId}) ](#switchDevice) | カメラまたはマイクデバイスの切り替え |


## TRTCCallingの詳細

### TRTCCallingコンポーネントのインスタンスの作成

まず、[Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc/app)でアプリケーションを作成し、SDKAppIDを取得する必要があります。
その後、`new TRTCCalling()`メソッドを使ってTRTCCalling コンポーネントのインスタンスを取得することができます。

<dx-codeblock>
::: javascript javascript
  npm i trtc-js-sdk --save
  npm i tim-js-sdk --save
  npm i tsignaling --save
  npm i trtc-calling-js --save
  // nodeを通じてダウンロードする依存関係の場合は、importによって次をインポートします
  import TRTCCalling from 'trtc-calling-js';

  // スクリプト方式によってtrtc-calling-jsを使用する場合は、順序どおりに
  // trtc.jsを手動でインポートします
  <script src="./trtc.js"></script>
  // 続いて、tim-js.jsを手動でインポートします。
  <script src="./tim-js.js"></script>
  // 次に、tsignaling.jsを手動でインポートします。
  <script src="./tsignaling.js"></script>
  // 最後に、trtc-calling-js.jsを手動でインポートします。
  <script src="./trtc-calling-js.js"></script>

let options = {
  SDKAppID: 0, // アクセスするときは、0をお客様のIMアプリケーションのSDKAppIDに置き換える必要があります
  // v0.10.2から、timパラメータを追加します
  // timパラメータはサービス内にすでに存在するTIMインスタンスに使用され、TIMインスタンスの一意性を保証します。
  tim: tim
};
let trtcCalling = new TRTCCalling(options);
:::
</dx-codeblock>

### イベントのサブスクリプション/サブスクリプションキャンセルに関するインターフェース関数 


[](id:on)
#### on(eventName, callback, context)

コンポーネントからディスパッチされたイベントを監視するために使用します。詳細については、[イベントリスト](#event)をご参照ください。

<dx-codeblock>
::: javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.on('onInvited', handleInvite, this);
:::
</dx-codeblock>


[](id:off)
#### off(eventName, callback, context)

イベント監視をキャンセルするために使用します。

<dx-codeblock>
::: javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.off('onInvited', handleInvite, this);
:::
</dx-codeblock>

### SDK基本関数

[](id:login)
#### login({userID, userSig})

インターフェースにログインします。

<dx-codeblock>
::: javascript javascript
trtcCalling.login({userID, userSig})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ------------------------------------------------------------- |
| userID  | String | 現在のユーザーのID。文字列タイプ。アルファベット（a-zおよびA-Z）、数字（0-9）、ハイフン（-）、アンダーバー（\_）のみ使用できます。    |
| userSig  | String         | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |


[](id:logout)
#### logout()

 インターフェースからログアウトします。

<dx-codeblock>
::: javascript javascript
trtcCalling.logout()
:::
</dx-codeblock>

### 通話操作に関連するインターフェース関数


[](id:call)
#### call({userID, type, offlinePushInfo})

1対1通話招待、そのうちtypeは通話タイプ、1は音声通話、2はビデオ通話です。

>?
>- v1.0.0およびそれ以降のバージョンで、timeoutパラメータを取り消しました
>- v1.0.0およびそれ以降のバージョンに、offlinePushInfoパラメータを新たに追加しました（**オフラインプッシュはAndroidまたはiOS端末にのみ適用されます。WebおよびWeChat Mini Programはサポートしていません**）。

<dx-codeblock>
::: javascript javascript
// v1.0.0より前
trtcCalling.call({userID, type, timeout});

// v1.0.0およびそれ以降のバージョン
const offlinePushInfo = {
  title: '',
  description: '通話リクエストが1件あります',
}
trtcCalling.call({userID, type, offlinePushInfo})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味     |
| --------------- | ------ | -------------------------- |
| userID          | String | 被招待者のuserID  |
| type   | Number | 1：音声通話、2：ビデオ通話  |
| timeout         | Number | 0はタイムアウトしていないことを意味し、単位はs（秒）。**v1.0.0より前のバージョンのみ**        |
| offlinePushInfo | Object | メッセージのオフラインプッシュをカスタマイズします（オプション）。**v1.0.0およびそれ以降のバージョンのみ** |

offlinePushInfoパラメータ（v1.0.0およびそれ以降のバージョンのみ）

| パラメータ  | タイプ   | 意味    |
| -------------------- | ------ | ------------------------- |
| title | String | オフラインプッシュタイトル（オプション）     |
| description          | String | オフラインプッシュコンテンツ（オプション）      |
| androidOPPOChannelID | String | オフラインプッシュのためのOPPO携帯（システム8.0以上）のチャンネルIDを設定します（オプション）。 |
| extension            | String | オフラインプッシュパススルーコンテンツ（オプション）。**TRTCCallingバージョン>=1.0.2、tsignalingバージョン>= 0.9.0のみ** |

[](id:groupCall)
#### groupCall({userIDList, type, groupID, offlinePushInfo})
groupID パラメータは IM SDKにおけるグループ IDです。このパラメータを設定すると、通話リクエストメッセージがグループメッセージシステムを介してブロードキャストされます。このメッセージブロードキャスト方式は簡単で信頼性の高い方法です。設定しない場合は、`TRTCCalling` コンポーネントが単発メッセージで1人1人に通知を行います。

>? v1.0.0およびそれ以降のバージョンに、offlinePushInfoパラメータを新たに追加しました（**オフラインプッシュはAndroidまたはiOS端末にのみ適用されます。WebおよびWeChat Mini Programはサポートしていません**）。

<dx-codeblock>
::: javascript javascript
// v1.0.0より前
trtcCalling.groupCall({userIDList, type, groupID});

// v1.0.0およびそれ以降
const offlinePushInfo = {
  title: '',
  description: '通話リクエストが1件あります',
}
trtcCalling.groupCall({userIDList, type, groupID, offlinePushInfo})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味     |
| --------------- | ------ | -------------------------- |
| userIDList      | Array  | 招待リスト |
| type   | Number | 1：音声通話、2：ビデオ通話  |
| groupID         | String | IMグループID（オプション）        |
| offlinePushInfo | Object | メッセージのオフラインプッシュをカスタマイズします（オプション）。**v1.0.0およびそれ以降のバージョンのみ** |

offlinePushInfoパラメータ（v1.0.0およびそれ以降のバージョンのみ）

| パラメータ  | タイプ   | 意味    |
| -------------------- | ------ | ------------------------- |
| title | String | オフラインプッシュタイトル（オプション）     |
| description          | String | オフラインプッシュコンテンツ（オプション）      |
| androidOPPOChannelID | String | オフラインプッシュのためのOPPO携帯（システム8.0以上）のチャンネルIDを設定します（オプション）。 |
| extension            | String | オフラインプッシュパススルーコンテンツ（オプション）。**TRTCCallingバージョン>=1.0.2、tsignalingバージョン>= 0.9.0のみ** |

[](id:accept)
#### accept()
招待を受け取った後、このインターフェースを呼び出すと、現在の招待を受け入れます。

>?
>- 前回のinvitationの処理が未完了の場合、コンポーネントはデフォルトでビジー状態になり、その後のすべての招待はビジーを返します。
>- v1.0.0およびそれ以降のバージョンで、paramsパラメータを取り消しました。

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  // v1.0.0より前
  const { roomID, callType } = inviteData;
  trtcCalling.accept({inviteID, roomID, callType})
  // v1.0.0およびそれ以降
  trtcCalling.accept();
})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                                                  |
| -------- | ------ | ----------------------------------------------------- |
| inviteID | String | 招待ID。1回の招待を表示します（イベントINVITEDコールバックデータのinviteIDを監視）。**v1.0.0より前のバージョンのみ**    |
| roomID   | Number | 通話ルームナンバーID（イベントINVITEDコールバックデータのinviteData.roomIDを監視）。**v1.0.0より前のバージョンのみ**            |
| callType | Number | 1：音声通話、2：ビデオ通話（イベントINVITEDコールバックデータのinviteData.callTypeを監視）。**v1.0.0より前のバージョンのみ** |

[](id:reject)
#### reject()
招待を受け取った後、このインターフェースを呼び出すと、現在の招待が拒否されます。

>? v1.0.0およびそれ以降のバージョンで、paramsパラメータを取り消しました。

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  // v1.0.0より前
  const { callType } = inviteData;
  trtcCalling.reject({inviteID, isBusy, callType})
  // v1.0.0およびそれ以降
  trtcCalling.reject();
})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ     | タイプ    | 意味                                                  |
| -------- | ------- | ----------------------------------------------------- |
| inviteID | String  | 招待ID。1回の招待を表示します（イベントINVITEDコールバックデータのinviteIDを監視）。**v1.0.0より前のバージョンのみ**   |
| isBusy   | Boolean | 回線ビジー状態の有無。**v1.0.0より前のバージョンのみ**    |
| callType | Number  | 1：音声通話、2：ビデオ通話（イベントINVITEDコールバックデータのinviteData.callTypeを監視）。**v1.0.0より前のバージョンのみ** |

[](id:hangup)
#### hangup()
1. 通話中にこの関数を呼び出せば、通話を終了することができます。
2. ダイヤルしていない状態では、通話をキャンセルするために用いることができます。

<dx-codeblock>
::: javascript javascript
trtcCalling.hangup()
:::
</dx-codeblock>


### ビデオ制御に関連するインターフェース関数

[](id:startRemoteView)
#### startRemoteView({userID, videoViewDomID})
リモートユーザーのカメラデータを指定されたDOM IDノードにレンダリングします。

<dx-codeblock>
::: javascript javascript
trtcCalling.startRemoteView({userID, videoViewDomID})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味       |
| -------------- | ------ | ---------------------------- |
| userID         | String | ユーザーID       |
| videoViewDomID | String | konoユーザーデータは、このDOM IDノードにレンダリングされたvideoタグを介して再生されます |

[](id:stopRemoteView)
#### stopRemoteView({userID})
リモートユーザーのカメラデータによってレンダリングされたDOMノードを削除します。

>? v1.0.0およびそれ以降のバージョンで、videoViewDomIDパラメータを削除しました。

<dx-codeblock>
::: javascript javascript
// v1.0.0より前
trtcCalling.stopRemoteView({userID, videoViewDomID});
// v1.0.0およびそれ以降
trtcCalling.stopRemoteView({userID});

:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| -------------- | ------ | ------------------------------- |
| userID         | String | ユーザーID       |
| videoViewDomID | String | 該当するDOM IDノードのvideoタグを削除し、ビデオ再生を停止します。**v1.0.0より前のバージョンのみ** |

[](id:startLocalView)
#### startLocalView({userID, videoViewDomID})
ローカルユーザーのカメラデータを指定されたDOM IDノードにレンダリングします。

<dx-codeblock>
::: javascript javascript
trtcCalling.startLocalView({userID, videoViewDomID})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味         |
| -------------- | ------ | ------------------------------ |
| userID         | String | ユーザーID       |
| videoViewDomID | String | ローカルユーザーデータは、このDOM IDノードにレンダリングされたvideoタグを介して再生されます |

[](id:stopLocalView)
#### stopLocalView({userID})

ローカルユーザーのカメラデータによってレンダリングされたDOMノードを削除します。

>?v1.0.0およびそれ以降のバージョンで、videoViewDomIDパラメータを削除しました。

<dx-codeblock>
::: javascript javascript
// v1.0.0より前
trtcCalling.stopLocalView({userID, videoViewDomID});
// v1.0.0およびそれ以降
trtcCalling.stopLocalView({userID});
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| -------------- | ------ | ------------------------------- |
| userID         | String | ユーザーID       |
| videoViewDomID | String | 該当するDOM IDノードのvideoタグを削除し、ビデオ再生を停止します。**v1.0.0より前のバージョンのみ** |

[](id:openCamera)
#### openCamera()
ローカルカメラをオンにします。

<dx-codeblock>
::: javascript javascript
trtcCalling.openCamera()
:::
</dx-codeblock>

[](id:closeCamera)
####  closeCamera()
カメラをオフにします。

<dx-codeblock>
::: javascript javascript
trtcCalling.closeCamera()
:::
</dx-codeblock>

[](id:setMicMute)
####  setMicMute(isMute) 
マイクをオン/オフします。

<dx-codeblock>
::: javascript javascript
trtcCalling.setMicMute(true) // マイクオフ
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味  |
| ------ | ------- | --------------- |
| isMute | Boolean | <li/>true: マイクのオフ <li/>false: マイクのオン |

[](id:setVideoQuality)
####  setVideoQuality(profile) 
ビデオの画質を設定します。
>?  
>- v0.8.0およびそれ以降のバージョンは、このメソッドが新規追加されました。
>- このメソッドは、call、groupCall、acceptの前に設定する必要があり、その後の設定は有効になりません。

<dx-codeblock>
::: javascript javascript
trtcCalling.setVideoQuality('720p') // ビデオの画質を720pに設定します
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味  |
| ------ | ------- | --------------- |
| profile | String | <li/>480p：640 × 480 <li/>720p：1280 × 720  <li/>1080p：1920 × 1080  |

[](id:switchToAudioCall)
####  switchToAudioCall() 
ビデオ通話を音声通話へ切り替えます。
>?  
>- v0.10.0およびそれ以降のバージョンは、このメソッドが新規追加されました。
>- 1v1通話中のみ使用をサポートします。
>- ERRORイベントの監視に失敗しました。code：60001。

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToVideoCall() // ビデオ通話を音声通話へ切り替え
:::
</dx-codeblock>

[](id:switchToVideoCall)
####  switchToVideoCall() 
音声通話をビデオ通話へ切り替えます。
>?  
>- v0.10.0およびそれ以降のバージョンは、このメソッドが新規追加されました。
>- 1v1通話中のみ使用をサポートします。
>- ERRORイベントの監視に失敗しました。code：60002。

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToVideoCall() // 音声通話をビデオ通話へ切り替え
:::
</dx-codeblock>

[](id:getCameras)
####  getCameras() 

このインターフェースを呼び出すと、カメラデバイスリストを取得することができます。

>? v1.0.0およびそれ以降のバージョンに、このメソッドを新たに追加しました。

<dx-codeblock>
::: javascript javascript
trtcCalling.getCameras() // カメラリストの取得
:::
</dx-codeblock>

[](id:getMicrophones)
####  getMicrophones() 

このインターフェースを呼び出すと、マイクデバイスリストを取得することができます。

>? v1.0.0およびそれ以降のバージョンに、このメソッドを新たに追加しました。

<dx-codeblock>
::: javascript javascript
trtcCalling.getMicrophones() // マイクリストの取得
:::
</dx-codeblock>

[](id:switchDevice)
####  switchDevice({deviceType, deviceId}) 

このインターフェースを呼び出すと、カメラまたはマイクのデバイスを切り替えることができます。

>? v1.0.0およびそれ以降のバージョンに、このメソッドを新たに追加しました。

<dx-codeblock>
::: javascript javascript
trtcCalling.switchDevice({deviceType: 'audio', deviceId: deviceId}) // デバイスの切り替え
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味          |
| ---------- | ------ | ------------------------------- |
| deviceType | String | video: カメラ、 audio: マイク   |
| deviceId   | String | <li/>カメラデバイスIDはgetCameras()で取得します<li/>マイクデバイスIDはgetMicrophones()で取得します |


[](id:event)
## TRTCCallingイベントリスト

次のコードを参照して、[TRTCCalling コンポーネントイベント](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/module-EVENT.html)を監視できます。

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
// etc
function handleInviteeReject({userID}) {

}
trtcCalling.on(TRTCCalling.EVENT.REJECT, handleInviteeReject)
:::
</dx-codeblock>

### 招待側イベント

|      CODE       |   イベント受信側   |  説明   |
| :--------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     招待側     |     被招待ユーザーは通話拒否      |
|[NO_RESP](#no_resp)     |     招待側     |    被招待ユーザーの応答がなくタイムアウト     |
|[LINE_BUSY](#line_busy)   |     招待側     | 被招待ユーザーは通話中、ビジー状態  |
|[INVITED](#invited)     |     被招待側     |      招待通知を受信済み       |
|[CALLING_CANCEL](#calling_cancel)       |     被招待側     |     相手側による今回通話のキャンセル      |
|[CALLING_TIMEOUT](#calling_timeout)      |     被招待側     |    今回の通話に応答せずにタイムアウト     |
|[USER_ENTER](#user_enter)  | 招待側と被招待側 |         ユーザー入室          |
|[USER_LEAVE](#user_leave)  | 招待側と被招待側 |      通話から離脱したユーザーあり       |
|[CALL_END](#call_end)    | 招待側と被招待側 |       今回の通話終了        |
|[KICKED_OUT](#kicked_out)  | 招待側と被招待側 |   ログイン重複により、ルームから強制退出    |
|[USER_VIDEO_AVAILABLE](#user_video_available) | 招待側と被招待側 | リモートユーザーによるカメラのオン/オフ |
|[USER_AUDIO_AVAILABLE](#user_audio_available) | 招待側と被招待側 | リモートユーザーによるマイクのオン/オフ |

### 一般的なイベントコールバック


#### SDK_READY

SDKがready状態に入るとこのコールバックを受信します

>?v1.0.0およびそれ以降のバージョンに、このイベントを新たに追加しました。

<dx-codeblock>
::: javascript javascript
let onSDKReady = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.SDK_READY, onSDKReady);
:::
</dx-codeblock>

#### USER_ENTER

ユーザーが入室しました。
トリガー条件：ユーザーが通話に参加する。

<dx-codeblock>
::: javascript javascript
let handleUserEnter = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.USER_ENTER, handleUserEnter);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID         | String | ユーザーID    |

#### USER_LEAVE

ユーザーが退室しました。
トリガー条件：ユーザーが通話を退出する。

<dx-codeblock>
::: javascript javascript
let handleUserLeave = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.USER_LEAVE, handleUserLeave);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID         | String | ユーザーID    |

#### GROUP_CALL_INVITEE_LIST_UPDATE

グループチャットで招待リストを更新するとこのコールバックを受信します

>?v1.0.0およびそれ以降のバージョンに、このイベントを新たに追加しました。

<dx-codeblock>
::: javascript javascript
let handleGroupInviteeListUpdate = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.GROUP_CALL_INVITEE_LIST_UPDATE, handleGroupInviteeListUpdate);
:::
</dx-codeblock>

#### CALL_END

今回の通話は終了しました。
トリガー条件：今回の通話を終了する。

<dx-codeblock>
::: javascript javascript
let handleCallingEnd = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALL_END, handleCallingEnd);
:::
</dx-codeblock>

#### KICKED_OUT

ログインを繰り返したことにより、ルームから強制退室させられました。
トリガー条件：他のページに重複ログインする。

<dx-codeblock>
::: javascript javascript
let handleKickedOut = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.KICKED_OUT, handleKickedOut);
:::
</dx-codeblock>

#### USER_VIDEO_AVAILABLE

リモートユーザーがカメラをオン/オフにします。
トリガー条件：リモートユーザーがカメラをオン/オフにする。

<dx-codeblock>
::: javascript javascript
let handleUserVideoChange = function({userID, isVideoAvailable}) {
  console.log(userID, isVideoAvailable)
};
trtcCalling.on(TRTCCalling.EVENT.USER_VIDEO_AVAILABLE, handleUserVideoChange);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味         |
| ---------------- | ------- | ------------------------------ |
| userID  | String  | ユーザーID      |
| isVideoAvailable | Boolean | <li/>true：リモートユーザーによるカメラオン<li/>false：リモートユーザーによるカメラオフ |

#### USER_AUDIO_AVAILABLE

リモートユーザーがマイクをオン/オフにしました。
トリガー条件：リモートユーザーがマイクをオン/オフする。

<dx-codeblock>
::: javascript javascript
let handleUserAudioChange = function({userID, isAudioAvailable}) {
  console.log(userID, isAudioAvailable)
};
trtcCalling.on(TRTCCalling.EVENT.USER_AUDIO_AVAILABLE, handleUserAudioChange);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味  |
| ---------------- | ------- | -------------------------------- |
| userID  | String  | ユーザーID        |
| isAudioAvailable | Boolean | <li/>true：リモートユーザーによるマイクオン  <li/> false：リモートユーザーによるマイクオフ |

### 招待側イベントコールバック

#### REJECT

ユーザーが通話を拒否しました。
トリガー条件：被招待者が通話を拒否し、発信者がREJECTイベントコールバックを受け取る。

<dx-codeblock>
::: javascript javascript
let handleInviteeReject = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.REJECT, handleInviteeReject);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID         | String | ユーザーID    |

#### NO_RESP

招待されたユーザーは応答しませんでした。
トリガー条件：call/groupCallにtimeoutを設定し、被招待者がtimeout内に出なかった場合、発信者がNO_RESPイベントコールバックを受け取る。

<dx-codeblock>
::: javascript javascript
let handleNoResponse = function({userID, userIDList}) {
  console.log(userID, userIDList)
};
trtcCalling.on(TRTCCalling.EVENT.NO_RESP, handleNoResponse);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味         |
| ---------- | ------ | ------------ |
| userID     | String | ユーザーID      |
| userIDList | Array  | タイムアウトユーザーリスト |

#### LINE_BUSY

被招待側は通話中で、ビジー状態です。
トリガー条件：被招待者が通話中である場合、発信者がLINE_BUSYイベントコールバックを受け取る。

<dx-codeblock>
::: javascript javascript
let handleLineBusy = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.LINE_BUSY, handleLineBusy);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID         | String | ユーザーID    |

### 被招待側イベントコールバック
#### INVITED
招待通知を受領しました。
トリガー条件：招待通知があった場合、被招待者がINVITEDイベントコールバックを受け取る。

<dx-codeblock>
::: javascript javascript
let handleNewInvitationReceived = function({
    sponsor, userIDList, isFromGroup, inviteData, inviteID
}) {
  console.log(sponsor, userIDList, isFromGroup, inviteData, inviteID)
};
trtcCalling.on(TRTCCalling.EVENT.INVITED, handleNewInvitationReceived);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ        | タイプ    | 意味         |
| ----------- | ------- | ------------------------------------------------ |
| sponsor     | String  | 招待者       |
| userIDList  | Array   | 同時に招待された人   |
| isFromGroup | Boolean | IMグループの招待の有無   |
| inviteData  | Object  | <li/>新しいユーザーへの招待： {version, callType, roomID} <li/>最後のユーザーとの通話終了：{version, callType, callEnd} |
| inviteID    | String  | 招待ID。1回の招待を表示       |

#### CALLING_CANCEL
今回の通話はキャンセルされました。
トリガー条件：発信者がコール中に通話をキャンセルし、被招待者がCALLING_CANCELイベントコールバックを受け取る。

<dx-codeblock>
::: javascript javascript
let handleCallingCancel = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALLING_CANCEL, handleCallingCancel);
:::
</dx-codeblock>


#### CALLING_TIMEOUT

今回の通話はタイムアウトで、応答はありませんでした。
トリガー条件：call/groupCallにtimeoutを設定し、被招待者がtimeout内に出なかった場合、被招待者がCALLING_TIMEOUTイベントコールバックを受け取る

<dx-codeblock>
::: javascript javascript
let handleCallingTimeout = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALLING_TIMEOUT, handleCallingTimeout);
:::
</dx-codeblock>

## TRTCCalling エラーコードリスト

EVENTのERRORフィールドを監視することによって、コンポーネントからスローされたエラーを処理することができます。サンプルコードは次のとおりです。

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
let onError = function(error) {
  console.log(error)
};
trtcCalling.on(TRTCCalling.EVENT.ERROR, onError);
:::
</dx-codeblock>

[](id:Error)
#### Error code

| code  | エラータイプ     | 意味        |
| ----- | ------------ | -------------------------- |
| 60001     | メソッドのコールに失敗しました  | switchToAudioCallのコールに失敗しました   |
| 60002     | メソッドのコールに失敗しました  | switchToAudioCallのコールに失敗しました   |
| 60003 | 権限の取得に失敗しました | 使用可能なマイクデバイスがありません       |
| 60004 | 権限の取得に失敗しました | 使用可能なカメラデバイスがありません       |
| 60005 | 権限の取得に失敗しました | ユーザーがデバイスの使用を禁止しています  |
| 60006 | 環境検出に失敗しました | 現在の環境はWebRTC（>=v1.0.4バージョン）をサポートしていません      |

## アップグレードガイド

- **TRTCCallingバージョンを>= 1.0.2にアップグレードします **
	- 注意：TSignalingバージョンを>= 0.9.0にアップグレードする必要があります
	- 原因：[ログの更新](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/tutorial-CHANGELOG.html#h2-3)
- **1.0.2にアップグレード >=TRTCCallingバージョン >=1.0.0**
	- 注意：TSignalingバージョンを>= 0.8.0にアップグレードする必要があります
	- 原因：[ログの更新](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/tutorial-CHANGELOG.html#h2-5)

## よくあるご質問

#### 通話がつながらなかったり、強制オフラインになったりするのはなぜですか？
コンポーネントは現在、マルチインスタンスのログインや**オフラインプッシュのシグナリング**機能をサポートしていません。現在のログインアカウントの一意性をご確認ください。
> ?
> - **マルチインスタンス**：1つのUserIDで繰り返しログインしたり、異なるターミナルからログインしたりすると、シグナリングの混乱が生じます。
> - **オフラインプッシュ**：インスタンスはオンラインの場合にのみメッセージを受信できます。インスタンスがオフラインのときに受信したシグナリングは、オンラインになった後は再度プッシュされません。
その他よくあるご質問については、 [TRTCCalling Webに関するご質問](https://intl.cloud.tencent.com/document/product/647/43096)をご参照ください。

## 技術的なお問い合わせ

詳細については、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)にご連絡をいただくか、colleenyu@tencent.comにメールでご連絡ください。


## 参考ドキュメント
- [TRTCCalling web公式サイトで体験](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html#/login)
- [TRTCCalling npm](https://www.npmjs.com/package/trtc-calling-js)
- [TRTCCalling web demoソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Web/TRTCScenesDemo/trtc-calling-web)
- [TRTCCalling web API](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/TRTCCalling.html)
- [TRTCCalling webに関するご質問](https://intl.cloud.tencent.com/document/product/647/43096)
