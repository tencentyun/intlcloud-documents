## Scenario
When trying to remotely connect to a Windows instance from Windows, you are prompted with the message shown in the following figure:
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

You cannot connect to the remote computer by using Remote Desktop for one of these reasons:
1) Remote access to the server is not enabled.
2) The remote computer is off.
3) The remote computer is not available on the network.

Check that the remote computer is on and connected to the network, and that remote access is enabled.


## Possible Causes

Possible causes for this problem include but are not limited to the following. Troubleshoot the problem based on your actual circumstances.
- The instance is in an abnormal state.
- The CVM does not have a public IP address or the public network bandwidth is 0.
- The remote login port (port 3389 by default) is not opened to the Internet in the security group(s) bound with the instance.
- Remote Desktop Services has not been started.
- Remote Desktop settings are incorrect.
- Windows Firewall settings are incorrect.

## Troubleshooting Steps

### Checking if the instance is running
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, check whether the instance is **Running**, as shown in the following figure:
![CVM list page](https://main.qcloudimg.com/raw/03cf75228bc468d2e436f876f229ebc9.png)
 - If yes, [check whether the CVM has a public IP address](#step01).
 - If no, start up the Windows instance.

<span id="step01"></span>
### Checking whether the CVM has a public IP address
Check whether the CVM has a public IP address in the CVM console, as shown in the following figure:
![No public IP addresses](https://main.qcloudimg.com/raw/58c75d68372069652ec09ab93cfdbdc0.png)
 - If yes, [check whether you have purchased a public network bandwidth](#step02).
 - If no, [apply for an elastic public IP address and bind it with the CVM](https://intl.cloud.tencent.com/document/product/213/16586).
 
<span id="step02"></span>
### Checking whether you have purchased a public network bandwidth
Check whether the public network bandwidth is 0 Mbps. You need to ensure at least 1 Mbps of public network bandwidth.
 - If yes, increase the bandwidth to 1 Mbps or above by [adjusting the network configuration](https://intl.cloud.tencent.com/document/product/213/15517).
![](https://main.qcloudimg.com/raw/29b771d9de5d1ecdadb872c0378a31c7.png)
 - If no, [check whether the remote login port (3389) of the instance has been opened to the Internet](#step03).

<span id="step03"></span>
### Checking whether the remote login port (3389) of the instance has been opened to the Internet
1. On the instance management page in the CVM console, click the ID or name of the instance for login to go to the instance details page.
2. On the "Security Groups" tab page, check whether the remote login port (port 3389 by default) has been opened to the Internet in the security group(s) bound with the instance, as shown in the following figure:
![Security groups](https://main.qcloudimg.com/raw/28b5f0a038dd354346745bd97f724350.png)
 - If yes, [check the system settings of the Windows instance](#step04).
 - If no, edit the corresponding security group rules to open the port to the Internet. For directions, see [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/213/34272).

<span id="step04"></span>
### Checking the system settings of the Windows instance
1. [Log in to the Windows instance by using VNC](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png) and check the system settings of the Windows instance.
> The following operations take Windows Server 2012 as an example.
>
2. In the operating system of the logged-in instance, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, choose **Run**, enter **services.msc** in **Run**, and press Enter to go to the "Service" window.
3. Double-click "Remote Desktop Services" to go to the "Remote Desktop Services Properties" window and check whether Remote Desktop Services are running, as shown in the following figure:
![Remote Desktop Services](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png)
 - If yes, go to [step 4](#step04_4).
 - If no, set "Startup type" to "Automatic" and click **Start** to set "Service status" to "Running".
4. <span id="step04_4">Right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, choose **Run**, enter **sysdm.cpl** in **Run**, and press Enter to go to the "System Settings" window.</span>
5. On the "Remote" tab page, check whether "Remote Desktop" is set to "Allow remote connections to this computer", as shown in the following figure:
![Remote Desktop settings](https://main.qcloudimg.com/raw/cbf2b2797bd48777008753f389574674.png)
 - If yes, go to [step 6](#step04_6).
 - If no, set Remote Desktop to "Allow remote connections to this computer".
6. <span id="step04_6">Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and choose **Control Panel** to open the control panel.</span>
7. In "Control Panel", choose **System and Security** > **Windows Defender Firewall** to open "Windows Defender Firewall".
8. In "Windows Defender Firewall", check the status of Windows Defender Firewall, as shown in the following figure:
![Windows Defender Firewall status](https://main.qcloudimg.com/raw/e74937594a03c141e6e5ac753f025d91.png)
 - If the state is "On", go to [step 9](#step04_9).
 - If the state is "Off", [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
9. <span id = “step04_9”>In "Windows Defender Firewall", select **Allow an app through Windows Firewall** to go to the "Allowed apps" window.</span>
10. In the "Allowed apps" window, check whether "Remote Desktop" is selected in "Allowed apps and features", as shown in the following figure:
![Selecting Remote Desktop](https://main.qcloudimg.com/raw/dfed8792ce1dd8b32bee4aaa02ef6bbf.png)
 - If yes, go to [step 11](#step04_11).
 - If no, select "Remote Desktop" to permit "Remote Desktop" through Windows Firewall.
11. <span id = “step04_11”>In "Windows Defender Firewall", select **Turn Windows Defender Firewall on or off** to go to the "Customize Settings" window.</span>
12. In the "Customize Settings" window, set "Private network settings" and "Public network settings" to "Turn off Windows Defender Firewall (not recommended)", as shown in the following figure:
![Turning off Windows Defender Firewall](https://main.qcloudimg.com/raw/5d5f8c4d7b783bc1018e03368ae400bc.png)

If you still cannot connect to the Windows instance through Remote Desktop after completing the preceding steps, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

