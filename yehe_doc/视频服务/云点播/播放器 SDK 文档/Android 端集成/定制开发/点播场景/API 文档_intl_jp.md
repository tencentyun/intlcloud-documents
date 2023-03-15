## TXVodPlayer

### VODプレーヤー

[TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html)をご参照ください。
主に指定されたVODストリーミングアドレスからオーディオビデオデータをプルし、デコードとローカルレンダリング再生を行う役割を担います。
プレーヤーには次の機能が含まれます。

- FLV、MP4、HLSという複数の再生形式をサポートし、基本再生（URL再生）およびVOD再生（Fileid再生）という2つの再生方式をサポートしています。
- スクリーンキャプチャにより、現在の再生ストリームのビデオ画面を切り取ることができます。
- ジェスチャー操作により、明るさ、音量、進行状況などを調節できます。
- 解像度は手動で切り替えることも、ネットワーク帯域幅に応じてアダプティブに選択することもできます。
- 様々な倍速再生を指定でき、イメージおよびハードウェアアクセラレーションを有効にすることもできます。
- 完全な機能については、[Player+ - 機能リスト](https://www.tencentcloud.com/document/product/266/38295)をご参照ください。

### プレーヤー設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ae69bc2dd060217e595c38f0dc819290a) | プレーヤー設定情報を設定します。設定情報については[TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html)をご参照ください。 |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a64eefab5bdb76cef17f609560eec5830) |　プレーヤーのビデオレンダリングTXCloudVideoViewを設定します。                      |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aeb2f15f370d50b6261b7832f02a0f411) | プレーヤーのビデオレンダリングTextureViewを設定します。                           |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | プレーヤーのビデオレンダリングSurfaceViewを設定します。                           |
| [setStringOption](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a23eedd175a85f171cb7c34638bab0c45) | プレーヤーの業務パラメータを設定します。パラメータの形式は`<String,Object>`です。            |

### 再生基本インターフェース  
| API                                                          | 説明                                                  |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a32fe5a77dedc7fc903345f00e6c47c3a) | HTTP URL形式のアドレスを再生します。                              |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac255cbe3a0481014f3d8aa4a6ca4d581) | fileId形式で再生し、TXPlayInfoParamsパラメータを渡します。        |
| [startPlayDrm](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a1e8443952146701507adb219d8b992b1) | DRMで暗号化されたビデオを再生します。                                     |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | 再生を停止します。                                            |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | 再生中かどうかです。                                        |
| [pause](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | 再生を一時停止し、ストリーミングデータの取得を停止し、最後の1フレームの画面を保持します。           |
| [resume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a41de8150eff044a237990c271d57ea27) | 再生を再開し、ストリーミングデータを再取得します。                            |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | ビデオストリームの指定した時点にジャンプします。単位は秒です。                      |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aa5d7fcf690ac3a1102ffa3c02192674d) | ビデオストリームの指定した時点にジャンプします。単位はミリ秒です。                    |
| [getCurrentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a128b89dd39053d6d19d262a5f45110cd) | 現在の再生位置を取得します。単位は秒です。                            |
| [getBufferDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#acebd6ae9dd87e10c8959a24d3b6d5e7f) | キャッシュの総時間を取得します。単位は秒です。                            |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a83ee44393f1e0db930be75b73ff47812) | 総時間を取得します。単位は秒です。                                  |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a37cb584556d48d043b93dfec33c40a97) | 再生可能時間を取得します。単位は秒です。                              |
| [getWidth](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a67a0997183f24da19b776d96c1052998) |  ビデオの幅を取得します。                                        |
| [getHeight](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a07efb2a4e9a982688c8bb3c3f21d1092) | ビデオの高さを取得します。                                        |
| [setAutoPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5e0e3d950eb3f525634adc7a9f60eab7) | オンデマンドがstartPlayになると自動的に再生を開始するかどうかを設定します。デフォルトでは自動再生されます。|
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a8f767f79fb69496cdbc532fced5dff33) | 再生開始時間を設定します。                                    |
| [setToken](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5f9eadc88ca97238f84226462f095536) | HLSのtokenを暗号化します。                                   |
| [getEncryptedPlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#acc32bf00b94774e5314cb733f9f339df) | 強化暗号化再生キーを取得します。                                |
| [setLoop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a3f5ae863c82509d1ed266503e8138781) | ループ再生するかどうかを設定します。                                    |
| [isLoop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aaa3fcc823e0fce316dea1cc9162f1c8e) | ループ再生状態であるかどうかを返します。                                |

### ビデオ関連インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | ビデオのハードデコードを有効または無効にします。                                       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6f1c0c128052960f084ef6d1d7a77b09) | 現在のビデオフレーム画像を取得します。<br/>**注意：現在のフレーム画像の取得は比較的時間がかかる操作のため、スクリーンキャプチャは非同期的なコールバックによって行われます。** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a4add579d2ec825502c5e3832aced5bc1) | ミラーリングを設定します。                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#add2bcd36c051900d697853155494865b) | オンデマンドの再生レートを設定します。デフォルトは1.0です。                                |
| [getBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#af6f9e1e680baa611642fb168007b1c45) | 現在再生されているビットレートのインデックスを返します。                                     |
| [getSupportedBitrates](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aedacfbc888f5446ab2318ea3a7199700) | 再生アドレスがHSLの際、サポートしているビットレート（解像度）のリストを返します。            |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a61f524a6ed275edaf9e9a0997f64d491) | 現在再生されているビットレートインデックスを設定し、シャープネスをシームレスに切り替えます。シャープネスの切り替えには、しばらく待つ必要がある場合があります。|
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | [画像タイリングモード](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)を設定します。 |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | [画像レンダリング角度](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)を設定します。 |

### オーディオ関連インターフェース

| API                                                          | 説明                                   |
| ------------------------------------------------------------ | --------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | 再生をミュートするかどうかを設定します。                      |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | 音量を設定します。範囲：0 ～ 100。           |
| [setRequestAudioFocus](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a676f0935eca038719f58100d31f169b1) | オーディオフォーカスを自動的に取得するかどうかを設定します。デフォルトでは自動的に取得されます。|

### イベント通知インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a0735b006fe8c56875665cb66881af144) | プレーヤーのコールバックを設定します（廃止されている場合、[setVodListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61)の使用をお勧めします）。|
| [setVodListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61) | プレーヤーのコールバックを設定します。                                           |

### TRTC関連インターフェース

次のインターフェースによって、VODプレーヤーのオーディオビデオストリームをTRTCでプッシュすることができます。その他のTRTCサービスについては、[TRTC製品概要](https://cloud.tencent.com/document/product/647/16788)をご参照ください。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ad6bd04b37a89012102e7bb71ea5554a6) | VODを[TRTC](https://cloud.tencent.com/document/product/647/16788)サービスにバインドします。 |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5b947acf9f4fc992f0f02f8d87de3334) | VODと[TRTC](https://cloud.tencent.com/document/product/647/16788)サービスとのバインドを解除します。 |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a8298f704cb659c725da28a27e08afbed) | ビデオストリームのプッシュを開始します。                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aaa6ecf72bfa9e35078561dd98d62be0c) | ビデオストリームのプッシュをキャンセルします。                                             |
| [ publishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | オーディオストリームのプッシュを開始します。                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a206d786a74ae3b71766755135161773e) | オーディオストリームのプッシュをキャンセルします。                                             |

## ITXVodPlayListener

Tencent Cloud VODのコールバック通知です。
### SDK基本コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPlayListener__android.html#aad1d875808cd4a68d429762e492aad05) | VOD再生イベント通知です。[再生イベントリスト](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a)、[イベントパラメータ](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)をご参照ください。 |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPlayListener__android.html#a2be0a0294ae21e68e736ac8fa4d3085d) | VODプレーヤーの[ネットワーク状態通知](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737)です。 |

## TXVodPlayConfig

VODプレーヤー設定クラスです。

### 基本設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | プレーヤーの再接続回数を設定します。                                         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | プレーヤーの再接続間隔を設定します。秒単位です。                                 |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ae44a6096c42cdb61adc10370ca2a42b6) | プレーヤー接続タイムアウトを設定します。秒単位です。                             |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a6ad0d546e6da3abacd5d4ea8bd6f94de) | このインターフェースは廃止されているため、非推奨です。<br/>VODキャッシュディレクトリを設定します。MP4、HLSのVODが有効です。 |
| [setMaxCacheItems](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#acc2f17764df9bb52163dac9faf81f11e) | このインターフェースは廃止されているため、非推奨です。<br/>キャッシュするファイルの個数を設定します。            |
| [setPlayerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a3594024855210dc07f50a6d7c5f8b088) | このインターフェースは廃止されているため、非推奨です。<br>プレーヤーのタイプを設定します。             |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | カスタムHTTPヘッダを設定します。                                    |
| [setEnableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a3caff179964976945f3754f1ec48a42b) | 正確なseekを実行するかどうかを設定します。デフォルトはtrueです。                               |
| [setAutoRotate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ab360b681c220c2adb57de2758916b227) | MP4ファイルの再生時にYESに設定すると、ファイル内の回転角度に基づいて自動的に回転します。<br>回転角度はPLAY_EVT_CHANGE_ROTATIONイベントから取得できます。デフォルト値はYESです。|
| [setSmoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a23fb393011e4663d0dfa765b72665a46) | マルチビットレートHLSをスムーズに切り替えます。デフォルト値はfalseです。                             |
| [setCacheMp4ExtName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#aaeccb662be133d4ded4fc17df29b94b5) | MP4ファイル拡張子をキャッシュします。                                        |
| [setProgressInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a01a46ce89e4979a6397b6deb2525007c) | 再生位置のコールバック間隔を設定します。ミリ秒単位です。                                 |
| [setMaxBufferSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a2705841bfedb3c44839cc355eaad26dc) | 最大プリロードサイズ（単位MB）。                                    |
| [setMaxPreloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a78d73bb26332151cbf5f8aa10240a4a5) | プリロードの最大バッファサイズを設定します。単位はMBです。                           |
| [setExtInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a080c7ab4f3b6f06e690561889eca3594) | 拡張情報を設定します。                                               |
| [setPreferredResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a369c5980be4748b11216a686482e910f) | 再生HLSに複数のコードストリームがある場合、設定したpreferredResolutionに応じて、最適なコードストリームを選択して再生を開始します。preferredResolutionは幅と高さを乗算（width * height）します。再生開始前に設定された場合のみ有効です。 |
| [setOverlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#abd8626115358e211fcbc5347a34b2e18) | HLSのセキュリティ強化暗号化/復号keyを設定します。                                |
| [setOverlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#adcdc2c60303e4b67757583904836dfab) | HLSのセキュリティ強化暗号化/復号Ivを設定します。                                 |
| [setEnableRenderProcess](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ab48a6ca2e64a61942f714c2b74710ba8) | ロード後にレンダリングの後処理サービスを許可するかどうか。                               |
| [setMediaType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a532518afe8abf910920278a0c21f225f) | メディア資産のタイプを設定します。デフォルトはautoタイプです。                             |

## TXPlayerGlobalSetting

VODプレーヤーグロバール設定クラス

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__android.html#adf3cf9c0b96e7eeb97b5e9ed56743df8) | 再生エンジンのcacheディレクトリを設定します。設定後、オフラインダウンロード、プリダウンロード、プレーヤーなどは優先的にこのディレクトリから読み取りおよび保存します |
| [setMaxCacheSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__android.html#a27de4890873400d4d4ff2c624138786d) | 再生エンジンの最大キャッシュのサイズを設定します。設定後は設定値に応じて自動的にCacheディレクトリのファイルをクリーンアップします。単位はMBです。 |

## TXVodPreloadManager

オンデマンドプレーヤーのプリダウンロードインターフェースクラス

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | --------------------------------------------- |
| [getInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#a9e52c1e94ef4b2a35fdb6dfbf89f5e92) | TXVodPreloadManagerインスタンスオブジェクトを取得します。シングルトンパターンです。 |
| [startPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#a1968e49655bc231c54247f9189176911) | プリダウンロード起動前に、再生エンジンのキャッシュディレクトリを設定してください。  |
| [stopPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#aa8425852d9c185f71b3933ac61834c5c) | プリダウンロードを停止します。                                  |

## ITXVodPreloadListener

ビデオプリダウンロードのコールバックインターフェースです。

| API               | 説明               |
| ------------------------------------------------------------ | ---------------- |
| [onComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPreloadListener__android.html#a2004a619f03a97617661985f0f79a767) | ビデオプリダウンロード完了です。 |
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPreloadListener__android.html#aac11d56117d32f2e1bf6afafb940db77) | ビデオプリダウンロードのエラーです。 |

## TXVodDownloadManager 

オンデマンドプレーヤーのビデオダウンロードインターフェースクラス。現在はネストされていないm3u8ビデオソースのダウンロードのみがサポートされており、simpleAES暗号化ビデオソースはTencent Cloudのプライベート暗号化アルゴリズムで暗号化され、セキュリティが向上します。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a84b3db42095ccb149b8f9be57ecdc0cc) | TXVodDownloadManagerインスタンスオブジェクトを取得します。シングルトンパターンです。               |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) |ダウンロードするHTTPヘッダーを設定します。                                           |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a123ff28866dca6b525f1f2defde28199) | ダウンロードのコールバック方法を設定します。ダウンロードする前に必ず設定してください。                           |
| [startDownloadUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a3e6424357de962092cff42d4c1a68654) | URL方式でダウンロードを開始します。                                        |
| [startDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a1d58d3e216c1016eb8d5cc051dd300f7) | fileid方式でダウンロードを開始します。                                     |
| [stopDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a86b884a71a6a11e729a964478612ed65) | ダウンロードを停止します。ITXVodDownloadListener.onDownloadStopコールバック時に停止が完了します。 |
| [deleteDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a0dab7dad33ef2b555abf31f07ab6447d) | ダウンロード情報を削除します。                                               |
| [getDownloadMediaInfoList](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#ad82cf86e7bad17efa86df162a4286a05) | すべてのユーザーのダウンロードリスト情報を取得します。                                 |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#ac8b38266ea66940fdd406487ff45a2fd) | ダウンロード情報を取得します。                                               |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a7e03beed3e30d3243b91853856da9d53) | ダウンロード情報を取得します。                                               |

## ITXVodDownloadListener

Tencent Cloudビデオダウンロードコールバック通知。

| API                                                          | 説明                                            |
| ------------------------------------------------------------ | ----------------------------------------------- |
| [onDownloadStart](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a3cbbd786c51f86aba84a182edd054343) | ダウンロードを開始                                         |
| [onDownloadProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a4dd74690b9ed22442ba9956d29d69b32) | ダウンロードの進行状況の更新                                    |
| [onDownloadStop](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#ac70254aa0f35a4ba01fc8de93214112b) | ダウンロードの停止                                        |
| [onDownloadFinish](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a0b6eb0287eea736f84ebe8c212ab2219) | ダウンロード終了                                        |
| [onDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#ae0faac6397f8df5a2d1e57e56e6e4ec3) | ダウンロードプロセスで発生したエラー                              |
| [hlsKeyVerify](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a206077037e4a5f8ef81707ec82514523) | HLSをダウンロードし、暗号化されたファイルに遭遇すると、復号keyを外部チェッカーに渡します |


## TXVodDownloadDataSource

Tencent CloudビデオFildidはダウンロード元です。ダウンロード時にパラメータとして渡されます。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TXVodDownloadDataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aef4a9306eddebbd7920089e48e09b260) | コンストラクタです。appid、fileid、quality、pSign、username などのパラメータを渡します |
| [getAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ab95e1b8c990ed3e41fc623e5e9ed47c3) | 渡されたappidを取得します                                             |
| [getFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aae60f2e5054da59d0f2d239d0e673cc8) | 渡されたfileidを取得します                                            |
| [getPSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aa7c355a0046a91c5f302f1602b985462) | 渡されたpsignを取得します                                             |
| [getQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ab03cb85fa393531d1fb702ab1e92008f) | 渡されたqualityを取得します                                           |
| [getUserName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ae3cc9307a896bbfcf570a0d077708f58) | 渡されたuserNameを取得します。デフォルトは「default」です                           |
| [getToken](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a20c1ba8630591cc399a35a7abc535728) | 渡されたtokenを取得します                                             |
| [getOverlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a8cceb76d2594cecb6615652a854e3245) | 渡されたoverlayKeyを取得します                                        |
| [getOverlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a86ac7a9d6239880059fc109128c9bb4b) | 渡されたoverlayIvを取得します                                         |

### 解像度のId定数

| code | 定数の定義                                                     | 意味の説明 |
| ---- | ------------------------------------------------------------ | -------- |
| 0    | [QUALITY_OD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#abb1129f5ddec88f4eb579e96afdd741a) | オリジナル画像     |
| 1    | [QUALITY_FLU](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a5b5a1363633c76ecfb35dea5daf3e0b2) | LD     |
| 2    | [QUALITY_SD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aad857cb177a777ba09aed2a312a3fe1f) | SD     |
| 3    | [QUALITY_HD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a70195f7d2882bf1918f599ff1c555717) | HD     |
| 4    | [QUALITY_FHD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aff4ebd940acb1937be588b6eb7879183) | FHD   |
| 5    | [QUALITY_2K](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a69635e7ebfc9895b840c7a5f1817e7b3) | 2K       |
| 6    | [QUALITY_4K](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a35eb8012dab226b7d0714ad98560715d) | 4K       |
| 1000 | [QUALITY_UNK](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a3380895e1edc2eb4394cac5d2b40fda5) | 定義されていません   |

## TXVodDownloadMediaInfo

Tencent Cloudビデオダウンロード情報。ダウンロードの進行状況や再生リンクなどの情報を入手することができます

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | -------------------------------------------- |
| [getDataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#ab8d408191666ef004ae7d1e4f8d4840a) | fileidダウンロード時に渡されたfileidダウンロードソースを取得します         |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a08c13081c0665a4336a0f022c955fb69) | ダウンロードの総時間を取得します                             |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#aea8be4cac1aaa5b79a1c3faf13ece59c) | ダウンロードした再生可能時間を取得します                       |
| [getSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a3c4029b904a61a9873e6d12785ce19a1) | ダウンロードファイルの合計サイズを取得します。fileidダウンロードソースにのみ有効です |
| [getDownloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#ab2ab8161365b107da0cf398c2e683533) | ダウンロードファイルの合計サイズを取得します。fileidダウンロードソースにのみ有効です |
| [getProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#afdfeed8666fff88f32b73cbd1d3a2770) | 現在のダウンロードの進行状況を取得します                             |
| [getPlayPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a52f40379c9ced15ea1d26d800ad6ac4b) | 現在の再生パスを取得します。TXVodPlayerに渡して再生することができます    |
| [getDownloadState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a2184d61558a641a71115c9efe9ad3a48) | ダウンロードのステータスを取得します                                 |
| [isDownloadFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#aed26755c5919fc7125e4e2400d30d1bc) | ダウンロードが完了したかどうかを判断します                             |

### 静的属性

| code | 属性の定義                                                     | 意味の説明   |
| ---- | ------------------------------------------------------------ | ---------- |
| 0    | [STATE_INIT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a1ac9cfa17538972c579f1bff39c2fe83) | 初期状態のダウンロード |
| 1    | [STATE_START](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a89be56b1eb6cd1441eae8ee501a995e1) | ダウンロードの開始   |
| 2    | [STATE_STOP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a88533f2a5acf4b41400bd14feeab9106) | ダウンロードの停止   |
| 3    | [STATE_ERROR](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a7474da17fe98cc77b5bfd257f5f39317) | ダウンロードのエラー   |
| 4    | [STATE_FINISH](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#abd0a89abf65650e0e16b613e34d8466f) | ダウンロードの完了   |

## TXPlayerAuthBuilder

fileIdにより暗号化したビデオの設定を再生します。

| API                                                          | 説明                   |
| ------------------------------------------------------------ | -------------------- |
| [setAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#a0b43955512510cd5c4930c236f3666bb) | アプリケーションappIdです。          |
| [setFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#abd423a3f7b11333d1b68506e25e4b77e) | ファイルidです。             |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#ac8cc3ccb3adfc2533c4a8fa97274625d) | タイムアウトタイムスタンプに暗号化リンクします。 |
| [setExper](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#a9855f630f9444c767a8085d68892faa1) | プレビュー時間です。           |
| [setUs](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#aca22d76e37e78b330084f6b228594894) | 固有の識別リクエストです。       |
| [setSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#afb81925d434438d6903b8016b0f26d8d) | リンク不正アクセス防止署名です。         |
| [setHttps](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#adcd67a70185ef7680ecfe0162aee0273) | httpsリクエストを用いるかどうかです。    |

## TXBitrateItem

ビデオビットレートの情報です。

| API                                                          | 説明                       |
| ------------------------------------------------------------ | -------------------------- |
| [index](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a750b5d744c39a06bfb13e6eb010e35d0) | m3u8ファイルの番号です。        |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a2474a5474cbff19523a51eb1de01cda4) | このストリームのビデオ幅です。           |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#ad12fc34ce789bce6c8a05d8a17138534) | このストリームのビデオの高さです。           |
| [bitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#ab5d8e1788d02d0e52941a0778776e289) | このストリームのビデオビットレートです。           |
| [compareTo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a1062863c4ed9def2a8af6edb834792a0) | 2つのストリームのビットレートが同じかどうかを比較します。 |

## TXImageSprite

スプライトイメージの解析タイプです。

| API                                                          | 説明                            |
| ------------------------------------------------------------ | ---------------------------------- |
| [TXImageSprite](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a0daa097ae5eaabb45ce5899d641108be) | コンストラクタです。                         |
| [setVTTUrlAndImageUrls](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#aea98e261dc8911344659a9e6c113f8e8) | スプライトイメージのアドレスを設定します。                   |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a16a3b680fcd8da1468d3ccfe675d47ed) | サムネイルを取得します。                       |
| [release](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a23b477d0e2d399f75d585d154c346591) | 使用完了呼び出しを行わないと、メモリ漏洩を起こします。 |

## TXPlayerDrmBuilder

DRM再生情報です。

| API                                                          | 説明                   |
| ------------------------------------------------------------ | --------------------- |
| [TXPlayerDrmBuilder](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#acee757f8bcb8d6af23f4963184f7b791) | DRM再生情報のオブジェクトを構築します。 |
| [setProvisionUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#a5f55511af44ef3e6619988d4002d1aa5) | 証明書プロバイダのurlを設定します。   |
| [setKeyLicenseUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#ac293b2b09e849a2b54382180c44dc37f) | 復号key urlを設定します。     |
| [setPlayUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#ad3970dca8235512ed26d2afd492de595) | 再生メディアのurlを設定します。   |

## TXPlayInfoParams

fileIdによりビデオパラメータ情報を再生します。

| API                                                          | 説明                   |
| ------------------------------------------------------------ | ------------------------ |
| [TXPlayInfoParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#a1f5bbdc7d3a4817ace0ff64e70af964c) | コンストラクタです。               |
| [getAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#ab95e1b8c990ed3e41fc623e5e9ed47c3) | アプリケーションidを取得します。             |
| [getFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#aae60f2e5054da59d0f2d239d0e673cc8) | ファイルidを取得します。             |
| [getPSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#aa7c355a0046a91c5f302f1602b985462) | Tencent Cloudビデオ暗号化署名を取得します。 |



## エラーコードリスト

### 一般的なイベント

| code | イベントの定義                   | 意味の説明                                                    |
| ---- | -------------------------- | ----------------------------------------------------------- |
| 2004 | PLAY_EVT_PLAY_BEGIN        | ビデオ再生を開始します（進捗インジゲータが表示されている場合は、この時点で停止します）。                |
| 2005 | PLAY_EVT_PLAY_PROGRESS     | ビデオ再生の進行状況です。現在の再生の進行状況、ロードの進行状況および全体の長さを通知します。      |
| 2007 | PLAY_EVT_PLAY_LOADING      | ビデオ再生をloading中です。再開できれば、その後にLOADING_ENDイベントが発生します。 |
| 2014 | PLAY_EVT_VOD_LOADING_END   | ビデオ再生ロードを終了します。ビデオは引き続き再生されます。                       |
| 2006 | PLAY_EVT_PLAY_END          | ビデオ再生を終了します。                                              |
| 2013 | PLAY_EVT_VOD_PLAY_PREPARED | プレーヤーの準備が整い、再生可能になりました。                                |
| 2003 | PLAY_EVT_RCV_FIRST_I_FRAME | ネットワークが最初のレンダリング可能なビデオデータパッケージ（IDR）を受信しました。                   |
| 2009 | PLAY_EVT_CHANGE_RESOLUTION | ビデオ解像度を変更します。                                            |
| 2011 | PLAY_EVT_CHANGE_ROTATION   | MP4ビデオの回転角度です。                                          |



### 警告イベント

| code   | イベントの定義                              | 意味の説明                                                     |
| ------ | ------------------------------------- | ------------------------------------------------------------ |
| \-2301 | PLAY\_ERR\_NET\_DISCONNECT            | ネットワーク接続が切断され、かつ複数回再接続しても再開できません。これ以上のリトライを行うには、ご自身で再生を再起動してください。   |
| \-2305 | PLAY\_ERR\_HLS\_KEY                   | HLS復号keyの取得に失敗しました。                                      |
| 2101   | PLAY\_WARNING\_VIDEO\_DECODE\_FAIL    | 現在のビデオフレームのデコードに失敗しました。                                         |
| 2102   | PLAY\_WARNING\_AUDIO\_DECODE\_FAIL    | 現在のオーディオフレームのデコードに失敗しました                                           |
| 2103   | PLAY\_WARNING\_RECONNECT              | ネットワーク接続が切断され、自動再接続が有効にされています（再接続回数が3回を超えるとPLAY\_ERR\_NET\_DISCONNECTがスローされます）。|
| 2106   | PLAY\_WARNING\_HW\_ACCELERATION\_FAIL | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください。                                     |
| \-2304 | PLAY\_ERR\_HEVC\_DECODE\_FAIL         | H265のデコードに失敗しました。                                              |
| \-2303 | PLAY\_ERR\_FILE\_NOT\_FOUND           | 再生ファイルが存在しません。                                           |

## Player+の定数

次の定数10.0バージョンから、`TXVodConstants`により対外的に提供を開始します。

### 画像タイリングモード

| code | イベントの定義                                                     | 意味の説明           |
| ---- | ------------------------------------------------------------ | ------------------ |
| 0    | [RENDER_MODE_FULL_FILL_SCREEN](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0645160ad90c67581f7f226a6c0c46ae) | ビデオ画面のフルスクリーン   |
| 1    | [RENDER_MODE_ADJUST_RESOLUTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7bc7babd208fa82866f80e9340a5354c) | ビデオ画面のアダプティブ画面 |

### 画像レンダリング角度

| code | イベントの定義                                                     | 意味の説明 |
| ---- | ------------------------------------------------------------ | -------- |
| 0    | [RENDER_ROTATION_PORTRAIT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad00f3ee125e574cab63d955e03f5f23f) | 標準縦画面 |
| 270  | [RENDER_ROTATION_LANDSCAPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga17bdfecb387ddb3b34a96a0474bd73e3) | 右に90度回転 |

### 再生イベントリスト

| code  | イベントの定義                                                     | 意味の説明                       |
| ----- | ------------------------------------------------------------ | ------------------------------ |
| 2003  | [VOD_PLAY_EVT_RCV_FIRST_I_FRAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad745daba38f53e17c19f648e51246044) | ネットワークが最初のビデオデータパッケージ(IDR)を受信  |
| 2004  | [VOD_PLAY_EVT_PLAY_BEGIN](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gada58f2a016424a22d053ff02818b705e) | ビデオ再生開始                   |
| 2005  | [VOD_PLAY_EVT_PLAY_PROGRESS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga69a17c951f665b929c0ced3e946b41b0) | ビデオ再生の進行状況                   |
| 2006  | [VOD_PLAY_EVT_PLAY_END](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9a4e84bd9d9e9c7ae1db0cfd3875e74a) | ビデオ再生の終了                   |
| 2007  | [VOD_PLAY_EVT_PLAY_LOADING](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga755928f9307a228f5b94c054fe888384) | ビデオ再生のLoading                |
| 2008  | [VOD_PLAY_EVT_START_VIDEO_DECODER](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7c3fc61aaa8865bccee4deb0b237f9e0) | デコーダ起動                     |
| 2009  | [VOD_PLAY_EVT_CHANGE_RESOLUTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa02aa77b481d6817ddd60ca3cad7131e) | ビデオ解像度の変更                 |
| 2010  | [VOD_PLAY_EVT_GET_PLAYINFO_SUCC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaebd8ad6fe4c09ebb9205422ed072b61f) | VODファイルの情報取得が成功しました           |
| 2011  | [VOD_PLAY_EVT_CHANGE_ROTATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga440c3d89bec97cea7170d293d590d5fd) | ビデオ回転情報                   |
| 2013  | [VOD_PLAY_EVT_VOD_PLAY_PREPARED](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga81e281a76a84d61f9f76cc45d51b7bd7) | ビデオのロード完了                   |
| 2014  | [VOD_PLAY_EVT_VOD_LOADING_END](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga22ef1d7404af3661eb6b600a6e6399fd) | loading終了                    |
| 2026  | [VOD_PLAY_EVT_RCV_FIRST_AUDIO_FRAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaecd3bbe2687021e769985deb88bd04ce) | オーディオ初回再生                   |
| 2103  | [VOD_PLAY_WARNING_RECONNECT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga029b64e10522699e622bd42706d10f65) | ネットワーク接続が切断され、自動再接続が開始されました       |
| -2301 | [VOD_PLAY_ERR_NET_DISCONNECT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae0ebb051cf1166a8c71cd0b981d260cc) | ネットワーク接続が切断され、かつ複数回再接続しても再開できません |
| -2303 | [VOD_PLAY_ERR_FILE_NOT_FOUND](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga1e71f9fdafabb1bd16fab933c308d070) | ファイルが存在しません                     |
| -2304 | [VOD_PLAY_ERR_HEVC_DECODE_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga79b7f1b580d0cab34fc5616ae474660f) | h265デコードに失敗しました                   |
| -2305 | [VOD_PLAY_ERR_HLS_KEY](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa3130bf22ec63513ddca17ef3a24267a) | HLS復号keyの取得に失敗しました             |
| -2306 | [VOD_PLAY_ERR_GET_PLAYINFO_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0b2d0a807f32a21c215eb0d523d1ba67) | VODファイルの情報取得に失敗しました           |
| 2106  | [VOD_PLAY_WARNING_HW_ACCELERATION_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaf669a195862852295bbfd67d77143097) | ハードウェアデコードの開始に失敗しました。ソフトフェアデコードを使用してください         |
| -5    | [VOD_PLAY_ERR_INVALID_LICENSE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gafde8fcf56aeef512220ea06e92db2e40) | licenseが不正のため、再生に失敗しました       |

### 再生イベントのパラメータ

| イベントの定義                                                     | 意味の説明                     |
| ------------------------------------------------------------ | ---------------------------- |
| [EVT_UTC_TIME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gafee483734d4d3a831a30c602406e77d6) | UTC時間                      |
| [EVT_TIME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga5cb5e37938b510270847d4f5c751a594) | イベントの発生時間                 |
| [EVT_DESCRIPTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga103453280f89ab536f1cc18f7b3cbf53) | イベントの説明                     |
| [EVT_PARAM1](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad627c73ec08206efdd221293acc5e716) | イベントのパラメータ1                    |
| [EVT_PARAM2](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa15b5dbb07de07d1b2dbe14cfcd4c3f8) | イベントのパラメータ2                    |
| [EVT_PLAY_COVER_URL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga40e4910ac679c2301b56d2b353782c45) | ビデオカバー                     |
| [EVT_PLAY_URL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gac913635a62c07ee774965c946db60cae) | ビデオのアドレス                     |
| [EVT_PLAY_NAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga018b2b66f3393288356448fd2520049b) | ビデオ名                     |
| [EVT_PLAY_DESCRIPTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga78f0b6a56bce879ab53e5c955ae9b72a) | ビデオの概要                     |
| [EVT_PLAY_PROGRESS_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0aa1661deb8e647fab5fd9f49e80c7f9) | 再生の進行状況（ミリ秒）             |
| [EVT_PLAY_DURATION_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga3abe5f92aa39728811ef148c2a9ad830) | 再生の総時間（ミリ秒）             |
| [EVT_PLAY_PROGRESS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga3f1f479ffccbb042f9fdf3f21a3276fc) | 再生の進行状況                     |
| [EVT_PLAY_DURATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga2c453eed399f105eec5803a3894ad81d) | 再生の総時間                     |
| [EVT_PLAYABLE_DURATION_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga315c2ebea16fbabde6dfa05b46365ec1) | VOD再生可能時間（ミリ秒）       |
| [EVT_PLAYABLE_RATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gab00428b5d3902980f809f281ab3113cd) | 再生速度                     |
| [EVT_PLAYABLE_DURATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga27916804840b52c8b012c65f23f5295c) | VOD再生可能時間               |
| [EVT_IMAGESPRIT_WEBVTTURL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gac5b62b9cd23553e5caa4ea25b8093594) | スプライトイメージweb vtt説明ファイルのダウンロードURL |
| [EVT_IMAGESPRIT_IMAGEURL_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8b4b82a700fad6dc290c6b9df836b379) | スプライトイメージ画像のダウンロードURL            |
| [EVT_DRM_TYPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8f621b0e05158b432a9bfce15b51929d) | 暗号化のタイプ                     |
| [EVT_CODEC_TYPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9aea07e52f99dfc5ce83e627207c3013) | ビデオコーデックのタイプ                 |
| [EVT_KEY_FRAME_CONTENT_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaf27d14de4e5ba1057f1687fb953bf0d6) | ビデオキーフレームの説明情報           |
| [EVT_KEY_FRAME_TIME_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaad3ea1d65ffad606f0e72b45229c883a) | キーフレーム時間                   |

### 再生ネットワーク状態の通知パラメータ

| イベントの定義                                                     | 意味の説明            |
| ------------------------------------------------------------ | ------------------- |
| [NET_STATUS_CPU_USAGE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga66b91ad00c61489fc2d7465999d1a77a) | CPU使用率           |
| [NET_STATUS_VIDEO_WIDTH](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga12f4f516e8a103c43cf1fd3409e3a076) | 解像度のwidth       |
| [NET_STATUS_VIDEO_HEIGHT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaccbc5e1a57b7575b7ecf812cb939002e) | 解像度のheight      |
| [NET_STATUS_VIDEO_FPS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga2ceaa8d4f26f94231cceb46ebc1ec01f) | 現在のビデオフレームレート        |
| [NET_STATUS_VIDEO_GOP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gacd77aba1bb25077ecd03269c311479b8) | 現在のビデオGOP         |
| [NET_STATUS_VIDEO_BITRATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa7190fc964cf23a567b56d9793ad5737) | ビデオデータのビットレート      |
| [NET_STATUS_AUDIO_BITRATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae77d554c71c9e298e09ae39cde8ff698) | オーディオデータのビットレート      |
| [NET_STATUS_NET_SPEED](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae2899ec3669bbf6261cead660c6e797c) | ネットワークの速度            |
| [NET_STATUS_AUDIO_CACHE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga71bf377ea1925873217c1c5ee600af53) | オーディオのフレーム数            |
| [NET_STATUS_VIDEO_CACHE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9e8fcc05e66967e0eb3348da202c7cde) | ビデオのフレーム数            |
| [NET_STATUS_AUDIO_INFO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga4107d46355fbcb54973cdfb82f25a2f4) | 現在のストリームのオーディオ情報    |
| [NET_STATUS_NET_JITTER](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga04f0c226d2b7571d07f118e05f43dc3a) | ネットワークジッターの状況        |
| [NET_STATUS_SERVER_IP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0d7111f8bfbb9aba0d2ea9e2c8d6d7bd) | 接続先ServerのIPアドレス |
| [NET_STATUS_VIDEO_DPS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga1ef238d0f43788fa5a5e01ea3d1cfce7) | 現在のデコーダの出力フレームレート  |
| [NET_STATUS_QUALITY_LEVEL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8f86732d6a56638c8697c20e614c8d68) | ネットワークの品質            |

### プレーヤーメディア資産のタイプ

| code | イベントの定義                                                     | 意味の説明                  |
| ---- | ------------------------------------------------------------ | ------------------------- |
| 0    | [MEDIA_TYPE_AUTO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7d204fdc431c5c3ffea9f5da094edf5f) | autoタイプ                  |
| 1    | [MEDIA_TYPE_HLS_VOD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae915784aa6e5b694a599cb79bb5f6051) | アダプティブビットレート再生のhls VODメディア資産 |
| 2    | [MEDIA_TYPE_HLS_LIVE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gacf7595f6e4617ad0da6e120ada7c7605) | アダプティブビットレート再生のhlsライブストリーミングメディア資産 |

### 未分類の変数

| code | イベントの定義                                                     | 意味の説明            |
| ---- | ------------------------------------------------------------ | ------------------- |
| -1   | [INDEX_AUTO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa49e56e7580286e85bce4c88feddb057) | アダプティブビットレートのindex識別 |
