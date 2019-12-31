To use Tencent Cloud Cloud Monitoring (CM) to view the metric data of Cloud Virtual Machine (CVM) instances and generate alarms, you need to properly install Agent on Tencent Cloud CVM instances, which will be used to collect the metric data of instances.

>
>- To properly report monitoring data, you need to open TCP dport 80 on your CVM.
>- You must log in to the CVM in order to run the command to acquire the Agent installer.

## Installing Agent on Linux
1. After [logging in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436), run the following commands:
```bash
wget http://update2.agent.tencentyun.com/update/linux_stargate_installer   //Downloads the Agent installer.
chmod +x linux_stargate_installer   //Grants the permission for executing the Agent installation script.
./linux_stargate_installer   //Installs Agent.
```
2. Check whether Agent has been successfully installed.
 1. Run the following commands to check whether Agent has been added to scheduled tasks:
```bash
crontab -l |grep stargate
```
If the command output shown in the following figure appears, Agent installation has been added to scheduled tasks.
![](https://main.qcloudimg.com/raw/dc37b46f45bdde2afd7956497ddca3bc.png)
 2. Run the following commands to check whether Agent-related processes have started:
```bash
ps ax |grep sgagent
ps ax |grep barad_agent
```
If the command output is shown as below, Agent-related processes have started and Agent has been successfully installed.
![](https://main.qcloudimg.com/raw/78427ff35cdd80ceaeca555f1fbe7f40.png)
![](https://main.qcloudimg.com/raw/2ea6857b89a12898d26cbd0580eba213.png)

## Installing Agent on Windows
1. After [logging in to a Windows instance](https://intl.cloud.tencent.com/document/product/213/5435), use private network to access `http://update2.agent.tencentyun.com/update/` and download the `windows-stargate-installer.exe` installer.
2. Run the installer to automatically install Agent.

## FAQs
- If you fail to download the Agent installer or encounter other problems, see [CVM monitoring component FAQs](https://intl.cloud.tencent.com/document/product/248/2259) for troubleshooting methods and solutions.
- Alternatively, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for troubleshooting.
