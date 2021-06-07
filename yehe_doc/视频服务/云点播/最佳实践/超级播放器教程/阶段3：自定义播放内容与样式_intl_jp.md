## 学習目標

本段階のチュートリアルを学習すると、Super playerで再生するビデオ内容と形式のカスタマイズの仕方を理解できるようになります。これには次が含まれます。

* サブストリーム再生の仕様の最低解像度は480p、最高解像度は1080pです。
* ビデオの中間部分のスクリーンキャプチャを使用してビデオタイトル画像を作成します。
* プログレスバー上のサムネイルプレビューは、20%の間隔に調整します。

これを読む前に、先にSuper playerガイドの[段階1：Super playerを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098) と[段階2：ホットリンク防止後のビデオ再生の有効化](https://intl.cloud.tencent.com/document/product/266/38292) 篇の部分を確実に学習しておくようにしてください。本チュートリアルでは [段階1](https://intl.cloud.tencent.com/document/product/266/38098) 篇でアクティブ化したアカウントおよびアップロードしたビデオを使用し、 [段階2](https://intl.cloud.tencent.com/document/product/266/38292)にしたがってホットリンク防止を有効化する必要があります。

## 手順1：アダプティブビットレートストリーミングテンプレートの作成

1. VODコンソールにログインし、【ビデオ処理設定】>[【テンプレート設定】](https://console.cloud.tencent.com/vod/video-process/template)と選択して、「アダプティブビットレートストリームテンプレート」のタグの下の【アダプティブビットレートストリーミングテンプレートの作成】をクリックします。
<img src="https://main.qcloudimg.com/raw/e9f8718aa8c6ae6dd05e4787cb76d586.png" width="800" />
2. 「テンプレート設定」画面に入って、【サブストリームの追加】をクリックし、サブストリーム1、サブストリーム2、サブストリーム3を新規作成して、以下のパラメータを入力します。
	- **基本情報モジュール**：
	  - 【テンプレート名】： MyTestTemplateと入力します。
	  - 【暗号化タイプ】：【非暗号化】を選択します。
	  - 【低解像度から高解像度への変換を許可するか】：有効にしません。
	  
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
<img src="https://main.qcloudimg.com/raw/755546d7ec20c5520f5f92adc6680e74.png" width="500" />
3. 【作成】をクリックすると、3つのサブストリームが含まれたアダプティブビットレートストリーミングテンプレートが生成されます。テンプレートID は125866です。

![](https://main.qcloudimg.com/raw/a7b09ef1aad0260a232dd55acaca6580.png)

## 手順2：スプライトイメージテンプレートの作成

1. VODコンソールにログインし、【ビデオ処理設定】>[【テンプレート設定】](https://console.cloud.tencent.com/vod/video-process/template)と選択して、「スクリーンキャプチャテンプレート」タグの下の【スクリーンキャプチャテンプレートの作成】をクリックします。
2. 「テンプレート設定」画面に入ってから、テンプレートのパラメータを入力します。
 * 【テンプレート名】： MyTestTemplateと入力します。
 * 【テンプレートタイプ】：【スプライトイメージのスクリーンキャプチャ】を入力します。
 * 【画像サイズ】：726px × 240px。
 * 【サンプリング間隔】：20%。
 * 【小さい画像の行数】：10。
 * 【小さい画像の列数】：10。
![](https://main.qcloudimg.com/raw/15c8b2a6fae675ea815ac7376ed83de6.png)
3. 【作成】をクリックすると、テンプレートIDが41377となるスプライトイメージテンプレートが生成されます。
![](https://main.qcloudimg.com/raw/df90feee40c75750e873ce53c6f4ddea.png)

## 手順3：タスクフローの作成と処理の実行

新しいアダプティブビットレートストリームテンプレート（ID：125866）とスプライトイメージテンプレート（ID：41377）を作成した後、新しいタスクフローを作成する必要があります。

1. VODコンソールにログインし、【ビデオ処理設定】>[【タスクフロー設定】](https://console.cloud.tencent.com/vod/video-process/taskflow)と選択して、【タスクフローの作成】をクリックします。
 * 【タスクフロー名】： MyTestProcedureと入力します。
 * 【タスクタイプ設定】：【アダプティブビットレートストリーミング】、【スクリーンキャプチャ】、【タイトル画像のスクリーンキャプチャ】にチェックを入れます。
	 *  【アダプティブビットレートストリーミングのタスク設定】のオプションカードで、【アダプティブビットレートストリーミングテンプレートの追加】をクリックし、「アダプティブビットレートストリーミングテンプレート/ID」欄で、**手順1**で作成したアダプティブビットレートストリームのカスタマイズテンプレートMyTestTemplate(126866)を選択します。
	 *  【スクリーンキャプチャタスク設定】のオプションカードで、【スクリーンキャプチャテンプレートの追加】をクリックします。「スクリーンキャプチャ方式」の欄は【スプライトイメージ】を選択し、「スクリーンキャプチャテンプレート」の欄は**手順2**で作成したカスタマイズスプライトイメージテンプレートMyTestTemplate(41377)を選択します。
	 *  【スクリーンキャプチャタイトル画像のタスク設定】のオプションカードで、【スクリーンキャプチャテンプレートの追加】をクリックします。「スクリーンキャプチャテンプレート」の欄は【TimepointScreenshot】を選択し、「時間ノードの選択」欄は【パーセンテージ】を選択して、50%と入力します。
<img src="https://main.qcloudimg.com/raw/dd707dadbb614868f999a4ef523a8636.png" width="900" />
2. 【サブミット】をクリックすると、MyTestProcedure という名前のタスクフローが生成されます。
![](https://main.qcloudimg.com/raw/e33008c55dcc18bed3b41f96d88c5c8c.png)
3. コンソールで【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択し、処理したいビデオ（FileId：528xxx3757278095）にチェックを入れ、【ビデオ処理】をクリックします。
4. ビデオ処理のポップアップボックスで：
 * 【処理タイプ】は【タスクフロー】を選択します。
 * 【タスクフローテンプレート】に【MyTestProcedure】を選択します。<span></span>
 <img src="https://main.qcloudimg.com/raw/3b2a2cf9f057cffe2caee84165a69d23.png" width="500" />
5. 【OK】をクリックし、**ビデオ状態**が“処理中”から“正常”に変わり、ビデオ処理完了と表示されるのを待ちます。
![](https://main.qcloudimg.com/raw/2894b49729ef223941360f2f814a63fa.png)
6. ビデオの「操作」バーの中の【管理】をクリックし、管理画面に入ります。
 * 【基本情報】欄で、生成したタイトル画像、およびアダプティブビットレートストリーミングの出力を見ることができます（テンプレートID：125866）。
 * 【スクリーンキャプチャ情報】欄で、生成したスプライトイメージを見ることができます（テンプレートID：41377）。

## 手順4：Super player設定の作成

カスタマイズしたアダプティブビットレートストリーミングとスプライトイメージを再生するために、カスタマイズしたプレーヤー設定を使用する必要があります。

1. VODコンソールにログインし、【配信と再生の設定】>[【Super player設定】](https://console.cloud.tencent.com/vod/distribute-play/super-player)と選択し、【新規作成】をクリックします。
2. Super player設定画面の中で、【アダプティブビットレートストリーミングテンプレートの追加】と【スプライトイメージテンプレートの追加】をそれぞれクリックし、その後以下のパラメータを記入します。
 * 【テンプレート名】： MyTestCfgと入力します。
 * 【再生に使用するアダプティブビットレートストリーミング】のオプションカードの「アダプティブビットレートストリーミングテンプレート/ID」欄は、MyTestTemplate(125866)を選択します。
 * 【再生に使用するスプライトイメージ】のオプションカードの「スクリーンキャプチャテンプレート」欄は、MyTestTemplate(41377)を選択します。
<img src="https://main.qcloudimg.com/raw/2459be6bd365e9a5143146d88d44a43c.png" width="400" />
3. 【OK】をクリックすると、新しいSuper player設 MyTestCfgが生成されます。

##   手順5：プレビューによる再生体験

これまでの手順で、ビデオに対する処理を行いました。ここでは、3種類の端末のSuper playerを使用して、再生の効果を素早く体験します。

1. [【ビデオ管理】](https://console.cloud.tencent.com/vod/media)の「アップロード済み」のタグを選択し、これまでの手順でアップロードおよび処理したビデオをさがして、「操作」バーの中の【管理】を選択し、「Super playerプレビュー」のタグを選択します。
2. 【再生設定】でMyTestCfgを選択します。
<img src="https://main.qcloudimg.com/raw/1518635e7f0b857e4406cd315e98ca3e.png" width="522" />
3. デフォルトの配信ドメイン名がホットリンク防止を有効にしているため、【再生制御】のオプションカードで、プレビュー時のホットリンク防止の期限切れ時間、テスト視聴時間などの選定をサポートしています。ここではデフォルトのパラメータを維持します（再生のホットリンク防止の期限切れ時間はデフォルトで1日、プレビュー時間、最大再生可能IP数は入力しません）。
 <img src="https://main.qcloudimg.com/raw/132832fdc9e28f4e1377b6cdaaee5b53.png" width="522" />

4. 【Webプレーヤー】の中で、プレーヤーの中間のボタンをクリックすると、 Web端末での再生が体験できます。

<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />


##  手順6：Demoを使用して検証

ホットリンク防止を有効にした後、ビデオを再生できるようにするためには、Super playerで有効期間内の署名を使用する必要があります。以下、署名ツールを使用して素早く署名を生成する方法を紹介します。

1. [Super player - 署名生成ツール](https://vods.cloud.tencent.com/signature/super-player-sign.html)の画面を開き、パラメータを入力します。
 * 【ユーザーappId】：ビデオが属するappId：1400xxx357を入力します（使用するのがサブアプリケーションの場合は、サブアプリケーションのappIdを入力します）。
 * 【ビデオfileId】：ビデオのFileId：528xxx3757278095を記入します。
 * 【現在のUnixタイムスタンプ】：ツールが自動生成した現在のUnix時間（1591756516）。入力不要です。
 * 【Super player設定】：カスタマイズしたSuper player設定名MyTestCfgを入力します。
 * 【署名期限切れUnix タイムスタンプ】：署名自身の期限切れ時間。未入力可、デフォルトは1日後に期限切れ。
 * 【リンク期限切れ時間】：Keyホットリンク防止期限切れ時間。6時間後の16進数Unix 時間：5ee09b44を入力します。
 * 【ホットリンク防止Key】：入力の前に取得したホットリンク防止Key：2WExxx48eWを入力します。
2. 【署名の生成】をクリックします。生成された署名が「署名生成結果」のテキストボックスに表示されます。

<img src="https://main.qcloudimg.com/raw/c7eff5906fbf01d8f28ec37119f8caf0.png" width="700" />
Super playerの署名を取得した後、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/tencentyun/SuperPlayer_Android)、[iOS](https://github.com/tencentyun/SuperPlayer_iOS)の3種類の端末のSuper playerのDemoを使用してそれぞれ検証することができます。具体的な内容は、Demoのソースコードをご参照ください。
>?コンソールの【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)>【Super playerプレビュー】の中で、プレビューのビデオに対応するWebプレーヤーのソースコードを取得でき、これを直接参照して使用できるようにしています。
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## まとめ

このチュートリアルの学習を終えると、Super playerで再生するビデオの内容と形式をカスタマイズする方法を把握できたことになります。
ビデオを暗号化し、暗号化後のビデオを再生したい場合は、 [段階4：暗号化したビデオの再生](https://intl.cloud.tencent.com/document/product/266/38294)をご参照ください。
