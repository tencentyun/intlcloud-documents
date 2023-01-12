COSBrowser is a visualization interface tool provided by Tencent Cloud COS. You can use it to view, transfer, and manage COS resources easily. Currently, it is available for desktop and mobile clients as described below. If you need to migrate or batch upload data, you can use [Migration Service Platform (MSP)](https://www.tencentcloud.com/products/msp).

- [User Guide for Desktop Version](https://intl.cloud.tencent.com/document/product/436/32565)
- [User Guide for Mobile Version](https://intl.cloud.tencent.com/document/product/436/41616)

## Download Address

<table>
   <tr>
      <th>COSBrowser</td>
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
      <td>Includes a GUI that supports the <a href="https://appimage.org">AppImage</a> format<br>
          Note: To launch a client that runs CentOS, you need to run <code>./cosbrowser.AppImage --no-sandbox</code> in the terminal.</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest-linux.zip">Linux</a></td>
   </tr>
   <tr>
      <td rowspan=2>Mobile Version</td>
      <td>Android</td>
      <td>Android 4.4 or later</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.apk">Android</a></td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>iOS 11 or above</td>
      <td><a href="https://apps.apple.com/cn/app/id1469323992">iOS</a></td>
   </tr>
   <tr>
      <td>Web</td>
      <td>Web</td>
      <td>Browsers such as Chrome, Firefox, Safari, and Internet Explorer 10+</td>
      <td><a href="https://cosbrowser.cloud.tencent.com/web">Web</a></td>
   </tr>
   <tr>
      <td>Uploader Plugin</td>
      <td>Web</td>
      <td>Chrome browsers</td>
      <td><a href="https://chrome.google.com/webstore/detail/cosbrowser-uploader/mggpkimgmmdbdbakdkaebhjhgomcmlnd">Web Store</a>/<a href="https://cos5.cloud.tencent.com/cosbrowser/latest-chrome.zip">Offline Download</a></td>
   </tr>
</table>

## COSBrowser Desktop Version

COSBrowser Desktop Version focuses on resource management and uploading and downloading data in batches.

> !COSBrowser Desktop Version uses the system-configured proxy to connect to the internet. Make sure that your proxy is set up properly, or you can disable the proxy configuration if it fails to connect to the internet.
>
> - For queries on Windows, go to **Internet Options**.
> - For queries on macOS, go to **Network Preferences**.
> - For queries on Linux, go to **System Settings** > **Network** > **Network Proxy**.

COSBrowser Desktop Version has the following features:

| Feature | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Creating/Deleting a bucket](https://intl.cloud.tencent.com/document/product/436/32565#createordelete) | Creates or deletes a bucket |
| [Viewing bucket details](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | Views the basic information of your bucket |
| [Viewing statistics](https://intl.cloud.tencent.com/document/product/436/32565#count)           | Views the current storage capacity and number of objects in your bucket                         |
| [Permission management](https://intl.cloud.tencent.com/document/product/436/32565#acl)                               | Modifies the permissions on your buckets and objects                                 |
| [Setting versioning](https://intl.cloud.tencent.com/document/product/436/32565#version)                                     | Enables/Suspends bucket versioning                                 |
| [Adding an access path](https://intl.cloud.tencent.com/document/product/436/32565#addaccess)                                     | Adds an access path                                             |
| [Uploading files/folders](https://intl.cloud.tencent.com/document/product/436/32565#upload) | Uploads files/folders to a bucket separately, in batches, or incrementally. <br><br>Note: <br>1. Up to 100,000 files can be batch uploaded in one request. <br>2. Checkpoint restart is not supported. <br>3. To migrate or batch upload data, use [Migration Service Platform (MSP)](https://www.tencentcloud.com/products/msp).     |
| [Downloading a file/folder](https://intl.cloud.tencent.com/document/product/436/32565#download) | Downloads files/folders to the local file system separately, in batches, or incrementally <br><br>Note: <br>1. Up to 100,000 files can be batch uploaded in one request. <br>2. Checkpoint restart is not supported. |
| [Deleting a file/folder](https://intl.cloud.tencent.com/document/product/436/32565#delete) | Deletes files/folders from a bucket separately or in batches |
| [Synchronizing files](https://intl.cloud.tencent.com/document/product/436/32565#synchronization)            |                                                     Synchronizes local files to your bucket in real time                  |
| [Copying and pasting files](https://intl.cloud.tencent.com/document/product/436/32565#copy) | Copies files/folders separately or in batches from one directory to another |
| [Renaming files](https://intl.cloud.tencent.com/document/product/436/32565#rename) | Renames files in a bucket |
| [Creating a folder](https://intl.cloud.tencent.com/document/product/436/32565#newfolder) | Creates a folder in a bucket |
| [Viewing file details](https://intl.cloud.tencent.com/document/product/436/32565#view) | Views the basic information of the files in a bucket |
| [Generating a file link](https://intl.cloud.tencent.com/document/product/436/32565#generatelinks) | Generates a file access link with a certain validity period by requesting a temporary signature |
| [Sharing a file/folder](https://intl.cloud.tencent.com/document/product/436/32565#share) | Shares a file/folder and sets a validity period for the sharing         |
| [Exporting file URLs](https://intl.cloud.tencent.com/document/product/436/32565#export) | Exports file URLs in batches         |
| [Previewing a file](https://intl.cloud.tencent.com/document/product/436/32565#preview) | Previews media files (images, video, and audio) in your bucket |
| [Searching a file](https://intl.cloud.tencent.com/document/product/436/32565#searchfile) | Searches files in a bucket through prefix search |
| [Searching buckets](https://intl.cloud.tencent.com/document/product/436/32565#searchbuckete) | Searches existing buckets |
| [Viewing file versions/incomplete multipart uploads](https://intl.cloud.tencent.com/document/product/436/32565#viewfiles) |  <li>Views multiple versions of a file in a versioning-enabled bucket<br><li>Views the incomplete multipart uploads in your bucket  |
| [Comparing files](https://intl.cloud.tencent.com/document/product/436/32565#compare) |     Compares files in a local folder to those in a bucket            |
| [Transcoding a video](https://intl.cloud.tencent.com/document/product/436/32565#transcoding)   |  Transcodes videos with the media processing feature enabled in a bucket    |
|  [Generating an authorization code](https://intl.cloud.tencent.com/document/product/436/32565#authorization)   |   Generates an authorization code for logging in to the COSBrowser client   |
|  [Processing an image](https://intl.cloud.tencent.com/document/product/436/32565#processing)  |  Scales, crops, or rotates an image, or adds text or image watermarks, and generates a URL of the output image   |
| [Setting up a proxy](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets up a proxy to access COS |
| [Setting the number of concurrent uploads/downloads](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of concurrent transfers for file upload or download |
| [Setting the number of parts to upload/download](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of parts for multipart upload or download |
| [Setting the number of retries upon upload/download failure](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of retries upon upload or download failure |
| [Limiting single-thread upload/download speed](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Limits the upload and download speeds for a single thread |
| [Setting upload check](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Double-checks files uploaded to a bucket |
| [Viewing a local log](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Saves the record of operations on COSBrowser in the form of a local log |

## COSBrowser Mobile Version

The COSBrowser mobile version is mainly used to monitor COS resources (such as storage usage and traffic) at any time you want. For more supported features, see basic features in [User Guide for Mobile Version](https://intl.cloud.tencent.com/document/product/436/41616).

## Changelog

- Desktop Version changelog: [changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md).
- Mobile Version changelog: [changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md).

## Feedback and Suggestions

If you have any questions or suggestions during your use of COSBrowser, please feel free to give us your feedback:

- Feedback on Desktop Version: [issues](https://github.com/tencentyun/cosbrowser/issues).
- Feedback on Mobile Version: [issues_mobile](https://support.qq.com/embed/phone/67467).
  


