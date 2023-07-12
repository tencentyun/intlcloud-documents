## Download and Installation

#### Download

| OS | System Requirements | Download Address |
| :--------- | :-------------- | :----------------------------------------------------------- |
| Android | Above Android 4.4 | [Android](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.apk) |
| iOS | Above iOS 11 | iOS|

#### Software installation

COSBrowser Mobile Version is currently available in most app platforms such as MyApp and App Store. You can download it from the above download address or in an app platform.

<span id="dulu"></span>

## Login

COSBrowser Mobile Version supports the following three login methods:

- **Login with WeChat**: if your Tencent Cloud account was created through WeChat or associated with a specific WeChat account, you can use the WeChat account to quickly log in to COSBrowser.
- **Login with email**: if your Tencent Cloud account was created through email or associated with a specific email address, you can log in to COSBrowser by entering the email address and password.
- **Login with permanent key**: you can log in using your TencentCloud API key (SecretId and SecretKey; project key is not supported), which can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM console. After successful login, the account will be kept logged in permanently.

> ?
>
> - If your Tencent Cloud account was created with a QQ account, you can also use the login with WeChat method to log in just by selecting login with QQ on the redirected WeChat Mini Program screen.
>
> - If you use a sub-account, you can log in with key or WeChat. For login with WeChat, just select the sub-account on the redirected WeChat Mini Program screen.



## Basic Features

<span id="dateview"></span>

#### 1. Data overview

The data overview page displays your COS data usage in the past 30 days, including total traffic, total read and write requests, storage trend, traffic trends (for public network downstream traffic, private network traffic, and CDN origin-pull traffic), trend in the number of requests, trend in the ratio of effective requests, amount of STANDARD_IA data retrieved, and amount of ARCHIVE data retrieved.

<img src="https://main.qcloudimg.com/raw/43b03ec33e6a52184e9913f7db3f8d3a.png" style="zoom:100%;" />

<span id="filebatch"></span>

#### 2. Batch file operations

**Batch upload**

In the specified bucket or path, tap **+** in the upper-right corner, tap **Upload Files**, and select a file to upload it. You can upload multiple files in batches.

> !COSBrowser for iOS only allows you to upload files in the device album.

**Other batch operations**

COSBrowser allows you to download, delete, copy, or move multiple files in your bucket in batches by selecting the files using the **Select Multiple Files** button in the upper-right corner.

> !
> - COSBrowser for iOS allows you to save image and video files to the album.
> - No batch operations can be performed on folders for the time being.

<img src="https://main.qcloudimg.com/raw/677300a8276ce0db713dfe66d180b6ee.png" style="zoom:45%;" />

<span id="shareupload"></span>

#### 3. Share and upload

In a third-party app, you can copy the specified file to your bucket by selecting **Open in another app** > **COSBrowser**.

<img src="https://main.qcloudimg.com/raw/32b998eddcb135b9c351435ca8ab194e.png" style="zoom:85%;" />

<span id="rename"></span>

#### 4. Rename a file

To rename a file, tap **Operation** on the right of the file to be renamed, tap **Rename** in the pop-up box, enter the new file name, and tap **OK**.

> ?Folders cannot be renamed.

<span id="newfolder"></span>

#### 5. Create a folder

In the specified bucket or path, tap **+** in the top-right corner, tap **Create a Folder**, enter the folder name, and tap OK to create a folder.

> ?
> - The folder name can contain up to 255 digits, letters, and visible characters.
> - The folder name cannot contain special characters such as `\ / : * ? " | < >`.
> - `..` cannot be used as the folder name.
> - The folder cannot be renamed, so name it with caution.

<span id="view"></span>

#### 6. View file details

To view the details of a file, tap its filename. File details include its basic information, such as the object size, storage class, and object address, as well as its permission information.
<img src="https://main.qcloudimg.com/raw/34e5aa857508257a80119356abffce80.png" style="zoom:85%;" />

<span id="filepreview"></span>

#### 7. Preview a file

COSBrowser supports previewing media files, currently including images, videos, and audio. You can tap a filename, and enter the file details page to see the preview area above the details.

> !
> - Preview is available for images in most formats, .mp4 and .webm videos, and .mp3. and .wav audios.
> - Please note that file preview will incur downstream traffic.

<span id="generatelinks"></span>

#### 8. Generate a file link

Each file stored in COS can be accessed through a specific link. File links with a specified domain such as a CDN acceleration domain name can be generated. If a file is private-read, you can request a temporary signature to generate a temporary access link with a certain validity period.

You can generate file links in the following ways:

- Tap **Operation** on the right of the file and select **Copy Link** to generate a link and copy it. If the file is **public-read**, the link will not carry a signature and will be valid permanently. If the file is **private-read**, the link will carry a signature and be valid for 1 hour.
- In the file details, you can easily generate a link by changing the validity period and tapping *Generate a Link*.

> !If you log in with a temporary key, you cannot configure the validity period of the file link, which is 1 hour by default.

<span id="searchfile"></span>

#### 9. Search for a file

To search for a file, enter the filename in the search box at the top of the bucket. COSBrowser only supports prefix search.

<span id="searchbuckete"></span>

#### 10. Search for a bucket

To quickly locate a bucket, enter the bucket name in the search box above the bucket list. Fuzzy search is supported.

<span id="viewbucket"></span>

#### 11. View bucket details

To view the details of a bucket, tap **Operation** on the right of the bucket on the bucket list page and tap **Bucket Details**. Bucket details include bucket name, region, creation time, access domain name, and access permission.

- Basic Information: this includes bucket name, region, creation time, and access permission.
- Domain Information: you can view the domain names owned by the current bucket, which contains the endpoint by default. For more information on domain names, please see [Overview](https://intl.cloud.tencent.com/document/product/436/18424).

<span id="createbucket"></span>

#### 12. Create a bucket

To create a bucket, tap **Create Bucket** in the upper-right corner on the bucket list page and specify the name, region, and access permission.

<img src="https://main.qcloudimg.com/raw/2cfabcbe6c970ef295a05029e4c03b63.png" style="zoom:35%;" />


<span id="addaccess"></span>

#### 13. Add an access path

If you log in with a sub-account that has no access to the bucket list, you can add the specified path to a bucket or directory to manage resources by tapping **Add Access Path** in the upper-right corner of the bucket list page.

<img src="https://main.qcloudimg.com/raw/3a81c3a3f090a269b6152d154ea4f8e7.png" style="zoom:25%;" />

<span id="package"></span>


