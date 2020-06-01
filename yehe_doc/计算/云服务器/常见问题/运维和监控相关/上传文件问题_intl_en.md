### Does a CVM go with FTP?
You may install and configure FTP as needed.
- To build FTP sites using the built-in FTP service of Windows, see [Building the FTP Service (Windows)](https://intl.cloud.tencent.com/document/product/213/10414).
- To build FTP sites using the vsftpd software, see [Building the FTP Service (Linux)](https://intl.cloud.tencent.com/document/product/213/10912).

### How do I upload files to a Windows CVM?
- For a local Windows, see [Uploading Files from Windows to a Windows CVM using MSTSC](https://intl.cloud.tencent.com/document/product/213/2761).
- For a local Linux, see [Uploading Files from Linux to a Windows CVM using RDP](https://intl.cloud.tencent.com/document/product/213/34822).
- For a local MacOS, see [Uploading Files from MacOS to a Windows CVM using MRD](https://intl.cloud.tencent.com/document/product/213/34820).

### How does a local host transfer data to and from a Windows CVM?
### To transfer data:
- Install QQ.exe and other tools on the local host and Windows CVM respectively.
- [Upload Files from Windows to a Windows CVM using MSTSC](https://intl.cloud.tencent.com/document/product/213/2761)
-[Build the FTP Service (Linux)](https://intl.cloud.tencent.com/document/product/213/10912) on the local host.

### How do I upload files to a Linux CVM using WinSCP?
For more information, see [Uploading Files via WinSCP to a Linux CVM from Windows](https://intl.cloud.tencent.com/document/product/213/2131).

### How do I upload files to or download files from a Linux CVM?
For more information, see [Uploading Files via SCP to a Linux CVM from Linux](https://intl.cloud.tencent.com/document/product/213/2133).

### What should I do for client-server connection timeout during file upload using FTP?
The server firewall or security group may block the connection. Troubleshoot the issues by:
1. Check for settings of the server firewall.
2. Disable the firewall or add rules.
