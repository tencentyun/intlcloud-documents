The virus scanning feature scans files in the container for viruses and trojans in real time or on schedule.

## Viewing the Risk Trend
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss/runtime/tojanDetection) and click **Runtime Security** > **Virus Scanning** on the left sidebar.
2. The **Virus Scanning** page displays the pending risks, number of affected containers, and trend.
 - Pending risks: It displays the trend of pending risks in the last 7 days and the comparison with the previous day. Hover over the trend to display the number of pending risks of a certain day.
 - Affected containers: It displays the trend of affected containers in the last 7 days and the comparison with the previous day. Hover over the trend to display the number of affected containers of a certain day.
![](https://qcloudimg.tencent-cloud.cn/raw/78da0f6e0be46ee3633788fe0c82233c.png)


## Setting the Risk Check
On the [**Virus Scanning**](https://console.cloud.tencent.com/tcss/runtime/tojanDetection) page, the risk check module allows you to set the scheduled check and real-time monitoring.
>?
>- Real-time monitoring applies to the incremental files in the configured path.
>- Scheduled check applies to all files in the configured path.

![](https://qcloudimg.tencent-cloud.cn/raw/a94f0ec326c88c7823d3c97f7f1d82f3.png)


### Setting scheduled check
1. In the risk check module, click ![](https://qcloudimg.tencent-cloud.cn/raw/817a9f9a8a94c577ad4db00e778b609d.png) on the right of **Scheduled check**.
2. On the **Scheduled check settings** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/e9dc8af888170e4d638b8d3df829e2a0.png) to enable scheduled check and set the check time, path to check, and scope of check.
<img src="https://qcloudimg.tencent-cloud.cn/raw/12fa578e15f94eaf0ea92f4c767b3ef9.png" style="zoom:50%;" />
**Parameter description:**
 - Scheduled check: Toggle on or off the switch to enable or disable the feature.
 - Checked at
    - Check cycle: It can be **Every day**, **Every 3 days**, or **Every 7 days**.
    - Check start time: Configure when to start the scheduled check task.
    - Timeout period: When the time consumed reaches the timeout period, the check task will end. The default value is five hours.
 - Path to check
    - All paths: Check all file paths in the container.
    - Specified paths: Check specified file paths in the container.
  - Scope of check
    - Nodes: You can select **All servers** or **Specified servers**. The latter option allows you to filter servers by server name/IP for scheduled scan.
    - Containers: You can select **All containers** or **Specified containers**. The latter option allows you to filter containers by container name/ID for scheduled scan.
3. Click **Save settings**.

### Setting real-time monitoring
1. In the risk check module, click ![](https://qcloudimg.tencent-cloud.cn/raw/817a9f9a8a94c577ad4db00e778b609d.png) on the right of **Real-time monitoring**.
2. On the **Real-time monitoring settings** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/e9dc8af888170e4d638b8d3df829e2a0.png) to enable real-time monitoring and configure parameters.
<img src="https://qcloudimg.tencent-cloud.cn/raw/903530cea2a239cf14f3086f929f1c13.png" style="zoom:67%;" />

**Parameter description:**
 - Real-time monitoring: Click ![](https://qcloudimg.tencent-cloud.cn/raw/791358be9d7b92e48b4e12569ec94290.png) or ![](https://qcloudimg.tencent-cloud.cn/raw/a2de0e7ebf784e5b864c4c7a3762d6ba.png) to enable or disable the feature.
 - Path to check
    - All paths: Check all file paths in the container.
    - Specified paths: Check specified file paths in the container.
  - Select a path: Select **Check the following paths** or **Check all paths except the following** as needed. Click ![](https://qcloudimg.tencent-cloud.cn/raw/9cddee4bce0b128b81985de84155a405.png) to add up to 30 paths.
3. Click **Save settings**.

### Setting quick check
1. In the risk check module, click **Quick check**.
2. On the **Quick check** page, select the path to check and scope of check and set the timeout period.
<img src="https://qcloudimg.tencent-cloud.cn/raw/240c2217890970ec46b5a27c0e237f54.png" style="zoom:50%;" />
**Parameter description:**
 - Path to check:
    - All paths: Check all file paths in the container.
    - Specified paths: Check specified file paths in the container.
  - Scope of check:
   - Nodes: You can select **All servers** or **Specified servers**. The latter option allows you to filter servers by server name/IP for scheduled scan.
   - Containers: You can select **All containers** or **Specified containers**. The latter option allows you to filter containers by container name/ID for scheduled scan.
 - Timeout settings: When the time consumed reaches the timeout period, the check task will end. The default value is five hours.
3. Click **Start check**.

### Viewing the last check result
In the risk check module, click **Last check result** to view the details.
![](https://qcloudimg.tencent-cloud.cn/raw/5640fd73fbf78ef60b8f5a11d92946a1.png)

**Check details:**
- **Overview**
  - Numbers of suspicious files, containers in risk, and scanned containers if suspicious files are found in the last scan.
  - Start time and end time of the last scan task.
- **Check details list**: Displays the overview of suspicious files found in the last scan and aggregates them by container.
  - The fields in the list include the container name/ID, image name/ID, node name/IP, check status, time consumption, number of risks, and operation items.
  - You can check again or stop a running task.
  - You can search by server name/IP, container name/ID, or image name/ID.
  - Click ![](https://qcloudimg.tencent-cloud.cn/raw/07ede18bc7eebcd0721ef5189a3b0460.png) to view the name and path of the suspicious file, the virus name, and the **View details** button. Click **View details** to view the details of the suspicious file.

## Viewing the Event List
On the [**Virus Scanning**](https://console.cloud.tencent.com/tcss/runtime/tojanDetection) page, the event list module displays the virus and trojan check results.

### Filtering events
In the event list module, filter events in either of the following methods:
- Click the search box and search for virus and trojan events by keyword such as filename, file path, virus name, or container name.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7f12b7fc2287d844a1c134132f7d0fb6.png" style="zoom:60%;" />
- Click **Container status** or ![](https://qcloudimg.tencent-cloud.cn/raw/1837d63ca61d7e3b533e3199089cb3cc.png) on the right to search for virus and trojan events by container status or event status.
![](https://qcloudimg.tencent-cloud.cn/raw/8e8235a5fbb9db129c44bf6aaf0ae4fd.png)

### Viewing details
In the event list module, click **View details** to pop up the drawer on the right, which displays the basic information of the virus file, event details, event description, and process information. The process information is displayed only in the details of events reported by the real-time monitoring feature.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0255b849b4b99f07940e0aa674ad686.png" style="zoom:50%;" />

### Processing an event
In the event list module, click **Process now** to add an event to the allowlist or isolate (recommended), ignore, or delete it and then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/9b59676c018cbadbd33af24845008112.png)
**Parameter description:**

- Add to allowlist: If you are sure that the file is not malicious and add it to the allowlist, **the file will no longer be checked**.
- Isolate (recommended): An isolated virus file cannot be launched again by a hacker. This makes it easy for you to locate and remove the virus file.
- Ignore: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
- Delete: The event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

## Automatic File Isolation
TCSS adds the automatic trojan isolation feature, which automatically isolates files found to be in the system blocklist and custom malicious files.

### Automatic file isolation
TCSS automatically isolates files found to be in the system blocklist. Some malicious files still need to be manually confirmed and isolated. We recommend you check all the security events in the virus scanning list to ensure that all files are processed. You can recover the files isolated by mistake from the list of isolated files.

1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss/runtime/tojanDetection) and click **Runtime Security** > **Virus Scanning** on the left sidebar.
2. On the **Virus Scanning** page, click **Detection settings** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/079eebf70e6abf0b657660b6b56b4bf5.png)
3. In the **Detection settings** pop-up window, click **Isolate files automatically**.
4. In the automatic file isolation module, click ![](https://qcloudimg.tencent-cloud.cn/raw/d41405db851c32a2709793ee8806946c.png) to enable or disable automatic isolation. You can also isolate and end processes involving malicious files.
>?
>- Blocked system files: This list is provided by Tencent Cloud security experts. Files in the list are automatically isolated.
>- The **Auto isolation** switch is toggled off by default and can be toggled on as needed. When enabling automatic isolation, you can specify whether to isolate and end processes involving malicious files.
>   - When automatic isolation is enabled, it takes effect for both the system blocklist and custom blocklist.
>   - When automatic isolation is disabled, it takes effect for both the system blocklist and custom blocklist, and malicious files associated with the alert will not be automatically isolated.

![](https://qcloudimg.tencent-cloud.cn/raw/7d8dce3b365d5d938d62a20074797a27.png)

### Custom isolated files
You can customize and view the list of custom isolated files and enable or disable automatic isolation for the files.

1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss/runtime/tojanDetection) and click **Runtime Security** > **Virus Scanning** on the left sidebar.
2. On the **Virus Scanning** page, click **Detection settings** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/e3b127d6f501de6a40d8cd80b04751af.png)
3. In the **Detection settings** pop-up window, click **Isolate files automatically**.
4. In the **Custom isolated files** module, toggle on or off the **Auto isolation** switch, view the details, and download the files.
![](https://qcloudimg.tencent-cloud.cn/raw/d30d835e7a3a91fd847b9c023fcefad3.png)
Instructions:
 - Toggle on or off the **Auto isolation** switch to enable or disable the feature.
 - Click **Details** to view the basic information of the malicious file, description, and fix suggestion.
 - Click **Download** to download the malicious file.

### List of isolated files
- In the event list on the [**Virus Scanning**](https://console.cloud.tencent.com/tcss/runtime/trojanDetection) page, when you manually isolate a malicious file and select "Automatically isolate next time", the MD5 value of the file will be recorded in the list of custom isolated files, and the **Auto isolation** switch will be on. Then, the system will automatically isolate similar files. When the option is deselected, the record will be deleted from the list, and automatic isolation will no longer take effect.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a07a879a86f8e6f8d734260973c394b3.png" style="zoom:50%;" />
- In the event list on the [**Virus Scanning**](https://console.cloud.tencent.com/tcss/runtime/trojanDetection) page, when you manually isolate a malicious file and don't select "Automatically isolate next time", the MD5 value of the file will be recorded in the list of custom isolated files, and the **Auto isolation** switch will be off.
>? To make the automatic isolation of custom isolated files effective, you need to toggle on the **Auto isolation** switch; otherwise, no automatic isolation will be performed even if you have selected "Automatically isolate next time" when processing security events.

<img src="https://qcloudimg.tencent-cloud.cn/raw/ce37192b0dcf6d13acd6552682ae7945.png" style="zoom:50%;" />


