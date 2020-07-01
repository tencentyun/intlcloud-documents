To use Cloud Monitor to view CVM metric data and generate alarms, install the monitoring component Agent on the CVM instance to collect metric data.

>
>- To ensure the normal reporting of the monitoring data, TCP dport 80 in the CVM instance must be opened to the Internet. Agent reports data without relying on security groups or the network ACL. Therefore, you do not need to open TCP dport 80 of the security groups or the network ACL.
>- To run the following command to obtain the Agent installer, you must first **log in to the CVM instance**.

## Installing Agent on a Linux CVM Instance

> Log in to the CVM instance to download the Agent installer. You can download the Agent installer only by using a private IP address of Tencent Cloud. Therefore, please ensure that the DNS of your CVM instance is a [private network DNS](https://intl.cloud.tencent.com/document/product/213/5225). Otherwise, the resolution of the URL for downloading the Agent installer will fail.



#### Installation directions

1. [Log in to a Linux CVM instance](https://intl.cloud.tencent.com/document/product/213/5436) and run the following commands to install Agent:
```plaintext
wget http://update2.agent.tencentyun.com/update/linux_stargate_installer   // Download the Agent installer.
chmod +x linux_stargate_installer   // Grant the permission to run the Agent installation script.
./linux_stargate_installer   // Install Agent.
```
2. Perform steps 3 and 4 to check whether the Agent installer has been executed correctly.
3. Run the following command to check whether Agent has been added to scheduled tasks.
```plaintext
crontab -l |grep stargate
```
If the following command output is returned, Agent has been added to scheduled tasks. If no prompt appears, the installation has failed.
![](https://main.qcloudimg.com/raw/dc37b46f45bdde2afd7956497ddca3bc.png)
2. Run the following commands to check whether Agent-related processes have been launched.
```plaintext
ps ax |grep sgagent
ps ax |grep barad_agent
```
If the following command output is returned, the Agent-related processes have been properly launched and Agent has been successfully installed.
![](https://main.qcloudimg.com/raw/78427ff35cdd80ceaeca555f1fbe7f40.png)
![](https://main.qcloudimg.com/raw/2ea6857b89a12898d26cbd0580eba213.png)

#### Other operations

Run the following command to access the Agent installation directory.
```plaintext
cd /usr/local/qcloud/stargate/admin
```
- Uninstall Agent: no output is returned after the uninstallation command is executed. You can run the `crontab -l |grep stargate` command to check whether there are any scheduled tasks. If there are no scheduled tasks, the uninstallation has been successfully completed.
 ```plaintext
./uninstall.sh
```
- Restart Agent: if `stargate agent run succ` appears, Agent has successfully restarted.
```plaintext
./restart.sh
```
- Stop Agent: no output is returned after the stop command is executed. You can run the `ps ax |grep sgagent` command to check whether any Agent-related processes are running. If there are no Agent-related processes running, Agent has successfully stopped running.
```plaintext
./stop.sh
```

## Installing Agent on a Windows CVM Instance

> Log in to the CVM instance to download the Agent installer. You can download the Agent installer only by using a private IP address of Tencent Cloud. Therefore, please ensure that the DNS of your CVM instance is a [private network DNS](https://intl.cloud.tencent.com/document/product/213/5225). Otherwise, the resolution of the URL for downloading the Agent installer will fail.

#### Installation directions
1. [Log in to a Windows instance](https://intl.cloud.tencent.com/document/product/213/5435), copy the download URL `http://update2.agent.tencentyun.com/update/windows-stargate-installer.exe`, and paste it in the address bar of your browser to download the `windows-stargate-installer.exe` installer.
2. Run the installer to automatically install Agent.
   If the installation is successful, the following will appear:
	 1. Run the service, and you will see that the `QCloud BaradAgent Monitor` and `QCloud Stargate Manager` services are running.
	 ![](https://main.qcloudimg.com/raw/fa88598d5d632b66867c0f3749058b14.jpg)
	 2. Run the task manager, and you will see the `BaradAgent` and `sgagent` processes.
	 ![](https://main.qcloudimg.com/raw/429863f3ffdd79e2b3ececf47d952701.jpg)

#### Other operations
Uninstall Agent: run the following commands. After "[SC] DeleteService succeeds" appears, restart the CVM instance.
```plaintext
sc.exe delete "BaradAgentSvc" 
sc.exe delete "StargateSvc"
```


## FAQs

- If you cannot download the Agent installer or encounter other problems, see FAQs for [CVM Agent](https://intl.cloud.tencent.com/document/product/248/2259).
- You can also [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us for assistance.
