
TencentDB for SQL Server doesn't come with SQL Server Management Studio (SSMS). You can choose to install the SSMS that supports SQL Server 2008R2 directly in the TencentDB instance if you need it.

**Recommended environment for installation**: Windows Server 2012 R2 Standard Edition 64-bit English Version

[**Official software download address**](https://go.microsoft.com/fwlink/?linkid=2014306)

[**Official software instructions**](https://docs.microsoft.com/zh-cn/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)


## Using SSMS Locally
Currently, public IP is not supported by TencentDB for SQL Server for data security considerations. If you need to use a public IP, you can use the port mapping function of SSH2 to connect to, configure and manage an instance from the Internet by following the simple steps below:
1. Prepare a Linux-based CVM instance with a public IP
2. Configure port mapping locally using an SSH tool (such as SecureCRT or PuTTY), start a service port locally, and use the SSH tool to establish a connection with the Linux instance. Then, you can connect to a local service port using SSMS.
![](https://main.qcloudimg.com/raw/b544cd0cb84c22fe8ba2b103f0c0487c.png)

**Take SecureCRT as an example:**
1. Go to the session properties settings and click Add.
![](//mccdn.qcloud.com/static/img/072a1ba13c5281b206d70e7ce5294c17/image.png)
2. In the session properties settings page, configure the corresponding parameters.
![](https://main.qcloudimg.com/raw/6b6b4a0ee3982ef6ec2261ce8cfc5559.png)
3. Log in to the Linux-based CVM instance and establish a connection.
4. Connect to the SQL Server instance using SSMS



