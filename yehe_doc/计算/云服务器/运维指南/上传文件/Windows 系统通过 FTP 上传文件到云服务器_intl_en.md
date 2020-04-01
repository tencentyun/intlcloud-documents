## Scenario

This document describes how to upload files from the local server to CVM via FTP.

## Prerequisites

[Build the FTP Service](https://intl.cloud.tencent.com/document/product/213/10414) on CVM.

## Directions

### Connecting CVM
1. Download and install FileZilla locally.
> If you use version 3.5.3 of FileZilla to upload files via FTP, the upload may fail. We recommend you download and use version 3.5.1 or 3.5.2 of FileZilla.
>
2. Open FileZilla.
3. In the FileZilla window, enter host, user name, password, and port information, and click **Quickconnect**
**Configuration description:**
 - Host: Public IP of the CVM. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm) to view the public IP of the CVM on the instance management page.
 - User name: FTP user account configured when you [build the FTP service](https://intl.cloud.tencent.com/document/product/213/10912). The figure below uses "ftpuser1" as an example.
 - Password: Password corresponding to the FTP user account configured when you [build the FTP service](https://intl.cloud.tencent.com/document/product/213/10912).
 - Port: FTP listener port, which is "21" by default.
If the connection is successful, you can view files on the CVM remote site.

### Uploading a file
In the "Local site" window at the bottom left, right-click the local file to be uploaded and select **Upload** to upload it to Linux CVM, as shown below:
> 
>- CVM FTP path does not support automatic unzipping or deleting of uploaded tar zip files.
>- The remote site path is the default path for uploading files to Linux CVM.
>

### Downloading a file
In the "Remote site" window at the bottom right, right-click the CVM file to be downloaded and select **Download** to download it to your local computer.


