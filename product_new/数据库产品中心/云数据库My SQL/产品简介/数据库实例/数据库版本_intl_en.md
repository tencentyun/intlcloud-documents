Currently, TencentDB for MySQL supports MySQL v5.5, v5.6, and v5.7. For more information on features of each version, see the [official documentation](https://dev.mysql.com/doc/refman/5.7/en/). MySQL's official service lifecycle support policies are as shown below:

| Release            | GA Date | Premier Support End | Extended Support End | Sustaining Support End |
| :------------------ | :------- | :------------ | :------------- | :-----------|
| MySQL Database 5.0 | Oct-05  | Dec-11              | Not Available        | Indefinite             |
| MySQL Database 5.1 | Dec-08  | Dec-13              | Not Available        | Indefinite             |
| MySQL Database 5.5 | Dec-10  | Dec-15              | Dec-18               | Indefinite             |
| MySQL Database 5.6 | Feb-13  | Feb-18              | Feb-21               | Indefinite             |
| MySQL Database 5.7 | Oct-15  | Oct-20              | Oct-23               | Indefinite             |
| MySQL Database 8.0 | Apr-18  | Apr-23              | Apr-26               | Indefinite             |

>
> - The extended official support for MySQL v5.5 ended in December 2018. There has been no explicit statement on further support extension, which is possibly because fixing issues takes more time. You are strongly recommended to use a higher version of MySQL.
> - MySQL v5.6 and higher no longer support MyISAM storage engine, so you are recommended to use the InnoDB engine which features better and more stable performance.
> - Currently, MySQL v5.6 and v5.7 support three replication modes: async, semi-sync, and strong sync. Only async mode is available in MySQL v5.5.
