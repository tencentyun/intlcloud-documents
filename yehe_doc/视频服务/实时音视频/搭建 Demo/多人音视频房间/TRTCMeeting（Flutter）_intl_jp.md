TRTCMeetingは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。
- キャスターがミーティングルームを作成し、参加者はルームナンバーを入力した後にミーティングに参加します。
- 参加者の間で画面共有を行います。
- 各種のテキストメッセージとカスタムメッセージの送信をサポートします。

TRTCMeetingは、1つのオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実現プロセスは、[多人数オーディオビデオルーム（Flutter）](https://intl.cloud.tencent.com/document/product/647/41945)をご参照ください。
- TRTC SDK： [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) を低遅延のビデオミーティングのコンポーネントとして使用します。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のMeetingRoomを利用して、ミーティング中のチャットルームの機能を実現します。

[](id:TRTCMeeting)

## TRTCMeeting API概要
### SDK基本インターフェース

| API          | 説明         |
|-----|-----|
| [sharedInstance](#sharedinstance) | シングルトンオブジェクトを取得します。|
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを破棄します。|
| [registerListener](#registerlistener) | イベント監視を設定します。|
| [unRegisterListener](#unregisterlistener) | イベント監視を破棄します。|
| [login](#login) | ログイン。|
| [logout](#logout)      | ログアウト。|
| [setSelfProfile](#setselfprofile) | 個人情報を修正します。|

### ミーティングルームに関するインターフェース

| API          | 説明         |
|-----|-----|
| [createMeeting](#createmeeting) | ルームの作成（キャスターが呼び出し）。|
| [destroyMeeting](#destroymeeting) | ルームの破棄（キャスターが呼び出し）。|
| [enterMeeting](#entermeeting) | 入室（参加者が呼び出し）。|
| [leaveMeeting](#leavemeeting) | 退室（参加者が呼び出し）。|
| [getUserInfoList](#getuserinfolist) | ルーム内の全メンバーのリストを取得します。enterMeeting()成功後に呼び出しが有効となります。|
| [getUserInfo](#getuserinfo) | ルーム内の指定メンバーの詳細情報を取得します。enterMeeting()成功後に呼び出しが有効となります。|

### リモートユーザーに関するインターフェース

| API          | 説明         |
|-----|-----|
| [startRemoteView](#startremoteview) | 指定メンバーのリモートビデオ画面を再生します。|
| [stopRemoteView](#stopremoteview) | 指定メンバーのリモートビデオ画面の再生を停止します。|
| [setRemoteViewParam](#setremoteviewparam) | 指定メンバーのリモート画像のレンダリングパラメータを設定します。|
| [muteRemoteAudio](#muteremoteaudio) | 指定メンバーのリモート音声をミュート/ミュート取り消しにします。|
| [muteAllRemoteAudio](#muteallremoteaudio) | 全メンバーのリモート音声をミュート/ミュート取り消しにします。|
| [muteRemoteVideoStream](#muteremotevideostream) | 指定メンバーのリモートビデオを一時停止/再開します。|
| [muteAllRemoteVideoStream](#muteallremotevideostream) | 全メンバーのリモートビデオストリームを一時停止/再開します。|

### ローカルのビデオ操作インターフェース

| API          | 説明         |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | ローカルビデオのプレビュー画面を立ち上げます。|
| [stopCameraPreview](#stopcamerapreview) | ローカルのビデオキャプチャおよびプレビューを停止します。|
| [switchCamera](#switchcamera) | フロント/リアカメラを切り替えます。 |
| [setVideoEncoderParam](#setvideoencoderparam) | ビデオエンコーダ関連パラメータを設定します。|
| [setLocalViewMirror](#setlocalviewmirror) | ローカル画面のミラーモードのプレビューを設定します。|

### ローカルの音声操作インターフェース

| API          | 説明         |
|-----|-----|
| [startMicrophone](#startmicrophone)     | マイクの集音開始。|
| [stopMicrophone](#stopmicrophone)       | マイクの集音停止。|
| [muteLocalAudio](#mutelocalaudio)       | ローカル音声のミュート起動/停止。|
| [setSpeaker](#setspeaker) | スピーカーまたはヘッドホン起動の設定。|
| [setAudioCaptureVolume](#setaudiocapturevolume) | マイクの集音音量設定。|
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 再生音量の設定。|
| [startAudioRecording](#startaudiorecording) | 録音の開始。|
| [stopAudioRecording](#stopaudiorecording) | 録音の停止。|
| [enableAudioVolumeEvaluation](#enableaudiovolumeevaluation) | 音声レベルリマインダを有効にします。|

### スクリーンキャプチャのインターフェース

| API          | 説明         |
|-----|-----|
| [startScreenCapture](#startscreencapture) | 画面共有を開始。|
| [stopScreenCapture](#stopscreencapture) | 画面キャプチャの停止。|
| [pauseScreenCapture](#pausescreencapture) | スクリーンキャプチャの一時停止。|
| [resumeScreenCapture](#resumescreencapture) | スクリーンキャプチャの再開。|

### 管理オブジェクト取得に関するインターフェース

| API          | 説明         |
|-----|-----|
| [getDeviceManager](#getdevicemanager) | デバイス管理オブジェクト[TXDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html)を取得します。|
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト[TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html)を取得します。|

### メッセージ送信関連インターフェース

| API          | 説明         |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | ミーティング中にテキストメッセージをブロードキャストします。通常、チャットに使用します。|
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズしたテキストメッセージを送信します。|

[](id:TRTCLiveRoomDelegate)
## TRTCLiveRoomDelegate API概要
### 一般的なイベントコールバック

| API          | 説明         |
|-----|-----|
| [onError](#onerror) | エラーのコールバック。|
| [onWarning](#onwarning) | 警告のコールバック。|
| [onKickedOffline](#onkickedoffline) | 他のユーザーが同じアカウントでログインすると、キックアウトされてオフラインになります。|

### ミーティングルームのイベントコールバック

| API          | 説明         |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | ミーティングルームが破棄された時のコールバック。|
| [onNetworkQuality](#onnetworkquality) | ネットワーク状態のコールバック。|
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。|

### 参加者入退室のイベントコールバック

| API          | 説明         |
|-----|-----|
| [onEnterRoom](#onenterroom) | ローカルの入室のコールバック。|
| [onLeaveRoom](#onleaveroom) | ローカルの退室のコールバック。|
| [onUserEnterRoom](#onuserenterroom) | 新しい参加者の入室のコールバック。|
| [onUserLeaveRoom](#onuserleaveroom) | 参加者の退出のコールバック。|

### 参加者の音声・ビデオのイベントコールバック

| API          | 説明         |
|-----|-----|
| [onUserAudioAvailable](#onuseraudioavailable) | 参加者がマイクを起動/停止したときのコールバック。|
| [onUserVideoAvailable](#onuservideoavailable) | 参加者がカメラを起動/停止したときのコールバック。|
| [onUserSubStreamAvailable](#onusersubstreamavailable) | 参加者がサブチャンネル画面を起動/停止したときのコールバック。|

### メッセージイベントのコールバック

| API          | 説明         |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | テキストメッセージ受信のコールバック。|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージ受信のコールバック。|

### スクリーンキャプチャのイベントコールバック

| API          | 説明         |
|-----|-----|
| [onScreenCaptureStarted](#onscreencapturestarted) | スクリーンキャプチャ開始のコールバック。|
| [onScreenCapturePaused](#onscreencapturepaused) | スクリーンキャプチャ一時停止のコールバック。|
| [onScreenCaptureResumed](#onscreencaptureresumed) | スクリーンキャプチャ再開のコールバック。|
| [onScreenCaptureStoped](#onscreencapturestoped) | スクリーンキャプチャ停止のコールバック。|

## SDK基本インターフェース
### sharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945)シングルトンオブジェクトを取得します。
```dart
static Future<TRTCMeeting> sharedInstance();
```

### destroySharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945)シングルトンオブジェクトを破棄します。
```dart
static void destroySharedInstance();
```
>? インスタンスを破棄すると、外部キャッシュのTRTCMeetingインスタンスは再利用できなくなります。あらためて[sharedInstance](#sharedinstance)を呼び出し、新しいインスタンスを取得する必要があります。

### registerListener

イベント監視を設定します。TRTCMeetingDelegateを介して、[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945)の各種ステータスの通知を取得できます。
```dart
void registerListener(MeetingListenerFunc func);
```
>? funcはTRTCMeetingのプロキシコールバックです。

### unRegisterListener

イベント監視を破棄します。
```dart
void unRegisterListener(MeetingListenerFunc func);
```

### login

ログイン
```dart
Future<ActionCallback> login(int sdkAppId, String userId, String userSig);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| sdkAppId | int | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報の中でSDKAppIDを確認できます。|
| userId | String | 現在のユーザーのID。文字列タイプ。アルファベット（a-z および A-Z）、数字（0-9）、ハイフン（-）、アンダーバー（\_）のみ使用できます。|
| userSig | String | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 [UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。|

### logout

ログアウト。
```dart
Future<ActionCallback> logout();
```

### setSelfProfile

個人情報の修正。
```dart
Future<ActionCallback> setSelfProfile(String userName, String avatarURL);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userName | String | ユーザーニックネーム。|
| avatarURL | String | ユーザープロフィール画像のアドレス。|

## ミーティングルーム関連インターフェース
### createMeeting

ミーティングの作成（キャスターの呼び出し）。
```dart
Future<ActionCallback> createMeeting(int roomId);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| roomId | int | ミーティングルームID。ご自身でアサインし、一括管理する必要があります。|

キャスターの通常の呼び出しフローは以下のとおりです。 
1. 【キャスター】`createMeeting()`を呼び出し、`roomId`を渡してミーティングを作成します。ミーティングルーム作成の成功の有無が`ActionCallback`によってキャスターに通知されます。 
2. 【キャスター】`startCameraPreview()`を呼び出し、カメラのプレビューを起動します。この時美顔パラメータを調整できます。
3. 【キャスター】`startMicrophone()`を呼び出し、マイクキャプチャを起動します。

### destroyMeeting

ミーティングルームを破棄します（キャスターが呼び出し）。キャスターは、ミーティング作成後、この関数を呼び出してミーティングを破棄できます。
```dart
Future<ActionCallback> destroyMeeting(int roomId);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| roomId | int | ミーティングルームID。ご自身でアサインし、一括管理する必要があります。|

### enterMeeting

ミーティングルームに参加します（参加者が呼び出し）。
```dart
Future<ActionCallback> enterMeeting(int roomId);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| roomId | int | ミーティングルームID。|

参加者がミーティングに参加する通常の呼び出しフローは以下のとおりです。 
1. 【参加者】`enterMeeting()`を呼び出し、`roomId`を渡せばミーティングルームに入れます。
2. 【参加者】`startCameraPreview()`を呼び出して、カメラのプレビューを起動し、`startMicrophone()`を呼び出し、マイクキャプチャを起動します。
3. 【参加者】`onUserVideoAvailable`のイベントを受信します。`startRemoteView()`を呼び出し、メンバーのuserIdを渡して再生を開始します

### leaveMeeting

ミーティングルームから退出します（参加者が呼び出し）。
```dart
Future<ActionCallback> leaveMeeting();
```

### getUserInfoList

ルーム内の全メンバーのリストを取得します。enterMeeting()成功後に呼び出しが有効となります。
```dart
Future<UserListCallback> getUserInfoList(List<String> userIdList);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userIdList | List&lt;String&gt; | 取得する必要があるuserId リスト。|

### getUserInfo

ルーム内の指定メンバーの詳細情報を取得します。enterMeeting()成功後に呼び出しが有効となります。
```dart
Future<UserListCallback> getUserInfo(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 指定メンバーのID。|

## リモートユーザーに関するインターフェース
### startRemoteView

指定メンバーのリモートビデオ画面を再生します。
```dart
Future<void> startRemoteView(String userId, int streamType, int viewId);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 指定メンバーのID。|
| streamType | int | 視聴したいビデオストリームのタイプ。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19)をご参照ください。 |
| viewId | int | TRTCCloudVideoViewが発行するviewId。|

### stopRemoteView

指定メンバーのリモートビデオ画面の再生を停止します。
```dart
Future<void> stopRemoteView(String userId, int streamType);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 指定メンバーのID。|
| streamType | int | 視聴したいビデオストリームのタイプ。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19)をご参照ください。|

### setRemoteViewParam

指定メンバーのリモート画像のレンダリングパラメータを設定します。
```dart
Future<void> setRemoteViewParam(String userId, int streamType,
  {int fillMode, int rotation, int mirrorType});
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 指定メンバーのID。|
| streamType | int | 視聴したいビデオストリームのタイプ。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19)をご参照ください。|
| fillMode | int | 画像レンダリングモード。FILL（デフォルト）またはFITモード。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ae697c0f66077568d33d0996064776b50)をご参照ください。|
| rotation | int | 画像の時計回りの回転角度。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ab3d380890a5e0b7b6a29bc5d0e58f8e8)をご参照ください。|
| mirrorType | int | イメージモード。詳細については、 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ae5d847e0006bf2cd689b1116721109ca)をご参照ください。|

### muteRemoteAudio

指定メンバーのリモート音声をミュート/ミュート取り消しにします。
```dart
Future<void> muteRemoteAudio(String userId, bool mute);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 指定メンバーのID。|
| mute | boolean | true：ミュート、false：ミュート停止。|

### muteAllRemoteAudio

全メンバーのリモート音声をミュート/ミュート取り消しにします。
```dart
Future<void> muteAllRemoteAudio(bool mute);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| mute | boolean | true：ミュート、false：ミュート停止。|

### muteRemoteVideoStream

指定メンバーのリモートビデオを一時停止/再開します。
```dart
Future<void> muteRemoteVideoStream(String userId, bool mute);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 指定メンバーのID。|
| mute | boolean | true：一時停止、false：再開。|

### muteAllRemoteVideoStream

全メンバーのリモートビデオストリームを一時停止/再開します。
```dart
Future<void> muteAllRemoteVideoStream(bool mute);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| mute | boolean | true：一時停止、false：再開。|

## ローカルのビデオ操作インターフェース
### startCameraPreview

ローカルビデオのプレビュー画面を立ち上げます。
```dart
Future<void> startCameraPreview(bool isFront, int viewId);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| isFront | boolean | true：フロントカメラ、false：リアカメラ。|
| viewId | int | TRTCCloudVideoViewが発行するviewId。|

### stopCameraPreview

ローカルのビデオキャプチャおよびプレビューを停止します。
```dart
Future<void> stopCameraPreview();
```

### switchCamera

フロント/リアカメラを切り替えます。
```dart
Future<void> switchCamera(bool isFront);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| isFront | boolean | true：フロントカメラ、false：リアカメラ。|

### setVideoEncoderParam

ビデオエンコーダ関連パラメータを設定します。
```dart
Future<void> setVideoEncoderParam({
  int videoFps,
  int videoBitrate,
  int videoResolution,
  int videoResolutionMode,
});
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| videoFps | int | ビデオキャプチャのフレームレート。 |
| videoBitrate | int | ビットレート。SDKは目標ビットレートに応じてエンコードを行い、ネットワークの状態が良くない場合のみ、ビデオビットレートを動的に引き下げます。|
| videoResolution | int | ビデオ解像度。|
| videoResolutionMode | int | 解像度モード。|
>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam)をご参照ください。

### setLocalViewMirror

ローカル画面のミラーモードのプレビューを設定します。
```dart
Future<void> setLocalViewMirror(bool isMirror);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| isMirror | boolean | イメージプレビューモードの起動の有無。true：オン、false：オフ。|

## ローカル音声操作のインターフェース
### startMicrophone

マイクの集音開始。
```dart
Future<void> startMicrophone({int quality});
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| quality | int | オーディオ品質。詳細については、 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a4451651bf7fc810efc4400964c3c0408)をご参照ください。 |

### stopMicrophone

マイクの集音停止。
```dart
Future<void> stopMicrophone();
```

### muteLocalAudio

ローカル音声のミュート起動/停止。
```dart
Future<void> muteLocalAudio(bool mute);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| mute | boolean | true：ミュート、false：ミュート取り消し。|

### setSpeaker

スピーカーまたはヘッドホンの起動設定。
```dart
Future<void> setSpeaker(bool useSpeaker);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| useSpeaker | boolean | true：スピーカー、false：ヘッドホン。|

### setAudioCaptureVolume

マイクの集音音量設定。
```dart
Future<void> setAudioCaptureVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| volume | int | 集音音量、値：0 - 100、デフォルト値：100。|

### setAudioPlayoutVolume

再生音量の設定。
```dart
Future<void> setAudioPlayoutVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| volume | int | 再生音量、値：0 - 100、デフォルト値：100。|

### startAudioRecording

録音の開始。
```dart
Future<int?> startAudioRecording(String filePath);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| filePath | String | 録音ファイルの保存パス。このパスはユーザーが自身で指定する必要があります。パスが存在し、記述できることを確認してください。このパスはファイル名およびフォーマットの拡張子まで正確に示す必要があります。フォーマットの拡張子によって録音ファイルの形式が決まります。現在サポートしている形式はPCM、WAV、AACです。|

### stopAudioRecording

録音の停止。
```dart
Future<void> stopAudioRecording();
```

### enableAudioVolumeEvaluation

音量レベルリマインダを有効にします。
```dart
Future<void> enableAudioVolumeEvaluation(int intervalMs);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| intervalMs | int | onUserVoiceVolume コールバックをトリガーするインターバルを決定します。単位はms。最小インターバルは100ms。0以下の場合、コールバックは停止します。設定を300msにすることを推奨します。|

## スクリーンキャプチャのインターフェース
### startScreenCapture

画面共有を開始。
```dart
Future<void> startScreenCapture({
  int videoFps,
  int videoBitrate,
  int videoResolution,
  int videoResolutionMode,
  String appGroup,
});
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| videoFps | int | ビデオキャプチャのフレームレート。 |
| videoBitrate | int | ビットレート。SDKは目標ビットレートに応じてエンコードを行い、ネットワークの状態が良くない場合のみ、ビデオビットレートを動的に引き下げます。|
| videoResolution | int | ビデオ解像度。|
| videoResolutionMode | int | 解像度モード。|
| appGroup | String | このパラメータはiOS端末でのみ有効となり、Android端末の場合、このパラメータを気にする必要はありません。このパラメータはメインAppとBroadcastが共有するApplication Group Identifierです。|
>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam)をご参照ください。

### stopScreenCapture

画面キャプチャの停止。
```dart
Future<void> stopScreenCapture();
```

### pauseScreenCapture

スクリーンキャプチャの一時停止。
```dart
Future<void> pauseScreenCapture();
```

### resumeScreenCapture

スクリーンキャプチャの再開。
```dart
Future<void> resumeScreenCapture();
```

## 管理オブジェクト取得に関するインターフェース
### getDeviceManager

デバイス管理オブジェクト [TXDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html)を取得します。
```dart
getDeviceManager();
```

### getBeautyManager

美顔管理オブジェクト[TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html)を取得します。
```dart
getBeautyManager();
```

美顔管理では、次の機能を使用できます。
- 「美顔のスタイル」、「美白」、「肌色補正（血色・つや感）」、「デカ眼」、「顔痩せ」、「V顔」、「下あご」、「面長補正」、「小鼻」、「キラキラ目」、「白い歯」、「目の弛み除去」、「シワ除去」、「ほうれい線除去」などの美容効果を設定します。
- 「髪の生え際」、「眼と眼の距離」、「眼角度」、「唇の形」、「鼻翼」、「鼻の位置」、「唇の厚さ」、「顔の形」を調整します。
- 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
- メイクアップを追加します。
- ジェスチャー認識を行います。

## メッセージ送信関連インターフェース
### sendRoomTextMsg

ミーティング中にテキストメッセージをブロードキャストします。通常、チャットに使用します。
```dart
Future<ActionCallback> sendRoomTextMsg(String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| message  | String   | テキストメッセージ。|

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。
```dart
Future<ActionCallback> sendRoomCustomMsg(String cmd, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| cmd | String | コマンドワード。開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。|
| message  | String   | テキストメッセージ。|

## TRTCMeetingDelegateイベントコールバック
## 一般的なイベントコールバック
### onError

エラーのコールバック。
>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| errCode | int | エラーコード。|
| errMsg | String | エラー情報。|
| extraInfo | String | 拡張情報フィールド。個別のエラーコードにより問題の特定に役立つ追加情報をもたせることが可能です。|

### onWarning

警告のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| warningCode | int | エラーコード。|
| warningMsg | String | 警告情報。|
| extraInfo | String | 拡張情報フィールド。個別のエラーコードにより問題の特定に役立つ追加情報をもたせることが可能です。|

### onKickedOffline

他のユーザーが同じアカウントでログインすると、キックアウトされてオフラインになります。

## ミーティングルームのイベントコールバック
### onRoomDestroy

ミーティングルームが破棄された時のコールバック。キャスターの退室時、ルーム内の全ユーザーがこの通知を受信します。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| roomId | String | ミーティングルームID。|

### onNetworkQuality

ネットワーク状態のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | アップストリームのネットワーク品質。|
| remoteQuality | List&lt;TRTCCloudDef.TRTCQuality&gt; | ダウンストリームのネットワーク品質。|

### onUserVolumeUpdate

ユーザーの通話音量のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userVolumes | List | 発言中のすべてのルーム参加者の音量。値の範囲：0～100。|
| totalVolume | int | すべてのリモート参加者の総音量。値の範囲：0～100。|

## 参加者入退室のイベントコールバック
### onEnterRoom

ローカルの入室のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| result | int | 0を上回るときは入室の所要時間（ms）、0未満のときは入室のエラーコードです。|

### onLeaveRoom

ローカルの退室のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| reason | int | ミーティング退出の原因。0：自主的にleaveMeetingを呼び出して退出。1：サーバーによる現在のミーティングからのキックアウト。2：現在のミーティング全体の解散。|

### onUserEnterRoom

新しい参加者の入室のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 新しい参加者のユーザーID。|

### onUserLeaveRoom

参加者の退出のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId | String | 退出した参加者のユーザーID。|

## 参加者の音声・ビデオのイベントコールバック
### onUserAudioAvailable

参加者のマイク起動/停止のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId    | String | ユーザーID。|
| available | boolean | true：ユーザーがマイクをオンにします。false：ユーザーがマイクをオフにします。|

### onUserVideoAvailable

参加者によるカメラ起動/停止のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId    | String | ユーザーID。|
| available | boolean | true：ユーザーがカメラをオンにします。false：ユーザーがカメラをオフにします。|

### onUserSubStreamAvailable

参加者がサブチャンネル画面を起動/停止したときのコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| userId    | String | ユーザーID。|
| available | boolean | true：ユーザーがサブチャンネル画面を起動。false：ユーザーがサブチャンネル画面を停止。|

## メッセージイベントのコールバック
### onRecvRoomTextMsg

テキストメッセージ受信のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| message  | String   | テキストメッセージ。|
| sendId | String | 送信者のユーザーID。|
| userAvatar | String | 送信者のユーザープロフィール画像。|
| userName | String | 送信者のユーザーニックネーム。|

### onRecvRoomCustomMsg

カスタムメッセージ受信のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| command | String | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。|
| message  | String   | テキストメッセージ。|
| sendId | String | 送信者のユーザーID。|
| userAvatar | String | 送信者のユーザープロフィール画像。|
| userName | String | 送信者のユーザーニックネーム。|

## スクリーンキャプチャのイベントコールバック
### onScreenCaptureStarted

スクリーンキャプチャ開始のコールバック。

### onScreenCapturePaused

スクリーンキャプチャ一時停止のコールバック。

### onScreenCaptureResumed

スクリーンキャプチャ再生のコールバック。

### onScreenCaptureStoped

スクリーンキャプチャ停止のコールバック。

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| reason | int | 停止の理由。0：ユーザーの自発的な停止。1：スクリーンウィンドウが閉じられたことによるによる停止。|
