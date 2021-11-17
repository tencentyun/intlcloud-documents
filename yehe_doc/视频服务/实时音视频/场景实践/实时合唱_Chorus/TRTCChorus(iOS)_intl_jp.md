TRTCChorusRoomは、Tencent CloudのTencent Real-Time Communication(TRTC)とIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- 管理者が新規作成したChorusルームで放送が開始され、リスナーはChorusルームに入って聴取/コーラスを行います。
- 管理者は、楽曲リクエスト、視聴者のマイク・オンへの招待、キックアウトしてマイク・オフ、コーラスの開始を管理することができます。
- 管理者はまた、座席をクローズすることができ、その他のリスナーはマイク・オンを申請することができなくなります。
- リスナーはマイク・オンの申請ができ、マイク・オンするとサブボーカルになります。マイク・オンした後は、キャスターとコーラスすることも、コーラスが終わるまで待って通常のリスナーになることもできます。
- ギフトや各種のテキストメッセージ、カスタムメッセージの送信をサポートします。カスタムメッセージを弾幕、「いいね」などを実装するために使用することができます。

TRTCChorusRoomはオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実装プロセスについては、[Chorus（iOS）](https://intl.cloud.tencent.com/document/product/647/42688)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のボイスチャットコンポーネントとして使用しています。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用してチャットルーム機能を実装します。同時にIMの属性インターフェースによって、マイクリストなどのルーム情報を保存し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。

[](id:TRTCChorusRoom)
## TRTCChorusRoom API概要

### SDK基本関数

| APII      | 説明       |
| ------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)       | シングルトンオブジェクトを取得します。 |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを破棄します。|
| [setDelegate](#setdelegate)       | イベントコールバックを設定します。|
| [delegateQueue](#delegatequeue)   | イベントコールバックが配置されているスレッドを設定します。 |
| [login](#login))| ログイン。|
| [logout](#logout)      | ログアウト。|
| [setSelfProfile](#setselfprofile) | 個人情報を修正します。|

### ルーム関連インターフェース関数

| API| 説明 |
| -------------- | ----------- |
| [createRoom](#createroom)               | ルームの作成（管理者が呼び出し）。ルームが存在しない場合は、システムが新しいルームを自動的に作成します。 |
| [destroyRoom](#destroyroom) | ルームの破棄（管理者が呼び出し）。|
| [enterRoom](#enterroom)     | 入室（リスナーが呼び出し）。|
| [exitRoom](#exitroom)       | 退室（リスナーが呼び出し）。|
| [getRoomInfoList](#getroominfolist) | ルームリストの詳細情報を取得します。|
| [getUserInfoList](#getuserinfolist) | 指定されたuserIdのユーザー情報を取得します。nilの場合は、ルーム内全員の情報を取得します。 |

### 音楽再生インターフェース

| API| 説明     |
| -------------- | --------------- |
| [startPlayMusic](#startPlayMusic)   | 音楽の再生を開始します。|
| [stopPlayMusic](#stopPlayMusic)     | 音楽の再生を停止します。|
| [pausePlayMusic](#pausePlayMusic)   | 音楽の再生を一時停止します。		|
| [resumePlayMusic](#resumePlayMusic) | 音楽の再生を再開します。		|

### マイク管理インターフェース

| API       | 説明    |
| ----------------------- | -------------- |
| [enterSeat](#enterseat) | ユーザーが発言者になる（リスナー側/管理者ともに呼び出し可）。|
| [leaveSeat](#leaveseat) | 自主的にマイク・オフ（キャスターが呼び出し）。|
| [pickSeat](#pickseat)   | 視聴者が発言できるように招待（管理者が呼び出し）。|
| [kickSeat](#kickseat)   | キックアウトしてマイク・オフ（管理者が呼び出し）。|
| [closeSeat](#closeseat) | 任意のマイクのクローズ/解除（管理者が呼び出し）。|

### ローカルの音声操作インターフェース

| API      | 説明   |
| ------------------- | -------------------- |
| [startMicrophone](#startmicrophone)     | マイクの集音開始。|
| [stopMicrophone](#stopmicrophone)       | マイクの集音停止。|
| [setAudioQuality](#setaudioquality)     | 音質の設定。|
| [muteLocalAudio](#mutelocalaudio)       | ローカル音声のミュート起動/停止。|
| [setSpeaker](#setspeaker) | スピーカーの起動設定 。|
| [setAudioCaptureVolume](#setaudiocapturevolume) | マイクの集音音量設定。|
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 再生音量の設定。|
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | インイヤーモニタリングのオン/オフ。|


### BGMサウンドエフェクト関連インターフェース

| API      | 説明 |
| ------------------- | ----------- |
| [getAudioEffectManager](#getaudioeffectmanager) | BGMサウンドエフェクト管理オブジェクト[TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager)の取得。 |

### メッセージ送信関連インターフェース

| API      | 説明 |
| ------------------ | ------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージのブロードキャスト。通常、弾幕によるチャットに使用します。|
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを送信します。|

### 招待シグナリング関連インターフェース

| API  | 説明     |
| ---------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | ユーザーに招待を送信。 |
| [acceptInvitation](#acceptinvitation) | 招待の同意。|
| [rejectInvitation](#rejectinvitation) | 招待の辞退。|
| [cancelInvitation](#cancelinvitation) | 招待の取り消し。|

<h2 id="TRTCChorusRoomDelegate">TRTCChorusRoomDelegate API概要</h2>

### 一般的なイベントコールバック

| API        | 説明       |
| ------------------------- | ---------- |
| [onError](#onerror) | エラーのコールバック。 |
| [onWarning](#onwarning)   | 警告のコールバック。 |
| [onDebugLog](#ondebuglog) | Logコールバック。|

### ルームイベントのコールバック

| API| 説明     |
| -------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)   | ルームが破棄された時のコールバック。|
| [onRoomInfoChange](#onroominfochange) | ボイスチャットルーム情報変更のコールバック。|
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。|

### マイク変更コールバック

| API      | 説明      |
| ------------------ | ---------------- |
| [onSeatListChange](#onseatlistchange)   |全量のマイクリストの変更。|
| [onAnchorEnterSeat](#onanchorenterseat) | 発言者のメンバーがいます（ユーザーが発言者になる/管理者が視聴者を発言できるように招待）。 |
| [onAnchorLeaveSeat](#onanchorleaveseat) | 視聴者のメンバーがいます（ユーザーが視聴者になる/管理者がキックアウトしてマイク・オフ）。 |
| [onUserMicrophoneMute](#onusermicrophonemute)       | ユーザーのマイクがミュートされているかどうか。|
| [onSeatClose](#onseatclose)     | 管理者のマイククローズ。|

### リスナーの入退室イベントのコールバック

| API| 説明       |
| -------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | リスナー入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | リスナー退室通知の受信。|

### メッセージイベントのコールバック

| API  | 説明     |
| ---------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | テキストメッセージの受信。|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージの受信。|

### シグナリングイベントのコールバック

| API        | 説明       |
| --------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 新規招待リクエストの受信。   |
| [onInviteeAccepted](#oninviteeaccepted)   | 被招待者が招待に同意。 |
| [onInviteeRejected](#oninviteerejected)   | 被招待者が招待を拒否。   |
| [onInvitationCancelled](#oninvitationcancelled)   | 招待者が招待を取り消し。|

### 楽曲イベントコールバック

| API        | 説明       |
| --------------------- | ----------------- |
| [onMusicProgressUpdate](#onMusicProgressUpdate)   | 楽曲再生進捗度のコールバック。 |
| [onMusicPrepareToPlay](#onMusicPrepareToPlay)     | 音楽再生準備のコールバック。 |
| [onMusicCompletePlaying](#onMusicCompletePlaying) | 音楽再生完了のコールバック。 |
| [onReceiveAnchorSendChorusMsg](#onReceiveAnchorSendChorusMsg) | 管理者から送信されたコーラスメッセージをコールバックします。 |

## SDK基本関数

[](id:sharedInstance)

### sharedInstance

[TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940)シングルトンオブジェクトを取得します。

```ObjectiveC
/**
* TRTCChorusシングルトンオブジェクトを取得します
*
* - returns: TRTCChorusインスタンス
* - note: {@link TRTCChorus#destroySharedInstance()}を呼び出してシングルトンオブジェクトを破棄することができます
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

[TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940)シングルトンオブジェクトを破棄します。

>?インスタンスの破棄後は、外部にキャッシュされたTRTCChorusインスタンスは再使用できなくなります。改めて[sharedInstance](#sharedInstance)を呼び出し、新しいインスタンスを取得する必要があります。

```ObjectiveC
/**
* TRTCChorusシングルトンオブジェクトを破棄します
*
* - note: インスタンスの破棄後、外部にキャッシュされたTRTCChorusインスタンスは再利用できなくなります。改めて{@link TRTCChorus#sharedInstance()}を呼び出し、新しいインスタンスを取得する必要があります
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

[TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940)イベントコールバック。 TRTCChorusDelegateを介して[TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940)の各種ステータス通知を受け取ることができます。

```ObjectiveC
/**
* コンポーネントコールバックインターフェースの設定
* 
* TRTCChorusDelegateを介してTRTCChorusの各種ステータス通知を受け取ることができます
*
* - parameter delegateコールバックインターフェース
* - note: TRTCChorusのコールバックイベントは、デフォルトではMain Queueでコールバックされます。イベントのコールバックが配置されているキューを指定する必要がある場合は、{@link TRTCChorus#setDelegateQueue(queue)}を使用することができます
*/
- (void)setDelegate:(id<TRTCChorusDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?setDelegateはTRTCChorusのプロキシコールバックです。   

### setDelegateQueue

イベントコールバックが所在するスレッドキューを設定し、デフォルトはメインスレッド MainQueue に発送します。

```ObjectiveC
/**
* イベントコールバックが配置されているキューの設定
*
* - parameter queueキュー、TRTCChorusの各種ステータス通知コールバックは、指定したqueueに発信されます。
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味          |
| ----- | ---------------- | ----------- |
| queue | dispatch_queue_t | TRTCChorusの各種ステータス通知は、指定したスレッドキューに発信されます。|

   

### login

ログイン

```ObjectiveC
- (void)login:(int)sdkAppID
       userId:(NSString *)userId
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userId:userSig:callback:));

```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味          |
| -------- | -------------- | ----------- |
| sdkAppId | int    | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報の中でSDKAppIDを確認できます。 |
| userId   | String             | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。 |
| userSig  | String         | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallback | ログインのコールバック。成功時にcodeは0になります。                                  |

   

### logout

ログアウト。

```ObjectiveC
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味  |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | ログアウトのコールバック。成功時にcodeは0になります。 |

   

### setSelfProfile

個人情報の修正。

```ObjectiveC
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味       |
| --------- | -------------- | -------------- |
| userName  | String | ニックネーム。 |
| avatarURL | String | プロフィール画像のアドレス。|
| callback | ActionCallback | 個人情報設定のコールバック。成功時にcodeは0になります。                                  |

   


## ルーム関連インターフェース関数

### createRoom

ルームの作成（管理者が呼び出し）。

```ObjectiveC
- (void)createRoom:(int)roomID roomParam:(RoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味          |
| --------- | ------------------- | ----------- |
| roomId    | int   | ルームIDは、ご自身でアサインし、一元管理する必要があります。複数のroomIDを、1つのボイスチャットルームリストにまとめることができます。Tencent Cloudでは現在、ボイスチャットルームリストの管理サービスを行っていませんので、ご自身でボイスチャットルームリストを管理してください。 |
| roomParam | TRTCCreateRoomParam | ルーム情報は、ルーム名、マイク情報、カバー情報など、ルームを説明するために用いる情報に使用します。マイク管理が必要な場合は、ルームのマイク数を記入する必要があります。 |
| callback  | ActionCallback | ルームの作成結果のコールバック。成功時にcodeは0になります。  |

管理者が配信を開始する際の通常の呼び出しプロセスは次のとおりです。 
1. 管理者は、`createRoom`を呼び出して新しいChorusルームを作成します。この時、ルームID、マイク・オンにすることの管理者の確認の要否、マイク数などルームの属性情報を渡します。
2. 管理者は、ルーム作成に成功した後、`enterSeat`を呼び出して参加します。
3. 管理者は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリスト変更をUI上に更新することができます。
4. 管理者は、マイクリストのメンバーが参加した`onAnchorEnterSeat`というイベント通知も受信します。この時、マイク集音は自動的に開始されます。

   

### destroyRoom

ルームの破棄（管理者が呼び出し）。管理者は、ルーム作成後、この関数を呼び出してルームを破棄します。

```ObjectiveC
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                     |
| -------- | -------------- | ---------------- |
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時にcodeは0になります。 |


### enterRoom

入室（リスナーが呼び出し）。

```ObjectiveC
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                     |
| -------- | -------------- | ---------------- |
| roomId   | int    | ルームID。 |
| callback | ActionCallback | 入室結果のコールバック。成功時にcodeは0になります。 |


リスナーが入室し聴取する際の通常の呼び出しプロセスは次のとおりです。 

1. リスナーがサーバーから取得する最新のChorusルームリストには、複数のボイスチャットルームのroomIdおよびルーム情報が含まれる場合があります。
2. リスナーは1つのChorusルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
3. 入室後、コンポーネントの`onRoomInfoChange` ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、発言者にする際の管理者への同意リクエストの要否の記録など。
4. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時にマイクリストの変更をUI上に更新することができます。
5. 入室後にマイクリストにキャスターが参加した`onAnchorEnterSeat`のイベント通知も受信します。

### exitRoom

ルームから退出します。

```ObjectiveC
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                     |
| -------- | -------------- | ---------------- |
| callback | ActionCallback | 退室結果のコールバック。成功時にcodeは0になります。 |

   

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、管理者が`createRoom()`作成時にroomInfoによって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```ObjectiveC
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(ChorusInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ        | 意味       |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | ルームナンバーリスト。|
| callback   | RoomInfoCallback    | ルーム詳細情報のコールバック。 |


### getUserInfoList

指定されたuserIdのユーザー情報を取得します。

```ObjectiveC
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(ChorusUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ       | 意味          |
| ---------------- | ------------------ | ----------- |
| userIdList       | List&lt;String&gt;        |取得すべきユーザーIDリスト。nullの場合は、ルーム内全員の情報を取得します。 |
| userlistcallback | UserListCallback   | ユーザーの詳細情報のコールバック。|


## 音楽再生インターフェース

### startPlayMusic

音楽を再生します（マイク・オン後に呼び出し）。
>?
>- 音楽を再生すると、`onMusicPrepareToPlay`というイベント通知を受信します。
>- 音楽の再生中、ルーム内の全メンバーは、`onMusicProgressUpdate`というイベント通知を継続して受け取ります。
>- 音楽の再生が完了すると、`onMusicCompletePlaying`というイベント通知を受信します。

```ObjectiveC
- (void)startPlayMusic:(int32_t)musicID url:(NSString *)url NS_SWIFT_NAME(startPlayMusic(musicID:url:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味   |
| --------- | -------------- | -------------------- |
| musicID 	| int32_t| 音楽のID。 |
| url       | String         | 音楽の絶対パス。|

このインターフェースを呼び出すと、最後に再生されていた楽曲が停止します。

### stopPlayMusic

音楽の再生を停止します（音楽を再生するときに呼び出します）。
>?再生が停止すると、`onMusicCompletePlaying`というイベント通知を受信します。

```ObjectiveC
- (void)stopPlayMusic NS_SWIFT_NAME(stopPlayMusic());
```

### pausePlayMusic

音楽の再生を一時停止します（音楽を再生するときに呼び出します）。
>? 
>- `onMusicProgressUpdate`というイベント通知が一時停止されます。
>- `onMusicCompletePlaying`というイベント通知を受信しません。

```ObjectiveC
- (void)pausePlayMusic NS_SWIFT_NAME(pausePlayMusic());
```

### resumePlayMusic

一時停止した音楽を再開します（一時停止後に呼び出します）。
>?`onMusicPrepareToPlay`というイベント通知を受信しません。

```ObjectiveC
- (void)resumePlayMusic NS_SWIFT_NAME(resumePlayMusic());
```

## マイク管理インターフェース

### enterSeat

ユーザーが発言者になります（リスナー側/管理者ともに呼び出し可）。

>?マイク・オンの成功後、ルーム内の全メンバーは、`onSeatListChange`および `onAnchorEnterSeat`というイベント通知を受信します。

```ObjectiveC
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味   |
| --------- | -------------- | -------------------- |
| seatIndex | int    | マイク・オンの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。|

このインターフェースを呼び出すと、直ちにマイクリストが変更されます。リスナーによるマイク・オンの申請に管理者の同意が必要となるケースの場合は、まず`sendInvitation`を呼び出してから管理者に申請し、`onInvitationAccept`を受信するとこの関数を呼び出せるようになります。

### leaveSeat

ユーザーが視聴者になる（キャスターが呼び出し）。

>? マイク・オフの成功後、ルーム内の全メンバーは、`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

```ObjectiveC
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味       |
| -------- | -------------- | ---------- |
| callback  | ActionCallback | 操作コールバック。           |

### pickSeat

視聴者が発言できるように招待（管理者が呼び出し）。

>?管理者が視聴者を発言できるように招待すると、ルーム内の全メンバーは、`onSeatListChange`と`onAnchorEnterSeat`というイベント通知を受信します。

```ObjectiveC
- (void)pickSeat:(NSInteger)seatIndex userId:(NSString *)userId callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(seatIndex:userId:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味     |
| --------- | -------------- | ---------------------- |
| seatIndex | int    | 視聴者が発言できるように招待する必要があるマイク番号。 |
| userId    | String | ユーザーID。|
| callback  | ActionCallback | 操作コールバック。|

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。管理者がリスナーの同意がなければマイク・オンできないケースの場合は、まず`sendInvitation`を呼び出してからリスナーに申請し、`onInvitationAccept`を受信すると、この関数を呼び出せるようになります。


### kickSeat

キックアウトしてマイク・オフ（管理者が呼び出し）。

>?管理者がキックアウトしてマイク・オフにすると、ルーム内の全メンバーは、`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

```ObjectiveC
- (void)kickSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(seatIndex:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味     |
| --------- | -------------- | ---------------------- |
| seatIndex | int    | キックアウトしてマイク・オフの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。|

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。

### muteSeat

任意のマイクのミュート/ミュート解除（管理者が呼び出し）。

>? 任意のマイクのミュート/ミュート解除は、ルーム内の全メンバーが`onSeatListChange`および`onSeatMute`というイベント通知を受信します。

```ObjectiveC
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味   |
| --------- | -------------- | ------------------------ |
| seatIndex | int    | 操作の必要があるマイク番号。|
| isMute    | boolean| true：該当するマイクのミュート；false：該当するマイクのミュート解除。 |
| callback  | ActionCallback | 操作コールバック。|

このインターフェースを呼び出すと、直ちにマイクリストが変更されます。seatIndexの座席に該当するキャスターは、muteAudioを自動的に呼び出してミュート/ミュートオフにします。

### closeSeat

任意のマイクのクローズ/解除（管理者が呼び出し）。

>? 管理者は、該当するマイクをクローズ/解除し、ルーム内の全メンバーは`onSeatListChange`および`onSeatClose`というイベント通知を受信します。

```ObjectiveC
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味      |
| --------- | -------------- | --------------------- |
| seatIndex | int    | 操作の必要があるマイク番号。 |
| isClose   | boolean| true：該当するマイクのクローズ； false：該当するマイクのクローズ解除。 |
| callback  | ActionCallback | 操作コールバック。|

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。該当するseatIndexの座席上のキャスターはクローズされ、自動的にマイク・オフになります。


## ローカル音声操作のインターフェース

### startMicrophone

マイクの集音開始。

```ObjectiveC
- (void)startMicrophone;
```

### stopMicrophone

マイクの集音停止。

```ObjectiveC
- (void)stopMicrophone;
```

### setAudioQuality

音質の設定。

```ObjectiveC
- (void)setAuidoQuality:(NSInteger)quality NS_SWIFT_NAME(setAuidoQuality(quality:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ | 意味          |
| ------- | ---- | ----------- |
| quality | int  | 音声品質。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルの音声のミュート/ミュート取り消し。

```ObjectiveC
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味          |
| ---- | ------- | ----------- |
| mute | boolean | ミュート/ミュート取り消し。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |



### setSpeaker

スピーカーの起動設定。

```ObjectiveC
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味  |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true：スピーカー、false：ヘッドホン。|



### setAudioCaptureVolume

マイクの集音音量設定。

```ObjectiveC
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味    |
| ------ | ---- | -------- |
| volume | int  | 集音音量、0 - 100、 デフォルト100。 |


### setAudioPlayoutVolume

再生音量の設定。

```ObjectiveC
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味    |
| ------ | ---- | -------- |
| volume | int  | 再生音量、0 - 100、 デフォルト100。 |

### muteRemoteAudio

指定メンバーのミュート/ミュート解除。

```ObjectiveC
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味        |
| ------ | ------- | ------------ |
| userId | String  | 指定ユーザーID。|
| mute   | boolean   | true：ミュート起動；false：ミュート停止。 |

### muteAllRemoteAudio

全メンバーのミュート/ミュート解除。

```ObjectiveC
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味        |
| ---- | ------- | ------------ |
| mute   | boolean   | true：ミュート起動；false：ミュート停止。 |

### setVoiceEarMonitorEnable

インイヤーモニタリングのオン/オフ。

```ObjectiveC
- (void)setVoiceEarMonitorEnable:(BOOL)enable NS_SWIFT_NAME(setVoiceEarMonitor(enable:));
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味        |
| ---- | ------- | ------------ |
| enable | boolean | true：インイヤーモニタリングをオン。false：インイヤーモニタリングをオフ。 |


## BGMサウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```ObjectiveC
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットに使用します。

```ObjectiveC
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味   |
| -------- | -------------- | -------------- |
| message  | String |テキストメッセージ。|
| callback | ActionCallback | 送信結果のコールバック。|

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。

```ObjectiveC
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味|
| -------- | -------------- | ---------------------- |
| cmd      | String   | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | String |テキストメッセージ。|
| callback | ActionCallback | 送信結果のコールバック。|

   

## 招待シグナリング関連インターフェース

### sendInvitation

ユーザーに招待を送信。

```ObjectiveC
- (NSString *)sendInvitation:(NSString *)cmd
                      userId:(NSString *)userId
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味     |
| -------- | -------------- | ---------------- |
| cmd      | String         | 業務カスタマイズコマンド。 |
| userId   | String | 招待ユーザーID。|
| content  | String | 招待コンテンツ。|
| callback | ActionCallback | 送信結果のコールバック。|

戻り値：

| 戻り値  | タイプ    | 意味    |
| -------- | ------ | --------------------- |
| inviteId | String | 今回の招待IDの識別に使用。 |

### acceptInvitation

招待の同意。

```ObjectiveC
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味   |
| -------- | -------------- | -------------- |
| id   | String | 招待ID。|
| callback | ActionCallback | 送信結果のコールバック。|

### rejectInvitation

招待の拒否。

```ObjectiveC
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味   |
| -------- | -------------- | -------------- |
| id   | String | 招待ID。|
| callback | ActionCallback | 送信結果のコールバック。|


### cancelInvitation

招待の取り消し。

```ObjectiveC
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味   |
| -------- | -------------- | -------------- |
| id   | String | 招待ID。|
| callback | ActionCallback | 送信結果のコールバック。|

[](id:TRTCChorusDelegate)
## TRTCChorusDelegateイベントのコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```ObjectiveC
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code    | int    | エラーコード。|
| message | String | エラーメッセージ。 |


### onWarning

警告のコールバック。

```ObjectiveC
- (void)onWarning:(int)code
                  message:(NSString  *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code    | int    | エラーコード。|
| message | String | 警告メッセージ。 |

   

### onDebugLog

Logコールバック。

```ObjectiveC
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | ログ情報。 |

   


## ルームイベントのコールバック

### onRoomDestroy

ルーム破棄のコールバック。管理者がルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

```ObjectiveC
- (void)onRoomDestroy:(NSString *)message
NS_SWIFT_NAME(onRoomDestroy(message:));
```

パラメータは下表に示すとおりです。

|パラメータ   | タイプ   | 意味      |
| ------ | ------ | --------- |
| roomId | String | ルームID。 |


### onRoomInfoChange

入室に成功後、このインターフェースをコールバックします。roomInfoの情報は、管理者がルームを作成するときに渡されます。

```ObjectiveC
- (void)onRoomInfoChange:(ChorusInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味       |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | ルーム情報。 |


### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。

```ObjectiveC
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味|
| ------ | ------ | ------------------------- |
| userVolumes | List | ユーザーリスト。|
| totalVolume | int    | 音量の大きさ。値：0～100。 |


## マイクコールバック

### onSeatListChange

全量のマイクリストの変更は、全てのマイクリストを含みます。

```ObjectiveC
- (void)onSeatInfoChange:(NSArray<ChorusSeatInfo *> *)seatInfolist
NS_SWIFT_NAME(onSeatListChange(seatInfoList:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味     |
| ------------ | -------------------- | ---------------- |
| seatInfoList | List&lt;SeatInfo&gt; | 全量のマイクリスト。 |

### onAnchorEnterSeat

発言者のメンバーがいます（ユーザーが発言者になる/管理者が視聴者を発言できるように招待）。

```ObjectiveC
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(ChorusUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味   |
| ----- | -------- | -------------------- |
| index | int      | メンバーがマイク・オンのマイク。|
| user  | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onAnchorLeaveSeat

視聴者のメンバーがいます（ユーザーが視聴者になる/管理者がキックアウトしてマイク・オフ）。

```ObjectiveC
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(ChorusUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味   |
| ----- | -------- | -------------------- |
| index | int      | マイク・オフのマイク。         |
| user  | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onSeatMute

管理者のマイクミュート。

```ObjectiveC
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味      |
| ------ | ------- | ------------- |
| index  | int     | 操作するマイク。                       |
| isMute | boolean | true：マイクミュート； false：ミュート解除。 |

### onSeatClose

管理者のマイククローズ。

```ObjectiveC
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味       |
| ------- | ------- | -------------- |
| index   | int     | 操作するマイク。|
| isClose | boolean | true：マイクのクローズ； false：マイクのクローズ解除。 |

## リスナーの入退室イベントのコールバック

### onAudienceEnter

リスナー入室通知の受信。

```ObjectiveC
- (void)onAudienceEnter:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味   |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 入室したリスナーの情報。 |

### onAudienceExit

リスナー退室通知の受信。

```ObjectiveC
- (void)onAudienceExit:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味   |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 退室したリスナーの情報。 |

   

## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```ObjectiveC
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味     |
| -------- | -------- | ---------------- |
| message  | String   | テキストメッセージ。|
| userInfo | UserInfo | 送信者のユーザー情報。 |

   

### onRecvRoomCustomMsg

カスタムメッセージの受信。

```ObjectiveC
- (void)onRecvRoomCustomMsg:(NSString *)cmd
                    message:(NSString  *)message
                   userInfo:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(cmd:message:userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味|
| -------- | -------- | ---------------------- |
| command  | String   | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | String   | テキストメッセージ。|
| userInfo | UserInfo | 送信者のユーザー情報。|

## 招待シグナリングイベントのコールバック

### onReceiveNewInvitation

新規招待リクエストの受信。

```ObjectiveC
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(identifier:inviter:cmd:content:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ     | 意味      |
| ------- | -------- | ------------- |
| id      | String   | 招待ID。|
| inviter | String   | 招待者のユーザーID。|
| cmd     | String   | 業務指定のコマンドワードは、開発者がカスタマイズします。 |
| content | UserInfo | 業務指定のコンテンツ。|

### onInviteeAccepted

被招待者が招待に同意。

```ObjectiveC
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味        |
| ------- | ------ | ------------------- |
| id      | String | 招待ID。|
| invitee    | String | 被招待者のユーザーID。 |

### onInviteeRejected

被招待者による招待の拒否。

```ObjectiveC
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味        |
| ------- | ------ | ------------------- |
| id      | String | 招待ID。|
| invitee    | String | 被招待者のユーザーID。 |

### onInvitationCancelled

招待者が招待を取り消し。

```ObjectiveC
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味      |
| ------- | ------ | ----------------- |
| id      | String | 招待ID。           |
| inviter    | String | 招待者のユーザーID。 |

## 音楽再生ステータスコールバック

### onMusicPrepareToPlay

音楽再生準備のコールバック

```ObjectiveC
- (void)onMusicPrepareToPlay:(int32_t)musicID
NS_SWIFT_NAME(onMusicPrepareToPlay(musicID:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味      |
| ------- | ------- | -------------------- |
| musicID | int32_t | 再生時に渡されたmusicID。|

### onMusicProgressUpdate

楽曲再生進捗度のコールバック

```ObjectiveC
- (void)onMusicProgressUpdate:(int32_t)musicID
                     progress:(NSInteger)progress total:(NSInteger)total
NS_SWIFT_NAME(onMusicProgressUpdate(musicID:progress:total:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味      |
| -------- | --------- | -------------------- |
| musicID  | int32_t   | 再生時に渡されたmusicID。|
| progress | NSInteger | 現在の再生時間。単位： ms。 |
| total    | NSInteger | 合計時間。単位： ms。|

### onMusicCompletePlaying

音楽再生完了のコールバック

```ObjectiveC
- (void)onMusicCompletePlaying:(int32_t)musicID
NS_SWIFT_NAME(onMusicCompletePlaying(musicID:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味      |
| -------- | --------- | -------------------- |
| musicID  | int32_t   | 再生時に渡されたmusicID。|

### onReceiveAnchorSendChorusMsg

管理者から送信されたコーラスメッセージのコールバックを受信します。

```ObjectiveC
- (void)onReceiveAnchorSendChorusMsg:(NSString *)musicId startDelay:(NSInteger)startDelay
NS_SWIFT_NAME(onReceiveAnchorSendChorusMsg(musicId:startDelay:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味      |
| -------- | --------- | -------------------- |
| musicId  | NSString   | コーラスの楽曲musicID。 |
| startDelay  | NSInteger   | コーラスの楽曲の再生が遅延した秒数。  |
