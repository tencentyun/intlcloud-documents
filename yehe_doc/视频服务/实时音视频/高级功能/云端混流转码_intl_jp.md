## 適用ケース

[CDN Relayed live Streaming](https://intl.cloud.tencent.com/document/product/647/35242)および[クラウドレコーディングおよび再生](https://intl.cloud.tencent.com/document/product/647/35426) などのアプリケーションユースケースでは、TRTCルームの複数のオーディオ・ビデオストリーミングを1つに常にミキシングする必要があります。Tencent CloudサーバーのMCUのミクスストリーミングトランスコードクラスターを使用してこの作業を完成させることができます。MCUクラスターはマルチチャネルオーディオ・ビデオストリーミングをニーズに応じてミキシングし、最終的に生成したビデオストリームをライブCDNおよびクラウドレコーディングシステムに送付します。

クラウドミクスストリーミングには、2種類の制御方式があります。

- **方法1**：サーバーのRESTインターフェースStartMCUMixTranscode（[数字のルーム番号バージョン](https://intl.cloud.tencent.com/document/product/647/37761) / [文字列のルーム番号バージョン](https://intl.cloud.tencent.com/document/product/647/39637)）およびStopMCUMixTranscode（[数字のルーム番号バージョン](https://intl.cloud.tencent.com/document/product/647/37760) / [文字列のルーム番号バージョン](https://intl.cloud.tencent.com/document/product/647/39636)）を使用して制御を実行します。そのインターフェースはCDN視聴およびクラウドレコーディングの起動もサポートしています。
- **方法2**：クライアントのTRTC SDKの[setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)インターフェースを使用して制御します。その原理は下図のとおりです。 
  ![](https://main.qcloudimg.com/raw/fd3017e7eb263b538fba858a362eab13.png)

>! 方法2は、iOS、Android、Windows、Mac、Electron、FlutterおよびデスクトップブラウザプラットフォームのSDKをサポートします。

## 原理解析

クラウドミクスストリーミングには、デコード、ミキシングおよび再エンコードの3つのプロセスがあります。

- **デコード**：MCUは、ビデオデコードやオーディオデコードなど、マルチチャネルオーディオ・ビデオストリーミングをデコードする必要があります。
- **ミキシング**：MCUは複数の画像チャネルを一つにミキシングし、SDKのミクスストリーミングコードコマンドに基づいて特定のレイアウトスキームを実現する必要があります。同時にMCUも、デコードされたマルチチャネルオーディオ信号をミキシング処理する必要があります。
- **エンコード**：MCUはミキシングされた画像およびオーディオを再エンコードして、1チャネルのオーディオ・ビデオストリーミングにパッケージ化し、ダウンストリームのシステム（例：ライブストリーミングやレコーディング）に配信する必要があります。

![](https://main.qcloudimg.com/raw/a5ce0215228eca3375ce47133df0be95.png)

[](id:restapi)

## 方法1：サーバーREST APIのミクスストリーミング方法

### ミクスストリーミングの起動

サーバーのREST API[StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)を呼び出してクラウドミクスストリーミングを起動できます。この APIについては、以下の詳細に注意していただく必要があります。

[](id:restapi_step1)

#### 手順1：画面のレイアウトモードの設定（必須）
`StartMCUMixTranscode`内の[LayoutParams]パラメータを使用して、以下のような様々なレイアウトモードを設定することができます。
![](https://main.qcloudimg.com/raw/be0205b5f624679302e57ca5aa1b133f.png)

**フロートテンプレート(LayoutParams.Template = 0)**

- 最初に入室するユーザーのビデオ画面は、全画面表示されます。その他のユーザーのビデオ画面は左下隅から順次横に配列され、小画面で表示されます。
- 最大で4行、各行最大で4個、小画面は大画面の上部に表示。
- 最大で1つの大画面および15個の小画面をサポート。
- ユーザーが音声のみを送信する場合は、そのまま画面の位置を占用します。

**グリッドテンプレート(LayoutParams.Template = 1)**

- すべてのユーザーのビデオ画面の大きさは同じで、画面全体が等分され、人数が増えるほど各画面のサイズは小さくなります。
- 最大で16画面を表示します。ユーザーが音声のみを発信する場合は、そのまま画面の位置を占有します。

**画面共有テンプレート(LayoutParams.Template = 2)**

- ビデオミーティングおよびeラーニングユースケースのレイアウトに適しています。
- 画面共有（または話し手のカメラ）は常にスクリーン左側の大画面の位置を占有し、その他のユーザーは順次右側に縦方向に配列されます。
- `LayoutParams.MainVideoUserId`および`LayoutParams.MainVideoStreamType`の2つのパラメータによって左側のメイン画面の内容を指定する必要があります。
- 最大で2列、各列最大で小画面8個、最大で大画面1個および小画面15個をサポートします。
- ユーザーが音声のみを送信する場合は、そのまま画面の位置を占用します。

**ピクチャーインピクチャーテンプレート(LayoutParams.Template = 3)**

- このテンプレートは、「大画面1つ小画面1つを前後に配置」というモードでルーム内の画面2つをミキシングします。これは、ルーム内で大画面1つを画面全体に表示し、小画面1つを大画面上に重ねて表示させた状態にします。小画面の位置はパラメータで指定できます。
- `LayoutParams`の`MainVideoUserId`および` MainVideoStreamType`パラメータを使用して、大画面のユーザーIDとストリームタイプを指定できます。
- `LayoutParams`の`SmallVideoLayoutParams`パラメータを使用して、小画面のユーザーIDとストリームタイプおよびレイアウト位置などの情報を指定できます。
- シーン例1：eラーニングのシーンでは、講師側のカメラ（通常は小画面）と講師側のスクリーン（通常は大画面）という2つのチャネルの画面がミキシングされ、教室内の受講生の声がミキシングされます。
- シーン例2：1対1のビデオ通話のシーンでは、リモートユーザーの画面（通常は大画面）とローカルユーザーの画面（通常は小画面）がミキシングされます。

**カスタムテンプレート(LayoutParams.Template = 4)**

- 各チャネルの画面位置をカスタマイズする必要があるシーンで使用します。`LayoutParams`の`PresetLayoutConfig`パラメータ（これは1つの配列）を介して、各チャネル画面の位置を事前に設定できます。
- `PresetLayoutConfig`パラメータの`UserId`パラメータを指定しない場合、レイアウトエンジンは、入室するユーザーを入室する順序に従って、`PresetLayoutConfig`配列で指定された各位置に順番に割り当てます。
- `PresetLayoutConfig`配列の1つが`UserId`パラメータに指定されている場合、レイアウトエンジンは指定されたユーザーのために画面内での位置を事前に確保します。
- ユーザーがアップストリームオーディオのみを使用し、アップストリームビデオを使用しない場合でも、ユーザーは画面位置を占有します。
- `PresetLayoutConfig`配列のプリセット位置がすべて使われると、レイアウトエンジンは他のユーザーの画面と音声をミキシングしなくなります。

>! クラウドミクスストリーミングサービスは、最大16チャネルのオーディオ・ビデオストリーミングを同時にサポートします。ユーザーがオーディオしか持っていない場合は、1チャネルとしてカウントされます。

[](id:restapi_step2)
#### 手順2：ミクスストリーミングコーデックパラメータ（必須）
`StartMCUMixTranscode`内の[EncodeParams]パラメータを使用して、ミクスストリーミングコーデックパラメータを設定することができます。

| 名称            | 説明                                         | 推奨値 |
| --------------- | -------------------------------------------- | ------ |
|AudioSampleRate | ミクスストリーミング-出力ストリームオーディオサンプルレート                       |  48000  |
|AudioBitrate    |ミクスストリーミング-出力ストリームオーディオビットレート。単位はkbps               | 64     |
|AudioChannels   |ミクスストリーミング-出力ストリームオーディオサウンドチャネル数                        | 2      |
| VideoWidth      | ミクスストリーミング-出力ストリーム幅。オーディオ・ビデオ出力時に入力必須              | カスタマイズ |
| VideoHeight     | ミクスストリーミング-出力ストリーム高。オーディオ・ビデオ出力時に入力必須             | カスタマイズ |
| VideoBitrate    | ミクスストリーミング-出力ストリームビットレート。単位はkbps。オーディオ・ビデオ出力時に入力必須 | カスタマイズ |
| VideoFramerate | ミクスストリーミング-出力ストリームフレームレート。オーディオ・ビデオ出力時に入力必須            | 15     |
| VideoGop        | ミクスストリーミング-出力ストリームGOP。オーディオ・ビデオ出力時に入力必須            | 3      |
| BackgroundColor | ミクスストリーミング-出力ストリーム背景色                            | カスタマイズ |

[](id:restapi_step4)
#### 手順3：合成後のstreamIDを指定（必須）
- **OutputParams.StreamId**
  このパラメータを使用して、ミキシング後のオーディオ・ビデオストリーミングをライブCDN上のstreamIDで指定することができます。ただし、ライブストリーミングサービスを有効にして再生ドメイン名を設定済みの状況でのみ、CDNを使用してこのCSSストリームを正常に視聴することができます。
- **OutputParams.PureAudioStream**
  ピュアオーディオのライブストリーミングのみを希望する場合は`OutputParams.PureAudioStream`パラメータを 1に設定します。これは、ミキシングされたオーディオデータストリームがCDNに転送されることを意味します。

[](id:restapi_step3)
#### 手順4：クラウドレコーディングの起動の有無の設定（オプション）
- **OutputParams.RecordId**
  このパラメータは、[クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426)の起動の有無を指定するのに使用します。このパラメータを指定した場合は、ミキシングされたオーディオ・ビデオストリーミングはファイルにレコーディングされ、[VOD](https://intl.cloud.tencent.com/zh/document/product/266)に保存されます。レコーディングファイルは、`OutputParams.RecordId_開始時間_終了時間`のフォーマットに従って命名されます。例：`file001_2020-02-16-12-12-12_2020-02-16-13-13-13`。
- **OutputParams.RecordAudioOnly**
  音声の録音だけを希望し、ビデオコンテンツが不要の場合は`OutputParams.RecordAudioOnly`パラメータを1に設定します。mp3フォーマットのファイルのみを録音することを意味します。

### ミクスストリーミングの終了

サーバーからREST API[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)を呼び出すと、ミクスストリーミングはすぐに終了できます。

[](id:sdkapi)

## 方法2：クライアントSDK APIのミクスストリーミング方法

TRTC SDKを使用してミクスストリーミングコマンドを発出するのは非常に簡単です。各プラットフォームの[setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)APIを呼び出せば完了です。現在SDKは、一般的に使用されている4種類のミクスストリーミングスキームを提供しています。

<table>
<thead><tr><th>パラメータ項目</th>
<th width="10%">ピュアオーディオモード（PureAudio）</th>
<th width="10%">プリセットレイアウトモード(PresetLayout)</th>
<th width="10%">画面共有モード（ScreenSharing）</th>
<th>全手動モード（Manual）</th>
</tr></thead>
<tbody><tr>
<td>呼び出し頻度</td>
<td>インターフェースを1回だけ呼び出す必要があります</td>
<td>インターフェースを1回だけ呼び出す必要があります</td>
<td>インターフェースを1回だけ呼び出す必要があります</td>
<td>次のケースではミクスストリーミングインターフェースを呼び出す必要あり：<li>マイク接続者を追加するとき</li><li>マイク接続者を解除するとき</li><li>マイク接続者がカメラをオン・オフしたとき</li><li>マイク接続者がマイクをオン・オフしたとき</li></td>
</tr><tr>
<td>コンテンツのミキシング</td>
<td>オーディオのみをミキシング</td>
<td>各チャネルのコンテンツをカスタマイズ</td>
<td>受講生端末画面はミキシングしない</td>
<td>各チャネルのコンテンツをカスタマイズ</td>
</tr><tr>
<td>audioSampleRate</td>
<td>48000を推奨</td>
<td>48000を推奨</td>
<td>48000を推奨</td>
<td>48000を推奨</td>
</tr><tr>
<td>audioBitrate</td>
<td>64を推奨</td>
<td>64を推奨</td>
<td>64を推奨</td>
<td>64を推奨</td>
</tr><tr>
<td>audioChannels</td>
<td>2を推奨</td>
<td>2を推奨</td>
<td>2を推奨</td>
<td>2を推奨</td>
</tr>
<tr><td>videoWidth</td>
<td>設定不要</td>
<td>0にできません</td>
<td>0を推奨</td>
<td>0にできません</td>
</tr><tr>
<td>videoHeight</td>
<td>設定不要</td>
<td>0にできません</td>
<td>0を推奨</td>
<td>0にできません</td>
</tr><tr>
<td>videoBitrate</td>
<td>設定不要</td>
<td>0にできません</td>
<td>0を推奨</td>
<td>0にできません</td>
</tr><tr>
<td>videoFramerate</td>
<td>設定不要</td>
<td>15を推奨</td>
<td>15を推奨</td>
<td>15を推奨</td>
</tr><tr>
<td>videoGOP</td>
<td>設定不要</td>
<td>3を推奨</td>
<td>3を推奨</td>
<td>3を推奨</td>
</tr><tr>
<td> mixUsers配列</td>
<td>設定不要</td>
<td>プレースホルダー設定を使用</td>
<td>設定不要</td>
<td>実際のuserId設定を使用</td>
</tr></tbody></table>


[](id:PureAudio)

### ピュアオーディオモード（PureAudio）

#### 適用ケース

ピュアオーディオモードは、オーディオ通話（AudioCall）およびボイスチャットルーム（VoiceChatRoom）などのピュアオーディオのユースケースに適用します。このユースケースでは、SDKの[enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)インターフェースを呼び出すときに設定することができます。
ピュアオーディオモードでは、SDKはルームのマルチチャネルのオーディオストリームを自動的に1チャネルにミキシングします。

#### 使用手順

1. `enterRoom()`関数を呼び出して入室するとき、業務のニーズに従ってAppSceneパラメータを`TRTCAppSceneAudioCall` または`TRTCAppSceneVoiceChatRoom`に設定します。現在のルームにはビデオはなく、オーディオしかないことを明確にします。
2. [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動し、TRTCParamsの`streamId`パラメータを設定します。MCU出力のミキシングオーディオストリームの行先を指定します。
3. `startLocalAudio()`を呼び出してローカルのオーディオキャプチャおよびオーディオのアップストリームを起動します。
>? クラウドミクスストリーミングは、本質的に、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオ・ビデオストリーミング上でマルチチャネルストリームをミクスストリーミングすることですから、現在のユーザーは自身でオーディオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4. `setMixTranscodingConfig()`インターフェースを呼び出してクラウドミクスストリーミングを起動するには、呼び出すときに`TRTCTranscodingConfig`の`mode`パラメータを**TRTCTranscodingConfigMode_Template_PureAudio**に設定し、`audioSampleRate`、`audioBitrate`および`audioChannels`などオーディオ出力品質に関するパラメータを指定する必要があります。
5. 上記手順を経て、現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後は、ドキュメント[CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を参照して再生ドメイン名を設定し、ライブストリーミングで視聴できます。また、ドキュメント[クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426)を参照してミキシング後のオーディオストリーミングを録音することもできます。

>! ピュアオーディオモードでは、`setMixTranscodingConfig()`インターフェースは何度も呼び出す必要はありません。入室に成功しローカルオーディオのアップストリームを起動してから1度呼び出せばOKです。

[](id:PresetLayout)
### プリセットレイアウトモード（PresetLayout）
#### 適用ケース
プリセットレイアウトモードは、ビデオ通話（VideoCall）およびインタラクティブライブストリーミング（LIVE）などのオーディオとビデオの両方を利用するユースケースに適用します。このユースケースではSDKの[enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)インターフェースを呼び出すときに設定できます。
プリセットレイアウトモードでは、SDKは事前に設定した各チャネル画面のレイアウトルールに従って、ルームのマルチチャネルオーディオストリームを1チャネルに自動的にミキシングします。

#### 使用手順
1. `enterRoom()`関数を呼び出して入室するときは、業務のニーズに従ってAppSceneパラメータを`TRTCAppSceneVideoCall`または`TRTCAppSceneLIVE`に設定します。
2. [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動し、TRTCParamsの`streamId`パラメータを設定します。MCU出力のミキシングオーディオストリームの行先を指定します。
3. `startLocalPreview()`および`startLocalAudio()`を呼び出して、ローカルのオーディオ・ビデオのアップストリームを起動します。
>? クラウドミクスストリーミングは、本質的に、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオ・ビデオストリーミング上でマルチチャネルストリームをミクスストリーミングすることですから、現在のユーザーは自身でオーディオ・ビデオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4. `setMixTranscodingConfig()`インターフェースを呼び出してクラウドミクスストリーミングを起動します。呼び出しが必要なときは`TRTCTranscodingConfig`の`mode`パラメータを**TRTCTranscodingConfigMode_Template_PresetLayout**に設定して、`audioSampleRate`、`audioBitrate`および`audioChannels`などオーディオ出力品質に関連するパラメータ、並びに`videoWidth`、`videoHeight`、`videoBitrate`、`videoFramerate`などのビデオ出力の品質に関連するパラメータを指定します。
5. `mixUser`パラメータを組み合わせます。プリセットレイアウトモードでは、`mixUser`の`userId`パラメータには**$PLACE_HOLDER_REMOTE$**、**$PLACE_HOLDER_LOCAL_MAIN$**および**$PLACE_HOLDER_LOCAL_SUB$**の3つのプレースホルダーの文字列を使用します。これらの意味は下表に示すとおりです。
<table>
<tr><th>プレースホルダー</th><th>意味</th><th>複数サポートの有無</th></tr><tr>
<td>$PLACE_HOLDER_LOCAL_MAIN$</td><td>ローカルカメラのチャネルを示しています</td><td>サポートなし</td>
</tr><tr>
<td>$PLACE_HOLDER_LOCAL_SUB$</td><td>ローカル画面共有（画面のみ）を示しています</td><td>サポートなし</td>
</tr><tr>
<td>$PLACE_HOLDER_REMOTE$</td><td>リモートマイク接続者が同時に複数設定可能であることを示しています</td><td>サポートあり</td>
</tr></table>
6. 上記手順を経て、現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後は、ドキュメント[CDN Relayed live Streaming](https://intl.cloud.tencent.com/document/product/647/35242)を参照して再生ドメイン名を設定し、ライブストリーミングで視聴できます。また、ドキュメント[クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426)を参照してミキシング後のオーディオストリーミングを録音することもできます。

![](https://main.qcloudimg.com/raw/4119e41cefe59b7a8b8edf675babdd38.png)

[](id:example_code)

#### サンプルコード
次のサンプルコードを使用して、「大画面1枚・小画面2枚を上下にオーバーレイ」というミキシング効果を実現できます。
<dx-codeblock>
::: iOS  Objective-C 
TRTCTranscodingConfig *config = [[TRTCTranscodingConfig alloc] init];
// 解像度は720 × 1280、ビットレートは1500kbps、フレームレートは20FPSに設定します
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// プリセットレイアウトモードを採用します
config.mode = TRTCTranscodingConfigMode_Template_PresetLayout;
config.mixUsers = [NSMutableArray new];

// キャスターカメラの画面位置
TRTCMixUser* local = [TRTCMixUser new];
local.userId = @"$PLACE_HOLDER_LOCAL_MAIN$"; 
local.zOrder = 0;   // zOrderを0とすることは、キャスター画面を最下層に位置付けることを意味します
local.rect   = CGRectMake(0, 0, videoWidth, videoHeight);
local.roomID = null; // ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
[config.mixUsers addObject:local];

// マイク接続者の画面位置
TRTCMixUser* remote1 = [TRTCMixUser new];
remote1.userId = @"$PLACE_HOLDER_REMOTE$"; 
remote1.zOrder = 1;
remote1.rect   = CGRectMake(400, 800, 180, 240); //参照用
remote1.roomID = 97392; // ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
[config.mixUsers addObject:remote1];

// マイク接続者の画面位置
TRTCMixUser* remote2 = [TRTCMixUser new];
remote2.userId = @"$PLACE_HOLDER_REMOTE$"; 
remote2.zOrder = 1;
remote2.rect   = CGRectMake(400, 500, 180, 240); //参照用
remote2.roomID = 97392; // ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
[config.mixUsers addObject:remote2];

// クラウドミクスストリーミングを開始します
[_trtc setMixTranscodingConfig:config];
:::
::: Android java
TRTCCloudDef.TRTCTranscodingConfig config = new TRTCCloudDef.TRTCTranscodingConfig();
// 解像度は720 × 1280、ビットレートは1500kbps、フレームレートは20FPSに設定します
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// プリセットレイアウトモードを採用します
config.mode = TRTCCloudDef.TRTC_TranscodingConfigMode_Template_PresetLayout;
config.mixUsers = new ArrayList<>();

// キャスターカメラの画面位置
TRTCCloudDef.TRTCMixUser local = new TRTCCloudDef.TRTCMixUser();
local.userId = "$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0;   // zOrderを0とすることは、キャスター画面を最下層に位置付けることを意味します
local.x      = 0;
local.y      = 0;
local.width  = videoWidth;
local.height = videoHeight;
local.roomId = null; // ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
config.mixUsers.add(local);

// マイク接続者の画面位置
TRTCCloudDef.TRTCMixUser remote1 = new TRTCCloudDef.TRTCMixUser();
remote1.userId = "$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.x      = 400; //参照用
remote1.x      = 800; //参照用
remote1.width  = 180; //参照用
remote1.height = 240; //参照用
remote1.roomId = "97392"; //ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
config.mixUsers.add(remote1);

// マイク接続者の画面位置
TRTCCloudDef.TRTCMixUser remote2 = new TRTCCloudDef.TRTCMixUser();
remote2.userId = "$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote1.x      = 400; //参照用
remote1.x      = 500; //参照用
remote1.width  = 180; //参照用
remote1.height = 240; //参照用
remote1.roomId = "97393"; //ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
config.mixUsers.add(remote2);

// クラウドミクスストリーミングを開始します
trtc.setMixTranscodingConfig(config);
:::
::: C++ C++
TRTCTranscodingConfig config;
// 解像度は1280 × 720、ビットレートは1500kbps、フレームレートは20fpsに設定します
config.videoWidth      = 1280;
config.videoHeight     = 720;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// プリセットレイアウトモードを採用します
config.mode == TRTCTranscodingConfigMode_Template_PresetLayout
TRTCMixUser* mixUsersArray = new TRTCMixUser[3];
mixUsersArray[0].userId      = "$PLACE_HOLDER_LOCAL_MAIN$";
mixUsersArray[0].zOrder      = 0; // zOrderを0とすることは、キャスター画面を最下層に位置付けることを意味します
mixUsersArray[0].rect.left   = 0;
mixUsersArray[0].rect.top    = 0;    
mixUsersArray[0].rect.right  = videoWidth;
mixUsersArray[0].rect.bottom = videoHeight;
mixUsersArray[0].roomId      = nullptr; //ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です

mixUsersArray[1].userId      = "$PLACE_HOLDER_REMOTE$";
mixUsersArray[1].zOrder      = 1;
mixUsersArray[1].rect.left   = 400; //参照用
mixUsersArray[1].rect.top    = 800; //参照用
mixUsersArray[1].rect.right  = 180; //参照用
mixUsersArray[1].rect.bottom = 240; //参照用
mixUsersArray[1].roomId      = "97392"; //ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です

mixUsersArray[2].userId      = "$PLACE_HOLDER_REMOTE$";
mixUsersArray[2].zOrder      = 1;
mixUsersArray[2].rect.left   = 400; //参照用
mixUsersArray[2].rect.top    = 500; //参照用   
mixUsersArray[2].rect.right  = 180; //参照用
mixUsersArray[2].rect.bottom = 240; //参照用
mixUsersArray[2].roomId      = "97393"; //ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
config.mixUsersArray = mixUsersArray;

// クラウドミクスストリーミングを開始します
trtc->setMixTranscodingConfig(&config);
:::
::: C# C#
TRTCTranscodingConfig config = new TRTCTranscodingConfig();
// 解像度は1280 × 720、ビットレートは1500kbps、フレームレートは20fpsに設定します
config.videoWidth      = 1280;
config.videoHeight     = 720;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
config.mode = RTCTranscodingConfigMode.TRTCTranscodingConfigMode_Template_PresetLayout;
TRTCMixUser[] mixUsersArray = new TRTCMixUser[3];

// キャスターカメラの画面位置
TRTCMixUser local = new TRTCMixUser();
local.userId = "$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0; // zOrderを0とすることは、キャスター画面を最下層に位置付けることを意味します
local.roomId = null; // ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
RECT rtLocal = new RECT() {
    left   = 0, 
    top    = 0,
    right  = videoWidth,
    bottom = videoHeight
};
local.rect = rtLocal;
mixUsersArray[0] = local;

// マイク接続者の画面位置
TRTCMixUser remote1 = new TRTCMixUser();
remote1.userId = "$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.roomId = “97392”; // ローカルユーザーはroomIDを入力する必要はありません。リモートでは必要です
RECT rtRemote1 = new RECT() { //参照用
    left   = 420,
    top    = 81,
    right  = 240 + left,
    bottom = 240 + top
};
remote1.rect = rtRemote1;
mixUsersArray[1] = remote1;

// マイク接続者の画面位置
TRTCMixUser remote2 = new TRTCMixUser();
remote2.userId = "$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote2.roomId = “97393”; // ローカルユーザーはroomIDを入力する必要はありません。リモートでは必要です
RECT rtRemote2 = new RECT() { //参照用
    left   = 660,
    top    = 400,
    right  = 240 + left,
    bottom = 240 + top
};
rtRemote2.rect   = rtRemote2;
mixUsersArray[2] = remote2;

// クラウドミクスストリーミングを開始します
config.mixUsersArray = mixUsersArray;
trtc.setMixTranscodingConfig(config);
:::
::: Flutter java
TRTCCloud trtcCloud = await TRTCCloud.sharedInstance();
trtcCloud.setMixTranscodingConfig(TRTCTranscodingConfig(
  appId: 1252463788, //参照用
  bizId: 3891, //参照用
  // 解像度は720 × 1280、ビットレートは1500kbps、フレームレートは20FPSに設定します
  videoWidth: 720,
  videoHeight: 1280,
  videoBitrate: 1500,
  videoFramerate: 20,
  videoGOP: 2,
  audioSampleRate: 48000,
  audioBitrate: 64,
  audioChannels: 2,

  // プリセットレイアウトモードを採用します
  mode: TRTCCloudDef.TRTC_TranscodingConfigMode_Template_PresetLayout,

  mixUsers: [
  // キャスターカメラの画面位置
    TRTCMixUser(
      userId: "$PLACE_HOLDER_LOCAL_MAIN$",
      roomId: null, // ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
      zOrder: 0, // zOrder を0とすることは、キャスター画面を最下層に位置付けることを意味します
      x: 0, //参照用
      y: 0,
      streamType: 0,
      width: 300,
      height: 400),
    TRTCMixUser(
      userId: '$PLACE_HOLDER_REMOTE$',
      roomId: '256', // ローカルユーザーはroomIDを入力する必要はありませんが、リモートでは必要です
      zOrder: 1,
      x: 100, //参照用
      y: 100,
      streamType: 0,
      width: 160,
      height: 200)
  ],
));
:::
::: Web JavaScript
try {
  // プリセットレイアウトモード
  const config = {
   mode: 'preset-layout',
   videoWidth: 720,
   videoHeight: 1280,
   videoBitrate: 1500,
   videoFramerate: 20,
   videoGOP: 2,
   audioSampleRate: 48000,
   audioBitrate: 64,
   audioChannels: 2,
   // 1チャネルのローカルカメラ、2チャネルのリモートストリーミングのレイアウト位置をプリセットします
   mixUsers: [
      {
        width: 720,
        height: 1280,
        locationX: 0,
        locationY: 0,
        pureAudio: false,
        userId: 'jack', // ローカルカメラプレースホルダー、入力プッシュカメラのclient userId
        zOrder: 1
      },
      {
        width: 180,
        height: 240,
        locationX: 400,
        locationY: 800,
        pureAudio: false,
        userId: '$PLACE_HOLDER_REMOTE$', // リモートストリーミングプレースホルダー
        zOrder: 2
      },
      {
        width: 180,
        height: 240,
        locationX: 400,
        locationY: 500,
        pureAudio: false,
        userId: '$PLACE_HOLDER_REMOTE$', // リモートストリーミングプレースホルダー
        zOrder: 2
      }
    ];
  }
  await client.startMixTranscode(config);
} catch (error) {
  console.error('startMixTranscode failed ', error);
}
:::
</dx-codeblock>  

>! 
>- プリセットレイアウトモードでは、`setMixTranscodingConfig()`インターフェースは何度も呼び出す必要はありません。入室に成功しローカルオーディオのアップストリームを起動してから1度呼び出せばOKです。
>- Web端末インターフェースの命名は他の端末と少々異なります。詳細については、[Client.startMixTranscode()](https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/web/docs/Client.html#startMixTranscode)をご参照ください。

[](id:ScreenSharing)
### 画面共有モード（ScreenSharing）
#### 適用ケース
画面共有モードは、eラーニングおよびインタラクティブな授業などのケースに使用します。このケースではSDKの[enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)インターフェースを呼び出すとき、AppSceneパラメータを`TRTCAppSceneLIVE`に設定できます。
画面共有モードでは、SDKはまず選定したターゲット解像度に従って一枚のキャンバスを作成します。講師が画面共有していないとき、SDKはカメラ画像をキャンバスと同じ比率で拡大します。講師が画面共有を起動すると、SDKは画面共有した画面を同じキャンバスに描出します。キャンバスを作成することで、ミクスストリーミングモジュールの出力解像度の一致を確保でき、録画およびウェブサイト視聴時のビデオ互換性に関する問題を防止（一般的な再生プレーヤーは解像度が変化するビデオをサポートしません）することができます。

#### 使用手順
1. `enterRoom()`関数を呼び出して入室するときは、業務のニーズに応じてAppSceneパラメータを`TRTCAppSceneLIVE`に設定します。
2. [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動し、TRTCParamsの`streamId`パラメータを設定し、MCU出力のミキシングオーディオ・ビデオストリーミングの行先を指定します。
3. `startLocalPreview()`および`startLocalAudio()`を呼び出して、ローカルのオーディオ・ビデオのアップストリームを起動します。
>? クラウドミクスストリーミングは、本質的に、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオ・ビデオストリーミング上でマルチチャネルストリームをミクスストリーミングすることですから、現在のユーザーは自身でオーディオ・ビデオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4. `setMixTranscodingConfig()`インターフェースを呼び出してクラウドミクスストリーミングを起動し、呼び出しが必要なときは`TRTCTranscodingConfig`の`mode`パラメータを**TRTCTranscodingConfigMode_Template_ScreenSharing**に設定し、`audioSampleRate`、`audioBitrate`および`audioChannels`などのオーディオ出力品質に関するパラメータ、並びに`videoWidth`、`videoHeight`、`videoBitrate`、`videoFramerate`などのビデオ出力品質に関するパラメータを指定します。
>? `videoWidth`および`videoHeight`パラメータを0に指定する場合は、SDKはユーザーの現在のスクリーンのアスペクト比に従って、適切な解像度を自動的に計算します。
5. 上記手順を経て、現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後は、ドキュメント[CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を参照して再生ドメイン名を設定し、ライブストリーミングで視聴できます。また、ドキュメント[クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426)を参照してミキシング後のオーディオストリーミングを録音することもできます。

>! 
>- 画面共有モードは、WindowsおよびMacのプラットフォームのみをサポートします。
> 画面共有モードでは、`setMixTranscodingConfig()`インターフェースは何度も呼び出す必要はありません。入室に成功しローカルオーディオのアップストリームを起動してから1度呼び出せばOKです。
>- 教育モードでのビデオコンテンツは画面共有がメインであるため、カメラ画像および画面共有画像の同時伝送は非常に帯域幅を消費します。そこで、カメラ画像および受講生の画像を`setLocalVideoRenderCallback()` および`setRemoteVideoRenderCallback()`インターフェースを介して、現在のスクリーン上に直接描出することをお勧めします。
>- TRTCTranscodingConfigの`videoWidth`および`videoHeight`パラメータをすべて0に指定することによって、SDKでインテリジェントに出力解像度を選択することができます。講師の現在のスクリーン幅が1920pxより小さい場合、SDKは講師の現在の画面の実際の解像度を使用します。講師の現在の画面幅が1920pxより大きい場合、SDKは現在のスクリーンのアスペクト比に従って1920 × 1080（16:9）、1920 × 1200（16:10）または1920 × 1440（4:3）の中から選択します。

[](id:Manual)

### 全手動モード（Manual）
#### 適用ケース
全手動モードは、上述の自動モードがすべて適用できないケースに適合します。全手動は最もフレキシブルで、各種のミクスストリーミング方法を自由に組み合わせることができます。しかし、使い勝手は最も劣ります。
全手動モードでは、`TRTCTranscodingConfig`のすべてのパラメータを設定し、TRTCCloudDelegateの`onUserVideoAvailable()`および`onUserAudioAvailable()`コールバックをモニタする必要があり、これによって現在のルームでの各マイク・オンしているユーザーのオーディオ・ビデオ状態に従って`mixUsers`パラメータを絶えず調整します。この設定がないとミクスストリーミングは失敗してしまいます。

#### 使用手順
1. `enterRoom()` 関数を呼び出して入室するときは、業務のニーズに応じてAppSceneパラメータを設定します。
2. [Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)を起動し、TRTCParamsの`streamId`パラメータを設定し、MCU出力のミキシングオーディオ・ビデオストリーミングの行先を指定します。
3. 業務のニーズに応じて、 `startLocalAudio()` を呼び出してローカルオーディオのアップストリームを起動します（または `startLocalPreview()` を同時に呼び出してビデオのアップストリームを起動します）。
>? クラウドミクスストリーミングは、本質的に、現在（すなわち、ミクスストリーミングコマンドを発出する）ユーザーが対応しているオーディオ・ビデオストリーミング上でマルチチャネルストリームをミクスストリーミングすることですから、現在のユーザーは自身でオーディオ・ビデオのアップストリームを有していなければ、ミクスストリーミングの前提条件を構成できません。
4. `setMixTranscodingConfig()`インターフェースを呼び出してクラウドミクスストリーミングを起動します。呼び出す必要があるときは、`TRTCTranscodingConfig`の`mode`パラメータを**TRTCTranscodingConfigMode_Manual**に設定し、`audioSampleRate`、`audioBitrate`および`audioChannels`などのオーディオ出力品質に関するパラメータを指定します。業務シーンにもビデオがある場合は、`videoWidth`、`videoHeight`、`videoBitrate`、`videoFramerate`などのビデオ出力品質に関するパラメータを同時に設定する必要があります。
5. TRTCCloudDelegateの`onUserVideoAvailable()`および`onUserAudioAvailable()`コールバックをモニタし、ニーズによって**mixUsers**パラメータを指定します。
 >?プリセットレイアウト（PresetLayout）モードとは異なり、Manualでは各`mixUser`の`userId`パラメータを実際のマイク接続者IDに指定する必要があり、このマイク接続者がビデオを起動しているかどうかで`mixUser`の`pureAudio`パラメータもそのとおりに設定する必要があります。
6. 上記手順を経て、現在のユーザーのリレーオーディオストリームは、ルームのその他のユーザーのオーディオを自動的にミキシングします。その後は、ドキュメント[CDN Relayed live Streaming](https://intl.cloud.tencent.com/document/product/647/35242)を参照して再生ドメイン名を設定し、ライブストリーミングで視聴できます。また、ドキュメント[クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426)を参照してミキシング後のオーディオストリーミングを録音することもできます。
>! 全手動モードでは、ルームのマイク接続者のマイク・オン、マイク・オフ動作をリアルタイムでモニタし、マイク接続者の人数やオーディオ・ビデオ状態に従って、`setMixTranscodingConfig()`インターフェースを何度も呼び出す必要があります。

## 関連料金

### 料金の計算

Cloud MixTranscodingでは、MCUクラスターに入力されたオーディオ・ビデオストリーミングをデコードし、出力を再エンコードする必要があり、このため追加のサービス料金が発生します。TRTCは、MCUクラスターを使用してCloud MixTranscodingを行ったユーザーに対し、追加の付加価値料金を請求します。Cloud MixTranscoding料金は、**トランスコーディング出力解像度サイズ**と**トランスコーディング期間**に応じて請求されます。トランスコーディングの出力解像度が高く、トランスコーディングの出力時間が長いほど、料金は高くなります。詳細については、[Cloud MixTranscoding課金説明](https://intl.cloud.tencent.com/document/product/647/38929)をご参照ください。

### 料金の節約

- **サーバーREST APIベースのミクスストリーミングスキームで、ミクスストリーミングを停止する場合**、次のいずれかの条件を満たす必要があります。
  - ルームのすべてのユーザー（キャスターと視聴者を含む）が全員退室している。
  - REST API[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)を呼び出して、ミクスストリーミングを自主的に停止します。
- **クライアントのSDK APIベースのミクスストリーミングスキームで、ミクスストリーミングを停止する場合**、次のいずれかの条件を満たす必要があります。
  - ミクスストリーミングを開始した（クライアントAPI `setMixTranscodingConfig`を呼び出した）キャスターが退室している。
  - [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)を呼び出して、パラメータを`nil/null`に設定し、ミクスストリーミングを自主的に停止する。

その他の場合、TRTC Cloudは、ミクスストリーミングの状態を継続して維持するために最善を尽くします。従って、予期せぬミクスストリーミング料金が発生しないよう、ミクスストリーミングが不要な場合は、上記の方法でクラウドミクスストリーミングを可能な限り速やかに終了してください。



