## 操作シナオリ
このドキュメントでは、CVMインスタンスでMicrosoft SharePoint 2016を構築する方法について説明します。

## ソフトウェアバージョン
このドキュメントでは、例として次のハードウェア仕様のCVMインスタンスを使用しています。
- vCPU：4コア
- メモリ：8GB

このドキュメントでは、例として次のソフトウェアバージョンを使用しています。
- OS：Windows Server 2012 R2 データセンター版 64ビット（中国語）
- データベース：SQL Server 2014

## 前提条件
Windows CVMを購入しました。CVMを購入していない場合は、[ Windows CVMのカスタム設定](https://intl.cloud.tencent.com/document/product/213/10516)をご参照ください。

## 操作手順

### ステップ1：Windowsインスタンスにログインする
[RDPファイルを利用してWindowsインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5435)。また、実際の操作方法により、[リモートデスクトップ接続を利用してWindowsインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32498)こともできます。

<span id="AddAD_DHCP_DNS_IIS"></span>
### ステップ2：AD、DHCP、DNS、およびIISサービスを追加する
1. OS画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> をクリックして、サーバマネージャーを開きます。
2. 左側のナビゲーションメニューバーで【ローカルサーバ】を選択し、【IEセキュリティ強化の構成】を見つけます。以下の通りです。
![](https://main.qcloudimg.com/raw/9192efa291cfbed136db9a6e3a7c3e59.png)
3. 次に示すように、【IEセキュリティ強化の構成】を無効にします。
![](https://main.qcloudimg.com/raw/8b860bb5dfc44ec4993c3a899058b1ae.png)
4. 左側のナビゲーションメニューバーで、【ダッシュボード】を選択し、【役割と機能の追加】をクリックし、「役割と機能の追加ウィザード」ウィンドウを開きます。
5. 「役割と機能の追加ウィザード」ウィンドウで、デフォルト設定のままにして、【次へ】を3回連続でクリックします。
6. 【サーバーの役割の選択】画面で、【Active Directoryドメインサービス】、【DHCPサーバ】、【DNSサーバ】、【Webサーバ(IIS)】を選択し、次のようにポップアップウィンドウで【機能の追加】をクリックします。
![](https://main.qcloudimg.com/raw/532dc46bf0682427e9b210bf36e1986f.png)
7.【次へ】をクリックします。
8.「機能の選択」画面で、【.NET Framework 3.5 】をチェックして、下図に示すように、ポップアップウィンドウで【機能の追加】をクリックしてください。
![](https://main.qcloudimg.com/raw/44998bf3effff6bec51ea9c502ec8c9a.png)
9.デフォルト設定のままにして、【次へ】を6回連続でクリックします。
10. インストール情報を確認し、【インストール】をクリックします。
11.インストールが完了すると、CVMを再起動します。
12. OS画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> をクリックして、サーバマネージャーを開きます。
13. サーバーマネージャウィンドウで、<img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img>をクリックして、【このサーバーをドメインコントローラーに昇格する】を選択します。以下の通りです。
![](https://main.qcloudimg.com/raw/03def6c00f1bed979c9dde28ebbd2202.png)
14. <span id="step14"></span>「配置構成」から「新しいフォレストを追加する(F)」を選択します。ルートドメイン名を入力して、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/adb2e7cbed1580eebeb201d837f41efa.png)
15. <span id="step15"></span>ディレクトリサービス復元モード（DSRM）パスワードを設定し、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/dc24edd5f6d194cacc7b6ff8511417b7.png)
16.デフォルト設定のままにして、【次へ】を4回連続でクリックします。
17.【インストール】をクリックします。
18. OS画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> をクリックして、サーバマネージャーを開きます。
19. 下図に示すように、サーバマネージャーウィンドウで、<img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> をクリックして、画面中央にある【DHCP構成を完了する】をクリックします。
![](https://main.qcloudimg.com/raw/132eb061b6fd53da22b6211fd2411537.png)
20.DHCPサーバーのインストール後、「DHCP インストール後の構成ウィザード」を使って、DHCPサーバーの基本的な構成を行います。【次へ】をクリックします。
21. デフォルト設定のままにして、【コミット】をクリックしてインストールを完了します。
![](https://main.qcloudimg.com/raw/6dab6c5968282757ff2e146c74765772.png)
22. 【閉じる】をクリックして、ウィザードウィンドウを閉じます。

### ステップ3：SQL Server 2014データベースのインストール

1. CVMでブラウザーを開き、SQL Server 2014公式サイトでSQL Server 2014インストールパッケージをダウンロードします。
> SQL Server 2014インストールパッケージは、サードパーティのウェブサイトまたはその他の有効なチャネルから入手することもできます。
>
2. 「Setup.exe」ファイルをダブルクリックして、SQL Serverインストールウィザードを開き、インストールタブ画面に入ります。以下の通りです。
![](https://main.qcloudimg.com/raw/66c2d6df469197d5550ce2fbae3cc5c9.png)
3. 【SQL Server の新規スタンドアロンインストールを実行するか、既存のインストールに機能を追加 】をクリックします。　　
4. 「プロダクト キー」 ページで、オプションを選択して、SQL Server の無償のエディション、または PID キーを持つ製品版のどちらをインストールするかを指定します。 続けるには、【次へ】を選択します。
5. 「ライセンス条項」ページで、ライセンス条項を確認します。 同意する場合は、 【ライセンス条項とプライバシーに関する声明に同意します】 チェックボックスをオンして、【次へ】を選択します。
6. デフォルト設定のままにして、【次へ】をクリックします。　
7. インストールチェックが完了したら、【次へ】をクリックします。
8. デフォルト設定のままにして、【次へ】をクリックします。
9. 「機能の選択」 ページで、「すべて選択」をクリックし、すべての機能にチェックを入れ、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/15bb32c2d2121aadc092428911cefc16.png)
10. 「インスタンス設定」画面で、「デフォルトインスタンス」を選択し、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/3663ca417620325c7b45bc8c60996db7.png)
11. 「サーバーの構成」画面で、SQL ServerデータベースエンジンサービスとSQL Server Analysis Servicesサービスのアカウントとパスワードを設定し、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/c0bb2b960115d66eda4e38b40a56fc78.png)
 - 「SQL Serverデータベースエンジン」のアカウント名を「NT AUTHORITY\NETWORK SERVICE」に設定します。
 - 「SQL Server Analysis Services」のアカウント名とパスワードを、[ステップ2：AD、DHCP、DNS、およびIISサービスの追加](#AddAD_DHCP_DNS_IIS)の [14](#step14) - [15](#step15) で設定されたドメインアカウントとパスワードに設定します。
12. 「データベースエンジン」画面で、【現在のユーザーを追加】をクリックし、現在のアカウントをSQL Serverの管理者アカウントとして使用し、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/c0218409bfb7044221cb6c0fe1862588.png)
13. 「Analysis Services設定」画面で、「現在のユーザーを追加」をクリックし、現在のアカウントにAnalysis Servicesの管理者権限を付与し、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/43243a387cc67f20ea125fb2491df24d.png)
14. デフォルト設定のままにして、【次へ】をクリックします。
15. 「Distributed Replayコントローラ」画面で、「現在のユーザーを追加」をクリックし、現在のアカウントにDistributed Replayコントローラの権限を追加して、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/46158b2f9a6e5f802c2ae27a2f5f0970.png)
16. デフォルト設定のままにして、【次へ】をクリックします。
17. SQL Serverの設定を確認し、【インストール】をクリックします。
18. SQL Serverのインストールが完了したら、【閉じる】をクリックします。


### ステップ4：SharePoint 2016のインストール

1. CVMでブラウザーを開き、Microsoft SharePoint 2016公式サイトからMicrosoft SharePoint 2016インストールパッケージをダウンロードします。
2. 「Microsoft SharePoint 2016」イメージファイルを開き、準備ツールの実行可能ファイル`prerequisiteinstaller.exeをダブルクリックして、Microsoft SharePoint 2016準備ツールをインストールします。以下の通りです。
![](https://main.qcloudimg.com/raw/2de50f6a3172bd870f86378e33f1f07e.png)
3. Microsoft SharePoint 2016 製品準備ツールのウィザードウィンドウが表示されたら、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/e5cd9c8ca37b36984258050443fdf5f1.png)
4. 【使用許諾契約書の条項に同意します】をチェックして、【次へ】をクリック。
5. 必須コンポーネントが順次インストールされるので、終わるまで待ちます。【完了】をクリックしてCVMを再起動します。以下の通りです。
![](https://main.qcloudimg.com/raw/cc8f3bf7b151946d5fdd8f3882ea9549.png)
6.「Microsoft SharePoint 2016」のイメージファイルを開き、インストールファイル`setup.exe`をダブルクリックして、Microsoft SharePoint 2016をインストールします。以下の通りです。
![](https://main.qcloudimg.com/raw/bf0369e20c77e1f57bfef3fef42fab31.png)
7. プロダクトキーを入力し、【続行】をクリックします。
8. 【「マイクロソフトソフトウェア ライセンス条項」に同意します】にチェックを入れ、【続行】をクリック。
9. インストールディレクトリ（この例ではデフォルト設定のままです。必要に応じて適切なインストールディレクトリを選択できます）を選択し、【今すぐインストール】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/0dbdfedb241b02a7f2fdaefb1a7599af.png)
10. インストールが完了したら、【SharePoint 製品構成ウィザードを今すぐ実行する】にチェックを入れたまま、【閉じる】をクリックして、製品構成ウィザードの実行に進みます。以下の通りです。
![](https://main.qcloudimg.com/raw/3fa47faa1f8bed1a8ec478260ee64481.png)

### ステップ5：SharePoint 2016の設定

1. SharePoint製品構成ウィザードウィンドウで、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/3e8d015ab34ab8de8172838dd21d31ac.png)
2. ポップアップボックスで【はい】をクリックし、設定中にサービスを再起動できるようにします。
3. 【新しいサーバーファームの作成】を選択し、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/f87545fb79d747bf64c38131fbb318d4.png)
4. 【構成データベースの設定】 ページで、次の操作を行います。以下の通りです。
SharePointデータベースはローカルホスト上にあるため、ローカルデータベースとアカウントを入力する必要があります。
![](https://main.qcloudimg.com/raw/cf9723c7885399e0e5004f1ecee4ea2d.png)
5. 指定したサーバファームのパスワードを入力し、【次へ】をクリックします。
6. 「マルチサーバファーム」を【フロントエンド】に設定し、【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/95da6977363606dd62835d12bc9b7ae2.png)
7. 「SharePoint サーバーの全体管理 Webアプリケーションの構成」 ページで、次の手順を実行します。「ポート番号を指定する」 チェックボックスをオンにして、SharePoint サーバーの全体管理 Web アプリケーションで使用するポート番号を入力するか、または 「ポート番号を指定する」チェックボックスをオフのままにして、既定のポート番号を使用します。「 NTLM」 または「ネゴシエート (Kerberos)」をクリックします。【次へ】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/26ef65e1e8e229e9c67c2eafc40c0d32.png)
8. 「SharePoint 製品構成ウィザードの完了」 ページで、構成設定を確認し、【次へ】 をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/a0e8ee05fcc2fc4b6f717bb0e03287af.png)
9.「構成成功」 ページで、【完了】をクリックします。

