## Overview

The CVM instance must have the monitoring component Agent installed to collect CVM metric data. If you cannot obtain the monitored metric data, refer to this document to troubleshoot this problem.

## Problem Analysis

The following causes may lead to the failure to obtain the monitored metric data of a CVM instance:

- Agent has not been installed or launched
- The user runs the CVM instance through the Console or CLI
- The CVM instance has a high load
- The DNS configuration of the CVM instance is incorrect

## Troubleshooting Approaches

- [Check whether Agent has been installed or launched](#step1)
- [Check whether Agent is offline](#step2)
- [Check whether the CVM instance has a high load](#step3)
- [Check whether the DNS configuration of the CVM instance is incorrect](#step4)
- If no problem is found after following the steps above, [check for other causes](#step5)

<span id="step1"></span>

## Directions

### Checking whether Agent has been installed or launched

The monitored metric data of a CVM instance could be unavailable because you have not installed [Agent](https://intl.cloud.tencent.com/document/product/248/6211).

#### **Agent has not been installed or launched in the Linux CVM instance**
1. Check whether Agent has been installed.
Run the following command to check whether Agent has been installed:
```plaintext
crontab -l |grep stargate
```
If the output similar to the following is returned, Agent has been installed.
![](https://main.qcloudimg.com/raw/23131e10c7a1fac9422411c94ae7f112.png)
2. After Agent has been installed, launch Agent.
Run the following command to launch Agent:
```plaintext
ps ax |grep sgagent
ps ax |grep barad_agent
```

#### Agent has not been installed or launched in the Windows CVM instance

Run services.msc to check whether Agent has been installed or launched. If BaradAgent or Stargate is not in the “Running” state, Agent has not been launched yet. In this case, click the corresponding service name to launch the service.

![](https://main.qcloudimg.com/raw/fa88598d5d632b66867c0f3749058b14.jpg)

> 
> - If Agent has been launched but the monitored metric data is still unavailable, check for other causes.
> - If Agent has not been installed, your CVM instance cannot be monitored. You will not receive a notification if the CVM instance fails, which is very risky. For more information on installing Agent, see [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211).

<span id="step2"></span>

### Checking whether Agent is offline

After the CVM instance is shut down, the instance’s Agent will be taken offline and no data will be reported.
When you perform CVM OPS operations such as restart, upgrade, reinstallation, or image creation on the CVM Console or after logging in to the CVM instance, the reporting of the CVM monitoring data may time out and Agent will be taken offline.

**Troubleshooting:** you can access the details page of the CVM instance and view the operation logs to determine whether any relevant operations were performed on the CVM instance at that time.

![](https://main.qcloudimg.com/raw/1616616de32307d1d9e8c30d38af4441.png)

<span id="step3"></span>

### Checking whether the CVM instance has a high load

Agent may fail to report data if the CPU usage, memory usage, or bandwidth utilization of the CVM instance is too high.

**Troubleshooting methods:** 

- High CPU usage: for more information on troubleshooting this problem, see [CVM CPU/Memory Usage Is Too High](https://intl.cloud.tencent.com/document/product/248/36204).
- High memory usage: you can log in to the CVM instance or view the monitoring charts to check whether the CPU usage reaches 100%. If yes, upgrade the CVM configuration based on the actual situation. 
- High bandwidth utilization: for more information on troubleshooting this problem, see [CVM Bandwidth Utilization Is Too High](https://intl.cloud.tencent.com/document/product/248/36207).


<span id="step4"></span>

### Checking whether the DNS configuration of the CVM instance is incorrect

If the configured private IP address of the DNS in the CVM instance is incorrect, Agent may fail to report data.

**Troubleshooting method:** for more information on the private IP address of the DNS, see **DNS Server Addresses** in [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225).

<span id="step5"></span>

### Troubleshooting methods for other problems

#### Using the Agent management tool to troubleshoot in Linux

1. Download the Agent management tool and grant the execution permission.
   ```plaintext
   wget http://update2.agent.tencentyun.com/update/monitor_agent_admin && chmod +x monitor_agent_admin
   ```
2. Install the Agent management tool. If the "OK" prompt is displayed, the tool has been successfully installed.
   ```plaintext
   ./monitor_agent_admin install
   ```
3. Run the following command. The script will start to check the system and the network and fix the problem. If the "OK" prompt is displayed, no problem was found or the problem was fixed. If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) along with the **monitor_agent_admin-\*.zip** file generated by the tool. For information on how to download a file in Linux, see **Downloading a File** in [Uploading files via WinSCP to a Linux CVM from Windows](https://intl.cloud.tencent.com/document/product/213/2131).
   ```plaintext
   sh ./monitor_agent_admin check
   ```

#### Other operations

To perform other operations on the Agent management tool, you must first access the directory where the downloaded monitor_agent_admin file is stored. These operations are as follows:
- Uninstall the Agent management tool. If the "OK" prompt is displayed, the tool has been successfully uninstalled.
```plaintext
./monitor_agent_admin uninstall
```
- Reinstall the Agent management tool. If the "OK" prompt is displayed, the tool has been successfully reinstalled.
```plaintext
./monitor_agent_admin reinstall
```
- Restart the Agent management tool. If the "OK" prompt is displayed, the tool has been successfully restarted.
```plaintext
./monitor_agent_admin restart
```

#### Troubleshooting procedure for Linux CVM instances

1. Check whether Agent has been installed.
   Run the following command to check whether Agent has been successfully installed:
```plaintext
 crontab -l |grep stargate
```
i. If the following output is returned, Agent has been successfully installed, as shown in the following figure:
![](https://main.qcloudimg.com/raw/dc37b46f45bdde2afd7956497ddca3bc.png)
ii. If no prompt appears, the installation of Agent has failed. If Agent has not been installed, your CVM instance cannot be monitored. You will not receive a notification if the CVM instance fails, which is very risky. For more information on installing Agent, see **Installing on Linux** in [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211#linux-.E5.AE.89.E8.A3.85.E6.8C.87.E5.BC.95).
2. If you have installed Agent, check whether the barad_agent logs are rolled every minute in real time and reported successfully.
   Log path in the Linux system: `/usr/local/qcloud/monitor/barad/log/dispatcher.log`
   Check that each log contains "nws send succ".
3. If the logs are not rolled, check whether Agent scheduling is normal. This problem often occurs only in Linux and may be caused by a change in the system time.
   You can restart barad_agent and check whether the `/usr/local/qcloud/monitor/barad/log/executor.log` log file contains any errors.
4. If data reporting fails (that is, "nws send fail" appears), identify the cause (such as timeout, CVM connection failure, or domain name resolution failure) based on the logs.
5. Check whether the `uuid` file has been modified.
   Path of the `uuid` file in Linux: `/etc/uuid`
6. If the `uuid` file has not been modified, check the CVM timestamp.
   In Linux, run the `/usr/sbin/ntpdate ntpupdate.tencentyun.com` command to check whether the offset of the time adjustment is within 50 seconds.
	 <img src="https://main.qcloudimg.com/raw/35ba7ff75e770397834f2f9fa2b3ca38.png" width="70%">\
   If the offset is large, run the following command to restart Agent.
```
./linux_stargate_installer restart
```
7. If the problem persists after you complete the steps above, use the `check_agent_profile` script.
   In your CVM instance, run the following command:
```shell
wget http://update2.agent.tencentyun.com/check_barad_agent && sh check_barad_agent
```
[Submit a ticket](https://console.cloud.tencent.com/workorder/category) along with the output of the command above.


#### Troubleshooting procedure for Windows CVM instances

1. Run services.msc to check whether Agent has been installed. If the following output is returned, Agent has been installed, as shown in the following figure:
   ![](https://main.qcloudimg.com/raw/fa88598d5d632b66867c0f3749058b14.jpg)
    i. If Agent has been installed in your CVM instance, check whether the barad_agent logs are rolled every minute in real time and reported successfully. 
   Log path in Windows: `C:\Program Files\QCloud\Monitor\Barad\logs\info.log`
   Check that each log contains "nws send succ".
   ii. If Agent has not been installed, your CVM instance cannot be monitored. You will not receive a notification if the CVM instance fails, which is very risky. For more information on installing Agent, see **Installing on Windows** in [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211#windows-.E5.AE.89.E8.A3.85.E6.8C.87.E5.BC.95).
2. If the logs are not rolled, check whether Agent scheduling is normal (this usually occurs in Linux and is generally caused by a system time change).
   You can restart Agent and check whether the `/usr/local/qcloud/monitor/barad/log/executor.log` log file contains any errors.
3. If data reporting fails (that is, "nws send fail" appears), identify the cause (such as timeout, CVM connection failure, or domain name resolution failure) based on the logs. 
   You can retrieve the reporting address from `nws_url` in the `plugin.ini` file under the `etc` directory.
4. If "nws send fail" does not appear during reporting, perform the next step.
5. Check whether the `uuid` file has been modified.
   Path of the `uuid` file:
    In Windows: `C:\windows\system32\drivers\etc\uuid`
   The `uuid` file is the latest file named in the uuid format in the `C:\windows\system32\drivers\etc\` directory.
6. If the `uuid` file has not been modified, check the CVM timestamp. If the offset is large, restart Agent.
7. If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
