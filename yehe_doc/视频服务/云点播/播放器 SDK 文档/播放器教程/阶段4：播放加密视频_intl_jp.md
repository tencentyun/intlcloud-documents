## 学習目標
この段階のチュートリアルを学習するとビデオを暗号化し、プレーヤーを使用して暗号化したビデオを再生する方法を理解、把握することができます。
お読みになる前に、プレーヤーガイドの [第1段階：オリジナルビデオの再生](https://www.tencentcloud.com/document/product/266/51564)の部分をすでに学習しているか確認してください。このチュートリアルでは、 [第1段階](https://intl.cloud.tencent.com/document/product/266/38098)でアクティブ化したアカウントとアップロードしたビデオを使用します。

## 手順1：ビデオの暗号化
1. VODコンソールにログインし、 **メディア資産管理**>[**オーディオビデオ管理**](https://console.cloud.tencent.com/vod/media)を選択し、処理するビデオ（FileIdは387xxxxx8142975036）にチェックを入れ、**タスクフロー**をクリックしてください。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/7ut4367_1.jpg" width="622" />

2. **メディア処理**インターフェースで
 - **処理タイプ**は**タスクストリーミング**を選択します。
 - **タスクフローのテンプレート**は**SimpleAesEncryptPreset**を選択します。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/GkuI523_2.jpg" width="" style="zoom:100%;" /><span>

>?
>- SimpleAesEncryptPresetはプリセットのタスクフローです。テンプレート12のアダプティブビットレートストリーム、テンプレート10のスクリーンキャプチャによるタイトル画像作成、テンプレート10のキャプチャしたスプライトイメージを使用します。
>- テンプレート12のアダプティブビットレートストリーミングはトランスコーディングして暗号化したマルチビットレートによる出力です。

3. **OK**をクリックし、[オーディオビデオ処理](https://console.cloud.tencent.com/vod/task)リストの「タスクステータス」が「処理中」から「完了」に変われば、ビデオの処理が完了したことを表します。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/hUM7408_3.png" style="zoom:80%;" />

4. メディア資産管理>[**オーディオビデオ管理**](https://console.cloud.tencent.com/vod/media)と進み、暗号化を開始したビデオエントリー右側の**管理**をクリックし、管理ページに進みます。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ETsG597_4.jpg" width="800" />

**基本情報** タブを選択します。
 - 生成したタイトル画像、および暗号化されたアダプティブビットレートストリーミングの出力を見ることができます（テンプレートID：12）。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/KBkV486_5.jpg" width="622" />
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/5NsV447_6.jpg" width="700" />

 **スクリーンキャプチャ情報** タブを選択します。
 - 生成したスプライトイメージを見ることができます（テンプレートID：10）。

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/XTu8560_7.jpg" width="700" />

### ステップ2：プレーヤー署名の生成
このステップでは、署名ツールを使用して速やかにプレーヤー署名を生成し、プレーヤーのビデオ再生に使用します。
**配信と再生の設定**>[**プレーヤー署名ツール**](https://console.cloud.tencent.com/vod/distribute-play/signature)を選択し、以下の情報を入力します。
 - **ビデオfileId**に**ステップ1**のFileId（387xxxxx8142975036）を入力します
 - **署名期限タイムスタンプ** プレーヤー署名の有効期間です。入力がなければ署名の有効期限が切れていないことを意味します
 - **再生可能なビデオタイプ**は**アダプティブビットレートストリーミング変換(暗号化)**を選択します
 - **暗号化タイプ**は**プライベート暗号化（SimpleAES）**を選択します
 - **再生可能なABSテンプレート**は`Adpative-HLS-Encrypt (12)`を選択します
 - **サムネイルプレビューに使用するスプライトイメージ** `SpriteScreenshot (10)`を選択します

**署名生成結果**をクリックし、署名結果文字列を取得します。

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
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Eapx633_9.png" width="800" />

### マルチプレーヤーDemo
プレーヤーの署名を取得した後、それぞれ、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android)、[iOS](https://github.com/LiteAVSDK/Player_iOS)という3つの端末のプレーヤーDemoで検証を行えます。詳細については、Demoのソースコードをご参照ください。


## まとめ

このチュートリアルの学習を終えると、ビデオの暗号化の方法、プレーヤーで再生する方法について理解できたことになります。
