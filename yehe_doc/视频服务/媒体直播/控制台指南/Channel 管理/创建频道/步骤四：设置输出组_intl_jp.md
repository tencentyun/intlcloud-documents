StreamLiveは、さまざまなタイプの出力をサポートします。このステップで出力と出力グループを作成できます。

## 複数の出力グループの設定
StreamLiveは、1つのチャネルに対して複数のOutput Groupの出力をサポートします。右上の**プラス記号**をクリックして、複数のOutput Groupを追加できます。
![](https://qcloudimg.tencent-cloud.cn/raw/3e13eac666167d0f867e51e8a97cc1f0.png)

## 出力グループの名前とタイプの設定
出力グループの名前とタイプを設定します：
![](https://qcloudimg.tencent-cloud.cn/raw/6b239c37c95f0cc226bc93e12a481395.png)
現在、HLS、DASH、HLS_STREAM_PACKAGE、DASH_STREAM_PACKAGE、HLS_ARCHIVE、DASH_ARCHIVEタイプの出力をサポートしています。

- HLS、DASHは、HTTP PUTプロトコルによって、Destinationへ出力します。
- HLS_STREAM_PACKAGE、DASH_STREAM_PACKAGEは、HTTP PUTプロトコルによって、同一アカウントでの[StreamPackage](https://intl.cloud.tencent.com/document/product/1048/45219)へ出力します。このようにして、クライアントは、ライブブロードキャストCDNのライブブロードキャストBack-to-Originに用いるための独自のオリジンサーバーを形成します。
- HLS_ARCHIVE、DASH_ARCHIVEは、ライブブロードキャストコンテンツを[Tencent Cloud　COS](https://intl.cloud.tencent.com/document/product/1048/45218)へ出力してアーカイブすることをサポートします。

## ターゲットアドレスの設定
- HLSまたはDASHプロトコルタイプの出力を選択した場合は、ここにCDNのプッシュアドレスを入力できます。プッシュアドレスに検証要件がある場合は、検証情報を入力できます。
![](https://qcloudimg.tencent-cloud.cn/raw/e76f39828aade1c04c31b17e521220ed.png)
- HLS_STREAM_PACKAGEまたはDASH_STREAM_PACKAGEプロトコルタイプの出力を選択した場合は、ここに**StreamPackage Channel Id**を入力できます。StreamLiveは、ライブブロードキャストコンテンツをStreamPackageへプッシュします。
![](https://qcloudimg.tencent-cloud.cn/raw/05cae1db0fcfe74a723a0d828e3f5485.png)
- HLS_ARCHIVEまたはDASH_ARCHIVEプロトコルタイプの出力を選択した場合は、ここに**COS Destination**を入力できます。StreamLiveは、過去7日間のライブブロードキャストコンテンツをCOSにアーカイブします。（再起動するたびに上書きされます）
![](https://qcloudimg.tencent-cloud.cn/raw/15f727c5101320835259eeb4b0f82529.png)

## DRMの設定
Tencent Cloud StreamLiveは、ユーザー定義のキー（CustomDRMKeys）とSDMCDRMをサポートするDRM暗号化の有効化をサポートします。実際のニーズに応じて選択できます。具体的な使用方法については、[DRM設定ドキュメント](https://intl.cloud.tencent.com/document/product/1048/45217)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/8d81955db11e160cb0be5e2a8ed9226a.png)

## トランスコーディングテンプレートの設定
トランスコーディングテンプレートは、組合せ式オーディオビデオのトランスコーディングおよび分離式オーディオビデオのトランスコーディングをサポートします。実際のニーズに応じて選択できます。主な違いは、HLS出力の場合、分離式オーディオビデオのトランスコーディングが複数のオーディオトラック(マルチオーディオ)の自由な組み合わせとマッチングをサポートできることです。そのようなニーズがない場合は、組合せ式オーディオビデオのトランスコーディングテンプレートを使用することをお勧めします。
- 組合せ式オーディオビデオのトランスコーディングテンプレート：オーディオビデオのトランスコーディング構成を1回限りで設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/5567d7eff345ae787a98f4e5c0692bc9.png)
- 分離式オーディオビデオのトランスコーディングテンプレート：オーディオトランスコーディングテンプレートとビデオトランスコーディングテンプレートを個別に設定してください。
![](https://qcloudimg.tencent-cloud.cn/raw/aa81355608bc2ad72eab06e043a88fb3.png)
![](https://qcloudimg.tencent-cloud.cn/raw/00196f0a0566111d33a4aef484809110.png)
>!  **Top Speed Codec Transcodingは、Tencent Cloud Videoチームによって開発された高性能ビデオトランスコーディングサービスです。この機能を有効にすると、AIアルゴリズム機能を使用して、低ビットレートで高品質なトランスコーディングサービスを実現するように、サービスシーンに適合する最適な動的コーディングパラメータをリアルタイムで計算できます。**Bitrate Compression Ratio**は、削減する必要があると予想されるビデオビットレートのパーセンテージです。

### 出力の設定
- 組合せ式のトランスコーディングテンプレート出力を使用する場合は、マルチビットレート出力のトランスコーディングギアの1つとして、各Outputに対して1つのトランスコーディングテンプレートのみを選択できます。
![](https://qcloudimg.tencent-cloud.cn/raw/b007445cb3f47a9ec6d827f959cff9ba.png)
- 分離式トランスコーディングテンプレート出力を使用する場合は、各Outputは、1つのビデオトランスコーディングテンプレートと複数のオーディオトランスコーディングテンプレートを選択できます。ビデオトランスコーディングテンプレートは、マルチビットレート出力のトランスコーディングギアの1つです。オーディオトランスコーディングテンプレートは、このトランスコーディングギアと一致させることができるオーディオトラック（オーディオ）です。
![](https://qcloudimg.tencent-cloud.cn/raw/8b758ded635531a9a24f1aae51eb9828.png)

### 設定完了
**Done**をクリックして設定を保存します。この時点で、チャネル全体の設定が完了します。【Start】をクリックして実行できます。
![](https://qcloudimg.tencent-cloud.cn/raw/a596817ccf73cd4573f83e3d572fcbee.png)