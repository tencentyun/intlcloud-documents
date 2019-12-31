You can determine that Agent is offline based on the following conditions:
>When Agent on a Cloud Virtual Machine (CVM) instance does not report any data for five minutes, the platform considers Agent to be offline.

The most common reasons that cause Agent to be offline and corresponding troubleshooting methods are described as follows:

### The user operates the CVM instance via the console or on the CLI
After a CVM instance is shut down, Agent on the instance goes offline and no data will be reported.

When you perform any common CVM OPS operations (such as restart, CVM instance upgrade, reinstallation, or image creation) in the CVM console or by logging into the CVM, the reporting of CVM monitoring data may time out, taking Agent offline.

**Troubleshooting:** You can access the CVM details page and view operation logs to determine whether any relevant OPS operations were performed on the CVM instance at that time.

### The CVM instance has a high load
If the CPU of the CVM instance bears a high load and the memory or bandwidth is fully occupied, Agent may fail to report data.


**Troubleshooting:** You can log into the CVM instance or check the monitoring view to determine whether the CPU, memory, or bandwidth is fully utilized. If yes, perform service expansion as needed.



### The DNS configuration in the CVM instance is incorrect

When the DNS configuration of the private network in the CVM instance is incorrect, Agent may fail to report data.

**Troubleshooting:** For more information about private network DNS configurations for Tencent Cloud, see [Private network access](https://intl.cloud.tencent.com/document/product/213/5225).


### Troubleshooting methods for other problems

#### Linux - Using the Agent management tool for troubleshooting

1. Download the Agent management tool.
   ```
   wget http://update2.agent.tencentyun.com/update/monitor_agent_admin && chmod +x monitor_agent_admin
   ```
2. Install Agent.
   ```
   ./monitor_agent_admin install
   ```
3. Run the following command to troubleshoot and fix the problem. If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) along with the tool output file **monitor_agent_admin-\*.zip**. We will help you solve the problem.
   ```
   sh ./monitor_agent_admin check
   ```

#### Other operations of the Agent management tool

1. Download the Agent management tool.
```sh
wget http://update2.agent.tencentyun.com/update/monitor_agent_admin && chmod +x monitor_agent_admin
```
2. Install Agent.
```sh
./monitor_agent_admin install
```
3. Uninstall Agent.
```sh
./monitor_agent_admin uninstall
```
4. Reinstall Agent.
```sh
./monitor_agent_admin reinstall
```
5. Troubleshoot and fix the problem.
```sh
./monitor_agent_admin check
```
6. Restart Agent.
```sh
./monitor_agent_admin restart
```


### Windows - Troubleshooting common problems

1. If you have installed Agent on your CVM instance, check whether barad_agent logs are rolled every minute in real time and reported successfully. 
   >
   >- Log path for Windows: C:\Program Files\QCloud\Monitor\Barad\logs\info.log
   >- Each log contains "nws send succ".
2. If the logs are not rolled, check whether Agent scheduling is abnormal (this problem usually occurs only in Linux, and generally caused by changes of the system time).
   You can restart barad_agent and check whether the `/usr/local/qcloud/monitor/barad/log/executor.log` log file contains any errors.
3. If reporting fails (nws send fail), identify the problem (such as timeout, CVM connection failure, or domain name parsing failure) based on the logs. 
   You can retrieve the reporting address from `nws_url` in the plugin.ini file under the etc directory.
4. If `nws send fail` does not appear during reporting, perform the following operations:
 1. Check whether the uuid file has been modified.
   uuid file path:
		```
   For Linux: /etc/uuid
   For Windows: c:\windows\system32\drivers\etc\uuid
   The latest file named in uuid format in the c:\windows\system32\drivers\etc\ directory
   ```
   2. If the uuid file has not been modified, check the CVM instance timestamp.
    In Linux, run the `/usr/sbin/ntpdate ntpupdate.tencentyun.com` command to check whether the time change is 50 seconds or less. If the time change is greater than 50 seconds, restart barad_agent.![](https://main.qcloudimg.com/raw/2be108329ee18a199ae1d5b28a571460.png).
5. If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to our customer service to solve the problem.
