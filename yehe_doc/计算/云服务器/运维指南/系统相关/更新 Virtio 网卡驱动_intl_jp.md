## ユースケース

Tencent Cloudの Window Server 2008 R2 Enterprise SP1 と Windows Server 2012 R2 は Virtio ENIドライバーを使用して、仮想化ハードウェアのネットワークパフォーマンスを最適化します。パフォーマンスを改善するため、Tencent ClouはENIドライバーを改善し続けます。このドキュメントはVirtio ENIドライバーの更新お及びドライバーのバージョンの確認方法について説明します。

## 前提条件

Tencent CloudのCVMにログインしました。

## 操作手順

### システムのバージョン情報を確認する

システムのバージョン情報は下記の方法を通して確認できます：
1. CVMにログインし、【PC】>【プロパティ】を右クリックして、「システム」ウィンドウを開きます。
2. 「システム」の【コンピューターの基本的な情報の表示】で、システムのバージョン情報を確認できます。次の図に示すように：
![](//mccdn.qcloud.com/static/img/5cd57bbbd48668cca57efdaba7e5ae84/image.png)   

###  Virtio ENIドライバーの更新方法
>! 更新プロセス中にネットワーク接続が切断される可能性があり、更新する前にサービスに影響があるかを確認してください。更新した後コンピューターを再起動する必要があります。
>

1. CVMのブラウザを通して Window Server 2008 R2 とWindows Server 2012 R2 に適用する VirtIO ENIドライバーのインストールファイルをダウンロードします。 
VirtIO ENIドライバーのダウンロードアドレス：http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msiです
2. ダウンロードが完了したら、インストールソフトウェアをダブルクリックし、【標準】インストールモードを選択して、【次へ】をクリックします。次の図に示すように：
![](//mccdn.qcloud.com/static/img/0d596e42ae299cfa295a0493dc68bc4d/image.png)
3. ポップアップしたセキュリティプロンプトで、【常に 「Tencent Technology（Shenzhen）Company Limited」からのソフトウェアを信頼する】をチェックし、【インストール】をクリックします。次の図に示すように：
![](//mccdn.qcloud.com/static/img/f2f5aea8ed1aa8814e69fa9142254537/image.png) 
インストールプロセス中、下記のポップアップボックスを表示された場合、【常にこのドライバーソフトウェアをインストールする】を選択してください。
![](//mccdn.qcloud.com/static/img/ca48d6e37f5deb2f4575bc608f5c49d6/image.png)      
4. プロンプトに従ってコンピューターを再起動して更新を完了します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       

### ドライバーのバージョンを確認する

1. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"  style="margin:0;"> をクリックし、「実行」ボックスで**ncpa.cpl**を入力し、かつ **Enter**を押します。次の図に示すように：
![](https://main.qcloudimg.com/raw/958e5f143dfabe5c63d5dec63b0d1292.png)
2. 開いた「ネットワーク接続」ウィンドウで、「イーサネット」アイコンを右クリックし、【属性】を選択します。次の図に示すように：
![](https://main.qcloudimg.com/raw/47a14b72bd71150eb126bcdca3d6157c.png)
3. ポップアップした「イーサネットのプロパティ」ウィンドウで、【設定】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/f9e00988e840d775c6ff5f9f789c5172.png)
4. 「Tencent VirtIO Ethernet Adapter のプロパテ」ウィンドウで、【ドライバー】タブを選択して、現在のドライバーのバージョンをクエリーできます。次の図に示すように：
![](https://main.qcloudimg.com/raw/ce1be9c37b22e945a11e530c39be41d9.png)


