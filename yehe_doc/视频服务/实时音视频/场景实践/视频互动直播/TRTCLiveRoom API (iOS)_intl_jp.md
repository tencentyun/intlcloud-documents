TRTCLiveRoomは、Tencent CloudのTRTCおよびIM サービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- キャスターが新しいライブルームを作成して放送を開始し、視聴者がライブルームに参加して視聴します。
- キャスターと視聴者がビデオでマイク接続によるコラボライブを行います。
- 2つの異なるルームの間でキャスター同士のPK（クロスルーム対戦）を行います。
- 各種のテキストメッセージやカスタマイズメッセージの発信をサポートし、情報を弾幕、「いいね」、ギフトに使えられるようにカスタマイズします。

TRTCLiveRoom はオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実現プロセスは、 [オーディオ・ビデオライブストリーミング（iOS）](https://intl.cloud.tencent.com/document/product/647/36060)をご参照ください。

- TRTC SDK： [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) をレイテンシーのライブストリーミングコンポーネントとして利用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用して、ライブストリーミングのチャットルーム機能を実現します。同時に、IMのメッセージでキャスター間のマイク接続のフローをつなげます。



<h2 id="TRTCLiveRoom">TRTCLiveRoom API 概要</h2>

### SDK 基本関数

| API                               | 説明           |
| --------------------------------- | -------------- |
| [delegate](#delegate)             | イベントコールバックを設定します。 |
| [login](#login)                   | ログイン。         |
| [logout](#logout)                 | ログアウト。         |
| [setSelfProfile](#setselfprofile) |  個人情報の修正。 |

### ルーム関連インターフェース関数

| API                                 | 説明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)           | ルームの新規作成（キャスターがコール）。ルームが存在していない場合は、システムが新しいルームを自動作成。｜
| [destroyRoom](#destroyroom)         | ルームの廃棄（キャスターがコール）。                                       |
| [enterRoom](#enterroom)             | 入室（視聴者がコール）。                                       |
| [exitRoom](#exitroom)               | 退室（視聴者がコール）。                                       |
| [getRoomInfos](#getroominfos)       | ルームリストの詳細情報を取得します。                                     |
| [getAnchorList](#getanchorlist)     | ルーム内の全キャスターのリストを取得します。enterRoom() 成功後に呼び出しが有効となります。     |
| [getAudienceList](#getaudiencelist) | ルーム内の全視聴者の情報を取得します。enterRoom() 成功後に呼び出しが有効となります。     |

### プッシュプルストリームに関連するインターフェース関数

| API                                       | 説明                                               |
| ----------------------------------------- | -------------------------------------------------- |
| [startCameraPreview](#startcamerapreview) | ローカルビデオのプレビュー画面を立ち上げます。                           |
| [stopCameraPreview](#stopcamerapreview)   | ローカルのビデオキャプチャおよびプレビューを停止します。                           |
| [startPublish](#startpublish)             | ライブストリーミング（プッシュ）を開始します。                                 |
| [stopPublish](#stoppublish)               | ライブストリーミング（プッシュ）を停止します。                                 |
| [startPlay](#startplay)                   | リモートのビデオ画面を再生します。普通の視聴とマイク接続のシーンで呼び出すことができます。 |
| [stopPlay](#stopplay)                     | リモートのビデオ画面のレンダリングを停止します。                             |

### キャスターと視聴者のマイク接続

| API                                       | 説明               |
| ----------------------------------------- | ------------------ |
| [requestJoinAnchor](#requestjoinanchor)   | 視聴者がマイク接続をリクエストします。     |
| [responseJoinAnchor](#responsejoinanchor) | キャスターがマイク接続のリクエストを処理します。 |
| [kickoutJoinAnchor](#kickoutjoinanchor)   | キャスターがマイク接続視聴者を追放します。 |

### キャスターのルーム間PK

| API                               | 説明                   |
| --------------------------------- | ---------------------- |
| [requestRoomPK](#requestroompk)   | キャスターがルーム間PKをリクエストします。      |
| [responseRoomPK](#responseroompk) | キャスターがルーム間PKのリクエストに応答します。 |
| [quitRoomPK](#quitroompk)         | ルーム間PKから退出します。          |

### 音声ビデオ制御に関連するインターフェース関数

| API                                       | 説明               |
| ----------------------------------------- | ------------------ |
| [switchCamera](#switchcamera)             | 前後カメラを切り替えます。   |
| [setMirror](#setmirror)                   | ミラー表示のオン／オフを設定します。 |
| [muteLocalAudio](#mutelocalaudio)         | ローカルオーディオをミュートにします。     |
| [muteRemoteAudio](#muteremoteaudio)       | リモートの音声をミュートにします。     |
| [muteAllRemoteAudio](#muteallremoteaudio) | 全てのリモート側の音声をミュートにします。 |

### バックグラウンドミュージック・サウンドエフェクト関連インターフェース関数

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | バックグラウンドミュージック・サウンドエフェクト管理オブジェクト[TXAudioEffectManager](#trtcaudioeffectmanagerapi)の取得。 |

### 美顔フィルタに関するインターフェース関数

| API                                   | 説明                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#interfaceTXBeautyManager)を取得します。 |

### メッセージ送信関連インターフェース関数

| API                                     | 説明                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージの放送には、通常弾幕によるチャットを使用します。｜
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを発信します。                     |

### デバックに関するインターフェース関数

| API                                     | 説明                        |
| --------------------------------------- | --------------------------- |
| [showVideoDebugLog](#showvideodebuglog) | debug情報をインターフェースに表示するかどうか。 |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API 概要</h2>

### 一般的なイベントコールバック

| API                       | 説明       |
| ------------------------- | ---------- |
| [onError](#onerror)       | エラーのコールバック。 |
| [onWarning](#onwarning)   | 警告のコールバック。 |
| [onDebugLog](#ondebuglog) | Log コールバック。 |

### ルームイベントのコールバック

| API                                   | 説明                   |
| ------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy) | ルームが廃棄された時のコールバック。|
| [onRoomInfoChange](#onroominfochange) | ライブルーム情報変更のコールバック。 |

### キャスターと視聴者の参加／退出のイベントコールバック

| API                                 | 説明                 |
| ----------------------------------- | -------------------- |
| [onAnchorEnter](#onanchorenter)     | 新しいキャスターのルーム参加の通知を受信します。 |
| [onAnchorExit](#onanchorexit)       | キャスターのルーム退出の通知を受信します。   |
| [onAudienceEnter](#onaudienceenter) |視聴者入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | 視聴者退室通知の受信。|

### キャスターと視聴者のマイク接続のイベントコールバック

| API                                         | 説明                           |
| ------------------------------------------- | ------------------------------ |
| [onRequestJoinAnchor](#onrequestjoinanchor) | キャスターが視聴者のマイク接続リクエストを受信した時のコールバック。 |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | マイク接続の視聴者がマイク接続から追放された通知を受信します。 |

### キャスター間PKのイベントコールバック

| API                                 | 説明                   |
| ----------------------------------- | ---------------------- |
| [onRequestRoomPK](#onrequestroompk) | ルーム間PKのリクエストの通知を受信。 |
| [onQuitRoomPK](#onquitroompk)       | ルーム間PK中止の通知を受信します。 |

### メッセージのイベントコールバック

| API                                         | 説明             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | テキストメッセージの受信。|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタマイズメッセージの受信。|



## SDK 基本関数

### delegate

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060) イベントコールバック。 TRTCLiveRoomDelegate を介して[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060)の各種ステータス通知を受け取ることができます。

```objc
@property(nonatomic, weak)id<TRTCLiveRoomDelegate> delegate;
```

>?delegateは、TRTCLiveRoomのプロキシコールバックです。


### login

ログイン。

```objc
/// コンポーネントシステムにログイン
/// - Parameters:
///   - sdkAppID: TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報でSDKAppIDを表示できます。
///   - userID: 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。
///   - userSig:  Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法 ](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
///   - config: グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。isAttachedTUIKit プロジェクトにTUIKitを導入し使用しているか。
///   - callback: ログインのコールバック。成功時に code は0になります。
/// - Note:
///   - userSigの設定は 7日を推奨します。usersign 期限切れによるIMのメッセージ送受信の失敗、TRTCのマイク接続の失敗等を効果的に回避できます。
- (void)loginWithSdkAppID:(int)sdkAppID
                  userID:(NSString *)userID
                 userSig:(NSString *)userSig
                  config:(TRTCLiveRoomConfig *)config
                callback:(Callback _Nullable)callback
NS_SWIFT_NAME(login(sdkAppID:userID:userSig:config:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                                                         |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| sdkAppID | Int                                       | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報でSDKAppIDを表示できます。 |
| userID   | String                                    | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。 |
| userSig  | String                                    |  Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法 ](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| config   | TRTCLiveRoomConfig                        | グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。<ul style="margin:0;"><li>useCDNFirst 属性：視聴者の視聴方式の設定に使用します。trueは、普通の視聴者のCDN経由での視聴を表し、費用は安価ですがディレーは高めです。falseは、普通の視聴者の低遅延による視聴を表し、費用は CDN とマイク接続の間ですが、ディレーを1s以内に抑えることができます。</li><li>CDNPlayDomain 属性： useCDNFirstの設定がtrueの時に有効となり、CDNでの視聴の再生ドメイン名の指定に使用します。ライブストリーミングコンソール >【<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>】の画面からログインし、設定を行います。</li></ul> |
| callback | (_ code: Int, _ message: String?) -> Void | ログインのコールバック。成功時に code は0になります。                                  |


### logout

ログアウト。

```objc
// ログイン状態から退出
/// - Parameter callback:  ログアウトのコールバック。成功時のcodeは0です。
- (void)logout:(Callback _Nullable)callback
NS_SWIFT_NAME(logout(_:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                        |
| -------- | ----------------------------------------- | --------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | ログアウトのコールバック。成功時に code は0になります。 |


### setSelfProfile

個人情報の修正。

```objc
/// ユーザー情報を設定します。設定したユーザー情報は、Tencent CloudのIMクラウドサーバーに保存されます。
/// - Parameters:
///   - name: ユーザーのニックネーム
///   - avatarURL: ユーザーのプロファイル写真URL
///   - callback: 個人情報設定のコールバック。成功時のcodeは0です。
- (void)setSelfProfileWithName:(NSString *)name
                     avatarURL:(NSString * _Nullable)avatarURL
                      callback:(Callback _Nullable)callback
NS_SWIFT_NAME(setSelfProfile(name:avatarURL:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                                      | 意味                                |
| --------- | ----------------------------------------- | ----------------------------------- |
| name      | String                                    | ニックネーム。                              |
| avatarURL | String                                    | プロファイル写真URL。                          |
| callback  | (_ code: Int, _ message: String?) -> Void | 個人情報設定のコールバック。成功時のcodeは0です。 |


## ルーム関連インターフェース関数

### createRoom

ルームの新規作成（キャスターがコール）。

```objc
/// ルームを作成（キャスターがコール）します。ルームが存在しない場合、システムが新しいルームを1つ自動作成します。
/// キャスターが放送を開始する時の通常の呼び出しフローは以下のとおりです。
/// 1.【キャスター】startCameraPreview()を呼び出し、カメラのプレビューを起動します。この時美顔パラメータを調整できます。
/// 2.【キャスター】 createRoom()を呼び出し、ライブルームを作成します。ルーム作成の成功の有無が callbackでキャスターに通知されます。
/// 3.【キャスター】startPublish() を呼び出し、プッシュを開始します。
/// - Parameters:
///   - roomID: ルームIDは、ご自身でアサインし、統一管理する必要があります。複数の roomID を、一つのライブルームリストにまとめることができます。Tencent Cloudではライブルームリストの管理サービスを一時的に行いませんので、ご自身でライブルームリストを管理してください。
///   - roomParam: TRTCCreateRoomParam | ルーム情報は、ルームの説明情報として利用します（例：ルーム名、カバー情報など）。ルームリストとルーム情報をご自分で管理する場合は、このパラメータは無視してかまいません。
///   - callback:  入室結果のコールバック。成功時に code は0になります。
/// - Note:
///   - キャスターがライブストリーミングを開始する時のコールでは、自分が作成したことがあるルームを再び作成することができます。
- (void)createRoomWithRoomID:(UInt32)roomID
                   roomParam:(TRTCCreateRoomParam *)roomParam
                    callback:(Callback _Nullable)callback
NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                                      | 意味                                                         |
| --------- | ----------------------------------------- | ------------------------------------------------------------ |
| roomID    | UInt32                                    | ルームIDは、ご自身でアサインし、統一管理する必要があります。複数の roomID を、一つのライブルームリストにまとめることができます。Tencent Cloudではライブルームリストの管理サービスを一時的に行いませんので、ご自身でライブルームリストを管理してください。 |
| roomParam | TRTCCreateRoomParam                       | ルーム情報は、ルームの説明情報として利用します（例：ルーム名、カバー情報など）。ルームリストとルーム情報をご自分で管理する場合は、このパラメータは無視してかまいません。 |
| callback  | (_ code: Int, _ message: String?) -> Void | ルームの新規作成結果のコールバック。成功時に code は0になります。                      |

キャスターが放送開始する通常のコールフローは以下のとおりです。 

1. 【キャスター】 `startCameraPreview()`を呼び出し、カメラのプレビューを起動します。この時美顔パラメータを調整できます。 
2. 【キャスター】`createRoom()`を呼び出し、ライブルームを作成します。ルーム作成の成功の有無が callbackでキャスターに通知されます。
3. 【キャスター】`starPublish()`を呼び出し、プッシュを開始します。

### destroyRoom

ルームの廃棄（キャスターがコール）。キャスターは、ルーム作成後、この関数をコールしてルームを廃棄します。

```objc
/// ルームの廃棄（キャスターがコール）
/// キャスターはルーム作成後、この関数を呼び出してルームを廃棄することができます。
/// - Parameter callback: ルーム廃棄結果のコールバック、成功時にcodeは0になります。
/// - Note:
///   - キャスターは、ルーム作成後、この関数をコールしてルームを廃棄します。
- (void)destroyRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(destroyRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                                  |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | ルーム廃棄結果のコールバック、成功時にcodeは0になります。 |



### enterRoom

入室（視聴者がコール）

```objc
/// 入室（視聴者がコール）
/// 視聴者のライブストリーミング視聴の通常の呼び出しフローは以下のとおりです。
/// 1.【視聴者】サーバーから取得する最新のライブルームリストには、多くのボイスチャットルームの roomId およびルーム情報が含まれます。
/// 2.【視聴者】視聴者は1つのライブルームを選択し、enterRoom()を呼び出して、このルームに参加します。
/// 3.【視聴者】お客様のサーバーが管理するルームリストの中にそれぞれのルームのキャスターのuserIDが含まれていますので、enterRoom() 成功後、直接 startPlay(userID)を呼び出せばキャスターの画面を再生できます。
/// お客様が管理するルームリストにroomidしかなくてもかまいません。視聴者は、enterRoom()成功後すぐに TRTCLiveRoomDelegateからonAnchorEnter(userID)のコールバックを受信します。
/// この時コールバックの中のuserIDを使用して startPlay(userID)を呼び出せば、キャスターの画面を再生できます。
/// - Parameters:
///   - roomID: ルームID。
///   - useCDNFirst: 優先的にCDNを使用して再生するかどうか。
///   - cdnDomain: CDNドメイン名
///   - callback: 入室結果のコールバック。成功時に code は0になります。
/// - Note:
///   - 視聴者がライブルームに参加する時のコール
///   - キャスターがこのインターフェースを呼び出して自分が作成したルームに参加することはできません。createRoomを使用する必要があります。
- (void)enterRoomWithRoomID:(UInt32)roomID
                useCDNFirst:(BOOL)useCDNFirst
                  cdnDomain:(NSString * _Nullable)cdnDomain
                   callback:(Callback)callback
NS_SWIFT_NAME(enterRoom(roomID:useCDNFirst:cdnDomain:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                                  |
| -------- | ----------------------------------------- | ------------------------------------- |
| roomID   | UInt32                                    | ルームID。                            |
| callback | (_ code: Int, _ message: String?) -> Void | 入室結果のコールバック。成功時に code は0になります。|



視聴者のライブストリーミング視聴の通常の呼び出しフローは以下のとおりです。 

1.【視聴者】サーバーから取得する最新のライブルームリストには、多くのボイスチャットルームの roomId およびルーム情報が含まれます。
2. 【視聴者】視聴者は1つのライブルームを選択し、`enterRoom()`を呼び出して、このルームに参加します。
3. 【視聴者】`startPlay(userID)`を呼び出し、キャスターのuserIDを渡して再生を開始します。
 - ライブルームリストにキャスターのuserID 情報がすでに含まれている場合、視聴者は、`startPlay(userID)`を直接呼び出せば、再生を開始できます。
 - ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者はルーム参加後に `TRTCLiveRoomDelegate`から`onAnchorEnter(userID)`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID 情報が含まれていますので、`startPlay(userID)`を再び呼び出せば、再生できます。 



### exitRoom

ルームを退出する。

```objc
/// 退室（視聴者がコール）
/// - Parameter callback: 退室結果のコールバック。成功時に code は0になります。
/// - Note:
///   - 視聴者がライブルームを退出する時のコール
///   - キャスターはこのインターフェースを呼び出してルームを退出できません。

- (void)exitRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(exitRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                                  |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | 退室結果のコールバック。成功時に code は0になります。 |

### getRoomInfos

ルームリストの詳細情報を取得します。ルーム情報は、キャスターが `createRoom()`作成時に roomInfoで設定します。
>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。

```objc
/// ルームリストの詳細情報を取得します。
/// その中の情報は、キャスターがcreateRoom()作成時に roomInfoで設定します。ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。
/// - Parameter roomIDs: ルームナンバーリスト
/// - Parameter callback: ルーム詳細情報のコールバック
- (void)getRoomInfosWithRoomIDs:(NSArray<NSNumber *> *)roomIDs
                       callback:(RoomInfoCallback _Nullable)callback
NS_SWIFT_NAME(getRoomInfos(roomIDs:callback:));

```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                                         | 意味               |
| -------- | ------------------------------------------------------------ | ------------------ |
| roomIDs  | [UInt32]                                                     | ルームナンバーリスト。       |
| callback | (_ code: Int, _ message: String?, _ roomList: [TRTCLiveRoomInfo]) -> Void | ルーム詳細情報のコールバック。 |



### getAnchorList

ルーム内の全キャスターのリストを取得します。`enterRoom()`成功後に呼び出しが有効となります。

```objc
/// ルーム内の全キャスターのリストを取得します。enterRoom() 成功後に呼び出しが有効となります。
/// - Parameter callback: ユーザーの詳細情報のコールバック
- (void)getAnchorList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAnchorList(callback:));

```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                                         | 意味               |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | ユーザーの詳細情報のコールバック。 |


### getAudienceList

ルーム内の全視聴者の情報を取得します。`enterRoom()`成功後に呼び出しが有効となります。

```objc
/// ルーム内の全視聴者の情報を取得します。enterRoom()成功後に呼び出しが有効となります。
/// - Parameter callback: ユーザーの詳細情報のコールバック
- (void)getAudienceList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAudienceList(callback:));

```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                                         | 意味               |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | ユーザーの詳細情報のコールバック。 |


## プッシュプルストリームに関連するインターフェース関数

### startCameraPreview

ローカルビデオのプレビュー画面を立ち上げます。

```objc
/// ローカルビデオのプレビュー画面を立ち上げます。
/// - Parameters:
///   - frontCamera: true：フロントカメラ；false：リアカメラ。
///   - view: ビデオ画像をロードするウィジェット。
///   - callback: 操作コールバック。
- (void)startCameraPreviewWithFrontCamera:(BOOL)frontCamera
                                     view:(UIView *)view
                                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startCameraPreview(frontCamera:view:callback:));

```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ                                      | 意味                                  |
| ----------- | ----------------------------------------- | ------------------------------------- |
| frontCamera | Bool                                      | true：フロントカメラ；false：リアカメラ。 |
| view        | UIView                                    | ビデオ画像をロードするウィジェット。                  |
| callback    | (_ code: Int, _ message: String?) -> Void | 操作コールバック。                            |


### stopCameraPreview

ローカルのビデオキャプチャおよびプレビューを停止します。

```objc
/// ローカルのビデオキャプチャおよびプレビューを停止します。
- (void)stopCameraPreview;

```


### startPublish

ライブストリーミング（プッシュ）を開始します。次のシーンに適用します。

- キャスターの放送開始時のコール
- 視聴者のマイク接続開始時のコール


```objc
/// ライブストリーミング（プッシュ）を開始します。次の2種類のシーンに適用します。
/// 1. キャスターの放送開始時のコール
/// 2. 視聴者のマイク接続開始時のコール
/// - Parameters:
///   - streamID: ライブストリーミングのCDNのstreamIdをバインドするために利用します。視聴者にCDN 経由でライブストリーミングを視聴させたい場合は、現在のキャスターのライブストリーミング streamIdを指定する必要があります。
///   - callback: 操作コールバック
- (void)startPublishWithStreamID:(NSString *)streamID
                        callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPublish(streamID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                                                         |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| streamID | String                                    | ライブストリーミングのCDNのstreamIdをバインドするために利用します。視聴者にCDN経由でライブストリーミングを視聴させたい場合は、現在のキャスターのライブストリーミング streamIdを指定する必要があります。 |
| callback | (_ code: Int, _ message: String?) -> Void | 操作コールバック。                                                   |


### stopPublish

ライブストリーミング（プッシュ）を停止します。次のシーンに適用します。

- キャスターがライブストリーミングを終了する時のコール。
- 視聴者がマイク接続を終了する時のコール。

```objc
/// ライブストリーミング（プッシュ）を停止します。次の2つのシーンに適用します。
/// 1. キャスターがライブストリーミングを終了する時のコール
/// 2. 視聴者がマイク接続を終了する時のコール
/// - Parameter callback: 操作コールバック。
- (void)stopPublish:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPublish(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味       |
| -------- | ----------------------------------------- | ---------- |
| callback | (_ code: Int, _ message: String?) -> Void | 操作コールバック。 |



### startPlay

リモートのビデオ画面を再生します。普通の視聴とマイク接続のシーンで呼び出すことができます。

```objc
/// リモートのビデオ画面を再生します。普通の視聴とマイク接続のシーンで呼び出すことができます。
/// 【普通の視聴シーン】
/// 1. お客様のサーバーが管理するルームリストの中にそれぞれのルームのキャスターのuserIDが含まれていますので、enterRoom() 成功後、直接 startPlay(userID)を呼び出せばキャスターの画面を再生できます。
/// 2. お客様が管理するルームリストに roomidしかなくてもかまいません。視聴者は enterRoom() 成功後すぐに TRTCLiveRoomDelegate からの onAnchorEnter(userID) のコールバックを受信します。
/// この時コールバックの中のuserIDを使用して startPlay(userID)を呼び出せば、キャスターの画面を再生できます。
/// 【ライブストリーミングのマイク接続シーン】
/// マイク接続の始動後、キャスターは TRTCLiveRoomDelegateから onAnchorEnter(userID)のコールバックを受信します。この時コールバックの中のuserIDを使用して startPlay(userID)を呼び出せば、マイク接続の画面を再生できます。
/// - Parameters:
///   - userID: 視聴が必要なユーザーのID。
///   - view: ビデオ画像をロードする view ウィジェット。
///   - callback: 操作コールバック。
- (void)startPlayWithUserID:(NSString *)userID
                       view:(UIView *)view
                   callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPlay(userID:view:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                       |
| -------- | ----------------------------------------- | -------------------------- |
| userID   | String                                    | 視聴が必要なユーザーのID。        |
| view     | UIView                                    | ビデオ画像をロードするview ウィジェット。 |
| callback | (_ code: Int, _ message: String?) -> Void | 操作コールバック。                 |


**普通の視聴シーン**

- ライブルームリストにキャスターのuserID 情報がすでに含まれている場合、視聴者は、`enterRoom()`成功後に`startPlay(userID)`を直接呼び出せば、キャスターの画面を再生できます。
- ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者はルーム参加後に `TRTCLiveRoomDelegate`から`onAnchorEnter(userID)`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID 情報が含まれていますので、`startPlay(userID)`を再び呼び出せば、キャスターの画面を再生できます。

**ライブストリーミングのマイク接続シーン**
マイク接続の始動後、キャスターは `TRTCLiveRoomDelegate`から `onAnchorEnter(userID)`のコールバックを受信します。この時コールバックの中のuserIDを使用して `startPlay(userID)` を呼び出せば、マイク接続の画面を再生できます。



### stopPlay

リモートのビデオ画面のレンダリングを停止します。`onAnchorExit()`のコールバック時、このインターフェースを呼び出す必要があります。

```objc
/// リモートのビデオ画面のレンダリングを停止。
/// - Parameters:
///   - userID: 相手側のユーザー情報。
///   - callback: 操作コールバック。
/// - Note:
///   - onAnchorExitのコールバック時、このインターフェースを呼び出します。
- (void)stopPlayWithUserID:(NSString *)userID
                  callback:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPlay(userID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味             |
| -------- | ----------------------------------------- | ---------------- |
| userID   | String                                    | 相手側のユーザー情報。 |
| callback | (_ code: Int, _ message: String?) -> Void | 操作コールバック。       |




## キャスターと視聴者のマイク接続

### requestJoinAnchor

視聴者がマイク接続をリクエストします。

```objc
/// 視聴者側がマイク接続をリクエストします。
/// - Parameters:
///   - reason: マイク接続リクエストの理由。
///   - responseCallback: マイク接続リクエストのコールバック。
/// - Note: 視聴者がリクエストを送信すると、キャスター側は`onRequestJoinAnchor`のコールバックを受信します。
- (void)requestJoinAnchor:(NSString *)reason
                  timeout:(double)timeout
         responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestJoinAnchor(reason:timeout:responseCallback:));
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ                                        | 意味           |
| ---------------- | ------------------------------------------- | -------------- |
| reason           | String?                                     | マイク接続の理由。     |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | キャスターの応答のコールバック。 |

キャスターと視聴者のマイク接続フローは次のとおりです。

1. 【視聴者】`requestJoinAnchor()`を呼び出し、キャスターにマイク接続リクエストを送信します。
2. 【キャスター】 `TRTCLiveRoomDelegate`から `onRequestJoinAnchor()`のコールバック通知を受信します。
3. 【キャスター】`responseJoinAnchor()`を呼び出して、視聴者からのマイク接続リクエストを受け入れるか決定します。
4. 【視聴者】responseCallbackのコールバック通知を受信します。この通知にはキャスターの処理結果が含まれています。
5. 【視聴者】リクエストが同意されると、`startCameraPreview()`が呼び出され、ローカルカメラが起動します。
6. 【視聴者】`startPublish()`を呼び出し、正式にプッシュストリームの状態に入ります。
7. 【キャスター】一度視聴者がマイク接続に入ると、キャスターは、`TRTCLiveRoomDelegate`の `onAnchorEnter()`の通知を受信します。
8. 【キャスター】キャスターが `startPlay()`を呼び出すと、マイク接続の視聴者のビデオ画面を見ることができるようになります。
9. 【視聴者】ライブルームの中で他の視聴者がすでにキャスターとマイク接続を行っている場合、新しく参加したマイク接続の視聴者は`onAnchorEnter()`の通知を受け取ります。この時に`startPlay()`を呼び出せば他のマイク接続者のビデオ画面を再生することができます。


### responseJoinAnchor

キャスターがマイク接続のリクエストを処理します。キャスターは `TRTCLiveRoomDelegate` の `onRequestJoinAnchor()`のコールバックを受け取った後、このインターフェースを呼び出して、視聴者のマイク接続リクエストを処理する必要があります。

```objc
/// キャスターが視聴者のマイク接続リクエストに回答します。
/// - Parameters:
///   - user: 視聴者 ID。
///   - agree: true：同意；false：拒否。
///   - reason: マイク接続を同意/拒否した理由の説明。
/// - Note: キャスターが回答すると、視聴者側は`requestJoinAnchor`で渡された`responseCallback`のコールバックを受信します。
- (void)responseJoinAnchor:(NSString *)userID
                     agree:(BOOL)agree
                    reason:(NSString *)reason
NS_SWIFT_NAME(responseJoinAnchor(userID:agree:reason:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                      |
| ------ | ------- | ------------------------- |
| userID | String  | 視聴者 ID。                 |
| agree  | Bool    | true：同意；false：拒否。 |
| reason | String? | マイク接続を同意/拒否した理由の説明。 |


### kickoutJoinAnchor

キャスターがマイク接続の視聴者を追放します。キャスターがこのインターフェースを呼び出し、マイク接続の視聴者を追放すると、追放されたマイク接続の視聴者は、`TRTCLiveRoomDelegate`の`onKickoutJoinAnchor()`のコールバック通知を受信します。

```objc
/// キャスターがマイク接続の視聴者を追放します。
/// - Parameters:
///   - userID: マイク接続の視聴者 ID。
///   - callback: 操作コールバック。
/// - Note: キャスターがこのインターフェースを呼び出し、マイク接続の視聴者を追放すると、追放されたマイク接続の視聴者は、trtcLiveRoomOnKickoutJoinAnchor()のコールバック通知を受信します。
- (void)kickoutJoinAnchor:(NSString *)userID
                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(kickoutJoinAnchor(userID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味          |
| -------- | ----------------------------------------- | ------------- |
| userID   | String                                    | マイク接続の視聴者 ID。 |
| callback | (_ code: Int, _ message: String?) -> Void | 操作コールバック。    |



## キャスターのルーム間PK

### requestRoomPK

キャスターがルーム間PKをリクエストします。

```objc
/// キャスターがルーム間PKをリクエストします。
/// - Parameters:
///   - roomID: 招待された側のルーム ID。
///   - userID: 招待された側のキャスター ID。
///   - responseCallback: ルーム間PKのリクエスト結果のコールバック。
/// - Note: リクエストを送信すると、相手側のキャスターが `onRequestRoomPK`のコールバックを受信します。
- (void)requestRoomPKWithRoomID:(UInt32)roomID
                         userID:(NSString *)userID
               responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestRoomPK(roomID:userID:responseCallback:));
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ                                        | 意味                     |
| ---------------- | ------------------------------------------- | ------------------------ |
| roomID           | UInt32                                      | 招待された側のルームID。          |
| userID           | String                                      | 招待された側のキャスター ID。          |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | ルーム間PKのリクエスト結果のコールバック。 |

キャスターとキャスターの間でルーム間PKを行うことができます。ライブストリーミング中の2名のキャスター AとBのルーム間PKのフローは次のとおりです。

1. 【キャスター A】 `requestRoomPK()`を呼び出してキャスターBに向けてマイク接続リクエストを送信します。
2. 【キャスター B】`TRTCLiveRoomDelegate`の`onRequestRoomPK()`のコールバック通知を受信します。
3. 【キャスター B】`responseRoomPK()`を呼び出して、キャスター AのPKのリクエストを受け入れるかどうか決定します
4. 【キャスター B】キャスター Aのリクエストを受け入れる場合は、`TRTCLiveRoomDelegate`の `onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出してキャスター Aのビデオ画面を表示させます。
5. 【キャスター A】`responseCallback`のコールバック通知を受信します。この通知にはキャスター B の処理結果が含まれます。
6. 【キャスター A】リクエストが同意された場合は、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出し、キャスター Bのビデオ画面を表示します。


### responseRoomPK

キャスターがルーム間PKのリクエストに応答します。キャスターが応答した後、相手側キャスターは `requestRoomPK`で渡された`responseCallback`のコールバックを受信します。

```objc
/// ルーム間PKのリクエストに応答します。
/// キャスターが他のルームのキャスターのPKのリクエストに応答します。
/// - Parameters:
///   - user: PKをリクエストしたキャスターID
///   - agree: true：同意；false：拒否
///   - reason: PKに同意/拒否した理由の説明
/// - Note: キャスターの回答後、相手側キャスターは `requestRoomPK`で渡された`responseCallback`のコールバックを受信します。
- (void)responseRoomPKWithUserID:(NSString *)userID
                           agree:(BOOL)agree
                          reason:(NSString *)reason
NS_SWIFT_NAME(responseRoomPK(userID:agree:reason:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                      |
| ------ | ------- | ------------------------- |
| userID | String  | PKをリクエストしたキャスターID。   |
| agree  | Bool    | true：同意；false：拒否。 |
| reason | String? |  PK に同意/拒否した理由の説明。 |


### quitRoomPK

ルーム間PKから退出します。PK中のいずれかのキャスターがルーム間PK 状態から退出すると、もう一方のキャスターは `TRTCLiveRoomDelegate`の`trtcLiveRoomOnQuitRoomPK()`のコールバック通知を受信します。

```objc
/// キャスターがルーム間PKから退出します。
/// - Parameter callback: ルーム間PK 退出の結果のコールバック
/// - Note: 2名のキャスターのうちのいずれかがルーム間PKの状態から退出した後、もう一方のキャスターは `trtcLiveRoomOnQuitRoomPK`のコールバック通知を受信します。
- (void)quitRoomPK:(Callback _Nullable)callback
NS_SWIFT_NAME(quitRoomPK(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味       |
| -------- | ----------------------------------------- | ---------- |
| callback | (_ code: Int, _ message: String?) -> Void | 操作コールバック。 |


## 音声ビデオ制御に関連するインターフェース関数

### switchCamera

前後カメラを切り替えます。

```objc
/// 前後カメラを切り替えます。
- (void)switchCamera;
```


### setMirror

ミラー表示のオン／オフを設定します。

```objc
/// ミラー表示のオン／オフを設定します。
/// - Parameter isMirror: ミラーオン／オフ。
- (void)setMirror:(BOOL)isMirror
NS_SWIFT_NAME(setMirror(_:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ | 意味            |
| -------- | ---- | --------------- |
| isMirror | Bool | ミラーオン/オフ。 |


### muteLocalAudio

ローカルオーディオをミュートにします。

```objc
/// ローカルオーディオをミュートにします。
/// - Parameter isMuted: true：ミュートオン；false：ミュートオフ
- (void)muteLocalAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteLocalAudio(_:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ | 意味                              |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | true：ミュートオン；false：ミュートオフ |

### muteRemoteAudio

リモートの音声をミュートにします。

```objc
/// リモートの音声をミュートにします。
/// - Parameters:
///   - userID: リモートのユーザーID。
///   - isMuted: true：ミュートオン；false：ミュートオフ
- (void)muteRemoteAudioWithUserID:(NSString *)userID isMuted:(BOOL)isMuted
NS_SWIFT_NAME(muteRemoteAudio(userID:isMuted:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                              |
| ------- | ------ | --------------------------------- |
| userID  | String | リモートのユーザーのID。                   |
| isMuted | Bool   | true：ミュートオン；false：ミュートオフ |



### muteAllRemoteAudio

全てのリモート側の音声をミュートにします。

```objc
/// 全てのリモート側の音声をミュートにします。
/// - Parameter isMuted: true：ミュートオン；false：ミュートオフ
- (void)muteAllRemoteAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteAllRemoteAudio(_:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ | 意味                              |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | true：ミュートオン；false：ミュートオフ |

### setAudioQuality

音質の設定

```objc
/// 音質を設定します。サポートする値は1 2 3で、低中高を表します。
/// - Parameter quality 音質
- (void)setAudioQuality:(NSInteger)quality
NS_SWIFT_NAME(setAudioiQuality(_:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ      | 意味                         |
| ------- | --------- | ---------------------------- |
| quality | NSInteger | 1：音声、2：標準、3：音楽 |

## バックグラウンドミュージック・サウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンドミュージック・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66)の取得。

```objc
/// サウンドエフェクト管理オブジェクトを取得します。
- (TXAudioEffectManager *)getAudioEffectManager;
```

## 美顔フィルタに関するインターフェース関数

### getBeautyManager

美顔管理オブジェクト [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#interfaceTXBeautyManager)の取得。

```objc
/* 美顔管理オブジェクト TXBeautyManagerを取得します。
*
* 美顔管理では、次の機能を利用できます。
* - "美顔のスタイル"、“美白”、“肌色補正（血色・つや感）”、“デカ眼”、“顔痩せ”、“V顔”、“下あご”、“面長修正”、“小鼻”、“キラキラ目”、“白い歯”、“目の弛み除去”、“シワ除去”、“ほうれい線除去”などの美容効果を設定します。
* - “髪の生え際”、“眼と眼の距離”、“眼の角度”、“唇の形”、“鼻翼”、“鼻の位置”、“唇の厚さ”、“顔の形”を調整します。
* - 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
* - メイクアップを追加します。
* - ジェスチャー認識を行います。
*/
- (TXBeautyManager *)getBeautyManager;
```

美顔管理では、次の機能を使用できます。

- 「美顔のスタイル」、「美白」、「肌色補正（血色・つや感）」、「デカ眼」、「顔痩せ」、「V顔」、「下あご」、「面長補正」、「小鼻」、「キラキラ目」、「白い歯」、「目の弛み除去」、「シワ除去」、「ほうれい線除去」などの美容効果を設定します。
- 「髪の生え際」、「眼と眼の距離」、「眼角度」、「唇の形」、「鼻翼」、「鼻の位置」、「唇の厚さ」、「顔の形」を調整します。
- 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
- メイクアップを追加します。
- ジェスチャー認識を行います。



## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でのテキストメッセージの放送には、通常弾幕によるチャットを使用します。

```objc
/// 送信したテキストメッセージは、ルーム内の全参加者が見ることができます。
/// - Parameters:
///   - message: テキストメッセージ。
///   - callback: 送信コールバック。
- (void)sendRoomTextMsg:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味           |
| -------- | ----------------------------------------- | -------------- |
| message  | String                                    | テキストメッセージ。     |
| callback | (_ code: Int, _ message: String?) -> Void | 結果のコールバックを送信 |


### sendRoomCustomMsg

カスタマイズしたテキストメッセージを発信します。

```objc
/// カスタマイズメッセージを送信します。
/// - Parameters:
///   - command: コマンドワードは、開発者がカスタマイズ。主に異なるメッセージタイプを区分するのに使用。
///   - message: テキストメッセージ。
///   - callback: 送信コールバック。
- (void)sendRoomCustomMsgWithCommand:(NSString *)cmd message:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                                      | 意味                                               |
| -------- | ----------------------------------------- | -------------------------------------------------- |
| command  | String                                    | コマンドワードは、開発者がカスタマイズ。主に異なるメッセージタイプを区分するのに使用。 |
| message  | String                                    | テキストメッセージ。                                         |
| callback | (_ code: Int, _ message: String?) -> Void | 結果のコールバックを送信。                                     |


## デバックに関するインターフェース関数

### showVideoDebugLog

インターフェースにdebug 情報を表示するかどうか。

```objc
/// インターフェースにdebug情報を表示するかどうか
/// - Parameter isShow: Debug 情報表示のオン/オフ
- (void)showVideoDebugLog:(BOOL)isShow
NS_SWIFT_NAME(showVideoDebugLog(_:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                       |
| ------ | ---- | -------------------------- |
| isShow | Bool |  Debug情報表示のオン/オフ |


## TRTCLiveRoomDelegateイベントのコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>?SDK リカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
             onError:(NSInteger)code
             message:(NSString  *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onError:message:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| code         | Int              | エラーコード。                     |
| message      | String?          | エラーメッセージ。                   |


### onWarning

警告のコールバック。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
           onWarning:(NSInteger)code
             message:(NSString *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onWarning:message:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| code         | Int              | エラーコード TRTCWarningCode。     |
| message      | String?          | 警告メッセージ。                   |



### onDebugLog

Log コールバック。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
          onDebugLog:(NSString *)log
NS_SWIFT_NAME(trtcLiveRoom(_:onDebugLog:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| log          | String           | ログ情報。                   |


## ルームイベントのコールバック

### onRoomDestroy

ルームが廃棄された時のコールバック。キャスターがルームを退出する時、ルーム内の全ユーザーがこの通知を受信します。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onRoomDestroy:(NSString *)roomID
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomDestroy:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| roomID       | String           | ルーム ID。                    |


### onRoomInfoChange

ライブルーム情報変更のコールバック。ライブストリーミングのマイク接続やPKで、ルーム状態の変化を通知するシーンに多用されます。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
    onRoomInfoChange:(TRTCLiveRoomInfo *)info
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomInfoChange:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| info         | TRTCLiveRoomInfo | ルーム情報。                   |




## キャスターと視聴者の参加／退出のイベントコールバック

### onAnchorEnter

新しいキャスターのルーム参加の通知を受信します。マイク接続の視聴者とルーム間PKのキャスターがルームに参加すると、視聴者は、新しいキャスターがルームに参加したというイベントを受信します。`TRTCLiveRoom`の `startPlay()`を呼び出して、そのキャスターのビデオ画面を表示することができます。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onAnchorEnter:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorEnter:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| userID       | String           | 新しくルームに参加したユーザー ID。              |



### onAnchorExit

キャスターのルーム退出の通知を受信します。ルーム内のキャスター（およびマイク接続中の視聴者）が、新しいキャスターのルーム退出のイベントを受信します。`TRTCLiveRoom`の`stopPlay()`を呼び出して、そのキャスターのビデオ画面を閉じることができます。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
        onAnchorExit:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorExit:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| userID       | String           | ルームを退出したユーザー ID。                |



### onAudienceEnter

視聴者入室通知の受信。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onAudienceEnter:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceEnter:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| user         | TRTCLiveUserInfo | 入室した視聴者の情報。               |


### onAudienceExit

視聴者退室通知の受信。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
      onAudienceExit:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceExit:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| user         | TRTCLiveUserInfo | 退室した視聴者の情報。               |


## キャスターと視聴者のマイク接続のイベントコールバック

### onRequestJoinAnchor

キャスターが視聴者のマイク接続リクエストを受信した時のコールバック。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
 onRequestJoinAnchor:(TRTCLiveUserInfo *)user
             reason:(NSString * _Nullable)reason
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestJoinAnchor:reason:timeout:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| user         | TRTCLiveUserInfo | マイク接続をリクエストした視聴者の情報。           |
| reason       | String?          | マイク接続の理由の説明。               |
| timeout      | Double           | リクエスト処理のタイムアウトの時間。         |


### onKickoutJoinAnchor

マイク接続の視聴者がマイク接続から追放された通知を受信します。マイク接続の視聴者は、キャスターからマイク接続追放のメッセージを受信した場合、`TRTCLiveRoom`の`stopPublish()` を呼び出してマイク接続から退出する必要があります。

```objc
- (void)trtcLiveRoomOnKickoutJoinAnchor:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnKickoutJoinAnchor(_:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |



## キャスター間PKのイベントコールバック

### onRequestRoomPK

ルーム間PKのリクエストの通知を受信します。キャスターは、他のルームのキャスターからPKのリクエストを受け取り、PKに同意する場合、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出して招待側キャスターのストリームを再生する必要があります。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onRequestRoomPK:(TRTCLiveUserInfo *)user
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestRoomPK:timeout:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| user         | TRTCLiveUserInfo | ルーム間マイク接続を始動したキャスターの情報。    |
| timeout      | Double           | リクエスト処理のタイムアウトの時間。         |


### onQuitRoomPK

ルーム間PK中止の通知を受信します。

```objc
 - (void)trtcLiveRoomOnQuitRoomPK:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnQuitRoomPK(_:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |



## メッセージのイベントコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
   onRecvRoomTextMsg:(NSString *)message
            fromUser:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onRecvRoomTextMsg:fromUser:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。 |
| message      | String           | テキストメッセージ。                   |
| user         | TRTCLiveUserInfo | 発信者ユーザーの情報。             |



### onRecvRoomCustomMsg

カスタマイズメッセージの受信。

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
onRecvRoomCustomMsgWithCommand:(NSString *)command
             message:(NSString *)message
            fromUser:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onRecvRoomCustomMsg:message:fromUser:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ             | 意味                                               |
| ------------ | ---------------- | -------------------------------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 現在のTRTCLiveRoomコンポーネントインスタンス。                       |
| command      | String           | コマンドワードは、開発者がカスタマイズ。主に異なるメッセージタイプを区分するのに使用。 |
| message      | String           | テキストメッセージ。                                         |
| user         | TRTCLiveUserInfo | 発信者ユーザーの情報。                                   |
