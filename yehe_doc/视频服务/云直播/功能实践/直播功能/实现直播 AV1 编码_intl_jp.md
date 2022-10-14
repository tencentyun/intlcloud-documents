AV1はオープンソースで、著作権フリーのビデオ圧縮形式です。前世代のH.265[HEVC]コーデックに比べて、同じ画質でのビットレートをさらに30%以上も低下させることができます。これは同じ帯域幅でより高画質な画像を伝送でき、それによって帯域幅コストを削減する効果を達成することを意味します。ここでは、どのようにしてビデオをAV1形式のビデオにトランスコードして再生するかを知ることができます。

## AV1の使用

### 前提条件

- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985) を行っていること。
- Tencent Cloud CSSサービスをアクティブ化し、 [プッシュ&再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済みであること。

[](id:step1)
### ステップ1：トランスコードテンプレートの作成
1. CSSコンソールにログインし、**機能設定** > [CSSトランスコード](https://console.cloud.tencent.com/live/config/transcode)と進みます。
2. **トランスコードテンプレートの作成**をクリックして、トランスコードタイプは標準トランスコーディングまたは高速高画質トランスコーディングを選択し、高度な設定を開きます。
3. コーデック方式から**AV1**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/9cd4c835c3cc37f3da93c07805ce4e5f.png) 
4. 入力が完了したら、**保存**をクリックして終了します。

[](id:step2)
### ステップ2：ドメイン名のバインド
トランスコードテンプレートを選択し、**ドメイン名のバインド**をクリックして、バインドが必要な**トランスコードテンプレート**および**再生ドメイン名**を選択し、**OK**をクリックするとバインドが成功します。
![](https://qcloudimg.tencent-cloud.cn/raw/a7d945597ae3ff71557720b4e6eeae43.png)

[](id:step3)
### ステップ3：再生アドレスの発行
**アドレスジェネレーター**をクリックし、ステップ2でバインドした再生ドメイン名と[ステップ1](#step1)のトランスコードテンプレートを選択し、再生アドレスを発行します。

[](id:step4)
### ステップ4：AV1ビデオの再生

AV1をサポートしているプレーヤーによって、再生ステップ3で発行したアドレスに従って再生すれば完了です。プレーヤーの選択では、AV1をサポートしているプレーヤーを選択することができ、独自のプレーヤーを改造することもできます。

- **AV1をサポートしているプレーヤー**
	- **Appクライアント**
		- [ExoPlayer](https://github.com/google/ExoPlayer) AV1対応で、libgav1を使用しています
		- [ijkplayer](https://github.com/bilibili/ijkplayer) FFmpegはバージョンが古いため、FFmpegをアップグレードして[dav1d](https://code.videolan.org/videolan/dav1d)に統合することができます
	- **Web端末**
		- [dash.js](http://cdn.dashjs.org/v2.4.0/jsdoc/index.html) サポート済みです（デコードはブラウザに依存し、Chromeをサポートしています）
		- [shaka-player](https://github.com/shaka-project/shaka-player) サポート済みです（デコードはブラウザに依存し、Chromeをサポートしています）
	- **PC端末**
	VLC PC版は、AV1 in FLV、HEVC in FLVをサポートしており、必要に応じて[Windowos版](https://share.weiyun.com/haPT1L0W) & [MacOS版](https://share.weiyun.com/W2btBASt)をダウンロードできます
- **独自のプレーヤーの改造**
プレーヤーにAV1形式のビデオを再生する機能がない場合は、 [お問い合わせ](https://intl.cloud.tencent.com/contact-us) からプレーヤーを改造できます。
