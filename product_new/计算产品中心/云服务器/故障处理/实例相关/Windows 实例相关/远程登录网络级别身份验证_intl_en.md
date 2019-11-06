This document describes how to handle alarm prompts like **network level authentication** when connecting to a Windows instance.

## Fault Symptoms
When using Windows remote desktop, an error occurs, asking for **network level authentication**.
![](https://main.qcloudimg.com/raw/409b3259fa13220e8cde0790aa87488b.jpg)

## Troubleshooting

> The following operations take Windows Server 2016 as an example.
>

### Logging in to the CVM using VNC
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page, find the target CVM instance, and click **Log in**. This is shown in the following figure:
![CVM list page](https://main.qcloudimg.com/raw/038fce530c6c6827796e51d896306a93.png)
3. In the **Log in to a Windows Instance** window that pops up, select **Ohter login methods (VNC)**, and click **Log in** to log in to the CVM.
4. In the login window that pops up, select **Send remote command** in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/2dec43fa6ddb5e442da59c75f7a34b0f.png)

### Modifying the Registry

1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, enter **regedit**, and press **Enter** to open the Registry Editor.
2. In the left-side navigation tree, expand the following directories: **Computer** > **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Lsa**, and in the right-side window, find **Security Packages**. This is shown in the following figure:
![Security Packages](https://main.qcloudimg.com/raw/db037b5131ff44af72b560fbac4931e1.png)
3. Double click **Security Packages** to open the **Edit Multi-String** dialog box.
4. In the **Edit Multi-String** dialog box, add **tspkg** in **Value data**, and click **OK**. This is shown in the following figure.
![](https://main.qcloudimg.com/raw/cca2bce345b48569d45fd391ee65bc51.png)
5. In the left-side navigation tree, expand the following directories: **Computer** > **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **SecurityProviders**, and in the right-side window, find **SecurityProviders**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/14e84c77ae1d1d3c5bc2ab091543a957.png)
6. Double click **SecurityProviders** to open the **Edit Multi-String** dialog box.
7. Add `, credssp.dll` to the end of **Value data** field in the **Edit Multi-String** dialog box. Click **OK**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/34b98c226c359b070e2f03c2ff1c6e42.png)
8. Close the registry editor and restart the instance. You can now connect remotely.

