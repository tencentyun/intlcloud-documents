## Overview
COS can be used on Windows mainly with APIs, COSBrowser, or COSCMD.

However, users using Windows Server can only use COSBrowser as cloud storage, which is not friendly to run programs or perform operations. In this case, you can mount the cost-effective COS to Windows Server as local drive by reading this guide.

>? Examples given in this document apply only to Windows 7 or Windows Server 2012 and later.
>

## Directions
### Download and installation

The following installation procedure is for your reference. You can perform the installation according to your OS:
- Go to [GitHub](https://github.com/billziss-gh/winfsp/releases) to download Winfsp.
You can then install it with the default options.
- Go to [Git](https://gitforwindows.org/) or [GitHub](https://github.com/git-for-windows/git/releases/) to download Git.
`Git-2.31.1-64-bit.exe` is downloaded as an example. You can then install it with the default options.
- Go to [Rclone](https://rclone.org/downloads/) or [GitHub](https://github.com/rclone/rclone/releases) to download Rclone.
`rclone-v1.55.0-windows-amd64.zip` is downloaded as an example. Note that you only need to decompress it to any directory named in English (decompressing to a path containing Chinese characters might cause an error). In this example, the package is decompressed to the `E:\AutoRclone`.

>? If GitHub cannot be opened or offers a low download speed, you can find another way for the download.
>

### Rclone configuration

1. Right-click **This PC** and then select **Properties**. Then, click **Advanced system settings** > **Environment Variables** > **System variables** > **Path**. Then, click **New**.
2. In the pop-up window, enter the path where Rclone is decompressed (E:\AutoRclone) and then click **OK**.
3. Open Windows PowerShell and run the `rclone --version` command to see whether Rclone is installed successfully.
4. If Rclone is installed successfully, run the `rclone config` command in Windows PowerShell.
5. In Windows PowerShell, enter **n** and then press **Enter** to create a New remote.
6. In Windows PowerShell, enter the name of the disk (for example, `myCOS`) and then press **Enter**.
7. From the options that are displayed, enter **4** (the one that contains Tencent Cloud**) and then press **Enter**.
8. From the options that are displayed, enter **11** (the one that contains Tencent Cloud COS) and then press **Enter**.
9. When `env_auth>` is displayed, press **Enter**.
10. When `access_key_id>` is displayed, enter the `SecretId` of COS and then press **Enter**.
>? Using sub-account permissions is recommended. You can go to [Manage API Key](https://console.cloud.tencent.com/cam/capi) to view your `SecretId` and `SecretKey`.
>
11. When `secret_access_key>` is displayed, enter the `SecretKey` of COS and then press **Enter**.
12. Choose the region of the bucket according to the gateway addresses of the Tencent Cloud regions that are displayed.
The Guangzhou region is used as an example herein. Therefore, you can enter **4** (`cos.ap-guangzhou.myqcloud.com`) and then press **Enter**.
13. Select the object permission (`private` or `public-read`) as needed, which takes effect only for objects that are uploaded later. `public-read` is used as an example herein. Therefore, you can press **2** and then press **Enter**.
14. Select the storage class for your objects uploaded to COS. `Default` is used as an example herein. Therefore, you can press **1** and then press **Enter**.
 - Default: default option
 - Standard storage class: STANDARD
 - Infrequent access storage mode: Standard_IA
 - Archive storage mode: ARCHIVE
 >?To use the INTELLIGENT TIERING or DEEP ARCHIVE storage class, please use the **modifying the configuration file** method and then set the value of `storage_class` to `INTELLIGENT_TIERING` or `DEEP_ARCHIVE`.
15. When `Edit advanced config? (y/n)` is displayed, press **Enter**.
16. After confirming the information, press **Enter**.
17. Enter **q** to complete the configuration.


### Modifying the configuration file

After performing the configuration above, the Rclone configuration file, `vrclone.conf`, can be found in the `C:\Users\Username\.config\rclone` directory. You can directly modify the file to update the Rclone configuration.


### Mounting COS as local drive

1. Open the installed Git CMD and run one of the following commands as needed:
<ul>
<li>Mount COS as a shared drive on a LAN (recommended):
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &amp;</code>
</pre>
</li>
<li>Mount COS as local drive:
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &</code>
</pre>
	<ul>
		<li>myCOS: Replace it with the user-defined disk name.</li>
		<li>Y: Replace it with the drive letter you want to assign to the drive. Ensure that it does not overlap with other drive letters.</li>
		<li>E:\temp: local cache directory, which can be configured as needed</li>
	 </ul>
</li>
</ul>
If “The service rclone has been started” is displayed, the mount is successful.
2. Enter **exit** to close the terminal.
3. Find the myCOS(Y:) drive in **This PC**.
If you open this drive, you can see all buckets in the Guangzhou region. You can upload, download, create, delete files, and do more via the drive as needed.
>!
> - If any error is reported during the process, you can view the error messages from Git Bash.
> - If you delete a bucket from the drive, the bucket will be deleted, regardless of whether there are objects stored in the bucket or not.
> - If you change the name of a bucket from the drive, the bucket name in COS will also be changed.
> 


### Running the mounted drive automatically at startup

The mounted drive will disappear after the server is restarted. Therefore, you can perform the following operations to set the drive to auto-run at startup.

1. Create the `startup_rclone.vbs` and `startup_rclone.bat` files in the `E:\AutoRclone` directory.
2. In `startup_rclone.bat`, write the following mount command:
 - If COS is mounted as a shared drive on a LAN, run the following command:
```plaintext
rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &
```
 - If COS is mounted as a local drive, run the following command:
```
rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &
```
3. In `startup_rclone.vbs`, write the following code:
```plaintext
CreateObject("WScript.Shell").Run "cmd /c E:\AutoRclone\startup_rclone.bat",0
```
 >! Please replace the path with the actual one.
 >
4. Cut the `startup_rclone.vbs` file to the `%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup` directory.
5. Restart the server.

## Relevant Operations

Using a third-party tool to mount COS to a Windows server as local drive is also available. The following shows the mounting procedure using the TntDrive tool:
1. Download and install TntDrive.
2. Open TntDrive and then click **Account** > **Add New Account** to create an account.
![](https://main.qcloudimg.com/raw/90b4a262b11b6933f48b4922cad4fdc4.png)
Main parameters are described as follows:
 - **Account Name**: user-defined account name
 - **Account Type**: account type. As COS is compatible with S3, you can select **Amazon S3 Compatible Storage**.
 - **REST Endpoint**: region of your bucket. For example, if your bucket resides in the Guangzhou region, set this parameter to `cos.ap-guangzhou.myqcloud.com`.
 - **Access Key ID**: the value of `SecretId`, which can be created/obtained at [Manage API Key](https://console.cloud.tencent.com/capi).
 - **Secret Access Key**: the value of `SecretKey`
3. Click **Add new account**.
4. In the TntDrive window, click **Add New Mapped Drive** to create a mapped drive.
![](https://main.qcloudimg.com/raw/fa09500f96ba8e5c8144d39cd5471991.png)
Main parameters are described as follows:
 - **Amazon S3 bucket**: path or name of the bucket. You can click the icon on the right to select a bucket. In this example, the bucket residing in the Guangzhou region that is set in step 2 is selected (mapping a bucket as a single network drive).
 - **Mapped drive letter**: drive letter of the mapped drive, which cannot overlap with existing drive letters
5. Click **Add new drive**.
6. Find the drive in **This PC**. If you want to map all buckets to the Windows server, repeat the steps above.



