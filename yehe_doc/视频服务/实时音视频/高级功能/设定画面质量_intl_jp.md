## 内容紹介

TRTRTCCloudでは、以下の方式で画質を調整できます。
- [TRTCCloud.enterRoom]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) のTRTCAppScene パラメータ：アプリケーションユースケースを使用するのに使用します。
- [TRTCCloud.setVideoEncoderParam]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)：エンコードのパラメータを設定するのに使用します。
- [TRTCCloud.setNetworkQosParam]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9)：ネットワークの制御ポリシーを設定するのに使用します。

ここでは、主に上述のパラメータを設定し、TRTC SDKの画質効果を項目のニーズに適合させる方法を紹介します。
以下のDemoを参照することもできます。
- [iOS：LivePushViewController.swift]
- [Android：LivePushActivity.java](https://github.com/tencentyun/TRTCSDK/blob/0123787812e04d3acb44eed06ec9803df363c580/Android/TRTCSimpleDemo/live/src/main/java/com/tencent/live/LivePushActivity.java)
- [Windows：TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp)
## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows |  Web | Electron|Flutter |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; | &#10003;   | &#10003;  |  &#10003;   | &#10003;  |&#10003;  |&#10003;  |

Web端末で画質の詳細操作を設定します。 [設定ガイド](https://www.qcloudtrtc.com/trtc-web-sdk/docs/api/tutorial-04-advanced-set-video-profile.html)をご参照ください。

## TRTCAppScene

- **VideoCall** 
ビデオ通信のユースケース、すなわち、長時間二人以上のビデオ通信に対応するユースケースです。内部のエンコーダーおよびネットワークプロトコルを最適化して流暢性に特化し、通話ディレーおよび遅延率を低下させます。

- **LIVE** 
ライブストリーミングのユースケース、すなわち、長時間一人でのライブストリーミングに対応し、時々多人数でのビデオインタラクティブのユースケースに対応します。内部エンコーダーおよびネットワークプロトコルは最適化して性能及び互換性に特化し、性能及び解像度をさらに良くします。	


## TRTCVideoEncParam

### 推奨する設定

| ユースケース | videoResolution |  videoFps | videoBitrate | 
|:-------------:|:-------------:|:-------------:|:-------------:|
| ビデオ通話（携帯電話） | 640x360 | 15 | 550kbps |
| ビデオミーティング（メイン画面 @ Mac Win） | 1280x720 | 15 | 1200kbps | 
| ビデオミーティング（メイン画面 @ 携帯電話） | 640x360 | 15 | 900kbps|
| ビデオミーティング（小画面） | 320x180 | 15 | 250kbps |
| eラーニング（教師 @ Mac Win） | 960x540 | 15 | 850kbps |
| eラーニング（教師 @ iPad） | 640x360 | 15 |  550kbps |
| eラーニング（学生） | 320x180 | 15 | 250kbps |

### 各フィールドの詳細説明

- **(TRTCVideoResolution) videoResolution**
エンコード解像度は、 例えば、640 x 360 はエンコードした画面の幅（画素） x 高さ（画素）を指し、TRTCVideoResolution で列挙した定義では、幅は高さ以上の長さとの横型スクリーン（Landscape）の解像度を定義しただけです。縦型スクリーン解像度を使用したい場合は、 resModeを Portraitに設定する必要があります。
 >!多くのハードウェアのコーデックが 16 で割り切れる画素数の幅のみをサポートすることから、 SDKが実際にエンコードする解像度は、必ずしもパラメータに従って自ら設定したわけではなく、 16 で割って自動で修正したものです。例えば、 640  x 360 の解像度なら、 SDK 内部では 640 x 368に対応することがありえます。

- **(TRTCVideoResolutionMode) resMode**
横スクリーンまたは縦スクリーンの解像度を指し、TRTCVideoResolution には横スクリーンの解像度しか定義していないことから、 360 x 640 のような縦スクリーン解像度を使用したい場合は、 resMode を TRTCVideoResolutionModePortraitに指定する必要があります。一般に PCおよび Macは、横スクリーン（Landscape）解像度を採用し、携帯電話は縦スクリーン（Portrait）解像度を採用しています。

- **(int) videoFps**
  フレームレート（FPS）も、毎秒どれだけのフレーム画面をエンコードするかを示すものです。15 FPSに設定することをお薦めします。そうすれば、画面が十分にスムーズに流れ、毎秒のフレーム数が多すぎることによりフレーム画面の明瞭度を下げることはありません。
	
 スムーズさへの要求が高い場合は、20FPSまたは25FPSに設定することができます。しかし、25FPSより大きい数値には設定しないでください。映画の通常のフレームレートも24FPSしかないためです。

- **(int) videoBitrate**
ビットレート（Bitrate）とは、毎秒エンコーダーがどれだけかのKbit のエンコードを出力した後のバイナリーデータのことです。 videoBitrate を 800kbpsに設定した場合は、エンコーダーが毎秒 800kbit のビデオデータを産生することになります。これらのデータを一つのファイルに保存すると、ファイル容量は 800kbit、つまり100KB、0.1MBになります。

 ビデオビットレートは高ければ良いというものではなく、解像度との間にやや適切なマッピング関係があり、下表の示すとおりになります。
 
### 解像度ビットレート参照表

| 解像度の定義 | アスペクト比 | 推奨ビットレート | ハイエンド設定 |
|:-------------:|:-------------:|:-------------:|:-------------:|
| TRTCVideoResolution_120_120 | 1:1 |   80kbps | 120kbps|
| TRTCVideoResolution_160_160 | 1:1 | 100kbps | 150kbps|
| TRTCVideoResolution_270_270 | 1:1 | 200kbps | 300kbps|
| TRTCVideoResolution_480_480 | 1:1 | 350kbps | 525kbps|
| TRTCVideoResolution_160_120 | 4:3 | 100kbps | 150kbps|
| TRTCVideoResolution_240_180 | 4:3 | 150kbps | 225kbps|
| TRTCVideoResolution_280_210 | 4:3 | 200kbps | 300kbps|
| TRTCVideoResolution_320_240 | 4:3 | 250kbps | 375kbps|
| TRTCVideoResolution_400_300 | 4:3 | 300kbps | 450kbps|
| TRTCVideoResolution_480_360 | 4:3 | 400kbps | 600kbps|
| TRTCVideoResolution_640_480 | 4:3 | 600kbps | 900kbps|
| TRTCVideoResolution_960_720 | 4:3 | 1000kbps | 1500kbps|
| TRTCVideoResolution_160_90   | 16:9 | 150kbps | 250kbps|
| TRTCVideoResolution_256_144 | 16:9 | 200kbps | 300kbps|
| TRTCVideoResolution_320_180 | 16:9 | 250kbps | 400kbps|
| TRTCVideoResolution_480_270 | 16:9 | 350kbps | 550kbps|
| TRTCVideoResolution_640_360 | 16:9 | 550kbps | 900kbps|
| TRTCVideoResolution_960_540 | 16:9 | 850kbps | 1300kbps|
| TRTCVideoResolution_1280_720 | 16:9 | 1200kbps | 1800kbps|

## TRTCNetworkQosParam
### QosPreference

ネットワークの帯域幅に比較的余裕がある状況では、明瞭度とスムーズさは同時に対応できます。しかし、ユーザーのネットワークが満足のいく状態でない場合は、最終的に明瞭度とスムーズさのどちらを優先するかを、TRTCNetworkQosParam の preference パラメータを指定することで選択することができます。 

- **スムーズさを優先（TRTCVideoQosPreferenceSmooth）**
ユーザーのネットワーク環境が脆弱な場合は、画面がぼやけ、モザイクが多くかかることがあります。しかし、スムーズさを維持しラグを軽減することができます。

- **解像度を優先（TRTCVideoQosPreferenceClear）**
ユーザーのネットワーク環境が脆弱な場合は、画面はできるだけ明瞭さを維持しますが、ラグが現れやすくなります。

### ControlMode

controlMode パラメータでは、 **TRTCQosControlModeServer** を選択すればOKです。TRTCQosControlModeClient は、Tencent Cloud研究開発チームが内部テスト用としたものですので、無視してください。

## よく見られるエラー箇所
**1. 解像度は高いほど良いのですか？**
やや高い解像度も、やや高いビットレートでのサポートが必要です。1280 x 720の解像度を選択した場合は、ビットレートを200kbpsに指定すると、画面に大量のモザイクが出てしまいます。 [解像度ビットレート参照リスト](https://intl.cloud.tencent.com/document/product/647/35153)を参照して設定することをお薦めします。

**2. フレームレートは高いほど良いですか？**
カメラで撮影する画面は、露出段階ですべての現実の物体の完全なマッピングですので、フレームレートが高いほど、スムーズに感じるわけではありません。この点でゲームのFPSと異なります。正反対に、フレームレートが高すぎると、各フレームの画質を損ない、カメラの露出時間も減少させ、効果はさらに落ちることになります。

**3. ビットレートは高いほど良いですか？**
高いビットレートも高い解像度によって対応します。 320 x 240 の解像度に、1000kbps のビットレートは大きすぎますので、 [解像度ビットレート参照リスト](https://intl.cloud.tencent.com/document/product/647/35153) を参照して設定することをお薦めします。

**4.  Wi-Fi を使用する場合、高い解像度およびビットレートを設定可能**
Wi-Fiのネット速度がいつも変わらないということはありません。無線ルーターから遠い場合、またはルーター回線が占有されている場合は、ネット速度は4Gよりも劣ることになります。
こうした状況では、TRTC SDKは速度計測機能を提供し、ビデオ通信前に速度を計測し、測定値からネットワークの良し悪しを判断します。


