## Introduction
You can upload objects to a bucket on the **File List** page in the COS Console. For more information on objects, see [Object Overview]((https://intl.cloud.tencent.com/document/product/436/13324)).
##  Prerequisites
Before uploading an object, please make sure that you have created a bucket. If no bucket has been created, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions
#### 1. Entering the file list
 Log in to the [COS Console](https://console.cloud.tencent.com/cos5). Click **Bucket List**, select the bucket to which you want to upload the objects, and you will be taken to the bucket's **File List** page. Click **Upload Files** and you will see the **Upload Files** window as shown below.
![](https://main.qcloudimg.com/raw/1f499717168f5559337899f635e19a13.png)


#### 2. Selecting the object(s) to be uploaded
On the **Upload Files** page, click **Select Files** or **Select Folders** to upload a single or multiple local files/folders. After selecting the objects to be uploaded, click **Upload**, or click **Next** to set the object attributes before the upload (see Step 3).
![](https://main.qcloudimg.com/raw/8489d2bae2ba778bac87386093cd51e7.png)

#### 3. Setting object attributes (optional)
Set the storage class, access permissions, server-side encryption and metadata (optional) for the files to be uploaded, and then click **Upload**. The configuration items are described as follows:
- Storage Class
You can set different storage classes for different objects in different scenarios. The default storage class is Standard Storage. For more information on storage classes, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/6222)。
- Access Permissions
You can set different access permissions for different objects as needed. The default is "Inherit Permissions", i.e. inheriting permissions from the bucket. For more information on access permissions, see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).
- Server-side Encryption
You can configure server-side encryption for the objects you want to upload. Tencent Cloud COS will apply data encryption protection to the uploaded objects. The objects will be automatically encrypted before they are written, and automatically decrypted when you access them. Tencent Cloud COS supports AES-256 encryption with the master key. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
- Metadata
The object metadata, or HTTP Header, is a string sent by the server before it sends HTML data to the browser with the HTTP protocol. By modifying the HTTP Header, you can change how the page responds or communicate configuration information, such as modifying the cache time. Modifying an object's HTTP Header does not modify the object itself. For more information, see [Custom Object Headers](https://intl.cloud.tencent.com/document/product/436/13361).
After an object is uploaded successfully, the system automatically refreshes the list to get the latest object information as shown below.
![](https://main.qcloudimg.com/raw/5a60ce06d3d2831b289a7c26294423cc.png)

> Some browsers do not support uploading multiple files. It is recommended to use mainstream browsers such as IE10 or above, Firefox, or Chrome.

#### 4. Verifying the completion of the upload
After clicking **Upload**, you can check the upload progress in **Task Completed** in the top right of the page. After the upload is complete, you can see the uploaded object in the **File List** page of the bucket.
![](https://main.qcloudimg.com/raw/eab5784b108fc096dbe317fed25f7925.png)

> The task progress in the figure indicates the number of tasks created by the current operation. For example, if you upload 10 files in a single operation and all are successfully uploaded, the task progress will display "1 succeeded, 0 failed, and 0 suspended".
