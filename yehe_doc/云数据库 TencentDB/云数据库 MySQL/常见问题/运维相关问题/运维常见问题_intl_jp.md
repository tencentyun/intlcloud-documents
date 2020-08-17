### MySQLがpt-online-schema-changeを使用する問題
MySQL 5.6バージョンはOnline DDLのサポートを始めました。5.5バージョンではテーブル構造の変更を行う時に、ロックテーブルによるビジネスへの影響を回避するため、ユーザーがpt-online-schema-changeなどのオープンソースツールを使用してこの操作を完了することをお勧めしていますが、多くのユーザーがCVMによりpt-online-schema-changeを使用してMySQLテーブル構造を変更する時に問題が発生しています。

- よくあるエラー情報：
`Use of uninitialized value $host in string eq at /usr/local/percona-toolkit-3.0.3/bin/pt-online-schema-change line 4284.`
- 対応するソースコードの表示：
``` perl
sub _find_slaves_by_processlist {
   my ( $self, $dsn_parser, $dbh, $dsn ) = @_;

   my @slaves = map  {
      my $slave        = $dsn_parser->parse("h=$_", $dsn);
      $slave->{source} = 'processlist';
      $slave;
   }
   grep { $_ }
   map  {
      my ( $host ) = $_->{host} =~ m/^([^:]+):/;
      if ( $host eq 'localhost' ) {
         $host = '127.0.0.1'; # Replication never uses sockets.
      }
      $host;
   } $self->get_connected_slaves($dbh);

   return @slaves;
}
```
コード上ではprocesslistの方法によりslaveの情報を探していますが、TencentDBがコピーアカウント関連の情報を処理するため、processlistによりslaveの情報を取得できません。
- 修正方法：
pt-oscを使用する時に以下のパラメーターを追加し、slaveの状態を確認しないようにします。
    `--recursion-method=none`
 
### TencentDBデータインポートでSpecified key was too longのエラーメッセージが表示されます
**エラーが表示される原因**：
クライアントがCVMのTencent Cloud Command Line InterfaceによりMySQLにXXXX.sqlファイルをインポートする時、MySQLがSpecified key was too longのエラーメッセージを戻します。
エラーメッセージ「ERROR 1071 (42000): Specified key was too long; max key length is 767 bytes」の意味は、「インデックスフィールドが長すぎで、767bytesを超えています」です。
- innodbストレージエンジンについては、多列インデックスの長さは以下のとおり制限されています。
 各列の長さは767bytesを超えてはならず、すべてのインデックス列を構成する長さは3072bytesを超えてはなりません。
- myisamストレージエンジンについては、多列インデックスの長さは以下のとおり制限されています。
各列の長さは1000bytesを超えてはならず、すべてのインデックス列を構成する長さは1000bytesを超えてはなりません。
> ?768/2=384の2バイトまたは767/3=255の3バイトのフィールド（GBKは2バイトで、UTF8は3バイトで、UTF8MB4は4バイト）

MySQL 5.6以上のバージョンは、すべてのmyisamテーブルが自動的にinnodbに自動変換されるため、自己構築データベース上には767bytesを超える連結インデックス列がありますが、自己構築データベース上にmyisamストレージエンジンがあるため、同じテーブル作成ステートメントを自己構築データベースで実行しても問題ありませんが、MySQL 5.6以上では問題が発生します。

**ソリューション：**
1. バックアップファイルにおけるエラー行の連結インデックス列の長さを変更します。
一般的なインデックス列：
`create table test(test varcahr(255) primary key)charset=utf8;`
-- 成功
`create table test(test varcahr(256) primary key)charset=utf8;`
-- 失敗
`ERROR 1071（42000）:Specified key was too long; max key length is 767 bytes`
2. TencentDB 5.5バージョンを使用すると、myisamエンジンはinnodbに自動変換されません。

<span id = "outfile"></span>
### select * from XX into outfile xxxxのエラーメッセージは何が原因ですか？
プラットフォームの安全性の理由により、file権限をアクティブにすることができず、select into outfile方式でデータをエクスポートすることができません。その他の方法でエクスポートすることをお勧めします。

<span id = "emoji"></span>
### MySQLデータベースで絵文字を挿入すると文字化けしますが、どうすればいいですか？
MySQLインスタンス内部、クライアント、MySQLインスタンスへの接続の3つの面について、統一して使用していないか、またはutf8mb4文字セットをサポートしているかを徹底調査する必要があります。
絵文字のMySQLインスタンスへの保存を実現するには、MySQLインスタンス内部、クライアント、MySQLインスタンスへの接続の3つの面について、統一して使用するかutf8mb4文字セットをサポートする必要があります。
1. まずMySQLインスタンスは文字セットをutf8mb4に設定する必要があります。コンソールにログインすることにより`character_set_server`パラメーターを変更することができます。
>! このパラメーターを変更すると、データベースが再起動されます。不要な損失が発生することを回避するため、事前にデータベースをバックアップすることをお勧めします。
2. ユーザーのアプリケーションクライアントは出力する文字列の文字セットがutf8mb4であることを保証する必要があります。 
3. アプリケーションプログラムの作成および接続は実行する文字セットを指定する必要があります。例として、一般的なjdbc接続を取り上げます。 
jdbc接続については、MySQL Connector/J 5.1.13以上のバージョンを使用する必要があります。サンプルコードは以下の通りです。 
```
String query = “set names utf8mb4”; 
stat.execute(query);
```
