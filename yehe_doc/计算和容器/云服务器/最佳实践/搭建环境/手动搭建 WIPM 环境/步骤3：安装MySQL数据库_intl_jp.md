本ドキュメントでは、Windows Server 2012 R2を例として、MySQL 5.5を構築するための具体的な手順を紹介します。

SQL Serverデータベースは、Windowsシステムで頻繁に使用されます。 SQL Serverは有料製品であるため、ユーザーがSQL Serverの承認を取得する必要があります。また、[Tencent Cloud  SQL Serverデータベース CDB インスタンス](http://cloud.tencent.com/product/sqlserver.html)を購入することもできます。

## 手順一： MySQLインストールパッケージをダウンロードする
&nbsp;&nbsp;&nbsp;CVMでブラウザを開き、ダウンロードアドレスを入力します：https://dev.mysql.com/downloads/mysql/5.5.html#downloads
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](//mc.qcloudimg.com/static/img/b1da1513321247e0daf1163f529d4cd9/image.png)

## 手順二：プログラムをインストールする
 1. インストールプログラムを実行し、【次へ(Next)】をクリックします。
![](//mc.qcloudimg.com/static/img/8dd2fc106b09c3538c1dd407c02adea4/image.png)
 
 2. 標準インストール(Typical)を選択します。
![](//mc.qcloudimg.com/static/img/9f45d5441da017feca7eb9bdc11260fd/image.png)

 3. [MySQLインスタンス構成ウィザードの起動]（Luanch the MySQL Instance Configuration Wizard）を選択します。
	![](//mc.qcloudimg.com/static/img/1a6b6ad499c0c00d294d6f24d5ee1645/image.png)

## 手順三：MySQLを設定する


 1. MySQLのタイプを設定します。ここでは、詳細な設定を例として説明します。
  - 詳細設定(Detailed Configuration)は、CVM設定をより細かく制御する必要がある上級ユーザーに適しています。
  - 標準設定(Standard Configuration)は、CVM設定を考慮することなく、MySQLをすばやく起動したい新規ユーザーに適しています。
 
 > **注意事項：**
 > 標準設定(Standard Configuration)は、OSと互換性がない可能性があります。 詳細設定を選択することをお勧めします。

	![](//mc.qcloudimg.com/static/img/434424a84d76f9492c511f567ae2d03f/image.png)
 
 2.  MySQLサーバーの種類を設定します。 ここでは、Developer Machineを例として説明します。
  -Developer Machineは典型的な個人用デスクトップワークステーションです。複数のデスクトップアプリケーションを同時に実行している場合、MySQLのサーバーがリソース使用率最小限の状態に設定します。
  -  サーバーマシン（Server Machine）はサーバーを表します。MySQLサーバーがFTP、電子メール、Webサーバーなどの他のアプリケーションと共に実行できます。MySQLサーバーが適切な比率でリソースを占める状態に設定します。　
  - 専用MySQLサーバーマシン（Dedicated MySQL Server Machine）はMySQLサービスのみを実行するサーバーを表します。MySQLサーバーがすべてのリソースを使用できる状態に設定します。

	![](//mc.qcloudimg.com/static/img/11b1162dd70e46882a43933f517dcaf4/image.png)

 3. MySQLデータベースを設定します。 ここでは、多機能データベース(Multifunctional Database)を例として説明します。
  - 多機能データベース（Multifunctional Database）は InnoDB と MyISAM ストレージエンジンを同時に使用できます。また、2つのエンジンにリソースを均等に割り当てます。このオプションは、2つのストレージエンジンを頻繁に使用するユーザーにお勧めします。
  - トランザクション処理データベース（Transactional Database Only）はInnoDBとMyISAMストレージエンジンを同時に使用しますが、ほとんどのサーバーリソースをInnoDBストレージエンジンの方に割り当てます。InnoDBを頻繁に使用し、偶にMyISAMを使用するユーザーにこのオプションを選択することをお勧めします。
  - 非トランザクション処理データベース（Non-Transactional Database Only）はInnoDBストレージエンジンの使用を完全に禁止し、すべてのサーバーリソースをMyISAMストレージエンジンの方に割り当てます。InnoDBを利用しないユーザーにこのオプションを選択することをお勧めします。
 
 ![](//mc.qcloudimg.com/static/img/37972855d5c880e59b5310a7872491f1/image.png)

 4. MySQLのInnoDBテーブルスベースを設定します。ここではデフォルト設定を選択します。
	![](//mc.qcloudimg.com/static/img/c4c8e8710e27b202a9694b2c1be0f4f6/image.png)

 5. MySQLの同時接続を設定します。 ここでは、デシジョンサポート(Decision Support)を例として説明します。
  - デシジョンサポート（Decision Support）は多数同時接続を必要としない場合に適しています。
  - オンライントランザクション処理（Online Transaction Processing ）は多数同時接続を必要とする場合に適しています。
  - 手動設定（Manual Setting）はサーバの最大同時接続数を手動で設定する必要がある場合に適しています。
 
 ![](//mc.qcloudimg.com/static/img/ef17aa905ea5bdd50b1ad61b416be4ea/image.png)

 6. MySQLのネットワークオプションを設定します。TCP/IPネットワークを有効または無効にし、MySQLサーバーへの接続のポート番号を設定できます。
 > **注意事項：**
 > TCP / IPネットワークはデフォルトで有効になっています。
 > デフォルトでは3306ポートを使用します。
 
	 ![](//mc.qcloudimg.com/static/img/b864e47b1e4b0e87cd5015007f9bd8dc/image.png)

 7. MySQL文字セットを設定します。 ここで標準文字セット(Standard Character Set)を例として説明します。
  - 標準文字セット（Standard Character Set）は、デフォルトではLatin1をサーバーの文字セットとして使用されます。
  - 多言語サポート（Best Support For Multilingualism）、デフォルトではUTF8をサーバーの文字セットとして使用されます。
  - 手動選択のデフォルトの文字セット/照合（Manual Selected Default Character Set/Collation）、ドロップダウンリストでご希望の文字セットを選択してください。
 
	![](//mc.qcloudimg.com/static/img/31c4f7f13a2b5b6aa0754cc3e4bd526e/image.png)

 8. MySQLのサービスオプションを設定します。 コマンドラインを使用してMySQLを管理するには、両方を選択することをお勧めします。
	![](//mc.qcloudimg.com/static/img/9f24e245f4b5d08e9d0658aa21cd70cd/image.png)

 9. rootパスワードを設定します。
	![](//mc.qcloudimg.com/static/img/65a265bcc69d6a75f0da51387dd3aedf/image.png)

 10.  設定を完了します。 【Excute】をクリックしてインストールを完了します。
	![](//mc.qcloudimg.com/static/img/fd815f05c40d11c61d801a321131e3ec/image.png)

## 手順四：MySQLのログインテスト

1. Cloud Virtual Machineで【スタート】をクリックし、【検索（アイコン）】をクリックし、```cmd```と入力して、管理者コマンドボックスを開きます：
![](//mc.qcloudimg.com/static/img/c7920f20daff62d136f6ba7987fb2ac8/image.png)

2. コマンド```mysql -u root -p```を入力し、Enterキーを押します。
 
3. 設定したrootパスワードを使用してMySQLにログインします。 下記の図は、MySQLが正常にインストールおよび設定されていることを示しています。
![](//mc.qcloudimg.com/static/img/18aef21cabf34db1bca266a8977018f4/image.png)


