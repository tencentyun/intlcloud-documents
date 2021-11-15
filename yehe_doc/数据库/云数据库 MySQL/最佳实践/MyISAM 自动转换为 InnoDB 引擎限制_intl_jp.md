このドキュメントでは、MyISAMエンジンが自動的にInnoDBエンジンに変換された後にテーブルを作成する時にエラーが発生することに対応するソリューションについて説明します。

## 背景
Tencent MySQLはInnoDBストレージエンジンをデフォルトでサポートしますが、MySQL 5.6以降のバージョンはMyISAMエンジンおよびMemoryエンジンがサポートされていません。詳細については、[データベースストレージエンジン](https://intl.cloud.tencent.com/document/product/236/9535)をご参照ください。
MySQL 5.6以降のバーションにマイグレーションを行うか、アップグレードすると、システムは自動的にMyISAMエンジンからInnoDBエンジンに変換されます。

MyISAMエンジンは自動採番列を含む複合プライマリキーをサポートしているが、InnoDBエンジンはサポートしていないので、MyISAMエンジンがInnoDBエンジンに変換された後、テーブルの作成時にエラーが発生します。この場合、エラーメッセージは`ERROR 1075 (42000):Incorrect table definition;there can be only one auto column and it must be defined as a key`です。

自動採番列へのインデックス作成を通じてInnoDBエンジンの複合プライマリキーに自動採番列構文を入れることをお勧めします。

## InnoDBエンジンの複合プライマリキーに自動採番列が含まれるための変更プログラム
1. テーブルを作成する時にエラーが発生する場合のSQL文：
```
 create table t_complexkey
 ( 
 id int(8) AUTO_INCREMENT, 
 name varchar(19), 
 value varchar(10), 
 primary key (name,id)
 ) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```
次の図にように作成するとエラーが発生します。
![](https://main.qcloudimg.com/raw/4ff00d33bc2d14b0a229dae99ab40b5d.png)
2. インデックス作成後のSQL文を変更します。
```
 create table t_complexkey
 ( 
 id int(8) AUTO_INCREMENT, 
 name varchar(19), 
 value varchar(10), 
 primary key (name,id),
 key key_id (id)  ## 自動採番列にインデックスを作成します
 ) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```
次の図にように作成が完了します。
![](https://main.qcloudimg.com/raw/34925406c1d5c36a7357f1735342907b.png)
3. 新規作成されたテーブル構造を確認します。
```
show create table t_complexkey;
```
![](https://main.qcloudimg.com/raw/8509780314f54ecebe54283c579b49f8.png)

