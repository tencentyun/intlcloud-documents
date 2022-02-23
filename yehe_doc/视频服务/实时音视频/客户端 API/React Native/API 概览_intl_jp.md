## TRTCCloud

### 基本的な方法

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#sharedInstance) | TRTCCloudシングルトンを作成します。 |
| [destroySharedInstance](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#destroySharedInstance) | TRTCCloudシングルトンを破棄します。 |
| [registerListener](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#registerListener) | イベントリスナーを設定します。 |
| [unRegisterListener](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#unRegisterListener) | イベントリスナーを削除します。 |

### ルーム関連インターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#enterRoom) | ルームに入室します。ルームが存在しない場合は、システムが新しいルームを自動的に作成します。           |
| [exitRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#exitRoom) | ルームから退出します。                                                   |
| [switchRole](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#switchRole) | ロールを切り替えます。ライブストリーミングシナリオ（TRTC_APP_SCENE_LIVEおよび TRTC_APP_SCENE_VOICE_CHATROOM）のみに適しています。 |
| [setDefaultStreamRecvMode](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setDefaultStreamRecvMode) | オーディオビデオの受信モードを設定します。有効にするには、入室する前に設定する必要があります。           |
| [connectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#connectOtherRoom) | ルーム間通話をリクエストします（キャスターPK）。          |
| [disconnectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#disconnectOtherRoom) | ルーム間通話から退出します。          |
| [switchRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#switchRoom) | ルームを切り替えます。         |



### CDN関連インターフェース関数

| API                                                          | 説明                       |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startPublishing) | Tencent CloudへのライブCDNのプッシュを開始します。      |
| [stopPublishing](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopPublishing) | Tencent CloudへのライブCDNのプッシュを停止します。      |
| [startPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startPublishCDNStream) | 同業他社CloudへのライブCDNの転送を開始します。      |
| [stopPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopPublishCDNStream) | Tencent Cloud以外のアドレスへの転送を停止します。     |
| [setMixTranscodingConfig](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setMixTranscodingConfig) | クラウドのミクスストリーミングトランスコードパラメータを設定します。      |


### ビデオ関連インターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [muteLocalVideo](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteLocalVideo) | ローカルのビデオデータのプッシュを一時停止/再開します。                                |
| [startRemoteView](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startRemoteView) | リモートビデオ画面の表示を開始します。                                       |
| [stopRemoteView](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopRemoteView) | リモートビデオ画面の表示を停止すると同時に、リモートユーザーのビデオデータストリームをプルしないようにします。   |
| [muteRemoteVideoStream](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteRemoteVideoStream) | 指定されたリモートビデオストリームの受信を一時停止/再開します。                              |
| [muteAllRemoteVideoStreams](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteAllRemoteVideoStream) | すべてのリモートビデオストリームの受信を一時停止/再開します。                              |
| [setVideoEncoderParam](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoEncoderParam) | ビデオエンコーダ関連のパラメータを設定します。                                     |
| [setNetworkQosParam](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setNetworkQosParam) | ネットワークフロー制御関連のパラメータを設定します。                                       |
| [setVideoEncoderRotation](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoEncoderRotation) | ビデオコーデックが出力する画面方向、すなわち、リモートユーザーが視聴する画面およびサーバーが録画する画面方向を設定します。 |
| [setVideoEncoderMirror](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoEncoderMirror) | エンコーダが出力する画面のミラーリングモードを設定します。 |
| [setGSensorMode](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setGSensorMode) | 重力センサーの適応モードを設定します。 |
| [setVideoMuteImage](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoMuteImage) | ローカルビデオが一時停止したときにプッシュしたい画像を設定します。                                    |

### オーディオ関連インターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startLocalAudio) | ローカルオーディオのキャプチャとアップストリームをオンにします。                                   |
| [stopLocalAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopLocalAudio) | ローカルオーディオのキャプチャとアップストリームをオフにします。                                   |
| [muteLocalAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteLocalAudio) | ローカルのオーディオをミュート/ミュート解除します。                                    |
| [setAudioRoute](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_device_manager.default.html#setAudioRoute) | オーディオルーティングを設定します。                                               |
| [muteRemoteAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteRemoteAudio) | 指定したリモートユーザーの音声をミュート/ミュート解除します。                          |
| [muteAllRemoteAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteAllRemoteAudio) | すべてのユーザーの音声をミュート/ミュート解除します。                                |
| [setAudioCaptureVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setAudioCaptureVolume) | SDKキャプチャ音量を設定します。                                          |
| [getAudioCaptureVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getAudioCaptureVolume) | SDKキャプチャ音量を取得します。                                          |
| [setAudioPlayoutVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setAudioPlayoutVolume) | SDK再生音量を設定します。                                          |
| [getAudioPlayoutVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getAudioPlayoutVolume) | SDK再生音量を取得します。                                          |
| [enableAudioVolumeEvaluation](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#enableAudioVolumeEvaluation) | 音量のプロンプトを有効にします。                                           |
| [startAudioRecording](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startAudioRecording) | 録音を開始します。                                                   |
| [stopAudioRecording](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopAudioRecording) | 録音を停止します。                                                   |


### デバイス管理インターフェース

| API      | 説明 |
|-----|-----|
| [getDeviceManager](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getDeviceManager) | デバイス管理モジュールを取得します。インターフェースの詳細については、[デバイス管理インターフェース](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_device_manager.default.html)のドキュメントをご参照ください。 |


### 美顔フィルタに関するインターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getBeautyManager](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getBeautyManager) | 美顔管理オブジェクトを取得します。インターフェースの詳細については、[美顔管理](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_beauty_manager.default.html)のドキュメントをご参照ください。 |
| [setWatermark](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setWatermark) | ウォーターマークを追加します。                                                   |


### 音楽の特殊効果および声の特殊効果

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getAudioEffectManager) | BGM、ショートオーディオエフェクトおよびボーカルエフェクトに用いられるオーディオエフェクト管理クラスTXAudioEffectManagerを取得します。インターフェースの詳細については、[オーディオエフェクト管理](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_audio_effect_manager.default.html)のドキュメントをご参照ください。 |

### ネットワークテスト

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startSpeedTest) | ネットワークスピードテストを開始します（通話品質への影響を避けるため、ビデオ通話中はテストしないでください）。 |
| [stopSpeedTest](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopSpeedTest) | サーバーのスピードテストを停止します。                                             |


### ログ関連インターフェース関数

| API                                                          | 説明                       |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getSDKVersion) | SDKのバージョン情報を取得します。         |
| [setLogLevel](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setLogLevel) | Log出力レベルを設定します。         |
| [setLogDirPath](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setLogDirPath) | ログ保存パスを変更します。         |
| [setLogCompressEnabled](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setLogCompressEnabled) | Logのローカル圧縮を有効または無効にします。        |
| [setConsoleEnabled](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setConsoleEnabled) | コンソールログの印刷を有効または無効にします。  |


## TRTCCloudListener

Tencent Cloudのビデオ通話機能のイベントコールバックインターフェース。

### エラーイベントおよび警告イベント

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onError) | エラーコールバックは、SDKのリカバリー不能なエラーを意味します。確実に監視し、状況に応じてユーザーに適切なインターフェースプロンプトを提供してください。 |
| [onWarning](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onWarning) | アラートコールバックは、ラグやリカバリー不能なデコードの失敗など、重大ではない問題を通知するために用いられます。|


### ルームイベントのコールバック

| API                                                          | 説明                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onEnterRoom) | ルームに参加済みのコールバック。                  |
| [onExitRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onExitRoom) | ルーム退出のイベントコールバック。                |
| [onSwitchRole](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSwitchRole) | ロール切り替えのイベントコールバック。                |
| [onConnectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onConnectOtherRoom) | ルーム間通話リクエスト（キャスターPK）の結果のコールバック。         |
| [onDisConnectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onConnectOtherRoom) | ルーム間通話の終了（キャスターPK）の結果のコールバック       |
| [onSwitchRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSwitchRoom) | ルーム切り替え(switchRoom)の結果のコールバック。               |

### メンバーイベントコールバック

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onRemoteUserEnterRoom) | ユーザーが現在のルームに参加しました。                |
| [onRemoteUserLeaveRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onRemoteUserLeaveRoom) | ユーザーが現在のルームから退出しました。                |
| [onUserVideoAvailable](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserVideoAvailable) | リモートユーザーに再生可能なメインチャネル画面があるかどうか（通常はカメラに用いられます）。 |
| [onUserSubStreamAvailable](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserSubStreamAvailable) | リモートユーザーに再生可能なサブチャネル画面があるかどうか（通常は画面共有に用いられます）。 |
| [onUserAudioAvailable](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserAudioAvailable) | リモートユーザーに再生可能なオーディオデータがあるかどうか。        |
| [onFirstVideoFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onFirstVideoFrame) | ローカルまたはリモートユーザーの最初のフレーム画面のレンダリングを開始します。 |
| [onFirstAudioFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onFirstAudioFrame) | リモートユーザーの最初のフレームのオーディオ再生を開始します（ローカル音声は現時点では通知されません）。   |
| [onSendFirstLocalVideoFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSendFirstLocalVideoFrame) | 最初のフレームのローカルビデオデータが送信されました。    |
| [onSendFirstLocalAudioFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSendFirstLocalVideoFrame) | ローカルオーディオデータの最初のフレームが送信されました。    |

### BGM再生のコールバックインターフェース

BGM再生のコールバックインターフェースです。

| API                                                          | 説明                   |
| ------------------------------------------------------------ | ------------------------ |
| [onMusicObserverStart](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverStart) | 音楽再生開始のコールバック通知。 |
| [onMusicObserverPlayProgress](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverPlayProgress) | 音楽再生の進捗状況のコールバック通知。 |
| [onMusicObserverComplete](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverStart) | 音楽再生終了のコールバック通知。 |

### 統計および品質コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onNetworkQuality) | ネットワーク品質。このコールバックは2秒ごとに1度トリガーされ、現在のネットワークのアップストリームとダウンストリーム品質の統計を行います。 |
| [onStatistics](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStatistics) | テクニカルインジケータ統計コールバック。                          |


### サーバーイベントコールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onConnectionLost) | SDKとサーバー間の接続が切断されます。                |
| [onTryToReconnect](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onTryToReconnect) | SDKはサーバーへの再接続を試みます。                |
| [onConnectionRecovery](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onConnectionRecovery) | SDKとサーバー間の接続が復元されます。         |
| [onSpeedTest](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSpeedTest) | サーバースピードテストのコールバックです。SDKは複数のサーバーIPに対するスピードテストを実行し、IPごとのスピードテスト結果をこのコールバックを使用して通知します。 |


### ハードウェアデバイスイベントコールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onCameraDidReady) | カメラの準備ができました。                                             |
| [onMicDidReady](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMicDidReady) | マイクの準備ができました。                         |
| [onUserVoiceVolume](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserVoiceVolume) | 音量レベルをリマインドするためのコールバックです。userIdごとの音量とリモートの総音量が含まれます。 |

### CDNバイパス転送コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStartPublishing) | Tencent CloudへのライブCDNのプッシュ開始のコールバック。[TRTCCloud](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startPublishing)のstartPublishing()インターフェースに対応します。 |
| [onStopPublishing](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStopPublishing) | Tencent CloudへのライブCDNのプッシュ停止のコールバック。[TRTCCloud](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopPublishing)のstopPublishing()インターフェースに対応します。 |
| [onStartPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStartPublishCDNStream) | Relayed Pushの起動からCDN完了までのコールバック。|
| [onStopPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStartPublishCDNStream) | Relayed Push停止からCDN完了までのコールバック。|
| [onSetMixTranscodingConfig](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSetMixTranscodingConfig) | クラウドのミクスストリーミングトランスコードパラメータ設定のコールバック。[TRTCCloud](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setMixTranscodingConfig)のsetMixTranscodingConfig()インターフェースに対応します。 |

## 主要なタイプの定義

| タイプ名                                                         | 説明                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCCloudDef](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud_def.TRTCCloudDef.html) | キータイプ定義変数。                              |
| [TRTCParams](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCParams) | 入室パラメータ。                              |
| [TRTCSwitchRoomConfig](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCSwitchRoomConfig) | ルームのパラメータを切り替えます。                              |
| [TRTCVideoEncParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCVideoEncParam) | ビデオコーデックパラメータ。                              |
| [TRTCNetworkQosParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCNetworkQosParam) | ネットワークフロー制御関連のパラメータ。                      |
| [TRTCRenderParams](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCRenderParams) | リモート画像パラメータ。 |
| [TRTCMixUser](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCMixUser) | クラウドミクスストリーミング内の各サブ画面の位置情報。 |
| [TRTCTranscodingConfig](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCTranscodingConfig) | クラウドミクスストリーミング（トランスコード）の構成。 |
| [TXVoiceChangerType](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TXVoiceChangerType) | ボイスチェンジタイプの定義（ロリ声、おじさん声、ロボット声、外国人など）。 |
| [TXVoiceReverbType](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TXVoiceReverbType) | ボイスチェンジタイプの定義（KTV、狭い部屋、ホール、低く沈んだ声、大きくて響く声など）。 |
| [AudioMusicParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#AudioMusicParam) | 音楽とボーカルを設定するインターフェースパラメータ。 |
| [TRTCAudioRecordingParams](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCAudioRecordingParams) | 録音パラメータ。 |
| [TRTCPublishCDNParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCPublishCDNParam) | CDN転送パラメータ。 |
