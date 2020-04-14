本ドキュメントでは、Windows Server 2012 R2を例として、MySQL 5.5をセットアップするための具体的な手順を紹介します。

通常Windows OSではSQL Serverデータベースを使用しますが、SQL Serverは有料製品であるため、利用者が自らライセンス認証する必要があります。また、[Tencent Cloud  SQL Serverデータベース CDB インスタンス](http://cloud.tencent.com/product/sqlserver.html)を購入することも可能です。

## 手順一： MySQLインストールパッケージをダウンロードする
&nbsp;&nbsp;&nbsp;CVMでブラウザを開き、ダウンロードアドレスを入力します：https://dev.mysql.com/downloads/mysql/5.5.html#downloads
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](//mc.qcloudimg.com/static/img/b1da1513321247e0daf1163f529d4cd9/image.png)

## 手順二：プログラムをインストールする
 1. インストーラーを実行し、【次へ(Next)】をクリックし、プロトコルに同意をチェックします。
![](//mc.qcloudimg.com/static/img/8dd2fc106b09c3538c1dd407c02adea4/image.png)
 
 2. 標準インストール(Typical)を選択します。
![](//mc.qcloudimg.com/static/img/9f45d5441da017feca7eb9bdc11260fd/image.png)

 3. MySQLを設定するオプション（Luanch the MySQL Instance Configuration Wizard）にチェックマークを付けます
	![](//mc.qcloudimg.com/static/img/1a6b6ad499c0c00d294d6f24d5ee1645/image.png)

## 手順三：MySQLを設定する


 1. MySQLのタイプを設定します。ここでは、詳細な設定(Detailed Configuration)を例とします。
  - 詳細設定(Detailed Configuration)は、さらに細かい粒度でサーバーを設定したい上級ユーザーに適しています。
  - 標準設定(Standard Configuration)は、サーバー設定を考慮することなく、MySQLをすばやく起動したい新規ユーザーに適しています。
 
 > **注意事項：**
 > 標準設定(Standard Configuration)は、OSと互換性がない可能性があります。 詳細設定を選択することをお勧めします。

	![](//mc.qcloudimg.com/static/img/434424a84d76f9492c511f567ae2d03f/image.png)
 
 2.  MySQLサーバーの種類を設定します。 ここでは、開発マシン(Developer Machine)を例とします。
  - 開発者マシーン（Developer Machine）は個人用デスクトップワークステーションの定番です。複数のデスクトップアプリケーションを同時に実行している場合、MySQLのサーバーがリソース使用率最小限の状態に設定します。
  - サーバーマシーン（Server Machine）はサーバーを表します。MySQLサーバーは他のアプリケーションと一緒に実行できます。例えば、FTP、email及びwebサーバー。MySQLサーバーが適切な比率でリソースを占める状態に設定します。
  - 専用MySQLサーバー（Dedicated MySQL Server Machine）はMySQLサービスのみ実行するサーバーです。MySQLサーバーがすべてのリソースを使用できる状態に設定します。

	![](//mc.qcloudimg.com/static/img/11b1162dd70e46882a43933f517dcaf4/image.png)

 3. MySQLデータベースを設定します。 ここでは、多機能データベース(Multifunctional Database)を例とします。
  - 多機能データベース（Multifunctional Database）は InnoDB と MyISAM ストレージエンジンを同時に使用できます。また、2つのエンジンにリソースを均等にアサインします。このオプションは、2つのストレージエンジンを頻繁に使用するユーザーにお勧めします。
  - トランザクションのみ処理するデータベース（Transactional Database Only）はInnoDBとMyISAMストレージエンジンを同時に使用しますが、ほとんどのサーバーリソースをInnoDBストレージエンジンの方に割り当てられます。InnoDBを頻繁に使用し、偶にMyISAMを使用するユーザーにこのオプションをお勧めします。
  - 非トランザクションのみ処理するデータベース（Non-Transactional Database Only）はInnoDBストレージエンジンの使用を完全に禁止し、すべてのサーバーリソースをMyISAMストレージエンジンの方に割り当てられます。InnoDBを利用しないユーザーにこのオプションをお勧めします。
 
 ![](//mc.qcloudimg.com/static/img/37972855d5c880e59b5310a7872491f1/image.png)

 4. MySQLのInnoDBテーブルスベースを設定します。ここではデフォルトの設定を選択します。
	![](//mc.qcloudimg.com/static/img/c4c8e8710e27b202a9694b2c1be0f4f6/image.png)

 5. MySQLの並列接続を設定します。 ここでは、デシジョンサポート(Decision Support)を例とします。
  - デシジョンサポート（Decision Support）は大量の並列接続を必要としない状況に適しています。
  - オンライントランザクション処理（Online Transaction Processing ）は大量の並列接続を必要とする状況に適しています。
  - マニュアル設定（Manual Setting）はサーバの並列接続最大数を手動で設定する場合に適しています。
 
 ![](//mc.qcloudimg.com/static/img/ef17aa905ea5bdd50b1ad61b416be4ea/image.png)

 6. MySQLネットワークオプションを設定します。TCP/IPネットワークを有効または無効にし、MySQLサーバーへの接続ポート番号を設定できます。
 > **注意事項：**
 > デフォルトではTCP/IPネットワークを有効にします。
 > デフォルトでは3306ポートを使用します。
 
	 ![](//mc.qcloudimg.com/static/img/b864e47b1e4b0e87cd5015007f9bd8dc/image.png)

 7. MySQLキャラクタセットを設定します。 ここで標準キャラクタセット(Standard Character Set)を例とします。
  - 標準キャラクタセット（Standard Character Set）、デフォルトではLatin1をサーバーのキャラクタセットとします。
  - 多言語サポート（Best Support For Multilingualism）、デフォルトではUTF8をサーバーのキャラクタセットとします。
  - マニュアル設定/校正規則（Manual Selected Default Character Set/Collation）プルダウンからご希望のキャラクタセットを選択してください。
 
	![](//mc.qcloudimg.com/static/img/31c4f7f13a2b5b6aa0754cc3e4bd526e/image.png)

 8. MySQLサービスオプションを設定します。 コマンドラインからMySQLを管理するために両方を選択することをお勧めします。
	![](//mc.qcloudimg.com/static/img/9f24e245f4b5d08e9d0658aa21cd70cd/image.png)

 9. rootパスワードを設定します。
	![](//mc.qcloudimg.com/static/img/65a265bcc69d6a75f0da51387dd3aedf/image.png)

 10.  設定を完了します。 【Excute】をクリックしてインストールを完了します。
	![](//mc.qcloudimg.com/static/img/fd815f05c40d11c61d801a321131e3ec/image.png)

## 手順四：MySQLテストにログインする

1. Cloud Virtual Machineで【スタート】をクリックし、【検索（アイコン）】をクリックし、```cmd```と入力して管理者コマンドボックスを開きます：
![](//mc.qcloudimg.com/static/img/c7920f20daff62d136f6ba7987fb2ac8/image.png)

2. コマンド```mysql -u root -p```を入力し、エンターを押します。
 
3. rootパスワードを設定してMySQLにログインすると、下記の図が表示されれば、インストール設定は成功です。
![](//mc.qcloudimg.com/static/img/18aef21cabf34db1bca266a8977018f4/image.png)


