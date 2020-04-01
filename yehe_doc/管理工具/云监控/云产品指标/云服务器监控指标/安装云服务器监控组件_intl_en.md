If you need to use Cloud Monitor to view CVM metric data and generate alarms, the CVM must have Agent installed, which will be used to collect metric data.

>
>- To ensure the reporting of monitoring data, TCP dport 80 must be open to the internet on CVM. Because Agent does not depend on security groups and network ACL for data reporting, there is no need to open their TCP dport 80.
>- You must **log in to the CVM instance** to run the following command and get the Agent installer.

## Installing on Linux
1. After [logging in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436), run the following commands:
```bash
wget http://update2.agent.tencentyun.com/update/linux_stargate_installer   // Download the Agent
chmod +x linux_stargate_installer   // Grant permission to execute the Agent installation script
./linux_stargate_installer   // Install the Agent
```
2. Check whether the Agent has been successfully installed.
 1. Run the following commands to check whether Agent has been added to scheduled tasks:
```bash
crontab -l |grep stargate
```
If the following command output is displayed, Agent installation has been added to scheduled tasks.
![](https://main.qcloudimg.com/raw/dc37b46f45bdde2afd7956497ddca3bc.png)
 2. Run the following commands to check whether Agent-related processes have started:
```bash
ps ax |grep sgagent
ps ax |grep barad_agent
```
If the following command output is displayed, Agent-related processes have started and Agent has been successfully installed.
![](https://main.qcloudimg.com/raw/78427ff35cdd80ceaeca555f1fbe7f40.png)
![](https://main.qcloudimg.com/raw/2ea6857b89a12898d26cbd0580eba213.png)

## Installing on Windows
1. After [logging in to a Windows instance](https://intl.cloud.tencent.com/document/product/213/5435), copy the download address `http://update2.agent.tencentyun.com/update/windows-stargate-installer.exe` and open it in a browser to download `windows-stargate-installer.exe`.
2. Run the installer to automatically install Agent.
The following will show if the installation is successful.

## FAQs
- If you can't download the Agent installer or encounter other problems, please see [CVM Agent](https://intl.cloud.tencent.com/document/product/248/2259).
- Alternatively, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
