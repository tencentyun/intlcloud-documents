## Overview
COS can be used on Windows mainly with APIs, COSBrowser, or COSCMD.

However, if you are a Windows Server user, you can only use COSBrowser for cloud file storage, which is not friendly for running programs or performing operations. In this case, you can mount the cost-effective COS to Windows Server as local drive as instructed in this document.

>? Examples given in this document apply only to Windows 7 or Windows Server 2012 and later.
>

## Directions
### Download and installation

The following installation procedure is for your reference only. You should perform the installation based on your actual OS:
- Go to [GitHub](https://github.com/billziss-gh/winfsp/releases) to download WinFsp.
You can install it with the default options.
- Go to [Git](https://gitforwindows.org/) or [GitHub](https://github.com/git-for-windows/git/releases/) to download Git.
`Git-2.31.1-64-bit.exe` is downloaded as an example. You can install it with the default options.
- Go to [Rclone](https://rclone.org/downloads/) or [GitHub](https://github.com/rclone/rclone/releases) to download Rclone.
`rclone-v1.55.0-windows-amd64.zip` is downloaded as an example. You can decompress it to any directory. In this example, the package is decompressed to `E:\AutoRclone`.

>? If GitHub cannot be opened or is slow, you can try another way on your own for the download.
>

### Rclone configuration

>!The following configuration process takes Rclone v1.55.0 as an example. Note that the configuration process of other versions may be different.


1. Open any folder, find **This PC** in the left navigation pane, right-click and select **Properties** > **Advanced system settings** > **Environment Variables** > **System variables** > Path**, and click **New* *.
2. In the pop-up window, enter the path where Rclone is decompressed (E:\AutoRclone) and click **OK**.
3. Open Windows PowerShell and run the `rclone --version` command to see whether Rclone is installed successfully.
4. If Rclone is installed successfully, run the `rclone config` command in Windows PowerShell.
5. In Windows PowerShell, enter **n** and press **Enter** to create a new remote.
6. In Windows PowerShell, enter the name of the drive (for example, `myCOS`) and press **Enter**.
7. In the options that are displayed, enter **4** (the one that contains Tencent Cloud) and press **Enter**.
8. In the options that are displayed, enter **11** (the one that contains Tencent Cloud COS) and press **Enter**.
9. When `env_auth>` is displayed, press **Enter**.
10. When `access_key_id>` is displayed, enter the `SecretId` of COS and press **Enter**.
>? We recommend you use sub-account permissions here. You can go to the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page to view your `SecretId` and `SecretKey`.
>
11. When `secret_access_key>` is displayed, enter the `SecretKey` of COS and press **Enter**.
12. Choose the region of the bucket based on the gateway addresses of the Tencent Cloud regions that are displayed.
Guangzhou region is used as an example here. Therefore, you can enter **4** (`cos.ap-guangzhou.myqcloud.com`) and press **Enter**.
13. Select the object permission (`private` or `public-read`) as needed, which takes effect only for objects that are uploaded subsequently. `public-read` is used as an example here. Therefore, you can press **2** and then press **Enter**.
14. Select the storage class for your objects uploaded to COS. `Default` is used as an example here. Therefore, you can press **1** and then press **Enter**.
 - Default: Default option
 - Standard storage class: STANDARD
 - Infrequent access storage mode: Standard_IA
 - Archive storage mode: ARCHIVE
>?To use the INTELLIGENT TIERING or DEEP ARCHIVE storage class, **modify the configuration file** and set the value of `storage_class` to `INTELLIGENT_TIERING` or `DEEP_ARCHIVE`.
>
15. When `Edit advanced config? (y/n)` is displayed, press **Enter**.
16. After confirming the information, press **Enter**.
17. Enter **q** to complete the configuration.


### Modifying configuration file

After performing the configuration above, the Rclone configuration file `vrclone.conf` can be found in the `C:\Users\Username\.config\rclone` directory. You can directly modify the file to update the Rclone configuration.


### Mounting COS as local drive

1. Open the installed Git CMD and enter the command in it. Two use cases are provided here for your choice as needed.
<ul>
<li>To mount COS as a shared drive on LAN (recommended), run the following command:
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &amp;</code>
</pre>
</li>
<li>To mount COS as a local drive, run the following command:
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &</code>
</pre>
	<ul>
		<li>myCOS: Replace it with the user-defined drive name.</li>
		<li>Y: Replace it with the drive letter you want to assign to the drive. Make sure that it does not conflict with other drive letters.</li>
		<li>E:\temp: Local cache directory, which can be configured as needed.</li>
	</ul>
</li>
</ul>
If "The service rclone has been started" is displayed, the mount is successful.
2. Enter **exit** to close the terminal.
3. Find the `myCOS(Y:)` drive in **This PC**.
If you open this drive, you can see all buckets in Guangzhou region. You can upload, download, create, and delete files and do more in the drive as needed.
>!
> - If any error is reported during the process, you can view the error messages from Git Bash.
> - If you delete a bucket from the drive, the bucket will be deleted from COS, no matter whether there are objects stored in it or not.
> - If you change the name of a bucket in the drive, the bucket name in COS will also be changed.
> 


### Running mounted drive automatically at startup

The mounted drive will disappear after the server is restarted. Therefore, you can perform the following operations to set the drive to automatically run at startup.

1. Create `startup_rclone.vbs` and `startup_rclone.bat` files in the `E:\AutoRclone` directory.
2. In `startup_rclone.bat`, write the following mount command:
 - To mount COS as a shared drive on LAN, enter the following command:
```plaintext
rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &
```
 - To mount COS as a local drive, enter the following command:
```
rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &
```
3. In `startup_rclone.vbs`, write the following code:
```plaintext
CreateObject("WScript.Shell").Run "cmd /c E:\AutoRclone\startup_rclone.bat",0
```
>! Replace the path with the actual one.
>
4. Cut the `startup_rclone.vbs` file to the `%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup` directory.
5. Restart the server.

## Related Operations

You can also use a third-party tool to mount COS to a Windows server as local drive. The following shows the mounting procedure with the TntDrive tool:
1. Download and install TntDrive.
2. Open TntDrive and click **Account** > **Add New Account** to create an account.
![](https://main.qcloudimg.com/raw/90b4a262b11b6933f48b4922cad4fdc4.png)
Main parameters are as described below:
 - **Account Name**: User-defined account name.
 - **Account Type**: Account type. As COS is compatible with S3, you can select **Amazon S3 Compatible Storage**.
 - **REST Endpoint**: Enter the region of your bucket. For example, if your bucket resides in Guangzhou region, set this parameter to `cos.ap-guangzhou.myqcloud.com`.
 - **Access Key ID**: Enter the value of your `SecretId`, which can be created/obtained on the [Manage API Key](https://console.cloud.tencent.com/capi) page.
 - **Secret Access Key**: Enter the value of your `SecretKey`.
3. Click **Add new account**.
4. In the TntDrive window, click **Add New Mapped Drive** to create a mapped drive.
![](https://main.qcloudimg.com/raw/fa09500f96ba8e5c8144d39cd5471991.png)
Main parameters are as described below:
 - **Amazon S3 bucket**: Enter the path or name of the bucket. You can click the icon on the right to select a bucket. In this example, the bucket in Guangzhou region set in step 2 is selected (mapping a bucket as a drive).
 - **Mapped drive letter**: Set the drive letter of the mapped drive, which cannot conflict with existing drive letters.
5. Click **Add new drive**.
6. Find the drive in **This PC**. If you want to map all buckets to the Windows server, repeat the steps above.



