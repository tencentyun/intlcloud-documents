##  操作シナリオ
このドキュメントでは、CVMコンソールとクラウドAPIを介して、シャットダウン状態のインスタンスを起動する方法について説明します。




##　操作手順
### コンソールからインスタンスを起動
1. [CVM コンソール](https://console.cloud.tencent.com/cvm/) にログインします。
2. 実際のニーズに応じて、異なる操作方式を選択します。
	- **単一インスタンスの起動**：起動する必要のあるインスタンスを選択し、インスタンスの右側で【その他】>【インスタンスのステータス】> 【起動】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/5adf1eaf69be183707a56c60991bb73f.png)
	- **複数インスタンスの起動**：：起動する必要のあるすべてのインスタンスを選択し、リスト上部にある【起動】をクリックして、インスタンスを一括起動します。次の図に示すように：
！[セキュリティグループとホスト]（https://main.qcloudimg.com/raw/240b3421c6a40829b3de4043941301a0.png）

### APIからインスタンスを起動
詳細については、[ResetInstance](https://intl.cloud.tencent.com/document/product/213/33236)をご参照ください。

## 後続操作
次の操作は、インスタンスを起動した場合にのみ実行できます。
- **インスタンスへのログイン**：OSに応じて、[Linuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)し、または[Windowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5435)してください。
- **[クラウドディスクを初期化](https://intl.cloud.tencent.com/document/product/362/31596)**：マウントされたクラウドディスクにフォーマット、パーティション、ファイルシステムの作成などの初期化操作を実行します。
