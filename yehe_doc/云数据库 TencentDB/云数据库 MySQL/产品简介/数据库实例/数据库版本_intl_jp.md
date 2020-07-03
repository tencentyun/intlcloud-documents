現在、MySQLはMySQL 5.7、MySQL 5.6、MySQL 5.5をサポートしています。各バージョンの機能については、[公式ドキュメント](https://dev.mysql.com/doc/refman/5.7/en/)をご参照ください。MySQLライフサイクル ポリシーは次の通りです。

| Release            | GA Date | Premier Support End | Extended Support End | Sustaining Support End |
| :------------------ | :------- | :------------ | :------------- | :-----------|
| MySQL Database 5.0 | Oct-05  | Dec-11              | Not Available        | Indefinite             |
| MySQL Database 5.1 | Dec-08  | Dec-13              | Not Available        | Indefinite             |
| MySQL Database 5.5 | Dec-10  | Dec-15              | Dec-18               | Indefinite             |
| MySQL Database 5.6 | Feb-13  | Feb-18              | Feb-21               | Indefinite             |
| MySQL Database 5.7 | Oct-15  | Oct-20              | Oct-23               | Indefinite             |
| MySQL Database 8.0 | Apr-18  | Apr-23              | Apr-26               | Indefinite             |

>
> - MySQL 5.5のExtended Supportは2018年12月まで締切り、期限が切れた後は、サービスのサポートに関する明確な説明はなく、問題の修復期間が長いと想定されるため、高いバージョンのMySQLを強く推奨します。
>- MySQL 5.6以降は、MyISAMストレージエンジンがサポートされていません。より高い性能で安定したInnoDBエンジンを使用することを推奨します。
>- 現在、MySQL 5.6、5.7バージョンは3種類のレプリケーション方法（非同期、半同期、強い同期）をサポートしています。5.5バージョンは非同期モードをサポートしています。
