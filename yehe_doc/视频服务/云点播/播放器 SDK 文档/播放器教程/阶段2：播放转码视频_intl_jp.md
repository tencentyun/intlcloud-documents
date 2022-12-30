## 学習目標
この段階のチュートリアルを学習すると、ビデオをトランスコードし、プレーヤーを使用してトランスコードされたビデオを再生する方法を理解、把握することができます。
お読みになる前に、プレーヤーガイドの [第1段階：オリジナルビデオの再生](https://www.tencentcloud.com/document/product/266/51564)の部分をすでに学習しているか確認してください。このチュートリアルでは、 [第1段階](https://intl.cloud.tencent.com/document/product/266/38098)でアクティブ化したアカウントとアップロードしたビデオを使用します。

## ステップ1：ビデオトランスコード
1. VODコンソールにログインし、 **メディア資産管理**>[**オーディオビデオ管理**](https://console.cloud.tencent.com/vod/media)と選択し、処理するビデオ（FileIdは387xxxxx8142975036）にチェックを入れ、**トランスコード**をクリックしてください。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3unX216_1.png" width="800" />

2. **メディア処理**インターフェースで
 - **処理タイプ**は **トランスコード**を選択します
 - **トランスコードテンプレート**の**テンプレートの選択**をクリックします

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/U4VK178_2.png" width="522" />

ポップアップした **トランスコードテンプレートの選択** ページでテンプレート（テンプレート名は`STD-H264-MP4-540P`、IDは`100020`）を選択してください。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/xtzd936_3.png" width="622" />

**OK**をクリックしてトランスコードタスクを開始します。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pahm058_4.png" width="550" />

3. [**タスクセンター**](https://console.cloud.tencent.com/vod/task)に進み、**オーディオビデオ処理** タブをクリックし、リストの「タスクステータス」が「処理中」から「完了」に変われば、ビデオの処理が完了したことを表します。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Q4bA978_5.png" width="800" />

4. メディア資産管理>[**オーディオビデオ管理**](https://console.cloud.tencent.com/vod/media)と進み、トランスコードを開始したビデオエントリー右側の**管理**をクリックし、管理ページに進みます。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Mfdx017_6.png" width="800" />

**基本情報** タブを選択します。
 - **標準トランスコーディングリスト**でトランスコードに成功したトランスコードテンプレートリストを見ることができます

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/LJcj256_7.jpg" width="700" />

### ステップ2：プレーヤー署名の生成
このステップでは、署名ツールを使用して速やかにプレーヤー署名を生成し、プレーヤーのビデオ再生に使用します。
**配信と再生の設定**>[**プレーヤー署名ツール**](https://console.cloud.tencent.com/vod/distribute-play/signature)を選択し、以下の情報を入力します。
 - **ビデオfileId**に**ステップ1**のFileId（387xxxxx8142975036）を入力します
 - **署名期限タイムスタンプ** プレーヤー署名の有効期間です。入力がなければ署名の有効期限が切れていないことを意味します
 - **再生可能なビデオタイプ**は**オリジナルビデオ**を選択します
 - **再生可能なトランスコードテンプレート**は`STD-H264-MP4-540P (100020)`を選択します

**署名生成結果**をクリックし、署名結果文字列を取得します。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/SpCE136_8.png" width="800" />

## ステップ3：ビデオ再生
ステップ2で、ビデオ再生に必要な3つのパラメータである`appId`、`fileId` 、プレーヤー署名（`psign`）を取得しています。Web端末ビデオ再生は以下のとおりです。

### Web端末再生の例
[Web端末プレーヤー体験](https://tcplayer.vcube.tencent.com/)を開き、以下のとおり設定します。
 - **プレーヤー機能**は**ビデオ再生**を選択します
 - **FileID再生**タブをクリックします
 - **fileID**に前のFileId（387xxxxx8142975036）を入力します
 - **appID**にファイルが所属するappId（前のステップで生成したプレーヤー署名ページのappID）を入力します
 - **psign**に前のステップで生成した署名結果文字列を入力します

**プレビュー** をクリックするとビデオを再生できます。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/kzkm097_9.png" width="800" />

### マルチプレーヤーDemo
プレーヤーの署名を取得した後、それぞれ、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android)、[iOS](https://github.com/LiteAVSDK/Player_iOS)という3つの端末のプレーヤーDemoで検証を行えます。詳細については、Demoのソースコードをご参照ください。


## まとめ

このチュートリアルの学習を終えると、ビデオをトランスコードして、プレーヤーで再生する方法について理解できたことになります。
