## 学習目標
この段階のチュートリアルの学習を終えると、ビデオをVODにアップロードして、プレーヤーで再生する機能が理解できるようになります。

## 前提条件
本チュートリアルを開始する前に、次の前提条件を満たしていることを確認してください。

### VODのアクティブ化
ＶＯＤをアクティブ化する必要があります。手順は以下のとおりです。

1. [Tencent Cloudアカウント](https://intl.cloud.tencent.com/document/product/378/17985)を登録し、[実名登録](https://intl.cloud.tencent.com/document/product/378/3629)を行います。
2. VODサービスを購入します。具体的な方法は、[課金概要](https://intl.cloud.tencent.com/document/product/266/2838)をご参照ください。
3. **クラウド製品**>**ビデオサービス**>[**VOD**](https://console.cloud.tencent.com/vod)を選択し、VODコンソールに入ります。

これで、VODのアクティブ化の手順が完了しました。

## 手順1：ビデオをアップロードする
このステップでは、どのようにビデオをアップロードするかについて指導します。

1. VODコンソールにログインし、 **メディア資産管理**>[ **オーディオビデオ管理** ](https://console.cloud.tencent.com/vod/media)と選択して、**オーディオビデオのアップロード**をクリックします。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/eDZY097_1.jpg" width="722" />

2. アップロードインターフェースで、 **ローカルからのアップロード**を選択し、 **ファイルの選択**をクリックしてローカルビデオをアップロードします。その他の設定は以下のとおりです。
	- **ビデオ処理**は**アップロードのみ、ビデオ処理は実施しない**を選択します。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/zB6K038_2.jpg)

3. **アップロード開始**をクリックして、「アップロード中」ページに進み、 **ステータス**が**アップロード成功**に変わるとアップロードが完了したことを意味します。**ファイルID**はオーディオビデオをアップロードしたFileIdです（ここでは 387xxxxx8142975036）。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nMEx197_3.jpg)

### ステップ2：プレーヤー署名の生成
このステップでは、署名ツールを使用して速やかにプレーヤー署名を生成し、プレーヤーのビデオ再生に使用します。
**配信と再生の設定**>[**プレーヤー署名ツール**](https://console.cloud.tencent.com/vod/distribute-play/signature)を選択し、以下の情報を入力します。
 - **ビデオfileId**に**ステップ1**のFileId（387xxxxx8142975036）を入力します
 - **署名期限タイムスタンプ** プレーヤー署名の有効期間です。入力がなければ署名の有効期限が切れていないことを意味します
 - **再生可能なビデオタイプ**で**オリジナルビデオ**を選択します

**署名生成結果**をクリックし、署名結果文字列を取得します。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3pgW155_4.jpg" width="800" />

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
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/SfPg988_5.png" width="800" />

### マルチプレーヤーDemo
プレーヤーの署名を取得した後、それぞれ、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android)、[iOS](https://github.com/LiteAVSDK/Player_iOS)という3つの端末のプレーヤーDemoで検証を行えます。詳細については、Demoのソースコードをご参照ください。


## まとめ

このチュートリアルの学習を終えると、ビデオをVODにアップロードして、プレーヤーで再生する方法について理解できたことになります。

次のことをしたい場合：
- トランスコードされたビデオの再生については、[第2段階：トランスコードされたビデオの再生](https://www.tencentcloud.com/document/product/266/51565)をご参照ください
- アダプティブビットレートストリーミングビデオの再生については、 [第3段階：アダプティブビットレートストリーミングビデオの再生](https://www.tencentcloud.com/document/product/266/51566)をご参照ください
- 暗号化したビデオの再生については、 [第4段階：暗号化したビデオの再生](https://www.tencentcloud.com/document/product/266/51556)をご参照ください
- 長編ビデオ再生スキームについては、 [第5段階：長編ビデオ再生スキーム](https://www.tencentcloud.com/document/product/266/51557)をご参照ください
