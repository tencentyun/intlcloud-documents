
## 機能の説明
高速列作成機能とは、データディクショナリだけを変更する方法によって、大きなテーブルでの高速列作成を実現する機能です。これまで列作成操作で必須だったデータコピーが不要になるため、大きなテーブルの列作成にかかる時間が大幅に短縮され、システムへの影響を軽減できます。

## サポートするバージョン
- カーネルバージョン MySQL 5.7 20190830およびそれ以降
- カーネルバージョン MySQL 8.0 20200630およびそれ以降

## ユースケース
データ量が大きいテーブルに列追加操作を行う必要があるケースに適しています。

## パフォーマンスデータ
データ量が5GBのテーブルでテストを実施し、1列追加の操作が40秒から1秒以内に短縮されました。

## 利用説明
- Instant Add Column構文
Alter Tableにalgorithm=instantサブステートメントが追加され、列作成操作を次のステートメントによって行うことができます：
```
ALTER TABLE t1 ADD COLUMN c INT, ADD COLUMN d INT DEFAULT 1000, ALGORITHM=INSTANT;
```

- パラメータinnodb_alter_table_default_algorithmが追加され、inplace、instantに設定することが可能です。
このパラメータはデフォルトではinplaceであり、このパラメータを設定することでAlter Tableのデフォルトのアルゴリズムを調整できます。例えば次のようになります：
```
SET @@global.innodb_alter_table_default_algorithm=instant;
```
このパラメータによってデフォルトのアルゴリズムを指定した後、アルゴリズムを特に指定しない場合は、デフォルトのアルゴリズムを使用してAlter Tableの操作を行います。

### Instant Add Column制限
- 1つのステートメントには列の追加操作のみがあり、同じステートメント内の他の操作はサポートされていません。
- 追加された列は最後に配置され、列の順序の変更はサポートされていません。
- 行の形式がCOMPRESSEDのテーブルでは、列の高速追加はサポートされていません。
- 全文索引が既にあるテーブルへの列の高速追加はサポートされていません。
- 一時テーブルへの列の高速追加はサポートされていません。
