This article describes how to troubleshoot remote login failures caused by port problems.
> The following uses a CVM instance running Windows Server 2012 as an example to describe the steps.
>

## Tools
You can use the following tools to check if the login issues are related to ports and security group configurations:
- [Self-diagnosis](https://console.cloud.tencent.com/workorder/check) 
- [Security group (port) helper](https://console.cloud.tencent.com/vpc/helper) 

If the problem is indeed a security group configuration problem, use **Open all ports** in the [Security group (port) helper](https://console.cloud.tencent.com/vpc/helper) to open related ports and try to log in again. If you still cannot log in after opening the ports, refer to the following for troubleshooting.

## Troubleshooting

### Checking network connectivity

You can use the Ping command to test network connectivity from your PC. You should run the test from computers in different network environments (such as different IP ranges or ISPs) to check whether it is a local network problem or a server problem.

1. Open the command line tool on your local computer.
 - Windows: Click **Start** -> **Run** and enter **cmd**. A Command Prompt window appears.
 - MacOS: Open a Terminal window.
2. Run the following command to test network connection.
```
ping + CVM_Instance_public_IP_address
```
For example, `ping 139.199.xxx.xxx`.
 - If you see results similar to what is shown in the following figure, your network connection to the CVM instance is normal. In this case, [check the remote desktop configuration](#F2).
![](https://main.qcloudimg.com/raw/52e6c15bc862dd7724643747ed8abcfb.png)
 - If **Request Timeout** appears, your network connection to the CVM instance is not working properly. In this case, refer to [Instance IP Address Ping Failure](https://intl.cloud.tencent.com/document/product/213/14639) for troubleshooting instructions.
3. Run the following command to check whether the remote port is open.
```
telnet CVM_instance_public_IP_address port_number
```
For example, `telnet 139.199.xxx.xxx 3389`, as shown in the following figure:
![](https://mc.qcloudimg.com/static/img/e18be3704977545d5c952d3a583f2ccc/image.png)
 - If you see a black screen with only the cursor, that indicates the port (3389) is open. For the next step, [check whether remote desktop service is enabled on the instance](#F2).
 - If the connection fails, as shown in the following figure, that means a network exception occurred. Check the corresponding part of the network.
 ![](https://main.qcloudimg.com/raw/e3996140e2c1895d2ba2b1dfa637f998.png)
 
<span id = "F2"></span>
### Checking remote desktop configuration

#### Logging in to the CVM instance using VNC

> It is recommended that you use VNC to login only if the standard login methods fail.
>
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. Select the desired CVM and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. The **Log into Windows instance** page appears. Select **Alternative login methods (VNC)** and click **Log In Now** to log in to the CVM instance.
4. The log in page appears. Select **Send Ctrl-Alt-Del** in the top left corner and click **Ctrl-Alt-Delete** to enter the system login interface, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

#### Checking if remote desktop is enabled on the CVM instance

1. Log in to the CVM instance. Right click **This Computer** from the Desktop and select **Properties** to open the **System** window.
2. In the **System** window, select **Advanced System Configurations** to open the **System Properties** window.
3. In the **System Properties** window, select the **Remote** tab. Check whether **Allow remote connections to this computer** under **Remote Desktop** is selected, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2ee4d1abf5ebf351ed814d6644bc7d58.png)
 - If it is selected, remote connection is enabled. Next, you should [check whether remote access ports are open](#F3).
 - If it is cleared, select **Allow remote connections to this computer** and try to connect to the instance again.

<span id = "F3"></span>
### Checking whether remote access ports are open

1. Log in to the CVM instance. Click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> to open a **Windows PowerShell** window.
2. In the **Windows PowerShell** window, run the following command to check the status of remote desktop (by default, the remote desktop uses port 3389).
```
netstat -ant | findstr 3389
```
 - If you see results similar to what is shown in the following figure, the status is normal. You can try to [restart remote desktop](#F4) and connect to the instance again to check whether the connection is successful.
![](https://main.qcloudimg.com/raw/5206af71e86f8126e9e6845bbeef21b2.png)
 - If no connection is shown, remote desktop is not functioning properly. You can [check whether the remote desktop ports in registry are consistent](#F5).

<span id = "F5"></span>
### Checking whether the remote desktop ports in registry are consistent

> This section describes how to check the values of **TCP PortNumber** and **RDP Tcp PortNumber**. They must be the same.
>
1. Log in to the CVM instance, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, select <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>, and enter **regedit**. Press **Enter** to open the **Registry Editor** window.
2. In the navigation pane on the left, expand the following directories: **HKEY_LOCAL_MACHINE** -> **SYSTEM** -> **CurrentControlSet** -> **Control** -> **Terminal Server** -> **Wds** -> **rdpwd** -> **Tds** -> **tcp**.
3. Locate the PortNumber in **tcp** and record the port number (3389 by default), as shown in the following figure:
![](https://main.qcloudimg.com/raw/6762d059263b1c589414461e522d1e9f.png)
4. In the navigation pane on the left, expand the following directories: **HKEY_LOCAL_MACHINE** -> **SYSTEM** -> **CurrentControlSet** -> **Control** -> **Terminal Server** -> **WinStations** -> **RDP-Tcp**.
5. Locate PortNumber in **RDP-Tcp** and check whether the PortNumber value in **RDP-Tcp** is the same as the one in **tcp**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/9d68cec10e75afe621beb6c914d393cb.png)
 - If they are not the same, follow [Step 6](#F5_step6).
 - If they are the same, [restart remote desktop](#F4).
6. Double click PortNumber in **RDP-Tcp**.
7. In the dialog box that appears, modify **Value Data** to an unoccupied port number between 0 - 65535. Ensure **TCP PortNumber** and **RDP Tcp PortNumber** are the same, and click **OK**.
7. Restart the instance using the [CVM Console](https://console.cloud.tencent.com/cvm), and try to remotely connect to the instance again to check whether the connection is successful.


<span id = "F4"></span>
### Restarting remote desktop

1. Log in to the CVM instance. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and select <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>. Enter **services.msc** and press **Enter** to open the **Services** window.
2. In the **Services** window, right-click **Remote Desktop Services** and select **Restart** to restart the remote desktop service, as shown in the following figure:
![](https://main.qcloudimg.com/raw/396ee711bb64c8fb1966112a81dd0fd4.png)

## If All Else Fails

If you are still unable to remotely log in after performing the above-mentioned steps, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2) for further assistance.
