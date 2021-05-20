TRTCChatSalonは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- キャスターが新しいボイスサロンを作成して配信を開始し、視聴者がボイスサロンに参加して視聴/インタラクティブなコミュニケーションを図ります。
- キャスターは、視聴者のマイク・オンに同意したり、マイク・オンのキャスターをキックアウトしたりすることもできます。
- 視聴者はマイク・オンを申請して、マイク・オンのキャスターになり、他者と対話することができます。また、いつでもマイク・オフにして、通常の視聴者になることも可能です。
- 各種のテキストメッセージの送信をサポートします。

TRTCChatSalonは、オープンソースのClassであり、Tencent Cloudの2つのクローズソースであるSDKに依存しています。具体的な実装プロセスについては、[ボイスサロン（Flutter）](https://cintl.loud.tencent.com/document/product/647/53582)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647)を低遅延のボイスチャットコンポーネントとして使用しています。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のAVChatroomを使用してチャットルーム機能を実装します。同時にIMのインターフェース属性によって、マイクリストなどのルーム情報を保存し、招待シグナリングはマイク・オン/ピックのリクエストに用いることができます。

[](id:TRTCChatSalon)

## TRTCChatSalon API概要

### SDK基本関数

| API                                             | 説明           |
| ----------------------------------------------- | -------------- |
| [sharedInstance](#sharedinstance) | シングルトンオブジェクトを取得します。 |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを廃棄します。 |
| [registerListener](#registerlistener)           | イベント監視を設定します。 |
| [unRegisterListener](#unregisterlistener)       | イベント監視を廃棄します。 |
| [login](#login)                                 | ログイン。         |
| [logout](#logout)                               | ログアウト。         |
| [setSelfProfile](#setselfprofile)               |  個人情報を修正します。 |

### ルーム関連インターフェース関数

| API                                     | 説明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)               | ルームの新規作成（キャスターが呼び出し）。ルームが存在しない場合は、システムが新しいルームを自動的に作成します。 |
| [destroyRoom](#destroyroom)             |ルームの廃棄（キャスターが呼び出し）。                                       |
| [enterRoom](#enterroom)                 | 入室（視聴者が呼び出し）。                                       |
| [exitRoom](#exitroom)                   | 退室（視聴者が呼び出し）。                                       |
| [getRoomInfoList](#getroominfolist)     | ルームリストの詳細情報を取得します。                              |
| [getRoomMemberList](#getroommemberlist) | ルーム内のすべてのユーザー情報を取得します。                              |
| [getArchorInfoList](#getarchorInfolist) | ルームのキャスターリストを取得します。                                           |
| [getUserInfoList](#getuserinfolist)     | 指定されたuserIdのユーザー情報を取得します。                                 |

### マイクのオン・オフインターフェース

| API                   | 説明                                 |
| --------------------- | ----------------------------------- |
| [enterMic](#entermic) | 視聴者のマイク・オン。                          |
| [enterMic](#entermic) | キャスターのマイク・オフ。                          |
| [muteSeat](#muteseat)   | 任意のマイクのミュート/ミュート解除（キャスターが呼び出し）。 |
| [kickMic](#kickmic)   | キックアウトしてマイク・オフ（グループマスターが呼び出し）。              |

### ローカルの音声操作インターフェース

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
| [muteRemoteAudio](#muteremoteaudio)       | ミュート/ミュート解除指定メンバー。 |
| [muteAllRemoteAudio](#muteallremoteaudio) | ミュート/ミュート解除全メンバー。 |

### バックグラウンドミュージック・サウンドエフェクト関連インターフェース

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | バックグラウンド・サウンドエフェクト管理オブジェクト[TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。 |

### メッセージ送信関連インターフェース

| API                                 | 説明                                     |
| ----------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | ルーム内でのテキストメッセージのブロードキャストには、通常、弾幕によるチャットを使用します。｜

### マイク・オン申請シグナリング関連インターフェース

| API                             | 説明           |
| ------------------------------- | -------------- |
| [raiseHand](#raisehand)         |視聴者からのマイク・オン申請。 |
| [agreeToSpeak](#agreetospeak)   | グループマスターによるマイク・オンの同意。 |
| [refuseToSpeak](#refusetospeak) | グループマスターによるマイク・オンの拒否。 |

[](id:TRTCChatSalonDelegate)
## TRTCChatSalonDelegate API概要

### 一般的なイベントコールバック

| API                                 | 説明       |
| ----------------------------------- | ---------- |
| [onError](#onerror)                 | エラーのコールバック。 |
| [onWarning](#onwarning)             | 警告のコールバック。 |
| [onKickedOffline](#onkickedoffline) | 警告のコールバック。 |

### ルームイベントのコールバック

| API                                       | 説明                     |
| ----------------------------------------- | ------------------------ |
| [onRoomDestroy](#onroomdestroy)           | ルームが廃棄されたときのコールバック。       |
| [onAnchorListChange](#onanchorlistchange) | キャスターリストに変更があったときのコールバック。 |
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。       |

### マイク変更コールバック

| API                                   | 説明                                  |
| ------------------------------------- | ------------------------------------- |
| [onAnchorEnterMic](#onanchorentermic) | マイク・オンのメンバー（自主的にマイク・オン/グループマスターがピックしてマイク・オン）。 |
| [onAnchorLeaveMic](#onanchorleavemic) | マイク・オフのメンバー（自主的にマイク・オフ/グループマスターがキックアウトしてマイク・オフ）。 |
| [onMicMute](#onmicmute)               | キャスターのマイクミュート。                          |

### 視聴者の入退室イベントのコールバック

| API                                 | 説明               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) |視聴者入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | 視聴者退室通知の受信。|

### メッセージイベントのコールバック

| API                                     | 説明          |
| --------------------------------------- | -------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | テキストメッセージの受信。 |

## マイク・オン申請シグナリングイベントのコールバック

| API                                    | 説明                                     |
| -------------------------------------- | ---------------------------------------- |
| [onRaiseHand](#onraisehand) | 視聴者の挙手によるマイク・オンの申請。                   |
| [onAgreeToSpeak](#onagreetospeak)   | 視聴者は挙手を申請すると、グループマスターから挙手に同意するコールバックを受け取ります。 |
| [onRefuseToSpeak](#onrefusetospeak)    | 視聴者は挙手を申請すると、グループマスターから挙手を拒否するコールバックを受け取ります。 |

## SDK基本関数

### sharedInstance

TRTCChatSalonシングルトンオブジェクトを取得します。

```dart
 static Future<TRTCChatSalon> sharedInstance()
```


### destroySharedInstance

TRTCChatSalonシングルトンオブジェクトを廃棄します。

>?インスタンスを廃棄すると、外部キャッシュのTRTCChatSalonインスタンスは再利用できなくなります。あらためて[sharedInstance](#sharedInstance)を呼び出し、新しいインスタンスを取得する必要があります。

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
| userId   | String | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
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
| roomId    |  int       | ルームIDは、ご自身でアサインし、統一管理する必要があります。複数のroomIDを、一つのボイスサロンのルームリストにまとめることができます。Tencent Cloudでは現在、ボイスサロンのルームリストの管理サービスを行っていませんので、ご自身でボイスサロンのルームリストを管理してください。 |
| roomParam | RoomParam | ルーム情報は、ルームについて説明するための情報です。例えば、ルーム名、カバー情報などです。     |

キャスターがブロードキャストを開始する際の通常の呼び出しプロセスは次のとおりです。 

1. キャスターは、`createRoom`を呼び出して新しいボイスサロンを作成します。このとき、ルームIDなどルームの属性情報を渡します。
2. キャスターは、マイクリストのメンバーが参加した`onAnchorEnterMic`のイベント通知も受信します。このとき、マイク集音は自動的に開始されます。

### destroyRoom

ルームの廃棄（キャスターが呼び出し）。キャスターは、ルーム作成後、この関数を呼び出してルームを廃棄します。

```dart
Future<ActionCallback> destroyRoom()
```


### enterRoom

入室（視聴者が呼び出し）

```dart
Future<ActionCallback> enterRoom(int roomId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味       |
| ------ | ---- | ---------- |
| roomId | int | ルームID。 |


視聴者が入室し視聴する際の通常の呼び出しプロセスは次のとおりです。 

1. 視聴者がサーバーから取得する最新のボイスサロンリストには、多くのボイスサロンのroomIdおよびルーム情報が含まれる場合があります。
2．視聴者は一つのボイスサロンを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
3. 入室後、`getArchorInfoList`を確認してキャスターリストを取得してから、`getRoomMemberList`に基づいてすべてのユーザーリストを取得してキャスターリストを差し引けば、視聴者リストを取得することができます。
4. 入室後にマイクリストにキャスターが参加した`onAnchorEnterMic`のイベント通知も受信します。

### exitRoom

ルームを退出します。

```dart
Future<ActionCallback> exitRoom()
```

### getRoomInfoList

ルームリストの詳細情報を取得します。このうち、ルーム名、ルームカバーは、キャスターが`createRoom()`作成時にroomInfoによって設定したものになります。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```dart
Future<RoomInfoCallback> getRoomInfoList(List<String> roomIdList)
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味         |
| ---------- | ------------------- | ------------ |
| roomIdList | List&lt;Integer&gt; | ルームナンバーリスト。 |


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

マイク・オン（視聴者/キャスターともに呼び出し可）。

>?マイク・オンが成功した後、ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。

```
Future<ActionCallback> enterMic();
```

このインターフェースを呼び出すと、マイクリストがすぐに修正されます。視聴者がまず`raiseHand`を呼び出してキャスターに申請する必要がある場合は、`onAgreeToSpeak`を受信した後にこの関数を呼び出します。

### leaveMic

自主的なマイク・オフ。

>? マイク・オフが成功した後、ルーム内の全メンバーは`onAnchorLeaveMic`のイベント通知を受信します。

```dart
Future<ActionCallback> leaveMic()
```

### muteMic

任意のマイクのミュート/ミュート解除（キャスターが呼び出し）。

>? マイク・オンの成功後、ルーム内の全メンバーは、`onAnchorListChange`および`onMicMute`のイベント通知を受信します。

```dart
Future<ActionCallback> muteMic(bool mute)
```

### kickMic

キックアウトしてマイク・オフ（キャスターが呼び出し）。

>? キャスターがキックアウトしてマイク・オフにすると、ルーム内の全メンバーは`onAnchorLeaveMic`のイベント通知を受信します。

```dart
Future<ActionCallback> kickMic(String userId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                 |
| ------ | ------ | -------------------- |
| userId | String |キックアウトしてマイク・オフにする必要のあるユーザーID。 |

このインターフェースを呼び出すと、すぐにマイクリストが修正されます。


## ローカル音声操作のインターフェース

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

ローカルの音声のミュート/ミュート取り消し。

```dart
void muteLocalAudio(bool mute)
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | ミュート/ミュート取り消し。詳細は [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |


### setSpeaker

スピーカーの起動設定。

```dart
void setSpeaker(bool useSpeaker)
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true：スピーカー；false：ヘッドホン。 |



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
| mute   | boolean | true：ミュート起動；false：ミュート停止。 |

### muteAllRemoteAudio

全メンバーのミュート/ミュート解除。

```dart
void muteAllRemoteAudio(bool mute)
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |


## バックグラウンドミュージック・サウンドエフェクト関連インターフェース関数

### getAudioEffectManager

バックグラウンド・サウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa)の取得。

```dart
TXAudioEffectManager getAudioEffectManager()
```


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットを使用します。

```dart
Future<ActionCallback> sendRoomTextMsg(String message)
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | テキストメッセージ。 |

   

## マイク・オン申請シグナリング関連インターフェース

### raiseHand

視聴者からのマイク・オン申請。

```dart
void raiseHand()
```

### agreeToSpeak

グループマスターによるマイク・オンの同意。

```dart
Future<ActionCallback> agreeToSpeak(String userId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味     |
| ------ | ------ | -------- |
| userId | String | ユーザーID。 |

### refuseToSpeak

グループマスターによるユーザーマイク・オンの拒否。

```dart
Future<ActionCallback> refuseToSpeak(String userId)
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味     |
| ------ | ------ | -------- |
| userId | String | ユーザーID。 |


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

ルーム廃棄のコールバック。キャスターがルームを解散するとき、ルーム内の全ユーザーはこの通知を受信します。

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
| userId     | String | マイク・オンのユーザーID。       |
| userName   | String | ユーザーのニックネーム。           |
| userAvatar | String | プロフィール画像URL。           |
| mute       | bool   | マイクステータス。デフォルトではマイク・オンになっています。 |

### onAnchorLeaveMic

マイク・オフのメンバー。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | マイク・オフのユーザーID。 |

### onMicMute

キャスターのマイクミュートの有無。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | マイク・オフのユーザーID。 |
| mute   | bool   | マイクステータス。     |


## 視聴者の入退室イベントのコールバック

### onAudienceEnter

視聴者入室通知の受信。


パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味           |
| ---------- | ------ | -------------- |
| userId     | String | マイク・オンのユーザーID。 |
| userName   | String | ユーザーのニックネーム。     |
| userAvatar | String | プロフィール画像URL。     |

### onAudienceExit

視聴者退室通知の受信。

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

グループマスターによるマイク・オン同意のコールバック。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | グループマスターのユーザーID。 |

### onRefuseToSpeak

グループマスターによるマイク・オン拒否のコールバック。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | -------------- |
| userId | String | グループマスターのユーザーID。 |
