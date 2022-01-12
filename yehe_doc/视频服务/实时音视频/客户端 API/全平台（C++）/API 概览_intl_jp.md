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

### インスタンスの作成およびイベントコールバック
| API             | 説明               |
|-----|-----|
| [getTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ga0ef57994050abf58a18a3defd4cc5fd0) | TRTCCloudインスタンスの作成（シングルトンモード） |
| [destroyTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#gaadc9070c962327451dbc949a4c5a4681) | TRTCCloudインスタンスを破棄 （シングルトンモード）  |
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | TRTCイベントコールバックを設定|
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | TRTCイベントコールバックを削除 |

### ルーム関連インターフェース関数
| API             | 説明               |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) | ルームに入室 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | ルームを退室 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | ロールの切り替え |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | ルームの切り替え |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab5a0622e5d3d521d79ba4f85c44244eb) | ルーム間通話のリクエスト |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | ルーム間通話を退出 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | サブスクライブモードを設定（有効にするには入室前に設定する必要があります） |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | サブルーム事例の作成（複数のルームで同時視聴するために使用されます） |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a980cf4d173abfb58c00ef35a20e12c85) | サブルーム事例の破棄 |

### CDN関連インターフェース関数
| API             | 説明               |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングの公開を開始 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングの公開を停止 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開を開始 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) |非Tencent Cloud CDNへのオーディオビデオストリーミングの公開を停止 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータを設定 |

### ビデオ関連インターフェース関数
| API             | 説明               |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8ac23e725c7ed75488df1be2ee514884) | ローカルカメラのプレビュー画面を有効化（モバイル端末） |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8ac23e725c7ed75488df1be2ee514884) | ローカルカメラのプレビュー画面を有効化（デスクトップ） |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0af978a75d5ba671b7ce5f0b81b003c8) | ローカルカメラのプレビュー画面を更新 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | カメラのプレビューを停止 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) | ローカルのビデオストリームの公開を一時停止/再開 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9) | リモートユーザーのビデオストリームをサブスクライブし、ビデオレンダリングウィジェットをバインド |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a027a8b23a363dc91e6ce1c9773ee8664) | リモートユーザーのビデオレンダリングウィジェットを更新 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abd186570272cd61b4a6e4aea870437e1) | リモートユーザーのビデオストリームのサブスクライブを停止し、レンダリングウィジェットをリリース |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | すべてのリモートユーザーのビデオストリームのサブスクライブを停止し、すべてのレンダリングリソースをリリース |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65) | リモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | すべてのリモートユーザーのビデオストリームのサブスクライブを一時停止/再開 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55b0710284e44ba3703e22b07c3665c8) | ビデオエンコーダのエンコードパラメータを設定 |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad21668c7550aad44f1ed61265ffceb24) | ネットワーク品質モニタリングの関連パラメータを設定 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | ローカル画面のレンダリングパラメータを設定 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | リモート画面のレンダリングモードを設定 |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | ビデオエンコーダが出力する画面の方向を設定 |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | エンコーダが出力する画面のイメージモードを設定 |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5019a8005cd96662ce2cface662a811e) | 大小画面のデュアルチャンネルコーディングモードを有効化 |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad2c6cc256f6e24178cd7c9cd2290ea4d) | 指定リモートユーザーの大小画面を切り替え |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c) | ビデオ画面のスクリーンキャプチャ |

### オーディオ関連インターフェース関数
| API             | 説明               |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a86c80ed357798e50ccf5c7ae47317f4c) | ローカルオーディオのキャプチャおよび公開を有効化 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | ローカルオーディオのキャプチャおよび公開を停止 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | ローカルのオーディオストリームの公開を一時停止/再開 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | リモートのオーディオストリームの再生を一時停止/再開 |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | すべてのリモートユーザーのオーディオストリームの再生を一時停止/再開 |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac49fa4a92105f01e2e296b20881a8324) | 特定リモートユーザーの音声再生音量を設定|
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | ローカルオーディオのキャプチャ音量を設定 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | ローカルオーディオのキャプチャ音量を取得 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) |リモートオーディオの再生音量を設定 |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | リモートオーディオの再生音量を設定 |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | 音量レベルのプロンプトを起動 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5224523e00d5167eb75cee9b65f72677) | 録音を開始 |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | 録音を停止 |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | ローカルメディアのレコーディングを有効化 |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8b9b6f0608e48c27fc7c646718cb41ba) | ローカルメディアのレコーディングを停止 |
| [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0e6e6434aaa03ce878280125a9c0fa4b) | リモートオーディオストリームのインテリジェント同時再生ポリシーを設定 |

### デバイス管理関連インターフェース
| API             | 説明               |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | デバイス管理タイプ（TXDeviceManager）を取得 |

### 美顔・特殊効果および画像ウォーターマーク
| API             | 説明               |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | 美顔、美白および肌の色調補正エフェクトレベルを設定 |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | ウォーターマークの追加 |

### BGMおよび音声の特殊効果
| API             | 説明               |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | オーディオエフェクトマネージャー（TXAudioEffectManager）を取得|
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) | システム音声キャプチャを有効化（デスクトップシステムのみに適用） |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | システム音声キャプチャを停止（デスクトップシステムのみに適用）|
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | システム音声のキャプチャ音量を設定 |

### 画面共有関連インターフェース
| API             | 説明               |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd) | デスクトップ画面共有を開始（このインターフェースはデスクトップシステムのみをサポート） |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | 画面共有を停止 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | 画面共有を一時停止 |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | 画面共有を再開 |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad23c03ad142e8a42c49967ff9ccf9592) | 共有可能な画面およびウィンドウを列挙（このインターフェースはデスクトップシステムのみをサポート）|
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | 共有したい画面またはウィンドウを選択（このインターフェースはデスクトップシステムのみをサポート） |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a542913f5081fb2479137a7416c970e2d) | 画面共有（サブストリーム）のビデオコーデックパラメータを設定（デスクトップシステムとモバイルシステムの両方をサポート） |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | 画面共有時の音声ミキシングの音量レベルを設定（このインターフェースはデスクトップシステムのみをサポート） |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac2a8a65dc2c1d0e4ffbd89eeae768fff) | 指定のウィンドウを画面共有のexcludeリストに追加（このインターフェースはデスクトップシステムのみをサポート） |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0bbbff5ea3cd764dbaaad0db887760bf) | 指定のウィンドウを画面共有のexcludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |
| [removeAllExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | すべてのウィンドウを画面共有のexcludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a442186322939f9b93d6c6e0a3ace7bd3) | 指定のウィンドウを画面共有のincludeリストに追加（このインターフェースはデスクトップシステムのみをサポート） |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3674c0ee6514d118fddd9a500ccafb03) | 指定のウィンドウを画面共有のincludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |
| [removeAllIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | すべてのウィンドウを画面共有のincludeリストから削除（このインターフェースはデスクトップシステムのみをサポート） |

### ユーザー定義キャプチャおよびカスタムレンダリング
| API             | 説明               |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aaeab72ed55be06685e293c3cf92b6f90) | ビデオユーザー定義キャプチャモードの起動/終了 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6) | 自身がキャプチャしたビデオフレームをSDKに送信 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | オーディオのユーザー定義キャプチャモードを起動 |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | 自身がキャプチャしたオーディオデータをSDKに送信 |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a896ff4b2731488821dd1ce382276ca0c) | ユーザー定義のオーディオトラックの起動/終了 |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3c99feacd22af10926d5a521ca598ecd) | ユーザー定義のオーディオトラックをSDKにミキシング|
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418) | プッシュ時にミキシングする外部オーディオのプッシュ音量および再生音量を設定 |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a33ed1b26695b6b75dc9ce78e5280cbb4) | ユーザー定義キャプチャ時のタイムスタンプを発行 |
| [setLocalVideoProcessCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3f6d32bdf3cb0fe72b61455304b975c6) | サードパーティによる美顔のビデオデータコールバックを設定 |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | ローカルビデオカスタムレンダリングコールバックを設定 |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | リモートビデオカスタムレンダリングコールバックを設定 |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | オーディオデータカスタムコールバックを設定 |
| [setMixedPlayAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1c4e3c6d0c2653609e748ceeda8bb46e) | 最終的にシステムから再生したいオーディオフレームコールバック形式を設定 |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7047f52811cefa10cf020ee20db1b087) | オーディオカスタム再生を有効化 |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac986d3ec66ab6681d94c8eb933b519de) | 再生可能なオーディオデータを取得 |

### カスタムメッセージ送信インターフェース
| API             | 説明               |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | UDPチャネルを利用してカスタムメッセージをルーム内のすべてのユーザーに送信 |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | SEIチャネルを利用して送信カスタムメッセージをルーム内のすべてのユーザーに送信  |

### ネットワークテストインターフェース
| API             | 説明               |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab9052b69fd4e12b5860da03a868e87d7) | ネットワークスピードテストを開始（入室前に使用） |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | ネットワークスピードテストを停止 |

### デバック関連インターフェース
| API             | 説明               |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | SDKのバージョン情報を取得 |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Log出力レベルを設定 |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | コンソールのログプリントを有効化/無効化 |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | ログのローカル圧縮を有効化/無効化 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | ローカルログの保存パスを設定 |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | ログコールバックを設定 |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | ダッシュボードを表示 |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a187cb56ce8bbdf9a74e347954d2c7c6a) | 試験的インターフェースの呼び出し |

### 破棄されたインターフェース
| API             | 説明               |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aaeab72ed55be06685e293c3cf92b6f90) | ビデオのユーザー定義キャプチャモード を起動 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6) | 自身がキャプチャしたビデオデータを送信 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) | ローカルのビデオストリームの公開を一時停止/再開 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65) | リモートユーザーのビデオストリームのサブスクライブを一時停止 / 再開 |
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab9052b69fd4e12b5860da03a868e87d7) |  ネットワークスピードテストを開始（入室前に使用） |

### エラーおよび警告イベント
| API             | 説明               |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a9724da0b3da9b2eca5736fa8e54aa410) | エラーイベントコールバック |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a53169ea41d90506cccbff507ba1932a4) | 警告イベントコールバック |

### ルーム関連イベントコールバック
| API             | 説明               |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a236a49e0525615b6435eaa826b7caffe) | 入室成功または失敗のイベントコールバック |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) | 退室のイベントコールバック |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a248335805c125e225cfec249697f2299) | ロール切り替えのイベントコールバック |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ac5889e412f38769f2d21887f9bd7eeec) | ルーム切り替え結果のコールバック |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a62333366a3a1ab09dc2b2f627a8a1bdd) | ルーム間通話リクエスト結果のコールバック |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a292d6661cb93ba30ff68b1f88cf173f1) | ルーム間通話終了結果のコールバック |

### ユーザー関連イベントコールバック
| API             | 説明               |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a43704996ae1f50749b7c7140755350f1) | ユーザーが現在のルームに入室 |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a5f7c705f3894d3a430ef1fac8bf8e2c5) | ユーザーが現在のルームを退室 |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) | リモートユーザーが公開/キャンセルしたビッグストリームのビデオ画面 |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a460922e4fb4b000d1dbd27b596dd0e5c) | リモートユーザーが公開/キャンセルしたサブストリームのビデオ画面 |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a6f449dc5294e369750bc15a39eaa856c) | リモートユーザーが公開/キャンセルした自身のオーディオ |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad28d27badd56ac274c44720cc9f253d5) |SDKが自身のローカルユーザーまたはリモートユーザーの最初のフレーム画面のレンダリングを開始 |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a123616289b3219bc36137bc77e8e8b7a) | SDKがリモートユーザーの最初のフレームのオーディオの再生を開始 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a454ea7e7103b2838440cafba3e524433) | 自身のローカルの最初のビデオフレームが公開済み |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0bd950cb774fd40cfdc2fbff885295d2) | 自身のローカルの最初のオーディオフレームが公開済み |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a967a9b593385a8081083e84d3f5648b5) | リモートビデオステータス変更のイベントコールバック |

### ネットワークおよび技術指標統計のコールバック
| API             | 説明               |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a377441bace65d98a1218817914a12ecb) | ネットワーク品質のリアルタイム統計のコールバック |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ae7e4117f9c8004c9bcc5a29d64e840c9) | オーディオビデオ技術指標のリアルタイム統計のコールバック |
| [onSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a7bbfbd86185f20935f8a23d7dad94d9a) | ネットワークスピードテストの結果のコールバック |

### クラウドとの接続状況のイベントコールバック
| API             | 説明               |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a34c34705bb67127ff6d28700cf2ab591) | SDKがクラウドとの接続を切断済み |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#afe74dff22fde93fe0f07fcf18153d334) | SDKがクラウドとの再接続を試行中 |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ae90cd149a676418016cb8736b217f1a8) |SDKがクラウドとの接続を再開済み |

### ハードウェアデバイス関連イベントコールバック
| API             | 説明               |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a13a9ad0933b7ab872987e432f005e8ad) | カメラの準備完了 |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0ba02a5d9009ebb9c4e80c0c43c80bca) | マイクの準備完了|
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a61df1f9eec0bfcebf421be865275ffc5) | 音量レベルフィードバックのコールバック |
| [onDeviceChange](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ac86c1b0d445a33f6340394b3b78490bd) | ローカルデバイスのオン/オフステータスに変更発生（デスクトップシステムのみに適用） |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a40eeba4a6034450bc055b8f62c763520) | 現在のマイクのシステムキャプチャ音量に変更発生|
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad87c12c924b781b3b8429f8e8aafc338) | 現在のシステムの再生音量に変更発生 |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a296665d16719c02dc055c983f88b40c3) | システム音声キャプチャが正常に開始されたかどうかのイベントコールバック（Macシステムのみに適用） |
| [onTestMicVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a9f0101fa8222c6163f1b23fcce81e22b) | マイクテスト時の音量のコールバック |
| [onTestSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a04bb10b06af17cdc43b7831336736539) | スピーカーテスト時の音量のコールバック |

### カスタムメッセージ受信イベントコールバック
| API             | 説明               |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0a5690652db3902e98e1168bad12ec1a) | カスタムメッセージ受信のイベントコールバック |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab5d0cb61c24b77ecdb177ff19fc95075) | カスタムメッセージ消失のイベントコールバック |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab364b929cd0d9ffff6e47c20ec52372c) | SEIメッセージ受信のコールバック |

### CDN関連イベントコールバック
| API             | 説明               |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a345ab7b45a9d0027926dbf580e8e0258) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングのイベントコールバックの公開を開始 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a8e046f5bd34498b13ae057caaab64913) | Tencent Cloud CSS CDNへのオーディオビデオストリーミングの公開停止のイベントコールバック|
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a16164548764979e84d3b5301f28890ff) | 非Tencent Cloud CDNへのオーディオビデオストリーミングのイベントコールバックの公開を開始|
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0da75e040521c0945c3735f4893e6c09) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開停止のイベントコールバック |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0f11cee9e2659f7ea8484fdffd6b8583) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータ設定のイベントコールバック |

### 画面共有関連イベントコールバック
| API             | 説明               |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a8baff9a6c699ea1d82c5e7abb6ded97b) | 画面共有開始のイベントコールバック|
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a32acecdafd9058cc7d70a3abe6995051) | 画面共有一時停止のイベントコールバック |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a63c073daf1ad93cfa2e6c79695434e22) | 画面共有再開のイベントコールバック|
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4d182e6b60d8be536e69253d906af84d) | 画面共有停止のイベントコールバック |
| [onScreenCaptureCovered](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a490f827ffd6e7728a6ec49cba63875b1) | 画面共有のターゲットウィンドウブロックのイベントコールバック（Windows OSのみに適用） |

### ローカルレコーディングおよびローカルスクリーンキャプチャのイベントコールバック
| API             | 説明               |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4a40b1b338d93c871f73354d1d45f24b) | ローカルレコーディングタスク開始済みのイベントコールバック |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0b226b8e627dad7850a880d48ffb91dd) | ローカルレコーディングタスク実行中の進捗のイベントコールバック |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4455252d3e0f5d869db18641e24da106) | ローカルレコーディングタスク完了済みのイベントコールバック |
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a10501027a79d1d05231319570c0e5603) | ローカルスクリーンキャプチャ完了のイベントコールバック |

### 破棄されたイベントコールバック
| API             | 説明               |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad606b861a3545832fb4821a7e0230925) | キャスターが現在のルームに入室（破棄済み） |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#abbc4fe2ccac90f77c80f55d46d6c8951) | キャスターが現在のルームを退室（破棄済み）|
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aab3c91276b6e570ea9acfe1581e1aa51) | オーディオエフェクト再生が完了済み（破棄済み） |
| [onPlayBGMBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad93b8204416558e63c18349bf29ff592) | BGMの再生を開始（破棄済み） |
| [onPlayBGMProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a1879cc4e50492431a3346828e9130f21) | BGMの再生進捗のコールバック（破棄済み） |
| [onPlayBGMComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#abaf89c758a4dd21e21db488e997bef2a) | BGMの再生が完了済み（破棄済み） |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a455264cfcf2a7a3f022f3bce0659f9f7) | サーバースピードテストの結果のコールバック（破棄済み） |

### ビデオデータカスタムコールバック
| API             | 説明               |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aea602851c96370558a7eeb850d7eb6b8) | カスタムビデオレンダリングのコールバック |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aa416979597d1bec68dc268a9432619ae) | サードパーティによる美顔コンポーネントを結合するためのビデオ処理のコールバック |

### オーディオデータカスタムコールバック
| API             | 説明               |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a1488e35460441c351cab75d9702498f6) | ローカルマイクがキャプチャしたオリジナルオーディオデータのコールバック |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#affb432a77f938d1e8dfb6c0d5488dbcf) | ローカルがキャプチャし、オーディオモジュールで前処理したオーディオデータのコールバック |
| [onPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab841da62beb88a9fa9bce58d25df6f23) | 音声ミキシング前のリモートユーザーごとのオーディオデータ|
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a6649f62d4138d9bc73ae484e63dec081) | 各再生待ちオーディオをミキシングし、最終的にシステムに送信して再生する前のデータコールバック |

### その他イベントコールバックインターフェース
| API             | 説明               |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a2fa3d9997c9810ffa6a95e0a7a4a50d0) | ローカルLOGのプリントコールバック |

### ビデオ関連列挙値の定義
| API             | 説明               |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gace04ad7a0bf531f4d09dc6a540f09f95) | ビデオ解像度|
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaa6787a9059d7b725a30ffcf9f4aabb64) | ビデオアスペクト比モード |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga461563be214e8f0579a79741f37d18e3) | ビデオストリームタイプ |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga496a32286104187149b4e40284cbfb36) | ビデオ画面塗りつぶしモード |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga4f8ab82260baa03f83f123ebeaa82b2e) | ビデオ画面回転方向 |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga46f49720df57d17b267054cb9ee4d079) | 美顔（美肌）アルゴリズム |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga98b07c6c79303f486682b3b92fa88c7e) | ビデオピクセル形式 |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga3a075ea5603cdd730550b37fc0032c68) | ビデオデータ伝達方式 |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga778fcc2797d6076745997327c8b20009) | ビデオのイメージタイプ |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga65de3d8416c7faabe1a8b77a6fd9cc7c) | ローカルビデオスクリーンキャプチャのデータソース |

### ネットワーク関連列挙値の定義
| API             | 説明               |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaa57f4545ef7331e3157eee1639d28780) |ユースケース |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga42ff820a33d9f3535d203fd5d6782cb5) | ロール |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga6615b296e31fc3d03c0df92e9755b5aa) | トラフィックコントロールモード（破棄済み） |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga60efcaeea7692bbce8dc362856683319) | 画質の好み |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCQualityInfo) | ネットワーク品質 |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga9ab84e3f9458dacd479937e5a24c95f2) | ビデオステータスタイプ |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga37b6311e4d5ba7376070ba65de520865) | ビデオステータス変更理由のタイプ |

### オーディオ関連列挙値の定義
| API             | 説明               |
|-----|-----|
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga96f3d4cdcf3baa9df39ab4e1b3f0eb40) | 音声音質 |

### その他列挙値の定義
| API             | 説明               |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gafa83683b4840bcb3200d1da63c10276d) | Logレベル |
| [TRTCScreenCaptureSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gad96fcfd4a65c0f99579b0c35ef86645d) | 画面共有のターゲットタイプ（デスクトップのみに適用） |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaec50c849a17b7706f6989d718fc6b7df) | クラウドミクスストリーミングのレイアウトモード|
| [TRTCLocalRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga92580ecee493fb524b84234305316238) | メディアレコーディングタイプ |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga323584f89d0479be0a1b554ec05672f7) | ミクスストリーミング入力タイプ |
| [TRTCDeviceType](https://liteav.sdk.qcloud.com/doc/api/en/namespaceliteav.html#abaf3d3254d2b2e11fb2064478975be17) | デバイスタイプ（デスクトッププラットフォームのみに適用） |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga5adbddb520b6eea48142c3b5be740205) | オーディオレコーディングコンテンツタイプ |

### TRTCコアタイプの定義
| API             | 説明               |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCParams) | 入室パラメータ |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVideoEncParam) | ビデオコーデックパラメータ |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCNetworkQosParam) | ネットワークトラフィックコントロール（Qos）パラメータセット |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCRenderParams) | ビデオ画面のレンダリングパラメータ |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCQualityInfo) | ネットワーク品質 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVolumeInfo) | 音量レベル |
| [TRTCSpeedTestParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSpeedTestParams) | スピードテストのパラメータ |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSpeedTestResult) | ネットワークスピードテスト結果 |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVideoFrame) |ビデオフレーム情報 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioFrame) | オーディオフレームデータ |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ac5b1947f21f77726cbff822eaf0003f9) | クラウドミクスストリーミングにおける各画面の説明情報 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCTranscodingConfig) | クラウドミクスストリーミングのレイアウトおよびトランスコードパラメータ |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCPublishCDNParam) | 非Tencent Cloud CDNへのオーディオビデオストリーミングの公開時に設定が必要な転送パラメータ |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioRecordingParams) | ローカルオーディオファイルのレコーディングパラメータ |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCLocalRecordingParams) | ローカルメディアファイルのレコーディングパラメータ |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioEffectParam) | オーディオエフェクトパラメータ（破棄済み） |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSwitchRoomConfig) | ルーム切り替えパラメータ |
| [TRTCAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioFrameCallbackFormat) | オーディオカスタムコールバックの形式パラメータ |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCScreenCaptureSourceInfo) | 画面共有のターゲット情報（デスクトップのみに適用） |
| [ITRTCScreenCaptureSourceList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#classliteav_1_1ITRTCScreenCaptureSourceList) | 共有可能な画面およびウィンドウのリスト |

