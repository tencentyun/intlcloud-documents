## ユースケース
リモート教育、ステージCSS、ビデオ会議、リモート確定損失、金融二重レコーディング、オンライン医療などのユースケースでは、証明取得、品質検査、審査、保存、再生などのニーズがあり、すべてのビデオ通話やILVBプロセスをレコーディングまたは保存する必要がよくあります。

TRTCのクラウドレコーディングは、ルームの各ユーザーのオーディオ・ビデオストリーミングを独立した一つのファイルにレコーディングします。
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

ルーム内のマルチチャネルのオーディオ・ビデオを、まず[クラウドミクスストリーミング](https://intl.cloud.tencent.com/document/product/647/34618)してから、ミックス後のオーディオ・ビデオストリーミングを一つのファイルにレコーディングします。
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## コンソールガイド
[ ](id:open)
### レコーディングサービスのアクティブ化
1. [TRTCコンソール]にログインして、左側のナビゲーションバーで【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. ターゲットアプリケーションが所在する行の【機能設定】をクリックして、機能設定ページカードに進みます。アプリケーションを作成したことがない場合は、【アプリケーションの作成】をクリックしてアプリケーション名を入力し、【OK】をクリックして新しいアプリケーションを作成します。
3. 【クラウドレコーディングの起動】の右側の<img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png">をクリックすると、クラウドレコーディング設定ページ画面がポップアップされます。


[ ](id:recordType)

### レコーディング形式の選択

TRTCのクラウドレコーディングサービスは、「Global Auto-Recording」および「指定ユーザーレコーディング」という2種類の異なるレコーディング形式を提供しています。
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **Global Auto-Recording**
  各TRTCルームの各ユーザーのアップストリームのオーディオとビデオは自動的にレコーディングされます。レコーディングタスクの開始と停止は自動的に行われるため、心配する必要はありません。操作は比較的シンプルで使いやすいです。具体的な使用方法については、[方法1：Global Auto-Recording](#autoRecord)をご参照ください。

- **指定ユーザーレコーディング**
  一部ユーザーのオーディオ・ビデオストリーミングのみをレコーディングするように指定できます。これには、クライアントのSDKAPIまたはサーバーのRESTAPIを介して制御する必要があり、追加の開発作業が必要になります。具体的な使用方法については、[方法2：指定ユーザーレコーディング（SDK API）](#recordSDKAPI)および[方法3：指定ユーザーレコーディング（REST API）](#recordRESTAPI)をご参照ください。


[ ](id:fileFormat)

###  ファイルのフォーマットの選択

クラウドレコーディングでは、HLS、MP4、FLV 、AACという4種類の異なるファイルフォーマットをサポートしています。4種類のフォーマットの違いと適用ケースを表形式でリストアップしているので、ご自分の業務のニーズに合わせて選択することができます。

<table>
<tr><th>パラメータ</th><th>パラメータ説明</th></tr>
<tr>
<td>ファイルタイプ</td>
<td>以下のファイルタイプをサポートします。<ul style="margin:0"><li><b>HLS</b>：このファイルタイプは、ほとんどのブラウザのオンライン再生をサポートしており、ビデオの再生シーンに適しています。このファイルタイプを選択したときは、ブレークポイントでの連続レコーディングをサポートし、単一ファイルの最大時間が制限されません。</li><li><b>FLV</b>：このファイルタイプは、ブラウザでのオンライン再生をサポートしていませんが、フォーマットはシンプルでフォールトトレラント性に優れています。レコーディングしたファイルをVODプラットフォームに保存する必要がない場合は、このファイルタイプを選択し、レコーディングが完了したらすぐにレコーディングファイルをダウンロードして、ソースファイルを削除できます。</li><li><b>MP4</b>：このファイルタイプはWebブラウザのオンライン再生をサポートしていますが、このフォーマットのフォールトトレラント性は劣ります。ビデオ通話のプロセスでは、どのようなパケットロスが生じても、レコーディングファイルの再生画質に影響します。</li><li><b>AAC</b>：オーディオレコーディングだけ必要な場合は、このファイルタイプを選択しても構いません。</li></td>
</tr>
<tr>
<td nowrap="nowrap">1ファイルの最大時間（分）</td>
<td><ul style="margin:0"><li/>実際の業務ニーズに応じて、1ビデオファイルの最大時間制限を設定できます。制限時間を超過すると、システムはビデオファイルを自動的に分単位で分割します。数値範囲は1～120です。<li/>この【ファイルタイプ】を【HLS】に設定するとき、1ファイルの最大時間を制限しなければ、そのパラメータは無効になります。</td>
</tr>
<tr>
<td>ファイル保存時間（日）</td>
<td>実際の業務ニーズに応じて、ビデオファイルをVODプラットフォームの日数の間保存します。日数単位で数値範囲は0～1500。期限後は、ファイルはVODプラットフォームによって自動的に削除され、回復できなくなります。 0は永久保存を表します。</td>
</tr>
<tr>
<td>連続レコーディングタイムアウト（秒）</td>
<td><ul style="margin:0"><li/>デフォルトでは、通話（またはライブストリーミング）プロセスが、ネットワークの変動またはその他の原因によって切断された場合、レコーディングファイルは複数のファイルに分割されます。<li/>「1回の通話（またはライブストリーミング）で1つしか再生リンクが生成されない」ようにしたい場合は、実情に応じて連続レコーディングタイムアウト時間を設定できます。切断間隔が設定した連続レコーディングタイムアウト時間を超えない場合、1回の通話（またはライブストリーミング）で1ファイルしか生成されません。ただし、レコーディングファイルは連続レコーディング時間がタイムアウトしてからでなければ受信できません。<li/>単位は秒で、数値範囲は1～1800です。0は、ブレークポイント後にレコーディングが再開されないことを表します。</ul></td>
</tr>
</table>


>? HLSは最長で30分間の連続レコーディングをサポートしており、「1講義に1つしか再生リンクが生成されないように」することができます。また、ほとんどのブラウザのオンライン視聴をサポートしており、eラーニングにおけるビデオ再生のユースケースに大変適しています。

[ ](id:storageLocation)

###  保存場所の選択

TRTCクラウドレコーディングファイルは、デフォルトではTencent Cloud VODサーバーに保存されます。プロジェクトで多くの業務が一つのTencent Cloud VODアカウントを共有している場合、レコーディングファイルの隔離が必要になることがあります。Tencent Cloud VODの「サブアプリ」機能によって、TRTCのレコーディングファイルをその他の業務エリアと切り離すことができます。

- **VODのメインアプリとサブアプリとは何ですか。**
  メインアプリとサブアプリとは、VODの1種類のリソース分割方式です。メインアプリはVODのメインアカウントに相当し、サブアプリは複数作成できます。各サブアプリは、ルートアカウント下の1個のサブアカウントに相当し、独立したリソース管理を備えています。ストレージ領域では、その他のサブアプリと相互に隔離することができます。

- **VODサービスのサブアプリケーションを有効にする方法。**
  ドキュメント[「VODサブアプリケーションを有効にする方法」](https://intl.cloud.tencent.com/document/product/266/33987) にもとづき、新規サブアプリケーションを追加することができます。このステップではVOD[コンソール](https://console.cloud.tencent.com/vod)に移動して操作する必要があります。

[ ](id:recordCallback)

###  レコーディングコールバックの設定
- **レコーディングコールバックアドレス：**
  新しいファイルの[ランディング通知](#callback)をリアルタイムで受信する必要がある場合は、サーバーがレコーディングファイルのコールバックを受け取るアドレスをここに入力できます。このアドレスは、HTTP（またはHTTPS）プロトコルに適合する必要があります。新しいレコーディングファイルが生成されたら、Tencent Cloudはこのアドレスを介して、サーバーに通知を送信します。
![](https://main.qcloudimg.com/raw/9b9beab813d929a7a364eb2d8ab045ba.png)
	
- **レコーディングコールバックキー：**
コールバックキーは、コールバックイベントの受信時に署名認証を生成するために使用します。このキーはアルファベットの大文字・小文字と数字で構成し、32文字を超えないようにしてください。使用については、[レコーディングイベントパラメータの説明](https://intl.cloud.tencent.com/document/product/267/38082)をご参照ください。
![](https://main.qcloudimg.com/raw/9fa611019c25e3c073683bc4e3ec38ae.png)

>? 詳細なレコーディングコールバックの受信と解読方法については、ドキュメント後半部分の[レコーディングファイルの受け取り](https://intl.cloud.tencent.com/document/product/647/35426)をご参照ください。



[ ](id:startAndStop)

## レコーディングの制御方法

TRTCでは、[Global Auto-Recording](#autoRecord)、[指定ユーザーレコーディング（SDK APIによる制御）](#recordSDKAPI)、 [指定ユーザーレコーディング（REST APIによる制御）](#recordRESTAPI)という3種類のクラウドレコーディング制御方法を提供しています。これらの方法を一つずつ、詳しくご紹介します。

- コンソールでこの方式の使用設定をする方法。
- レコーディングタスクを開始する方法。
- レコーディングタスクを終了する方法。
- ルームのマルチチャネル画面を1チャネルにミックスする方法。
- レコーディングしたファイルの命名方法。
- ほかにどのような方法でプラットフォームをサポートするのか。


[](id:autoRecord)

### 方法1：Global Auto-Recording

- **コンソールでの設定**
  このレコーディング方法を使用したい場合は、コンソールの[レコーディング形式の選択](#recordType)で「Global Auto-Recording」に設定してください。

- **レコーディングタスクの開始**
  TRTCルームの各ユーザーのオーディオ・ビデオストリーミングは、すべてファイルに自動レコーディングされるので、追加の操作は必要ありません。

- **レコーディングタスクの終了**
  自動停止。各キャスターがオーディオ・ビデオのアップストリームを停止すると、このキャスターのクラウドレコーディングは自動的に停止します。[ファイルフォーマットの選択](#fileFormat)のときに「連続レコーディング時間」を設定すると、レコーディングファイルを受信する前に、連続レコーディング時間がタイムアウトするのを待つ必要が出てきます。

- **マルチ画面のミックス**
  Global Auto-Recordingモードでのクラウドミクスストリーミングには、「サーバーREST API方式」と「クライアントSDK API方式」という2つの方式があります。この2つの方式を混合して使用しないでください。
  - [サーバーREST APIミクスストリーミング方式](#recordRESTAPI)：お客様のサーバーからAPI呼び出しを起動する必要があります。クライアントのプラットフォームバージョンの制限は受けません。
  - [クライアントSDK APIミクスストリーミング方式](#recordSDKAPI)：直接クライアントからミクスストリーミングを開始できます。現在サポートしているのは、iOS、Android、Windows、Mac、Electronなどのプラットフォームであり、WeChat Mini ProgramおよびWebブラウザは現在サポートしていません。

- **レコーディングファイルの命名**
  - キャスターが入室時に [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータを指定した場合、レコーディングファイルは `userDefineRecordId_streamType_開始時刻_終了時刻` で命名されます（streamTypeにはmainおよびauxの2つの値があり、mainはメインパスを、auxはサブパスを表します。サブパスは通常、画面共有に利用されます）。
  - キャスターが入室時に [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータを指定していなかったが、 [streamId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) パラメータを指定していた場合は、レコーディングファイルは`streamId_開始時刻_終了時刻` で命名されます。
  - キャスターが入室時に [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) パラメータ、 [streamId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) パラメータをいずれも指定していない場合は、レコーディングファイルは `sdkappid_roomid_userid_streamType_開始時刻_終了時刻` で命名されます（streamTypeにはmainおよびauxの2つの値があり、mainはメインパスを、auxはサブパスを表します。サブパスは通常、画面共有に利用されます）。

- **サポート済みのプラットフォーム**
  お客様側のサーバーで制御し、クライアント側プラットフォームの制限は受けません。

[](id:recordSDKAPI)

### 方法2：指定ユーザーレコーディング（SDK API）

TRTC SDKが提供するいくつかのAPIインターフェースとパラメータを呼び出すことで、クラウドミクスストリーミング、クラウドレコーディング、Relayed live streamingという3つの機能が実装可能です。

| クラウド機能 | 開始方法 | 停止方法 |
| :------- | :------- | :------- |
| クラウドレコーディング | 入室時にパラメータ`TRTCParams`の中の`userDefineRecordId`フィールドを指定します   | キャスター退室時に自動停止します                                           |
| クラウドミクスストリーミング| SDK API  [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) を呼び出してクラウドミクスストリーミングを起動 | クラウドミクスを発出したキャスターが退室したら、ミクスストリーミングは自動的に停止するか、途中で [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) を呼び出してパラメータを `null/nil` 手動停止に設定します |
| Relayed live streaming | 入室時にパラメータ`TRTCParams`の中の`streamId`フィールドを指定します           | キャスター退室時に自動停止します                                           |

![](https://main.qcloudimg.com/raw/7daf8430ca74adeec019c10fc384a48e.gif)

- **コンソールでの設定**
  このレコーディング方法を使用したい場合は、コンソールの[レコーディング形式の選択](#recordType)のときに、「指定ユーザーレコーディング」に設定してください。

- **レコーディングタスクの開始**
  キャスターが入室時に入室パラメータ [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) の [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) フィールドを指定すると、その後、同キャスターのアップストリームのオーディオ・ビデオデータがクラウドレコーディングされます。このパラメータを指定していないキャスターはレコーディングタスクを起動することはありません。
<dx-codeblock>
::: Objective-C Objective-C
// サンプルコード：レコーディングユーザーrexchangのオーディオ・ビデオストリーミングを指定し、ファイルidを1001_rexchangにします
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTCのSDKAppIDは、アプリケーション作成後に取得できます
param.roomId   = 1001;           // ルームナンバー
param.userId   = @"rexchang";    // ユーザー名
param.userSig  = @"xxxxxxxx";    // ログイン署名
param.role     = TRTCRoleAnchor; // ロール：キャスター
param.userDefineRecordId = @"1001_rexchang";  // レコーディングID。そのユーザーのレコーディング開始を指定します。
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // LIVEモードを使用してください
:::
</dx-codeblock>

- **レコーディングタスクの終了**
  自動停止。入室時に[userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)パラメータのキャスターを指定してオーディオ・ビデオのアップストリームを停止すると、クラウドレコーディングは自動的に停止します。[ファイルフォーマットの選択](#fileFormat)のときに「連続レコーディング時間」を設定すると、レコーディングファイルを受信する前に、連続レコーディング時間がタイムアウトするのを待つ必要が出てきます。

- **マルチ画面のミックス**
  SDK API[setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)を呼び出すことによって、ルーム内の他のユーザーの画面や音声をカレントユーザーのチャネルのオーディオ・ビデオストリーミングにミックスすることができます。この部分の詳細については、次のドキュメント[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88)をご参照ください。
>! 1つのTRTCルーム内では、1人のキャスター（配信を開始したキャスターを推奨）のみが`setMixTranscodingConfig`を呼び出せばOKです。複数のキャスターが呼び出すと、ステータスの混乱を生じて、エラーが起きる可能性があります。

- **レコーディングファイルの命名**
  レコーディングファイルは、`userDefineRecordId_開始時間_終了時間` のフォーマットで命名されます。

- **サポート済みのプラットフォーム**
  [iOS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Android](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520)、[Windows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc)、[Mac](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Electron](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)などの端末でレコーディング制御の開始をサポートしていますが、現時点ではWeChat Mini ProgramおよびWebブラウザからの制御はサポートしていません。

[](id:recordRESTAPI)

### 方法3：指定ユーザーレコーディング（REST  API）

TRTCのサーバーはREST APIのペア（ [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)および[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)）を提供し、クラウドミクスストリーミング、クラウドレコーディング、Relayed live streamingという3つの機能を実装するために使用します。

| クラウド機能 | 開始方法  | 停止方法 |
| :------- | :------- | :------- |
| クラウドレコーディング |  [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)を呼び出す時に、`OutputParams.RecordId`パラメータを指定すれば、レコーディングを開始できます | 自動停止、または途中で[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)を呼び出して停止します |
| クラウドミクスストリーミング |  [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)を呼び出す時に`LayoutParams` パラメータを指定すれば、レイアウトテンプレートとレイアウトパラメータを設定できます | 全ユーザーが退室した後自動停止、または途中で[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)を呼び出して手動停止します |
| Relayed live streaming |  [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)を呼び出す時に`OutputParams.StreamId`パラメータを指定すれば、CDNへのRelayed live streamingを起動できます | 自動停止、または途中で[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) を呼び出して停止します |

>? これらのREST APIに対する制御は、TRTCクラウドサービスの中のコアのミクスストリーミングモジュール（MCU）となり、MCU ミクスストリーミング後の結果はレコーディングシステムとライブCDNに送信されるため、APIの名前を `Start/StopMCUMixTranscode`としています。このため、機能の点からいうと、`Start/StopMCUMixTranscode` はミクスストリーミングの機能を実装できるだけでなく、クラウドレコーディングとRelayed live streaming CDNの機能も実装できます。

![](https://main.qcloudimg.com/raw/65ef546c0e424af77f7d20f23aa1d363.gif)

- **コンソールでの設定**
  このレコーディング方法を使用したい場合は、コンソールの[レコーディング形式の選択](#recordType)のときに、「指定ユーザーレコーディング」に設定してください。

- **レコーディングタスクの開始**
  サーバーから[StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)を呼び出して、`OutputParams.RecordId`パラメータを指定すると、ミクスストリーミングおよびレコーディングを起動することができます。
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
>- REST APIを使用すると、シングルストリームのレコーディングはサポートされません。シングルストリームをレコーディングしたい場合は、 [方法1](#autoRecord)または[方法2](#recordSDKAPI)を選択してください。

- **レコーディングタスクの終了**
  自動停止。途中で[StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)を呼び出してミクスストリーミングおよびレコーディングタスクを停止することもできます。

- **マルチ画面のミックス**
  [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)を呼び出す時に、同時に `LayoutParams` パラメータを指定すれば、クラウドミクスストリーミングを実装できます。このAPIは、 ライブストリーミング全時間内での複数回呼び出しをサポートしていますので、必要に応じて `LayoutParams` パラメータを修正し、このAPIを再度呼び出して合成画面のレイアウトを調整することができます。ただし、注意が必要なのは、パラメータ `OutputParams.RecordId` と `OutputParams.StreamId`が複数回呼び出しの中で一致性を維持する必要があることです。そうしない場合、ストリームが切断され、複数のレコーディングファイルが生成されてしまいます。

>?クラウドミクスストリーミングのより詳しい紹介については、[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#restapi)をご参照ください。

- **レコーディングファイルの命名**
  レコーディングファイルは、[StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) を呼び出すときに指定した`OutputParams.RecordId`パラメータで命名します。命名フォーマットは、`OutputParams.RecordId_開始時間_終了時間`です。

- **サポート済みのプラットフォーム**
  お客様側のサーバーで制御し、クライアント側プラットフォームの制限は受けません。

[](id:search)
## レコーディングファイルの検索

レコーディング機能を起動させた後、TRTCシステムからレコーディングしたファイルは、Tencent CloudのVODサーバーから探し出せます。VODコンソールから手動で直接探し出したり、バックエンドサーバーからREST APIを使用して所定の時間にフィルタリングを行うこともできます。

#### 方法1：VODコンソールで手動で検索
1. [VODコンソール](https://console.cloud.tencent.com/vod)にログインし、左側ナビゲーションバーで【メディア資産管理】を選択します。
2. リスト上側の【プレフィックス検索】をクリックして【プレフィックス検索】を選択し、検索ボックスにキーワードを入力します。例えば、`1400000123_1001_rexchang_main`の場合、<img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">をクリックすると、ビデオ名のプレフィックスに一致するビデオファイルが表示されます。
3. 作成時間に基づき、必要なターゲットファイルをフィルタリングすることができます。

#### 方法2：VOD REST APIによる検索
Tencent CloudのVODシステムは、一連のREST APIを提供してその上のオーディオ・ビデオファイルを管理します。[メディア情報検索](https://intl.cloud.tencent.com/document/product/266/34179)のこのREST APIによって、VODシステム上のファイルを検索します。パラメータ表の`Text`パラメータをリクエストすることで、あいまい一致や、`StreamId`パラメータをもとに正確な検索を行うこともできます。
RESTリクエスト例：
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<パブリックリクエストパラメータ>
```

[](id:callback)

## レコーディングファイルの受け取り

[レコーディングファイルの検索](#search)のほかにも、コールバックアドレスを設定することによって、Tencent Cloudに新たにレコーディングしたファイル情報をサーバーに自動的にプッシュさせることもできます。
ルームの最後の1チャネルのオーディオ・ビデオストリーミングが終了すると、Tencent Cloudはレコーディングを終了し、ファイルをVODプラットフォームに転送して保存します。このプロセスには、デフォルトで約30秒から2分かかります（連続レコーディング時間を300秒に設定した場合、待ち時間はデフォルトの時間に300秒を加えた時間になります）。転送と保存が完了すると、Tencent Cloudは[レコーディングコールバック設定](#recordCallback)で設定したコールバックアドレス（HTTP/HTTPS）を介してサーバーに通知を送信します。

Tencent Cloudは、レコーディングおよびレコーディング関連のイベントを、設定したコールバックアドレスを介して、サーバーにプッシュします。コールバックメッセージの例を次の図に示します。
![](https://main.qcloudimg.com/raw/483dba536acd022f93af3ca5ff6cd74a.png)
下表のフィールドによって、現在のコールバックがどの通話（またはCSS）に対応するかを確定することができます。

<table>
<tr>
<th>番号</ th> <th>フィールド名</ th> <th>説明</ th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>メッセージタイプ。event_typeが100のときは、このコールバックメッセージが、レコーディングファイルが生成したメッセージであることを表します。</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>ライブCDNのstreamIdです。入室時にTRTCParamsの<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a>フィールドを設定することで指定でき（推奨）、また、TRTCCloudのstartPublishingを呼び出すときにパラメータstreamIdで指定することもできます。</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>ユーザー名のBase64コード。</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>カスタムフィールド。 TRTCParams の <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a> フィールドを設定することで指定できます。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>レコーディングファイルの視聴アドレスは、<a href="#play">VOD再生に使用できます</a>。</td>
</tr></table>

>? コールバックフィールドに関するその他の説明については、[CSS-レコーディングイベントの通知](https://intl.cloud.tencent.com/document/product/267/38082)をご参照ください。


[](id:delete)
## レコーディングファイルの削除

Tencent CloudのVODシステムは、一連のシステムREST APIを提供して、その上のオーディオ・ビデオファイルを管理します。[メディアAPIの削除](https://intl.cloud.tencent.com/document/product/266/37571)によって任意の指定したファイルを削除することができます。
RESTリクエスト例：
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<パブリックリクエストパラメータ>
```

[](id:play)
## レコーディングファイルの再生

オンライン教育などのユースケースでは、通常CSSが終了後、何度もレコーディングファイルを再生し、教育リソースを十分に活用しやすくする必要があります。

#### ファイルフォーマットの選択（HLS）
[レコーディングフォーマットの設定](#fileFormat)では、ファイルフォーマットをHLSに選択します。
HLSは最長30分間のブレークポイントでの連続レコーディングをサポートしており、「1つのライブストリーミング（または1回の授業）で1つしか再生リンクが生成されないように」することができます。また、HLSファイルは、ほとんどのブラウザのオンライン再生をサポートしており、ビデオ再生のユースケースに大変適しています。

#### VODアドレス（video_url）の取得
[レコーディングファイルの受け取り](#callback)のときに、コールバック情報の**video_url**フィールドを取得できます。このフィールドは、現在のレコーディングファイルのTencent CloudにおけるVODアドレスになります。

#### VODプレーヤーとの接続
使用するプラットフォームに基づいてVODプレーヤーと接続します。具体的な操作は以下をご参照ください。
- [iOSプラットフォーム](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html)
- [Androidプラットフォーム](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html)
- [Webブラウザ](https://intl.cloud.tencent.com/document/product/266/33977)

>! [プロフェッショナル版](https://intl.cloud.tencent.com/document/product/647/34615)TRTC SDKの使用を推奨します。プロフェッショナル版には [Super Player（Player+）](https://intl.cloud.tencent.com/document/product/266/7836)、[モバイルライブストリーミング](https://intl.cloud.tencent.com/product/mlvb) などの機能が統合され、基盤モジュールを高度に再利用することにより、プロフェッショナル版の容量増加は同時に2つの独立したSDKを統合させたよりも小さくなっています。さらにシンボル重複（symbol duplicate）の問題も回避できます。


## 関連料金

クラウドレコーディングと再生の関連料金には次の項目が含まれています。このうち、レコーディング料金は基本料金となり、その他の料金はお客様の使用状況およびニーズに応じて徴収されます。

>?ここでは価格を例示し、参考としてのみ提供しています。価格と実際の状況とが一致しない場合は、[クラウドレコーディング課金説明](https://intl.cloud.tencent.com/document/product/647/38385)、[CSS](https://buy.intl.cloud.tencent.com/pricing/css) 、[VOD](https://buy.intl.cloud.tencent.com/pricing/vod)の料金を基準とします。

#### レコーディング料金：トランスコーディングまたはそのパッケージングに発生した料金の計算

レコーディングは、オーディオ・ビデオストリーミングのトランスコーディングまたはそのパッケージングが必要となるため、サーバーの計算リソースの消費が発生します。このため、レコーディング業務が計算リソースを占有するコストに応じて費用を徴収する必要があります。

>!
>- 2020年7月1日以降、初めてTRTCコンソールでアプリケーションを作成したTencent Cloudアカウントの場合、クラウドレコーディング機能を使用した後に発生するレコーディング料金については、[クラウドレコーディング課金説明](https://intl.cloud.tencent.com/document/product/647/38385)を基準とします。
>- 2020年7月1日以前に TRTC コンソールでアプリケーションを作成したことのあるTencent Cloudアカウントは、2020年7月1日以前またはそれ以降に作成したアプリケーションであっても、クラウドレコーディング機能を使用して発生するレコーディング料金については、デフォルトで、**CSSレコーディング**の課金ルールを引き続き採用します。

**CSSレコーディング**課金の計算方法は、同時レコーディングのチャネル数に応じて課金し、同時実行数が多くなるほど、レコーディング費用も高くなります。課金説明の詳細は [CSS > CSSレコーディング](https://intl.cloud.tencent.com/document/product/267/39605)をご参照ください。

>例えば、現在1000名のキャスターがいて、夕方のピーク時に、最多500チャンネルのキャスターのオーディオ・ビデオストリーミングを同時レコーディングする必要があるとします。仮にレコーディング単価が5.2941米ドル/チャンネル/月とすると、合計レコーディング料金は、`500チャンネル × 5.2941米ドル/チャンネル/月 = 2647.05米ドル/月`となります。
>[レコーディングフォーマットの設定](#fileFormat)をする時に同時に2種類のレコーディングファイルを選択した場合、レコーディング料金とストレージ料金はいずれも× 2になります。同様の理屈により、3種類のファイルを選択した時のレコーディング料金とストレージ料金は× 3になります。不要な場合は、必要な1種類のファイルフォーマットのみを選択することを推奨します。コストを大幅に抑えることができます。

**ストレージ料金：ファイルをTencent Cloudに保存するとこの料金が発生します**
レコーディングしたファイルをTencent Cloudに保存する場合は、保存自体にディスクリソースの消費が発生しますので、保存するリソースの占用状況に応じて料金を徴収する必要があります。保存期間が長いほど料金も高くなるため、特殊なニーズがない場合は、ファイルの保存期間を短めに設定して、費用を節約するか、またはファイルを自分のサーバーに保存することもできます。保存料金は、 [ビデオ保存（日次決済）価格](https://intl.cloud.tencent.com/document/product/266/14666)選択し、日次決算で計算することができます。

>例えば、[setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)を介してキャスターのビットレート（videoBitrate）を1000kbpsに設定し、そのキャスターのライブストリーミングビデオ（1種類のファイルフォーマットを選択）をレコーディングし、1時間レコーディングすると、おおよそ`(1000 / 8)KBps × 3600秒 = 450000KB = 0.45GB`サイズのビデオファイルが生成されます。このファイルに毎日発生するおおよそのストレージ料金は、`0.45GB × 0.0009 米ドル/GB/日 = 0.000405米ドル`となります。

#### 視聴料金：ファイルをVOD視聴に利用するとこの料金が発生します

レコーディングしたファイルをオンデマンド視聴に利用する場合は、視聴自体にCDNトラフィックが消費されるため、VODの価格にもとづき課金する必要があります。デフォルトは、トラフィックによる課金となっています。視聴者数が多いほど料金は高くなります。視聴料金は[ビデオアクセラレーション（日次決済）価格](https://intl.cloud.tencent.com/document/product/266/14666) を選択し、日次決算で計算できます。

>例えば、クラウドレコーディングによって1GBのファイルが生成され、1000名の視聴者が最初から最後まで完全にそのビデオを視聴すると、約1TBのVOD視聴トラフィックが発生します。この場合は、階層価格表にもとづき、1000名の視聴で、`1000 × 1GB × 0.0794米ドル/GB = 79.4米ドル`の料金が発生します。
>Tencent Cloudからファイルをお客様のサーバーにダウンロードするように選択した場合も、非常に小さなVODトラフィックが消費され、お客様の月次請求書の中に反映されます。

#### トランスコード料金：ミクスストリーミングレコーディングを有効にすると、この料金が発生します

ミクスストリーミングレコーディングを作動させた場合は、ミクスストリーミング自体はデコーディングとコーディングする必要があるため、追加ミクスストリーミングトランスコード料金が発生します。ミクスストリーミングトランスコーディングは、解像度の大きさおよびトランスコーディング時間によって計算され、キャスター用の解像度が高く、マイク接続時間（通常はマイク接続のシーンではMixTranscodingが必要です）が長いほど、料金は高くなります。費用計算の詳細は[CSSトランスコード](https://intl.cloud.tencent.com/document/product/267/39604)をご参照ください。

>例えば、 [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)を介してキャスターのビットレート（videoBitrate）を1500kbps、解像度を720Pに設定したとします。1名のキャスターが視聴者と1時間マイク接続し、マイク接続の間に[クラウドミクスストリーミング](https://intl.cloud.tencent.com/document/product/647/34618)を有効にした場合、発生するトランスコード料金は`0.0057米ドル/分 × 60分 = 0.342米ドル`となります。


## 関連する質問
### TRTCはどのようにサーバーでのレコーディングを実現しますか。
サーバーでのレコーディングにはLinux SDKを使用する必要があります。Linux SDKはまだ完全公開されていません。お問い合わせまたは関連サービスの利用をご希望の場合は、colleenyu@tencent.comまでご連絡ください。
