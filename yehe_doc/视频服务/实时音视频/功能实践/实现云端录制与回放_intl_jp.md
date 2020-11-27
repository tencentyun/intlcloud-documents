## 適用ケース
リモート教育、ステージライブストリーミング、ビデオミーティング、リモートでの確定損失、金融における録音録画、オンライン医療などのユースケースでは、証明取得、品質検査、審査、保存、再生などのニーズを考慮して、すべてのビデオミーティングやILVBプロセスをレコーディングまたは保存する必要がよくあります。

TRTCのクラウドレコーディングは、ルームの各ユーザーのオーディオ・ビデオストリーミングを独立した一つのファイルにレコーディングします。
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

ルーム内のマルチチャネルの音声ビデオをまず [クラウドミクスストリーミング](https://intl.cloud.tencent.com/document/product/647/34618)してから、MIX後のオーディオ・ビデオストリーミングを一つのファイルにレコーディングします。
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## コンソールガイド

<span ID = "open"></span>
### レコーディングサービスのアクティブ化
1. [Tencent Real-Time Communicationtコンソール]にログインして、左側のナビゲーションバーで【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. 目標アプリケーションが所在する行の【機能設定】をクリックして、機能設定ページカードに入ります。アプリケーションを作成したことがない場合は、【アプリケーション作成】をクリックしてアプリケーション名を記入し、【確定】をクリックして新しいアプリケーションを作成します。
3. 【クラウドレコーディングの起動】の右側の <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"  style="margin:0;"> をクリックすると、クラウドレコーディング設定ページ画面がポップアップされます。

<span id="recordType"></span>
### レコーディング形式の選択
TRTC のクラウドレコーディングサービスは、「Global Auto-Recording」および「指定ユーザーレコーディング」の2種類の異なるレコーディング形式を提供しています。
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **Global Auto Recording**
各TRTCルームの各ユーザーのアップストリームのオーディオとビデオは自動的にレコーディングされます。レコーディングタスクの開始と停止は自動的に行われるため、心配する必要はありません。操作は比較的シンプルで使いやすいです。特定の使用法については、[方法一：Global Auto-Recording](#autoRecord)をご覧ください。

- **指定ユーザーレコーディング**
一部のユーザーのオーディオ・ビデオストリーミングのレコーディングしか指定できません。このことは、クライアントのSDK API またはサーバーの REST API を通じて制御するため、追加の開発作業が必要になります。具体的な使用方法は、 [方法二：指定ユーザーレコーディング（SDK API）](#recordSDKAPI) および [方法三：指定ユーザーレコーディング（REST API）](#recordRESTAPI)をご覧ください。

<span id="fileFormat"></span>
###  ファイルのフォーマットの選択
クラウドレコーディングでは、 HLS、MP4、FLV 、AAC の四種類の異なるファイルフォーマットをサポートしています。形式と適用条件が異なる四種類のフォーマットを、自身の業務のニーズに合わせて選択することができます。

<table>
<tr>
<th>パラメータ</th>
<th>パラメータ説明</th>
</tr>
<tr>
<td>ファイル形式</td>
<td>以下のファイル形式をサポートします。<ul><li><b>HLS</b>：このファイル形式は、大多数のブラウザのオンライン再生をサポートし、ビデオの再生シーンに適合します。このファイル形式を選択したときは、ブレークポイントでの継続レコーディングをサポートし、個別のファイル最大時間は制限されません。</li><li><b>FLV</b>：このファイル形式は、ブラウザのオンライン再生をサポートしませんが、簡単でフォールトトレランス性が優れています。レコーディングしたファイルをVODプラットフォームに保存する必要がない場合は、このファイル形式を選択することができます。レコーディングの完了後、すぐにダウンロードしてファイルをレコーディングして、元のファイルを削除できます。</li><li><b>MP4</b>：このファイル形式は Web ブラウザのオンライン再生をサポートしますが、フォールトトレランスは劣ります。ビデオ通話のプロセスでは、どのパケットロスでも、レコーディングファイルの再生画質に影響します。</li><li><b>AAC</b>：音声レコーディングだけ必要な場合は、このファイル形式を選択できます。</li></td>
</tr>
<tr>
<td nowrap="nowrap">１ファイルの最大時間（分）</td>
<td>実際の業務ニーズに応じて1ビデオファイルの最大時間制限を設定できます。時間制限を超過すると、システムはビデオファイルを自動的に分単位で分割します。数値範囲は5 - 120。<br>この【ファイル形式】を【HLS】に設定するとき、1ファイルの最大時間を制限しなければ、そのパラメータは無効になります。</td>
</tr>
<tr>
<td>ファイル保存時間（日数）</td>
<td>実際の業務ニーズに応じて、ビデオファイルをVODプラットフォームの日数の間保存します。日数単位で数値範囲は0 - 1800。期限後は、ファイルはVODプラットフォームによって自動的に削除され、回復できなくなります。 0は永久保存を表します。</td>
</tr>
<tr>
<td>記録超過時間（秒）</td>
<td>【ファイル形式】を【HLS】に設定したときのみ、このパラメータは有効になります。<br>デフォルトでは、通話（またはライブストリーミング）プロセスが、ネットワークの不安定またはその他の原因によって遮断された場合は、ファイルのレコーディングは複数のファイルに切断されます。「一回通話（またはライブストリーミング）では1回しか再生接続ができない」を実現したい場合は、実情に応じて再開超過時間を設定し、遮断間隔が設定されたレコーディング再開超過時間を下回る場合は、一回通話（またはライブストリーミング）は1ファイルしか生成しません。秒単位。数値範囲は1 - 300。0は、ブレークポイント後は、継続レコーディングしないことを表します。</td>
</tr>
</table>

>? 
- オンライン教育分野の業務では、 HLS を選択してカリキュラムの再生に用いることを推奨します。
HLSは最長で5分間の継続レコーディングをサポートし、「1講義に1個のみの再生接続」が可能で、大多数のブラウザのオンライン視聴をサポートしており、ビデオ再生のユースケースにとても適しています。
- レコーディングファイルを自身で保存する必要があるときは、FLVフォーマットを選択することを推奨します。
HLS は一連の小さな ts ファイルで構成されており、サーバー間のマイグレーションは決して便利ではありません。そのため、自身で自社構築したサーバーに保存したい場合は、フォーマットが簡易でフォールトトレランス能力に優れた FLVの選択をお薦めします。

<span id="storageLocation"></span>
###  保存場所の選択
TRTCクラウドレコーディングファイルは、デフォルトではTencent Cloud VODサーバーに保存されます。プロジェクトで多くの業務が一つのTencent Cloud VODアカウントを共有している場合は、レコーディングファイルを隔離させる必要があるかもしれません。Tencent Cloud VODの「サブアプリ」機能によって、TRTCのレコーディングファイルをその他の業務エリアと切り離すことができます。

- **VODのメインアプリとサブアプリとは？**
メインアプリとサブアプリとは、VODの一種のリソース分割方式です。メインアプリはVODのメインアカウントに相当し、サブアプリは複数作成できます。各サブアプリは、メインアカウント下の1個のサブアカウントに相当し、独立したリソース管理を有しています。保存エリアではその他のサブアプリと相互に切り離されることがあります。

- **VODサービスのサブアプリを起動する方法は？**
ドキュメント [“VODアプリを起動する方法”](https://intl.cloud.tencent.com/document/product/266/33987) を基に新しいサブアプリを追加できます。この手順にはVOD[コンソール](https://console.cloud.tencent.com/vod)に移動して操作する必要があります。

<span id="recordCallback"></span>
###  レコーディングコールバックの設定
新しいファイルの [保存通知](#callback)をリアルタイムで受信する必要がある場合は、サーバーがレコーディングファイルのコールバックを受け取るアドレスを入力できます。このアドレスは、 HTTP（または HTTPS）プロトコルに適合する必要があります。新しいレコーディングファイルが生成されたら、Tencent Cloudはこのアドレスを介して、サーバーに通知を発信します。



詳細なレコーディングコールバックの受信及び解釈方法は、ドキュメント後半部分の：[レコーディングファイルの受信](#callback)をご参照ください。

<span id="startAndStop"></span>
## レコーディングの制御方法
TRTCは、三種類のクラウドレコーディングの制御方法を提供しています。それぞれ“クラウドレコーディング”、“指定ユーザーレコーディング（ SDK API制御）”および“指定ユーザーレコーディング（REST API 制御）”です。そのうちの各方法について、詳しく紹介します。
- コンソールでこの方法の使用設定をする方法は？
- レコーディングタスクを開始する方法は？
- レコーディングタスクを終了する方法は？
- ルームのマルチチャネル画面を1チャネルにMixする方法は？
- レコーディングしたファイルをどのように命名しますか？
- この方法をサポートするプラットフォームには何がありますか？

<span id="autoRecord"></span>
### 方法一：Global Auto-Recording
- **コンソールの設定**
このレコーディング方法を使用したい場合は、コンソールの [レコーディング形式の選択](#recordType)のとき、「Global Auto-Recording」に設定してください。

- **レコーディングタスクの開始**
TRTCルームの各ユーザーのオーディオ・ビデオストリーミングは、すべてファイルに自動レコーディングされるので、追加の操作は必要ありません。

- **レコーディングタスクの終了**
自動停止。各キャスターが音声ビデオのアップストリームを停止すると、このキャスターのクラウドレコーディングは自動的に停止します。 [ファイルフォーマットの選択](#fileFormat) のとき、“再開超過時間”を設定すると、再開超過時間時間を超過しないと、レコーディングファイルを受け取れなくなります。

- **マルチ画面のMix**
Global Auto-Recordingモードでは、クラウドミクスストリーミングに2つの方法があります。すなわち、「サーバー REST API 」 および 「クライアント SDK API 」です。2つの方法は混合して使用しないでください。
 + [サーバー REST API のMix方法](https://intl.cloud.tencent.com/document/product/647/34618#restapi)：サーバーから API のコールを発出する必要があり、クライアント側プラットフォームバージョンの制限は受けません。
 + [クライアント側 SDK API のMix方法](https://intl.cloud.tencent.com/document/product/647/34618#sdkapi)：クライアント側からMixを直接発出することができ、現在 iOS、Android、Windows、Mac および Electron などのプラットフォームをサポートし、一時的にWeChatのミニプログラムおよび Web サーバーはサポートしていません。


- **レコーディングファイルの命名**
 + キャスターが入室時に[userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータを指定した場合、レコーディングファイルは `userDefineRecordId_開始時間_終了時間` によって命名されます。
 + キャスターが入室時に [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータを指定していないが、 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) パラメータを指定している場合は、レコーディングファイルは `streamId_開始時間_終了時間` によって命名されます。
 + キャスターが入室時に [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータも、 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) パラメータも指定していない場合、レコーディングファイルは `sdkappid_roomid_userid_開始時間_終了時間` によって命名されます。
 
- **サポート済みのプラットフォーム**
サーバー側から制御し、クライアント側プラットフォームからの制限は受けません。

<span id="recordRESTAPI"></span>
### 方法二：ユーザーレコーディングの指定（SDK API）

![](https://main.qcloudimg.com/raw/e3d81ef76c64d2fb6631d98d22bfb0dc.png)

- **コンソールの設定**
このレコーディング方法を使用したい場合は、コンソールの [レコーディング形式の選択](#recordType)のときに、「指定ユーザーレコーディング」に設定してください。

- **レコーディングタスクの開始**
キャスターが入室時に入室パラメータ [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) の [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) のフィールドを指定してから、そのキャスターのアップストリームの音声ビデオデータは、クラウドにレコーディングされ、そのパラメータのキャスターを指定しないと、レコーディングタスクは作動しません。

```Objective-C
// サンプルコード：レコーディングユーザー rexchang の音声ビデオストリーミングを指定し、ファイルid を 1001_rexchangにします
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC の SDKAppID、アプリケーション作成後、取得可
param.roomId   = 1001;           // ルームナンバー
param.userId   = @"rexchang";    // ユーザー名
param.userSig  = @"xxxxxxxx";    // 署名ログイン
param.role     = TRTCRoleAnchor; // ロール：キャスター
param.userDefineRecordId = @"1001_rexchang";  // レコーディング IDは、そのユーザーのレコーディング開始を指定します。
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; //  LIVE モードを使用してください
```

- **レコーディングタスクの終了**
自動停止。入室時に [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータのキャスターを指定して音声ビデオのアップストリームを停止した後、クラウドレコーディングは自ら停止します。[ファイルフォーマットの選択](#fileFormat)のときに「継続レコーディング時間」を設定すると、継続レコーディング時間が超過するまでレコーディングファイルを受け取ることができなくなります。

- **マルチ画面のMix**
 SDK API  [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) をコールすることによって、ルーム内のその他のユーザーの画面および音声を現在のユーザーの一チャネルの音声ビデオストリーミング上にMixできます。この部分の詳細は、ドキュメント：[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88)で閲覧することができます。

- **レコーディングファイルの命名**
レコーディングファイルは、 `userDefineRecordId_開始時間_終了時間` のフォーマットで命名されます。

- **サポート済みのプラットフォーム**
[iOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Android](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520)、[Windows](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc)、[Mac](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) などの端末でレコーディング制御をサポートし、 Web ブラウザやWeChat Mini Program端末からの制御は一時的にサポートしません。

<span id="recordRESTAPI"></span>
### 方法三：指定ユーザーレコーディング（REST  API）

![](https://main.qcloudimg.com/raw/71b4b6705cee61000660c13c2a0fe595.png)

>? TRTC のサーバーは一対の REST API（ [StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) および [StopMCUMixTranscode](https://cloud.tencent.com/document/product/647/44269)）を提供し、クラウドミクスストリーミング、クラウドレコーディング、Relayed live streamingの三機能に使用します。
>- クラウドミクスストリーミング： `LayoutParams` パラメータによって、Mix時の画面レイアウトを制御できます。
>- クラウドレコーディング： `OutputParams.RecordId` パラメータによって、クラウドレコーディングの起動／停止ができます。
>- Relayed live streaming： `OutputParams.StreamId` パラメータによって、 CDN LVBの起動／停止ができます。

- **コンソールの設定**
このレコーディング方法を使用したい場合は、コンソールの [レコーディング形式の選択](#recordType)のときに、「指定ユーザーレコーディング」に設定してください。

- **レコーディングタスクの開始**
サーバーから [StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) をコールして、 `OutputParams.RecordId` パラメータを指定すると、Mixおよびレコーディングが行えます。

```
// コードサンプル： REST API によってクラウドミクスストリーミングおよびクラウドレコーディングのタスクを起動します
https://trtc.tencentcloudapi.com/?Action=StartMCUMixTranscode
&SdkAppId=1400000123
&RoomId=1001
&OutputParams.RecordId=1400000123_room1001
- **OutputParams.RecordAudioOnly**
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

- **レコーディングタスクの終了**
自動停止。途中で [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) をコールしてMixおよびRecordingタスクを停止することもできます。

- **マルチ画面のMix**
サーバーから [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) をコールして `LayoutParams` パラメータを指定すればOKです。この部分の詳細は、ドキュメント：[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88)で閲覧できます。

- **レコーディングファイルの命名**
レコーディングファイルは、 [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) をコールするときに指定した `OutputParams.RecordId` パラメータで命名します。命名フォーマットは、 `OutputParams.RecordId_開始時間_終了時間`です。

- **サポート済みのプラットフォーム**
サーバーで制御し、クライアント側プラットフォームの制限は受けません。

<span id="search"></span>
## レコーディングファイルの検索
レコーディング機能を起動させた後、TRTCシステムからレコーディングしたファイルは、Tencent CloudのVODサーバーから探し出せます。VODコンソールから手動で直接探し出したり、バックエンドサーバーからREST APIを使用して定刻にスクリーニングを行うこともできます。

**方法一：VODコンソールで手動で検索**
1. [VODコンソール](https://console.cloud.tencent.com/vod)にログインし、左側のナビゲーションバーで【メディアソース管理】を選択します。
2. 表の上側の【接頭辞検索】をクリックして【接頭辞検索】を選択し、検索枠にキーワードを入力します。例：`1400000123_1001_rexchang_main`では、<img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">をクリックして、ビデオ名称の接頭辞に相当するビデオファイルを表示します。
3．作成時間に基づき、必要な目標ファイルをスクリーニングすることができます。

**方法二： VOD REST API による検索**
Tencent CloudのVODシステムは、一連のREST API を提供してその上の音声ビデオファイルを管理します。 [メディア情報エンジン](https://intl.cloud.tencent.com/document/product/266/34179) のこの REST API によって、VODシステム上のファイルを検索します。パラメータ表の `Text` パラメータをリクエストすることで、曖昧マッチングや、 `StreamId` パラメータを基に正確な検索を行うこともできます。
RESRESTリクエスト例：
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<パブリックリクエストパラメータ>
```

<span id="callback"></span>
## レコーディングファイルの受け取り
 [レコーディングファイルの検索](#search)のほかにも、コールバックアドレスを設定することによって、Tencent Cloudに新たにレコーディングしたファイル情報をサーバーに主動的に送信させることもできます。
ルームの最後の一チャネルの音声ビデオストリーミングが退出後、Tencent Cloudはレコーディングを終え、ファイルをVODプラットフォームに移転して保存します。このプロセスのおよそのデフォルトは、約30秒から2分間（継続レコーディング時間を300秒に設定した場合、待ち時間はデフォルトの基礎時間に300秒を加えた時間）。転送保存が完了後は、Tencent Cloudは [レコーディングコールバック設定](#recordCallback) で設定したコールバックアドレス（HTTP/HTTPS）によってサーバーに通知を発信します。

Tencent Cloudは、レコーディングおよびレコーディング関連のイベントを、設定したコールバックアドレスを通じてサーバーに送信します。コールバック情報のサンプルは下図に示すとおりです。
![](https://main.qcloudimg.com/raw/483dba536acd022f93af3ca5ff6cd74a.png)
下表のフィールドによって、現在のコールバックがどの通話（またはライブストリーミング）に対応するかを確定することができます。

<table>
<tr>
<th>番号</th>
<th>フィールド名</th>
<th>説明</th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>情報形式。 event_type が100のときは、このコールバック情報が、レコーディングファイルが生成した情報であることを表します。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>入室時に TRTCParams の <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a> フィールドを設定することで指定できます。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>ユーザー名の Base64 コード。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>フィールドのカスタマイズ。 TRTCParams の <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a> フィールドを設定することで指定できます。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>レコーディングファイルの視聴アドレスは、 <a href="#play">VOD再生に使用できます</a>。</td>
</tr></table>

<span id="delete"></span>
## レコーディングファイルの削除
Tencent CloudのVODシステムは、一連のシステムREST APIを提供して、その上の音声ビデオファイルを管理します。 [メディア APIの削除](https://intl.cloud.tencent.com/document/product/266/37571) によって任意の指定したファイルを削除することができます。
RESRESTリクエスト例：
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<パブリックリクエストパラメータ>
```

<span id="Play"></span>
## レコーディングファイルの再生
オンライン教育などのユースケースでは、通常ライブストリーミングの終了後、何度もレコーディングファイルを再生し、教育リソースを十分に活用しやすくする必要があります。

**ファイルフォーマットの選択（HLS）**
 [レコーディングフォーマットの設定](#fileFormat)では、ファイルフォーマットを HLSに選択します。
HLS は最長5分間のブレークポイントの継続レコーディングをサポートしており、「一つのライブストリーミング（または1回の授業）から1回だけの再生接続」が行えます。かつ、 HLS ファイルは、大多数のブラウザのオンライン再生をサポートしており、ビデオ再生のユースケースにとても適しています。

**VODアドレス（video_url）の取得**
 [レコーディングファイルの受取](#callback) のときに、コールバック情報の **video_url** フィールドを取得できます。このフィールドは、現在のレコーディングファイルのTencent CloudにおけるオVODアドレスになります。

**VODプレイヤーの接続**
プラットフォームの使用に基づき、VODプレイヤーに接続します。具体的な操作は以下をご参照ください。
- [iOS プラットフォーム](http://doc.qcloudtrtc.com/group__TXVodPlayer__ios.html)
- [Android プラットフォーム](http://doc.qcloudtrtc.com/group__TXVodPlayer__android.html)

>!  [プロフェッショナルバージョン](https://intl.cloud.tencent.com/document/product/647/34615) のTRTC SDKの使用を推奨します。基盤となるコンポーネントの高度な再利用により、統合されたプロフェッショナル版のボリューム増分は、2つの独立したSDKを同時に統合する場合よりも小さくなり、さらにシンボルの衝突(symbol duplicate)といった課題を解消できます。

