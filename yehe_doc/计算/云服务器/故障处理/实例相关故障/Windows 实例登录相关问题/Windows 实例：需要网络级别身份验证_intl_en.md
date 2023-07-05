This document describes how to solve the issue of **network level authentication** when connecting to a Windows instance using Remote Desktop.

## Issue
Windows Remote Desktop fails to connect to your Windows instance with the error message **The remote computer requires Network Level Authentication, which your computer does not support. For assistance, contact your system administrator or technical support.**
![](https://main.qcloudimg.com/raw/409b3259fa13220e8cde0790aa87488b.jpg)

## Troubleshooting

> In the following steps, we use Windows Server 2016 as an example.
>

### Logging in to the CVM using VNC
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, find the desired CVM instance. Click **Log In**, as shown in the following figure:
![CVM index page](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the **Log in to Windows instance** window that appears, select **Alternative login methods (VNC)**. Click **Log In Now** to log in to the CVM.
4. In the login window that appears, select **Send Remote Command** in the top-left corner. Click **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Modifying the Windows registry

1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>. Enter **regedit** and press **Enter** to open the Registry Editor.
2. Using navigation tree on the left-side, navigate to **Computer** > **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Lsa**. In the right-side pane, select **Security Packages**, as shown in the following figure:
![Security Packages](https://main.qcloudimg.com/raw/db037b5131ff44af72b560fbac4931e1.png)
3. Double click **Security Packages** to open the **Edit Multi-String** dialog box.
4. In the **Edit Multi-String** dialog box, add **tspkg** under **Value Data** and click **OK**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/cca2bce345b48569d45fd391ee65bc51.png)
5. Using navigation tree on the left-side, navigate to **Computer** > **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **SecurityProviders**. In the right-side pane, select **SecurityProviders**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/14e84c77ae1d1d3c5bc2ab091543a957.png)
6. Double-click **SecurityProviders** to open the **Edit Multi-String** dialog box.
7. Append `,credssp.dll` to the end of the **Value Data** field in the **Edit Multi-String** dialog box. Click **OK** as shown in the following figure:
![](https://main.qcloudimg.com/raw/34b98c226c359b070e2f03c2ff1c6e42.png)
8. Close the registry editor and restart the instance. You can now log in remotely.

