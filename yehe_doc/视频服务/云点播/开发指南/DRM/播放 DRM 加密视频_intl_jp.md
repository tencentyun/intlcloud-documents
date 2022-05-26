## 学習目標

本段階のチュートリアルの学習は、ビデオのDRM暗号化方法、およびプレイヤーによる暗号化ビデオの再生方法を把握することを目的とします。

## 前提条件
本チュートリアルを開始する前に、次の前提条件を満たしていることを確認してください。

### VODの有効化
VODを有効化してください。手順は以下のとおりです：

1. [Tencent Cloudアカウント](https://intl.cloud.tencent.com/document/product/378/17985)を登録し、[実名登録](https://intl.cloud.tencent.com/document/product/378/3629)を行います。
2. VODサービスを購入します。詳細については、[課金概要](https://intl.cloud.tencent.com/document/product/266/2838)をご参照ください。
3. **クラウド製品**>**ビデオサービス**>[**VOD**](https://console.cloud.tencent.com/vod)を選択し、VODコンソールに入ります。

これで、VODの有効化の手順が完了しました。 

### FairPlay証明書の申請と提出
[FairPlay証明書の申請・提出方法](https://intl.cloud.tencent.com/document/product/266/46643)をご参照ください。正常にFairPlay証明書を提出した後、コンソールで証明書のURLを確認して取得し、それを今後のビデオの再生と使用に利用することができます。

## 手順1：ホットリンク防止の有効化

アカウントにおけるデフォルトの配信ドメイン名でKeyホットリンク防止を有効にしたケースを例にします。
>? ご利用中のネットワークドメイン名に対して直接ホットリンク防止を有効にしないでください。ご利用中のネットワークでビデオを再生できなくなる場合があります。

1. VODコンソールにログインし、【配信と再生の設定】>[【ドメイン名の管理】](https://console.cloud.tencent.com/vod/distribute-play/domain)を選択して、「デフォルトの配信ドメイン名」の【設定】をクリックします。【アクセス制御】をクリックして、設定画面に入ります。
   <img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
【Keyホットリング防止の有効化】をオンにし、【ランダムKeyの生成】をクリックしてランダムKeyを生成します。本チュートリアルは`testtest`で、生成されたKeyをコピーしてから、【OK】をクリックし、保存して有効にします。ホットリング防止Keyを後続の手順でのSuper Playerの署名の生成に使用することができます。
   ![image-KEY](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## 手順２：ビデオへのDRM暗号化

1. VODコンソールにログインし、**メディア資産管理**>[**ビデオ管理**](https://console.cloud.tencent.com/vod/media)を選択し、処理するビデオ（FileId 为387702299667618135）にチェックを入れて、**ビデオ処理**をクリックします。

   ![image-20220426211316803](https://qcloudimg.tencent-cloud.cn/raw/4eab2858c67f4efbf1383a3b03810428.png)

2. ビデオ処理の画面で：
 - **処理タイプ**は**タスクストリーム**を選択します。
 - **タスクストリームテンプレート**は**WidevineFairPlayPreset**を選択します。
 ![image-20220425192205432](https://qcloudimg.tencent-cloud.cn/raw/cef2c1e79343ea9688654791b6fb6762.png)

>?
>- WidevineFairPlayPresetは事前に設定されたタスクストリームです。具体的には、11番と13番のテンプレートを使用し、アダプティブストリームへのトランスコーディングを行い、10番テンプレートのスクリーンショットをカバーとして使用します。10番テンプレートのスクリーンショットはスプライトイメージです。
>- 11番テンプレートのアダプティブストリームは、暗号化タイプが「FairPlay」であるマルチビットレートの出力であり、13番テンプレートのアダプティブストリームは、暗号化タイプが「Widevine」であるマルチビットレートの出力です。

3. **OK**をクリックします。「ビデオ状態」欄が「処理中」から「正常」に変わると、ビデオの処理が完了します：
<img src="https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png" width="" />
4. ビデオの「操作」欄の下の**管理**をクリックし、管理画面に入ります：
 - 「基本情報」タグを選択すると、生成されたカバーとDRMで暗号化されたアダプティブストリームの出力（テンプレートIDは11と13）を確認できます。

   ![image-20220426201159056](https://qcloudimg.tencent-cloud.cn/raw/696e894ed0c3665990c12cc57ebf23bf.png)

 - 「スクリーンキャプチャ情報」タグを選択すると、生成したスプライトイメージ（テンプレートID：10）を確認できます。

   ![image-20220426201309975](https://qcloudimg.tencent-cloud.cn/raw/1a5878fd0286c46ef487bdf81ad8503a.png)

## 手順3：Super Playerの署名の生成

Super Playerの署名は、後続の再生情報の確認に使用されます。生成方法については、[Super Playerの署名ドキュメント](https://intl.cloud.tencent.com/document/product/266/38099)をご参照ください。本チュートリアルのSuper Player署名のPayLoadを以下に示します：

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

本チュートリアルのKeyが`testtest`である場合、生成されたSuper Playerの署名(`psign`)を以下に示します：

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

##  手順4：再生情報の確認

以下では、URLで再生情報を確認する方法について詳しく説明します。

確認リクエストはHTTP GETの方法で実行され、URLは`https://playvideo.qcloud.com/getplayinfo/v4/{appId}/{fileId}?psign={psign}`です。

ここで、`{appId}`はアプリケーションIDで、サブアプリケーションを使用した場合は、対応する[サブアプリケーションID](https://intl.cloud.tencent.com/document/product/266/33987)を入力し、fileIdは再生するビデオファイルのIDとします。

本チュートリアルは手順3で取得した`psign`を使用すると、リクエストURLは以下になります：

`https://playvideo.qcloud.com/getplayinfo/v4/1500012416/387702299667618135?psign=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

応答は以下になります：

```json
{
  "code":0,
  "message": "",
  "requestId": "9c7fab8704994c6b96375393e6544b5c",
  ...
  "media":{
	...
    "streamingInfo":{
      "drmOutput":[
        {
          "type": "FairPlay",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        },
        {
          "type": "Widevine",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        }
      ],
      "drmToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8",
      "widevineLicenseUrl": "https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2",
      "fairplayLicenseUrl": "https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2"
    },
    ...
  }
}
```



上記の応答構成から以下の再生情報を取得できます：

1. ビデオコンテンツのURL。
2. 再生ライセンスのアドレス（License Server URL）：
   - `Widevine`再生ライセンスのアドレス：` drmToken`は、query stringパラメータと`widevineLicenseUrl`を結合することで取得されます。
   - `FairPlay`再生ライセンスのアドレス：` drmToken`は、query stringパラメータと`fairplayLicenseUrl`を結合することで取得されます。

本チュートリアルの再生情報は以下のとおりです：

`Widevine`暗号化について：

- ビデオコンテンツのURLは`https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`です
- 再生ライセンスのアドレスは`https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`です

FairPlay暗号化について：

- ビデオコンテンツのURLは`https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`です
- 再生ライセンスのアドレスは`https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`です


## 手順5：プレイヤーによるDRM暗号化ビデオの再生。

以下では、プレーヤーを使用してWidevineおよびFairPlayで暗号化ビデオをそれぞれ再生する方法について説明します。

#### `Widevine`暗号化ビデオの再生

`Chrome`ブラウザを使用して[Shaka Playerオンラインプレーヤーページ](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled)を開きます。

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/e58eb9f3795a328b2ba01d15943389e7.png)

**+**をクリックし、`Manifest URL`の欄に手順3で取得したビデオコンテンツのURLを入力します。`Name`の欄には任意の値を入力でき、ここでは`Widevine`と入力します。

![image-20220426163853470](https://qcloudimg.tencent-cloud.cn/raw/0846706a160112ccea2712cd9c6b4d4c.png)

`Custom License Server URL`の欄に手順3で取得したWidevine再生ライセンスのアドレスを入力して、最後に**Save**ボタンをクリックします。

![image-20220426163939777](https://qcloudimg.tencent-cloud.cn/raw/702199c544c829db6f5d4815dcd4ff48.png)

保存すると、ページに`Widevine`という再生オプションが表示されます。

![image-20220426164129657](https://qcloudimg.tencent-cloud.cn/raw/7d70df750e283d8a5a0d42596e08c14b.png)

**Play**をクリックすると、復号化済みのビデオを再生できます。

#### `FairPlay`暗号化ビデオの再生

`Safari`ブラウザを使用して[Shaka Playerオンラインプレーヤーページ](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled)を開きます。

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/0b9b5ae58e65c6b3c0789b8d98af57a1.png)

**+**をクリックし、`Manifest URL`の欄に手順3で取得したビデオコンテンツのURLを入力します。`Name`の欄には任意の値を入力でき、ここでは`FairPlay`と入力します。

![image-20220426164907499](https://qcloudimg.tencent-cloud.cn/raw/70f01463b0afdf231dd014ea4782728f.png)

`Custom License Server URL`の欄に手順3で取得したFairPlay再生ライセンスのアドレスを入力し、`Custom License Certificate URL`の欄に上記の手順で設定した`FairPlay`証明書アドレス（コンソールで確認可能）を入力します。最後に**Save**ボタンをクリックします。

![image-20220426164950762](https://qcloudimg.tencent-cloud.cn/raw/bdd9c3ecd2882537df76d657768855e9.png)

保存すると、ページに`FairPlay`という再生オプションが表示されます。

![image-20220426165137520](https://qcloudimg.tencent-cloud.cn/raw/9da228ea1db9ab54a1631f605e24d806.png)

**Play**をクリックすると、復号化済みのビデオを再生できます。

## まとめ

本チュートリアルの学習を完了すると、ビデオのDRM暗号化方法、プレイヤーで暗号化されたビデオを再生する方法を把握したことになります。