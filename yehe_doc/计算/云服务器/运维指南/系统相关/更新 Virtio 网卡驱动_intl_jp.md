## 概要

Tencent Cloud CVM Windows Server 2008 R2、Windows Server 2012 R2、Windows Server 2016およびWindows Server 2019は、Virtio ENIドライバーをインストールすることにより、仮想化ハードウェアのネットワークパフォーマンスを最適化します。Tencent Cloudは、パフォーマンスの向上とトラブルシューティングのため、ENIドライバーを継続的に改善します。ここでは、Virtio ENIドライバーを更新し、ドライバーのバージョンを確認する方法についてご説明します。

##  前提条件

Windows CVMにログインしていること。

## 操作手順

### システムのバージョン情報を確認する

システムのバージョン情報は下記の方法を通して確認できます：
1. CVMにログインし、<img src="https://qcloudimg.tencent-cloud.cn/raw/67b4c8b9bac6c8f0c8a60a5ed9c6b5dd.png" style="margin:-3px 0px">を右クリックし、表示されたメニューから**実行**を選択します。
2. 開いた「実行」ウィンドウに`cmd`と入力して**Enter**を押します。
3. 開いた「cmd」ウィンドウで`systeminfo`コマンドを実行すると、システム情報が確認できます。
今回のシステムバージョンは「Windows Server 2016データセンター版64ビット英語版」を例としているため、下図のような情報が取得されます。
![](https://qcloudimg.tencent-cloud.cn/raw/8c46c9c368201575fafed26272638544.png)

###  Virtio ENIドライバーの更新方法

<dx-alert infotype="notice" title="">
更新中はネットワークが瞬断しますので、更新前に業務に影響が出ないかご確認ください。更新後はコンピュータを再起動する必要があります。
</dx-alert>


1. CVMのブラウザから、OSのバージョンに適したVirtio ENIドライバーのインストールファイルをダウンロードします。 
Virtio ENIドライバーのダウンロードアドレスは次のとおりです。実際のネットワーク環境に応じてダウンロードしてください。
 -  **パブリックネットワークのダウンロードアドレス**：`http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe`
 -  **プライベートネットワークのダウンロードアドレス**：`http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe`
2. ダウンロードが完了したら、ダブルクリックでインストーラーを起動し、**Next**をクリックします。
3. デフォルトで「VirtioDrivers」にチェックを入れたまま、**Next**をクリックします。下図のとおりです。
![](https://qcloudimg.tencent-cloud.cn/raw/e77875fd9fdac5364188bc989bba0c05.png)
4. インストール先を選択し、**Install**をクリックします。下図のとおりです。
![](https://qcloudimg.tencent-cloud.cn/raw/d38b32cba76dbb2cdfad95bae3de1f58.png)
5. 表示されたセキュリティプロンプトで、「「Tencent Technology(Shenzhen)Company Limited」からのソフトウェアを常に信頼する」にチェックを入れ、**インストール**をクリックします。
インストール時に次のポップアップボックスが表示された場合は、**このドライバーソフトウェアを常にインストールする**を選択してください。      
6. プロンプトに従ってコンピューターを再起動して更新を完了します。


### ドライバーのバージョンを確認する

1. <img src="https://qcloudimg.tencent-cloud.cn/raw/67b4c8b9bac6c8f0c8a60a5ed9c6b5dd.png" style="margin:-3px 0px">を右クリックし、表示されたメニューから**実行**を選択します。
2. 開いた「実行」ウィンドウに**ncpa.cpl**と入力して**Enter**を押します。
2. 開いた「ネットワーク接続」ウィンドウで、「イーサネット」のアイコンを右クリックし、**プロパティ**を選択します。
4. 表示された「イーサネットのプロパティ」ウィンドウで、**構成**をクリックします。
5. 「Tencent VirtIO Ethernet Adapterプロパティ」ウィンドウで、**ドライバー**タブを選択すると、現在のドライバーのバージョンが確認できます。

