## Problem Description
To protect TencentDB from DDoS attacks, TencentDB for MySQL prohibits the ping command from being used to check the network connectivity by default.

## Solution
You are recommended to troubleshoot and locate network connectivity problems quickly with the telnet command.

- **The command format is as follows:**
```
telnet private/public IP address private/public port
```

- **After the command is executed, network access status is as follows**:
 - Normal network access
![](https://main.qcloudimg.com/raw/576f29ab50c2b8c347514a59242a7ae9.png)
 - Exceptional network access
![](https://main.qcloudimg.com/raw/76ce15542eb5278ad2c4e1f58c80f4db.png)

>If there is still no network access after running the telnet command, you can easily troubleshoot private and public network connection problems with the [connectivity check tool](https://intl.cloud.tencent.com/document/product/236/31927).



