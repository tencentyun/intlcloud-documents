TRTCVoiceRoom は、Tencent CloudのTRTCおよびIM サービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- キャスターが新しいボイスチャットルームを作成して放送を開始し、視聴者がボイスチャットルームに参加して視聴/インタラクティブなコミュニケーションを図ります。
- キャスターは、視聴者をマイク・オンに招待したり、マイク・オンのキャスターをマイク・オフにすることもできます。
- キャスターはまた、座席をクローズすることができ、その他の視聴者はマイク・オンを再度リクエストすることができなくなります。
- 視聴者は、マイク・オンをリクエストして、マイク・オンのキャスターに変わることができます。他人とインタラクティブの会話ができ、随時マイク・オフにして通常の視聴者になることも可能です。
- 各種のテキストメッセージやカスタマイズメッセージの発信をサポートし、情報を弾幕、「いいね」、ギフトなどに使えられるようにカスタマイズします。

TRTCVoiceRoom は、オープンソースの Classであり、Tencent Cloudの2つのクローズソースであるSDKに依存しています。具体的な実装プロセスは [ボイスチャットルーム（Android）](https://intl.cloud.tencent.com/document/product/647/37286)を参照してください。

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
| [createRoom](#createroom)           | ルームの新規作成（キャスターがコール）。ルームが存在していない場合は、システムが新しいルームを自動作成。｜
| [destroyRoom](#destroyroom)         | ルームの廃棄（キャスターがコール）。                                       |
| [enterRoom](#enterroom)             | 入室（視聴者がコール）。                                       |
| [exitRoom](#exitroom)               | 退室（視聴者がコール）。                                       |
| [getRoomInfoList](#getroominfolist) | ルームリストの詳細情報の取得。                              |
| [getUserInfoList](#getuserinfolist) | 指定された userId のユーザー情報の取得。 nullの場合は、ルーム内全員の情報を取得。 |

### マイク管理インターフェース

| API                                             | 説明                                                         |
| ----------------------- | ------------------------------------- |
| [enterSeat](#enterseat) | 自主的にマイク・オン（視聴者／キャスターともにコール可）。    |
| [leaveSeat](#leaveseat) | 自主的にマイク・オフ（視聴者／キャスターともにコール可）。    |
| [pickSeat](#pickseat)   | ピックしてマイク・オン（キャスターがコール）。                  |
| [kickSeat](#kickseat)   | キックしてマイク・オフ（キャスターがコール）。                  |
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

| API                                             | 説明                                                         |
| ----------------------------------------- | -------------------- |
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

| API                                             | 説明                                                         |
| --------------------------------------- | ----------------------------------- |
| [onSeatListChange](#onseatlistchange)   |全量のマイクリストの変更。                |
| [onAnchorEnterSeat](#onanchorenterseat) | マイク・オンの参加者（自主的にマイク・オン／キャスターがピックしてマイク・オン）。 |
| [onAnchorLeaveSeat](#onanchorleaveseat) | マイク・オフの参加者（自主的にマイク・オフ／キャスターがキックしてマイク・オフ）。 |
| [onSeatMute](#onseatmute)               | キャスターのマイクミュート。                          |
| [onSeatClose](#onseatclose)             | キャスターのマイククローズ。                          |

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

## シグナリングインシデントのコールバック

| API                                             | 説明                                                         |
| ------------------------------------------------- | ---------------- |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 新規招待リクエストの受信。   |
| [onInviteeAccepted](#oninviteeaccepted)           | 被招待者が招待に同意。   |
| [onInviteeRejected](#oninviteerejected)           | 被招待者による招待の辞退。   |
| [onInvitationCancelled](#oninvitationcancelled)   | 招待者が招待を取り消し。 |

## SDK 基本関数

<span id="sharedInstance"></span>

### sharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) シングルトンオブジェクトの取得。

```java
 public static synchronized TRTCLiveRoom sharedInstance(Context context);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| context | Context | Android 前後関係，コンテンツをApplicationContext に転換してシステム API のコールに使用 |

   

### destroySharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) シングルトンオブジェクトの廃棄。

>?インスタンスを廃棄後は、外部にキャッシュされた  TRTCVoiceRoom インスタンスの再使用ができません。改めて [sharedInstance](#sharedInstance) をコールして、インスタンスを新規取得する必要があります。

```java
public static void destroySharedInstance();
```

### setDelegate

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) イベントコールバック、 TRTCVoiceRoomDelegate を介して [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) の各種ステータス通知を受け取ることができます。

```java
public abstract void setDelegate(TRTCLiveRoomDelegate delegate);
```

>?setDelegate は、 TRTCVoiceRoom のプロキシコールバックです。   

### setDelegateHandler

イベントのコールバックが所在するスレッドを設定します。

```java
public abstract void setDelegateHandler(Handler handler);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| handler | Handler | TRTCVoiceRoom の各種ステータス通知は指定した handler スレッドに発送されます。 |

   

### login

ログイン。

```java
public abstract void login(int sdkAppId,
 String userId, String userSig,
TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppID | int         | Tencent Real-Time Communicationコンソール> 【[アプリケーション管理]（https://console.cloud.tencent.com/trtc/app）】>アプリケーション情報でSDKAppIDを表示できます。 |
| user     | String                | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String                | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法 ](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallback | ログインのコールバック。成功時に code は0になります。                                  |

   

### logout

ログアウト。

```java
public abstract void logout(TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                        |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | ログアウトのコールバック。成功時に code は0になります。 |

   

### setSelfProfile

個人情報の修正。

```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCVoiceRoomCallback.ActionCallback callback);
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

```java
public abstract void createRoom(int roomId, TRTCVoiceRoomDef.RoomParam roomParam, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                | 意味                                                         |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomId | int | ルームIDは、ご自身でアサインし、統一管理する必要があります。複数の roomID を、一つのボイスチャットルームリストにまとめることができます。Tencent Cloudではボイスチャットルームリストの管理サービスを一時的に行いませんので、ご自身でボイスチャットルームリストを管理してください。 |
| roomParam | TRTCCreateRoomParam | ルーム情報は、ルーム名、マイク情報、カバー情報などのルーム説明の情報に使用します。マイク管理が必要な場合は、ルームのマイク数を記入する必要があります。 |
| callback | ActionCallback | ルームの新規作成結果のコールバック。成功時に code は0になります。                                  |

キャスターが放送開始する通常のコールフローは以下のとおりです。 
1. キャスターは、 `createRoom` をコールして新しいボイスチャットルームを作成します。この時にルーム ID、マイク・オンにキャスターの確認の要否、マイク数などルームのプロパティ情報を送信します。
2. キャスターは、ルーム作成に成功した後、 `enterSeat` をコールして参加します。
3. キャスターは、コンポーネントの `onSeatListChange` マイクリストの変更インシデント通知を受信します。この時、マイクリストの変更を UI 上で更新することができます。
4. キャスターは、マイクリストのメンバーが参加した `onAnchorEnterSeat` のインシデント通知も受信し、この時にマイクは自動的に集音を始めます。

   

### destroyRoom

ルームの廃棄（キャスターがコール）。キャスターは、ルーム作成後、この関数をコールしてルームを廃棄します。

```java
public abstract void destroyRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時に code は0になります。                                  |


### EnterRoom

入室（視聴者がコール）

```java
public abstract void enterRoom(int roomId, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | int            | ルームID。                            |
| callback | ActionCallback | 入室結果のコールバック。成功時に code は0になります。                                  |


視聴者が入室し視聴した通常のコールフローは以下のとおりです。 

1. 視聴者がサーバーから取得する最新のボイスチャットルームリストには、多くのボイスチャットルームの roomId およびルーム情報が含まれます。
2．オーディエンスは一つのボイスチャットルームを選択し、 `enterRoom` をコールしてルームナンバーを送信すると、そのルームに入室できます。
3. 入室後、コンポーネントの `onRoomInfoChange` ルームプロパティの変更インシデント通知を受信します。この時はルームプロパティを記録して相応の修正を行うことができます。例：UI は、ルーム名、キャスターにマイク・オンの同意を求める要否の記録などを表示します。
4. 入室後は、コンポーネントの `onSeatListChange` マイクリストの変更インシデント通知を受信します。この時、マイクリストの変更を UI上に更新することができます。
5. 入室後に、マイクリストにキャスターが参加した `onAnchorEnterSeat` のインシデント通知も受信することがあります。

### exitRoom

ルームを退出する。

```java
public abstract void exitRoom(TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 退室結果のコールバック。成功時に code は0になります。                                  |

   

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、キャスターが `createRoom()` 作成時に roomInfo によって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```java
public abstract void getRoomInfoList(List<Integer> roomIdList, TRTCVoiceRoomCallback.RoomInfoCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味               |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | ルームナンバーリスト。       |
| callback   | RoomInfoCallback    | ルーム詳細情報のコールバック。 |


### getUserInfoList

指定 userId のユーザー情報を取得します。

```java
public abstract void getUserInfoList(List<String> userIdList, TRTCVoiceRoomCallback.UserListCallback userlistcallback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                      | 意味                                                       |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt; | 取得すべきユーザー ID 表、 nullの場合は、ルーム内全員の情報を取得します。 |
| userlistcallback | UserListCallback   | ユーザーの詳細情報のコールバック。                                          |


## マイク管理インターフェース

### enterSeat

自主的にマイク・オン（視聴者／キャスターともにコール可）。

>?マイク・オンの成功後、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorEnterSeat` のインシデント通知を受信します。

```java
public abstract void enterSeat(int seatIndex, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ             | 意味                           |
| --------- | -------------- | -------------------- |
| seatIndex | int            | マイク・オンの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。           |

このインターフェースをコールすると、すぐにマイクリストを修正します。オーディエンスがキャスターのリクエストを必要とするユースケースの場合は、先に `sendInvitation` をコールしてからキャスターにリクエストし、 `onInvitationAccept ` を受信してから、該当する関数をコールすることができます。

### leaveSeat

自主的にマイク・オフ（視聴者／キャスターともにコール可）。

>?マイク・オフの成功後、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorLeaveSeat` のインシデント通知を受信します。

```java
public abstract void leaveSeat(TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback  | ActionCallback | 操作コールバック。 |

### pickSeat

ピックしてマイク・オン（キャスターがコール）。  

>?キャスターが着席してマイク・オンし、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorEnterSeat` のインシデント通知を受信します。

```java
public abstract void pickSeat(int seatIndex, String userId, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | 着席してマイク・オンの必要があるマイク番号。 |
| userId | String           | ユーザー ID。        |
| callback  | ActionCallback | 操作コールバック。             |

そのインターフェースをコールすると、すぐにマイクリストを修正します。キャスターがオーディエンスの同意がなければマイク・オンにできないユースケースの場合は、先ず `sendInvitation` をコールしてからオーディエンスにリクエストし、 `onInvitationAccept ` を受信してから、その関数をコールすることができます。


### kickSeat

キックしてマイク・オフ（キャスターがコール）。   

>?キャスターが離席してマイク・オフにすると、ルーム内の全メンバーは、 `onSeatListChange` および `onAnchorLeaveSeat` のインシデント通知を受信します。

```java
public abstract void kickSeat(int seatIndex, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                   |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | キックしてマイク・オフの必要があるマイク番号。 |
| callback  | ActionCallback | 操作コールバック。             |

そのインターフェースをコールすると、すぐにマイクリストを修正します。キャスターがオーディエンスの同意がなければ、マイク・オンにできないユースケースの場合は、先ず `sendInvitation` をコールしてからオーディエンスにリクエストし、 `onInvitationAccept ` を受信してから、その関数をコールすることができます。

### muteSeat

任意のマイクのミュート／ミュート解除（キャスターがコール）。

>? 任意のマイクのミュート/ミュート解除では、ルーム内の全メンバーが `onSeatListChange` および `onSeatMute` のインシデント通知を受信します。

```java
public abstract void muteSeat(int seatIndex, boolean isMute, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                          |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | int            | 操作の必要があるマイク番号。                          |
| isMute    | boolean        | true：対応マイクのミュート；false：対応マイクのミュート解除。 |
| callback  | ActionCallback | 操作コールバック。                                    |

このインターフェースをコールすると、すぐにマイクリストが修正されます。 seatIndex の座席に該当するキャスターは、 muteAudio を自動的にコールしてミュート／ミュートオフにします。

### closeSeat

任意のマイクのクローズ/解除（キャスターがコール）。

>? キャスターは、該当するマイクをクローズ/解除し、ルーム内の全メンバーは `onSeatListChange` および `onSeatClose` のインシデント通知を受信します。

```java
public abstract void closeSeat(int seatIndex, boolean isClose, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                                       |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | int            | 操作の必要があるマイク番号。                       |
| isClose   | boolean        | true：該当するマイクのクローズ； false：該当するマイクのクローズ解除。 |
| callback  | ActionCallback | 操作コールバック。                                    |

このインターフェースをコールすると、すぐにマイクリストが修正されます。対応するseatIndex をクローズされた座席上のキャスターは、自動的にマイク・オフになります。


## ローカル音声操作インターフェース

### startMicrophone

マイクの集音開始。 

```java
public abstract void startMicrophone();
```

### stopMicrophone

マイクの集音停止。 

```java
public abstract void startMicrophone();
```

### setAudioQuality

音質の設定。

```java
public abstract void setAudioQuality(int quality);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 音声品質。詳細は [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルの音声のミュート／ミュート取り消し

```java
public abstract void muteLocalAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | ミュート／ミュート取り消し。詳細は [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |



### setSpeaker

スピーカーの起動設定。

```java
public abstract void setSpeaker(boolean useSpeaker);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true：スピーカー；false：ヘッドホン。 |



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

ミュート／ミュート解除指定メンバー。

```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| userId | String           | 指定ユーザー ID。        |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |

### muteAllRemoteAudio

ミュート／ミュート解除全メンバー。 |

```java
public abstract void muteAllRemoteAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |

   

## バックグラウンドミュージック・サウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でのテキストメッセージの放送には、通常弾幕によるチャットを使用します。

```java
public abstract void sendRoomTextMsg(String message, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| message  | String         | テキストメッセージ。     |
| callback  | ActionCallback | 発信結果のコールバック。 |

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを発信します。

```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | String         | コマンドワードは、開発者がカスタマイズ。主に異なるメッセージタイプを区分するのに使用。 |
| message  | String         | テキスト情報。                                         |
| callback  | ActionCallback | 発信結果のコールバック。                                    |

   

## 招待シグナリング関連インターフェース

### sendInvitation

ユーザーに招待を発信。

```java
public abstract String sendInvitation(String cmd, String userId, String content, TRTCVoiceRoomCallback.ActionCallback callback);
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

```java
public abstract void acceptInvitation(String id, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待 ID。      |
| callback  | ActionCallback | 発信結果のコールバック。 |

### rejectInvitation

招待の辞退。

```java
public abstract void rejectInvitation(String id, TRTCVoiceRoomCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味     |
| ---- | ------ | -------- |
| id   | String | 招待 ID。 |
| callback  | ActionCallback | 発信結果のコールバック。|


### cancelInvitation

招待の取り消し。

```java
public abstract void cancelInvitation(String id, TRTCVoiceRoomCallback.ActionCallback callback);
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

```java
void onError(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message  | String  | エラーメッセージ。 |


### onWarning

警告のコールバック。

```java
void onError(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| code   | int    | エラーコード。   |
| message | String | 警告メッセージ。 |

   

### onDebugLog

Log コールバック。

```java
void onDebugLog(String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | ログ情報。 |

   


## ルームイベントのコールバック

### onRoomDestroy

ルーム廃棄のコールバック。キャスターがルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

```java
void onRoomDestroy(String roomId);
```

パラメータは下表に示すとおりです。

|パラメータ     | タイプ        | 意味|
| ------ | ------ | --------- |
| roomId | String | ルーム ID。 |


### onRoomInfoChange

入室に成功後、このインターフェースをコールバックします。roomInfo は作成されたルームの情報を含みます。

```java
void onRoomInfoChange(TRTCVoiceRoomDef.RoomInfo roomInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味       |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | ルーム情報。 |

   

### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。

```java
void onUserVolumeUpdate(String userId, int volume);

```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
| ------ | ------ | ------------------------- |
| userId | String|  ユーザー ID。                 |
| volume | int    | 音量、値：0 - 100。 |


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
 マイク・オンの参加者（自主的にマイク・オン／キャスターがピックしてマイク・オン）。 

```java
void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user);
```
パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | int      | 参加者がマイク・オンのマイク。     |
| user  | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onAnchorLeaveSeat

マイク・オフの参加者（自主的にマイク・オフ／キャスターがキックしてマイク・オフ）。

```java
void onAnchorLeaveSeat(int index, TRTCVoiceRoomDef.UserInfo user);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ     | 意味                 |
| ----- | -------- | -------------------- |
| index | int      | マイク・オフのマイク。         |
| user  | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onSeatMute

キャスターのマイクミュート。

```java
void onSeatMute(int index, boolean isMute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                               |
| ------ | ------- | ---------------------------------- |
| index  | int     | 操作するマイク。                       |
| isMute    | boolean        | true：ミュートマイク；false：ミュート解除。 |

### onSeatClose

キャスターのマイククローズ。

```java
void onSeatClose(int index, boolean isClose);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                |
| ------- | ------- | ----------------------------------- |
| index  | int     | 操作するマイク。                       |
| isClose   | boolean        | true：マイクのクローズ； false：マイクのクローズ解除。 |

## 視聴者の入退室イベントのコールバック

### onAudienceEnter

視聴者入室通知の受信。

```java
void onAudienceEnter(TRTCVoiceRoomDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 入室した視聴者の情報。 |

### onAudienceExit

視聴者退室通知の受信。

```java
void onAudienceExit(TRTCVoiceRoomDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 退室した視聴者の情報。 |

   

## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```java
void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味             |
| -------- | -------- | ---------------- |
| message  | String         | テキストメッセージ。                                         |
| userInfo | UserInfo | 発信者ユーザーの情報。 |

   

### onRecvRoomCustomMsg

カスタマイズメッセージの受信。

```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCVoiceRoomDef.UserInfo userInfo);
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

```java
void onReceiveNewInvitation(String id, String inviter, String cmd, String content);
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

```java
void onInviteeAccepted(String id, String invitee);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待 ID。           |
| inviter | String | 被招待者のユーザー ID。 |

### onInviteeRejected

被招待者による招待の辞退。

```java
void onInviteeAccepted(String id, String invitee);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待 ID。           |
| inviter | String | 被招待者のユーザー ID。 |

### onInvitationCancelled

招待者が招待を取り消し。

```java
void onInvitationCancelled(String id, String inviter);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味               |
| ------- | ------ | ----------------- |
| id      | String | 招待 ID。         |
| inviter | String | 招待者のユーザー ID。 |
