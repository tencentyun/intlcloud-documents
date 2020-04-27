このドキュメントでは、リモートデスクトップを使用してWindowsインスタンスに接続する時に、「ネットワークレベルの認証が必要です」などのアラームを処理する方法について説明します。

## 故障について
 Windows OSの標準機能の1つ「リモートデスクトップ接続」を利用すると、リモートコンピューターに接続できない問題があって、「ネットワークレベルの認証が必要です」というプロンプトが表示されます。
![](https://main.qcloudimg.com/raw/a2976a1f9d34cadeb378687ce4f1ff64.png)

## トラブルシューティング

>? 以下の操作は Windows Server 2016 を例として説明します。
>

###  VNC を使用してCVMにログインする
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理ページで、対象のCVMインスタンスを見つけて、【ログイン】をクリックします。下図に示すように：
![CVMリストページ](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ポップアップされた 「Windowsインスタンスにログインする」ウィンドウで、【その他の方式(VNC）】を選択し、【今すぐログイン】をクリックして、CVMにログインします。
4. ポップアップされたログインウィンドウで、左上の「リモートコマンドの送信」を選択し、**Ctrl-Alt-Delete** をクリックして、システムログインインターフェースに入ります。下図に示すように：
![](https://main.qcloudimg.com/raw/2dec43fa6ddb5e442da59c75f7a34b0f.png)

### レジストリを変更する

1.  OSインターフェースで、<img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>をクリックして、 **regedit**を入力して、**Enter**を押して、レジストリエディターを開きます。
2. 左側のナビゲーションツリーで、【コンピューター】>【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Lsa】ディレクトリを開き、右側のウィンドウで【Security Packages】を見つけます。以下に示すように：
![Security Packages](https://main.qcloudimg.com/raw/7a082160ed82ca713ca6a4f46af84eaf.png)
3. 【Security Packages】をダブルクリックして、【複数行文字列の編集】ダイアログボックスを開きます。
4. 「複数行文字列の編集」ダイアログボックスで、【tspkg】文字を追加し、【OK】をクリックします。以下に示すように：
![](https://main.qcloudimg.com/raw/5568c403df3d9aa9afb3cdc5972df0f6.png)
5. 左側のナビゲーションツリーで、【コンピューター】>【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【SecurityProviders】ディレクトリを展開し、右側のウィンドウで【SecurityProviders】を見つけます。次の図に示すように：
![](https://main.qcloudimg.com/raw/41611d8e70772cf2254236a7fb7fa1f0.png)
6. 【SecurityProviders】をダブルクリックして、【文字列の編集】ダイアログボックスを開きます。
7. 「文字列の編集」ダイアログボックスの【値のデータ】の最後に`, credssp.dll`を追加し、【OK】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/b62ae3112e4fadc99817fcf0864740cf.png)
8. レジストリエディターを閉じて、インスタンスを再起動してリモートログインできます。

