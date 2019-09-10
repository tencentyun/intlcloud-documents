## Overview
You can upload objects on the **Objects** page of buckets via COS Console. For more information on objects, see [Object Overview](https://cloud.tencent.com/document/product/436/13324).

## Directions
### 1. Entering the objects
 Log in to the [COS Console](https://console.cloud.tencent.com/cos5). Click **Bucket List**, and select the bucket to store objects to enter the bucket's **Objects** page. Click **Upload Files** and the **Upload Files** window pops up as shown below.
![](https://main.qcloudimg.com/raw/33a7f9bdd6e5bcb307b1c3d8a9eaa927.png)

### 2. Selecting the Object(s) to Upload
On the **Upload Files** page, click **Select Files** or **Select Folders** to upload a single or multiple local files/folders. After selecting the objects to upload locally, click **Upload** to upload the objects, or click **Next** to set the object attributes before upload (see Step 3).
![](https://main.qcloudimg.com/raw/8489d2bae2ba778bac87386093cd51e7.png)

### 3. Setting Object Attributes (Optional)
Set the storage class, access permissions, server-side encryption and metadata (optional) for the files to upload, and then click **Upload**. The configuration items are described as follows:
- Storage Class
You can set a storage class for each object based on the use case. The default storage class is COS Standard. For more information on storage classes, see [Storage Classes](https://cloud.tencent.com/document/product/436/6222#.E5.AF.B9.E8.B1.A1.E5.AD.98.E5.82.A8.E7.B1.BB.E5.9E.8B).
- Access Permissions
You can set access permissions for each object as needed. Default is "Inherit Permissions" (inherit permissions from bucket). For more information on access permissions, see [Basic Concepts of Access Control](https://cloud.tencent.com/document/product/436/30749).
- Server-side Encryption
You can configure server-side encryption for the objects you want to upload. Tencent Cloud COS will apply data encryption protection to the uploaded objects, so as to automatically encrypt data before it is written, and automatically decrypt the data when you access it. Tencent Cloud COS supports AES-256 encryption of data using the master key. For more information, see [Server-side Encryption Overview](https://cloud.tencent.com/document/product/436/18145).
- Metadata
The object metadata, or HTTP Header, is a string sent by the server over HTTP protocol before it sends HTML data to browser. By modifying the HTTP Header, you can change the response form of the page or communicate configuration information, such as modifying the caching time. Modifying an object's HTTP Header does not modify the object itself. For more information, see [Custom Object Headers](https://cloud.tencent.com/document/product/436/13361).
After an object is uploaded successfully, the system automatically refreshes the list to get the latest object information, as shown below.
![](https://main.qcloudimg.com/raw/5a60ce06d3d2831b289a7c26294423cc.png)

>Some browsers do not support uploading multiple files. It is recommended to use mainstream browsers such as IE10 or above, Firefox, or Chrome.

### 4. Verifying the Completion of Upload
After clicking **Upload**, you can check the upload progress in **Task completed** in the top right of the page. After the upload is completed, you can see the uploaded object in the **Objects**page of the bucket.
![](https://main.qcloudimg.com/raw/b8c944667a6e0ab7113cc6b2ade26887.png)
