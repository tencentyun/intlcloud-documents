本文では、instantアルゴリズムを使用してデータのコピーを回避して、大規模なテーブルにカラムを高速に追加する機能について説明します。データをコピーせず、ディスク容量やディスクI/Oを消費せず、ピーク期でもリアルタイムで変更することができます。

## 制限条件
- インスタンスバージョン：MySQL 5.7高可用版及び金融版
- カーネルバージョン：20190830以上
>新規購入したインスタンスは、デフォルトで最新のカーネルバージョンになります。カーネルバージョンは[カーネルバージョン番号の表示](https://intl.cloud.tencent.com/document/product/236/35995)、カーネルバージョンの更新は[カーネルバージョンの更新動向](https://intl.cloud.tencent.com/document/product/236/35989)をご参照ください。

## 利用説明
[データベースへのログイン](https://intl.cloud.tencent.com/document/product/236/3130)。カラム高速追加構文が次の通りです。
```
ALTER TABLE t1 ADD COLUMN c1 int，algorithm=instant;
```
>
>- innodb_alter_table_default_algorithmパラメータは、デフォルトのALTER TABLEアルゴリズムを指定します。INSTANTに設定すると、ALTER TABLEではalgorithm=instant構文を指定する必要はありません。現時点では、ユーザーがこのパラメータのデフォルト値を直接変更することはできません。変更するには、[作業依頼書を提出](https://console.cloud.tencent.com/workorder/category)を使用します。
>- innodb_alter_table_default_algorithmパラメータはINPLACE又はINSTANTに設定できます。デフォルト値はINPLACEです。
