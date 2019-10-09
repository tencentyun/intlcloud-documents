## Scenario
When trying to connect to a Windows instance remotely from Windows, you get the following message:
![](https://main.qcloudimg.com/raw/fc8eb4050af9a2b5d808b6bf5f40cbe7.png)

Remote Desktop can’t connect to the remote computer for one of these reasons:
I) Remote access to the server is not enabled
II) The remote computer is turned off
III) The remote computer is not available on the network

Make sure the remote computer is turned on and connected to the network, and that remote access is enabled.


## Possible Causes

Possible causes include but are not limited to the following. Please make analysis based on the actual situation.
- The instance is in an abnormal state 
-  The CVM does not have a public IP or the public network bandwidth is 0
- The remote login port (3389 by default) is not opened to the Internet in the security group(s) bound with the instance
- Remote Desktop Services is not started
- There are issues with Remote Desktop settings
- There are issues with Windows Firewall settings

## Troubleshooting Steps

### Checking if the instance is running
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance list, check if the instance is **Running** as shown below:
![CVM list page](https://main.qcloudimg.com/raw/eacd0a1d69d696d81a39d8239c6c04bc.png)
 - If it is running, please [check whether the CVM has a public IP](#step01).
 - If it is not, please start up the Windows instance.

<span id="step01"></span>
### Checking whether the CVM has a public IP
Please check whether the CVM has a public IP in the CVM console as shown below:
![No public IP](https://main.qcloudimg.com/raw/c3de8a36a5fec23c75eceb22eb239d66.png)
 - If there is one, please [check whether you have purchased public network bandwidth](#step02).
 - If there is not, please [apply for an elastic public IP and bind it with the CVM](https://intl.cloud.tencent.com/document/product/213/16586).
 
<span id="step02"></span>
### Checking whether you have purchased public network bandwidth
Check whether the public network bandwidth is 0 MB. You need to have at least 1 MB of public network bandwidth.
 - If it is, please increase the bandwidth to 1 Mbps or above by [adjusting network configuration](https://intl.cloud.tencent.com/document/product/213/15517).
![](https://main.qcloudimg.com/raw/08fa61c6bd7c539ced5efa21988c7057.png)
 - If it is not, please [check whether the remote login port (3389) of the instance is opened to the Internet](#step03).

<span id="step03"></span>
### Checking whether the remote log in port (3389) of the instance is opened to the Internet
1. Click the instance you want to log in in the console to enter the instance information page.
2. In the Security Groups tab, check whether the remote login port (3389 by default) is opened to the Internet in the security group(s) bound with the instance as shown below:
![Security Group](https://main.qcloudimg.com/raw/8591cea100c0e39b7d2f6cde250b4b16.png)
 - If it is, please [check the system settings of the Windows instance](#step04)
 - If it is not, please edit the corresponding security group rules to open the port to the Internet. For directions, see [Operation Guide](https://intl.cloud.tencent.com/document/product/213/18197) on security group.

<span id="step04"></span>
### Checking the system settings of the Windows instance
1. Log in to the instance using VNC and check the system settings of the Windows instance.
>? For details on VNC login, refer to the “Login via VNC” section in [Log into Windows Instances](https://intl.cloud.tencent.com/document/product/213/5435).
2. In the operating system interface, click **Start** > **Run**, enter **services.msc** in the Run box, press **Enter** to open the Services window.
3. Double click Remote Desktop Services to open the “Remote Desktop Services Properties” window and check whether Remote Desktop Services is running as shown below:
![Remote Desktop Services](https://main.qcloudimg.com/raw/ad9fc18310fc823ea11883f9c31b7838.png)
 - If it is, please go to [Step 4](#step04_4).
 - If it is not, please set the “Startup type” to “Automatic” and click **Start** to set “Service status” to “Running”.
4. <span id="step04_4">Click **Start** > **Run**，enter **sysdm.cpl** in the Run box, and press **Enter** to open the “System Properties” window.</span>
5. In the “Remote” tab, check whether the “Remote Desktop” is set to “Allow remote connections to this computer” as shown below:
![Remote configuration](https://main.qcloudimg.com/raw/7cadb6d62af77f7035d973283b104ac8.png)
 - If it is, please go to [Step 6] (#step04_6).
 - If it is not, please set Remote Desktop to “Allow remote connections to this computer”.
6. <span id="step04_6">Click **Start**, select **Control Panel** to open the control panel.</span>
7. In the “Control Panel”, select **System and Security** > **Windows Defender Firewall** to open “Windows Defender Firewall”.
8. In “Windows Defender Firewall”, check the status of Windows Defender Firewall as shown below:
![Windows Defender Firewall status](https://main.qcloudimg.com/raw/5a18e345dd8fcb6aaa5b9f95c4bc4d63.png)
 - If the status is “On”, please go to [Step 9] (#step04_9).
 If the status is “Off”, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
9. <span id = “step04_9”>In “Windows Defender Firewall”, select **Allow an app through Windows Firewall** to open the “Allowed apps” window. </span>
10. In the "Allowed apps" window, check whether "Remote Desktop” is checked in "Allowed apps and features” as shown below:
![Check Remote Desktop](https://main.qcloudimg.com/raw/4a0d3906b5be714610fa8e21e4ed3624.png)
 - If it is, please go to [Step 11](#step04_11).
 - If it is not, please check “Remote Desktop”, to allow “Remote Desktop” through Windows Firewall.
11. <span id = “step04_11”>In “Windows Defender Firewall”, select **Turn Windows Defender Firewall on or off** to open the “Customize Settings” window. </span>
12. In the “Customize Settings” window, set “Private network settings” and “Public network settings” to “Turn off Windows Defender Firewall (not recommended)” as shown below:
![Turn off](https://main.qcloudimg.com/raw/4a09dea7a9695599b02a2facc1be02ec.png)

If you still cannot connect to the Windows instance through Remote Desktop after taking the steps above, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

