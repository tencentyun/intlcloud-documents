If you need to use Cloud Monitor to view CVM metric data and generate alarms, the CVM must have Agent installed, which will be used to collect CVM metric data.

>
> - To ensure the reporting of monitoring data, TCP dport 80 must be opened to the internet on CVM. Because Agent does not depend on security groups and network ACL for data reporting, there is no need to open the TCP dport 80 of security groups and network ACL.
> - You must **log in to the CVM instance** before running the following command to acquire the Agent installer.

## Installing on Linux

#### Installation

1. After you [log in to a Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436), run the following commands:
```bash
wget http://update2.agent.tencentyun.com/update/linux_stargate_installer   // Download Agent
chmod +x linux_stargate_installer   // Grant permission to execute the Agent installation script
./linux_stargate_installer   // Install Agent
```
2. Check whether Agent has been successfully installed.
3. Run the following commands to check whether Agent has been added to scheduled tasks:
```bash
crontab -l |grep stargate
```
If the following command output is displayed, Agent installation has been added to scheduled tasks (If no prompt is displayed, the installation has failed).
![](https://main.qcloudimg.com/raw/dc37b46f45bdde2afd7956497ddca3bc.png)
2. Run the following commands to check whether Agent-related processes have started:
```bash
ps ax |grep sgagent
ps ax |grep barad_agent
```
If the following command output is displayed, Agent-related processes have started and Agent has been successfully installed.
![](https://main.qcloudimg.com/raw/78427ff35cdd80ceaeca555f1fbe7f40.png)
![](https://main.qcloudimg.com/raw/2ea6857b89a12898d26cbd0580eba213.png)

#### Other Operations

Run the following commands to access the Agent installation directory:
```shell
cd /usr/local/qcloud/stargate/admin
```
- Uninstall Agent: this command does not display a result. You can run `crontab -l |grep stargate` to check whether there is any scheduled task. If there are no scheduled tasks, the uninstallation has succeeded.
 ```shell
./uninstall.sh
```
- Restart Agent: if `stargate agent run succ` is displayed, the restart is successful.
```shell
./restart.sh
```
- Stop Agent: this command does not display a result. You can run `ps ax |grep sgagent` to check whether any Agent-related processes are running. If no, Agent has successfully stopped running.
```shell
./stop.sh
```

## Installing on Windows

#### Installation
1. After you [log in to a Windows instance using the RDP file (recommended)](https://intl.cloud.tencent.com/document/product/213/5435), copy the download link `http://update2.agent.tencentyun.com/update/windows-stargate-installer.exe` and open it in your browser to download the `windows-stargate-installer.exe` installer.
2. Run the installer to automatically install Agent.
   If the installation is successful, the following will be displayed:
	 1. Run the service. You can see that the `QCloud BaradAgent Monitor` and `QCloud Stargate Manager` services are running.
	 ![](https://main.qcloudimg.com/raw/fa88598d5d632b66867c0f3749058b14.jpg)
	 2. Run the task manager. You can see `BaradAgent` and `sgagent` processes.
	 ![](https://main.qcloudimg.com/raw/429863f3ffdd79e2b3ececf47d952701.jpg)

#### Other Operations
Uninstall Agent: run the following commands on the command line. After "[SC] DeleteService succeeds" is displayed, restart the CVM instance.
```shell
sc.exe delete "BaradAgentSvc" 
sc.exe delete "StargateSvc"
```


## FAQs

- If you cannot download the Agent installer or encounter other problems, please refer to the FAQs document at [CVM Agent](https://intl.cloud.tencent.com/document/product/248/2259).
- Alternatively, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
