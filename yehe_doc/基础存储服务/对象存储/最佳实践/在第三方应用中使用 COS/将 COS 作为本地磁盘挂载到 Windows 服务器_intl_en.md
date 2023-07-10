## Overview
COS can be used on Windows mainly with APIs, COSBrowser, or COSCMD.

However, users using Windows Server can only use COSBrowser as cloud storage, which is not friendly to run programs or perform operations. In this case, you can mount the cost-effective COS to Windows Server as local drive by reading this guide.

>? Examples given in this document apply only to Windows 7 or Windows Server 2012/2016/2019/2022.
>

## Directions
### Download and installation

Three types of software are involved in examples given in this document. You can install the software version that is compatible with your system.
1. Go to [GitHub](https://github.com/billziss-gh/winfsp/releases) to download WinFsp.
`winfsp-1.12.22301` is downloaded as an example. You can then install it with the default options.
>? For Windows Server 2012 R2, WinFsp 1.12.22242 is not compatible, but WinFsp 1.11.22176 is compatible.
2. Go to [Git](https://gitforwindows.org/) or [GitHub](https://github.com/git-for-windows/git/releases/) to download Git.
`Git-2.38.1-64-bit` is downloaded as an example. You can then install it with the default options.
3. Go to [Rclone](https://rclone.org/downloads/) or [GitHub](https://github.com/rclone/rclone/releases) to download Rclone.
`rclone-v1.60.1-windows-amd64` is downloaded as an example. Note that you only need to decompress it to any directory named in English (decompressing to a path containing Chinese characters might cause an error). In this example, the package is decompressed to the `E:\AutoRclone`.

>? If GitHub cannot be opened or offers a low download speed, you can find another way for the download.
>

### Rclone configuration

>!The following configuration process takes `rclone-v1.60.1-windows-amd64` as an example. Note that the configuration process may vary by version.


1. Open any folder, find **This PC** in the left navigation pane, right-click and select **Properties** > **Advanced system settings** > **Environment Variables** > **System variables** > Path**, and click **New**.
2. In the pop-up window, enter the path where Rclone is decompressed (E:\AutoRclone) and then click **OK**.
3. Open Windows PowerShell and run the `rclone --version` command to check whether Rclone is installed successfully.
4. If Rclone is installed successfully, run the `rclone config` command in Windows PowerShell.
5. In Windows PowerShell, enter **n** and then press **Enter** to create a New remote.
6. In Windows PowerShell, enter the name of the disk (for example, `myCOS`) and then press **Enter**.
7. From the options that are displayed, select the option containing `Tencent COS` (that is, enter **5**) and then press **Enter**.
![](https://qcloudimg.tencent-cloud.cn/raw/edd4b224879b2c854c9a32167d3f2aaa.png)
8. From the options that are displayed, select the option containing `TencentCOS` (that is, enter **21**) and then press **Enter**.
![](https://qcloudimg.tencent-cloud.cn/raw/c7ada8335827fff90078628f05927141.png)
9. When `env_auth>` is displayed, press **Enter**.
10. When `access_key_id>` is displayed, enter the `SecretId` of COS and then press **Enter**.
>? Using sub-account permissions is recommended. You can go to [Manage API Key](https://console.cloud.tencent.com/cam/capi) to view your `SecretId` and `SecretKey`.
>
11. When `secret_access_key>` is displayed, enter the `SecretKey` of COS and then press **Enter**.
12. Choose the region of the bucket according to the gateway addresses of the Tencent Cloud regions that are displayed.
The Guangzhou region is used as an example herein. Therefore, you can enter **4** (`cos.ap-guangzhou.myqcloud.com`) and then press **Enter**.
13. Select the object permission (such as `default` or `public-read`) as needed, which takes effect only for objects that are uploaded later. `default` is used as an example herein. Therefore, you can enter **1** and then press **Enter**.
![](https://qcloudimg.tencent-cloud.cn/raw/7756d7599713939368c6bb42cd075d07.png)
15. Select the storage class for your objects uploaded to COS. `Default` is used as an example herein. Therefore, you can enter **1** and then press **Enter**.
![](https://qcloudimg.tencent-cloud.cn/raw/48e7f6c7d65d13d9fdde690e819bad6c.png)
 - Default: default option
 - Standard storage class: STANDARD
 - Archive storage mode: ARCHIVE
 - Infrequent access storage mode: STANDARD_IA
>?To use the INTELLIGENT TIERING or DEEP ARCHIVE storage class, use the **modifying the configuration file** method and then set the value of `storage_class` to `INTELLIGENT_TIERING` or `DEEP_ARCHIVE`. For more information about the storage class, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925).
>
15. When `Edit advanced config? (y/n)` is displayed, press **Enter**.
16. After confirming the information, press **Enter**.
17. Enter **q** to complete the configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/9cd97c7d75b1b9cfd42a244c03d00fff.png)

### Modifying the configuration file

After the preceding configuration is complete, a configuration file named `rclone.conf` will be generated in the `C:\Users\Username\AppData\Roaming\rclone` directory. You can directly modify the file to update the Rclone configuration. If the file is not found, you can run the `rclone config file` command in the command line window to view the Rclone configuration file.


### Mounting COS as local drive

1. Open the installed Git Bash and enter the command in it. Two use cases are provided here for your choice as needed.
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
		<li>myCOS: Replace it with the user-defined disk name.</li>
		<li>Y: Replace it with the drive letter you want to assign to the drive. Ensure that it does not overlap with other drive letters.</li>
		<li>E:\temp: A local cache directory, which can be set as needed. Note that you have the permission for the directory.</li>
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
>? Use correct encoding when you create text files through PowerShell. Otherwise, the generated .bat and .vbs files cannot be executed.
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
>? Usually, the successful mounting prompt will be displayed tens of seconds after auto-mounting configuration is complete and the server is restarted.



## More

Using a third-party tool to mount COS to a Windows server as local drive is also available. The following shows the mounting procedure using the TntDrive tool:
1. Download and install TntDrive.
2. Open TntDrive and then click **Account** > **Add New Account** to create an account.
![](https://main.qcloudimg.com/raw/90b4a262b11b6933f48b4922cad4fdc4.png)
The main parameters are described as follows:
 - **Account Name**: user-defined account name
 - **Account Type**: account type. As COS is compatible with S3, you can select **Amazon S3 Compatible Storage**.
 - **REST Endpoint**: region of your bucket. For example, if your bucket resides in the Guangzhou region, set this parameter to `cos.ap-guangzhou.myqcloud.com`.
 - **Access Key ID**: the value of `SecretId`, which can be created/obtained at [Manage API Key](https://console.cloud.tencent.com/capi).
 - **Secret Access Key**: the value of `SecretKey`
3. Click **Add new account**.
4. In the TntDrive window, click **Add New Mapped Drive** to create a mapped drive.
![](https://main.qcloudimg.com/raw/fa09500f96ba8e5c8144d39cd5471991.png)
The main parameters are described as follows:
 - **Amazon S3 bucket**: path or name of the bucket. You can click the icon on the right to select a bucket. In this example, the bucket residing in the Guangzhou region that is set in step 2 is selected (mapping a bucket as a single network drive).
 - **Mapped drive letter**: drive letter of the mapped drive, which cannot overlap with existing drive letters
5. Click **Add new drive**.
6. Find the drive in **This PC**. If you want to map all buckets to the Windows server, repeat the steps above.




