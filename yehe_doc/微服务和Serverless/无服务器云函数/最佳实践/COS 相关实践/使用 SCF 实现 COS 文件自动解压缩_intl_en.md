## Overview
This document describes how to use SCF to automatically decompress files in COS. COS is used to store uploaded .zip files and decompressed files, and SCF automatically decompresses .zip files uploaded to COS.


## Directions
### Creating bucket
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and select **Bucket List** on the left sidebar.
2. Click **Create Bucket** on the "Bucket List" page.
3. In the "Create Bucket" pop-up window, create a bucket.

The main parameter information is as follows. Keep the remaining parameters as default:
 - **Name**: enter a custom bucket name. This document uses `mubucket` as an example.
 - **Region**: select "Guangzhou".
 - **Access Permission**: select "Private Read/Write".
4. Click **OK**.


### Configuring decompression function
1. On the bucket management page, select **Function Service** on the left.
2. Click **Add Function** in "ZIP File Decompression Function". In the "Create ZIP File Decompression Function" window that pops up,
configure the following information.

 - **Function Name**: a function will be automatically created in the corresponding region. The function name uniquely identifies the function and cannot be modified after creation. You can view the function in the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Event Type**: an event refers to an operation that triggers a function. Taking an upload operation as an example, the upload operation may be performed by calling the `PUT Object` or `POST Object` API. When **Create using Put method** is selected as the event, only packages uploaded through the `PUT Object` API will trigger decompression.
> ! If your file is uploaded to the bucket by means of simple upload, multipart upload, or cross-region replication, we recommend you select the **File upload** event.
> 
 - **Trigger Condition**: it means that a function will be triggered when a package is uploaded to the specified path. If you select a specified prefix, the function will be triggered only when a package is uploaded to the path with the specified prefix. If you select the whole bucket, the function will be triggered when a package is uploaded to any location in the bucket.
> !If there is a containment relationship between the configured destination file prefix and the trigger condition, loop triggering may be caused, which should be avoided. For example, if the destination prefix is `prefix` and the trigger condition is `pre`, decompression will be triggered repeatedly when a `pref` package is uploaded.
> 
 - **Decompression Format**: the compression format that is currently supported. Only ZIP packages can be decompressed currently.
 - **Destination Bucket**: the bucket where the files will be stored after a package is decompressed.
 - **Destination File Prefix**: the specific path for storage of the files after a package is decompressed. If this parameter is not set, it will be the root directory of the bucket by default.
 - **SCF Authorization**: decompression requires you to authorize SCF to read the packages in your bucket and upload the decompressed files to the location you specify; therefore, you need to add this authorization.
3. After adding the configuration, select **Confirm**, and you will see that the function has been added.
You can select **View Log** to view the history of decompression. If an error occurs during decompression, you can quickly enter the SCF Console to view the error details by selecting **View Log**. If you need to delete a file decompression rule no longer used, select **Delete** to delete the relevant configuration.

### Testing function
1. On the bucket management page, select **File List** on the left.
2. On the file list page, click **Upload Files** and select a .zip file for upload.

3. Refresh the current bucket to check whether files are generated after decompression.
4. Switch to **Function Service** to view the log or enter the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) to view the execution result, and you will see the printed log information in **Execution Log**.
