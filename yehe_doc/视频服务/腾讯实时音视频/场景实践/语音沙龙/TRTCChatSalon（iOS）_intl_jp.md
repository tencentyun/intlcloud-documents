TRTCChatSalonは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- キャスターは新しいボイスサロンを作成して配信を開始し、視聴者はボイスサロンに参加して視聴/インタラクティブなコミュニケーションを行います。
- キャスターは、視聴者をマイク・オンに招待したり、マイク・オンのキャスターをキックアウトしたりすることもできます。
- 視聴者はマイク・オンを申請して、マイク・オンのキャスターになり、他者と対話することができます。また、いつでもマイク・オフにして、通常の視聴者になることも可能です。
- 各種のテキストメッセージやカスタマイズメッセージの発信をサポートし、カスタムメッセージは弾幕、「いいね」、ギフトなどに使用することきます。

TRTCChatSalonは、オープンソースのClassであり、Tencent Cloudの2つのクローズドソースであるSDKに依存しています。具体的な実装プロセスは、[ボイスサロン（iOS）](https://intl.cloud.tencent.com/document/product/647/39804)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のボイスチャットコンポーネントとして使用しています。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用してチャットルーム機能を実装します。同時にIMの属性インターフェースによって、マイクリストなどのルーム情報を保存し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。


[](id:TRTCChatSalon)

## TRTCChatSalon API概要

### SDK基本関数

| API                                             | 説明                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを廃棄します。           |
| [setDelegate](#setdelegate)                      | イベントコールバックを設定します。           |
| [delegateQueue](#delegatequeue)   | イベントコールバックが配置されているスレッドを設定します。 |
| [login](#login)                                 | ログイン。                   |
| [logout](#logout)                               | ログアウト。                   |
| [setSelfProfile](#setselfprofile)               | 個人情報を修正します。           |

### ルーム関連インターフェース関数

| API                                 | 説明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)           | ルームの新規作成（キャスターが呼び出し）。ルームが存在しない場合は、システムが新しいルームを自動作成します。｜
| [destroyRoom](#destroyroom)         | ルームの廃棄（キャスターが呼び出し）。                                       |
| [enterRoom](#enterroom)             | 入室（視聴者が呼び出し）。                                       |
| [exitRoom](#exitroom)               | 退室（視聴者が呼び出し）。                                       |
| [getRoomInfoList](#getroominfolist) | ルームリストの詳細情報を取得します。                              |
| [getUserInfoList](#getuserinfolist) | 指定されたuserIdのユーザー情報を取得します。nilの場合は、ルーム内全員の情報を取得します。 |

### マイクのオン・オフインターフェース

| API                     | 説明                               |
| ----------------------- | ---------------------------------- |
| [enterSeat](#enterseat) | 自主的にマイク・オン（視聴者/キャスターともに呼び出し可）。 |
| [leaveSeat](#leaveseat) | 自主的にマイク・オフ（視聴者/キャスターともに呼び出し可）。 |
| [pickSeat](#pickseat)   | ピックしてマイク・オン（キャスターが呼び出し）。             |
| [kickSeat](#kickseat)   | キックアウトしてマイク・オフ（キャスターが呼び出し）。                  |

### ローカルの音声操作インターフェース

| API                                             | 説明                  |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | マイクの集音開始。     |
| [stopMicrophone](#stopmicrophone)               | マイクの集音停止。     |
| [setAudioQuality](#setaudioquality)             | 音質の設定。           |
| [muteLocalAudio](#mutelocalaudio)               | ローカルオーディオミュートの開始/停止。  |
| [setSpeaker](#setspeaker)                       | スピーカーの起動設定。     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | マイクの集音音量設定。 |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 再生音量の設定。       |


### リモートユーザー音声操作インターフェース

| API                                       | 説明                    |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | 指定メンバーをミュート/ミュート解除。 |
| [muteAllRemoteAudio](#muteallremoteaudio) | 全メンバーをミュート/ミュート解除。 |

### BGMサウンドエフェクト関連インターフェース

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | BGMサウンドエフェクト管理オブジェクト [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。 |

### メッセージ送信関連インターフェース

| API                                     | 説明                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージのブロードキャスト。通常、弾幕によるチャットに使用します。｜
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを送信します。                     |

### 招待シグナリング関連インターフェース

| API                                  | 説明             |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | ユーザーに招待を送信。 |
| [acceptInvitation](#acceptinvitation) | 招待の同意。       |
| [rejectInvitation](#rejectinvitation) | 招待の辞退。       |
| [cancelInvitation](#cancelinvitation) | 招待の取り消し。       |

[](id:TRTCChatSalonDelegate)

## TRTCChatSalonDelegate API概要

### 一般的なイベントコールバック

| API                       | 説明       |
| ------------------------- | ---------- |
| [onError](#onerror) | エラーのコールバック。 |
| [onWarning](#onwarning)   | 警告のコールバック。 |
| [onDebugLog](#ondebuglog) | Logコールバック。 |

### ルームイベントのコールバック

| API                                       | 説明                   |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | ルームが廃棄された時のコールバック。     |
| [onRoomInfoChange](#onroominfochange) | ボイスチャットルーム情報変更のコールバック。|
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。     |

### マイク変更コールバック

| API                                     | 説明                                  |
| --------------------------------------- | ------------------------------------- |
| [onAnchorEnterSeat](#onanchorenterseat) | マイク・オンのメンバーがいます（自主的にマイク・オン/キャスターがピックしてマイク・オン）。 |
| [onAnchorLeaveSeat](#onanchorleaveseat) | マイク・オフのメンバーがいます（自主的にマイク・オフ/キャスターがキックアウトしてマイク・オフ）。 |
| [onSeatMute](#onseatmute)               | キャスターのマイクミュート。                            |

### 視聴者の入退室イベントのコールバック

| API                                 | 説明               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) |視聴者入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | 視聴者退室通知の受信。|

### メッセージイベントのコールバック

| API                                         | 説明             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | テキストメッセージの受信。   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージの受信。 |

### シグナリングイベントのコールバック

| API                                               | 説明               |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 新規招待リクエストの受信。 |
| [onInviteeAccepted](#oninviteeaccepted)           | 被招待者が招待に同意。 |
| [onInviteeRejected](#oninviteerejected)           | 被招待者による招待の辞退。 |
| [onInvitationCancelled](#oninvitationcancelled)   | 招待者が招待を取り消し。   |

## SDK基本関数

[](id:sharedInstance)

### sharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804)シングルトンオブジェクトを取得します。

```Objective-C
/**
* TRTCChatSalonシングルトンオブジェクトを取得します
*
* - returns: TRTCChatSalonインスタンス
* - note: {@link TRTCChatSalon#destroySharedInstance()}を呼び出してシングルトンオブジェクトを廃棄することができます
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804)シングルトンオブジェクトを廃棄します。

>?インスタンスを廃棄すると、外部キャッシュのTRTCChatSalonインスタンスは再利用できなくなります。あらためて[sharedInstance](#sharedInstance)を呼び出し、新しいインスタンスを取得する必要があります。

```Objective-C
/**
* TRTCChatSalonシングルトンオブジェクトを廃棄します
*
* - note: インスタンスの廃棄後、外部にキャッシュされた TRTCChatSalonインスタンスは再利用できなくなります。あらためて{@link TRTCChatSalon#sharedInstance()}を呼び出し、新しいインスタンスを取得する必要があります
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804)イベントコールバック。TRTCChatSalonDelegateを介して[TRTCChatSalon][TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804)の各種ステータス通知を受け取ることができます。

```Objective-C
/**
* コンポーネントコールバックインターフェースの設定
* 
* TRTCChatSalonDelegateを介してTRTCChatSalonの各種ステータス通知を受け取ることができます
*
* - parameter delegateコールバックインターフェース
* - note: TRTCChatSalonのコールバックイベントは、デフォルトではMain Queueでコールバックされます。イベントのコールバックが配置されているキューを指定する必要がある場合は、 {@link TRTCChatSalon#setDelegateQueue(queue)}を使用することができます
*/
- (void)setDelegate:(id<TRTCChatSalonDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?setDelegateはTRTCChatSalonのプロキシコールバックです。   

### setDelegateQueue

イベントコールバックが配置されているスレッドキューを設定します。デフォルトでは、メインスレッドMainQueueに送信されます。

```Objective-C
/**
* イベントコールバックが配置されているキューの設定
*
* - parameter queueキュー、TRTCChatSalonの各種ステータス通知コールバックは、指定したqueueに発信されます。
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ             | 意味                                                       |
| ----- | ---------------- | ------------------------------------------------------------ |
| queue | dispatch_queue_t | TRTCChatSalonの各種ステータス通知は、指定したスレッドキューに発信されます。|

   

### login

ログイン。

```Objective-C
- (void)login:(int)sdkAppID
       userID:(NSString *)userID
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userID:userSig:callback:));

```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int         | TRTCコンソール> 【[アプリケーション管理]（https://console.cloud.tencent.com/trtc/app）】>アプリケーション情報の中でSDKAppIDを確認できます。 |
| userId   | String                | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String         | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
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
| userName  | String         | ニックネーム。                              |
| avatarURL | String         | プロフィール画像のアドレス。                          |
| callback | ActionCallback | 個人情報設定のコールバック。成功時にcodeは0になります。                                  |

   


## ルーム関連インターフェース関数

### createRoom

ルームの新規作成（キャスターが呼び出し）。

```Objective-C
- (void)createRoom:(int)roomID roomParam:(ChatSalonParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                                        |
| --------- | -------------- | ------------------------------------------------------------ |
| roomI    | int            | ルームIDは、ご自身でアサインし、統一管理する必要があります。複数のroomIDを、一つのボイスチャットルームリストにまとめることができます。Tencent Cloudでは現在、ボイスチャットルームリストの管理サービスを行っていませんので、ご自身でボイスチャットルームリストを管理してください。 |
| roomParam | ChatSalonParam | ルーム情報は、ルームについて説明するための情報です。例えば、ルーム名、マイク情報、カバー情報などです。 |
| callback  | ActionCallback | ルームの新規作成結果のコールバック。成功時にcodeは0になります。 |

キャスターがブロードキャストを開始する際の通常の呼び出しプロセスは次のとおりです。 
1. キャスターは、 `createRoom`を呼び出して新しいボイスチャットルームを作成します。この時にルームID、マイク・オンにキャスターの確認の要否などルームのプロパティ情報を渡します。
2. キャスターは、ルーム作成の成功後、`enterSeat` を呼び出して参加します。
3. キャスターは、マイクリストのメンバーが参加した`onAnchorEnterSeat`のイベント通知も受信します。このとき、マイク集音は自動的に開始されます。

   

### destroyRoom

ルームの廃棄（キャスターが呼び出し）。キャスターは、ルーム作成後、この関数を呼び出してルームを廃棄します。

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時にcodeは0になります。 |


### enterRoom

入室（視聴者が呼び出し）

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | int            | ルームID。                            |
| callback | ActionCallback | 入室結果のコールバック。成功時にcodeは0になります。 |


視聴者が入室し視聴する際の通常の呼び出しプロセスは次のとおりです。 

1. 視聴者がサーバーから取得する最新のボイスサロンリストには、多くのボイスサロンのroomIdおよびルーム情報が含まれる場合があります。
2．視聴者は一つのボイスチャットルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
3. 入室後、コンポーネントの`onRoomInfoChange` ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、マイク・オンの際のキャスターへの同意リクエストの要否の記録など。
4. 入室後に、マイクリストにキャスターが参加した `onAnchorEnterSeat`のイベント通知も受信します。

### exitRoom

ルームを退出します。

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 退室結果のコールバック。成功時にcodeは0になります。 |

   

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、キャスターが`createRoom()`作成時にroomInfoによって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(ChatSalonInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                  | 意味               |
| ---------- | --------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt;   | ルームナンバーリスト。       |
| callback   | ChatSalonInfoCallback | ルーム詳細情報のコールバック。 |


### getUserInfoList

指定されたuserIdのユーザー情報を取得します。

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(ChatSalonUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ                      | 意味                                                         |
| ---------------- | ------------------------- | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt;        |取得すべきユーザーIDリスト。nullの場合は、ルーム内全員の情報を取得します。 |
| userlistcallback | ChatSalonUserListCallback | ユーザーの詳細情報のコールバック。                                           |


## マイクのオン・オフインターフェース

### enterSeat

自主的にマイク・オン（視聴者/キャスターともに呼び出し可）します。

>?マイク・オンが成功した後、ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。

```Objective-C
- (void)enterSeat:(ActionCallback _Nullable)callback
NS_SWIFT_NAME(enterSeat(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 操作コールバック。 |

このインターフェースを呼び出すと、すぐにマイクリストが変更されます。視聴者がキャスターからの申請を必要とするシーンの場合は、まず`sendInvitation`を呼び出してキャスターに申請し、`onInvitationAccept `を受信した後にこの関数を呼び出すことができます。

### leaveSeat

自主的にマイク・オフ（視聴者/キャスターともに呼び出し可）します。

>? マイク・オフが成功した後、ルーム内の全メンバーは`onAnchorLeaveSeat`のイベント通知を受信します。

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 操作コールバック。 |

### pickSeat

ピックしてマイク・オン（キャスターが呼び出し）。

>? キャスターがピックしてマイク・オンにすると、ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。

```Objective-C
- (void)pickSeat:(NSString *)userID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(userID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| userID   | String         | ユーザーID 。  |
| callback | ActionCallback | 操作コールバック。 |

このインターフェースを呼び出すと、すぐにマイクリストが変更されます。キャスターが、視聴者の同意がなければマイク・オンできないユースケースの場合は、まず `sendInvitation` を呼び出してから視聴者にリクエストし、 `onInvitationAccept `を受信した後にこの関数を呼び出すことができます。


### kickSeat

キックアウトしてマイク・オフ（キャスターが呼び出し）。

>?キャスターがキックアウトしてマイク・オフにすると、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorLeaveSeat` のイベント通知を受信します。

```Objective-C
- (void)kickSeat:(NSString *)userID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(userID:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                |
| -------- | -------------- | -------------------- |
| userID   | String         | キックアウトしてマイク・オフにする必要のあるユーザーID。 |
| callback | ActionCallback | 操作コールバック。           |

そのインターフェースをコールすると、すぐにマイクリストが修正されます。キャスターが視聴者の同意がなければマイク・オンできないユースケースの場合は、まず `sendInvitation` を呼び出してから視聴者にリクエストし、 `onInvitationAccept` を受信してから、その関数をコールすることができます。

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

| パラメータ    | タイプ | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 音声品質。詳細については、[TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルの音声のミュート/ミュート取り消し。

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | ミュート/ミュート取り消し。詳細については[TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |



### setSpeaker

スピーカーの起動設定。

```Objective-C
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味                        |
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

指定メンバーのミュート/ミュート解除。

```Objective-C
- (void)muteRemoteAudio:(NSString *)userID mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                              |
| ------ | ------- | --------------------------------- |
| userID | String  | 指定ユーザーID。                   |
| mute   | boolean | true：ミュート起動；false：ミュート停止。 |

### muteAllRemoteAudio

全メンバーのミュート/ミュート解除。

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |

   

## BGMサウンドエフェクト関連インターフェース関数

### getAudioEffectManager

BGMサウンドエフェクト管理オブジェクト [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

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
| message  | String         | テキストメッセージ。     |
| callback | ActionCallback | 送信結果のコールバック。 |

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。

```Objective-C
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | String         | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | String         | テキストメッセージ。                                         |
| callback  | ActionCallback | 送信結果のコールバック。                                    |

   

## 招待シグナリング関連インターフェース

### sendInvitation

ユーザーに招待を送信。

```Objective-C
- (NSString *)sendInvitation:(NSString *)cmd
                      userID:(NSString *)userID
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味             |
| -------- | -------------- | ---------------- |
| cmd      | String         | 業務カスタマイズコマンド。 |
| userID   | String         | 招待ユーザーID。  |
| content  | String         | 招待コンテンツ。     |
| callback  | ActionCallback | 送信結果のコールバック。   |

戻り値：

| 戻り値   | タイプ   | 意味                  |
| -------- | ------ | --------------------- |
| inviteId | String | 今回の招待IDの識別に使用。 |

### acceptInvitation

招待の同意。

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ           |意味          |
| ---------- | -------------- | -------------- |
| identifier | String         | 招待ID。      |
| callback   | ActionCallback | 送信結果のコールバック。|

### rejectInvitation

招待の拒否。

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ           |意味          |
| ---------- | -------------- | -------------- |
| identifier | String         | 招待ID。      |
| callback   | ActionCallback | 送信結果のコールバック。|


### cancelInvitation

招待の取り消し。

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(identifier:callback:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ           |意味          |
| ---------- | -------------- | -------------- |
| identifier | String         | 招待ID。      |
| callback   | ActionCallback | 送信結果のコールバック。|

## TRTCChatSalonDelegateイベントコールバック

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
| message | String | エラーメッセージ。 |


### onWarning

警告のコールバック。

```Objective-C
- (void)onWarning:(int)code
                  message:(NSString *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message | String | 警告メッセージ。 |

   

### onDebugLog

Logコールバック。

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

|パラメータ   | タイプ   | 意味      |
| ------ | ------ | --------- |
| roomId | String | ルームID。 |


### onRoomInfoChange

入室に成功後、このインターフェースをコールバックします。roomInfoは作成されたルームの情報を含みます。

```Objective-C
- (void)onRoomInfoChange:(ChatSalonInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ          | 意味       |
| -------- | ------------- | ---------- |
| roomInfo | ChatSalonInfo | ルーム情報。 |

   

### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。

```Objective-C
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ                            | 意味               |
| ----------- | ------------------------------- | ------------------ |
| userVolumes | NSArray&lt;TRTCVolumeInfo *&gt; | 各ユーザーの音量情報。 |
| totalVolume | int                             | 全体の音量情報。     |


## マイクコールバック

### onAnchorEnterSeat

マイク・オンのメンバーがいます（自主的にマイク・オン/キャスターがピックしてマイク・オン）。

```Objective-C
- (void)onAnchorEnterSeat:(ChatSalonUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(user:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ              | 意味                 |
| ---- | ----------------- | -------------------- |
| user | ChatSalonUserInfo | マイク・オンのユーザーの詳細情報。 |

### onAnchorLeaveSeat

マイク・オフのメンバーがいます（自主的にマイク・オフ/キャスターがキックアウトしてマイク・オフ）。

```Objective-C
- (void)onAnchorLeaveSeat:(ChatSalonUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(user:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ              | 意味                 |
| ---- | ----------------- | -------------------- |
| user | ChatSalonUserInfo | マイク・オンのユーザーの詳細情報。 |

### onSeatMute

キャスターのマイクミュート。

```Objective-C
- (void)onSeatMute:(NSString *)userID
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(userID:isMute:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                               |
| ------ | ------- | ---------------------------------- |
| userID | String  | マイクのユーザーid。                     |
| isMute | boolean | true：マイクミュート； false：ミュート解除。 |

## 視聴者の入退室イベントのコールバック

### onAudienceEnter

視聴者入室通知の受信。

```Objective-C
- (void)onAudienceEnter:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ              | 意味           |
| -------- | ----------------- | -------------- |
| userInfo | ChatSalonUserInfo | 入室した視聴者の情報。 |

### onAudienceExit

視聴者退室通知の受信。

```Objective-C
- (void)onAudienceExit:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ              | 意味           |
| -------- | ----------------- | -------------- |
| userInfo | ChatSalonUserInfo | 退室した視聴者の情報。 |

   

## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```Objective-C
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ              | 意味             |
| -------- | ----------------- | ---------------- |
| message  | String            | テキストメッセージ。       |
| userInfo | ChatSalonUserInfo | 送信者のユーザー情報。 |

   

### onRecvRoomCustomMsg

カスタムメッセージの受信。

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)cmd
                    message:(NSString *)message
                   userInfo:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(cmd:message:userInfo:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ              | 意味                                               |
| -------- | ----------------- | -------------------------------------------------- |
| command  | String            | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | String            | テキストメッセージ。                                         |
| userInfo | ChatSalonUserInfo | 送信者のユーザー情報。                                   |

## 招待シグナリングイベントのコールバック

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

| パラメータ       | タイプ    | 意味                               |
| ---------- | ------ | ---------------------------------- |
| identifier | String | 招待ID。                          |
| inviter    | String | 招待者のユーザーID。                  |
| cmd        | String |業務指定のコマンドワードは、開発者がカスタマイズします。 |
| content    | String | 業務指定のコンテンツ。                   |

### onInviteeAccepted

被招待者が招待に同意。

```Objective-C
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味                |
| ---------- | ------ | ------------------- |
| identifier | String | 招待ID。           |
| invitee    | String | 被招待者のユーザーID。 |

### onInviteeRejected

被招待者による招待の拒否。

```Objective-C
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味                |
| ---------- | ------ | ------------------- |
| identifier | String | 招待ID。           |
| invitee    | String | 被招待者のユーザーID。 |

### onInvitationCancelled

招待者が招待を取り消し。

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(identifier:invitee:));
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味              |
| ---------- | ------ | ----------------- |
| identifier | String | 招待ID。         |
| inviter    | String | 招待者のユーザーID。 |

### onInvitationTimeout

招待のタイムアウト。

```Objective-C
- (void)onInvitationTimeout:(NSString *)identifier;
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味      |
| ---------- | ------ | --------- |
| identifier | String | 招待ID。 |
