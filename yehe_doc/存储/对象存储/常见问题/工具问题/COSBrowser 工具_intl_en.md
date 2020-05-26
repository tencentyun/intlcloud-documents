### What is COSBrowser?

COSBrowser is a visual interface tool that Tencent Cloud COS released to make it easier for you to view, transfer and manage COS resources with simpler interactions. Currently, it is available for desktops (Windows, macOS, Linux), and mobile clients (Android, iOS). For more information, see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).


### How to download COSBrowser?

For the download URL and instructions, see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).


### Why can’t I find the storage path when I log in to COSBrowser with a sub-account?

1. Please make sure the sub-account has the permission to access COS. See [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).
2. If the sub-account only has the permission to access a specified bucket or a specified directory under a bucket, then you need to manually add a storage path (format: “Bucket” or “Bucket/Object-prefix”, e.g. `examplebucket-1250000000`), and select the region where the bucket should reside when you log in.
![](https://main.qcloudimg.com/raw/bf6b59f824af9413fbe83bb8968f926d.png)


### How can I transfer a massive number of files faster?

Take Windows COSBrowser as an example. You can do so by navigating to **Advanced Settings**, and configuring a greater number of concurrent files and parts for **Upload** and **Download**.
![img](https://main.qcloudimg.com/raw/d74eae3fb53dce13fee5c6b6e517e526.png)


### What should I do if I am prompted that “Update failed. Permission is denied.” using macOS-based COSBrowser?
![](https://main.qcloudimg.com/raw/b07cd00819c3f27b05ac361ed561c52a.png)

**Cause**
The above issue may occur when the two files `com.tencent.cosbrowser` and `com.tencent.cosbrowser.ShipIt` under `/Users/username/Library/Caches/` belong to a root account and a user account, respectively.

##Solution##
Run the following command in your Mac device:
```plaintext
sudo chown $USER ~/Library/Caches/com.tencent.cosbrowser.ShipIt/
```

### What should I do if I am prompted that “no such file or directory, stat 'C:\Users\XXX\AppData\Local\Temp\cosbrowser\logs\cosbrowser.log'”, and cannot use the tool?

![](https://main.qcloudimg.com/raw/eb8bb8881c69849e782cea5611c9c1ce.png)

**Solution**: we recommend that you download Version 2.1.x or a later version.

### What should I do if the installation of cosbrowser.exe is aborted automatically?

**Cause**
This is because that COSBrowser has been installed before, and its traces have not been removed from your system when you deleted it manually. Therefore, when you reinstall it, the installer aborts the installation as it identifies the existing useless application with traces.

##Solution##
Manually remove the traces when you installed COSBrowser, or do so by using a cleaner tool (such as the Software Management tool provided by Tencent PC Manager).

