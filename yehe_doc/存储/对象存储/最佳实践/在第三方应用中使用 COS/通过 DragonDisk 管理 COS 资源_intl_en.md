## Overview

DragonDisk is a free file manager with a GUI similar to Windows File Explorer and supports data backup and sharing. You can use it to easily and quickly manage files in COS.

## Supported Systems

Windows, macOS, and various Linux distributions.

## Download Address

Go to the [DragonDisk Download](http://download.dragondisk.com/download-s3-compatible-cloud-client.html) page and download it.


## Installation and Configuration

>!The following configuration process takes DragonDisk Windows v1.05 as an example. Note that the configuration process may vary by version.
>

1. Double-click the installation package and complete the installation as prompted.
2. Open the tool, select **File** > **Accounts**, and click **New** in the pop-up window to add the account configuration information.
3. Configure the following information in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/a8d83b57beafd32f916e7d530dd46416.png)
The configuration items are described as follows:
 - Provider: Select **Other S3 compatible service**.
 - Service Endpoint: The format is `cos.<Region>.myqcloud.com`; for example, to access a bucket in Chengdu region, enter `cos.ap-chengdu.myqcloud.com`. For applicable region abbreviations, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
 - Account name: Enter a custom username.
 - Access key: Enter the access key SecretId. You can go to the [API Keys](https://console.cloud.tencent.com/capi) page of the console to create and view access keys. |
 - Secret key: Enter the access key SecretKey. You can go to the [API Keys](https://console.cloud.tencent.com/capi) page of the console to create and view access keys. |
4. After adding the account information, select the configured username in **Root** to view the list of buckets under the username. At this point, the configuration is completed.
![](https://qcloudimg.tencent-cloud.cn/raw/aa2cf3f681233d692d58ddcc7f16a833.png)

## Managing COS File

### Querying the bucket list

Select the configured username in **Root** to view the list of buckets under the username.

>! With this operation, you can only view the buckets in the region configured by the **Service Endpoint**. To view buckets in other regions, click **File** > **Accounts**, select a username, and change **Service Endpoint** to another region.
>



### Creating a bucket

1. Right-click the username and select **Create bucket**, and enter the full bucket name in the pop-up window such as `examplebucket-1250000000`.
![](https://qcloudimg.tencent-cloud.cn/raw/46fd8b1296908a39b2949b7895dd1a60.png)
2. After confirming that everything is correct, click **OK**.
For bucket naming conventions, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).

### Deleting a bucket

Right-click the target bucket in the bucket list and select **Delete bucket** in the context menu.


### Uploading an object

In the bucket list, select the destination bucket or path, select the object to be uploaded on the local computer, and drag and drop it to the bucket or path.


### Downloading an object

Find the target bucket in the bucket list and drag and drop the object to a folder on the local computer on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/45fcab5119da7ab87d958853e8b6100a.png)


### Copying an object

Right-click the target object in the left window, select **Copy**, right-click under the destination path, and select **Paste**.


### Renaming an object

Right-click the target object in the bucket, select **Rename**, and enter a new name.


### Deleting an object

Right-click the target object in the bucket and select **Delete**.

### Moving an object

Right-click the target object in the left window, select **Cut**, right-click under the destination path, and select **Paste**.


### Other features

In addition to the above features, DragonDisk also allows you to set object ACLs, view object metadata, customize headers, and get object URLs.







