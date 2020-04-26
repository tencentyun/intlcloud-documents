## Scenario

This document describes how to use the FTP service on a local Windows machine to upload files to a CVM.

## Prerequisites

[The FTP service](https://intl.cloud.tencent.com/document/product/213/10912) has been built on the CVM.

## Procedure

### Connecting to the CVM
1. Download and install FileZilla locally.
> If you use FileZilla 3.5.3 to upload files through FTP, the upload may fail. We recommend that you download FileZilla 3.5.1 or 3.5.2 from the official website.
>
2. Open FileZilla.
3. In the FileZilla window, complete the host, username, password, and port information, and click **Quickconnect**.
**Configuration description:**
 - Host: indicates the public IP address of the CVM. To view the public IP address of the CVM, log in to the [CVM console](https://console.cloud.tencent.com/cvm) and navigate to the instance management page.
 - Username: indicates the FTP user account configured when you [set up the FTP service](https://intl.cloud.tencent.com/document/product/213/10912). Here, "ftpuser1" is used as an example.
 - Password: indicates the password of the FTP user account configured when you [set up the FTP service](https://intl.cloud.tencent.com/document/product/213/10912).
 - Port: indicates the FTP listening port, which is port **21** by default.
After the connection is successfully established, you can view files on the remote CVM site.

### Uploading a file
In the "Local site" window in the lower-left corner, right-click the local file to be uploaded and choose **Upload** to upload it to the Linux CVM.
> 
>- The CVM FTP path does not support the automatic decompression or deletion of uploaded tar packages.
>- The remote site path is the default path for uploading files to the Linux CVM.
>


### Downloading a file
In the "Remote site" window in the lower-right corner, right-click the CVM file to be downloaded and choose **Download** to download it to a local directory.


