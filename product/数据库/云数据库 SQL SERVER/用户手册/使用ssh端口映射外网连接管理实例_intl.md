For data security considerations, TencentDB for SQL Server currently doesn't support public IP. If you need to use a public IP, you can use the port mapping function of SSH2 to connect to, configure and manage an instance from the Internet by following the simple steps below:
1. Prepare a Linux-based CVM instance with a public IP
2. Configure port mapping locally using an SSH tool (such as SecureCRT or PuTTY), start a service port locally, and use the SSH tool to establish a connection with the Linux instance. Then, you can connect to a local service port using SSMS.
![](//mccdn.qcloud.com/static/img/3f9a661b42fed1648d8b00091d5ace60/image.png)

**Take SecureCRT as an example:**
1.	Go to the session properties settings and click Add.
![](//mccdn.qcloud.com/static/img/072a1ba13c5281b206d70e7ce5294c17/image.png)
2.	In the session properties settings page, configure the corresponding parameters.
![](//mccdn.qcloud.com/static/img/edf3d44003eda115015002d28bd98266/image.png)
3.	Log in to the Linux-based CVM instance and establish a connection.
4.	Connect to the SQL Server instance using SSMS
![](//mccdn.qcloud.com/static/img/0a25f830093d59d77a2b74f5c3d3e769/image.png)
