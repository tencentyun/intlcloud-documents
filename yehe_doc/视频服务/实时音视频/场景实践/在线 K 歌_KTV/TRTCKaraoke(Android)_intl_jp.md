TRTCKaraokeRoomは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- 管理者が作成した新しいKaraokeルームが配信を開始すると、リスナーはKaraokeルームに入室して聴取/インタラクションを行います。
- 管理者は、楽曲の順序を管理し、マイク・オンのキャスターをキックアウトすることもできます。
- 管理者はまた、座席をクローズすることができ、その他のリスナーはマイク・オンを申請することができなくなります。
- リスナーはマイク・オンを申請して、マイク・オンのキャスターになり、マイク・オン後は楽曲の選択や歌唱ができるようになります。また、いつでもマイク・オフにして、通常のリスナーになることも可能です。
- ギフトや各種のテキストメッセージ、カスタムメッセージの送信をサポートします。カスタムメッセージを弾幕、「いいね」などを実装するために使用することができます。

TRTCKaraokeRoomはオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実装プロセスについては、[Karaoke（Android)](https://intl.cloud.tencent.com/document/product/647/41941)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のボイスチャットコンポーネントとして使用しています。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用してチャットルーム機能を実装します。同時にIMの属性インターフェースによって、マイクリストなどのルーム情報を保存し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。

[](id:TRTCKaraokeRoom)
## TRTCKaraokeRoom API概要

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
| [getUserInfoList](#getuserinfolist) | 指定されたuserIdのユーザー情報を取得します。 nullの場合は、ルーム内全員の情報を取得します。 |

### 音楽再生インターフェース

| API                                 | 説明             |
| ----------------------------------- | --------------- |
| [startPlayMusic](#startplaymusic)   | 音楽の再生を開始します。     |
| [stopPlayMusic](#stopplaymusic)     | 音楽の再生を停止します。     |
| [pausePlayMusic](#pauseplaymusic)    | 音楽の再生を一時停止します。     |
| [resumePlayMusic](#resumeplaymusic) | 音楽の再生を再開します。     |

### マイク管理インターフェース

| API                     | 説明                                  |
| ----------------------- | ------------------------------------- |
| [enterSeat](#enterseat) | ユーザーが発言者になる（リスナー側/管理者ともに呼び出し可）。  |
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

| API                                       | 説明                 |
| ----------------------------------------- | -------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | 指定メンバーをミュート/ミュート解除。 |
| [muteAllRemoteAudio](#muteallremoteaudio) | 全メンバーをミュート/ミュート解除。 |

### BGMサウンドエフェクト関連インターフェース

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | BGMサウンドエフェクト管理オブジェクト[TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager)を取得します。|

### メッセージ送信関連インターフェース

| API                                     | 説明                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージのブロードキャスト。通常、弾幕によるチャットに使用します。 |
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを送信します。                     |

### 招待シグナリング関連インターフェース

| API                                   | 説明             |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | ユーザーに招待を送信。 |
| [acceptInvitation](#acceptinvitation) | 招待の同意。       |
| [rejectInvitation](#rejectinvitation) | 招待の辞退。       |
| [cancelInvitation](#cancelinvitation) | 招待の取り消し。       |

[](id:TRTCKaraokeRoomDelegate)
## TRTCKaraokeRoomDelegate API概要

### 一般的なイベントコールバック

| API                       | 説明       |
| ------------------------- | ---------- |
| [onError](#onerror) | エラーのコールバック。 |
| [onWarning](#onwarning)   | 警告のコールバック。 |
| [onDebugLog](#ondebuglog) | Logコールバック。|

### ルームイベントのコールバック

| API                                       | 説明                 |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | ルームが廃棄された時のコールバック。     |
| [onRoomInfoChange](#onroominfochange) | Karaoke情報変更のコールバック。 |
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。     |

### マイク変更コールバック

| API                                     | 説明                                |
| --------------------------------------- | ----------------------------------- |
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

## シグナリングイベントのコールバック

| API                                               | 説明             |
| ------------------------------------------------- | ---------------- |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 新規招待リクエストの受信。   |
| [onInviteeAccepted](#oninviteeaccepted)           | 被招待者が招待に同意。   |
| [onInviteeRejected](#oninviteerejected)           | 被招待者が招待を拒否。   |
| [onInvitationCancelled](#oninvitationcancelled)   | 招待者が招待を取り消し。   |

### 楽曲イベントコールバック

| API                                               | 説明             |
| ------------------------------------------------- | ----------------- |
| [onMusicProgressUpdate](#onmusicprogressupdate)   | 楽曲再生進捗度のコールバック。 |
| [onMusicPrepareToPlay](#onmusicpreparetoplay)     | 音楽再生準備のコールバック。 |
| [onMusicCompletePlaying](#onmusiccompleteplaying) | 音楽再生完了のコールバック。 |

## SDK基本関数

[](id:sharedInstance)
### sharedInstance

[TRTCKaraokeRoom](https://intl.cloud.tencent.com/document/product/647/41941)シングルトンオブジェクトを取得します。

```java
 public static synchronized TRTCKaraokeRoom sharedInstance(Context context);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| context | Context | Androidコンテキスト。内部ではApplicationContextに変換してシステムAPIの呼び出しに使用します |

   

### destroySharedInstance

[TRTCKaraokeRoom](https://intl.cloud.tencent.com/document/product/647/41941)シングルトンオブジェクトを破棄します。

>?インスタンスの破棄後は、外部にキャッシュされたTRTCKaraokeRoomインスタンスの再使用ができません。改めて[sharedInstance](#sharedInstance)を呼び出し、インスタンスを新規取得する必要があります。

```java
public static void destroySharedInstance();
```

### setDelegate

[TRTCKaraokeRoom](https://intl.cloud.tencent.com/document/product/647/41941)イベントコールバック。 TRTCKaraokeRoomDelegateを介して[TRTCKaraokeLiveRoom](https://intl.cloud.tencent.com/document/product/647/41941)の各種ステータス通知を受け取ることができます。

```java
public abstract void setDelegate(TRTCKaraokeRoomDelegate delegate);
```

>?setDelegateはTRTCKaraokeRoomのプロキシコールバックです。   

### setDelegateHandler

イベントコールバックが配置されているスレッドを設定します。

```java
public abstract void setDelegateHandler(Handler handler);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| handler | Handler | TRTCKaraokeRoomの各種ステータス通知は、指定したhandlerスレッドに発信されます。 |

   

### login

ログイン

```java
public abstract void login(int sdkAppId,
 String userId, String userSig,
TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int         | TRTCコンソール> 【[アプリケーション管理]（https://console.cloud.tencent.com/trtc/app）】>アプリケーション情報の中でSDKAppIDを確認できます。 |
| userId   | String                | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String         |Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallback | ログインのコールバック。成功時にcodeは0になります。                                  |

   

### logout

ログアウト。

```java
public abstract void logout(TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                        |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | ログアウトのコールバック。成功時にcodeは0になります。 |

   

### setSelfProfile

個人情報の修正。

```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                |
| --------- | -------------- | ----------------------------------- |
| userName  | String         | ニックネーム。                              |
| avatarURL | String         | プロフィール画像のアドレス。                          |
| callback | ActionCallback | 個人情報設定のコールバック。成功時にcodeは0になります。                                  |

   


## ルーム関連インターフェース関数

### createRoom

ルームの作成（管理者が呼び出し）。

```java
public abstract void createRoom(int roomId, TRTCKaraokeRoomDef.RoomParam roomParam, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                | 意味                                                         |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomI    | int            | ルームIDは、ご自身でアサインし、一元管理する必要があります。複数のroomIDを、一つのKaraokeルームリストにまとめることができます。Tencent Cloudでは現在、Karaokeルームリストの管理サービスを行っていませんので、ご自身でKaraokeルームリストを管理してください。 |
| roomParam | TRTCCreateRoomParam | ルーム情報は、ルーム名、マイク情報、カバー情報など、ルームを説明するために用いる情報に使用します。マイク管理が必要な場合は、ルームのマイク数を記入する必要があります。 |
| callback | ActionCallback | ルームの新規作成結果のコールバック。成功時にcodeは0になります。                                  |

管理者が配信を開始する際の通常の呼び出しプロセスは次のとおりです。 
1. 管理者は、`createRoom`を呼び出して新しいKaraokeルームを作成します。この時、ルームID、マイク・オンにすることの管理者の確認の要否、ルームタイプなどルームの属性情報を渡します。
2. 管理者は、ルーム作成に成功した後、`enterSeat`を呼び出して参加します。
3. 管理者は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
4. 管理者は、マイクリストのメンバーが参加した`onAnchorEnterSeat`というイベント通知も受信します。この時、マイク集音は自動的に開始されます。

   

### destroyRoom

ルームの破棄（管理者が呼び出し）。管理者は、ルーム作成後、この関数を呼び出してルームを破棄します。

```java
public abstract void destroyRoom(TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時にcodeは0になります。 |


### enterRoom

入室（リスナーが呼び出し）。

```java
public abstract void enterRoom(int roomId, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | int            | ルームID。                            |
| callback | ActionCallback | 入室結果のコールバック。成功時にcodeは0になります。 |


リスナーが入室し聴取する際の通常の呼び出しプロセスは次のとおりです。 

1. リスナーがサーバーから取得する最新のKaraokeルームリストには、多くのKaraokeルームのroomIdおよびルーム情報が含まれる場合があります。
2. リスナーは1つのKaraokeルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
3. 入室後、コンポーネントの`onRoomInfoChange`ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、マイク・オンの際の管理者への同意リクエストの要否の記録など。
4. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
5. 入室後に、マイクリストにキャスターが参加した`onAnchorEnterSeat`のイベント通知も受信します。

### exitRoom

ルームから退出します。

```java
public abstract void exitRoom(TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 退室結果のコールバック。成功時にcodeは0になります。 |

   

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、管理者が`createRoom()`作成時にroomInfoによって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```java
public abstract void getRoomInfoList(List<Integer> roomIdList, TRTCKaraokeRoomCallback.RoomInfoCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味               |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt;   | ルームナンバーリスト。       |
| callback   | RoomInfoCallback    | ルーム詳細情報のコールバック。 |


### getUserInfoList

指定されたuserIdのユーザー情報を取得します。

```java
public abstract void getUserInfoList(List<String> userIdList, TRTCKaraokeRoomCallback.UserListCallback userlistcallback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                      | 意味                                                       |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt;        |取得すべきユーザーIDリスト。nullの場合は、ルーム内全員の情報を取得します。 |
| userlistcallback | UserListCallback   | ユーザーの詳細情報のコールバック。                                          |

## 音楽再生インターフェース

### startPlayMusic

音楽を再生します（マイク・オン後に呼び出し）。
>?
>- 音楽を再生すると、`onMusicPrepareToPlay`というイベント通知を受信します。
>- 音楽の再生中、ルーム内の全メンバーは、`onMusicProgressUpdate`というイベント通知を継続して受け取ります。
>- 音楽の再生が完了すると、`onMusicCompletePlaying`というイベント通知を受信します。

```java
public abstract void startPlayMusic(int musicID, String originalUrl, String accompanyUrl);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ            | 意味                 |
| --------- | -------------- | -------------------- |
|musicID   |   int | 音楽のID。  |
|originalUrl  | String | 原曲の絶対パス。   |
|accompanyUrl |  String | 伴奏の絶対パス。  |

このインターフェースを呼び出すと、最後に再生されていた楽曲が停止します。

### stopPlayMusic

音楽の再生を停止します（音楽を再生するときに呼び出します）。
>?再生が停止すると、`onMusicCompletePlaying`というイベント通知を受信します。

```java
public abstract void stopPlayMusic();
```

### pausePlayMusic

音楽の再生を一時停止します（音楽を再生するときに呼び出します）。
>? 
>- `onMusicProgressUpdate`というイベント通知が一時停止されます
>- `onMusicCompletePlaying`というイベント通知を受信しません。

```java
public abstract void pausePlayMusic();
```

### resumePlayMusic

一時停止した音楽を再開します（一時停止後に呼び出します）。
>?`onMusicPrepareToPlay`というイベント通知を受信しません。

```java
public abstract void resumePlayMusic();
```

## マイク管理インターフェース

### enterSeat

ユーザーが発言者になります（リスナー側/管理者ともに呼び出し可）。

>?マイク・オンの成功後、ルーム内の全メンバーは、`onSeatListChange`および`onAnchorEnterSeat`というイベント通知を受信します。

```java
public abstract void enterSeat(int seatIndex, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ           | 意味                 |
| --------- | -------------- | -------------------- |
| seatIndex | int            | マイク・オンの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。           |

このインターフェースを呼び出すと、直ちにマイクリストが変更されます。リスナーによるマイク・オンの申請に管理者の同意が必要となるケースの場合は、まず`sendInvitation`を呼び出してから管理者に申請し、`onInvitationAccept`を受信するとこの関数を呼び出せるようになります。

### leaveSeat

ユーザーが視聴者になる（キャスターが呼び出し）。

>? マイク・オフの成功後、ルーム内の全メンバーは、`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

```java
public abstract void leaveSeat(TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 操作コールバック。|

### pickSeat

視聴者が発言できるように招待（管理者が呼び出し）。

>?、管理者が視聴者を発言できるように招待すると、ルーム内の全メンバーは、`onSeatListChange`と`onAnchorEnterSeat`というイベント通知を受信します。

```java
public abstract void pickSeat(int seatIndex, String userId, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | 視聴者が発言できるように招待する必要があるマイク番号。 |
| userId | String           | ユーザーID。        |
| callback  | ActionCallback | 操作コールバック。           |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。管理者がリスナーの同意がなければマイク・オンできないケースの場合は、まず`sendInvitation`を呼び出してからリスナーに申請し、`onInvitationAccept`を受信すると、この関数をコールできるようになります。


### kickSeat

キックアウトしてマイク・オフ（管理者が呼び出し）。

>?管理者がキックアウトしてマイク・オフにすると、ルーム内の全メンバーは、`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

```java
public abstract void kickSeat(int seatIndex, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | キックアウトしてマイク・オフの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。           |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。

### muteSeat

任意のマイクのミュート/ミュート解除（管理者が呼び出し）。

>? 任意のマイクのミュート/ミュート解除は、ルーム内の全メンバーが`onSeatListChange`および`onSeatMute`というイベント通知を受信します。

```java
public abstract void muteSeat(int seatIndex, boolean isMute, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                          |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | int            | 操作の必要があるマイク番号。                       |
| isMute    | boolean        | true：該当するマイクのミュート；false：該当するマイクのミュート解除。 |
| callback  | ActionCallback | 操作コールバック。                                 |

このインターフェースを呼び出すと、直ちにマイクリストが変更されます。seatIndexの座席に該当するキャスターは、muteAudioを自動的に呼び出してミュート/ミュートオフにします。

### closeSeat

任意のマイクのクローズ/解除（管理者が呼び出し）。

>? 管理者は、該当するマイクをクローズ/解除し、ルーム内の全メンバーは`onSeatListChange`および`onSeatClose`というイベント通知を受信します。

```java
public abstract void closeSeat(int seatIndex, boolean isClose, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                       |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | int            | 操作の必要があるマイク番号。                       |
| isClose   | boolean        | true：該当するマイクのクローズ； false：該当するマイクのクローズ解除。 |
| callback  | ActionCallback | 操作コールバック。                                 |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。該当するseatIndexの座席上のキャスターはクローズされ、自動的にマイク・オフになります。


## ローカル音声操作のインターフェース

### startMicrophone

マイクの集音開始。

```java
public abstract void startMicrophone();
```

### stopMicrophone

マイクの集音停止。

```java
public abstract void stopMicrophone();
```

### setAudioQuality

音質の設定。

```java
public abstract void setAudioQuality(int quality);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ             | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 音声品質。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルの音声のミュート/ミュート取り消し。

```java
public abstract void muteLocalAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ    | 意味                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | ミュート/ミュート取り消し。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |



### setSpeaker

スピーカーの起動設定。

```java
public abstract void setSpeaker(boolean useSpeaker);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true：スピーカー、false：ヘッドホン。|



### setAudioCaptureVolume

マイクの集音音量設定。

```java
public abstract void setAudioCaptureVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 集音音量、0 - 100、 デフォルト100。 |


### setAudioPlayoutVolume

再生音量の設定。

```java
public abstract void setAudioPlayoutVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                        |
| ------ | ---- | --------------------------- |
| volume | int  | 再生音量、0 - 100、 デフォルト100。 |

### muteRemoteAudio

指定メンバーのミュート/ミュート解除。

```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| userId | String  | 指定ユーザーID。                   |
| mute | boolean | true：ミュート起動、false：ミュート停止。|

### muteAllRemoteAudio

全メンバーのミュート/ミュート解除。

```java
public abstract void muteAllRemoteAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true：ミュート起動、false：ミュート停止。|

### setVoiceEarMonitorEnable

インイヤーモニタリングのオン/オフ。

```java
public abstract void setVoiceEarMonitorEnable(boolean enable);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| enable | boolean | true：インイヤーモニタリングをオン。false：インイヤーモニタリングをオフ。 |


## BGMサウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットに使用します。

```java
public abstract void sendRoomTextMsg(String message, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| message  | String         | テキストメッセージ。     |
| callback | ActionCallback | 送信結果のコールバック。|

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。

```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCKaraokeRoomCallback.ActionCallback callback);
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

```java
public abstract String sendInvitation(String cmd, String userId, String content, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味             |
| -------- | -------------- | ---------------- |
| cmd      | String         | 業務カスタマイズコマンド。 |
| userId | String           | 招待ユーザーID。  |
| content  | String         | 招待コンテンツ。     |
| callback  | ActionCallback | 送信結果のコールバック。   |

戻り値：

| 戻り値   | タイプ   | 意味                  |
| -------- | ------ | --------------------- |
| inviteId | String | 今回の招待IDの識別に使用。 |

### acceptInvitation

招待の同意。

```java
public abstract void acceptInvitation(String id, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。|

### rejectInvitation

招待の拒否。

```java
public abstract void rejectInvitation(String id, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味     |
| ---- | ------ | -------- |
| id   | String | 招待ID。 |
| callback | ActionCallback | 送信結果のコールバック。|


### cancelInvitation

招待の取り消し。

```java
public abstract void cancelInvitation(String id, TRTCKaraokeRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。|

[](id:TRTCKaraokeRoomDelegate)
## TRTCKaraokeRoomDelegateイベントコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```java
void onError(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message | String | エラーメッセージ。 |


### onWarning

警告のコールバック。

```java
void onWarning(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message | String | 警告メッセージ。 |

   

### onDebugLog

Logコールバック。

```java
void onDebugLog(String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | ログ情報。 |

   


## ルームイベントのコールバック

### onRoomDestroy

ルーム破棄のコールバック。管理者がルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

```java
void onRoomDestroy(String roomId);
```

パラメータは下表に示すとおりです。

|パラメータ   | タイプ   | 意味      |
| ------ | ------ | --------- |
| roomId | String | ルームID。 |


### onRoomInfoChange

入室に成功後、このインターフェースをコールバックします。roomInfoの情報は、管理者がルームを作成するときに渡されます。

```java
void onRoomInfoChange(TRTCKaraokeRoomDef.RoomInfo roomInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味       |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | ルーム情報。 |

   

### onUserMicrophoneMute

ユーザーのマイクがミュートになっているかどうかについて、ユーザーがmuteLocalAudioを呼び出すと、ルームの他のユーザーがこの通知を受信します。

```java
void onUserMicrophoneMute(String userId, boolean mute);

```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
| ------ | ------ | ------------------------- |
| userId | String           | ユーザーID。        |
| mute | boolean    | 音量の大きさ。値：0～100。 |

### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。

```java
void onUserVolumeUpdate(List<TRTCCloudDef.TRTCVolumeInfo> userVolumes, int totalVolume);

```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
| ------ | ------ | ------------------------- |
| userVolumes | List | ユーザーリスト。                 |
| totalVolume | int    | 音量の大きさ。値：0～100。 |


## マイクコールバック

### onSeatListChange

全量のマイクリストの変更は、全てのマイクリストを含みます。

```java
void onSeatListChange(List<SeatInfo> seatInfoList);
```

パラメータは下表に示すとおりです。

| パラメータ         | タイプ           | 意味             |
| ------------ | -------------- | ---------------- |
| seatInfoList | List&lt;SeatInfo&gt; | 全量のマイクリスト。 |

### onAnchorEnterSeat
発言者のメンバーがいます（ユーザーが発言者になる/管理者が視聴者を発言できるように招待）。

```java
void onAnchorEnterSeat(int index, TRTCKaraokeRoomDef.UserInfo user);
```
パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | int      | メンバーがマイク・オンのマイク。     |
| user  | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onAnchorLeaveSeat

視聴者のメンバーがいます（ユーザーが視聴者になる/管理者がキックアウトしてマイク・オフ）。

```java
void onAnchorLeaveSeat(int index, TRTCKaraokeRoomDef.UserInfo user);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | int      | マイク・オフのマイク。         |
| user  | UserInfo | マイク・オフのユーザーの詳細情報。 |

### onSeatMute

管理者のマイクミュート。

```java
void onSeatMute(int index, boolean isMute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                               |
| ------ | ------- | ---------------------------------- |
| index  | int     | 操作するマイク。                       |
| isMute | boolean | true：マイクミュート； false：ミュート解除。 |

### onSeatClose

管理者のマイククローズ。

```java
void onSeatClose(int index, boolean isClose);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                |
| ------- | ------- | ----------------------------------- |
| index   | int     | 操作するマイク。                        |
| isClose | boolean | true：マイクのクローズ； false：マイクのクローズ解除。 |

## リスナーの入退室イベントのコールバック

### onAudienceEnter

リスナー入室通知の受信。

```java
void onAudienceEnter(TRTCKaraokeRoomDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 入室したリスナーの情報。 |

### onAudienceExit

リスナー退室通知の受信。

```java
void onAudienceExit(TRTCKaraokeRoomDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 退室したリスナーの情報。 |

   

## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```java
void onRecvRoomTextMsg(String message, TRTCKaraokeRoomDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味             |
| -------- | -------- | ---------------- |
| message  | String  | テキストメッセージ。       |
| userInfo | UserInfo | 送信者のユーザー情報。 |

   

### onRecvRoomCustomMsg

カスタムメッセージの受信。

```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCKaraokeRoomDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味                                               |
| -------- | -------- | -------------------------------------------------- |
| command  | String   | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | String   | テキストメッセージ。                                         |
| userInfo | UserInfo | 送信者のユーザー情報。                                   |

## 招待シグナリングイベントのコールバック

### onReceiveNewInvitation

新規招待リクエストの受信。

```java
void onReceiveNewInvitation(String id, String inviter, String cmd, String content);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ     | 意味                               |
| ------- | -------- | ---------------------------------- |
| id      | String   | 招待ID。                          |
| inviter | String   | 招待者のユーザーID。                  |
| cmd     | String   | 業務指定のコマンドワードは、開発者がカスタマイズします。 |
| content | String   | 業務指定のコンテンツ。                   |

### onInviteeAccepted

被招待者が招待に同意。

```java
void onInviteeAccepted(String id, String invitee);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待ID。           |
| invitee    | String | 被招待者のユーザーID。 |

### onInviteeRejected

被招待者による招待の拒否。

```java
void onInviteeRejected(String id, String invitee);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待ID。           |
| invitee    | String | 被招待者のユーザーID。 |

### onInvitationCancelled

招待者が招待を取り消し。

```java
void onInvitationCancelled(String id, String inviter);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味               |
| ------- | ------ | ----------------- |
| id      | String | 招待ID。         |
| inviter    | String | 招待者のユーザーID。 |

## 音楽再生ステータスコールバック

### onMusicPrepareToPlay

音楽再生準備のコールバック

```java
void onMusicPrepareToPlay(int musicID);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味               |
| ------- | ---- | -------------------- |
| musicID | int  | 再生時に渡されたmusicID。  |

### onMusicProgressUpdate

楽曲再生進捗度のコールバック

```java
void onMusicProgressUpdate(int musicID, long progress, long total);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味               |
| -------- | ---- | -------------------- |
| musicID  | int  | 再生時に渡されたmusicID。  |
| progress | long | 現在の再生時間。単位： ms。 |
| total    | long | 合計時間。単位： ms。      |

### onMusicCompletePlaying

音楽再生完了のコールバック

```java
void onMusicCompletePlaying(int musicID);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味               |
| -------- | ----- | -------------------- |
| musicID  | int   | 再生時に渡されたmusicID。  |
