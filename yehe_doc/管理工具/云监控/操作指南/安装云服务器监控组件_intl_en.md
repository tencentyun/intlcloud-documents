If you need to use Cloud Monitor to view CVM metric data and generate alarms, the CVM instance must have Agent installed, which will be used to collect metric data.

> !
> - To ensure the reporting of monitoring data, TCP dport 80 must be opened to the internet on the CVM instance. Because Agent does not depend on security groups and network ACL for data reporting, there is no need to open their TCP dport 80.
> - You must **log in to the CVM instance** to run the following command and get the Agent installer.
>- For CentOS, Agent can only be installed on CentOS 5.8 and above.

## Installing on Linux




### Installation

1. Download Agent over the Tencent Cloud private network (recommended) or public network.
#### Download over Tencent Cloud private network
After logging in to the CVM instance, you can run the following command to download Agent:
``` plaintext
wget http://update2.agent.tencentyun.com/update/linux_stargate_installer
```

 > !Before downloading Agent over the private network, please [log in to the Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) to run the command and make sure that the instance uses the [private network DNS](https://intl.cloud.tencent.com/document/product/213/5225); otherwise, the Agent download address cannot be resolved.

#### Download over public network
Agent download over the public network is suitable for cases where you are not logged in to the CVM instance; for example, you can download it on your local computer:
 - If your local computer is on Windows, copy the download address below and paste it into your browser to download:
```plaintext
https://cloud-monitor-1258344699.cos.ap-guangzhou.myqcloud.com/sgagent/linux_stargate_installer
```

 - If your local computer is on Linux, run the following command to download:
``` plaintext
wget https://cloud-monitor-1258344699.cos.ap-guangzhou.myqcloud.com/sgagent/linux_stargate_installer
```
> ?Agent can only run in the CVM instance. After downloading it over the public network, you need to upload it to the CVM instance first before you can perform the following installation and operation steps.

2. To install Agent, run the following command:
```
chmod +x linux_stargate_installer   // Grant permission to run the Agent installation script
./linux_stargate_installer   // Install Agent
```
> ?You can determine whether Agent is installed successfully by performing steps 3 and 4 below. If it cannot be added to scheduled tasks or started normally, the installation failed.
3. Run the following command to check whether Agent has been added to scheduled tasks:
```plaintext
crontab -l |grep stargate
```
 If the following command output is displayed, Agent installation has been added to scheduled tasks. (If no prompt is displayed, the installation failed.)
![](https://main.qcloudimg.com/raw/dc37b46f45bdde2afd7956497ddca3bc.png)
4. Run the following command to check whether Agent-related processes have started:
```plaintext
ps ax |grep sgagent
ps ax |grep barad_agent
```
 If the following command output is displayed, Agent-related processes have started and Agent has been successfully installed.
![](https://main.qcloudimg.com/raw/78427ff35cdd80ceaeca555f1fbe7f40.png)
![](https://main.qcloudimg.com/raw/2ea6857b89a12898d26cbd0580eba213.png)








### Other operations

Run the following command to enter the Agent installation directory:
```plaintext
cd /usr/local/qcloud/stargate/admin
```

- Uninstall Agent: this command does not have an output. You can run `crontab -l |grep stargate` to check whether there is any scheduled task; and if not, the uninstallation is successful.
```plaintext
./uninstall.sh
```

- Restart Agent: if `stargate agent run succ` is displayed, the restart is successful.
```plaintext
./restart.sh
```

- Stop Agent: this command does not have an output. You can run `ps ax |grep sgagent` to check whether there are running Agent-related processes; and if not, Agent is successfully stopped.
```plaintext
./stop.sh
```

## Installing on Windows

### Installation

1. Download Agent over the Tencent Cloud private network (recommended) or public network.
#### Download over Tencent Cloud private network
After logging in to the CVM instance, copy the following Tencent Cloud private network download address and paste it into the private network browser to download Agent:
``` plaintext
http://update2.agent.tencentyun.com/update/windows-stargate-installer.exe
```
> !Before downloading Agent over the private network, please [log in to the Windows instance](https://intl.cloud.tencent.com/document/product/213/5435) to open the download address in the private network browser and make sure that the instance uses the [private network DNS](https://intl.cloud.tencent.com/document/product/213/5225); otherwise, the Agent download address cannot be resolved.

#### Download over public network
Agent download over the public network is suitable for cases where you are not logged in to the CVM instance; for example, you can download it on your local computer:
 - If your local computer is on Windows, copy the download address below and paste it into your browser to download:
``` plaintext
https://cloud-monitor-1258344699.cos.ap-guangzhou.myqcloud.com/sgagent/windows-stargate-installer.exe
```
 - If your local computer is on Linux, run the following command to download:
``` plaintext
wget https://cloud-monitor-1258344699.cos.ap-guangzhou.myqcloud.com/sgagent/windows-stargate-installer.exe
```
 >?Agent can only run in the CVM instance. After downloading it over the public network, you need to upload it to the CVM instance first before you can perform the following installation and operation steps.
2. Run the installer to automatically install Agent.
The following will be displayed if the installation is successful.
 1. Run the service. You can see that there are running `QCloud BaradAgent Monitor` and `QCloud Stargate Manager` services.
![](https://main.qcloudimg.com/raw/fa88598d5d632b66867c0f3749058b14.jpg)
 2. Open Task Manager. You can see the `BaradAgent` and `sgagent` processes.
 ![](https://main.qcloudimg.com/raw/429863f3ffdd79e2b3ececf47d952701.jpg)






### Other operations

Uninstall Agent: run the following command on the command line. After "[SC] DeleteService succeeds" is displayed, restart the CVM instance.
```plaintext
sc.exe delete "BaradAgentSvc" 
sc.exe delete "StargateSvc"
```

## FAQs

- If you can't download the Agent installer or encounter other problems, please see [CVM Agent](https://intl.cloud.tencent.com/document/product/248/2259).
- If you cannot log in to the CVM instance, please see [CVM Login Failure](https://intl.cloud.tencent.com/document/product/248/36206) for solutions.
- Alternatively, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
