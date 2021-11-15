このドキュメントでは、コンソールとコマンドラインツールの両方を使用してデータを移行する方法について説明します。

## コンソールによるデータの移行
コンソールによるデータの移行には、物理バックアップと論理バックアップの2つの方法があります。詳細については、次の内容をご参照ください。
- [物理バックアップによるデータベースの復元](https://intl.cloud.tencent.com/zh/document/product/236/31910)
- [論理バックアップによるデータベースの復元](https://intl.cloud.tencent.com/zh/document/product/236/31909)

<span id="AA"></span>
## コマンドラインツールによるデータの移行
1. MySQLコマンドラインツールmysqldumpを使用して、インポートするSQLファイルを次のように生成します。
>!
>- mysqldumpを使用してエクスポートされたデータファイルは、購入したMySQLバージョンのSQL仕様と互換性がある必要があります。MySQLにログインして、`select version()を使用して対応するMySQLのバージョン情報を取得できます。生成されたSQLファイル名には、英語/数字/下線を使用できますが、「test」文字は使用できません。
>- 移行元と移行先のデータベースのバージョン、文字セット、およびmysqldumpツールのバージョンが一致しているようにしてください。文字セットはパラメータ`--default-character-set`で指定できます。
>
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
ここで、optionsはエクスポート用オプション、db_nameはデータベース名、tbl_nameはテーブル名、bak_pathnameはエクスポート用パス名です。
mysqldumpのデータエクスポートの詳細については、[MySQL公式マニュアル](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html)をご参照ください。
2. MySQLコマンドラインツールを使用して、次のように移行先データベースにデータをインポートします。
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
ここで、hostnameはデータをリストアする移行先ホスト、portは移行先ホストのポート、usernameは移行先ホストのデータベースのユーザー名、bak_pathnameはバックアップファイルのフルパスです。

### データの移行（Windowsシステム）
1. Windowsシステムのmysqldumpツールを使用して、インポートするSQLファイルを生成します。詳細については、[コマンドラインツールによるデータの移行](#AA)をご参照ください。

2. コマンドプロンプトを起動し、MySQLコマンドラインツールを使用して、移行先データベースにデータをインポートします。

  ![](https://main.qcloudimg.com/raw/82fece0fed5c61437215836a6a5fdc54.png)

3. [移行先MySQLデータベースにログイン](https://dev.mysql.com/doc/refman/5.7/en/connecting.html)して、`show databases;`コマンドを実行すると、バックアップされたデータベースが移行先データベースにインポートされたことを確認できます。
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### データの移行（Linuxシステム）
このドキュメントでは、LinuxシステムのCVMを例にして説明します。CVMからデータベースにアクセスするには、<a href="https://intl.cloud.tencent.com/zh/document/product/236/37788" target="_blank">MySQLデータベースへのアクセス</a>をご参照ください。

1. [CVMにログイン](https://intl.cloud.tencent.com/zh/document/product/236/37788)して、MySQLコマンドラインツールmysqldumpを使用して、インポートするSQLファイルを生成します。MySQLのdb_blogデータベースを例にして説明します。
![](https://main.qcloudimg.com/raw/de40c98620c6fdd96bc7839645b70103.png)
2. MySQLコマンドラインツールを使用して、データを移行先データベースにリストアします。
3. 移行先MySQLデータベースにログインして、`show databases;`コマンドを実行すると、バックアップされたデータベースが移行先データベースにインポートされたことを確認できます。
![](https://main.qcloudimg.com/raw/072f4b0c6f2353cdd1bab1ca9b87a783.png)

## インポートされたデータファイルの文字セットの符号化方式について
1. MySQLにインポートされたデータファイルに文字セットの符号化方式が指定されていない場合は、MySQLで設定されている文字セットの符号化方式で実行します。
2. インポートされたデータファイルに文字セットの符号化方式が指定された場合は、指定された文字セットの符号化方式で実行します。
3. インポートされたデータファイルの文字セットの符号化方式がMySQLの現在の文字セットの符号化方式と異なる場合、文字化けが発生する可能性があります。

文字セットの符号化方式の詳細については、文字セットに関する<a href="https://intl.cloud.tencent.com/zh/document/product/236/7259?from_cn_redirect=1#.E5.AD.97.E7.AC.A6.E9.9B.86.E8.AF.B4.E6.98.8E" target="_blank">使用制限</a>の説明をご参照ください。


