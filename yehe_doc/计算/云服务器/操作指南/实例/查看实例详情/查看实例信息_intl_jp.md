## 概要
ユーザーがCVMインスタンス情報を確認しやすいように、Tencent Cloudは下記の3種類の確認方法を提供しています。
- コンソールの [概要](https://console.cloud.tencent.com/cvm/overview) ページでアカウントにおけるCVMインスタンス総数及びそれらの稼動状態、各リージョンのリソース数、クォータ等の情報を確認します。
- コンソール [CVM](https://console.cloud.tencent.com/cvm/index) ページで、特定リージョン内のすべてのCVMインスタンスに関する情報を確認します。
- インスタンス詳細ページであるCVMインスタンスの詳細情報を確認します。

##  前提条件

[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。

## 操作手順
### インスタンス概要情報の確認

左側ナビゲーションバーで、 **[概要](https://console.cloud.tencent.com/cvm/overview)**を選択し、CVM概要ページに移動します。
当該ページでは、確認可能な情報、及び実行可能な操作は下記を含んでいます。

- CVM状態（即ちCVMの総数）、7日以内に期限切れになるインスタンス数、ごみ箱のインスタンス数、正常なサーバー数。
- 更新待ちCVMリスト、当該ページでCVMを更新できます。
- リソース数とクォータ。各リージョンの従量課金CVM、カスタムイメージ及びスナップショットクォータ情報を確認できます。また、当該ページでクォータを申請できます。
- クロスリージョンでクラウドリソースをサーチします。

### CVMリスト情報の確認

下図のように、左側ナビゲーションバーで、**[インスタンス](https://console.cloud.tencent.com/cvm/index)**を選択し、インスタンスリストページに移動します。
![](https://main.qcloudimg.com/raw/6d1d1e3312b92c4c32099df85e6e26b3.png)
このページでは、ID/インスタンス名、監視、ステータス、アベイラビリティーゾーン、インスタンスタイプ、設定、メインIPv4アドレス、メイン IPv6 アドレス、インスタンス課金モデル、ネットワーク課金モデルおよび所属プロジェクトなどを含む情報操作を確認できます。
<dx-alert infotype="explain" title="">
実際のニーズに応じて使用できます [コンソールインスタンスのページビューへの切替](https://intl.cloud.tencent.com/document/product/213/45918)。
</dx-alert>

下図のように、右上コーナーの<img style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/93d28b8ce995f53c460707e44038e0ad.png"></img>をクリックし、ポップアップした「カスタムリストフィールド」ウィンドウで表示したいリストの詳細情報を選択します。
![](https://main.qcloudimg.com/raw/824b948f247147cd538d696b0dbe6a28.png)

### インスタンス詳細情報の確認

1. [インスタンス](https://console.cloud.tencent.com/cvm/index) の管理ページ上部で、リージョンを選択します。
2. 詳細を確認しようとするインスタンスを見つけ、 ID/インスタンス名をクリックし、インスタンス詳細ページに入ります。下図の通りです。
インスタンス詳細ページで、インスタンス情報、アーキテクチャ図、ネットワーク情報、設定情報、イメージ情報、課金情報、Elastic Network Interface（ENI）、監視、セキュリティグループ、操作ログなどを確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/c6cfd9bdb5ab7a9c67676d9a4f7ee925.png)

