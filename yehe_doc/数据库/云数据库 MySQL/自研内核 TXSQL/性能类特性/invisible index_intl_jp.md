## 機能の説明
インデックスを見えなくして、それを削除してよいかどうかを確認する機能は、多くのユーザーが必要としています。このinvisible index方式では、ユーザーはそのインデックスを削除する最終決定を行う前に、何らかのアプリケーションやデータベースユーザーが実際にそれを使用していないか（何らかのエラーが生成/報告されないか）を確認することができます。この機能はバージョン8.0から5.7へ移植されています。

## サポートするバージョン
カーネルバージョン MySQL 5.7 20180918およびそれ以降

## ユースケース
インデックスの削除前に、そのインデックスをinvisibleに設定することで有用性を確認でき、インデックスを安全に削除することができます。

## 利用説明
次のステートメントを使用すると、invisibleインデックスの作成や、あるインデックスのinvisibleインデックスへの変更ができます。
```sql
CREATE TABLE t1 (
  i INT,
  j INT,
  k INT,
  INDEX i_idx (i) INVISIBLE
) ENGINE = InnoDB;
CREATE INDEX j_idx ON t1 (j) INVISIBLE;
ALTER TABLE t1 ADD INDEX k_idx (k) INVISIBLE;
```

次のステートメントを使用すると、visibleインデックスに変更することができます。
```sql
ALTER TABLE t1 ALTER INDEX i_idx INVISIBLE;
ALTER TABLE t1 ALTER INDEX i_idx VISIBLE
```
