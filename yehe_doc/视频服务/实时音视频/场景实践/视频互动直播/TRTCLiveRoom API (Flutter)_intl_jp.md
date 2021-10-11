TRTCLiveRoomは、Tencent CloudのTencent Real-Time Communication（TRTC）およびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。

- キャスターが新しいライブストリーミングルームを作成して配信を開始し、視聴者がライブストリーミングルームに参加して視聴します。
- キャスターと視聴者がビデオでマイク接続によるコラボライブを行います。
- 2つの異なるルームの間でキャスター同士のPK（クロスルーム対戦）を行います。
- 各種のテキストメッセージやカスタムメッセージの送信をサポートします。カスタムメッセージは弾幕、「いいね」、ギフトを実装するために使用することができます。

TRTCLiveRoomはオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実現プロセスは、 [ビデオマイク接続ライブストリーミング（Flutter）](https://intl.cloud.tencent.com/document/product/647/41944)をご参照ください。

- TRTC SDK： [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615) を低遅延のライブストリーミングコンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996)のAVChatroomを使用して、ライブストリーミングチャットルーム機能を実装します。同時に、IMのメッセージでキャスター間のマイク接続のフローをつなげます。

[](id:TRTCLiveRoom)

## TRTCLiveRoom API 概要

### SDK基本関数

| API                                             | 説明                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを破棄します。           |
| [registerListener](#registerlistener)           | イベントコールバックを設定します。 |
| [unRegisterListener](#unregisterlistener)       | イベントコールバックのあるスレッドを設定します。                                   |
| [login](#login)                                 | ログイン。                   |
| [logout](#logout)                               | ログアウト。                   |
| [setSelfProfile](#setselfprofile)               | 個人情報を修正します。           |

### ルーム関連インターフェース関数

| API                                     | 説明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)               | ルームの新規作成（キャスターが呼び出し）。ルームが存在しない場合は、システムが新しいルームを自動的に作成します。 |
| [destroyRoom](#destroyroom)             |ルームの廃棄（キャスターが呼び出し）。                                       |
| [enterRoom](#enterroom)                 | 入室（視聴者が呼び出し）。                                       |
| [exitRoom](#exitroom)                   | 退室（視聴者が呼び出し）。                                       |
| [getRoomInfos](#getroominfos)           | ルームリストの詳細情報を取得します。                                     |
| [getAnchorList](#getanchorlist)         | ルーム内の全キャスターのリストを取得します。enterRoom() 成功後に呼び出しが有効となります。     |
| [getRoomMemberList](#getroommemberlist) | ルーム内のすべてのメンバー情報を取得し、enterRoom() 成功後に呼び出しが有効となります。     |

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
| [kickoutJoinAnchor](#kickoutjoinanchor)   | キャスターがマイク接続視聴者をキックアウトします。 |

### キャスターのルーム間PK

| API                               | 説明                   |
| --------------------------------- | ---------------------- |
| [requestRoomPK](#requestroompk)   | キャスターがルーム間PKをリクエストします。      |
| [responseRoomPK](#responseroompk) | キャスターがルーム間PKのリクエストに応答します。 |
| [quitRoomPK](#quitroompk)         | ルーム間PKから退出します。          |

### オーディオビデオ制御に関連するインターフェース関数

| API                                       | 説明               |
| ----------------------------------------- | ------------------ |
| [switchCamera](#switchcamera)             | フロント/リアカメラを切り替えます。   |
| [setMirror](#setmirror)                   | ミラー表示のオン／オフを設定します。 |
| [muteLocalAudio](#mutelocalaudio)         | ローカルオーディオをミュートにします。     |
| [muteRemoteAudio](#muteremoteaudio)       | リモートオーディオをミュートにします。     |
| [muteAllRemoteAudio](#muteallremoteaudio) | 全てのリモートオーディオをミュートにします。 |

### BGMサウンドエフェクト関連インターフェース関数

| API                                             | 説明                                                          |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | BGMサウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html)の取得。 |

### 美顔フィルタに関するインターフェース関数

| API                                   | 説明                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html)を取得します。 |

### メッセージ送信関連インターフェース関数

| API                                     | 説明                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージのブロードキャスト。通常、弾幕によるチャットに使用します。|
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを送信します。                     |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API概要</h2>

### 一般的なイベントコールバック

| API                                                          | 説明                        |
| ----------------------------------- | ---------------------------------- |
| [onError](#onerror)                 | エラーのコールバック。                         |
| [onWarning](#onwarning)             | 警告のコールバック。                         |
| [onKickedOffline](#onkickedoffline) | 他のユーザーが同じアカウントでログインすると、キックアウトされてオフラインになります。 |

### ルームイベントコールバック

| API                                           | 説明                                                 |
| --------------------------------------------- | ---------------------------------------------------- |
| [onEnterRoom](#onenterroom)                   | ローカルの入室のコールバック。                                       |
| [onUserVideoAvailable](#onuservideoavailable) | リモートユーザーが再生できるビッグストリーム画面が存在するかどうか（一般的にはカメラに用いられる）。 |
| [onRoomDestroy](#onroomdestroy)           | ルームが破棄されたときのコールバック。                                   |

### キャスターと視聴者の参加／退出のイベントコールバック

| API                                 | 説明                 |
| ----------------------------------- | -------------------- |
| [onAnchorEnter](#onanchorenter)     | 新しいキャスターの入室通知を受信します。 |
| [onAnchorExit](#onanchorexit)       | キャスターの退室通知を受信します。   |
| [onAudienceEnter](#onaudienceenter) |視聴者入室通知の受信。|
| [onAudienceExit](#onaudienceexit) | 視聴者退室通知の受信。|

### キャスターと視聴者のマイク接続のイベントコールバック

| API                                         | 説明                           |
| ------------------------------------------- | ------------------------------ |
| [onRequestJoinAnchor](#onrequestjoinanchor) | キャスターが視聴者のマイク接続リクエストを受信した時のコールバック。 |
| [onAnchorAccepted](#onanchoraccepted)       | キャスターが視聴者のマイク接続リクエストに同意します。       |
| [onAnchorRejected](#onanchorrejected)       | キャスターが視聴者のマイク接続リクエストを拒否します。       |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | マイク接続の視聴者がマイク接続からキックアウトされた通知を受信します。 |

### キャスター間PKのイベントコールバック

| API                                   | 説明                   |
| ------------------------------------- | ---------------------- |
| [onRequestRoomPK](#onrequestroompk)  | ルーム間PKのリクエストの通知を受信。 |
| [onRoomPKAccepted](#onroompkaccepted) | キャスターがルーム間PKのリクエストに同意します。 |
| [onRoomPKRejected](#onroompkrejected) | キャスターがルーム間PKのリクエストを拒否します。 |
| [onQuitRoomPK](#onquitroompk)         | ルーム間PK中止の通知を受信します。 |

### メッセージイベントのコールバック

| API                                         | 説明             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | テキストメッセージの受信。   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージの受信。 |

## SDK基本関数

### sharedInstance

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) シングルトンオブジェクトを取得します。

```java
 static Future<TRTCLiveRoom> sharedInstance()
```

### destroySharedInstance

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) シングルトンオブジェクトを破棄します。

>?インスタンスを破棄後は、外部にキャッシュされたTRTCLiveRoomインスタンスの再使用ができません。改めて [sharedInstance](#sharedinstance) を呼び出して、インスタンスを新規取得する必要があります。

```java
static void destroySharedInstance()
```

### registerListener

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) イベントコールバック。 TRTCLiveRoomDelegate を介して[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944)の各種ステータス通知を受け取ることができます。

```java
void registerListener(VoiceListenerFunc func);
```

>?registerListenerは、TRTCLiveRoomのプロキシコールバックです。   


### unRegisterListener

コンポーネントイベントの監視インターフェースを削除します。

```java
void unRegisterListener(VoiceListenerFunc func);
```


### login

ログイン。

```java
Future<ActionCallback> login(
      int sdkAppId, String userId, String userSig, TRTCLiveRoomConfig config);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ               | 意味                                                         |
| -------- | ------------------ | ------------------------------------------------------------ |
| sdkAppId | int         | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報でSDKAppIDを確認できます。 |
| userId   | String             | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。 |
| userSig  | String             | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| config   | TRTCLiveRoomConfig | グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。<ul style="margin:0;"><li>useCDNFirst 属性：視聴者の視聴方式の設定に使用します。trueは、普通の視聴者のCDN経由での視聴を表し、費用は安価ですがレイテンシーは高めです。falseは、普通の視聴者の低レイテンシーによる視聴を表し、費用は CDN とマイク接続の間ですが、レイテンシーを1s以内に抑えることができます。</li><li>CDNPlayDomain 属性： useCDNFirstの設定がtrueの時に有効となり、CDNでの視聴の再生ドメイン名の指定に使用します。CSSコンソール >【<a href="https://console.cloud.tencent.com/live/domainmanage">ドメイン名管理</a>】の画面からログインし、設定を行います。</li></ul> |

### logout

ログアウト。

```java
Future<ActionCallback> logout();
```

### setSelfProfile

個人情報の修正。

```java
Future<ActionCallback> setSelfProfile(String userName, String avatarURL);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味       |
| --------- | ------ | ---------- |
| userName | String | ニックネーム。 |
| avatarURL | String | プロフィール画像URL。 |

## ルーム関連インターフェース関数

### createRoom

ルームの新規作成（キャスターが呼び出し）。

```java
Future<ActionCallback> createRoom(int roomId, TRTCCreateRoomParam roomParam);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ      | 意味                                                         |
| --------- | --------- | ------------------------------------------------------------ |
| roomId    | int       | ルームIDは、ご自身でアサインし、一元管理する必要があります。複数の roomID を、1つのライブストリーミングルームリストにまとめることができます。Tencent Cloudでは現在、ライブストリーミングルームリストの管理サービスを行っていませんので、ご自身でライブストリーミングルームリストを管理してください。 |
| roomParam | RoomParam | ルーム情報は、ルーム名、カバー情報など、ルームを説明するための情報です。ルームリストおよびルーム情報をご自身のサーバーで管理する場合は、このパラメータは無視してもかまいません。 |

キャスターがブロードキャストを開始する際の通常の呼び出しプロセスは次のとおりです。 

1. 【キャスター】 `startCameraPreview()`を呼び出し、カメラのプレビューを起動します。この時美顔パラメータを調整できます。 
2. 【キャスター】`createRoom()`を呼び出し、ライブストリーミングルームを作成します。ルーム作成が成功したかどうかがActionCallbackでキャスターに通知されます。
3. 【キャスター】`starPublish()`を呼び出し、プッシュを開始します。

### destroyRoom

ルームの破棄（キャスターが呼び出し）。キャスターは、ルーム作成後、この関数を呼び出してルームを破棄します。

```java
Future<ActionCallback> destroyRoom();
```


### enterRoom

入室（視聴者が呼び出し）。

```java
Future<ActionCallback> enterRoom(int roomId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味       |
| ------ | ---- | ---------- |
| roomId | int | ルームID。 |

視聴者のライブストリーミング視聴の通常の呼び出しフローは以下のとおりです。 

1.【視聴者】サーバーから取得する最新のライブストリーミングルームリストには、多くのライブストリーミングルームのroomIdおよびルーム情報が含まれる場合があります。
2. 【視聴者】視聴者は1つのライブストリーミングルームを選択し、`enterRoom()`を呼び出して、このルームに参加します。
3. 【視聴者】`startPlay(userId)`を呼び出し、キャスターのuserIdを渡して再生を開始します。
 - ライブストリーミングルームリストにキャスターのuserId情報がすでに含まれている場合、視聴者は、`startPlay(userID)`を直接呼び出せば、再生を開始できます。
 - 入室前にキャスターのuserIdが一時的に取得できない場合、視聴者は入室後に `TRTCLiveRoomDelegate`から`onAnchorEnter(userId)`のイベントコールバックを受信します。このコールバックの中にキャスターのuserId情報が含まれていますので、`startPlay(userId)`を再び呼び出せば、再生できます。 

### exitRoom

ルームを退出します。

```java
Future<ActionCallback> exitRoom();
```


### getRoomInfos

ルームリストの詳細情報を取得します。ルーム情報は、キャスターが `createRoom()`作成時にroomInfoによって設定します。

>?ルームリストおよびルーム情報をご自身で管理する場合は、この関数は無視してもかまいません。


```java
Future<RoomInfoCallback> getRoomInfos(List<String> roomIdList);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ               | 意味         |
| ---------- | ------------------ | ------------ |
| roomIdList | List&lt;String&gt; | ルームナンバーリスト。 |

### getAnchorList

ルーム内の全キャスターのリストを取得します。`enterRoom()`成功後に呼び出しが有効となります。

```java
Future<UserListCallback> getAnchorList();
```

### getRoomMemberList

ルーム内の全視聴者の情報を取得します。`enterRoom()`成功後に呼び出しが有効となります。

```java
Future<UserListCallback> getRoomMemberList(int nextSeq)
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| nextSeq | int  | ページネーションプルフラグ。最初のプルに0と入力すると、コールバックが成功します。nextSeqがゼロでない場合は、ページネーションが必要であり、0になるまで渡して再度プルします。 |

   

## プッシュプルストリームに関連するインターフェース関数

### startCameraPreview

ローカルビデオのプレビュー画面を立ち上げます。

```java
Future<void> startCameraPreview(bool isFrontCamera, int viewId);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ | 意味                                  |
| ------------- | ---- | ------------------------------------- |
| isFrontCamera | bool | true：フロントカメラ；false：リアカメラ。 |
| viewId        | int  | ビデオviewのコールバック ID。                 |

### stopCameraPreview

ローカルのビデオキャプチャおよびプレビューを停止します。

```java
  Future<void> stopCameraPreview();
```

   

### startPublish

ライブストリーミング（プッシュ）を開始します。次のシーンに適用します。
- キャスターの放送開始時の呼び出し。
- 視聴者のマイク接続開始時の呼び出し。

```java
Future<void> startPublish(String streamId);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ    | 意味                                                         |
| -------- | ------- | ------------------------------------------------------------ |
| streamId | String? | ライブストリーミングのCDNのstreamIdをバインドするために利用します。視聴者にライブCDN経由でライブストリーミングを視聴させたい場合は、現在のキャスターのライブストリーミングstreamIdを指定する必要があります。 |


### stopPublish

ライブストリーミング（プッシュ）を停止します。次のシーンに適用します。
- キャスターがライブストリーミングを終了する時の呼び出し。
- 視聴者がマイク接続を終了する時の呼び出し。


```java
Future<void> stopPublish();
```

### startPlay

リモートのビデオ画面を再生します。普通の視聴とマイク接続のシーンで呼び出すことができます。

```java
Future<void> startPlay(String userId, int viewId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味               |
| ------ | ------ | ------------------ |
| userId | String | 視聴が必要なユーザーid。 |
| viewId | int    | ビデオviewのコールバックid。 |

- **普通の視聴シーン：**
    - ライブストリーミングルームリストにキャスターのuserId情報がすでに含まれている場合、視聴者は、`enterRoom()`成功後に`startPlay(userId)`を直接呼び出せばキャスターの画面を再生できます。
    - 入室前にキャスターのuserIdが一時的に取得できない場合、視聴者は入室後に `TRTCLiveRoomDelegate`の`onAnchorEnter(userId)`のイベントコールバックを受信します。このコールバックの中にキャスターのuserId 情報が含まれていますので、`startPlay(userId)`を再び呼び出せば、キャスターの画面を再生できます。

- **ライブストリーミングのマイク接続シーン：**
マイク接続の始動後、キャスターは`TRTCLiveRoomDelegate`から`onAnchorEnter(userId)`のコールバックを受信します。この時コールバックの中のuserIdを使用して`startPlay(userId)`を呼び出せば、マイク接続の画面を再生できます。

### stopPlay

リモートのビデオ画面のレンダリングを停止します。`onAnchorExit()`のコールバック時、このインターフェースを呼び出す必要があります。

```java
Future<void> stopPlay(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味             |
| ------ | ------ | ---------------- |
| userId | String | 相手側のユーザー情報。 |

## キャスターと視聴者のマイク接続

### requestJoinAnchor

視聴者がマイク接続をリクエストします。

```java
Future<ActionCallback> requestJoinAnchor();
```

キャスターと視聴者のマイク接続フローは次のとおりです。

1. 【視聴者】`requestJoinAnchor()`を呼び出し、キャスターにマイク接続リクエストを送信します。
2. 【キャスター】 `TRTCLiveRoomDelegate`の`onRequestJoinAnchor()`のコールバック通知を受信します。
3. 【キャスター】`responseJoinAnchor()`を呼び出して、視聴者からのマイク接続リクエストを受け入れるか決定します。
4. 【視聴者】responseCallbackのコールバック通知を受信します。この通知にキャスターの処理結果が含まれています。
5. 【視聴者】リクエストが同意されると、`startCameraPreview()`が呼び出され、ローカルカメラが起動します。
6. 【視聴者】その後 `startPublish()`を呼び出し、正式にプッシュストリームの状態に入ります。
7. 【キャスター】一度視聴者がマイク接続に入ると、キャスターは、`TRTCLiveRoomDelegate`の `onAnchorEnter()`の通知を受信します。
8. 【キャスター】キャスターが `startPlay()`を呼び出すと、マイク接続の視聴者のビデオ画面を見ることができるようになります。
9. 【視聴者】ライブストリーミングルームの中で他の視聴者がすでにキャスターとマイク接続を行っている場合、新しく参加したマイク接続の視聴者は`onAnchorEnter()`の通知を受け取ります。この時に`startPlay()`を呼び出せば他のマイク接続者のビデオ画面を再生することができます。

   

### responseJoinAnchor

キャスターがマイク接続のリクエストを処理します。キャスターは、`TRTCLiveRoomDelegate`の `onRequestJoinAnchor()`のコールバックを受け取った後、このインターフェースを呼び出して、視聴者のマイク接続リクエストを処理する必要があります。

```java
Future<ActionCallback> responseJoinAnchor(String userId, boolean agreee);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
| ------ | ------ | ------------------------- |
| userId | String | 視聴者ID。                 |
| agree  | bool   | true：同意；false：拒否。 |


### kickoutJoinAnchor

キャスターがマイク接続の視聴者をキックアウトします。キャスターがこのインターフェースを呼び出し、マイク接続の視聴者をキックアウトすると、キックアウトされたマイク接続の視聴者は、`TRTCLiveRoomDelegate`の`onKickoutJoinAnchor()`のコールバック通知を受信します。

```java
Future<ActionCallback> kickoutJoinAnchor(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味          |
| ------ | ------ | ------------- |
| userId | String | マイク接続の視聴者 ID。 |


## キャスターのルーム間PK

### requestRoomPK

キャスターがルーム間PKをリクエストします。

```java
Future<ActionCallback> requestRoomPK(int roomId, String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| roomId | int    | 招待された側のルーム ID。 |
| userId | String | 招待された側のキャスター ID。 |

キャスターとキャスターの間でルーム間PKを行うことができます。ライブストリーミング中の2名のキャスターAとBのルーム間PKのフローは次のとおりです。

1. 【キャスター A】 `requestRoomPK()`を呼び出してキャスターBに向けてマイク接続リクエストを送信します。
2. 【キャスター B】`TRTCLiveRoomDelegate`の`onRequestRoomPK()`のコールバック通知を受信します。
3. 【キャスター B】`responseRoomPK()`を呼び出して、キャスター AのPKのリクエストを受け入れるかどうか決定します。
4. 【キャスター B】キャスター Aのリクエストを受け入れる場合は、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出してキャスターAのビデオ画面を表示させます 。
5. 【キャスター A】 `onRoomPKAccepted`または`onRoomPKRejected`のコールバック通知を受信します。
6. 【キャスターA】リクエストが同意された場合は、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出し、キャスターBのビデオ画面を表示します。

   

### responseRoomPK

キャスターがルーム間PKのリクエストに応答します。キャスターが応答した後、相手側キャスターは `requestRoomPK`で渡された`responseCallback`のコールバックを受信します。

```java
Future<ActionCallback> responseRoomPK(String userId, boolean agree);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
| ------ | ------ | ------------------------- |
| userId | String  | PKをリクエストしたキャスターID。   |
| agree  | bool   | true：同意；false：拒否。 |


### quitRoomPK

ルーム間PKから退出します。PK中のいずれかのキャスターがルーム間PKの状態から退出すると、もう一方のキャスターは`TRTCLiveRoomDelegate`の`onQuitRoomPk()`のコールバック通知を受信します。

```java
Future<ActionCallback> quitRoomPK();
```


## オーディオビデオ制御に関連するインターフェース関数

### switchCamera

フロント/リアカメラを切り替えます。

```java
Future<void> switchCamera(boolean isFrontCamera);
```

### setMirror

ミラー表示のオン／オフを設定します。

```java
Future<void> setMirror(boolean isMirror);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ | 意味            |
| -------- | ---- | --------------- |
| isMirror | bool | ミラーオン/オフ。 |

   

### muteLocalAudio

ローカルオーディオをミュートにします。

```java
Future<void> muteLocalAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味                              |
| ---- | ---- | --------------------------------- |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |

   

### muteRemoteAudio

リモートオーディオをミュートにします。

```java
Future<void> muteRemoteAudio(String userId, boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                              |
| ------ | ------ | --------------------------------- |
| userId | String | リモートユーザーID。                   |
| mute   | boolean   | true：ミュート起動；false：ミュート停止。 |

   

### muteAllRemoteAudio

すべてのリモート側のオーディオをミュートにします。

```java
Future<void> muteAllRemoteAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味                              |
| ---- | ---- | --------------------------------- |
| mute | boolean | true：ミュート起動；false：ミュート停止。 |

   

## BGMサウンドエフェクト関連インターフェース関数

### getAudioEffectManager

BGMサウンドエフェクト管理オブジェクト [TXAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html)の取得。

```java
getAudioEffectManager();
```


## 美顔フィルタに関するインターフェース関数

### getBeautyManager

美顔管理オブジェクト[TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html)を取得します。

```java
getBeautyManager();
```

美顔管理では、次の機能を使用できます。

- 「美顔のスタイル」、「美白」、「肌色補正（血色・つや感）」、「デカ眼」、「顔痩せ」、「V顔」、「下あご」、「面長補正」、「小鼻」、「キラキラ目」、「白い歯」、「目の弛み除去」、「シワ除去」、「ほうれい線除去」などの美容効果を設定します。
- 「髪の生え際」、「眼と眼の距離」、「眼角度」、「唇の形」、「鼻翼」、「鼻の位置」、「唇の厚さ」、「顔の形」を調整します。
- 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
- メイクアップを追加します。
- ジェスチャー認識を行います。


## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージをブロードキャストします。通常、弾幕によるチャットに使用します。

```java
Future<ActionCallback> sendRoomTextMsg(String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | テキストメッセージ。 |

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。

```java
Future<ActionCallback> sendRoomCustomMsg(String cmd, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                                               |
| ------- | ------ | -------------------------------------------------- |
| cmd     | String | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message    | String | テキストメッセージ。                                         |


## TRTCLiveRoomDelegateイベントのコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| errCode   | int    | エラーコード。   |
| errMsg    | String | エラー情報。 |


### onWarning

警告のコールバック。

パラメータは下表に示すとおりです。

| パラメータ        | タイプ   | 意味       |
| ----------- | ------ | ---------- |
| warningCode | int    | エラーコード。   |
| warningMsg  | String | 警告情報。 |


### onKickedOffline

他のユーザーが同じアカウントでログインすると、キックアウトされてオフラインになります。




## ルームイベントのコールバック

### onRoomDestroy

ルームが破棄された時のコールバック。キャスターが退室する時、ルーム内の全ユーザーがこの通知を受信します。

### onEnterRoom

ローカル入室

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                                     |
| ------ | ---- | -------------------------------------------------------- |
| result | int  | result &gt; 0 の場合は入室に費やした時間（ms）、result &lt; 0 の場合は入室エラーコード。 |

### onUserVideoAvailable

リモートユーザーが再生できるビッグストリーム画面が存在するかどうか（一般的にはカメラに用いられる）。

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味           |
| --------- | ------ | -------------- |
| userId     | String | ユーザーID。      |
| available | boolean   | 画面の起動の有無。 |

## キャスターと視聴者の参加／退出のイベントコールバック

### onAnchorEnter

新しいキャスターの入室の通知を受信します。マイク接続の視聴者とルーム間PKのキャスターが入室すると、視聴者は、新しいキャスターが入室したというイベントを受信します。`TRTCLiveRoom`の `startPlay()`を呼び出して、そのキャスターのビデオ画面を表示することができます。


パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味            |
| ---------- | ------ | --------------- |
| userId | String | 新しく入室したキャスターの ID。 |
| userName   | String | ユーザーのニックネーム。        |
| userAvatar | String | ユーザーのプロフィール画像のアドレス。    |

### onAnchorExit

キャスターの退室の通知を受信します。ルーム内のキャスター（およびマイク接続中の視聴者）が、新しいキャスターの退室のイベントを受信します。`TRTCLiveRoom`の`stopPlay()`を呼び出して、そのキャスターのビデオ画面を閉じることができます。

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味           |
| ---------- | ------ | -------------- |
| userId     | String | 退出するキャスターの ID。  |
| userName   | String | ユーザーのニックネーム。     |
| userAvatar | String | ユーザーのプロフィール画像のアドレス。 |


### onAudienceEnter

視聴者入室通知の受信。

```java
void onAudienceEnter(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                             | 意味                                |
| -------- | -------------------------------- | ----------------------------------- |
| userInfo | TRTCLiveRoomDef.TRTCLiveUserInfo | 入室する視聴者のユーザーID、ニックネーム、プロフィール画像などの情報。 |


### onAudienceExit

視聴者退室通知の受信。


パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味           |
| ---------- | ------ | -------------- |
| userId | String | 退室した視聴者の情報。 |
| userName   | String | ユーザーのニックネーム。     |
| userAvatar | String | ユーザーのプロフィール画像のアドレス。 |

### onRequestJoinAnchor

キャスターが視聴者のマイク接続リクエストを受信した時のコールバック。


パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味              |
| ---------- | ------ | ----------------- |
| userId     | String | マイク接続をリクエストするユーザーID。                          |
| userName   | String | ユーザーのニックネーム。        |
| userAvatar | String | ユーザーのプロフィール画像のアドレス。    |

### onAnchorAccepted

キャスターが視聴者のマイク接続リクエストに同意します。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| userId | String | キャスターのユーザーID。 |


### onAnchorRejected

キャスターが視聴者のマイク接続リクエストを拒否します。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| userId | String | キャスターのユーザーID。 |

### onKickoutJoinAnchor

マイク接続の視聴者がマイク接続からキックアウトされた通知を受信します。マイク接続の視聴者は、キャスターからマイク接続キックアウトのメッセージを受信した場合、`TRTCLiveRoom`の`stopPublish()` を呼び出してマイク接続から退出する必要があります。


## キャスター間PKのイベントコールバック

### onRequestRoomPK

ルーム間PKのリクエストの通知を受信します。キャスターは、他のルームのキャスターからPKのリクエストを受け取り、PKに同意する場合、`TRTCLiveRoomDelegate`の`onAnchorEnter()`の通知を待ってから、`startPlay()`を呼び出して招待側キャスターのストリームを再生する必要があります。

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味              |
| ---------- | ------ | ----------------- |
| userId     | String | ルーム間をリクエストするユーザーID。 |
| userName   | String | ユーザーのニックネーム。        |
| userAvatar | String | ユーザーのプロフィール画像のアドレス。    |

### onRoomPKAccepted

キャスターはルーム間PKのリクエストに同意します。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                    |
| ------ | ------ | ----------------------- |
| userId | String | ルーム間PKに同意するユーザーID。 |

### onRoomPKRejected

キャスターはルーム間PKのリクエストに同意します。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                    |
| ------ | ------ | ----------------------- |
| userId | String | ルーム間PKを拒否するユーザーID。 |


### onQuitRoomPK

ルーム間PK中止の通知を受信します。


## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。


パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ------- | ------ | ---------- |
| message | String | テキストメッセージ。 |


### onRecvRoomCustomMsg

カスタムメッセージの受信。


パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                                               |
| ------- | ------ | -------------------------------------------------- |
| command  | String            | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message    | String | テキストメッセージ。                                         |

