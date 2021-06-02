## 適用ケース
リモート教育、ステージライブストリーミング、ビデオミーティング、リモートでの確定損失、金融における録音や録画、オンライン医療などのユースケースでは、証明取得、品質検査、審査、保存、再生などのニーズを考慮して、すべてのビデオミーティングやILVBプロセスをレコーディングまたは保存する必要がよくあります。

TRTCのクラウドレコーディングは、ルームの各ユーザーのオーディオ・ビデオストリーミングを独立した一つのファイルにレコーディングします。
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

ルーム内の複数チャネルのオーディオ・ビデオに先に[クラウドミクスストリーミング](https://intl.cloud.tencent.com/document/product/647/34618)を行い、ミックス後のオーディオ・ビデオストリーミングを1つのファイルにレコーディングします。
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## コンソールガイド
<span id="open"></span>
### レコーディングサービスのアクティブ化
1. TRTCコンソールにログインして、左側のナビゲーションバーから【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. 目標アプリケーションが所在する行の【機能設定】をクリックして、機能設定ページカードに入ります。アプリケーションを作成したことがない場合は、【アプリケーションの作成】をクリックしてアプリケーション名を記入し、【OK】をクリックして新しいアプリケーションを作成します。
3. 【クラウドレコーディングの起動】右側の<img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png">をクリックすると、クラウドレコーディングの設定ページがポップアップで表示されます。


<span id="recordType"></span>

### レコーディング形式の選択

TRTCのクラウドレコーディングサービスは、「Global Auto-Recording」および「指定ユーザーレコーディング」の2種類の異なるレコーディング形式を提供しています。
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **Global Auto-Recording**
  各TRTCルームの各ユーザーのアップストリームのオーディオとビデオは自動的にレコーディングされます。レコーディングタスクの開始と停止は自動的に行われるため、心配する必要はありません。操作は比較的シンプルで使いやすいです。特定の使用法については、[方法1：Global Auto-Recording](#autoRecord)をご参照ください。

- **指定ユーザーレコーディング**
  一部のユーザーのオーディオ・ビデオストリーミングのレコーディングしか指定できません。このことは、クライアントのSDK APIまたはサーバーのREST APIを通じて制御するため、追加の開発作業が必要になります。具体的な使用方法は、 [方法2：指定ユーザーレコーディング（SDK API）](#recordSDKAPI) および [方法3：指定ユーザーレコーディング（REST API）](#recordRESTAPI)をご参照ください。


<span id="fileFormat"></span>

###  ファイルのフォーマットの選択

クラウドレコーディングでは、 HLS、MP4、FLV 、AACの4種類の異なるファイルフォーマットをサポートしています。形式と適用条件が異なる4種類のフォーマットを、自身の業務のニーズに合わせて選択することができます。

<table>
<tr><th>パラメータ</th><th>パラメータの説明</th></tr>
<tr>
<td>ファイルタイプ</td>
<td>以下のファイル形式をサポートします。<ul style="margin:0"><li><b>HLS</b>：このファイル形式は、大多数のブラウザのオンライン再生をサポートし、ビデオの再生シーンに適合します。このファイル形式を選択したときは、ブレークポイントでの継続レコーディングをサポートし、個別のファイル最大時間は制限されません。</li><li><b>FLV</b>：このファイル形式は、ブラウザのオンライン再生をサポートしませんが、簡単でフォールトトレランス性が優れています。レコーディングしたファイルをVODプラットフォームに保存する必要がない場合は、このファイル形式を選択することができます。レコーディングの完了後、すぐにダウンロードしてファイルをレコーディングして、元のファイルを削除できます。</li><li><b>MP4</b>：このファイル形式はWebブラウザのオンライン再生をサポートしますが、フォールトトレランスは劣ります。ビデオ通話のプロセスでは、どのパケットロスでも、レコーディングファイルの再生画質に影響します。</li><li><b>AAC</b>：音声レコーディングだけ必要な場合は、このファイル形式を選択できます。</li></td>
</tr>
<tr>
<td nowrap="nowrap">単一ファイルの最長時間（分）</td>
<td><ul style="margin:0"><li/>実際の業務ニーズに応じて1ビデオファイルの最大時間制限を設定できます。時間制限を超過すると、システムはビデオファイルを自動的に分単位で分割します。数値範囲は5～120。<li/>この【ファイルタイプ】を【HLS】に設定するとき、1ファイルの最大時間を制限しなければ、そのパラメータは無効になります。</td>
</tr>
<tr>
<td>ファイルの保存期間（日）</td>
<td>実際の業務ニーズに応じて、ビデオファイルをVODプラットフォームの日数の間保存します。日数単位で数値範囲は0～1080。期限後は、ファイルはVODプラットフォームによって自動的に削除され、回復できなくなります。 0は永久保存を表します。</td>
</tr>
<tr>
<td>連続レコーディングタイムアウト時間（秒）</td>
<td><li/>【ファイルタイプ】を【HLS】に設定したときのみ、このパラメータは有効になります。<li/>デフォルトでは、通話（またはライブストリーミング）プロセスが、ネットワークの不安定またはその他の原因によって遮断された場合は、ファイルのレコーディングは複数のファイルに切断されます。「一回通話（またはライブストリーミング）では1回しか再生接続ができない」を実現したい場合は、実情に応じて再開超過時間を設定し、遮断間隔が設定されたレコーディング再開超過時間を下回る場合は、一回通話（またはライブストリーミング）は1ファイルしか生成しません。秒単位。数値範囲は1～1800。0は、ブレークポイント後は、継続レコーディングしないことを表します。</td>
</tr>
</table>


>? HLSは最長で30分間の継続レコーディングをサポートし、「1講義に1個のみの再生接続」が可能で、大多数のブラウザのオンライン視聴をサポートしており、eラーニングにおけるビデオ再生のユースケースにとても適しています。

<span id="storageLocation"></span>

###  保存場所の選択

TRTCクラウドレコーディングファイルは、デフォルトではTencent Cloud VODサーバーに保存されます。プロジェクトで多くの業務が一つのTencent Cloud VODアカウントを共有している場合は、レコーディングファイルを隔離させる必要があるかもしれません。Tencent Cloud VODの「サブアプリ」機能によって、TRTCのレコーディングファイルをその他の業務エリアと切り離すことができます。

- **VODのメインアプリとサブアプリとは。**
  メインアプリとサブアプリとは、VODの一種のリソース分割方式です。メインアプリはVODのメインアカウントに相当し、サブアプリは複数作成できます。各サブアプリは、ルートアカウント下の1個のサブアカウントに相当し、独立したリソース管理を有しています。保存エリアではその他のサブアプリと相互に切り離されることがあります。

- **VODサービスのサブアプリケーションを有効にする方法とは。**
  ドキュメント [「VODのサブアプリケーションを有効にする方法」](https://intl.cloud.tencent.com/document/product/266/33987) をもとに新しいサブアプリケーションを追加できます。この手順では、VODの[コンソール](https://console.cloud.tencent.com/vod)にジャンプして操作する必要があります。

<span id="recordCallback"></span>

###  レコーディングコールバックの設定

新しいファイルの [保存通知](#callback)をリアルタイムで受信する必要がある場合は、サーバーがレコーディングファイルのコールバックを受け取るアドレスを入力できます。このアドレスは、 HTTP（または HTTPS）プロトコルに適合する必要があります。新しいレコーディングファイルが生成されたら、Tencent Cloudはこのアドレスを介して、サーバーに通知を発信します。

![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

詳細なレコーディングコールバックの受信及び解釈方法は、ドキュメント後半部分の：[レコーディングファイルの受け取り](#callback)をご参照ください。

<span id="startAndStop"></span>

## レコーディングの制御方法

TRTC では、3種類のクラウドレコーディング制御方式を提供し、それぞれ、[Global Auto-Recording](#autoRecord)、[指定ユーザーレコーディング（SDK APIによる制御）](#recordSDKAPI)、 [指定ユーザーレコーディング（REST APIによる制御）](#recordRESTAPI)となっています。この中の各方式について、詳しく紹介します。

- コンソールでこの方式の使用設定をする方法とは。
- レコーディングタスクを開始する方法とは。
- レコーディングタスクを終了する方法とは。
- ルームのマルチチャネル画面を1チャネルにミックスする方法とは。
- レコーディングしたファイルをどのように命名しますか。
- この方法をサポートするプラットフォームには何がありますか。


<span id="autoRecord"></span>

### 方法1：Global Auto-Recording

- **コンソールでの設定**
  このレコーディング方法を使用したい場合は、コンソールの [レコーディング形式の選択](#recordType)のとき、「Global Auto-Recording」に設定してください。

- **レコーディングタスクの開始**
  TRTCルームの各ユーザーのオーディオ・ビデオストリーミングは、すべてファイルに自動レコーディングされるので、追加の操作は必要ありません。

- **レコーディングタスクの終了**
  自動停止。各キャスターが音声ビデオのアップストリームを停止すると、このキャスターのクラウドレコーディングは自動的に停止します。 [ファイルフォーマットの選択](#fileFormat) のとき、“再開超過時間”を設定すると、再開超過時間時間を超過しないと、レコーディングファイルを受け取れなくなります。

- **マルチ画面のミックス**
  Global Auto-Recordingモードでは、クラウドミクスストリーミングに2つの方法があります。すなわち、「サーバーREST API」 および 「クライアントSDK API」です。2つの方法は混合して使用しないでください。
  - [サーバーREST APIミクスストリーミング方式](#recordRESTAPI)：お客様のサーバーからAPI呼び出しを起動する必要があります。クライアントのプラットフォームバージョンの制限は受けません。
  - [クライアントSDK APIミクスストリーミング方式](#recordSDKAPI)：直接クライアントからミクスストリーミングを発動できます。現在サポートしているのは、iOS、Android、Windows、Mac、Electronなどのプラットフォームとなり、Webブラウザは現在サポートしていません。

- **レコーディングファイルの命名**
  - キャスターが入室時に [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータを指定した場合、レコーディングファイルは `userDefineRecordId_streamType_開始時刻_終了時刻` で命名されます（streamTypeにはmainおよびauxの2つの値があり、mainはメインパスを、auxはサブパスを表します。サブパスは通常、画面共有に利用されます）。
  - キャスターが入室時に [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータを指定していなかったが、 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) パラメータを指定していた場合は、レコーディングファイルは`streamId_開始時刻_終了時刻` で命名されます。
  - キャスターが入室時に [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータ、 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) パラメータをいずれも指定していない場合は、レコーディングファイルは `sdkappid_roomid_userid_streamType_開始時刻_終了時刻` で命名されます（streamTypeにはmainおよびauxの2つの値があり、mainはメインパスを、auxはサブパスを表します。サブパスは通常、画面共有に利用されます）。

- **サポート済みのプラットフォーム**
  お客様側のサーバーで制御し、クライアント側プラットフォームの制限は受けません。

<span id="recordSDKAPI"></span>

### 方法2：ユーザーレコーディングの指定（SDK API）

TRTC SDKが提供するいくつかの API インターフェースとパラメータを呼び出すことで、クラウドミクスストリーミング、クラウドレコーディング、Relayed live streamingの3つの機能を実装可能です。

| クラウド機能 | 開始方法とは。                                                   | 停止方法とは。                                                   |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| クラウドレコーディング | 入室時にパラメータ `TRTCParams` の中の `userDefineRecordId` フィールドを指定します   | キャスター退室時に自動停止します                                           |
| クラウドミクスストリーミング| SDK API  [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) を呼び出してクラウドミクスストリーミングを起動 | クラウドミクスを発出したキャスターが退室したら、ミクスストリーミングは自動的に停止するか、途中で [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) を呼び出してパラメータを `null/nil` 手動停止に設定します |
| Relayed live streaming | 入室時にパラメータ `TRTCParams`の中の `streamId` フィールドを指定します             | キャスター退室時に自動停止します                                           |
![](https://main.qcloudimg.com/raw/7daf8430ca74adeec019c10fc384a48e.gif)

- **コンソールでの設定**
  このレコーディング方法を使用したい場合は、コンソールの [レコーディング形式の選択](#recordType)のときに、「指定ユーザーレコーディング」に設定してください。

- **レコーディングタスクの開始**
  キャスターが入室時に入室パラメータ [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) の [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) フィールドを指定すると、その後、同キャスターのアップストリームのオーディオ・ビデオデータがクラウドレコーディングされます。このパラメータを指定していないキャスターはレコーディングタスクを起動することはありません。
```
// サンプルコード：レコーディングユーザーrexchangのオーディオ・ビデオストリーミングを指定し、ファイルid を 1001_rexchangにします
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTCのSDKAppID。アプリケーション作成後、取得可
param.roomId   = 1001;           // ルームナンバー
param.userId   = @"rexchang";    // ユーザー名
param.userSig  = @"xxxxxxxx";    // 署名ログイン
param.role     = TRTCRoleAnchor; // ロール：キャスター
param.userDefineRecordId = @"1001_rexchang";  // レコーディングID。そのユーザーのレコーディング開始を指定します。
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; //  LIVE モードを使用してください
```

- **レコーディングタスクの終了**
  自動停止。入室時に [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)パラメータのキャスターを指定して音声ビデオのアップストリームを停止した後、クラウドレコーディングは自ら停止します。[ファイルフォーマットの選択](#fileFormat)のときに「継続レコーディング時間」を設定すると、継続レコーディング時間が超過するまでレコーディングファイルを受け取ることができなくなります。

- **マルチ画面のミックス**
  SDK API  [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)をコールすることによって、ルーム内のその他のユーザーの画面および音声を現在のユーザーの一チャネルの音声ビデオストリーミング上にMixできます。この部分の詳細は、ドキュメント：[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88)で閲覧することができます。
>! 1つのTRTCルーム内では、1人のキャスター（配信を開始したキャスターを推奨）のみが `setMixTranscodingConfig`を呼び出しすればよく、複数のキャスターが呼び出すと、状況が混乱し、エラーが起きる可能性があります。

- **レコーディングファイルの命名**
  レコーディングファイルは、 `userDefineRecordId_開始時間_終了時間` のフォーマットで命名されます。

- **サポート済みのプラットフォーム**
  [iOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Android](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520)、[Windows](http://doc.qcloudtrtc.com/group__TRTCTypeDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc)、[Mac](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Electron](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html) などの端末をサポートして、レコーディング制御を起動します。

<span id="recordRESTAPI"></span>

### 方法3：指定ユーザーレコーディング（REST  API）

TRTC のサーバーは1対のREST API（ [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) および[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)）を提供して、クラウドミクスストリーミング、クラウドレコーディング、Relayed live streamingの3つの機能を実装するのに使用します。

| クラウド機能 | 開始方法とは。  | 停止方法とは。 |
| :------- | :------- | :------- |
| クラウドレコーディング |   [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 呼び出し時に `OutputParams.RecordId` パラメータを指定すればすぐにレコーディングを開始 | 自動停止、または途中で [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) を呼び出して停止 |
| クラウドミクスストリーミング |   [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 呼び出し時に `LayoutParams` パラメータを指定すれば、レイアウトテンプレートおよびレイアウトユーザーを設定できます | すべてのユーザーが退室後に自動停止、または途中で [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) を呼び出して手動で停止できます |
| Relayed live streaming |   [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 呼び出し時に `OutputParams.StreamId` パラメータを指定すればCDNのRelayed live streamingを起動できます | 自動停止、または途中で [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) を呼び出して停止できます |

>? これらのREST APIに対する制御は、TRTCクラウドサービスの中のコアのミクスストリーミングモジュール（MCU）となり、MCU ミクスストリーミング後の結果はレコーディングシステムとライブCDNに送信されるため、APIの名前を `Start/StopMCUMixTranscode`としています。このため、機能の点からいうと、`Start/StopMCUMixTranscode` はミクスストリーミングの機能を実装できるだけでなく、クラウドレコーディングとRelayed live streaming CDNの機能も実装できます。

![](https://main.qcloudimg.com/raw/65ef546c0e424af77f7d20f23aa1d363.gif)

- **コンソールでの設定**
  このレコーディング方法を使用したい場合は、コンソールの [レコーディング形式の選択](#recordType)のときに、「指定ユーザーレコーディング」に設定してください。

- **レコーディングタスクの開始**
  サーバーから [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) を呼び出して、 `OutputParams.RecordId` パラメータを指定すると、ミクスストリーミングおよびレコーディングが実行できます。
```
// コードサンプル： REST APIによってクラウドミクスストリーミングおよびクラウドレコーディングのタスクを起動します
https://trtc.tencentcloudapi.com/?Action=StartMCUMixTranscode
&SdkAppId=1400000123
&RoomId=1001
&OutputParams.RecordId=1400000123_room1001
&OutputParams.RecordAudioOnly=0
&EncodeParams.VideoWidth=1280
&EncodeParams.VideoHeight=720
&EncodeParams.VideoBitrate=1560
&EncodeParams.VideoFramerate=15
&EncodeParams.VideoGop=3
&EncodeParams.BackgroundColor=0
&EncodeParams.AudioSampleRate=48000
&EncodeParams.AudioBitrate=64
&EncodeParams.AudioChannels=2
&LayoutParams.Template=1
&<パブリックリクエストパラメータ>
```

>! 
>- このREST APIは、ルーム内の少なくとも1人のユーザーが入室（enterRoom）に成功した場合に有効になります。
>- REST APIを使用すると、シングルストリームのレコーディングはサポートされません。シングルストリームをレコーディングしたい場合は、 [方法1](#autoRecord) または [方法2](#recordSDKAPI)を選択してください。

- **レコーディングタスクの終了**
  自動停止では、途中で [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) を呼び出して、ミクスストリーミングおよびレコーディングのタスクを停止することもできます。

- **マルチ画面のミックス**
  [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)を呼び出す時に、同時に `LayoutParams` パラメータを指定すれば、クラウドミクスストリーミングを実装できます。このAPIは、 ライブストリーミング全時間内での複数回呼び出しをサポートしていますので、必要に応じて `LayoutParams` パラメータを修正し、このAPIを再度呼び出して合成画面のレイアウトを調整することができます。ただし、注意が必要なのは、パラメータ `OutputParams.RecordId` と `OutputParams.StreamId`が複数回呼び出しの中で一致性を維持する必要があることです。そうしない場合、ストリームが切断され、複数のレコーディングファイルが生成されてしまいます。

>?クラウドミクスストリーミングの詳細については、 [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#restapi)をご参照ください。

- **レコーディングファイルの命名**
  レコーディングファイルは、 [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) を呼び出すときに指定した `OutputParams.RecordId` パラメータで命名します。命名フォーマットは、 `OutputParams.RecordId_開始時間_終了時間`です。

- **サポート済みのプラットフォーム**
  お客様側のサーバーで制御し、クライアント側プラットフォームの制限は受けません。

<span id="search"></span>
## レコーディングファイルの検索

レコーディング機能を起動させた後、TRTCシステムからレコーディングしたファイルは、Tencent CloudのVODサーバーから探し出せます。VODコンソールから手動で直接探し出したり、バックエンドサーバーからREST APIを使用して定刻にスクリーニングを行うこともできます。

#### 方法1：VODコンソールで手動で検索
1. [VODコンソール](https://console.cloud.tencent.com/vod/)にログインして、左側のナビゲーションバーから【メディア資産管理】を選択します。
2. リスト上方の【プレフィックス検索】をクリックして、【プレフィックス検索】を選択します。検索ボックスに、例えば`1400000123_1001_rexchang_main`といったキーワードを入力して<img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">をクリックすると、ビデオ名がプレフィックスと符合するビデオファイルを表示します。
3．作成時間に基づき、必要な目標ファイルをスクリーニングすることができます。

#### 方法2：VOD REST APIによる検索
Tencent CloudのVODシステムは、一連のREST APIを提供してその上の音声ビデオファイルを管理します。 [メディア情報検索](https://intl.cloud.tencent.com/document/product/266/34179) のこのREST APIによって、VODシステム上のファイルを検索します。パラメータ表の `Text` パラメータをリクエストすることで、曖昧マッチングや、 `StreamId` パラメータを基に正確な検索を行うこともできます。
RESTリクエスト例：
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<パブリックリクエストパラメータ>
```

<span id="callback"></span>

## レコーディングファイルの受け取り

[レコーディングファイルの検索](#search)のほかにも、コールバックアドレスを設定することによって、Tencent Cloudに新たにレコーディングしたファイル情報をサーバーに自動的に送信させることもできます。
ルームの最後の1チャネルの音声ビデオストリーミングが退出後、Tencent Cloudはレコーディングを終え、ファイルをVODプラットフォームに移転して保存します。このプロセスのおよそのデフォルトは、約30秒から2分間（継続レコーディング時間を300秒に設定した場合、待ち時間はデフォルトの基礎時間に300秒を加えた時間）。転送保存が完了後、Tencent Cloudは [レコーディングコールバック設定](#recordCallback) で設定したコールバックアドレス（HTTP/HTTPS）によってサーバーに通知を発信します。

Tencent Cloudは、レコーディングおよびレコーディング関連のイベントを、設定したコールバックアドレスを通じてサーバーに送信します。コールバック情報のサンプルは下図に示すとおりです。
![](https://main.qcloudimg.com/raw/483dba536acd022f93af3ca5ff6cd74a.png)
下表のフィールドによって、現在のコールバックがどの通話（またはライブストリーミング）に対応するかを確定することができます。

<table>
<tr>
<th>番号</th><th>フィールド名</th><th>説明</th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>情報形式。 event_typeが100のときは、このコールバック情報が、レコーディングファイルが生成した情報であることを表します。</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>入室時にパラメータ `TRTCParams`の中の <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a> フィールドを設定することで指定できます。</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>ユーザー名のBase64コード。</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>フィールドのカスタマイズは、TRTCParamsの中の<a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a>フィールドを設定することで指定できます。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>レコーディングファイルの視聴アドレスは、VOD再生</a>に使用<a href="#play">できます。</td>
</tr></table>



<span id="delete"></span>
## レコーディングファイルの削除

Tencent CloudのVODシステムは一連のREST APIを提供して、その上のオーディオ・ビデオファイルを管理します。 [メディアAPIの削除](https://intl.cloud.tencent.com/document/product/266/37571) によって指定したファイルを削除できます。
RESTリクエスト例：
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<パブリックリクエストパラメータ>
```

<span id="play"></span>
## レコーディングファイルの再生

eラーニングなどのユースケースでは、通常ライブストリーミングの終了後、何度もレコーディングファイルを再生し、教育リソースを十分に活用しやすくする必要があります。

#### ファイルフォーマットの選択（HLS）
[レコーディングフォーマットの設定](#fileFormat)では、ファイルフォーマットをHLSに選択します。
HLSは最長30分間のブレークポイントの継続レコーディングをサポートしており、「1つのライブストリーミング（または1回の授業）から1回だけの再生接続」が行えます。かつ、HLSファイルは、大多数のブラウザのオンライン再生をサポートしており、ビデオ再生のユースケースにとても適しています。

#### VODアドレス（video_url）の取得
[レコーディングファイルの受け取り](#callback) のときに、コールバック情報の **video_url** フィールドを取得できます。このフィールドは、現在のレコーディングファイルのTencent CloudにおけるVODアドレスになります。

#### VODプレーヤーとの接続
プラットフォームの使用に基づき、VODプレーヤーに接続します。具体的な操作は以下をご参照ください。
- [iOSプラットフォーム](http://doc.qcloudtrtc.com/group__TXVodPlayer__ios.html)
- [Androidプラットフォーム](http://doc.qcloudtrtc.com/group__TXVodPlayer__android.html)
- [Webブラウザ](https://intl.cloud.tencent.com/document/product/266/33977)

>! [プロフェッショナル版](https://intl.cloud.tencent.com/document/product/647/34615)のTRTC SDKの使用を推奨します。プロフェッショナル版は[モバイルライブストリーミング（MLVB）](https://intl.cloud.tencent.com/product/mlvb)などの機能を統合したものです。基盤となるモジュールの高度な再利用により、統合されたプロフェッショナル版のボリューム増分は、2つの独立したSDKを同時に統合する場合よりも小さくなり、さらにシンボルの衝突(symbol duplicate)の悩みを解消できます。


## 関連料金

クラウドレコーディングと再生の関連料金には次の項目が含まれています。このうち、レコーディング料金は基本料金となり、その他の料金はお客様の使用状況およびニーズ応じて徴収されます。

>?ここでの価格は例であり、参考にすぎません。料金が実際と一致しない場合は[クラウドレコーディング課金説明](https://intl.cloud.tencent.com/document/product/647/38385)、[LVB](https://buy.cloud.tencent.com/price/lvb) および [VOD](https://buy.cloud.tencent.com/price/vod)の定価を基準とします。

#### レコーディング料金：トランスコーディングまたはそのパッケージングに発生した料金の計算

レコーディングは、オーディオ・ビデオストリーミングのトランスコーディングまたはそのパッケージングが必要となるため、サーバーの計算リソースの消費が発生します。このため、レコーディング業務が計算リソースを占有するコストに応じて費用を徴収する必要があります。

>!
>- 2020年7月1日以降、初めてTRTC コンソールでアプリケーションを作成したTencent Cloudアカウントは、クラウドレコーディング機能の利用後に発生したレコーディング費用については、[クラウドレコーディング課金説明](https://intl.cloud.tencent.com/document/product/647/38385)を基準とします。
>- 2020年7月1日以前に TRTC コンソールでアプリケーションを作成したことのあるTencent Cloudアカウントは、2020年7月1日以前またはそれ以降に作成したアプリケーションであっても、クラウドレコーディング機能を使用して発生するレコーディング料金については、デフォルトで、**LVBレコーディング**の課金ルールを引き続き採用します。

**LVBレコーディング**課金の計算方法は、同時レコーディングのチャネル数に応じて課金し、同時実行数が多くなるほど、レコーディング費用も高くなります。課金説明の詳細は [LVB > LVBレコーディング](https://intl.cloud.tencent.com/document/product/267/39605)をご参照ください。

>例えば、現在1000名のキャスターがいて、夕方のピーク時に、最多500チャンネルのキャスターのオーディオ・ビデオストリーミングを同時レコーディングする必要があるとします。仮にレコーディング単価が5.2941米ドル/チャンネル/月とすると、総レコーディング料金は、`500チャンネル × 5.2941米ドル/チャンネル/月 = 2647.05米ドル/月`となります。
>[レコーディングフォーマットの設定](#fileFormat)をする時に同時に2種類のレコーディングファイルを選択した場合、レコーディング料金と保存料金はいずれも × 2になります。同様の理屈により、3種類のファイルを選択した時のレコーディング料金と保存料金は × 3になります。不要な場合は、必要な1種類のファイルフォーマットのみを選択することを推奨します。コストを大幅に抑えることができます。

**保存料金：ファイルをTencent Cloudに保存するとこの料金が発生します**
レコーディングしたファイルをTencent Cloudに保存する場合は、保存自体にディスクリソースの消費が発生しますので、保存するリソースの占用状況に応じて料金を徴収する必要があります。保存期間が長いほど料金も高くなるため、特殊なニーズがない場合は、ファイルの保存期間を短めに設定して、費用を節約するか、またはファイルを自分のサーバーに保存することもできます。保存料金は、 [ビデオ保存（日次決済）価格](https://intl.cloud.tencent.com/document/product/266/14666)選択し、日次決算で計算することができます。

>例えば、 [setVideoEncodrParam()](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html) を介してキャスターのビットレート（videoBitrate）を1000kbpsに設定し、そのキャスターのライブストリーミングビデオ（1種類のファイルフォーマットを選択）をレコーディングし、1時間レコーディングすると、おおよそ `(1000 / 8)KBps × 3600秒 = 450000KB = 0.45GB` サイズのビデオファイルが生成されます。このファイルに毎日発生するおおよその保存料金は、`0.45GB × 0.0009 米ドル/GB/日 = 0.000405米ドル`となります。

#### 視聴料金：ファイルをVOD視聴に利用するとこの料金が発生します

レコーディングしたファイルをオンデマンド視聴に利用する場合は、視聴自体にCDNトラフィックが消費されるため、VODの価格にもとづき課金する必要があります。デフォルトは、トラフィックによる課金となっています。視聴者数が多いほど料金は高くなります。視聴料金は [ビデオアクセラレーション（日次決済）価格](https://intl.cloud.tencent.com/document/product/266/14666) を選択し、日次決算で計算できます。

>例えば、クラウドレコーディングによって1GBのファイルが生成され、1000名の視聴者が最初から最後まで完全にそのビデオを視聴すると、約1TBのVOD視聴トラフィックが発生します。この場合は、階層価格表にもとづき、1000名の視聴で、`1000 × 1GB × 0.0794米ドル/GB = 79.4米ドル`の料金が発生します。
>Tencent Cloudからファイルをお客様のサーバーにダウンロードするように選択した場合も、非常に小さなVODトラフィックが消費され、お客様の月次請求書の中に反映されます。

#### トランスコード料金：ミクスストリーミングレコーディングを有効にすると、この料金が発生します。

ミクスストリーミングレコーディングを作動させた場合は、ミクスストリーミング自体はデコーディングとコーディングする必要があるため、追加ミクスストリーミングトランスコード料金が発生します。ミクスストリーミングトランスコーディングは、解像度の大きさおよびトランスコーディング時間によって計算され、キャスター用の解像度が高く、マイク接続時間（通常はマイク接続のシーンではMixTranscodingが必要です）が長いほど、料金は高くなります。費用計算の詳細は[LVBトランスコード](https://intl.cloud.tencent.com/document/product/267/39604)をご参照ください。

>例えば、 [setVideoEncodrParam()](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam) によってキャスターのビットレート（videoBitrate）を1500kbps、解像度を720Pに設定するとします。1人のキャスターが視聴者と1時間マイク接続した場合 、マイク接続時間は [クラウドミクスストリーミング](https://intl.cloud.tencent.com/document/product/647/34618)を開始します。そのときに発生するトランスコード料金は `0.0057 米ドル/分 × 60分間 = 0.342米ドル`になります。
>
