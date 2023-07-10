## 概要

高度な画像圧縮とは、Cloud Object Storage（COS）からリリースされたCloud Infiniteをベースとする画像圧縮機能です。画像をより効率的にTPGやHEIFといった高圧縮率形式にトランスコードし、画像伝送リンクとロード時間を効果的に短縮し、帯域幅とトラフィックコストを削減することができます。

>?
> - 高度な画像圧縮機能により、JPG、PNG、WEBPなどの形式の画像をTPG、HEIF形式にトランスコードできます。
> - TPGは、Tencent Cloudが自社開発した画像形式です。使用する場合は、**画像ロード環境がTPGデコードをサポートしている**ことを確認してください。Tencent CloudのCloud Infiniteは、TPGデコーダを統合した iOS、Android、[Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) ターミナルSDKを提供し、TPGへのすばやいアクセスと使用を支援することができます。
> - 現在、iOS 11以降およびAndroid PシステムはHEIF形式をネイティブにサポートしています。
> - 高度な画像圧縮は有料サービスであり、Cloud Infiniteによって課金されます。具体的な料金については、Cloud Infiniteの[料金ドキュメント](https://intl.cloud.tencent.com/document/product/1045/33431)をご参照ください。
> 

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5/bucket)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリストに進みます。

3. 高度な画像圧縮機能を有効にしたいバケットを選択し、バケット管理ページに進みます。
4. **データ処理**>**画像処理**タブをクリックします。
5. **高度な画像圧縮**の設定項目を見つけ、**編集**をクリックし、現在のステータスを「有効」にして、**保存**をクリックします。

![](https://main.qcloudimg.com/raw/f336e71135338664375a4953fabb5a6e.png)
機能を有効にすると、現在バケットにある画像リソースに対応する[画像の高度圧縮](https://intl.cloud.tencent.com/document/product/436/40119)APIを使用して、ダウンロード時にTPG、HEIF圧縮を実行することができます。
