TUIRoomは、Tencent CloudのTencent Real-Time Communication（TRTC）およびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。
- キャスターがルームを作成し、入室者はルームナンバーを入力した後に入室できます。
- 入室者の間で画面共有を行います。
- 各種のテキストメッセージとカスタムメッセージの送信をサポートします。

TUIRoomはオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実装プロセスについては、 [多人数オーディオビデオルーム(iOS)](https://intl.cloud.tencent.com/document/product/647/37284)をご参照ください。
- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオルームコンポーネントとして使用します。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047) を利用してチャットルームの機能（**IM SDKはiOSバージョンを使用**）を実装します。


## TUIRoom API概要

### TUIRoomCore基本関数

| API| 説明  |
| ----------------------------------- | -------------- |
| [shareInstance](#shareinstance)     | シングルトンオブジェクトを取得します。 |
| [destroyInstance](#destroyinstance) | シングルトンオブジェクトを破棄します。 |
| [setDelegate](#setdelegate)         | イベントコールバックを設定します。 |

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
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__ios.html)を取得します。 |


### 関連設定インターフェース

| API| 説明       |
| ----------------------------------------------- | ---------------------- |
| [setVideoQosPreference](#setvideoqospreference) | ネットワークトラフィックコントロール関連パラメータを設定します。|

### SDKバージョンインターフェース関数の取得

| API  | 説明|
| ------------------------------- | --------------- |
| [getSDKVersion](#getsdkversion) | SDKバージョンを取得します。 |

## TUIRoomCoreDelegate API概要

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
| [onReceiveChatMessage](#onreceivechatmessage) | テキストメッセージ受信のコールバック。 |

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

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37284) シングルトンオブジェクトを取得します。
```objectivec
+ (instancetype)shareInstance;
```
### destroyInstance

```objectivec
+ (void)destroyInstance;
```

### setDelegate

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37284) イベントコールバック。TUIRoomCoreDelegateを介して[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37284)の各種ステータス通知を取得できます。

```objectivec
- (void)setDelegate:(id<TUIRoomCoreDelegate>)delegate;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| delegate | TUIRoomCoreDelegate | イベントコールバッククラスを受信します。 |

### createRoom

ルームの作成（キャスターが呼び出し）。
```objectivec
- (void)createRoom:(NSString *)roomId
        speechMode:(TUIRoomSpeechMode)speechMode
        callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ | 意味  |
|-----------| ------------- | -------------------------------------- |
| roomId  | NSString  |ルームID。ご自身でアサインし、一元管理する必要があります。 |
| speechMode| TUIRoomSpeechMode | 発言モード。|
| callback | TUIRoomActionCallback | ルームの作成結果のコールバック。|

キャスターの通常の呼び出しフローは以下のとおりです。
1. **キャスター**が`createRoom()`を呼び出し、ルームを作成します。ルーム作成の成否はTUIRoomActionCallbackでキャスターに通知されます。
2. **キャスター**が`startCameraPreview()`を呼び出し 、カメラキャプチャとプレビューを起動します。
3. **キャスター**が`startLocalAudio()`を呼び出し、ローカルマイクを起動します。

### destroyRoom

ルームの破棄（キャスターが呼び出し）。キャスターは、ルームの作成後、この関数を呼び出して、ルームを破棄できます。
```objectivec
- (void)destroyRoom:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ | 意味  |
| ------- | ------ | ---------- |
| callback | TUIRoomActionCallback | ルームの破棄結果のコールバック。 |

### enterRoom

入室（ルーム参加メンバーが呼び出し）。
```objectivec
- (void)enterRoom:(NSString *)roomId
        callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| roomId | NSString | ルームID。 |
| callback | TUIRoomActionCallback| 結果のコールバック。 |


ルーム参加メンバーが入室する場合の通常の呼び出し手順は次のとおりです。
1. **入室メンバー**が`enterRoom`を呼び出し、roomIdを渡せば、入室できます。
2. **入室メンバー**が`startCameraPreview()`を呼び出してカメラプレビューを起動し、`startLocalAudio()`を呼び出して、マイクキャプチャを起動します。
3. **入室メンバー**が`onRemoteUserCameraAvailable`のイベントを受信し、`startRemoteView()`を呼び出して、ビデオ再生を開始します。

### leaveRoom

退室（入室メンバーが呼び出し）。
```objectivec
 - (void)leaveRoom:(TUIRoomActionCallback)callback;
```

  パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### getRoomInfo

ルーム情報を取得します。
```objectivec
- (nullable TUIRoomInfo *)getRoomInfo;
```

### getRoomUsers

ルームの全メンバー情報を取得します。
```objectivec
 - (nullable NSArray<TUIRoomUserInfo *> *)getRoomUsers;
```

### getUserInfo

ルームのメンバー情報を取得します。
```objectivec
- (void)getUserInfo:(NSString *)userId
           callback:(TUIRoomUserInfoCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| userId | NSString | ユーザーID。 |
| callback | TUIRoomUserInfoCallback | ルームメンバーの詳細情報のコールバック。 |


### setSelfProfile

ユーザー情報を設定します。
```objectivec
- (void)setSelfProfile:(NSString *)userName
        avatarURL:(NSString *)avatarURL
        callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味  |
| ---------- | ------ | -------------- |
| userName  | NSString | ユーザーの氏名。  |
| avatarURL | NSString | ユーザーのプロフィール画像URL。 |
| callback | TUIRoomActionCallback | 設定が成功したかどうかの結果のコールバック。 |


### transferRoomMaster

グループを他のユーザーに引き渡します。
```objectivec
 - (void)transferRoomMaster:(NSString *)userId
                  callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| userId | NSString | ユーザーID。 |
| callback | TUIRoomActionCallback| 結果のコールバック。 |


## ローカルプッシュインターフェース

### startCameraPreview

ローカルカメラプレビューを起動します。
```objectivec
- (void)startCameraPreview:(BOOL)isFront
                      view:(UIView *)view;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| isFront | BOOL | YES：フロントカメラ、NO：リアカメラ。 |
| view    | UIView | ビデオ画像をロードするウィジェット。                  |


### stopCameraPreview

ローカルカメラプレビューを停止します。
```objectivec
- (void)stopCameraPreview;
```

### startLocalAudio

マイクの集音開始。
```objectivec
- (void)startLocalAudio:(TRTCAudioQuality)quality;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| quality | TRTCAudioQuality | キャプチャの音質。 |

### stopLocalAudio

マイクの集音停止。
```objectivec
- (void)stopLocalAudio;
```
### setVideoMirror

ローカル画面のミラーモードのプレビューを設定します。
```objectivec
 - (void)setVideoMirror:(TRTCVideoMirrorType)type;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| type | TRTCVideoMirrorType | イメージタイプ。 |

### setSpeaker

スピーカーの起動設定。
```objectivec
 - (void)setSpeaker:(BOOL)isUseSpeaker;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ  | 意味 |
| ---- | -------------- | ---------- |
| isUseSpeaker | BOOL | YES：スピーカー、NO：ヘッドホン。 |

## リモートユーザーに関するインターフェース

### startRemoteView
リモートユーザーのビデオストリームのサブスクリプション。

```objectivec
- (void)startRemoteView:(NSString *)userId
                   view:(UIView *)view
             streamType:(TUIRoomStreamType)streamType
               callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ | 意味  |
| -------------- | ------------- | -------------------------- |
| userId  | NSString  | 再生が必要なユーザー ID。  |
| view | UIView  | ビデオ画像をロードするviewウィジェット。 |
| streamType  | TUIRoomStreamType | ストリームのタイプ。|
| callback  | TUIRoomActionCallback | 結果のコールバック。|


### stopRemoteView

サブスクリプションをキャンセルし、リモートビデオ画面の再生を停止します。
```objectivec
- (void)stopRemoteView:(NSString *)userId
            streamType:(TUIRoomStreamType)streamType
              callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味  |
| ------- | ------------- | ----------------------- |
| userId | NSString  | 再生停止が必要なユーザーのID。 |
| streamType | TUIRoomStreamType  | ストリームのタイプ。 |
| callback  | TUIRoomActionCallback | 結果のコールバック。|

### switchCamera

フロント/リアカメラを切り替えます。
```objectivec
- (void)switchCamera:(BOOL)isFront;

```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ    | 意味  |
| ------- | ------------- | ----------------------- |
| isFront | BOOL  | YES：フロントカメラ、NO：リアカメラ。 |

## メッセージ送信インターフェース

### sendChatMessage

ルーム内でテキストメッセージをブロードキャストします。通常、テキストによるチャットに使用します。
```objectivec
- (void)sendChatMessage:(NSString *)message
               callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| message | NSString | メッセージの内容。 |
| callback  | TUIRoomActionCallback | 送信結果のコールバック。|

## フィールドコントロール関連インターフェース

### muteUserMicrophone

特定ユーザーのマイクを無効化/再有効化します。
```objectivec
- (void)muteUserMicrophone:(NSString *)userId
                      mute:(BOOL)mute
                  callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | NSString| ユーザーID。  |
| mute  | BOOL  | 無効にするかどうか。 |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### muteAllUsersMicrophone

全ユーザーのマイクを無効化/再有効化します。
```objectivec
- (void)muteAllUsersMicrophone:(BOOL)mute
                      callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ---- | ---- | ---------- |
| mute | BOOL | 無効にするかどうか。 |
| callback | TUIRoomActionCallback | 結果のコールバック。 |


### muteUserCamera

特定ユーザーのカメラを無効化/再有効化します。
```objectivec
- (void)muteUserCamera:(NSString *)userId
                  mute:(BOOL)mute
              callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | NSString| ユーザーID。  |
| mute  | BOOL  | 無効にするかどうか。 |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### muteAllUsersCamera

全ユーザーのカメラを無効化/再有効化します。
```objectivec
- (void)muteAllUsersCamera:(BOOL)mute
                  callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ---- | ---- | ---------- |
| mute  | BOOL  | 無効にするかどうか。 |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### muteChatRoom

テキストチャットのミュート/再有効化。
```objectivec
- (void)muteChatRoom:(BOOL)mute
            callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
| ---- | ---- | ---------- |
| mute  | BOOL  | 無効にするかどうか。 |
| callback | TUIRoomActionCallback | 結果のコールバック。 |


### kickOffUser

キャスターがキックアウトします。
```objectivec
- (void)kickOffUser:(NSString *)userId
           callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | NSString| ユーザーID。  |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### startCallingRoll

キャスターが点呼を開始します。
```objectivec
 - (void)startCallingRoll:(TUIRoomActionCallback)callback;
```
パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### stopCallingRoll

キャスターが点呼を終了します。
```objectivec
- (void)stopCallingRoll:(TUIRoomActionCallback)callback;
```
パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### replyCallingRoll

メンバーがキャスターの点呼に応答します。
```objectivec
- (void)replyCallingRoll:(TUIRoomActionCallback)callback;
```
パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### sendSpeechInvitation

キャスターがメンバーの発言を要請します。
```objectivec
- (void)sendSpeechInvitation:(NSString *)userId
                    callback:(TUIRoomInviteeCallback)callback
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | NSString| ユーザーID。  |
| callback | TUIRoomInviteeCallback | 結果のコールバック。 |

### cancelSpeechInvitation

キャスターがメンバーへの発言要請をキャンセルします。
```objectivec
- (void)cancelSpeechInvitation:(NSString *)userId
                      callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | NSString| ユーザーID。  |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### replySpeechInvitation

メンバーがキャスターの発言要請に同意/を拒否します。
```objectivec
- (void)replySpeechInvitation:(BOOL)agree
                     callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| agree | BOOL  | 同意するかどうか。 |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### sendSpeechApplication

メンバーが発言を要請します。
```objectivec
- (void)sendSpeechApplication:(TUIRoomInviteeCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomInviteeCallback | 結果のコールバック。 |

### cancelSpeechApplication

メンバーが発言申請をキャンセルします。
```objectivec
- (void)cancelSpeechApplication:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback| 結果のコールバック。 |

### replySpeechApplication

キャスターがメンバーの発言申請に同意/を拒否します。
```objectivec
- (void)replySpeechApplication:(BOOL)agree
                        userId:(NSString *)userId
                      callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| agree  | BOOL| 同意するかどうか  |
| userId  | NSString| ユーザーID。  |
| callback | TUIRoomActionCallback | 結果のコールバック。 |

### forbidSpeechApplication

キャスターが発言申請を禁止します。
```objectivec
- (void)forbidSpeechApplication:(BOOL)forbid
                       callback:(TUIRoomActionCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味 |
| ------ | ---- | ---------- |
| forbid | BOOL | 禁止するかどうか。|
| callback | TUIRoomActionCallback | 結果のコールバック。 |


### sendOffSpeaker

キャスターがメンバーに発言の停止を命令します。
```objectivec
- (void)sendOffSpeaker:(NSString *)userId
              callback:(TUIRoomInviteeCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| userId  | NSString| ユーザーID。  |
| callback | TUIRoomInviteeCallback | 結果のコールバック。 |

### sendOffAllSpeakers

キャスターが全メンバーに発言の停止を命令します。
```objectivec
- (void)sendOffAllSpeakers:(TUIRoomInviteeCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomInviteeCallback| 結果のコールバック。 |

### exitSpeechState

メンバーが発言を停止し、視聴者になります。
```objectivec
- (void)exitSpeechState:(TUIRoomActionCallback)callback;
```
パラメータは下表に示すとおりです。

| パラメータ  | タイプ  | 意味 |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | 結果のコールバック。 |


## 画面共有インターフェース
### startScreenCapture

画面共有を開始。
```objectivec
- (void)startScreenCapture:(TRTCVideoEncParam *)encParam API_AVAILABLE(ios(11.0));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| encParams | TRTCVideoEncParam | 画面共有時のエンコードパラメータを設定します。 |

>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff)をご参照ください。

### stopScreenCapture

画面キャプチャの停止。
```objectivec
- (void)stopScreenCapture API_AVAILABLE(ios(11.0));
```

## 美顔フィルタに関するインターフェース関数
### getBeautyManager

美顔管理オブジェクト[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__ios.html)を取得します。
```objectivec
- (TXBeautyManager *)getBeautyManager;
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
```objectivec
- (void)setVideoQosPreference:(TRTCNetworkQosParam *)preference;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味  |
| ---------- | --------------------- | -------------- |
| preference | TRTCNetworkQosParam | ネットワークトラフィックコントロールポリシー。 |

### setAudioQuality

音質の設定。
```objectivec
- (void)setAudioQuality:(TRTCAudioQuality)quality;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| quality | TRTCAudioQuality | 音質。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53)をご参照ください。 |

### setVideoResolution

解像度の設定。

```objectivec
- (void)setVideoResolution:(TRTCVideoResolution)resolution;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| resolution | TRTCVideoResolution | ビデオの解像度。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5)をご参照ください。 |


### setVideoFps

フレームレートの設定。
```objectivec
- (void)setVideoFps:(int)fps;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| fps  | int  | ビデオキャプチャのフレームレート。 |

>? **推奨する値**：15fpsまたは20fps。5fps以下ではラグ感が目立ち、10fps以下では軽微なラグ感があります。20fps以上は高すぎて浪費になります（映画のフレームレートは24fps）。


### setVideoBitrate

ビットレートの設定。
```objectivec
- (void)setVideoBitrate:(int)bitrate;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| bitrate | int | ビットレート。SDKは、目標ビットレートに応じてエンコードを行い、ネットワークの状態が良くない場合のみ、ビデオビットレートを動的に引き下げます。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454)をご参照ください。 |

>?**推奨する値**：TRTCVideoResolutionの各クラスに注記する最適ビットレートをご参照ください。これをもとにより高いレートに適宜調整することも可能です。例えば、TRTC_VIDEO_RESOLUTION_1280_720に対応する目標ビットレートが1200kbpsであるならば、設定を1500kbpsにし、より鮮明な画像を得ることができます。

### enableAudioEvaluation

音量レベルリマインダを有効にします。
```objectivec
- (void)enableAudioEvaluation:(BOOL)enable;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| enable | BOOL | YES：オン、NO：オフ。 |

>? 有効化すると、onUserVolumeUpdateの中でSDKの音量のボリュームに対する評価を取得できます。

### setAudioPlayVolume

再生音量の設定。
```objectivec
- (void)setAudioPlayVolume:(NSInteger)volume;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| volume | int | 再生音量、0-100、 デフォルト100。 |

### setAudioCaptureVolume

マイクの集音音量設定。
```objectivec
- (void)setAudioCaptureVolume:(NSInteger)volume;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| volume | int | 集音音量、0-100、 デフォルト100。 |

### startFileDumping

録音の開始。
```objectivec
- (void)startFileDumping:(TRTCAudioRecordingParams *)params;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| params | TRTCAudioRecordingParams | 録音パラメータ。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams)をご参照ください。 |

>? この方法で呼び出した後、 SDKは通話プロセスの中のすべての音声（ローカル音声、リモート音声、BGMなど）を1つのファイルにレコーディングします。ルームに参加しているか否かにかかわらず、このインターフェースを呼び出せば有効となります。leaveRoomを呼び出した時に録音中であれば、録音は自動的に停止します。

### stopFileDumping

録音の停止。
```objectivec
- (void)stopFileDumping;
```

## SDKバージョンインターフェースの取得

### getSdkVersion

SDKバージョン情報を取得します。
```objectivec
- (NSInteger)getSdkVersion;
```

## エラーイベントコールバック
### onError

```objectivec
- (void)onError:(NSInteger)code message:(NSString *)message;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| code | NSInteger | エラーコード。|
| message | NSString  | エラー情報。 |

## 基本イベントコールバック

### onDestroyRoom

ルーム解散のコールバック。
```objectivec
- (void)onDestroyRoom;
```

### onUserVoiceVolume

ユーザー音量の大きさのコールバック。
```objectivec
- (void)onUserVoiceVolume:(NSString *)userId volume:(NSInteger)volume;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------------------------------- |
| userId | NSString | ユーザーID。  |
| volume  | NSInteger | ユーザーの音量の大きさ。値の範囲は0～100。 |

### onRoomMasterChanged

キャスター変更のコールバック。
```objectivec
- (void)onRoomMasterChanged:(NSString *)previousUserId
              currentUserId:(NSString *)currentUserId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| previousUserId | NSString | 変更前のキャスターユーザーID。 |
| currentUserId | NSString | 変更後のキャスターユーザーID。 |


## リモートユーザーコールバックイベント

### onRemoteUserEnter

リモートユーザー入室コールバック。
```objectivec
- (void)onRemoteUserEnter:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | NSString       | ユーザーID。              |

### onRemoteUserLeave

リモートユーザー退室コールバック。
```objectivec
- (void)onRemoteUserLeave:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | NSString       | ユーザーID。              |

### onRemoteUserCameraAvailable

リモートユーザーが、カメラ、ビデオを起動しているかどうか。
```objectivec
- (void)onRemoteUserCameraAvailable:(NSString *)userId
                          available:(BOOL)available;
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ| 意味  |
| --------- | ------ | ----------------------------------------- |
| userId| NSString | ユーザーID。|
| available | BOOL| YES：ビデオストリームデータあり、NO：ビデオストリームデータなし。 |

### onRemoteUserScreenVideoAvailable

メンバーのビデオ共有**オン**/**オフ**の通知。
```objectivec
- (void)onRemoteUserScreenVideoAvailable:(NSString *)userId
                               available:(BOOL)available;
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ| 意味  |
| --------- | ------ | ----------------------------------------- |
| userId| NSString | ユーザーID。|
| available | BOOL| 画面共有ストリームデータの有無。 |

### onRemoteUserAudioAvailable

リモートユーザーがオーディオアップストリームを開始したかどうかのコールバック。
```objectivec
- (void)onRemoteUserAudioAvailable:(NSString *)userId
                         available:(BOOL)available;
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ| 意味  |
| --------- | ------ | ----------------------------------------- |
| userId| NSString | ユーザーID。|
| available | BOOL| オーディオデータの有無。 |

### onRemoteUserEnterSpeechState

リモートユーザーが発言を開始します。
```objectivec
- (void)onRemoteUserEnterSpeechState:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | NSString       | ユーザーID。              |

### onRemoteUserExitSpeechState

リモートユーザーが発言を終了します。
```objectivec
- (void)onRemoteUserExitSpeechState:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | NSString       | ユーザーID。              |


## チャットルームメッセージイベントコールバック

### onReceiveChatMessage

テキストメッセージの受信。
```objectivec
- (void)onReceiveChatMessage:(NSString *)userId message:(NSString *)message;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味 |
| ------- | ------ | ---------- |
| userId | NSString | ユーザーID。  |
| message  | NSString       | テキストメッセージ。     |


## フィールドコントロールメッセージコールバック

### onReceiveSpeechInvitation

ユーザーがキャスターの発言要請を受信する場合のコールバック。
```objectivec
- (void)onReceiveSpeechInvitation:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | NSString | キャスターユーザーID。 |

### onReceiveInvitationCancelled

ユーザーがキャスターの発言要請キャンセルを受信する場合のコールバック。
```objectivec
- (void)onReceiveInvitationCancelled:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | NSString | キャスターユーザーID。 |

### OnReceiveSpeechApplication

キャスターがユーザーの発言要請を受信する場合のコールバック。
```objectivec
void onReceiveSpeechApplication(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | NSString       | ユーザーID。              |

### onSpeechApplicationCancelled

ユーザーが発言申請をキャンセルする場合のコールバック。
```objectivec
- (void)onSpeechApplicationCancelled:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | NSString       | ユーザーID。              |

### onSpeechApplicationForbidden

キャスターが発言申請を禁止する場合のコールバック。
```objectivec
- (void)onSpeechApplicationForbidden:(BOOL)isForbidden userId:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味 |
| --------- | ---- | ---------- |
| isForbidden | BOOL | 禁止するかどうか。 |
| userId    | NSString       | ユーザーID。              |

### onOrderedToExitSpeechState

メンバーが発言を停止するようリクエストされる場合のコールバック。
```objectivec
- (void)onOrderedToExitSpeechState:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | NSString | キャスターユーザーID。 |


### onCallingRollStarted

キャスターが点呼を開始し、メンバーが受信する場合のコールバック。
```objectivec
- (void)onCallingRollStarted:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | NSString | キャスターユーザーID。 |

### onCallingRollStopped

キャスターが点呼を終了し、メンバーが受信する場合のコールバック。
```objectivec
- (void)onCallingRollStopped:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | ------------ |
| userId | NSString | キャスターユーザーID。 |

### onMemberReplyCallingRoll

メンバーが点呼に応答し、キャスターが受信する場合のコールバック。
```objectivec
- (void)onMemberReplyCallingRoll:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ| 意味|
| ------- | ------ | --------- |
| userId    | NSString       | ユーザーID。              |

### onChatRoomMuted

キャスターがチャットルームのミュートを変更する場合のコールバック。
```objectivec
- (void)onChatRoomMuted:(BOOL)muted userId:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| muted | BOOL | 無効にするかどうか。 |
| userId | NSString | キャスターユーザーID。 |

### onMicrophoneMuted

キャスターがマイクの無効化を設定する場合のコールバック。
```objectivec
- (void)onMicrophoneMuted:(BOOL)muted userId:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| muted | BOOL | 無効にするかどうか。 |
| userId | NSString | キャスターユーザーID。 |

### onCameraMuted

キャスターがカメラの無効化を設定する場合のコールバック。
```objectivec
- (void)onCameraMuted:(BOOL)muted userId:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| muted | BOOL | 無効にするかどうか。 |
| userId | NSString | キャスターユーザーID。 |

### onReceiveKickedOff

キャスターによるキックアウトのコールバック。
```objectivec
- (void)onReceiveKickedOff:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ  | タイプ   | 意味          |
| ----- | ---- | ---------- |
| userId | NSString | キャスター/管理者ユーザーID。 |

## 統計および品質コールバック

### onStatistics

技術指標統計のコールバック。
```objectivec
- (void)onStatistics:(TRTCStatistics *)statistics;
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味 |
| ------ | ---------------------- | ---------- |
| statis | TRTCStatistics | 統計データ。 |

### onNetworkQuality

ネットワーク状況のコールバック。
```objectivec
- (void)onNetworkQuality:(TRTCQualityInfo *)localQuality remoteQuality:(NSArray<TRTCQualityInfo *> *)remoteQuality;

```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| localQuality  | TRTCQualityInfo            | アップストリームネットワークの品質。 |
| remoteQuality |NSArray&lt;TRTCQualityInfo *&gt; | ダウンストリームネットワークの品質。 |

>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28)をご参照ください。


## 画面共有イベントコールバック

### onScreenCaptureStarted

画面共有開始のコールバック。

```objectivec
 - (void)onScreenCaptureStarted;
```

### onScreenCaptureStopped

画面共有停止のコールバック。

```objectivec
- (void)onScreenCaptureStopped:(NSInteger)reason;
```

パラメータは下表に示すとおりです。

| パラメータ| タイプ | 意味|
| ------ | ---- | ------------------------------------------------------ |
| reason | NSInteger  | 停止の理由。0：ユーザーの自発的な停止。1：その他のアプリケーションに占有されたことによる停止。 |
