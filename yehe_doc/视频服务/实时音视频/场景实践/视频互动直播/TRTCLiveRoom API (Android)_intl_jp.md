TRTCLiveRoomは、Tencent CloudのTencent Real-Time Communication（TRTC）およびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。
- キャスターが新しいライブストリーミングルームを作成して配信を開始し、視聴者がライブストリーミングルームに参加して視聴します。
- キャスターと視聴者がビデオでマイク接続によるコラボライブを行います。
- 2つの異なるルームの間でキャスター同士のPK（クロスルーム対戦）を行います。
- 各種のテキストメッセージやカスタムメッセージの送信をサポートします。カスタムメッセージは弾幕、「いいね」、ギフトを実装するために使用することができます。

TRTCLiveRoom はオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実現プロセスは、[ビデオマイク接続ライブストリーミング（Android）](https://intl.cloud.tencent.com/document/product/647/36061)をご参照ください。
- TRTC SDK： [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615) を低遅延のライブストリーミングコンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996)のAVChatroomを使用して、ライブストリーミングチャットルーム機能を実装します。同時に、IMのメッセージでキャスター間のマイク接続のフローをつなげます。

[](id:TRTCLiveRoom)
## TRTCLiveRoom API概要

### SDK基本関数

| API | 説明 |
|-----|-----|
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを破棄します。 |
| [setDelegate](#setdelegate) | イベントコールバックを設定します。|
| [setDelegateHandler](#setdelegatehandler) | イベントコールバックが設定されているスレッドです。 |
| [login](#login) | ログイン。|
| [logout](#logout) | ログアウト。|
| [setSelfProfile](#setselfprofile) | 個人情報を修正します。|

### ルーム関連インターフェース関数

| API | 説明 |
|-----|-----|
| [createRoom](#createroom) | ルームの作成（キャスターが呼び出し）。ルームが存在しない場合は、システムが新しいルームを自動作成します。|
| [destroyRoom](#destroyroom) |ルームの破棄（キャスターが呼び出し）。|
| [enterRoom](#enterroom) | 入室（視聴者が呼び出し）。|
| [exitRoom](#exitroom) | 退室（視聴者が呼び出し）。|
| [getRoomInfos](#getroominfos) | ルームリストの詳細情報を取得します。|
| [getAnchorList](#getanchorlist) | ルーム内の全キャスターのリストを取得します。enterRoom()成功後に呼び出しが有効になります。|
| [getAudienceList](#getaudiencelist) | ルーム内の全視聴者の情報を取得します。enterRoom()成功後に呼び出しが有効になります。|

### プッシュプルストリームに関連するインターフェース関数

| API | 説明 |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | ローカルビデオのプレビュー画面を立ち上げます。|
| [stopCameraPreview](#stopcamerapreview) | ローカルのビデオキャプチャおよびプレビューを停止します。|
| [startPublish](#startpublish) | ライブストリーミング（プッシュ）を開始します。|
| [stopPublish](#stoppublish) | ライブストリーミング（プッシュ）を停止します。|
| [startPlay](#startplay) | リモートのビデオ画面を再生します。普通の視聴とマイク接続のシーンで呼び出すことができます。|
| [stopPlay](#stopplay) | リモートのビデオ画面のレンダリングを停止します。|

### キャスターと視聴者のマイク接続

| API | 説明 |
|-----|-----|
| [requestJoinAnchor](#requestjoinanchor) | 視聴者がマイク接続をリクエストします。|
| [responseJoinAnchor](#responsejoinanchor) | キャスターがマイク接続のリクエストを処理します。|
| [kickoutJoinAnchor](#kickoutjoinanchor) | キャスターがマイク接続の視聴者をキックアウトします。|

### キャスターのルーム間PK

| API | 説明 |
|-----|-----|
| [requestRoomPK](#requestroompk) | キャスターがルーム間のPKをリクエストします。|
| [responseRoomPK](#responseroompk) | キャスターがルーム間PKのリクエストに応答します。|
| [quitRoomPK](#quitroompk) | ルーム間PKから退出します。|

### オーディオビデオ制御に関連するインターフェース関数

| API | 説明 |
|-----|-----|
| [switchCamera](#switchcamera) | フロント/リアカメラを切り替えます。 |
| [setMirror](#setmirror) | ミラー表示のオン/オフを設定します。|
| [muteLocalAudio](#mutelocalaudio) | ローカルオーディオをミュートにします。|
| [muteRemoteAudio](#muteremoteaudio) | リモートオーディオをミュートにします。|
| [muteAllRemoteAudio](#muteallremoteaudio) | 全てのリモート側のオーディオをミュートにします。|

### BGMサウンドエフェクト関連インターフェース関数

| API | 説明 |
|-----|-----|
| [getAudioEffectManager](#getaudioeffectmanager) | BGMサウンドエフェクト管理オブジェクト[TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager)を取得します。|

### 美顔フィルタに関するインターフェース関数

| API | 説明 |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得します。|

### メッセージ送信関連インターフェース関数

| API | 説明 |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | ルーム内でのテキストメッセージのブロードキャスト。通常、弾幕によるチャットに使用します。|
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを送信します。|

### デバックに関するインターフェース関数

| API | 説明 |
|-----|-----|
| [showVideoDebugLog](#showvideodebuglog) | インターフェースにdebug情報を表示するか。|

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API概要</h2>

### 一般的なイベントコールバック

| API | 説明 |
|-----|-----|
| [onError](#onerror) | エラーのコールバック。|
| [onWarning](#onwarning) | 警告のコールバック。|
| [onDebugLog](#ondebuglog) | Logコールバック。|

### ルームイベントコールバック

| API | 説明 |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | ルームが破棄された時のコールバック。|
| [onRoomInfoChange](#onroominfochange) | ライブストリーミングルーム情報変更のコールバック。|

### キャスターと視聴者の参加/退出のイベントコールバック

| API | 説明 |
|-----|-----|
| [onAnchorEnter](#onanchorenter) | 新しいキャスターの入室通知を受信します。|
| [onAnchorExit](#onanchorexit) | キャスターの退室通知を受信します。|
| [onAudienceEnter](#onaudienceenter) | 視聴者入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | 視聴者退室通知の受信。|

### キャスターと視聴者のマイク接続のイベントコールバック

| API | 説明 |
|-----|-----|
| [onRequestJoinAnchor](#onrequestjoinanchor) | キャスターが視聴者のマイク接続リクエストを受信した時のコールバック。|
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | マイク接続の視聴者がマイク接続からキックアウトされた通知を受信します。|

### キャスター間PKのイベントコールバック

| API | 説明 |
|-----|-----|
| [onRequestRoomPK](#onrequestroompk) | ルーム間PKのリクエストの通知を受信。|
| [onQuitRoomPK](#onquitroompk) | ルーム間PK中止の通知を受信します。|

### メッセージイベントのコールバック

| API | 説明 |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | テキストメッセージの受信。|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージの受信。|

## SDK基本関数

[](id:sharedInstance)
### sharedInstance

[TRTCLiveRoom](https://cloud.tencent.com/document/product/647/43182) シングルトンオブジェクトを取得します。
```java
 public static synchronized TRTCLiveRoom sharedInstance(Context context);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| context | Context | Androidコンテキスト。内部ではApplicationContextに変換してシステムAPIの呼び出しに使用します |

   

### destroySharedInstance

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061) シングルトンオブジェクトを破棄します。
>?インスタンスの破棄後は、外部にキャッシュされたTRTCLiveRoomインスタンスの再使用ができません。改めて [sharedInstance](#sharedInstance) をコールして、インスタンスを新規取得する必要があります。

```java
public static void destroySharedInstance();
```

### setDelegate

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061) イベントコールバック。 TRTCLiveRoomDelegateを介して[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061)の各種ステータス通知を受け取ることができます。
```java
public abstract void setDelegate(TRTCLiveRoomDelegate delegate);
```

>?setDelegateはTRTCLiveRoomのプロキシコールバックです。   

### setDelegateHandler

イベントコールバックが配置されているスレッドを設定します。
```java
public abstract void setDelegateHandler(Handler handler);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| handler | Handler | TRTCLiveRoomの中の各種状態の通知のコールバックは、このhandlerによって通知されます。setDelegateと混用しないでください。 |

   

### login

ログイン。

<dx-codeblock>
::: java java
public abstract void login(int sdkAppId,
 String userId, String userSig,
 TRTCLiveRoomDef.TRTCLiveRoomConfig config, 
 TRTCLiveRoomCallback.ActionCallback callback);
:::
</dx-codeblock>

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| sdkAppId | int |  TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報の中でSDKAppIDを確認できます。 |
| user     | String | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig | String | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 [UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| config | TRTCLiveRoomConfig | グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。<ul style="margin:0;"><li>useCDNFirst属性：視聴者の視聴方式の設定に使用します。trueは、普通の視聴者のCDN経由での視聴を表し、費用は安価ですがディレーは高めです。falseは、普通の視聴者の低遅延による視聴を表し、費用はCDNとマイク接続の間ですが、ディレーを1s以内に抑えることができます。</li><li>CDNPlayDomain属性：useCDNFirstの設定をtrueにすると有効になり、CDN経由で視聴する再生ドメイン名の指定に利用します。CSSコンソール>【<a href="https://console.cloud.tencent.com/live/domainmanage">ドメイン名管理</a>】の画面からログインし、設定を行います。</li></ul> |
| callback | ActionCallback | ログインのコールバック。成功時にcodeは0になります。 |

   

### logout

ログアウト。
```java
public abstract void logout(TRTCLiveRoomCallback.ActionCallback callback);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | ActionCallback | ログアウトのコールバック。成功時にcodeは0になります。 |

   

### setSelfProfile

個人情報の修正。
```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味       |
|-----|-----|-----|
| userName  | String         | ニックネーム。                              |
| avatarURL | String         | プロフィール画像のアドレス。                          |
| callback | ActionCallback | 個人情報設定のコールバック。成功時にcodeは0になります。                                  |

   


## ルーム関連インターフェース関数
### createRoom

ルームの新規作成（キャスターが呼び出し）。
```java
public abstract void createRoom(int roomId, TRTCLiveRoomDef.TRTCCreateRoomParam roomParam, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| roomId | int | ルームIDは、ご自身でアサインし、一元管理する必要があります。複数のroomID を、1つのライブストリーミングルームリストにまとめることができます。Tencent Cloudではライブストリーミングルームリストの管理サービスを一時的に行いませんので、ご自身でライブストリーミングルームリストを管理してください。 |
| roomParam | TRTCCreateRoomParam | ルーム情報は、ルーム名、マイク情報、カバー情報などのルーム説明の情報に使用します。ルームリストおよびルーム情報をご自身のサーバーで管理する場合は、このパラメータは無視してもかまいません。 |
| callback | ActionCallback | ルームの作成結果のコールバック。成功時にcodeは0になります。 |

キャスターが配信を開始する際の通常の呼び出しプロセスは次のとおりです。 
1. 【キャスター】 `startCameraPreview()`を呼び出し、カメラのプレビューを起動します。この時美顔パラメータを調整できます。 
2. 【キャスター】`createRoom()`を呼び出し、ライブストリーミングルームを作成します。ルーム作成の成功の有無がActionCallbackでキャスターに通知されます。
3. 【キャスター】`starPublish()`を呼び出し、プッシュを開始します。

   

### destroyRoom

ルームの破棄（キャスターが呼び出し）。キャスターは、ルーム作成後、この関数を呼び出してルームを破棄します。
```java
public abstract void destroyRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時にcodeは0になります。 |


### enterRoom

入室（視聴者が呼び出し）。
```java
public abstract void enterRoom(int roomId, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味       |
|-----|-----|-----|
| roomId   | int            | ルームID。                            |
| callback | ActionCallback | 入室結果のコールバック。成功時にcodeは0になります。 |


視聴者のライブストリーミング視聴の通常の呼び出しフローは以下のとおりです。 
1.【視聴者】サーバーから取得する最新のライブストリーミングルームリストには、多くのライブストリーミングルームのroomIdおよびルーム情報が含まれる場合があります。
2. 【視聴者】視聴者は1つのライブストリーミングルームを選択し、`enterRoom()`を呼び出して、このルームに参加します。
3. 【視聴者】`startPlay(userId)`を呼び出し、キャスターのuserIdを渡して再生を開始します。
 - ライブストリーミングルームリストにキャスターのuserId情報がすでに含まれている場合、視聴者は、`startPlay(userId)`を直接呼び出せば、再生を開始できます。
 - ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者はルーム参加後に `TRTCLiveRoomDelegate`の中の `onAnchorEnter(userID)`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID 情報が含まれていますので、`startPlay(userID)`再び呼び出しせば、再生できます。 

   

### exitRoom

ルームを退出します。
```java
public abstract void exitRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | ActionCallback | 退室結果のコールバック。成功時にcodeは0になります。 |

   

### getRoomInfos

ルームリストの詳細情報を取得します。ルーム情報は、キャスターが`createRoom()`作成時にroomInfoによって設定します。
>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```java
public abstract void getRoomInfos(List<Integer> roomIdList, TRTCLiveRoomCallback.RoomInfoCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味         |
|-----|-----|-----|
| roomIdList | List&lt;Integer&gt; | ルームナンバーリスト。       |
| callback   | RoomInfoCallback    | ルーム詳細情報のコールバック。 |


### getAnchorList

ルーム内の全キャスターのリストを取得します。`enterRoom()`成功後に呼び出しが有効となります。
```java
public abstract void getAnchorList(TRTCLiveRoomCallback.UserListCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | UserListCallback | ユーザーの詳細情報のコールバック。 |

   

### getAudienceList

ルーム内の全視聴者の情報を取得します。`enterRoom()`成功後に呼び出しが有効となります。
```java
public abstract void getAudienceList(TRTCLiveRoomCallback.UserListCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | UserListCallback | ユーザーの詳細情報のコールバック。 |

   

## プッシュプルストリームに関連するインターフェース関数
### startCameraPreview

ローカルビデオのプレビュー画面を立ち上げます。
```java
public abstract void startCameraPreview(boolean isFront, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| isFront | boolean | true：フロントカメラ；false：リアカメラ。 |
| view | TXCloudVideoView | ビデオ画像をロードするウィジェット。 |
| callback | ActionCallback | 操作コールバック。|

   

### stopCameraPreview

ローカルのビデオキャプチャおよびプレビューを停止します。
```java
public abstract void stopCameraPreview();
```

   

### startPublish

ライブストリーミング（プッシュ）を開始します。次のシーンに適用します。
- キャスターの配信開始時のコール
- 視聴者のマイク接続開始時の呼び出し


```java
public abstract void startPublish(String streamId, TRTCLiveRoomCallback.ActionCallback callback);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| streamId | String | ライブCDNのstreamIdをバインドするために利用します。視聴者にライブCDN経由で視聴させたい場合は、現在のキャスターのライブストリーミングstreamIdを指定する必要があります。|
| callback | ActionCallback | 操作コールバック。|


### stopPublish

ライブストリーミング（プッシュ）を停止します。次のシーンに適用します。
- キャスターがライブストリーミングを終了する時の呼び出し
- 視聴者がマイク接続を終了する時の呼び出し


```java
public abstract void stopPublish(TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | ActionCallback | 操作コールバック。|



   

### startPlay

リモートのビデオ画面を再生します。普通の視聴とマイク接続のシーンで呼び出すことができます。
```java
public abstract void startPlay(String userId, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | 視聴が必要なユーザーid。 |
| view | TXCloudVideoView | ビデオ画像をロードするviewウィジェット。 |
| callback | ActionCallback | 操作コールバック。|

**普通の視聴シーン**
- ライブストリーミングルームリストにキャスターのuserId情報がすでに含まれている場合、視聴者は、`enterRoom()`成功後に`startPlay(userId)`を直接呼び出せばキャスターの画面を再生できます。
- ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者はルーム参加後に `TRTCLiveRoomDelegate`の中の`onAnchorEnter(userId)`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID情報が含まれていますので、`startPlay(userId)`を再び呼び出せば、キャスターの画面を再生できます。

**ライブストリーミングのマイク接続シーン**
マイク接続の始動後、キャスターは`TRTCLiveRoomDelegate`から`onAnchorEnter(userId)`のコールバックを受信します。この時コールバックの中のuserIDを使用してstartPlay(userID)を呼び出せば、マイク接続の画面を再生できます。

   

### stopPlay

リモートのビデオ画面のレンダリングを停止します。`onAnchorExit()`のコールバック時、このインターフェースを呼び出す必要があります。
```java
public abstract void stopPlay(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | 相手側のユーザー情報。|
| callback | ActionCallback | 操作コールバック。|


## キャスターと視聴者のマイク接続
### requestJoinAnchor

視聴者がマイク接続をリクエストします。
```java
public abstract void requestJoinAnchor(String reason, int timeout, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| reason | String | マイク接続の理由。 |
| timeout | int | タイムアウトの時間。 |
| callback | ActionCallback | キャスターの応答のコールバック。 |


キャスターと視聴者のマイク接続フローは次のとおりです。
1. 【視聴者】`requestJoinAnchor()`を呼び出し、キャスターにマイク接続リクエストを送信します。
2. 【キャスター】 `TRTCLiveRoomDelegate`の`onRequestJoinAnchor()`のコールバック通知を受信します。
3. 【キャスター】`responseJoinAnchor()`を呼び出して、視聴者からのマイク接続リクエストを受け入れるか決定します。
4. 【視聴者】responseCallbackのコールバック通知を受信します。この通知にキャスターの処理結果が含まれています。
5. 【視聴者】リクエストが同意されると、`startCameraPreview()`が呼び出され、ローカルカメラが起動します。
6. 【視聴者】その後`startPublish()`を呼び出し、正式にプッシュストリームの状態に入ります。
7. 【キャスター】一度視聴者がマイク接続に入ると、キャスターは、`TRTCLiveRoomDelegate`の `onAnchorEnter()`の通知を受信します。
8. 【キャスター】キャスターが `startPlay()`を呼び出すと、マイク接続の視聴者のビデオ画面を見ることができるようになります。
9. 【視聴者】ライブストリーミングルームの中で他の視聴者がすでにキャスターとマイク接続を行っている場合、新しく参加したマイク接続の視聴者は`onAnchorEnter()`の通知を受け取ります。この時に`startPlay()`を呼び出せば他のマイク接続者のビデオ画面を再生することができます。

   

### responseJoinAnchor

キャスターがマイク接続のリクエストを処理します。キャスターは、`TRTCLiveRoomDelegate`の `onRequestJoinAnchor()`のコールバックを受け取った後、このインターフェースを呼び出して、視聴者のマイク接続リクエストを処理する必要があります。
```java
public abstract void responseJoinAnchor(String userId, boolean agree, String reason);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | 視聴者ID。 |
| agree | boolean | true：同意；false：拒否。 |
| reason | String | マイク接続に同意/拒否した理由の説明。 |


### kickoutJoinAnchor

キャスターがマイク接続の視聴者をキックアウトします。キャスターがこのインターフェースを呼び出し、マイク接続の視聴者をキックアウトすると、キックアウトされたマイク接続の視聴者は、`TRTCLiveRoomDelegate`の`onKickoutJoinAnchor()`のコールバック通知を受信します。

```java
public abstract void kickoutJoinAnchor(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | マイク接続の視聴者ID。 |
| callback | ActionCallback | 操作コールバック。|



## キャスターのルーム間PK
### requestRoomPK

キャスターがルーム間PKをリクエストします。
```java
public abstract void requestRoomPK(int roomId, String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| roomId | int | 招待された側のルームID。 |
| userId | String | 招待された側のキャスターID。 |
| callback | ActionCallback | ルーム間PKのリクエスト結果のコールバック。 |

キャスターとキャスターの間でルーム間PKを行うことができます。ライブストリーミング中の2名のキャスターAとBのルーム間PKのフローは次のとおりです。
1. 【キャスター A】 `requestRoomPK()`を呼び出してキャスターBに向けてマイク接続リクエストを送信します。
2. 【キャスター B】`TRTCLiveRoomDelegate`の`onRequestRoomPK()`のコールバック通知を受信します。
3. 【キャスター B】`responseRoomPK()`を呼び出して、キャスター AのPKのリクエストを受け入れるかどうか決定します。
4. 【キャスターB】キャスターAのリクエストを受け入れる場合は、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出してキャスターAのビデオ画面を表示させます。
5. 【キャスター A】`responseCallback`のコールバック通知を受信します。この通知にはキャスター B の処理結果が含まれます。
6. 【キャスターA】リクエストが同意された場合は、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出し、キャスターBのビデオ画面を表示します。

   

### responseRoomPK

キャスターがルーム間PKのリクエストに応答します。キャスターが応答した後、相手側キャスターは `requestRoomPK`で渡された`responseCallback`のコールバックを受信します。
```java
public abstract void responseRoomPK(String userId, boolean agree, String reason);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | PKをリクエストしたキャスターID。 |
| agree | boolean | true：同意；false：拒否。 |
| reason | String | PKを同意/拒否した理由の説明。 |


### quitRoomPK

ルーム間PKから退出します。PK中のいずれかのキャスターがルーム間PKの状態から退出すると、もう一方のキャスターは`TRTCLiveRoomDelegate`の`onQuitRoomPk()`のコールバック通知を受信します。
```java
public abstract void quitRoomPK(TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | ActionCallback | 操作コールバック。|


## オーディオビデオ制御に関連するインターフェース関数
### switchCamera

フロント/リアカメラを切り替えます。
```java
public abstract void switchCamera();
```

   

### setMirror

ミラー表示のオン/オフを設定します。
```java
public abstract void setMirror(boolean isMirror);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| isMirror | boolean | ミラーオン/オフ。 |

   

### muteLocalAudio

ローカルオーディオをミュートにします。
```java
public abstract void muteLocalAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| mute | boolean | true：ミュート起動、false：ミュート停止。|

   

### muteRemoteAudio

リモートオーディオをミュートにします。
```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | リモートユーザーID。 |
| mute | boolean | true：ミュート起動、false：ミュート停止。|

   

### muteAllRemoteAudio

すべてのリモート側のオーディオをミュートにします。
```java
public abstract void muteAllRemoteAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| mute | boolean | true：ミュート起動、false：ミュート停止。|

   

## BGMサウンドエフェクト関連インターフェース関数
### getAudioEffectManager

BGMサウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。
```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## 美顔フィルタに関するインターフェース関数
### getBeautyManager

美顔管理オブジェクト [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得します。
```java
public abstract TXBeautyManager getBeautyManager();
```

美顔管理では、次の機能を使用できます。
- 「美顔のスタイル」、「美白」、「肌色補正（血色・つや感）」、「デカ眼」、「顔痩せ」、「V顔」、「下あご」、「面長補正」、「小鼻」、「キラキラ目」、「白い歯」、「目の弛み除去」、「シワ除去」、「ほうれい線除去」などの美容効果を設定します。
- 「髪の生え際」、「眼と眼の距離」、「眼の角度」、「唇の形」、「鼻翼」、「鼻の位置」、「唇の厚さ」、「顔の形」を調整します。
- 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
- メイクアップを追加します。
- ジェスチャー認識を行います。


## メッセージ送信関連インターフェース関数
### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットに使用します。
```java
public abstract void sendRoomTextMsg(String message, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
|-----|-----|-----|
| message | String | テキストメッセージ。 |
| callback | ActionCallback | 送信結果のコールバック。|

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。
```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| cmd      | String         | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message | String | テキストメッセージ。 |
| callback | ActionCallback | 送信結果のコールバック。|

   

## デバックに関するインターフェース関数
### showVideoDebugLog

インターフェースの中にdebug情報を表示するかどうか。
```java
public abstract void showVideoDebugLog(boolean isShow);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| isShow | boolean | Debug情報表示のオン/オフ。 |

   

## TRTCLiveRoomDelegateイベントのコールバック

## 一般的なイベントコールバック
### onError

エラーのコールバック。
>?SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```java
void onError(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code   | int    | エラーコード。   |
| message | String | エラー情報。 |


### onWarning

警告のコールバック。
```java
void onWarning(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code | int | エラーコード。 |
| message | String | 警告メッセージ。 |

   

### onDebugLog

Logコールバック。
```java
void onDebugLog(String message);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| message | String | ログ情報。 |

   


## ルームイベントのコールバック
### onRoomDestroy

ルームが破棄された時のコールバック。キャスターが退室する時、ルーム内の全ユーザーがこの通知を受信します。
```java
void onRoomDestroy(String roomId);
```

パラメータは下表に示すとおりです。

|パラメータ   | タイプ   | 意味      |
|-----|-----|-----|
| roomId | String | ルームID。 |



   

### onRoomInfoChange

ライブストリーミングルーム情報変更のコールバック。ライブストリーミングのマイク接続やPKで、ルーム状態の変化を通知するシーンに多用されます。
```java
void onRoomInfoChange(TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| roomInfo | TRTCLiveRoomInfo | ルーム情報。 |

   


## キャスターと視聴者の参加/退出のイベントコールバック
### onAnchorEnter

新しいキャスターの入室の通知を受信します。マイク接続の視聴者とルーム間PKのキャスターが入室すると、視聴者は、新しいキャスターが入室したというイベントを受信します。`TRTCLiveRoom`の `startPlay()`を呼び出して、そのキャスターのビデオ画面を表示することができます。
```java
void onAnchorEnter(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | 新しくルームに参加したキャスターのID。 |


### onAnchorExit

キャスターの退室の通知を受信します。ルーム内のキャスター（およびマイク接続中の視聴者）が、新しいキャスターの退室のイベントを受信します。`TRTCLiveRoom`の`stopPlay()`を呼び出して、そのキャスターのビデオ画面を閉じることができます。
```java
void onAnchorExit(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | ルームを退出したユーザーID。 |


### onAudienceEnter

視聴者入室通知の受信。
```java
void onAudienceEnter(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | 入室した視聴者の情報。 |

   

### onAudienceExit

視聴者退室通知の受信。
```java
void onAudienceExit(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | 退室した視聴者の情報。 |

   


## キャスターと視聴者のマイク接続のイベントコールバック
### onRequestJoinAnchor

キャスターが視聴者のマイク接続リクエストを受信した時のコールバック。
```java
void onRequestJoinAnchor(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, String reason, int timeOut);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | マイク接続をリクエストした視聴者の情報。|
| reason | String | マイク接続の理由の説明。|
| timeout | int | リクエスト処理のタイムアウトの時間。上の階層がこの時間をオーバーしても処理しない場合、このリクエストは自動的に破棄されます。 |

   

### onKickoutJoinAnchor

マイク接続の視聴者がマイク接続からキックアウトされた通知を受信します。マイク接続の視聴者は、キャスターからマイク接続キックアウトのメッセージを受信した場合、`TRTCLiveRoom`の`stopPublish()` を呼び出してマイク接続から退出する必要があります。
```java
void onKickoutJoinAnchor();
```



## キャスター間PKのイベントコールバック
### onRequestRoomPK

ルーム間PKのリクエストの通知を受信します。キャスターは、他のルームのキャスターからPKのリクエストを受け取り、PKに同意する場合、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出して招待側キャスターのストリームを再生する必要があります。
```java
void onRequestRoomPK(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, int timeout);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | ルーム間マイク接続を始動したキャスターの情報。|
| timeout | int | リクエスト処理のタイムアウトの時間。 |


### onQuitRoomPK

ルーム間PK中止の通知を受信します。
```java
void onQuitRoomPK();
```

   


## メッセージイベントのコールバック
### onRecvRoomTextMsg

テキストメッセージの受信。
```java
void onRecvRoomTextMsg(String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| message | String | テキストメッセージ。|
| userInfo | TRTCLiveUserInfo | 送信者のユーザー情報。|

   

### onRecvRoomCustomMsg

カスタムメッセージの受信。
```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| command | String | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。|
| message | String | テキストメッセージ。|
| userInfo | TRTCLiveUserInfo | 送信者のユーザー情報。 |


[](id:TRTCAudioEffectManager)
## TRTCAudioEffectManager
### playBGM

BGMを再生します。
```java
void playBGM(String url, int loopTimes, int bgmVol, int micVol, TRTCCloud.BGMNotify notify);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| url | String | BGMファイルパス。 |
| loopTimes | int | ループ回数 |
| bgmVol | int | BGM音量 |
| micVol | int | キャプチャ音量 |
| notify | TRTCCloud.BGMNotify | 再生の通知 |

   

### stopBGM

BGMの再生を停止します。
```java
void stopBGM();
```

   

### pauseBGM

BGMの再生を一時停止します。
```java
void pauseBGM();
```

   

### resumeBGM

BGMの再生を続けます
```java
void resumeBGM();
```

   

### setBGMVolume

BGMの音量の大きさを設定します。BGMをミキシングして再生する時に使用し、BGMの音量の大きさの制御に利用します。
```java
void setBGMVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| volume | int | 音量の大きさ。100は通常の音量を表し、値の範囲は0 - 100です。デフォルト値は100です。 |

   

### setBGMPosition

BGM再生の進度を設定します。
```java
int setBGMPosition(int position);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| position | int | BGM再生の進度。単位はミリ秒（ms）。 |

__戻る__

0：成功。

   

### setMicVolume

マイク音量の大きさを設定します。BGMをミキシングして再生する時に使用し、マイク音量の大きさの制御に利用します。
```java
void setMicVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| volume | Int | 音量の大きさ。値の範囲は0 - 100、デフォルト値は100です。 |

   

### setReverbType

リバーブ効果を設定します。
```java
void setReverbType(int reverbType);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| reverbType | int | リバーブタイプ。詳細は、`TRTCCloudDef`の中の[TRTC_REVERB_TYPE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a60ecba31f49f70780e623d24bcfa1a7d)の定義をご参照ください。 |

   

### setVoiceChangerType

ボイスチェンジのタイプを設定します。
```java
void setVoiceChangerType(int type);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| type | int | リバーブタイプ。詳細は、`TRTCCloudDef`の中の[TRTC_VOICE_CHANGER_TYPE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a899e72b3e4a16288e6c2edfd779e3beb)の定義をご参照ください。 |

   

### playAudioEffect

サウンドエフェクトを再生します。サウンドエフェクトごとに具体的なIDを指定する必要があります。このIDでサウンドエフェクトのスタート、ストップ、音量等を設定することができます。aac、mp3、m4a形式をサポートしています。
```java
void playAudioEffect(int effectId, String path, int count, boolean publish, int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| effectId | int | サウンドエフェクト ID。 |
| path | String | サウンドエフェクトパス。 |
| count | int | ループ回数。 |
| publish | boolean | プッシュかどうか / trueは視聴者に対するプッシュ、 falseはローカルプレビューです。 |
| volume | int | 音量の大きさ。数値の範囲は0 - 100、デフォルト値は100です。 |

   

### pauseAudioEffect

サウンドエフェクトの再生を一時停止します。
```java
void pauseAudioEffect(int effectId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| effectId | int | サウンドエフェクト ID。 |

   

### resumeAudioEffect

サウンドエフェクトの再生を再開します。
```java
void resumeAudioEffect(int effectId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| effectId | int | サウンドエフェクト ID。 |

   

### stopAudioEffect

サウンドエフェクトの再生を停止します。
```java
void stopAudioEffect(int effectId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| effectId | int | サウンドエフェクト ID。 |

   

### stopAllAudioEffects

すべてのサウンドエフェクトの再生を停止します。
```java
void stopAllAudioEffects();
```

   

### setAudioEffectVolume

サウンドエフェクトの音量を設定します。
```java
void setAudioEffectVolume(int effectId, int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| effectId | int | サウンドエフェクト ID。 |
| volume | int | 音量の大きさ。数値の範囲は0 - 100、デフォルト値は100です。 |

   

### setAllAudioEffectsVolume

全てのサウンドエフェクトの音量を設定します。
```java
void setAllAudioEffectsVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| volume | int | 音量の大きさ。数値の範囲は0 - 100、デフォルト値は100です。 |

   
