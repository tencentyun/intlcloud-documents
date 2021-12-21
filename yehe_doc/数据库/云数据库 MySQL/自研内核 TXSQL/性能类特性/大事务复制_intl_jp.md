## 機能の説明
row方式では、1つのステートメントによって多くの行が更新される大規模トランザクションは、1行ごとに1個のeventを生成します。一方では大量のbinlogが生成され、また一方ではレプリケーション時にスレーブデータベースがapplyする場合は速度が比較的遅いため、スレーブデータベースのレプリケーション遅延が発生してしまいます。
Tencent Cloudカーネルチームは大規模トランザクションレプリケーションのケースを分析および最適化し、この機能を開発しました。大規模トランザクションレプリケーション最適化機能は、大規模トランザクションを自動的に認識し、row方式のbinlogをstatement形式のbinlogに変換することで、binlogを減少させるとともにレプリケーション効率を高めます。

## サポートするバージョン
- カーネルバージョン MySQL 5.6 20210630およびそれ以降
- カーネルバージョン MySQL 5.7 20200630およびそれ以降
- カーネルバージョン MySQL 8.0 20200830およびそれ以降

## ユースケース
- この機能は主にrow方式において、プライマリキーのないテーブルの大規模トランザクション再生速度を向上させるものであり、プライマリキーのないテーブルの再生が遅いことが遅延の原因であることが確実な場合にオンにできます。
- この機能は主に、row方式において大規模トランザクションが存在し、レプリケーション速度が遅いケースに対応します。

## パフォーマンスデータ
レプリケーション時間はupdateシーンでは85%、insertシーンでは約30%、それぞれ減少します。

## 利用説明
大規模トランザクションレプリケーションの最適化機能は、SQLの過去に実行した統計状況を基に、それが大規模トランザクションである可能性の有無を判断します。大規模トランザクションと認識し、かつ最適化が可能と判断すると、分離レベルを自動的にRR（反復可能読み取り）レベルに引き上げ、binlogをStatement形式に変換することで、大規模トランザクションのスレーブデータベースでの実行時間を短縮します。このうち、
- cdb_optimize_large_trans_binlogはこの機能のスイッチです。
- cdb_sql_statisticsはSQL実行状況の統計を行うスイッチです。
- cdb_optimize_large_trans_binlog_last_affected_rows_thresholdとcdb_optimize_large_trans_binlog_aver_affected_rows_threshold は大規模トランザクションのしきい値条件を共同で構成します。
- cdb_sql_statistics_info_thresholdはメモリに保存されている過去の統計データの数です。

トランザクションの実行状況をより適切に監視するため、information_schemaデータベースのテーブル、CDB_SQL_STATISTICS を追加し、現在のトランザクションの統計情報照会に用います。

#### 追加されたパラメータ

| 名称                                                         | ステータス | タイプ      | デフォルト | 説明                                      |
| :----------------------------------------------------------- | :------ | :-------- | :------ | :----------------------------------------------- |
| cdb_optimize_large_trans_binlog                              | true    | bool      | false   | binlog大規模トランザクション最適化スイッチ                           |
| cdb_optimize_large_trans_binlog_last_affected_rows_threshold | true    | ulonglong | 10000   | 大規模トランザクション最適化の条件：前回影響を受けた行数のしきい値              |
| cdb_optimize_large_trans_binlog_aver_affected_rows_threshold | true    | ulonglong | 10000   | 大規模トランザクション最適化の条件：影響を受けた平均行数のしきい値              |
| cdb_sql_statistics                                           | true    | bool      | false   | SQL実行状況の統計を開始するかどうかのスイッチ            |
| cdb_sql_statistics_info_threshold                            | true    | ulonglong | 10000   | CDB_SQL_STATISTICSのmap内に保存される最大の統計SQL数 |

#### 追加されたinformation_schema.CDB_SQL_STATISTICSテーブル

| 名称                           | タイプ                | 説明                                             |
| :----------------------------- | :------------------ | :------------------------------------------------------ |
| DIGEST_MD5                     | MYSQL_TYPE_STRING   | このSQLのdigestから換算したMD5                            |
| DIGEST_TEXT                    | MYSQL_TYPE_STRING   | SQLのdigestテキスト形式                                   |
| SQL_COMMAND                    | MYSQL_TYPE_STRING   | SQLコマンドのタイプ                                           |
| FIRST_UPDATE_TIMESTAMP         | MYSQL_TYPE_DATETIME | この統計情報の初回生成時間                            |
| LAST_UPDATE_TIMESTAMP          | MYSQL_TYPE_DATETIME | この統計情報の前回更新時間                              |
| LAST_ACCESS_TIMESTAMP          | MYSQL_TYPE_DATETIME | この統計情報への前回アクセス時間                          |
| EXECUTE_COUNT                  | MYSQL_TYPE_LONGLONG | このタイプのSQLが実行された回数                                       |
| TOTAL_AFFECTED_ROWS            | MYSQL_TYPE_LONGLONG | 影響を受けた行の総数                                            |
| AVER_AFFECTED_ROWS             | MYSQL_TYPE_LONGLONG | 影響を受けた行数の平均                                          |
| LAST_AFFECTED_ROWS             | MYSQL_TYPE_LONGLONG | 前回影響を受けた行数                                          |
| STMT_BINLOG_FORMAT_IF_POSSIBLE | MYSQL_TYPE_STRING   | このタイプのSQLをstatement形式のbinlogに変換可能かどうか。TRUEまたはFALSE |

