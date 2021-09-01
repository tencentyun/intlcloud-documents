## C++ 全プラットフォームインターフェースの紹介
バージョン8.0より、従来のWindows（C++）インターフェースをベースとした、新しいC++ インターフェースを提供しています。Windows、iOS、Mac、Androidプラットフォームに適用します。
C++ インターフェースを統合する方法がわからない場合は、各プラットフォームの統合ガイドをご参照ください。  
- [iOS C++インターフェース統合ガイド](https://intl.cloud.tencent.com/document/product/647/35092)  
- [Android C++インターフェース統合ガイド](https://intl.cloud.tencent.com/document/product/647/35093)  
- [Mac C++インターフェース統合ガイド](https://intl.cloud.tencent.com/document/product/647/35094)  
- [Windows統合ガイド](https://intl.cloud.tencent.com/document/product/647/35095)  

>?
>- 現在C++インターフェースは簡易版（TRTC）の中でのみ提供されています。  
>- Windowsプラットフォームでは、TRTCヘッダーファイルで自動的に「trtc」ネームスペースを使用するようになっていますので、あらためて指定する必要はありません。

## ITRTCCloud @ TXLiteAVSDK
### ITRTCCloudCallbackコールバックの設定

| API | 説明|
|-----|-----|
| [addCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | コールバックインターフェース[ITRTCCloudCallback](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#classtrtc_1_1ITRTCCloudCallback)を設定します。 |
| [removeCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | イベントコールバックを削除します。 |



### ルーム関連インターフェース関数

| API | 説明|
|-----|-----|
| [enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f) | ルームに参加します。 |
| [exitRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | ルームから退出します。 |
| [switchRole](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | ロールの切り替え。ライブストリーミングシナリオ（TRTCAppSceneLIVEおよびTRTCAppSceneVoiceChatRoom）にのみ適用します。 |
| [connectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae472af11c30db29fcd21ea01854ab32f) | ルーム間通話（キャスターのPK）をリクエストします。 |
| [disconnectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | ルーム間マイク接続を解除します。 |
| [setDefaultStreamRecvMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | オーディオビデオデータの受信モードの設定。有効にするには入室前に設定する必要があります。 |
| [createSubCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | サブTRTCCloudインスタンスを作成します。 |
| [destroySubCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0555e9e9d9d02c8c116946915f969d18) | サブTRTCCloudインスタンスを廃棄します。 |
| [switchRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | ルームを切り替えます。 |


### CDN関連インターフェース関数

| API | 説明|
|-----|-----|
| [startPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac2f616263c108bf6ac5ef2b66b83a380) | Tencent CloudのライブCDNに向けたプッシュを開始します。 |
| [stopPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Tencent CloudのライブCDNに向けたプッシュを停止します。 |
| [startPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | 友好関係にあるクラウドのライブCDNに向けたプッシュ転送を開始します。 |
| [stopPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Tencent Cloud以外のアドレスへのプッシュ転送を停止します。 |
| [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | クラウドのミクスストリーミングトランスコードパラメータを設定します。 |


### ビデオ関連インターフェース関数

| API | 説明|
|-----|-----|
| [startLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaf4651f9913924560859f4541211f2df) | ローカルビデオのプレビュー画面を有効にします(Windows、 Mac版)。 |
| [startLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaf4651f9913924560859f4541211f2df2) | ローカルビデオのプレビュー画面(iOS、 Androidバージョン)を有効にし、enterRoomの前にこの関数を呼び出すと、SDKはカメラのみを有効にし、enterRoomの呼び出しがあるまで待ってからプッシュを開始します。enterRoomの後にこの関数を呼び出すと、SDKがカメラを有効にし、ビデオのプッシュを自動的に開始します。1フレーム目のカメラ画面のレンダリングが開始されると、[ITRTCCloudCallback](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#classtrtc_1_1ITRTCCloudCallback)の中のonFirstVideoFrame(null)コールバックを受信します。 |
| [updateLocalView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6db572d1e387b21328c6c78de561838c) | ローカルビデオプレビュー画面のウィンドウを更新します。 |
| [stopLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | ローカルのビデオキャプチャおよびプレビューを停止します。 |
| [muteLocalVideo](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6070313a28d3302c94ad807c636eb60f) | ローカルのビデオデータのプッシュを一時停止/再開します。 |
| [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a25f09552efac99d88a7aad53960146d7) | 指定ユーザーのリモート画面のプルおよび表示を開始します。 |
| [updateRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9f774f9abb7970fb32c3172fa3229fd2) | リモートビデオのレンダリングのウィンドウを更新します。 |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | リモートビデオ画面の表示を停止するとともに、当該リモートユーザーのビデオデータストリームをプルしなくなります。 |
| [stopAllRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | すべてのリモートビデオ画面の表示を停止するとともに、リモートユーザーのビデオデータストリームをプルしなくなります。 |
| [muteRemoteVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a22155f6fe17dde77a16c273e0d5a02a3) | 指定リモートビデオストリームの受信を一次停止/再開します。 |
| [muteAllRemoteVideoStreams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | すべてのリモートビデオストリームの受信を一次停止/再開します。 |
| [setVideoEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa2bc2739031035b40e8f2a76184c20d9) | ビデオコーデック関連パラメータを設定します。 |
| [setNetworkQosParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a374f1000d443de80d70747cba876f879) | ネットワークストリーム制御関連パラメータを設定します。 |
| [setLocalRenderParams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | ローカル画像（メインストリーム）のレンダリングパラメータを設定します。 |
| [setVideoEncoderRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | ビデオコーデックで出力する画面の方向を設定します。すなわち、リモートユーザーが視聴する画面およびサーバーが録画する画面の方向を設定します。 |
| [setVideoEncoderMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | エンコーダで出力する画面のミラーモードを設定します。 |
| [setRemoteRenderParams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | リモート画像のレンダリングモードを設定します。 |
| [enableSmallVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a80648f76afbda35c9bf5d96701c62a9e) | 大小2画面のデュアルチャンネルコーディングモードを有効にします。 |
| [setRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abd330074a9e99cb9c75d42ef3d1d63a0) | 指定userIdの大画面または小画面を選択して視聴します。 |
| [snapshotVideo](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c) | ビデオ画面のスクリーンキャプチャ。 |


### オーディオ関連インターフェース関数

| API | 説明|
|-----|-----|
| [startLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a05765322423454da0ad304faa7efba4a) | ローカル音声のキャプチャとアップストリームを有効にします。 |
| [stopLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | ローカル音声のキャプチャとアップストリームを無効にします。 |
| [muteLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | ローカル音声をミュート/ミュート解除します。 |
| [muteRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | 指定リモートユーザーの音声をミュート/ミュート解除します。 |
| [muteAllRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | 全ユーザーの音声をミュート/ミュート解除します。 |
| [setRemoteAudioVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac49fa4a92105f01e2e296b20881a8324) | 特定のリモートユーザーの再生音量を設定します。 |
| [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | SDKがキャプチャする音量を設定します。 |
| [getAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | SDKがキャプチャする音量を取得します。 |
| [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | SDKの再生音量を設定します。 |
| [getAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | SDKの再生音量を取得します。 |
| [enableAudioVolumeEvaluation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | 音声ボリュームの表示を有効または無効にします。 |
| [startAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a15b74c793aea807ef9142230c088473b) | 録音を開始します。 |
| [stopAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | 録音を停止します。 |
| [startLocalRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | ローカルレコーディングを開始します。 |
| [stopLocalRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8b9b6f0608e48c27fc7c646718cb41ba) | ローカルレコーディングを停止します。 |


### デバイス関連インターフェース関数

| API | 説明|
|-----|-----|
| [getDeviceManager](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | デバイス管理モジュールを取得します。 |


### 美顔・特殊効果および画像ウォーターマーク

| API | 説明|
|-----|-----|
| [setBeautyStyle](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | 美顔、美白、肌色補正効果のレベルを設定します。 |
| [setWaterMark](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | ウォーターマークを設定します。 |


### 音楽の特殊効果および声の特殊効果

| API | 説明|
|-----|-----|
| [getAudioEffectManager](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | サウンドエフェクト管理クラスITXAudioEffectManagerを取得します。 |
| [startSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad6a651a786871927917b087ae7094c8a) | システムのオーディオキャプチャをオンにします。 |
| [stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | システムのオーディオキャプチャをオフにします。 |
| [setSystemAudioLoopbackVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | システムのオーディオキャプチャのボリュームを設定します。 |


### 画面共有関連インターフェース関数

| API | 説明|
|-----|-----|
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0f8b23d8c48b9a056ca0e61ddcc894f) | 画面共有を開始します。 |
| [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | スクリーンキャプチャを停止します。 |
| [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | 画面共有を一時停止します。 |
| [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | 画面共有を再開します。 |
| [getScreenCaptureSources](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3777e1506f1aa806bee116e7117993b5) | 共有可能な画面のウィンドウを列挙します。startScreenCapture前の呼び出しを推奨します。 |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a) | 画面共有パラメータを設定します。この方法は画面共有中でも呼び出しが可能です。 |
| [setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abdc3d6339afd741bd8d3ed88ea551282) | 画面共有のエンコーダパラメータを設定します。 |
| [setSubStreamMixVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | 画面共有の音声ミキシングのボリュームを設定します。 |
| [addExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0edaac7111c63d9a00b7749ee0c7b137) | 指定ウィンドウを画面共有の除外リスト（exclude list）の中に加えます。除外リストに加えられたウィンドウは共有されなくなります。 |
| [removeExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a39db493034f2898788898e6669168c61) | 指定ウィンドウを画面共有の除外リストから取り除きます。 |
| [removeAllExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | すべてのウィンドウを画面共有の除外リストから取り除きます。 |
| [addIncludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a76c684e860bca4e48f06269261d73fc0) | 指定ウィンドウを画面共有の対象リスト（include list）の中に加えます。対象リストに加えられたウィンドウは、ウィンドウキャプチャエリア内にいる場合共有されます。 |
| [removeIncludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae9e324dac071b6d2bbc7b6e2a676ea05) | 指定ウィンドウを画面共有の対象リストから取り除きます。 |
| [removeAllIncludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | すべてのウィンドウを画面共有の対象リストから取り除きます。 |


### ユーザー定義キャプチャとレンダリング

| API | 説明|
|-----|-----|
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3278ac2b7b2e093ef22332cff3e6d97f) | ビデオのユーザー定義キャプチャモードを有効にします。 |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629) | 自身がキャプチャしたビデオデータをSDKに送信します。 |
| [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | オーディオのユーザー定義キャプチャモードを有効にします。このモードを有効にすると、SDKは、コーディングと送信機能のみを残し、既存のオーディオキャプチャフローの実行を停止します。[sendCustomAudioData()](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d)を使用して、ご自身がキャプチャしたオーディオデータをSDKに向けて絶えず送りこむ必要があります。 |
| [sendCustomAudioData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | SDKに自身がキャプチャしたオーディオデータを送信します。 |
| [enableMixExternalAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a896ff4b2731488821dd1ce382276ca0c) | 外部音声に対する合成によるプッシュおよび合成による再生の要否を制御します。 |
| [mixExternalAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f) | SDKにカスタマイズしたサブストリームのオーディオデータを送信します。 |
| [setLocalVideoRenderCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | ローカルビデオのカスタムレンダリングを設定します。 |
| [setRemoteVideoRenderCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | リモートビデオのカスタムレンダリングを設定します。 |
| [setAudioFrameCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | オーディオデータコールバックを設定します。 |
| [generateCustomPTS](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a33ed1b26695b6b75dc9ce78e5280cbb4) | ユーザー定義キャプチャタイムスタンプを生成します。 |


### カスタムメッセージ送信

| API | 説明|
|-----|-----|
| [sendCustomCmdMsg](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | カスタムメッセージをルーム内の全ユーザーに送信します。 |
| [sendSEIMsg](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | 小容量のカスタムデータをビデオフレーム内に埋め込ます。 |


### デバイスおよびネットワークテスト

| API | 説明|
|-----|-----|
| [startSpeedTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af86b2903b95b6e74f02d701701ce3380) | ネットワーク速度テストを開始します（通話品質に影響が出るのを避けるため、ビデオ通話中にはテストを実施しないでください）。 |
| [stopSpeedTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | ネットワーク速度テストを停止します。 |


### LOG関連インターフェース関数

| API | 説明|
|-----|-----|
| [getSDKVersion](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | SDKバージョン情報を取得します。 |
| [setLogLevel](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Log出力レベルを設定します。 |
| [setConsoleEnabled](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | コンソールでのログ出力を有効化または無効化します。 |
| [setLogCompressEnabled](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | Logのローカル圧縮を有効化または無効化します。 |
| [setLogDirPath](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | ログ保存パスを設定します。 |
| [setLogCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | ログコールバックを設定します。 |
| [showDebugView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | ダッシュボードを表示します。 |
| [callExperimentalAPI](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab15fc0877664a8ac257ca4d6e7afc7b0) | 試験的APIインターフェースを呼び出します。 |


### 使用停止インターフェース関数

| API | 説明|
|-----|-----|
| [startLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a05765322423454da0ad304faa7efba4a) | ローカル音声のキャプチャとアップストリームを有効にします。 |
| [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a50ec31c281de91903a1ef492a2ec7997) | リモートビデオ画面の表示を開始します。 |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | リモートビデオ画面の表示を停止するとともに、当該リモートユーザーのビデオデータストリームをプルしなくなります。 |
| [setLocalViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acdfe0dc822f074d5c42dfe308dc313a0) | ローカル画像のフィルモードを設定します。 |
| [setLocalViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4447783c52960cffbaedb7ccd7c456a2) | ローカル画像の時計回り回転角度を設定します。 |
| [setLocalViewMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5a04c60eb2e9997e745412374b7b8d19) | ローカルカメラプレビュー画面のミラーモードを設定します。 |
| [setRemoteViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab5be71379d671f77b99cf6ccd86cdbc7) | リモート画像のレンダリングモードを設定します。 |
| [setRemoteViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a385042d69e79468c9ef60dee8ec8cc96) | リモート画像の時計回り回転角度を設定します。 |
| [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5935a852496c1a033576cc6fbf676746) | リモートユーザーのサブストリーム画面（TRTCVideoStreamTypeSub、通常画面共有に使用）の表示を開始します。 |
| [stopRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a56a7770d90cad9141aecbd70d93af588) | リモートユーザーのサブストリーム画面（TRTCVideoStreamTypeSub、通常画面共有に使用）の表示を停止します。v8.0バージョンは廃棄されました。stopRemoteView(userId,streamType)インターフェースをご利用ください。 |
| [setRemoteSubStreamViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7832e5870431ccb0e75614b51af51205) | サブストリーム画面（TRTCVideoStreamTypeSub、通常画面共有に使用）の表示モードを設定します。 |
| [setRemoteSubStreamViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab63344839afca9bd4a890f6f609fd9e7) | サブストリーム画面（TRTCVideoStreamTypeSub、通常画面共有に使用）の時計回り回転角度を設定します。 |
| [setAudioQuality](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a742eefe8508e744918f704e2fa0d3405) | 音声品質を設定します。 |
| [setPriorRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a074579fcbcd5f4639ab40a2d5884fa3f) | 視聴者側で優先的に選択するビデオ品質を設定します。 |
| [getCameraDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ace7e563213b43c1763b1eb60d5b2e8c5) | カメラデバイスリストを取得します。 |
| [setCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af5ce3a160a7f0dc889322983f5cfa68a) | 使用したいカメラを設定します。 |
| [getCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0f4a19bdc82b81dd1e0a8ac8b735261a) | 現在使用しているカメラを取得します。 |
| [getMicDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab85ff9472d499bd740f953ccff549147) | マイクデバイスリストを取得します。 |
| [getCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5a17cc110f2b9c146df4498aa35eebc6) | 現在選択しているマイクを取得します。 |
| [setCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aded68bf47cb1e381961b0b69dde8931b) | 使用したいマイクを設定します。 |
| [getCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#addb5ea84bf67a3fdd49eee30e66f4826) | システムの現在のマイクデバイスの音量を取得します。 |
| [setCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaa35154699a59962bc065519e79761fa) | システムの現在のマイクデバイスの音量を設定します。 |
| [setCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a44453f04c53f19f65ca362a1cb55963b) | システムの現在のマイクデバイスをミュートにするか否かを設定します。 |
| [getCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac7df6f29e11ded5faf7996334d4af61b) | システムの現在のマイクデバイスがミュートか否かを取得します。 |
| [getSpeakerDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20fa0073543ed1bd1df5dbb825b408bf) | スピーカーデバイスリストを取得します。 |
| [getCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0ac0ecdbf0d077563fd6d2fb1ee65bee) | 現在のスピーカーデバイスを取得します。 |
| [setCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a768367aba35b104f8529740b86802b73) | 使用したいスピーカーを設定します。 |
| [getCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#accb2d6bc752f550b968462ba5a5c0538) | システムの現在のスピーカーデバイスの音量を取得します。 |
| [setCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae99882060b048467a0f39f13b168775f) | システムの現在のスピーカーデバイスの音量を設定します。 |
| [setCurrentSpeakerDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad8c3800ba3e2101ff63de7117dc729f3) | システムの現在のスピーカーデバイスをミュートにするか否かを設定します。 |
| [getCurrentSpeakerDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa4ec49fc0c07c04031d328db5814793f) | システムの現在のスピーカーデバイスがミュートか否かを取得します。 |
| [startCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | カメラのテストを開始します。 |
| [startCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | カメラのテストを開始します。 |
| [stopCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3cb3fd62d04b5975c9c50210e98f0a2d) | カメラのテストを停止します。v8.0バージョンは廃棄されました。ITXDeviceManager::stopCameraDeviceTestインターフェースをご利用ください。 |
| [startMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aca6add13bdd6535bed6d28407b5468af) | マイクのテストを開始します。 |
| [stopMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a29c2a5a42f65108074174e0bc58c0aee) | マイクのテストを停止します。v8.0バージョンは廃棄されました。ITXDeviceManager::stopMicDeviceTestインターフェースをご利用ください。 |
| [startSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af60f0db87d1f7001860f1bf330eeee3c) | スピーカーのテストを開始します。 |
| [stopSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa4b7a172067664fe50015c758e02a822) | スピーカーのテストを停止します。v8.0バージョンは廃棄されました。ITXDeviceManager::stopSpeakerDeviceTestインターフェースをご利用ください。 |
| [setMicVolumeOnMixing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4e3fb7ca730f15b6ab201e73e21f1260) | マイクのボリュームを設定します。 |
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0f8b23d8c48b9a056ca0e61ddcc894f2) | 画面共有を開始します。 |
| [playBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a815aa5a969dcb0617e02f955a9ee7cd4) | BGMの再生を開始します。 |
| [stopBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8eec0a8a7edf45d3b49b897286154b4f) | BGMの再生を停止します。 |
| [pauseBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed6272ead63eb14b9f64a92a59196c28) | BGMの再生を一時停止します。 |
| [resumeBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a221c73557814b71880c9a9323e3f31d2) | BGMの再生を継続します。 |
| [getBGMDuration](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a487cff035a50da09ab39e87f7488d647) | オーディオファイルの総時間を取得します。単位：ミリ秒。 |
| [setBGMPosition](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a2e2050b96d2b453e0ca83e483efec02c) | BGM再生の進行状態を設定します。 |
| [setBGMVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab651d0daff2d1b7e25b43606a4776796) | BGM再生のボリュームを設定します。 |
| [setBGMPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9c083e91e2af46503e522443a7b51b32) | BGMのローカル再生のボリュームを設定します。 |
| [setBGMPublishVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af193ff23e008485cf949d761028ce6e9) | BGMのリモート再生のボリュームを設定します。 |
| [playAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4db6f176c155c0f83d11eb302f6e1dab) | サウンドエフェクトを再生します。 |
| [setAudioEffectVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a401d82c610be2136896c0f60621d66cf) | サウンドエフェクトの音量を設定します。 |
| [stopAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a254acc2f0fe96ffcce33629eb4309877) | サウンドエフェクトを停止します。 |
| [stopAllAudioEffects](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a07a2dfd7ce4e76b28172d73ee8405dbe) | すべてのサウンドエフェクトを停止します。 |
| [setAllAudioEffectsVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a06219d65076c6c7024fab30d2516b167) | すべてのサウンドエフェクト音量を設定します。 |
| [pauseAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a2b004f3a3a7bdde7b2926930f31afa6c) | サウンドエフェクトを一時停止します。 |
| [resumeAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af10583316f15ed709247590a081b2307) | サウンドエフェクトを再開します。 |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a2) | 画面共有パラメータを設定します。 |
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac9d547341170330a70623299b366c44a) | ビデオのユーザー定義キャプチャモードを有効化します。 |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3a53ae79c1bd28825cb276c7555500fe) | TRTCVideoFrameには次の入力方式を推奨します（その他のフィールドは入力不要）。|


