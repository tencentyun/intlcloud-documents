TUIRoomは、Tencent CloudのTencent Real-Time Communication（TRTC）およびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。
- キャスターがルームを作成し、参加者はルームナンバーを入力した後に入室できます。
- 参加者の間で画面共有を行います。
- 各種のテキストメッセージとカスタムメッセージの送信をサポートします。

TUIRoomはオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実装プロセスについては、 [多人数オーディオビデオルーム(Windows&Mac)](https://intl.cloud.tencent.com/document/product/647/44071)をご参照ください。
- TRTC SDK： [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) を低遅延のビデオミーティングのコンポーネントとして使用します。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047) を利用してチャットルームの機能（**IM SDKはC++バージョンを使用**）を実装します。


## TUIRoom API概要[](id:TUIRoom)

### TUIRoomCore基本関数

| API                                 | 説明           |
|-----|-----|
| [GetInstance](#getinstance)         |  シングルトンオブジェクトを取得します。 |
| [DestroyInstance](#destroyinstance) | シングルトンオブジェクトを破棄します。 |
| [SetCallback](#setcallback)         | イベントコールバックを設定します。 |

### ルーム関連インターフェース関数

| API          | 説明         |
|-----|-----|
| [login](#login)                           | ログイン。                             |
| [logout](#logout)                         | ログアウト。                             |
| [CreateRoom](#createroom)                 | ルームの作成（キャスターが呼び出し）。           |
| [DestroyRoom](#destroyroom)               | ルームの破棄（キャスターが呼び出し）。           |
| [EnterRoom](#enterroom)                   | 入室（参加者が呼び出し）。         |
| [LeaveRoom](#leaveroom)                   | 退室（参加者またはキャスターが呼び出し）。 |
| [GetRoomInfo](#getroominfo)               | ルーム情報の取得。                     |
| [GetRoomUsers](#getroomusers)             | ルーム内全メンバー情報の取得。           |
| [GetUserInfo](#getuserinfo)               | 特定ユーザーの情報の取得。               |
| [TransferRoomMaster](#transferroommaster) | キャスター権限の移転（キャスターが呼び出し）。     |

### ローカルのオーディオビデオ操作インターフェース

| API                                                   | 説明                       |
|-----|-----|
| [StartCameraPreview](#startcamerapreview)             | ローカルビデオのプレビュー画面を立ち上げます。   |
| [StopCameraPreview](#stopcamerapreview)               | ローカルビデオキャプチャおよびプレビューを停止します。   |
| [UpdateCameraPreview](#updatecamerapreview)           | ローカルビデオレンダリングウィンドウを変更します。     |
| [StartLocalAudio](#startlocalaudio)                   | マイクキャプチャを起動します。           |
| [StopLocalAudio](#stoplocalaudio)                     | マイクキャプチャを停止します。           |
| [StartSystemAudioLoopback](#startsystemaudioloopback) | システム音声のキャプチャを起動/停止します。  |
| [StopSystemAudioLoopback](#stopsystemaudioloopback)   | システム音声のキャプチャを起動/停止します。  |
| [SetVideoMirror](#setvideomirror)                     | ローカル画面のミラーモードのプレビューを設定します。 |

### リモートユーザーに関するインターフェース

| API                                   | 説明                               |
|-----|-----|
| [StartRemoteView](#startremoteview)   | 指定メンバーのリモートビデオ画面をサブスクリプションし再生します。 |
| [StopRemoteView](#stopremoteview)     |  リモートビデオ画面のサブスクリプションをキャンセルし再生を停止します。   |
| [UpdateRemoteView](#updateremoteview) | リモートユーザーのビデオレンダリングウィンドウを変更します。       |

### チャットメッセージ送信インターフェース

| API                                     | 説明             |
|-----|-----|
| [SendChatMessage](#sendchatmessage)     | チャットメッセージを送信します。   |
| [SendCustomMessage](#sendcustommessage) | カスタムメッセージを送信します。 |

### フィールドコントロール関連インターフェース

| API                                                 | 説明                                                    |
|-----|-----|
| [MuteUserMicrophone](#muteusermicrophone)           | 特定ユーザーのマイクを無効化/再有効化します。                               |
| [MuteAllUsersMicrophone](#muteallusersmicrophone)   | 全ユーザーのマイクを無効化/再有効化し、ステータスをルーム情報に同期させます。 |
| [MuteUserCamera](#muteusercamera)                   |特定ユーザーのカメラを無効化/再有効化します。                               |
| [MuteAllUsersCamera](#mutealluserscamera)           | 全ユーザーのカメラを無効化/再有効化し、ステータスをルーム情報に同期させます。 |
| [MuteChatRoom](#mutechatroom)                       | チャットルームのミュートを開始/停止します（キャスターが呼び出し）。                     |
| [KickOffUser](#kickoffuser)                         | ルーム内の特定ユーザーをリムーブします（キャスターが呼び出し）。                        |
| [StartCallingRoll](#startcallingroll)               | キャスターが点呼を開始します。                                        |
| [StopCallingRoll](#stopcallingroll)                 | キャスターが点呼を終了します。                                        |
| [ReplyCallingRoll](#replycallingroll)               | メンバーがキャスターの点呼に応答します。                                    |
| [SendSpeechInvitation](#sendspeechinvitation)       | キャスターがメンバーに発言するようインビテーションを送信します。                                    |
| [CancelSpeechInvitation](#cancelspeechinvitation)   | キャスターがメンバーの発言のためのインビテーションをキャンセルします。                                |
| [ReplySpeechInvitation](#replyspeechinvitation)     | メンバーがキャスターの発言申請に同意/を拒否します。                         |
| [SendSpeechApplication](#sendspeechapplication)     | メンバーが発言を要請します。                                          |
| [CancelSpeechApplication](#cancelspeechapplication) | メンバーが発言申請をキャンセルします。                                      |
| [ReplySpeechApplication](#replyspeechapplication)   | キャスターがメンバーの発言申請に同意/拒否します。                         |
| [ForbidSpeechApplication](#forbidspeechapplication) | キャスターが発言申請を禁止します。                                    |
| [SendOffSpeaker](#sendoffspeaker)                   | キャスターがメンバーに発言を停止するよう命令します。                                  |
| [SendOffAllSpeakers](#sendoffallspeakers)           | キャスターが全員に発言を停止するよう命令します。                                  |
| [ExitSpeechState](#exitspeechstate)                 | メンバーは発言を停止し、視聴者になります。                               |

### 基本コンポーネントインターフェース関数

| API                                             | 説明                                       |
|-----|-----|
| [GetDeviceManager](#getdevicemanager)           | ローカル設定管理オブジェクトITXDeviceManagerを取得します。    |
| [GetScreenShareManager](#getscreensharemanager) | 画面共有管理オブジェクトIScreenShareManagerを取得します。 |

### クラウドレコーディングインターフェース関数

| API                                   | 説明          |
|-----|-----|
| [StartCloudRecord](#startcloudrecord) | クラウドレコーディングを開始します 。 |
| [StopCloudRecord](#stopcloudrecord)   | クラウドレコーディングを停止します 。 |

### 美顔関連インターフェース関数

| API          | 説明         |
|-----|-----|
| [SetBeautyStyle](#setbeautystyle) | 美顔を設定します。|

### 関連設定インターフェース

| API          | 説明         |
|-----|-----|
| [SetVideoQosPreference](#setvideoqospreference) | ネットワークトラフィックコントロール関連パラメータを設定します。|

### SDKバージョンインターフェース関数の取得

| API          | 説明         |
|-----|-----|
| [GetSDKVersion](#getsdkversion) | SDKバージョンを取得します。|

## TUIRoomCoreCallback API概要[](id:TUIRoomCoreCallback)

### エラーイベントコールバック

| API          | 説明         |
|-----|-----|
| [OnError](#onerror) | エラーのコールバック。 |

### 基本イベントコールバック

| API                                         | 説明               |
|-----|-----|
| [OnLogin](#onlogin)                         | ログインコールバック。         |
| [OnLogout](#onlogout)                       | ログアウトコールバック。         |
| [OnCreateRoom](#oncreateroom)               | ルーム作成のコールバック。     |
| [OnDestroyRoom](#ondestroyroom)             | ルーム解散のコールバック。     |
| [OnEnterRoom](#onenterroom)                 | 入室のコールバック。     |
| [OnExitRoom](#onexitroom)                   | 退室のコールバック。     |
| [OnFirstVideoFrame](#onfirstvideoframe)     | 最初のフレーム画面のコールバック。     |
| [OnUserVoiceVolume](#onuservoicevolume)     | 音量の大きさのコールバック。 |
| [OnRoomMasterChanged](#onroommasterchanged) | キャスター変更のコールバック。   |

### リモートユーザーイベントコールバック

| API                                                          | 説明                            |
|-----|-----|
| [OnRemoteUserEnter](#onremoteuserenter)                      | リモートユーザー入室コールバック。           |
| [OnRemoteUserLeave](#onremoteuserleave)                      | リモートユーザー退室コールバック。           |
| [OnRemoteUserCameraAvailable](#onremoteusercameraavailable)  | リモートユーザーがカメラビデオを起動するかどうかのコールバック。 |
| [OnRemoteUserScreenAvailable](#onremoteuserscreenavailable) | リモートユーザーが画面共有を開始するかどうかのコールバック。   |
| [OnRemoteUserAudioAvailable](#onremoteuseraudioavailable)    | リモートユーザーがマイクをオンにしているかどうかのコールバック。   |
| [OnRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | リモートユーザーの発言開始のコールバック。           |
| [OnRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | リモートユーザーの発言終了のコールバック。           |

### メッセージイベントのコールバック

| API                                               | 説明             |
|-----|-----|
| [OnReceiveChatMessage](#onreceivechatmessage)     | テキストメッセージ受信のコールバック。 |
| [OnReceiveCustomMessage](#onreceivecustommessage) | テキストメッセージ受信のコールバック。 |

### フィールドコントロールイベントコールバック

| API                                                          | 説明                            |
|-----|-----|
| [OnReceiveSpeechInvitation](#onreceivespeechinvitation)      | ユーザーがキャスターの発言要請を受信した場合のコールバック。       |
| [OnReceiveInvitationCancelled](#onreceiveinvitationcancelled) | ユーザーがキャスターの発言要請キャンセルを受信する場合のコールバック。   |
| [OnReceiveReplyToSpeechInvitation](#onreceivereplytospeechinvitation) | キャスターがユーザーの発言要請への同意を受信する場合のコールバック。 |
| [OnReceiveSpeechApplication](#onreceivespeechapplication)    | キャスターがユーザーの発言要請を受信する場合のコールバック。     |
| [OnSpeechApplicationCancelled](#onspeechapplicationcancelled) | ユーザーが発言申請をキャンセルする場合のコールバック。             |
| [OnReceiveReplyToSpeechApplication](#onreceivereplytospeechapplication) | キャスターが発言要請に同意する場合のコールバック。           |
| [OnSpeechApplicationForbidden](#onspeechapplicationforbidden) | キャスターが発言申請を禁止する場合のコールバック。           |
| [OnOrderedToExitSpeechState](#onorderedtoexitspeechstate)  | メンバーが発言の停止をリクエストされる場合のコールバック。         |
| [OnCallingRollStarted](#oncallingrollstarted)                | キャスターが点呼を開始し、メンバーが受信する場合のコールバック。   |
| [OnCallingRollStopped](#oncallingrollstopped)                | キャスターが点呼を終了し、メンバーが受信する場合のコールバック。   |
| [OnMemberReplyCallingRoll](#onmemberreplycallingroll)        | メンバーが点呼に応答し、キャスターが受信する場合のコールバック。   |
| [OnChatRoomMuted](#onchatroommuted)                          | キャスターがチャットルームのミュートを変更する場合のコールバック。     |
| [OnMicrophoneMuted](#onmicrophonemuted)                      | キャスターがマイクの無効化を設定する場合のコールバック。         |
| [OnCameraMuted](#oncameramuted)                              | キャスターがカメラの無効化を設定する場合のコールバック。         |

### 統計および品質コールバック

| API          | 説明         |
|-----|-----|
| [OnStatistics](#onstatistics)         | 技術指標統計のコールバック。 |
| [OnNetworkQuality](#onnetworkquality) | ネットワーク品質のコールバック。     |

### 画面共有関連コールバック

| API                                               | 説明             |
|-----|-----|
| [OnScreenCaptureStarted](#onscreencapturestarted) | 画面共有開始のコールバック。 |
| [OnScreenCaptureStopped](#onscreencapturestopped) | 画面共有停止のコールバック。 |

### ビデオレコーディングコールバック

| API                                   | 説明           |
|-----|-----|
| [OnRecordError](#onrecorderror)       | レコーディングエラーのコールバック。 |
| [OnRecordComplete](#onrecordcomplete) | レコーディング完了のコールバック。 |
| [OnRecordProgress](#onrecordprogress) | レコーディング進捗のコールバック。 |


### ローカルデバイステストコールバック

| API                                                          | 説明                   |
|-----|-----|
| [OnTestSpeakerVolume](#ontestspeakervolume)                  | スピーカー音量のコールバック。       |
| [OnTestMicrophoneVolume](#ontestmicrophonevolume)            | マイク音量のコールバック。       |
| [OnAudioDeviceCaptureVolumeChanged](#onaudiodevicecapturevolumechanged) | システムキャプチャ音量調節のコールバック。 |
| [OnAudioDevicePlayoutVolumeChanged](#onaudiodeviceplayoutvolumechanged) | システム再生音量調節のコールバック。 |

## TUIRoomCore基本関数

### GetInstance

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/44071) シングルトンオブジェクトを取得します。
```C++
 static TUIRoomCore* GetInstance();
```

### DestroyInstance

```C++
static void DestroyInstance();
```

### SetCallback

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/44071)イベントコールバック。TUIRoomCoreCallbackを介して[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/44071)の各種ステータス通知を取得できます。

```C++
virtual void SetCallback(const TUIRoomCoreCallback* callback) = 0;
```

### Login

ログイン
```C++
virtual int Login(int sdk_appid, const std::string& user_id, const std::string& user_sig) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| sdk_appid | int | TRTCコンソール > **[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)**> アプリケーション情報の中でSDKAppIDを確認できます。 |
| user_id | string | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-z、A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。 |
| user_sig | string | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 [UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |

### Logout

ログアウト。
```C++
virtual int Logout() = 0;
```

### CreateRoom

ルームの作成（キャスターが呼び出し）。
```C++
virtual int CreateRoom(const std::string& room_id, TUISpeechMode speech_mode) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| room_id | string |ルームIDは、ご自身でアサインし、一元管理する必要があります。 |
| speech_mode | TUISpeechMode | 発言モード。 |

キャスターの通常の呼び出しフローは以下のとおりです。
1. **キャスター**が`CreateRoom()` を呼び出し、ルームを作成します。ルームの作成に成功したかどうかがOnCreateRoomを介してキャスターに通知されます。
2. **キャスター**が`EnterRoom()`を呼び出し、入室します。
3. **キャスター**が`StartCameraPreview()`を呼び出し 、カメラキャプチャとプレビューを起動します。
4. **キャスター**が`StartLocalAudio()`を呼び出し、ローカルマイクを起動します。

### DestroyRoom

ルームの破棄（キャスターが呼び出し）。キャスターは、ルームの作成後、この関数を呼び出して、ルームを破棄できます。
```C++
virtual int DestroyRoom() = 0;
```

### EnterRoom

入室（参加者が呼び出し）。
```C++
virtual int EnterRoom(const std::string& room_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| room_id | string | ルームID。 |

参加者が入室する場合の通常の呼び出し手順は次のとおりです。
1. **参加者**が`EnterRoom`を呼び出し、room_idを渡せば、入室できます。
2. **参加者**が`startCameraPreview()`を呼び出して、カメラプレビューを起動し、`StartLocalAudio()`を呼び出して、マイクキャプチャを起動します。
3. **参加者**が`OnRemoteUserCameraAvailable`のイベントを受信し、`StartRemoteView()`を呼び出して、ビデオ再生を開始します。

### LeaveRoom

退室（参加者が呼び出し）。
```C++
virtual int LeaveRoom() = 0;
```

### GetRoomInfo

ルーム情報を取得します。
```C++
virtual TUIRoomInfo GetRoomInfo() = 0;
```

### GetRoomUsers

ルームの全メンバー情報を取得します。
```C++
virtual std::vector<TUIUserInfo> GetRoomUsers() = 0;
```

### GetUserInfo

ルームのメンバー情報を取得します。
```C++
virtual const TUIUserInfo* GetUserInfo(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザーID。 |

### SetSelfProfile

ユーザーの属性を設定します。
```C++
virtual int SetSelfProfile(const std::string& user_name, const std::string& avatar_url) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_name | string | ユーザー氏名。 |
| avatar_url | string | ユーザーのプロフィール画像URL。 |

### TransferRoomMaster

グループを他のユーザーに引き渡します。
```C++
virtual int TransferRoomMaster(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザーID。 |

## ローカルプッシュインターフェース

### StartCameraPreview

ローカルカメラプレビューを起動します。
```C++
virtual int StartCameraPreview(const liteav::TXView& view) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| view | liteav::TXView | ウィンドウハンドル。 |

### StopCameraPreview

ローカルカメラプレビューを停止します。
```C++
virtual int StopCameraPreview() = 0;
```

### UpdateCameraPreview

ローカルビデオプレビュー画面のウィンドウを更新します。
```C++
virtual int UpdateCameraPreview(const liteav::TXView& view) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| view | liteav::TXView | ウィンドウハンドル。 |

### StartLocalAudio

ローカルオーディオデバイスを起動します。
```C++
virtual int StartLocalAudio(const liteav::TRTCAudioQuality& quality) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| view | liteav::TXView | ウィンドウハンドル。 |

### StopLocalAudio

ローカルオーディオデバイスを停止します。
```C++
virtual int StopLocalAudio() = 0;
```

### StartSystemAudioLoopback

システム音声のキャプチャを開始します。
```C++
virtual int StartSystemAudioLoopback() = 0;
```

### StopSystemAudioLoopback

システム音声のキャプチャを停止します。
```C++
virtual int StopSystemAudioLoopback() = 0;
```

### SetVideoMirror

イメージを設定します。
```C++
virtual int SetVideoMirror(bool mirror) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| mirror | bool | ミラーオン/オフ。 |

## リモートユーザーに関するインターフェース

### StartRemoteView
リモートユーザーのビデオストリームのサブスクリプション。

```C++
virtual int StartRemoteView(const std::string& user_id, const liteav::TXView& view,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | 再生が必要なユーザー ID。 |
| liteav::TXView | TXView | ビデオ画像をロードするviewウィジェット。|
| type | TUIStreamType | ストリームのタイプ。|

### StopRemoteView

サブスクリプションをキャンセルし、リモートビデオ画面の再生を停止します。
```C++
virtual int StopRemoteView(const std::string& user_id,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | 再生の停止が必要なユーザー ID。 |
| type | TUIStreamType | ストリームのタイプ。|

### UpdateRemoteView

リモートビデオレンダリングウィンドウを更新します。
```C++
virtual int UpdateRemoteView(const std::string& user_id, TUIStreamType type, liteav::TXView& view) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| type | TUIStreamType | ストリームのタイプ。|
| view | liteav::TXView | レンダリングウィンドウハンドル。|

## メッセージ送信インターフェース

### SendChatMessage

テキストメッセージを送信します。
```C++
virtual int SendChatMessage(const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| message | string | メッセージの内容。 |

### SendCustomMessage

カスタムメッセージを送信します。
```C++
virtual int SendCustomMessage(const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| message | string | メッセージの内容。 |

## フィールドコントロール関連インターフェース

### MuteUserMicrophone

特定ユーザーのマイクを無効化/再有効化します。
```C++
virtual int MuteUserMicrophone(const std::string& user_id, bool mute, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| mute | bool | 無効にするかどうか。 |
| callback | Callback | インターフェースコールバック。 |

### MuteAllUsersMicrophone

全ユーザーのマイクを無効化/再有効化します。
```C++
virtual int MuteAllUsersMicrophone(bool mute) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| mute | bool | 無効にするかどうか。 |

### MuteUserCamera

特定ユーザーのカメラを無効化/再有効化します。
```C++
virtual int MuteUserCamera(const std::string& user_id, bool mute, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| mute | bool | 無効にするかどうか。 |
| callback | Callback | インターフェースコールバック。 |

### MuteAllUsersCamera

全ユーザーのカメラを無効化/再有効化します。
```C++
virtual int MuteAllUsersCamera(bool mute) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| mute | bool | 無効にするかどうか。 |

### MuteChatRoom

チャットルームのミュートを開始/停止します。
```C++
virtual int MuteChatRoom(bool mute) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| mute | bool | 無効にするかどうか。 |

### KickOffUser

キャスターがキックアウトします。
```C++
virtual int KickOffUser(const std::string& user_id, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| callback | Callback | インターフェースコールバック。 |

### StartCallingRoll

キャスターが点呼を開始します。
```C++
virtual int StartCallingRoll() = 0;
```

### StopCallingRoll

キャスターが点呼を終了します。
```C++
virtual int StopCallingRoll() = 0;
```

### ReplyCallingRoll

メンバーがキャスターの点呼に応答します。
```C++
virtual int ReplyCallingRoll(Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| callback | Callback | インターフェースコールバック。 |

### SendSpeechInvitation

キャスターがメンバーの発言を要請します。
```C++
virtual int SendSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| callback | Callback | インターフェースコールバック。 |

### CancelSpeechInvitation

キャスターがメンバーへの発言要請をキャンセルします。
```C++
virtual int CancelSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| callback | Callback | インターフェースコールバック。 |

### ReplySpeechInvitation

メンバーがキャスターの発言要請に同意/を拒否します。
```C++
virtual int ReplySpeechInvitation(bool agree, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| agree | bool | 同意するかどうか。 |
| callback | Callback | インターフェースコールバック。 |

### SendSpeechApplication

メンバーが発言を要請します。
```C++
virtual int SendSpeechApplication(Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| callback | Callback | インターフェースコールバック。 |

### CancelSpeechApplication

メンバーが発言申請をキャンセルします。
```C++
virtual int CancelSpeechApplication(Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| callback | Callback | インターフェースコールバック。 |

### ReplySpeechApplication

キャスターがメンバーの発言申請に同意/を拒否します。
```C++
virtual int ReplySpeechApplication(const std::string& user_id, bool agree, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| callback | Callback | インターフェースコールバック。 |

### ForbidSpeechApplication

キャスターが発言申請を禁止します。
```C++
virtual int ForbidSpeechApplication(bool forbid) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| forbid | bool | 禁止するかどうか。|

### SendOffSpeaker

キャスターがメンバーに発言の停止を命令します。
```C++
virtual int SendOffSpeaker(const std::string& user_id, Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| callback | Callback | インターフェースコールバック。 |

### SendOffAllSpeakers

キャスターが全メンバーに発言の停止を命令します。
```C++
virtual int SendOffAllSpeakers(Callback callback) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| callback | Callback | インターフェースコールバック。 |

### ExitSpeechState

メンバーが発言を停止し、視聴者になります。
```C++
virtual int ExitSpeechState() = 0;
```

## 基本コンポーネントインターフェース

### GetDeviceManager

デバイス管理のオブジェクトポインタを取得します。
```C++
virtual liteav::ITXDeviceManager* GetDeviceManager() = 0;
```

### GetScreenShareManager

画面共有管理のオブジェクトポインタを取得します。
```C++
virtual IScreenShareManager* GetScreenShareManager() = 0;
```

## クラウドレコーディングインターフェース

### StartCloudRecord

クラウドレコーディングを開始します。
```C++
virtual int StartCloudRecord() = 0;
```

### StopCloudRecord

クラウドレコーディングを停止します。
```C++
virtual int StopCloudRecord() = 0;
```

## 美顔関連インターフェース関数

### SetBeautyStyle

美顔、美白、肌の色調補正効果のランクを設定します。
```C++
virtual int SetBeautyStyle(liteav::TRTCBeautyStyle style, uint32_t beauty_level,
        uint32_t whiteness_level, uint32_t ruddiness_level) = 0;
```

美顔管理では、次の機能を使用できます。
- 「美顔スタイル」を「スムース」または「ナチュラル」に設定します。「スムース」では、より強力な美肌補正効果が得られます。
- 「美顔レベル」を設定します。数値の範囲は0～9で、0はオフ、1～9までは数値が大きくなるほど効果が高くなります。
- 「美白レベル」を設定します。数値の範囲は0～9で、0はオフ、1～9までは数値が大きくなるほど効果が高くなります。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| style | liteav::TRTCBeautyStyle | 美顔スタイル。 |
| beauty_level | uint32_t | 美顔レベル。 |
| whiteness_level | uint32_t | 美白レベル。 |
| ruddiness_level | uint32_t | 肌色補正レベル。 |

## 関連設定インターフェース

### SetVideoQosPreference

ネットワークトラフィックコントロール関連パラメータを設定します。
```C++
virtual int SetVideoQosPreference(TUIVideoQosPreference preference) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| preference | TUIVideoQosPreference | ネットワークトラフィックコントロールポリシー。 |

## SDKバージョンインターフェースの取得

### GetSDKVersion

SDKバージョン情報を取得します。
```C++
virtual const char* GetSDKVersion() = 0;
```

## エラーイベントコールバック
### OnError

```C++
void OnError(int code, const std::string& message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code    | int    | エラーコード。|
| message | string | エラー情報。 |

## 基本イベントコールバック
### OnLogin

```C++
virtual void OnLogin(int code, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code    | int    | エラーコード。|
| message | string | ログイン情報またはログイン失敗のエラー情報。 |

### OnLogout

```C++
virtual void OnLogout(int code, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code    | int    | エラーコード。|
| message | string | エラー情報。 |

### OnCreateRoom

ルーム作成のコールバック。
```C++
virtual void OnCreateRoom(int code, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code    | int    | エラーコード。|
| message | string | エラー情報。 |

### OnDestroyRoom

ルーム解散のコールバック。
```C++
virtual void OnDestroyRoom(int code, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code    | int    | エラーコード。|
| message | string | エラー情報。 |

### OnEnterRoom

入室コールバック。
```C++
virtual void OnEnterRoom(int code, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code    | int    | エラーコード。|
| message | string | エラー情報。 |

### OnExitRoom

退室コールバック。
```C++
virtual void OnExitRoom(TUIExitRoomType type, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| type | TUIExitRoomType | 退室のタイプ。 |
| message | string | エラー情報。 |

### OnFirstVideoFrame

自身のローカルまたはリモートユーザーの最初のフレーム画面のレンダリングを開始します。
```C++
virtual void OnFirstVideoFrame(const std::string& user_id, const TUIStreamType stream_type) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| stream_type | TUIStreamType | ストリームのタイプ。 |

### OnUserVoiceVolume

ユーザー音量の大きさのコールバック。
```C++
virtual void OnUserVoiceVolume(const std::string& user_id, int volume)
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| volume | int | ユーザーの音量の大きさ、値の範囲0～100。 |

### OnRoomMasterChanged

キャスター変更のコールバック。
```C++
virtual void OnRoomMasterChanged(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |

## リモートユーザーコールバックイベント

### OnRemoteUserEnter

リモートユーザー入室コールバック。
```C++
virtual void OnRemoteUserEnter(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |

### OnRemoteUserLeave

リモートユーザー退室コールバック。
```C++
virtual void OnRemoteUserLeave(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |

### OnRemoteUserCameraAvailable

リモートユーザーが、カメラ、ビデオを起動しているかどうか。
```C++
virtual void OnRemoteUserCameraAvailable(const std::string& user_id, bool available) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| available | bool | true：ビデオストリームデータあり；false：ビデオストリームデータなし。 |

### OnRemoteUserScreenAvailable

リモートユーザーが画面共有を開始しているかどうか。
```C++
virtual void OnRemoteUserScreenAvailable(const std::string& user_id, bool available) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| available | bool | true：ビデオストリームデータあり；false：ビデオストリームデータなし。 |

### OnRemoteUserAudioAvailable

 リモートユーザーがマイクをオンにしているかどうか。
```C++
virtual void OnRemoteUserAudioAvailable(const std::string& user_id, bool available) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| available | bool | true：オーディオストリームデータあり、false：オーディオストリームデータなし。 |

### OnRemoteUserEnterSpeechState

リモートユーザーが発言を開始します。
```C++
virtual void OnRemoteUserEnterSpeechState(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |

### OnRemoteUserExitSpeechState

リモートユーザーが発言を終了します。
```C++
virtual void OnRemoteUserExitSpeechState(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |


## チャットルームメッセージイベントコールバック

### OnReceiveChatMessage

テキストメッセージの受信。
```C++
virtual void OnReceiveChatMessage(const std::string& user_id, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| message | string | テキストメッセージ。|

### OnReceiveCustomMessage

カスタムメッセージの受信。
```C++
virtual void OnReceiveCustomMessage(const std::string& user_id, const std::string& message) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| message | string | カスタムメッセージ。|

## フィールドコントロールメッセージコールバック

### OnReceiveSpeechInvitation

ユーザーがキャスターの発言要請を受信する場合のコールバック。
```C++
virtual void OnReceiveSpeechInvitation() = 0;
```

### OnReceiveInvitationCancelled

ユーザーがキャスターの発言要請キャンセルを受信する場合のコールバック。
```C++
virtual void OnReceiveInvitationCancelled() = 0;
```

### OnReceiveReplyToSpeechInvitation

キャスターがユーザーの発言要請への同意を受信する場合のコールバック。
```C++
virtual void OnReceiveReplyToSpeechInvitation(const std::string& user_id, bool agree) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |
| agree | bool | 同意するかどうか。|

### OnReceiveSpeechApplication

キャスターがユーザーの発言要請を受信する場合のコールバック。
```C++
virtual void OnReceiveSpeechApplication(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |

### OnSpeechApplicationCancelled

ユーザーが発言申請をキャンセルする場合のコールバック。
```C++
virtual void OnSpeechApplicationCancelled(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |

### OnReceiveReplyToSpeechApplication

キャスターが発言申請に同意する場合のコールバック。
```C++
virtual void OnReceiveReplyToSpeechApplication(bool agree) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| agree | bool | 同意するかどうか。 |

### OnSpeechApplicationForbidden

キャスターが発言申請を禁止する場合のコールバック。
```C++
virtual void OnSpeechApplicationForbidden(bool forbidden) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| forbidden | bool | 禁止するかどうか。|

### OnOrderedToExitSpeechState

メンバーが発言を停止するようリクエストされる場合のコールバック。
```C++
virtual void OnOrderedToExitSpeechState() = 0;
```

### OnCallingRollStarted

キャスターが点呼を開始し、メンバーが受信する場合のコールバック。
```C++
virtual void OnCallingRollStarted() = 0;
```

### OnCallingRollStopped

キャスターが点呼を終了し、メンバーが受信する場合のコールバック。
```C++
virtual void OnCallingRollStopped() = 0;
```

### OnMemberReplyCallingRoll

メンバーが点呼に応答し、キャスターが受信する場合のコールバック。
```C++
virtual void OnMemberReplyCallingRoll(const std::string& user_id) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| user_id | string | ユーザー ID。 |

### OnChatRoomMuted

キャスターがチャットルームのミュートを変更する場合のコールバック。
```C++
virtual void OnChatRoomMuted(bool muted) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| muted | bool | 無効にするかどうか。 |

### OnMicrophoneMuted

キャスターがマイクの無効化を設定する場合のコールバック。
```C++
virtual void OnMicrophoneMuted(bool muted) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| muted | bool | 無効にするかどうか。 |

### OnCameraMuted

キャスターがカメラの無効化を設定する場合のコールバック。
```C++
virtual void OnCameraMuted(bool muted) = 0;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| muted | bool | 無効にするかどうか。 |

## 統計および品質コールバック

### OnStatistics

技術指標統計のコールバック。
```C++
virtual void OnStatistics(const liteav::TRTCStatistics& statis) {}
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| statis | liteav::TRTCStatistics | 統計データ。 |

### OnNetworkQuality

ネットワーク状況のコールバック。
```C++
virtual void OnNetworkQuality(const liteav::TRTCQualityInfo& local_quality, liteav::TRTCQualityInfo* remote_quality,
        uint32_t remote_quality_count) {}
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| local_quality | liteav::TRTCQualityInfo | ローカルユーザー品質情報。 |
| remote_quality | liteav::TRTCQualityInfo* | リモートユーザー品質情報ポインタ。 |
| remote_quality_count | uint32_t | リモートユーザー数。 |

## スクリーンキャプチャのイベントコールバック

### OnScreenCaptureStarted

画面共有開始のコールバック。

```C++
virtual void OnScreenCaptureStarted() {}
```

### OnScreenCaptureStopped

画面共有停止のコールバック。

```C++
void OnScreenCaptureStopped(int reason) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | 停止の理由。0：ユーザーの自発的な停止。1：その他アプリケーションに占有されたことによる停止。 |

## ビデオレコーディングコールバック

### OnRecordError

レコーディングエラーのコールバック。

```C++
virtual void OnRecordError(TXLiteAVLocalRecordError error, const std::string& messgae) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| error | TXLiteAVLocalRecordError  | エラー情報。 |
| messgae | string  | エラー説明。 |

### OnRecordComplete

レコーディング完了のコールバック。

```C++
virtual void OnRecordComplete(const std::string& path) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| path | string  | エラーの説明。 |

### OnRecordProgress

レコーディング進捗のコールバック。

```C++
virtual void OnRecordProgress(int duration, int file_size) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| duration | int  | ファイルの長さ。 |
| file_size | int  | ファイルのサイズ。 |

## ローカルデバイステストコールバック

### OnTestSpeakerVolume

スピーカー音量の大きさのコールバック。

```C++
virtual void OnTestSpeakerVolume(uint32_t volume) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 音量の大きさ。 |

### OnTestMicrophoneVolume

マイク音量の大きさのコールバック。

```C++
virtual void OnTestMicrophoneVolume(uint32_t volume) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 音量の大きさ。 |

### OnAudioDeviceCaptureVolumeChanged

システムキャプチャ音量調節のコールバック。

```C++
virtual void OnAudioDeviceCaptureVolumeChanged(uint32_t volume, bool muted) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 音量の大きさ。 |
| muted | bool  | 無効にされるかどうか |

### OnAudioDevicePlayoutVolumeChanged

システム再生音量調節のコールバック。

```C++
virtual void OnAudioDevicePlayoutVolumeChanged(uint32_t volume, bool muted) {}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 音量の大きさ。 |
| muted | bool  | 無効にされるかどうか |
