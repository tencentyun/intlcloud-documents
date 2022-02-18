
TRTCMeetingは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。
- キャスターがミーティングルームを作成し、参加者はルームナンバーを入力した後にミーティングに参加します。
- 参加者の間で画面共有を行います。
- 各種のテキストメッセージとカスタムメッセージの送信をサポートします。

TRTCMeetingは、1つのオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実現プロセスは、[多人数ビデオミーティング(iOS)](https://intl.cloud.tencent.com/document/product/647/37284)をご参照ください。

- TRTC SDK： [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) を低遅延のビデオミーティングのコンポーネントとして使用します。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のMeetingRoomを利用して、ミーティング中のチャットルームの機能を実現します。

## TRTCMeeting API概要

### SDK基本関数

| API                                 | 説明                     |
| ----------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | シングルトンオブジェクトを取得します。           |
| [delegateQueue](#delegatequeue)   | イベントコールバックが設定されているスレッドです。 |
| [delegate](#delegate)             | イベントコールバックを設定します。           |
| [login](#login)                   | ログイン。                   |
| [logout](#logout)                 | ログアウト。                   |
| [setSelfProfile](#setselfprofile) | ユーザー情報を設定します。           |

### ミーティングルームに関するインターフェース関数

| API                                 | 説明                           |
| ----------------------------------- | ------------------------------ |
| [createMeeting](#createmeeting)   | ルームの作成（キャスターが呼び出し）。   |
| [destroyMeeting](#destroymeeting) | ルームの破棄（キャスターが呼び出し）。   |
| [enterMeeting](#entermeeting)     | 入室（参加者が呼び出し）。 |
| [leaveMeeting](#leavemeeting)     | 退室（参加者が呼び出し）。 |

### リモートユーザーのインターフェース

| API                                               | 説明                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| [getUserInfoList](#getuserinfolist)             | ルーム内の全メンバーのリストを取得します。enterMeeting()の成功後に呼び出しが有効となります。  |
| [getUserInfo](#getuserinfo)                     | ルーム内の指定メンバーの詳細情報を取得します。enterMeeting()の成功後に呼び出しが有効となります。 |
| [startRemoteView](#startremoteview)             | 指定メンバーのリモートビデオ画面を再生します。                                 |
| [stopRemoteView](#stopremoteview)               | リモートビデオ画面の再生を停止します。                                       |
| [setRemoteViewFillMode](#setremoteviewfillmode) | ユーザーIDと設定に基づくリモート画像のレンダリングモード。                         |
| [setRemoteViewRotation](#setremoteviewrotation) | リモート画像の時計回りの回転角度を設定します。                               |
| [muteRemoteAudio](#muteremoteaudio)             | リモートの指定参加者の音声をミュートにします。                                     |
| [muteRemoteVideoStream](#muteremotevideostream) | リモートの指定参加者のビデオストリームを非表示にします。                                   |

### ローカルのビデオ操作インターフェース

| API                                         | 説明                       |
| ------------------------------------------- | -------------------------- |
| [startCameraPreview](#startcamerapreview) | ローカルビデオのプレビュー画面を立ち上げます。   |
| [stopCameraPreview](#stopcamerapreview)   | ローカルのビデオキャプチャおよびプレビューを停止します。   |
| [switchCamera](#switchcamera)   | フロント/リアカメラを切り替えます。           |
| [setVideoResolution](#setvideoresolution) | 解像度の設定。               |
| [setVideoFps](#setvideofps)               | フレームレートの設定。                 |
| [setVideoBitrate](#setvideobitrate)       | ビットレートの設定。                 |
| [setLocalViewMirror](#setlocalviewmirror) | ローカル画面のミラーモードのプレビューを設定します。 |

### ローカルのオーディオ操作インターフェース

| API                                               | 説明                 |
| ------------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | マイクの集音開始。     |
| [stopMicrophone](#stopmicrophone)               | マイクの集音停止。     |
| [setAudioQuality](#setaudioquality)             | 音質の設定。           |
| [muteLocalAudio](#mutelocalaudio)               | ローカル音声のミュート起動。       |
| [setSpeaker](#setspeaker)                       | スピーカーの起動設定。     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | マイクの集音音量設定。 |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 再生音量の設定。       |
| [startFileDumping](#startfiledumping)           | 録音の開始。           |
| [stopFileDumping](#stopfiledumping)             | 録音の停止。           |
| [enableAudioEvaluation](#enableaudioevaluation) | 音量レベルリマインダを有効にします。   |

### スクリーンキャプチャのインターフェース

| API                                           | 説明           |
| --------------------------------------------- | -------------- |
| [startScreenCapture](#startscreencapture)   | 画面共有を開始。 |
| [stopScreenCapture](#stopscreencapture)     |画面キャプチャの停止。 |
| [pauseScreenCapture](#pausescreencapture)   | 画面共有の一時停止。 |
| [resumeScreenCapture](#resumescreencapture) | 画面共有のリカバー。 |

### 美顔フィルタに関するインターフェース関数

| API                                     | 説明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html)を取得します。 |

### 共有のインターフェース

| API                                                 | 説明              |
| --------------------------------------------------- | ----------------- |
| [getLiveBroadcastingURL](#getlivebroadcastingurl) | CDN共有のリンク先を取得します。 |

### メッセージ送信関連インターフェース関数

| API                                       | 説明                                                       |
| ----------------------------------------- | ---------------------------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | ルーム内でのテキストメッセージのブロードキャスト。通常、テキストによるチャットに使用します。                     |
| [sendRoomCustomMsg](#sendroomcustommsg) | ルーム内でカスタマイズ（シグナリング）したメッセージを送信します。 |

## TRTCMeetingDelegate API概要

### 一般的なイベントコールバック

| API                   | 説明       |
| --------------------- | ---------- |
| [onError](#onerror) | エラーのコールバック。 |

### ミーティングルームのイベントコールバック

| API                                         | 説明                   |
| ------------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | ミーティングルームが破棄された時のコールバック。 |
| [onNetworkQuality](#onnetworkquality)     | ネットワーク状態のコールバック。         |
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。     |

### 参加者入退室のイベントコールバック

| API                                   | 説明                 |
| ------------------------------------- | -------------------- |
| [onUserEnterRoom](#onuserenterroom) | 新しい参加者の入室の通知を受信します。 |
| [onUserLeaveRoom](#onuserleaveroom) | 参加者の退室の通知を受信します。   |

### 参加者の音声・ビデオのイベントコールバック

| API                                             | 説明                        |
| ----------------------------------------------- | --------------------------- |
| [onUserVideoAvailable](#onuservideoavailable) | 参加者のカメラ・オン/オフの通知。 |
| [onUserAudioAvailable](#onuseraudioavailable) | 参加者のマイク・オン/オフの通知。 |

### スクリーンキャプチャのイベントコールバック

| API                                                 | 説明          |
| --------------------------------------------------- | -------------- |
| [onScreenCaptureStarted](#onscreencapturestarted) | スクリーンキャプチャ開始の通知。 |
| [onScreenCapturePaused](#onscreencapturepaused)   | スクリーンキャプチャ一時停止のコールバック。 |
| [onScreenCaptureResumed](#onscreencaptureresumed) | スクリーンキャプチャ再開のコールバック。 |
| [onScreenCaptureStoped](#onscreencapturestoped)   | スクリーンキャプチャ停止のコールバック。 |

### メッセージイベントのコールバック

| API                                           | 説明             |
| --------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | テキストメッセージの受信。   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージの受信。 |

### スクリーンキャプチャのイベントコールバック

| API                                                 | 説明          |
| --------------------------------------------------- | -------------- |
| [onScreenCaptureStarted](#onscreencapturestarted) | スクリーンキャプチャ開始の通知。 |
| [onScreenCapturePaused](#onscreencapturepaused)   | スクリーンキャプチャ一時停止のコールバック。 |
| [onScreenCaptureResumed](#onscreencaptureresumed) | スクリーンキャプチャ再開のコールバック。 |
| [onScreenCaptureStoped](#onscreencapturestoped)   | スクリーンキャプチャ停止のコールバック。 |

## TRTCMeetingDef API概要

### TRTCMeetingUserInfoミーティングのユーザー情報

| 属性                                    | 説明                                   |
| --------------------------------------- | -------------------------------------- |
| [userId](#userid)       | ユーザーID。           |
| [userName](#username)   | ユーザー名（ニックネーム）。 |
| [avatarURL](#avatarurl) | ユーザープロフィール画像URL。      |
| [isVideoAvailable](#isvideoavailable) | ユーザーがビデオを立ち上げているかどうか。                   |
| [isAudioAvailable](#isaudioavailable) | ユーザーが音声を有効にしているかどうか。                     |
| [isMuteVideo](#ismutevideo)           | ユーザーのビデオを非表示にするかどうか（当該ユーザーのビデオを再生しない）。 |
| [isMuteAudio](#ismuteaudio)           | ユーザーの音声をミュートにするかどうか（当該ユーザーの音声を再生しない）。 |


## SDK基本関数

### sharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37284) シングルトンオブジェクトを取得します。

```objective-c
+ (instancetype)sharedInstance;
```

### delegateQueue

イベントコールバックが設定されているスレッドです。

```objective-c
- (void)setDelegateQueue:(dispatch_queue_t)delegateQueue
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ             | 意味                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| delegateQueue | dispatch_queue_t | TRTCMeetingの中の各種状態の通知のコールバックは、当該queueによって通知されます。setDelegateと混用しないでください。 |

### delegate

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37284)のイベントコールバック。TRTCMeetingDelegate を介して、[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37284)の各種ステータスの通知を取得できます。

### login

ログイン。

```objective-c
- (void)login:(UInt32)sdkAppId userId:(NSString *)userId userSig:(NSString *)userSig callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                                                         |
| -------- | ------------------- | ------------------------------------------------------------ |
| sdkAppId | UInt32              | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報の中でSDKAppIDを確認できます。 |
| userId   | NSString            | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。 |
| userSig  | NSString            | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | TRTCMeetingCallback | ログインのコールバック。成功時にcodeは0になります。                                  |

### logout

ログアウト。

```objective-c
- (void)logout:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                        |
| -------- | ------------------- | --------------------------- |
| callback | TRTCMeetingCallback | ログアウトのコールバック。成功時にcodeは0になります。 |

### setSelfProfile

個人情報の修正。

```objective-c
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(TRTCMeetingCallback)callback;
```

| パラメータ      | タイプ                | 意味                                      |
| --------- | ------------------- | ----------------------------------------- |
| userName  | NSString            | ユーザーのニックネーム。                                |
| avatarURL | NSString            | ユーザーのプロフィール画像。                                |
| callback  | TRTCMeetingCallback | ユーザー情報の設定結果のコールバック、成功時に codeは0になります。 |



## ミーティングルームに関するインターフェース関数

### createMeeting

ミーティングの作成（キャスターの呼び出し）。

```objective-c
- (void)createMeeting:(UInt32)roomId callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                                   |
| -------- | ------------------- | -------------------------------------- |
| roomId   | UInt32              | ルームIDは、ご自身でアサインし、一元管理する必要があります。 |
| callback | TRTCMeetingCallback | ルームの新規作成結果のコールバック。成功時にcodeは0になります。  |

キャスターの通常の呼び出しフローは以下のとおりです。 

1. 【キャスター】 `createMeeting()`を呼び出し、ミーティングを作成します。ミーティングルーム作成の成功の有無が、`TRTCMeetingCallback`でキャスターに通知されます。
2. 【キャスター】`startCameraPreview()`を呼び出し、カメラのプレビューを起動します。この時美顔パラメータを調整できます。 
3. 【キャスター】`startMicrophone()`を呼び出し、マイクキャプチャを起動します。

### destroyMeeting

ミーティングルームを破棄します（キャスターが呼び出し）。キャスターは、ミーティング作成後、この関数を呼び出してミーティングを破棄できます。

```objective-c
- (void)destroyMeeting:(UInt32)roomId callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                                   |
| -------- | ------------------- | -------------------------------------- |
| roomId   | UInt32              | ルームIDは、ご自身でアサインし、一元管理する必要があります。 |
| callback | TRTCMeetingCallback | ルームの新規作成結果のコールバック。成功時にcodeは0になります。  |

### enterMeeting

ミーティングに参加します（参加者が呼び出し）。

```objective-c
- (void)enterMeeting:(UInt32)roomId callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                                   |
| -------- | ------------------- | -------------------------------------- |
| roomId   | UInt32              | ルームIDは、ご自身でアサインし、一元管理する必要があります。 |
| callback | TRTCMeetingCallback | 入室結果のコールバック。成功時にcodeは0になります。  |

参加者がミーティングに参加する通常の呼び出しフローは以下のとおりです。 
1. 【参加者】`enterMeeting`を呼び出し、roomIdを渡すと、ミーティングルームに参加できます。
2. 【参加者】`startCameraPreview()`を呼び出して、カメラのプレビューを起動し、`startMicrophone()`を呼び出し、マイクキャプチャを起動します。
3. 【参加者】`onUserVideoAvailable`のイベントを受信します。`startRemoteView(userId)`を呼び出し、メンバーのuserIdを渡して再生を開始します
   
### leaveMeeting

ミーティングから退出します（参加者が呼び出し）。

```objective-c
- (void)leaveMeeting:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                                  |
| -------- | ------------------- | ------------------------------------- |
| callback | TRTCMeetingCallback | 退室結果のコールバック。成功時にcodeは0になります。 |



## リモートユーザーに関するインターフェース

### getUserInfoList

ルーム内の全メンバーのリストを取得します。enterMeeting()の成功後に呼び出しが有効となります。

```objective-c
- (void)getUserInfoList:(TRTCMeetingUserListCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                        | 意味               |
| -------- | --------------------------- | ------------------ |
| callback | TRTCMeetingUserListCallback | ユーザーの詳細情報のコールバック。 |

### getUserInfo

ルーム内の指定メンバーの詳細情報を取得します。enterMeeting()の成功後に呼び出しが有効となります。

```objective-c
- (void)getUserInfo:(NSString *)userId callback:(TRTCMeetingUserListCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                        | 意味               |
| -------- | --------------------------- | ----------- |
| userId | NSString | リモートのユーザーID。                   |
| callback | TRTCMeetingUserListCallback | ユーザーの詳細情報のコールバック。 |

### startRemoteView

指定メンバーのリモートビデオ画面を再生します。`onUserVideoAvailable()`がtrueのコールバックの時、このインターフェースを呼び出します。

```objective-c
- (void)startRemoteView:(NSString *)userId view:(UIView *)view callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                       |
| -------- | ------------------- | -------------------------- |
| userId   | NSString            | 視聴が必要なユーザーのID。         |
| view     | UIView              | ビデオ画像をロードするviewウィジェット。 |
| callback | TRTCMeetingCallback | 操作のコールバック。                 |

### stopRemoteView

リモートのビデオ画面のレンダリングを停止します。 `onUserVideoAvailable()`がfalseのコールバック時、このインターフェースを呼び出します。

```objective-c
- (void)stopRemoteView:(NSString *)userId callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味             |
| -------- | ------------------- | ---------------- |
| userId   | NSString            | 再生停止が必要なユーザーのID。 |
| callback | TRTCMeetingCallback | 操作のコールバック。       |

### setRemoteViewFillMode

ユーザーidと設定に基づくリモート画像のレンダリングモード

```objective-c
- (void)setRemoteViewFillMode:(NSString *)userId fillMode:(TRTCVideoFillMode)fillMode;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ              | 意味                                                         |
| -------- | ----------------- | ------------------------------------------------------------ |
| userId   | NSString          | ユーザーID。                                                    |
| fillMode | TRTCVideoFillMode | FILLまたはFITモード。デフォルト値：FILL（TRTCVideoFillMode_Fill）。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff)をご参照ください。 |

### setRemoteViewRotation

リモート画像の時計回りの回転角度を設定します

```objective-c
- (void)setRemoteViewRotation:(NSString *)userId rotation:(NSInteger)rotation;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ      | 意味                                                         |
| -------- | --------- | ------------------------------------------------------------ |
| userId   | NSString  | 相手側のユーザーID。                                              |
| rotation | NSInteger | 時計回りの回転角度。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90)をご参照ください。 |

### muteRemoteAudio

リモートの音声をミュートにします。

```objective-c
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味                              |
| ------ | -------- | --------------------------------- |
| userId | NSString | リモートのユーザーID。                   |
| mute   | BOOL     | true：ミュート起動、false：ミュート停止。 |

### muteRemoteVideoStream

指定参加者のビデオストリームを非表示にします。

```objective-c
- (void)muteRemoteVideoStream:(NSString *)userId mute:(BOOL)mute;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味                          |
| ------ | -------- | ----------------------------- |
| userId | NSString | リモートのユーザーID。               |
| mute   | BOOL     | true：非表示；false：非表示解除 |



## ローカルのビデオ操作インターフェース

### startCameraPreview

ローカルビデオのプレビュー画面を立ち上げます。

```objective-c
- (void)startCameraPreview:(BOOL)isFront view:(UIView *)view;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                                  |
| ------- | ------ | ------------------------------------- |
| isFront | BOOL   | true：フロントカメラ；false：リアカメラ |
| view    | UIView | ビデオ画像をロードするウィジェット。                  |

### stopCameraPreview

ローカルのビデオキャプチャおよびプレビューを停止します。

```objective-c
- (void)stopCameraPreview;
```

### switchCamera

フロント/リアカメラを切り替えます。

```objective-c
- (void)switchCamera:(BOOL)isFront;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ | 意味                                                  |
| ------- | ---- | ----------------------------------------------------- |
| isFront | BOOL | 前後カメラを切り替えます。true：フロントカメラ；false：リアカメラ |

### setVideoResolution

解像度の設定。

```objective-c
- (void)setVideoResolution:(TRTCVideoResolution)resolution;
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                | 意味                                                         |
| ---------- | ------------------- | ------------------------------------------------------------ |
| resolution | TRTCVideoResolution | ビデオの解像度。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5)をご参照ください。 |

### setVideoFps

フレームレートの設定。

```objective-c
- (void)setVideoFps:(int)fps;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味           |
| ---- | ---- | -------------- |
| fps  | int  | ビデオキャプチャのフレームレート。 |

>? 【推奨する値】 15fpsまたは20fps。5fps以下ではラグ感が顕著。10fps以下では軽微なラグ感があります。20fps以上は高すぎて浪費になります（映画のフレームレートは24fps）。

### setVideoBitrate

ビットレートの設定。

```objective-c
- (void)setVideoBitrate:(int)bitrate;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ | 意味                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| bitrate | int  | ビットレート。SDKは、目標ビットレートに応じてエンコードを行い、ネットワークの状態が良くない場合のみ、ビデオビットレートを動的に引き下げます。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454)をご参照ください。 |

>?【推奨する値】TRTCVideoResolutionの各クラスに注記する最適ビットレートをご参照ください。これをもとにより高いレートに適宜調整することも可能です。例えば、TRTC_VIDEO_RESOLUTION_1280_720に対応する目標ビットレートが1200kbpsであるならば、設定を1500kbpsにし、より鮮明な画像を得ることができます

### setLocalViewMirror

ローカル画面のミラーモードのプレビューを設定します。

```objective-c
- (void)setLocalViewMirror:(TRTCLocalVideoMirrorType)type;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ                     | 意味                                                         |
| ---- | ------------------------ | ------------------------------------------------------------ |
| type | TRTCLocalVideoMirrorType | ミラーモード。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454)をご参照ください。 |



## ローカルのオーディオ操作インターフェース

### startMicrophone

マイクの集音開始。

```objective-c
- (void)startMicrophone;
```

### stopMicrophone

マイクの集音停止。

```objective-c
- (void)stopMicrophone;
```

### setAudioQuality

音質の設定。

```objective-c
- (void)setAudioQuality:(TRTCAudioQuality)quality;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ             | 意味                                                         |
| ------- | ---------------- | ------------------------------------------------------------ |
| quality | TRTCAudioQuality | 音質。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53)をご参照ください。 |

### muteLocalAudio

ローカルの音声のミュート/ミュート取り消し。

```objective-c
- (void)muteLocalAudio:(BOOL)mute;
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味                                                         |
| ---- | ---- | ------------------------------------------------------------ |
| mute | BOOL | ミュート/ミュート取り消し。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9)をご参照ください。 |

### setSpeaker

スピーカーの起動設定。

```objective-c
- (void)setSpeaker:(BOOL)useSpeaker;
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ | 意味                         |
| ---------- | ---- | ---------------------------- |
| useSpeaker | BOOL | true：スピーカー、false：ヘッドホン。 |

### setAudioCaptureVolume

マイクの集音音量設定。

```objective-c
- (void)setAudioCaptureVolume:(NSInteger)volume;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ      | 意味                        |
| ------ | --------- | --------------------------- |
| volume | NSInteger | 集音音量、0-100、 デフォルト100。 |

### setAudioPlayoutVolume

再生音量の設定。

```objective-c
- (void)setAudioPlayoutVolume:(NSInteger)volume;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ      | 意味                        |
| ------ | --------- | --------------------------- |
| volume | NSInteger | 再生音量、0-100、 デフォルト100。 |

### startFileDumping

録音の開始。

```objective-c
- (void)startFileDumping:(TRTCAudioRecordingParams *)params;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ                     | 意味                                                         |
| ------ | ------------------------ | ------------------------------------------------------------ |
| params | TRTCAudioRecordingParams | 録音パラメータ。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioRecordingParams)をご参照ください。 |

>? この方法で呼び出した後、 SDKは通話プロセスの中のすべての音声（ローカル音声、リモート音声、BGMなど）を1つのファイルにレコーディングします。ルームに参加しているか否かにかかわらず、このインターフェースを呼び出せば有効となります。exitMeetingを呼び出した時に録音中であれば、録音は自動的に停止します。

### stopFileDumping

録音の停止。

```objective-c
- (void)stopFileDumping;
```

### enableAudioEvaluation

音量レベルリマインダを有効にします。

```objective-c
- (void)enableAudioEvaluation:(BOOL)enable;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                      |
| ------ | ---- | ------------------------- |
| enable | BOOL | true：オン；false：オフ |

>? 有効化すると、onUserVolumeUpdateの中でSDKの音量のボリュームに対する評価を取得できます。



## スクリーンキャプチャのインターフェース

### startScreenCapture

画面共有を開始。

```objective-c
- (void)startScreenCapture:(TRTCVideoEncParam *)params;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ              | 意味                                                         |
| ------ | ----------------- | ------------------------------------------------------------ |
| params | TRTCCloudDef.TRTCVideoEncParam | 画面共有時のエンコードパラメータを設定します。上記の推奨設定を採用することをお勧めします。encParamsにnilを指定した場合、startScreenCaptureを呼び出す前のエンコードパラメータ設定が使用されます。 |

>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff)をご参照ください。

### stopScreenCapture

画面キャプチャの停止。

```objective-c
- (int)stopScreenCapture
```

### pauseScreenCapture

画面共有の一時停止。

```objective-c
- (int)pauseScreenCapture
```

### resumeScreenCapture

画面共有のリカバー。

```objective-c
- (int)resumeScreenCapture
```



## 共有のインターフェース

### getLiveBroadcastingURL

CDN共有のリンク先を取得します。

```objective-c
- (NSString *)getLiveBroadcastingURL;
```

戻り値は下表に示すとおりです。

| 戻り値 | タイプ     | 意味          |
| ------ | -------- | ------------- |
| url    | NSString | CDN共有のリンク先。 |



## 美顔フィルタに関するインターフェース関数

### getBeautyManager

美顔管理オブジェクト[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html)を取得します。

```objective-c
- (TXBeautyManager *)getBeautyManager;
```

美顔管理では、次の機能を使用できます。

- 「美顔のスタイル」、「美白」、「肌色補正（血色・つや感）」、「デカ眼」、「顔痩せ」、「V顔」、「下あご」、「面長補正」、「小鼻」、「キラキラ目」、「白い歯」、「目の弛み除去」、「シワ除去」、「ほうれい線除去」などの美容効果を設定します。
- 「髪の生え際」、「眼と眼の距離」、「眼角度」、「唇の形」、「鼻翼」、「鼻の位置」、「唇の厚さ」、「顔の形」を調整します。
- 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
- メイクアップを追加します。
- ジェスチャー認識を行います。



## メッセージ送信関連インターフェース関数

### sendRoomTextMsg

ルーム内でテキストメッセージを発信します。

```objective-c
- (void)sendRoomTextMsg:(NSString *)message callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味           |
| -------- | ------------------- | -------------- |
| message  | NSString            | テキストメッセージ。     |
| callback | TRTCMeetingCallback | 発信結果のコールバック。 |

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。

```objective-c
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(TRTCMeetingCallback)callback;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                                               |
| -------- | ------------------- | -------------------------------------------------- |
| cmd      | NSString            | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | NSString            | テキストメッセージ。                                         |
| callback | TRTCMeetingCallback | 発信結果のコールバック。                                     |



## TRTCMeetingDelegateイベントコールバック

## 一般的なイベントコールバック

### onError

>? SDKのリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```objective-c
- (void)onError:(NSInteger)code message:(NSString* _Nullable)message;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ      | 意味       |
| ------- | --------- | ---------- |
| code    | NSInteger | エラーコード。   |
| message | NSString  | エラー情報。 |



## ルームイベントのコールバック

### onRoomDestroy

ルームが破棄された時のコールバック。キャスターがルームを退出する時、ルーム内の全ユーザーがこの通知を受信します。

```objective-c
- (void)onRoomDestroy:(NSString *)roomId;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味      |
| ------ | -------- | --------- |
| roomId | NSString | ルーム ID。 |

### onNetworkQuality

ネットワーク状態のコールバック。

```objective-c
- (void)onNetworkQuality:(TRTCQualityInfo *)localQuality
           remoteQuality:(NSArray<TRTCQualityInfo*> *)remoteQuality;
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                       | 意味           |
| ------------- | -------------------------- | -------------- |
| localQuality  | TRTCQualityInfo            | アップストリームネットワークの品質。 |
| remoteQuality | NSArray&lt;TRTCQualityInfo *&gt; | ダウンストリームネットワークの品質。 |

>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28)をご参照ください。

### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します。

```objective-c
- (void)onUserVolumeUpdate:(NSString *)userId volume:(NSInteger)volume;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ      | 意味                  |
| ------ | --------- | --------------------- |
| userId | NSString  | ユーザーID 。           |
| volume | NSInteger | 音量の大きさ。値：0～100。 |



## 参加者入退室のイベントコールバック

### onUserEnterRoom

新しい参加者の入室の通知を受信します。

```objective-c
- (void)onUserEnterRoom:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味            |
| ------ | -------- | --------------- |
| userId | NSString | ルームの新たな参加者のユーザーID。 |


### onUserLeaveRoom

参加者の退室の通知を受信します。

```objective-c
- (void)onUserLeaveRoom:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味          |
| ------ | -------- | ------------- |
| userId | NSString | 退室する参加者のユーザーID |



## 参加者の音声・ビデオのイベントコールバック

### onUserVideoAvailable

参加者のカメラ・オン/オフの通知。

```objective-c
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ     | 意味                                          |
| --------- | -------- | --------------------------------------------- |
| userId    | NSString | ユーザーID。                                    |
| available | BOOL     | true：ユーザーがカメラをオンにします。false：ユーザーがカメラをオフにします。 |

### onUserAudioAvailable

参加者のマイク・オン/オフの通知。

```objective-c
- (void)onUserAudioAvailable:(NSString *)userId available:(BOOL)available;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ     | 意味                                          |
| --------- | -------- | --------------------------------------------- |
| userId    | NSString | ユーザーID。                                    |
| available | BOOL     | true：ユーザーがマイクをオンにします。false：ユーザーがマイクをオフにします。 |

   

## メッセージイベントのコールバック

### onRecvRoomTextMsg

テキストメッセージの受信。

```objective-c
- (void)onRecvRoomTextMsg:(NSString* _Nullable)message userInfo:(TRTCMeetingUserInfo *)userInfo;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ                | 意味             |
| ------- | ------------------- | ---------------- |
| message | NSString            | テキストメッセージ。       |
| userInfo | TRTCMeetingUserInfo | 送信者のユーザー情報。 |

### onRecvRoomCustomMsg

カスタムメッセージの受信。

```objective-c
- (void)onRecvRoomCustomMsg:(NSString* _Nullable)cmd message:(NSString* _Nullable)message userInfo:(TRTCMeetingUserInfo *)userInfo;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                | 意味                                               |
| -------- | ------------------- | -------------------------------------------------- |
| cmd      | NSString            | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message  | NSString            | テキストメッセージ。                                         |
| userInfo | TRTCMeetingUserInfo | 送信者のユーザー情報。                                   |



## スクリーンキャプチャのイベントコールバック

### onScreenCaptureStarted

スクリーンキャプチャ開始の通知。

```objective-c
- (void)onScreenCaptureStarted;
```

### onScreenCapturePaused

スクリーンキャプチャ一時停止の通知。

```objective-c
- (void)onScreenCapturePaused:(int)reason;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | 一時停止の理由。0：ユーザーの自発的な一時停止。1：スクリーンウィンドウが視認できないことによる一時停止。 |

### onScreenCaptureResumed

スクリーンキャプチャ再開の通知。

```objective-c
- (void)onScreenCaptureResumed:(int)reason;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                                       |
| ------ | ---- | ---------------------------------------------------------- |
| reason | int  | 再開の理由。0：ユーザーの自発的な再開。1：スクリーンウィンドウの視認性回復による共有の回復。 |

### onScreenCaptureStoped

スクリーンキャプチャ停止の通知。

```objective-c
- (void)onScreenCaptureStoped:(int)reason;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                                 |
| ------ | ---- | ---------------------------------------------------- |
| reason | int  | 停止の理由。0：ユーザーの自発的な停止。1：スクリーンウィンドウが閉じられたことによる停止。 |



## TRTCMeetingDef に関する属性

## TRTCMeetingUserInfo

### userId

ユーザーID。

```objective-c
@property (nonatomic, strong) NSString *userId;
```

### userName

ユーザー名（ニックネーム）。

```objective-c
@property (nonatomic, strong) NSString *userName;
```

### avatarURL

ユーザープロフィール画像URL。

```objective-c
@property (nonatomic, strong) NSString *avatarURL;
```

### roomId

ルームナンバー。

```objective-c
@property (nonatomic, assign) UInt32 roomId;
```

### isVideoAvailable

ユーザーがビデオを立ち上げているかどうか。

```objective-c
@property (nonatomic, assign) BOOL isVideoAvailable;
```

### isAudioAvailable

ユーザーが音声を有効にしているかどうか。

```objective-c
@property (nonatomic, assign) BOOL isAudioAvailable;
```

### isMuteVideo

ユーザーのビデオを非表示にするかどうか（当該ユーザーのビデオを再生しない）。

```objective-c
@property (nonatomic, assign) BOOL isMuteVideo;
```

### isMuteAudio

ユーザーの音声をミュートにするかどうか（当該ユーザーの音声を再生しない）。

```objective-c
@property (nonatomic, assign) BOOL isMuteAudio;
```

