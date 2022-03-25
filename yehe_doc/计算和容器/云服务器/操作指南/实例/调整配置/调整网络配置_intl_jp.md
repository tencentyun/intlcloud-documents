## 概要
Tencent Cloudは必要に応じて、パブリックネットワークネット課金モードまたはパブリックネットワーク帯域幅の変更をサポートし、直ちにアクティブ化します。帯域幅および課金方式の制限の変更および変更後の課金説明については、[パブリックネットワーク課金の変更](https://intl.cloud.tencent.com/document/product/213/10580)をご参照ください。

## 操作手順
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、「インスタンス」ページの上部で、帯域幅を変更する必要があるCVMインスタンスのリージョンを選択します。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
<dx-tabs>
::: リストビュー
下図のように、対象のCVMインスタンスの行の右側にある**その他**>**リソース調整**>**ネットワークの調整**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/bcece3bef3230a16bbe4b00e71105cf8.png)

:::
::: タブビュー
下図のように、対象のCVMインスタンスページ右上コーナーの**その他操作** > **リソースの調整** > **ネットワークの調整**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/4a57295676734b183310cfc8f06a8e25.png)

:::
</dx-tabs>
3. ポップアップした「ネットワークの調整」ダイアログボックスで、必要に応じてパブリックネットワーク課金モデルまたはパブリックネットワーク帯域幅を調整します。
 - ネットワーク課金モデル[](id:adjustModule)：Tencent Cloudは**トラフィック課金**と**帯域幅課金**という2種類のネットワーク課金モデルを提供しています。その内、帯域幅課金モデルには**帯域幅1時間ごとに後払い**というモデルがあります。
 - ターゲットの帯域幅の制限[]（id：adjustBandwidth）：Tencent Cloudは、**専用型パブリックネットワーク**と**共有型パブリックネットワーク**という2つのネットワーク構成を提供しています。 その内、共有型パブリックネットワークサービスの帯域幅パッケージによる課金は、現在、ベータ版テスト段階にあります。 本テキストでは、単一CVMの帯域幅上限を調整する専用型パブリックネットワーク設定の調整を例示します。
<dx-alert infotype="explain" title="">
帯域幅の上限については、[パブリックの帯域幅上限](https://intl.cloud.tencent.com/document/product/213/12523)をご参照ください。
</dx-alert>
4. 変更したい対象の課金モデルを選択するか、対象の帯域幅の値を設定して、**確認**をクリックします。



## 関連ドキュメント

- [パブリックネットワーク課金の変更](https://intl.cloud.tencent.com/document/product/213/10580)
- [パブリックネットワーク課金モード]（https://intl.cloud.tencent.com/document/product/213/10578） 
- [Bandwidth Package課金モード]（https://intl.cloud.tencent.com/document/product/684/15254）
- [パブリックネットワーク帯域幅の上限]（https://intl.cloud.tencent.com/document/product/213/12523）
