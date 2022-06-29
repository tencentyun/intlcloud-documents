## ユースケース
このドキュメントでは、CVMインスタンス上でMicrosoft SharePoint 2016を構築する方法についてご説明します。

## ソフトウェアバージョンの例
ここで例に挙げる手順において使用するCVMインスタンスのハードウェア仕様は次のとおりです。
- vCPU：4コア
- メモリ： 8GB

ここで例に挙げる手順では、次のソフトウェアバージョンを使用しています。
- OS：Windows Server 2012 R2 データセンターバージョン64ビット英語版
- データベース：SQL Server 2014

## 前提条件
Windows CVMを購入済みであること。CVMを購入していない場合は、[Windows CVMのクイック設定](https://intl.cloud.tencent.com/document/product/213/10516)をご参照ください。

## 操作手順

### ステップ1：Windowsインスタンスへのログイン
[RDPファイルを使用してWindowsインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5435)します。実際の操作習慣に合わせて、[リモートデスクトップを利用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32498)することもできます。


### ステップ2：AD、DHCP、DNS、IISサービスの追加[](id:AddAD_DHCP_DNS_IIS)
1. OSの画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>をクリックして、サーバーマネージャーを開きます。
2. 下図のように、左側ナビゲーションバーで**ローカルサーバー**を選択し、**Internet Explorer拡張セキュリティ構成**を見つけます。
![](https://main.qcloudimg.com/raw/c2b0791555bbc910cea70732c75daa0f.png)
3. 下図のように、**Internet Explorer拡張セキュリティ構成**をオフにします。
![](https://main.qcloudimg.com/raw/6acbf171bc703100401e48e362539b21.png)
4. 左側ナビゲーションバーで**ダッシュボード**を選択し、**ロールと機能の追加**をクリックして、「ロールと機能の追加ウィザード」ウィンドウを開きます。
5. 「ロールと機能の追加ウィザード」ウィンドウで、デフォルトの設定を維持したまま、**次へ**を3回続けてクリックします。
6. 下図のように、「サーバーロールの選択」画面で、**Active Directoryドメインサービス**、**DHCPサーバー**、**DNSサーバー**、**Webサーバー(IIS)**にチェックを入れ、ポップアップしたウィンドウで**機能の追加**をクリックします。
![](https://main.qcloudimg.com/raw/a2bb1c86c9277ca870c629ecf5b0d3f5.png)
7. **次へ**をクリックします。
8. 下図のように、「機能の選択」画面で、「.NET Framework 3.5機能」にチェックを入れ、ポップアップしたウィンドウで**機能の追加**をクリックします。
![](https://main.qcloudimg.com/raw/bf47abbb95ad42b9d6c720c3bb2c846b.png)
9. デフォルトの設定を維持したまま、**次へ**を6回続けてクリックします。
10. インストール情報を確認し、**インストール**をクリックします。
11. インストールの完了後にCVMを再起動します。


### ステップ3： ADサービスの設定
1. OSの画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>をクリックして、サーバーマネージャーを開きます。
2. 下図のように、サーバーマネージャーのウィンドウで、<img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img>をクリックして、**このサーバーをドメインコントローラに変更する**を選択します。
![](https://main.qcloudimg.com/raw/1e6aa1d75044898357709909bb969c6f.png)
3. [](id:step14)下図のように、表示された「Active Directoryドメインサービスの設定ウィザード」画面で、「デプロイ操作の選択」を**フォレストの新規追加**に設定し、ルートドメイン名を入力し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/017acc0e5939632f3808698f36320fd2.png)
4. [](id:step15)下図のように、ディレクトリサービス復元モデル（DSRM）のパスワードを設定して、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/078672b95294790e4985108bd58d8504.png)
5. デフォルトの設定を維持したまま、**次へ**を4回続けてクリックします。
6. **インストール**をクリックします。

### ステップ4： DHCPサービスの設定
1. OSの画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>をクリックして、サーバーマネージャーを開きます。
2. 下図のように、サーバーマネージャーのウィンドウで、<img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img>をクリックして、**DHCPの設定を完了する**を選択します。
![](https://main.qcloudimg.com/raw/4c65a7990acc647866d73c1b5ba20a6c.png)
3. 表示された「DHCPインストール後設定ウィザード」ウィンドウで、**次へ**をクリックします。
4. 下図のように、デフォルトの設定を維持し、**送信**をクリックすると、インストール設定が完了します。
![](https://main.qcloudimg.com/raw/4162a8fbde1b7af1d8fadacaa61965cf.png)
5. **閉じる**をクリックし、ウィザードウィンドウを閉じます。

### ステップ5：データベースSQL Server 2014のインストール

1. CVMでブラウザを開き、SQL Server 2014公式サイトにアクセスし、SQL Server 2014インストールパッケージをダウンロードします。
<dx-alert infotype="explain" title="">
サードパーティのウェブサイトまたはその他の合法的な手段によってSQL Server 2014インストールパッケージを入手することもできます。
</dx-alert>
2. 「Setup.exe」ファイルをダブルクリックしてSQL Serverインストールウィザードを開き、下図のように、インストールオプションタブ画面で**新SQL Serverの単体インストールまたは既存のインストールに機能を追加する**をクリックします。
![](https://main.qcloudimg.com/raw/f2cc33aef5ec2662238ffeca56d08a7d.png)
3. 製品キーを入力し、**次へ**をクリックします。
4. 「ライセンス条項に同意する」にチェックを入れ、**次へ**をクリックします。
5. デフォルトの設定を維持したまま、**次へ**をクリックします。
6. インストールチェックの完了後、**次へ**をクリックします。
7. デフォルトの設定を維持したまま、**次へ**をクリックします。
8. 下図のように、「機能の選択」画面で**すべて選択**をクリックし、すべての機能を選択して**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/92eac7b681dae5937bafa484874ae122.png)
9. 下図のように、「インスタンスの設定」画面で**デフォルトのインスタンス**を選択し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/2bf1682b927b66224c574435ee35e7af.png)
10. 下図のように、「サーバーの設定」画面で、SQL ServerデータベースエンジンサービスおよびSQL Server Analysis Servicesのアカウントとパスワードを設定し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/1310d9db077772be6dad6f58a698273e.png)
 - 「SQL Serverデータベースエンジン」のアカウント名を「NT AUTHORITY\NETWORK SERVICE」に設定します。
 - 「SQL Server Analysis Services」のアカウント名とパスワードに、[ステップ2：AD、DHCP、DNS、IISサービスの追加](#AddAD_DHCP_DNS_IIS) 中 [14](#step14) - [15](#step15)で設定したドメインアカウントとパスワードを設定します。
11. 下図のように、「データベースエンジン」画面で、**現在のユーザーを追加する**をクリックし、現在のアカウントをSQL Serverの管理者アカウントとし、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/90ac80988b45a6b08650d97fd0d08c09.png)
12. 下図のように、「Analysis Servicesの設定」画面で、**現在のユーザーを追加する**をクリックし、現在のアカウントにAnalysis Servicesの管理者権限を追加し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/5fda4e9b2ac31d8394ab0dfa14847d73.png)
13. デフォルトの設定を維持したまま、**次へ**をクリックします。
14. 下図のように、「Distributed Replayコントローラ」画面で、**現在のユーザーを追加する**をクリックし、現在のアカウントにDistributed Replayコントローラの権限を追加し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/2b67cc38051c51cb88ba7bbb740027b3.png)
15. デフォルトの設定を維持したまま、インストールが完了するまで**次へ**をクリックします。


### ステップ6：SharePoint 2016のインストール

1. CVMでブラウザを開き、Microsoft SharePoint 2016公式サイトにアクセスし、Microsoft SharePoint 2016インストールパッケージをダウンロードします。
2. 下図のように、Microsoft SharePoint 2016イメージファイルを開き、準備ツールの実行可能ファイル`prerequisiteinstaller.exe`をダブルクリックし、Microsoft SharePoint 2016準備ツールをインストールします。
![](https://main.qcloudimg.com/raw/1c6c2e0970ea456bbabd4a77ef454a5e.png)
3. 下図のように、表示されたMicrosoft SharePoint 2016製品準備ツールのウィザードウィンドウで、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/4b42cde60ca558a7c905c6f8031e3a50.png)
4. 「ライセンス規約の条項に同意する」にチェックを入れ、**次へ**をクリックします。
5. 下図のように、必須コンポーネントのインストールが完了してから、**完了**をクリックし、CVMを再起動します。
![](https://main.qcloudimg.com/raw/a8c14625c359decb9941511e267ea2a6.png)
6. 下図のように、Microsoft SharePoint 2016イメージファイルを開き、インストールファイル`setup.exe`をダブルクリックし、Microsoft SharePoint 2016のインストールを開始します。
![](https://main.qcloudimg.com/raw/2614739955551657148d9c3a72e566df.png)
7. 製品キーを入力し、**続ける**をクリックします。
8. 「この規約の条項に同意する」にチェックを入れ、**続ける**をクリックします。
9. 下図のように、インストールディレクトリを選択し（この例ではデフォルト設定を維持していますが、実際の状況に応じて対応するインストールディレクトリを選択できます）、**今すぐインストール**をクリックします。
![](https://main.qcloudimg.com/raw/3ea703e1632ec78b3f8f4b961c189208.png)
10. インストールの完了後、下図のように、「SharePoint製品設定ウィザードを今すぐ実行する」にチェックを入れ、**閉じる**をクリックします。
![](https://main.qcloudimg.com/raw/368fa9a4cdb3b47a77c554db855737e0.png)

### ステップ7：SharePoint 2016の設定

1. 下図のように、実行したSharePoint製品設定ウィザードで、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/73aa25130b0e24e6784760a28d6d8fe2.png)
2. ポップアップしたプロンプトウィンドウで、**はい**をクリックし、設定途中でのサービスの再起動を許可します。
3. 下図のように、**サーバーファームを新規作成する**を選択し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/b66da626c4883f2f2fb1b75bce6042f6.png)
4. 下図のように、データベース設定とデータベースにアクセスするアカウントの情報を指定し、**次へ**をクリックします。
Sharepointのデータベースはローカルマシンにあるため、ローカルマシンのデータベースとアカウントを入力します。
![](https://main.qcloudimg.com/raw/d1ccac780ddb9fb308b071fe385ad3f6.png)
5. 指定するサーバーファームのパスワードを設定し、**次へ**をクリックします。
6. 下図のように、「マルチサーバーファーム」を**フロントエンド**に設定し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/c23051f73ae543002bc9c15d3d2b3387.png)
7. 下図のように、Sharepoint管理センターのポート番号を設定し（この例ではポート番号を10000としていますが、ポート番号は実際の状況に応じて設定することができます）、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/c7622761e6eb45b1935fccc851379b29.png)
8. 下図のように、SharePointの設定を確認し、**次へ**をクリックします。
![](https://main.qcloudimg.com/raw/8d97c6aff42bb8b27fb3e108fa3d16d8.png)
9. SharePointの設定完了後、**完了**をクリックします。

