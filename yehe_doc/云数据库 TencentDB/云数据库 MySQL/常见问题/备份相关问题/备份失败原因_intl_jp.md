
### 単一インスタンスのテーブル数が100万を超えた場合
単一インスタンスのテーブル数が100万を超えた場合、バックアップエラーになる恐れがあり、データベースへの監視にも影響を与えます。そのために、単一インスタンスのテーブル数が100万を超えないようにテーブルの数の基準を適切に設けてください。

### 非プライマリキーテーブルによる大規模トランザクション
### 原因の解析
インスタンス中に非プライマリキーテーブルが存在しかつbinlogがrow形式の時、sqlが大量のデータを更新/削除すると、スレーブマシンでの再生により大規模なトランザクションが発生し、それによりバックアップスレッドがロックされ、バックアップが失敗します。

#### ソリューション
1. sqlによりインスタンス中に存在するすべての非プライマリキーテーブルを検査します。
```
select TABLE_SCHEMA,TABLE_NAME,TABLE_TYPE,ENGINE,TABLE_ROWS from information_schema.tables where (table_schema,table_name) not in (select table_schema,table_name from information_schema.columns where COLUMN_KEY='PRI') and table_schema not in ('sys','mysql','information_schema','performance_schema');
```
2. 非プライマリキーテーブルにプライマリキーを追加します。
```
alter table table_name add primary key(`column_name`);
```
