## Download and installation

## Downloading software

| OS | System Requirements | Download Address |
| :------- | :----------------------------------------------------- | :----------------------------------------------------------- |
| Windows | Above Windows 7 32/64-bit or Windows Server 2008 R2 64-bit | [Windows](https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-setup-latest.exe) |
| macOS | Above macOS 10.13 | [macOS](https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-latest.dmg) |
| Linux | Includes GUI which supports [AppImage](https://appimage.org/) format | [Linux](https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-latest-linux.zip) |

#### Installing software

The COSBrowser installation package is an executable application. After downloading it, double-click it and then install as prompted by the system.

## Login

You can log in to COSBrowser Desktop Edition using your TencentCloud API key, which can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. After successful login, the key will be saved in **Historical Keys** for future use. The login page is as shown below:

> You cannot log in to COSBrowser using a project key.

![](https://main.qcloudimg.com/raw/5170518a724f47bdd309512b34489a44.png)

## Basic features

<span id="upload"></span>

#### 1. Uploading file/folder

<table>
   <tr>
      <th width="50">Upload Feature</th>
      <th width="25">Description</th>
      <th width="450">Directions</th>
   </tr>
   <tr>
      <td>Uploading file</td>
      <td >COSBrowser allows you to upload a single file or multiple files in batches in different ways</td>
      <td >You can upload a file in the following ways. In the specified bucket or path:<br>1. Click  【Upload Files】 to upload files directly. <br>2. Right-click in the blank space of the file list and select 【Upload Files】 to upload files. <br>3. Drag a file to the file list pane to upload it.</td>
   </tr>
   <tr>
      <td >Uploading folder and the contained files</td>
      <td>If a file or folder with the same name as the one to be uploaded already exists in the bucket or path, it will be overwritten by default</td>
      <td >You can upload a folder in the following ways. In the specified bucket or path:<br>1. Click 【Upload Folder】 to upload a folder directly. <br>2. Right-click in the blank space of the file list and select 【Upload Folder】 to upload a folder. <br>3. Drag a folder to the file list pane to upload it.</td>
   </tr>
   <tr>
      <td>Incremental upload</td>
      <td>Incremental upload refers to the process of comparing the file to be uploaded with existing objects in the bucket before uploading it and skipping it if an object with the same name already exists in the bucket</td>
      <td>You can perform an incremental upload by following the steps below. In the specified bucket or path:<br>1. Move the cursor to 【Upload Folder】 and a drop-down list will appear.<br>2. Click 【Advance Upload Folder】 in the drop-down list.<br>3. Upload a folder by selecting 【Skip】 in the pop-up window.</td>
   </tr>
</table>



<span id="download"></span>

#### 2. Downloading file/folder

<table>
   <tr>
      <th width="50">Download Feature</th>
      <th width="25">Description</th>
      <th width="450">Directions</th>
   </tr>
   <tr>
      <td>Downloading file</td>
      <td>COSBrowser allows you to download a single file or multiple files in batches in different ways</td>
      <td>You can download a file in the following ways:<br>1. Select the file to be downloaded and click 【Download】 in the UI to download it.<br>2. Right-click a file and select 【Download】.<br>3. Drag a file to the local file system to download it.</td>
   </tr>
   <tr>
      <td>Downloading folder and the contained files</td>
      <td>If a file or folder with the same name as the one to be downloaded already exists in the local file system, the one to be downloaded will be renamed by default</td>
      <td>You can download a folder and files in it in the following ways:<br>1. Select the folder to be downloaded and click 【Download】 in the UI to download it.<br>2. Right-click a folder and select 【Download】 to download it directly.<br>3. Drag a folder to the local file system to download it.</td>
   </tr>
   <tr>
      <td>Incremental download</td>
      <td>Incremental download refers to the process of comparing the object to be downloaded with local files before downloading it and skipping it if an object with the same name already exists</td>
      <td>You can perform an incremental download by following the steps below:<br>1. Select the file/folder to be downloaded and move the cursor to 【Download】 and a drop-down list will appear.<br>2. Click 【Advanced Download】 in the drop-down list and select 【Skip】 in the pop-up window.<br>3. Then, click 【Download Now】 to incrementally download new files/folders.</td>
   </tr>
</table>



<span id="delete"></span>

#### 3. Deleting file/folder

To delete a file/folder, select the file/folder to be deleted and click 【Delete】 in the UI, or right-click it and select 【Delete】. You can delete multiple files/folders in batches.

<span id="synchronization"></span>
#### 4. Synchronizing file

Using file synchronization feature, you can upload the specified files in your local folders to a bucket in real time. Detailed directions are as follows: 

(1) Click the **Sync** button on the bottom left of the interface. 
(2) Specify a local folder and bucket directory in the pop-up.
(3) Click **Start Sync** to enable file synchronization feature.
(4) View synchronization history logs in **Sync Logs** tab.
<img src="https://main.qcloudimg.com/raw/4120641544d696a8cab7f3cd9d92ef02.png" style="zoom:100%;" />

>
>- Synchronization means that when the file is uploaded, the system automatically recognizes whether the same file exists in the bucket. Only the files that do not exist in the bucket are uploaded by the synchronization feature.
>- Only supports synchronizing local files to bucket currently. Reverse operation is not supported.
>- Supports for both manual and automatic synchronization.

<span id="copy"></span>

#### 5. Copying and pasting file

To copy a file/folder, select the file/folder to be copied in the specified bucket or path and click **Copy** in the UI, or right-click it and select **Copy**. After the file/folder is successfully copied, you can paste it to **another bucket or path**. You can copy and paste multiple files/folders in batches.

> If a file/folder with the same name as the one to be pasted already exists in the destination path, it will be overwritten by default.

<span id="rename"></span>

#### 6. Renaming file

To rename a file, select the file to be renamed and click **Rename** in the UI, or right-click it and select **Rename**, enter the new filename, and click OK.

> Folders cannot be renamed.

<span id="newfolder"></span>

#### 7. Creating folder

To create a folder in the specified bucket or path, click **Create Folder** in the UI, or right-click in the UI and select **Create Folder**, enter the folder name, and click OK.

> 
> - The folder name can contain up to 255 digits, letters, and visible characters.
> - The folder name cannot contain special characters such as `\ / : * ? " | < >`.
> - `..` cannot be used as the folder name.
> - The folder cannot be renamed, so name it with caution.

<span id="view"></span>

#### 8. Viewing file details

To view the details of a file, click its filename or right-click it and select **Details**. File details include file name, file size, modification time, access permission, storage class, ETag, headers, object address, and option to create a temporary link.

![](https://main.qcloudimg.com/raw/e2050d7a5312e40ef274643e9ee05f16.png)

<span id="generatelinks"></span>

#### 9. Generating file link

Each file stored in COS can be accessed through a specific link. If a file is private-read, you can request a temporary signature to generate a temporary access link with a certain validity period.

COSBrowser allows you to generate a file link in the following ways:

- In the list view, click the "Copy Link" icon to the right of the file to generate a link and copy it. If the file is public-read, the link will not carry a signature and be valid permanently. If the file is private-read, the link will carry a signature and be valid for 2 hours.
- Right-click a file and select **Copy Link** to generate a link and copy it. If the file is public-read, the link will not carry a signature and be valid permanently. If the file is private-read, the link will carry a signature and be valid for 2 hours.
- In **File Details**, click **Create a temporary link** and set its validity period.
  ![](https://main.qcloudimg.com/raw/f0cd218fb67851da736853cfc85a9f9e.png)

<span id="preview"></span>

#### 10. Previewing file

COSBrowser allows you to preview media files, including images, videos, and audio. To preview a media file, double-click it or right-click it and select **Preview** or **Playback** in the context menu. On the file preview or playback screen, you can click:

- **Copy Link** to generate a file access link and copy it.
- **Download** to download the file to the local file system. If a file with the same name already exists in the local file system, it will be overwritten by default.
- **View on Mobile** to generate a QR code for the file, which can be scanned on a mobile phone for direct view.

> 
>
> - Preview is available for images in most formats, .mp4 and .webm videos, and .mp3. and .wav audios.
> - File preview will incur downstream traffic. Please use it with caution.

![](https://main.qcloudimg.com/raw/1e4a4a0c01b0681aff43dc2b80e8fdec.png)

<span id="searchfile"></span>

#### 11. Searching for file

To search for a file, enter the filename in the search box at the top right of the bucket. COSBrowser only supports prefix search.

<span id="searchbuckete"></span>

#### 12. Searching for bucket

To quickly locate a bucket, enter the bucket name in the search box above the bucket list on the left. Fuzzy search is supported.

<span id="viewfiles"></span>

#### 13. Viewing multiple file versions

After versioning is enabled for your bucket, you can view the historical versions of a file by right-clicking in the blank space of the file list and select **View multiple versions** in the context menu.

![](https://main.qcloudimg.com/raw/3e127b8af49f1a64c0c001e21c042c45.png)

<span id="viewbucket"></span>

#### 14. Viewing bucket details

To view the details of a bucket, right-click in the blank space of the list and select **Bucket details** in the context menu. Bucket details include bucket name, access permission, and versioning status.

<span id="sets"></span>

## Software settings

<table>
   <tr>
      <th width="100">System Feature</th>
      <th width="200">Description</th>
      <th width="400">Directions</th>
   </tr>
   <tr>
      <td>Setting up proxy</td>
      <td >COSBrowser uses the system-configured proxy to connect to the internet. Please make sure that your proxy is set up properly or disable the proxy configuration if it fails to connect to the internet</td>
      <td>1. Select 【Settings】 > 【Proxy】.<br>2. Set up a proxy to connect to the internet.</td>
   </tr>
   <tr>
      <td>Setting the number of concurrent transfers</td>
      <td>COSBrowser supports uploading/downloading multiple files in batches</td>
      <td>1. Select 【Settings】 > 【Download/Upload】. <br>2. Set the number of concurrent transfers, which is 5 by default</td>
   </tr>
   <tr>
      <td>Setting the number of parts to be transferred</td>
      <td>COSBrowser supports uploading/downloading a file in multiple parts. When the file to be transferred exceeds a certain size, multipart transfer will be performed by default</td>
      <td>1. Select 【Setting】 > 【Download/Upload】.<br>2. Set the number of concurrent parts to be transferred, which is 5 by default.</td>
   </tr>
   <tr>
      <td>Setting the number of retries upon transfer failure</td>
      <td>COSBrowser will retry failing tasks by default when transferring files</td>
      <td>1. Select 【Settings】 > 【Download/Upload】.<br>2. Set the number of retries upon transfer failure, which is 5 by default.</td>
   </tr>
   <tr>
      <td>Setting upload check</td>
      <td>COSBrowser supports checking files online after upload to verify whether their size and status are correct</td>
      <td>1. Select 【Settings】 > 【Upload】.<br>2. Select "Upload Check".</td>
   </tr>
   <tr>
      <td>Setting MD5 checksum calculation during upload</td>
      <td>COSBrowser supports calculating MD5 checksum during file upload and adding it to the file metadata as the `x-cos-meta-md5` custom header. Next time when the file is requested, the header will be returned for file check</td>
      <td>1. Select 【Settings】 > 【Upload】.<br>2. Select "Calculate meta-md5 Header".</td>
   </tr>
   <tr>
      <td>Viewing local log</td>
      <td>COSBrowser will record all the performed operations in the `cosbrowser.log` local file</td>
      <td>1. Select 【Settings】 > 【About】.<br>2. Click 【Local Log】 and the system will open the directory where the local log is stored.</td>
   </tr>
</table>

