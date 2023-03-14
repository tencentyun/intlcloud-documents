## 概要

Cloud Object Storage（COS）の容量には上限がなく、アーカイブストレージタイプとディープアーカイブストレージに自動的に移行でき、テープストレージ並みの低コストのため、特にバックアップアーカイブのケースに適しています。

現在、バックアップのクラウド化を選択するお客様がますます増えています。OracleのバックアップモジュールをCOSと接続できるようになり、COSをベースにした低コストのデータベースバックアップや復元の実装がベストチョイスとなっています。

## OSBとTencent Cloud COSの接続

OracleのOracle Secure Backup Cloud Moduleモジュールは、Oracle Secure Backup（OSB）製品群の1つです。COSとの接続を実現し、Oracleデータベースのバックアップをクラウド化してTencent Cloud COSに直接バックアップすることができます。Oracle Secure Backup Cloud ModuleはRMAN機能との統合も実現し、ユーザーはRMANスクリプトをカスタマイズすることで、効率的にOracleデータベースをTencent Cloud COSに直接バックアップすることができます。

Oracle 9iまたはそれ以降のバージョンはOracle Secure Backup Cloud Moduleをサポートしています。詳細については[Oracle公式ドキュメント](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-6FCF4FD8-861C-4D52-BB41-32E6EF03789F)をご参照ください。


## OSBのインストール

1. [Oracle公式サイト](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-964AADD2-3405-4476-8698-E9F2133CB5B7)で最新バージョンを取得し、OSBをインストールします。
2. ダウンロードしたosbws_installer.zip圧縮パッケージを解凍し、実際のCOSサービスのSecretId、SecretKey、リージョン、endpointパラメータに基づいて設定します。次のコマンドを実行し、OSBをインストールします。
>!サブアカウントキーを優先的に使用し、[最小権限ガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従うことで、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、[サブアカウントのアクセスキー管理](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
>
```
java -jar osbws_install.jar -AWSID <SecretId> -AWSKey <SecretKey> -walletDir $ORACLE_HOME/osbws_wallet -libDir $ORACLE_HOME/lib -location <リージョン> -awsEndPoint <endpoint>

// 圧縮パッケージを保存しているディレクトリに基づいて置き換えます
```
例：
```
java -jar osbws_install.jar -AWSID AKIDxxxx -AWSKey XXXX -walletDir $ORACLE_HOME/osbws_wallet -libDir $ORACLE_HOME/lib -location ap-guangzhou -awsEndPoint cos.ap-guangzhou.myqcloud.com
```
>? Oracle 12およびそれ以降のバージョンにはOSBモジュールが付属しています。インストールの際にdownloadが長時間反応しない場合は、公式サイトで最新のOSBモジュールをダウンロードしてインストールするか、またはプロキシサーバーを使用してインストールすることを検討できます。
>


## RMANによってデータベースをCOSにバックアップする

1. データベースにログインし、次のコマンドを実行してRMANに接続します。
```
rman target / 
```
2. 次のコマンドを実行し、データベースをCOSバケットにバックアップします。このうち`lib/libcos.so`と`cosorcl.ora`の部分はデータベース名に関連します。実際の値に応じて変更してください。
```
	run {
	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	backup channel=ch1 database format='ora_%d_%I_%T_%s_%t_%c_%p.dbf' plus archivelog;
	backup channel=ch1  current controlfile  format='%d_%I_%T_%s_%t_%c_%p.conf';
	backup channel=ch1 spfile format='ora_%d_%I_%T_%s_%t_%c_%p.spf' ;
	release channel ch1;
	}
```

## RMANによるCOSからのデータベース復元

1. データベースをシャットダウンし、非マウント状態にします。
 - 次のコマンドを実行して、データベースをシャットダウンします。
```
shutdown immediate;
```
 - 次のコマンドを実行して、データベースをnomount状態にします。
```
startup nomount;
```
2. rmanコマンドのlist backupによってすべてのバックアップファイルをリストアップし、復元したいバックアップファイルを選択し、選択したバックアップファイルとハンドル（Handle）名およびタグ（TAG）値を記録しておきます。
3. 次のrestoreコマンドを実行し、バックアップファイルをバインドします。
ハンドルが「ORACLE_1880733115_20190507_5_1007656283_1_1.conf」のバックアップファイルをバインドし、list backupによって取得します。このうち`lib/libcos.so`および`cosorcl.ora`の部分はデータベース名に関連し、実際の値に応じて変更可能であり、バックアップのときと一致させることができます。
```
	run {
	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	restore controlfile from 'ORACLE_1880733115_20190507_5_1007656283_1_1.conf';
	release channel ch1;
	}
```
4. 次のrestoreコマンドを実行し、データベースをmount状態のalter database mountに切り替えます。
```
	run {

	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	restore database from tag='TAG20190507T163102';
	recover database from tag='TAG20190507T163102';
	release channel ch1;
	}
```
 - このうち、**TAG20190507T163102**のtag値は各バックアップのID番号に相当し、list backupによって取得します。その前に復元した制御ファイルと一致すること、すなわちハンドルが「**ORACLE_1880733115_20190507_5_1007656283_1_1.conf**」のバックアップファイルのtagであることを確認する必要があります。
 - このうち`lib/libcos.so`と`cosorcl.ora`の部分はデータベース名に関連します。実際の値に応じて変更し、バックアップのときと一致させます。
5. データベースを開くと、データがCOSから復元されていることを確認できます。


## RMANの同時実行設定の変更

>? RMANはデフォルトでは同時実行を行いません。手動で変更する必要があります。
>

RMANにログインし、同時実行パラメータの設定を変更します。ここでは同時実行数が15の場合の例を挙げます。
```
	run {
	configure channel device type sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so ENV=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	configure default device type to SBT;
	configure device type SBT parallelism 15;
	}
```

## 関連の参照

その他のヘルプ情報については、[oracle公式ドキュメント](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-6FCF4FD8-861C-4D52-BB41-32E6EF03789F)をご参照ください。


