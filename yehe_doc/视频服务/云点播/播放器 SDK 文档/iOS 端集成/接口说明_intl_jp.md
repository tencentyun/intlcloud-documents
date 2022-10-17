## TXVodPlayer

### VODプレーヤー

[TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html)をご参照ください。
主に指定されたVODストリーミングアドレスからオーディオビデオデータをプルし、デコードとローカルレンダリング再生を行う役割を担います。
プレーヤーには次の機能が含まれます。

- FLV、MP4、HLSという複数の再生形式をサポートし、基本再生（URL再生）およびVOD再生（Fileid再生）という2つの再生方式をサポートしています。
- スクリーンキャプチャにより、現在の再生ストリームのビデオ画面を切り取ることができます。
- ジェスチャー操作により、明るさ、音量、進行状況などを調節できます。
- 解像度は手動で切り替えることも、ネットワーク帯域幅に応じてアダプティブに選択することもできます。
- さまざまな倍速再生を指定でき、イメージおよびハードウェアアクセラレーションを有効にすることもできます。
- 完全な機能については、[VOD Super Player - 機能リスト](https://intl.cloud.tencent.com/document/product/266/38295)をご参照ください。

### プレーヤー設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [config](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3ad68ed80140f20cf3229bf344886a04) | VOD設定です。設定情報については[TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html)ご参照ください。 |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | startPlay後にすぐに再生するかどうかです。デフォルトではYESです。                         |
| [token](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | HLSのtokenを暗号化します。この値を設定すると、プレーヤーはURL内のファイル名の前に`voddrm.token.TOKEN TextureView`を自動的に追加します。 |
| [loop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1cdc15a39387295573f41caee9a05932) | SurfaceViewを繰り返し再生するかどうかです。                                   |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | ビデオレンダリングのコールバックです。（ハードウェアデコードのみサポート）                                 |
| setExtentOptionInfo                                          | プレーヤーサービスパラメータを設定します。パラメータ形式は<NSString *, id>です               |

### 再生基本インターフェース  
| API                                                          | 説明                        |
| ------------------------------------------------------------ | --------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ac1af59fe9e4bc2b390661787097d2c8b) | HTTP URL形式の再生アドレスです。 |
| [startPlayWithParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a0b4db90eafbc8c4d9be498e5ffefe961) | fileId形式で再生します。 |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | 再生を停止します。 |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8438e3403946accc1986a05b89ee7b03) | 再生中かどうかです。      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | 再生を一時停止し、ストリーミングデータの取得を停止し、最後の1フレームの画面を保持します。 |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41de8150eff044a237990c271d57ea27) | 再生を再開し、ストリーミングデータを再取得します。 |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | ビデオストリームの指定した時点にジャンプします。単位は秒です。 |
| [currentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8b0ca7fda398996b355179bd9a479785) | 現在の再生位置を取得します。単位は秒です。 |
| [duration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7fd4f66e650bd1656a97d1db7fabaeda) | 総時間を取得します。単位は秒です。 |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a4acb1f7a723d342f7bfb9c5e540e5e77) | 再生可能時間を取得します。単位は秒です。 |
| [width](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3eeed61a3424d2f907c8a1e420fddf6d) | ビデオの幅を取得します。 |
| [height](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a822ae85493a742654ba563619492b26a) | ビデオの高さを取得します。 |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41001e6276c4853500f78579d6bd2218) | 再生開始時間を設定します。 |

### ビデオ関連インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9646437dc38d7dcce8c32dfec5d0bc5b) | 現在のビデオフレーム画像を取得します。<br>**注意：現在のフレーム画像の取得は比較的時間がかかる操作のため、スクリーンキャプチャは非同期的なコールバックによって行われます。** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaf347826e1a9fad9998c0eea9791ed0c) | イメージを設定します。                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | VODの再生速度を設定します。デフォルトでは1.0です。                                |
| [bitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9a325ed94acf6b545c88755855449a12) | 現在再生中のビットレートインデックスを返します。                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1aa8e1f3a63b46c8a1166447e2457abc) | 現在再生中のビットレートインデックスを設定し、解像度をシームレスに切り替えます。<br>解像度の切り替えにはしばらく時間がかかる場合があります。 |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | [画像タイリングモード](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)を設定します。 |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | [画像レンダリング角度](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)を設定します。 |

### オーディオ関連インターフェース

| API                                                          | 説明                          |
| ------------------------------------------------------------ | ----------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | ミュート再生にするかどうかを設定します。            |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ac92633d1cdfff1f93f48b7aec1d35b98) | 音量を設定します。範囲は0～100です。 |

### イベント通知インターフェース

| API                    | 説明                   |
| ---------------------- | ---------------------- |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | イベントコールバックです。[vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79)の使用をお勧めします。 |
| [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) | プレーヤーのコールバックを設定します。                                 |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | ビデオレンダリングのコールバックです（ハードウェアデコードのみサポート）。                  |

### TRTC関連インターフェース

次のインターフェースによって、VODプレーヤーのオーディオビデオストリームをTRTCでプッシュすることができます。その他のTRTCサービスについては、[TRTC製品概要](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#affcfcba7937a7ef88a918afb0b3d73bc) | VODを[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)サービスにバインドします。 |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a5b947acf9f4fc992f0f02f8d87de3334) | VODと[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)サービスとのバインドを解除します。 |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8298f704cb659c725da28a27e08afbed) | ビデオストリームのプッシュを開始します。                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaa6ecf72bfa9e35078561dd98d62be0c) | ビデオストリームのプッシュをキャンセルします。                                             |
| [publishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | オーディオストリームのプッシュを開始します。                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a206d786a74ae3b71766755135161773e) | オーディオストリームのプッシュをキャンセルします。                                             |

## TXVodPlayListener

Tencent Cloud VODのコールバック通知です。
### SDK基本コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a6330db18bb40862fc2d66474fc34166b) | VOD再生イベント通知です。[再生イベントリスト](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a)、[イベントパラメータ](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)をご参照ください。 |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a08721fef1ba130fd182de4bed3b4430e) | VODプレーヤーの[ネットワーク状態通知](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737)です。 |

## TXVodPlayConfig

VODプレーヤー設定クラスです。

### 基本設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [connectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad89d728973fb42eced3ac18be873af1b) | プレーヤーの再接続回数を設定します。                                         |
| [connectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a07fde7cd21980c096b5bbd93aed137d5) | プレーヤーの再接続間隔を設定します。単位は秒です。                                 |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a39233eb85b4cbae04411577510e7c5e6) | プレーヤーの接続タイムアウト時間を設定します。単位は秒です。                             |
| [cacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aec1a8f0064562368fe3c2df4f7fb72eb) | VODキャッシュディレクトリを設定します。MP4、HLSのVODが有効です。                       |
| [maxCacheItems](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aedbc9cc868baa2c44e3badbe6fdf4a43) | キャッシュファイル数を設定します。                                           |
| [playerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a4595fb5853016c5e5919324e71ad6f4c) | プレーヤーのタイプを設定します。                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad69aaf8885027863ea19657425ef1974) | カスタムHTTP headersを設定します。                                    |
| [enableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ada91e71bad4df942e6190650915a7728) | 正確なseekを行うかどうかを設定します。デフォルトではtrueです。                               |
| [autoRotate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1a372684aaaf95b9b17abf0c7a4e6c6) | MP4ファイルを再生する際、YESに設定すると、ファイル内の回転角度に応じて自動的に回転します。<br>回転角度はPLAY_EVT_CHANGE_ROTATIONイベントから取得できます。デフォルトではYESです。 |
| [smoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1caeddde1f950ec7965dcc721109928) | マルチビットレートHLSへのスムーズな切り替えを行います。デフォルトではfalseです。                             |
| [progressInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a943e212cbd5e3d89de0529ab7c6042fb) | 進行状況コールバックの間隔を設定します。単位はミリ秒です。                                 |
| [maxBufferSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa4934cef81784d3a195a5d95a43953f5) | 最大プリロードサイズです。単位はMBです。                                    |
| maxPreloadSize                                               | プリロードの最大バッファサイズを設定します。単位はMBです。                           |
| firstStartPlayBufferTime                                     | 最初のキャッシュにロードする必要があるデータ時間を設定します。単位はmsで、デフォルト値は100msです。          |
| nextStartPlayBufferTime                                      | バッファ時（バッファデータが不十分であることによる二次バッファ、またはseekによるドラッグバッファ）に少なくともどのくらいのデータをキャッシュするとバッファを終了できるかです。単位はmsで、デフォルト値では250msです。 |
| overlayKey                                                   |  HLSセキュリティ強化暗号化/復号keyを設定します。                                   |
| overlayIv                                                    | HLSセキュリティ強化暗号化/復号Ivを設定します。                                    |
| extInfoMap                                                   | 拡張情報を設定します。                                               |
| preferredResolution                                          | 再生HLSに複数のコードストリームがある場合、設定したpreferredResolutionに応じて最適なコードストリームを選択して再生を開始します *。preferredResolutionは幅と高さを乗算（width * height）します。再生開始前に設定された場合のみ有効です。 |
| enableRenderProcess                                          | ロード後にレンダリングの後処理サービス(例えば解像度プラグインサービス）を許可するかどうかです。デフォルトでは有効です。     |

## TXPlayerGlobalSetting

VODプレーヤーのグローバル設定クラス

| API                | 説明                                                         |
| ------------------ | ------------------------------------------------------------ |
| setCacheFolderPath | 再生エンジンのcacheディレクトリを設定します。設定後、プリダウンロード、プレーヤーなどは優先的にこのディレクトリから読み取りおよび保存します |
| setMaxCacheSize    | 再生エンジンの最大キャッシュのサイズを設定します。設定後は設定値に応じて自動的にCacheディレクトリのファイルをクリーンアップします。単位はMBです。 |

## TXVodPreloadManager

VODプレーヤーのプリダウンロードのインターフェースクラス

| API           | 説明                                                         |
| ------------- | ------------------------------------------------------------ |
| sharedManager | TXVodPreloadManagerインスタンスオブジェクトを取得します。シングルトンモードです。                    |
| startPreload  | プリダウンロードを有効化する前に、まず再生エンジンのキャッシュディレクトリTXPlayerGlobalSetting#setCacheFolderPathとキャッシュサイズTXPlayerGlobalSetting#setMaxCacheSizeを設定してください。 |
| stopPreload   | プリダウンロードの停止                                                 |

## TXVodDownloadManager

VODプレーヤーのビデオダウンロードインターフェースクラス

| API                      | 説明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| shareInstance            |  TXVodDownloadManagerインスタンスオブジェクトを取得します。シングルトンモードです。                   |
| setDownloadPath          | ダウンロードのルートディレクトリを設定します。                                               |
| setHeaders               | ダウンロード HTTPヘッダーを設定します。                                               |
| setListener              | ダウンロードのコールバック方法を設定します。ダウンロード前に設定する必要があります。                             |
| startDownloadUrl         | URL方式でダウンロードを開始します。                                            |
| startDownload            | FileID方式でダウンロードを開始します。                                         |
| stopDownload             | ダウンロードを停止し、ITXVodDownloadListener.onDownloadStopがコールバックされると正常に停止します。 |
| deleteDownloadFile       | ダウンロードファイルを削除します。                                                 |
| deleteDownloadMediaInfo  | ダウンロード情報を削除します。                                                 |
| getDownloadMediaInfoList | すべてのユーザーのダウンロードリスト情報を取得します。                                   |



## ITXVodDownloadListener

Tencent Cloudビデオダウンロードのコールバック通知です。

| API                | 説明                                         |
| ------------------ | -------------------------------------------- |
| onDownloadStart    | ダウンロードを開始します。                                     |
| onDownloadProgress | ダウンロード進捗を更新します。                                 |
| onDownloadStop     | ダウンロードを停止します。                                    |
| onDownloadFinish   | ダウンロードを終了します。                                     |
| onDownloadError    | ダウンロードプロセスでエラーが発生しました。                           |
| hlsKeyVerify       | HLSをダウンロードし、暗号化されたファイルに遭遇すると、復号Keyを外部チェッカーに渡します。 |



## エラーコードリスト

### 一般的なイベント

| code | イベントの定義                   | 意味の説明                                                    |
| ---- | -------------------------- | ----------------------------------------------------------- |
| 2004 | PLAY_EVT_PLAY_BEGIN        | ビデオ再生を開始します（進捗インジケータが表示されている場合は、この時点で停止します）。                |
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
| -2301 | PLAY_ERR_NET_DISCONNECT           | ネットワーク接続が切断され、かつ複数回再接続しても再開できません。これ以上のリトライを行うには、ご自身で再生を再起動してください。    |
| -2305 | PLAY_ERR_HLS_KEY                  | HLS復号keyの取得に失敗しました。                                      |
| 2101  | PLAY_WARNING_VIDEO_DECODE_FAIL    | 現在のビデオフレームのデコードに失敗しました。                                         |
| 2102  | PLAY_WARNING_AUDIO_DECODE_FAIL    | 現在のオーディオフレームのデコードに失敗しました。                                         |
| 2103  | PLAY_WARNING_RECONNECT            | ネットワーク接続が切断されましたが、自動再接続が開始されました（再接続が3回を超えると、PLAY_ERR_NET_DISCONNECTが直接スローされます）。 |
| 2106  | PLAY_WARNING_HW_ACCELERATION_FAIL | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください。                                     |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL         | H265デコードに失敗しました。                                              |
| -2303 | PLAY_ERR_FILE_NOT_FOUND           | 再生ファイルが存在しません。                                           |
