## TRTCCallingの概要

[TRTCCalling](https://www.npmjs.com/package/trtc-calling-js)コンポーネントは、Tencent CloudのTencent Real-Time Communication（TRTC）とInstant Messaging（IM）サービスの組み合わせにより構成されており、1対1および複数人でのビデオ/音声通話をサポートしています。具体的な実装プロセスについては、[リアルタイム音声通話（Web）](https://intl.cloud.tencent.com/document/product/647/38928)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。

## TRTCCalling API 

#### イベントサブスクリプション/サブスクリプションのキャンセルに関するインターフェース関数 
このコンポーネントはイベントのディスパッチに基づいて管理します。アプリケーション層は、コンポーネントからディスパッチされるイベントにインタラクティブに応じて変更することができます。

| API                                                                         | 説明         |
| --------------------------------------------------------------------------- | ------------ |
| [on(eventName, callback, context)](#on(eventname.2C-callback.2C-context))   | イベントをサブスクライブします     |
| [off(eventName, callback, context)](#off(eventname.2C-callback.2C-context)) | イベントのサブスクライブをキャンセルします |

#### SDK 基本関数

| API                                                         | 説明                                           |
| ----------------------------------------------------------- | ---------------------------------------------- |
| [login({userID, userSig})](#login(.7Buserid.2C-usersig.7D)) | IMインターフェースにログインします。すべての機能は、まずログインしてからでないと使用できません |
| [logout()](#logout())                                       | インターフェースからログアウトします。ログアウトした後は、ダイヤル操作ができなくなります           |

#### 通話操作に関連するインターフェース関数
| API                                                                                       | 説明         |
| ----------------------------------------------------------------------------------------- | ------------ |
| [call({userID, type, timeout}))](#call(.7Buserid.2C-type.2C-timeout.7D))                  | 個人の通話の招待 |
| [groupCall({userIDList, type, groupID})](#groupcall(.7Buseridlist.2C-type.2C-groupid.7D)) | グループチャット通話の招待 |
| [accept({inviteID, roomID, callType})](#accept(.7Binviteid.2C-roomid.2C-calltype.7D))     | 通話招待の受け入れ |
| [reject({inviteID, isBusy, callType})](#reject(.7Binviteid.2C-isbusy.2C-calltype.7D))     | 通話招待の拒否 |
| [hangup()](#hangup())                                                                     | 現在通話の終了 |

#### ビデオ制御に関連するインターフェース関数
| API                                                                                           | 説明               |
| --------------------------------------------------------------------------------------------- | ------------------ |
| [startRemoteView({userID, videoViewDomID})](#startremoteview(.7Buserid.2C-videoviewdomid.7D)) | リモート画像のレンダリングの起動   |
| [stopRemoteView({userID, videoViewDomID})](#stopremoteview(.7Buserid.2C-videoviewdomid.7D))   | リモート画像のレンダリングの停止   |
| [startLocalView({userID, videoViewDomID})](#startlocalview(.7Buserid.2C-videoviewdomid.7D))   | ローカル画像のレンダリングの起動   |
| [stopLocalView({userID, videoViewDomID})](#stoplocalview(.7Buserid.2C-videoviewdomid.7D))     | ローカル画像のレンダリングの停止   |
| [openCamera()](#opencamera())                                                                 | カメラの起動         |
| [closeCamera()](#closecamera())                                                               | カメラの終了         |
| [setMicMute(isMute)](#setmicmute(ismute))                                                     | デバイスマイクのミュートの有無 |
| [setVideoQuality(profile)](#setvideoquality(profile) ) |   ビデオ品質の設定 |
| [switchToAudioCall()](#switchtoaudiocall()) | ビデオ通話を音声通話へ切り替え|
| [switchToVideoCall()](#switchtovideocall()) | 音声通話をビデオ通話へ切り替え|

## TRTCCallingの詳細

### TRTCCallingコンポーネントのインスタンスの作成

まず、Tencent Real-Time Communication [コンソール](https://console.cloud.tencent.com/trtc/app)でアプリケーションを作成し、SDKAppIDを取得する必要があります。
その後、`new TRTCCalling()`メソッドを使ってTRTCCalling コンポーネントのインスタンスを取得することができます。

<dx-codeblock>
:::  javascript javascript
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



#### on(eventName, callback, context)
コンポーネントからディスパッチされたイベントを監視するために使用します。詳細については、[イベントリスト](#event)をご参照ください。

<dx-codeblock>
:::  javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.on('onInvited', handleInvite, this);
:::
</dx-codeblock>



#### off(eventName, callback, context)
イベント監視をキャンセルするために使用します。

<dx-codeblock>
:::  javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.off('onInvited', handleInvite, this);
:::
</dx-codeblock>

### SDK 基本関数



#### login({userID, userSig})
インターフェースにログインします。

<dx-codeblock>
:::  javascript javascript
trtcCalling.login({userID, userSig})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                                                                                                                    |
| ------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| userID   | String | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。 |
| userSig  | String                | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法 ](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |



#### logout()
 インターフェースからログアウトします。
<dx-codeblock>
:::  javascript javascript
trtcCalling.logout()
:::
</dx-codeblock>

### 通話操作に関連するインターフェース関数



#### call({userID, type, timeout})

1対1通話招待、そのうちtypeは通話タイプ、1は音声通話、2はビデオ通話です。

<dx-codeblock>
:::  javascript javascript
trtcCalling.call({userID, type, timeout})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                     |
| ------- | ------ | ------------------------ |
| userID  | String | 被招待者のuserID          |
| type    | Number | 1：音声通話、2：ビデオ通話 |
| timeout | Number | 0はタイムアウトしていないことを意味し、単位はs（秒）    |



#### groupCall({userIDList, type, groupID})
groupID パラメータは IM SDKにおけるグループ IDです。このパラメータを設定すると、通話リクエストメッセージがグループメッセージシステムを介してブロードキャストされます。このメッセージブロードキャスト方式は簡単で信頼性の高い方法です。設定しない場合は、`TRTCCalling` コンポーネントが単発メッセージで1人1人に通知を行います。

<dx-codeblock>
:::  javascript javascript
trtcCalling.groupCall({userIDList, type, groupID})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味                     |
| ---------- | ------ | ------------------------ |
| userIDList | Array  | 招待リスト                 |
| type       | Number | 1：音声通話、2：ビデオ通話 |
| groupID    | String | IMグループID （オプション）      |


#### accept({inviteID, roomID, callType})
招待を受け取った後、このインターフェースを呼び出すと、現在の招待を受け入れます。
>? 前回のinvitationの処理が未完了の場合、コンポーネントはデフォルトでビジー状態になり、その後のすべての招待はビジーを返します。

<dx-codeblock>
:::  javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.accept({inviteID, roomID, callType})
})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                     |
| -------- | ------ | ------------------------ |
| inviteID | String | 招待ID、1回の招待を表示    |
| roomID   | Number | 通話ルーム番号 ID            |
| callType | Number | 1：音声通話、2：ビデオ通話 |


#### reject({inviteID, isBusy, callType})
招待を受け取った後、このインターフェースを呼び出すと、現在の招待が拒否されます。

<dx-codeblock>
:::  javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.reject({inviteID, isBusy, callType})
})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ     | タイプ    | 意味                    |
| -------- | ------- | ------------------------ |
| inviteID | String  | 招待ID、1回の招待を表示    |
| isBusy   | Boolean | ビジー状態の有無             |
| callType | Number  | 1：音声通話、2：ビデオ通話 |



#### hangup()
1. 通話中にこの関数を呼び出せば、通話を終了することができます。
2. ダイヤルしていない状態では、通話をキャンセルするために用いることができます。

<dx-codeblock>
:::  javascript javascript
trtcCalling.hangup()
:::
</dx-codeblock>


### ビデオ制御に関連するインターフェース関数


#### startRemoteView({userID, videoViewDomID})
リモートユーザーのカメラデータを指定されたDOM IDノードにレンダリングします。
<dx-codeblock>
:::  javascript javascript
trtcCalling.startRemoteView({userID, videoViewDomID})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                                      |
| -------------- | ------ | --------------------------------------------------------- |
| userID         | String | ユーザーID                                                   |
| videoViewDomID | String | konoユーザーデータは、このDOM IDノードにレンダリングされたvideoタグを介して再生されます |


#### stopRemoteView({userID, videoViewDomID})
リモートユーザーのカメラデータによってレンダリングされたDOMノードを削除します。
<dx-codeblock>
:::  javascript javascript
trtcCalling.stopRemoteView({userID, videoViewDomID})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                              |
| -------------- | ------ | ------------------------------------------------- |
| userID         | String | ユーザーID                                           |
| videoViewDomID | String | このDOM ID ノードのvideoタグを削除し、ビデオの再生を停止します |


#### startLocalView({userID, videoViewDomID})
ローカルユーザーのカメラデータを指定されたDOM IDノードにレンダリングします。
<dx-codeblock>
:::  javascript javascript
trtcCalling.startLocalView({userID, videoViewDomID})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                                         |
| -------------- | ------ | ----------------------------------------------------------- |
| userID         | String | ユーザーID                                                     |
| videoViewDomID | String | ローカルユーザーデータは、このDOM IDノードにレンダリングされたvideoタグを介して再生されます |


#### stopLocalView({userID, videoViewDomID})
ローカルユーザーのカメラデータによってレンダリングされたDOMノードを削除します。
<dx-codeblock>
:::  javascript javascript
trtcCalling.stopLocalView({userID, videoViewDomID})
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                              |
| -------------- | ------ | ------------------------------------------------- |
| userID         | String | ユーザーID                                           |
| videoViewDomID | String | このDOM IDノードのvideoタグを削除し、ビデオの再生を停止します |


#### openCamera()
ローカルカメラをオンにします。
<dx-codeblock>
:::  javascript javascript
trtcCalling.openCamera()
:::
</dx-codeblock>


####  closeCamera()
カメラをオフにします。
<dx-codeblock>
:::  javascript javascript
trtcCalling.closeCamera()
:::
</dx-codeblock>


####  setMicMute(isMute) 
マイクをオン/オフします。
<dx-codeblock>
:::  javascript javascript
trtcCalling.setMicMute(true) // マイクのオン
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                                          |
| ------ | ------- | --------------------------------------------- |
| isMute | Boolean | <li/>true：マイクのオフ <li/> false：マイクのオン |

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

| パラメータ   | タイプ    | 意味                                         |
| ------ | ------- | -------------------------------------------- |
| profile | String | <li/>480p: 640 × 480 <li/>720p: 1280 × 720  <li/>1080p: 1920 × 1080  |

####  switchToAudioCall() 
ビデオ通話を音声通話へ切り替えます。
>?  
>- v0.10.0以降のバージョンで、このメソッドを追加します。
>- 1v1通話中のみ使用をサポートします。
>- ERRORイベントの監視に失敗しました。code：60001。

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToVideoCall() // ビデオ通話を音声通話へ切り替え
:::
</dx-codeblock>

####  switchToVideoCall() 
音声通話をビデオ通話へ切り替えます。
>?  
>- v0.10.0以降のバージョンで、このメソッドを追加します。
>- 1v1通話中のみ使用をサポートします。
>- ERRORイベントの監視に失敗しました。code：60002。

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToVideoCall() // 音声通話をビデオ通話へ切り替え
:::
</dx-codeblock>


[](id:event)
## TRTCCallingイベントリスト
次のコードを参照して、[TRTCCalling コンポーネントイベント](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/module-EVENT.html)を監視できます。

<dx-codeblock>
:::  javascript javascript
import TRTCCalling from 'trtc-calling-js';
// etc
function handleInviteeReject({userID}) {

}
trtcCalling.on(TRTCCalling.EVENT.REJECT, handleInviteeReject)
:::
</dx-codeblock>

### 招待側イベント
|                     CODE                      |   イベント受領側   |           説明            |
| :-------------------------------------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     招待側     |     被招待ユーザーは通話拒否      |
|              [NO_RESP](#no_resp)              |     招待側     |    被招待ユーザーはタイムアウト後に応答なし     |
|            [LINE_BUSY](#line_busy)            |     招待側     | 被招待ユーザーは通話中、ビジー状態  |
|              [INVITED](#invited)              |     被招待側     |      招待通知を受領済み       |
|       [CALLING_CANCEL](#calling_cancel)       |     被招待側     |     今回の通話をキャンセル済み      |
|      [CALLING_TIMEOUT](#calling_timeout)      |     被招待側     |    今回の通話はタイムアウト後に応答なし     |
|           [USER_ENTER](#user_enter)           | 招待側と被招待側 |         ユーザー入室          |
|           [USER_LEAVE](#user_leave)           | 招待側と被招待側 |       ユーザーが通話を退出しました        |
|             [CALL_END](#call_end)             | 招待側と被招待側 |       今回の通話終了        |
|           [KICKED_OUT](#kicked_out)           | 招待側と被招待側 |   ログインを繰り返したことにより、ルームから強制退室    |
| [USER_VIDEO_AVAILABLE](#user_video_available) | 招待側と被招待側 | リモートユーザーによるカメラのオン/オフ |
| [USER_AUDIO_AVAILABLE](#user_audio_available) | 招待側と被招待側 | リモートユーザーによるマイクのオン/オフ |

### 一般的なイベントコールバック

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
| userID | String | ユーザーID |

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
| userID | String | ユーザーID |

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

重複ログインにより、ルームから強制退室させられました。
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

| パラメータ             | タイプ    | 意味                                                         |
| ---------------- | ------- | ----------------------------------------------------------- |
| userID           | String  | ユーザーID                                                     |
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

| パラメータ             | タイプ    | 意味                                                           |
| ---------------- | ------- | ------------------------------------------------------------- |
| userID           | String  | ユーザーID                                                       |
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
| userID | String | ユーザーID |

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
| userID | String | ユーザーID |

### 被招待側イベントコールバック

#### INVITED

招待通知を受け取りました。
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

| パラメータ        | タイプ    | 意味                                                                                                     |
| ----------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| sponsor     | String  | 招待者                                                                                                   |
| userIDList  | Array   | 同時に招待された人                                                                                         |
| isFromGroup | Boolean | IMグループの招待の有無                                                                                           |
| inviteData  | Object  | <li/>新しいユーザーへの招待： {version, callType, roomID} <li/>最後のユーザーとの通話終了：{version, callType, callEnd} |
| inviteID    | String  | 招待ID、1回招待を表示                                                                                      |

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
:::  javascript javascript
import TRTCCalling from 'trtc-calling-js';
let onError = function(error) {
  console.log(error)
};
trtcCalling.on(TRTCCalling.EVENT.ERROR, onError);
:::
</dx-codeblock>

#### Error code
| code      | エラータイプ    | 意味                        |
| --------- | ----------- | ----------------------------- |
| 60001     | メソッドのコールに失敗しました  | switchToAudioCallのコールに失敗しました   |
| 60002     | メソッドのコールに失敗しました  | switchToVideoCallのコールに失敗しました   |


## よくあるご質問
#### 通話がつながらなかったり、強制オフラインになったりするのはなぜですか？
コンポーネントは現在、マルチインスタンスのログインや**オフラインプッシュのシグナリング**機能をサポートしていません。現在のログインアカウントの一意性をご確認ください。
> ?
> - **マルチインスタンス**：1つのUserIDで繰り返しログインしたり、異なるターミナルからログインしたりすると、シグナリングの混乱が生じます。
> - **オフラインプッシュ**：インスタンスはオンラインの場合にのみメッセージを受信できます。インスタンスがオフラインのときに受信したシグナリングは、オンラインになった後は再度プッシュされません。
