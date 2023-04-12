## 概要
Tencent Cloudは必要に応じて、パブリックネットワーク課金モデルまたはパブリックネットワーク帯域幅の変更をサポートし、変更はすぐに有効になります。制限と価格の詳細については、[パブリックネットワーク課金方式の変更](https://intl.cloud.tencent.com/document/product/213/10580)をご参照ください。

## 操作手順
1.  [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、「インスタンス」ページの上部で、帯域幅を変更するCVMインスタンスが存在するリージョンを選択します。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
<dx-tabs>
::: リストビュー
下図のように、対象のCVMインスタンスの行の右側にある**さらに**>**リソース調整**>**ネットワークを調整**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/bcece3bef3230a16bbe4b00e71105cf8.png)

:::
::: タブビュー
下図のように、対象のCVMインスタンスのページの右上隅にある**その他の操作** &gt; **リソース調整** &gt; **ネットワークを調整**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/4a57295676734b183310cfc8f06a8e25.png)

:::
</dx-tabs>
3. ポップアップした「ネットワークを調整」ダイアログボックスで、必要に応じてパブリックネットワーク課金モデルまたはパブリックネットワーク帯域幅を調整します。
 - ネットワーク課金モデル[](id:adjustModule)：Tencent Cloudは**トラフィック課金**と**帯域幅課金**という2つの異なる課金モデルが用意されています。帯域幅課金モデルは、**利用した時間単位で課金される**仕組みです。
 - ターゲット帯域幅制限[]（id：adjustBandwidth）：Tencent Cloudは、**専用型パブリックネットワーク**と**共有型パブリックネットワーク**（帯域幅パッケージによって課金され、現在ベータテストの段階）という2つのネットワーク構成を提供しています。このドキュメントでは、専用型パブリックネットワークの構成のへ変更、つまり単一CVMインスタンスの帯域幅上限の変更を例に取り上げます。
<dx-alert infotype="explain" title="">
帯域幅上限の詳細については、[パブリックネットワーク帯域幅上限](https://intl.cloud.tencent.com/document/product/213/12523)をご参照ください。
</dx-alert>
4. ターゲット課金モデルを選択するか、ターゲット帯域幅の値を設定して、**OK**をクリックします。

## 関連ドキュメント

- [パブリックネットワーク課金方式の変更](https://intl.cloud.tencent.com/document/product/213/10580)
- [パブリックネットワーク課金方式](https://www.tencentcloud.com/document/product/213/10578)
- [Product Pricing](https://www.tencentcloud.com/document/product/684/15254)
- [パブリックネットワーク帯域幅の上限](https://www.tencentcloud.com/document/product/213/12523)
