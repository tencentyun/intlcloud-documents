
このドキュメントでは、instantのアルゴリズムによってデータのレプリケーションを回避し、さらに大きなテーブルに迅速に列を追加する機能をご紹介します。データのレプリケーションやディスクの空き容量、ディスク I/Oなどの占用を防ぎ、業務ピーク時のリアルタイムな変更を実現させます。

## 制限条件
- インスタンスバージョン：MySQL 5.7 2ノード、3ノード
-カーネルマイナーバージョン：20190830およびそれ以上
>?インスタンスを新規購入した場合、デフォルトはカーネルの最新マイナーバージョンとなります。カーネルマイナーバージョンを確認するには、[カーネルマイナーバージョンの確認](https://intl.cloud.tencent.com/document/product/236/35995)をご参照ください。カーネルバージョン更新状況については、 [カーネルバージョンの更新](https://intl.cloud.tencent.com/document/product/236/35989)をご参照ください。

## 利用説明
[データベース](https://intl.cloud.tencent.com/document/product/236/37788)にログインし、次の構文で高速なテーブル列の追加を実現させます。
```
ALTER TABLE t1 ADD COLUMN c1 int，algorithm=instant;
```
>?
>- innodb_alter_table_default_algorithm パラメータは、デフォルトの ALTER TABLE アルゴリズムの指定に用います。 INSTANT を設定するときは、 ALTER TABLE は algorithm=instant 構文の記述を必要としません。現在お客様サイドではこのパラメータのデフォルト値を変更することはできません。変更が必要な場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category)して行う必要があります。
>- innodb_alter_table_default_algorithm パラメータには INPLACEまたはINSTANTを設定でき、デフォルト値は INPLACEです。
