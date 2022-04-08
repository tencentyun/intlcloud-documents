## TRTCCloud

### 基本的な方法

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sharedInstance.html) | TRTCCloudシングルトンを作成します。|
| [destroySharedInstance](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/destroySharedInstance.html) | TRTCCloudシングルトンを廃棄します。|
| [registerListener](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/registerListener.html) | イベント監視を設定します。|
| [unRegisterListener](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/unRegisterListener.html) | イベント監視を削除します。|

### ルーム関連インターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enterRoom.html) | ルームに参加し、ルームが存在しない場合、システムが自動的に新しいルームを作成します。           |
| [exitRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/exitRoom.html) | ルームから退出します。                                                   |
| [switchRole](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/switchRole.html) | ロールを切り替えます。ライブストリーミングシナリオ（TRTC_APP_SCENE_LIVEおよび TRTC_APP_SCENE_VOICE_CHATROOM）のみに適しています。 |
| [setDefaultStreamRecvMode](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setDefaultStreamRecvMode.html) | オーディオビデオの受信モードを設定します。有効にするには、入室する前に設定してください。           |
| [connectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/connectOtherRoom.html) | ルーム間通話（キャスターPK）リクエストします。          |
| [disconnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/disconnectOtherRoom.html) | ルーム間通話から退出します。          |
| [switchRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/switchRoom.html) | ルームを切り替えます。         |



### CDN関連インターフェース関数

| API                                                          | 説明                       |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishing.html) | Tencent CloudへのライブCDNのプッシュを開始します。      |
| [stopPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishing.html) | Tencent CloudへのライブCDNのプッシュを停止します。      |
| [startPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishCDNStream.html) | 他社のクラウドへのライブCDNのリツイートを開始します。      |
| [stopPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishCDNStream.html) | Tencent Cloud以外のアドレスへのリツイートを停止します。     |
| [setMixTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setMixTranscodingConfig.html) | クラウドのミクスストリーミングトランスコードパラメータを設定します。      |


### ビデオ関連インターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalPreview](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startLocalPreview.html) | ローカルビデオのプレビュー画面を開始します。                                     |
| [stopLocalPreview](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalPreview.html) | ローカルビデオの収集およびプレビューを停止します。                                     |
| [muteLocalVideo](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteLocalVideo.html) | ローカルビデオデータのプッシュを一時停止/再開します。                                |
| [startRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startRemoteView.html) | リモートビデオ画面の表示を開始します。                                       |
| [stopRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopRemoteView.html) | リモートビデオ画面の表示を停止すると同時に、リモートユーザーのビデオデータトラフィックのプルを停止します。   |
| [stopAllRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopAllRemoteView.html) | すべてのリモートビデオ画面の表示を停止すると同時に、リモートユーザーのビデオデータトラフィックのプルを停止します。 |
| [muteRemoteVideoStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteRemoteVideoStream.html) | 指定したたリモートビデオストリームの受信を一時停止/再開します。                              |
| [muteAllRemoteVideoStreams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteAllRemoteVideoStreams.html) | すべてのリモートビデオトラフィックを一時停止/再開します。                                |
| [setVideoEncoderParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderParam.html) | ビデオエンコーダに関するパラメータを設定します。                                     |
| [setNetworkQosParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setNetworkQosParam.html) | ネットワークフロー制御に関するパラメータを設定します。                                       |
| [setLocalRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLocalRenderParams.html) | ローカル画像のレンダリングモードを設定します。|
| [setRemoteRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setRemoteRenderParams.html) | リモート画像に関するパラメータを設定します。|
| [setVideoEncoderRotation](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderRotation.html) | ビデオコーデック出力先の画面方向、すなわちリモートユーザーが見ている画面方向とサーバーで記録された画面方向を設定します。|
| [setVideoEncoderMirror](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderMirror.html) | エンコーダ出力の画面イメージモードを設定します。|
| [setGSensorMode](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setGSensorMode.html) | 重力感知の適応モードを設定します。|
| [enableEncSmallVideoStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enableEncSmallVideoStream.html) | 大小画面の2ウェイコーディングモードを設定します。|
| [setRemoteVideoStreamType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setRemoteVideoStreamType.html) | 指定したuidの大画面または小画面を選択します。                          |
| [snapshotVideo](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/snapshotVideo.html) | ビデオ画面のスクリーンショット。|


### オーディオ関連インターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startLocalAudio.html) | ローカルオーディオの収集およびアップストリームを有効にします。                                   |
| [stopLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalAudio.html) | ローカルオーディオの収集およびアップストリームを無効にします。                                   |
| [muteLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteLocalAudio.html) | ローカルオーディオをミュート/ミュート解除します。                                    |
| [setVideoMuteImage](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoMuteImage.html) | ローカルビデオのプッシュを一時停止するときにプッシュする画像を設定します。                                    |
| [setAudioRoute](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager/setAudioRoute.html) | オーディオルーティングを設定します。                                               |
| [muteRemoteAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteRemoteAudio.html) | 指定したリモートユーザーのサウンドをミュート/ミュート解除します。                          |
| [muteAllRemoteAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteAllRemoteAudio.html) | すべてのユーザーのサウンドをミュート/ミュート解除します。                                |
| [setAudioCaptureVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setAudioCaptureVolume.html) | SDKの収音量を設定します。                                          |
| [getAudioCaptureVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioCaptureVolume.html) | SDKの収音量を取得します。                                          |
| [setAudioPlayoutVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setAudioPlayoutVolume.html) | SDKの再生音量を設定します。                                          |
| [getAudioPlayoutVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioPlayoutVolume.html) | SDKの再生音量を取得します。                                          |
| [enableAudioVolumeEvaluation](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enableAudioVolumeEvaluation.html) | 音量通知を有効にします。                                           |
| [startAudioRecording](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startAudioRecording.html) | 録音を開始します。                                                   |
| [stopAudioRecording](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopAudioRecording.html) | 録音を停止します。                                                   |
| [setSystemVolumeType](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager/setSystemVolumeType.html) | 通話時に使用するシステム音量タイプを設定します。                               |


### デバイス管理インターフェース

| API               | 説明         |
|-----|-----|
| [getDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getDeviceManager.html) | デバイス管理モジュールを取得し、インターフェースの詳細について[デバイス管理インターフェース](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html)ドキュメントをご参照ください。|


### 美顔フィルタに関するインターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getBeautyManager.html) | 美顔管理オブジェクトを取得し、インターフェースの詳細について[美顔管理](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html)ドキュメントをご参照ください。|
| [setWatermark](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setWatermark.html) | ウォーターマークを追加します。                                                   |


### 音楽の特殊効果および声の特殊効果

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioEffectManager.html) | 音色管理クラス TXAudioEffectManagerを取得し、BGM、短音色および声の特殊効果の管理に使用され、インターフェースの詳細について[音色管理](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html)ドキュメントをご参照ください。|

### サブストリーム関連インターフェース関数

| API                                                          | 説明         |
| ------------------------------------------------------------ | -------------- |
| [startScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html) | 画面共有をオンにします。 |
| [stopScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopScreenCapture.html) | 画面収集をオフにします。|
| [pauseScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/pauseScreenCapture.html) | 画面共有を一時停止します。|
| [resumeScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/resumeScreenCapture.html) | 画面共有を再開します。|

### カスタムメッセージ送信

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sendCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sendCustomCmdMsg.html) | カスタムメッセージをルーム内のすべてのユーザーに送信します。|
| [sendSEIMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sendSEIMsg.html) | 小さいデータ量のカスタムデータをビデオフレーム内に埋め込みます。                                           |


### ネットワークテスト

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startSpeedTest.html) | ネットワーク速度測定（ビデオ通話中にはテストしないでください。通話品質に影響するおそれがあります）。|
| [stopSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopSpeedTest.html) | サーバーの速度測定を停止します。                                             |


### ログ関連インターフェース関数

| API                                                          | 説明                       |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getSDKVersion.html) | SDKのバージョン情報を取得します。         |
| [setLogLevel](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogLevel.html) | Logの出力レベルを設定します。         |
| [setLogDirPath](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogDirPath.html) | ログ保存パスを変更します。         |
| [setLogCompressEnabled](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogCompressEnabled.html) | Logのローカル圧縮を有効または無効にします。         |
| [setConsoleEnabled](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setConsoleEnabled.html) | コンソールログの印刷を有効または無効にします。  |


## TRTCCloudListener

Tencent Cloudのビデオ通話機能のイベントコールバックインターフェース。

### エラーイベントおよび警告イベント

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onError) | エラーコールバック。SDKの回復不可能なエラーを示します。監視し、状況に応じてユーザーに適切な画面メッセージを表示しなければなりません。|
| [onWarning](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onWarning) | 警告コールバック。ラグやリカバリ可能なデコードの失敗など、重大度の低い問題を通知します。|


### ルームイベントのコールバック

| API                                                          | 説明                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onEnterRoom) | ルーム参加済のコールバック。                  |
| [onExitRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onExitRoom) | ルーム退出のイベントコールバック。                |
| [onSwitchRole](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSwitchRole) | ロール切り替えのイベントコールバック。                |
| [onConnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onConnectOtherRoom) | ルーム間通話（キャスターPK）リクエストの結果コールバック。         |
| [onDisConnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onDisConnectOtherRoom) | ルーム間通話（キャスターPK）終了の結果コールバック。        |
| [onSwitchRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSwitchRoom) | ルーム切り替え(switchRoom)の結果コールバック。               |

### メンバーイベントコールバック

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRemoteUserEnterRoom) | 現在ルームに参加するユーザーがいます。                |
| [onRemoteUserLeaveRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRemoteUserLeaveRoom) | 現在のルームから退出するユーザーがいます。                |
| [onUserVideoAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserVideoAvailable) | リモートユーザーに再生可能なメインチャネル画面があるかどうか（通常はカメラに用いられます）。 |
| [onUserSubStreamAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserSubStreamAvailable) | リモートユーザーに再生可能なサブチャネル画面があるかどうか（通常は画面共有に用いられます）。 |
| [onUserAudioAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserAudioAvailable) | リモートユーザーが再生可能なオーディオデータを持っていますか。        |
| [onFirstVideoFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onFirstVideoFrame) | ローカルまたはリモートユーザーの最初のフレーム画面のレンダリングを開始します。           |
| [onFirstAudioFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onFirstAudioFrame) | リモートユーザーの最初のフレームオーディオの再生を開始します（ローカルサウンドは通知されません）。   |
| [onSendFirstLocalVideoFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSendFirstLocalVideoFrame) | 最初のフレームのローカルビデオデータが送信されました。    |
| [onSendFirstLocalAudioFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSendFirstLocalAudioFrame) | 最初のフレームのローカルオーディオデータが送信されました。       |

### BGM再生のコールバックインターフェース

BGM再生のコールバックインターフェースです。

| API                                                          | 説明                   |
| ------------------------------------------------------------ | ------------------------ |
| [onMusicObserverStart](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMusicObserverStart) | 音楽再生開始のコールバック通知。|
| [onMusicObserverPlayProgress](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMusicObserverPlayProgress) | 音楽再生の進捗状況のコールバック通知。 |
| [onMusicObserverComplete](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMusicObserverComplete) | 音楽再生終了のコールバック通知。|

### 統計および品質コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onNetworkQuality) | ネットワーク品質。このコールバックは2秒ごとに1度トリガーされ、現在のネットワークのアップストリームとダウンストリーム品質の統計を行います。 |
| [onStatistics](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStatistics) | 技術指標統計コールバック。                          |


### サーバーイベントコールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onConnectionLost) | SDKとサーバーの接続が切断されました。                |
| [onTryToReconnect](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onTryToReconnect) | SDKがサーバーに再接続しようとします。                |
| [onConnectionRecovery](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onConnectionRecovery) | SDKとサーバーの接続が回復しました。         |
| [onSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSpeedTest) | サーバースピードテストのコールバックです。SDKは複数のサーバーIPに対するスピードテストを実行し、IPごとのスピードテスト結果をこのコールバックを使用して通知します。 |


### ハードウェアデバイスイベントコールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onCameraDidReady) | カメラの準備ができました。                                             |
| [onMicDidReady](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMicDidReady) | マイクの準備ができました。                         |
| [onUserVoiceVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserVoiceVolume) | 音量レベルをリマインドするためのコールバックです。userIdごとの音量とリモートの総音量が含まれます。 |


### カスタムメッセージ受信のコールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onRecvCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRecvCustomCmdMsg) | カスタムメッセージ受信のコールバック。|
| [onMissCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMissCustomCmdMsg) | カスタムメッセージ紛失のコールバック。|
| [onRecvSEIMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRecvSEIMsg) | SEIメッセージ受信のコールバック。|


### CDNバイパス転送コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStartPublishing) | Tencent CloudへのライブCDN プッシュ開始のコールバック。[TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishing.html)のstartPublishing()インターフェースに対応します。|
| [onStopPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStopPublishing) | Tencent CloudへのライブCDN プッシュ停止のコールバック。[TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishing.html)のstopPublishing()インターフェースに対応します。|
| [onStartPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStartPublishCDNStream) | Relayed Pushの起動からCDN完了までのコールバック。|
| [onStopPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStopPublishCDNStream) | Relayed Push停止からCDN完了までのコールバック。|
| [onSetMixTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSetMixTranscodingConfig) | クラウドのミクスストリーミングトランスコードパラメータ設定のコールバック。[TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setMixTranscodingConfig.html)のsetMixTranscodingConfig()インターフェースに対応します。|


### 画面共有コールバック

| API               | 説明               |
| ------------------------------------------------------------ | ---------------- |
| [onScreenCaptureStarted](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCaptureStarted) | 画面共有開始時にSDKがこのコールバックで通知します |
| [onScreenCapturePaused](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCapturePaused) | 画面共有がpauseScreenCapture()を呼び出すときに、SDKがこのコールバックで通知します。|
| [onScreenCaptureResumed](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCaptureResumed) | 画面共有がresumeScreenCapture()を呼び出すときに、SDKがこのコールバックで通知します。|
| [onScreenCaptureStoped](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCaptureStoped) | 画面共有停止ときにはSDKがこのコールバックで通知します。|

### スクリーンキャプチャコールバック

| API               | 説明               |
| ------------------------------------------------------------ | ---------------- |
| [onSnapshotComplete](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSnapshotComplete) | スクリーンショット完了時のコールバック。|


## 主要なタイプの定義

| タイプ名                                                         | 説明                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCCloudDef](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCCloudDef-class.html) | 主要なタイプ定義用変数。                              |
| [TRTCParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCParams-class.html) | 入室パラメータ。                              |
| [TRTCSwitchRoomConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCSwitchRoomConfig-class.html) | ルームパラメータ切り替え用パラメータ。                              |
| [TRTCVideoEncParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCVideoEncParam-class.html) | ビデオエンコーダパラメータ。                              |
| [TRTCNetworkQosParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCNetworkQosParam-class.html) | ネットワークフロー制御に関するパラメータ。                      |
| [TRTCRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCRenderParams-class.html) | リモート画像パラメータ。|
| [TRTCMixUser](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCMixUser-class.html) | クラウドミクスストリーミングにおける各チャンネル子画面の位置情報。|
| [TRTCTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCTranscodingConfig-class.html) | クラウドミクスストリーミング（トランスコード）の構成。|
| [TXVoiceChangerType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TXVoiceChangerType-class.html) | ボイス変更タイプの定義（ロリ、オヤジ、ヘビーメタル、外国人など）。|
| [TXVoiceReverbType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TXVoiceReverbType-class.html) | ボイス変更タイプの定義（KTV、小ルーム、大会堂、低音、広音など）。|
| [AudioMusicParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/AudioMusicParam-class.html) | 音楽と声設定インターフェースパラメータ。|
| [TRTCAudioRecordingParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCAudioRecordingParams-class.html) | 録音パラメータ。|
| [TRTCPublishCDNParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCPublishCDNParam-class.html) | CDNリツイートパラメータ。|
