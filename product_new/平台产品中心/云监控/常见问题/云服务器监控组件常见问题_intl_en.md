<span id="agent"></span>
### What should I do if the CVM fails to download Agent?
If the private DNS configuration of the Cloud Virtual Machine (CVM) is incorrect, the Agent will fail to be downloaded and monitoring components will fail to report data. For more information on the private DNS configurations of Tencent Cloud CVMs, see [Private network access](https://intl.cloud.tencent.com/document/product/213/5225).


### What is the installation directory for Agent?
- The Agent installation directory for Linux is `/usr/local/qcloud/stargate` or `/usr/local/qcloud/monitor`.
- The Agent installation directory for CoreOs is `/var/lib/qcloud/stargate` or `/var/lib/qcloud/monitor`.
- The Agent installation directory for Windows is `C:\Program Files\QCloud\Stargate` or `C:\Program Files\QCloud\Monitor`.

### Why no prompt is displayed after I double-click the installer on Windows?

The installation on Windows is automatic. The installer automatically exits after installation. If you want to view the prompt during installation, run the installer in CLI mode.

### Why can I only see the sgagent process after installation?
After the installation is complete, the sgagent process will start first, followed by the barad_agent process to be launched within 5 minutes. Before installation, check whether the disk partition where the installation directory resides is full, whether inode is full, whether the write permission has been granted, and whether the network is normal.

### When can users view monitoring data at the fronend after installation?
If the network is normal, users can view the monitoring data at the frontend 5 minutes after the barad_agent process is started.

### How can I uninstall Agent?
Run the uninstallation script in the `admin` sub-directory under the Agent installation directory to automatically uninstall Agent.

### How can I restart Agent monitoring?

- For Windows
   Choose **Server Manager** > **Service List** and select **QCloud BaradAgent Monitor** to stop and then start Agent.
- For Linux
   Access the `/usr/local/qcloud/monitor/barad/admin` directory, run the stop.sh script to stop Agent, and then run the trystart.sh script to start Agent. 

### What can cause the installation of monitoring components to fail?
- Modifying the DNS configuration can cause the backend server connection to fail.
- If the server is invaded and hackers tamper with PS files, information output will fail.

### After installation, why does the monitoring view show that Agent has not been installed?

If you see a yellow exclamation mark (!) on the monitoring list page in **Cloud Monitor** > **Cloud Product Monitor** > **Cloud Virtual Machine**, log in to the CVM and check if Agent is running. If Agent is running properly, the reported failure may be caused by a network error, and the backend fails to detect the Agent status of the CVM, and a yellow exclamation mark (!) is displayed in the console. In this case, you can try enabling the firewall. If the problem persists, you can [Submit Ticket](https://console.cloud.tencent.com/workorder/category) or contact customer service for troubleshooting.

### Why is there no monitoring data after Agent is installed?

Troubleshoot the problem by referring to [CVM has no monitoring data](https://cloud.tencent.com/document/product/248/17468).





