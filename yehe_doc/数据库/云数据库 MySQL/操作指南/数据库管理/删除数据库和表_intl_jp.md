## phpMyAdminコンソールのグラフィカルユーザインターフェースの使用
### データベースの削除
1. [phpMyAdminコンソールにログイン](https://intl.cloud.tencent.com/document/product/236/32341)を実行し、管理するデータベース名をクリックしてデータベース管理インターフェースが表示されたら、【操作】をクリックします。
![](https://main.qcloudimg.com/raw/dc2a0cec1568a8b98afa5ee745b130d0.png)
2. このページでは、データベースに対して【データテーブルを新規作成】、【データベースを削除】などの一連の操作を行うことができます。【データベース（DROP）を削除】をクリックすると、データベースを削除することができます。


### データテーブルを削除
テーブルを削除するデータベースを選択します。このページでは、データテーブルに対して【閲覧】、【構成】、【検索】、【削除】などの一連の操作を行うことができます。【削除】をクリックします。
![](https://main.qcloudimg.com/raw/d782e2f163851208d175b58e4d1383b6.png)

## phpMyAdminコンソールのSQLコマンドの使用
### データベースの削除
1. phpMyAdminコンソールにログインし、SQLコマンドでデータベースを削除して【SQL】をクリックします。
![](https://main.qcloudimg.com/raw/d6ddac058780924dc717d54c61e92083.png)
2. 以下のコマンドを実行してデータベースを削除します。
```
drop database <database name>
```

### データテーブルを削除
1. SQLコマンドでデータテーブルを削除して【SQL】をクリックします。
![](https://main.qcloudimg.com/raw/b487a3625a974f45f9b5ebc6c58372f0.png)
2. 以下のコマンドを実行してデータテーブルを削除します。
```
drop table <table name>
```
