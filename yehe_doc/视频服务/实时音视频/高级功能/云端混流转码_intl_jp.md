## 適用ケース
[CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) および [クラウドレコーディングとリプレイ](https://intl.cloud.tencent.com/document/product/647/35426) などのアプリケーションユースケースでは、 TRTC ルームの複数のオーディオ・ビデオストリームを1つに常にミキシングする必要があります。Tencent Cloudサーバーの MCUのCloud MixTranscodingのクラスタを使用してこの作業を完成させることができます。MCU クラスタはマルチチャネルオーディオ・ビデオストリームをニーズに応じてミキシングし、最終的に生成したビデオストリーミングをライブ CDNおよびクラウドレコーディングシステムに送付します。

クラウドミクスストリーミングには、2種類の制御方式があります。
- 方法一：サーバーの REST API StartMCUMixTranscode および StopMCUMixTranscode を使用して制御し、この REST API はCDN relayed live streaming およびクラウドレコーディングの起動を同時にサポートできます。

- 方法二：クライアントの TRTC SDKの [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) インターフェースを使用して制御します。その原理は下図のとおりです： 
![](https://main.qcloudimg.com/raw/fd3017e7eb263b538fba858a362eab13.png)
>! 方法二は、iOS、Android、Windows、Mac および Electron のこれら5つのプラットフォームの SDKのみをサポートします。

## 原理解析
クラウドミクスストリーミングには、デコード、ミキシングおよび再エンコードの3工程があります。
- デコード：MCU はマルチチャネルオーディオビデオストリーミングをデコードし、ビデオデコード、オーディオデコードを含みます。
- ミキシング：MCU は複数の画像チャネルを一つにミキシングし、 SDK のミクスストリーミングコードコマンドに基づいて特定のレイアウトスキームを実現する必要があります。同時にMCU も、デコードされたマルチチャネルオーディオ信号をミキシング処理する必要があります。
- エンコード：MCU はミキシングされた画像およびオーディオを再エンコードして、1チャネルのオーディオ・ビデオストリームにパッケージ化し、ダウンストリームのシステム（例：ライブストリーミングやレコーディング）に配信する必要があります。

![](https://main.qcloudimg.com/raw/a5ce0215228eca3375ce47133df0be95.png)

<span id="restapi"></span>
## 方法一：サーバー REST API のミクスストリーミング方法
### ミクスストリーミングの起動
サーバーの REST API [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) をコールしてクラウドミクスストリーミングを起動できます。この APIには、以下の詳細に注意していただく必要があります。

#### 1. 画面のレイアウトモードの設定
 `StartMCUMixTranscode` の [LayoutParams](https://intl.cloud.tencent.com/document/product/647/36760#LayoutParams) パラメータによって、以下のいくつかのレイアウトモードを設定できます：

![](https://main.qcloudimg.com/raw/f2e3eae87fcc9ae61ca11e196d02f04c.png)

**フロートテンプレート**
- 始めにルームに入るユーザーのビデオ画面はスクリーンすべてに表示されます。その他のユーザーのビデオ画面は左下角から順次横に配列され、小画面で表示されます。
- 最大で4行，各行最大で4個，小画面は大画面の上部に表示。
- 最大で1つの大画面および15個の小画面をサポート。
- ユーザーが音声のみを発信する場合は、そのまま画面の位置を占有します。


**3×3マスのテンプレート**
- すべてのユーザーのビデオ画面の大きさは同じで、すべてのスクリーンを等分し、人数が増えるほど各画面のサイズは小さくなります。
- 最大で16画面を表示します。ユーザーが音声のみを発信する場合は、そのまま画面の位置を占有します。

**画面共有テンプレート**
- ビデオミーティングおよびeラーニングユースケースのレイアウトに適応。
- 画面共有（または担当者のカメラ）が終始スクリーン左側の大画面の位置を占有し、その他のユーザーは順次右側に縦方向に配列。
-  `LayoutParams.MainVideoUserId` および`LayoutParams.MainVideoStreamType` の2つのパラメータによって左側のメイン画面の内容を指定する必要があります。
- 最大で2列、各列最大で8個の小画面。最大で1個の大画面および15個の小画面をサポート。
- ユーザーが音声のみを送信する場合は、そのまま画面の位置を占用します。

#### 2. ミクスストリーミングエンコードパラメータの設定
 `StartMCUMixTranscode` の [EncodeParams](https://intl.cloud.tencent.com/document/product/647/36760#EncodeParams) パラメータによって、ミクスストリーミングエンコードパラメータを設定できます：

| 名称  |説明  | 推奨値 | 
|---------|---------|---------| 
|AudioSampleRate | ミクスストリーミング-出力ストリームオーディオサンプリングレート|  48000 |
|AudioBitrate         |ミクスストリーミング-出力ストリームオーディオビットレート、単位kbps | 64 |
|AudioChannels   |ミキシングストリーミング-出力ストリームオーディオチャネル数 | 2 |
|VideoWidth       | ミクスストリーミング-出力ストリーム幅，オーディオ・ビデオ出力時に記入必須 | カスタマイズ |
|VideoHeight      | ミクスストリーミング-出力ストリーム高、オーディオ・ビデオ出力時に記入必須 | カスタマイズ |
|VideoBitrate        | ミクスストリーミング-出力ストリームビットレート、単位kbps，オーディオ・ビデオ出力時に記入必須| カスタマイズ |
|VideoFramerate  |ミクスストリーミング-出力ストリームフレームレート，オーディオ・ビデオ出力時に記入必須 | 15 | 
|VideoGop        |ミクスストリーミング-出力ストリームgop，オーディオ・ビデオ出力時に記入必須 | 3 | 
|BackgroundColor|ミクスストリーミング-出力ストリーム背景色 | カスタマイズ |

#### 3. クラウドレコーディングの起動の有無を設定
  `StartMCUMixTranscode` の [OutputParams](https://intl.cloud.tencent.com/document/product/647/36760#OutputParams) パラメータによって、ミクスストリーミング後のビデオストリームの方向を指定できます。

- **OutputParams.RecordId**
このパラメータは、 [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426)の起動の有無を指定するのに使用します。このパラメータを指定した場合は、ミキシングされたオーディオ・ビデオストリームはファイルにレコーディングされ 、[VOD](https://intl.cloud.tencent.com/product/vod) に保存されます。レコーディングファイルは 、`OutputParams.RecordId_開始時間_終了時間` のフォーマットに従って命名されます。例：`file001_2020-02-16-12-12-12_2020-02-16-13-13-13`。

- **OutputParams.RecordAudioOnly**
音声の録音だけを希望し、ビデオコンテンツが不要の場合は、`OutputParams.RecordAudioOnly` パラメータを1に設定します。 mp3 フォーマットのファイルのみを録音することを意味します。

#### 4.  CDN relayed live streamingの起動の有無を設定

- **OutputParams.StreamId**
このパラメータは、 [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)の起動の有無を指定するのに使用します。このパラメータを指定する場合は、ミキシングされた後のオーディオ・ビデオストリームが [LVBシステム](https://intl.cloud.tencent.com/product/LVB) にインポートされます。しかし、LVBサービスをアクティブにし、再生ドメイン名の状況を設定しないと、 CDN によってこのライブストリーミングを正常に視聴することができません。

- **OutputParams.PureAudioStream**
ピュアオーディオのライブストリーミングのみを希望する場合は、`OutputParams.PureAudioStream` パラメータを 1に設定します。これは、ミキシングされたオーディオデータストリームが CDN に転送されることを意味します。

### ミクスストリーミングの終了
サーバーから REST API  [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) をコールすると、ミクスストリーミングはすぐに終了できます。

<span id="sdkapi"></span>
## 方法二：クライアント SDK API のミクスストリーミング方法
 TRTC SDK を使用してミクスストリーミングコマンドを発出するのは極めて簡単です。各プラットフォームの [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) API をコールしさえすれば、OKです。現在 SDK は、 4 種類の通常のミクスストリーミング方法を提供しています。

| パラメータ項目 | ピュアオーディオモード（PureAudio） | プリセットレイアウトモード（PresetLayout） | 画面共有モード（ScreenSharing） | 全手動モード（Manual）|
|-------|-------|-------|-------|-------|
| コール回数 | インターフェースを1回だけコールする必要 | インターフェースを1回だけコールする必要  | インターフェースを1回だけコールする必要 | 以下のユースケースではミクスストリーミングインターフェースをコールする必要：<li>マイク接続者を追加するとき</li><li>マイク接続者が解除するとき</li><li>マイク接続者がカメラをON、OFFしたとき</li><li>マイク接続者がマイクをON、OFFしたとき</li>|
| ミキシングコンテンツ |音声のみミキシング | 各チャネルのコンテンツのカスタマイズ設定 | 学生端末画面はミキシングしない | 各チャネルのコンテンツのカスタマイズ設定|
| audioSampleRate | 推奨48000 | 推奨48000 | 推奨48000 | 推奨48000|
| audioBitrate         | 推奨64       | 推奨64      | 推奨64      | 推奨64      |
| audioChannels     | 推奨2         | 推奨2        | 推奨2       | 推奨2        |
| videoWidth       | 設定の必要なし | 0は不可 | 推奨0   | 0は不可|
| videoHeight      | 設定の必要なし | 0は不可 | 推奨0   | 0は不可|
| videoBitrate      | 設定の必要なし | 0は不可 | 推奨0   | 0は不可|
| videoFramerate | 設定の必要なし | 推奨15  | 推奨15 | 推奨15 |
| videoGOP         | 設定の必要なし | 推奨3    | 推奨3   | 推奨3   |
| mixUsers 数组  | 設定の必要なし | プレースホルダの設定| 設定の必要なし | 真の userId を使用して設定|

<span id="PureAudio"></span>
### ピュアオーディオモード（PureAudio）

**適用ケース：**
ピュアオーディオモードは、オーディオ通話（AudioCall）およびボイスチャットルーム（VoiceChatRoom）などのピュアオーディオのユースケースに適用します。このユースケースでは、 SDK の [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) インターフェースをコールするとき設定することができます。
ピュアオーディオモードでは、SDK はルームのマルチチャネルのオーディオストリームを自動的に1チャネルにミキシングします。

**使用手順：**
1.  `enterRoom()` 関数をコールして入室するとき、業務のニーズに従って AppScene パラメータ を`TRTCAppSceneAudioCall` または`TRTCAppSceneVoiceChatRoom`に設定します。現在のルームにはビデオはなく、オーディオしかないことを明確にします。
2.  [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動して TRTCParams の `streamId` パラメータを設定し、 MCU 出力のミキシングオーディオストリームの行先を指定します。
3.  `startLocalAudio()` をコールしてローカルのオーディオキャプチャおよびオーディオのアップストリームを起動します。
 クラウドミクスストリーミングを行う本質は、マルチチャネルストリームを、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオビデオストリーミング上でミクスストリーミングすることですから、現在のユーザーは自身でオーディオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4.  `setMixTranscodingConfig()` インターフェースをコールしてクラウドミクスストリーミングを起動するには、コールするとき `TRTCTranscodingConfig` の `mode` パラメータを **TRTCTranscodingConfigMode_Template_PureAudio**に設定し、 `audioSampleRate`、`audioBitrate` および `audioChannels` などオーディオ出力品質に関するパラメータを指定する必要があります。
5. 上記手順を経て，現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後ファイル [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) を参考に再生ドメイン名を設定してライブストリーミングで視聴できますし、ファイル [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) を参照してミキシング後のオーディオストリーミングを録音することもできます。

>! ピュアオーディオモードでは、`setMixTranscodingConfig()` インターフェースは何度もコールする必要はありません。入室に成功しローカルオーディオのアップストリームを起動してから一回コールすればOKです。

<span id="PresetLayout"></span>
### プリセットレイアウトモード（PresetLayout）
**適用ケース：**
プリセットレイアウトモードは、ビデオ通話（VideoCall）およびILVB（LIVE）などのオーディオやビデオによく見られるユースケースに適用します。このユースケースでは SDK の [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) インターフェースをコールするとき設定できます。
プリセットレイアウトモードでは、SDK は事前に設定した各チャネル画面のレイアウトルールに従って、ルームのマルチチャネルオーディオストリームを1チャネルに自動的にミキシングします。

**使用手順：**
1.  `enterRoom()` 関数をコールして入室するときは、業務のニーズに従って AppScene パラメータを `TRTCAppSceneVideoCall` または `TRTCAppSceneLIVE`に設定します。
2.  [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動し TRTCParams の `streamId` パラメータを設定します。 MCU 出力のミキシングオーディオストリームの行先を指定します。
3.  `startLocalPreview()` および `startLocalAudio()` をコールして、ローカルのオーディオ・ビデオのアップストリームを起動します。
 クラウドミクスストリーミングを行う本質は、マルチチャネルストリームを、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオビデオストリーミング上でミクスストリーミングすることですから、現在のユーザーは自身でオーディオ・ビデオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4.  `setMixTranscodingConfig()` インターフェースをコールしてクラウドミクスストリーミングを起動します。コールが必要なときは `TRTCTranscodingConfig` の `mode` パラメータを **TRTCTranscodingConfigMode_Template_PresetLayout** に設定して、 `audioSampleRate`、`audioBitrate` および `audioChannels` などオーディオ出力品質に関連するパラメータ、並びに `videoWidth`、`videoHeight`、`videoBitrate`、`videoFramerate` などのビデオ出力の品質に関連するパラメータを指定します。
5.  `mixUser` パラメータを組み合わせ、プリセットレイアウトモードでは `mixUser` の `userId` パラメータは **$PLACE_HOLDER_REMOTE$**、**$PLACE_HOLDER_LOCAL_MAIN$** および**$PLACE_HOLDER_LOCAL_SUB$** のこれら3個が占めている文字列を使用してください。それらの意味は下表に示すとおりです。
 <table>
<tr>
<th>プレースホルダ</th>
<th>意味</th>
<th>複数をサポートの有無</th>
</tr><tr>
<td>$PLACE_HOLDER_LOCAL_MAIN$</td>
<td>ローカルカメラのチャネルを指します。</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>$PLACE_HOLDER_LOCAL_SUB$</td>
<td>ローカルの画面共有のチャネル（画面のみ）を指します。</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>$PLACE_HOLDER_REMOTE$</td>
<td>リモートマイク接続者が同時に複数を設定できることを示します。</td>
<td>サポートしています</td>
</tr></table>
6. 上記手順を経て，現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後ファイル [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) を参考に再生ドメイン名を設定してライブストリーミングで視聴できますし、ファイル [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) を参照してミキシング後のオーディオストリーミングを録音することもできます。

![](https://main.qcloudimg.com/raw/4119e41cefe59b7a8b8edf675babdd38.png)

**サンプルコード**
ここでは、 iOS 端末の Objective-C コードを例に“一大二小，上下オーバーレイ”のミキシング効果を実現します：

``` Objective-C
TRTCTranscodingConfig *config = [[TRTCTranscodingConfig alloc] init];
// 解像度は720 × 1280, ビットレートは1500kbps，フレームレートは20FPSに設定
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
// プリセットレイアウトモードを採用
config.mode = TRTCTranscodingConfigMode_Template_PresetLayout;
config.mixUsers = [NSMutableArray new];

// ホストカメラの画面位置
TRTCMixUser* local = [TRTCMixUser new];
local.userId = @"$PLACE_HOLDER_LOCAL_MAIN$"; 
local.zOrder = 0;   // zOrder を0とすることは、ホスト画面を最下層に位置付けることを意味します
local.rect   = CGRectMake(0, 0, videoWidth, videoHeight);
local.roomID = nil; // ローカルユーザーは roomIDを記入する必要はありません、リモートでは必要です。
[config.mixUsers addObject:local];
		
// マイク接続者の画面位置
TRTCMixUser* remote1 = [TRTCMixUser new];
remote1.userId = @"$PLACE_HOLDER_REMOTE$";  
remote1.zOrder = 1;
remote1.rect   = CGRectMake(400, 800, 180, 240); //参照用
remote1.roomID = 97392; // ローカルユーザーは roomIDを記入する必要はありません。リモートでは必要です
[config.mixUsers addObject:remote1];

// マイク接続者の画面位置
TRTCMixUser* remote2 = [TRTCMixUser new];
remote2.userId = @"$PLACE_HOLDER_REMOTE$"; 
remote2.zOrder = 1;
remote2.rect   = CGRectMake(400, 500, 180, 240); //参照用
remote2.roomID = 97392; // ローカルユーザーは roomIDを記入する必要はありません。リモートでは必要です
[config.mixUsers addObject:remote2];
		
// クラウドミクスストリーミングの発出
[_trtc setMixTranscodingConfig:config];
```

>! プリセットレイアウトモードでは、`setMixTranscodingConfig()` インターフェースを何度もコールする必要はありません。入室に成功しローカルオーディオのアップストリームを起動してから一回コールすればOKです。

<span id="ScreenSharing"></span>
### 画面共有モード（ScreenSharing）
**適用ケース：**
画面共有モードは、eラーニングおよびインタラクティブな授業などのユースケースに適用し、このユースケースでは SDK の [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) インターフェースをコールするとき、 AppScene パラメータを `TRTCAppSceneLIVE`に設定できます。
画面共有モードでは、SDK はまず選定した目標解像度に従って一枚のキャンバスを構築します。教師が画面共有していないとき、SDK はカメラ画面などを、このキャンバス上に比例して拡大して描出します。；教師が画面共有を起動してからは、SDK は画面共有した画面を同様にキャンバス上に描出します。キャンバスの構築によってミクスストリーミングのコンポーネントの出力解像度を一致させることができ、録画およびネットワーク視聴のビデオの互換性の問題を防止（通常再生プレイヤーは解像度が変化するビデオをサポートしません）することができます。

**使用手順：**
1.  `enterRoom()` 関数をコールして入室するときは、業務のニーズに従って AppScene パラメータを `TRTCAppSceneLIVE`に設定します。
2.  [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動し、 TRTCParams の `streamId` パラメータを設定し、 MCU 出力のミキシングオーディオ・ビデオストリームの行先を指定します。
3.  `startLocalPreview()` および `startLocalAudio()` をコールして、ローカルのオーディオ・ビデオのアップストリームを起動します。
 クラウドミクスストリーミングを行う本質は、マルチチャネルストリームを、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオビデオストリーミング上でミクスストリーミングすることですから、現在のユーザーは自身でオーディオ・ビデオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4.  `setMixTranscodingConfig()` インターフェースをコールしてクラウドミクスストリーミングを起動し、コールが必要なときは `TRTCTranscodingConfig` の `mode` パラメータを**TRTCTranscodingConfigMode_Template_ScreenSharing** に設定し、`audioSampleRate`、`audioBitrate` および`audioChannels` などのオーディオ出力品質関連のパラメータ、並びに `videoWidth`、`videoHeight`、`videoBitrate`、`videoFramerate` などのビデオ出力品質関連のパラメータを指定します。
 >? `videoWidth` および `videoHeight` パラメータを0に指定する場合は、SDK はユーザーの現在のスクリーンのアスペクト比に従って、適切な解像度を自動的に計算します。
 >
5. 上記手順を経て，現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後ファイル [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) を参考に再生ドメイン名を設定してライブストリーミングで視聴できますし、ファイル [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) を参照してミキシング後のオーディオストリーミングを録音することもできます。



> 
>- 画面共有モードは、 Windowsおよび Mac のプラットフォームのみをサポートします。
>- 画面共有モードでは、`setMixTranscodingConfig()` インターフェースは何度もコールする必要はありません。入室に成功しローカルオーディオのアップストリームを起動してから一回コールすればOKです。
>- 教育モデルでのビデオコンテンツは画面共有がメインであることから、カメラ画面および画面共有画面の同時伝送は非常に帯域幅を消費します。カメラ画面および学生の画面を `setLocalVideoRenderCallback()` および`setRemoteVideoRenderCallback()` インターフェースによって現在のスクリーン上に直接自ら描出することを提案します。
>-  TRTCTranscodingConfig の `videoWidth` および`videoHeight` パラメータをすべて 0に指定することによって、 SDK でインテリジェントに解像度の出力選択ができます。教師の現在のスクリーン幅が1920pxより小さい場合は、SDK は教師の現在のスクリーンの実際の解像度を使用します。教師の現在のスクリーンの幅が1920pxより大きい場合は、SDK は現在のスクリーンのアスペクト比に従って 1920 × 1080（16:9）、1920 × 1200（16:10）または1920 × 1440（4:3）の中から選択します。

<span id="Manual"></span>
### 全手動モード（Manual）
**適用ケース：**
全手動モードは、上述の自動モードがすべて適用できないユースケースに適合します。全手動は最もフレキシブルで、各種のミクスストリーミング方法を自由に組み合わせることができます。しかし、使い勝手は最も劣ります。
全手動モードでは、 `TRTCTranscodingConfig` のすべてのパラメータを設定し、 TRTCCloudDelegate の`onUserVideoAvailable()` および `onUserAudioAvailable()` コールバックをモニタする必要があり、これによって現在のルームでの各マイク・オンしているユーザーのオーディオ・ビデオ状態に従って `mixUsers` パラメータを絶えず調整します。この設定がないとミクスストリーミングは失敗してしまいます。

**使用手順：**
1.  `enterRoom()` 関数をコールして入室するときは、業務のニーズに応じて AppScene パラメータを設定します。
2.  [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動し、 TRTCParams の `streamId` パラメータを設定し、 MCU 出力のミキシングオーディオ・ビデオストリームの行先を指定します。
3. 業務のニーズに応じて、 `startLocalAudio()` をコールしてローカルオーディオのアップストリームを起動します（または `startLocalPreview()` を同時コールしてビデオのアップストリームの起動します）。
 クラウドミクスストリーミングを行う本質は、マルチチャネルストリームを、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオビデオストリーミング上でミクスストリーミングすることですから、現在のユーザーは自身でオーディオ・ビデオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4.  `setMixTranscodingConfig()` インターフェースをコールしてクラウドミクスストリーミングを起動します。コールの必要があるときは、 `TRTCTranscodingConfig` の `mode` パラメータを **TRTCTranscodingConfigMode_Manual** に設定し、 `audioSampleRate`、`audioBitrate` および `audioChannels` などのオーディオ出力品質関連のパラメータを指定します。業務ユースケースにもビデオがある場合は、 `videoWidth`、`videoHeight`、`videoBitrate`、`videoFramerate` などのビデオ出力品質関連のパラメータを同時に設定する必要があります。
5.  TRTCCloudDelegate の `onUserVideoAvailable()` および `onUserAudioAvailable()` コールバックをモニタし、ニーズによって **mixUsers** パラメータを指定します。
 >?プリセットレイアウト（PresetLayout）モードとは異なり、Manualでは各 `mixUser` の `userId` パラメータを実際のマイク接続者 IDに指定する必要があり、このマイク接続者がビデオを起動しているかどうかで `mixUser` の `pureAudio` パラメータもその通りに設定する必要があります。
 >
6. 上記手順を経て，現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後ファイル [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) を参考に再生ドメイン名を設定してライブストリーミングで視聴できますし、ファイル [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) を参照してミキシング後のオーディオストリーミングを録音することもできます。

>! 全手動モードでは、ルームのマイク接続者のマイク・オン、マイク・オフ動作をリアルタイムでモニタし、マイク接続者の人数やオーディオ・ビデオ状態に従って、 `setMixTranscodingConfig()` インターフェースを何度もコールする必要があります。
