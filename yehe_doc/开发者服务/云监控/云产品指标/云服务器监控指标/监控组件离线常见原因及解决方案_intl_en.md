You can determine whether Agent is offline based on the following conditions:
>If the Agent on a Cloud Virtual Machine (CVM) instance does not report any data for five minutes, the platform considers Agent to be offline.

The top reasons why Agent goes offline and corresponding troubleshooting methods are described as follows:

### The user operates on the CVM through the console or CLI
After the CVM is shut down, Agent on the instance goes offline and no data will be reported.

When you perform any CVM OPS such as restart, upgrade, reinstallation, or image creation in the CVM console or after logging in to the CVM, the reporting of CVM monitoring data may time out and Agent will be taken offline.

**Troubleshooting:** You can access the CVM details page and view operation logs to determine whether any relevant operations were performed on the CVM at that time.

### The CVM has a high load
If the CVM CPU has a high load and the memory or bandwidth is used up, Agent may fail to report data.


**Troubleshooting Method:** You can log in to the CVM or check the monitoring view to determine whether the CPU, memory, or bandwidth is fully utilized. If yes, expand the service as needed.



### The DNS configuration of the CVM is incorrect

If the private DNS configuration of the CVM is incorrect, Agent may fail to report data.

**Troubleshooting:** for more information on private network DNS configuration, see [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225).


### Troubleshooting methods for other problems

#### Using the Agent management tool for troubleshooting in Linux

1. Download the Agent management tool.
   ```
   wget http://update2.agent.tencentyun.com/update/monitor_agent_admin && chmod +x monitor_agent_admin
   ```
2. Install Agent.
   ```
   ./monitor_agent_admin install
   ```
3. Run the following command to troubleshoot and fix the problem. If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) along with the tool output file **monitor_agent_admin-\*.zip**. We will help you solve the problem.
   ```
   sh ./monitor_agent_admin check
   ```

#### Other operations on the Agent management tool

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


#### Troubleshooting common problems in Windows

1. If you have installed Agent, check whether barad_agent logs are rolled every minute in real time and reported successfully. 
   >
   >- Log path for Windows: C:\Program Files\QCloud\Monitor\Barad\logs\info.log
   >- Each log contains "nws send succ".
2. If the logs are not rolled, check whether Agent scheduling is normal (this usually occurs in Linux and is caused by system time change).
   You can restart barad_agent and check whether the `/usr/local/qcloud/monitor/barad/log/executor.log` log file contains any errors.
3. If reporting fails (nws send fail), locate the problem (such as timeout, CVM connection failure, or domain name resolution failure) based on the logs. 
   You can retrieve the reporting address from `nws_url` in the plugin.ini file under the etc directory.
4. If `nws send fail` does not appear during reporting, perform the following operations:
 1. Check whether the uuid file has been modified.
   uuid file path:
		```sh
   In Linux: /etc/uuid
   In Windows: C:\windows\system32\drivers\etc\uuid
   The latest file named in uuid format in the C:\windows\system32\drivers\etc\ directory
   ```
   2. If the uuid file has not been modified, check the CVM timestamp.
    In Linux, run the `/usr/sbin/ntpdate ntpupdate.tencentyun.com` command to check whether the time change is 50 seconds or less. If the time change exceeds 50 seconds, restart barad_agent.![](https://main.qcloudimg.com/raw/2be108329ee18a199ae1d5b28a571460.png).
5. If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to our customer service for troubleshooting.
