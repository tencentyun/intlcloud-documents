## コンソールでのデータマイグレーション
コンソールによるデータのマイグレーションには物理バックアップおよび論理バックアップの2種類の方式があります。操作の詳細は以下をご参照ください。
- [物理バックアップを使用してデータベースを復旧](https://intl.cloud.tencent.com/document/product/236/31910)
- [論理バックアップを使用してデータベースを復旧](https://intl.cloud.tencent.com/document/product/236/31909)

<span id="AA"></span>
## コマンドラインツールによるデータマイグレーション
1. MySQLコマンドラインツールmysqldumpを使用してインポートするSQLファイルを生成します。方式は次のとおりです。
>
>- mysqldumpがエクスポートしたデータファイルを使用するには、購入したクラウドデータベースMySQLバージョンのSQL仕様に対応していることが必要です。クラウドデータベースにログインして `select version();` を通じて対応するMySQLバージョン情報を取得することができます。生成したSQLファイル名は英字/数字/下線が認められていますが、「test」の文字は認められていません。
>- 元データベースと目標データベースのバージョン、それらの文字セット、およびmysqldumpツールのバージョンが一致することを確認してください。パラメータ```--default-character-set```を通じて文字セットを指定することができます。
>
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
このうち、optionsはエクスポートオプション、db_nameはデータベース名、tbl_nameはテーブル名、bak_pathnameはエクスポートパス名です。
そのほかのmysqldumpエクスポートデータの説明は、[MySQL公式ガイドライン](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html)をご参照ください。
2. MySQLコマンドラインツールによってデータを目標データベースにインポートします。方式は次のとおりです。
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
このうち、hostnameは還元データの目標マスター、portは目標マスターのポート、usernameは目標マスターのデータベースユーザー名、bak_pathnameはバックアップファイルのフルパスです。

### データマイグレーション（Windowsシステム）
1. Windowsシステムのmysqldumpツールを使用してインポートするSQLファイルを生成します。具体的には[コマンドラインツールデータマイグレーション](#AA)の記載をご参照ください。
2. コマンドプロンプトに入り、MySQLコマンドラインツールを通じてデータを目標データベースにインポートします。
![](https://main.qcloudimg.com/raw/82fece0fed5c61437215836a6a5fdc54.png)
3. [目標MySQLデータベースにログイン](https://dev.mysql.com/doc/refman/5.7/en/connecting.html)し、`show databases;`コマンドを実行すると、バックアップデータベースが目標データベースにインポートされているかを確認できます。
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### データマイグレーション（Linuxシステム）
このドキュメントはLinuxシステムのCVMを例にしています。CVMからデータベースへのアクセスは <a href="https://intl.cloud.tencent.com/document/product/236/3130" target="_blank">MySQLデータベースへのアクセス</a>をご参照ください。

1. [CVMにログイン](https://intl.cloud.tencent.com/document/product/213/2936)して、MySQLコマンドラインツールmysqldumpを使用してインポートするSQLファイルを生成します。クラウドデータベース上のdb_blogデータベースを例にしています。
![](https://main.qcloudimg.com/raw/de40c98620c6fdd96bc7839645b70103.png)
2. MySQLコマンドラインツールによってデータを目標データベースに戻します。
3. 目標MySQLデータベースにログインし、`show databases;`コマンドを実行すると、バックアップデータベースが目標データベースにインポートされているかを確認できます。
![](https://main.qcloudimg.com/raw/072f4b0c6f2353cdd1bab1ca9b87a783.png)

## データファイルの文字セットコードのインポートの問題
1. クラウドデータベースのインポートファイルに指定した文字セットコードがない場合、クラウドデータベースで設定した文字セットコードで実行します。
2. インポートしたデータファイルに指定した文字セットコードがあれば、指定した文字セットコードで実行します。
3. インポートしたデータファイルの文字セットコードがクラウドデータベースの現在の文字セットコードと異なっている場合、文字化けが生じることがあります。

文字セットコードの問題の詳細は、<a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">使用制限</a> の文字コードセットの説明をご参照ください。


