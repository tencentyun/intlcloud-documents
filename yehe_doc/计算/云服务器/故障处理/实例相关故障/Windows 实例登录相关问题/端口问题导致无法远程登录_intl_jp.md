このドキュメントでは、Cloud Virtual Machineがポートの問題によりリモートログインできない場合のトラブルシューディングと解決案について説明します。
> 以下の操作は、Windows Server 2012システムを使用したCVMを例にします。
>

## 検証ツール
Tencent Cloudが提供するツールを使用して、ログインできない問題はポートとセキュリティグループの設定に関連しているかどうかを判断することができます：
-  [セルフ診断](https://console.cloud.tencent.com/workorder/check) 
- [セキュリティグループ（ポート）検証ツール](https://console.cloud.tencent.com/vpc/helper)  

セキュリティグループの設定の問題を検出された場合、[セキュリティグループ(ポート)検証ツール](https://console.cloud.tencent.com/vpc/helper)中の【Open all ports】機能を利用して、関連するポートを開放し、再度ログインを試みます。ポートを開放してもまだログインできない場合、以下の内容を参照して原因を特定します。

## トラブルシューティング

### ネットワーク接続を検査する

ローカルのPingコマンドを通じて、ネットワーク接続をテストすることができます。同時に、異なるネットワーク環境（異なるIPレンジ或いはキャリア）のコンピューターでテストを行い、ローカルネットワークの問題なのか、サーバーの問題なのかを確認できます。

1.ローカルコンピューターでコマンドラインツールを開きます。
 - Windows システム：【スタート】>【実行】をクリックし、**cmd**を入力すると、コマンドラインダイアログボックスが表示されます。
 - Mac OS システム：Terminalツールを開きます。
2. 以下のコマンドを実行して、ネットワーク接続をテストします。
```
ping + CVM インスタンスのパブリックIP アドレス
```
例えば、`ping 139.199.XXX.XXX`コマンドを実行します。
 - ネットワークが正常な場合、次の果が返されます。[リモートデスクトップサービス設定を検査](#F2)してください。
![](https://main.qcloudimg.com/raw/52e6c15bc862dd7724643747ed8abcfb.png)
 - ネットワークに異常がある場合、【要求がタイムアウトしました】が提示された場合、[インスタンスIPアドレスのPingの失敗](https://cloud.tencent.com/document/product/213/14639)を参照して検査してださい。
3. 以下のコマンドを実行し、**Enter**キーを押して、リモートポートの開放状態をテストし、ポートにアクセスできるかどうかを判断します。
```
telnet + CVM インスタンスのパブリックIP アドレス + ポート番号
```
例えば、`telnet 139.199.XXX.XXX 3389`コマンドを実行します。下記画像に示すように：
![](https://mc.qcloudimg.com/static/img/e18be3704977545d5c952d3a583f2ccc/image.png)
 - 正常状態：ブラックスクリーン、カーソルキーのみ表示されます。これはリモートポート(3389)にアクセスできることを示しています。[インスタンスのリモートデスクトップサービスが有効になっているかどうかを確認](#F2)してください。
 - 異常状態：接続失敗は、下記画像に示すようになります。これはネットワークに問題があることを示しています。問題のあるネットワークの該当部分を検査してください。
 ![](https://main.qcloudimg.com/raw/e3996140e2c1895d2ba2b1dfa637f998.png)
 
<span id = "F2"></span>
### リモートデスクトップサービスの設定を検査する

#### VNCを介してCVMにログインする

> 標準方式でCVMにログインできない場合、VNC方式を使用することをお勧めします。
>
1.  [CVMコンソール](https://console.cloud.tencent.com/cvm)にログインします。
2. チェックするCVMを選択し、【ログイン】をクリックします。下記画像に示すように：
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ポップアップした 「Windowsインスタンスにログインする」ウィンドウで、【その他の方式(VNC）】を選択し、【すぐにログインする】をクリックします。
4. ポップアップしたログインウィンドウで、左上隅にある「Sent CtrlAltDe」を選択し、 **Ctrl-Alt-Delete** をクリックすると、システムログイン画面に入ります。下図の通りです。
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

#### CVMのリモートデスクトップ設定が有効になっているかどうかを確認する

1. CVMで、【PC】>【プロパティ】を右クリックして、「システム」ウィンドウを開きます。
2. 「システム」ウィンドウで、【システムの詳細設定】を選択して、「システムのプロパティ」ウィンドウを開きます。
3. 「システムのプロパティ」ウィンドウで、【リモート】タブを選択して、「リモートデスクトップ」機能欄の【このコンピューターへのリモート接続を許可する】をチェックしているかどうかを確認します。下記画像に示すのように：
![](https://main.qcloudimg.com/raw/2ee4d1abf5ebf351ed814d6644bc7d58.png)
 - はい、リモート接続設定が有効になっています。[リモートアクセスポートが開いているかどうかを確認](#F3)してください。
 - いいえ、【このコンピューターへのリモート接続を許可する】をチェックし、もう一度インスタンスにリモート接続して、接続が成功したかどうかを確認します。

<span id = "F3"></span>
### リモートアクセスポートが開いているかどうかを確認する

1. CVMで、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> をクリックして、「Windows PowerShell」ウインドウを開きます。
2. 「Windows PowerShell」ウィンドウで、以下のコマンドを実行し、リモートデスクトップの運行状態を確認します（デフォルトでは、リモートデスクトップサービスのポート番号が3389です）。
```
netstat -ant | findstr 3389
```
 - 以下のような結果が返されたら、正常状態であることを示します。[リモートデスクトップを再起動](#F4)してください。もう一度インスタンスにリモート接続して、接続が成功したかどうかを確認できます。
![](https://main.qcloudimg.com/raw/5206af71e86f8126e9e6845bbeef21b2.png)
 - 接続が表示されない場合は、異常状態であることを示し、[レジストリのリモートポートが一致するかどうかを確認](#F5)してください。

<span id = "F5"></span>
### レジストリのリモートポートが一致するかどうかを確認する

> このステップでは、 **TCP PortNumber**と **RDP Tcp PortNumer** が同じであるかどうかを確認します。
>
1. CVMで、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>をクリックし、 <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>を選択して、 **regedit**を入力して、**Enter**キーを押して、「レジストリエディター」ウィンドウを開きます。
2. 左側のレジストリナビゲーションで、【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Terminal Server】>【Wds】>【rdpwd】>【Tds】>【tcp】の順でディレクトリを展開します。
3. 【tcp】でPortNumberを見つけて、PortNumberデータ（ポート番号、デフォルトが3389）を記入します。下記画像に示すように：
![](https://main.qcloudimg.com/raw/e67b696fd25b3355c9038f99a08b90be.png)
4. 左側のレジストリナビゲーションで、【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Terminal Server】>【WinStations】>【RDP-Tcp】の順でディレクトリを展開します。
5. 【RDP-Tcp】でPortNumberを見つけて、【RDP-Tcp】中のPortNumberデータ（ポート番号）が【tcp】中のPortNumberデータ（ポート番号）と同じかどうかを確認します。下記の画像に示すように：
![](https://main.qcloudimg.com/raw/8240dd43dcb3ca246caf3397e4a1e84f.png)
 - 同じでない場合、[ステップ 6](#F5_step6) を実行してください。
 - 同じ場合は、[リモートログインサービスを再起動](#F4)してください。
6.【RDP-Tcp】中のPortNumberをダブルクリックします。
7. ポップアップしたダイアログボックスで、「値データ」を0 - 65535の間で未使用ポートに変更して、**TCP PortNumber**と**RDP Tcp PortNumer**のポート番号を一致させて、【OK】クリックします。
8. 変更後、[CVMコンソール](https://console.cloud.tencent.com/cvm) でインスタンスを再起動します。もう一度インスタンスにリモート接続して、接続が成功したかどうかを確認します。


<span id = "F4"></span>
### リモートログインサービスを再起動する

1. CVMの中で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>をクリックし、<img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>を選択して、 **services.msc**を入力して、**Enter**キーを押して、「サービス」ウィンドウを開きます。
2. 「サービス」ウィンドウで、【リモートデスクトップサービス】を見つけて右クリックします。【再開】を選択して、リモートログインサービスを再起動します。下記の画像に示すように：
![](https://main.qcloudimg.com/raw/396ee711bb64c8fb1966112a81dd0fd4.png)

## その他の操作

上記操作を行ってもリモートでログインできない場合は、 [チケットを送信](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)してフィードバックしてください。
