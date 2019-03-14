## 概要情報

BatchはCloud-initサービスを利用してCVMを初期化するため、Batchを使用するときに記入されるイメージはCloud-initを正常にインストールおよび構成した必要があります。そうでなければ、ジョブ実行または計算環境内のCVMの作成は``失敗``します。

（Cloud-initはCVMが初めて初期化されたときのカスタム構成機能を提供します）

Cloud-initをインストールして構成するには、以下のガイドに従ってください。
* Linuxの``新規作成``CVM/カスタムイメージ：現在、Tencent Cloud CentOS、UbuntuのすべてのバージョンのパブリックイメージがデフォルトでCloud-initをサポートしており、これらのパブリックイメージからCVMとカスタムイメージを作成するために手動でCloud-initをインストールして構成する必要はありません
* Linuxの``ストレージ``CVM/カスタムイメージ：以前に作成したCVMやカスタムイメージの場合は、手動でCloud-initをインストールする必要があります。[Linux Cloud-initの手動インストール>>>](https://intl.cloud.tencent.com/document/product/213/12587)を参照してください

既にCloud-initを含む共通操作システムイメージIDは次のとおりです。
* img-31tjrtph（CentOS 7.2 64ビット）
* img-pyqx34y1（Ubuntu Server 16.04.1 LTS 64ビット）









