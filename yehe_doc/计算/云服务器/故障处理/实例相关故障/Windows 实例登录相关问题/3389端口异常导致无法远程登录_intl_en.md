## Issue
When you are trying to remotely log in to a Windows instance, the login fails. Your [self-diagnosis](https://console.cloud.tencent.com/workorder/check) suggests that there is an exception on the remote login port 3389, but it was already open in the security groups of the CVM instance.

>? This document uses Windows Server 2012 as an example. The procedure may vary slightly depending on the operating system version and language.
>

## Troubleshooting the Issue

1. [Log in to a Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Once you log in, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> to open the **Windows PowerShell** window.
3. Run the following command to check the status of the port 3389.
```
netstat -ano | findstr 3389
```
If the result similar to the following is returned, the 3389 port is running improperly. Follow the [solutions](#3389Solution) below to solve this issue.
![](https://main.qcloudimg.com/raw/9632169a7ae2f4ff6b640ff8b9297da8.png)


<span id="3389Solution"></span>
## Solutions

The default remote login port 3389 is susceptible to attacks. When the port is attacked, you will be prompted that you are unable to use the remote login due to the port error. To solve this problem, you can change the remote login port of the CVM instance, and create an inbound rule for allowing traffic on the new port in the security group.

### Changing the remote login port of the CVM instance

1. <span id="step07">In the **Windows PowerShell** window, enter **regedit** and press **Enter**. The **Registry Editor** window will appear.</span>
2. In the registry navigation pane on the left, expand the following directories in order: **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Terminal Server** > **Wds** > **rdpwd** > **Tds** > **tcp**.
3. <span id="step09">Find the PortNumber key in **tcp**. Then, change the value of the PortNumber key (that is, port 3389) to an unoccupied port number within the range of 0 to 65535, as shown in the following figure:</span>
![](https://main.qcloudimg.com/raw/903761b80a8c414aaee0d53a76d3d29c.png)
4. In the registry navigation pane on the left, expand the following directories in order: **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Terminal Server** > **WinStations** > **RDP-Tcp**.
5. Find the PortNumber key in **RDP-Tcp** and change its value to that of the PortNumber key in **tcp**.
![](https://main.qcloudimg.com/raw/832694ca74026f25bba1e39e141d6a15.png)
6. In the **Windows PowerShell** window, enter **services.msc** and press **Enter**. The **Services** window will appear.
7. In the **Services** window, locate and right-click **Remote Desktop Services**, and then select **Restart** to restart the remote login service.

### Modifying security group rules

8. Refer to [Modifying Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34825) to disable the 3389 port and open the port set in [Step 3](#step09).
9. After modification, restart the instance in the [CVM Console](https://console.cloud.tencent.com/cvm), and try to remotely connect to the instance again to check whether the connection is successful.

## Other Operations
If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2) to contact us.


