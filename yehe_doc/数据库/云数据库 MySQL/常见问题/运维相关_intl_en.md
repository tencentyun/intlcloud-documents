### What should I do when a problem with pt-online-schema-change occurs in TencentDB for MySQL?
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
 
### What should I do if "Specified key was too long" is displayed during data import to TencentDB?
**Cause**:
TencentDB for MySQL returns the error message "Specified key was too long" when you import XXXX.sql file to the TencentDB for MySQL instance on the CVM command line.
The error message "ERROR 1071 (42000): The error information that Specified key was too long and max key length is 767 bytes" indicates that the index field exceeds 767 bytes and is too long.
- For the InnoDB storage engine, the maximum length of multi-column index is as follows:
 The maximum length of a single index column is 767 bytes and the total length of all columns should not be greater than 3,072 bytes.
- For the MyISAM storage engine, the maximum length of multi-column index is as follows:
The maximum length of a single index column is 1000 bytes and the total length of all columns should not be greater than 1000 bytes.
>?In fields such as 768/2=384 double-bytes or 767/3=255 three-bytes, GBK is double-byte, UTF8 is three-byte, and UTF8MB4 is four-byte.

In MySQL v5.6 and higher, all MyISAM tables are automatically converted to InnoDB table. Therefore, with the MyISAM storage engine, a self-built database may contain combined index column of more than 767 bytes in length; however, due to the use of the MyISAM storage engine, the same table creation statement that can run in the self-built database won't work in MySQL v5.6 or higher.

**Solution:**
1. Modify the length of index columns in the erroneous rows in the backup file.
Common  erroneous row: 
`create table test(test varchar(255) primary key)charset=utf8;`
-- Success
`create table test(test varchar(256) primary key)charset=utf8;`
-- Failure
`ERROR 1071（42000）:Specified key was too long; max key length is 767 bytes`
2. You can use TencentDB v5.5 where MyISAM won't be automatically converted into InnoDB.

### What should I do if an error occurs with "select * from XX into outfile xxxx"?
For the sake of platform security, file permission is unavailable, and data cannot be exported through "select into outfile". You are recommended to export the data in another way.

### What should I do if emojis inserted into a TencentDB for MySQL become garbled?
Check whether the TencentDB for MySQL instance, client, and connection to the instance all use or support the utf8mb4 character set.
To store an emoji in an instance, you need to follow the steps below.
1. Set the character set of the instance to utf8mb4. You can log in to the TencentDB for MySQL console and modify the `character_set_server` parameter.
>!Modifying this parameter will restart the database; therefore, you are recommended to back up your data in advance to prevent any loss.
2. The client of your application should use the utf8mb4 character set for the outputted string. 
3. When creating a connection to your application, you should specify the executed character set. Take the common JDBC connection for example: 
MySQL Connector/J v5.1.13 or higher should be used. Below is the sample code: 
```
String query = “set names utf8mb4”; 
stat.execute(query);
```

