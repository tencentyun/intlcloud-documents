## 学習目標
この段階のチュートリアルの学習を終えると、以下の内容を含むアダプティブビットレートストリーミングビデオを再生する方法について理解できたことになります。

* サブストリーム再生の仕様の最低解像度は480p、最高解像度は1080pです。
* ビデオの中間部分のスクリーンキャプチャを使用してビデオタイトル画像を作成します。
* プログレスバー上のサムネイルプレビューは、20%の間隔に調整します。

お読みになる前に、プレーヤーガイドの [第1段階：オリジナルビデオの再生](https://www.tencentcloud.com/document/product/266/51564)の部分をすでに学習しているか確認してください。このチュートリアルでは、 [第1段階](https://intl.cloud.tencent.com/document/product/266/38098)でアクティブ化したアカウントとアップロードしたビデオを使用します。

## 手順1：アダプティブビットレートストリーミングテンプレートの作成
1. VODコンソールにログインし、【メディアプロセッシングサービス設定】>[【テンプレート設定】](https://console.cloud.tencent.com/vod/video-process/template)を選択して、「アダプティブストリームトランスコーディングのテンプレート」のタブの下の【アダプティブストリームトランスコーディングのテンプレートの作成】をクリックします。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/PEXG353_1.png" width="800" />

2. 「テンプレート設定」画面に入って、【サブストリームの追加】をクリックし、サブストリーム1、サブストリーム2、サブストリーム3を新規作成して、以下のパラメータを入力します。
	- **基本情報モジュール**：
	  - 【テンプレート名】： MyTestTemplateと入力します。
	  - 【パッケージ化形式】：【HLS】を選択します。
	  - 【暗号化タイプ】：【非暗号化】を選択します。
	  - 【低解像度から高解像度への変換】：有効にしません。
	  - 【トランスコード方式】：【通常トランスコード】を選択します。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/9InI915_2.png" width="622" />

 - **サブストリーム情報モジュール**：
<table>
<thead>
<tr>
<th>サブストリーム番号</th>
<th>ビデオビットレート</th>
<th>解像度</th>
<th>フレームレート</th>
<th>オーディオビットレート</th>
<th>サウンドチャンネル</th>
</tr>
</thead>
<tbody><tr>
<td>サブストリーム1</td>
<td>512kbps</td>
<td>ビデオ長辺0px、ビデオ短辺480px</td>
<td>24fps</td>
<td>48kbps</td>
<td>ダブルサウンドチャンネル</td>
</tr>
<tr>
<td>サブストリーム2</td>
<td>512kbps</td>
<td>ビデオ長辺0px、ビデオ短辺720px</td>
<td>24fps</td>
<td>48kbps</td>
<td>ダブルサウンドチャンネル</td>
</tr>
<tr>
<td>サブストリーム3</td>
<td>1024kbps</td>
<td>ビデオ長辺0px、ビデオ短辺1080px</td>
<td>24fps</td>
<td>48kbps</td>
<td>ダブルサウンドチャンネル</td>
</tr>
</tbody></table>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/MxKn964_3.jpg" width="700" />

3. 【作成】をクリックすると、3つのサブストリームが含まれたABSテンプレートが生成されます。テンプレートIDは`1429212`です。

![](https://qcloudimg.tencent-cloud.cn/raw/1b1ffba4a8c37c8d81132e8f93c801b6.png)

## 手順2：スプライトイメージテンプレートの作成
1. VODコンソールにログインし、【ビデオ処理設定】>[【テンプレート設定】](https://console.cloud.tencent.com/vod/video-process/template)と選択して、「スクリーンキャプチャテンプレート」タグの下の【スクリーンキャプチャテンプレートの作成】をクリックします。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/hrUE650_5.png" width="700" />

2. 「テンプレート設定」画面に入ってから、テンプレートのパラメータを入力します。
 * 【テンプレート名】： MyTestTemplateと入力します。
 * 【テンプレートタイプ】：【スプライトイメージのスクリーンキャプチャ】を入力します。
 * 【小さい画像のサイズ】：726px × 240px。
 * 【サンプリング間隔】：20%。
 * 【小さい画像の行数】：10。
 * 【小さい画像の列数】：10。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LIw5399_6.png)

3. 【作成】をクリックすると、テンプレートIDが`131342`となるスプライトイメージテンプレートが生成されます。

![](https://qcloudimg.tencent-cloud.cn/raw/4cf44757d6dbb339aa29c3c29fc480d7.png)

## 手順3：タスクフローの作成と処理の実行
新しいABS生成テンプレート（ID ：1429212）とスプライトイメージテンプレート（ID：131342）を作成した後、新しいタスクフローを作成する必要があります。

1. VODコンソールにログインし、【ビデオ処理設定】>[【タスクフロー設定】](https://console.cloud.tencent.com/vod/video-process/taskflow)と選択して、【タスクフローの作成】をクリックします。
 * 【タスクフロー名】： MyTestProcedureと入力します。
 * 【タスクタイプ設定】：【アダプティブビットレートストリーミング】、【スクリーンキャプチャ】、【タイトル画像のスクリーンキャプチャ】にチェックを入れます。
	 *  【アダプティブビットレートストリーミングのタスク設定】のオプションタブで、【ABSテンプレートの追加】をクリックし、「ABSテンプレート/ID」欄で、**ステップ1**で作成したカスタムABS生成テンプレートMyTestTemplate(1429212)を選択します。
	 *  【スクリーンキャプチャタスク設定】のオプションカードで、【スクリーンキャプチャテンプレートの追加】をクリックします。「スクリーンキャプチャ方式」の欄は【スプライトイメージ】を選択し、「スクリーンキャプチャテンプレート」の欄は**手順2**で作成したカスタマイズスプライトイメージテンプレートMyTestTemplate(131342)を選択します。
	 *  【スクリーンキャプチャタイトル画像のタスク設定】のオプションカードで、【スクリーンキャプチャテンプレートの追加】をクリックします。「スクリーンキャプチャテンプレート」の欄は【TimepointScreenshot】を選択し、「時間ノードの選択」欄は【パーセンテージ】を選択して、50%と入力します。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Q6nQ449_8.png" width="900" />

2. 【サブミット】をクリックすると、MyTestProcedure という名前のタスクフローが生成されます。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/y7xz109_9.jpg)

3. コンソールで【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択し、処理するビデオ（FileIdは387xxxxx8142975036）にチェックを入れ、【ビデオ処理】をクリックします。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Mpj9208_10.jpg" width="622" />

4. ビデオ処理のポップアップボックスで：

 * 【処理タイプ】は【タスクフロー】を選択します。
 * 【タスクフローテンプレート】で【MyTestProcedure】を選択します。

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ctNZ059_11.png" width="500" />

5. **OK**をクリックし、[オーディオビデオ処理](https://console.cloud.tencent.com/vod/task)リストの「タスクステータス」が「処理中」から「完了」に変われば、ビデオの処理が完了したことを表します。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/IuU9256_12.jpg" width="800" />

6. メディア資産管理>[**オーディオビデオ管理**](https://console.cloud.tencent.com/vod/media)と進み、アダプティブビットレートストリーミングへのトランスコードを開始したビデオエントリー右側の**管理**をクリックし、管理ページに進みます。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/UBpg014_13.png" width="800" />

**基本情報** タブを選択します。
 - 生成したタイトル画像、およびアダプティブビットレートストリーミングの出力を見ることができます（テンプレートID： 1429212）。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/gtLx554_14.jpg" width="522" />
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/358v600_15.jpg" width="700" />

 **スクリーンキャプチャ情報** タブを選択します。
 - 生成したスプライトイメージを見ることができます（テンプレートID：131342）。

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/KiVV307_16.jpg" width="700" />

### ステップ4：プレーヤー署名の生成
このステップでは、署名ツールを使用して速やかにプレーヤー署名を生成し、プレーヤーのビデオ再生に使用します。
**配信と再生の設定**>[**プレーヤー署名ツール**](https://console.cloud.tencent.com/vod/distribute-play/signature)を選択し、以下の情報を入力します。
 - **ビデオfileId**に**ステップ3**のFileId（387xxxxx8142975036）を入力します
 - **署名期限タイムスタンプ** プレーヤー署名の有効期間です。入力がなければ署名の有効期限が切れていないことを意味します
 - **再生可能なビデオタイプ**は**アダプティブビットレートストリーミング変換(非暗号化)**を選択します
 - **再生可能なABSテンプレート**は`MyTestTemplate (1429212)`を選択します
 - **サムネイルプレビューに使用するスプライトイメージ**は`MyTestTemplate (131342)`を選択します

**署名生成結果**をクリックし、署名結果文字列を取得します。

## ステップ5：ビデオの再生
ステップ4で、ビデオ再生に必要な3つのパラメータである`appId`、`fileId` 、プレーヤー署名（`psign`）を取得しています。Web端末ビデオ再生は以下のとおりです。

### Web端末再生の例
[Web端末プレーヤー体験](https://tcplayer.vcube.tencent.com/)を開き、以下のとおり設定します。
 - **プレーヤー機能**は**ビデオ再生**を選択します
 - **FileID再生**タブをクリックします
 - **fileID**に前のFileId（387xxxxx8142975036）を入力します
 - **appID**にファイルが所属するappId（前のステップで生成したプレーヤー署名ページのappID）を入力します
 - **psign**に前のステップで生成した署名結果文字列を入力します

**プレビュー** をクリックするとビデオを再生できます。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/V98D696_18.png" width="800" />

### マルチプレーヤーDemo
プレーヤーの署名を取得した後、それぞれ、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android)、[iOS](https://github.com/LiteAVSDK/Player_iOS)という3つの端末のプレーヤーDemoで検証を行えます。詳細については、Demoのソースコードをご参照ください。

## まとめ
このチュートリアルの学習を終えると、アダプティブビットレートストリーミングビデオを再生する方法について理解できたことになります。
- ビデオの暗号化と暗号化されたビデオを再生したい場合、[第4段階：暗号化したビデオの再生](https://www.tencentcloud.com/document/product/266/51556)をご参照ください。
