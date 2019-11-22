COSBrowser is a visual tool launched by COS that allows you to easily view, transfer, and manage COS resources through simple interactions. Currently, COSBrowser is available in Desktop Version and Mobile Version. For more information, see:

- [User Guide for Desktop Version](https://intl.cloud.tencent.com/document/product/436/32565)
- [User Guide for Mobile Version](https://intl.cloud.tencent.com/document/product/436/32566)

Download URL

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
      <td>Above Windows 7 32/64-bit or Windows Server 2008 R2 64-bit</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-setup-latest.exe">Windows</a></td>
   </tr>
   <tr>
      <td>macOS</td>
      <td>Above macOS 10.13</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-latest.dmg">macOS</a></td>
   </tr>
   <tr>
      <td>Linux</td>
      <td>Includes GUI which supports <a href="https://appimage.org">AppImage</a> format</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-latest-linux.zip">Linux</a></td>
   </tr>
   <tr>
      <td rowspan="2">Mobile Version</td>
      <td>Android</td>
      <td>Above Android 4.4</td>
      <td><a href="https://sj.qq.com/myapp/detail.htm?apkName=com.qcloud.cos.client">Android</a></td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>Above iOS 11</td>
      <td><a href="https://apps.apple.com/cn/app/id1469323992">iOS</a></td>
   </tr>
</table>

## COSBrowser desktop version

COSBrowser Desktop Version focuses on resource management and allows you to upload and download data in batches.

> COSBrowser Desktop Version uses the system-configured proxy to connect to the internet. Please make sure that your proxy is set up properly or disable the proxy configuration if it fails to connect to the internet.
> - For queries on Windows, go to "Internet Options".
> - For queries on macOS, go to "Network Preferences".
> - For queries on Linux, go to System Settings > Network > Network Proxy.

## Basic features

COSBrowser Desktop Version has the following features:

| Feature | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Uploading file/folder](https://intl.cloud.tencent.com/document/product/436/32565#upload) | This feature allows you to upload files/folders to a bucket separately, in batches, or incrementally |
| [Downloading file/folder](https://intl.cloud.tencent.com/document/product/436/32565#download) | This feature allows you to download files/folders to the local file system separately, in batches, or incrementally |
| [Deleting file/folder](https://intl.cloud.tencent.com/document/product/436/32565#delete) | This feature allows you to delete files/folders from a bucket separately or in batches |
|      [Synchronizing file](https://intl.cloud.tencent.com/document/product/436/32565#synchronization)            |                                                    This feature allows you to synchronize local files to buckets in real time                  |   
| [Copying and pasting file](https://intl.cloud.tencent.com/document/product/436/32565#copy) | This feature allows you to copy files/folders separately or in batches from one directory to another directory |
| [Renaming file](https://intl.cloud.tencent.com/document/product/436/32565#rename) | This feature allows you to rename files in a bucket |
| [Creating folder](https://intl.cloud.tencent.com/document/product/436/32565#newfolder) | This feature allows you to create folders in a bucket |
| [Viewing file details](https://intl.cloud.tencent.com/document/product/436/32565#view) | This feature allows you to view the basic information of files in a bucket |
| [Generating file link](https://intl.cloud.tencent.com/document/product/436/32565#generatelinks) | This feature allows you to generate a file access link with a validity period by requesting a temporary signature |
| [Previewing file](https://intl.cloud.tencent.com/document/product/436/32565#preview) | This feature allows you to preview media files (images, videos, and audios) in a bucket |
| [Searching for file](https://intl.cloud.tencent.com/document/product/436/32565#searchfile) | This feature allows you to search for files in a bucket through prefix search |
| [Searching for bucket](https://intl.cloud.tencent.com/document/product/436/32565#searchbuckete) | This feature allows you to search for created buckets |
| [Viewing multiple file versions](https://intl.cloud.tencent.com/document/product/436/32565#viewfiles) | This feature allows you to view the historical versions of files in a bucket where versioning is enabled |
| [Viewing bucket details](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | This feature allows you to view the basic information of buckets |
| [Setting up proxy](https://intl.cloud.tencent.com/document/product/436/32565#sets) | This feature allows you to set up a proxy to access COS |
| [Setting the number of concurrent transfers](https://intl.cloud.tencent.com/document/product/436/32565#sets) | This feature allows you to set the number of concurrent transfers for file upload or download |
| [Setting the number of parts to be transferred](https://intl.cloud.tencent.com/document/product/436/32565#sets) | This feature allows you to set the number of parts for multipart upload or download |
| [Setting the number of retries upon transfer failure](https://intl.cloud.tencent.com/document/product/436/32565#sets) | This feature allows you to set the number of retries upon upload or download failure |
| [Setting upload check](https://intl.cloud.tencent.com/document/product/436/32565#sets) | This feature allows you to double-check files uploaded to a bucket |
| [Setting MD5 checksum calculation during upload](https://intl.cloud.tencent.com/document/product/436/32565#sets) | This feature allows you to calculate MD5 checksums of files uploaded to a bucket and add them to custom headers |
| [Viewing local log](https://intl.cloud.tencent.com/document/product/436/32565#sets) | This feature allows you to save the record of operations on COSBrowser in the form of local log |

## COSBrowser mobile version

COSBrowser Mobile Version focuses on viewing and monitoring of resources and allows you to monitor data of COS such as storage and traffic anytime, anywhere.

## Basic features

COSBrowser Mobile Version has the following features:

| Operation Name | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Login with WeChat](https://intl.cloud.tencent.com/document/product/436/32566#dulu) | This feature allows you to log in with WeChat |
| [Data overview](https://intl.cloud.tencent.com/document/product/436/32566#dateview) | This feature allows you to view recent data usage |
| [File batch operations](https://intl.cloud.tencent.com/document/product/436/32566#filebatch) | This feature allows you to upload, download, delete, copy, or move files in a bucket in batches |
| [Sharing and uploading](https://intl.cloud.tencent.com/document/product/436/32566#shareupload) | This feature allows you to share and upload files from third-party apps to a bucket |
| [Renaming file](https://intl.cloud.tencent.com/document/product/436/32566#rename) | This feature allows you to rename files in a bucket |
| [Creating folder](https://intl.cloud.tencent.com/document/product/436/32566#newfolder) | This feature allows you to create folders in a bucket |
| [Viewing file details](https://intl.cloud.tencent.com/document/product/436/32566#view) | This feature allows you to view the basic information of files in a bucket |
| [Generating file link](https://intl.cloud.tencent.com/document/product/436/32566#generatelinks) | This feature allows you to generate a file access link with a validity period by requesting a temporary signature |
| [Searching for file](https://intl.cloud.tencent.com/document/product/436/32566#searchfile) | This feature allows you to search for files in a bucket through prefix search |
| [Searching for bucket](https://intl.cloud.tencent.com/document/product/436/32566#searchbuckete) | This feature allows you to search for created buckets |
| [Viewing bucket details](https://intl.cloud.tencent.com/document/product/436/32566#viewbucket) | This feature allows you to view the basic information of buckets |
| [Creating bucket](https://intl.cloud.tencent.com/document/product/436/11366#searchbuckete) | This feature allows you to create new buckets |
| [Adding access path](https://intl.cloud.tencent.com/document/product/436/32566#addaccess) | This feature allows a sub-account that has no access to the bucket list to enter a bucket for resource management by adding an access path |

**Changelog**

- Desktop Version changelog: [changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md).
- Mobile Version changelog: [changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md).

## Feedback and suggestions

If you have any questions or suggestions during your use of COSBrowser, please feel free to give us your feedback:

- Feedback on Desktop Version: [issues](https://github.com/tencentyun/cosbrowser/issues).
- Feedback on Mobile Version: [issues_mobile](https://support.qq.com/embed/phone/67467).
