TRTCChatSalonは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- キャスターが新しいボイスサロンを作成して配信を開始し、視聴者がボイスサロンに参加して視聴/インタラクティブなコミュニケーションを図ります。
- キャスターは、視聴者をマイク・オンに招待したり、マイク・オンのキャスターをマイク・オフにしたりすることもできます。
- 視聴者はマイク・オンを申請して、マイク・オンのキャスターになり、他者と対話することができます。また、いつでもマイク・オフにして、通常の視聴者になることも可能です。
- さまざまなテキストメッセージやカスタムメッセージの送信をサポートしており、カスタムメッセージを使用して、弾幕、「いいね」、ギフトなどを実装できます。

TRTCChatSalonは、オープンソースのClassであり、Tencent Cloudの2つのクローズドソースであるSDKに依存しています。具体的な実装プロセスについては、[ボイスサロン（Android）](https://intl.cloud.tencent.com/document/product/647/53537)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647)を低遅延のボイスチャットコンポーネントとして使用しています。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用してチャットルーム機能を実装します。同時にIMのインターフェース属性によって、マイクリストなどのルーム情報を保存し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。

[](id:TRTCChatSalon)

## TRTCChatSalon API概要

### SDK基本関数

| API                                             | 説明                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを廃棄します。                                   |
| [setDelegate](#setdelegate)                     | イベントコールバックを設定します。     |
| [setDelegateHandler](#setdelegatehandler)       |イベントのコールバックが配置されているスレッドを設定します。 |
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
| [getUserInfoList](#getuserinfolist) | 指定されたuserIdのユーザー情報を取得します。 nullの場合は、ルーム内全員の情報を取得します。 |

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
| [muteRemoteAudio](#muteremoteaudio)       | ミュート/ミュート解除指定メンバー。 |
| [muteAllRemoteAudio](#muteallremoteaudio) | ミュート/ミュート解除全メンバー。 |

### バックグラウンドミュージック・サウンドエフェクト関連インターフェース

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | バックグラウンド・サウンドエフェクト管理オブジェクト[TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。 |

### メッセージ送信関連インターフェース

| API                                     | 説明                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージのブロードキャストには、通常、弾幕によるチャットを使用します。｜
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

| API                                       | 説明                       |
| ----------------------------------------- | -------------------------- |
| [onRoomDestroy](#onroomdestroy)           | ルームが廃棄されたときのコールバック。         |
| [onRoomInfoChange](#onroominfochange) | ボイスサロン情報変更のコールバック。|
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。         |

### マイク変更コールバック

| API                                            | 説明                                   |
| ---------------------------------------------- | -------------------------------------- |
| [onAnchorEnterSeat](#onanchorenterseat)       |マイク・オンのメンバー（自主的にマイク・オン/キャスターがピックしてマイク・オン）。  |
| [onAnchorLeaveSeat](#onanchorleaveseat) | マイク・オフのメンバー（自主的にマイク・オフ/キャスターがキックアウトしてマイク・オフ）。  |
| [onSeatMute](#onseatmute)                      | キャスターのマイクミュート。                             |

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

## シグナリングイベントのコールバック

| API                                               | 説明               |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 新規招待リクエストの受信。 |
| [onInviteeAccepted](#oninviteeaccepted)           | 被招待者が招待に同意。 |
| [onInviteeRejected](#oninviteerejected)           | 被招待者による招待の辞退。 |
| [onInvitationCancelled](#oninvitationcancelled)   | 招待者が招待を取り消し。   |

## SDK基本関数

### sharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/53537) シングルトンオブジェクトの取得。

```java
 public static synchronized TRTCChatSalon sharedInstance(Context context);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| context | Context | Androidコンテキスト。内部ではApplicationContextに変換してシステムAPIの呼び出しに使用します |


### destroySharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/53537)シングルトンオブジェクトを廃棄します。

>?インスタンスを廃棄すると、外部キャッシュのTRTCChatSalonインスタンスは再利用できなくなります。あらためて[sharedInstance](#sharedInstance)を呼び出し、新しいインスタンスを取得する必要があります。

```java
public static void destroySharedInstance();
```

### setDelegate
[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/53537)イベントコールバック。TRTCChatSalonDelegateを介して[TRTCChatSalon](https://cloud.tencent.com/document/product/647/53537)の各種ステータス通知を受け取ることができます。

```java
public abstract void setDelegate(TRTCChatSalonDelegate delegate);
```

>?setDelegateはTRTCChatSalonのプロキシコールバックです。   

### setDelegateHandler
イベントコールバックが配置されているスレッドを設定します。

```java
public abstract void setDelegateHandler(Handler handler);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ    | 意味                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| handler | Handler | TRTCChatSalonの各種ステータス通知は、指定したhandlerスレッドに発信されます。 |

   

### login

ログイン。

```java
public abstract void login(int sdkAppId,
 String userId, String userSig,
TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int         | TRTCコンソール> 【[アプリケーション管理]（https://console.cloud.tencent.com/trtc/app）】>アプリケーション情報の中でSDKAppIDを確認できます。 |
| userId   | String                | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String         |Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallback | ログインのコールバック。成功時にcodeは0になります。                                  |

   

### logout

ログアウト。

```java
public abstract void logout(TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                        |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | ログアウトのコールバック。成功時にcodeは0になります。 |

   

### setSelfProfile

個人情報の修正。

```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCChatSalonCallback.ActionCallback callback);
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

```java
public abstract void createRoom(int roomId, TRTCChatSalonDef.RoomParam roomParam, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ           | 意味                                                         |
| --------- | -------------- | ------------------------------------------------------------ |
| roomId    | int            | ルームIDは、ご自身でアサインし、統一管理する必要があります。複数のroomIDを、一つのボイスサロンのルームリストにまとめることができます。Tencent Cloudでは現在、ボイスサロンのルームリストの管理サービスを行っていませんので、ご自身でボイスサロンのルームリストを管理してください。 |
| roomParam | RoomParam      | ルーム情報は、ルームについて説明するための情報です。例えば、ルーム名、マイク情報、カバー情報などです。 |
| callback  | ActionCallback | ルームの新規作成結果のコールバック。成功時にcodeは0になります。 |

キャスターがブロードキャストを開始する際の通常の呼び出しプロセスは次のとおりです。 

1. キャスターは、`createRoom`を呼び出して新しいボイスサロンを作成します。このとき、ルームID、マイク・オンに管理者の確認の要否などルームの属性情報を渡します。
2. キャスターは、ルーム作成に成功した後、`enterSeat` を呼び出して参加します。
3. キャスターは、マイクリストのメンバーが参加した`onAnchorEnterSeat`のイベント通知も受信します。このとき、マイク集音は自動的に開始されます。

   

### destroyRoom

ルームの廃棄（キャスターが呼び出し）。キャスターは、ルーム作成後、この関数を呼び出してルームを廃棄します。

```java
public abstract void destroyRoom(TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | ルームの廃棄結果のコールバック。成功時にcodeは0になります。 |


### enterRoom

入室（視聴者が呼び出し）

```java
public abstract void enterRoom(int roomId, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | int            | ルームID。                            |
| callback | ActionCallback | 入室結果のコールバック。成功時にcodeは0になります。 |


視聴者が入室し視聴する際の通常の呼び出しプロセスは次のとおりです。 

1. 視聴者がサーバーから取得する最新のボイスサロンリストには、多くのボイスサロンのroomIdおよびルーム情報が含まれる場合があります。
2．視聴者は一つのボイスサロンを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
3. 入室後、コンポーネントの`onRoomInfoChange`というルーム属性の変更イベント通知を受信します。このとき、ルーム属性を記録し、UIに表示されるルーム名、マイク・オンにキャスターへの同意のリクエストの要否の記録など、対応する変更を行うことができます。
4. 入室後に、マイクリストにキャスターが参加した`onAnchorEnterSeat`のイベント通知も受信します。

### exitRoom

ルームを退出します。

```java
public abstract void exitRoom(TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 退室結果のコールバック。成功時にcodeは0になります。 |

   

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、キャスターが`createRoom()`作成時にroomInfoによって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```java
public abstract void getRoomInfoList(List<Integer> roomIdList, TRTCChatSalonCallback.RoomInfoCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味               |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | ルームナンバーリスト。       |
| callback   | RoomInfoCallback    | ルーム詳細情報のコールバック。 |


### getUserInfoList

指定されたuserIdのユーザー情報を取得します。

```java
public abstract void getUserInfoList(List<String> userIdList, TRTCChatSalonCallback.UserListCallback userlistcallback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                      | 意味                                                       |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt; | 取得すべきユーザーIDリスト。nullの場合は、ルーム内全員の情報を取得します。 |
| userlistcallback | UserListCallback   | ユーザーの詳細情報のコールバック。                                          |


## マイクのオン・オフインターフェース

### enterSeat

自主的にマイク・オン（視聴者/キャスターともに呼び出し可）します。

>?マイク・オンが成功した後、ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。

```java
public abstract void enterSeat(TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 操作コールバック。 |

このインターフェースを呼び出すと、すぐにマイクリストが変更されます。視聴者がキャスターからの申請を必要とするシーンの場合は、まず`sendInvitation`を呼び出してからキャスターに申請し、`onInvitationAccept `を受信した後にこの関数を呼び出すことができます。

### leaveSeat

自主的にマイク・オフ（視聴者/キャスターともに呼び出し可）します。

>? マイク・オフが成功した後、ルーム内の全メンバーは`onAnchorLeaveSeat`のイベント通知を受信します。

```java
public abstract void leaveSeat(TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 操作コールバック。 |

### pickSeat

ピックしてマイク・オン（キャスターが呼び出し）。

>? キャスターがピックしてマイク・オンにすると、ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。

```java
public abstract void pickSeat(String userId, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味       |
| -------- | -------------- | ---------- |
| userId   | String         | ユーザーID。  |
| callback | ActionCallback | 操作コールバック。 |

このインターフェースを呼び出すと、すぐにマイクリストが変更されます。キャスターが、マイク・オンするために視聴者の同意を必要とするシーンの場合は、まず`sendInvitation`を呼び出してから視聴者に申請し、`onInvitationAccept `を受信した後にこの関数を呼び出すことができます。


### kickSeat

キックアウトしてマイク・オフ（キャスターが呼び出し）。

>? キャスターがキックアウトしてマイク・オフにすると、ルーム内の全メンバーは`onAnchorLeaveSeat`のイベント通知を受信します。

```java
public abstract void kickSeat(String userId, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                |
| -------- | -------------- | -------------------- |
| userId   | String         | キックアウトしてマイク・オフにする必要のあるユーザーID。 |
| callback  | ActionCallback | 操作コールバック。           |

このインターフェースを呼び出すと、すぐにマイクリストが変更されます。キャスターが、マイク・オンするために視聴者の同意を必要とするシーンの場合は、まず`sendInvitation`を呼び出してから視聴者に申請し、`onInvitationAccept `を受信した後にこの関数を呼び出すことができます。


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

| パラメータ    | タイプ | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 音声品質。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルの音声のミュート/ミュート取り消し。

```java
public abstract void muteLocalAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                                                         |
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

| パラメータ   | タイプ | 意味                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 再生音量、0 - 100、 デフォルト100。 |

### muteRemoteAudio

指定メンバーのミュート/ミュート解除。

```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                              |
| ------ | ------- | --------------------------------- |
| userId | String  | 指定ユーザーID。                   |
| mute   | boolean | true：ミュート起動；false：ミュート停止。 |

### muteAllRemoteAudio

全メンバーのミュート/ミュート解除。

```java
public abstract void muteAllRemoteAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |

   

## バックグラウンドミュージック・サウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットを使用します。

```java
public abstract void sendRoomTextMsg(String message, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| message  | String         | テキストメッセージ。     |
| callback | ActionCallback | 送信結果のコールバック。 |

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。

```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCChatSalonCallback.ActionCallback callback);
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
public abstract String sendInvitation(String cmd, String userId, String content, TRTCChatSalonCallback.ActionCallback callback);
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
public abstract void acceptInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。 |

### rejectInvitation

招待の拒否。

```java
public abstract void rejectInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。 |


### cancelInvitation

招待の取り消し。

```java
public abstract void cancelInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
| -------- | -------------- | -------------- |
| id       | String         | 招待ID。      |
| callback | ActionCallback | 送信結果のコールバック。 |

## TRTCChatSalonDelegateイベントコールバック

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

ルーム廃棄のコールバック。キャスターがルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

```java
void onRoomDestroy(String roomId);
```

パラメータは下表に示すとおりです。

|パラメータ     | タイプ   | 意味      |
| ------ | ------ | --------- |
| roomId | String | ルームID。 |


### onRoomInfoChange

入室に成功後、このインターフェースをコールバックします。roomInfoは作成されたルームの情報を含みます。

```java
void onRoomInfoChange(TRTCChatSalonDef.RoomInfo roomInfo);
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
| userId | String|  ユーザーID。                 |
| volume | int    | 音量の大きさ。値：0～100。 |


## マイクコールバック

### onAnchorEnterSeat

マイク・オンのメンバー（自主的にマイク・オン/キャスターがピックしてマイク・オン）。

```java
void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo user);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ     | 意味                 |
| ---- | -------- | -------------------- |
| user | UserInfo | マイク・オンのユーザーの詳細情報。 |

### onAnchorLeaveSeat

マイク・オフのメンバー（自主的にマイク・オフ/キャスターがキックアウトしてマイク・オフ）。

```java
void onAnchorLeaveSeat(TRTCChatSalonDef.UserInfo user);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ     | 意味                 |
| ---- | -------- | -------------------- |
| user | UserInfo | マイク・オンのユーザーの詳細情報。 |


### onSeatMute

キャスターのマイクミュート。

```java
void onSeatMute(String userId, boolean isMute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                               |
| ------ | ------- | ---------------------------------- |
| userId  | String     | マイクのユーザーID。                   |
| isMute | boolean | true：ミュートマイク；false：ミュート解除。 |



## 視聴者の入退室イベントのコールバック

### onAudienceEnter

視聴者入室通知の受信。

```java
void onAudienceEnter(TRTCChatSalonDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 入室した視聴者の情報。 |

### onAudienceExit

視聴者退室通知の受信。

```java
void onAudienceExit(TRTCChatSalonDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 退室した視聴者の情報。 |

   

## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```java
void onRecvRoomTextMsg(String message, TRTCChatSalonDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味             |
| -------- | -------- | ---------------- |
| message  | String  | テキストメッセージ。       |
| userInfo | UserInfo | 送信者のユーザー情報。 |

   

### onRecvRoomCustomMsg

カスタムメッセージの受信。

```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCChatSalonDef.UserInfo userInfo);
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
| content | UserInfo | 業務指定のコンテンツ。                   |

### onInviteeAccepted

被招待者が招待に同意。

```java
void onInviteeAccepted(String id, String invitee);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待ID。           |
| inviter | String | 被招待者のユーザーID。 |

### onInviteeRejected

被招待者による招待の拒否。

```java
void onInviteeRejected(String id, String invitee);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                |
| ------- | ------ | ------------------- |
| id      | String | 招待ID。           |
| inviter | String | 被招待者のユーザーID。 |

### onInvitationCancelled

招待者が招待を取り消し。

```java
void onInvitationCancelled(String id, String inviter);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味               |
| ------- | ------ | ----------------- |
| id      | String | 招待ID。         |
| inviter | String | 招待者のユーザーID。 |

### onInvitationTimeout

招待のタイムアウト。

```java
void onInvitationTimeout(String id);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味               |
| ------- | ------ | ----------------- |
| id      | String | 招待ID。         |
