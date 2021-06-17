### What is COSBrowser?

COSBrowser is a visual interface tool launched by Tencent Cloud to make it easier and simpler for you to view, transfer, manage, and interact with COS resources. Currently, it is available for desktop (Windows, macOS, Linux) and mobile clients (Android, iOS). For more information, please see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).


### How do I download COSBrowser?

For the download URL and instructions, please see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).

### What should I do if I cannot launch the COSBrowser client by double-clicking the CentOS GUI?

You can run the `./cosbrowser.AppImage --no-sandbox` command in the terminal to launch COSBrowser.


### Why can’t I find the storage path when I log in to COSBrowser with a sub-account?

1. Please make sure the sub-account has permission to access COS. For more information, please see [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).
2. If the sub-account only has permission to access a specified bucket or a specified directory under a bucket, you need log in to COSBrowser and manually add a storage path in "Bucket" or "Bucket/Object-prefix" format (for example, `examplebucket-1250000000`), and select the region where the bucket should reside.
![](https://main.qcloudimg.com/raw/bf6b59f824af9413fbe83bb8968f926d.png)


### How do I transfer a large number of files at a greater speed?

Take Windows COSBrowser as an example. You can navigate to **Advanced Settings**, and configure a greater number of concurrent files and parts under **Upload** and **Download**.
![](https://main.qcloudimg.com/raw/d74eae3fb53dce13fee5c6b6e517e526.png)


### What should I do if the message "Update failed due to permission denied" is prompted when I use a COSBrowser client that runs macOS?
![](https://main.qcloudimg.com/raw/b07cd00819c3f27b05ac361ed561c52a.png)

**Cause**
The above issue may occur when the two files `com.tencent.cosbrowser` and `com.tencent.cosbrowser.ShipIt` under the `/Users/username/Library/Caches/` directory belong to a root account and a user account, respectively. The resulting permission issue can cause update failure. 

##Solution##
Run the following command on your Mac device:
```plaintext
sudo chown $USER ~/Library/Caches/com.tencent.cosbrowser.ShipIt/
```

### What should I do if the message "no such file or directory, stat 'C:\Users\XXX\AppData\Local\Temp\cosbrowser\logs\cosbrowser.log'" is prompted and COSBrowser cannot be used?

![](https://main.qcloudimg.com/raw/42629a0686b7a892fef8946e547c9ef6.png)

**Solution**: We recommend that you download Version 2.1.x or later.

### What should I do if the installation of cosbrowser.exe is aborted automatically?

**Cause**
This problem occurs when COSBrowser has been installed before, and its traces have not been removed from your system after manual deletion. Therefore, when you reinstall it, the installer aborts the installation as it identifies existing traces but no actual application.

##Solution##
Manually remove the traces left after the previous installation of COSBrowser, or use a cleaner tool (such as the Software Management tool provided by Tencent PC Manager).

