COSBrowser is a visual tool launched by Tencent Cloud to help you easily view, transfer, and manage COS resources through simple interactions. Currently, COSBrowser is available in Desktop Version and Mobile Version. For more information, see:

- [User Guide for Desktop Version](https://intl.cloud.tencent.com/document/product/436/32565)
- [User Guide for Mobile Version](https://intl.cloud.tencent.com/document/product/436/32566)

## Download URL

<table>
   <tr>
      <th>COSBrowser</td>
      <th>OS</td>
      <th>System Requirements</td>
      <th>Download Address</td>
   </tr>
   <tr>
      <td rowspan="3">Desktop Version</td>
      <td>Windows</td>
      <td>Windows 7 32/64-bit or above, Windows Server 2008 R2 64-bit or above</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe">Windows</a></td>
   </tr>
   <tr>
      <td>macOS</td>
      <td>macOS 10.13 or above</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.dmg">macOS</a></td>
   </tr>
   <tr>
      <td>Linux</td>
      <td>Includes GUI which supports <a href="https://appimage.org">AppImage</a> format</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest-linux.zip">Linux</a></td>
   </tr>
   <tr>
      <td rowspan="2">Mobile Version</td>
      <td>Android</td>
      <td>Android 4.4 or above</td>
      <td><a href="https://sj.qq.com/myapp/detail.htm?apkName=com.qcloud.cos.client">Android</a></td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>iOS 11 or above</td>
      <td><a href="https://apps.apple.com/cn/app/id1469323992">iOS</a></td>
   </tr>
</table>

## COSBrowser Desktop Version

COSBrowser Desktop Version focuses on resource management and  upload and download data in batches.

>COSBrowser Desktop Version uses the system-configured proxy to connect to the internet. Please make sure that your proxy is set up properly or disable the proxy configuration if it fails to connect to the internet.
>
> - For queries on Windows, go to "Internet Options".
> - For queries on macOS, go to "Network Preferences".
> - For queries on Linux, go to System Settings > Network > Network Proxy.

COSBrowser Desktop Version has the following features:

| Feature | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Creating/Deleting bucket](https://intl.cloud.tencent.com/document/product/436/32565#createordelete) | Creates or deletes a bucket |
| [Viewing bucket details](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | Views the basic information of your bucket |
| [Viewing statistics](https://intl.cloud.tencent.com/document/product/436/32565#count)           | Views the current storage capacity and number of objects in your bucket                         |
| [Permission management](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket)                               | Modifies the permissions on your buckets and objects                                 |
| [Setting versioning](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket)                                     | Enable/Suspends bucket versioning                                 |
| [Adding access path](https://intl.cloud.tencent.com/document/product/436/32565#addaccess)                                     | Adds an access path                                             |
| [Uploading file/folder](https://intl.cloud.tencent.com/document/product/436/32565#upload) | Uploads files/folders to a bucket separately, in batches, or incrementally |
| [Downloading file/folder](https://intl.cloud.tencent.com/document/product/436/32565#download) | Downloads files/folders to the local file system separately, in batches, or incrementally |
| [Deleting file/folder](https://intl.cloud.tencent.com/document/product/436/32565#delete) | Deletes files/folders from a bucket separately or in batches |
| [Synchronizing file](https://intl.cloud.tencent.com/document/product/436/32565#synchronization)            |                                                     Synchronizes local files to your bucket in real time                  |
| [Copying and pasting file](https://intl.cloud.tencent.com/document/product/436/32565#copy) | Copies files/folders separately or in batches from one directory to another |
| [Renaming file](https://intl.cloud.tencent.com/document/product/436/32565#rename) |  Renames files in your bucket |
| [Creating folder](https://intl.cloud.tencent.com/document/product/436/32565#newfolder) | Creates folders in your bucket |
| [Viewing file details](https://intl.cloud.tencent.com/document/product/436/32565#view) | Views the basic information of files in your bucket |
| [Generating file link](https://intl.cloud.tencent.com/document/product/436/32565#generatelinks) | Generates a file access link with a validity period by requesting a temporary signature |
| [Previewing file](https://intl.cloud.tencent.com/document/product/436/32565#preview) |  Previews media files (images, video, and audio) in your bucket |
| [Searching for file](https://intl.cloud.tencent.com/document/product/436/32565#searchfile) | Searches for files in your bucket through prefix search |
| [Searching for bucket](https://intl.cloud.tencent.com/document/product/436/32565#searchbuckete) | Searches for existing buckets |
| [Viewing file versions/incomplete multipart uploads](https://intl.cloud.tencent.com/document/product/436/32565#viewfiles) |  <li>Views multiple versions of a file in a versioning-enabled bucket<br><li>Views the incomplete multipart uploads in your bucket  |
| [Setting up proxy](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets up a proxy to access COS |
| [Setting the number of concurrent transfers](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of concurrent transfers for file upload or download |
| [Setting the number of parts to be transferred](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of parts for multipart upload or download |
| [Setting the number of retries upon transfer failure](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of retries upon upload or download failure |
| [Setting upload check](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Double-checks files uploaded to a bucket |
| [Setting MD5 checksum calculation during upload](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Calculates MD5 checksums of files uploaded to a bucket and add them to custom headers |
| [Viewing local log](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Saves the record of operations on COSBrowser in the form of local log |

## COSBrowser Mobile Version

COSBrowser Mobile Version focuses on viewing and monitoring of resources and  monitor data of COS such as storage and traffic anytime, anywhere.

COSBrowser Mobile Version has the following features:

| Operation Name | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Login with WeChat](https://intl.cloud.tencent.com/document/product/436/32566#dulu) | Logs in with WeChat |
| [Data overview](https://intl.cloud.tencent.com/document/product/436/32566#dateview) | Views recent data usage |
| [File batch operations](https://intl.cloud.tencent.com/document/product/436/32566#filebatch) |  Uploads, downloads, deletes, copies, or moves files in a bucket in batches |
| [Sharing and uploading](https://intl.cloud.tencent.com/document/product/436/32566#shareupload) | Shares and uploads files from third-party apps to a bucket |
| [Renaming file](https://intl.cloud.tencent.com/document/product/436/32566#rename) | Renames files in a bucket |
| [Creating folder](https://intl.cloud.tencent.com/document/product/436/32566#newfolder) |  Creates folders in a bucket |
| [Viewing file details](https://intl.cloud.tencent.com/document/product/436/32566#view) |  Views the basic information of files in a bucket |
| [Previewing file](https://intl.cloud.tencent.com/document/product/436/32566#filepreview) | Previews media files (images, video, and audio) in a bucket |
| [Generating file link](https://intl.cloud.tencent.com/document/product/436/32566#generatelinks) | Generates a file access link with a validity period by requesting a temporary signature |
| [Searching for file](https://intl.cloud.tencent.com/document/product/436/32566#searchfile) | Searches for files in a bucket through prefix search |
| [Searching for bucket](https://intl.cloud.tencent.com/document/product/436/32566#searchbuckete) | Searches for existing buckets |
| [Viewing bucket details](https://intl.cloud.tencent.com/document/product/436/32566#viewbucket) | Views the basic information and domain name of your bucket |
| [Creating bucket](https://intl.cloud.tencent.com/document/product/436/32565) | Creates new buckets |
| [Adding access path](https://intl.cloud.tencent.com/document/product/436/32566#addaccess) | Allows a sub-account that has no access to the bucket list to enter a bucket for resource management by adding an access path |
| [Viewing storage pack](https://intl.cloud.tencent.com/document/product/436/32566#package)          | Views the usage of your current storage pack                          |

## Changelog

- Desktop Version changelog: [changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md).
- Mobile Version changelog: [changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md).

## Feedback and Suggestions

If you have any questions or suggestions during your use of COSBrowser, please feel free to give us your feedback:

- Feedback on Desktop Version: [issues](https://github.com/tencentyun/cosbrowser/issues).
- Feedback on Mobile Version: [issues_mobile](https://support.qq.com/embed/phone/67467).
