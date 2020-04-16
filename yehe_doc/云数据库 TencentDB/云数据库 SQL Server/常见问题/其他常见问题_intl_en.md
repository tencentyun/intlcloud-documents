
### Is there an upper limit for the number of databases in TencentDB for SQL Server?
No; however, for the sake of performance, you are recommended to keep the number of databases created in one single TencentDB for SQL Server instance below 70. If you need more databases, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### After an SQL Server database is created, no or only a small amount of data is written, but why does the storage capacity monitor show that 500 MB of capacity has been used?
When Tencent Cloud creates each SQL Server database, it will automatically allocate 500 MB of initial capacity to which the data will be written first when any data is written at all.
Therefore, even if you write no or only a very small amount of data, the storage capacity monitor will still display 500 MB.

### After I delete the data written to my TencentDB for SQL Server instance, the storage capacity monitor still shows that a considerable amount of capacity is used. Won't the used capacity be released?
After the data is deleted from SQL Server, the extended data files don't shrink, and the free capacity inside the files can support subsequent operations such as insertion and update.
For example, if you apply for an instance of 50 GB and write 50 GB of data to a database and then delete all the data, the system monitor will show that you have used up the 50 GB of capacity. However, you can still continue to write a lot of files.

### When managing a database with Microsoft SQL Server Management, the system prompts "Login failed. The login is from an untrusted domain and cannot be used with Windows authentication." Why?
Please change the authentication method to "SQL Server Authentication".

### How do I use SSH port mapping for TencentDB for SQL Server instance management from the internet?
For data security considerations, TencentDB for SQL Server currently doesn't support public IP. If you need to use a public IP, you can use the port mapping feature of SSH2 to connect to, configure, and manage an instance from the internet. For detailed directions, please see [Connecting to Instances](https://cloud.tencent.com/document/product/238/11627).














