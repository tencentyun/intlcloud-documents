This document describes how to diagnose and troubleshoot remote login failures caused by port problems.
> The following operations take a CVM with the Windows Server 2012 system as an example.
>

## Diagnosis Tool
You can use the following tool to check whether login issues are related to port or security group configuration:
- [Port Verification](https://console.cloud.tencent.com/vpc/helper) 

For security group configuration problems, you can use **Open all ports** in [Port Verification](https://console.cloud.tencent.com/vpc/helper) to open related ports to the Internet and then try to log in again. If you still cannot log in after opening the ports to the Internet, refer to the following methods for troubleshooting.

## Troubleshooting

### Checking network connectivity

You can use the local Ping command to test network connectivity. At the same time, you can test on computers in different environments (different IP ranges or carriers) to check whether it is a local network problem or a server problem.

1. Open the command line tool on your local computer.
 - Windows systems: Click **Start** > **Run**, enter **cmd**, and the command line dialog box will pop up.
 - Mac OS systems: Open the **Terminal** tool.
2. Execute the following command to test network connection.
```
ping + CVM Instance public IP address
```
For example, execute the `ping 139.199.XXX.XXX` command.
 - If the network is normal, the following result is returned. In this case, please [check the remote desktop service configuration](#F2).
![](https://main.qcloudimg.com/raw/52e6c15bc862dd7724643747ed8abcfb.png)
 - If the network has an exception, the **Request Timeout** prompt will appear. In this case, refer to [Instance IP Address Ping Failure](https://intl.cloud.tencent.com/document/product/213/14639) for troubleshooting.
3. Execute the following command and press **Enter** to check whether the remote port is open and accessible.
```
telnet + CVM instance public IP address + Port number
```
For example, execute the `telnet 139.199.XXX.XXX 3389` command. This is shown in the following figure:
![](//mc.qcloudimg.com/static/img/e18be3704977545d5c952d3a583f2ccc/image.png)
 - Normal: Black screen, only the cursor appears. This indicates that the port (3389) is accessible. Please [check whether the instance remote desktop service is enabled](#F2).
 - Abnormal: The connection fails, as shown in the following figure. A network exception occurs, please check the corresponding part of the network.
 ![](https://main.qcloudimg.com/raw/e3996140e2c1895d2ba2b1dfa637f998.png)
 
<span id = "F2"></span>
### Checking remote desktop service configuration

#### Logging in to the CVM using the VNC

> We recommend you use the VNC method if standard CVM login methods fail.
>
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
2. Select the CVM to be checked and click **Log In**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the **Log into Windows instance** window that pops up, select **Alternative login methods (VNC)**, and click **Log In Now** to log in to the CVM.
4. In the login window that pops up, select **Send Remote Command** in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

#### Checking whether the remote desktop configuration of the CVM is enabled

1. In the CVM, right click **This Computer** > **Properties** to open the **System** window.
2. In the **System** window, select **Advanced System Configurations** to open the **System Properties** window.
3. In the **System Properties** window, select the **Remote** tab page. Check whether **Allow remote connections to this computer** under **Remote Desktop** is checked. This is shown in the following figure.
![](https://main.qcloudimg.com/raw/2ee4d1abf5ebf351ed814d6644bc7d58.png)
 - If yes, the remote connection configuration is enabled. Please [check whether remote access ports are enabled](#F3).
 - If no, check **Allow remote connections to this computer**, and try to remotely connect to the instance again to check whether the connection is successful.

<span id = "F3"></span>
### Checking whether remote access ports are open

1. In the CVM, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> to open the **Windows PowerShell** window.
2. Execute the following command to check the remote desktop running status (remote desktop service port is 3389 by default).
```
netstat -ant | findstr 3389
```
 - If a result similar to the following is returned, the status is normal. You can [restart the remote desktop](#F4) and try to remotely connect to the instance again to check whether the connection is successful.
![](https://main.qcloudimg.com/raw/5206af71e86f8126e9e6845bbeef21b2.png)
 - If no connection is shown, the status is abnormal. You can [check whether the remote ports of the registry are correct](#F5).

<span id = "F5"></span>
### Checking whether the remote ports in the registry are consistent

> This step guides you to check whether the **TCP PortNumber** and **RDP Tcp PortNumer** are the same.
>
1. In the CVM, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, select <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>, and enter **regedit**. Press **Enter** to open the **Registry Editor** window.
2. In the registry navigation on the left, expand the following directories in order: **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Terminal Server** > **Wds** > **rdpwd** > **Tds** > **tcp**.
3. Locate the PortNumber in **tcp** and note down the port number (3389 by default), as shown below:
![](https://main.qcloudimg.com/raw/e67b696fd25b3355c9038f99a08b90be.png)
4. In the registry navigation on the left, expand the following directories in order: **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Terminal Server** > **WinStations** > **RDP-Tcp**.
5. Locate PortNumber in **RDP-Tcp** and check whether the PortNumber data in **RDP-Tcp** is the same as the one in **tcp**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/8240dd43dcb3ca246caf3397e4a1e84f.png)
 - If they are not the same, execute [Step 6](#F5_step6).
 - If they are the same, [restart the remote login service](#F4).
6. Double click PortNumber in **RDP-Tcp**.
7. In the dialog box that pops up, modify **Value Data** to an unoccupied port number between 0 - 65535, ensuring **TCP PortNumber** and **RDP Tcp PortNumer** port numbers are the same, and click **OK**.
7. After modification, restart the instance in [CVM Console](https://console.cloud.tencent.com/cvm), and try to remotely connect to the instance again to check whether the connection is successful.


<span id = "F4"></span>
### Restarting the remote log in service

1. In the CVM, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, select <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>, and enter **services.msc**. Press **Enter** to open the **Services** window.
2. Locate and right-click **Remote Desktop Services**. Select **Restart** to restart the remote login service. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/396ee711bb64c8fb1966112a81dd0fd4.png)

## Other Operations

If you are still unable to remotely log in after performing the above-mentioned operations, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
