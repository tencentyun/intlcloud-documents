## ITRTCCloud @ TXLiteAVSDK

### ITRTCCloudシングルトンの作成と破棄

| API | 説明 |
|-----|-----|
| [getTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac6fe6c4bad8206322a32a9d75ca835bd) | [ITRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#classManageLiteAV_1_1ITRTCCloud)シングルトンオブジェクトを取得します。 |
| [destroyTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4a0722972418aa87ae602f7e12d466ac) | [ITRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#classManageLiteAV_1_1ITRTCCloud)シングルトンオブジェクトをリリースします。 |


### TRTCCloudCallbackコールバックの設定

| API | 説明 |
|-----|-----|
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af4b26fe08378fb4d303cecbaa495e259) | コールバックインターフェース [ITRTCCloudCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#interfaceManageLiteAV_1_1ITRTCCloudCallback)を設定します。 |
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6a76c8a9f2dbbeb43285c01c4019a71d) | イベントコールバックを削除します。 |


### ルーム関連インターフェース関数

| API | 説明 |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afbb3a1e6f73f339d47368a7d620a995f) | ルームに入室します。 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a715f5b669ad1d7587ae19733d66954f3) | ルームを退室します。 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a94ab2e8a7df0c120def9d4b0c7658d84) | ロールを切り替えます。ライブストリーミングシナリオ（TRTCAppSceneLIVEおよびTRTCAppSceneVoiceChatRoom）のみに適用します。 |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0002794efb0f0d68d7928570a9e18246) | ルーム間通話をリクエストします（キャスターPK）。 |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#abd656e4c9b6a01231810ae897627e9bc) | ルーム間のマイク接続をオフにします。 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae870243f89b5829cd7ac5612ec958cdf) | オーディオビデオデータ受信モードを設定します（有効にするには入室前に設定する必要があります）。 |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0ea3a44e69394b68c5515b117fe76cf5) | ルームを切り替えます。 |


### CDN関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9968ab708775bd2908a3b39790f1319e) | Tencent CloudのライブCDNへのプッシュを開始します。 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afc00ba747be5299cd7235928a628339e) | Tencent CloudのライブCDNへのプッシュを停止します。 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af003758b499a542b1795f55f41afbd18) | 提携プロバイダクラウドのライブCDNへの転送を開始します。 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | 非Tencent Cloudアドレスへの転送を停止します。 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad7b4b8bddf959f40b644339986e41f92) | クラウドのミクスストリーミングトランスコードパラメータを設定します。 |


### ビデオ関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a74a3e5ec77196bd9bca67bf422e25b14) | ローカルビデオのプレビュー画面を起動します。 |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1ac7c1b6934150c07a7e9ee1918cfebe) | ローカルビデオプレビュー画面のウィンドウを更新します。 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | ローカルビデオのキャプチャおよびプレビューを停止します。 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad531b6af4f07d93b937901aea73d9008) | ローカルのビデオデータのプッシュを一時停止/再開します。 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa66214a9ebfbe0cd19fc9c9681e9c4b7) | プルを開始し、指定ユーザーのリモート画面を表示します。 |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a760a5a8c7df8119166f2050dde38dcea) | リモートビデオレンダリングのウィンドウを更新します。 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#add9d112f4206fd4e4f4490163f4a2da3) | リモートビデオ画面の表示を停止すると同時に、リモートユーザーのビデオデータストリームのプルを停止します。 |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aaa75cd1b98c226bb7b8a19412b204d2b) | すべてのリモートビデオ画面の表示を停止すると同時に、リモートユーザーのビデオデータストリームのプルを停止します。 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6e8bd59935a710e3e19c673671d48ab1) | 指定のリモートビデオストリームの受信を一時停止/再開します。 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a129fb0485b0ba8b002e5806e57642715) | すべてのリモートビデオストリームの受信を一時停止/再開します。 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad60c4b7c9c9c685fcf2a0e1be0cc2404) | ビデオエンコーダ関連パラメータを設定します。 |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac6c51c82c9246a562fe4dabe3b8f4c5e) | ネットワークトラフィックコントロール関連パラメータを設定します。 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a509c5bb9ed2e6c30f0a09678290bf2e8) | ローカル画像（メインストリーム）のレンダリングパラメータを設定します。 |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a291f1c48e5446135c29188f759f023cb) | ビデオコーデックが出力する画面の方向、すなわち、リモートユーザーが視聴する画面およびサーバーが録画する方向を設定します。 |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3e6dae3e385f1e15d528ec3d6f57a59c) |エンコーダが出力する画面のイメージモードを設定します。 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a46d610de4d78069b9dadc29e4674632b) | リモート画像のレンダリングモードを設定します。 |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a214f8a610feda5f192b048afd476d740) | 大小画面のデュアルチャンネルコーディングモードを有効にします。 |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af85d4c7d523c19a11f029aa81c27d05f) | 指定userIdの大画面または小画面での視聴を選択します。 |


### オーディオ関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad81ec081fa63f5bb2ba0979a405766ff) | ローカルオーディオのキャプチャとアップストリームを有効にします。 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab78601c38f1b872b03b662e6856be84c) | ローカルオーディオのキャプチャとアップストリームを無効にします。 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a16d9b4a197a7bc1955240a1ede889246) |ローカルのオーディオをミュートにします/ミュートをキャンセルします。 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a57006bbedfbbe508ad18e04021767125) | 指定のリモートユーザーの音声をミュートにします/ミュートをキャンセルします。 |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9c118b189a47109289528b3c00019649) | すべてのユーザーの音声をミュートにします/ミュートをキャンセルします。 |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a53681962139b81140f2d66abc4ea6a0f) | SDKキャプチャ音量を設定します 。 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad3dd226f138590f0e2c6b03f108c4e38) | SDKキャプチャ音量を取得します。 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | SDK再生音量を設定します。 |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#acd6e6336d8f314cef76de9da831a58dd) | SDK再生音量を取得します。 |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a28e0bc3692cbad87ee7d07f2d018b4ba) | 音量レベルのリマインダを起動/終了します。 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a38e565f1b02f28757f7a40d9ae1dcc4a) | 録音を開始します。 |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac8c12476bbcf3d691060954fcdb6ebe6) | 録音を停止します。 |


### デバイス関連インターフェース関数

| API | 説明 |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aedb2fed650caceab82b00c48585916d9) | デバイス管理モジュールを取得します。 |


### 美顔特殊効果および画像のウォーターマーク

| API | 説明 |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#add2a188f795e5a93ab00a6aee601da25) | 美顔、美白、肌の色調補正エフェクトレベルを設定します。 |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4845a45a629f050f4f5bbb295d035c41) | ウォーターマークを設定します。 |


### 音楽の特殊効果および声の特殊効果

| API                                                          | 説明 |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad3a3c7b20c5420fce97c5828d614047f) | オーディオエフェクトマネージャーITXAudioEffectManagerを取得します。 |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a966d1b9ed824365f567497b052c2ca41) | システム音声キャプチャを起動します。 |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adef486f26a2c7d74a8cccb537367e66a) | システム音声キャプチャを終了します。 |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad4f30caacc7252472ed21a17bfb4ebdd) | システム音声キャプチャの音量を設定します。 |


### 画面共有関連インターフェース関数

| API | 説明 |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac7d05e0eb209b774489a3f843081b2fb) | 画面共有を起動します。 |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | 画面キャプチャを停止します。 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | 画面共有を一時停止します。 |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | 画面共有を再開します。 |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae11fbc1c3d29f40fa29dd3c45a739a96) | 共有可能な画面ウィンドウを列挙します。startScreenCaptureの前に呼び出すことをお勧めします。 |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a766dd7fa395c2e3ae6cc26781c1ef98b) | 画面共有パラメータを設定します。画面共有中にもこの方法を呼び出すことができます。 |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a67e267ae6043ae873580a2a56306a1d8) | 画面共有のエンコーダパラメータを設定します。 |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a91d9fb6b6e037dc0d4e65b40e8bf781f) | 画面共有時の音声ミキシングの音量レベルを設定します。 |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab975f0d54e63bf810b1a92539ad78057) | 指定ウィンドウを画面共有のexcludeリストに追加します。excludeリストに追加したウィンドウは共有できなくなります。 |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3794c820d0d45cf55802b7162df063c9) | 指定ウィンドウを画面共有のexcludeリストから削除します。 |
| [removeAllExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a179d325cc9f043d049cdedc35a64497a) | すべてのウィンドウを画面共有のexcludeリストから削除します。 |

### ユーザー定義キャプチャとレンダリング

| API                                                          | 説明                            |
| ------------------------------------------------------------ | ------------------------------- |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a87dace307d0df1eb4a5801d65517f40b) | ビデオユーザー定義キャプチャモードを起動します。        |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4b0e29533e0fea8dfb1bd207ec68a577) | 自身がキャプチャしたビデオデータSDKに送信します。 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6cf1f1f480d3a6228f55d7e57ad506a8) | オーディオユーザー定義キャプチャモードを起動します。        |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a12c6c039a6ffda1519fe4fcbc6e863a0) | 自身がキャプチャしたオーディオデータをSDKに送信します。 |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a427084cbb7613b229b5b29c8a9479497) | ローカルビデオカスタムレンダリングを設定します。        |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1b795d10cdb8a959505c09c443667d59) | リモートビデオカスタムレンダリングを設定します。        |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a33d475c807ae068e71183a0de14b6cd7) | オーディオデータコールバック を設定します。              |

### カスタムメッセージの送信

| API                                                          | 説明                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a92ed9ed2ba1bd3c65c21c223aa05aab4) | カスタムメッセージをルーム内のすべてのユーザーに送信します。     |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6c64e92e73628496c4f3e35d25b4e57b) | データ量の小さなカスタムデータをビデオフレームに埋め込みます。 |


### ネットワークテスト

| API | 説明 |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af9a96c20afda0325655f5cff4878e62f) | ネットワークスピードテストを開始します（通話品質への影響を避けるため、ビデオ通話中はテストしないでください）。 |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a58d732ba648d1f9a3a460c02de79bb9b) | ネットワークスピードテストを停止します。 |

### LOG関連インターフェース関数

| API                                                          | 説明                        |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af48f494210612771269b3c3893683403) |  SDKバージョン情報を取得します。         |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab941d390cf7df8034c522edd8dd2f3eb) |  Log出力レベルを設定します。         |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a452f7778aaba21498765444f907bb0a0) | コンソールのログプリントを有効または無効にします。  |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af6d9f433c0c17ca34b040c51403865db) | Logのローカル圧縮を有効または無効にします。 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa735664fb9f7636744f4b0f3e4482669) | ログ保存パスを設定します。          |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1a5f967baf4f3772820e1c03a78447d) | ログコールバックを設定します。              |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a08d4c264ef3f43eea7616e4264a1e4e6) | ダッシュボードを表示します。                |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2a3f591a5091fa7db2158cfd7440cd68) | 試験的APIインターフェースを呼び出します。       |

### 使用停止インターフェース関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7104b3996ed49714cd34cbca71e6efb2) | マイクの音量レベルを設定します。                                       |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | 画面共有を起動します。                                               |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a177d006b52fdc3232d8ad0ef9dfbfd50) | BGMの再生を起動します。                                           |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a11004f1ba27b057985850a25307b0bec) | BGMの再生を停止します。                                           |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa4b92d4c989e99612f6c4dab03a78764) | BGMの再生を一時停止します。                                           |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aed6e8f224b5f834b1bc0c15f9701f692) | BGMの再生を継続します。                                           |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0abf49e1884aad560fb7741afc16cf64) | ミュージックファイルの総時間を取得します。単位はミリ秒です。                               |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a034da21d55333df96f1f912432d7eb64) | BGM再生の進捗を設定します。                                          |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2ce1461e15c3d000e02b3c99d126843e) | BGM再生の音量レベルを設定します。                                 |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac6c967a33924903c4f2dc6b9daf050cf) | BGMローカル再生の音量レベルを設定します。                             |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af398e75cb3334b5ed5911f74ac138949) | BGMリモート再生の音量レベルを設定します。                             |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aacf76f546a4b47abc13e046d0bd38328) | オーディオエフェクトを再生します。                                                   |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a942a6f358980c8520e2155fb4ef55bd0) | オーディオエフェクト音量を設定します。                                               |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a61561195216ac575235b67d410070563) |オーディオエフェクト を停止します。                                                   |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7066509af1de32c290b7cc297cd00f2b) | すべてのオーディオエフェクトを停止します。                                               |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a19416181cce88c58052a4eb2e87adeb8) | すべてのオーディオエフェクトの音量を設定します。                                         |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a43f83a1323cc39c1610c61cf79ab652c) | オーディオエフェクトを一時停止します。                                                   |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a23b65446d7dd9835da888b5285867629) | オーディオエフェクトを再開します。                                                   |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a45d88faf382acd56d0dd3ec8ce3744e2) | 画面共有パラメータを設定します。                                           |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3cf91279c13a4f10f8d955b0b6ed1a46) | リモートビデオ画面の表示を開始します。                                       |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a998268e8e9c857367d4ff75a3232daad) | リモートビデオ画面の表示を停止すると同時に、リモートユーザーのビデオデータストリームのプルを停止します。     |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ada1aa39d0b579f0f939d17c3ca78df92) | ローカル画像のレンダリングモードを設定します。                                     |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1dceb7f02cf974f6944c5c306b86cab6) | リモート画像のレンダリングモードを設定します。                                     |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8d5dc6995392c71257493353e3571e86) | ローカル画像の時計回りの回転角度を設定します。                               |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0290931f9fb237a9ab38c37d5e911a54) | リモート画像の時計回りの回転角度を設定します。                               |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a050a53b8bed638f76a64ad82ecd89078) | ローカルカメラプレビュー画面のイメージモードを設定します。                           |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5c153269c676a12b20327f9600f9206d) | リモートユーザーのサブストリーム画面（TRTCVideoStreamTypeSub、通常は画面共有に使用）の表示を開始します。 |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a41c333a00cc151c909b7d0fe4f4b34b5) | リモートユーザーのサブストリーム画面（TRTCVideoStreamTypeSub、通常は画面共有に使用）の表示を停止します。 |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8ee2941c51edc2218fa224c03b650a78) | サブストリーム画面（TRTCVideoStreamTypeSub、通常は画面共有に使用）の表示モードを設定します。 |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7edb64ac7d4e6755d7f79d75d94770fd) | サブストリーム画面（TRTCVideoStreamTypeSub、通常は画面共有に使用）の時計回りの回転角度を設定します。 |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5cc9f8652845ff0d7adc5b2d24b8a269) | 視聴者が優先的に選択するビデオ品質を設定します。                               |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae241d03683fdde1e033078a6057f609c) | オーディオ品質を設定します。                                               |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3177329bc84e94727a1be97563800beb) | ローカルオーディオのキャプチャとアップストリームを有効にします。                                   |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae9b8a8e04f14a10827af80c6cf3fd390) | カメラデバイスリストを取得します。                                         |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afc1cb1512326ff70fd2f303726af9475) | 使用したいカメラを設定します。                                         |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3cd193c8867f5332297e0d664b2a9516) | 現在使用するカメラを取得します。                                       |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aae179b7da159ec44d748345cb79cb645) | マイクデバイスリストを取得します。                                         |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5bcd6e1c8526f2ffb4a04477bdd84abb) | 現在選択しているマイクを取得します。                                       |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2591a4c670807e507a1cd70a0c574df7) | 使用したいマイクを設定します。                                         |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad86183c23657588ef232a6d9796e11c0) | システムの現在のマイクデバイスの音量を取得します。                                 |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a585cb97ea5fbf80bb7f57f3fa2a49c27) | システムの現在のマイクデバイスの音量を設定します。                               |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2e69c8cefc75cd5a0bb6277d83faba4a) | スピーカーデバイスリストを取得します。                                         |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4a9c4c8a642976a234b1a5ce607e370d) | 現在のスピーカーデバイスを取得します。                                       |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3881585d770b639260437b3127c6a5d7) | 使用したいスピーカーを設定します。                                         |
| [getCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad83afd5da873a7b6c690c02c3f5d32a4) | システムの現在のスピーカーデバイスの音量を取得します。                                 |
| [setCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a72a814a76c9a16cbf5cfdeefdb37ca13) | システムの現在のスピーカーデバイスの音量を設定します。                                 |
| [startCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adfdfd81465003ac6d21e5be20c119c41) | カメラテストを開始します。                                         |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1b67fa3f322efe538d924b381c06e676) | カメラテストを停止します。                                             |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0bab0a75a4f96746974918126255c66c) | マイクテストを開始します。                                             |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8cca1c5913ac021987680195075e5fc9) | マイクテストを停止します。                                             |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac7f15eee92377d3bb5d1b7ec5e99d3be) | スピーカーテストを開始します。                                             |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#abf383f971dc54f0254b2d40f100cc9ca) | スピーカーテストを停止します。                                             |


## TRTCCloudCallback @ TXLiteAVSDK

Tencent Cloudビデオ通話機能のコールバックインターフェース。

### エラーイベントおよび警告イベント

| API | 説明 |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7c34b7b7918c7db1a2b3fb4dbf90213d) | エラーコールバックです。SDKがリカバリー不能なエラーは、監視する必要があり、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。 |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aad50ebc5637840fecd88ae1fed6510a5) | 警告コールバック：ラグやリカバリー不能なデコードの失敗など、非常に重大な問題を告知するために使用されます。 |

### ルームイベントコールバック

| API                                                          | 説明                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9540be761c1563aa2d8eddb62ccb5578) | 入室済みのコールバック。                  |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad5ac26478033ea9c0339462c69f9c89e) | 退室のイベントコールバック。                |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a720d216a5b81d02669810cab9e9f3232) | ロール切り替え結果のコールバック。                  |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a4fb0e99751e6c15a1e5f702e643640b9) | ルーム間通話（キャスターPK）リクエスト結果のコールバック。 |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a53d2f8b13139a59202cb198bc92deb85) | ルーム間通話（キャスターPK）終了結果のコールバック。 |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6b698ae14a2bf21542bce4be4ea09610) | ルーム切り替え(switchRoom)結果のコールバック。  |

### メンバーイベントコールバック

| API                                                          | 説明                                             |
| ------------------------------------------------------------ | ------------------------------------------------ |
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a966b16d2f3042c0c45d9f372126c455a) | ユーザーが現在のルームに入室します。                             |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a2a84fc3062a578584f219210f6b9bba7) | ユーザーが現在のルームを退室します。                             |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad76012a12ae044c3a30e248070eb0fb2) | ユーザーはカメラとビデオを有効にしていますか。                         |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a52ad5b09959df6e940aec7fb9615de9c) | ユーザーは画面共有を有効にしていますか。                           |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#abd6c0a2a5994b95d7d467deaacf36269) | ユーザーはオーディオアップストリームを有効にしていますか。                           |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a04e7917781c8cd3fec23a976acf05f80) |ローカルまたはリモートユーザーの最初のフレーム画面のレンダリングを開始します。               |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1942830ce2261dc25f80e973cd104fd8) | リモートユーザーの最初のフレームのオーディオ再生を開始します（現在、ローカル音声は通知しません）。 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a266f7551ab47384616b36ad2783615d1) | 最初のフレームのローカルビデオデータが送信されました。                     |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#acb73daf4ce82cd03f787f057b233b412) | 最初のフレームのローカルオーディオデータが送信されました。                     |


### 統計および品質コールバック

| API | 説明 |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aa7694d95e5c47ec79dd06572a8a89c94) | ネットワーク品質：このコールバックは2秒ごとに1度トリガーされ、現在のネットワークのアップストリームとダウンストリーム品質を統計します。 |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a61c2b1f320733667a5208e424998b886) | 技術指標統計のコールバックです。 |

### サーバーイベントコールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aed43a70b4a95eb95181e2b410013bf54) | SDKがサーバーとの接続を切断します。                                     |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | SDKがサーバーへの再接続を試行中です。                                   |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | SDKがサーバーとの接続を再開します。                                     |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6c3984e5bf71912718638884107ad408) | サーバースピードテストのコールバックです。SDKは複数のサーバーIPに対するスピードテストを実行し、IPごとのスピードテスト結果をこのコールバックを介して通知します。 |

### ハードウェアデバイスイベントコールバック

| API                                                          | 説明                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aaa74021e5fd2564afb2df50e25eedeff) | カメラの準備が完了しました。                                            |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#afdac7dee94451913a4dc9982badc8035) | マイクの準備が完了しました。                                            |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aa6b7c420cd4effacaf16eb73a5da288f) | 音量レベルをリマインドするためのコールバックです。userIdごとの音量とリモートの総音量が含まれます。 |
| [onDeviceChange](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#acda9040715f8a332d36ca9d6e4015ff9) | ローカルデバイスオン/オフのコールバック。                                          |
| [onTestMicVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a24817d5d5810778ea1e3465d6ac3609c) | マイクテスト音量のコールバック。                                        |
| [onTestSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a03f4eb9af917dcc5d62717f1c1940ffc) | スピーカーテスト音量のコールバック。                                        |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a28d95bff7fe7a5c8062e07e92dffd02d) | 現在のオーディオキャプチャデバイスの音量変更通知。                              |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a79f4f4302849a5c71892986a93b17246) | 現在のオーディオ再生デバイスの音量変更通知。                              |


### カスタムメッセージ受信のコールバック

| API | 説明 |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a139d77ca75e7baee6a9017beca20fff3) | カスタムメッセージ受信のコールバックです。 |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a048194ab37bec16c6ee068ac7ee9fef3) | カスタムメッセージ消失のコールバックです。 |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9c16a1ce79d6d50c3576330d0493fd1b) | SEIメッセージ受信のコールバックです。 |

### CDNバイパス転送コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a765ef1ca062295a1d84ac262e27ed5a8) | Tencent CloudのライブCDNへのプッシュ開始のコールバックです。TRTCCloudのstartPublishing()インターフェースに対応します。 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a47a960139fb4732ff90999fa79139544) | Tencent CloudのライブCDNへのプッシュ停止のコールバックです。TRTCCloudのstopPublishing()インターフェースに対応します。 |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9cb1e74a2446045924d8959e7232732e) | CDNへのRelayed Push起動完了のコールバックです。                              |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1b9f3dab153a4b9d84217de1c590d25b) | CDNへのRelayed Push停止完了のコールバックです。                              |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a0f02456093b0a82629695ec15c945e88) | クラウドのミクスストリーミングトランスコードパラメータ設定のコールバックです。TRTCCloudのsetMixTranscodingConfig()インターフェースに対応します。 |

### 画面共有コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onScreenCaptureCovered](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aca39d43f65ee8d5007ce075d8c808dc1) | SDKは画面共有ウィンドウがブロックされ、正常にキャプチャできないことをこのコールバックを介して通知します。このコールバックでユーザーにウィンドウのブロックを解除するよう通知できます。 |
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7d15537d26fb001045ff95157d59ed3f) | SDKは画面共有の開始を、このコールバックを介して通知します。                     |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9e49f6e6887d63e3e817033681f0ad95) | SDKは画面共有の一時停止を、このコールバックを介して通知します。                     |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a399959bd81e349cb76c9b7c939202410) | SDKは画面共有の再開を、このコールバックを介して通知します。                     |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad0c359a7cefb8f246d498a3fbf52b1ac) | SDKは画面共有の停止を、このコールバックを介して通知します。                     |

### 使用停止インターフェースコールバック

| API                                                          | 説明                                   |
| ------------------------------------------------------------ | -------------------------------------- |
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a3d806371c6912d889e9e0bc198e2d2bd) | 破棄されたインターフェース：キャスターが現在のルームに入室します。         |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1d6099d0439eec6c44abfe166ccb8aee) | 破棄されたインターフェース：ユーザー（キャスター）が現在のルームを退室します。 |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#abe967d855abae66836877fe0dacf8b5f) | 破棄されたインターフェース：オーディオエフェクト再生終了のコールバックです。           |
| [onPlayBGMBegin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a61d9fa641b1790094e955aeb355cca92) | 破棄されたインターフェース：BGMの再生を開始します。           |
| [onPlayBGMProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6ce46d86ba3f04613c8c3eb16f96ae44) | 破棄されたインターフェース：BGM再生の進捗です。         |
| [onPlayBGMComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aff8d7c6c3d2a5984ddd6448008041340) | 破棄されたインターフェース：BGM再生の終了です。           |


### ビデオデータフレームのカスタム処理コールバック

| API | 説明 |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a473b28cb74e44a9629c21b64ca23bf98) | カスタムビデオレンダリングのコールバックです。 |


### 音声データフレームのカスタム処理コールバック（読み取り専用）

コールバック関数はSDK内部スレッドで同期的にスローされます。時間のかかる操作は行わないでください。 
>?不必要な性能ロスを減らすため、必要に応じて関連する関数の実装を定義してください。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCapturedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a329db3f999a740633c2446368f9babb0) | ローカルマイクがキャプチャしたオーディオデータのコールバックです。                             |
| [onPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a12f83dbce03e0770d09f9910e58ec72c) | 音声ミキシング前のリモートユーザーごとのオーディオデータ（たとえば、特定の音声をテキストに変換する場合は、ミキシング後のデータではなく、このオリジナルデータを使用する必要があります）。 |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1e620894f820b28e94d644cfcdea3c17) | 各オーディオデータミキシング後にスピーカーに送信され再生されるオーディオデータです。                   |

### ログ関連コールバック

| API | 説明 |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ab96d17528679cb05cf1f28978b2cf432) | ログプリント時のコールバックです。 |


## 主要なタイプの定義

| タイプ名 | 説明 |
|-----|-----|
| [TRTCImageBuffer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a115d7544222e40e31d1766f7770f4619) | 画像のキャッシュです。 |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a78b6e0861f6c951b7269e5b0e13b8c36) | 画面キャプチャ情報です。 |
| [SIZE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1SIZE) | bufferの長さと幅を記録します。 |
| [ITRTCScreenCaptureSourceList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#interfaceManageLiteAV_1_1ITRTCScreenCaptureSourceList) | 画面ウィンドウリストです。 |
| [ITRTCDeviceCollection](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__csharp.html#interfaceManageLiteAV_1_1ITRTCDeviceCollection) | デバイスリストです。 |
| [ITRTCDeviceInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__csharp.html#interfaceManageLiteAV_1_1ITRTCDeviceInfo) | デバイスItem情報です。 |
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | 入室関連パラメータです。 |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a43a83bd5122296aa87cc7f6e964921c5) | ビデオコーデックパラメータ。 |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a7cd5c078b248a32557a85226f1d30697) | ネットワークトラフィックコントロール関連パラメータです。 |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#af6aab62536869726ee32b158ddbbf5ce) | ビデオ品質です。 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#abdeba26e639757957fd75f528ba14f6e) | 音量レベルです。 |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a0f5d7607bc170be903d207b4e0c87fab) | ビデオフレームデータです。 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a3c9f428bf1fc390b37a9c74accf226c6) | オーディオフレームデータです。 |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a8858167e09ab4d55f5e49c89bd4a1848) | ネットワークスピードテスト結果です。 |
| [RECT](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1RECT) |長方形の4点の座標を記録します。 |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#ac5b1947f21f77726cbff822eaf0003f9) | クラウドミクスストリーミングにおける各サブ画面の位置情報です。 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a6066a5537ad8c1bc6158d43e8a4765db) | クラウドミクスストリーミング（トランスコード）の設定です。 |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a0b977361cb4d84b1ece0b26c949dcde6) | CDN Relayed Pushパラメータです。 |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a724e3aa5cbc2249b7ce31bd7f9362d7b) | レコーディングパラメータです。 |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCAudioEffectParam) | オーディオエフェクト再生です。 |
| [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCLocalStatistics) | 自身のローカルオーディオビデオ統計情報です。 |
| [TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCRemoteStatistics) | リモートメンバーのオーディオビデオ統計情報です。 |
| [TRTCStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCStatistics) | 統計データです。 |

