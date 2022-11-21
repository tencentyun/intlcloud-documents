## 学習目標

この段階のチュートリアルを学習すると、ビデオをDRMで暗号化する方法と、暗号化されたビデオを再生するプレーヤーを使用する方法を理解、把握することができます。

##  前提条件
本チュートリアルを開始する前に、次の前提条件を満たしていることを確認してください。

### VODをアクティブ化する
VODをアクティブにする必要があります。手順は以下のとおりです。

1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了します。
2. VODサービスを購入します。詳細については、[課金概要](https://intl.cloud.tencent.com/document/product/266/2838)をご参照ください。
3. **クラウド製品**>**Video Service**>[**VOD**](https://console.cloud.tencent.com/vod)を選択し、VODコンソールに進みます。

これで、VODのアクティブ化の手順が完了しました。 

### FairPlay証明書情報の申請

[FairPlay証明書情報の申請方法](https://intl.cloud.tencent.com/document/product/266/46643)をご参照ください。

### FairPlay証明書情報の提出

[華曦達コンソールでのFairPlay証明書情報の申請方法](https://intl.cloud.tencent.com/document/product/266/49665)をご参照ください。

### 華曦達ユーザーキー情報の設定

[華曦達ユーザーキー情報の設定](https://intl.cloud.tencent.com/document/product/266/49666)をご参照ください。

## ステップ1：リンク不正アクセス防止の有効化

アカウントにおけるデフォルトの配信ドメイン名でKeyリンク不正アクセス防止を有効にしたケースを例にします。
>? 現在使用中のネットワークドメイン名に対して直接リンク不正アクセス防止を有効にしないでください。現在のネットワークのビデオが再生できなくなります。

1. VODコンソールにログインし、【配信と再生の設定】 >[ 【ドメイン名管理】 ](https://console.cloud.tencent.com/vod/distribute-play/domain)を選択し、「デフォルト配信ドメイン名」の【設定】をクリックし、【アクセス制御】をクリックして設定画面に進みます。
   <img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. 【Keyリンク不正アクセス防止の有効化】を開き、【ランダムKeyの生成】をクリックしてランダムKeyを生成します。生成したKeyをコピーしてから、【OK】をクリックすると保存が有効になります。リンク不正アクセス防止Keyは、次のステップでプレーヤーの署名を生成するため使用することができます。
   ![image-KEY](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## ステップ2：ビデオのDRM暗号化

1. VODコンソールにログインし、**メディア資産管理**>[**ビデオ管理**](https://console.cloud.tencent.com/vod/media)を選択し、処理するビデオ（FileIdは387702299667618135）にチェックを入れ、**ビデオ処理**をクリックしてください。

   ![image-20220426211316803](https://qcloudimg.tencent-cloud.cn/raw/4eab2858c67f4efbf1383a3b03810428.png)

2. ビデオ処理の画面で：
 - **処理タイプ**は**タスクフロー**を選択します。
 - **タスクフローテンプレート**は、**WidevineFairPlayPreset**を選択します。
 ![image-20220425192205432](https://qcloudimg.tencent-cloud.cn/raw/cef2c1e79343ea9688654791b6fb6762.png)

>?
>? WidevineFairPlayPresetはプリセットのタスクフローです。テンプレート11、13をそれぞれ使用してアダプティブビットレートストリーミングに変換し、テンプレート10のスクリーンキャプチャによりタイトル画像を作成し、テンプレート10でスプライトイメージをキャプチャします。
>- テンプレート11のアダプティブビットレートストリーミングは暗号化タイプ`FairPlay`のマルチビットレート出力で、テンプレート13のアダプティブビットレートストリーミングは暗号化タイプ`Widevine`のマルチビットレート出力です。

3. **OK**をクリックし、「ビデオステータス」欄が「処理中」から「正常」に変わり、ビデオ処理完了と表示されるのを待ちます。
<img src="https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png" width="" />
4. ビデオ「操作」バーの下の**管理**をクリックし、管理ページに進みます。
 - 「基本情報」タグを選択すると、生成したタイトル画像、およびDRMで暗号化されたアダプティブビットレートストリーミングの出力（テンプレートID：11、13）を見ることができます。

   ![image-20220426201159056](https://qcloudimg.tencent-cloud.cn/raw/696e894ed0c3665990c12cc57ebf23bf.png)

 - 「スクリーンキャプチャ情報」タグを選択すると、生成したスプライトイメージ（テンプレートID：10）を見ることができます。

   ![image-20220426201309975](https://qcloudimg.tencent-cloud.cn/raw/1a5878fd0286c46ef487bdf81ad8503a.png)

### ステップ3：プレーヤー署名の生成

プレーヤー署名は、今後の再生情報の照会に使用されます。生成方法については、[プレーヤー署名ドキュメント](https://intl.cloud.tencent.com/document/product/266/38099)をご参照ください。このチュートリアルのプレーヤー署名のPayLoadは以下のとおりです。

```json
{
  "appId": 1500012416,
  "fileId": "387702299667618135",
  "currentTimeStamp": 1650886156,
  "expireTimeStamp": 1966435200,
  "urlAccessInfo": {
    "t": "75356B80",
    "us": "72d4cd1101"
  },
  "pcfg":"advanceDrmPreset"
}
```

このチュートリアルのKeyが`testtest`の場合、生成されるプレーヤー署名(`psign`)は以下のようになります。

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`


## ステップ4：プレーヤーを使用して、DRMで暗号化されたビデオを再生します。

### Web端末

#### VODプレーヤーを使用して再生します

プレーヤーの初期化時に必要な再生ファイルのパラメータを渡すだけで、DRMで暗号化されたビデオを再生できます。


### ステップ1：ページでファイルを導入します

適切な場所にプレーヤースタイルファイルと関連スクリプトファイルを導入します。

```
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.3/tcplayer.min.css" rel="stylesheet">
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.3/libs/hls.min.1.1.5.js"></script>
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.3/tcplayer.v4.5.3.min.js"></script>
```

### ステップ2：プレーヤーコンテナを配置します

プレーヤーを表示する必要がある画面の場所に、プレーヤーコンテナを追加します。コードは以下のとおりです。

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>? コンテナIDや幅・高さはカスタマイズできます。

#### ステップ3：初期化コード

画面初期化用のコードに、以下の初期化スクリプトを追加し、必要な初期化パラメータを渡します。コードは以下のとおりです。

```
var player = TCPlayer('player-container-id', {
    appID: '1500012416', // VODアカウントのappIDを渡してください（必須）
    fileID: '387702299667618135', // 再生したいビデオのfilIDを渡してください（必須）
    psign: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg',
    // その他のパラメータについては、開発ドキュメントhttps://intl.cloud.tencent.com/document/product/266/39105をご参照ください
});
```

### iOS端末
アクセスガイドの`FileId方式`の使用方法を参照して、DRMで暗号化されたビデオを再生してください。

>? アクセスする前にチケットを提出して、DRM機能をサポートするSDKの取得について、弊社までご連絡ください。

![](https://qcloudimg.tencent-cloud.cn/raw/fec2838bedc7d8748931e535fbcbb8ad.png)

### Android端末
アクセスガイドの`FileId方式`の使用方法を参照して、DRMで暗号化されたビデオを再生してください。

>? アクセスする前にチケットを提出して、DRM機能をサポートするSDKの取得について、弊社までご連絡ください。

 ![](https://qcloudimg.tencent-cloud.cn/raw/fb296ca490abe23bc6e63d021e694143.png)


## まとめ

このチュートリアルの学習を終えると、ビデオをDRMで暗号化する方法、およびプレーヤーを使用して暗号化後のビデオを再生する方法を理解できたことになります。

>? DRMまたは華曦達への接続プロセスで発生したいかなる問題についても、[お問い合わせ](https://console.cloud.tencent.com/workorder/category)からチケットを提出することができます。すべての工程でお客様の問題解決をサポートします。
