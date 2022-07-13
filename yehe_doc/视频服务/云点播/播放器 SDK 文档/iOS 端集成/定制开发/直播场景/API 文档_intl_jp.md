## TXLivePlayer

### ビデオプレーヤー

[TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html)をご参照ください。

主にライブストリームのオーディオビデオ画面のデコードとローカルレンダリングを実行します。次の技術的特徴が含まれています：

- Tencent Cloudのプルアドレスに対し、低遅延プルを使用し、ライブストリーミングのマイク接続などの関連シーンを実現できます。
- Tencent Cloudのプルアドレスに対し、ライブストリーミングのタイムシフト機能が利用でき、ライブストリーミング視聴とタイムシフト視聴のシームレスな切り替えが可能になります。
- カスタマイズされたオーディオビデオデータ処理をサポートしているため、プロジェクトのニーズに合わせてライブストリームのオーディオビデオデータを処理した後、レンダリングと再生を実行することができます。

### SDK基本関数 

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | 再生コールバックを設定します。`TXLivePlayListener.h`ファイルの詳細定義をご参照ください。     |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | ビデオ処理コールバックを設定します。`TXVideoCustomProcessDelegate.h`ファイルの詳細定義をご参照ください。|
| [audioRawDataDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a4d08f185792a92a087aff32b52b6b7b9) | オーディオ処理コールバックを設定します。`TXAudioRawDataDelegate.h`ファイルの詳細定義をご参照ください。|
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | ハードウェアアクセラレーションをオンにするかどうか。デフォルト値はNOです。                               |
| [config](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aac73c062f0bbe5d97be40d85b68cb98a) | [TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aac73c062f0bbe5d97be40d85b68cb98a)の再生設定項目を設定します。`TXLivePlayConfig.h`ファイルの詳細定義をご参照ください。|
| [recordDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7a3f4c66d5019d8e8899823e04be924d) | ショート動画録画コールバックを設定します。`TXLiveRecordListener.h`ファイルの詳細定義をご参照ください。|
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a946828345d302a28708d78fa1a931763) | startPlay後すぐに再生するかどうか。デフォルトではYESで、オンデマンドのみが有効です。           |


### 再生基本インターフェース

| API                                                          | 説明                                             |
| ------------------------------------------------------------ | -------------------------------------------------- |
| [setupVideoWidget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a9195fa66ee874328a5b48400f2a0cb14) | VideoのレンダリングViewを作成します。このコントロールはビデオコンテンツの表示を実行します。|
| [removeVideoWidget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#adf77d29895e70602556fdc51b931951e) | VideoレンダリングWidgetを削除します。                           |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a37e97416ec7a5853d217679be49cea26) | 指定したURLからRTMPオーディオビデオストリームの再生を開始します。                |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | オーディオビデオストリームの再生を停止します。                                   |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7d3378ad416bfd00522acaedefc47dda) | 再生されているかどうか。                                     |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | 再生の一時停止。                                         |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a41de8150eff044a237990c271d57ea27) | 引き続き再生します。オンデマンドやライブストリーミングに適用します。                       |


### ビデオ関連インターフェース

| API                                                          | 説明                   |
| ------------------------------------------------------------ | -------------------- |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | 画面の向きを設定します。     |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | 画面の切り取りモードを設定します。|
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa24051e4c0271d994a5008cfc2db4775) | スクリーンショット。               |


### 音声に関連するインターフェース

| API                                                          | 説明                                   |
| ------------------------------------------------------------ | -------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | ミュートを設定します。                             |
| [setVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a5a3bf801bad5591a3d8fe284aa6b3134) | 音量を設定します。                             |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#ad56c52832a8efe45d6e0c50049406d74) | サウンド再生モード（スピーカーや受話器の切り替え）を設定します。|
| [setAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a87d74a7afe3f768bd9e7ca276a189533) | 音量コールバックインタフェースを設定します。                 |


### ライブストリーミングのタイムシフトに関するインターフェース

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | ------------------------------------------ |
| [prepareLiveSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#acf638c46e1e866ef06abda5ac938f07f) | ライブストリーミングタイムシフトの準備をし、ライブストリーミングの開始時間をプルします。|
| [resumeLive](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a4fa26fd4aea472d02de56d5f0bf653bf) | タイムシフト再生を停止し、ライブストリーミングに戻ります。                   |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | -                                          |


### ビデオ録画関連インターフェース

| API               | 説明               |
| ------------------------------------------------------------ | ---------------- |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7224d5a8ab5fadc1d4c0fe1feb6ac972) | ショート動画の録画を開始します。|
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a13313c5410c2a10a704b991f28141e6e) | ショート動画の録画を終了します。|
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | 再生レートを設定します。   |


### その他の実用的なインターフェース

| API                                                          | 説明                                   |
| ------------------------------------------------------------ | ----------------------------------------- |
|[setLogViewMargin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa906f88b51df74ab8f3c1125d9856293)|は、レンダリングview上のポップオーバーviewのマージンを設定します。  |
| [showVideoDebugLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a70ec322b088ad3c38b5a41d7528467f2) | 再生状態の統計とイベントメッセージのポップオーバーviewを表示するかどうかを指定します。|
| [switchStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a88751ad91dff45a9d6cc96dbda903b69) | FLVライブストリーミングをシームレスに切り替えます。                        |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | 実験的なAPIインタフェースを呼び出します。                     |


### 列挙値

| 列挙                                                         | 説明                   |
| ------------------------------------------------------------ | ---------------------- |
| [TX_Enum_PlayType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#gaa164f735d1c349ce715f313c5d75892a) | サポートされているライブストリーミング及びオンデマンドのタイプ。|


## TXLivePlayConfig

### Tencent Cloudライブブロードキャストプレーヤーパラメーター設定モジュール

[TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__ios.html#interfaceTXLivePlayConfig)をご参照ください。

主に[TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html)のパラメータ設定を実行します。ほとんどの設定項目は、再生開始後に設定しても有効ではありません。

## TXLivePlayListener

### Tencent Cloudライブブロードキャスト再生コールバック通知

[TXLivePlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html)をご参照ください。

| API                                                          | 説明         |
| ------------------------------------------------------------ | -------------- |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html#a1e33d0cf9ed5f89ea2db32d0d7db9701) | ライブストリーミングイベント通知。|
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html#aee80e62b7950c7d0a75ab97d993c10c6) | ネットワークステータス通知。|

