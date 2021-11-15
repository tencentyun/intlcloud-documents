ここでは、インスタンスを作成し初期化した後、プライベートネットワークまたはパブリックネットワークアドレスを介してMySQLインスタンスに接続する方法をご紹介します。

## 準備作業
- 初期化されたMySQLインスタンスを準備します。[MySQLインスタンスの初期化](https://intl.cloud.tencent.com/document/product/236/3128)をご参照ください。
- データベースアカウントを準備し、 MySQLへのアクセスを許可するIPを承認します。[アカウントの作成](https://intl.cloud.tencent.com/document/product/236/31900)、[アクセス権限を付与するホストアドレスの修正](https://intl.cloud.tencent.com/document/product/236/31903)をご参照ください。なおrootアカウントを直接使用することもできます。
クラウドサーバーCVMとMySQLのセキュリティグループのインバウンドおよびアウトバウンドルールを設定し、MySQLへのアクセスを許可するIPを制限します。 [クラウドデータベースのセキュリティグループの管理](https://intl.cloud.tencent.com/document/product/236/14470)をご参照ください。

##接続方式
TencentDB for MySQLを接続する方法は次のとおりです。
- **プライベートネットワークアドレス接続**：プライベートネットワークアドレスを介してTencentDB for MySQLに接続し、CVMを使用してクラウドデータベースのプライベートネットワークアドレスに直接接続します。この接続方法は低遅延の高速プライベートネットワークを使用します。
 - CVMとデータベースは同一アカウントで、かつ同一の［VPC］(https://intl.cloud.tencent.com/document/product/215/535)内（同一のリージョンであることを保障するため）、または同一の基本ネットワーク内にある必要があります。
 - プライベートネットワークアドレスはシステムによってデフォルトで提供され、[MySQLコンソール](https://console.cloud.tencent.com/cdb) のインスタンスリストまたはインスタンス詳細ページで確認することができます。
>?異なるVPC（同一アカウント/異なるアカウント、同一リージョン/異なるリージョンを含む）のCVMとデータベースのプライベートネットワーク接続方式については、[CCN](https://intl.cloud.tencent.com/zh/document/product/1003)をご参照ください。
>
- **パブリックネットワークアドレス接続**：プライベートネットワークを介して接続できない時は、パブリックネットワークアドレス経由でTencentDB for MySQLに接続することができます。パブリックネットワークアドレスは[手動で有効化する](#waiwang)必要があり、[MySQLコンソール](https://console.cloud.tencent.com/cdb) のインスタンス詳細ページで表示することができ、不要な場合は無効にすることもできます。
 - 広州、上海、北京、成都、重慶、南京、中国香港、シンガポール、ソウル、東京、シリコンバレー、フランクフルトなどの各リージョンのマスターインスタンスは、パブリックネットワークアドレス接続アドレスの有効化をサポートしています。読み取り専用インスタンスはパブリックネットワークが有効なリージョンをサポートしていますので、コンソールを基準としてください。
 - パブリックネットワークアドレスを有効化すると、データベースサービスがパブリックネットワークに公開され、データベースへの侵入や攻撃が発生する恐れがあります。プライベートネットワーク接続を使用してデータベースに接続することをお勧めします。 
 - クラウドデータベースのパブリックネットワーク接続は、データベースの開発または管理補助にご使用ください。パブリックネットワーク接続が利用できなくなる制御できない要因（DDOS攻撃、突然の大量トラフィックアクセスなど）が存在する恐れがあるため、正式な業務の接続に使用することはお勧めしません。


次の例では、Windows CVMまたはLinux CVMからログインし、プライベートネットワークとパブリックネットワークという2つの異なる方法でTencentDB for MySQLに接続する方法をそれぞれご紹介します。
## Windows CVMからの接続
1. Windows CVMにログインします。 <a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">クイックコンフィグレーションWindows CVM</a>をご参照ください。
2. 標準のSQLクライアントをダウンロードします。
>?MySQL Workbenchをダウンロードし、システムに応じて適合するバージョンのインストールプログラムをダウンロードすることをお勧めします。ダウンロードアドレスについては、https://dev.mysql.com/downloads/workbench/をご参照ください。
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. インターフェースに**Login**、**Sign Up**および**No, thanks, just start my download.**が表示されますので、**No thanks, just start my download.**を選択し、クイックダウンロードします。
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. このCVMにMySQL Workbenchをインストールします。
>?
>- このコンピューターには、Microsoft .NET Framework 4.5およびVisual C++ Redistributable for Visual Studio 2015をインストールする必要があります。
>- MySQL Workbenchインストールウィザードの**Download Prerequisites**をクリックし、該当するページにジャンプしてこの2つのソフトウェアをダウンロードしてインストールしてから、MySQL Workbenchをインストールします。
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. MySQL Workbenchを開き、**Database**>**Connect to Database**を選択し、MySQLデータベースインスタンスのプライベートネットワーク（またはパブリックネットワーク）アドレス、ユーザー名、パスワードを入力し、**OK**をクリックしてログインします。
 - Hostname:プライベートネットワーク（またはパブリックネットワーク）アドレスを入力します。[MySQLコンソール](https://console.cloud.tencent.com/cdb) のインスタンス詳細ページでプライベートネットワーク（またはパブリックネットワーク）アドレスとポート番号を確認することができます。パブリックネットワークアドレスの場合は、有効化されているかどうかを確認してください。[パブリックネットワークアドレスの有効化](#waiwang)をご参照ください。
 - Port:プライベートネットワーク（またはパブリックネットワーク）対応ポート。
 - Username:デフォルトはrootです。接続の制御と管理を容易にするため、パブリックネットワーク接続時に個別に[アカウントの作成](https://intl.cloud.tencent.com/document/product/236/31900) を行うことをお勧めします。
 - Password:Usernameに対応するパスワードです。パスワードを忘れた場合は、[パスワードの再設定](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更することができます。
![](https://main.qcloudimg.com/raw/946b50fb05de11d7c68c2262ac4fe933.png)
6. ログインに成功したページは図に示すとおりです。このページでは、MySQLデータベースの各種スキーマとオブジェクトを確認することができます。テーブルの作成を開始し、データの挿入とクエリー操作を実行できます。
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## Linux CVMからの接続
1. Linux CVMにログインします。<a href="https://intl.cloud.tencent.com/document/product/213/10517" target="_blank">クイックコンフィグレーション Linux CVM</a>をご参照ください。
2. ここではCentOS 7.2 64ビットシステムのCVMを例として説明します。次のコマンドを実行してMySQLクライアントをインストールします。
```
yum install mysql
```
`Complete!`の表示は、MySQLクライアントのインストールが完了したことを意味します。
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)
3. 接続方式に応じて、対応する操作を選択します。
 - **プライベートネットワーク接続時：**
    1. 次のコマンドを実行し、MySQLデータベースインスタンスにログインします。
```
mysql -h hostname -u username -p
```
      - hostname:対象のMySQLデータベースインスタンスのプライベートネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでプライベートネットワークアドレスを確認することができます。
    	- username:デフォルトのユーザー名rootに置き換えます。
    2. `Enter password：`が表示されたら、MySQLインスタンスのrootアカウントに対応するパスワードを入力します。パスワードを忘れた場合は、[パスワードの再設定](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更することができます。
    この例では、`MySQL [(none)]>`の表示は、MySQLに正常にログインしたことを意味します。
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **パブリックネットワーク接続時：**

    1. 次のコマンドを実行し、MySQLデータベースインスタンスにログインします。
```
mysql -h hostname -P port -u username -p
```
      - hostname:対象のMySQLデータベースインスタンスのパブリックネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb) のインスタンス詳細ページでパブリックネットワークアドレスとポート番号を確認することができます。パブリックネットワークアドレスが有効化されていない場合は、 [パブリックネットワークアドレスの有効化](#waiwang)を参照して有効化してください。
      - port:パブリックネットワークポート番号に置き換えます。
      - username:パブリックネットワーク接続に使用するパブリックネットワーク接続ユーザー名に置き換えます。接続の制御と管理を容易にするため、個別に [アカウントの作成](https://intl.cloud.tencent.com/document/product/236/31900) を行うことをお勧めします。
    2. `Enter password：`が表示されたら、パブリックネットワーク接続ユーザー名に対応するパスワードを入力します。パスワードを忘れた場合は、[パスワードの再設定](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更することができます。
    この例では、hostnameは59281c4exxx.myqcloud.com、パブリックネットワークポート番号は15311です。
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. `MySQL \[(none)]>`プロンプトが表示されたら、SQLステートメントを実行したいMySQLサーバーに送信することができます。具体的なコマンドについては、 [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html)をご参照ください。
下図に`show databases;`を例示します。
![](https://main.qcloudimg.com/raw/2873c8675d0ce123771a63dbf05df8b9.png)

## 付録1：インスタンスに接続できない問題
インスタンスに接続できない問題が発生した場合は、[クイック接続チェックツール](https://intl.cloud.tencent.com/document/product/236/31927)を使用して調査を行い、チェックレポートの表示に従って、[インスタンスに接続できない場合](https://intl.cloud.tencent.com/document/product/236/40333) で対応する解決方法を検索してください。

## 付録2：ネットワーク接続性検証方法
ネットワーク接続の問題を迅速に調査して特定するには、telnetコマンドを使用することをお勧めします。[telnetコマンド](https://intl.cloud.tencent.com/document/product/236/31929)をご参照ください。

telnetでクラウドデータベースのネットワークアクセスが正常であることを検証した後、CVMのコマンドラインからクラウドデータベースにログインする際にエラーが報告された場合は[インスタンスの接続に関する問題](https://intl.cloud.tencent.com/document/product/236/37783)をご参照ください。

## 付録3パブリックネットワーク接続アドレスの有効化](id:waiwang)
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb/ )にログインし、インスタンスリストのインスタンス名または「操作」の列の**管理**をクリックし、インスタンス詳細ページに進みます。
2. インスタンス詳細ページの「パブリックネットワークアドレス」で、**有効化**をクリックします。
>?パブリックネットワークアドレスとパブリックネットワークポート情報があれば、パブリックネットワークアドレスが有効化されたことを意味します。
>
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
3. ポップアップしたダイアログボックスで、**OK**をクリックします。
>?
>- 有効化に成功したら、基本情報でパブリックネットワークアドレスを確認することができます。
>- 切り替えによりパブリックネットワーク接続権限をオフにした後、パブリックネットワーク接続を再開することができます。この時、ドメイン名に対応するパブリックネットワークアドレスは変更されません。
