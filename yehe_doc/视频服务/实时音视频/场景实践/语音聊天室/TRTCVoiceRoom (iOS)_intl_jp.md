TRTCVoiceRoomは、Tencent CloudのTencent Real-Time Communication（TRTC）およびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- 管理者が新しいボイスチャットルームを作成して配信を開始し、リスナーがボイスチャットルームに参加して視聴/インタラクティブなコミュニケーションを行います。
- 管理者は、リスナーを招待してマイク・オンにしたり、マイク・オンのキャスターをキックアウトしたりすることもできます。
- 管理者はまた、座席をクローズすることができ、その他のリスナーはマイク・オンを申請することができなくなります。
- リスナーはマイク・オンを申請して、マイク・オンのキャスターになり、他者と音声インタラクションを行うことができます。また、いつでもマイク・オフにして、通常のリスナーになることも可能です。
- 各種のテキストメッセージやカスタマイズメッセージの発信をサポートし、カスタムメッセージは弾幕、「いいね」、ギフトなどに使用することきます。

TRTCVoiceRoomは、オープンソースのClassであり、Tencent Cloudの2つのクローズソースであるSDKに依存しています。具体的な実装プロセスは [ボイスチャットルーム（iOS）](https://intl.cloud.tencent.com/document/product/647/37287)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のボイスチャットコンポーネントとして使用しています。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用してチャットルーム機能を実装します。同時にIMの属性インターフェースによって、マイクリストなどのルーム情報を保存し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。


<h2 id="TRTCVoiceRoom">TRTCVoiceRoom API 概要</h2>

### SDK基本関数

| API                                             | 説明                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを廃棄します。           |
| [setDelegate](#setdelegate)                      | イベントコールバックを設定します。           |
| [setDelegateHandler](#setdelegatehandler)       |イベントのコールバックが配置されているスレッドを設定します。 |
| [login](#login)                                 | ログイン。                   |
| [logout](#logout)                               | ログアウト。                   |
| [setSelfProfile](#setselfprofile)               | 個人情報を修正します。           |

### ルーム関連インターフェース関数

| API                                 | 説明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)               | ルームの作成（管理者が呼び出し）。ルームが存在しない場合は、システムが新しいルームを自動的に作成します。 |
| [destroyRoom](#destroyroom)        | ルームの破棄（管理者が呼び出し）。                                       |
| [enterRoom](#enterroom)                 | 入室（リスナーが呼び出し）。                                       |
| [exitRoom](#exitroom)                   | 退室（リスナーが呼び出し）。                                       |
| [getRoomInfoList](#getroominfolist) | ルームリストの詳細情報を取得します。                              |
| [getUserInfoList](#getuserinfolist) | 指定されたuserIdのユーザー情報を取得します。nilの場合は、ルーム内全員の情報を取得します。 |

### マイク管理インターフェース

| API                     | 説明                                |
| ----------------------- | ----------------------------------- |
| [enterSeat](#enterseat) | ユーザーが発言者になる（リスナー側/管理者ともに呼び出し可）。  |
| [moveSeat](#moveseat)   | マイクの移動 (マイク・オンするキャスター側で呼び出せます) 。 |
| [leaveSeat](#leaveseat) | 自主的にマイク・オフ（キャスターが呼び出し）。    |
| [pickSeat](#pickseat)   | 視聴者が発言できるように招待（管理者が呼び出し）。              |
| [kickSeat](#kickseat)   | キックアウトしてマイク・オフ（管理者が呼び出し）。              |
| [muteSeat](#muteseat)   | 任意のマイクのミュート/ミュート解除（管理者が呼び出し）。 |
| [closeSeat](#closeseat) | 任意のマイクのクローズ/解除（管理者が呼び出し）。     |

### ローカルの音声操作インターフェース

| API                                             | 説明                  |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | マイクの集音開始。     |
| [stopMicrophone](#stopmicrophone)               | マイクの集音停止。     |
| [setAudioQuality](#setaudioquality)             | 音質の設定。           |
| [muteLocalAudio](#mutelocalaudio)               | ローカルオーディオミュートの開始/停止。  |
| [setSpeaker](#setspeaker)                       | スピーカーの起動設定。     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | マイクの集音音量設定。|
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 再生音量の設定。       |
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | インイヤーモニタリングのオン/オフ。       |


### リモートユーザー音声操作インターフェース

| API                                       | 説明                    |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | 指定メンバーをミュート/ミュート解除。 |
| [muteAllRemoteAudio](#muteallremoteaudio) | 全メンバーをミュート/ミュート解除。 |

### BGMサウンドエフェクト関連インターフェース

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | BGMサウンドエフェクト管理オブジェクト[TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager)の取得。 |

### メッセージ送信関連インターフェース

| API                                     | 説明                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージのブロードキャスト。通常、弾幕によるチャットに使用します。|
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを送信します。                     |

### 招待シグナリング関連インターフェース

| API                                   | 説明             |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | ユーザーに招待を送信。 |
| [acceptInvitation](#acceptinvitation) | 招待の同意。       |
| [rejectInvitation](#rejectinvitation) | 招待の辞退。       |
| [cancelInvitation](#cancelinvitation) | 招待の取り消し。       |

<h2 id="TRTCVoiceRoomDelegate">TRTCVoiceRoomDelegate API概要</h2>

### 一般的なイベントコールバック

| API                       | 説明       |
| ------------------------- | ---------- |
| [onError](#onerror) | エラーのコールバック。 |
| [onWarning](#onwarning)   | 警告のコールバック。 |
| [onDebugLog](#ondebuglog) | Logコールバック。|

### ルームイベントのコールバック

| API                                       | 説明                   |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | ルームが廃棄された時のコールバック。     |
| [onRoomInfoChange](#onroominfochange) | ボイスチャットルーム情報変更のコールバック。|
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。     |

### マイク変更コールバック

| API                                     | 説明                                |
| --------------------------------------- | ------------------------------------- |
| [onSeatListChange](#onseatlistchange)   |全量のマイクリストの変更。                |
| [onAnchorEnterSeat](#onanchorenterseat) | 発言者のメンバーがいます（ユーザーが発言者になる/管理者が視聴者を発言できるように招待）。 |
| [onAnchorLeaveSeat](#onanchorleaveseat) | 視聴者のメンバーがいます（ユーザーが視聴者になる/管理者がキックアウトしてマイク・オフ）。 |
| [onSeatMute](#onseatmute)               | 管理者のマイクミュート。                          |
| [onUserMicrophoneMute](#onusermicrophonemute)               | ユーザーのマイクがミュートされているかどうか。                          |
| [onSeatClose](#onseatclose)             | 管理者のマイククローズ。                          |

### リスナーの入退室イベントのコールバック

| API                                 | 説明               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | リスナー入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | リスナー退室通知の受信。|

### メッセージイベントのコールバック

| API                                         | 説明             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | テキストメッセージの受信。   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージの受信。|

### シグナリングイベントのコールバック

| API                                               | 説明             |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 新規招待リクエストの受信。   |
| [onInviteeAccepted](#oninviteeaccepted)           | 被招待者が招待に同意。   |
| [onInviteeRejected](#oninviteerejected)           | 被招待者が招待を拒否。   |
| [onInvitationCancelled](#oninvitationcancelled)   | 招待者が招待を取り消し。   |

## SDK基本関数

[](id:sharedInstance)

### sharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) シングルトンオブジェクトを取得します。

```Objective-C
/**
* TRTCVoiceRoom シングルトンオブジェクトの取得
*
* - returns: TRTCVoiceRoom インスタンス
* - note: {@link TRTCVoiceRoom#destroySharedInstance()}を呼び出してシングルトンオブジェクトを破棄することができます
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) シングルトンオブジェクトを破棄します。

>?インスタンスの破棄後は、外部にキャッシュされた TRTCVoiceRoomインスタンスの再使用ができません。改めて [sharedInstance](#sharedInstance) を呼び出し、インスタンスを新規取得する必要があります。

```Objective-C
/**
* TRTCVoiceRoom のシングルトンオブジェクトの破棄
*
* - note: インスタンスの破棄後は、外部にキャッシュされたTRTCVoiceRoomインスタンスの再使用ができません。改めて {@link TRTCVoiceRoom#sharedInstance()} を呼び出し、インスタンスを新規取得する必要があります
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) イベントコールバック、 TRTCVoiceRoomDelegate を介して [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) の各種ステータス通知を受け取ることができます。

```Objective-C
/**
* コンポーネントコールバックインターフェースの設定
* 
* TRTCVoiceRoomDelegate によって TRTCVoiceRoom の各種ステータス通知を取得することができます
*
* - parameter delegateコールバックインターフェース
* - note: TRTCVoiceRoomのコールバックイベントは、デフォルトではMain Queueでコールバックされます。イベントのコールバックが配置されているキューを指定する必要がある場合は、 {@link TRTCVoiceRoom#setDelegateQueue(queue)}を使用することができます
*/
- (void)setDelegate:(id<TRTCVoiceRoomDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?setDelegate は、 TRTCVoiceRoom のプロキシコールバックです。   

### setDelegateQueue

イベントコールバックが所在するスレッドキューを設定し、デフォルトはメインスレッド MainQueue に発送します。

```Objective-C
/**
* イベントコールバックが配置されているキューの設定
*
* - parameter queueキュー，TRTCVoiceRoomの各種ステータス通知コールバックは、指定したqueueに発信されます。
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ             | 意味                                                       |
| ----- | ---------------- | ------------------------------------------------------------ |
| パラメータ  | タイプ             | 意味                                                       |
| queue | dispatch_queue_t | TRTCVoiceRoomの各種ステータス通知は、指定したスレッドキューに発信されます。|

   

### login

ログイン

```Objective-C
- (void)login:(int)sdkAppID
       userId:(NSString *)userId
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userId:userSig:callback:));

```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int            | **TRTCコンソール >[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)**> アプリケーション情報でSDKAppIDを確認できます。 |
| userId   | NSString       | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。 |
| userSig  | NSString       | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallback | ログインのコールバック。成功時にcodeは0になります。                                  |

   

### logout

ログアウト。

```Objective-C
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                        |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | ログアウトのコールバック。成功時にcodeは0になります。 |

   

### setSelfProfile

個人情報の修正。

```Objective-C
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                |
| --------- | -------------- | ----------------------------------- |
| userName  | NSString       | ニックネーム。                              |
| avatarURL | NSString       | プロフィール画像のアドレス。                          |
| callback | ActionCallback | 個人情報設定のコールバック。成功時にcodeは0になります。                                  |

   


## ルーム関連インターフェース関数

### createRoom

ルームの作成（管理者が呼び出し）。

```Objective-C
- (void)createRoom:(int)roomID roomParam:(VoiceRoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                | 意味                                                         |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomId | int | ルームIDは、ご自身でアサインし、一元管理する必要があります。複数のroomIDを、1つのボイスチャットルームリストにまとめることができます。Tencent Cloudでは現在、ボイスチャットルームリストの管理サービスを行っていませんので、ご自身でボイスチャットルームリストを管理してください。 |
| roomParam | VoiceRoomParam | ルーム情報は、ルーム名、マイク情報、カバー情報など、ルームを説明するために用いる情報に使用します。マイク管理が必要な場合は、ルームのマイク数を入力する必要があります。 |
| callback | ActionCallback | ルームの新規作成結果のコールバック。成功時にcodeは0になります。                                  |

管理者が配信を開始する際の通常の呼び出しプロセスは次のとおりです。 
1. 管理者は、`createRoom`を呼び出して新しいボイスチャットルームを作成します。この時にルームID、マイク・オンに管理者の確認の要否、マイク数などルームのプロパティ情報を渡します。
2. 管理者は、ルーム作成に成功した後、`enterSeat`を呼び出して参加します。
3. 管理者は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリスト変更をUI上に更新することができます。
4. 管理者は、マイクリストのメンバーが参加した`onAnchorEnterSeat`というイベント通知も受信します。この時、マイク集音は自動的に開始されます。

   

### destroyRoom

ルームの破棄（管理者が呼び出し）。管理者は、ルーム作成後、この関数を呼び出してルームを破棄します。

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時にcodeは0になります。 |


### enterRoom

入室（リスナーが呼び出し）。

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | NSInteger            | ルームID。                            |
| callback | ActionCallback | 入室結果のコールバック。成功時にcodeは0になります。 |


リスナーが入室し聴取する際の通常の呼び出しプロセスは次のとおりです。 

1. リスナーがサーバーから取得する最新のボイスチャットルームリストには、多くのボイスチャットルームのroomIdおよびルーム情報が含まれる場合があります。
2．リスナーが1つのボイスチャットルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
3. 入室後、コンポーネントの`onRoomInfoChange` ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、発言者にする際の管理者への同意リクエストの要否の記録など。
4. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時にマイクリストの変更をUI上に更新することができます。
5. 入室後にマイクリストにキャスターが参加した`onAnchorEnterSeat`のイベント通知も受信します。

### exitRoom

ルームから退出します。

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 退室結果のコールバック。成功時にcodeは0になります。 |

   

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、管理者が`createRoom()`作成時にroomInfoによって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(VoiceRoomInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味               |
| ---------- | ------------------- | ------------------ |
| roomIdList | NSArray&lt;NSNumber&gt; | ルームナンバーリスト。       |
| callback   | RoomInfoCallback    | ルーム詳細情報のコールバック。 |


### getUserInfoList

指定されたuserIdのユーザー情報を取得します。

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(VoiceRoomUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                      | 意味                                                       |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | NSArray&lt;NSString&gt; | 取得すべきユーザーIDリスト。nullの場合は、ルーム内全員の情報を取得します。 |
| userlistcallback | UserListCallback   | ユーザーの詳細情報のコールバック。                                          |


## マイク管理インターフェース

### enterSeat

ユーザーが発言者になります（リスナー側/管理者ともに呼び出し可）。

>?マイク・オンの成功後、ルーム内の全メンバーは、`onSeatListChange`および `onAnchorEnterSeat`というイベント通知を受信します。

```Objective-C
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                 |
| --------- | -------------- | -------------------- |
| seatIndex | NSInteger      | マイク・オンの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。           |

このインターフェースを呼び出すと、直ちにマイクリストが変更されます。リスナーによるマイク・オンの申請に管理者の同意が必要となるケースの場合は、まず`sendInvitation`を呼び出してから管理者に申請し、`onInvitationAccept`を受信するとこの関数を呼び出せるようになります。

### moveSeat
マイクの移動 (マイク・オンするキャスター側で呼び出せます)。
>? マイクの移動に成功したら、ルーム内のすべてのメンバーが`onSeatListChange`、`onAnchorLeaveSeat`、`onAnchorEnterSeat`のイベント通知を受け取ります。(キャスターが呼び出した後に変更できるのは、マイクのシート番号情報のみで、ユーザーのキャスターロールを切り替えることはできません。)

```Objective-C
- (NSInteger)moveSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback
NS_SWIFT_NAME(moveSeat(seatIndex:callback:))
```
パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                 |
| --------- | -------------- | -------------------- |
| seatIndex | NSInteger      | 移動の必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。           |

戻り値：

| 戻り値   | タイプ   | 意味                  |
| -------- | --------- | --------------------- |
| code     | NSInteger | マイク移動操作の結果（0は成功、その他は失敗、10001はインターフェース呼び出し頻度制限）。 |

このインターフェースを呼び出すと、直ちにマイクリストが変更されます。リスナーによるマイク・オンの申請に管理者の同意が必要となるケースの場合は、まず`sendInvitation`を呼び出してから管理者に申請し、`onInvitationAccept`を受信するとこの関数を呼び出せるようになります。

### leaveSeat

ユーザーが視聴者になる（キャスターが呼び出し）。

>? マイク・オフの成功後、ルーム内の全メンバーは、`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback  | ActionCallback | 操作コールバック。|

### pickSeat

視聴者が発言できるように招待（管理者が呼び出し）。

>?管理者が視聴者を発言できるように招待すると、ルーム内の全メンバーは、`onSeatListChange`と`onAnchorEnterSeat`というイベント通知を受信します。

```Objective-C
- (void)pickSeat:(NSInteger)seatIndex userId:(NSString *)userId callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(seatIndex:userId:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | NSInteger      |  マイク・オンの必要があるマイク番号。 |
| userId    | NSString       | ユーザーID。              |
| callback  | ActionCallback | 操作コールバック。             |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。管理者がリスナーの同意がなければマイク・オンできないケースの場合は、まず`sendInvitation`を呼び出してからリスナーに申請し、`onInvitationAccept`を受信すると、この関数を呼び出せるようになります。


### kickSeat

キックアウトしてマイク・オフ（管理者が呼び出し）。

>?管理者がキックアウトしてマイク・オフにすると、ルーム内の全メンバーは、`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

```Objective-C
- (void)kickSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(seatIndex:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | NSInteger      | キックアウトしてマイク・オフの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。             |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。

### muteSeat

任意のマイクのミュート/ミュート解除（管理者が呼び出し）。

>? 任意のマイクのミュート/ミュート解除は、ルーム内の全メンバーが`onSeatListChange`および`onSeatMute`というイベント通知を受信します。

```Objective-C
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                          |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | NSInteger      | 操作が必要なマイク番号。                          |
| isMute    | BOOL           | YES：該当するマイクのミュート；NO：該当するマイクのミュート解除。 |
| callback  | ActionCallback | 操作コールバック。                                    |

このインターフェースを呼び出すと、直ちにマイクリストが変更されます。seatIndexの座席に該当するキャスターは、muteAudioを自動的に呼び出してミュート/ミュートオフにします。

### closeSeat

任意のマイクのクローズ/解除（管理者が呼び出し）。

>? 管理者は、該当するマイクをクローズ/解除し、ルーム内の全メンバーは`onSeatListChange`および`onSeatClose`というイベント通知を受信します。

```Objective-C
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                       |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | NSInteger      | 操作が必要なマイク番号。                       |
| isClose   | BOOL           | YES：該当するマイクのクローズ； NO：該当するマイクのクローズ解除。 |
| callback  | ActionCallback | 操作コールバック。                                 |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。該当するseatIndexの座席上のキャスターはクローズされ、自動的にマイク・オフになります。


## ローカル音声操作のインターフェース

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

| パラメータ    | タイプ             | 意味                                                         |
| ------- | ---------- | ------------------------------------------------------------ |
| quality | NSInteger  | オーディオ品質。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルの音声のミュート/ミュート取り消し。

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ    | 意味                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | BOOL    | ミュート/ミュートの取り消し。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |



### setSpeaker

スピーカーの起動設定。

```Objective-C
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | BOOL    | YES：スピーカー；NO：ヘッドホン。 |



### setAudioCaptureVolume

マイクの集音音量設定。

```Objective-C
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                          |
| ------ | ---- | ----------------------------- |
| volume | NSInteger  | 集音音量、0 - 100、デフォルト100。 |


### setAudioPlayoutVolume

再生音量の設定。

```Objective-C
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                          |
| ------ | ---------- | ----------------------------- |
| volume | NSInteger  | 再生音量、0 - 100、デフォルト100。 |

### muteRemoteAudio

指定メンバーのミュート/ミュート解除。

```Objective-C
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                              |
| ------ | ------- | --------------------------------- |
| userId | NSString  | 指定のユーザーID。                   |
| mute   | BOOL      | YES：ミュート起動；NO：ミュート停止。 |

### muteAllRemoteAudio

全メンバーのミュート/ミュート解除。

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | BOOL | YES：ミュート起動；NO：ミュート停止。 |

### setVoiceEarMonitorEnable

インイヤーモニタリングのオン/オフ。

```Objective-C
- (void)setVoiceEarMonitorEnable:(BOOL)enable NS_SWIFT_NAME(setVoiceEarMonitor(enable:));
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                              |
| ---- | ------- | --------------------------------- |
| enable | BOOL | YES：インイヤーモニタリング起動；NO：インイヤーモニタリング停止。 |


## BGMサウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```Objective-C
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットに使用します。

```Objective-C
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| message  | NSString       | テキストメッセージ。     |
| callback | ActionCallback | 送信結果のコールバック。|

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。

```Objective-C
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | NSString        | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | NSString        | テキストメッセージ。                                         |
| callback  | ActionCallback | 送信結果のコールバック。                                    |

   

## 招待シグナリング関連インターフェース

### sendInvitation

ユーザーに招待を送信。

```Objective-C
- (NSString *)sendInvitation:(NSString *)cmd
                      userId:(NSString *)userId
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味             |
| -------- | -------------- | ---------------- |
| cmd      | NSString       | 業務カスタマイズコマンド。 |
| userId   | NSString       | 招待するユーザーID。  |
| content  | NSString       | 招待するコンテンツ。     |
| callback  | ActionCallback | 送信結果のコールバック。   |

戻り値：

| 戻り値   | タイプ   | 意味                  |
| -------- | ------ | --------------------- |
| inviteId | NSString | 今回の招待IDの識別に使用。 |

### acceptInvitation

招待の同意。

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(id:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | NSString       |招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。|

### rejectInvitation

招待の拒否。

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(id:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | NSString       |招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。|


### cancelInvitation

招待の取り消し。

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(id:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | NSString       |招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。|

[](id:TRTCVoiceRoomDelegate)
## TRTCVoiceRoomDelegateイベントのコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```Objective-C
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message | NSString  | エラー情報。 |


### onWarning

警告のコールバック。

```Objective-C
- (void)onWarning:(int)code
                  message:(NSString  *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message | NSString | 警告メッセージ。 |

   

### onDebugLog

Logコールバック。

```Objective-C
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | NSString | ログ情報。 |

   


## ルームイベントのコールバック

### onRoomDestroy

ルーム破棄のコールバック。管理者がルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

```Objective-C
- (void)onRoomDestroy:(NSString *)roomId
NS_SWIFT_NAME(onRoomDestroy(roomId:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味      |
| ------ | ------ | --------- |
| roomId | NSString | ルーム ID。 |


### onRoomInfoChange

入室に成功後、このインターフェースをコールバックします。roomInfoの情報は、管理者がルームを作成するときに渡されます。

```Objective-C
- (void)onRoomInfoChange:(VoiceRoomInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味       |
| -------- | -------- | ---------- |
| roomInfo | VoiceRoomInfo | ルーム情報。 |


### onUserMicrophoneMute

ユーザーのマイクがミュートになっているかどうかについて、ユーザーがmuteLocalAudioを呼び出すと、ルームの他のユーザーがこの通知を受信します。

```Objective-C
- (void)onUserMicrophoneMute:(NSString *)userId mute:(BOOL)mute
NS_SWIFT_NAME(onUserMicrophoneMute(userId:mute:));

```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                      |
| ------ | ------ | ------------------------- |
| userId | NSString  | ユーザーID 。           |
| mute | BOOL    | YES：マイクミュート； NO：ミュート解除。 |


### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。

```Objective-C
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                      |
| ------ | ------ | ------------------------- |
| userVolumes | NSArray | ユーザーリスト。                 |
| totalVolume | NSInteger    | 音量の大きさ。値：0 - 100。 |


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
| seatInfoList | NSArray&lt;VoiceRoomSeatInfo&gt; | 全量のマイクリスト。 |

### onAnchorEnterSeat

発言者のメンバーがいます（ユーザーが発言者になる/管理者が視聴者を発言できるように招待）。

```Objective-C
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | NSInteger      | メンバーがマイク・オンするマイク。     |
| user  | VoiceRoomUserInfo |  マイク・オンユーザーの詳細情報。 |

### onAnchorLeaveSeat

視聴者のメンバーがいます（ユーザーが視聴者になる/管理者がキックアウトしてマイク・オフ）。

```Objective-C
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | NSInteger      | マイク・オフのマイク。         |
| user  | VoiceRoomUserInfo |  マイク・オンユーザーの詳細情報。 |

### onSeatMute

管理者のマイクミュート。

```Objective-C
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                               |
| ------ | ------- | ---------------------------------- |
| index  | NSInteger     | 操作するマイク。                       |
| isMute | BOOL | YES：マイクミュート； NO：ミュート解除。 |

### onSeatClose

管理者のマイククローズ。

```Objective-C
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                |
| ------- | ------- | ----------------------------------- |
| index   | NSInteger     | 操作するマイク。                        |
| isClose | BOOL | YES：マイクのクローズ； NO： マイクのクローズ解除。 |

## リスナーの入退室イベントのコールバック

### onAudienceEnter

リスナー入室通知の受信。

```Objective-C
- (void)onAudienceEnter:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | VoiceRoomUserInfo | 入室したリスナーの情報。 |

### onAudienceExit

リスナー退室通知の受信。

```Objective-C
- (void)onAudienceExit:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | VoiceRoomUserInfo | 退室したリスナーの情報。 |

   

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
| message  | NSString   | テキストメッセージ。       |
| userInfo | VoiceRoomUserInfo | 送信者のユーザー情報。 |

   

### onRecvRoomCustomMsg

カスタムメッセージの受信。

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)command
                    message:(NSString  *)message
                   userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(command:message:userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味                                               |
| -------- | -------- | -------------------------------------------------- |
| command  | NSString   | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | NSString   | テキストメッセージ。                                         |
| userInfo | VoiceRoomUserInfo | 送信者のユーザー情報。                                   |

## 招待シグナリングイベントのコールバック

### onReceiveNewInvitation

新規招待リクエストの受信。

```Objective-C
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(id:inviter:cmd:content:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ     | 意味                               |
| ------- | -------- | ---------------------------------- |
| id      | NSString   |招待ID。                          |
| inviter | NSString   | 招待者のユーザーID。                  |
| cmd     | NSString   | 業務指定のコマンドワードは、開発者がカスタマイズします。 |
| content | NSString | 業務指定のコンテンツ。                   |

### onInviteeAccepted

被招待者が招待に同意。

```Objective-C
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(id:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | NSString | 招待ID。           |
| invitee | NSString | 被招待者のユーザーID。 |

### onInviteeRejected

被招待者による招待の拒否。

```Objective-C
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(id:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | NSString | 招待ID。           |
| invitee | NSString | 被招待者のユーザーID。 |

### onInvitationCancelled

招待者が招待を取り消し。

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(id:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味              |
| ------- | ------ | ----------------- |
| id      | NSString |招待ID。         |
| inviter | NSString | 招待者のユーザーID。 |
