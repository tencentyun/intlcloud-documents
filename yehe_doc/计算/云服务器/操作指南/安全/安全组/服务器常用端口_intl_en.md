
This document describes common server ports. For more information on service application ports for Windows, see [Service Overview and Network Port Requirements for Windows](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB).

| Port | Service | Description |
|---------|---------|---------|
| 21 | FTP | An open FTP server port for uploading and downloading. |
| 22 | SSH | An SSH port for remotely connecting to Linux servers in CLI mode. |
| 25 | SMTP | An open SMTP server port for sending emails. |
| 80 | HTTP | A port for web services, such as IIS, Apache, and Nginx, to provide external access. |
| 110 | POP3 | A port for the POP3 (email protocol 3) service. |
| 137, 138, 139 | NetBIOS protocol | Ports 137 and 138 are UDP ports for transferring files through My Network Places. <br>Port 139: connections established through port 139 attempt to access the NetBIOS/SMB service. This protocol is used for file and printer sharing on Windows and SAMBA. |
| 143 | IMAP | A port for Internet Message Access Protocol (IMAP) v2, which is a protocol for receiving emails like POP3. |
| 443 | HTTPS | A port for web browsing. HTTPS is a variant of HTTP that provides encryption and transmission over secure ports. |
| 1433 | SQL Server | Default port for SQL Server. The SQL Server service uses two ports: TCP-1433 and UDP-1434. Port 1433 is used to provide external services, and port 1434 is used to return a response to the requester to indicate the TCP/IP port used by SQL Server. |
| 3306 | MySQL | Default port for MySQL databases, which is used by MySQL to provide external services. |
| 3389 | Windows Server Remote Desktop Services | Service port for the Windows Server remote desktop, through which you can connect to a remote server by using the "Remote Desktop" connection tool. |
| 8080 | Proxy port | Similar to port 80, port 8080 is used in the WWW proxy service for web browsing. The port number ":8080" is often appended to the URL when you visit a website or use a proxy. In addition, after the Apache Tomcat web server is installed, its default service port is port 8080. |
