## 適用ケース
CDN relayed live streamingは、TRTC が UDPプロトコルを採用して音声ビデオデータの伝送を行い、標準的なLVB CDN が採用した RTM╲PHLS╲FLV などのプロトコルがデータ伝送を行っていることから、 TRTC の音声ビデオデータをライブ CDN に**Relayed**しなければ、視聴者がライブ CDNによって視聴することができません。

TRTCをCDNに接続して視聴することは、通常以下の2つの問題の解決に使用されます。
- **問題一：超高並列視聴**
TRTC の低遅延時の視聴能力は、シングルルームで最大10万人をサポートし、CDNは、遅延が若干多いものの、10万人以上の並列視聴をサポートしています。かつ、CDNにかかる費用は極めて安価です。
- **問題二：移動端末サイトによる再生**
TRTC は、 WebRTC プロトコルのアクセスをサポートしていますが、主に Chrome デスクトップ版ブラウザに使用されており、モバイル版ブラウザの兼用性は極めて扱いにくくなっています。とりわけ Android 携帯ブラウザの WebRTC に対するサポートは一般に劣っています。そのため、 Web ページによってモバイル端末でライブストリーミングコンテンツのシェアリングを希望する場合は、やはり HLS(m3u8)の 再生プロトコルの使用を推奨します。このことも、ライブ CDN の能力を介してHLS プロトコルをサポートすることが必要です。


## 原理解析
Tencent Cloudは、一連のRelayed Transcodingクラスタを使用し、TRTCの音声ビデオデータをライブ CDNシステムにRelayします。このクラスタは、TRTCが使用するUDPプロトコルを標準のライブストリーミング　RTMPプロトコルへの変換を担っています。
<span id="directCDN"></span>
**シングル画面のRelayed live streaming**
TRTC ルームにキャスターが一人しかいないときは、TRTC のRelayed Pushは標準の RTMP プロトコルのライブプッシュ機能と同じです。しかし、TRTC の UDP は、 RTMP に比較して弱ネットワーク時のイミュニティがより強くなります。
![](https://main.qcloudimg.com/raw/23ac68cb46b06cc4eb6000fa98500dc4.jpg)

<span id="mixCDN"></span>
**Mix画面のRelayed live streaming**
TRTC が最も得意とする領域は、音声ビデオのインタラクティブマイク接続です。一つのルームに同時に複数のキャスターがいて、CDN の視聴側が1チャネルの音声ビデオ画面の取出ししか希望しない場合は、 [クラウドミクスストリーミングサービス](https://intl.cloud.tencent.com/document/product/647/34618) を使用して、複数画面を1チャネルに統一する必要があります。その原理は下図のとおりです。
![](https://main.qcloudimg.com/raw/77eeed776e61c3a6bd0e1669e5747727.jpg)

> **マルチチャネルのCDN画面を直接再生しない理由は？**
>マルチチャネルの CDN 画面は、マルチ画面の遅延を揃えるという問題を解決するのが困難です。同時にマルチ画面が消費するダウンロードのトラフィックも単独画面よりも多くなるため、業務では通常クラウドミクスストリーミングの手段を採用しています。

## 前提条件
テンセントの [LVB](https://console.cloud.tencent.com/live) サービスはすでにアクティブになっています。国家の関連部門の要求に応じて、ライブストリーミング再生は、再生ドメイン名を設定する必要があります。具体的な操作は [自身のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

## 使用手順

<span id="step1"></span>
### 手順1：Relayed Push機能の起動

1.  [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2．左側ナビゲーションバーで【アプリケーション管理】を選択し、目標アプリケーションのある行の【機能設定】をクリックします。
3. 【Relayed Push設定】で【Relayed Pushの起動】の右側にある![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png)をクリックし、ポップアップした【Relayed Push機能の起動】ダイアログボックスの中から【Relayed Push機能の起動】をクリックすると、アクティブになります。

<span id="step2"></span>
### 手順2：再生ドメイン名を設定し CNAMEを完成
1. [LVBコンソール](https://console.cloud.tencent.com/live/)にログインします。
2. 左側ナビゲーションバーで【Domain Management】を選択すると、ドメイン名リストにPushドメイン名が新規追加されたことがわかります。フォーマットは `xxxxx.livepush.myqcloud.com`になります。このうち、 xxxxx は一つの数字で、 bizidといいます。TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】>【アプリケーション情報】から bizid 情報を探し出すことができます。
3. 【ドメイン名の追加】をクリックして、届出済みの再生ドメイン名を入力し、ドメイン名のタイプを【再生ドメイン名】に選択し、アクセラレーションエリア（デフォルトは【中国大陸】）を選択し、【確定】をクリックすれば完了です。
4. ドメイン名の追加が成功した後、システムは一つの CNAME ドメイン名（`.liveplay.myqcloud.com`を拡張子とする）を自動的にアサインします。CNAME ドメイン名は直接アクセスができませんので、ドメイン名のサービスプロバイダーでCNAME 設定を完了する必要があります。設定が有効になったら、クラウドのLVBサービスを楽しむことができるようになります。具体的な操作は [CNAME 設定](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。

> **Pushドメイン名の追加は必要ありません**。 [手順1](#step1) でRelayed live streaming機能を起動した後、クラウドはデフォルトでLVBコンソールにフォーマットが `xxxxx.livepush.myqcloud.com` のプッシュドメイン名を追加します。このドメイン名はTencent CloudライブストリーミングサービスおよびTRTCサービスとの間で取り決めたデフォルトのプッシュドメイン名であり、当面修正をサポートすることはありません。

<span id="step3"></span>
### 手順3： TRTC に関連するstreamIdへのオーディオ・ビデオストリーミング
Relayed Push機能を起動した後、TRTCルームの各チャネル画面には1チャネルに対応するplayback URLを公開し、そのアドレスのフォーマットは以下のとおりです。
```
http://再生ドメイン名/live/[streamId].flv
```
アドレスの streamId は、ライブストリーミングで唯一の一本のライブストリーミングを表示するもので、自ら streamIdを指定することもできますし、システムのデフォルトを使用して生成することもできます。

#### 方式一： streamIdのカスタマイズ指定
 `TRTCCloud` の `enterRoom` 関数をコールするとき、そのパラメータ `TRTCParams` の `streamId` パラメータによってライブストリームIDを指定することができます。
 iOS 側の Objective-C コードの例：

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC 的 SDKAppID、アプリケーション作成後、取得可
param.roomId   = 1001;           // ルームナンバー
param.userId   = @"rexchang";    // ユーザー名
param.userSig  = @"xxxxxxxx";    // 署名ログイン
param.role     = TRTCRoleAnchor; // ロール：キャスター
param.streamId = @"stream1001";  // ストリーミング ID
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; //  LIVE モードを使用してください
```
- `userSig`の計算方法は [ UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

#### 方式二： システムの指定streamId
Auto-Relayed Pushを起動後、 streamIdをカスタマイズ指定していない場合、システムは生成された既定の 1個のstreamIdをデフォルトとします。生成規則は次のとおりです。

- ** streamId を使用したフィールドの組立**
  - sdkAppID:  [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】から見つかります。
  - bizid:  [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】から見つかります。
  - roomId： `enterRoom` 関数のパラメータ `TRTCParams` から指定します。
  - userId： `enterRoom` 関数のパラメータ `TRTCParams` から指定します。
  - streamType： カメラ画面は main、スクリーンは aux （WebRTC は、同時に1チャネルのアップストリームしかサポートできないため、 WebRTC のスクリーンシェアリングのストリーミング型は main）をシェアします。

- ** streamId 組立の計算ルール**
 <table>
<tr>
<th>組立</th>
<th>2020年01月09日以降に作成したアプリケーション</th>
<th>2020年01月09日よりも前に作成し使用したことのあるアプリケーション</th>
</tr>
<tr>
<td>組立ルール</td>
<td>streamId = urlencode(sdkAppId_roomId_userId_streamType)</td>
<td>StreamId = bizid_MD5(roomId_userId_streamType)</td>
</tr>
<tr>
<td>計算例</td>
<td>例：sdkAppId = 12345678，roomId = 12345，userId = userA，ユーザーが現在使用しているカメラ。<br>そうであれば：streamId = 12345678_12345_userA_main</td>
<td>例：bizid = 1234，roomId = 12345，userId = userA，ユーザーが現在使用しているカメラ。<br>でそうであれば：streamId = 1234_MD5(12345_userA_main) = 1234_8D0261436C375BB0DEA901D86D7D70E8</td>
</tr>
</table>


<span id="step4"></span>
### 手順4：マルチチャネル画面を制御するMix案

ミックス後のライブ画面を取得したい場合は、 TRTCCloud の `setMixTranscodingConfig` インターフェースをコールしてCloud MixTranscodingを起動する必要があります。このインターフェースのパラメータ `TRTCTranscodingConfig` は設定に使用することができます。
 - 各サブ画面の配置位置およびその大きさ。
 - ミックス画面の画面品質およびコードパラメータ。

画面にレイアウトした詳細設定方法は、 [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)をgosannshou ください。すべてのフローに関係する各コンポーネントの関係は [原理解析](#mixCDN)を参照することができます。

> `setMixTranscodingConfig` は、端末でミクスストリーミングをするものではなく、ミクスストリーミング設定をクラウドに発送するものです。クラウドサーバーでミクスストリーミングおよびトランスコードを行います。ミクスストリーミング及びトランスコードを元の動画データにデコードおよびリエンコードすることから、処理時間はより長くなるため、ミックス画面の実際の視聴レイテンシーは独立画面よりも1s - 2s長くなります。

<span id="step5"></span>
### 手順5：再生アドレスの取得および接続再生
 [手順2](#step2) で再生ドメイン名の設定を終え、 [手順3](#step3) で streamId のマッピングを終えると、LVBの再生アドレスを取得することができます。再生アドレスの標準フォーマットは次のとおりです。
```
http://再生ドメイン名/live/[streamId].flv
```

例：再生ドメイン名は`live.myhost.com`で、ルーム（1001）のユーザー userA のライブストリームID は入室パラメータによって streamId = "streamd1001"に指定します。
これによって、3チャネルの再生アドレスを取得できます。
```
 rtmp プロトコルの再生アドレス：rtmp://live.myhost.com/live/streamd1001
 flv プロトコルの再生アドレス：rtmp://live.myhost.com/live/streamd1001.flv
 hls プロトコルの再生アドレス：rtmp://live.myhost.com/live/streamd1001.m3u8
```

 `http` を接頭辞とし、 `.flv` を接尾辞とする **http - flv** アドレスを推奨します。このアドレスでの再生は、レイテンシーが低く、インスタントブロードキャスティング効果が高く、信頼性に優れた特徴があります。
再生プレイヤーの選択では、下表のガイドプランを推奨します。

| 属するプラットフォーム  | API 概要 | サポートするフォーマット|
|:-------:|:-------:|-------|
| iOS App|   TXLivePlayer(iOS) | 推奨 FLV |
| Android App | TXLivePlayer(Android) | 推奨 FLV |
| Webブラウザ |  - |  デスクトップ端末 Chrome ブラウザは FLV <br> Mac 端末 Safariをサポートし、モバイル携帯ブラウザは HLSしかサポートしていません |
|WeChat Mini Program|   [&lt;live-player&gt; タグ](https://developers.weixin.qq.com/miniprogram/en/dev/component/live-player.html)| 推奨 FLV |


<span id="step6"></span>
### 手順6：再生遅延の最適化

Relayed live streaming起動後の http - flv アドレスは、ライブ CDNの拡散および分散によって、視聴レイテンシーは直接 TRTC のLVBでの通話時のレイテンシーよりも確実に高くなります。
現在のTencent Cloudのライブ CDN技術を基に、TXLivePlayer プレイヤーを組み合わせると、下表の遅延基準に到達できます。

| Relayed streaming型 | TXLivePlayer の再生モード |  平均レイテンシー | 実測効果 |
|:-------:|:-------:|:--------:|:---------:|
| 独立画面 | クイックモード（推奨） | **2s - 3s** | 下図の左側の比較図（オレンジ色）|
| Mix画面 | クイックモード（推奨） | **4s - 5s** | 下図の右側の比較図（青色）|

下図の実測効果は、同じ一組の携帯電話を採用しており、左側の iPhone 6s は TRTC SDK を使用してライブストリーミングを行い、右側のシャオミー6は TXLivePlayer を使用して FLV プロトコルのライブストリーミングを再生します。


実測で遅延が上表よりもさらに大きい場合は、以下のガイドに従って遅延の最適化を行うことができます。

- ** TRTC SDK 標準装備の TXLivePlayerの使用**
通常の ijkplayer または ffmpeg は、 ffmpeg のコアを基にパッケージした再生プレイヤーであり、レイテンシーの調整能力が劣るため、この種のプレイヤーで上述のLVBストリーミングアドレスを再生する場合は、レイテンシーは一般に制御できません。TXLivePlayer には、自社開発した再生エンジンがあり、レイテンシーの調整能力を備えています。

- ** TXLivePlayer の再生モードのクイックモードへの設定**
 TXLivePlayerConfig の3パラメータを設定することで、クイックモードを実現できます。 iOS の場合：
 iOS 側の Objective-C コードの例：
```
 //  TXLivePlayer の再生モードをクイックモードに設定します
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // 最小バッファ1s
    config.maxAutoAdjustCacheTime = 1; // 最大バッファ1s
    [player setConfig:config];
    //ライブストリーミング再生の起動
```

<span id="expense"></span>
## 関連料金

CDN relayed live streamingを実現するための料金には、**視聴料金**および**トランスコーディング料金**が含まれます。視聴料金は、基本料金であり、トランスコーディング料金は [マルチ画面Mix](#mixCDN)を使用したときのみ徴収します。

>本文中の価格はサンプルであり、参考用にすぎません。価格と実際が一致しない場合は、 [LVB > 標準ライブストリーミング](https://intl.cloud.tencent.com/document/product/267/2819) の料金説明に準じます。

### 視聴料金：ライブ CDN を視聴することで発生する料金

ライブ CDN を視聴するとき、**クラウドLVB**は視聴したことで発生したダウンストリームトラフィック／帯域幅の費用を徴収します。実際のニーズに合わせて適切な個人料金方式を選択し、デフォルトでのトラフィック料金を採用することができます。


### トランスコーディング料金：マルチ画面のMixを作動時に徴収
 [マルチチャネル画面Mix](#mixCDN) を作動させた場合は、Mixはデコーディングとコーディングする必要があるため、想定外のMixTranscoding料金が発生することがあります。MixTranscodingは、解像度の大きさおよびトランスコーディング時間によって計算され、キャスター用の解像度が高く、マイク接続時間（通常はマイク接続のシーンではMixTranscodingが必要です）が長いほど、料金は高くなります。

## よくあるご質問
**ルームに一人しかいないときでも、画面が遅くぼやける理由は？**
`enterRoom` の中のTRTCAppSceneのパラメータを **TRTCAppSceneLIVE**と指定してください。
VideoCallモードではビデオ通話を対象に最適化を行っています。このため、ルーム内にユーザーが1人しかいない時は、ユーザーのネットワークトラフィックを節約するため、低めのビットレートとフレームレートを維持しますので、見たところ止まったりぼやけたりしているように感じられます。
