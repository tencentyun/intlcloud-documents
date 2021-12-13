## TRTCCloud @ TXLiteAVSDK

### インスタンスの作成およびイベントコールバック
| API | 説明 |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac5da416bb06d461c7e1e555e3fd143ee) | TRTCCloudインスタンスの作成（シングルトンモード） |
| [destroySharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a69e76ca12b727c7cbcbdda274fc007a2) | TRTCCloudインスタンスを破棄 （シングルトンモード）  |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a22fe2f31f2ef62fb3c6cba083dc6c016) | TRTCイベントコールバックを設定 |
| [setListenerHandler](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a48c867145dcc09289f7af41871b4fdd9) | TRTCCloudDelegate イベントコールバックを起動するキューを設定 |

### ルーム関連インターフェース関数
| API | 説明 |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) | ルームに入室 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) | ルームを退室 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) | ロールの切り替え |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09fbe471def0c1790357fc2b70149784) | ルームの切り替え |
| [ConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) | ルーム間通話のリクエスト |
| [DisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af777ac398ac47c8e5649c983fa2053fa) | ルーム間通話を退出 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) | サブスクライブモードを設定（有効にするには入室前に設定する必要があります） |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3c4a93d24e0ef076168b44cf3545a8d4) | サブルーム事例の作成（複数のルームで同時視聴するために使用されます） |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6dc091ead812c50497c4b4e87e5c2fcf) | サブルーム事例の破棄 |

### CDN関連インターフェース関数
| API | 説明 |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c168a9aa35ccd0b24981526425e4730) |Tencent Cloud CSS CDNへのオーディオビデオストリーミングの公開を開始 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3067efa528fb9ffb8cf7685ce29925d4) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングの公開を停止 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41aefb8be652f8f6803020e543acaadc) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開を開始 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0e1e8a1eb1cac3f5e5d4433b4aa21e8e) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開を停止 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af7cf5544f9b8027e9526c32319a13838) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータを設定|

### ビデオ関連インターフェース関数
| API | 説明 |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) | ローカルカメラのプレビュー画面を有効化（モバイル端末） |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae91432ada1767f793c460c7b897b6809) | ローカルカメラのプレビュー画面を更新 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af6ee50bf2c4c592294061077fc727505) | カメラのプレビューを停止 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | ローカルのビデオストリームの公開を一時停止/再開 |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d) | ローカル画面の一時停止中の代替画像を設定 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) | リモートユーザーのビデオストリームをサブスクライブし、ビデオレンダリングウィジェットをバインド |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9be8a4c5ea4da16fb1ca42e8e258effd) | リモートユーザーのビデオレンダリングウィジェットを更新 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | リモートユーザーのビデオストリームのサブスクライブを停止し、レンダリングウィジェットをリリース |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) | すべてのリモートユーザーのビデオストリームのサブスクライブを停止し、すべてのレンダリングリソースをリリース |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | リモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2d8a7b74068026a85158262cc9aedd66) | すべてのリモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) | ビデオエンコーダのエンコードパラメータを設定|
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a02631a5e4251657875535c38ab319239) | ネットワーク品質モニタリングの関連パラメータを設定 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a916eab6c78587300165008f61a473f8b) | ローカル画面のレンダリングパラメータを設定 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2e37d4b9555c58148ad507938375505f) | リモート画面のレンダリングモードを設定 |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272afecae1d291033cb9cd4b1d7b52e0) | ビデオエンコーダが出力する画面の方向を設定 |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a32d9ba3696b305373508253f9bee8236) | エンコーダが出力する画面のイメージモードを設定 |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abbbe1548bfba0bd082a08478ce35e9bc) | 重力センサーの適合モードを設定 |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3a040c5012cf572b9dfabcca87f2cbb7) | 大小画面のデュアルチャンネルコーディングモード を有効化 |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2a018cc1010587ea9b0fbd791eb3c54f) | 指定リモートユーザーの大小画面を切り替え |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae75285c95fc53651e24fa23c4141093b) | ビデオ画面のスクリーンキャプチャ |

### オーディオ関連インターフェース関数
| API | 説明 |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | ローカルオーディオのキャプチャおよび公開を有効化 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272bba21d046347ac42d76069ba5972c) | ローカルオーディオのキャプチャおよび公開を停止 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86) | ローカルのオーディオストリームの公開を一時停止/再開 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) | リモートのオーディオストリームの再生を一時停止/再開 |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) | すべてのリモートユーザーのオーディオストリームの再生を一時停止/再開 |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4a3dda74823afa597b42b981257e9e22) | オーディオルートを設定 |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3dabe4a4e13509cf1bd5b3d58aabaa06) | 特定リモートユーザーの音声再生音量を設定|
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6af5e2c4819a683042f382688aff41e9) | ローカルオーディオのキャプチャ音量を設定 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a81037b960fb2b3501b1e8e60f2b5f9f3) | ローカルオーディオのキャプチャ音量を取得 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b20e1eec637c82190c5264d78d686af) | リモートオーディオの再生音量を設定|
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5a1636fa1300b0b4e2829846c36450a2) | リモートオーディオの再生音量を取得 |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a43e99323fd5680fd377b95b97f0885c3) | 音声レベルのプロンプトを起動 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8b04666d32535637308605d5e15b7220) | 録音を開始 |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7d55e5f15d1291afc89f7e1dfe0a25d8) | 録音を停止 |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5d6bf60e9d3051f601988e55106b296c) | ローカルメディアのレコーディングを有効化 |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae982c3c04c0195711ee4e56132522c4b) | ローカルメディアのレコーディングを停止 |

### デバイス管理関連インターフェース
| API | 説明 |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae66395bc404d205fcd7fe9082ca85ce9) | デバイス管理タイプ（TXDeviceManager）を取得 |

### 美顔特殊効果および画像のウォーターマーク
| API | 説明 |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) | 美顔管理タイプ（TXBeautyManager）を取得 |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1083aaf0441e3d90ce6641d278a97a63) | ウォーターマークの追加 |

### BGMおよび音声の特殊効果
| API | 説明 |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) | オーディオエフェクトマネージャー（TXAudioEffectManager）を取得|

### 画面共有関連インターフェース
| API | 説明 |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | 画面共有を起動|
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab6c3014f6f88c775aa91fccea19ce8a4) | 画面共有を停止 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) | 画面共有を一時停止 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) | 画面共有を再開 |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a34d994fbba559994aaf3a1f20420a885) | 画面共有（サブストリーム）のビデオコーデックパラメータを設定（このインターフェースはデスクトップシステムのみをサポート） |

### ユーザー定義キャプチャおよびカスタムレンダリング
| API | 説明 |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | ビデオユーザー定義キャプチャモード の起動/終了 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | 自身がキャプチャしたビデオフレームをSDKに送信 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a206b9ce3594aa535b633d4f7c8f97210) | オーディオのユーザー定義キャプチャモードを起動|
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a30a542b7d540c8699595a22ca3401f29) | 自身がキャプチャしたオーディオデータをSDKに送信 |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7b7d3707d2ed8e8f1221faf73af49027) |ユーザー定義のオーディオトラックの起動/終了 |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a899a1e9d42c9bf9ce1474aec13ac6747) | ユーザー定義のオーディオトラックをSDKにミキシング|
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a362490afb9028595635b52d041a2bfb0) | プッシュ時にミキシングする外部オーディオのプッシュ音量および再生音量を設定 |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b36383129314d70f150c08de182e2b8) | ユーザー定義キャプチャ時のタイムスタンプを発行 |
| [setLocalVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b565dc8c77df7fb826f0c45d8ad2d85) | サードパーティによる美顔のビデオデータコールバックを設定 |
| [setLocalVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa3cbb7a501c3151d94473965e2538c7a) | ローカルビデオカスタムレンダリングコールバックを設定|
| [setRemoteVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4fca6803d13e4c7ff00dcac2974637e4) | リモートビデオカスタムレンダリングコールバックを設定 |
| [setAudioFrameListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034b6fce9a517267acd874c243efc575) | オーディオデータカスタムコールバックを設定 |
| [setCapturedRawAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9047b34857b12d85688b3b3f1ca1c3f0) | ローカルマイクによってキャプチャされたオリジナルオーディオフレームコールバック形式を設定 |
| [setLocalProcessedAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac0f65e13815edc05ebd765826a94e3dc) | 前処理後のローカルオーディオフレームコールバック形式を設定 |
| [setMixedPlayAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a98a2e38d75366fbc2c4da92fec5c0a30) | 最終的にシステムから再生したいオーディオフレームコールバック形式を設定 |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803) | オーディオカスタム再生を有効化 |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c1c268173ab9b1bc24d34766e433931) | 再生可能なオーディオデータを取得 |

### カスタムメッセージ送信インターフェース
| API | 説明 |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa4847ad53acc9ab5990194b21ff5b070) |UDPチャネルを利用してカスタムメッセージをルーム内のすべてのユーザーに送信   |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034f9e1effbdadf8b9bfb7f3f06486c4) |  SEIチャネルを利用して送信カスタムメッセージをルーム内のすべてのユーザーに送信  |

### ネットワークテストインターフェース
| API | 説明 |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0dbceb18d61d99ca33e967427dd0a344) |ネットワークスピードテストを開始（ルーム入室前に使用） |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3e862cef0e818ddecdc3dc4d66a6f8f9) | ネットワークスピードテストを停止 |

### デバック関連インターフェース
| API | 説明 |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aeb5168abbd62c631b65247e6289d1e2d) | SDKのバージョン情報を取得 |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0ec9520dda7e2062f7455956d093113b) | Log出力レベルを設定 |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2942d9d05045d3f0e0add45a3e10b3ee) | コンソールのログプリントを有効化/無効化 |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a495d2122a4098ab371d825c1f0bb90f5) | ログのローカル圧縮を有効化/無効化 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a44c20358d08da798e0f15d142c9c3914) | ローカルログの保存パスを設定 |
| [setLogListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a299a71f4addb3638c7790de446fbdf37) | ログコールバックを設定 |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2cdb5d447114534f53bad5bdc48afba) | ダッシュボードを表示 |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa2014c293033e9ea60aa6ffd525ee2fa) | ダッシュボードのマージンを設定 |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f331dd0cfff51ab5a3becf4950a55e) | 試験的インターフェースの呼び出し |
| [setNetEnv](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a28ae49c86c5e5ba7e5ad2eae171bde76) | TRTCのバックエンドクラスターを設定(Tencent Cloud研究開発チームのみに適用) |

### 破棄されたインターフェース
| API | 説明 |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab356494d1b7dd924be69b23aa631a85a) | マイクの音量レベルを設定 |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) | 美顔、美白および肌の色調補正エフェクトレベルを設定 |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4ff69ce783f648f23dd737641344ac52) | デカ目レベルを設定 |
| [setFaceSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78a159a2a45d24dbd5722eb73d237e8a) | 小顔レベルを設定 |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a58bb7ce1fbbc40a50647d64693ac5d41) | フェイスシェイプレベルを設定 |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a774eb948494cecec024771434ccd9d3c) | 下あご引き伸ばしまたは縮小幅を設定 |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa14091f0d02330cbd02da5186e9dd874) | 面長修正レベルを設定 |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3f806534b2596d7e29ea0ea6c070b591) |小鼻レベルを設定|
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a521a0446d0922d480a1eec4b86f1ecb2) | 動的エフェクトステッカーを設定 |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a066cbf8f4f6c1cd23fe9451b82c5a073) | 動的エフェクトミュートを設定 |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a925323ab809957ccaeb4cef30841cb72) | カラーフィルターエフェクトを設定 |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5fb4c8bc9948e61a75b9ef85f618309d) | カラーフィルター濃度を設定 |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aef56a36b901d5e525ee539e7d5642063) | クロマキー背景ビデオを設定 |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3df738557f5c658c37174ac9aeae9684) | BGMの再生を起動 |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3ee7bdd15de4ba9010aa5ece3abff0ab) | BGMの再生を停止 |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a21ddee03e6f4cec028a24e5d5e30955e) | BGMの再生を停止 |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aaa8b34ef2b334bd22a1cb6541a4c6702) | BGMの再生を停止 |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae7342a8bcfda22a872aa684f06a4677f) | BGMの総時間を取得（単位：ミリ秒） |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78f901b6175352a31b0236776bfdc661) | BGM再生の進捗を設定 |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ada9c2b4aaf9a1a9ab9cd846593fdf9e6) | BGMの音量レベルを設定 |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab1e1c94c9efd967dbffb46d3ba08fef5) | BGMのローカル再生音量を設定 |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a535eab48f9df390f4de5ebd5afcd59e3) | BGMのリモート再生音量を設定 |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6f4f89be3c810acfa2430ad65fd7ea68) | リバーブエフェクトを設定|
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37acaf3b2539e0b1c18123a646e91189) | ボイスチェンジタイプを設定 |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad1ed7667282eccfac1992c1e547a5aeb) | オーディオエフェクトを再生 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | オーディオエフェクトの音量を設定 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | オーディオエフェクトの再生を停止|
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a770543c80d3a5629a26d1382535fb6c4) | すべてのオーディオエフェクトを停止 |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9bb41c4ff1a5b24ca742fe3ce45a2bc0) | すべてのオーディオエフェクト音量を設定 |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab32923d04ce164b82879b3e05833959f) | オーディオエフェクトを一時停止 |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a33ab6e798d3da245435166464b702d4f) | オーディオエフェクトを一時停止|
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9306bca7c6a13e0443a3fa1b40c9f343) | インイヤーモニタリングを有効化（または無効化） |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) |リモートビデオ画面の表示を開始 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | リモートビデオ画面の表示を停止すると同時に、このリモートユーザーのビデオデータストリームのプルを停止 |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) | リモート画像のレンダリングモードを設定 |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8478d804d2a07520ce2bc5466b727839) | リモート画像の時計回りの回転角度を設定 |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) | ローカル画像のレンダリングモードを設定 |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69) | ローカル画像の時計回りの回転角度を設定 |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1) | ローカルカメラプレビュー画面のイメージモードを設定 |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#acdbe3829d20f58cedd5a0c2f49ea24dc) | リモートユーザーのサブストリーム画面の表示を開始 |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae5f540d795425046c9166b0a2361a8de) | リモートユーザーのサブストリーム画面の表示を停止 |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a73f66e66ffee44e19ebb4d8c56c89718) | サブストリーム画面の塗りつぶしモードを設定 |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#affdf177b468fdf40a41782e2e47524cc) | サブストリーム画面の時計回りの回転角度を設定 |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2efc2703c86ee009bd4a1d440d0c1e0) | 大画面または小画面の視聴優先順位を設定|
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55) | オーディオ品質を設定 |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | オーディオ品質を設定 |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1b43a65a32f9dcb81b39b9c51c5bc4c6) | カメラの切り替え |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac7ae26eca2f9a673121803d6d175b034) | 現在のカメラがズームをサポートしているかどうかを照会 |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9f761eebdf04f724e0d1591c41c6045f) | カメラズームの倍数（フォーカス距離）を設定 ） |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a645183ba7c0cea748973796cb38aad8c) | フラッシュの切り替えをサポートしているかどうかを照会 |
| [enableTorch](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09253f6547914d54058831b61325e770) | フラッシュのオン/オフ |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abd39aca40adfc8da6beaf32141f84cfa) | カメラがフォーカスの設定をサポートしているかどうかを照会 |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa7c65fb033727804e7a79b8f135c776c) | カメラのフォーカス座標位置を設定 |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a23f25ffb81215a32517da78455459ff2) | 顔の位置の自動認識をサポートしているかどうかを照会 |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5438dcc45dc2f26a3771a5feddcdef5d) | システムの音量タイプを設定 |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | ビデオユーザー定義キャプチャモード の起動|
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | 自身がキャプチャしたビデオデータを送信 |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | 画面共有を起動（Android） |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | ローカルのビデオストリームの公開を一時停止/再開 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | リモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |

### エラーおよび警告イベント
| API | 説明 |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a511d0007e1990e63e853e46ce3f02670) | エラーイベントコールバック |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9871472ee8195dfc5d0c34fae3294465) | 警告イベントコールバック |

### ルーム関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) | 入室成功または失敗のイベントコールバック |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) | 退室のイベントコールバック |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6a4b7f39bc5dfb0c5d75ef8802e2e758) | ロール切り替えのイベントコールバック |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9778a84932f02de9be52ea7513f606c1) | ルーム切り替え結果のコールバック|
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) | ルーム間通話リクエスト結果のコールバック|
| [onDisConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6f7db4f0aaadad2cdfa822ba0060414c) | ルーム間通話終了結果のコールバック|

### ユーザー関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a891f38e4cdeaf3ff18937726f0269c2c) | ユーザーが現在のルームに入室 |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abfec3607f97823956fad77a7a63dc441) | ユーザーが現在のルームを退室 |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) | リモートユーザーが公開/キャンセルしたビッグストリームのビデオ画面 |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390) | リモートユーザーが公開/キャンセルしたサブストリームのビデオ画面 |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) | リモートユーザーが公開/キャンセルした自身のオーディオ |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0c1ccf1bec2d3261e9f11894b32e357e) | SDKが自身のローカルユーザーまたはリモートユーザーの最初のフレーム画面のレンダリングを開始 |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a3516aaef4cb63e512cd713e4ec96d118) | SDKがリモートユーザーの最初のフレームのオーディオの再生を開始 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a181788d7441d41022ce014095ee05353) |自身のローカルの最初のビデオフレームが公開済み |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#acb73daf4ce82cd03f787f057b233b412) | 自身のローカルの最初のオーディオフレームが公開済み |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aa75cd2a93cfb096357e2de226ff2ea47) |リモートビデオステータス変更のイベントコールバック |

### ネットワークおよび技術指標統計のコールバック
| API | 説明 |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b) |ネットワーク品質のリアルタイム統計のコールバック |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a24a6ee3b3709a42af226be7258521612) | オーディオビデオ技術指標のリアルタイム統計のコールバック |

### クラウドとの接続状況のイベントコールバック
| API | 説明 |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aed43a70b4a95eb95181e2b410013bf54) | SDKがクラウドとの接続を切断済み |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | SDKがクラウドとの再接続を試行中 |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a36d96a42ec4b00a0e3808f7f8460cd7f) |SDKがクラウドとの接続を再開済み |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ab77a0dff287e1642527cd414fc5fe5f5) | サーバースピードテストの結果のコールバック |

### ハードウェアデバイス関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aaa74021e5fd2564afb2df50e25eedeff) | カメラの準備完了 |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#afdac7dee94451913a4dc9982badc8035) | マイクの準備完了 |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1a608275247d2912e26bd83f648d6378) | 現在のオーディオルートに変更発生（モバイルデバイスのみに適用） |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4e3b79968ccbb86de5b79e326a2daafa) | 音量レベルフィードバックのコールバック |

### カスタムメッセージ受信イベントコールバック
| API | 説明 |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a51fd654c5ec030ff84f208f2ba50298d) | カスタムメッセージ受信のイベントコールバック|
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a98af11ba5b25d3124bd9533dc5197127) | カスタムメッセージ消失のイベントコールバック |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3640e6bf80a1f93991644701e9b0d96) | SEIメッセージ受信のコールバック |

### CDN関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a03d0ef687b2973b9b13cb041bd35bb85) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングのイベントコールバックの公開を開始 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3cb7e5ceb69954d762eafca5a0e3a62) |Tencent Cloud CSS CDNへのオーディオビデオストリーミングのイベントコールバックの公開を停止 |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a64df36d6c56dd69d8b6f051fd9fffcbc) | 非Tencent Cloud CDNへのオーディオビデオストリーミングのイベントコールバックの公開を開始 |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c3d63538897ddb9ed1b170819c41dca) | 非Tencent Cloud CDNへのオーディオビデオストリーミングのイベントコールバックの公開を停止 |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af1c79a5ec3e0c106939e7f0d7849d694) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータ設定のイベントコールバック |

### 画面共有関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a7d15537d26fb001045ff95157d59ed3f) | 画面共有開始のイベントコールバック |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a12c57991389e32f04a56774df5d1ce76) | 画面共有一時停止のイベントコールバック |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ade88963a254d297d3be1993e8a599f6e) | 画面共有再開のイベントコールバック |
| [onScreenCaptureStopped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c09b21b733da7d314d1db2cb03c8bcb) | 画面共有停止のイベントコールバック |

### ローカルレコーディングおよびローカルスクリーンキャプチャのイベントコールバック
| API | 説明 |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6d252931944577cc08d40db1f5ecd7bb) | ローカルレコーディングタスク開始済みのイベントコールバック |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22f09234dc198d33fa38bbb595fb5764) | ローカルレコーディングタスク実行中の進捗のイベントコールバック |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0a3eef0daeb5107290cb5190ceb9467b) | ローカルレコーディングタスク完了済みのイベントコールバック |

### 破棄されたイベントコールバック
| API | 説明 |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aff18b3bc5b1e448b21b7614e5716e73e) | キャスターが現在のルームに入室（破棄済み） |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0d1361e52e96b4c7c1a5f1b89f4ef0fb) | キャスターが現在のルームを退室（破棄済み） |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abe967d855abae66836877fe0dacf8b5f) | オーディオエフェクト再生が完了済み（破棄済み） |

### ビデオデータカスタムコールバック
| API | 説明 |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a41b44f9b0583bbf56ad9e96065ea825c) | カスタムビデオレンダリングのコールバック |
| [onGLContextCreated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af4a7a3a4e4945bf216d87f81b6926dab) | SDK内部のOpenGL環境作成済みの通知 |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22afb08b2a1a18563c7be28c904b166a) | サードパーティによる美顔コンポーネントを結合するためのビデオ処理のコールバック |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a5f6d5ef01d3cd610959433107f78aa60) | SDK内部のOpenGL環境破棄の通知 |

### オーディオデータカスタムコールバック
| API | 説明 |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) | ローカルマイクがキャプチャしたオリジナルオーディオデータのコールバック |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46) | ローカルがキャプチャし、オーディオモジュールで前処理したオーディオデータのコールバック |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902) | 音声ミキシング前のリモートユーザーごとのオーディオデータ |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7) | 各再生待ちオーディオをミキシングし、最終的にシステムに送信して再生する前のデータコールバック |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a96923a9286a88b83d6890f607884ceb3) | SDKのすべてのオーディオミキシング後のオーディオデータ（キャプチャしたデータおよび再生待ちのデータを含む） |

### その他イベントコールバックインターフェース
| API | 説明 |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a77d78090666e330606b670bf8ce2d854) | ローカルLOGのプリントコールバック |

### ビデオ関連列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp01d5e1111c2ba49a53879c343fd484f2) | ビデオ解像度 |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp509a1d5f7a44e1d60cf25e4afb640347) | ビデオアスペクト比モード |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp8f7c7bceb683fdba0c3cb0a4766dd281) | ビデオストリームタイプ |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFillMode) | ビデオ画面塗りつぶしモード |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp9edface2441370ef72f70dd4945ff0f9) | ビデオ画面回転方向 |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa173483f8f2f9cbfd604328c0a8cba50) | 美顔（美肌）アルゴリズム |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpde7f16ea7692e7c649e9a16638f48dbe) | ビデオピクセル形式 |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2c1424df181810edcbd68a9d2cb4adde) | ビデオデータ伝達方式 |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa367a3c86bde4916b80b03acd05ec218) | ビデオのイメージタイプ |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSnapshotSourceType) | ローカルビデオスクリーンキャプチャのデータソース|

### ネットワーク関連列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa53ec28e9d73b79c701a709f44efbebe) | ユースケース |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp32cd3ba884366b8a2d45cad705f28b18) | ロール |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp39c937e1be1c70563f58a5a6fdde96a1) | トラフィックコントロールモード（破棄済み）|
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp3a953a9777c6e1447a27bc454f9f00b9) | 画質の好み |
| [TRTCQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp43d6beae8b3d7c79f02df2f125c090a7) | ネットワーク品質 |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5f5cc2365ee675bbc0f5a14095b1e0fc) | ビデオステータスタイプ |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp66f48a69ecc92051ca32055008a19c3e) | ビデオステータス変更理由のタイプ |

### オーディオ関連列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2b7efdf7211746ab55166bb4d55ed619) | オーディオサンプルレート |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp96d66d1098694549803eaba6baedb9c0) | 音声品質 |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7340a7d82950a691c95bde594a44959f) | オーディオルート（音声の再生モード） |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp30e899d6cb29154e1d73867d199b7191) | 音声リバーブモード |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpac19166c196a2905657f2a3b52a68ce0) | ボイスチェンジタイプ |
| [TRTCSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp70bfa071c4ebab5e7ed1811a780a53d9) | システム音量タイプ（モバイルデバイスのみに適用） |

### その他列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2f4911d8563ae1db783b963d626681d8) | Logレベル |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7821baad731a6db4d8977d304fafce63) | 重力センサースイッチ（モバイル端末のみに適用） |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5e2e800d31dc99373db17e2def3afc99) | クラウドミクスストリーミングのレイアウトモード |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpaa193560ab798cc5dcdb9624ce9740aa) | メディアレコーディングタイプ |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa7e631ba74d7c9f6832a6ad3be7a81af) | ミクスストリーミング入力タイプ |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp25c9df32061d8ad991f04b21fc6acacb) | オーディオレコーディングコンテンツタイプ |

### TRTCコアタイプの定義
| API | 説明 |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | 入室パラメータ |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam) | ビデオコーデックパラメータ |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCNetworkQosParam) | ネットワークトラフィックコントロール（Qos）パラメータセット |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCRenderParams) | ビデオ画面のレンダリングパラメータ |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCQualityInfo) | ネットワーク品質 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVolumeInfo) | 音量レベル |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestResult) | ネットワークスピードテスト結果 |
| [TRTCTexture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCTexture) | ビデオテクスチャデータ（Androidプラットフォームのみに適用。テクスチャIDおよびEGL環境を含む） |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFrame) | ビデオフレーム情報 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrame) | オーディオフレームデータ |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ac5b1947f21f77726cbff822eaf0003f9) | クラウドミクスストリーミングにおける各画面の説明情報 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a6066a5537ad8c1bc6158d43e8a4765db) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータ |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCPublishCDNParam) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開時に設定が必要な転送パラメータ |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams) | ローカルオーディオファイルのレコーディングパラメータ |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCLocalRecordingParams) | ローカルメディアファイルのレコーディングパラメータ |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ad82a59c2209c0596dabaee1152820494) | オーディオエフェクトパラメータ（破棄済み） |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a1b79e0e45a5f137df2e1995af7c0885c) | ルーム切り替えパラメータ|
| [TRTCAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrameCallbackFormat) | オーディオカスタムコールバックの形式パラメータ |




