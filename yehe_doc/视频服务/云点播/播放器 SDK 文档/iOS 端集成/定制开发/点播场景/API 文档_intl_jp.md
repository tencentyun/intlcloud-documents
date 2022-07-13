## TXVodPlayer

### VODプレーヤー

[TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html)をご参照ください。
主に指定されたオンデマンドストリーミングアドレスからオーディオビデオデータをプルし、デコードとローカルレンダリング再生を行います。
プレーヤーには次の機能があります：

- FLV、MP4およびHLSの複数の再生形式に対応し、基本再生（URL再生）とオンデマンド再生（Fileid再生）の2つの再生方法をサポートしています。
- 現在再生されているストリームの映像画面をキャプチャするスクリーンショット。
- ジェスチャー操作で、明るさや音、再生位置などを調節します。
- シャープネスを手動で切り替えることも、ネットワーク帯域幅に応じてシャープネスを適応的に選択することもできます。
- 異なる再生速度を指定し、ミラーリングとハードウェアアクセラレーションをオンにすることができます。
- 完全機能については、[Super Player機能リスト](https://intl.cloud.tencent.com/document/product/266/38295)をご参照ください。

### プレーヤーの設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [config](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3ad68ed80140f20cf3229bf344886a04) | プレーヤーのコンフィグレーション。コンフィグレーション情報については[TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html)をご参照ください。|
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | startPlay後すぐに再生するかどうか。デフォルト値はYESです。                         |
| [setToken](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | HLSのtokenを暗号化します。この値を設定すると、プレーヤーはURL内のファイル名の前に`voddrm.token.TOKENTextureView`を自動的に追加します。|
| [loop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1cdc15a39387295573f41caee9a05932) | SurfaceViewをループ再生するかどうか。                                   |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | ビデオレンダリングのコールバック。（ハードウェアデコードのみがサポートされます） |
| setExtentOptionInfo                                          | プレーヤーの業務パラメータを`<NSString *, id>`の形式で設定します               |

### 再生基本インターフェース  
| API                                                          | 説明                       |
| ------------------------------------------------------------ | --------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ac1af59fe9e4bc2b390661787097d2c8b) | HTTP URL形式のアドレスを再生します。|
| [startPlayWithParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a0b4db90eafbc8c4d9be498e5ffefe961) | fileId方式で再生されます。|
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | 再生を停止します。 |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8438e3403946accc1986a05b89ee7b03) | 再生されているかどうか。      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | 再生を一時停止し、ストリームデータの取得を停止し、最後のフレームを保持します。|
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41de8150eff044a237990c271d57ea27) | 再生を再開し、ストリームデータを再取得します。|
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | 指定した時点のビデオストリームにジャンプします。秒単位です。|
| [currentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8b0ca7fda398996b355179bd9a479785) | 現在の再生位置を取得します。秒単位です。|
| [duration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7fd4f66e650bd1656a97d1db7fabaeda) | 合計時間を取得します。秒単位です。|
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a4acb1f7a723d342f7bfb9c5e540e5e77) | 再生可能時間を取得します。秒単位です。|
| [width](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3eeed61a3424d2f907c8a1e420fddf6d) | ビデオ幅を取得します。|
| [height](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a822ae85493a742654ba563619492b26a) | ビデオの高さを取得します。|
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41001e6276c4853500f78579d6bd2218) | 再生開始時間を設定します。|

### ビデオ関連インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9646437dc38d7dcce8c32dfec5d0bc5b) | 現在のビデオフレーム画像を取得します。<br>**注：現在のフレーム画像の取得には時間がかかるため、スクリーンショットは非同期でコールバックされます。**|
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaf347826e1a9fad9998c0eea9791ed0c) | ミラーリングを設定します。                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | オンデマンドの再生レートを設定します。デフォルトは1.0です。                                |
| [bitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9a325ed94acf6b545c88755855449a12) | 現在再生されているビットレートのインデックスを返します。                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1aa8e1f3a63b46c8a1166447e2457abc) | 現在再生されているビットレートインデックスを設定し、シャープネスをシームレスに切り替えます。<br>シャープネスの切り替えには、しばらく待つ必要がある場合があります。|
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | [画像タイル表示モード](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)を設定します。|
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | [画像レンダリング角度](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)を設定します。|

### 音声に関連するインターフェース

| API                                                          | 説明                       |
| ------------------------------------------------------------ | ----------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | 再生をミュートするかどうかを設定します。            |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ac92633d1cdfff1f93f48b7aec1d35b98) | 音量を設定します。範囲：0 ～ 100。|

### イベント通知インターフェース

| API                                                          | 説明                   |
| ---------------------- | ---------------------- |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | イベントコールバック。[vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79)を推奨します。|
| [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) | プレーヤーのコールバックを設定します。                                 |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | ビデオレンダリングコールバック（ハードウェアデコードのみがサポートされます）。                  |

### TRTC関連インターフェース

次のインターフェースを使用して、オンデマンドプレーヤーからのオーディオビデオストリームをTRTC経由でプッシュすることができます。TRTCサービスの詳細については、[TRTC製品の概要](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#affcfcba7937a7ef88a918afb0b3d73bc) | オンデマンドは[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)サービスにバインドされています。|
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a5b947acf9f4fc992f0f02f8d87de3334) | オンデマンド[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)サービスにバインド解除されます。|
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8298f704cb659c725da28a27e08afbed) | ビデオストリームのプッシュを開始します。                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaa6ecf72bfa9e35078561dd98d62be0c) | ビデオストリームのプッシュをキャンセルします。                                             |
| [ publishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | オーディオストリームのプッシュを開始します。                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a206d786a74ae3b71766755135161773e) | オーディオストリームのプッシュをキャンセルします。                                             |

## TXVodPlayListener

Tencent Cloudオンデマンドのコールバック通知。
### SDK基礎コールバック

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a6330db18bb40862fc2d66474fc34166b) | オンデマンド再生イベント通知については、[再生イベントリスト](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a)、[イベントパラメータ](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)をご参照ください。|
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a08721fef1ba130fd182de4bed3b4430e) | オンデマンドプレーヤー[ネットワークステータス通知](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737)。|

## TXVodPlayConfig

VODプレーヤー設定クラス。

### 基礎設定インターフェース

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [connectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad89d728973fb42eced3ac18be873af1b) | プレーヤーの再接続回数を設定します。                                         |
| [connectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a07fde7cd21980c096b5bbd93aed137d5) | プレーヤーの再接続間隔を設定します。秒単位です。                                 |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a39233eb85b4cbae04411577510e7c5e6) | プレーヤー接続タイムアウトを設定します。秒単位です。                             |
| [cacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aec1a8f0064562368fe3c2df4f7fb72eb) | オンデマンドキャッシュディレクトリを設定します。MP4、HLSのオンデマンドは有効です。                       |
| [maxCacheItems](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aedbc9cc868baa2c44e3badbe6fdf4a43) | キャッシュファイルの数を設定します。                                           |
| [playerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a4595fb5853016c5e5919324e71ad6f4c) | プレーヤーのタイプを設定します。                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad69aaf8885027863ea19657425ef1974) | カスタムHTTP headersを設定します。                                    |
| [enableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ada91e71bad4df942e6190650915a7728) | 正確なseekを実行するかどうかを設定します。デフォルトはtrueです。                               |
| [autoRotate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1a372684aaaf95b9b17abf0c7a4e6c6) | MP4ファイルの再生時にYESに設定すると、ファイル内の回転角度に基づいて自動的に回転します。<br>回転角度はPLAY_EVT_CHANGE_ROTATIONイベントから取得できます。デフォルト値はYESです。|
| [smoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1caeddde1f950ec7965dcc721109928) | マルチビットレートHLSをスムーズに切り替えます。デフォルト値はfalseです。                             |
| [progressInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a943e212cbd5e3d89de0529ab7c6042fb) | 再生位置のコールバック間隔を設定します。ミリ秒単位です。                                 |
| [maxBufferSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa4934cef81784d3a195a5d95a43953f5) | 最大プリロードサイズで、単位はMBです。                                    |
| maxPreloadSize                                               | プリロードされた最大バッファサイズをMB単位で設定します。                           |
| firstStartPlayBufferTime                                     | 初回キャッシュとしてロードするために必要な時間をで設定します。単位はmsで、デフォルト値は100です。          |
| nextStartPlayBufferTime                                      | バッファリング時（バッファリングデータ不足による二次バッファリング、またはseekによるドラッグバッファリング）に、最低どの程度のデータをバッファリングすればバッファリングが終了するか。単位はmsで、デフォルト値は250msです。|
| overlayKey                                                   | HLSのSecurity Reinforceの暗号復号keyを設定します。                                   |
| overlayIv                                                    | HLSのSecurity Reinforceの暗号復号Ivを設定します。                                    |
| extInfoMap                                                   | 拡張情報を設定します。                                               |
| preferredResolution                                          | 複数のビットストリームのHLSを再生する場合、設定されたpreferredResolutionに基づいて最適なビットストリームを選択して再生を開始する*が、preferredResolutionは幅と高さの積（width*height）であり、再生開始前に設定します。|
| enableRenderProcess                                          | 後レンダリング後処理サービス（超解像プラグインサービスなど）のロードが許可されているかどうか。デフォルトではオンです。     |

## TXPlayerGlobalSetting

VODプレーヤーグロバール設定クラス

| API                                                          | 説明                   |
| ------------------ | ------------------------------------------------------------ |
| setCacheFolderPath | 再生エンジンのcacheディレクトリを設定します。設定後、プレダウンロード、プレーヤーなどが優先的にこのディレクトリから読み込まれ、保存されます |
| setMaxCacheSize    | 再生エンジンの最大キャッシュサイズを設定します。設定すると、設定値に基づいてCacheディレクトリのファイルが自動的にクリーンアップされます。単位MB。|

## TXVodPreloadManager

オンデマンドプレーヤーのプリダウンロードインターフェースクラス

| API                                                          | 説明                   |
| ------------- | ------------------------------------------------------------ |
| sharedManager | TXVodPreloadManagerインスタンスオブジェクトを取得します。シングルトンモードです。                    |
| startPreload  | プリダウンロードを開始する前に、再生エンジンのキャッシュディレクトリTXPlayerGlobalSetting#setCacheFolderPathとキャッシュサイズTXPlayerGlobalSetting#setMaxCacheSizeをあらかじめ設定してください。|
| stopPreload   | プリダウンロードを停止します                                                   |

## TXVodDownloadManager

オンデマンドプレーヤーのビデオダウンロードインターフェースクラス

| API                                                          | 説明                   |
| ------------------------ | ------------------------------------------------------------ |
| shareInstance            | TXVodDownloadManagerインスタンスオブジェクトを取得します。シングルトンモードです。                   |
| setDownloadPath          | ダウンロードルートを設定します。                                               |
| setHeaders               | ダウンロードHTTPヘッダーを設定します。                                               |
| setListener              | ダウンロードのコールバックメソッドを設定します。ダウンロード前に設定しておく必要があります。                             |
| startDownloadUrl         | URL方式でダウンロードを開始します。                                            |
| startDownload            | FileID方式でダウンロードを開始します。                                         |
| stopDownload             | ダウンロードを停止し、ITXVodDownloadListener.onDownloadStopがコールバックに成功しました。|
| deleteDownloadFile       | ダウンロードファイルを削除します。                                                 |
| deleteDownloadMediaInfo  | ダウンロード情報を削除します。                                                 |
| getDownloadMediaInfoList | すべてのユーザーのダウンロードリスト情報を取得します。                                   |



## ITXVodDownloadListener

Tencent Cloudビデオダウンロードコールバック通知。

| API                                                          | 説明                   |
| ------------------ | -------------------------------------------- |
| onDownloadStart    | ダウンロード開始。                                     |
| onDownloadProgress | ダウンロードの進行状況の更新。                                 |
| onDownloadStop     | ダウンロード停止。                                    |
| onDownloadFinish   | ダウンロードの終了。                                     |
| onDownloadError    | ダウンロード中にエラーが発生しました。                           |
| hlsKeyVerify       | HLSをダウンロードし、暗号化されたファイルに遭遇すると、復号化されたKeyを外部検証に渡します。|



## エラーコードリスト

### 一般的なイベント

| code | イベント定義                   | 意味説明                                                    |
| ---- | -------------------------- | ----------------------------------------------------------- |
| 2004 | PLAY_EVT_PLAY_BEGIN        | ビデオの再生が開始されます（もしくるくると回る表示が出たら停止します）。                |
| 2005 | PLAY_EVT_PLAY_PROGRESS     | ビデオ再生位置。現在の再生位置、ロードの進行状態と全体時間を通知します。      |
| 2007 | PLAY_EVT_PLAY_LOADING      | ビデオ再生のloading。再開可能な場合、その後にLOADING_ENDイベントが発生します。|
| 2014 | PLAY_EVT_VOD_LOADING_END   | ビデオ再生loadingが終了し、ビデオが引き続き再生します。                       |
| 2006 | PLAY_EVT_PLAY_END          | ビデオ再生終了。                                              |
| 2013 | PLAY_EVT_VOD_PLAY_PREPARED | プレーヤーの再生準備が完了し、再生可能状態です。                                |
| 2003 | PLAY_EVT_RCV_FIRST_I_FRAME | ネットワークが最初のレンダリング可能なビデオパケット(IDR)を受信しました。                   |
| 2009 | PLAY_EVT_CHANGE_RESOLUTION | ビデオ解像度の変更。                                            |
| 2011 | PLAY_EVT_CHANGE_ROTATION   | MP4ビデオ回転角度。                                          |



### 警告イベント

| code | イベント定義                   | 意味説明                                                    |
| ----- | --------------------------------- | ------------------------------------------------------------ |
| -2301 | PLAY_ERR_NET_DISCONNECT           | ネットワーク接続が切断され、何度も再接続しても回復できません。さらにリトライしたい場合には、手動で再起動後、再生してください。    |
| -2305 | PLAY_ERR_HLS_KEY                  | HLS復号キーの取得に失敗しました。                                      |
| 2101  | PLAY_WARNING_VIDEO_DECODE_FAIL    | 現在のビデオフレームのデコードに失敗しました。                                         |
| 2102  | PLAY_WARNING_AUDIO_DECODE_FAIL    | 現在のオーディオフレームのデコードに失敗しました。                                         |
| 2103  | PLAY_WARNING_RECONNECT            | ネットワーク接続が切断され、自動再接続が有効にされています（再接続回数が3回を超えるとPLAY_ERR_NET_DISCONNECTがスローされます）。|
| 2106  | PLAY_WARNING_HW_ACCELERATION_FAIL | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください。                                     |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL         | H265デコードに失敗しました。                                              |
| -2303 | PLAY_ERR_FILE_NOT_FOUND           | 再生されたファイルは存在しません。                                           |
