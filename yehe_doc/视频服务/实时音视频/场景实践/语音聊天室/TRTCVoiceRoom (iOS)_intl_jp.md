TRTCVoiceRoom は、Tencent CloudのTRTCおよびIM サービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- キャスターが新しいボイスチャットルームを作成して放送を開始し、視聴者がボイスチャットルームに参加して視聴/インタラクティブなコミュニケーションを図ります。
- キャスターは、視聴者をマイク・オンに招待したり、マイク・オンのキャスターをマイク・オフにすることもできます。
- キャスターはまた、座席をクローズすることができ、その他の視聴者はマイク・オンを再度リクエストすることができなくなります。
- 視聴者は、マイク・オンをリクエストして、マイク・オンのキャスターに変わることができます。他人とインタラクティブの会話ができ、随時マイク・オフにして通常の視聴者になることも可能です。
- 各種のテキストメッセージやカスタマイズメッセージの発信をサポートし、情報を弾幕、「いいね」、ギフトなどに使えられるようにカスタマイズします。

TRTCVoiceRoom は、オープンソースの Classであり、Tencent Cloudの2つのクローズソースであるSDKに依存しています。具体的な実装プロセスは [ボイスチャットルーム（iOS）](https://intl.cloud.tencent.com/document/product/647/37287)を参照してください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低レイテンシーのオーディオビデオ通話コンポーネントとして使用しています。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047) の AVChatroom を使用してチャットルーム機能を実現します。同時に IM のインターフェース属性によって、マイクリストなどのルーム情報を保管し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。


<h2 id="TRTCVoiceRoom">TRTCVoiceRoom API 概要</h2>

### SDK 基本関数

| API                                             | 説明                                             |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを廃棄します。                                   |
| [setDelegate](#setdelegate)                     | イベントコールバックを設定します。     |
| [setDelegateHandler](#setdelegatehandler)       |イベントのコールバックが所在するスレッドを設定します。 |
| [login](#login)                                 | ログイン。                   |
| [logout](#logout)                               | ログアウト。                   |
| [setSelfProfile](#setselfprofile)               | 個人情報の修正。           |

### ルーム関連インターフェース関数

| API                                             | 説明                                             |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)           | ルームの新規作成（キャスターがコール）。ルームが存在していない場合は、システムが新しいルームを自動作成。
| [destroyRoom](#destroyroom)         | ルームの廃棄（キャスターがコール）。                                       |
| [enterRoom](#enterroom)             | 入室（視聴者がコール）。                                       |
| [exitRoom](#exitroom)               | 退室（視聴者がコール）。                                       |
| [getRoomInfoList](#getroominfolist) | ルームリストの詳細情報の取得。                              |
| [getUserInfoList](#getuserinfolist) | 指定された userId のユーザー情報の取得。 nullの場合は、ルーム内全員の情報を取得。 |

### マイク管理インターフェース

| API                                             | 説明                                             |
| ----------------------- | ----------------------------------- |
| [enterSeat](#enterseat) | 自主的にマイク・オン（視聴者／キャスターともにコール可）。  |
| [leaveSeat](#leaveseat) | 自主的にマイク・オフ（視聴者／キャスターともにコール可）。  |
| [pickSeat](#pickseat)   | ピックしてマイク・オン（キャスターがコール）。              |
| [kickSeat](#kickseat)   | キックしてマイク・オフ（キャスターがコール）。              |
| [muteSeat](#muteseat)   | 任意のマイクのミュート／ミュート解除（キャスターがコール）。 |
| [closeSeat](#closeseat) | 任意のマイクのクローズ/解除（キャスターがコール）。     |

### ローカル音声操作インターフェース

| API                                             | 説明                  |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | マイクの集音開始。     |
| [stopMicrophone](#stopmicrophone)               | マイクの集音停止。     |
| [setAudioQuality](#setaudioquality)             | 音質の設定。           |
| [muteLocalAudio](#mutelocalaudio)               | ローカルオーディオミュートの開始／停止。  |
| [setSpeaker](#setspeaker)                       | スピーカーの起動設定。     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | マイクの集音音量設定。 |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 再生音量の設定。       |


### リモートユーザー音声操作インターフェース

| API                                             | 説明                                             |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | ミュート／ミュート解除指定メンバー。 |
| [muteAllRemoteAudio](#muteallremoteaudio) | ミュート／ミュート解除全メンバー。 |

### バックグラウンドミュージック・サウンドエフェクト関連インターフェース

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | バックグラウンドミュージック・サウンドエフェクト管理オブジェクト[TXAudioEffectManager](#trtcaudioeffectmanagerapi)の取得。 |

### 情報発信関連インターフェース

| API                                     | 説明                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージの放送には、通常弾幕によるチャットを使用します。｜
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを発信します。                     |

### 招待シグナリング関連インターフェース

| API                                  | 説明             |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | ユーザーに招待を発信。 |
| [acceptInvitation](#acceptinvitation) | 招待の同意。       |
| [rejectInvitation](#rejectinvitation) | 招待の辞退。       |
| [cancelInvitation](#cancelinvitation) | 招待の取り消し。       |

<h2 id="TRTCVoiceRoomDelegate">TRTCVoiceRoomDelegate API 概要</h2>

### 一般的なイベントコールバック

| API                       | 説明       |
| ------------------------- | ---------- |
| [onError](#onerror) | エラーのコールバック。 |
| [onWarning](#onwarning)   | 警告のコールバック。 |
| [onDebugLog](#ondebuglog) | Log コールバック。 |

### ルームイベントのコールバック

| API                                       | 説明                   |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | ルームが廃棄された時のコールバック。     |
| [onRoomInfoChange](#onroominfochange) | ボイスチャットルーム情報変更のコールバック。|
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。     |

### マイク変更コールバック

| API                                     | 説明                                  |
| --------------------------------------- | ------------------------------------- |
| [onSeatListChange](#onseatlistchange)   |全量のマイクリストの変更。                  |
| [onAnchorEnterSeat](#onanchorenterseat) |  マイク・オンの参加者（自主的にマイク・オン／キャスターがピックしてマイク・オン）。  |
| [onAnchorLeaveSeat](#onanchorleaveseat) | マイク・オフの参加者（自主的にマイク・オフ／キャスターがキックしてマイク・オフ）。|
| [onSeatMute](#onseatmute)               | キャスターのマイクミュート。                            |
| [onSeatClose](#onseatclose)             | キャスターのマイククローズ。                            |

### 視聴者の入退室イベントのコールバック

| API                                 | 説明               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) |視聴者入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | 視聴者退室通知の受信。|

### メッセージイベントのコールバック

| API                                         | 説明             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | テキストメッセージの受信。|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタマイズメッセージの受信。|

### シグナリングイベントのコールバック

| API                                               | 説明               |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 新規招待リクエストの受信。 |
| [onInviteeAccepted](#oninviteeaccepted)           | 被招待者が招待に同意。 |
| [onInviteeRejected](#oninviteerejected)           | 被招待者による招待の辞退。 |
| [onInvitationCancelled](#oninvitationcancelled)   | 招待者が招待を取り消し。   |

## SDK 基本関数

<span id="sharedInstance"></span>

### sharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) シングルトンオブジェクトの取得。

```Objective-C
/**
*  TRTCVoiceRoom シングルトンオブジェクトの取得
*
* - returns: TRTCVoiceRoom インスタンス
* - note:  {@link TRTCVoiceRoom#destroySharedInstance()} をコールしてシングルトンオブジェクトを廃棄することができます
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) シングルトンオブジェクトの廃棄。

>?インスタンスを廃棄後は、外部にキャッシュされた  TRTCVoiceRoom インスタンスの再使用ができません。改めて [sharedInstance](#sharedInstance) をコールして、インスタンスを新規取得する必要があります。

```Objective-C
/**
*  TRTCVoiceRoom のシングルトンオブジェクトの廃棄
*
* - note: インスタンスの廃棄後が、外部似キャッシュされた TRTCVoiceRoom インスタンスは再使用ができません。改めて {@link TRTCVoiceRoom#sharedInstance()} をコールして、インスタンスを新規取得する必要があります
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) イベントコールバック、 TRTCVoiceRoomDelegate を介して [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) の各種ステータス通知を受け取ることができます。

```Objective-C
/**
* コンポーネントコールバックインターフェースの設定
* 
*  TRTCVoiceRoomDelegate によって TRTCVoiceRoom の各種ステータス通知を取得することができます
*
* - parameter delegate コールバックインターフェース
* - note: TRTCVoiceRoom のコールバックイベント。デフォルトは Main Queue の中でコールバック。イベントのコールバックが所在するキューを指定する必要がある場合は、 {@link TRTCVoiceRoom#setDelegateQueue(queue)}を使用できます
*/
- (void)setDelegate:(id<TRTCVoiceRoomDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?setDelegate は、 TRTCVoiceRoom のプロキシコールバックです。   

### setDelegateQueue

イベントコールバックが所在するスレッドキューを設定し、デフォルトはメインスレッド MainQueue に発送します。

```Objective-C
/**
* イベントのコールバックが所在するキューの設定
*
* - parameter queue キュー，TRTCVoiceRoom の各種ステータス通知のコールバックは、指定するqueueに発信します。
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ             | 意味                                                       |
| ----- | ---------------- | ------------------------------------------------------------ |
| queue | dispatch_queue_t | TRTCVoiceRoom の各種ステータス通知は、指定するスレッドキューに発信します。|

   

### login

ログイン。

```Objective-C
- (void)login:(int)sdkAppID
       user:(NSString *)userID
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userId:userSig:callback:));

```
【[アプリケーション管理]（https://console.cloud.tencent.com/trtc/app）】
パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppID | int         | Tencent Real-Time Communicationコンソール> **[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)** >アプリケーション情報でSDKAppIDを表示できます。 |
| user     | String                | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String                | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法 ](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallback | ログインのコールバック。成功時に code は0になります。                                  |

   

### logout

ログアウト。

```Objective-C
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                        |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | ログアウトのコールバック。成功時に code は0になります。 |

   

### setSelfProfile

個人情報の修正。

```Objective-C
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                |
| --------- | -------------- | ----------------------------------- |
| userName  | String         | ニックネーム。                              |
| avatarURL | String         | プロファイル写真のアドレス。                          |
| callback | ActionCallback | 個人情報設定のコールバック。成功時に code は0になります。                                  |

   


## ルーム関連インターフェース関数

### createRoom

ルームの新規作成（キャスターがコール）。

```Objective-C
- (void)createRoom:(int)roomID roomParam:(VoiceRoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                | 意味                                                         |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomId | int | ルームIDは、ご自身でアサインし、統一管理する必要があります。複数の roomID を、一つのボイスチャットルームリストにまとめることができます。Tencent Cloudではボイスチャットルームリストの管理サービスを一時的に行いませんので、ご自身でボイスチャットルームリストを管理してください。 |
| roomParam | TRTCCreateRoomParam | ルーム情報は、ルーム名、マイク情報、カバー情報などのルーム説明の情報に使用します。マイク管理が必要な場合は、ルームのマイク数を記入する必要があります。 |
| callback | ActionCallback | ルームの新規作成結果のコールバック。成功時に code は0になります。                                  |

キャスターが放送開始する通常のコールフローは以下のとおりです。 
1. キャスターは、 `createRoom` をコールして新しいボイスチャットルームを作成します。この時にルーム ID、マイク・オンに管理者の確認の要否、マイク数などルームの属性情報を伝達します。
2. キャスターは、ルーム作成の成功後、 `enterSeat` をコールして参加します。
3. キャスターは、コンポーネントの `onSeatListChange` マイクリストの変更イベント通知を受信します。この時にマイクリストの変更を UI 上に更新することができます。
4. キャスターは、マイクリストのメンバーが`onAnchorEnterSeat` に参加したとのイベント通知も受信します。この時にマイクは自動的に集音を開始します。

   

### destroyRoom

ルームの廃棄（キャスターがコール）。キャスターは、ルーム作成後、この関数をコールしてルームを廃棄します。

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時に code は0になります。                                  |


### EnterRoom

入室（視聴者がコール）

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | int            | ルームID。                            |
| callback | ActionCallback | 入室結果のコールバック。成功時に code は0になります。                                  |


視聴者が入室し視聴した通常のコールフローは以下のとおりです。 

1. 視聴者がサーバーから取得する最新のボイスチャットルームリストには、多くのボイスチャットルームの roomId およびルーム情報が含まれます。
2．視聴者は一つのボイスチャットルームを選択し、 `enterRoom` をコールしてルームナンバーを伝送すると、そのルームに参加できます。
3. 入室後、コンポーネントの `onRoomInfoChange` ルーム属性の変更イベント通知を受信することがあります。この時にルーム属性を記録し、適応する修正を行うことができます。例：UI に表示されるルーム名、マイク・オンにキャスターの同意を求める要否など。
4. 入室後は、コンポーネントの `onSeatListChange` マイクリスト変更イベント通知を受信します。この時にマイクリストの変更を UI 上に更新することができます。
5. 入室後にマイクリストにキャスターが参加した `onAnchorEnterSeat` のイベント通知も受信します。

### ExitRoom

ルームを退出する。

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 退室結果のコールバック。成功時に code は0になります。                                  |

   

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、キャスターが `createRoom()` 作成時に roomInfo によって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(VoiceRoomInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味               |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | ルームナンバーリスト。       |
| callback   | RoomInfoCallback    | ルーム詳細情報のコールバック。 |


### getUserInfoList

指定された userId のユーザー情報を取得します。

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(VoiceRoomUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ               | 意味                                                         |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt; | 取得すべきユーザー ID 表、 nullの場合は、ルーム内全員の情報を取得します。 |
| userlistcallback | UserListCallback   | ユーザーの詳細情報のコールバック。                                          |


## マイク管理インターフェース

### enterSeat

自主的にマイク・オン（視聴者／キャスターともにコール可）。

>?マイク・オンの成功後、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorEnterSeat` のイベント通知を受信します。

```Objective-C
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                 |
| --------- | -------------- | -------------------- |
| seatIndex | int            | マイク・オンの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。           |

このインターフェースをコールすると、すぐにマイクリストが修正されます。視聴者がキャスターにのリクエストを必要とするユースケースの場合は、まず `sendInvitation` をコールしてからキャスターにリクエストし、 `onInvitationAccept ` を受信してから、該当する関数をコールすることができます。

### leaveSeat

自主的にマイク・オフ（視聴者／キャスターともにコール可）。

>?マイク・オフの成功後、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorLeaveSeat` のイベント通知を受信します。

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback  | ActionCallback | 操作コールバック。 |

### pickSeat

ピックしてマイク・オン（キャスターがコール）。  

>?キャスターによって視聴者がピックしてマイク・オンに成功後、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorEnterSeat` のイベント通知を受信します。

```Objective-C
- (void)pickSeat:(NSInteger)seatIndex userId:(NSString *)userId callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(seatIndex:userId:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | 着席してマイク・オンの必要があるマイク番号。 |
| userId | String           | ユーザー ID。        |
| callback  | ActionCallback | 操作コールバック。             |

このインターフェースをコールすると、すぐにマイクリストが修正されます。キャスターが、視聴者の同意がなければマイク・オンできないユースケースの場合は、まず `sendInvitation` をコールしてから視聴者にリクエストし、 `onInvitationAccept ` を受信してから、その関数をコールできます。


### kickSeat

キックしてマイク・オフ（キャスターがコール）。   

>?キャスターがキックしてマイク・オフにすると、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorLeaveSeat` のイベント通知を受信します。

```Objective-C
- (void)kickSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(seatIndex:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | キックしてマイク・オフの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。             |

そのインターフェースをコールすると、すぐにマイクリストが修正されます。キャスターが視聴者の同意がなければマイク・オンできないユースケースの場合は、まず `sendInvitation` をコールしてから視聴者にリクエストし、 `onInvitationAccept ` を受信してから、その関数をコールすることができます。

### muteSeat

任意のマイクのミュート／ミュート解除（キャスターがコール）。

>? 任意のマイクのミュート／ミュート解除は、ルーム内の全メンバーが `onSeatListChange` および `onSeatMute` のイベント通知を受信します。

```Objective-C
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                     | 意味                                                       |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | int            | 操作の必要があるマイク番号。                          |
| isMute    | boolean        | true：対応マイクのミュート；false：対応マイクのミュート解除。 |
| callback  | ActionCallback | 操作コールバック。                                    |

このインターフェースをコールすると、すぐにマイクリストが修正されます。 seatIndex の座席に該当するキャスターは、 muteAudio を自動的にコールしてミュート／ミュートオフにします。

### closeSeat

任意のマイクのクローズ/解除（キャスターがコール）。

>? キャスターは、該当するマイクをクローズ／解除し、ルーム内の全参加者は `onSeatListChange` および `onSeatClose` のイベント通知を受信します。

```Objective-C
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                       |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | int            | 操作の必要があるマイク番号。                       |
| isClose   | boolean        | true：該当するマイクのクローズ； false：該当するマイクのクローズ解除。 |
| callback  | ActionCallback | 操作コールバック。                                 |

このインターフェースをコールすると、すぐにマイクリストが修正されます。対応するseatIndex をクローズされた座席上のキャスターは、自動的にマイク・オフになります。


## ローカル音声操作インターフェース

### startMicrophone

マイクの集音開始。 

```Objective-C
- (void)startMicrophone;
```

### stopMicrophone

マイクの集音停止。 

```Objective-C
- (void)stopMicrophone;
```

### setAudioQuality

音質の設定。

```Objective-C
- (void)setAuidoQuality:(NSInteger)quality NS_SWIFT_NAME(setAuidoQuality(quality:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 音声品質。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルの音声のミュート／ミュート取り消し

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | ミュート／ミュート取り消し。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |



### setSpeaker

スピーカーの起動設定。

```Objective-C
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ | 意味                           |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true：スピーカー；false：ヘッドホン。 |



### setAudioCaptureVolume

マイクの集音音量設定。

```Objective-C
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 集音音量、0 - 100、 デフォルト100。 |


### setAudioPlayoutVolume

再生音量の設定。

```Objective-C
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 再生音量、0 - 100、 デフォルト100。 |

### muteRemoteAudio

ミュート／ミュート解除指定メンバー。

```Objective-C
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                              |
| ------ | ------- | --------------------------------- |
| userId | String           | 指定ユーザー ID。        |
| mute   | boolean | true：ミュート起動；false：ミュート停止。 |

### muteAllRemoteAudio

ミュート／ミュート解除全メンバー。 |

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |

   

## バックグラウンドミュージック・サウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```Objective-C
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でのテキストメッセージの放送には、通常弾幕によるチャットを使用します。

```Objective-C
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| message  | String         | テキストメッセージ。     |
| callback  | ActionCallback | 発信結果のコールバック。 |

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを発信します。

```Objective-C
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                               |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | String         | コマンドワードは、開発者がカスタマイズ。主に異なるメッセージタイプを区分するのに使用。 |
| message  | String         | テキストメッセージ。                                         |
| callback  | ActionCallback | 発信結果のコールバック。                                    |

   

## 招待シグナリング関連インターフェース

### sendInvitation

ユーザーに招待を発信。

```Objective-C
- (NSString *)sendInvitation:(NSString *)cmd
                      userId:(NSString *)userID
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味             |
| -------- | -------------- | ---------------- |
| cmd      | String         | 業務カスタマイズコマンド。 |
| userId | String           | 招待ユーザー ID。  |
| content  | String         | 招待コンテンツ。     |
| callback  | ActionCallback | 発信結果のコールバック。   |

戻り値：

| 戻り値   | タイプ   | 意味                  |
| -------- | ------ | --------------------- |
| inviteId | String | 今回の招待 IDの識別に使用。 |

### acceptInvitation

招待の同意。

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待 ID。      |
| callback  | ActionCallback | 発信結果のコールバック。 |

### rejectInvitation

招待の辞退。

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待 ID。      |
| callback  | ActionCallback | 発信結果のコールバック。 |


### cancelInvitation

招待の取り消し。

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待 ID。      |
| callback  | ActionCallback | 発信結果のコールバック。 |

## TRTCVoiceRoomDelegateイベントのコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>?SDK リカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```Objective-C
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message  | String  | エラーメッセージ。 |


### onWarning

警告のコールバック。

```Objective-C
- (void)onWarning:(int)code
                  message:(NSString*)message
NS_SWIFT_NAME(onWarning(code:message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message | String | 警告メッセージ。 |

   

### onDebugLog

Log コールバック。

```Objective-C
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | ログ情報。 |

   


## ルームイベントのコールバック

### onRoomDestroy

ルーム廃棄のコールバック。キャスターがルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

```Objective-C
- (void)onRoomDestroy:(NSString *)message
NS_SWIFT_NAME(onRoomDestroy(message:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味      |
| ------ | ------ | --------- |
| roomId | String | ルーム ID。 |


### onRoomInfoChange

入室に成功後、このインターフェースをコールバックします。roomInfo は作成されたルームの情報を含みます。

```Objective-C
- (void)onRoomInfoChange:(VoiceRoomInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味       |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | ルーム情報。 |

   

### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。

```Objective-C
- (void)onUserVolumeUpdate:(NSString *)userId
                              volume:(NSInteger)volume
NS_SWIFT_NAME(onUserVolumeUpdate(userId:volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                      |
| ------ | ------ | ------------------------- |
| userId | String|  ユーザー ID。                 |
| volume | int    | 音量、値：0 - 100。 |


## マイクコールバック

### onSeatListChange

全量のマイクリストの変更は、全てのマイクリストを含みます。

```Objective-C
- (void)onSeatInfoChange:(NSArray<VoiceRoomSeatInfo *> *)seatInfolist
NS_SWIFT_NAME(onSeatListChange(seatInfoList:));
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ                 | 意味             |
| ------------ | -------------------- | ---------------- |
| seatInfoList | List&lt;SeatInfo&gt; | 全量のマイクリスト。 |

### onAnchorEnterSeat

 マイク・オンの参加者（自主的にマイク・オン／キャスターがピックしてマイク・オン）。 

```Objective-C
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | int      | 参加者がマイク・オンのマイク。     |
| user  | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onAnchorLeaveSeat

マイク・オフの参加者（自主的にマイク・オフ／キャスターがキックしてマイク・オフ）。

```Objective-C
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | int      | マイク・オフのマイク。         |
| user  | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onSeatMute

キャスターのマイクミュート。

```Objective-C
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                               |
| ------ | ------- | ---------------------------------- |
| index  | int     | 操作するマイク。                       |
| isMute    | boolean        | true：ミュートマイク；false：ミュート解除。 |

### onSeatClose

キャスターのマイククローズ。

```Objective-C
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ         | 意味                                |
| ------- | ------- | ----------------------------------- |
| index  | int     | 操作するマイク。                       |
| isClose   | boolean        | true：マイクのクローズ； false：マイクのクローズ解除。 |

## 視聴者の入退室イベントのコールバック

### onAudienceEnter

視聴者入室通知の受信。

```Objective-C
- (void)onAudienceEnter:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 入室した視聴者の情報。 |

### onAudienceExit

視聴者退室通知の受信。

```Objective-C
- (void)onAudienceExit:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 退室した視聴者の情報。 |

   

## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```Objective-C
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味             |
| -------- | -------- | ---------------- |
| message  | String         | テキストメッセージ。                                         |
| userInfo | UserInfo | 発信者ユーザーの情報。 |

   

### onRecvRoomCustomMsg

カスタマイズメッセージの受信。

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)cmd
                    message:(NSString*)message
                   userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(cmd:message:userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味                                               |
| -------- | -------- | -------------------------------------------------- |
| command  | String   | コマンドワードは、開発者がカスタマイズ。主に異なるメッセージタイプを区分するのに使用。 |
| message  | String         | テキストメッセージ。                                         |
| userInfo | UserInfo | 発信者ユーザーの情報。                                   |

## 招待シグナリングのイベントのコールバック

### onReceiveNewInvitation

新規招待リクエストの受信。

```Objective-C
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(identifier:inviter:cmd:content:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ     | 意味                               |
| ------- | -------- | ---------------------------------- |
| id      | String   | 招待 ID。                          |
| inviter | String   | 招待者のユーザー ID。                  |
| cmd     | String   | 業務指定のコマンドワードは、開発者がカスタマイズ。 |
| content | UserInfo | 業務指定のコンテンツ。                   |

### onInviteeAccepted

被招待者が招待に同意

```Objective-C
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待 ID。           |
| inviter | String | 被招待者のユーザー ID。 |

### onInviteeRejected

被招待者による招待の辞退。

```Objective-C
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待 ID。           |
| inviter | String | 被招待者のユーザー ID。 |

### onInvitationCancelled

招待者が招待を取り消し。

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味              |
| ------- | ------ | ----------------- |
| id      | String | 招待 ID。         |
| inviter | String | 招待者のユーザー ID。 |
