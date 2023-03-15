## TXVodPlayer

### VODプレーヤー

[TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html)をご参照ください。
主に指定されたVODストリーミングアドレスからオーディオビデオデータをプルし、デコードとローカルレンダリング再生を行う役割を担います。
プレーヤーには次の機能が含まれます。

- FLV、MP4、HLSという複数の再生形式をサポートし、基本再生（URL再生）およびVOD再生（Fileid再生）という2つの再生方式をサポートしています。
- スクリーンキャプチャにより、現在の再生ストリームのビデオ画面を切り取ることができます。
- ジェスチャー操作により、明るさ、音量、進行状況などを調節できます。
- 解像度は手動で切り替えることも、ネットワーク帯域幅に応じてアダプティブに選択することもできます。
- 様々な倍速再生を指定でき、イメージおよびハードウェアアクセラレーションを有効にすることもできます。
- 完全な機能については、[Player+ - 機能リスト](https://intl.cloud.tencent.com/document/product/266/38295)をご参照ください。

### プレーヤー設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [config](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3ad68ed80140f20cf3229bf344886a04) | VOD設定です。設定情報については[TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html)をご参照ください。 |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | startPlay後すぐに再生するかどうか。デフォルト値はYESです。                         |
| [setToken](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | HLSのtokenを暗号化します。この値を設定すると、プレーヤーはURL内のファイル名の前に`voddrm.token.TOKENTextureView`を自動的に追加します。|
| [loop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1cdc15a39387295573f41caee9a05932) | SurfaceViewをループ再生するかどうか。                                   |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | ビデオレンダリングのコールバック。（ハードウェアデコードのみがサポートされます）|
| [setExtentOptionInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a842c8863f91f274031be0109a5cb28f5) | プレーヤーの業務パラメータを設定します。パラメータの形式は`<NSString *, id>`です             |

### 再生基本インターフェース  
| API                                                          | 説明                                           |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ac1af59fe9e4bc2b390661787097d2c8b) | HTTP URL形式の再生アドレスです。                       |
| [startPlayDrm:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaa492de602b58d75b0489435b20be811) | 標準Fairplay drm再生を起動します。                 |
| [startPlayWithParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a0b4db90eafbc8c4d9be498e5ffefe961) | fileId形式で再生します。                           |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | 再生を停止します。                                     |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8438e3403946accc1986a05b89ee7b03) | 再生中かどうかです。                                 |
| [pause](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | 再生を一時停止し、ストリーミングデータの取得を停止し、最後の1フレームの画面を保持します。    |
| [resume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a41de8150eff044a237990c271d57ea27) | 再生を再開し、ストリーミングデータを再取得します。                     |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | ビデオストリームの指定した時点にジャンプします。単位は秒です。               |
| [currentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8b0ca7fda398996b355179bd9a479785) | 現在の再生位置を取得します。単位は秒です。                     |
| [duration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7fd4f66e650bd1656a97d1db7fabaeda) | 総時間を取得します。単位は秒です。                           |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a4acb1f7a723d342f7bfb9c5e540e5e77) | 再生可能時間を取得します。単位は秒です。                       |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3eeed61a3424d2f907c8a1e420fddf6d) | ビデオの幅を取得します。                                 |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a822ae85493a742654ba563619492b26a) | ビデオの高さを取得します。                                 |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a41001e6276c4853500f78579d6bd2218) | 再生開始時間を設定します。                             |
| [setupVideoWidget:insertIndex:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a370c35a44549bad3a162741c288b8eb8) | VideoレンダリングViewを作成します。このコントロールはビデオコンテンツの表示をロードしています。 |
| [removeVideoWidget](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#adf77d29895e70602556fdc51b931951e) | VideoレンダリングViewを削除します。                            |

### ビデオ関連インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9646437dc38d7dcce8c32dfec5d0bc5b) | 現在のビデオフレーム画像を取得します。<br>**注：現在のフレーム画像の取得には時間がかかるため、スクリーンショットは非同期でコールバックされます。**|
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaf347826e1a9fad9998c0eea9791ed0c) | ミラーリングを設定します。                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | オンデマンドの再生レートを設定します。デフォルトは1.0です。                                |
| [bitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9a325ed94acf6b545c88755855449a12) | 現在再生されているビットレートのインデックスを返します。                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1aa8e1f3a63b46c8a1166447e2457abc) | 現在再生されているビットレートインデックスを設定し、シャープネスをシームレスに切り替えます。<br>シャープネスの切り替えには、しばらく待つ必要がある場合があります。|
| [supportedBitrates](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1c7f996e3c1e5ec04fe3f3b184491495) | 再生アドレスがmaster playlistの際、サポートしているビットレート（解像度）を返します。     |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | [画像タイリングモード](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)を設定します。 |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | [画像レンダリング角度](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)を設定します。 |
| [enterPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ae0118065e4d29cb7dbab4ccd0ba6b3e5) | ピクチャーインピクチャー機能に移動します。                                             |
| [exitPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a5f0bc0ade6e99f31392f6f8d897ae84c) | ピクチャーインピクチャー機能から退出します。                                             |

### オーディオ関連インターフェース

| API                                                          | 説明                       |
| ------------------------------------------------------------ | ----------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | 再生をミュートするかどうかを設定します。            |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ac92633d1cdfff1f93f48b7aec1d35b98) | 音量を設定します。範囲：0 ～ 100。|

### イベント通知インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | イベントコールバックです。[vodDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79)の使用をお勧めします。 |
| [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) | プレーヤーのコールバックを設定します。                                           |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | ビデオレンダリングのコールバックです（ハードウェアデコードのみサポート）。                                 |

### TRTC関連インターフェース

次のインターフェースによって、VODプレーヤーのオーディオビデオストリーミングをTRTCでプッシュすることができます。その他のTRTCサービスについては、[TRTC製品概要](https://cloud.tencent.com/document/product/647/16788)をご参照ください。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#affcfcba7937a7ef88a918afb0b3d73bc) | VODを[TRTC](https://cloud.tencent.com/document/product/647/16788)サービスにバインドします。 |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a5b947acf9f4fc992f0f02f8d87de3334) | VODと[TRTC](https://cloud.tencent.com/document/product/647/16788)サービスとのバインドを解除します。 |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8298f704cb659c725da28a27e08afbed) | ビデオストリームのプッシュを開始します。                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaa6ecf72bfa9e35078561dd98d62be0c) | ビデオストリームのプッシュをキャンセルします。                                             |
| [ publishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | オーディオストリームのプッシュを開始します。                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a206d786a74ae3b71766755135161773e) | オーディオストリームのプッシュをキャンセルします。                                             |

### タイプ方法

| API                                                          | 説明                                             |
| ------------------------------------------------------------ | ------------------------------------------------- |
| [getEncryptedPlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#acdb2823140afb92657f840b7b765636d) | 強化暗号化再生キーを取得します。                            |
| [isSupportPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a2b0eae752e8cd548572e747a85602c71) | Picture In Picture機能（「ピクチャーインピクチャー」機能）をサポ－トするかどうかです。 |

## TXVodPlayListener

Tencent Cloud VODのコールバック通知です。
### SDK基本コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent:event:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a6330db18bb40862fc2d66474fc34166b) | VOD再生イベント通知です。[再生イベントリスト](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a)、[イベントパラメータ](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)をご参照ください。 |
| [onNetStatus:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a08721fef1ba130fd182de4bed3b4430e) | VODプレーヤーの[ネットワーク状態通知](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737)です。 |
| [onPlayer:pictureInPictureStateDidChange:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#ac0e5e698f62a9d8a58b0e8e63fc8afb1) | ピクチャーインピクチャー状態のコールバックです。                                             |
| [onPlayer:pictureInPictureErrorDidOccur:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a4dcee189760af5752bd112a725994d0b) | ピクチャーインピクチャーエラー状態のコールバックです。                                         |

## TXVodPlayConfig

VODプレーヤー設定クラスです。

### 基本設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [connectRetryCount](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ad89d728973fb42eced3ac18be873af1b) | プレーヤーの再接続回数を設定します。                                         |
| [connectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a07fde7cd21980c096b5bbd93aed137d5) | プレーヤーの再接続間隔を設定します。秒単位です。                                 |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a39233eb85b4cbae04411577510e7c5e6) | プレーヤー接続タイムアウトを設定します。秒単位です。                             |
| [cacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aec1a8f0064562368fe3c2df4f7fb72eb) | このインターフェースは廃止されているため[TXPlayerGlobalSetting##setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html)の使用をお勧めします。  <br>VODキャッシュディレクトリを設定します。VOD MP4、HLSは有効です。 |
| [maxCacheItems](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aedbc9cc868baa2c44e3badbe6fdf4a43) | このインターフェースは廃止されているため[TXPlayerGlobalSetting#setMaxCacheSizeMB](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html)の使用をお勧めします。<br>キャッシュファイルの個数を設定します。 |
| [playerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a4595fb5853016c5e5919324e71ad6f4c) | プレーヤーのタイプを設定します。                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ad69aaf8885027863ea19657425ef1974) | カスタムHTTP headersを設定します。                                    |
| [enableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ada91e71bad4df942e6190650915a7728) | 正確なseekを実行するかどうかを設定します。デフォルトはtrueです。                               |
| [autoRotate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa1a372684aaaf95b9b17abf0c7a4e6c6) | MP4ファイルの再生時にYESに設定すると、ファイル内の回転角度に基づいて自動的に回転します。<br>回転角度はPLAY_EVT_CHANGE_ROTATIONイベントから取得できます。デフォルト値はYESです。|
| [smoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa1caeddde1f950ec7965dcc721109928) | マルチビットレートHLSをスムーズに切り替えます。デフォルト値はfalseです。                             |
| [progressInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a943e212cbd5e3d89de0529ab7c6042fb) | 再生位置のコールバック間隔を設定します。ミリ秒単位です。                                 |
| [maxBufferSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa4934cef81784d3a195a5d95a43953f5) | 最大プリロードサイズで、単位はMBです。                                    |
| [maxPreloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3ae31483070f62cf35abd9003ccce0e0) | プリロードの最大バッファサイズを設定します。単位はMBです。                           |
| [firstStartPlayBufferTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a5a6373341623385672a12e9e3617c1c2) | 最初のキャッシュにロードする必要があるデータ時間を設定します。単位はmsで、デフォルト値は100msです。          |
| [nextStartPlayBufferTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ab17865763b40e7d86913dd2c6fb3110f) | バッファ時（バッファデータが不十分であることによる二次バッファ、またはseekによるドラッグバッファ）に少なくともどのくらいのデータをキャッシュするとバッファを終了できるかです。単位はmsで、デフォルト値では250msです。 |
| [overlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#adc41276c8fa265cb622657b581ba3f3b) | HLSのセキュリティ強化暗号化/復号keyを設定します。                                |
| [overlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3de0b922b54d46f11a8e203026d44fed) | HLSのセキュリティ強化暗号化/復号Ivを設定します。                                 |
| [extInfoMap](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a55b7d33d270ac9004aad798bd6027879) | 拡張情報を設定します。                                               |
| [preferredResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#afcfb593028655bbac25a753f8ffe9904) | 再生HLSに複数のコードストリームがある場合、設定したpreferredResolutionに応じて最適なコードストリームを選択して再生を開始します *。preferredResolutionは幅と高さを乗算（width * height）します。再生開始前に設定された場合のみ有効です。 |
| [enableRenderProcess](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3b7f6694446ab09764315f003192fc5a) | ロード後にレンダリングの後処理サービス(例えば超解像プラグインサービス）を許可するかどうかです。デフォルトでは有効です。     |
| [playerPixelFormatType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ac1ae36ec22cc49f49ceb7842cb86be3b) | ビデオレンダリングオブジェクトコールバックのビデオ形式です。                                 |
| [keepLastFrameWhenStop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ace241f4953a14aac301ecd1e196de3f8) | stopPlayの際に、最後の1フレームの画面を保持するかどうかです。デフォルト値はNOです。           |
| [mediaType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a5877610faab7f5148bc34072a0c92a5b) | メディア資産タイプを設定します。                                               |
|                                                              |                                                              |

## TXPlayerGlobalSetting

VODプレーヤーグロバール設定クラス

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__ios.html#a604b66ab880e7a5d056ce5c3132ddf48) | 再生エンジンのcacheディレクトリを設定します。設定後、プリダウンロード、プレーヤーなどは優先的にこのディレクトリから読み取りおよび保存します |
| [setMaxCacheSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__ios.html#ad511345d985ae9bc271a1e867c3f71f0) | 再生エンジンの最大キャッシュのサイズを設定します。設定後は設定値に応じて自動的にCacheディレクトリのファイルをクリーンアップします。単位はMBです。 |

## TXVodPreloadManager

オンデマンドプレーヤーのプリダウンロードインターフェースクラス

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a84882e4d61f22f51a18d3b639d881138) | TXVodPreloadManagerインスタンスオブジェクトを取得します。シングルトンパターンです。                |
| [startPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#af67a02c9fba5c07f83b2d36d24b764fd) | プリダウンロードを有効化する前に、まず再生エンジンのキャッシュディレクトリTXPlayerGlobalSetting#setCacheFolderPathとキャッシュサイズTXPlayerGlobalSetting#setMaxCacheSizeを設定してください。 |
| [stopPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a5c29884349c8f6436eff8f70f302d33e) | プリダウンロード停止                                                   |

### ビデオプリダウンロードのコールバック

| API                                                          | 説明         |
| ------------------------------------------------------------ | -------------- |
| [onComplete:url:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#aa887ac7b6bcf155eb22816f880eed270) | ダウンロード完了のコールバックです。 |
| [onError:url:error:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a07e337f1e638e458a3e761507deec525) | ダウンロードエラーのコールバックです。 |

## TXVodDownloadManager

オンデマンドプレーヤーのビデオダウンロードインターフェースクラス

### TXVodDownloadDataSource

| API                                                          | 説明                   |
| ------------------------------------------------------------ | ------------------------- |
| [auth](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a59eb64ffe11d0bdee5c67009f5ebdd8c) | fileid情報                |
| [quality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ab674303410c354ab3d0d6957b86dcf14) | ダウンロードの解像度、デフォルトのオリジナル画像      |
| [token](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a2f0d5a61a262b1362f51c943b6a03f17) | アドレスの暗号化のように、tokenを入力してください |
| [templateName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0c960f307400330cb261513cde7c2906) | 解像度のテンプレート                |
| [fileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a66c446aeaf5eef1ee21764d4bdf7b8ae) | ファイルのId                    |
| [pSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0411129c1f5cf0bdfac7baabeb12c7a2) | 署名の情報                  |
| [appId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a5b3217c0ab223c526d557b09d2b0d6c0) | アプリケーションのappIdです。入力必須です          |
| [userName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac38202c6f4861ad216f9fbc5d962b5ab) | アカウント名                  |
| [overlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adc41276c8fa265cb622657b581ba3f3b) | HLS EXT-X-KEY暗号化/復号パラメータ  |
| [overlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a3de0b922b54d46f11a8e203026d44fed) | 暗号化/復号パラメータoverlayIv      |

### TXVodDownloadMediaInfo

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | ------------------------------- |
| [isDownloadFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#aca53b9773ade9052bc8ff2592bea0c01) | ダウンロードが完了したかどうかです                    |
| [dataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a74a85fcd734fe688c3a65083dc815a6a) | fileidダウンロードオブジェクト（オプション）          |
| [url](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a43481294fa1d2f0ebe7cff14b17726cc) | ダウンロードアドレス                        |
| [userName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac38202c6f4861ad216f9fbc5d962b5ab) | アカウント名                        |
| [duration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac6e4b2a3cf932b33832d4e4e4e7cd0de) | 時間                            |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a1945ed3669e000f80e294331d6c302b4) | 再生可能時間                      |
| [size](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a439227feff9d7f55384e8780cfc2eb82) | ファイルの合計サイズで、単位はbyteです          |
| [downloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a15989d553be239ea233f9957236fa767) | すでにダウンロードしたサイズで、単位はbyteです          |
| [segments](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a32e4172d8952ac9f1db668982da57128) | セグメンテーションの総数                        |
| [downloadSegments](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac2e85e36301b166ed1bb92844f6f5399) | すでにダウンロードしたセグメンテーションの数                  |
| [progress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac7abb4766cd3f65c31f56279d7decff8) | 進行状況                            |
| [playPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a6567e969a0aa9ef88a4a2ff601ea8527) | 再生パスです。TXVodPlayerに渡して再生することができます |
| [speed](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a218b4f7c6cc2681a99c23a3b089d68b1) | ダウンロード速度で、byte毎秒です              |
| [downloadState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ae87c7de3c7e2888cfe6298bc25c4f9be) | ダウンロードの状態                        |

### TXVodDownloadManager

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [shareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a8a1039302b46bec56fcc15c2ffdcbf16) | TXVodDownloadManagerインスタンスオブジェクトを取得します。シングルトンパターンです。               |
| [setDownloadPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a5ca035da8c8f8771f08fe15c6857a304) | ダウンロードのルートディレクトリを設定します。                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ad69aaf8885027863ea19657425ef1974) | ダウンロードするHTTPヘッダーを設定します。                                           |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a507e1dcc250a5764bd84d6e8a6598b23) | ダウンロードのコールバック方法を設定します。ダウンロードする前に必ず設定してください。                           |
| [startDownloadUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac886a33c24af3bea16b4b2b9ab1bcfde) | URL方式でダウンロードを開始します。                                        |
| [startDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a6093eec0836566ad15a4fdeb2b0682e9) | FileID方式でダウンロードを開始します。                                     |
| [stopDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#af1c09ed1089c935a46d6f9d8f1587dc4) | ダウンロードを停止します。ITXVodDownloadListener.onDownloadStopコールバック時に停止が完了します。 |
| [deleteDownloadFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a9564ad5e676445ffe2cccdbfacfd7b11) | ダウンロードファイルを削除します。                                               |
| [deleteDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a8f38d437419ecbe1d906e5826893194e) | ダウンロード情報を削除します。                                               |
| [getDownloadMediaInfoList](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adad0276021a21fdfca8b1925b8c46ca5) | すべてのユーザーのダウンロードリスト情報を取得します。                                 |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a255dd9b7ce63b862e0674ba144a68aac) | ダウンロード情報を取得します。                                               |
| [getOverlayKeyIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a4b0e452471aa28879bd855886127bcfd) | HLS EXT-X-KEYを取得します。                                          |
| [genRandomHexStringForHls](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0c96770dd135d266dfc14779fedad775) | 暗号化乱数を取得します。                                             |
| [encryptHexStringHls:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ab6277c0f8c42ee94a1a56055ead6ea13) | 暗号化します。                                                       |

### TXVodDownloadDelegate

| API                                                          | 説明                                             |
| ------------------------------------------------------------ | ------------------------------------------------- |
| [onDownloadStart](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ad375a3205d19472a2e5f22fbce384f6a) | ダウンロードを開始します。                                        |
| [onDownloadProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a7fcc9b089f4cabcd1b843fdccbd7f58b) | ダウンロードの進行状況を更新します。                                    |
| [onDownloadStop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a11ad404425936a29dd9f2edc1aaca8f6) | ダウンロードを停止します。                                        |
| [onDownloadFinish](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a4453811b7217726930d8f05b62cc4902) | ダウンロード終了です。                                        |
| [onDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adf5abf41239950b68347a085704db523) | ダウンロードプロセスでエラーが発生しました。                              |
| [hlsKeyVerify](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a32e5b4e7d5eaa14a9b144747e174390f) | HLSをダウンロードし、暗号化されたファイルに遭遇すると、復号Keyを外部チェッカーに渡します。 |

### [TXDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga625ad66cfaed6a449961936a37740dd9)

エラーコードのダウンロード

| 列挙値                | 意味の説明           |
| --------------------- | ------------------ |
| TXDownloadSuccess     | ダウンロードに成功しました           |
| TXDownloadAuthFaild   | fileid認証に失敗しました     |
| TXDownloadNoFile      | この解像度のファイルはありません     |
| TXDownloadFormatError | サポートしていない形式です         |
| TXDownloadDisconnet   | ネットワークが切断されました           |
| TXDownloadHlsKeyError | HLS復号keyの取得に失敗しました |
| TXDownloadPathError   | ダウンロードディレクトリへのアクセスに失敗しました   |

### [TXVodDownloadMediaInfoState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga7378c6cdd737126deb060ee3eb31f00a)

ダウンロードの状態

| 列挙値                            | 意味の説明   |
| --------------------------------- | ---------- |
| TXVodDownloadMediaInfoStateInit   | 初期状態のダウンロード |
| TXVodDownloadMediaInfoStateStart  | ダウンロードの開始   |
| TXVodDownloadMediaInfoStateStop   | ダウンロードの停止   |
| TXVodDownloadMediaInfoStateError  | ダウンロードのエラー   |
| TXVodDownloadMediaInfoStateFinish | ダウンロードの完了   |

### [TXVodQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga7079416c4ef1fec0f33755d7a2bc7c58)

ダウンロードビデオの解像度

| 列挙値          | 意味の説明 |
| --------------- | -------- |
| TXVodQualityOD  | オリジナル画像     |
| TXVodQualityFLU | LD     |
| TXVodQualitySD  | SD     |
| TXVodQualityHD  | HD     |
| TXVodQualityFHD | FHD   |
| TXVodQuality2K  | 2K       |
| TXVodQuality4K  | 4K       |

## TXPlayerAuthParams

fileIdにより暗号化したビデオの設定を再生します。

| API                                                          | 説明                   |
| ------------------------------------------------------------ | -------------------- |
| [appId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a5b3217c0ab223c526d557b09d2b0d6c0) | アプリケーションappIdです。         |
| [fileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a66c446aeaf5eef1ee21764d4bdf7b8ae) | ファイルidです。             |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a4f13e124e054004dcd7930ecd6df0f57) | タイムアウトタイムスタンプに暗号化リンクします。 |
| [exper](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a9e4e9de0c34814be700575f5ebdf725e) | プレビュー時間です。           |
| [us](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a6a5fc78b476fcbcdcc2a9888faa75ea3) | 固有の識別リクエストです。       |
| [sign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a37aa22c94233901cd1afee101f759348) | リンク不正アクセス防止署名です。         |
| [https](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a33d23e482c312a90cae72781bdfa1c4a) |  httpsリクエストを用いるかどうかです。    |

## TXBitrateItem

HLSマルチビットレートの情報です。

| API               | 説明               |
| ------------------------------------------------------------ | ------------------- |
| [index](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#a43d1d245fab4496928fe2e287fdc3f59) | m3u8ファイルの番号です。 |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#ab581e554cfc9559c9e2cd57ecf126d02) | このストリームのビデオ幅です。    |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#a1cdeaaebe1687fd7b3237fd45e3d5740) | このストリームのビデオ高さです。    |
| [bitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#abee909d3e29c2c87de16464920736759) | このストリームのビデオビットレートです。    |

## TXImageSprite

スプライトイメージの解析ツールです。

| API               | 説明               |
| ------------------------------------------------------------ | ---------------- |
| [setVTTUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__ios.html#a0075e38dc6b4291851c35f896ce7a28d) | スプライトイメージのアドレスを設定します。 |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__ios.html#a4561e9ea43d7273caf9197d96f5f7307) | サムネイルを取得します。     |

## TXPlayerDrmBuilder

VOD Drmのコンストラクタです。

| API               | 説明               |
| ------------------------------------------------------------ | ---------------- |
| [certificateUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#a24e49ee9ffc468e63b10c120af3a842f) | 証明書プロバイダのURLです。 |
| [keyLicenseUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#a1d393eafdb9cc90f7f6beeeb8eb94157) | 復号keyのURLです。   |
| [playUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#ab08c768d03824654011cf36aedc16193) | 再生リンクです。       |

## エラーコードリスト

### 一般的なイベント

| code | イベントの定義                   | 意味の説明                                                    |
| ---- | -------------------------- | ----------------------------------------------------------- |
| 2004 | PLAY_EVT_PLAY_BEGIN        | ビデオの再生が開始されます（もしくるくると回る表示が出たら停止します）。                |
| 2005 | PLAY_EVT_PLAY_PROGRESS     | ビデオ再生の進行状況です。現在の再生の進行状況、ロードの進行状況および全体の長さを通知します。      |
| 2007 | PLAY_EVT_PLAY_LOADING      | ビデオ再生をloading中です。再開できれば、その後にLOADING_ENDイベントが発生します。 |
| 2014 | PLAY_EVT_VOD_LOADING_END   | ビデオ再生ロードを終了します。ビデオは引き続き再生されます。                       |
| 2006 | PLAY_EVT_PLAY_END          | ビデオ再生を終了します。                                              |
| 2013 | PLAY_EVT_VOD_PLAY_PREPARED | プレーヤーの準備が整い、再生可能になりました。                                |
| 2003 | PLAY_EVT_RCV_FIRST_I_FRAME | ネットワークが最初のレンダリング可能なビデオデータパッケージ（IDR）を受信しました。                   |
| 2009 | PLAY_EVT_CHANGE_RESOLUTION | ビデオ解像度を変更します。                                            |
| 2011 | PLAY_EVT_CHANGE_ROTATION   | MP4ビデオの回転角度です。                                          |



### 警告イベント

| code  | イベントの定義                          | 意味の説明                                                     |
| ----- | --------------------------------- | ------------------------------------------------------------ |
| -2301 | PLAY_ERR_NET_DISCONNECT           | ネットワーク接続が切断され、かつ複数回再接続しても再開できません。それ以上のリトライを行うには、ご自身で再生を再起動してください。    |
| -2305 | PLAY_ERR_HLS_KEY                  | HLS復号keyの取得に失敗しました。                                      |
| 2101  | PLAY_WARNING_VIDEO_DECODE_FAIL    | 現在のビデオフレームのデコードに失敗しました。                                         |
| 2102  | PLAY_WARNING_AUDIO_DECODE_FAIL    | 現在のオーディオフレームのデコードに失敗しました。                                         |
| 2103  | PLAY_WARNING_RECONNECT            | ネットワーク接続が切断されましたが、自動再接続が開始されました（再接続が3回を超えると、PLAY_ERR_NET_DISCONNECTが直接スローされます）。 |
| 2106  | PLAY_WARNING_HW_ACCELERATION_FAIL | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください。                                     |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL         | H265デコードに失敗しました。                                              |
| -2303 | PLAY_ERR_FILE_NOT_FOUND           | 再生ファイルが存在しません。                                           |

## Player+の定数

### [イベントコードおよびエラーコードの定義](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#gabc22cbb50603d49430a22f2812d9e616)

| 列挙値                                   | 意味                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| VOD_PLAY_EVT_RCV_FIRST_I_FRAME           | 再生イベント: 最初のビデオフレームの受信に成功しました                             |
| VOD_PLAY_EVT_RCV_FIRST_AUDIO_FRAME       | 再生イベント: 最初のオーディオフレームの受信に成功しました                             |
| VOD_PLAY_EVT_PLAY_BEGIN                  | 再生イベント: すでに再生を開始しました                                       |
| VOD_PLAY_EVT_PLAY_PROGRESS               | 再生イベント: 再生進行状況の更新です。VODプレーヤー（VodPlayer）専用です          |
| VOD_PLAY_EVT_PLAY_END                    | 再生イベント: 再生はすでに終了しました                                       |
| VOD_PLAY_EVT_PLAY_LOADING                | 再生イベント: データをバッファ中です                                         |
| VOD_PLAY_EVT_START_VIDEO_DECODER         | 再生イベント: ビデオデコーダはすでに起動しています                                 |
| VOD_PLAY_EVT_CHANGE_RESOLUTION           | 再生イベント: ビデオ解像度に変化が発生しました                                |
| VOD_PLAY_EVT_GET_PLAYINFO_SUCC           | 再生イベント: VODファイルの情報取得に成功しました。VODプレーヤー（VodPlayer）専用です |
| VOD_PLAY_EVT_CHANGE_ROTATION             | 再生イベント: MP4ビデオの回転角度に変化が発生しました。VODプレーヤー（VodPlayer）専用です |
| VOD_PLAY_EVT_VOD_PLAY_PREPARED           | 再生イベント: ビデオのロード完了です。VODプレーヤー（VodPlayer）専用です          |
| VOD_PLAY_EVT_VOD_LOADING_END             | 再生イベント: ビデオのバッファが終了しました。VODプレーヤー（VodPlayer）専用です          |
| VOD_PLAY_EVT_STREAM_SWITCH_SUCC          | 再生イベント: すでにストリーム切り替えに成功しました（異なる解像度のビデオストリーム間で切り替えを行います） |
| VOD_PLAY_EVT_VOD_PLAY_TCP_CONNECT_SUCC   | TCPの接続に成功しました                                                 |
| VOD_PLAY_EVT_VOD_PLAY_FIRST_VIDEO_PACKET | 最初のフレームデータを受信しました                                                 |
| VOD_PLAY_EVT_VOD_PLAY_SEEK_COMPLETE      | ビデオ再生Seekが完成しました                                           |
| VOD_PLAY_EVT_AUDIO_SESSION_INTERRUPT     | 再生イベント: Audio Sessionがその他のAppによって中断されました（iOSプラットフォームにおいてのみ適用） |
| VOD_PLAY_ERR_NET_DISCONNECT              | ライブストリーミングエラー: ネットワーク接続が切断されました（再接続を3回行いましたが再開できませんでした）。 |
| VOD_PLAY_ERR_FILE_NOT_FOUND              | VODエラー: 再生ファイルが存在しません                                     |
| VOD_PLAY_ERR_HLS_KEY                     | VODエラー: HLSデコーダKEYの取得に失敗しました                               |
| VOD_PLAY_ERR_GET_PLAYINFO_FAIL           | VODエラー: VODファイルのファイル情報取得に失敗しました                         |

### [ピクチャーインピクチャーのエラータイプ](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#ga2b903483a07868f795ed52c27bfc08ac)

| 列挙値                                           | 意味                                         |
| ------------------------------------------------ | -------------------------------------------- |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_NONE                | エラーはありません                                       |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_DEVICE_NOT_SUPPORT  | デバイスまたはシステムバージョンがサポートされていません（iPad iOS9+はPIPをサポート） |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PLAYER_NOT_SUPPORT  | プレーヤーをサポートしていません                                 |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_VIDEO_NOT_SUPPORT   | ビデオをサポートしていません                                   |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_IS_NOT_POSSIBLE | PIPコントローラは利用不可です                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_ERROR_FROM_SYSTEM   | PIPコントローラエラー                               |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PLAYER_NOT_EXIST    | プレーヤーオブジェクトは存在しません                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_IS_RUNNING      | PIP機能はすでに実行されています                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_NOT_RUNNING     | PIP機能は起動していません                             |

### [ピクチャーインピクチャーコントローラの状態](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#ga96479f1446227115f7183ae97a1527e3)

| 列挙値                             | 意味           |
| ---------------------------------- | -------------- |
| TX_VOD_PLAYER_PIP_STATE_UNDEFINED  | 未設定状態     |
| TX_VOD_PLAYER_PIP_STATE_WILL_START | ピクチャーインピクチャーはまもなく開始します |
| TX_VOD_PLAYER_PIP_STATE_DID_START  | ピクチャーインピクチャーはすでに開始しました |
| TX_VOD_PLAYER_PIP_STATE_WILL_STOP  | ピクチャーインピクチャーはまもなく終了します |
| TX_VOD_PLAYER_PIP_STATE_DID_STOP   | ピクチャーインピクチャーは終了済みです |
| TX_VOD_PLAYER_PIP_STATE_RESTORE_UI | UIリセット        |
