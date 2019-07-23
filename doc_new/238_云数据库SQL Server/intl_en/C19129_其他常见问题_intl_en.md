
### Is there a restriction to the number of databases in TencentDB for SQL Server?
No. however, we recommend keeping the number of databases created in one single TencentDB for SQL Server instance below 70 for the better performance. If you need more databases, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### What happens to my TencentDB SQL Server instance when it expires?
- The system will send you a renewal notification via email, SMS, and internal message 7 days before your TencentDB resources expiration.
- You can continue using the TencentDB services for an additional 7 days after the expiration. The system will send you an expiration reminder for the TencentDB services, and you need to renew them as soon as possible.
- If you fail to renew the TencentDB resources within 7 days after the expiration date, the resources will be repossessed by the system and all the data will be cleared and cannot be recovered.

### After a SQL Server database is created, no or only a small amount of data is written, but why does the storage space monitor show that 500 MB of capacity has been used?
When Tencent Cloud creates each SQL Server database, it automatically allocates 500 MB of initial capacity to which the data will be written first when any data is written at all.
Therefore, even if you write no or only a very small amount of data, storage monitor will also display 500 MB.

### After I delete the data I have written to my TencentDB for SQL Server instance, the storage capacity monitor still shows that a considerable amount of capacity is used. Won't the used capacity be released?
After the data is deleted from SQL Server, the extended data files don't shrink, and the free capacity inside the files can support subsequent operations such as insertion and update.
For example, if you apply for an instance of 50 GB and write 50 GB of data to a database and then delete all the data, the system monitor will show that you have used up the 50 GB of capacity. However, you can still continue to write a lot of files.

### When managing a database with Microsoft SQL Server Management, the system prompts "Login failed. The login is from an untrusted domain and cannot be used with Windows authentication." Why?
Please change the authentication method to "SQL Server Authentication".

### How do I use SSH port mapping for TencentDB for SQL Server instance management from the internet?
For data security considerations, TencentDB for SQL Server currently doesn't support public IP. If you need to use a public IP, you can use the port mapping function of SSH2 to connect to, configure and manage an instance from the internet. For detailed directions, see [Connecting to an Instance](https://cloud.tencent.com/document/product/238/11627#.E4.BA.8C.E3.80.81.E8.BF.9E.E6.8E.A5-sql-server-.E4.BA.91.E6.95.B0.E6.8D.AE.E5.BA.93.E5.AE.9E.E4.BE.8B.EF.BC.88.E6.9C.AC.E5.9C.B0.E7.AB.AF.EF.BC.89).














