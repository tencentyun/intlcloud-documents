1. TUIRoomは、Tencent CloudのTencent Real-Time Communication（TRTC）およびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。
- キャスターがルームを作成し、入室者はルームナンバーを入力した後に入室できます。
- 入室者の間で画面共有を行います。
- 各種のテキストメッセージとカスタムメッセージの送信をサポートします。

2. TUIRoomはオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実装プロセスについては、 [多人数オーディオビデオルーム(Android)](https://intl.cloud.tencent.com/document/product/647/37283)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオルームコンポーネントとして使用します。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047) を利用してチャットルームの機能（**IM SDKはAndroidバージョンを使用**）を実装します。


## TUIRoom API概要

### TUIRoomCore基本関数

| API| 説明  |
| ----------------------------------- | -------------- |
| [getInstance](#getinstance)         |  シングルトンオブジェクトを取得します。 |
| [destroyInstance](#destroyinstance) | シングルトンオブジェクトを破棄します。 |
| [setListener](#setlistener)         | イベントコールバックを設定します。 |

### ルーム関連インターフェース関数

| API| 説明       |
| ----------------------------------------- | ---------------------------------- |
| [createRoom](#createroom)                 | ルームの作成（キャスターが呼び出し）。       |
| [destroyRoom](#destroyroom)               | ルームの破棄（キャスターが呼び出し）。       |
| [enterRoom](#enterroom)                   | 入室（入室メンバーが呼び出し）。 |
| [leaveRoom](#leaveroom)                   | 退室（その他のルームメンバーが呼び出し）。 |
| [getRoomInfo](#getroominfo)               | ルーム情報の取得。                 |
| [getRoomUsers](#getroomusers)             | ルーム内全メンバー情報の取得。       |
| [getUserInfo](#getuserinfo)               | 特定ユーザーの情報の取得。           |
| [transferRoomMaster](#transferroommaster) | キャスター権限の移転（キャスターが呼び出し）。 |

### ローカルのオーディオビデオ操作インターフェース

| API| 説明  |
| ----------------------------------------- | -------------------------- |
| [startCameraPreview](#startcamerapreview) | ローカルビデオのプレビュー画面を立ち上げます。   |
| [stopCameraPreview](#stopcamerapreview)   | ローカルのビデオキャプチャおよびプレビューを停止します。   |
| [startLocalAudio](#startlocalaudio)       | マイクキャプチャを起動します。           |
| [stopLocalAudio](#stoplocalaudio)         | マイクキャプチャを停止します。           |
| [setVideoMirror](#setvideomirror)         | ローカル画面のミラーモードのプレビューを設定します。 |
| [setSpeaker](#setspeaker)                 | スピーカーの起動を設定します。           |

### リモートユーザーに関するインターフェース

| API| 説明       |
| ----------------------------------- | ---------------------------------- |
| [startRemoteView](#startremoteview) | 指定メンバーのリモートビデオ画面をサブスクリプションし再生します。 |
| [stopRemoteView](#stopremoteview)   | リモートビデオ画面のサブスクリプションをキャンセルし再生を停止します。   |

### チャットメッセージ送信インターフェース

| API| 説明  |
| ----------------------------------- | -------------- |
| [sendChatMessage](#sendchatmessage)     | チャットメッセージを送信します。   |
| [sendCustomMessage](#sendcustommessage) | カスタムメッセージを送信します。 |

### フィールドコントロール関連インターフェース

| API          | 説明         |
| --------------------------------------------------- | ------------------------------------------------------- |
| [muteUserMicrophone](#muteusermicrophone)           | 特定ユーザーのマイクを無効化/再有効化します。                               |
| [muteAllUsersMicrophone](#muteallusersmicrophone)   | 全ユーザーのマイクを無効化/再有効化し、ステータスをルーム情報に同期させます。 |
| [muteUserCamera](#muteusercamera)                   |特定ユーザーのカメラを無効化/再有効化します。                               |
| [muteAllUsersCamera](#mutealluserscamera)           | 全ユーザーのカメラを無効化/再有効化し、ステータスをルーム情報に同期させます。 |
| [muteChatRoom](#mutechatroom)                       | チャットルームのミュートを開始/停止します（キャスターが呼び出し）。                     |
| [kickOffUser](#kickoffuser)                         | ルーム内の特定ユーザーをリムーブします（キャスターが呼び出し）。                        |
| [startCallingRoll](#startcallingroll)               | キャスターが点呼を開始します。                                        |
| [stopCallingRoll](#stopcallingroll)                 | キャスターが点呼を終了します。                                        |
| [replyCallingRoll](#replycallingroll)               | メンバーがキャスターの点呼に応答します。                                    |
| [sendSpeechInvitation](#sendspeechinvitation)       | キャスターがメンバーに発言するようインビテーションを送信します。                                    |
| [cancelSpeechInvitation](#cancelspeechinvitation)   | キャスターがメンバーの発言のためのインビテーションをキャンセルします。                                |
| [replySpeechInvitation](#replyspeechinvitation)     | メンバーがキャスターの発言申請に同意/拒否します。                         |
| [sendSpeechApplication](#sendspeechapplication)     | メンバーが発言を要請します。                                          |
| [replySpeechApplication](#replyspeechapplication)   | キャスターがメンバーの発言申請に同意/拒否します。                         |
| [forbidSpeechApplication](#forbidspeechapplication) | キャスターが発言申請を禁止します。                                    |
| [sendOffSpeaker](#sendoffspeaker)                   | キャスターがメンバーに発言を停止するよう命令します。                                  |
| [sendOffAllSpeakers](#sendoffallspeakers)           | キャスターが全員に発言を停止するよう命令します。                                  |
| [exitSpeechState](#exitspeechstate)                 | メンバーは発言を停止し、視聴者になります。                              |

### 画面共有インターフェース

| API          | 説明         |
|-----|-----|
| [startScreenCapture](#startscreencapture) | 画面共有を開始。|
| [stopScreenCapture](#stopscreencapture)   | 画面キャプチャの停止。 |

### 美顔フィルタに関するインターフェース関数

| API          | 説明         |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト[TXBeautyManager。](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得します。 |


### 関連設定インターフェース

| API| 説明       |
| ----------------------------------------------- | ---------------------- |
| [setVideoQosPreference](#setvideoqospreference) | ネットワークトラフィックコントロール関連パラメータを設定します。 |

### SDKバージョンインターフェース関数の取得

| API  | 説明|
| ------------------------------- | --------------- |
| [getSDKVersion](#getsdkversion) | SDKバージョンを取得します。 |

## TUIRoomCoreListener API概要[](id:TUIRoomCoreListener)

### エラーイベントコールバック

| API  | 説明         |
| ------------------- | ---------- |
| [onError](#onerror)                 | エラーのコールバック。                         |

### 基本イベントコールバック

| API  | 説明|
| ------------------------------------------- | ------------------ |
| [onDestroyRoom](#ondestroyroom)             | ルーム解散のコールバック。     |
| [onUserVoiceVolume](#onuservoicevolume)     | 音量の大きさのコールバック。 |
| [onRoomMasterChanged](#onroommasterchanged) | キャスター変更のコールバック。   |

### リモートユーザーイベントコールバック

| API | 説明  |
| ------------------------------------------------------------ | -------------------------------- |
| [onRemoteUserEnter](#onremoteuserenter)                      | リモートユーザー入室コールバック。           |
| [onRemoteUserLeave](#onremoteuserleave)                      | リモートユーザー退室コールバック。           |
| [onRemoteUserCameraAvailable](#onremoteusercameraavailable)  | リモートユーザーがカメラビデオを起動するかどうかのコールバック。 |
| [onRemoteUserScreenVideoAvailable](#onremoteuserscreenvideoavailable) | リモートユーザーが画面共有を開始するかどうかのコールバック。   |
| [onRemoteUserAudioAvailable](#onremoteuseraudioavailable)    | リモートユーザーがオーディオのアップストリームを開始するかどうかのコールバック。   |
| [onRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | リモートユーザーの発言開始のコールバック。           |
| [onRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | リモートユーザーの発言終了のコールバック。           |

### メッセージイベントのコールバック

| API  | 説明|
| ------------------------------------------------- | ------------------ |
| [onReceiveChatMessage](#onreceivechatmessage)     | テキストメッセージ受信のコールバック。   |
| [onReceiveRoomCustomMsg](#onreceiveroomcustommsg) | カスタムメッセージ受信のコールバック。 |

### フィールドコントロールイベントコールバック

| API          | 説明         |
| ------------------------------------------------------------ | ---------------------------------- |
| [onReceiveSpeechInvitation](#onreceivespeechinvitation)      | ユーザーがキャスターの発言要請を受信した場合のコールバック。       |
| [onReceiveInvitationCancelled](#onreceiveinvitationcancelled) | ユーザーがキャスターの発言要請キャンセルを受信する場合のコールバック。   |
| [onReceiveSpeechApplication](#onreceivespeechapplication)    | キャスターがユーザーの発言要請を受信する場合のコールバック。     |
| [onSpeechApplicationCancelled](#onspeechapplicationcancelled) | ユーザーが発言申請をキャンセルする場合のコールバック。             |
| [onSpeechApplicationForbidden](#onspeechapplicationforbidden) | キャスターが発言申請を禁止する場合のコールバック。           |
| [onOrderedToExitSpeechState](#onorderedtoexitspeechstate)  | メンバーが発言の停止をリクエストされる場合のコールバック。         |
| [onCallingRollStarted](#oncallingrollstarted)                | キャスターが点呼を開始し、メンバーが受信する場合のコールバック。   |
| [onCallingRollStopped](#oncallingrollstopped)                | キャスターが点呼を終了し、メンバーが受信する場合のコールバック。   |
| [onMemberReplyCallingRoll](#onmemberreplycallingroll)        | メンバーが点呼に応答し、キャスターが受信する場合のコールバック。   |
| [onChatRoomMuted](#onchatroommuted)                          | キャスターがチャットルームのミュートを変更する場合のコールバック。     |
| [onMicrophoneMuted](#onmicrophonemuted)                      | キャスターがマイクの無効化を設定する場合のコールバック。         |
| [onCameraMuted](#oncameramuted)                              | キャスターがカメラの無効化を設定する場合のコールバック。         |
| [onReceiveKickedOff](#onreceivekickedoff)                    | メンバーがキャスターからキックアウトされた場合のコールバック。         |


### 統計および品質コールバック

| API  | 説明|
| ------------------------------------- | ------------------ |
| [onStatistics](#onstatistics)         | 技術指標統計のコールバック。 |
| [onNetworkQuality](#onnetworkquality) | ネットワーク品質のコールバック。     |

### 画面共有関連コールバック

| API  | 説明|
| ------------------------------------------------- | ------------------ |
| [onScreenCaptureStarted](#onscreencapturestarted) | 画面共有開始のコールバック。 |
| [onScreenCaptureStopped](#onscreencapturestopped) | 画面共有停止のコールバック。 |

## TUIRoomCore基本関数

### getInstance

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283) シングルトンオブジェクトを取得します。
```java
public static TUIRoomCore getInstance(Context context);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| context | Context | Androidコンテキスト。内部ではApplicationContextに変換してシステムAPIの呼び出しに使用します。 |


### destroyInstance

```java
void destroyInstance();
```

### setListener

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283) イベントコールバック。TUIRoomCoreListener を介して[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283)の各種ステータス通知を取得できます。

```java
void setListener(TUIRoomCoreListener listener);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| listener | TUIRoomCoreListener | イベントコールバッククラスを受信します。 |

### createRoom

ルームの作成（キャスターが呼び出し）。
```java
void createRoom(String roomId, TUIRoomCoreDef.SpeechMode speechMode, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ | 意味  |
|-----------| ------------- | -------------------------------------- |
| roomId  | String  | ルームID。ご自身でアサインし、一元管理する必要があります。 |
| speechMode| TUIRoomCoreDef.SpeechMode | 発言モード。|
| callback | TUIRoomCoreCallback.ActionCallback | ルームの作成結果のコールバック。|

キャスターの通常の呼び出しフローは以下のとおりです。
1. **キャスター**が`createRoom()`を呼び出し、ルームを作成します。ルーム作成の成否は`TUIRoomCoreCallback.ActionCallback`でキャスターに通知されます。
2. **キャスター**が`startCameraPreview()`を呼び出し 、カメラキャプチャとプレビューを起動します。
3. **キャスター**が`startLocalAudio()`を呼び出し、ローカルマイクを起動します。

### destroyRoom

ルームの破棄（キャスターが呼び出し）。キャスターは、ルームの作成後、この関数を呼び出して、ルームを破棄できます。
```java
void destroyRoom(TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ | 意味  |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | ルームの破棄結果のコールバック。 |

### enterRoom

入室（ルーム参加メンバーが呼び出し）。
```java
void enterRoom(String roomId, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| roomId | String | ルームID。 |
| callback | UIRoomCoreCallback.ActionCallback | 結果のコールバック。  |


ルーム参加メンバーが入室する場合の通常の呼び出し手順は次のとおりです。
1. **入室メンバー**が`enterRoom`を呼び出し、roomIdを渡せば入室できます。
2. **入室メンバー**が`startCameraPreview()`を呼び出してカメラプレビューを起動し、`startLocalAudio()`を呼び出して、マイクキャプチャを起動します。
3. **入室メンバー**が`onRemoteUserCameraAvailable`のイベントを受信し、`startRemoteView()`を呼び出して、ビデオ再生を開始します。

### leaveRoom

退室（入室メンバーが呼び出し）。
```java
 void leaveRoom(TUIRoomCoreCallback.ActionCallback callback);
```

  パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | 結果のコールバック。|

### getRoomInfo

ルーム情報を取得します。
```java
TUIRoomCoreDef.RoomInfo getRoomInfo();
```

### getRoomUsers

ルームの全メンバー情報を取得します。
```java
 List<TUIRoomCoreDef.UserInfo> getRoomUsers();
```

### getUserInfo

ルームのメンバー情報を取得します。
```java
void getUserInfo(String userId, TUIRoomCoreCallback.UserInfoCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| userId     | String | ユーザーID。      |
| callback | UIRoomCoreCallback.UserInfoCallback | ルームメンバーの詳細情報のコールバック。 |


### setSelfProfile

ユーザー情報を設定します。
```java
void setSelfProfile(String userName, String avatarURL, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味  |
| ---------- | ------ | -------------- |
| userName  | String | ユーザーの氏名。  |
| avatarURL | String | ユーザーのプロフィール画像URL。 |
| callback | TUIRoomCoreCallback.ActionCallback | 設定が成功したかどうかの結果のコールバック。 |


### transferRoomMaster

グループを他のユーザーに引き渡します。
```java
 void transferRoomMaster(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| userId     | String | ユーザーID。      |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |


## ローカルプッシュインターフェース

### startCameraPreview

ローカルカメラプレビューを起動します。
```java
void startCameraPreview(boolean isFront, TXCloudVideoView view);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| isFront | boolean | true：フロントカメラ、false：リアカメラ。|
| view | TXCloudVideoView | ビデオ画像をロードするウィジェット。 |


### stopCameraPreview

ローカルカメラプレビューを停止します。
```java
 void stopCameraPreview();
```

### startLocalAudio

マイクの集音開始。
```java
 void startLocalAudio(int quality);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| quality | int | キャプチャの音質：<li/>TRTC_AUDIO_QUALITY_MUSIC<li/>TRTC_AUDIO_QUALITY_DEFAULT<li/>TRTC_AUDIO_QUALITY_SPEECH |

### stopLocalAudio

マイクの集音停止。
```java
void stopLocalAudio();
```

### setVideoMirror

ローカル画面のミラーモードのプレビューを設定します。
```java
 void setVideoMirror(int type);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| type | int | イメージタイプ。 |

### setSpeaker

スピーカーの起動設定。
```java
 void setSpeaker(boolean isUseSpeaker);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| isUseSpeaker | boolean | true：スピーカー、false：ヘッドホン。 |

## リモートユーザーに関するインターフェース

### startRemoteView
リモートユーザーのビデオストリームのサブスクリプション。

```java
void startRemoteView(String userId, TXCloudVideoView view, TUIRoomCoreDef.SteamType streamType, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ | 意味  |
| -------------- | ------------- | -------------------------- |
| userId  | String  | 再生が必要なユーザーのID。  |
| view | TXCloudVideoView  | ビデオ画像をロードするviewウィジェット。 |
| streamType  | TUIRoomCoreDef.SteamType | ストリームのタイプ。|
| callback  | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。|


### stopRemoteView

サブスクリプションをキャンセルし、リモートビデオ画面の再生を停止します。
```java
void stopRemoteView(String userId, TUIRoomCoreCallback.ActionCallback callback);

```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味  |
| ------- | ------------- | ----------------------- |
| userId | String  | 再生停止が必要なユーザーのID。 |
| callback  | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。|

### switchCamera

フロント/リアカメラを切り替えます。
```java
void switchCamera(boolean isFront);

```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味  |
| ------- | ------------- | ----------------------- |
| isFront | boolean  | true：フロントカメラ、false：リアカメラ。 |

## メッセージ送信インターフェース

### sendChatMessage

ルーム内でテキストメッセージをブロードキャストします。通常、テキストによるチャットに使用します。
```java
void sendChatMessage(String message, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| message | String | メッセージの内容。 |
| callback  | TUIRoomCoreCallback.ActionCallback | 送信結果のコールバック。|


### sendCustomMessage

カスタムメッセージを送信します。
```java
void sendCustomMessage(String data, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| data | String | メッセージの内容。 |
| callback  | TUIRoomCoreCallback.ActionCallback | 送信結果のコールバック。|

## フィールドコントロール関連インターフェース

### muteUserMicrophone

特定ユーザーのマイクを無効化/再有効化します。
```java
void muteUserMicrophone(String userId, boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | String| ユーザーID。  |
| mute  | boolean  | 無効にするかどうか。 |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### muteAllUsersMicrophone

全ユーザーのマイクを無効化/再有効化します。
```java
void muteAllUsersMicrophone(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ---- | ---- | ---------- |
| mute | boolean | 無効にするかどうか。 |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |


### muteUserCamera

特定ユーザーのカメラを無効化/再有効化します。
```java
void muteUserCamera(String userId, boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | String| ユーザーID。  |
| mute  | boolean  | 無効にするかどうか。 |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### muteAllUsersCamera

全ユーザーのカメラを無効化/再有効化します。
```java
void muteAllUsersCamera(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ---- | ---- | ---------- |
| mute  | boolean  | 無効にするかどうか。 |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### muteChatRoom

テキストチャットのミュート/再有効化。
```java
void muteChatRoom(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ---- | ---- | ---------- |
| mute  | boolean  | 無効にするかどうか。 |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |


### kickOffUser

キャスターがキックアウトします。
```java
void kickOffUser(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | String| ユーザーID。  |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### startCallingRoll

キャスターが点呼を開始します。
```java
 void startCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### stopCallingRoll

キャスターが点呼を終了します。
```java
 void stopCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
 
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### replyCallingRoll

メンバーがキャスターの点呼に応答します。
```java
void replyCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |


### sendSpeechInvitation

キャスターがメンバーの発言を要請します。
```java
void sendSpeechInvitation(String userId, TUIRoomCoreCallback.InvitationCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | String| ユーザーID。  |
| callback | TUIRoomCoreCallback.InvitationCallback | 結果のコールバック。 |

### cancelSpeechInvitation

キャスターがメンバーへの発言要請をキャンセルします。
```java
 void cancelSpeechInvitation(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | String| ユーザーID。  |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### replySpeechInvitation

メンバーがキャスターの発言要請に同意/を拒否します。
```java
void replySpeechInvitation(boolean agree, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| agree | boolean  | 同意するかどうか。 |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### sendSpeechApplication

メンバーが発言を要請します。
```java
void sendSpeechApplication(TUIRoomCoreCallback.InvitationCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.InvitationCallback | 結果のコールバック。 |

### cancelSpeechApplication

メンバーが発言申請をキャンセルします。
```java
void cancelSpeechApplication(TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### replySpeechApplication

キャスターがメンバーの発言申請に同意/を拒否します。
```java
void replySpeechApplication(boolean agree, String userId, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| agree  | boolean| 同意するかどうか。 |
| userId  | String| ユーザーID。  |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### forbidSpeechApplication

キャスターが発言申請を禁止します。
```java
 void forbidSpeechApplication(boolean forbid, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味 |
| ------ | ---- | ---------- |
| forbid | boolean | 禁止するかどうか。 |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |


### sendOffSpeaker

キャスターがメンバーに発言の停止を命令します。
```java
void sendOffSpeaker(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | String| ユーザーID。  |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### sendOffAllSpeakers

キャスターが全メンバーに発言の停止を命令します。
```java
void sendOffAllSpeakers(TUIRoomCoreCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |

### exitSpeechState

メンバーが発言を停止し、視聴者になります。
```java
void exitSpeechState(TUIRoomCoreCallback.ActionCallback callback);
```
パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 結果のコールバック。 |


## 画面共有インターフェース
### startScreenCapture

画面共有を開始。
```java
void startScreenCapture(TRTCCloudDef.TRTCVideoEncParam encParams, TRTCCloudDef.TRTCScreenShareParams screenShareParams);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| encParams | TRTCCloudDef.TRTCVideoEncParam | 画面共有時のエンコードパラメータを設定します。上記の推奨設定を採用することをお勧めします。encParamsにnullを指定した場合、startScreenCaptureを呼び出す前のエンコードパラメータ設定が使用されます。 |
| screenShareParams | TRTCCloudDef.TRTCScreenShareParams | 画面共有の特殊なレイアウト設定については、その中のfloatingViewの設定を推奨します。一方で、Appがシステムから強制排除されるのを回避でき、もう一方で、ユーザーのプライバシー保護にも役立ちます。 |

>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)をご参照ください。 |

### stopScreenCapture

画面キャプチャの停止。
```java
void stopScreenCapture();
```

## 美顔フィルタに関するインターフェース関数
### getBeautyManager

美顔管理オブジェクト [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得します。
```java
TXBeautyManager getBeautyManager();
```

美顔管理では、次の機能を使用できます。
- 「美顔のスタイル」、「美白」、「肌色補正（血色・つや感）」、「デカ眼」、「顔痩せ」、「V顔」、「下あご」、「面長補正」、「小鼻」、「キラキラ目」、「白い歯」、「目の弛み除去」、「シワ除去」、「ほうれい線除去」などの美容効果を設定します。
- 「髪の生え際」、「眼と眼の距離」、「眼角度」、「唇の形」、「鼻翼」、「鼻の位置」、「唇の厚さ」、「顔の形」を調整します。
- 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
- メイクアップを追加します。
- ジェスチャー認識を行います。

## 関連設定インターフェース

### setVideoQosPreference

ネットワークトラフィックコントロール関連パラメータを設定します。
```java
 void setVideoQosPreference(TRTCCloudDef.TRTCNetworkQosParam preference);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味  |
| ---------- | --------------------- | -------------- |
| preference | TRTCCloudDef.TRTCNetworkQosParam | ネットワークトラフィックコントロールポリシー。 |

### setAudioQuality

音質の設定。
```java
void setAudioQuality(int quality);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| quality | int | オーディオ品質。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |

### setVideoResolution

解像度の設定。

```java
void setVideoResolution(int resolution);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| resolution | int | ビデオの解像度。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#aa3b72c532f3ffdf64c6aacab26be5f87)をご参照ください。 |


### setVideoFps

フレームレートの設定。
```java
void setVideoFps(int fps);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| fps  | int  | ビデオキャプチャのフレームレート。 |

>? **推奨する値**：15fpsまたは20fps。5fps以下ではラグ感が目立ち、10fps以下では軽微なラグ感があります。20fps以上は高すぎて浪費になります（映画のフレームレートは24fps）。


### setVideoBitrate

ビットレートの設定。
```java
void setVideoBitrate(int bitrate);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| bitrate | int | ビットレート。SDKは、目標ビットレートに応じてエンコードを行い、ネットワークの状態が良くない場合のみ、ビデオビットレートを動的に引き下げます。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html)をご参照ください。 |

>?**推奨する値**：TRTCVideoResolutionの各クラスに注記する最適ビットレートをご参照ください。これをもとにより高いレートに適宜調整することも可能です。例えば、TRTC_VIDEO_RESOLUTION_1280_720に対応する目標ビットレートが1200kbpsであるならば、設定を1500kbpsにし、より鮮明な画像を得ることができます。

### enableAudioEvaluation

音量レベルリマインダを有効にします。
```java
void enableAudioEvaluation(boolean enable);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| enable | boolean | true：オン、false：オフ。 |

>? 有効化すると、onUserVolumeUpdateの中でSDKの音量のボリュームに対する評価を取得できます。

### setAudioPlayVolume

再生音量の設定。
```java
void setAudioPlayVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| volume | int | 再生音量、0-100、 デフォルト100。 |

### setAudioCaptureVolume

マイクの集音音量設定。
```java
void setAudioCaptureVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| volume | int | 集音音量、0-100、 デフォルト100。 |

### startFileDumping

録音の開始。
```java
void startFileDumping(TRTCCloudDef.TRTCAudioRecordingParams trtcAudioRecordingParams);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| trtcAudioRecordingParams | TRTCCloudDef.TRTCAudioRecordingParams | 録音パラメータ。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams)をご参照ください。 |

>? この方法で呼び出した後、 SDKは通話プロセスの中のすべての音声（ローカル音声、リモート音声、BGMなど）を1つのファイルにレコーディングします。ルームに参加しているか否かにかかわらず、このインターフェースを呼び出せば有効となります。leaveRoomを呼び出した時に録音中であれば、録音は自動的に停止します。

### stopFileDumping

録音の停止。
```java
void stopFileDumping();
```

## SDKバージョンインターフェースの取得

### getSdkVersion

SDKバージョン情報を取得します。
```java
int getSdkVersion();
```

## エラーイベントコールバック
### onError

```java
void onError(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| code    | int    | エラーコード。|
| message | String | エラーメッセージ。 |

## 基本イベントコールバック

### onDestroyRoom

ルーム解散のコールバック。
```java
void onDestroyRoom();
```

### onUserVoiceVolume

ユーザー音量の大きさのコールバック。
```java
void onUserVoiceVolume(String userId, int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------------------------------- |
| userId   | String         | ユーザーID。  |
| volume  | int | ユーザーの音量の大きさ、値の範囲0～100。 |

### onRoomMasterChanged

キャスター変更のコールバック。
```java
void onRoomMasterChanged(String previousUserId, String currentUserId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| previousUserId | String | 変更前のキャスターユーザーID。 |
| currentUserId | String | 変更後のキャスターユーザーID。 |


## リモートユーザーコールバックイベント

### onRemoteUserEnter

リモートユーザー入室コールバック。
```java
void onRemoteUserEnter(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | String | ユーザーID。|

### onRemoteUserLeave

リモートユーザー退室コールバック。
```java
void onRemoteUserLeave(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | String | ユーザーID。|

### onRemoteUserCameraAvailable

リモートユーザーが、カメラ、ビデオを起動しているかどうか。
```java
void onRemoteUserCameraAvailable(String userId, boolean available);
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ| 意味  |
| --------- | ------ | ----------------------------------------- |
| userId| String | ユーザーID。|
| available | boolean| true：ビデオストリームデータあり、false：ビデオストリームデータなし。 |

### onRemoteUserScreenVideoAvailable

メンバーのビデオ共有**オン**/**オフ**の通知。
```java
void onRemoteUserScreenVideoAvailable(String userId, boolean available);
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ| 意味  |
| --------- | ------ | ----------------------------------------- |
| userId| String | ユーザーID。|
| available | boolean| 画面共有ストリームデータの有無。 |

### onRemoteUserAudioAvailable

リモートユーザーがオーディオアップストリームを開始したかどうかのコールバック。
```java
void onRemoteUserAudioAvailable(String userId, boolean available);
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ| 意味  |
| --------- | ------ | ----------------------------------------- |
| userId| String | ユーザーID。|
| available | boolean| オーディオデータの有無。 |

### onRemoteUserEnterSpeechState

リモートユーザーが発言を開始します。
```java
void onRemoteUserEnterSpeechState(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | String | ユーザーID。|

### onRemoteUserExitSpeechState

リモートユーザーが発言を終了します。
```java
void onRemoteUserExitSpeechState(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | String | ユーザーID。|


## チャットルームメッセージイベントコールバック

### onReceiveChatMessage

テキストメッセージの受信。
```java
void onReceiveChatMessage(String userId, String message);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| userId   | String         | ユーザーID。  |
| message  | String   | テキストメッセージ。|

### onReceiveRoomCustomMsg

カスタムメッセージの受信。
```java
void onReceiveRoomCustomMsg(String userId, String data);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId    | String | ユーザーID。|
| message | String | カスタムメッセージ。 |

## フィールドコントロールメッセージコールバック

### onReceiveSpeechInvitation

ユーザーがキャスターの発言要請を受信する場合のコールバック。
```java
void onReceiveSpeechInvitation(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | String | キャスターユーザーID。 |

### onReceiveInvitationCancelled

ユーザーがキャスターの発言要請キャンセルを受信する場合のコールバック。
```java
void onReceiveInvitationCancelled(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | String | キャスターユーザーID。 |


### onReceiveSpeechApplication

キャスターがユーザーの発言要請を受信する場合のコールバック。
```java
void onReceiveSpeechApplication(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | String | ユーザーID。|

### onSpeechApplicationCancelled

ユーザーが発言申請をキャンセルする場合のコールバック。
```java
void onSpeechApplicationCancelled(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | String | ユーザーID。|

### onSpeechApplicationForbidden

キャスターが発言申請を禁止する場合のコールバック。
```java
void onSpeechApplicationForbidden(boolean isForbidden);
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味 |
| --------- | ---- | ---------- |
| isForbidden | boolean | 禁止するかどうか。 |

### onOrderedToExitSpeechState

メンバーが発言を停止するようリクエストされる場合のコールバック。
```java
void onOrderedToExitSpeechState(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | String | キャスターユーザーID。 |


### onCallingRollStarted

キャスターが点呼を開始し、メンバーが受信する場合のコールバック。
```java
void onCallingRollStarted(String userId);
```

### onCallingRollStopped

キャスターが点呼を終了し、メンバーが受信する場合のコールバック。
```java
void onCallingRollStopped(String userId);
```

### onMemberReplyCallingRoll

メンバーが点呼に応答し、キャスターが受信する場合のコールバック。
```java
void onMemberReplyCallingRoll(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | String | ユーザーID。|

### onChatRoomMuted

キャスターがチャットルームのミュートを変更する場合のコールバック。
```java
void onChatRoomMuted(boolean muted);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| muted | boolean | 無効にするかどうか。 |

### onMicrophoneMuted

キャスターがマイクの無効化を設定する場合のコールバック。
```java
void onMicrophoneMuted(boolean muted);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| muted | boolean | 無効にするかどうか。 |

### onCameraMuted

キャスターがカメラの無効化を設定する場合のコールバック。
```java
void onCameraMuted(boolean muted);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| muted | boolean | 無効にするかどうか。 |

### onReceiveKickedOff

キャスターによるキックアウトのコールバック。
```java
void onReceiveKickedOff(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| userId | String | キャスター/管理者ユーザーID。 |

## 統計および品質コールバック

### onStatistics

技術指標統計のコールバック。
```java
void onStatistics(TRTCStatistics statistics);
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味 |
| ------ | ---------------------- | ---------- |
| statis | TRTCStatistics | 統計データ。 |

### onNetworkQuality

ネットワーク状況のコールバック。
```java
void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality, List<TRTCCloudDef.TRTCQuality> remoteQuality);

```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | アップストリームのネットワーク品質。|
| remoteQuality | List&amp;lt;TRTCCloudDef.TRTCQuality&amp;gt; | ダウンストリームのネットワーク品質。 |

>? 詳細については、 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b)をご参照ください。


## 画面共有イベントコールバック

### onScreenCaptureStarted

画面共有開始のコールバック。

```java
 void onScreenCaptureStarted();
```

### onScreenCaptureStopped

画面共有停止のコールバック。

```java
void onScreenCaptureStopped(int reason);
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味|
| ------ | ---- | ------------------------------------------------------ |
| reason | int  | 停止の理由。0：ユーザーの自発的な停止。1：その他アプリケーションに占有されたことによる停止。 |
