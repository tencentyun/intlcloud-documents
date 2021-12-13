## TRTCCloud @ TXLiteAVSDK

### インスタンスの作成およびイベントコールバック
| API | 説明 |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) | TRTCCloudインスタンスの作成（シングルトンモード） |
| [destroySharedIntance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad8961d03736d8a52df5a3a991d0a77c4)  | TRTCCloudインスタンスの破棄（シングルトンモード） |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6a8e20d57b7890e4dbf6652c426d7015) | TRTCイベントコールバックを設定 |
| [delegateQueue](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a97158c52f2a4011454b4eb3ee369a8a1) | TRTCCloudDelegate イベントコールバックを起動するキューの設定 |

### ルーム関連インターフェース関数
| API | 説明 |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) | ルームに入室 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) | ルームを退室 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) | ロールの切り替え |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7c5a2aa06d649492f546d9c70a5de4a1) | ルームの切り替え |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) | ルーム間通話のリクエスト |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abd656e4c9b6a01231810ae897627e9bc) | ルーム間通話を退出 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) | サブスクライブモードを設定（有効にするには入室前に設定する必要があります） |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6100a5f395442d38ce9adab922382caf) | サブルーム事例の作成（複数のルームで同時視聴するために使用されます） |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a19e0d7921ac494fb588a4654d97abe86) | サブルーム事例の破棄 |

### CDN関連インターフェース関数
| API | 説明 |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6d2f4d81f0944072053d7dc9e9265f22) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングの公開を開始 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afc00ba747be5299cd7235928a628339e) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングの公開を停止 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aad42e78d355fd563b959a5053bac54cb) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開を開始 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開を停止 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータを設定 |

### ビデオ関連インターフェース関数
| API | 説明 |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | ローカルカメラのプレビュー画面を有効化（モバイル端末） |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | ローカルカメラのプレビュー画面を有効化（デスクトップ） |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) | ローカルカメラのプレビュー画面を更新 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | カメラのプレビューを停止 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | ローカルのビデオストリームの公開を一時停止/再開 |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2) | ローカル画面の一時停止中の代替画像を設定 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | リモートユーザーのビデオストリームをサブスクライブし、ビデオレンダリングウィジェットをバインド |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a518d3a8a3b4a4cfd8b5e0dfe7899756b) | リモートユーザーのビデオレンダリングウィジェットを更新 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | リモートユーザーのビデオストリームのサブスクライブを停止し、レンダリングウィジェットをリリース |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) | すべてのリモートユーザーのビデオストリームのサブスクライブを停止し、すべてのレンダリングリソースをリリース |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | リモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adf7cd002366760749c6f4d1ee9291db1) | すべてのリモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) | ビデオエンコーダのエンコードパラメータを設定 |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9) | ネットワーク品質モニタリングの関連パラメータを設定 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5d4f0aba952a355f153d374899e6dcec) | ローカル画面のレンダリングパラメータを設定 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7147d9c93af6a92f594ea394fc796081) |リモート画面のレンダリングモードを設定|
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) | ビデオエンコーダが出力する画面の方向を設定|
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a29a7cae6b4e82098fc342d4f0066d2ad) | エンコーダが出力する画面のイメージモードを設定 |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7a8c22e2f02d313590d4c499e18ebe3f) | 重力センサーの適合モードを設定 |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2aa9c464203b1c62cbb9ccabccc6334a) | 大小画面のデュアルチャンネルコーディングモード を有効化|
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a49440df0907b12c0ad8fe9e93bdbed0d) | 指定リモートユーザーの画面サイズを切り替え |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | ビデオ画面のスクリーンキャプチャ |

### オーディオ関連インターフェース関数
| API | 説明 |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | ローカルオーディオのキャプチャおよび公開を有効化 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab78601c38f1b872b03b662e6856be84c) | ローカルオーディオのキャプチャおよび公開を停止 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9) |ローカルのオーディオストリームの公開を一時停止/再開 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) | リモートのオーディオストリームの再生を一時停止/再開|
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) | すべてのリモートユーザーのオーディオストリームの再生を一時停止/再開 |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa62f2af2d86a64c0ebc7b9f00e4a54fe) | オーディオルートを設定 |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d38580f2c35f7e9828c4e41c56db35a) | 特定リモートユーザーの音声再生音量を設定 |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5475b81c1712323257c10baaf7ad6969) | ローカルオーディオのキャプチャ音量を設定 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7ce26486575e72bc445432929fdff26c) | ローカルオーディオのキャプチャ音量を取得 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af2602b1e9dfe932c89dd411f2f227192) | リモートオーディオの再生音量を設定 |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aba445625df38b8676d599df4a67a8407) | リモートオーディオの再生音量を取得|
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57d48cb0dbd7705486453b46e30e3fea) | 音声レベルのプロンプトを起動 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9eadd65cef0ac6b9c04ddfd7265afb01) | 録音を開始|
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac8c12476bbcf3d691060954fcdb6ebe6) | 録音を停止 |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b) | ローカルメディアのレコーディングを有効化 |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#affae72630393980fee79c21f2d20f602) | ローカルメディアのレコーディングを停止 |

### デバイス管理関連インターフェース
| API | 説明 |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a950f3f1c949def9e1e470f467db7b27a) | デバイス管理タイプ（TXDeviceManager）を取得 |

### 美顔特殊効果および画像のウォーターマーク
| API | 説明 |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a) | 美顔管理タイプ（TXBeautyManager）を取得 |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad0bedbddf415d26cff8242d5842a0908) | ウォーターマークの追加 |

### BGMおよび音声の特殊効果
| API | 説明 |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66) | オーディオエフェクトマネージャー（TXAudioEffectManager）を取得 |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) | システム音声キャプチャ を有効化（Macシステムのみに適用）|
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adef486f26a2c7d74a8cccb537367e66a) | システム音声キャプチャを停止（デスクトップシステムのみに適用） |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae) | システム音声のキャプチャ音量を設定|

### 画面共有関連インターフェース
| API | 説明 |
|-----|-----|
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) | アプリケーション内の画面共有を開始（ iOS 13.0以上のシステムのみをサポート） |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4) | 全システムの画面共有 を開始（ iOS 11.0以上のシステムのみをサポート） |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | デスクトップ画面共有を開始（このインターフェースはデスクトップシステムのみをサポート） |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) | 画面共有を停止 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) | 画面共有を一時停止 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) | 画面共有を再開 |
| [getScreenCaptureSourcesWithThumbnailSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a37df498cbc8d9b1135e3caafdcee906f) | 共有可能な画面およびウィンドウを列挙（このインターフェースはMac OSシステムのみをサポート ） |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18) | 共有したい画面またはウィンドウを選択（このインターフェースはMac OSシステムのみをサポート） |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) | 画面共有（サブストリーム）のビデオコーデックパラメータを設定（このインターフェースはデスクトップシステムのみをサポート） |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a18d3fb6535c9884784c5ad5f8dfd0b12) | 画面共有時の音声ミキシングの音量レベルを設定（このインターフェースはデスクトップシステムのみをサポート） |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa567171999b17a7f5655213b193415a7) | 指定のウィンドウを画面共有のexcludeリストに追加（このインターフェースはデスクトップシステムのみをサポート） |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a95b1f3fbc6ff755f67f7e9b86240ea5f) | 指定のウィンドウを画面共有のexcludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |
| [removeAllExcludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab2b6a778a528d58e2a42c9adfc7684f2) | すべてのウィンドウを画面共有のexcludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233) | 指定のウィンドウを画面共有のincludeリストに追加（このインターフェースはデスクトップシステムのみをサポート） |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a058ac1e2141d6eb1962219167add42bc) | 指定のウィンドウを画面共有のincludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |
| [removeAllIncludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a18a20767a0e1076ba16cd473a2512156) | すべてのウィンドウを画面共有のincludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |

### ユーザー定義キャプチャおよびカスタムレンダリング
| API | 説明 |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | ビデオユーザー定義キャプチャモード の起動/終了|
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | 自身がキャプチャしたビデオフレームをSDKに送信 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) | オーディオのユーザー定義キャプチャモードを起動 |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a62cab4ec7c336ae135c2f681aca25da1) | 自身がキャプチャしたオーディオデータをSDKに送信 |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1101d883d65882f735e3d17f874a25cb) | ユーザー定義のオーディオトラックの起動/終了|
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9f408915460e86e889056066ca4e0908) | ユーザー定義のオーディオトラックをSDKにミキシング |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abd8823c40d31e122ed34f7ac33c678a6) | プッシュ時にミキシングする外部オーディオのプッシュ音量および再生音量を設定 |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) | ユーザー定義キャプチャ時のタイムスタンプを発行 |
| [setLocalVideoProcessDelegete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2f73c33b1010a63bd3a06e639b3cf348) | サードパーティによる美顔のビデオデータコールバックを設定|
| [setLocalVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aba3d309645d27304b6d4ea31b21a4cda) | ローカルビデオカスタムレンダリングコールバックを設定 |
| [setRemoteVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5244e73ac27599370f966575e11959ff) | リモートビデオカスタムレンダリングコールバックを設定 |
| [setAudioFrameDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01726b03b102c32222a2a26b16abcd48) | オーディオデータカスタムコールバックを設定 |
| [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) | ローカルマイクによってキャプチャされたオリジナルオーディオフレームコールバック形式を設定 |
| [setLocalProcessedAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9ec7c7123eb2f333769508de193ea51f) | 前処理後のローカルオーディオフレームコールバック形式を設定 |
| [setMixedPlayAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a24ad642b88cd3b2ca2d3044d72817090) | 最終的にシステムから再生したいオーディオフレームコールバック形式を設定 |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a325da4ec57db06b91b74da8699b47d7c) | オーディオカスタム再生を有効化 |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aeebe3811918c8250d32d872fee83a2c2) | 再生可能なオーディオデータを取得 |

### カスタムメッセージ送信インターフェース
| API | 説明 |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acbc86da0cb558c549f42e7e987c7beaf) |  UDPチャネルを利用してカスタムメッセージをルーム内のすべてのユーザーに送信  |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6de26e5efddf899d31158e4d48f17c02) | SEIチャネルを利用して送信カスタムメッセージをルーム内のすべてのユーザーに送信  |

### ネットワークテストインターフェース
| API | 説明 |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a058556b224315dcde3601ab621a09dee) | ネットワークスピードテストを開始（ルーム入室前に使用） |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a58d732ba648d1f9a3a460c02de79bb9b) | ネットワークスピードテストを停止 |

### デバック関連インターフェース
| API | 説明 |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ace5acd2fe597b6656b45aaa93e3e45a1) | SDKのバージョン情報を取得 |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9d2b6a99e137a9667743edc8ac909493) | Log出力レベルを設定 |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a177c4f1fbb2a011ff496417dc0245667) |コンソールのログプリント を有効化/無効化 |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa51a341a43a854ac6e3fa1d0093fec95) | ログのローカル圧縮を有効化/無効化 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a93b48089741f7022aea1f8f93ce8fff9) | ローカルログの保存パスを設定 |
| [setLogDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a41497e4242e3c42acfa35730cdc1ddf6) | ログコールバックを設定 |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3bd71c8a99029c1a4708bf1c176aa299) | ダッシュボードを表示 |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aad41ff6d5b5565046911acf27bb3dee4) | ダッシュボードのマージンを設定 |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | 試験的インターフェースの呼び出し |

### 破棄されたインターフェース
| API | 説明 |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abb57991f5e4f4ca1b95c2181a7e538c8) | マイクの音量レベルを設定 |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1336146862fb742de6cbe5718f9b7008) | 美顔、美白および肌の色調補正エフェクトレベルを設定 |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae0e4341ef565cc5ba28101574179cd56) | デカ目レベルを設定 |
| [setFaceScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a52ad635b237ccb1eef53a4ed9e650035) | 小顔レベルを設定 |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1bf6dd0f5a5c6c013323d31f60d494e2) | フェイスシェイプレベルを設定 |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a145d4ed3d5790a449a9884d282420216) | 下あご引き伸ばしまたは縮小幅を設定 |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac11082c88aba749acd7cd2c7a7caa953) | 面長修正レベルを設定 |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae94b107a9c476337585906c79b42ee95) | 小鼻レベルを設定 |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3aa8c561d744e3d921dff6186a6e4ade) | 動的エフェクトステッカーを設定 |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa6689d734b9f46cb84a848b7e8f39cbd) | 動的エフェクトミュートを設定 |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | 画面共有を起動 |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) | カラーフィルターエフェクトを設定|
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3b0d7db70674f961c14b316f4e8e7a2b) | カラーフィルター濃度を設定 |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab4682edfc605ba06e24fd7b3e758ce5d) | クロマキー背景ビデオを設定 |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4d9983591fa2a847e226b7a30e8db294) | BGMの再生を起動 |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a11004f1ba27b057985850a25307b0bec) | BGMの再生を停止 |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa4b92d4c989e99612f6c4dab03a78764) | BGMの再生を停止 |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aed6e8f224b5f834b1bc0c15f9701f692) | BGMの再生を停止 |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac1f96932d02198cd045ee96f1306c8ba) | BGMの総時間を取得（単位：ミリ秒） |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7fd043ae358c43f6a178837fb2846ef9) | BGM再生の進捗を設定|
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adbfc8e226df7c6caaaca1a89a9842f23) | BGMの音量レベルを設定 |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a08c468f48d99aef0e89716111db1f422) | BGMのローカル再生音量を設定 |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0cf0c090285038b23843c646009073d1) | BGMのリモート再生音量を設定 |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a555cde4eda63d13bbad0dbdba7094a47) | リバーブエフェクトを設定 |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa60f54923826cc59d8a4526669c4ea5e) | ボイスチェンジタイプを設定 |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2ae175694198a9b3d1b1647b7ce1dae0) | オーディオエフェクトを再生 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | オーディオエフェクトの音量を設定 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | オーディオエフェクトの再生を停止 |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7066509af1de32c290b7cc297cd00f2b) | すべてのオーディオエフェクトを停止 |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6b345c95b5b68198d8dbc64a3652ed35) | すべてのオーディオエフェクト音量を設定 |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab0d46ccb8fca811851b30e7731958024) | オーディオエフェクトを一時停止 |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a207dd8909c05d4a8a1431d33e644d4fe) | オーディオエフェクトを一時停止|
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa26564f3388bc249ecbd2813d9c45390) | インイヤーモニタリングを有効化（または無効化） |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | リモートビデオ画面の表示を開始 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | リモートビデオ画面の表示を停止すると同時に、このリモートユーザーのビデオデータストリームのプルを停止 |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) | リモート画像のレンダリングモードを設定 |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90) | リモート画像の時計回りの回転角度を設定 |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) | ローカル画像のレンダリングモードを設定 |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4d2d95ad8fbaf8edce18667aa835848e) | ローカル画像の時計回りの回転角度を設定 |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af68f13fba5a02e4e9ca338596fb64916) | ローカルカメラプレビュー画面のイメージモードを設定 |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) | リモートユーザーのサブストリーム画面の表示を開始|
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acab6e31898857af876af66e779216203) | リモートユーザーのサブストリーム画面の表示を停止 |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a487b3cd9a6b41581d4b45c752c5ede4c) | サブストリーム画面の塗りつぶしモードを設定 |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a72c66b67eacd24a0e796a3213219fb6d) | サブストリーム画面の時計回りの回転角度を設定 |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2b2d43a3955480f2d6200bf20e66f3cf) | 大画面または小画面の視聴優先順位を設定|
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53) | オーディオ品質を設定 |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | オーディオ品質を設定 |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa9a1952f442020bc92ce1beb65959e56) | カメラの切り替え |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8662b8ecab04a55a321ee9f16d0680a7) | 現在のカメラがズームをサポートしているかどうかを照会 |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9777fe95f7830746c1ba6b10446c37a0) | カメラズームの倍数（フォーカス距離）を設定 |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd005524f8e2c2fbfcc415049e666ced) | フラッシュの切り替えをサポートしているかどうかを照会 |
| [enbaleTorch](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af6b128ee01d91a63dc1976db7a9be555) | フラッシュのオン/オフ |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0e164f727b990581a42f97dca1bf7548) | カメラがフォーカスの設定をサポートしているかどうかを照会 |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6a77cc99c41b926cd99909ae1ace39ae) |カメラのフォーカス座標位置を設定 |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5af361145f04227ff1a451fee2705a77) | 顔の位置の自動認識をサポートしているかどうかを照会 |
| [enableAutoFaceFoucs](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a32a8f584879b17f211df75494a5be96c) | 顔追尾フォーカスの有効化/無効化|
| [startCameraDeviceTestInView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1bd6289b969adde0096c83d6a5532332) |カメラテストを開始 |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1b67fa3f322efe538d924b381c06e676) | カメラテストを開始 |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa6f467c12fcea7e09cc97861d511498a) | マイクテストを開始 |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8cca1c5913ac021987680195075e5fc9) | マイクテストを開始 |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a60aa520016687bea03f17cb4ec19c1b6) | スピーカーテストを開始 |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf383f971dc54f0254b2d40f100cc9ca) | スピーカーテストを停止 |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5e267aa0d820f78b761be1d485369b3b) | マイクデバイスリストを取得 |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afa6a82cbf407b0bd6eb63093940e189d) | 現在のマイクデバイスを取得 |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) | 現在使用するマイクを選択 |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af69d237159163eebcb6876e767d7692e) | 現在のマイクのデバイス音量を取得 |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aaa6810f64c153e779697dc2d5bd30f6a) | 現在のマイクのデバイス音量を設定 |
| [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae9c936081b96348ce047337a1d3bb7b0) |現在のシステムのマイクデバイスがミュートされているかどうかを取得|
| [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) | システムの現在のマイクデバイスのミュートステータスを設定 |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5b888d0ebe697fdc5e11759f1b154fc3) | スピーカーデバイスリストを取得|
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9d6d48c3937e3cb2632ced9a6a002368) | 現在のスピーカーデバイスを取得 |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6c951071ac218930680febd84314ee05) | 使用したいスピーカーを設定 |
| [getCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa25ac85f6f84b352175aebb9c7007247) | 現在のスピーカーのデバイス音量を取得 |
| [setCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a019001b23569c8b6da7f3276af58e0a7) | 現在のスピーカーのデバイス音量を設定 |
| [getCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a793d11364882c7fac7f9200f8761400c) | システムの現在のスピーカーデバイスがミュートされているかどうかを確認 |
| [setCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a738ea0dffd48d5bc2b05b146eb79ec46) | システムの現在のスピーカーデバイスのミュートステータスを設定 |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0a1b764ff4238afaeaba41ee728a1451) | カメラデバイスリストを取得 |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa238683cb00f508b05b9ac031a17bc37) | 現在使用しているカメラを取得 |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) | 現在使用したいカメラを選択 |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab098daa610ae506dbf6c2a4f666ae32c) | システムの音量タイプを設定 |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | ビデオスクリーンキャプチャ |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | ビデオのユーザー定義キャプチャモードを起動|
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | 自身がキャプチャしたビデオデータを送信 |
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) | アプリケーション内の画面共有を開始（iOS） |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4) | 全システムの画面共有を開始（iOS） |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | ローカルのビデオストリームの公開を一時停止/再開 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | リモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |

### エラーおよび警告イベント
| API | 説明 |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a10a711eb68abcacc1ca690501fc7c9fb) | エラーイベントコールバック |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a25ac0da9ad798a2313bdf8f296828541) | 警告イベントコールバック |

### ルーム関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) | 入室成功または失敗のイベントコールバック |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) | 退室のイベントコールバック |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ade2c2eab48a30e7ca1c9246e573b7f28) | ロール切り替えのイベントコールバック |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ad848cbee89f8b6258c9f03f4cb253a31) | ルーム切り替え結果のコールバック |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) | ルーム間通話リクエスト結果のコールバック |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a26b34d83afac68928a156096862c9c06) | ルーム間通話終了結果のコールバック |

### ユーザー関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58) | ユーザーが現在のルームに入室 |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) | ユーザーが現在のルームを退室 |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) | リモートユーザーが公開/キャンセルしたビッグストリームのビデオ画面 |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) | リモートユーザーが公開/キャンセルしたサブストリームのビデオ画面 |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) | リモートユーザーが公開/キャンセルした自身のオーディオ |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7fc7fd0144af2bc4ce0797f9de530d96) | SDKが自身のローカルユーザーまたはリモートユーザーの最初のフレーム画面のレンダリングを開始 |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aafc4536f552199368e48c8527783c410) | SDKがリモートユーザーの最初のフレームのオーディオの再生を開始 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a17567554f413629a80b5970bdffdff7b) | 自身のローカルの最初のビデオフレームが公開済み |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#acb73daf4ce82cd03f787f057b233b412) | 自身のローカルの最初のオーディオフレームが公開済み |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af7fef48407b65423871ed6f7652e4176) | リモートビデオステータス変更のイベントコールバック |

### ネットワークおよび技術指標統計のコールバック
| API | 説明 |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28) | ネットワーク品質のリアルタイム統計のコールバック |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afb0811035e97c8544dbc9ecbef461dd9) | オーディオビデオ技術指標のリアルタイム統計のコールバック |

### クラウドとの接続状況のイベントコールバック
| API | 説明 |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aed43a70b4a95eb95181e2b410013bf54) | SDKがクラウドとの接続を切断済み |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | SDKがクラウドとの再接続を試行中 |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | SDKがクラウドとの接続を再開済み |

### ハードウェアデバイス関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aaa74021e5fd2564afb2df50e25eedeff) | カメラの準備完了 |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afdac7dee94451913a4dc9982badc8035) | マイクの準備完了 |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1859305732dfd03de63c9b780f99d513) | 現在のオーディオルートに変更発生（モバイルデバイスのみに適用） |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7775c3fbd84b8da3b7a75bdea27ed5c5) | 音量レベルフィードバックのコールバック |
| [onDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a0152908c497bd5ee5225251d9e93e500) | ローカルデバイスのオン/オフステータスに変更発生（デスクトップシステムのみに適用） |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1c36efd81dc4edf88fc3bc6af83b1b5a) | 現在のマイクのシステムキャプチャ音量に変更発生 |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f) | 現在のシステムの再生音量に変更発生 |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676) | システム音声キャプチャが正常に開始されたかどうかのイベントコールバック（Macシステムのみに適用） |

### カスタムメッセージ受信イベントコールバック
| API | 説明 |
|-----|-----|
| [onRecvCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a324311b3d4f3930d9a50b8449b155dd3) | カスタムメッセージ受信のイベントコールバック |
| [onMissCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af1b8e7d0f73773eca509afc1cf4c9ece) | カスタムメッセージ消失のイベントコールバック |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6e4365456cb4df6e1bdf870511b72042) | SEIメッセージ受信のコールバック |

### CDN関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a75c6bf4a7c7ec60a24aabfe8e47ea1f4) | Tencent Cloud CSS CDN上へのオーディオビデオストリーミングのイベントコールバックの公開を開始 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a379dcf84e15f93b64efe2cb9f362877c) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングのイベントコールバックの公開を停止 |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a817783f364bf9f6f0a1df4bc26bad628) | 非Tencent Cloud CDNへのオーディオビデオストリーミングのイベントコールバックの公開を開始 |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aab032eb48a56e8351ada60ce5b510d5e) |非Tencent Cloud CDNへのオーディオビデオストリーミングのイベントコールバックの公開を停止 |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab5c98341b7536b5b65c04b835c4d28fb) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータ設定のイベントコールバック |

### 画面共有関連イベントコールバック
| API | 説明 |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7d15537d26fb001045ff95157d59ed3f) | 画面共有開始のイベントコールバック |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a9cc6106085b2049838e21bb50e192786) | 画面共有一時停止のイベントコールバック |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ae9c08ef9dd260cf6fd946209fda8a011) | 画面共有再開のイベントコールバック |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a323d2b3e5b8b364722e0b161ab11c816) | 画面共有停止のイベントコールバック |

### ローカルレコーディングおよびローカルスクリーンキャプチャのイベントコールバック
| API | 説明 |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a044ce179ac4bc0bc987a3b74ecd911e7) | ローカルレコーディングタスク開始済みのイベントコールバック |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab4250c05ea4b843c27385f77d5004fc3) | ローカルレコーディングタスク実行中の進捗のイベントコールバック |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ae78ca25acea4152bfd9d0ccf71bd4108) | ローカルレコーディングタスク完了済みのイベントコールバック |

### 破棄されたイベントコールバック
| API | 説明 |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af26948706dc0dff24946470066e9c4e0) | キャスターが現在のルームに入室（破棄済み） |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a72f0a872a13500cb5394f77c586ab3f5) | キャスターが現在のルームを退室（破棄済み） |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#accb36b0eb1d1b72f32cf72617bb1c730) | オーディオエフェクト再生が完了済み（破棄済み） |

### ビデオデータカスタムコールバック
| API | 説明 |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7b43888945a9d12f088ed99a5854e3c1) | カスタムビデオレンダリングのコールバック |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8d4f000b4169a64a8a8af15e51e5dd95) | サードパーティによる美顔コンポーネントを結合するためのビデオ処理のコールバック |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a5f6d5ef01d3cd610959433107f78aa60) | SDK内部 OpenGL環境破棄の通知 |

### オーディオデータカスタムコールバック
| API | 説明 |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) | ローカルマイクがキャプチャしたオリジナルオーディオデータのコールバック |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0) | ローカルがキャプチャし、オーディオモジュールで前処理したオーディオデータのコールバック |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a) | 音声ミキシング前のリモートユーザーごとのオーディオデータ |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e) | 各再生待ちオーディオをミキシングし、最終的にシステムに送信して再生する前のデータコールバック |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a905748efe966e94ec1212fda14161aee) | SDKのすべてのオーディオミキシング後のオーディオデータ（キャプチャしたデータおよび再生待ちのデータを含む） |

### その他イベントコールバックインターフェース
| API | 説明 |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab1364c78a6f31a8c08d0138c4f6e9647) | ローカルLOG のプリントコールバック |

### ビデオ関連列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5) | ビデオ解像度 |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gafdfe57c064658b38b78b0fd11e2706c0) | ビデオアスペクト比モード |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1974ff7e5e78b4455925faf74e38f1e8) | ビデオストリームタイプ |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1a66aad6fff71205c7a266268e16f55c) | ビデオ画面塗りつぶしモード |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gae8bd6b06a2ca5f89f9b3cea393fc6eb9) | ビデオ画面回転方向 |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga9bafd3233be6cec1b380d469017ed3e6) | 美顔（美肌）アルゴリズム |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gabb58c142deac29da242c957f21c963e3) | ビデオピクセル形式 |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga0fce6f58df3d3021696d15eff683ed8b) | ビデオデータ伝達方式 |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga13da9775774c3251999f1e46d279305f) | ビデオのイメージタイプ |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga50f989651c9f893de7716ffbc2d2a5fc) | ローカルビデオスクリーンキャプチャのデータソース |

### ネットワーク関連列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga6ab617b26cf503a8c1bfec34a9918dbe) | ユースケース |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gad147b9b0249d0c2759cf1514c8978881) | ロール |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga915f86fec1b00787147d40a189444823) | トラフィックコントロールモード（破棄済み） |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga2c460e7365ad67ee0213545b0a67aa6d) | 画質の好み |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | ネットワーク品質 |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga0a200753a7e0c539ce4f584cd8d17510) | ビデオステータスタイプ |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga349e42c3f8a2de5a031e90a1240d7f54) | ビデオステータス変更理由のタイプ |

### オーディオ関連列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga346b09a7691ce8c9813bac0feb057d08) | オーディオサンプルレート |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) | 音声音質 |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga81305fea3aae73346d04f0013e0194d4) | オーディオルート（音声の再生モード） |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1c0a768f9f7855e87c486617816c7759) | 音声リバーブモード |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaeb48457146f2279c912e345ce532ecef) | ボイスチェンジタイプ |
| [TRTCSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaac0cd0da9dd789dcec4ba16471006f23) | システム音量タイプ（モバイルデバイスのみに適用） |

### その他列挙値の定義
| API | 説明 |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gacefec5143acae6d0524b5500f0155908) | Logレベル |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga894251078222f9ac4ba5815aac4b493c) | 重力センサースイッチ（モバイル端末のみに適用） |
| [TRTCScreenCaptureSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaeabd30a270055e48105a34c781c782b0) | 画面共有のターゲットタイプ（デスクトップのみに適用） |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga907c7b1ef1f09fb7417a549e82110855) | クラウドミクスストリーミングのレイアウトモード |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga4bb9927d377aa27b781fcfef5cf1058a) | メディアレコーディングタイプ |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga9359cd77f4759e5b1a82fe1b94de638d) | ミクスストリーミング入力タイプ |
| [TRTCMediaDeviceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga4a04a7c25ed48ab15603e8c3db115b95) | デバイスタイプ（デスクトッププラットフォームのみに適用） |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gade0f3fa25d9d1c876660e230152567b0) | オーディオレコーディングコンテンツタイプ |

### TRTCコアタイプの定義
| API | 説明 |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCParams) | 入室パラメータ |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam) | ビデオコーデックパラメータ |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCNetworkQosParam) | ネットワークトラフィックコントロール（Qos）パラメータセット |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCRenderParams) | ビデオ画面のレンダリングパラメータ |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | ネットワーク品質 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCVolumeInfo) | 音量レベル |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult) | ネットワークスピードテスト結果 |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCVideoFrame) | ビデオフレーム情報 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCAudioFrame) | オーディオフレームデータ |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCMixUser) | クラウドミクスストリーミングにおける各画面の説明情報 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCTranscodingConfig) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータ |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCPublishCDNParam) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開時に設定が必要な転送パラメータ |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCAudioRecordingParams) | ローカルオーディオファイルのレコーディングパラメータ |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCLocalRecordingParams) | ローカルメディアファイルのレコーディングパラメータ |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCAudioEffectParam) | オーディオエフェクトパラメータ（破棄済み） |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCSwitchRoomConfig) | ルーム切り替えパラメータ |


