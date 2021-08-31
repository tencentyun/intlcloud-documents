## Overview

The CVM instance must have the monitoring component Agent installed to collect CVM metric data. If you cannot obtain the monitored metric data, refer to this document for troubleshooting.

## Causes and Solutions

| Cause | Solution |
| ------------------------------- | ------------------------------------- |
| The Agent is not installed/started | Troubleshoot by referring to [Step 1](#step1) |
| The reporting domains cannot be resolved | Troubleshoot by referring to [Step 2](#step2) |
| The Agent failed to obtain the UUID | Troubleshoot by referring to [Step 3](#step3) |
| The CVM instance is shut down or being restarted | Troubleshoot by referring to [Step 4](#step4) |
| The CVM instance is under high load | Troubleshoot by referring to [Step 5](#step5) |



## Troubleshooting Procedure

<span id="step1"></span>

### Step 1. Check whether the Agent has been installed or started

The troubleshooting procedures for Linux and Windows are different. You can refer to a procedure as needed.


#### Linux
**1. Run the following command to check whether the Agent has been installed successfully**.

```plaintext
crontab -l |grep stargate
```

If the following message is displayed, the Agent has been installed:
![](https://main.qcloudimg.com/raw/23131e10c7a1fac9422411c94ae7f112.png)
If not, please [install Agents](https://intl.cloud.tencent.com/document/product/248/6211).

**2. Check whether the Agents run properly**.
Run the following commands to check whether the Agents run properly:

```plaintext
ps ax | grep sgagent
ps ax | grep barad_agent
```

If the following messages are displayed, the Agents can run properly:
![](https://main.qcloudimg.com/raw/78427ff35cdd80ceaeca555f1fbe7f40.png)
![](https://main.qcloudimg.com/raw/2ea6857b89a12898d26cbd0580eba213.png)
If there is no output, the Agents are not started. In this case, run the following commands as the root account to start the Agents. If the messages `stargate agent run succ` and `barad_agent run succ` are displayed, the Agents have been restarted successfully.

```plaintext
cd /usr/local/qcloud/stargate/admin
./restart.sh
cd /usr/local/qcloud/monitor/barad/admin
./stop.sh
./trystart.sh
```

> ?After the Agents are started, wait for 3 minutes and then check whether there is monitoring data in the CVM console.

#### Windows
Run `services.msc` to check whether the Agents are installed and started. If the status of BaradAgent or Stargate is not `Running`, the service is not started. In this case, click the name of the corresponding service and start it.

![](https://main.qcloudimg.com/raw/fa88598d5d632b66867c0f3749058b14.jpg)

>?
>- If the Agents are already started but there is still no monitoring data, you can proceed with the troubleshooting.
>- If the Agents have not been installed, your CVM instance cannot be monitored and you will not receive a notification when the CVM instance runs abnormally, which can pose a high risk. For more information about the installations of Agents, please see [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211).



<span id="step2"></span>
### Step 2. Check the reporting domains
The following 4 domains need to be resolved for the Agents to run properly:

- update2.agent.tencentyun.com
- receiver.barad.tencentyun.com
- custom.message.tencentyun.com
- metadata.tencentyun.com 

The procedures for checking and fixing the reporting domains are different for Linux and Windows. You can refer to a procedure as needed.

#### Linux
**1. Check whether the reporting domains can be resolved properly**.
Run the following commands to check whether these 4 domains can be resolved properly:

```
ping -c 1 update2.agent.tencentyun.com
ping -c 1 receiver.barad.tencentyun.com
ping -c 1 custom.message.tencentyun.com
ping -c 1 metadata.tencentyun.com 
```

In normal cases, these 4 domains can be resolved on the CVM instance. If `unknown host` is displayed, the domains fail to be resolved. You can proceed to the next step to fix it.

**2. Fix DNS resolution**.
Tencent Cloud provides reliable private network DNS servers in different regions. You are not advised to overwrite the default DNS configurations. If you need to modify them, fix the resolution for the 4 domains above as follows:

1. If you use a self-built/third-party DNS service, you are advised to add the private network DNS provided by Tencent Cloud in `/etc/resolv.conf`. For more information, please see [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225).
2. If you use a self-built DNS service, you can also add the 4 domains above to your DNS. The domain and IP mappings are as follows:
<escape>
<table>
<tr>
<th>Domain Name</th>
<th>IP</th>
</tr>
<tr>
<td>update2.agent.tencentyun.com</td>
<td>169.254.0.15</td>
</tr>
<tr>
<td>receiver.barad.tencentyun.com</td>
<td>169.254.0.4</td>
</tr>
<tr>
<td>custom.message.tencentyun.com</td>
<td>169.254.0.5</td>
</tr>
<tr>
<td>metadata.tencentyun.com </td>
<td>169.254.10.10</td>
</tr>
</table>
</escape>
3. If the two methods above cannot work, you can add the following configuration to the `/etc/hosts` file on the server:

```
169.254.0.15 update2.agent.tencentyun.com
169.254.0.4 receiver.barad.tencentyun.com
169.254.0.5 custom.message.tencentyun.com
169.254.10.10 metadata.tencentyun.com 
```

> ?After the domain resolution issue is fixed, check whether the domains can be resolved properly. If yes, wait for 3 minutes and then go to the CVM console to confirm whether there is monitoring data.

#### Windows
**1. Check whether the reporting domains can be resolved properly**.
Run the following commands to check whether these 4 domains can be resolved properly:

```
ping -n 1 update2.agent.tencentyun.com
ping -n 1 receiver.barad.tencentyun.com
ping -n 1 custom.message.tencentyun.com
ping -n 1 metadata.tencentyun.com 
```

In normal cases, these 4 domains can be resolved on the CVM instance. If "host not found" is displayed, the domain resolution fails. In this way, you can fix the resolution as follows:

**2. Fix DNS resolution**.

Tencent Cloud provides reliable private network DNS servers in different regions. You are not advised to overwrite the default DNS configurations. If you need to modify them, fix the resolution for the 4 domains above as follows:

1. Log in to Windows CVM.
2. On the operating system interface, open **Control Panel** > **Network and Sharing Center** > **Change adapter settings**.
3. Right-click the **Ethernet** and select **Properties** to open the “Ethernet Properties” window.
4. In the “Ethernet Properties” window, double-click **IP version 4 (TCP/IPv4)**, as shown below:
   ![](https://main.qcloudimg.com/raw/58280feb376db039922bfe7cdbbc49c5.png)
5. Select [Use the following DNS server address] and modify the DNS IP according to the corresponding region in the [Private Network DNS](https://intl.cloud.tencent.com/document/product/213/5225) list. After the modification, click **OK**.
   ![](https://main.qcloudimg.com/raw/2252fbae5a0ed17fcd9dcd981183b486.png)
6. If the method above does not work, you can add the following configuration to the `C:\Windows\System32\drivers\etc\hosts` file:
   ```
   169.254.0.15 update2.agent.tencentyun.com
   169.254.0.4 receiver.barad.tencentyun.com
   169.254.0.5 custom.message.tencentyun.com
   169.254.10.10 metadata.tencentyun.com 
   ```
7. Run `services.msc`. Then, right-click the SgAgent and BaradAgent services and then click **Restart the service**.
   ![](https://main.qcloudimg.com/raw/fa88598d5d632b66867c0f3749058b14.jpg)
>?
> After the domain resolution issue is fixed, wait for 3 minutes and then go to the CVM console to confirm whether there is monitoring data.
> If there is still no monitoring data after the restart, uninstall and reinstall the Agents by referring to [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211).

<span id="step3"></span>
### Step 3. Check whether the UUID is correct

Currently, the incorrect UUID configuration issue occurs only in Linux OS. For details, please see the following directions.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance) and go to the instance detail page to view the UUID.
   ![](https://main.qcloudimg.com/raw/8a2362e6b36f6a3d4cb1440094d6b248.png)

2. Log in to the CVM instance and run the following command to view the UUID:
```
cat /sys/class/dmi/id/product_serial
```
 If the UUID on the server is different from that displayed in the CVM console, run the following command as the root account to fix the UUID and restart the Agent:
``` 
echo `cat /etc/uuid |awk -F '= ' '{print $NF}'` > /etc/uuid_to_serial; mount --bind /etc/uuid_to_serial /sys/class/dmi/id/product_serial
cd /usr/local/qcloud/stargate/admin
./restart.sh
cd /usr/local/qcloud/monitor/barad/admin
./stop.sh
./trystart.sh
```

>?
>After fixing the UUID, wait for 3 minutes and then go to the CVM console to confirm whether there is monitoring data.

<span id="step4"></span>
### Step 4. Check the operation logs of the CVM instance

After the CVM instance is shut down, the instance′s Agent will be taken offline and thus no data will be reported.
When you perform CVM OPS operations such as restart, upgrade, reinstallation, or image creation through the CVM console or through logging in to the CVM instance, the reporting of the CVM monitoring data may time out and the Agent will be taken offline.

**Troubleshooting:** You can access the detail page of the CVM instance and view the operation logs to determine whether any relevant OPS operations were performed on the CVM instance at that time.

![](https://main.qcloudimg.com/raw/9b38b21ec502a64a27785777c5892f9b.png)


<span id = "step5"></span>
### Step 5. Check the CVM instance load

The Agent may fail to report data if the CPU usage, memory usage, or bandwidth utilization of the CVM instance is too high.

**Troubleshooting methods:** 

- High CPU usage: For detailed troubleshooting directions, please see [CVM CPU/Memory Usage Is Too High](https://intl.cloud.tencent.com/document/product/248/36204).
- High memory usage: You can log in to the CVM instance or view the monitoring charts to check whether the CPU usage reaches 100%. If yes, upgrade the CVM configuration as needed. 
- High bandwidth utilization: For detailed troubleshooting directions, please see [CVM Bandwidth Utilization Is Too High](https://intl.cloud.tencent.com/document/product/248/36207).

