## TRTCCloud @ TXLiteAVSDK

Tencent Cloudビデオ通話機能の主なインターフェース。

- **主なドキュメントアドレス**：[TRTC Electron SDK](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- **サンプルコードアドレス**：[TRTC Electron Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)

### TRTCオブジェクトの作成
```js
const TRTCCloud = require('trtc-electron-sdk').default;
// import TRTCCloud from 'trtc-electron-sdk';
this.rtcCloud = new TRTCCloud();
```

v7.9.348から、TRTC Electron SDKはtrtc.d.tsファイルを追加しており、 typescriptを使用する開発者の操作性が向上しました。

```javascript
import TRTCCloud from 'trtc-electron-sdk';

const rtcCloud: TRTCCloud = new TRTCCloud();
// SDKバージョン番号の取得
rtcCloud.getSDKVersion();
```

// コールバックの設定
```js
subscribeEvents = (rtcCloud) => {
    rtcCloud.on('onError', (errcode, errmsg) => {
    console.info('trtc_demo: onError :' + errcode + " msg" + errmsg);
    }); 
    rtcCloud.on('onEnterRoom', (elapsed) => {
    console.info('trtc_demo: onEnterRoom elapsed:' + elapsed);
    });
    rtcCloud.on('onExitRoom', (reason) => {
    console.info('onExitRoom: userenter reason:' + reason);
    });
};


subscribeEvents(this.rtcCloud);
```

### TRTCCloudシングルトンの作成と破棄

| API | 説明 |
|-----|-----|
| [getTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.getTRTCShareInstance) | dllを動的にロードするために使用する場合は、[TRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html)オブジェクトシングルトンを作成します。 |
| [destroyTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.destroyTRTCShareInstance) | [TRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html)シングルトンオブジェクトをリリースし、リソースをクリーンアップします。 |

### ルーム関連インターフェース関数

| API | 説明 |
|-----|-----|
| [enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) | ルームに入室します。ルームが存在しない場合は、システムが新しいルームを自動的に作成します。 |
| [exitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom) | ルームを退室します。 |
| [switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom) | ルームを切り替えます。 |
| [switchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRole) | ロールを切り替えます。ライブストリーミングシナリオ（TRTCAppSceneLIVEおよびTRTCAppSceneVoiceChatRoom）のみに適用します。 |
| [connectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#connectOtherRoom) | ルーム間のマイク接続をリクエストします（キャスタールーム間PK）。 |
| [disconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#disconnectOtherRoom)| ルーム間のマイク接続を終了します（キャスタールーム間PK）。 |


### CDN関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishing) | Tencent CloudのライブCDNへのプッシュを開始します。 |
| [stopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishing) | Tencent CloudのライブCDNへのプッシュを停止します。 |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishCDNStream) | 非Tencent CloudのライブCDNへの転送を開始します。|
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishCDNStream) | 非Tencent CloudのライブCDNへのプッシュを停止します。 |
| [setMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig) | クラウドのミクスストリーミングトランスコードパラメータを設定します。 |


### ビデオ関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview) | ローカルカメラのキャプチャとプレビューを起動します。 |
| [stopLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalPreview) | ローカルカメラのキャプチャとプレビューを停止します。 |
| [muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo) | 自身のビデオ画面をブロックしますか。 |
| [startRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) | リモートビデオ画面の表示を開始します。 |
| [stopRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteView) | リモートビデオ画面の表示を停止すると同時に、このリモートユーザーのビデオデータトラフィックのプルを停止します。 |
| [stopAllRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllRemoteView) | すべてのリモートビデオ画面の表示を停止すると同時に、リモートユーザーのビデオデータトラフィックのプルを停止します。 |
| [muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream) | 指定のリモートビデオストリームの受信を一時停止します。 |
| [muteAllRemoteVideoStreams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteVideoStreams) | すべてのリモートビデオストリームの受信を停止します。 |
| [setVideoEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) | ビデオエンコーダの関連パラメータを設定します。 |
| [setNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setNetworkQosParam) | ネットワークトラフィックコントロールの関連パラメータを設定します。 |
| [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams) | ローカル画像（メインストリーム）のレンダリングパラメータを設定します。 |
| [setLocalViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode) | 破棄されたインターフェース：ローカル画像のレンダリングモードを設定します。 |
| [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams) | リモート画像のレンダリングパラメータを設定します。 |
| [setRemoteViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewFillMode) | 破棄されたインターフェース：リモート画像のレンダリングモードを設定します。 |
| [setLocalViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewRotation) | 破棄されたインターフェース：ローカル画像の時計回りの回転角度を設定します。 |
| [setRemoteViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewRotation) | 破棄されたインターフェース：リモート画像の時計回りの回転角度を設定します。 |
| [setVideoEncoderRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderRotation) | ビデオコーデックが出力する画面（リモートユーザーが視聴する画面およびサーバーが録画する画面）方向を設定します。 |
| [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) | 破棄されたインターフェース：ローカルカメラプレビュー画面のイメージモードを設定します。 |
| [setVideoEncoderMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderMirror) | エンコーダが出力する画面のイメージモードを設定します。 |
| [enableSmallVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableSmallVideoStream) | 大小画面のデュアルチャンネルコーディングモードを有効にします。 |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteVideoStreamType) | 指定userIdの大画面または小画面での視聴を選択します。 |
| [setPriorRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setPriorRemoteVideoStreamType) | 破棄されたインターフェース： 視聴者が優先的に選択するビデオ品質を設定します。 |
| [snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo) | ビデオ画面のスクリーンキャプチャです。 |


### オーディオ関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio) |ローカルオーディオのキャプチャとアップストリームを開始します。 |
| [stopLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalAudio) | ローカルオーディオのキャプチャとアップストリームを終了します。 |
| [muteLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalAudio) |ローカルのオーディオをミュートにします。 |
| [muteRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio) | 特定ユーザーの音声をミュートにすると同時に、このリモートユーザーのオーディオデータトラフィックのプルを停止します。 |
| [muteAllRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteAudio) | すべてのユーザーの音声をミュートにすると同時に、リモートユーザーのオーディオデータトラフィックのプルを停止します。 |
| [setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioCaptureVolume) | SDKキャプチャ音量を設定します 。 |
| [getAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioCaptureVolume) | SDKキャプチャ音量を取得します。 |
| [setAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioPlayoutVolume) | SDK再生音量を設定します。 |
| [getAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioPlayoutVolume) | SDK再生音量を取得します。 |
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableAudioVolumeEvaluation) | 音量レベルプロンプトを起動または終了します。 |
| [startAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startAudioRecording) | 録音を開始します。 |
| [stopAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioRecording) | 録音を停止します。 |
| [setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality) | 破棄されたインターフェース：オーディオ品質を設定します。 |
| [setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume) | リモートユーザーの再生音量を設定します。 |


### カメラ関連インターフェース関数

| API | 説明 |
|-----|-----|
| [getCameraDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCameraDevicesList) | カメラデバイスリストを取得します。 |
| [setCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentCameraDevice) | 使用したいカメラを設定します。 |
| [getCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentCameraDevice) |現在使用するカメラ を取得します。 |


### オーディオデバイス関連インターフェース関数

| API | 説明 |
|-----|-----|
| [getMicDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMicDevicesList) | マイクデバイスリストを取得します。 |
| [getCurrentMicDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDevice) | 現在選択しているマイクを取得します。 |
| [setCurrentMicDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDevice) | 使用したいマイクを設定します。 |
| [getCurrentMicDeviceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceVolume) | システムの現在のマイクデバイス音量を取得します。 |
| [setCurrentMicDeviceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceVolume) | システムの現在のマイクデバイスの音量を設定します。 |
| [setCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceMute) | システムの現在のマイクデバイスのミュートステータスを設定します。 |
| [getCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceMute) | システムの現在のマイクデバイスがミュートであるかどうかを取得します。 |
| [getSpeakerDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getSpeakerDevicesList) | スピーカーデバイスリストを取得します。 |
| [getCurrentSpeakerDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDevice) | 現在のスピーカーデバイスを取得します。 |
| [setCurrentSpeakerDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDevice) | 使用したいスピーカーを設定します。 |
| [getCurrentSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerVolume) | システムの現在のスピーカーデバイス音量を取得します。 |
| [setCurrentSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerVolume) |システムの現在のスピーカーデバイス音量を設定します。 |
| [setCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDeviceMute) | システムの現在のスピーカーデバイスのミュートステータスを設定します。 |
| [getCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDeviceMute) | システムの現在のスピーカーデバイスがミュートかどうかを取得します。 |

### 美顔関連インターフェース関数

| API | 説明 |
|-----|-----|
| [setBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBeautyStyle) | 美顔、美白および肌の色調補正エフェクトレベルを設定します。 |
| [setWaterMark](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setWaterMark) | ウォーターマークを設定します。 |


### サブストリーム関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteSubStreamView) | 破棄されたインターフェース：リモートユーザーのサブストリーム（画面共有）画面のレンダリングを開始します。 |
| [stopRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteSubStreamView) | 破棄されたインターフェース：リモートユーザーのサブストリーム（画面共有）画面のレンダリングを停止します。 |
| [setRemoteSubStreamViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewFillMode) | 破棄されたインターフェース：サブストリーム（画面共有）画面のレンダリングモードを設定します。 |
| [setRemoteSubStreamViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewRotation) | 破棄されたインターフェース：サブストリーム（画面共有）画面の時計回りの回転角度を設定します。 |
| [getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources) | 共有可能なウィンドウリストを列挙します。 |
| [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) | 画面共有パラメータを設定します。画面共有中にもこの方法を呼び出すことができます。 |
| [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) | 画面共有を起動します。 |
| [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) | 画面共有を一時停止します。 |
| [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture) | 画面共有を再開します。 |
| [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) | 画面共有を停止します。 |
| [setSubStreamEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamEncoderParam) | サブストリーム（画面共有）のエンコーダパラメータを設定します。 |
| [setSubStreamMixVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamMixVolume) | サブストリーム（画面共有）の音声ミキシングの音量レベルを設定します。 |
| [addExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#addExcludedShareWindow) | 指定ウィンドウを画面共有のexcludeリストに追加します。excludeリストに追加したウィンドウは共有できなくなります。|
| [removeExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeExcludedShareWindow) | 指定ウィンドウを画面共有のexcludeリストから削除します。|
| [removeAllExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeAllExcludedShareWindow) | すべてのウィンドウを画面共有のexcludeリストから削除します。|


### カスタムメッセージの送信

| API | 説明 |
|-----|-----|
| [sendCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendCustomCmdMsg) | カスタムメッセージをルーム内のすべてのユーザーに送信します。 |
| [sendSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendSEIMsg) | データ量の小さなカスタムデータをビデオフレームに埋め込みます。 |


### BGMミキシング関連インターフェース関数

| API | 説明 |
|-----|-----|
| [playBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playBGM) | 破棄されたインターフェース：BGMの再生を起動します。 |
| [stopBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopBGM) | 破棄されたインターフェース：BGMの再生を停止します。 |
| [pauseBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseBGM) | 破棄されたインターフェース：BGMの再生を一時停止します。 |
| [resumeBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeBGM) | 破棄されたインターフェース：BGMの再生を継続します。 |
| [getBGMDuration](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getBGMDuration) | 破棄されたインターフェース：BGMファイルの総時間を取得します。単位はミリ秒です。 |
| [setBGMPosition](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPosition) | 破棄されたインターフェース：BGM再生の進捗を設定します。 |
| [setBGMVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMVolume) | 破棄されたインターフェース：BGM再生音量レベルを設定します。 |
| [setBGMPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPlayoutVolume) | 破棄されたインターフェース：BGMローカル再生音量レベルを設定します。 |
| [setBGMPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPublishVolume) | 破棄されたインターフェース：BGMリモート再生音量レベルを設定します。 |
| [startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback) | システム音声キャプチャを起動します。 |
| [stopSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSystemAudioLoopback) | システム音声キャプチャを終了します。 |
| [setSystemAudioLoopbackVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSystemAudioLoopbackVolume) | システム音声キャプチャの音量を設定します。 |
| [startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic) | BGMの再生を起動します。 |
| [stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic) | BGMの再生を停止します。 |
| [pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic) | BGMの再生を一時停止します。 |
| [resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic) |BGMの再生を再開します。 |
| [getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS) | BGMファイルの総時間を取得します。単位はミリ秒です。 |
| [seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime) |BGM再生の進捗を設定します。 |
| [setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume) | BGMの音量レベルを設定します。BGMの音量レベルを制御するために、BGMの再生や音声ミキシング時に使用します。 |
| [setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume) | BGMのローカル再生音量レベルを設定します。 |
| [setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume) | BGMのリモート再生音量レベルを設定します。 |


### オーディオエフェクト関連インターフェース関数

| API | 説明 |
|-----|-----|
| [playAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playAudioEffect) | 破棄されたインターフェース：オーディオエフェクトを再生します。 |
| [setAudioEffectVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioEffectVolume) | 破棄されたインターフェース：オーディオエフェクト音量を設定します。 |
| [stopAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioEffect) | 破棄されたインターフェース：オーディオエフェクトを停止します。 |
| [stopAllAudioEffects](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllAudioEffects) | 破棄されたインターフェース：すべてのオーディオエフェクトを停止します。 |
| [setAllAudioEffectsVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllAudioEffectsVolume) | 破棄されたインターフェース：すべてのオーディオエフェクトの音量を設定します。 |
| [pauseAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseAudioEffect) | 破棄されたインターフェース：オーディオエフェクトを一時停止します。 |
| [resumeAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeAudioEffect) | 破棄されたインターフェース：オーディオエフェクトを再開します。 |


### デバイスおよびネットワークテスト

| API | 説明 |
|-----|-----|
| [startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest) | ネットワークスピードテストを開始します（通話品質への影響を避けるため、ビデオ通話中はテストしないでください）。 |
| [stopSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeedTest) | ネットワークスピードテストを停止します。 |
| [startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startCameraDeviceTest) | カメラテストを開始します。 |
| [stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopCameraDeviceTest) | カメラテストを停止します。 |
| [startMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startMicDeviceTest) | マイクテストを開始します。 |
| [stopMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopMicDeviceTest) | マイクテストを停止します。 |
| [startSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeakerDeviceTest) | スピーカーテストを開始します。 |
| [stopSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeakerDeviceTest) | スピーカーテストを停止します。 |


### LOG関連インターフェース関数

| API | 説明 |
|-----|-----|
| [getSDKVersion](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getSDKVersion) | SDKバージョン情報を取得します。 |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogLevel) | Log出力レベルを設定します。 |
| [setConsoleEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setConsoleEnabled) | コンソールのログプリントを有効または無効にします。 |
| [setLogCompressEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCompressEnabled) | Logのローカル圧縮を有効または無効にします。 |
| [setLogDirPath](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogDirPath) |ログ保存パスを設定します。 |
| [setLogCallback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCallback) | ログコールバックを設定します。 |
| [callExperimentalAPI](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#callExperimentalAPI) | 試験的APIインターフェースを呼び出します。 |


### 使用停止インターフェース関数

| API | 説明 |
|-----|-----|
| [setMicVolumeOnMixing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMicVolumeOnMixing) | v6.9バージョンから破棄します。 |


## TRTCCallback @ TXLiteAVSDK

Tencent Cloudビデオ通話機能のコールバックインターフェース。

### エラーイベントおよび警告イベント

| API | 説明 |
|-----|-----|
| [onError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onError) | エラーコールバック：SDKがリカバリー不能なエラーは、監視する必要があり、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。 |
| [onWarning](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onWarning) | 警告コールバック：ラグやリカバリー不能なデコードの失敗など、非常に重大な問題を告知するために使用されます。|


### ルームイベントコールバック

| API | 説明 |
|-----|-----|
| [onEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) | 入室済みのコールバックです。 |
| [onExitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) | 退室のイベントコールバックです。 |
| [onSwitchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRole) | ロール切り替えのイベントコールバック。 |
| [onConnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectOtherRoom) | ルーム間マイク接続（キャスタールーム間PK）リクエスト結果のコールバック。 |
| [onDisconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDisconnectOtherRoom) | ルーム間マイク接続（キャスタールーム間PK）終了結果のコールバック。 |
| [onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom) | ルームを切り替えます。 |


### メンバーイベントコールバック

| API | 説明 |
|-----|-----|
| [onRemoteUserEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserEnterRoom) | ユーザーが現在のルームに入室します。 |
| [onRemoteUserLeaveRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserLeaveRoom) | ユーザーが現在のルームを退室します。 |
| [onUserVideoAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) | ユーザーはカメラとビデオを有効にしていますか。 |
| [onUserSubStreamAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserSubStreamAvailable) | ユーザーは画面共有を開始していますか。 |
| [onUserAudioAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) | ユーザーはオーディオのアップストリームを開始していますか。 |
| [onFirstVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstVideoFrame) | ローカルまたはリモートユーザーの最初のフレーム画面のレンダリングを開始します。 |
| [onFirstAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstAudioFrame) |リモートユーザーの最初のフレームのオーディオ再生を開始します（現在、ローカル音声は通知しません）。 |
| [onSendFirstLocalVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalVideoFrame) | 最初のフレームのローカルビデオデータが送信されました。 |
| [onSendFirstLocalAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalAudioFrame) | 最初のフレームのローカルオーディオデータが送信されました。 |
| [onUserEnter](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserEnter) | 破棄されたインターフェース：キャスターが現在のルームに入室します。 |
| [onUserExit](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserExit) | 破棄されたインターフェース： キャスターが現在のルームを退室します。 |


### 統計および品質コールバック

| API | 説明 |
|-----|-----|
| [onNetworkQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onNetworkQuality) | ネットワーク品質：このコールバックは2秒ごとに1度トリガーされ、現在のネットワークのアップストリームとダウンストリーム品質を統計します。 |
| [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics) | 技術指標統計のコールバックです。 |


### サーバーイベントコールバック

| API | 説明 |
|-----|-----|
| [onConnectionLost](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionLost) | SDKがサーバーとの接続を切断します。 |
| [onTryToReconnect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTryToReconnect) | SDKがサーバーとの再接続を試行中です。 |
| [onConnectionRecovery](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionRecovery) | SDKがサーバーとの接続を再開します。 |
| [onSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTest) | サーバースピードテストのコールバックです。SDKは複数のサーバーIPに対するスピードテストを実行し、IPごとのスピードテスト結果をこのコールバックを介して通知します。 |


### ハードウェアデバイスイベントコールバック

| API | 説明 |
|-----|-----|
| [onCameraDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onCameraDidReady) | カメラの準備が完了しました。 |
| [onMicDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMicDidReady) | マイクの準備が完了しました。 |
| [onUserVoiceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVoiceVolume) | 音量レベルをリマインドするためのコールバックです。userIdごとの音量とリモートの総音量が含まれます。 |
| [onDeviceChange](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDeviceChange) | ローカルデバイスオン/オフのコールバック。 |
| [onTestMicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestMicVolume) | マイクテスト音量のコールバックです。 |
| [onTestSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestSpeakerVolume) | スピーカーテスト音量のコールバックです。 |
| [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) | 現在のオーディオキャプチャデバイス音量変更のコールバックです。 |
| [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) | 現在のオーディオ再生デバイス音量変更のコールバックです。 |


### カスタムメッセージ受信のコールバック

| API | 説明 |
|-----|-----|
| [onRecvCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvCustomCmdMsg) | カスタムメッセージ受信のコールバックです。 |
| [onMissCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMissCustomCmdMsg) | カスタムメッセージ消失のコールバックです。 |
| [onRecvSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvSEIMsg) | SEIメッセージ受信のコールバックです。 |


### CDNバイパス転送コールバック

| API | 説明 |
|-----|-----|
| [onStartPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishing) | Tencent CloudのライブCDNへのプッシュ開始のコールバックです。TRTCCloudのstartPublishing()インターフェースに対応します。 |
| [onStopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishing) | Tencent CloudのライブCDNへのプッシュ停止のコールバックです。TRTCCloudのstopPublishing()インターフェースに対応します。 |
| [onStartPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishCDNStream) | CDNへのRelayed Push起動完了のコールバックです。 |
| [onStopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishCDNStream) | CDNへのRelayed Push停止完了のコールバック。 |
| [onSetMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSetMixTranscodingConfig) | クラウドのミクスストリーミングトランスコードパラメータ設定のコールバックです。TRTCCloudのsetMixTranscodingConfig()インターフェースに対応します。 |

### システム音量キャプチャコールバック
| API | 説明 |
|-----|-----|
| [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError) | システム音量キャプチャステータスのコールバック（Macのみで有効）。 |

### オーディオエフェクトコールバック

| API | 説明 |
|-----|-----|
| [onAudioEffectFinished](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioEffectFinished) | 破棄されたインターフェース：オーディオエフェクト再生終了のコールバック。 |

### 画面共有コールバック

| API | 説明 |
|-----|-----|
| [onScreenCaptureCovered](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureCovered) | SDKは画面共有ウィンドウがブロックされ、正常にキャプチャできないことをこのコールバックを介して通知します。このコールバックでユーザーにウィンドウのブロックを解除するよう通知できます。|
| [onScreenCaptureStarted](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStarted) | SDKは画面共有の開始をこのコールバックを介して通知します。 |
| [onScreenCapturePaused](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCapturePaused) | SDKは画面共有の一時停止をこのコールバックを介して通知します。 |
| [onScreenCaptureResumed](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureResumed) | SDKは画面共有の再開をこのコールバックを介して通知します。 |
| [onScreenCaptureStopped](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStopped) | SDKは画面共有の停止をこのコールバックを介して通知します。 |


### スクリーンキャプチャコールバック

| API | 説明 |
|-----|-----|
| [onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete) | SDKはスクリーンキャプチャの完了をこのコールバックを介して通知します。 |


### BGMミキシングイベントコールバック

| API | 説明 |
|-----|-----|
| [onPlayBGMBegin](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMBegin) | 破棄されたインターフェース：BGMの再生を開始します。 |
| [onPlayBGMProgress](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMProgress) | 破棄されたインターフェース：BGM再生の進捗です。 |
| [onPlayBGMComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMComplete) | 破棄されたインターフェース：BGMの再生を終了します。 |


## 主要なタイプの定義

### 主要なタイプ

| タイプ名 | 説明 |
|-----|-----|
| [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)| 入室関連パラメータ。 |
| [TRTCVideoEncParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVideoEncParam.html) | ビデオコーデックパラメータ。 |
| [TRTCNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCNetworkQosParam.html) | ネットワークトラフィックコントロール関連パラメータ。 |
| [TRTCQualityInfo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCQualityInfo.html)| ビデオ品質です。 |
| [TRTCVolumeInfo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVolumeInfo.html) | 音量レベルです。 |
| [TRTCSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCSpeedTestResult.html)| ネットワークスピードテスト結果です。 |
| [TRTCMixUser](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCMixUser.html)| クラウドミクスストリーミングにおける各サブ画面の位置情報です。 |
| [TRTCTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCTranscodingConfig.html)| クラウドミクスストリーミング（トランスコード）の設定です。 |
| [TRTCPublishCDNParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCPublishCDNParam.html)| CDN Relayed Pushパラメータです。 |
| [TRTCAudioRecordingParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCAudioRecordingParams.html)| 録音パラメータです。 |
| [TRTCLocalStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCLocalStatistics.html)| 自身のローカルオーディオビデオ統計情報です。 |
| [TRTCRemoteStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCRemoteStatistics.html) | リモートメンバーのオーディオビデオ統計情報です。 |
| [TRTCStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCStatistics.html)| 統計データです。 |

### 列挙値

| 列挙 | 説明 |
|-----|-----|
| [TRTCVideoResolution](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution)| ビデオ解像度です。 |
| [TRTCVideoResolutionMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolutionMode)| ビデオ解像度モードです。 |
| [TRTCVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoStreamType) | ビデオストリームタイプです。 |
| [TRTCQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQuality)| 画質レベルです。 |
| [TRTCVideoFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoFillMode)| ビデオ画面塗りつぶしモードです。 |
| [TRTCBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCBeautyStyle) | 美顔（美肌）アルゴリズムです。 |
| [TRTCAppScene](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)| ユースケースです。 |
| [TRTCRoleType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCRoleType)| ロールです。ライブストリーミングシナリオ（TRTCAppSceneLIVE）のみに適用します。 |
| [TRTCQosControlMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQosControlMode)| トラフィックコントロールモードです。 |
| [TRTCVideoQosPreference](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoQosPreference)| 画質の好みです。 |
| [TRTCDeviceState](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceState)| デバイスの操作です。 |
| [TRTCDeviceType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceType)| デバイスのタイプです。 |
| [TRTCWaterMarkSrcType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCWaterMarkSrcType)| ウォーターマーク画像のオリジナルタイプです。 |
| [TRTCTranscodingConfigMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode)| ミクスストリーミングパラメータ設定モードです。 |
