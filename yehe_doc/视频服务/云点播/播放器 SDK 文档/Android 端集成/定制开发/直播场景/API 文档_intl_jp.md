## TXLivePlayer

### ビデオプレーヤー

[TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html)をご参照ください。
 
主にライブストリームのオーディオビデオ画面のデコードとローカルレンダリングを実行します。次の技術的特徴が含まれています：

- Tencent Cloudのプルアドレスに対し、低遅延プルを使用し、ライブストリーミングのマイク接続などの関連シーンを実現できます。
- Tencent Cloudのプルアドレスに対し、ライブストリーミングのタイムシフト機能が利用でき、ライブストリーミング視聴とタイムシフト視聴のシームレスな切り替えが可能になります。
- カスタマイズされたオーディオビデオデータ処理をサポートしているため、プロジェクトのニーズに合わせてライブストリームのオーディオビデオデータを処理した後、レンダリングと再生を実行することができます。

### SDK基本関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) | [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html)インスタンスを作成します。|
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#aec057eaad309a040e689eae94d81f6c2) | [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html)の再生設定項目を設定します。|
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a0735b006fe8c56875665cb66881af144) | プッシュコールバックインターフェースを設定します。                                           |


### 再生基本インターフェース  

| API                                                          | 説明                            |
| ------------------------------------------------------------ | ------------------------------- |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | プレーヤーのビデオレンダリングViewを設定します。     |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a966517cd67d967afe969b3d275239934) | プレーヤーが再生を開始します。                |
| [ stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | 再生を停止します。                      |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | 再生されているかどうか。                  |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | 再生を一時停止します。                      |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a41de8150eff044a237990c271d57ea27) | 再生を再開します。                      |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | ローカルレンダリングにSurfaceモードを使用します。|
| [setSurfaceSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#adfa92e76bde9450b135c48f531e5434d) | レンダリングされるSurfaceのサイズを設定します。       |


### プレーヤーの設定インターフェース

| API                                                          | 説明                   |
| ------------------------------------------------------------ | ---------------------- |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | 再生レンダリングモードを設定します。     |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | 画像レンダリング角度を設定します。     |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | ハードウェアアクセラレーションをオンにします。         |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | 再生をミュートするかどうかを設定します。     |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a3f0305de6ccd826ab62c442408416df9) | サウンド再生モードを設定します。     |
| [setVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6715d5315d47c73b3838f2cb771e7b58) | 音量を設定します。             |
| [switchStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a53f1f75a9a06e03bbb35e2ff5368c6f9) | 複数のシャープネスを切り替えます。         |
| [setAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#acd5e085b916732b2141ddae9ef93fc21) | 音量コールバックインタフェースを設定します。|


### ローカル録画とスクリーンショット

| API                                                          | 説明                   |
| ------------------------------------------------------------ | -------------------- |
| [setVideoRecordListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#acd229e0c77d3eea61dc0762557417478) | 録音コールバックインターフェースを設定します。   |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#aed6b1e9d26a36166ee31c0544bd95ca4) | ビデオ録画を開始します。       |
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a13313c5410c2a10a704b991f28141e6e) | ビデオ録画を停止します。       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a1377ad3e2678d3fef21f5037e274dd1a) | 再生中のローカルスクリーンショット。|


### カスタムデータ処理

| API                                                          | 説明                       |
| ------------------------------------------------------------ | --------------------------- |
| [addVideoRawData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a31d3d4067f5e61b80d7b750a6b5d97e2) | ソフトウェアデコードされたデータキャリアBufferを設定します。|
| [setVideoRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a093d4928d038dcc1c5413e771b5f8962) | ソフトウェアデコードされたビデオデータのコールバックを設定します。    |
| [setAudioRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a36183b7ad026bc3e9718e82e38497e96) | オーディオデータのコールバックを設定します。          |


### ライブストリーミングのタイムシフトインターフェース

| API                                                          | 説明         |
| ------------------------------------------------------------ | -------------- |
| [prepareLiveSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a081d01beb281348300bd9e9689949c59) | ライブストリーミングのタイムシフトの準備。|
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | ライブストリーミングのタイムシフトのジャンプ。|
| [resumeLive](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a4fa26fd4aea472d02de56d5f0bf653bf) | ライブブロードキャスト再生を再開します。|


### スクリーンショットコールバックインターフェースクラス

[ITXSnapshotListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXSnapshotListener)をご参照ください。

| API                                                          | 説明                   |
| ------------------------------------------------------------ | ---------- |
| [onSnapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) | スクリーンショットコールバック。|


### ソフトウェアデコードビデオデータコールバックインターフェースクラス

[ITXVideoRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXVideoRawDataListener)をご参照ください。

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | ------------------------------ |
| [onVideoRawDataAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a466e71718261727174795a3cd2b95d9e/34775#onvideorawdataavailable) | ソフトウェアデコーダが1フレームをデコードするごとに1回コールバックします。|


### オーディオオリジナルデータインターフェースクラス

[ITXAudioRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXAudioRawDataListener)をご参照ください。

| API                                                          | 説明                            |
| ------------------------------------------------------------ | ---------------------------------- |
| [onPcmDataAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a33e835ad16580a93ae40e0723368af32) | オーディオ再生データのコールバック。データ形式はPCMです。|
| [onAudioInfoChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a2aa86c3f5bd33047692b3d4dd0a59c32) | オーディオ再生情報コールバック。                 |


### プレーヤー音量インターフェースクラス

[ITXAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXAudioVolumeEvaluationListener)をご参照ください。

| API                                                          | 説明                                   |
| ------------------------------------------------------------ | --------------------------------------- |
| [onAudioVolumeEvaluationNotify](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ae83090684b162568b729c010acd69828) | プレーヤーの音量のコールバック。数値範囲[0,100]です。|

## TXLivePlayConfig

### Tencent Cloudライブブロードキャストプレーヤーパラメーター設定モジュール

[TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#classcom_1_1tencent_1_1rtmp_1_1TXLivePlayConfig)をご参照ください。

主に[TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html)のパラメータ設定を実行します。ほとんどの設定項目は、再生開始後に設定しても有効ではありません。

### 一般的な設定項目

| API                                                          | 説明                       |
| ------------------------------------------------------------ | ---------------------------- |
| [setAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ad2b54e62edb8d9cf287ac34a0ee0bc6e) | キャッシュ時間を自動的に調整するかどうかを設定します。   |
| [setCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ac911ed6c1650c8723d11bb4aaa49f73f) | プレーヤーのキャッシュ時間を設定します。         |
| [setMaxAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ab400433f30e53d4827b8c16c449c107c) | 最大キャッシュ時間を設定します。         |
| [setMinAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#af495df5fea5e42779c007c5600e7bc4a) | 最小キャッシュ時間を設定します。         |
| [setVideoBlockThreshold](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a5d403dd5553d58ce309f26dbec61e20f) | プレーヤーのビデオのラグアラームしきい値を設定します。|
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | プレーヤーの再接続回数を設定します。         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | プレーヤーの再接続間隔を設定します。         |


### 高級設定項目

| API                                                          | 説明         |
| ------------------------------------------------------------ | -------------- |
| [setEnableMessage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a7c8e9ce786b57f2fddf921c4f336523d) | メッセージチャネルをオンにします。|
| [enableAEC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a2fb8e9e6f182cdd49f1260484cc484e5) | エコーキャンセルを設定します。|


## ITXLivePlayListener

### Tencent Cloudライブブロードキャスト再生コールバック通知

[ITXLivePlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html)をご参照ください。

| API                                                          | 説明         |
| ------------------------------------------------------------ | -------------- |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html#a57e1f63dbe15f1242e3b842d0454f74f) | 再生イベント通知。|
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html#a826de3acd9a9d2da1604a076772f2f2e) | ネットワークステータス通知。|
