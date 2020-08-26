## コンソールでのデータマイグレーション
コンソールによるデータのマイグレーションには物理バックアップおよび論理バックアップの2種類の方式があります。操作の詳細は以下をご参照ください。
- [物理バックアップを使用してデータベースを復旧](https://intl.cloud.tencent.com/document/product/236/31910)
- [論理バックアップを使用してデータベースを復旧](https://intl.cloud.tencent.com/document/product/236/31909)

<span id="AA"></span>
## コマンドラインツールによるデータマイグレーション
1. MySQLコマンドラインツール「mysqldump」を使用してインポートするSQLファイルを生成します。方式は次のとおりです。
>
>- mysqldumpを使用してエクスポートしたデータファイルは、購入したTencentDB for MySQLバージョンのSQL仕様と互換性がある必要があります。クラウドデータベースにログインして `select version();` を通じて対応するMySQLバージョン情報を取得することができます。生成したSQLファイル名は英字/数字/下線が認められていますが、「test」の文字は認められていません。
>- ソースデータベースとターゲットデータベースのバージョン、それらの文字セット、およびmysqldumpツールのバージョンが同じであることを確認してください。パラメータ```--default-character-set```を通じて文字セットを指定することができます。
>
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
このうち、optionsはエクスポートオプション、db_nameはデータベース名、tbl_nameはテーブル名、bak_pathnameはエクスポートパス名です。
そのほかのmysqldumpエクスポートデータの説明は、[MySQL公式ドキュメント](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html)をご参照ください。
2. MySQLコマンドラインツールによってデータをターゲットデータベースにインポートします。方式は次のとおりです。
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
このうち、hostnameはデータ復元のターゲットサーバー、portはターゲットサーバーのポート、usernameはターゲットサーバー上のデータベースユーザー名、bak_pathnameはバックアップファイルのフルパスです。

### データマイグレーション（Windowsシステム）
1. Windowsシステムのmysqldumpツールを使用して、インポートするSQLファイルを生成します。詳細については、[コマンドラインツールによるデータマイグレーション](#AA)の説明をご覧ください。
2. コマンドプロンプトに入り、MySQLコマンドラインツールを通じてデータをターゲットデータベースにインポートします。
![](https://main.qcloudimg.com/raw/82fece0fed5c61437215836a6a5fdc54.png)
3. [ターゲットMySQLデータベースにログイン](https://dev.mysql.com/doc/refman/5.7/en/connecting.html)し、`show databases;`コマンドを実行すると、バックアップデータベースがターゲットデータベースにインポートされているかを確認できます。
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### データマイグレーション（Linuxシステム）
このドキュメントでは、LinuxシステムのCVMインスタンスを例にしています。CVMインスタンスからデータベースにアクセスする方法の詳細については、<a href="https://intl.cloud.tencent.com/document/product/236/3130" target="_blank">MySQLデータベースへのアクセス</a>をご参照ください。

1. [CVMインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/2936)して、MySQLコマンドラインツール「mysqldump」を使用してインポートするSQLファイルを生成します。クラウドデータベース上のdb_blogデータベースを例にしています。
![](https://main.qcloudimg.com/raw/de40c98620c6fdd96bc7839645b70103.png)
2. MySQLコマンドラインツールによってデータをターゲットデータベースに復元します。
3. ターゲットMySQLデータベースにログインし、`show databases;`コマンドを実行すると、バックアップデータベースがターゲットデータベースにインポートされているかを確認できます。
![](https://main.qcloudimg.com/raw/072f4b0c6f2353cdd1bab1ca9b87a783.png)

## インポートされたデータファイルの文字セットに関する問題
1. インポートしたデータファイルに指定した文字セットエンコーディングがない場合、クラウドデータベースで設定した文字セットエンコーディングが使用されます。
2. インポートしたデータファイルに指定した文字セットエンコーディングがあれば、指定した文字セットエンコーディングが使用されます。
3. インポートしたデータファイルの文字セットエンコーディングがクラウドデータベースの現在の文字セットエンコーディングと異なっている場合、文字化けが生じることがあります。

文字セットエンコーディングの問題の詳細は、<a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">使用制限</a> の文字セットの説明をご参照ください。


