## ユースケース
CVMのデフォルトポートは、悪意のあるソフトウェアによるスキャンや攻撃の影響を受けやすくなっています。ポート攻撃が原因でCVMにリモート接続できなくなることを防ぐために、CVMのデフォルトのリモートポートを一般的でないポートに変更して、CVMのセキュリティを確保することができます。

ポートの変更を有効にするには、サービスポートの変更が、セキュリティグループルールとCVMで変更を同期する必要があります。次の操作では、CVMのデフォルトのリモートポートを変更する方法について説明します。CVMのOSの種類に応じて、対応する変更方法を選択してください。
-[Windows CVMのデフォルトのリモートポートを変更する]（#ModifyWindows CVMPort）
-[Linux CVMのデフォルトのリモートポートを変更する]（#ModifyLinux CVMPort）

### 操作手順

<span id="ModifyWindows CVMPort"></span>
### Windows CVMのデフォルトのリモートポートを変更する
>以下の操作は、Windows Server 2012 OSを例として説明し、操作手順は、OSと言語によって若干異なる場合があります。
>
- [VNCを使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32496)します。
1. OSの画面で、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;">をクリックして、「Windows PowerShell」ウィンドウを開きます。
3. 「Windows PowerShell」画面で、**regedit**を入力して、**Enter**キーを押して、「レジストリエディタ」を開きます。
4. 左側のレジストリナビゲーションで、【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Terminal Server】>【Wds】>【rdpwd】>【Tds】>【tcp】ディレクトリの順で展開します。
5. <span id="Windows_step05"></span>【tcp】中のPortNumberを見つけて、以下に示すように、PortNumberデータ（すなわち3389のポート番号）を0～65535間の未使用ポートに変更します。
![](https://main.qcloudimg.com/raw/7044cef95fd7e56b56946afdb64de346.png)
6. 左側のレジストリナビゲーションで、【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Terminal Server】>【WinStations】>【RDP-Tcp】ディレクトリの順で展開します。
7. 【RDP-Tcp】中のPortNumberを見つけ、【RDP-Tcp】中のPortNumberデータ（ポート番号）を【tcp】中のPortNumberデータ（ポート番号）と同じポート番号に変更します。
![](https://main.qcloudimg.com/raw/fa54eb32c20dcc8a7c942c8e707fa665.png)
8.（オプション）CVMでファイアウォールが有効になっている場合は、新しいポートをファイアウォールに追加して、接続を許可するように設定する必要があります。
 1. 「Windows PowerShell」ウィンドウで、**wf.msc**を入力して、**Enter**キーを押して、「セキュリティが強化されたWindowsファイアウォール」ウィンドウを開きます。
 2.「セキュリティが強化されたWindowsファイアウォール」ウィンドウで、以下に示すように、【インバウンドルール】を選択し、【新規ルール】をクリックします。
![](https://main.qcloudimg.com/raw/ac93eed862e215971073912030fdbc41.png)
 3.「新規のインバウンドルールウィザード」ウィンドウで、【ポート】 をオンにして 【次へ】 をクリックします。
 4.「新規のインバウンドルールウィザード」ウィンドウの「プロトコルとポート」ステップで、以下に示すように、【TCP】を選択して、【特定のローカルポート】に[ステップ5]（#Windows_step05）で設定されたポート番号を入力して、【次へ】をクリックします。　
 ![](https://main.qcloudimg.com/raw/73a7ca280f4f6b733d687597014b57b4.png)
 5.「新規のインバウンドルールウィザード」ウィンドウの「操作」ステップで、【接続を許可する】を選択し、【次へ】をクリックします。
 6.「新規のインバウンドルールウィザード」ウィンドウの「設定ファイル」ステップで、デフォルト設定のままにして、【次へ】をクリックします。
 7.「新規のインバウンドルールウィザード」ウィンドウの「名前」ステップで、ルール名を入力し、【完了】をクリックします。
9.「Windows PowerShel」ウィンドウで** diskmgmt.msc **を入力し、** Enter **キーを押して「サービス」ウィンドウを開きます。
10.「サービス」ウィンドウで、【Remote Desktop Services】を右クリックし、【再起動】を選択して、リモートログインサービスを再起動します。
11. [セキュリティグループルールの変更](https://intl.cloud.tencent.com/document/product/213/34825)を参照し、プロトコルポートが「TCP:3389」のセキュリティグループルールを[ステップ5](#Windows_step05)で設定されたポート番号に変更します。
![](https://main.qcloudimg.com/raw/a447d7e69ce95d349f0d78b5b72b9228.png)


<span id="ModifyLinuxCVMPort"></span>
### Linux CVMのデフォルトのリモートポートを変更する
>
> - Linux CVMのデフォルトのリモートポートを変更する前に、SSHポート番号を追加して、新しいポートがCVMに正常に接続されているかどうかをテストしてから、デフォルトポート22をを削除することをお勧めします。これにより、新しいポートがCVMに接続できない場合は、デフォルトポート22を使用してCVMに接続できます。
> - 以下の操作は、CentOS 7.3 OSを例として説明し、操作手順は、OSと言語によって若干異なる場合があります。
>
- [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2.次のコマンドを実行して、設定ファイルを変更します。
```
vim /etc/ssh/sshd_config
```
3. <span id="Linux_step03"></span>**i**を押して編集モードに切り替え、新しいポートを追加し、以下に示すように、`#Port 22`の下に`Port new port number`を追加して、`Port 22`のコメントを削除します（つまり、その前の`#`を削除します）。
例：`Port 23456`を追加します。
![](https://main.qcloudimg.com/raw/54e5d9b4301271fbbeca8b2718b985dc.png)
4. **Esc**キーを押して、**：wq**を入力し、内容を保存して戻ります。
5.以下のコマンドを実行して、変更後の構成を有効にします。
```
systemctl restart sshd.service
```
6.（オプション）ファイアウォールを設定します。
 - CentOS 7より前のバージョンを使用するLinux CVMでは、デフォルトでiptablesサービスをファイアウォールとします。CVMにiptablesルールが設定されている場合、次の操作を実行してファイアウォールを設定する必要があります。
    1. 次のコマンドを実行して、ファイアウォールを設定します。
```
iptables -A INPUT -p tcp --dport 新しいポート番号 -j ACCEPT
```
たとえば、新しいポート番号が23456の場合、次のコマンドを実行します。
```
iptables -A INPUT -p tcp --dport 23456 -j ACCEPT
```
    2. 次のコマンドを実行して、ファイアウォールを再起動します。
```
service iptables restart
```
 -CentOS 7以降のバージョンを使用するLinux CVMでは、デフォルトでFirewalldサービスをファイアウォールとします。CVMでfirewalld.serviceが有効になっている場合は、次の操作を実行してファイアウォールを設定する必要があります。
以下のコマンドを実行して、[ステップ3]（#Linux_step03）で新しく追加されたポート番号を開放します。
```
firewall-cmd --add-port=新しいポート番号/tcp --permanent
```
たとえば、新しく追加されたポート番号が23456の場合、次のコマンドを実行します。
```
firewall-cmd --add-port=23456/tcp --permanent
```
返される結果が`success`の場合、ポートは正常に構成されています。
7. [セキュリティグループルールの変更]（https://intl.cloud.tencent.com/document/product/213/34825）を参照し、プロトコルポートが「TCP：22」のセキュリティグループルールを[ステップ3]（#Linux_step03）で新しく追加されたポート番号に変更します。
![](https://main.qcloudimg.com/raw/add0bba23dc32f73b5d1fbbdad71c9ab.png)


## 検証操作

### Windows CVMの検証

1. ローカルコンピュータがWindows OSの場合を例として、リモートデスクトップ接続ダイアログボックスを開きます。
2. 次の図に示すように、【コンピュータ】の後に `Windows サーバーのパブリックIP：変更後のポート番号`を入力して、【接続】をクリックします。
![](https://main.qcloudimg.com/raw/1452f968e3c2c4d4c1083bdf0742df9d.png)
3.画面の指示に従って、インスタンスの管理者アカウントとパスワードを入力し、【OK】をクリックします。
Windows CVMのOSインターフェイスが表示された場合は、接続が確立されています。
> RDPファイルを使用してWindows CVMにログインする場合は、以下に示すように、先にRDPファイルの`full address：s`パラメータを変更してください。
>[](https://main.qcloudimg.com/raw/84dd85a9547fc64f2daccba32f1d59d7.png)
>

### Linux CVMの検証

1. リモートログインソフトウェア「PuTTY」を例として、PuTTYクライアントを開きます。
2. PuTTY Configurationウィンドウで、以下に示すように、Linux CVMのパブリックIPを入力し、【Port】を新しいポート番号に設定して、【Open】をクリックします。
![](https://main.qcloudimg.com/raw/c89c2064ed82e738fd60fcab39b09206.png)
3. 画面の指示に従って、Linux CVMのユーザー名とパスワードを入力し、**Enter**キーを押します。
次の画面に進むと、接続が確立されています。
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
4. 新しいポートを使用してLinux CVMに正常に接続した後、以下のコマンドを実行して、デフォルトのポート22をコメントアウトします。
```
vim /etc/ssh/sshd_config
```
5. **i**を押して編集モードに切り替え、`Port 22`の前に`#`を入力して、当該ポートをコメントアウトします。
6. **Esc**キーを押して、**：wq**を入力し、内容を保存して戻ります。
7. 以下のコマンドを実行して、変更後の構成を有効にします。次回ログインする際、新しいポートを使用してリモートでLinux CVMにログインしてください。
```
systemctl restart sshd.service
```

