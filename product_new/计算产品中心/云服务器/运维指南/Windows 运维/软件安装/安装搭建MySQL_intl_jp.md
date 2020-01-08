## ユースケース
本ドキュメントでは、Windows Server 2012 R2 データセンターバージョン64ビット中国語版OSのCVMを例として、MySQL 5.5の構築を具体的な手順を紹介します。
通常Windows OSではSQL Serverデータベースを使用しますが、SQL Serverは有料製品であるため、利用者が自分で認証する必要があります。また、[Tencent Cloud クラウドデータベース TencentDB for SQL Server インスタンス](http://cloud.tencent.com/product/sqlserver.html)を購入することも可能です。

## 操作手順

### MySQLインストールパッケージをダウンロードする
1. CVMにログインします。
2. CVMからブラウザを開き、`https://dev.mysql.com/downloads/mysql/5.5.html#downloads`にアクセスし、MySQLインストールパッケージをダウンロードします。下図に示すように：
![](https://main.qcloudimg.com/raw/b96236244404b3e65d3e750dec8ea8c0.png)

### MySQLをインストールする

1.ダブルクリックしてMySQLインストールパッケージをを開き、「MySQL Server 5.5 Setup」のインストールインターフェースで【Next】をクリックします。
2.【I accept the terms in the License Agreement】をチェックし、【Next】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/fd10bf4885214fc586940663f37b29bd.png)
3.【Typical】をクリックします。下図に示すように：
Typicalは、典型的なインストール方式を示します。
![](https://main.qcloudimg.com/raw/85292c920bafd81c341e23214c01eac7.png)
4.【Install】をクリックし、MySQLをインストールします。下図に示すように：
![](https://main.qcloudimg.com/raw/e4e73dd70f382ed5d3abcbda619f07ea.png)
5.【Luanch the MySQL Instance Configuration Wizard】をチェックし、【Finish】をクリックします。下図に示すように：
MySQLインストールウィンドウを閉じ、MySQLの構成ウィザードインターフェイスに入ります。
![](https://main.qcloudimg.com/raw/46932c0a2868178be1cbdb1af02a1716.png)

### MySQLを構成する

1. MySQLの構成ウィザードインターフェイスで、【Next】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/018a37f73b3493f2f72a58393530eb60.png)
2.【Detailed Configuration】をチェックし、【Next】をクリックします。下図に示すように：
> 以下の手順は Detailed Configuration を例とします。
>
![](https://main.qcloudimg.com/raw/64374e0257e0b5c13838bd4fc2a3631e.png)
 - Detailed Configuration（詳細構成）はもっと細かい粒度でサーバーを構成したい上級ユーザーに適しています。
 - Standard Configuration（標準構成）はMySQLをすばやく起動したいがサーバー構成を考慮することなくの新規ユーザーに適しています。ただし、標準構成はOSと交換性がない可能性があるため、詳細構成を選択することをお勧めします。
3.【Developer Machine】を選択し、【Next】をクリックします。下図に示すように：
> 以下の手順は Developer Machine を例とします。
>
![](https://main.qcloudimg.com/raw/40ba999555a5f7de8299aeb09b4f7fdd.png)
 - Developer Machine（開発者マシーン）は個人用デスクトップワークステーションの定番です。複数のデスクトップアプリケーションを同時に実行している場合、MySQLのサーバーがリソース使用率最小限の状態に構成します。
 - Server Machine（サーバーマシーン）はサーバーを意味します。MySQLサーバーはその他のアプリケーションと一緒に実行できます。例えば、FTP、email及びwebサーバー。MySQLサーバーが適切な比率でリソースを占める状態に構成します。
 - Dedicated MySQL Server Machine（MySQL専用サーバー）はMySQLサービスのみを実行するサーバーです。MySQLサーバーがすべてのリソースを使用できる状態に構成します。
4.【Multifunctional Database】を選択し、【Next】をクリックします。下図に示すように：
> 以下の手順は Multifunctional Database を例とします。
>
![](https://main.qcloudimg.com/raw/20a581e1af44694cc0f3188438f10742.png)
 - Multifunctional Database（マルチ機能データベース）はInnoDBとMyISAMストレージエンジンを同時に使用できます。また、2つのエンジンにリソースを均等にアサインするので、上記2つのストレージエンジンを頻繁に使用するユーザーにおすすめします。
 - Transactional Database Only（トランザクションのみを処理するデータベース）はInnoDBとMyISAMストレージエンジンを同時に使用しますが、ほとんどのサーバーリソースをInnoDBの方に割り当てられます。InnoDBを頻繁に使用し、偶にMyISAMを使用するユーザーにこちらの設定をおすすめします。
 - Non-Transactional Database Only（非トランザクションのみを処理するデータベース）はInnoDBストレージエンジンの使用を完全に禁止し、すべてのサーバーリソースをMyISAMの方に割り当てられます。InnoDBを利用しないユーザーにこちらの設定をおすすめします。
5. デフォルト設定のままにして、【Next】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/7cef832b46fdf9855d02e21762ce8978.png)
6.【Decision Support (DSS)/OLAP】を選択し、【Next】をクリックします。下図に示すように：
> 以下の手順はDecision Support (DSS)/OLAPを例とします。
>
![](https://main.qcloudimg.com/raw/6e0158904bd05862c423d84b33adb260.png)
 - Decision Support (DSS)/OLAP（決定サポート）は大量の並列接続を必要としない状況に適しています。
 - Online Transaction Processing (OLTP)（オンライントランザクション処理）は大量の並列接続を必要とする状況に適しています。
 - Manual Setting（マニュアル設定）はサーバの並列接続最大数を手動で設定する場合に適しています。
7. TCP/IPネットワークを設定し、MySQLサーバーに接続するポート番号を設定した後、【Next】をクリックします。下図に示すように：
> 
> - デフォルトのままTCP/IPネットワークを有効にします。
> - デフォルトのまま3306ポートを使用します。
> 
![](https://main.qcloudimg.com/raw/15dafbfbb27d6195effc8d94aa9a109f.png)
8.【Standard Character Set】を選択し、【Next】をクリックします。下図に示すように：
> 以下の手順はStandard Character Setを例とします。
>
![](https://main.qcloudimg.com/raw/d995acdb742ead678d3909305e560e7f.png)
 - Standard Character Set（標準文字セット）、デフォルトではLatin1をサーバーの文字セットとします。
 - Best Support For Multilingualism（多言語サポート）、デフォルトではUTF8をサーバーの文字セットとします。
 - Manual Selected Default Character Set/Collation（マニュアル設定/校正規則）プルダウンからご希望の文字セットを選択してください。 
9.【Install As Windows Service】と【Include Bin Directory in Windows PATH】をチェックし、【Next】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/4e3f9b7c330a0f59e3ed319ddc8b882d.png)
10. rootのパスワードを設定し、【Next】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/8c66302686ca7c47eb32583b4722e4f8.png)
11.【Execute】をクリックし、MySQLの構成を開始します。下図に示すように：
![](https://main.qcloudimg.com/raw/328fa1f3eb39ed00f9492ffcf5b93c46.png)
12. 【Finish】をクリックし、構成を完了させます。

### MySQLのインストールが成功したかを確認する

1. OSのインターフェースで、【実行】 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> > を右クリックし、実行ボックスを開きます。
2. 実行ボックスに**cmd**を入力し、**Enter**を押すと管理者コマンドフレームが開きます。
3. 管理者コマンドフレームで以下のコマンドを実行します。
```
mysql -u root -p
```
4. rootのパスワードを入力し、**Enter**を押して、MySQLにログインします。
以下の画面情報が表示すると、インストールと構成は成功したことを示します。




