
**1. After a SQL Server database is created, no or only a small amount of data is written, but why does the storage space monitor show that 500 MB of space has been used?**
When Tencent Cloud creates each SQL Server database, it automatically allocates 500 MB of initial space to which the data will be written first when any data is written at all; therefore, even if you write no or only a very small amount of data, storage monitor will also display 500 MB.

**2. After I delete the data I have written, the storage space monitor still shows that a considerable amount of storage space is used. Won't the used space be released?**
After the data is deleted from SQL Server, the extended data files don't shrink, and the free space inside the files can support subsequent operations such as insertion and update. For example, if you apply for an instance of 50 GB and write 50 GB of data to a database and then delete all the data, the system monitor will show that you have used up the 50 GB of space. However, you can still continue to write a lot of files.

**3. When managing a database with Microsoft SQL Server Management, the system prompts "Login failed. The login is from an untrusted domain and cannot be used with Windows authentication."**
Please change the authentication method to "**SQL Server Authentication**".
