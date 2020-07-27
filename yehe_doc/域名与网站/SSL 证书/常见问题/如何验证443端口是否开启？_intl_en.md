
### How do I check whether port 443 is enabled on a Linux server?
1. Log in to your Linux instance from the [CVM Console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. On the server terminal, run the `lsof -i:443` command. If the related information is displayed, port 443 is enabled; otherwise, port 443 is disabled.
 - Port 443 enabled:
![](https://main.qcloudimg.com/raw/66407c9fd01217b95d58631223d0e9e7.png)
 - Port 443 disabled:
![](https://main.qcloudimg.com/raw/651876723c7c40cde9552b87ea9f1567.png)

### How do I check whether port 443 is enabled on a Windows server?

1. Log in to your Windows instance from the [CVM Console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. On the server terminal, run the `netstat -ano -p tcp | find "443" >nul 2>nul && echo Port 443 enabled || echo Port 443 disabled` command. If "Port 443 enabled" is displayed, port 443 is enabled. If "Port 443 disabled" is displayed, port 443 is disabled.
 - Port 443 enabled:
![](https://main.qcloudimg.com/raw/1e8bf446a02e202f020053876d9427a9.png)
 - Port 443 disabled:
![](https://main.qcloudimg.com/raw/e022771b2115877812bdeb1084ab6409.png)

