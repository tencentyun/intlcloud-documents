## 概要

Tencent Cloudの Window Server 2008 R2 Enterprise SP1 と Windows Server 2012 R2 は Virtio ENIドライバーを使用して、仮想化ハードウェアのネットワークパフォーマンスを最適化します。パフォーマンスを改善するため、Tencent ClouはENIドライバーを改善し続けます。このドキュメントでは、Virtio ENIドライバーを更新し、ドライバーのバージョンを確認する方法について説明します。

## 前提条件

Tencent Cloud CVMにログインしました。

##　操作手順

### システムのバージョン情報の確認

システムバージョンを表示するには、次の手順を実行します。
1. CVMにログインし、実際のOSに対応する次の操作を実行して、「システム」ウィンドウを開きます。
 - **Window Server 2008 R2 Enterprise SP1**：スタートメニューから【コンピューター】を右クリックし、表示されるリストから【プロパティ】を選択します。
 - **Windows Server 2012 R2**：「コントロールパネル」を開き、【システム】を選択します。
2. 「システム」の【コンピューターの基本的な情報の表示】で、システムのバージョン情報を確認できます。   

###  Virtio ENIドライバーの更新方法
>! 更新プロセス中にネットワーク接続が切断される可能性があり、更新する前にサービスに影響があるかを確認してください。更新した後コンピューターを再起動する必要があります。
>
1. CVMのブラウザを通して Window Server 2008 R2 とWindows Server 2012 R2 に適用する VirtIO ENIドライバーのインストールファイルをダウンロードします。 
VirtIO ENIドライバーのダウンロードアドレスは次の通りです。実際のネットワーク環境に基づいてダウンロードアドレスを選択します。
 - パブリックネットワークダウンロードアドレス：：http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msiです
 - プライベートネットワークダウンロードアドレス：http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msiです
2. ダウンロードが完了したら、インストールソフトウェアをダブルクリックし、【標準】インストールモードを選択して、【次へ】をクリックします。
3. ポップアップしたセキュリティプロンプトで、【常に 「Tencent Technology（Shenzhen）Company Limited」からのソフトウェアを信頼する】をチェックし、【インストール】をクリックします。 
インストールプロセス中、下記のポップアップボックスを表示された場合、【常にこのドライバーソフトウェアをインストールする】を選択してください。      
4. プロンプトに従ってコンピューターを再起動して更新を完了します。


### ドライバーのバージョンの確認

1. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"  style="margin:0;"> をクリックし、「実行」ボックスで**ncpa.cpl**を入力し、かつ **Enter**を押します。
2. 開いた「ネットワーク接続」ウィンドウで、「イーサネット」アイコンを右クリックし、【属性】を選択します。
3. ポップアップした「イーサネットのプロパティ」ウィンドウで、【設定】をクリックします。
4. 「Tencent VirtIO Ethernet Adapter のプロパテ」ウィンドウで、【ドライバー】タブを選択して、現在のドライバーのバージョンをクエリーできます。


