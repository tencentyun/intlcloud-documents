本節では、ローカルのビデオファイルをVODにすばやくアップロードし、VODサービスを利用してビデオを処理する方法について説明します。最終的に、**Webページでアクセラレーションされたウォーターマーク入りのトランスコード済みビデオを直接視聴できます**。ここでは、ローカルビデオファイルの「TencentCloud.mp4」を例として説明します。


## ステップ1：VODをアクティブ化する
1. [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985)で登録して、[Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)を完了する必要があります。
2. VODサービスを購入します。
3.【Cloud Products】> 【Video Services】 >[【Video on Demand】](https://console.cloud.tencent.com/vod)の順に選択して、VODコンソールに入ります。

>VODサービスがアクティブ化済みの場合は、次のステップに直接進みます。



## ステップ2：ビデオをアップロードする
1. 左側ナビゲーションバーにある[【Media Assets】](https://console.cloud.tencent.com/vod/media)をクリックします。
2.【Upload Video】をクリックして、【Upload method】設定項目で【Local Upload】を選択します
3. 【Select Video】をクリックして、ローカルビデオファイル「Tencent Cloud.mp4」を選択します。
4.【Video Processing】設定項目で【No Processing After Upload】を選択して、左下の【Start Upload】をクリックします。

## ステップ3：ウォーターマークテンプレートを作成する
1. 左側ナビゲーションバーで【Video Processing】>[【Templates】](https://console.cloud.tencent.com/vod/video-process/template)を選択します。
2. タブ欄で【Watermarking Template】を選択します。
3. 【Create Watermarking Template】をクリックし、このページで以下の設定を行ってから、【Create】をクリックします。<br>
<img src="https://main.qcloudimg.com/raw/c85044cca9840a8f83bc5747e87985a9.png" width="450">
	
## ステップ4：ビデオを処理する
1. [Media asset](https://console.cloud.tencent.com/vod/media)タブで【Uploaded】を選択します。
2.「Tencent Cloud.mp4」にチェックを入れて、【Video Processing】をクリックします。
![](https://main.qcloudimg.com/raw/535b71cfc6374ff65bc46c1ab07eccd1.png)
3.「Video Processing 」ポップアップボックスで、【Processing Type】設定項目で【Transcode】を選択します。
4.【Transcoding Template】の設定項目で、左側のドロップダウンリストをクリックして【Select Transcoding Template】を選択します。次に、右側のドロップダウンリストをクリックして【MP4-SD(20)】 と【MP4-HD(30)】 (複数トランスコーディングテンプレートを選択可能)を選択します。
5.【Watermarking Template】の設定項目で、ドロップダウンリストをクリックして【Select Watermarking Template】を選択します。右側にドロップダウンリストが表示され、【p001】を選択します。
6. 【Video Cover】の設定項目で【Use First Frame as Cover】にチェックを入れ、【OK】をクリックします。
<img src="https://main.qcloudimg.com/raw/69abe9f386f0e12a79ae6596d6a994e4.png">

## ステップ5：再生リンクを取得する
1. 「Tencent Cloud.mp4」の行の操作欄で【Manage】をクリックします。
2.【Standard Transcoding List】モジュールの中の【MP4-SD-SD】に対応する操作欄の【Copy address】をクリックします。
<img src="https://main.qcloudimg.com/raw/d6936a55fcc0a1e7df5fdf9265c25f7a.png" width="850">
3. コピーしたURLをWebブラウザのアドレスバーに貼り付け、Enterキーを押してビデオを再生します。


