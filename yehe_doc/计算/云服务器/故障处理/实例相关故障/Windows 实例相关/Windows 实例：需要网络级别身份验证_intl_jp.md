本文では Windows インスタンスにリモート接続する時に、「ネットワークレベル認証が必要です」のアラームを処理する方法について説明します。

## 故障事象
 Windows 付属のリモートデスクトップ接続を使用する場合、リモートコンピューターに接続できない問題があって、「ネットワークレベルの認証が必要です」のプロンプトが表示されます。
![](https://main.qcloudimg.com/raw/409b3259fa13220e8cde0790aa87488b.jpg)

## 故障処理

>? 以下の操作は Windows Server 2016 を例として説明します。
>

###  VNC 方式を通してCVMにログインする
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理ページで、対象のCVMインスタンスを見つけて、【ログイン】をクリックします。下図に示すように：
![CVMリストページ](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ポップアップされた 「Windowsインスタンスにログインする」ウィンドーで、【その他の方式(VNC）】を選択し、【今すぐログイン】をクリックして、CVMにログインします。
4. ポップアップされたログインウィンドーで、左上の「リモートコマンドの送信」を選択し、**Ctrl-Alt-Delete** をクリックして、システムログインインターフェースに入ります。下図に示すように：
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### レジストリを修正する

1.  OSインターフェースで、<img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>をクリックして、 **regedit**を入力して、**Enter**を押して、レジストリエディターを開きます。
2. 左側のナビゲーションツリーで、【コンピューター】>【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Lsa】ディレクトリを展開し、右側のウィンドウで【Security Packages】を見つけます。以下に示すように：
![Security Packages](https://main.qcloudimg.com/raw/db037b5131ff44af72b560fbac4931e1.png)
3. 【Security Packages】をダブルクリックして、【複数行文字列の編集】ダイアログボックスを開きます。
4. 「複数行文字列の編集」ダイアログボックスで、【tspkg】文字を追加し、【OK】をクリックします。以下に示すように：
![](https://main.qcloudimg.com/raw/cca2bce345b48569d45fd391ee65bc51.png)
5. 左側のナビゲーションツリーで、【コンピューター】>【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【SecurityProviders】ディレクトリを展開し、右側のウィンドウで【SecurityProviders】を見つけます。以下に示すように：
![](https://main.qcloudimg.com/raw/14e84c77ae1d1d3c5bc2ab091543a957.png)
6. 【SecurityProviders】をダブルクリックして、【文字列の編集】ダイアログボックスを開きます。
7. 「文字列の編集」ダイアログボックスの【値のデータ】の最後に`, credssp.dll`を追加し、【OK】をクリックします。以下に示すように：
![](https://main.qcloudimg.com/raw/34b98c226c359b070e2f03c2ff1c6e42.png)
8. レジストリエディターを閉じ、インスタンスをリスタートして、リモートでログインできます。

