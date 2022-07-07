## Symptom
When trying to connect to a Windows instance remotely from Windows, you get the following message:
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

The remote desktop can't connect to the remote computer for one of the following reasons:
1) Remote access to the server is not enabled
2) The remote computer is turned off
3) The remote computer is not available on the network

Make sure the remote computer is turned on and connected to the network, and that remote access is enabled.


## Possible Causes

Possible causes include but are not limited to the following:
- The instance is in an abnormal status.
- The CVM instance does not have a public IP or the public network bandwidth is 0.
- The remote login port (3389 by default) is not opened in the security group bound to the instance.
- Remote Desktop Services is not started.
- Incorrect Remote Desktop settings
- Incorrect Windows Firewall settings

## Troubleshooting Directions


### Checking instance status
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, check whether the instance is "Running".
![](https://main.qcloudimg.com/raw/03cf75228bc468d2e436f876f229ebc9.png)
 - If yes, [check whether the CVM instance has a public IP](#step01).
 - If no, start up the Windows instance.


### Checking public IP[](id:step01)
Check whether the CVM instance has a public IP in the CVM console.
![](https://main.qcloudimg.com/raw/58c75d68372069652ec09ab93cfdbdc0.png)

 - If yes, [check whether you have purchased public network bandwidth](#step02).
 - If no, [apply for an EIP and bind it to the CVM instance](https://intl.cloud.tencent.com/document/product/213/16586).


### Checking public network bandwidth[](id:step02)
Check whether the public network bandwidth is 0 Mbps. At least 1 Mbps of public network bandwidth is required.
 - If yes, increase the bandwidth to 5 Mbps or above by [adjusting network configuration](https://intl.cloud.tencent.com/document/product/213/15517).
![](https://main.qcloudimg.com/raw/29b771d9de5d1ecdadb872c0378a31c7.png)
 - If no, [check whether the remote login port (3389) of the instance is opened](#step03).


### Checking remote login port (3389)[](id:step03)
1. On the instance management page in the CVM console, click the target instance ID/name to enter its details page.
2. In the **Security Groups** tab, check whether the remote login port (3389 by default) is opened.
![](https://main.qcloudimg.com/raw/28b5f0a038dd354346745bd97f724350.png)
 - If yes, [check the remote desktop service](#step04).
 - If no, edit the corresponding security group rules to open the port as instructed in [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

### Checking remote desktop service[](id:step04)
1. [Log in to the instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496) and check whether the remote desktop service of the Windows instance is enabled.
<dx-alert infotype="explain" title="">
 The following operations use an instance on Windows Server 2016 as an example.
</dx-alert>
2. Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **System** in the pop-up menu.
3. In the *System* pop-up window, select **Advanced System Settings**.
4. In the *System Properties* pop-up window, select the **Remote** tab and check whether the **Allow remote connections to this computer** is selected:
 - If yes, proceed to [step 5](#step04_5).
 - If no, select it and click **OK**.
5. [](id:step04_5) Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **Computer Management** in the pop-up menu.
6. On the left sidebar in the **Computer Management** window, select **Services and Applications** > **Services**.
7. In the service list on the right, check whether **Remote Desktop Services* is started:
 - If yes, proceed to [step 8](#step04_8).
 - If no, start the service.
8. [](id:step04_8) Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **Run** in the pop-up menu.
9. In the **Run** pop-up window, enter **msconfig** and click **OK**.
10. In the **System Configuration** pop-up window, check whether **Normal startup** is selected:
 - If yes, [check Windows instance system settings](#step05).
 - If no, select it and click **OK**.


### Checking Windows instance system settings[](id:step05)
1. [Log in to the Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496) and check the system settings of the instance.
<dx-alert infotype="explain" title="">
The following operations use an instance on Windows Server 2012 as an example.
</dx-alert>
2. Right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img> and select **Run** in the pop-up menu.
3. In the **Run** pop-up window, enter **services.msc** and press **Enter** to open the **Services** window.
4. Double-click to open the **Remote Desktop Services** properties and check whether **Remote Desktop Services** is running as shown below:
![](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png)
 - If yes, proceed to [step 5](#step05_5).
 - If no, set **Startup Type** to **Automatic** and **Service Status** to **Running** (i.e., clicking **Start**).
5. [](id:step05_5)Right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img> and select **Run** in the pop-up menu.
6. In the **Run** pop-up window, enter **sysdm.cpl** and press **Enter** to open the **System Properties** window.
7. On the **Remote** tab, check whether the **Remote Desktop** is set to **Allow remote connections to this computer** as shown below:
![](https://main.qcloudimg.com/raw/cbf2b2797bd48777008753f389574674.png)
 - If yes, proceed to [Step 8](#step05_8).
 - If no, set **Remote Desktop** to **Allow remote connections to this computer**.
8. [](id:step05_8) Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img> and select **Control Panel** in the pop-up menu.
9. In **Control Panel**, select **System and Security** > **Windows Defender Firewall**.
10. In **Windows Defender Firewall**, check the Windows Defender Firewall status as shown below:
![](https://main.qcloudimg.com/raw/e74937594a03c141e6e5ac753f025d91.png)
 - If the status is **On**, proceed to [Step 11](#step05_11).
 - If the status is **Off**, contact [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
11. [](id:step05_11) In **Windows Defender Firewall**, click **Allow an app or feature through Windows Defender Firewall** to open the **Allowed apps** window.
12. In the **Allowed apps** window, check whether **Remote Desktop** is selected in **Allowed apps and features**.
![](https://main.qcloudimg.com/raw/dfed8792ce1dd8b32bee4aaa02ef6bbf.png)
 - If yes, proceed to [Step 13](#step05_13).
 - If no, select **Remote Desktop** to allow **Remote Desktop** through Windows Defender Firewall.
13. [](id:step05_13) In **Windows Defender Firewall**, click **Turn Windows Firewall on or off** to open the **Customize Settings** window.
14. In the **Customize Settings** window, set **Private network settings** and **Public network settings** to **Turn off Windows Defender Firewall (not recommended)** as shown below:
![](https://main.qcloudimg.com/raw/5d5f8c4d7b783bc1018e03368ae400bc.png)

If you still cannot connect to the Windows instance on a remote desktop, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.



