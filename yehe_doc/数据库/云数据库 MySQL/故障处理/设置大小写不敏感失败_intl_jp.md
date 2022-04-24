
## 故障状況
データベースで大文字と小文字を区別しない設定に失敗しました。エラーは次のとおりです。
![](https://main.qcloudimg.com/raw/e10049c280384344318379432bc294fb.png)
>?データベースがバージョン8.0の場合、テーブル名の大文字と小文字の区別の有無に関する設定は、購入ページからインスタンス作成するときにのみ設定可能です。インスタンス作成後、lower_case_table_namesパラメータを変更することで修正することはできません。

## 考えられる原因
大文字のデータベーステーブル名があります。

## 処理手順
このインスタンス配下のデータベースとテーブルがすべて小文字であるかどうかを確認します。大文字のデータベーステーブル名がある場合は、それらをすべて小文字に変更してから、lower_case_table_namesパラメータを変更してください。
>!lower_case_table_namesパラメータを変更すると、データベースが再起動されます。
>
- 大文字のテーブルの有無の確認
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
- 大文字のデータベースの有無の確認
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```

