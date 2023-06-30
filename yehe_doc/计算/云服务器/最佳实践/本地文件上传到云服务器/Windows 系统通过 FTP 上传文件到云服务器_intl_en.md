## Overview

This document describes how to use the FTP service to upload files from a local Windows computer to a CVM.

## Prerequisites

You have built the FTP service on CVM.
- To use FTP to upload files to a Linux CVM, see [Building the FTP Service (Linux)](https://intl.cloud.tencent.com/document/product/213/10912)
- To use FTP to upload files to a Windows CVM, see [Building the FTP Service (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)


## Directions

### Connecting to the CVM
1. Download and install the open-source FileZilla locally.
<dx-alertinfotype="explain"title="">
If you use version 3.5.3 of FileZilla to upload files via FTP, the upload may fail. We recommend you download and use versions 3.5.1 or 3.5.2 of FileZilla from its official website.
</dx-alert>
2. Open FileZilla.
3. In the FileZilla window, enter information such as the host, username, password, and port, and click **Quickconnect**.

**Configuration description:**
 - Host: the public IP of the CVM. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm) to view the public IP of the CVM on the **Instances** page.
 - Username: the FTP user account configured when you [built the FTP service](https://intl.cloud.tencent.com/document/product/213/10912). The figure below uses "ftpuser1" as an example.
 - Password: the password corresponding to the FTP user account configured when you [built the FTP service](https://intl.cloud.tencent.com/document/product/213/10912).
 - Port: the FTP listening port, which is **21** by default.
After the connection is successful, you can view the files on the remote CVM site.

### Uploading a file
In the lower-left "Local site" window, right-click the local file to be uploaded and select **Upload** to upload it to a Linux CVM, as shown below:
<dx-alertinfotype="explain"title="">
- CVM FTP path does not support the automatic decompression or deletion of uploaded compressed tar files.
- The remote site path is the default path for uploading files to a Linux CVM.
</dx-alert>

### Downloading a file
In the lower-right "Remote site" window, right-click the CVM file to be downloaded and choose **Download** to download it to a local directory.


