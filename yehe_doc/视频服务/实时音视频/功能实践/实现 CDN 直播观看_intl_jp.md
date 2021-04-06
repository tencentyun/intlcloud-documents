## 適用ケース
CDNライブストリーミング、別名「CDN relayed live streaming」といいます。TRTCがUDPプロトコルを採用してオーディオ・ビデオデータの伝送を行うのに対し、標準のライブCDNはRTM\PHLS\FLVなどのプロトコルを採用してデータ伝送を行っているため、TRTCのオーディオ・ビデオデータをライブCDNに**バイパス**することによって、視聴者がライブCDNを介して視聴できるようになります。

TRTCとCDNとの接続・視聴は、通常、次の2つの問題を解決するために用いられます。
- **問題1：超高画質・同時視聴**
TRTC の低遅延時の視聴能力は、シングルルームで最大10万人をサポートし、CDNは、遅延が若干多いものの、10万人以上の並列視聴をサポートしています。かつ、CDNにかかる費用は極めて安価です。
- **問題2：モバイル端末サイトでの再生**
TRTCは、 WebRTCプロトコルのアクセスをサポートしていますが、主にChromeデスクトップ版ブラウザに使用されており、モバイル版ブラウザの兼用性は極めて扱いにくくなっています。とりわけAndroidスマホブラウザのWebRTCに対するサポートは一般に劣っています。そのため、 Web ページによってモバイル端末でライブストリーミングコンテンツのシェアリングを希望する場合は、やはりHLS(m3u8)の再生プロトコルの使用を推奨します。このことも、ライブCDN の能力を介してHLS プロトコルをサポートすることが必要です。


## 原理解析
Tencent Cloudは、一連のバイパストランスコードクラスターを使用し、TRTCのオーディオ・ビデオデータをライブCDNシステムにバイパスします。このクラスターは、TRTCが使用するUDPプロトコルを標準のライブストリーミングRTMPプロトコルに変換する役割を果たします。
<span id="directCDN"></span>
**単一チャネル画面のRelayed live streaming**
TRTCルームにキャスターが1人しかいないときは、TRTCのRelayed Pushは標準のRTMPプロトコルのライブプッシュ機能と同じです。しかし、TRTC のUDP は、RTMPと比較して弱ネットワーク時の耐性がより強くなります。
![](https://main.qcloudimg.com/raw/23ac68cb46b06cc4eb6000fa98500dc4.jpg)

<span id="mixCDN"></span>
**合成画面のRelayed live streaming**
TRTCが最も得意とする分野は、オーディオ・ビデオのインタラクティブマイク接続です。ルーム1室に同時に複数のキャスターがいて、CDNの視聴者側がオーディオ・ビデオ画面を1チャネルだけプルしたい場合は、[クラウドミクスストリーミングサービス](https://intl.cloud.tencent.com/document/product/647/34618)を使用して、複数画面を1チャネルに統合する必要があります。その原理は下図のとおりです。
![](https://main.qcloudimg.com/raw/77eeed776e61c3a6bd0e1669e5747727.jpg)

>? **マルチチャネルのCDN画面を直接再生しない理由とは。**
>マルチチャネルCDN画面の再生では、マルチチャネル画面の遅延アライメントという問題を解決するのが困難です。同時に、複数の画面をプルするために消費されるダウンロードトラフィックも単一画面よりも多いため、業界では通常、クラウドミクスストリーミングソリューションが採用されています。

## 前提条件
テンセントの[LVB](https://console.cloud.tencent.com/live)サービスはアクティブ化されています。国の関連部局の要請に従い、ライブストリーミング再生では、再生ドメイン名を構成する必要があります。具体的な操作については、[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

## 使用手順

<span id="step1"></span>
### 手順1：Relayed Push機能をオンにする

1. [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目標アプリケーションのある行の【機能設定】をクリックします。
3. 【Relayed Push設定】で【Relayed Pushの起動】の右側にある![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png)をクリックし、ポップアップした【Relayed Push機能の起動】ダイアログボックスの中から【Relayed Push機能をオンにする】をクリックすると、アクティブになります。


<span id="step2"></span>
### 手順2：再生ドメイン名を構成しCNAMEを完了する
1. [LVBコンソール](https://console.cloud.tencent.com/live/)にログインします。
2. 左側ナビゲーションバーで【Domain Management】を選択すると、ドメイン名リストにプッシュドメイン名が新規追加されたことがわかります。フォーマットは`xxxxx.livepush.myqcloud.com`になります。このうち、xxxxxは一つの数字で、bizidといいます。TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】>【アプリケーション情報】からbizid情報を探し出すことができます。
3. 【ドメイン名の追加】をクリックして、ICP登録済みの再生ドメイン名を入力し、ドメイン名のタイプを【再生ドメイン名】に選択し、アクセラレーションリージョン（デフォルトは【中国大陸】）を選択し、【OK】をクリックすれば完了です。
4. ドメイン名の追加が成功した後、システムは一つのCNAMEドメイン名（`.liveplay.myqcloud.com`を拡張子とする）を自動的にアサインします。CNAMEドメイン名は直接アクセスができませんので、ドメイン名のサービスプロバイダでCNAME 設定を完了する必要があります。設定が有効になったら、クラウドのLVBサービスを楽しむことができるようになります。具体的な操作は [CNAME設定](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。

>! **Pushドメイン名の追加は必要ありません**。 [手順1](#step1) でRelayed live streaming機能を起動した後、クラウドはデフォルトでLVBコンソールにフォーマットが `xxxxx.livepush.myqcloud.com` のプッシュドメイン名を追加します。このドメイン名はTencent Cloud LVBサービスおよびTRTCサービスとの間で取り決めたデフォルトのプッシュドメイン名であり、当面は修正をサポートすることはありません。

<span id="step3"></span>
### 手順3：TRTCのオーディオ・ビデオストリーミングをライブストリーミングstreamIdに関連付ける
Relayed Push機能をオンにすると、TRTCルームの各チャネル画面に対応する再生アドレスが割り当てられます。そのアドレスの形式は次のとおりです。
```
http://再生ドメイン名/live/[streamId].flv
```
アドレスのstreamIdは、ライブストリーミング中のLVBストリームを一意に識別することができます。ご自分でstreamIdを指定することもできますし、システムのデフォルトを使用して生成することもできます。

#### 方式1：streamIdのカスタマイズ指定
`TRTCCloud`の`enterRoom`関数を呼び出すときに、そのパラメータ`TRTCParams`の`streamId`パラメータによってライブストリームIDを指定することができます。
iOS端末のObjective-Cコードの例：

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTCのSDKAppID。アプリケーション作成後、取得可
param.roomId   = 1001;           // ルームナンバー
param.userId   = @"rexchang";    // ユーザー名
param.userSig  = @"xxxxxxxx";    // ログイン署名
param.role     = TRTCRoleAnchor; // ロール：キャスター
param.streamId = @"stream1001";  // ストリームID
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; //  LIVEモードを使用してください
```
`userSig`の計算方法は [UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

#### 方式2： システムの指定streamId
Auto-Relayed Pushをオンにした後、streamIdをカスタマイズ指定していない場合、システムはデフォルトで既定のstreamIdを生成します。生成ルールは次のとおりです。

- ** streamIdを使用したフィールドの結合**
  - sdkAppID: [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】にあります。
  - bizid:  [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】にあります。
  - roomId：`enterRoom`関数のパラメータ`TRTCParams`から指定します。
  - userId： `enterRoom` 関数のパラメータ`TRTCParams`から指定します。
  - streamType： カメラ画面がmain、画面共有がaux （WebRTCは、同時に一方向のアップストリームしかサポートできないため、WebRTCの画面共有のストリームタイプがmain）です。

- ** streamIdの計算ルールの結合**
 <table>
<tr>
<th>スプライシング</th>
<th>2020年1月9日以降に作成したアプリケーション</th>
<th>2020年1月9日よりも前に作成し使用したことのあるアプリケーション</th>
</tr>
<tr>
<td>スプライシングルール</td>
<td>streamId = urlencode(sdkAppId_roomId_userId_streamType)</td>
<td>StreamId = bizid_MD5(roomId_userId_streamType)</td>
</tr>
<tr>
<td>計算例</td>
<td>例：sdkAppId = 12345678、roomId = 12345、userId = userA、ユーザーが現在カメラを使用しています。<br>その場合：streamId = 12345678_12345_userA_main</td>
<td>例：bizid = 1234、roomId = 12345、userId = userA、ユーザーが現在カメラを使用しています。<br>その場合：streamId = 1234_MD5(12345_userA_main) = 1234_8D0261436C375BB0DEA901D86D7D70E8</td>
</tr>
</table>


<span id="step4"></span>
### 手順4：マルチチャネル画面を制御するためのミックスソリューション

合成した後のライブストリーミング画面を取得したい場合は、TRTCCloud の`setMixTranscodingConfig`インターフェースを呼び出してCloud MixTranscodingを起動する必要があります。このインターフェースのパラメータ`TRTCTranscodingConfig`を使用して、次のような構成を行うことができます。
 - 各サブ画面の配置位置およびその大きさ。
 - 合成画面の画面品質およびコードパラメータ。

画面レイアウトの詳細な設定方法については、[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)をご参照ください。プロセス全体に関わるモジュール間の関係については、[原理解析](#mixCDN)を参照することができます。

>! `setMixTranscodingConfig` は、端末でミクスストリーミングをするものではなく、ミクスストリーミング設定をクラウドに発送するものです。クラウドサーバーでミクスストリーミングおよびトランスコードを行います。ミクスストリーミング及びトランスコードを元の動画データにデコードおよび再エンコードすることから、処理時間はより長くなるため、合成画面の実際の視聴レイテンシーは独立画面よりも1s - 2s長くなります。

<span id="step5"></span>
### 手順5：再生アドレスを取得し、接続して再生する
[手順2](#step2) で再生ドメイン名の設定を終え、 [手順3](#step3) でstreamIdのマッピングを終えると、LVBの再生アドレスを取得することができます。再生アドレスの標準フォーマットは次のとおりです。
```
http://再生ドメイン名/live/[streamId].flv
```

例：再生ドメイン名が`live.myhost.com`の場合、ルーム（1001）のユーザーuserA のライブストリームIDを入室パラメータによってstreamId = "streamd1001"に指定します。
これによって、3チャネルの再生アドレスを取得できます。
```
 rtmpプロトコルの再生アドレス：rtmp://live.myhost.com/live/streamd1001
 flvプロトコルの再生アドレス：http://live.myhost.com/live/streamd1001.flv
 hlsプロトコルの再生アドレス：http://live.myhost.com/live/streamd1001.m3u8
```

プレフィックスに`http`、拡張子に`.flv`を付けた**http - flv** アドレスをお勧めします。このアドレスでの再生は、低遅延、優れたインスタントブロードキャスティング効果、高信頼性といった特徴があります。
プレーヤーの選択については、下表のガイドラインのソリューションを参照することをお勧めします。

| 属するプラットフォーム | ドッキングドキュメント | API概要 | サポートするフォーマット|
|:-------:|:-------:|:-------:|-------|
| iOS App| [アクセスガイド](https://intl.cloud.tencent.com/document/product/1071/38159) | TXLivePlayer(iOS)  | FLVを推奨 |
| Android App |[アクセスガイド](https://intl.cloud.tencent.com/document/product/1071/38160) | TXLivePlayer(Android) | FLVを推奨 |
| Webブラウザ | アクセスガイド | - |  デスクトップChromeブラウザはFLVをサポートします <br> Mac端末のSafariとモバイル端末・スマホブラウザはHLSのみをサポートします |


<span id="step6"></span>
### 手順6：再生レイテンシーを最適化する

Relayed live streamingがオンになった後のhttp-flvアドレスは、ライブCDNの拡散と配信のため、TRTCのライブストリーミングルームでの直接の通話遅延よりも視聴遅延を確実に大きくする必要があります。
現在のTencent CloudのライブCDN技術では、TXLivePlayerプレーヤーを組み合わせると、下表のレイテンシー基準に達することができます。

| Relayed streaming型 | TXLivePlayerの再生モード |  平均レイテンシー | 実測効果 |
|:-------:|:-------:|:--------:|:---------:|
| 独立画面 | 超高速モード（推奨） | **2～3秒** | 下図の左側の比較図（オレンジ色）|
| 合成画面 | 超高速モード（推奨） | **4～5秒** | 下図の右側の比較図（青色）|

実測でレイテンシーが上表よりも大きい場合は、次のガイドに従ってレイテンシーの最適化を行うことができます。

- **TRTC SDKに付属のTXLivePlayerの使用**
ffmpegカーネルをベースとしてパッケージ化された通常のijkplayerまたはffmpegプレーヤーには、レイテンシーを調整する機能がありません。このタイプのプレーヤーを使用して上記のLVBストリームアドレスを再生する場合、レイテンシーは通常、制御できません。TXLivePlayerには、レイテンシーを調整する機能を備えた自社開発の再生エンジンがあります。

- **TXLivePlayerの再生モードの超高速モードへの設定**
超高速モードは、TXLivePlayerConfigという3つのパラメータを設定することで実装できます。例として、[iOS](https://intl.cloud.tencent.com/document/product/1071/38159#Delay)を取り上げます。
iOS端末のObjective-Cコードの例：
```
 // TXLivePlayerの再生モードを超高速モードに設定します
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // 最小バッファ1秒
    config.maxAutoAdjustCacheTime = 1; // 最大バッファ1秒
    [player setConfig:config];
    //ライブストリーミング再生の起動
```

<span id="expense"></span>
## 関連料金

CDNライブストリーミングを実装するための料金には、**視聴料金**および**トランスコード料金**が含まれます。視聴料金は基本料金で、トランスコード料金は[マルチ画面合成](#mixCDN)を使用したときのみ請求されます。

>!本文中の価格はあくまでも参考例です。価格と実際の状況が一致しない場合は、[LVB > 標準ライブストリーミング](https://intl.cloud.tencent.com/document/product/267/2819)の課金の説明に従ってください。

### 視聴料金：ライブCDNを視聴することで発生する料金

ライブCDNで視聴する場合、**LVB**は、視聴によって生成されたダウンストリームトラフィック/帯域幅料金を請求します。実際のニーズに応じて適切な課金方法を選択できます。デフォルトでは、トラフィック課金が適用されます。詳細については、[LVB >標準ライブストリーミング > トラフィック帯域幅](https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#traffic-and-bandwidth)課金の説明をご参照ください。


### トランスコード料金：マルチ画面合成が有効になっている場合に課金されます
[マルチ画面合成](#mixCDN)を有効にすると、ミクスストリーミングをデコードしてエンコードする必要があるため、別途ミクスストリーミングトランスコード料金が発生します。ミクスストリーミングトランスコードは、解像度とトランスコード所要時間に応じて課金されます。キャスターが使用する解像度が高く、マイク接続時間が長いほど（通常、マイク接続シーンにのみミクスストリーミングトランスコードが必要）、料金が高くなります。詳細については、 [LVB > LVBトランスコード](https://intl.cloud.tencent.com/document/product/39604)をご参照ください。

>例えば、[setVideoEncodrParam()](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam)を介して、キャスターのビットレート（videoBitrate）を1500kbpsに、解像度を720Pに設定します。キャスターがマイクを視聴者に1時間接続し、マイク接続期間中に [マルチ画面合成](#mixCDN)をオンにした場合、発生するトランスコード料金は、`0.0057米ドル/分 × 60分 = 0.342米ドル`となります。

## よくあるご質問
**ルームに人が1人しかいないのに、画面が遅くなったり、ぼやけたりするのはなぜですか。**
`enterRoom`の中のTRTCAppSceneのパラメータを**TRTCAppSceneLIVE**と指定してください。
VideoCallモードはビデオ通話用に最適化されているため、ルーム内にユーザーが1人しかいない場合、ユーザーのネットワークトラフィックを節約するために低めのビットレートとフレームレートを維持するため、遅くなったり、ぼやけて見えたりします。
