## Symptom
When trying to connect to a Windows Lighthouse instance remotely on a local computer, you see the following error message:
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

Remote Desktop can't connect to the remote computer for one of these reasons: 
1) Remote access to the server is not enabled
2) The remote computer is turned off
3) The remote computer is not available on the network

Make sure the remote computer is turned on and connected to the network, and that remote access is enabled.


## Possible Cause

Possible causes include but are not limited to the following. Make analysis based on the actual situation.
- The instance is in an abnormal status.
- The remote login port (3389 by default) is not opened in the firewall of the instance.
- Remote Desktop Services is not started.
- There are issues with Remote Desktop settings.
- There are issues with Windows Firewall settings.


## Solutions
Troubleshoot the problems as instructed in [Steps](#ProcessingSteps).


## Steps[](id:ProcessingSteps)


### Checking if the instance is running
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. On the **Instances** page, check whether the instance is in **Running** status.
![](https://qcloudimg.tencent-cloud.cn/raw/bb5692c525a98a1ec44a16919d8a1082.png)
 - If yes, proceed to the next step.
 - If no, start the Windows instance.


### Checking if port 3389 is opened
1. On the instance details page, select the **Firewall** tab.
2. Check whether the remote login port (3389 by default) is opened.
![](https://qcloudimg.tencent-cloud.cn/raw/309afd38d27cb32cc87b9ed13a528903.png)
 - If yes, proceed to the next step.
 - If no, edit the firewall rules to open the port as instructed in [Adding firewall rules](https://intl.cloud.tencent.com/document/product/1103/41393).

### Checking remote desktop service
1. [Log in to the Windows instance via VNC](https://intl.cloud.tencent.com/document/product/1103/46399) and check whether the remote desktop service of the instance is enabled.
<dx-alert infotype="explain" title="">
 - The following operations use an instance on Windows Server 2016 as an example.
</dx-alert>
2. Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **System** in the pop-up menu.
3. In the *System* pop-up window, select **Advanced System Settings**.
4. In the *System Properties* pop-up window, select the **Remote** tab and check whether the **Allow remote connections to this computer** is selected.
![](https://qcloudimg.tencent-cloud.cn/raw/0356bda5bdedb2344e340d7995d29146.png)
 - If yes, proceed to [step 5](#step04_5).
 - If no, select it and click **OK**.
5. [](id:step04_5) Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **Computer Management** in the pop-up menu.
6. On the left sidebar in the **Computer Management** window, select **Services and Applications** > **Services**.
7. In the service list on the right, check whether **Remote Desktop Services* is started.
![](https://qcloudimg.tencent-cloud.cn/raw/42fba8503a6053ecd14af65f05f7aea5.png)
 - If yes, proceed to [step 8](#step04_8).
 - If no, start the service.
8. [](id:step04_8) Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **Run** in the pop-up menu.
9. In the **Run** pop-up window, enter **msconfig** and click **OK**.
10. In the **System Configuration** pop-up window, check whether **Normal startup** is selected as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b677a97fd46216dc02b9415d44fd3c1e.png)
 - If yes, proceed to the next step.
 - If no, select it and click **OK**.


### Checking Windows instance system settings
1. [Log in to the Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496) and check the system settings of the instance.
<dx-alert infotype="explain" title="">
 The following operations use an instance on Windows Server 2016 as an example.
</dx-alert>
2. Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **Run** in the pop-up menu.
3. In the **Run** pop-up window, enter **services.msc** and press **Enter** to open the **Services** window.
4. Double-click to open the **Remote Desktop Services** properties and check whether **Remote Desktop Services** is running.
![](https://qcloudimg.tencent-cloud.cn/raw/ed7f0b5c0f23091ee39168d6596aa722.png)
 - If yes, proceed to [step 5](#step05_5).
 - If no, set **Startup Type** to **Automatic** and **Service Status** to **Running** (i.e., clicking **Start**).
5. [](id:step05_5) Right-click <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;"> and select **Control Panel** in the pop-up menu.
6. In **Control Panel**, select **System and Security** > **Windows Firewall**.
7. In **Windows Firewall**, check the status of the Windows firewall.
![](https://qcloudimg.tencent-cloud.cn/raw/116284aa8fff898a0c7923cc2764594b.png)
 - If the status is **On**, proceed to [step 8](#step8).
 - If the status is **Off**, toggle it on. If you can't turn it on, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
8. [](id:step8) In **Windows Firewall**, select **Allow an app through Windows Firewall** to open the **Allowed apps** window.
9. In the **Allowed apps** window, check whether **Remote Desktop** is selected in **Allowed apps and features**.
![](https://qcloudimg.tencent-cloud.cn/raw/1a44e0f5259913bc8204ebeba4227692.png)
 - If yes, proceed to [step 10](#step10).
 - If no, select **Remote Desktop** to allow it through Windows Firewall.
10. [](id:step10) In **Windows Firewall**, click **Turn Windows Firewall on or off** to open the **Custom Settings** window.
11. In the **Custom Settings** window, set **Private network settings** and **Public network settings** to **Turn off Windows Firewall (not recommended)**.
![](https://qcloudimg.tencent-cloud.cn/raw/96cfb97a26526ffc3aa31e7f1c7339e3.png)

If you still cannot connect to the Windows instance from the remote desktop, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.



