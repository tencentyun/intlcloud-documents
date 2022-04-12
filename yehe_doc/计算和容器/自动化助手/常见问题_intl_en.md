### What is TencentCloud Automation Tools?
TencentCloud Automation Tools (TAT) is a native Ops deployment tool for Tencent Cloud CVM and Lighthouse instances. It supports console and API operations. With TAT, you can execute shell commands in batch without connecting to an instance remotely.

### How do I use TAT?
You can create and execute commands in the Lighthouse console. For more details, see [Getting Started](https://intl.cloud.tencent.com/document/product/1147/46040).

### What operating systems does TAT support?
TAT supports all Linux 64-bit releases.

### Can I modify an existing command?
Yes. 
1. Log in to the Lighthouse console and select [My Commands](https://console.cloud.tencent.com/lighthouse/command) under **Automation Tools** on the left sidebar. 
2. In the **My commands** page, locate the target command and click **Modify**.
3. Modify the command in the pop-up window and click **Save**.

### How can I check the command execution status?
You can check the command execution status by logging in to the instance or in the Lighthouse console. For more details, see [Checking Command Execution Status](https://intl.cloud.tencent.com/document/product/1147/46045).

### I got garbled characters in the command output.
Common reasons: 
- The command entered is not UTF-8 encoded. 
- The command outputs non-UTF8 characters. For example, if the command is `tail -n4 /usr/bin/ls`, the output of the command is in garbled characters.

### What’s the default installation path of the TAT agent?
The default installation path is `/usr/local/qcloud/tat_agent/`.

### How can I check the status of TAT agent?
Two approaches are provided: 
- Log in to the instance, and execute `cd /usr/local/qcloud/tat_agent/log/`. You can check the running logs of the agent.
- Log in to the instance, and execute `ps -ef | grep tat_agent` to check the process status. If the process does not exist, execute `/usr/local/qcloud/tat_agent/tat_agent` to start the process or reinstall the TAT agent.

### How can I install the TAT agent?
Download the installation package, decompress and install. See [Installing TAT Agent](https://intl.cloud.tencent.com/document/product/1147/46042).

### I tried to execute a command in the console, but got the error message saying that the TAT agent was not installed. 
It means that the TAT agent is not correctly installed in the instance. Please re-install the agent as instructed in [Installing TAT Agent](https://intl.cloud.tencent.com/document/product/1147/46042).


### I can run the script in my local machine. But when I run it in TAT, it says “command not found”.
It may be caused by the configuration of PATH environment variables. Please use an absolute path to execute the command, or make sure that the command path is in the PATH environment variable. For example, you can replace `python3 test.py` with `/usr/local/bin/python3 test.py`.


### How can I uninstall the TAT agent?
Run the command according to your OS.
<dx-tabs>
::: Linux
Run the following command as the root user:
```
curl https://raw.githubusercontent.com/Tencent/tat-agent/main/install/uninstall.sh | sh
```
:::
::: Windows
Open the PowerShell terminal and run the command below: 
```
wget https://raw.githubusercontent.com/Tencent/tat-agent/main/install/uninstall.bat  -OutFile .\tat-uninstall.bat; .\tat-uninstall.bat
```
:::
</dx-tabs>
