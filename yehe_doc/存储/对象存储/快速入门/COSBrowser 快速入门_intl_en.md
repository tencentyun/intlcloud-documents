
COSBrowser is a visual interface tool launched by Tencent Cloud COS to make it easier and simpler for you to view, transfer, manage, and interact with COS resources. Currently, it is available for desktop and mobile clients. For more information, see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).

This document describes how to use COSBrowser to quickly create a bucket and upload, download, and share an object.


## Prerequisites

1. You have activated COS under your Tencent Cloud account.
>?
>- If you don't have a Tencent Cloud account, sign up as instructed in [About Account](https://www.tencentcloud.com/document/product/378).
>- If you haven't activated COS, go to the [COS console](https://console.cloud.tencent.com/cos5) and activate it as prompted.
2. If this is your first time using COS, we recommend you understand the following concepts first:
 - [Bucket](https://intl.cloud.tencent.com/document/product/436/13312): a carrier of objects, which can be considered as a "container" for storing objects. Each bucket can store an unlimited number of objects.
 - [Object](https://intl.cloud.tencent.com/document/product/436/13324): the basic unit of COS storage. It can be data in any format, such as images, documents, audio and video, and others.
 - [Region](https://intl.cloud.tencent.com/document/product/436/6224): a physical location where data centers are hosted on Tencent Cloud. COS data is stored in the buckets in these regions.


## Step 1. Download and install COSBrowser


1. Taking COSBrowser for Windows as an example, you can download it [here](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe).
2. After download, double-click the installation package for installation as prompted.


>?
>- System requirements of COSBrowser for Windows: Windows 7 32/64-bit or later or Windows Server 2008 R2 64-bit or later
>- You can download COSBrowser for other operating systems in [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).



## Step 2. Log in to COSBrowser

COSBrowser for Windows supports multiple login methods, including login via an API key, Tencent Cloud account, and shared link. Below takes a Tencent Cloud account as an example.


## Step 3. Create a bucket

1. After you logged in, click **Create bucket** in the upper-left corner of the COSBrowser page.
2. Enter your bucket information in the pop-up window.
![](https://main.qcloudimg.com/raw/d5c11a8be17d9a3462c0ca73ee189c73.png)
 - Bucket Name: a user-defined bucket name, for example, `examplebucket`
 - Region: Region where the bucket resides. Select the region closest to you. For example, if you are in Shenzhen, you can select the Guangzhou region, i.e., `ap-guangzhou`.
 - ACL: access permission for the bucket. For example, you can select **Private (read-write)**.
 - **Bucket Tag** and **MAZ configuration** are optional. They are left blank in this example.
3. Click **OK**. In the bucket list, you can view the created bucket.


## Step 4. Upload an object

1. Click the newly created bucket to enter the bucket management page.
2. Click **Upload** > **Select Files** and select a local file to upload to the bucket, for example, `exampleobject.txt`.
3. Click **Upload**.


## Step 5. Download an object

Right-click the target file and click **Download**.

## Step 6. Share an object

COSBrowser allows you to share a file via a URL or QR code. Below takes a URL as an example.

1. Select the target file and click <img src="https://main.qcloudimg.com/raw/37acaeb370eb77e1bb0c792d542792e2.jpg"  style="margin:0;"> on the right to quickly generate a sharing URL.
>?As the file inherits the private read/write permission of the bucket, the generated sharing URL is temporary and only valid for 2 hours.
2. Send the generated URL to the recipient. Then, the recipient can access the file online or download it.
>?
>By default, if the shared file can be directly opened in the browser, then accessing the temporary URL will directly preview the file online rather than downloading it.


## More

In addition to the above capabilities, COSBrowser has many more to offer, such as modifying bucket access permissions, file preview, etc. For more information, please see [COSBrowser for Desktop](https://intl.cloud.tencent.com/document/product/436/11366#.E6.A1.8C.E9.9D.A2.E7.AB.AF.E5.8A.9F.E8.83.BD.E5.88.97.E8.A1.A8).

## Troubleshooting

If you have any questions, see [COSBrowser](https://intl.cloud.tencent.com/document/product/436/35735) or [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.

## References

To learn more about iOS- or Android-powered COSBrowser, see the following documents:

- [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366)
- [User Guide for Mobile Version](https://intl.cloud.tencent.com/document/product/436/41616)
