This document describes how to quickly get started with CWPP.

## 限制说明
所有腾讯云用户均可按本文接入主机安全。

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Server List** in the left sidebar.

### Step 1: Install the CWPP agent
Select **Agent not installed** in the left menu to view the servers without  CWPP agent installed.
![](https://qcloudimg.tencent-cloud.cn/raw/3b2fd4103cbb397f7f82ecf0d1a57b71.png)
Click **Reinstall agent** in the Operation list to open the CWPP agent installation guide, and select an installation method.

### Step 2: Resolve the security events reported by the agent
When the CWPP agent is installed on a server, CWPP Basic is activated by default. It detects abnormal logins and brute-force attacks, and send alerts accordingly. You can process the events on the CWPP console.
![](https://qcloudimg.tencent-cloud.cn/raw/87fee85d70ed0df94e7e16937e4a0f67.png)
You can upgrade the edition to unlock more protection features. For the features in different editions, see [Features in Different Editions](https://intl.cloud.tencent.com/document/product/296/2222).


### Step 3: Troubleshoot
When your server is compromised, troubleshoot the event by referring to the guide to restore the website or system. For details, see [Linux Servers Compromised](https://intl.cloud.tencent.com/document/product/296/34230) or [Windows Server Compromised](https://intl.cloud.tencent.com/document/product/296/34231).

### Step 4: Uninstall the CWPP agent
If you no longer need the CWPP agent, you can uninstall it as follows:
- Uninstall it in the console
Go to the [Server list](https://intl.cloud.tencent.com/document/product/296/49372) and click **Uninstall agent** in the Operation column. The server status is updated after 10 minutes.
- Uninstall it in the system
  - Windows: Find and double-click the uninst.exe file in the following path to uninstall the CWPP agent: C:\Program Files\QCloud\YunJing\uninst.exe.
  - Linux: Run the following command to uninstall CWPP: `if [ -w '/usr' ]; then /usr/local/qcloud/YunJing/uninst.sh ; else /var/lib/qcloud/YunJing/uninst.sh ; fi.`
