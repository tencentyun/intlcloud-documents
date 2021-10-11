.TRTCChatSalonは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- 管理者は新しいボイスサロンを作成して配信を開始し、リスナーはボイスサロンに参加して視聴/インタラクションを行います。
- 管理者は、リスナーのマイク・オンに同意したり、マイク・オンのキャスターをキックアウトしたりすることもできます。
- リスナーはマイク・オンを申請して、マイク・オンのキャスターになり、他者と音声インタラクションを行うことができます。また、いつでもマイク・オフにして、通常のリスナーになることも可能です。
- 各種のテキストメッセージの送信をサポートします。

TRTCChatSalonは、オープンソースのClassであり、Tencent Cloudの2つのクローズドソースであるSDKに依存しています。具体的な実装プロセスについては、[ボイスサロン（Flutter）](https://intl.cloud.tencent.com/document/product/647/39805)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のボイスチャットコンポーネントとして使用します。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用してチャットルーム機能を実装します。同時にIMの属性インターフェースによって、マイクリストなどのルーム情報を保存し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。

[](id:TRTCChatSalon)

## TRTCChatSalon API概要

### SDK基本関数

| API                                             | 説明           |
| ----------------------------------------------- | -------------- |
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを廃棄します。 |
| [registerListener](#registerlistener)           | イベント監視を設定します。 |
| [unRegisterListener](#unregisterlistener)       | イベント監視を廃棄します。 |
| [login](#login)                                 | ログイン。         |
| [logout](#logout)                               | ログアウト。         |
| [setSelfProfile](#setselfprofile)               | 個人情報を修正します。           |

### ルーム関連インターフェース関数

| API                                     | 説明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)               | ルームの作成（管理者が呼び出し）。ルームが存在しない場合は、システムが新しいルームを自動的に作成します。 |
| [destroyRoom](#destroyroom)             | ルームの破棄（管理者が呼び出し）。                                       |
| [enterRoom](#enterroom)                 | 入室（リスナーが呼び出し）。                                       |
| [exitRoom](#exitroom)                   | 退室（リスナーが呼び出し）。                                       |
| [getRoomInfoList](#getroominfolist)     | ルームリストの詳細情報を取得します。                              |
| [getRoomMemberList](#getroommemberlist) | ルーム内のすべてのユーザー情報を取得します。                              |
| [getArchorInfoList](#getarchorInfolist) | ルームのキャスターリストを取得します。                                           |
| [getUserInfoList](#getuserinfolist)     | 指定されたuserIdのユーザー情報を取得します。                                 |

### マイクのオン・オフインターフェース

| API                   | 説明                                 |
| --------------------- | ----------------------------------- |
| [enterMic](#entermic) | リスナーのマイク・オン。                          |
| [enterMic](#entermic) | キャスターのマイク・オフ。                          |
| [muteMic](#mutemic)   | 任意のマイクのミュート/ミュート解除（キャスターが呼び出し）。 |
| [kickMic](#kickmic)   | キックアウトしてマイク・オフ（管理者が呼び出し）。              |

### ローカルのオーディオ操作インターフェース

| API                                             | 説明                  |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | マイクの集音開始。     |
| [stopMicrophone](#stopmicrophone)               | マイクの集音停止。     |
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

| API                                             | 説明                                                          |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | バックグラウンド・サウンドエフェクト管理オブジェクト[TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。 |

### メッセージ送信関連インターフェース

| API                                 | 説明                                     |
| ----------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | ルーム内でのテキストメッセージのブロードキャストには、通常、弾幕によるチャットを使用します。|

### マイク・オン申請シグナリング関連インターフェース

| API                             | 説明           |
| ------------------------------- | -------------- |
| [raiseHand](#raisehand)         | リスナーがマイク・オンを申請しました。 |
| [agreeToSpeak](#agreetospeak)   | 管理者はマイク・オンに同意しました。 |
| [refuseToSpeak](#refusetospeak) | 管理者はマイク・オンを拒否しました。 |

[](id:TRTCChatSalonDelegate)
## TRTCChatSalonDelegate API概要

### 一般的なイベントコールバック

| API                                 | 説明       |
| ----------------------------------- | ---------- |
| [onError](#onerror)                 | エラーのコールバック。 |
| [onWarning](#onwarning)             | 警告のコールバック。 |
| [onKickedOffline](#onkickedoffline) | キックアウトされてオフラインになります。 |

### ルームイベントのコールバック

| API                                       | 説明                   |
| ----------------------------------------- | ------------------------ |
| [onRoomDestroy](#onroomdestroy)           | ルームが廃棄されたときのコールバック。       |
| [onAnchorListChange](#onanchorlistchange) | キャスターリストに変更があったときのコールバック。 |
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。       |

### マイク変更コールバック

| API                                   | 説明                                  |
| ------------------------------------- | ------------------------------------- |
| [onAnchorEnterMic](#onanchorentermic) | 発言者のメンバーがいます（ユーザーが発言者になる/管理者が視聴者を発言できるように招待）。 |
| [onAnchorLeaveMic](#onanchorleavemic) | 視聴者のメンバーがいます（ユーザーが視聴者になる/管理者がキックアウトしてマイク・オフ）。 |
| [onMicMute](#onmicmute)               | キャスターのマイクミュート。                          |

### リスナーの入退室イベントのコールバック

| API                                 | 説明               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) |リスナー入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | リスナー退室通知の受信。|

### メッセージイベントのコールバック

| API                                     | 説明          |
| --------------------------------------- | -------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | テキストメッセージの受信。 |

## マイク・オン申請シグナリングイベントのコールバック

| API                                    | 説明                                     |
| -------------------------------------- | ---------------------------------------- |
| [onRaiseHand](#onraisehand) | 挙手してマイク・オン申請しているリスナーがいます。                   |
| [onAgreeToSpeak](#onagreetospeak)   | リスナーが挙手を申請すると、管理者から挙手に同意するコールバックを受け取ります。 |
| [onRefuseToSpeak](#onrefusetospeak)    | リスナーが挙手を申請すると、管理者が挙手のコールバックを拒否します。     |

## SDK基本関数

### sharedInstance

TRTCChatSalonシングルトンオブジェクトを取得します。

```dart
 static Future<TRTCChatSalon> sharedInstance()
```


### destroySharedInstance

TRTCChatSalonシングルトンオブジェクトを廃棄します。

>?インスタンスを破棄すると、外部キャッシュのTRTCChatSalonインスタンスは再利用できなくなります。あらためて[sharedInstance](#sharedInstance)を呼び出し、新しいインスタンスを取得する必要があります。

```dart
static void destroySharedInstance()
```

### registerListener

イベント監視の設定

```
void registerListener(VoiceListenerFunc func)
```

>?setDelegateはTRTCChatSalonのプロキシコールバックです。   

### unRegisterListener

コンポーネントイベントの監視インターフェースを削除します。

```dart
void unRegisterListener(VoiceListenerFunc func)
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ              | 意味                                                      |
| ---- | ----------------- | --------------------------------------------------------- |
| func | VoiceListenerFunc | TRTCChatSalonの各種ステータス通知は、指定したfunc関数に発信されます |


### login

ログイン。

```dart
Future<ActionCallback> login(int sdkAppId, String userId, String userSig)
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ    | 意味                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| sdkAppId | int    | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報の中でSDKAppIDを確認できます。 |
| user     | String | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |


### logout

ログアウト。

```dart
Future<ActionCallback> logout()
```

### setSelfProfile

個人情報の修正。

```dart
Future<ActionCallback> setSelfProfile(String userName, String avatarURL)
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味       |
| --------- | ------ | ---------- |
| userName | String | ニックネーム。 |
| avatarURL | String | プロフィール画像URL。 |

## ルーム関連インターフェース関数

### createRoom

ルームを作成します（新しいルームを作成するときに呼び出します）。

```
Future<ActionCallback> createRoom(int roomId, RoomParam roomParam)
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ      | 意味                                                         |
| --------- | --------- | ------------------------------------------------------------ |
| roomId    |  intt       | ルームIDは、ご自身でアサインし、統一管理する必要があります。複数のroomIDを、一つのボイスサロンのルームリストにまとめることができます。Tencent Cloudでは現在、ボイスサロンのルームリストの管理サービスを行っていませんので、ご自身でボイスサロンのルームリストを管理してください。 |
| roomParam | RoomParam | ルーム情報は、ルームについて説明するための情報です。例えば、ルーム名、カバー情報などです。     |

管理者が配信を開始する際の通常の呼び出しプロセスは次のとおりです。 

1. 管理者は`createRoom`を呼び出して新しいボイスサロンを作成し、ルームIDなどルームの属性情報を渡します。
2. 管理者はマイクリストのメンバーが参加した`onAnchorEnterMic`というイベント通知も受信します。この時、マイク集音は自動的に開始されます。

### destroyRoom

ルームの破棄（管理者が呼び出し）。管理者は、ルーム作成後、この関数を呼び出してルームを破棄します。

```dart
Future<ActionCallback> destroyRoom()
```


### enterRoom

入室（リスナーが呼び出し）

```dart
Future<ActionCallback> enterRoom(int roomId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味       |
| ------ | ---- | ---------- |
| roomId | int | ルームID。 |


リスナーが入室し視聴する際の通常の呼び出しプロセスは次のとおりです。 

1. リスナーがサーバーから取得する最新のボイスサロンリストには、多くのボイスサロンのroomIdおよびルーム情報が含まれる場合があります。
2. リスナーはボイスサロンの1つを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
3. 入室後、`getArchorInfoList`を確認してキャスターリストを取得してから、`getRoomMemberList`に基づいて、すべてのユーザーリストを取得してキャスターリストを差し引けば、リスナーリストを取得することができます。
4. 入室後、マイクリストにキャスターが参加した`onAnchorEnterMic`というイベント通知も受信します。

### exitRoom

ルームから退出します。

```dart
Future<ActionCallback> exitRoom()
```

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、管理者が`createRoom()`作成時にroomInfoによって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```dart
Future<RoomInfoCallback> getRoomInfoList(List<String> roomIdList)
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味         |
| ---------- | ------------------- | ------------ |
| roomIdList | List&lt;String&gt; | ルームナンバーリスト。 |


### getRoomMemberList

ルーム内の全メンバーのリストを取得します。

>?IMライブストリーミンググループは、デフォルトで直近メンバー31人のリストだけをプルすることができます。


```dart
Future<MemberListCallback> getRoomMemberList(double nextSeq)
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                                                         |
| ------- | ------ | ------------------------------------------------------------ |
| nextSeq | double | ページネーションプルフラグ。最初のプルに0と入力すると、コールバックは成功します。nextSeqがゼロでない場合は、ページネーションが必要であり、0になるまで渡して再度プルされます。 |

### getArchorInfoList

ルーム内のキャスターリストを取得します。

```dart
Future<UserListCallback> getArchorInfoList()
```


### getUserInfoList

指定されたuserIdのユーザー情報を取得します。

```dart
Future<UserListCallback> getUserInfoList(List<String> userIdList)
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ               |意味                                                         |
| ---------- | ------------------ | ------------------------------------------------------------ |
| userIdList | List&lt;String&gt; | 取得すべきユーザーIDリスト。nullの場合は、ルーム内全員の情報を取得します。 |


## マイクのオン・オフインターフェース

### enterMic

マイク・オン（リスナー側/管理者ともに呼び出し可）します。

>?マイク・オンが成功した後、ルーム内の全メンバーは`onAnchorEnterSeat`というイベント通知を受信します。

```
Future<ActionCallback> enterMic();
```

このインターフェースを呼び出すと、マイクリストが直ちに変更されます。リスナーがまず`raiseHand`を呼び出して管理者に申請する必要がある場合は、`onAgreeToSpeak`を受信した後にこの関数を呼び出します。

### leaveMic

キャスターのマイク・オフ。

>? マイク・オフが成功した後、ルーム内の全メンバーは`onAnchorLeaveMic`というイベント通知を受信します。

```dart
Future<ActionCallback> leaveMic()
```

### muteMic

任意のマイクのミュート/ミュート解除（管理者が呼び出し）。

>? マイク・オンの成功後、ルーム内の全メンバーは、`onAnchorListChange`および`onMicMute`というイベント通知を受信します。

```dart
Future<ActionCallback> muteMic(bool mute)
```

### kickMic

キックアウトしてマイク・オフ（管理者が呼び出し）。

>? 管理者がキックアウトしてマイク・オフにすると、ルーム内の全メンバーは`onAnchorLeaveMic`というイベント通知を受信します。

```dart
Future<ActionCallback> kickMic(String userId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                 |
| ------ | ------ | -------------------- |
| userId | String |キックアウトしてマイク・オフにする必要のあるユーザーID。 |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。


## ローカルのオーディオ操作インターフェース

### startMicrophone

マイクの集音開始。

```dart
void startMicrophone(int quality)
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 音声品質。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |

### stopMicrophone

マイクの集音停止。

```dart
void stopMicrophone()
```

### muteLocalAudio

ローカルのオーディオのミュート/ミュート取り消し。

```dart
void muteLocalAudio(bool mute)
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | bool | ミュート/ミュート取り消し。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |


### setSpeaker

スピーカーの起動設定。

```dart
void setSpeaker(bool useSpeaker)
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | bool | true：スピーカー、false：ヘッドホン。 |



### setAudioCaptureVolume

マイクの集音音量設定。

```dart
void setAudioCaptureVolume(int volume)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 集音音量、0 - 100、 デフォルト100。 |


### setAudioPlayoutVolume

再生音量の設定。

```dart
void setAudioPlayoutVolume(int volume)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 再生音量、0 - 100、 デフォルト100。 |

### muteRemoteAudio

指定メンバーのミュート/ミュート解除。

```dart
void muteRemoteAudio(String userId, bool mute)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                              |
| ------ | ------- | --------------------------------- |
| userId | String  | 指定ユーザーID。                   |
| mute   | bool | true：ミュート起動、false：ミュート停止。 |

### muteAllRemoteAudio

全メンバーのミュート/ミュート解除。

```dart
void muteAllRemoteAudio(bool mute)
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | bool | true：ミュート起動、false：ミュート停止。 |


## BGMサウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```dart
TXAudioEffectManager getAudioEffectManager()
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットに使用します。

```dart
Future<ActionCallback> sendRoomTextMsg(String message)
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | テキストメッセージ。 |

   

## マイク・オン申請シグナリング関連インターフェース

### raiseHand

リスナーがマイク・オンを申請しました。

```dart
void raiseHand()
```

### agreeToSpeak

管理者がマイク・オンに同意しました。

```dart
Future<ActionCallback> agreeToSpeak(String userId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味     |
| ------ | ------ | -------- |
| userId | String | ユーザーID。 |

### refuseToSpeak

管理者がユーザーのマイク・オンを拒否しました。

```dart
Future<ActionCallback> refuseToSpeak(String userId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味     |
| ------ | ------ | -------- |
| userId | String | ユーザーID。 |

[](id:TRTCChatSalonDelegate)
## TRTCChatSalonDelegateイベントコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。


パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味                                                     |
| --------- | ------ | -------------------------------------------------------- |
| errCode   | int    | エラーコード。                                                 |
| errMsg    | String | エラーメッセージ。                                               |
| extraInfo | String | 拡張情報フィールドでは、個別のエラーコードによる追加の情報が問題個所の特定に役立つ場合があります。 |

### onWarning

警告のコールバック。

パラメータは下表に示すとおりです。

| パラメータ        | タイプ   | 意味                                                     |
| ----------- | ------ | -------------------------------------------------------- |
| warningCode | int    | エラーコード。                                                 |
| warningMsg  | String | 警告メッセージ。                                               |
| extraInfo   | String | 拡張情報フィールドでは、個別のエラーコードによる追加の情報が問題個所の特定に役立つ場合があります。 |


### onKickedOffline

他のユーザーが同じアカウントでログインすると、キックアウトされてオフラインになります。


## ルームイベントのコールバック

### onRoomDestroy

ルーム破棄のコールバック。管理者がルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

### onAnchorListChange

キャスターリスト変更発生の通知。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味       |
| ------ | ------ | ---------- |
| userId | String | ユーザーID。  |
| mute   | bool   | ミュート状態。 |


### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
| ------ | ------ | ------------------------- |
| userId | String|  ユーザーID。                 |
| volume | int    | 音量の大きさ。値：0～100。 |


## マイクコールバック


### onAnchorEnterMic

マイク・オンのメンバー。

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味                 |
| ---------- | ------ | -------------------- |
| userId     | String | 入室したユーザーID。 |
| userName   | String | ユーザーのニックネーム。           |
| userAvatar | String | プロフィール画像URL。           |
| mute       | bool   | マイクステータス。デフォルトではマイク・オンになっています。 |

### onAnchorLeaveMic

マイク・オフのメンバー。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | ルームを退出したユーザーID。 |

### onMicMute

管理者のマイクミュートの有無。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | マイク・オフのユーザーID。 |
| mute   | bool   | マイクステータス。     |


## リスナーの入退室イベントのコールバック

### onAudienceEnter

リスナー入室通知の受信。


パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味           |
| ---------- | ------ | -------------- |
| userId     | String | マイク・オンのユーザーID。       |
| userName   | String | ユーザーのニックネーム。     |
| userAvatar | String | プロフィール画像URL。     |

### onAudienceExit

リスナー退室通知の受信。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | マイク・オフのユーザーID。 |


## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味             |
| ---------- | ------ | ---------------- |
| message    | String | テキストメッセージ。       |
| sendId     | String | 送信者のユーザーID。   |
| userAvatar | String | 送信者のユーザープロフィール画像URL。 |
| userName   | String | 送信者のユーザーニックネーム。 |


## 挙手申請シグナリングイベントのコールバック

### onRaiseHand

新規マイクリクエストの受信。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味               |
| ------ | ------ | ------------------ |
| userId | String | 挙手申請したユーザーID。 |


### onAgreeToSpeak

管理者によるマイク・オン同意のコールバック。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | 管理者のユーザーID。 |

### onRefuseToSpeak

管理者によるマイク・オン拒否のコールバック。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | 管理者のユーザーID。 |
