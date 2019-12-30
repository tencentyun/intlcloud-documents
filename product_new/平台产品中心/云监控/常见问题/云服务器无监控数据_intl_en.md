### How should I troubleshoot the problem where CVM has no monitoring data?

The reasons may be as follows: Agent has not been installed, the user manipulates the CVM in the console or on the CLI, the CVM has a high load, or the private DNS configuration for the CVM is incorrect. This document describes how to troubleshoot and resolve these problems.

#### Agent has not been installed
The CVM will have no monitoring data if you have not installed [Agent](https://intl.cloud.tencent.com/document/product/248/6211). To find the exact cause of the problem, complete the following steps:
1. Check whether barad_agent is installed.

If Agent is not installed, your CVM cannot be monitored. If your CVM fails, you will not receive a notification, which is highly risky. For more information about Agent, see [Install monitoring component](https://intl.cloud.tencent.com/document/product/248/6211).

#### The user manipulates the CVM in the console or on the CLI
After the CVM is shut down, Agent goes offline and no data is generated.
Common CVM OPS operations performed by users in the CVM console or by logging in to the CVM - such as restart, CVM upgrade, reinstallation, or image creation - may cause a timeout in reporting CVM monitoring data, taking Agent offline.

**Troubleshooting Method:** You can access the CVM details page and view operation logs to determine whether relevant OPS operations have been performed on the CVM at the time.


#### The CVM has a high load
If the CVM CPU has a high load and the memory or bandwidth is exhausted, the Agent may fail to report data.
**Troubleshooting Method:** You can log in to the CVM or check the monitoring view to determine whether the CPU, memory, or bandwidth is fully utilized. If yes, perform service expansion as required.

####  The DNS configuration in the CVM is incorrect
If the private DNS configuration in the CVM is incorrect, Agent may fail to report data.
**Troubleshooting Method:** For more information about private network DNS configurations for Tencent Cloud, see [Private network access](https://intl.cloud.tencent.com/document/product/213/5225).

#### Troubleshooting guide for other problems

#### For Linux - Using the Agent management tool for troubleshooting

1. Download the Agent management tool.
   ```
   wget http://update2.agent.tencentyun.com/update/monitor_agent_admin && chmod +x monitor_agent_admin
   ```
2. Install Agent.
   ```
   ./monitor_agent_admin install
   ```
3. Run the following command. If the problem persists, submit the tool output file **monitor_agent_admin-\*.zip** in a ticket. Our engineers will help you troubleshoot the problem.
   ```
   sh ./monitor_agent_admin check
   ```
    Other operations of the Agent management tool

      i. Download the Agent management tool.
      ```
       wget http://update2.agent.tencentyun.com/update/monitor_agent_admin && chmod +x monitor_agent_admin
      ```
     ii. Install Agent.
       ```
       ./monitor_agent_admin install
      ```
  iii. Uninstall Agent.
       ```
       ./monitor_agent_admin uninstall
       ```
   iv. Reinstall Agent.
        ```
       ./monitor_agent_admin reinstall
       ```
    v. Check and solve the problem.
       ```
       ./monitor_agent_admin check
        ```
    vi. Restart Agent.
       ```
      ./monitor_agent_admin restart
      ```


#### For Windows - Troubleshooting common problems

1. If you have installed Agent on your CVM, check whether barad_agent logs are refreshed in real time every minute and are reported successfully. 
Log path in Windows: `C:\Program Files\QCloud\Monitor\Barad\logs\info.log`
Each log contains "nws send succ".
2. If the logs are not refreshed, check whether there is a problem with Agent scheduling (this problem usually only occurs in Linux and is generally due to changes of the system time.)
   You can restart barad_agent and check whether the `/usr/local/qcloud/monitor/barad/log/executor.log` log file contains an error.
3. If reporting fails (nws send fail), identify the problem (such as timeout, CVM connection failure, or domain name parsing failure) based on the logs. 
   You can retrieve the reporting address from `nws_url` in the plugin.ini file under the etc directory.
4. If "nws send fail" does not appear during reporting, complete the following steps:

    i. Check whether the uuid file has been modified.
    uuid file path:
 ` For Linux: /etc/uuid`
 `For Windows: c:\windows\system32\drivers\etc\uuid`
The latest file named in uuid format in the `c:\windows\system32\drivers\etc\` directory

    ii. If the uuid file has not been modified, check the CVM timestamp.
    In Linux, run the `/usr/sbin/ntpdate ntpupdate.tencentyun.com` command to check whether the time change is 50 seconds or less. If the time change is greater than 50 seconds, restart barad_agent.![](https://main.qcloudimg.com/raw/2be108329ee18a199ae1d5b28a571460.png)
5. If the problem persists, please [Submit Ticket](https://console.cloud.tencent.com/workorder/category) to contact customer service to solve the problem.
