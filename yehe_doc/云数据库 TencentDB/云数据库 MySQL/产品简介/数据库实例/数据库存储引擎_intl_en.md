
Storage engine of a database refers to the type of tables and determines how tables are stored in computers. Although MySQL supports different types of storage engines, not all of them have been optimized for data restoration and persistence. TencentDB for MySQL features such as point-in-time restoration and snapshot restoration require a restoration-enabled storage engine and are available in the InnoDB storage engine only.

TencentDB for MySQL supports InnoDB by default. It no longer supports the MyISAM and Memory engines in MySQL 5.6 and higher mainly for the following reasons:
- TencentDB for MySQL greatly optimizes the kernels for InnoDB and achieves higher performance.
- MyISAM adopts a table-level locking mechanism, while InnoDB uses a row-level one. Normally, InnoDB features higher write efficiency.
>
>- With the widest lock scope, table-level locking is to lock the entire table that is being manipulated in MySQL.
>- With the narrowest lock scope, row-level locking is to lock only the row that is being manipulated in MySQL.
- MyISAM has defects in protecting data integrity, which may lead to data corruption or even loss. Moreover, many of these defects are attributable to design issues and can only be fixed at the cost of compatibility.
- Migration from MyISAM to InnoDB can be done at low costs by simply changing the code of created tables for most applications.
- MyISAM is giving ground to InnoDB. In the latest MySQL 8.0, all system tables come in the InnoDB type.

For more information, please see [InnoDB Overview](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html) and [MyISAM Overview](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html).

