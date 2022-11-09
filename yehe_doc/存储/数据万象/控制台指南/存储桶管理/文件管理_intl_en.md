## Overview

CI's storage feature is based on COS, which uses buckets to store objects.

On the file management page, you can view the list of files in the bucket and [upload](#1), [download, delete](#2), and [search for](#3) files.

## Prerequisites

1. Log in to the [CI Console](https://console.cloud.tencent.com/ci) and click **Bucket Management** on the left sidebar to enter the bucket management page.
2. Click the name of the target bucket or **Manage** in the "Operation" column on the right to enter the bucket page.

<span id=1>

## Uploading File

1. On the file management page, click **Upload Files**. In the pop-up dialog box, click **Select Files** and select a local file for upload.
   If workflow is enabled, the uploaded video file will automatically trigger the workflow, and applicable feature fees will be incurred. You can click the drop-down list to view all the workflows enabled under this path. For more information on workflow, please see [Setting Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).
2. Click **OK**. If the information of the uploaded video is displayed in the resource list, the upload is successful.
>!
>
>- A single file of up to 512 GB in size can be uploaded in the console. If you need to upload bigger files, please use the [multipart upload](https://intl.cloud.tencent.com/document/product/436/14112) feature of COS.
>- If you upload a file that has the same name as an existing file in the bucket, the existing file will be overwritten.

<span id=2>

## Downloading and Deleting File

After a file is uploaded, you can download or delete it in the "Operation" column on the right. In addition, you can view its information, such as attributes, URL, and size.

<span id=3>

## Searching for File

You can enter a **filename prefix** in the search box in the top-right corner on the page to search for files.

 
