If you are a first time user of Cloud Object Storage (COS) of Tencent Cloud, we recommend that you first read [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312), [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324), [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518), and [FAQs](https://intl.cloud.tencent.com/document/product/436/6282).

COSBrowser is a GUI-enabled tool provided by COS. Available on Windows, macOS, Linux, Android, and iOS, it provides an easier way to view, transfer, and manage COS resources.
This document uses the Windows version as an example to show you in detail how to create buckets, and upload, download, and share objects.


## Prerequisites

1. The COS service is activated for your Tencent Cloud account. If not, please go to [COS console](https://console.cloud.tencent.com/cos5) and follow the instructions to activate it.
2. You should log in to COSBrowser using an API key. First, go to the [API Key](https://console.cloud.tencent.com/cam/capi) management page to create one.


## Step 1. Download and install COSBrowser

<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe" target="_blank"  style="color: white; font-size:16px;">Click here to download COSBrowser</a></div><br>


System requirements of COSBrowser for Windows: Windows 7 32/64-bit or later or Windows Server 2008 R2 64-bit or later
For COSBrowser for other systems, download it from [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).



## Step 2. Log in to COSBrowser

Use your [API Key](https://console.cloud.tencent.com/cam/capi) to log in to COSBrowser.


## Step 3. Create a bucket

1. After you logged in, click **Create bucket** in the upper-left corner of the COSBrowser page.
2. Enter your bucket information in the pop-up window.
![](https://main.qcloudimg.com/raw/d5c11a8be17d9a3462c0ca73ee189c73.png)
 - Bucket Name: a user-defined bucket name, for example, `examplebucket`
 - Region: Region where the bucket resides. Select the region closest to you. For example, if you are in Shenzhen, you can select the Guangzhou region, i.e., `ap-guangzhou`.
 - ACL: access permission for the bucket. For example, you can select **Private (read-write)**.
 - **Bucket Tag** and **MAZ configuration** are optional. They are left blank in this example.
3. Click **OK**.


## Step 4. Upload an object

1. Click the bucket created in Step 3 to go to the bucket management page.
2. Click **Upload** > **Select files** and select a local file to upload to the bucket, for example, `exampleobjext.txt`.
3. Click **Upload**.


## Step 5. Download an object

#### Option 1


1. Click <img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;"> in the upper-right of the COSBrowser page to switch to list view (Skip this step if you are already in list view).
2. Under **Operation** on the right side, click <img src="https://main.qcloudimg.com/raw/0631f784902fb5e146ac0d0f6befe346.jpg"  style="margin:0;"> to download the file.


#### Option 2

1. Right-click a file, and in the drop-down list, click **Advanced Download**.
2. In the pop-up window, select **Rename**, **Replace**, or **Skip** as needed.
![](https://main.qcloudimg.com/raw/6e533ea1b75df3de7dba029a6976f844.png)
3. Click **Download now**. COSBrowser will start downloading the selected file.


## Step 6. Share an object

Each file stored in COS can be accessed through a specific link. If a file is private-read, you can request a temporary signature to generate a temporary access link with a certain validity period. The two methods for generating object links are as follows:

#### Option 1

1. Click <img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;"> in the upper-right of the COSBrowser page to switch to list view (Skip this step if you are already in list view).
2. In the action bar to the right of the file, click <img src="https://main.qcloudimg.com/raw/37acaeb370eb77e1bb0c792d542792e2.jpg"  style="margin:0;">.
3. Your link is generated and copied successfully if COSBrowser displays **Temporary object url copy success, link effective for 2 hours** at the top.
4. You can now access your file via this link. File links generated in this way are valid for 2 hours. To customize the validity period, you can use Method 2.


#### Option 2

1. Click <img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;"> in the upper-right of the COSBrowser page to switch to list view (Skip this step if you are already in list view).
2. Under **Actions** on the right side, click **...**, and in the drop-down list, click **Share**.
![](https://main.qcloudimg.com/raw/1ab8d2c4a61ae3e0b94c06c9d65ce3f7.png)
3. In the **Copy URL** pop-up window, configure your file URL. If your file is **Private read-write**, select **Signed URL, with validity**. Note that the URL is valid for the period of time you specify.
![](https://qcloudimg.tencent-cloud.cn/raw/be35af7fe2e1a4138ec75e2fa90e5343.png)
4. Click **Copy** to copy the temporary file URL, with which you can access your file.

## More

In addition to the above capabilities, COSBrowser has many more to offer, such as modifying bucket access permissions, file preview, etc. For more information, see [COSBrowser for Desktop](https://intl.cloud.tencent.com/document/product/436/11366#.E6.A1.8C.E9.9D.A2.E7.AB.AF.E5.8A.9F.E8.83.BD.E5.88.97.E8.A1.A8).

## Troubleshooting

If you have any questions, [contact us](https://intl.cloud.tencent.com/contact-sales).

## References

To learn more about iOS- or Android-powered COSBrowser, see the following documents:

- [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366)
- [User Guide for Mobile Version](https://intl.cloud.tencent.com/document/product/436/41616)

