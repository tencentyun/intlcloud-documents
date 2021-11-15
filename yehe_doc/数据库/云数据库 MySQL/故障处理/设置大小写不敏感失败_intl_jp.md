
## 現象の説明
データベースで大文字と小文字を区別しない設定に失敗しました。エラーは次のとおりです。
![](https://main.qcloudimg.com/raw/e10049c280384344318379432bc294fb.png)

## 考えられる原因
- 大文字のデータベーステーブル名がある。
- データベースのバージョンが8.0である。

## 処理手順
### 大文字のデータベーステーブル名がある
このインスタンス配下のデータベースとテーブルがすべて小文字であるかどうかを確認します。大文字のデータベーステーブル名がある場合は、それらをすべて小文字に変更してから、lower_case_table_namesパラメータを変更する必要があります。
>!lower_case_table_namesパラメータを変更すると、データベースが再起動します。
>
- 大文字のテーブルがあるかどうか調べます
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
- 大文字のデータベースがあるかどうか調べます
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```

### データベースデータベースのバージョンが8.0である
データベースのバージョンが8.0の場合、lower_case_table_namesパラメータを変更することはできません。8.0バージョンでは、デフォルトで大文字と小文字が区別されます。
