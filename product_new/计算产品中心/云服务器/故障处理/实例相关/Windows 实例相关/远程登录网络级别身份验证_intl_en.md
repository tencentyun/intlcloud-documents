This document describes how to manage alarm prompts such as **network level authentication** when connecting to a Windows instance.

## Problems
When using Windows remote desktop, you cannot connect to a remote computer and a prompt appears, requiring **network level authentication**.
![](https://main.qcloudimg.com/raw/a2976a1f9d34cadeb378687ce4f1ff64.png)

## Troubleshooting

>? The following operations take Windows Server 2016 as an example.
>

### Logging in to the CVM using VNC
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page, find the target CVM instance, and click **Log In**. This is shown in the following figure:
![CVM list page](https://main.qcloudimg.com/raw/038fce530c6c6827796e51d896306a93.png)
3. In the **Log into Windows instance** window that pops up, select **Alternative login methods (VNC)**, and click **Log In Now** to log in to the CVM.
4. In the login window that pops up, select **Send Remote Command** in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/2dec43fa6ddb5e442da59c75f7a34b0f.png)

### Modifying the registry

1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, enter **regedit**, and press **Enter** to open the Registry Editor.
2. In the left-side navigation tree, expand the following directories: **Computer** > **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Lsa**, and in the right-side window, find **Security Packages**. This is shown in the following figure:
![Security Packages](https://main.qcloudimg.com/raw/7a082160ed82ca713ca6a4f46af84eaf.png)
3. Double click **Security Packages** to open the **Edit Multi-String** dialog box.
4. In the **Edit Multi-String** dialog box, add **tspkg** in **Value Data**, and click **OK**. This is shown in the following figure.
![](https://main.qcloudimg.com/raw/5568c403df3d9aa9afb3cdc5972df0f6.png)
5. In the left-side navigation tree, expand the following directories: **Computer** > **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **SecurityProviders**, and in the right-side window, find **SecurityProviders**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/41611d8e70772cf2254236a7fb7fa1f0.png)
6. Double click **SecurityProviders** to open the **Edit Multi-String** dialog box.
7. Add `, credssp.dll` at the end of **Value Data** field in **Edit Multi-String** dialog box. Click **OK**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/b62ae3112e4fadc99817fcf0864740cf.png)
8. Close the registry editor and restart the instance. You can now log in remotely.

