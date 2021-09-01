UDP伝送プロトコルのTRTCサービスを基に、プロトコル転換によってオーディオ・ビデオストリームを標準的なライブCDNシステム上に接続できます。このプロセスを「Relayed push」または「Relayed live streaming」と呼びます。
TRTCコンソールでRelayed live streaming機能を起動し、同機能が起動すると、TRTCルームにある各チャネルのオーディオ・ビデオストリームを自動的に取得します。同時に、 TRTCCloudで提供する **setMixTranscodingConfig** インターフェースを通じてCloud MixTranscodingを起動します。こうして、複数チャネル画面を一つのライブストリーミング上に合成することができます。

以下、Tencent CloudのLVB CDNシステムにて、標準的な**http + flv** プロトコルを通じてTRTCルームの各オーディオ・ビデオストリームを視聴する方法を主に紹介します。


## Demo
Tencent Real-Time Communication[Demo](https://intl.cloud.tencent.com/document/product/647/35076) にRelayed live streaming機能を追加しており、ビデオ通話の途中で【その他の機能】をクリックしてその機能の体験エントリー（再生プレイヤー TXLivePlayer のダウンロードアドレスはMLVBページを参照）を探すことができます。

## サンプルコード

| 所属プラットフォーム |  CDN 視聴アドレス計算 | クラウドミクスストリーミングパラメータの設定 |
|---------|---------|---------|
| iOS | ファイル：TRTCMoreViewController.m<br>関数：onBtnClick() | ファイル：TRTCMainViewController.m<br>関数：updateCloudMixtureParams() |
| Android | ファイル：CdnPlayManager.java<br>関数：initPlayUrl() | ファイル：TRTCRemoteUserManager.java<br>関数：updateCloudMixtureParams() |
| Windows（C++） |  ファイル：[TRTCSettingViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCSettingViewController.cpp)<br>関数：NotifyOtherTab | ファイル：[TRTCCloudCore.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/sdkinterface/TRTCCloudCore.cpp)<br>関数：updateMixTranCodeInfo() |
| Windows（C#） |  ファイル：[TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs)<br>関数：OnShareUrlLabelClick| ファイル：[TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs)<br>関数：UpdateMixTranCodeInfo() |
| Mac |  現時点で無し | ファイル：TRTCMainWindowController.m<br>関数：updateCloudMixtureParams() |

## ユースケース
Relayed live streaming機能に基づき、メインストリームのライブストリーミングプラットフォームによく見られるホストマイク接続およびライブストリーミングのPK機能を実現することができます。

1. ホストは、 TRTCCloud の `enterRoom()` インターフェースを通じて、一つの TRTCルームを新規作成できます。  `connectOtherRoom()` インターフェースを通じてその他のルームのホストとリアルタイムビデオのマイク接続PKを行えます。現在のアカウントは“Relayed live streaming”機能を起動してから、そのルームに対応する1チャネルのライブストリーミングのCDN playback URLを取得することができます（推奨：http - flv プロトコル、インスタントブロードキャスティングのパフォーマンスは良好）。
2. 視聴者は、 TXLivePlayer 再生プレイヤーを通してこのチャネルの playback URLで視聴でき、 TRTCCloud の `enterRoom()` インターフェースを通じてホストの現在の TRTCルームに入ることもでき、ホストとリアルタイムでのビデオマイク接続が行えます。
4. ホストは、マイク接続またはPK状態に入ってから、 TRTCCloud の `setMixTranscodingConfig()` インターフェースを通じて、オーディオミクスストリーミング（すなわち、マルチチャネルビデオ画面を1チャネルにミキシング）を通知し、元のCDN playback URLのビデオ画面を一人用画面から多人数用の混合画面に切り替えることができます。その過程で、視聴を続ける視聴者はライブCDN playback URLを切り替える必要はありません。
5. マイク接続が終了後、ホストは再度 `setMixTranscodingConfig()` インターフェースをコールしてミクスストリーミングを閉鎖し、 CDN playback URLのビデオ画面を一人用画面に戻すことができます。

## 使用手順

### 手順1：サービスのアクティブ化

[Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/rav) にログイン。目標のアプリケーションカードをクリックし、【機能設定】を選択すれば、“Auto-relay Live Streaming”機能を起動できます。この機能を起動する前提は、先ずTencent Cloudの [Live Video Broadcasting](https://console.cloud.tencent.com/live) サービスをアクティブにする必要があります。

### 手順2：独立画面

Relayed live streaming機能を起動した後、TRTCルームの各チャネル画面には1チャネルに対応するplayback URLをデプロイし、そのアドレスのフォーマットは以下のとおりです：
```
http://[bizid].liveplay.myqcloud.com/live/[streamid].flv
```

このうち、`bizid`、`streamid` は記入する必要がある部分です。具体的に記入するルールは次のとおりです。

- bizid： ライブストリーミングサービスと関係する一つの数字です。 [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/rav) で新規作成済みのアプリケーションを選択し、【アカウント情報】をクリックしてから“ライブストリーミング情報”で取得します。

- ストリーム型：カメラ画面のストリーム型は mainで、画面共有のストリーム型は aux（例外はあります。 WebRTC 側が同時にチャネルのアップストリームだけをサポートするため、WebRTC 上では画面共有のストリーム型も mainになります）です。
- `streamid = bizid_MD5 (ルームナンバー_userId_ストリーム型)`，つまり、`bizid`、`_`および`“ルームナンバー_userId_ストリーム型”から MD5 の結果`を計算し合成します。


以下のサンプルによって一次計算プロセスを詳細に提示し、このサンプルから自身のCDN playback URLを計算します。
```
例：bizid = 8888，Relayed live streamingのルームナンバーの実行 = 12345、userId = userA，ユーザーが現在カメラを使用。

1.  MD5(12345_userA_main) の計算= 8d0261436c375bb0dea901d86d7d70e8
2．合成後、userA　この1チャネルのTencent Cloud　CDN視聴アドレスは次のとおりです：
 flv プロトコル：http://8888.liveplay.myqcloud.com/live/8888_8d0261436c375bb0dea901d86d7d70e8.flv
 hls プロトコル：http://8888.liveplay.myqcloud.com/live/8888_8d0261436c375bb0dea901d86d7d70e8.m3u8
```

>! 上述のサンプルでは、`[bizid].liveplay.myqcloud.com` この部分は再生ドメイン名と呼ばれます。国の関係部門の要求に応じて、アプリケーション市場でAppのリリースを希望する場合は、ご自身が申請した再生ドメイン名を必ず使用し、設定方法は簡単にして、 “LVBコンソール > [Domain Management](https://console.cloud.tencent.com/live/domainmanage)” インターフェースで自身の再生ドメイン名を追加しさえすればOKです。 `[bizid].liveplay.myqcloud.com` ドメイン名は、デバッグにのみ使用し、同時にTencent Cloudがそのドメイン名を徐々に回収していますので、将来の可用性は保証できません。

### 手順3：ミックス画面

ミックス後のライブ画面を取得したい場合は、 TRTCCloud の `setMixTranscodingConfig` インターフェースをコールしてCloud MixTranscodingを起動する必要があります。このインターフェースのパラメータ `TRTCTranscodingConfig` は設定に使用することができます。
 - 各サブ画面の配置位置およびその大きさ。
 - ミックス画面の画面品質およびコードパラメータ。

設定方法の詳細は[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)をご参照ください。
>! `setMixTranscodingConfig` は、端末でミクスストリーミングをするものではなく、ミクスストリーミング設定をクラウドに発送するものです。クラウドサーバーでミクスストリーミングおよびトランスコードを行います。ミクスストリーミング及びトランスコードを元の動画データにデコードおよびリエンコードすることから、処理時間はより長くなるため、ミックス画面の実際の視聴レイテンシーは独立画面よりも1s - 2s長くなります。

### 手順4：再生接続

 `http` を接頭辞にして `.flv` を接尾辞とする **http - flv** アドレスをお薦めします。このアドレスによる再生は、レイテンシーが低く、インスタントブロードキャスティングが良く、かつ安定性に優れるという特徴があります。再生プレイヤーには、 TRTC SDK にパッケージされている TXLivePlayer 再生プレイヤーの使用を推奨します。この再生プレイヤーは次のファイルを参照してください：
- TXLivePlayer(iOS)
- TXLivePlayer(Android)


### 手順5：遅延の最適化

Relayed live streaming後の http - flv アドレスを起動して、ライブCDN の拡散及び分配によって、レイテンシーでの視聴は、TRTC ライブルームでの直接通話のレイテンシーよりも確実に高まります。具体的なレイテンシーは、現在のTencent Cloudのライブ CDN技術に基づけば、 TXLivePlayer 再生プレイヤーと組み合わせ、下表のレイテンシー基準になります。

| バイパスストリーム型 | TXLivePlayer の再生モード |  平均レイテンシー|
|:-------:|:-------:|:--------:|
| 独立画面 | クイックモード（推奨） | **2s - 3s** |
| ミックス画面 |クイックモード（推奨） | **4s - 5s** |


実測中に確認したレイテンシーが上表よりも大きい場合は、以下のガイドに従ってレイテンシーを最適化できます：

- ** TRTC SDK 標準装備の TXLivePlayerの使用**
通常の ijkplayer または ffmpeg を使用してこれらのライブストリーミングアドレスを再生する場合は、 ffmpeg のコアを基にパッケージした再生プレイヤーであり、レイテンシーの調整能力が劣るため、レイテンシーは一般に制御できません。TXLivePlayer には、自社開発した再生エンジンがあり、レイテンシーの調整能力を備えています。

- ** TXLivePlayer の再生モードのクイックモードへの設定**
 TXLivePlayerConfig の3パラメータを設定することでクイックモードを実現できます。 iOS を例にとれば、以下の通りコードを設定します。
    ```
    //  TXLivePlayer の再生モードをクイックモードに設定します
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // 最小バッファ1s
    config.maxAutoAdjustCacheTime = 1; // 最大バッファ1s
    [player setConfig:config];
    //ライブストリーミング再生の起動
    ```

## よくあるご質問
**ルームに一人しかいないときでも、画面が遅くぼやける理由は？**
 `enterRoom` の TRTCAppScene パラメータを **TRTCAppSceneLIVE**に指定してください。VideoCall モードは、ビデオ通話を最適化しますので、部屋に一人しかいなくても、画面は低いビットレートおよびフレームレートを維持してユーザーのネットワークトラフィックを節約するため、見た目では遅くぼやけて見えます。
