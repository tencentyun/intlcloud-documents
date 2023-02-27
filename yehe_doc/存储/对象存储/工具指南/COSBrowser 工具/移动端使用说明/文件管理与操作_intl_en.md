
>?
>COSBrowser for iOS v2.7.6 is used as an example here. For other versions, see [Changelog](https://github.com/TencentCloud/cosbrowser/blob/master/changelog_mobile.md).
>


<span id="CreateFolder"></span>
## Creating Folders

COSBrowser Mobile Version allows you to create a folder in a bucket as follows:

1. On the bucket's file list page, click **+** in the top-right corner.
2. In the displayed operation list, click **Create Folder**.
3. On the **Create Folder** page, enter a folder name and click **OK**.

<span id="DeleteFolder"></span>
## Deleting Folders

>! Deleting a folder will delete all files under it and its sub-directories.
>

#### Directions

1. Click **...** on the right of the target folder.
2. In the displayed operation list, click **Delete**.


<span id="UploadFile"></span>
## Uploading Files

You can use COSBrowser Mobile Version to upload local and remote files and files from other apps or the file manager to COS and set information such as file storage class, access permission, encryption method, object tags, and metadata during upload.




<span id="UploadPicturesAndVideos"></span>
### Uploading image/video

COSBrowser allows you to batch upload images or videos from your album to COS.

#### Directions

1. On the bucket list or file list page, click **+** in the top-right corner to display the operation list.
2. In the operation list, click **Upload Images**.
3. In the file list of the displayed album, select the target files and click **Next**.
4. (Optional) Configure the upload parameters. COSBrowser allows you to set the following file attributes during upload:
 - **Storage Class**: Select the storage class for your object as needed. This field is set to `STANDARD` by default. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/6222).
>! If your bucket has MAZ configuration enabled, you can only select a MAZ-enabled storage class, such as MAZ_STANDARD. If it also has INTELLIGENT TIERING configuration enabled, you can also select MAZ_INTELLIGENT TIERING.
>
  - **Access Permissions**: select the access permission for your object as needed. This field is set to `Inherit` by default (inheriting permissions of the bucket). For more information, please see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).
  - **Server-Side Encryption**: configure server-side encryption for the object you want to upload. COS will automatically encrypt your data as it is written and decrypt it when you access it. Currently, COS offers two encryption types: SSE-KMS (only available in Beijing, Shanghai, and Guangzhou regions) and SSE-COS. For more information, please see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
 -**Object Tag**: An object tag is composed of a tag key, equal sign (=), and a tag value, for example, `group = IT`. You can set, query, and delete tags of a specified object.
 - **Metadata**: object metadata, or HTTP header, is a string sent by the server over HTTP before it sends HTML data to the browser. By modifying HTTP headers, you can modify how the webpage responds as well as certain configurations, such as caching time. Modifying an object's HTTP headers does not modify the object itself. For more information, please see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).
5. Click **Upload**.


<span id="UploadFile;ink"></span>
### Uploading file through link

COSBrowser allows you to upload a file through the file link. Every time you enter the app, it will check the current clipboard. If there is any valid file link on the clipboard, a message will pop up asking you whether to upload the file through the link. In this case, you simply need to click **Upload Now**.

You can also upload a file through the link as follows:

1. On the bucket list or file list page, click **+** in the top-right corner to display the operation list.
2. Click **Upload Link**, paste the link for file upload into the text box, select an upload path, and click **Upload**.

<span id="UploadThirdPartySharing"></span>
### Uploading file shared by third-party app

You can also share a file from another app to COSBrowser to upload it.

>! This feature requires that the third-party app supports file sharing to other apps.
>

#### Directions

Take QQ as an example:
1. In QQ, click a file to preview it, click **...** in the top-right corner, and select **Other Apps**.
2. Click COSBrowser in the app list.


<span id="UploadFileManager"></span>
### Uploading file from file manager

COSBrowser can upload files from the system file manager ("Files" on iOS and the corresponding system file manager app on Android) to COS.

#### Directions

1. On the bucket list or file list page, click **+**.
2. In the displayed operation list, click **Upload Files**.
3. On the displayed file manager page, click the target file.

<span id="BackupFile"></span>
## Backing up Files

COSBrowser provides the auto backup feature. After this feature is enabled, COSBrowser will automatically back up the files in your album to the specified bucket. To help you manage backup files, COSBrowser displays the backup data as a separate module on the homepage.

>!
> - The album backup feature is only supported for the root account.
> - The album module displays only image and video files. To view all files, go to the bucket list and search for the backup bucket.
>



<span id="SetBackup"></span>
### Setting backup

Go to **Personal** > **Album Backup** and toggle on **Automatic Photo Backup** or **Automatic Video Backup**.

- **Automatic Photo Backup**: After it is enabled, all images in the album will be backed up.
- **Automatic Video Backup**: After it is enabled, all videos in the album will be backed up.
- **Back up over Wi-Fi Only**: After it is enabled, files will be backed up only over a Wi-Fi network.
- **Region**: After the backup region is selected, a bucket named `from-phone-date-APPID` will be created in the region by default.
>! The region can be set only before backup is enabled and cannot be modified after the settings are saved.
>
- **Enable Smart Storage**: This option is suitable for buckets with INTELLIGENT TIERING enabled. After it is enabled, files in the album will be uploaded to COS in INTELLIGENT TIERING. COS will automatically switch between the STANDARD and STANDARD_IA classes based on the access frequency of INTELLIGENT TIERING objects with no data retrieval fees incurred, which reduces your storage costs. For more information, see [INTELLIGENT TIERING Overview](https://intl.cloud.tencent.com/document/product/436/38305).


<span id="ManageBackupFiles"></span>
### Managing backup file

COSBrowser supports batch file upload and download.

#### Directions

1. On the **Album** page, click the batch operation icon in the top-right corner to display operation buttons.
2. Select the target files and click **Download** or **Delete** to download or delete the files.


<span id="AddFileToBackupBucket"></span>
### Adding file to backup bucket

You can also add image or video files from other buckets to the backup bucket to quickly preview them in the **Album** module.

#### Directions

1. Click **...** on the right of the target image or video file.
2. In the displayed operation list, click **Add to Album**.
3. Enter the **Album** module again to view the file.


<span id="DownloadFile"></span>
## Downloading Files

COSBrowser allows you to download files from COS to your local file system. It also enables you to save images to the system album.

<span id="DownloadToApp"></span>
### Downloading to app

COSBrowser provides multiple download entries for you to download files anytime, anywhere.

- Method 1:
 1. On the file list page, click **...** on the right of the target file.
 2. In the displayed operation list, click **Download**.
- Method 2:
On the **File Details** page, click **...**. In the displayed operation list, click **Download**.
- Method 3:
On the file preview page, click **...** in the top-right corner. In the displayed operation list, click **Download**.


<span id="SaveToGallery"></span>
### Saving to album

COSBrowser allows you to save images to the local album as follows:

1. On the file list page, click **...** on the right of the target file to display the operation list.
2. Click **Download** and select **Save to Album**.


<span id="BatchOperation"></span>
## Batch Operations

COSBrowser allows you to batch download, delete, copy, and move files from a bucket.


<span id="BatchDownload"></span>
### Batch download

1. Click a bucket to enter the file list page and click **...** in the top-right corner.
2. In the displayed operation list, click **Batch Operation**.

3. Batch select files and click **Download** on the bottom operation bar.
You can also click the **Transfer** button in the top-right corner of the file list page to view the jobs on the transfer list page.


<span id="BatchDelete"></span>
### Deleting domain names by batches

1. Click a bucket to enter the file list page and click **...** in the top-right corner.
2. In the displayed operation list, click **Batch Operation**.

3. Batch select files and click **Delete** on the bottom operation bar.


<span id="BatchCopy"></span>
### Batch copy

>? When you use COSBrowser to copy a source file, its information such as ACLs, policies, and tags will also be copied.
>

1. Click a bucket to enter the file list page and click **...** in the top-right corner.
2. In the displayed operation list, click **Batch Operation**.

3. Batch select files and click **More** > **Copy** on the bottom operation bar.



<span id="BatchMobile"></span>
### Batch moving

>? When you use COSBrowser to move a source file, its information such as ACLs, policies, and tags will also be moved.
>

1. Click a bucket to enter the file list page and click **...** in the top-right corner.
2. In the displayed operation list, click **Batch Operation**.

3. Batch select files and click **More** > **Move** on the bottom operation bar.



<span id="FilePreview"></span>
## Previewing Files

COSBrowser allows you to preview various file formats such as image, audio, video, and document. It also supports online file decompression.


<span id="ImagePreviewOnline"></span>
### Online image preview

COSBrowser allows you to preview images online without downloading them.

#### Enabling image preview

You can preview images in the following three methods:

1. Enable the feature globally

Select **Personal** > **Settings** and toggle on **Image Preview**.




2. Enable the feature temporarily

When you launch the app for the first time and enter the file list page, the app will check whether the current list page contains images, and if yes, a pop-up window will appear asking you whether to enable image preview. You can click **Enable Preview** to quickly enable the **image preview** feature. If you don't need this feature, you can click **Cancel**. If you want to use it in the future, you can manually enable it in **Personal** > **Settings**.


3. Enable the feature for one image

If you have disabled image preview in **Personal** > **Settings**, and it's not the first time that you open the app, when you enter the image details page, the app will ask you whether to enable preview. In this case, you can click **Click to Preview** to preview a file.

>? This switch doesn't change the status of the global **image preview** toggle.
>



#### Big image mode

COSBrowser provides the big image mode feature for you to view image details more clearly.

1. On the file list page, click the target image to enter the **File Details** page.
2. Click the image to enter the big image mode, in which you can zoom in the image with two fingers to view its details.
![](https://main.qcloudimg.com/raw/c5ded442635308a003ac6e98a740fdf6.jpg)


<span id="AudioDisplay"></span>
### Playing back audio

COSBrowser can play back audio files in MP3, OGG, AAC, WMA, WAV, APE, or FLAG format.

#### Directions

1. On the file list page, click an audio file to enter the **File Details** page.

2. Click the playback button.
You can speed up or pause the playback.



<span id="VideoDisplay"></span>
### Playing back video

COSBrowser provides a simple online video playback feature, which supports various formats such as AVI, WMV, MPEG, RM, RMVB, MKV, MOV, QT, and MP4. You can speed up or pause the video playback during watch. You can also play back the video in a floating window after the app enters the background.

#### Directions

1. On the file list page, click the target video file to enter the **File Details** page.
2. Click the playback button.
You can speed up or pause the playback.

>? After the app enters the background, you can still watch the video in a floating window.
>


<span id="DocumentPreview"></span>
### Previewing document

COSBrowser allows you to preview files in multiple formats such as PDF.

#### Directions

1. Click the target document to enter the **File Details** page. If you haven't enabled the document preview feature, click **Click to Enable**.

2. On the document preview feature configuration page, click **Enable Now**.

3. Return to the previous page and click **Click to Preview**.

4. On the document preview page, swipe left to view the next page.



<span id="UnzipFiles"></span>
## Decompressing Files

COSBrowser allows you to decompress files in ZIP, TAR, or GZ format online. The extracted files will be stored in the current directory.

1. On the file list page, click **...** on the right of a compressed file.

2. In the displayed operation list, click **Online Decompression**.

3. After the file is successfully decompressed, the extracted files will be displayed in the current directory.



<span id="ShareFiles"></span>
## Sharing Files

COSBrowser provides the folder and file sharing feature for you to quickly collect data or share the data in a bucket with other users.


<span id="SharedFolder"></span>
### Sharing folders

>?
> - You can only share a single folder but not multiple files.
> - A sharing duration of up to 2 hours and up to 1.5 days can be set for the root account and a sub-account respectively.
> - If multiple users share a folder, the file content may be hard to manage. In this case, we recommend you enable versioning for your bucket so that you can roll back to the desired historical version.
>

#### Generating sharing QR code/link

The detailed steps are as follows:

1. Click **...** on the right of a folder and click **Share** in the displayed operation list.

2. On the displayed sharing page, you can select QR code or link for sharing.

3. (Optional) Configure the sharing parameters, which are as detailed below. You can skip this step to keep the parameters as default.

 - **Permission**: Sets the access permission for the shared folder.
    - Can view: Pulls the folder list and downloads files in the folder using the access URL.
    - Can edit: Pulls the folder list and downloads files in the folder, upload files to the folder, and create folders using the access URL.
 - **Validity Period**: It is in minutes, hours, or days. The validity period for the root account and a sub-account is two hours and 24 hours respectively by default, which cannot be changed.
 - **Password**: A 6-character password automatically generated by the system. You can customize one as needed (numbers, letters, and symbols are supported).
4. Click **Generate Link** or **QR Code Sharing** to generate the sharing link or QR code.


### Viewing folder shared by another user

You can open a folder shared by another user from a mobile or desktop client.

**Method 1. View on mobile device**

1. On the **Login** or **Personal** page, click **Scan** to scan the QR code.

2. Enter the password and click **OK** to view the shared folder.


**Method 2. View on PC**

1. Click **Log in with Shared Link** on the **Login** page.

2. Enter the obtained URL address and password and log in.

**Method 3. View in browser**

1. Open the browser and enter the shared URL to open it.

2. Enter the password and click **Extract** to enter the shared folder.


<span id="ShareFile"></span>
### Sharing files

Each file stored in COS can be accessed through a specific URL. You can generate a file URL with the specified domain name if you have set other domain names (such as CDN acceleration domain name and custom origin domain name) for the bucket. If a file is private-read, you can request a temporary signature to generate a temporary access URL with a certain validity period.

>!
>- If you log in with a temporary key, you cannot configure the validity period of the file link, which is 1 hour by default.
>- If the file is public-read, the URL will not carry a signature and will be valid permanently. If the file is private-read, the URL will carry a temporary signature and will be valid for one hour.
>

#### Directions

1. Click a file to enter the **File Details** page.
The configuration items are described as follows:
 - Specify Domain: Set the domain name for the URL (optional).
 - Validity Period: Set the validity period for the URL (optional).
2. After confirming that the configuration is correct, click **Generate Link**.
3. Send the generated file URL.


<span id="RenameFile"></span>
## Renaming Files

>?Folders cannot be renamed.
>

#### Directions

1. Click **...** on the right of a file.
2. In the file operation list, click **Rename**.
2. In the pop-up window, enter the new filename and click **OK**.
If you select **Overwrite Duplicate File**, the original file will be overwritten; otherwise, a new file will be generated. You can also enable overwriting globally in **Personal** > **Settings** > **Default Upload Options** > **Rename Duplicate File**.


<span id="SearchFile"></span>
## Searching for Files

COSBrowser Mobile Version provides the fuzzy search and search by type features. You can use a prefix to search for files with that filename prefix in the current folder and its sub-folders. You can also specify the file type first to search for files in that type.


<span id="SearchKeyword"></span>
### Search by keyword

You can enter a search keyword to filter out all filenames containing the keyword in the current folder and all its sub-folders.



<span id="SearchTypes"></span>
### Search by type

COSBrowser allows you to search for files by type, such as video, folder, audio, document, image, and others.

#### Directions
Taking folder search as an example:

1. Click the search box and then **Folder**.

2. All files (which are folders here) in the folder type in the current directory will be listed.



<span id="SortOrFilterObjects"></span>
## Sorting or Filtering Objects

COSBrowser allows you to sort and filter files in a bucket.
>? Currently, sorting by file name/file size/modification time, and filtering by storage class are supported.
>

#### Directions

1. Enter the file list page and click the filter and sort button on the right of the search box.
2. In the operation list, sort or filter files in the bucket.<br>



<span id="ManageFilePermissions"></span>
## Managing File Permissions

COSBrowser allows you to set file access permissions, which takes priority over that for buckets.

>!
> - Object access permissions take effect only when the access is made via the default endpoint. For any access made via a CDN acceleration endpoint or a custom endpoint, bucket access permissions will take effect.
> - There are limits on the number of ACL rules. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).
>


<span id="ModifyPublicPermissions"></span>
### Modifying public permission

1. Click the target file to enter the **File Details** page.
2. Click **Permission Info** at the top to enter the permission list page.
3. Click **Public Permission** to modify the access permissions of the file.

<span id="SetUserPermissions"></span>
### Setting user permissions

1. Click the target file to enter the **File Details** page.
2. Click **Permission Info** at the top to enter the permission list page.
3. Click **Public Permission** to modify the user permissions of the file.
You can click **Add User** to add a user permission. Then, you can swipe left on a user permission to edit or delete it.


