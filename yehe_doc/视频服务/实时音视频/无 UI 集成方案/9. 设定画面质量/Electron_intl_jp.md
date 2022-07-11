このドキュメントでは、主にビデオ通話やInteractive Live Video Broadcastingで画質を設定する方法を紹介します。開発者は、具体的なのサービスニーズに応じてビデオ画像の鮮明さと滑らかさを調整して、ユーザーエクスペリエンスを向上させることができます。
ビデオのプロパティには、解像度、フレームレート、ビットレートが含まれます。

## 内容紹介
Electron SDKにおいて、以下の方法で画質を調整できます：
- [enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)のTRTCAppSceneパラメータ：ユースケースの選択に使用されます。
- [setVideoEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam)：エンコードパラメータの設定に使用されます。
- [setNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setNetworkQosParam)：ネットワークチューニングポリシーの設定に使用されます。

このドキュメントでは、主にTRTC SDKの画質をプロジェクトのニーズに合わせるために、上記のパラメーターを設定する方法を紹介します。
[Electron API Example：video-quality](https://github.com/tencentyun/TRTCSDK/blob/master/Electron/TRTC-API-Example/assets/code/advanced/video-quality/index.js)Demoを参照することもできます。

## TRTCAppScene

- **VideoCall：**ビデオ通話シーン、つまり、ほとんどの時間において2人以上がビデオ通話を行うシーンに対応して、内部エンコーダとネットワークプロトコルの最適化は、滑らかさ、通話遅延の低減、ラグ率に重点を置いています。
- **LIVE：**ライブストリーミングシーン、つまり、ほとんど1人がライブストリーミングし、時々に複数の人のビデオインタラクションがあるシーンに対応して、内部エンコーダとネットワークプロトコルの最適化は、性能と互換性に重点を置き、性能と鮮明さが向上します。	


## TRTCVideoEncParam

### 推奨される構成

| ユースケース | videoResolution |  videoFps | videoBitrate | 
|:-------------:|:-------------:|:-------------:|:-------------:|
| ビデオ会議（メイン画面 @ Mac Win） | 1280x720 | 15 | 1200kbps | 
| オンライン教育（教師 @ Mac Win） | 960x540 | 15 | 850kbps |

### 各フィールドの詳細な説明

- **(TRTCVideoResolution) videoResolution**
640 x 360などのエンコード解像度は、エンコードされた画像の幅（ピクセル）x高さ（ピクセル）を指します。TRTCVideoResolution列挙定義で幅>=高さの横向きの解像度のみを定義します。縦向きを使用する場合はresModeをPortraitに設定してください。
>!多くのハードウェアコーデックは16で割り切れるピクセル幅のみをサポートするため、SDKによって実際にエンコードされる解像度は、必ずしもパラメータに従って完全にカスタマイズされるとは限りませんが、16で割り切れる値によって自動的に修正されます。たとえば、640x360の解像度は、SDK内部で640x368に適合させることができます。

- **(TRTCVideoResolutionMode) resMode**
横向きまたは縦向きの解像度を指します。TRTCVideoResolutionでは横向きの解像度のみが定義されているため、360x640などの縦向きの解像度を使用する場合は、resModeをTRTCVideoResolutionModePortraitとして指定してください。一般的に、PCとMacは横向き(Landscape)の解像度を使用し、携帯電話は縦向き(Portrait)の解像度を使用します。

- **(int) videoFps**
  フレームレート(FPS)も、毎秒どれだけのフレーム画面をエンコードするかを示すものです。15 FPSに設定することをお勧めします。そうすれば、画面が十分にスムーズに流れ、毎秒のフレーム数が多すぎることによりフレーム画面の解像度を下げることはありません。
	
 滑らかさの要件が高い場合は、20FPSまたは25FPSに設定できます。ただし、映画の通常のフレームレートは24FPSのみであるため、25FPS以上の値を設定しないでください。

- **(int) videoBitrate**
ビデオビットレートは、エンコーダが1秒間に出力するエンコードされたバイナリデータのKbit数です。videoBitrateを800kbpsに設定すると、エンコーダは1秒間に800kbitのビデオデータを生成します。これらのデータをファイルとして保存すると、ファイルサイズは800kbit、つまり100KB、つまり0.1Mになります。

 ビデオのビットレートは高いほどよいとは限りません。次の表に示すように、ビデオのビットレートと解像度との間にはより適切なマッピング関係が必要です。
 
### 解像度とビットレートの参照テーブル

| 解像度の定義 | アスペクト比 | 推奨ビットレート（VideoCall） | 推奨ビットレート（LIVE） |
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
|TRTCVideoResolution_1920_1080 	| 16:9 | 2000kbps| 3000kbps |

## TRTCNetworkQosParam
### QosPreference

ネットワーク帯域幅が十分な場合は、鮮明さと滑らかさの両方を考慮に入れることができますが、ユーザーのネットワークが理想的でない場合、鮮明さと滑らかさを確保するための優先事項はどちらですか？TRTCNetworkQosParamのpreferenceパラメータを指定して選択できます。 

- **滑らかさを優先とする（TRTCVideoQosPreferenceSmooth）**
ユーザーが弱いネットワーク環境に遭遇すると、画像がぼやけてモザイクが増えますが、滑らかなままになるか、わずかにラグする可能性があります。

- **鮮明さを優先とする（TRTCVideoQosPreferenceClear）**
ユーザーが弱いネットワーク環境に遭遇すると、画像は可能な限り鮮明に保たれますが、ラグしやすくなる可能性があります。

### ControlMode

controlModeパラメーターには**TRTCQosControlModeServer**を選択してよいです。TRTCQosControlModeClientは、Tencent Cloud R&Dチームが内部デバッグに使用されます。注意しないでください。

## よくある間違い
#### 1. 解像度が高いほど良いですか。
解像度が高いほど、サポートするにはビットレートも高くなります。解像度が1280x720で、ビットレートが200kbpsに指定されている場合、画像には多くのモザイクが現れます。設定については、[解像度とビットレートの参照テーブル](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution)を参照することをお勧めします。

#### 2. フレームレートが高いほど良いですか。
カメラで取得した画像は、露光段階のすべての実物を完全にマッピングしたものであるため、フレームレートが高いほど感覚が滑らかになるわけではなく、これはゲームのFPSとは異なります。逆に、フレームレートが高すぎると、各フレームの画質が低下し、カメラの露光時間も短くなり、効果がより低下する場合があります。

#### 3. ビットレートが高いほど良いですか。
ビットレートが高いほど、一致する解像度も高くなります。320x240などの解像度の場合、1000kbpsのビットレートは無駄です。設定については、[解像度とビットレートの参照テーブル](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution)を参照することをお勧めします。

#### 4. Wi-Fi使用時に高い解像度とビットレートを設定できますか。
Wi-Fiの速度が一定というわけではありません。無線ルーターから遠く離れている場合やルーターのチャネルが占有されている場合は、ネットワーク速度が4Gほど良くない場合があります。
このような状況に対応するために、TRTC SDKは速度測定機能を提供しており、ビデオ通話前に速度を測定し、採点値に応じてネットワークの品質を判断することができます。

