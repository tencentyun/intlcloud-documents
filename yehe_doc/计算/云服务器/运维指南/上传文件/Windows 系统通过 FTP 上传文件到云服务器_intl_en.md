## Scenario

This topic describes how to upload files from local Windows to a CVM using FTP services.

## Prerequisites

You have built the FTP service on CVM.
- To upload files to a Linux CVM using FTP, see [Building the FTP Service (Linux)](https://intl.cloud.tencent.com/document/product/213/10912)
- To upload files to a Windows CVM using FTP, see [Building the FTP Service (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)


## Directions

### Connecting CVM
1. Download and install FileZilla locally.
> If you use version 3.5.3 of FileZilla to upload files via FTP, the upload may fail. We recommend you download and use version 3.5.1 or 3.5.2 of FileZilla.
>
2. Open FileZilla.
3. In the FileZilla window, enter the host, username, password, and port information, and click **Quickconnect**.

**Configuration description:**
 - Host: public IP of the CVM. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm) to view the public IP of the CVM on the **Instances** page.
 - User name: FTP user account configured when you are [building the FTP service] (https://intl.cloud.tencent.com/document/product/213/10912). The figure below uses "ftpuser1" as an example.
 - Password: password corresponding to the FTP user account configured when you are [building the FTP service] (https://intl.cloud.tencent.com/document/product/213/10912).
 - Port: FTP listener port. Default value: 21.
If the connection is successful, you can view files on the CVM remote site.

### Uploading a file
In the lower-left "Local site" window, right-click the local file to be uploaded and select **Upload** to upload it to a Linux CVM, as shown below:
> 
>- CVM FTP path does not support automatic unzipping or deleting of uploaded tar zip files.
>- The remote site path is the default path for uploading files to Linux CVM.
>

### Downloading a file
In the lower-right "Remote site" window, right-click the CVM file to be downloaded and choose **Download** to download it to a local directory.


