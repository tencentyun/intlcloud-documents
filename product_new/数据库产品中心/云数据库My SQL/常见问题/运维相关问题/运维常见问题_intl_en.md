### What if a problem with pt-online-schema-change occurs in TencentDB for MySQL?
TencentDB for MySQL v5.6 and higher supports Online DDL. To protect your business from being affected by table locking, you are recommended to change the table structure in v5.5 by using open-source tools such as pt-online-schema-change. However, you may encounter problems when using pt-online-schema-change to change the TencentDB for MySQL table structure through CVM.

- Common error message:
`Use of uninitialized value $host in string eq at /usr/local/percona-toolkit-3.0.3/bin/pt-online-schema-change line 4284.`
- View the corresponding source code:
``` perl
sub _find_slaves_by_processlist {
   my ( $self, $dsn_parser, $dbh, $dsn ) = @_;

   my @slaves = map  {
      my $slave        = $dsn_parser->parse("h=$_", $dsn);
      $slave->{source} = 'processlist';
      $slave;
   }
   grep { $_ }
   map  {
      my ( $host ) = $_->{host} =~ m/^([^:]+):/;
      if ( $host eq 'localhost' ) {
         $host = '127.0.0.1'; # Replication never uses sockets.
      }
      $host;
   } $self->get_connected_slaves($dbh);

   return @slaves;
}
```
As the code suggests, processlist cannot get the slave information it is looking for, because TencentDB has processed the information related to account replication.
- Solution:
Add the following parameter so that pt-osc can be used without checking the slave status.
    `--recursion-method=none`
 
### What if "Specified key was too long" is displayed during data import to TencentDB?
**Cause**:
TencentDB for MySQL returns the error message "Specified key was too long" when you import XXXX.sql file to the TencentDB for MySQL instance on the CVM command line.
The error message "ERROR 1071 (42000): The error information that Specified key was too long and max key length is 767 bytes" indicates that the index field exceeds 767 bytes and is too long.
- For the InnoDB storage engine, the maximum length of multi-column index is as follows:
 The maximum length of a single index column is 767 bytes and the total length of all columns should not be greater than 3,072 bytes.
- For the MyISAM storage engine, the maximum length of multi-column index is as follows:
The maximum length of a single index column is 1,000 bytes and the total length of all columns should not be greater than 1,000 bytes.
>In fields such as 768/2=384 double-bytes or 767/3=255 three-bytes, GBK is double-byte, UTF8 is three-byte, and UTF8MB4 is four-byte.

In MySQL v5.6 and higher, all MyISAM tables are automatically converted to InnoDB table. Therefore, with the MyISAM storage engine, a self-built database may contain combined index column of more than 767 bytes in length; however, due to the use of the MyISAM storage engine, the same table creation statement that can run in the self-built database won't work in MySQL v5.6 or higher.

**Solution:**
1. Modify the length of index columns in the erroneous rows in the backup file.
Common error rows:
`create table test(test varcahr(255) primary key)charset=utf8;`
-- Success
`create table test(test varcahr(256) primary key)charset=utf8;`
-- Failure
`ERROR 1071（42000）:Specified key was too long; max key length is 767 bytes`
2. You can use TencentDB v5.5 where MyISAM won't be automatically converted into InnoDB.

<span id = "outfile"></span>
### What if an error occurs with "select * from XX into outfile xxxx"?
For the sake of platform security, file permission is unavailable, and data cannot be exported through "select into outfile". You are recommended to export the data in another way.

<span id = "emoji"></span>
### What if emojis inserted into a TencentDB for MySQL become garbled?
Check whether the TencentDB for MySQL instance, client, and connection to the instance all use or support the utf8mb4 character set.
To store an emoji in an instance, you need to follow the steps below.
1. Set the character set of the instance to utf8mb4 by logging in to the TencentDB for MySQL Console and modifying the `character_set_server` parameter.
>Modifying this parameter will restart the database; therefore, you are recommended to back up your data in advance to prevent any loss.
2. The client of your application should use the utf8mb4 character set for the outputted string. 
3. When creating a connection to your application, you should specify the executed character set. Take the common JDBC connection for example: 
MySQL Connector/J v5.1.13 or higher should be used. Below is the sample code: 
```
String query = “set names utf8mb4”; 
stat.execute(query);
```

<span id = "canshuxiugai"></span>
### Modifications of Common Parameters and Effect
TencentDB for MySQL has been optimized on the basis of official default values in MySQL. After purchasing an instance, you are still recommended to configure the following parameters properly based on your business scenarios.

#### character_set_server
- Default value: LATIN1
- Whether restart is required: Yes
- Role: It is used to configure the default character set for the MySQL server. TencentDB for MySQL offers four character sets: LATIN1, UTF8, GBK, and UTF8MB4. Among them, LATIN1 supports English characters, with one character having one byte; UTF8 is the generally used international coding that contains all characters used by all countries, with one character having three bytes; in GBK, every character has two bytes; and UTF8MB4 (a superset of UTF8) is totally backward compatible and supports emojis, with one character having four bytes.
- Recommendation: After purchasing an instance, you need to select the appropriate character set based on the data format required in your business so as to ensure that the client and the server use the same character set, which can prevent garbled text and unnecessary restarts.

#### lower_case_table_names
- Default value: 0
- Whether restart is required: Yes
- Role: When creating a database or table, you can set whether storage and query operations are case-sensitive. This parameter can be set to 0 (case-sensitive) or 1 (case-insensitive), and the default value is 0.
- Recommendation: TencentDB for MySQL is case-sensitive by default. Please configure this parameter properly based on your business needs and using habits.

#### sql_mode
- Default value:
```
NO_ENGINE_SUBSTITUTION (v5.6), ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION (v5.7)
```
- - Whether restart is required: No
- Role: TencentDB for MySQL can operate in different SQL modes, which define the SQL syntax and data check that it should support.
The default value of this parameter in v5.6 is `NO_ENGINE_SUBSTITUTION`, which means that if the used storage engine is disabled or not compiled, an error will be thrown; in v5.7, the default value is `ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION`.
Here:
 - `ONLY_FULL_GROUP_BY` means that in a GROUP BY operation, the column in SELECT or the HAVING or ORDER BY subquery must be a function column that appears in or relies on GROUP BY.
 - `STRICT_TRANS_TABLES` enables strict mode. `NO_ZERO_IN_DATE` indicates whether the month and day of a date can contain 0 and is subject to the status of the strict mode.
 - `NO_ZERO_DATE` means that dates in the database cannot contain zero date and is subject to the status of the strict mode.
 - `ERROR_FOR_DIVISION_BY_ZERO` means that in strict mode, if data is divided by 0 during the INSERT or UPDATE process, an error rather than a warning will be generated, while in non-strict mode, NULL will be returned.
 - `NO_AUTO_CREATE_USER` prohibits GRANT from creating a user whose password is empty.
 - `NO_ENGINE_SUBSTITUTION` means that if the used storage engine is disabled or not compiled, an error will be thrown.
- Recommendation: As different SQL modes support different SQL syntax, you are recommended to configure them properly based on your business needs and development habits.

#### long_query_time
- Default value: 10
- - Whether restart is required: No
- Role: It is used to define the time threshold for slow queries, with the default value as 10s. If the query execution take 10s or longer, the execution details will be recorded in the slow log for future analysis.
- Recommendation: As business scenarios and performance sensitivity vary, you are recommended to set the value properly for future performance analysis.

