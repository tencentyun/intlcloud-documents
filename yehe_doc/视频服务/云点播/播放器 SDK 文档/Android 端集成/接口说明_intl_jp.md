## TXVodPlayer

### VODプレーヤー

[TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html)をご参照ください。
主に指定されたVODストリーミングアドレスからオーディオビデオデータをプルし、デコードとローカルレンダリング再生を行う役割を担います。
プレーヤーには次の機能が含まれます。

- FLV、MP4、HLSという複数の再生形式をサポートし、基本再生（URL再生）およびVOD再生（Fileid再生）という2つの再生方式をサポートしています。
- スクリーンキャプチャにより、現在の再生ストリームのビデオ画面を切り取ることができます。
- ジェスチャー操作により、明るさ、音量、進行状況などを調節できます。
- 解像度は手動で切り替えることも、ネットワーク帯域幅に応じてアダプティブに選択することもできます。
- 様々な倍速再生を指定でき、イメージおよびハードウェアアクセラレーションを有効にすることもできます。
- 完全な機能については、[VOD Super Player - 機能リスト](https://intl.cloud.tencent.com/document/product/266/38295)をご参照ください。

### プレーヤー設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ae69bc2dd060217e595c38f0dc819290a) | プレーヤーのコンフィグレーション情報を設定します。コンフィグレーション情報については[TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html) をご参照ください。|
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | プレーヤーのビデオレンダリングTXCloudVideoViewを設定します。                        |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aeb2f15f370d50b6261b7832f02a0f411) | プレーヤーのビデオレンダリングTextureViewを設定します。                             |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | プレーヤーのビデオレンダリングSurfaceViewを設定します。                             |
| setStringOption                                              | プレーヤーの業務パラメータを`<String,Object>`の形式で設定します。                |

### 再生基本インターフェース  
| API                                                          | 説明                       |
| ------------------------------------------------------------ | --------------------------- |
| [startVodPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a32fe5a77dedc7fc903345f00e6c47c3a) | HTTP URL形式のアドレスを再生します。バージョン10.7からは、`startPlay`が`startVodPlay`に変更になり、正常に再生を行うには、`V2TXLivePremier#setLicence`または`TXLiveBase#setLicence`でのLicenseの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicense、UGSV Licenseおよびビデオ再生Licenseがすべて使用できます。 |
| [startVodPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a32fe5a77dedc7fc903345f00e6c47c3a) | fileId形式で再生し、TXPlayInfoParamsパラメータを渡します。バージョン10.7からは、`startPlay`が`startVodPlay`に変更になり、正常に再生を行うには、`V2TXLivePremier#setLicence`または`TXLiveBase#setLicence`でのLicenseの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicense、UGSV Licenseおよびビデオ再生Licenseがすべて使用できます。 |
| [ stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | 再生を停止します。|
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | 再生されているかどうか。      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | 再生を一時停止し、ストリームデータの取得を停止し、最後のフレームを保持します。|
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a41de8150eff044a237990c271d57ea27) | 再生を再開し、ストリームデータを再取得します。|
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | 指定した時点のビデオストリームにジャンプします。秒単位です。|
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aa5d7fcf690ac3a1102ffa3c02192674d) | 指定した時点のビデオストリームにジャンプします。ミリ秒単位です。|
| [getCurrentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a128b89dd39053d6d19d262a5f45110cd) | 現在の再生位置を取得します。秒単位です。|
| [getBufferDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#acebd6ae9dd87e10c8959a24d3b6d5e7f) | キャッシュの合計時間を取得します。秒単位です。|
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a83ee44393f1e0db930be75b73ff47812) | 合計時間を取得します。秒単位です。|
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a37cb584556d48d043b93dfec33c40a97) | 再生可能時間を取得します。秒単位です。|
| [getWidth](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a67a0997183f24da19b776d96c1052998) | ビデオ幅を取得します。|
| [getHeight](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a07efb2a4e9a982688c8bb3c3f21d1092) | ビデオの高さを取得します。|
| [setAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5e0e3d950eb3f525634adc7a9f60eab7) | VODがstartVodPlay後に自動的に再生されるかどうかです。デフォルトでは自動再生します。 |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a8f767f79fb69496cdbc532fced5dff33) | 再生開始時間を設定します。|
| [setToken](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5f9eadc88ca97238f84226462f095536) | HLSのtokenを暗号化します。|
| [setLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a3f5ae863c82509d1ed266503e8138781) | ループ再生するかどうかを設定します。|
| [isLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aaa3fcc823e0fce316dea1cc9162f1c8e) | ループ再生ステータスであるかどうかを返します。|

### ビデオ関連インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | ビデオのハードデコードを有効または無効にします。                                       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6f1c0c128052960f084ef6d1d7a77b09) | 現在のビデオフレーム画像を取得します。<br>**注：現在のフレーム画像の取得には時間がかかるため、スクリーンショットは非同期でコールバックされます。**|
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a4add579d2ec825502c5e3832aced5bc1) | ミラーリングを設定します。                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#add2bcd36c051900d697853155494865b) | オンデマンドの再生レートを設定します。デフォルトは1.0です。                                |
| [getBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#af6f9e1e680baa611642fb168007b1c45) | 現在再生されているビットレートのインデックスを返します。                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a61f524a6ed275edaf9e9a0997f64d491) | 現在再生されているビットレートインデックスを設定し、シャープネスをシームレスに切り替えます。シャープネスの切り替えには、しばらく待つ必要がある場合があります。|
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | [画像タイル表示モード](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)を設定します。|
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | [画像レンダリング角度](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)を設定します。|

### オーディオ関連インターフェース

| API                                                          | 説明                                   |
| ------------------------------------------------------------ | --------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | 再生をミュートするかどうかを設定します。                      |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | 音量を設定します。範囲：0 ～ 100。           |
| [setRequestAudioFocus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a676f0935eca038719f58100d31f169b1) | オーディオフォーカスを自動的に取得するかどうかを設定します。デフォルトでは自動的に取得されます。|

### イベント通知インターフェース

| API                    | 説明                   |
| ---------------------- | ---------------------- |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a0735b006fe8c56875665cb66881af144) | プレーヤーのコールバックを設定します（廃止されました。[setVodListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61)の使用を推奨します）。|
| [setVodListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61) | プレーヤーのコールバックを設定します。                                 |
| [onNotifyEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a1e4be8c3cfef68a8909d66a9243b6ec5) | オンデマンド再生イベント通知。                                 |
| [onNetSuccess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ae6febac01c1cba85f8fe387a0c14d9d0) | オンデマンド再生ネットワークステータス通知。                             |
| [onNetFailed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a74942758292eb41138c7a01ed9056da2) | 再生fileIdネットワーク例外通知。                         |

### TRTC関連インターフェース

次のインターフェースを使用して、オンデマンドプレーヤーからのオーディオビデオストリームをTRTC経由でプッシュすることができます。TRTCサービスの詳細については、[TRTC製品の概要](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ad6bd04b37a89012102e7bb71ea5554a6) | オンデマンドは[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)サービスにバインドされています。|
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5b947acf9f4fc992f0f02f8d87de3334) | オンデマンド[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)サービスにバインド解除されます。|
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a8298f704cb659c725da28a27e08afbed) | ビデオストリームのプッシュを開始します。                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aaa6ecf72bfa9e35078561dd98d62be0c) | ビデオストリームのプッシュをキャンセルします。                                             |
| [ publishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | オーディオストリームのプッシュを開始します。                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a206d786a74ae3b71766755135161773e) | オーディオストリームのプッシュをキャンセルします。                                             |

## ITXVodPlayListener

Tencent Cloud VODのコールバック通知です。
### SDK基本コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXVodPlayListener__android.html#aad1d875808cd4a68d429762e492aad05) | オンデマンド再生イベント通知については、[再生イベントリスト](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a)、[イベントパラメータ](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)をご参照ください。|
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXVodPlayListener__android.html#a2be0a0294ae21e68e736ac8fa4d3085d) | オンデマンドプレーヤー[ネットワークステータス通知](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737)。|

## TXVodPlayConfig

VODプレーヤー設定クラスです。

### 基本設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | プレーヤーの再接続回数を設定します。                                         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | プレーヤーの再接続間隔を設定します。秒単位です。                                 |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#ae44a6096c42cdb61adc10370ca2a42b6) | プレーヤー接続タイムアウトを設定します。秒単位です。                             |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a6ad0d546e6da3abacd5d4ea8bd6f94de) | オンデマンドキャッシュディレクトリを設定します。MP4、HLSのオンデマンドは有効です。                       |
| [setMaxCacheItems](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#acc2f17764df9bb52163dac9faf81f11e) | キャッシュファイルの数を設定します。インターフェースが破棄されました。TXPlayerGlobalSetting#setMaxCacheSizeを使用してグローバル設定をしてください。|
| [setPlayerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a3594024855210dc07f50a6d7c5f8b088) | プレーヤーのタイプを設定します。                                             |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | カスタムHTTPヘッダを設定します。                                    |
| [setEnableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a3caff179964976945f3754f1ec48a42b) | 正確なseekを実行するかどうかを設定します。デフォルトはtrueです。                               |
| [setAutoRotate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#ab360b681c220c2adb57de2758916b227) | MP4ファイルの再生時にYESに設定すると、ファイル内の回転角度に基づいて自動的に回転します。<br>回転角度はPLAY_EVT_CHANGE_ROTATIONイベントから取得できます。デフォルト値はYESです。|
| [setSmoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a23fb393011e4663d0dfa765b72665a46) | マルチビットレートHLSをスムーズに切り替えます。デフォルト値はfalseです。                             |
| [setCacheMp4ExtName](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#aaeccb662be133d4ded4fc17df29b94b5) | MP4ファイル拡張子をキャッシュします。                                        |
| [setProgressInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a01a46ce89e4979a6397b6deb2525007c) | 再生位置のコールバック間隔を設定します。ミリ秒単位です。                                 |
| [setMaxBufferSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a2705841bfedb3c44839cc355eaad26dc) | 最大プリロードサイズ（単位MB）。                                    |
| setMaxPreloadSize                                            | プリロードされた最大バッファサイズをMB単位で設定します。                           |
| setExtInfo                                                   | 拡張情報を設定します。                                               |
| setPreferredResolution                                       | 複数のビットストリームのHLSを再生する場合、設定されたpreferredResolutionに基づいて最適なビットストリームを選択して再生を開始するが、preferredResolutionは幅と高さの積(width*height)であり、再生開始前に設定します。|

## TXPlayerGlobalSetting

VODプレーヤーグロバール設定クラス

| API                                                          | 説明                   |
| ------------------ | ------------------------------------------------------------ |
| setCacheFolderPath | 再生エンジンのcacheディレクトリを設定します。設定後、オフラインダウンロード、プレダウンロード、プレーヤーなどが優先的にこのディレクトリから読み込まれ、保存されます |
| setMaxCacheSize    | 再生エンジンの最大キャッシュサイズを設定します。設定すると、設定値に基づいてCacheディレクトリのファイルが自動的にクリーンアップされます。単位MB。|

## TXVodPreloadManager

オンデマンドプレーヤーのプリダウンロードインターフェースクラス

| API                                                          | 説明                   |
| ------------ | ------------------------------------------------------------ |
| getInstance  | TXVodPreloadManagerインスタンスオブジェクトを取得します。シングルトンモードです。                    |
| startPreload | プリダウンロードを開始する前に、再生エンジンのキャッシュディレクトリを設定してください。TXPlayerGlobalSetting#setCacheFolderPathとキャッシュサイズ。TXPlayerGlobalSetting#setMaxCacheSize。|
| stopPreload  | プリダウンロードを停止します。                                                   |

## TXVodDownloadManager 

オンデマンドプレーヤーのビデオダウンロードインターフェースクラス。現在はネストされていないm3u8ビデオソースのダウンロードのみがサポートされており、simpleAES暗号化ビデオソースはTencent Cloudのプライベート暗号化アルゴリズムで暗号化され、セキュリティが向上します。

| API                                                          | 説明                   |
| ------------------------ | ------------------------------------------------------------ |
| getInstance              | TXVodDownloadManagerインスタンスオブジェクトを取得します。シングルトンモードです。                   |
| setHeaders               | ダウンロードHTTPヘッダーを設定します。                                               |
| setListener              | ダウンロードのコールバックメソッドを設定します。ダウンロード前に設定しておく必要があります。                             |
| startDownloadUrl         | URL方式でダウンロードを開始します。                                          |
| startDownload            | fileid方式でダウンロードを開始します。                                         |
| stopDownload             | ダウンロードを停止し、ITXVodDownloadListener.onDownloadStopがコールバックに成功しました。|
| deleteDownloadMediaInfo  | ダウンロード情報を削除します。                                                 |
| getDownloadMediaInfoList | すべてのユーザーのダウンロードリスト情報を取得します。                                   |
| getDownloadMediaInfo     | ダウンロード情報を取得します。                                   |

## ITXVodDownloadListener

Tencent Cloudビデオダウンロードコールバック通知。

| API                | 説明                                         |
| ------------------ | -------------------------------------------- |
| onDownloadStart    | ダウンロード開始                                     |
| onDownloadProgress | ダウンロードの進行状況の更新                                 |
| onDownloadStop     | ダウンロード停止                                     |
| onDownloadFinish   | ダウンロードの終了                                     |
| onDownloadError    | ダウンロード中にエラーが発生しました                           |


## TXVodDownloadDataSource

Tencent CloudビデオFildidはダウンロード元です。ダウンロード時にパラメータとして渡されます。

| API                        | 説明                                         |
| ------------------         | -------------------------------------------- |
| TXVodDownloadDataSource    | appid、fileid、quality、pSign、usernameなどの引数を渡す構造関数                                    |
| getAppId  | 渡したappidの取得                                |
| getFileId  | 渡したfileidの取得                                |
| getPSign     | 渡したpsignの取得                                     |
| getQuality   | 渡したqualityの取得                                     |
| getUserName    | 渡したuserNameを取得します。デフォルトは「default」です。                          |


## TXVodDownloadMediaInfo

Tencent Cloudビデオダウンロード情報。ダウンロードの進行状況や再生リンクなどの情報を入手することができます

| API                        | 説明                                         |
| ------------------         | -------------------------------------------- |
| getDataSource    | fileidダウンロード時に渡したfileidダウンロード元を取得します                                    |
| getDuration  | ダウンロードの合計時間を取得します                                |
| getPlayableDuration  | ダウンロードした再生可能時間を取得します                                |
| getSize     | ダウンロードファイルの合計サイズを取得します。fileidダウンロード元に対してのみ有効です           |
| getDownloadSize   | ダウンロードされたファイルのサイズを取得します。fileidダウンロード元に対してのみ有効です                                    |
| getProgress    | 現在のダウンロードの進行状況を取得します                         |
| getPlayPath    | 現在の再生パスを取得し、TXVodPlayerの再生に渡すことができます                         |
| getDownloadState    | ダウンロードステータスを取得します                       |
| isDownloadFinished    | ダウンロードが完了したかどうかの判断                       |


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

| code | イベント定義                   | 意味説明                                                    |
| ------ | ------------------------------------- | ------------------------------------------------------- |
| \-2301 | PLAY\_ERR\_NET\_DISCONNECT            | ネットワーク接続が切断され、かつ複数回再接続しても再開できません。これ以上のリトライを行うには、ご自身で再生を再起動してください。   |
| \-2305 | PLAY\_ERR\_HLS\_KEY                   | HLS復号keyの取得に失敗しました。                                      |
| 2101   | PLAY\_WARNING\_VIDEO\_DECODE\_FAIL    | 現在のビデオフレームのデコードに失敗しました。                                         |
| 2102   | PLAY\_WARNING\_AUDIO\_DECODE\_FAIL    | 現在のオーディオフレームのデコードに失敗しました                                           |
| 2103   | PLAY\_WARNING\_RECONNECT              | ネットワーク接続が切断され、自動再接続が有効にされています（再接続回数が3回を超えるとPLAY\_ERR\_NET\_DISCONNECTがスローされます）。|
| 2106   | PLAY\_WARNING\_HW\_ACCELERATION\_FAIL | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください。                                     |
| \-2304 | PLAY\_ERR\_HEVC\_DECODE\_FAIL         | H265のデコードに失敗しました。                                              |
| \-2303 | PLAY\_ERR\_FILE\_NOT\_FOUND           | 再生ファイルが存在しません。                                           |
