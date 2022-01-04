COSBrowser is a visual interface tool launched by Tencent Cloud to make it easier and simpler for you to view, transfer, manage, and interact with COS resources. Currently, COSBrowser is available for desktop and mobile devices. For more information, see:

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
      <td rowspan=3>Desktop Version</td>
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
      <td>Includes a GUI that supports the <a href="https://appimage.org">AppImage</a> format<br>
          Note: To launch a client that runs CentOS, you need to run <code>./cosbrowser.AppImage --no-sandbox</code></td> in the terminal.
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
      <td>Web Edition</td>
      <td>Web</td>
      <td>Browsers such as Chrome, FireFox, Safari, and IE10+</td>
      <td><a href="https://cosbrowser.cloud.tencent.com/web">Web</a></td>
   </tr>
   <tr>
      <td>Uploader Plugin</td>
      <td>Web</td>
      <td>Chrome browsers</td>
      <td><a href="https://chrome.google.com/webstore/detail/cosbrowser-uploader/mggpkimgmmdbdbakdkaebhjhgomcmlnd">Web Store</a>/<a href="https://cos5.cloud.tencent.com/cosbrowser/latest-chrome.zip">Offline Download</a></td>
   </tr>
</table>

## COSBrowser for Desktop

COSBrowser for desktop focuses on resource management and uploading and downloading data in batches.

> !COSBrowser Desktop Version uses the system-configured proxy to connect to the internet. Please make sure that your proxy is set up properly or disable the proxy configuration if it fails to connect to the Internet.
>
> - For queries on Windows, go to "Internet Options".
> - For queries on macOS, go to "Network Preferences".
> - For queries on Linux, go to System Settings > Network > Network Proxy.

COSBrowser for desktop has the following features:

| Feature | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Creating/Deleting a bucket](https://intl.cloud.tencent.com/document/product/436/32565#createordelete) | Creates or deletes a bucket |
| [Viewing bucket details](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | Views the basic information of your bucket |
| [Viewing statistics](https://intl.cloud.tencent.com/document/product/436/32565#count)           | Views the current storage capacity and number of objects in your bucket                         |
| [Permission management](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket)                               | Modifies the permissions on your buckets and objects                                 |
| [Setting versioning](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket)                                     | Enable/Suspends bucket versioning                                 |
| [Adding an access path](https://intl.cloud.tencent.com/document/product/436/32565#addaccess)                                     | Adds an access path                                             |
| [Uploading a file/folder](https://intl.cloud.tencent.com/document/product/436/32565#upload) | Uploads files/folders to a bucket separately, in batches, or incrementally |
| [Downloading a file/folder](https://intl.cloud.tencent.com/document/product/436/32565#download) | Downloads files/folders to the local file system separately, in batches, or incrementally |
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
| [Setting up a proxy](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets up a proxy to access COS |
| [Setting the number of concurrent transfers](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of concurrent transfers for file upload or download |
| [Setting the number of parts to be transferred](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of parts for multipart upload or download |
| [Setting the number of retries upon transfer failure](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Sets the number of retries upon upload or download failure |
| [Setting upload check](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Double-checks files uploaded to a bucket |
| [Limiting single-thread speed](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Limits the upload and download speeds for a single thread |
| [Viewing a local log](https://intl.cloud.tencent.com/document/product/436/32565#sets) | Saves the record of operations on COSBrowser in the form of a local log |

## COSBrowser Mobile Version

The COSBrowser mobile version is mainly used to monitor COS resources (such as storage usage and traffic) at any time you want. For more supported features, please see [Mobile Version Features](https://intl.cloud.tencent.com/document/product/436/41616).

## Changelog

- Desktop Version changelog: [changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md).
- Mobile Version changelog: [changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md).

## Feedback and Suggestions

If you have any questions or suggestions during your use of COSBrowser, please feel free to give us your feedback:

- Feedback on Desktop Version: [issues](https://github.com/tencentyun/cosbrowser/issues).
- Feedback on Mobile Version: [issues_mobile](https://support.qq.com/embed/phone/67467).
