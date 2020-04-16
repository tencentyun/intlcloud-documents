このドキュメントでは、Cloud Virtual Machineがポートの問題によりリモートログインできない場合のトラブルシューディングと解決案を紹介します。
> 以下の操作はWindows Server 2012のCVMを例にします。
>

## 検査ツール
Tencent Cloudから提供された以下のツールを通じて、ログインできない問題はポートやセキュリティグループ設定と関係があるかどうかを判断することができます：
-  [セルフ診断](https://console.cloud.tencent.com/workorder/check) 
- [セキュリティグループ（ポート）検証ツール](https://console.cloud.tencent.com/vpc/helper)  

セキュリティグループ設定の問題を検出された場合、[セキュリティグループ(ポート)検証ツール](https://console.cloud.tencent.com/vpc/helper)中の【Open all ports】機能を利用して、関連するポートを開放し、再ログインを試みます。ポートを開放してもまだログインできない場合、以下の内容を参照して原因を特定します。

## 特定方法

### ネットワークの接続を検査する

ローカルPingコマンドを通じて、ネットワーク接続をテストすることができます。同時に、異なるネットワーク環境（異なるIPレンジ或いはキャリア）内のコンピューターでテストを行い、ローカルネットワークの問題なのか、サーバーの問題なのかを判断できます。

1. ローカルコンピューターOSが異なるため、Tencent Cloud Command Line Interfaceツールの開き方式を選択します。
 - Windows システム：【スタート】>【実行】をクリックし、**cmd**を入力して、コマンドラインがポップアップされます。
 - Mac OS システム：Terminalツールを開きます。
2. 以下のコマンドを実行してネットワーク接続をテストします。
```
ping + CVM インスタンス パブリックIP アドレス
```
例えば、`ping 139.199.XXX.XXX`コマンドを実行します。
 - ネットワークが正常であれば、以下の結果に戻ります。[リモートデスクトップサービス設定を検査](#F2)してください。
![](https://main.qcloudimg.com/raw/52e6c15bc862dd7724643747ed8abcfb.png)
 - ネットワークに異常があれば、【要求がタイムアウトしました】が提示された場合、[インスタンス IPアドレス Ping 接続できない](https://cloud.tencent.com/document/product/213/14639)を参照して検査してださい。
3. 以下のコマンドを実行し、**Enter**を押して、リモートポートの開放状態をテストし、ポートがアクセスできるかどうかを判断します。
```
telnet + CVM インスタンス パブリックIP アドレス + ポート番号
```
例えば、`telnet 139.199.XXX.XXX 3389`コマンドを実行します。下記画像に示すように：
![](https://mc.qcloudimg.com/static/img/e18be3704977545d5c952d3a583f2ccc/image.png)
 - 正常状態：ブラックスクリーン、カーソルキーのみ表示されます。これはリモートポート(3389)にアクセスできることを示します。[インスタンスのリモートデスクトップサービスが開放しているかどうかを検査](#F2)してください。
 - 異常状態：接続失敗は、下記画像に示すようになります。これはネットワークの問題があることを示します。問題のあるネットワークの該当部分を検査してください。
 ![](https://main.qcloudimg.com/raw/e3996140e2c1895d2ba2b1dfa637f998.png)
 
<span id = "F2"></span>
### リモートデスクトップサービスの設定を検査する

#### VNCの方式でCVMにログインする

> VNC 方式は標準な方式でCVMにログインできない場合、おすすめのログイン方式です。
>
1.  [CVMコンソール](https://console.cloud.tencent.com/cvm)にログインします。
2. チェック対象のCVMを選択し、【ログイン】をクリックします。下記画像に示すように：
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ポップアップした 「Windowsインスタンスにログインする」ウィンドーで、【その他の方式(VNC）】を選択し、【今すぐログイン】をクリックします。
4. ポップアップしたログインウィンドーで、左上の「リモートコマンドの送信」を選択し、 **Ctrl-Alt-Delete** をクリックすると、システムログイン画面に入ります。下図の通りです。
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

#### CVMのリモートデスクトップ設定がオンにしているかどうかを検査する

1. CVMの中で、【PC】>【プロパティ】を右クリックして、「システム」ウィンドウを開きます。
2. 「システム」ウィンドウで、【システムの詳細設定】を選択して、「システムのプロパティ」ウィンドウを開きます。
3. 「システムのプロパティ」ウィンドウの中で、【リモート】タブを選択して、「リモートデスクトップ」機能欄の【このコンピューターへのリモート接続を許可する】をチェックしているかどうかを検査します。下記画像に示すのように：文言修正
![](https://main.qcloudimg.com/raw/2ee4d1abf5ebf351ed814d6644bc7d58.png)
 - はい、リモート接続設定が開放していることを示します。[リモートアクセスポートが開放しているかどうかを確認](#F3)してください。
 - いいえ、【このコンピューターへのリモート接続を許可する】をチェックし、再びリモートでインスタンスを接続して、接続が成功するかどうかを確認します。

<span id = "F3"></span>
### リモートアクセスポートが開放しているかどうかを検査する

1. CVMの中で、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> をクリックして、「Windows PowerShell」ウインドウを開きます。
2. 「Windows PowerShell」ウィンドウの中で、以下のコマンドを実行し、リモートデスクの運行状態を検査します（デフォルトではリモートデスクトップサービスポート番号が3389）。
```
netstat -ant | findstr 3389
```
 - 以下のような結果が返されたら、正常状態であることを示めします。[リモートデスクトップをリスタートし](#F4)てください。再びリモートでインスタンスを接続して、接続が成功するかどうかを確認します。
![](https://main.qcloudimg.com/raw/5206af71e86f8126e9e6845bbeef21b2.png)
 - 接続が表示されない場合は、異常状態であることを示し、[レジストリのリモートポートが一致するかどうかを検査](#F5)してください。

<span id = "F5"></span>
### レジストリのリモートポートが一致するかどうかを検査する

> このステップでは客様に**TCP PortNumber**と**RDP Tcp PortNumer**の二つのポート番号を検査することを指導します。二つのポート番号が一致しなければなりません。
>
1. CVMの中で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>をクリックし、 <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>を選択して、 **regedit**を入力して、**Enter**を押して、「レジストリエディター」ウィンドウを開きます。
2. 左側のレジストリナビゲーションの中で、【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Terminal Server】>【Wds】>【rdpwd】>【Tds】>【tcp】の順でディレクトリを展開します。
3. 【tcp】中の PortNumberを検索し、PortNumberのデータ（ポート番号、デフォルトが3389）を記入します。下記画像に示すように：
![](https://main.qcloudimg.com/raw/e67b696fd25b3355c9038f99a08b90be.png)
4. 左側のレジストリナビゲーションの中で、【HKEY_LOCAL_MACHINE】>【SYSTEM】>【CurrentControlSet】>【Control】>【Terminal Server】>【WinStations】>【RDP-Tcp】の順でディレクトリを展開します。
5. 【RDP-Tcp】中の PortNumberを検索し、【RDP-Tcp】中の PortNumber データ（ポート番号）は【tcp】中の PortNumber データ（ポート番号）が一致するかどうかを確認します。下記の画像に示すように：
![](https://main.qcloudimg.com/raw/8240dd43dcb3ca246caf3397e4a1e84f.png)
 - 一致しなければ、[ステップ 6](#F5_step6) を実行してください。
 - 一致すれば、[リモートログインサービスをリスタート](#F4)をしてください。
6.【RDP-Tcp】中のPortNumberをダブルクリックします。
7. ポップアップしたダイアログボックスの中で、「値のデータ」を0 - 65535の間でまだ占用していないポートに修正して、**TCP PortNumber**と**RDP Tcp PortNumer**のポート番号を一致させて、【OK】クリックします。
7. 修正した後、[CVMコンソール](https://console.cloud.tencent.com/cvm) でインスタンスをリスタートします。再びリモートでインスタンスを接続して、接続が成功するかどうかを確認します。


<span id = "F4"></span>
### リモートログインサービスをリスタートする

1. CVMの中で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>をクリックし、<img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>を選択して、 **services.msc**を入力して、**Enter**を押して、「サービス」ウィンドウを開きます。
2. 「サービス」ウィンドウの中で、【Remote Desktop Services】を検索し、【Remote Desktop Services】を右クリックして、【再開】を選択して、リモートログインサービスをリスタートします。下記の画像に示すように：
![](https://main.qcloudimg.com/raw/396ee711bb64c8fb1966112a81dd0fd4.png)

## その他の操作

上記の操作でまだ問題が解決されていない場合は、 [チケットを発行](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)してフィードバックしてください。
