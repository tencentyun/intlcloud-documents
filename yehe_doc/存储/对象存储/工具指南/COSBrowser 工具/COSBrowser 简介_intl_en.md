COSBrowser is a visualization interface tool provided by Tencent Cloud COS. You can use it to view, transfer, and manage COS resources easily. Currently, it is available for desktop and mobile clients as described below. If you need to migrate or batch upload data, you can use [Migration Service Platform (MSP)](https://www.tencentcloud.com/products/msp).

- [User Guide for Desktop Version](https://intl.cloud.tencent.com/document/product/436/32565)
- [Mobile Version Features](https://intl.cloud.tencent.com/document/product/436/41616)

## Download Address

<table>
   <tr>
      <th>COSBrowser Version</td>
      <th>OS</td>
      <th>System Requirements</td>
      <th>Download Address</td>
   </tr>
   <tr>
      <td rowspan=3>Desktop</td>
      <td>Windows</td>
      <td>Windows 7 32/64-bit or later, Windows Server 2008 R2 64-bit or later</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe">Windows</a></td>
   </tr>
   <tr>
      <td>macOS</td>
      <td>macOS 10.13 or later</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.dmg">macOS</a></td>
   </tr>
   <tr>
      <td>Linux</td>
      <td>Distributions with a GUI that supports the <a href="https://appimage.org">AppImage</a> format<br>
          Note: To launch the client on CentOS, you need to run <code>./cosbrowser.AppImage --no-sandbox</code> in the terminal.</td> 
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest-linux.zip">Linux</a></td>
   </tr>
   <tr>
      <td>Mobile</td>
      <td>Android</td>
      <td>Android 4.4 or later</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.apk">Android</a></td>
   </tr>
   <tr>
      <td>Web</td>
      <td>Web</td>
      <td>Browsers such as Chrome, Firefox, Safari, and Internet Explorer 10+</td>
      <td><a href="https://cosbrowser.cloud.tencent.com/web">Web</a></td>
   </tr>
   <tr>
      <td>Uploader plugin</td>
      <td>Web</td>
      <td>Chrome</td>
      <td><a href="https://chrome.google.com/webstore/detail/cosbrowser-uploader/mggpkimgmmdbdbakdkaebhjhgomcmlnd">Chrome Web Store</a>/<a href="https://cos5.cloud.tencent.com/cosbrowser/latest-chrome.zip">Download</a></td>
   </tr>
</table>

## Desktop Version Features

COSBrowser Desktop Version focuses on resource management and batch data upload/download.

> !COSBrowser Desktop Version uses the system-configured proxy to connect to the internet. Make sure that your proxy is set up properly, or you can disable the proxy configuration if it fails to connect to the internet.
>
> - For queries on Windows, go to **Internet Options**.
> - For queries on macOS, go to **Network Preferences**.
> - For queries on Linux, go to **System Settings** > **Network** > **Network Proxy**.

COSBrowser Desktop Version has the following features:

| Feature | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Creating/Deleting buckets](https://intl.cloud.tencent.com/document/product/436/32565#createordelete) | Creates or deletes buckets |
| [Viewing bucket details](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | Views the basic information of a bucket |
| [Viewing statistics](https://intl.cloud.tencent.com/document/product/436/32565#count)           | Views the current storage capacity and number of objects in a bucket                         |
| [Managing permissions](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket)                               | Modifies the permissions on buckets and objects                                 |
| [Setting versioning](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket)                                     | Enables/Suspends bucket versioning                                 |
| [Adding access paths](https://intl.cloud.tencent.com/document/product/436/32565#addaccess)                                     | Adds access paths                                             |
| [Uploading files/folders](https://intl.cloud.tencent.com/document/product/436/32565#upload) | Uploads files/folders to a bucket separately, in batches, or incrementally. <br><br>Note: <br>1. Up to 100,000 files can be batch uploaded in one request. <br>2. Checkpoint restart is not supported. <br>3. To migrate or batch upload data, use [Migration Service Platform (MSP)](https://www.tencentcloud.com/products/msp).     |
| [Downloading files/folders](https://intl.cloud.tencent.com/document/product/436/32565#download) | Downloads files/folders to the local file system separately, in batches, or incrementally. <br><br>Note: <br>1. Up to 100,000 files can be batch downloaded in one request. <br>2. Checkpoint restart is not supported.     |
| [Deleting files/folders](https://intl.cloud.tencent.com/document/product/436/32565#delete) | Deletes files/folders from a bucket separately or in batches |
| [Syncing files](https://intl.cloud.tencent.com/document/product/436/32565#synchronization)            |                                                     Synchronizes local files to a bucket in real time                  |
| [Copying and pasting files](https://intl.cloud.tencent.com/document/product/436/32565#copy) | Copies files/folders separately or in batches from one directory to another |
| [Renaming files](https://intl.cloud.tencent.com/document/product/436/32565#rename) | Renames files in a bucket |
| [Creating folders](https://intl.cloud.tencent.com/document/product/436/32565#newfolder) | Creates folders in a bucket |
| [Viewing file details](https://intl.cloud.tencent.com/document/product/436/32565#view) | Views the basic information of files in a bucket |
| [Generating file links](https://intl.cloud.tencent.com/document/product/436/32565#generatelinks) | Generates file access links with a certain validity period by requesting a temporary signature |
| [Sharing files/folders](https://intl.cloud.tencent.com/document/product/436/32565#share) | Shares files/folders and sets the validity period for sharing         |
| [Exporting file URLs](https://intl.cloud.tencent.com/document/product/436/32565#export) | Exports file URLs in batches         |
| [Previewing files](https://intl.cloud.tencent.com/document/product/436/32565#preview) | Previews media files (image, video, or audio) in a bucket |
| [Searching for files](https://intl.cloud.tencent.com/document/product/436/32565#searchfile) | Searches for files in a bucket through prefix search |
| [Searching for buckets](https://intl.cloud.tencent.com/document/product/436/32565#searchbuckete) | Searches for created buckets |
| [Viewing file versions/incomplete multipart uploads](https://intl.cloud.tencent.com/document/product/436/32565#viewfiles) |  <li>Views multiple versions of a file in a versioning-enabled bucket<br><li>Views incomplete multipart uploads in a bucket  |
| [Comparing files](https://intl.cloud.tencent.com/document/product/436/32565#compare) |     Compares files in a local folder to those in a bucket            |
| [Transcoding videos](https://intl.cloud.tencent.com/document/product/436/32565#transcoding)   |  Transcodes videos in a bucket with the media processing feature enabled    |
|  [Generating authorization codes](https://intl.cloud.tencent.com/document/product/436/32565#authorization)   |   Generates authorization codes for logging in to the COSBrowser client   |
|  [Processing images](https://intl.cloud.tencent.com/document/product/436/32565#processing)  |  Scales, crops, or rotates images, adds text or image watermarks, and generates URLs of output images   |
| [Setting up a proxy](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets up a proxy for COS access |
| [Setting the number of concurrent uploads/downloads](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of concurrent transfers for file upload or download |
| [Setting the number of concurrent parts to be uploaded/downloaded](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of parts for multipart upload or download |
| [Setting the number of retries upon upload/download failure](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of retries upon upload or download failure |
| [Limiting the single-thread upload/download speed](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Limits the upload/download speed for a single thread |
| [Setting upload check](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Double-checks files uploaded to a bucket |
| [Viewing local logs](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Saves records of operations on COSBrowser in the form of local logs |

## Mobile Version Features

COSBrowser Mobile Version is mainly used to monitor COS resources (such as storage usage and traffic) at any time you want. For more supported features, see [Mobile Version Features](https://intl.cloud.tencent.com/document/product/436/41616).

## Changelog

- Desktop Version: [Changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md).
- Mobile Version: [Changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md).

## Feedback and Suggestions

If you have any questions or suggestions when using COSBrowser, feel free to give us your feedback:

- Desktop Version: [Issues](https://github.com/tencentyun/cosbrowser/issues).
- Mobile Version: [Issues_mobile](https://support.qq.com/embed/phone/67467).
  
   
