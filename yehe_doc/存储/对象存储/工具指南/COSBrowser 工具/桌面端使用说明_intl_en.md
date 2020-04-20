## Download and Installation

#### Download

| OS | System Requirements | Download Address |
| :------- | :---------------------------------------------------------- | :----------------------------------------------------------- |
| Windows | Windows 7 32/64-bit or above, Windows Server 2008 R2 64-bit or above | [Windows](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe) |
| macOS | macOS 10.13 or above | [macOS](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.dmg) |
| Linux | Includes GUI which supports [AppImage](https://appimage.org/) format | [Linux](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest-linux.zip) |

#### Installation

The COSBrowser installation package is an executable application. After downloading it, double-click it and then install as prompted by the system.

## Login

You can log in to COSBrowser Desktop Edition using your TencentCloud API key, which can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. After successful login, the key will be saved in **Historical Keys** for future use. The login page is as shown below:

>You cannot log in to COSBrowser using a project key.

<img src="https://main.qcloudimg.com/raw/a4eda1e692750c3e6c610b498acd8eb0.jpg" width="90%">


## Basic Features

<span id="createordelete"></span>

#### 1. Creating/Deleting bucket

| Feature       | Description                                   | Directions                                                     |
| ---------- | -------------------------------------- | ------------------------------------------------------------ |
| Create Bucket | You can create a bucket directly in your client | 1. In the bucket list, click **Add Bucket** in the upper left corner<br />2. Enter the bucket name correctly, and select your region and access permissions<br />3. Click **OK**|
| Delete Bucket | Before deleting a bucket, make sure that all the data in the bucket has been cleared | 1. In the bucket list, click **Delete** to the right of the bucket you have chosen<br />2. Click **OK**|

<span id="viewbucket"></span>

#### 2. Viewing bucket details

You can view bucket details by clicking **Details** to the right of the bucket list. Such details include bucket name, access permissions, and versioning.

In the bucket details, you can change bucket access permissions and enable/disable versioning.


<span id="addaccess"></span>

#### 3. Adding access path

If you log in with a sub-account that does not have permission to access the bucket list, you can initiate an access by **Add Access Path**, for which COSBrowser provides two methods as follows:
(1) Add an access path directly in the login page, and select your bucket region correctly. Once you log in, you can manage your resources immediately.
<img src="https://main.qcloudimg.com/raw/ec7b54a49fdc0f3188433f1770972dc3.jpg" width="90%">
(2) After you log in with your sub account, in the upper left corner of the bucket list page, click **Add Path**, and enter a specified path so that you can enter a bucket and manage its resources.
<img src="https://main.qcloudimg.com/raw/729c41763c5366454fc9b806582826fd.png" width="90%">

<span id="upload"></span>

#### 4. Uploading file/folder

<table>
   <tr>
      <th>Upload Feature</th>
      <th>Remarks</th>
      <th>Directions</th>
   </tr>
   <tr>
      <td>Uploading file</td>
      <td >COSBrowser allows you to upload a single file or multiple files in batches in different ways</td>
      <td nowrap="nowrap">You can upload a file in the following ways. In the specified bucket or path:<br>1. Click **Upload Files** to upload files directly. <br>2. Right-click in the blank space of the file list and select **Upload Files** to upload files. <br>3. Drag a file to the file list pane to upload it.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Uploading folder and the contained files</td>
      <td>If a file or folder with the same name as the one to be uploaded already exists in the bucket or path, it will be overwritten by default</td>
      <td nowrap="nowrap">You can upload a folder in the following ways. In the specified bucket or path:<br>1. Click **Upload Folder** to upload a folder directly. <br>2. Right-click in the blank space of the file list and select **Upload Folder** to upload a folder. <br>3. Drag a folder to the file list pane to upload it.</td>
   </tr>
   <tr>
      <td>Incremental upload</td>
      <td>Incremental upload refers to the process of comparing the file to be uploaded with existing objects in the bucket before uploading it and skipping it if an object with the same name already exists in the bucket</td>
      <td> To use incremental upload, follows these 2 steps: In a bucket or path you specify:<br>1. Upload as you do with a folder, and click **Next**.<br>2.In **Store Mode**, Select **Skip**, and click **Upload** to begin incremental upload.</td>
   </tr>
</table>



<span id="download"></span>

#### 5. Downloading file/folder

<table>
   <tr>
      <th>Download Feature</th>
      <th>Remarks</th>
      <th>Directions</th>
   </tr>
   <tr>
      <td>Downloading file</td>
      <td>COSBrowser allows you to download a single file or multiple files in batches in different ways</td>
      <td nowrap="nowrap">You can download a file in the following ways:<br>1. Select the file to be downloaded and click **Download** in the UI to download it.<br>2. Right-click a file and select **Download**.<br>3. Drag a file to the local file system to download it.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Downloading folder and the contained files</td>
      <td>If a file or folder with the same name as the one to be downloaded already exists in the local file system, the one to be downloaded will be renamed by default</td>
      <td>You can download a folder and files in it in the following ways:<br>1. Select the folder to be downloaded and click **Download** in the UI to download it.<br>2. Right-click a folder and select **Download** to download it directly.<br>3. Drag a folder to the local file system to download it.</td>
   </tr>
   <tr>
      <td>Incremental download</td>
      <td>Incremental download refers to the process of comparing the object to be downloaded with local files before downloading it and skipping it if an object with the same name already exists</td>
      <td>You can perform an incremental download by following the steps below:<br>1. Select the file/folder to be downloaded and move the cursor to **Download** and a drop-down list will appear.<br>2. Click **Advanced Download** in the drop-down list and select **Skip** in the pop-up window.<br>3. Then, click **Download Now** to incrementally download new files/folders.</td>
   </tr>
</table>

<span id="delete"></span>

#### 6. Deleting file/folder	

To delete a file/folder, select the file/folder to be deleted and click **Delete** in **More** at the top of the UI, or right-click it and select **Delete**. You can delete multiple files/folders in batches.

<span id="synchronization"></span>

#### 7. Synchronizing file

Using file synchronization feature, you can upload the specified files in your local folders to a bucket in real time. Detailed directions are as follows:

(1) Click **Sync** at the top right of the UI.
(2) Specify a local folder and bucket directory in the pop-up.
(3) Click **Start Sync** to enable file synchronization.
(4) View synchronization history logs in **Sync Logs** tab.
<img src="https://main.qcloudimg.com/raw/76b16c34adc1874c611eef80acae1a31.png" width="90%" />

>
> - Synchronization means that when the file is uploaded, the system automatically recognizes whether the same file exists in the bucket. Only the files that do not exist in the bucket are uploaded by the synchronization feature.
> - Only supports synchronizing local files to bucket currently. Reverse operation is not supported.
> - Supports for both manual and automatic synchronization.

<span id="copy"></span>

#### 8. Copying and pasting file

To copy a file/folder, select the file/folder to be copied in the specified bucket or path and click **Copy** in **More** at the top of the UI, or right-click it and select **Copy**. After the file/folder is successfully copied, you can paste it to **another bucket or path**. You can copy and paste multiple files/folders in batches.

>If a file/folder with the same name as the one to be pasted already exists in the destination path, it will be overwritten by default.

<span id="rename"></span>

#### 9. Renaming file

Select a file you want to rename, right-click and select **Rename**, or click **Rename** in **More Actions** to the right of the file. Then enter your file name, and click **OK**.

>Folders cannot be renamed.

<span id="newfolder"></span>

#### 10. Creating folder

To create a folder in the specified bucket or path, click **Create Folder** in the UI, or right-click in the UI and select **Create Folder**, enter the folder name, and click OK.

>
> - The folder name can contain up to 255 digits, letters, and visible characters.
> - The folder name cannot contain special characters such as `\ / : * ? " | < >`.
> - `..` cannot be used as the folder name.
> - The folder cannot be renamed, so name it with caution.

<span id="view"></span>

#### 11. Viewing file details

To view the details of a file, click its filename or right-click it and select **Details**. File details include file name, file size, modification time, access permission, storage class, ETag, headers, object address, and option to create a temporary link.

<img src="https://main.qcloudimg.com/raw/eb1b59df170aaa03a161f260c1c486c6.png" width="70%">


<span id="generatelinks"></span>

#### 12. Generating file link

Each file stored in COS can be accessed through a specific link. If a file is private-read, you can request a temporary signature to generate a temporary access link with a certain validity period.

COSBrowser allows you to generate a file link in the following ways:

- In the list view, click the Share icon to the right of the file to generate a link and copy it. If the file is public-read, the link will not carry a signature and be valid permanently. If the file is private-read, the link will carry a signature and be valid for 2 hours.
- Right-click a file and select **Copy Link** to generate a link and copy it. If the file is public-read, the link will not carry a signature and be valid permanently. If the file is private-read, the link will carry a signature and be valid for 2 hours.
- In **File Details**, click **Create a temporary link** and set its validity period.
 <img src="https://main.qcloudimg.com/raw/f901ffb368a14d967601aa3fa38f4e6c.png" width="60%">

<span id="preview"></span>

#### 13. Previewing file

COSBrowser allows you to preview media files, including images, videos, and audio. To preview a media file, double-click it or right-click it and select **Preview** or **Playback** in the context menu. On the file preview or playback screen, you can click:

- **Copy Link** to generate a file access link and copy it.
- **Download** to download the file to the local file system. If a file with the same name already exists in the local file system, it will be overwritten by default.
- **View on Mobile** to generate a QR code for the file, which can be scanned on a mobile phone for direct view.

>
> - Preview is available for images in most formats, .mp4 and .webm videos, and .mp3. and .wav audios.
> - File preview will incur downstream traffic. Please use it with caution.

![](https://main.qcloudimg.com/raw/8111561c400277a920fd1919de7220ec.png)

<span id="searchfile"></span>

#### 14. Searching for file

To search for a file, enter the filename in the search box at the top right of the bucket. COSBrowser supports prefix search and fuzzy search.

<span id="searchbuckete"></span>

#### 15. Searching for bucket

To quickly locate a bucket, enter the bucket name in the search box above the bucket list on the left.

<span id="viewfiles"></span>

#### 16. Viewing multiple file versions

After versioning is enabled for your bucket, you can view the historical versions of a file by right-clicking in the blank space of the file list and select **View multiple versions** in the context menu.

 <img src="https://main.qcloudimg.com/raw/b9018ff12b0c7726d393004b838f6d1c.png" width="80%">


<span id="sets"></span>

## Settings

<table>
   <tr>
      <th nowrap="nowrap">System Feature</th>
      <th>Remarks</th>
      <th>Directions</th>
   </tr>
   <tr>
      <td>Setting up proxy</td>
      <td >COSBrowser uses the system-configured proxy to connect to the internet. Please make sure that your proxy is set up properly or disable the proxy configuration if it fails to connect to the internet</td>
      <td nowrap="nowrap">1. Select **Settings** > **Proxy**.<br>2. Set up a proxy to connect to the internet.</td>
   </tr>
   <tr>
      <td>Setting the number of concurrent transfers</td>
      <td>COSBrowser supports uploading/downloading multiple files in batches</td>
      <td>1. Select **Settings** > **Download/Upload**. <br>2. Set the number of concurrent transfers, which is 5 by default</td>
   </tr>
   <tr>
      <td>Setting the number of parts to be transferred</td>
      <td>COSBrowser supports uploading/downloading a file in multiple parts. When the file to be transferred exceeds a certain size, multipart transfer will be performed by default</td>
      <td>1. Select **Setting** > **Download/Upload**.<br>2. Set the number of concurrent parts to be transferred, which is 5 by default.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Setting the number of retries upon transfer failure</td>
      <td>COSBrowser will retry failing tasks by default when transferring files</td>
      <td>1. Select **Settings** > **Download/Upload**.<br>2. Set the number of retries upon transfer failure, which is 5 by default.</td>
   </tr>
   <tr>
      <td>Setting upload check</td>
      <td>COSBrowser supports checking files online after upload to verify whether their size and status are correct</td>
      <td>1. Select **Settings** > **Upload**.<br>2. Select "Upload Check".</td>
   </tr>
   <tr>
      <td>Setting MD5 checksum calculation during upload</td>
      <td>COSBrowser supports calculating MD5 checksum during file upload and adding it to the file metadata as the `x-cos-meta-md5` custom header. Next time when the file is requested, the header will be returned for file check</td>
      <td>1. Select **Settings** > **Upload**.<br>2. Select "Calculate meta-md5 Header".</td>
   </tr>
   <tr>
      <td>Viewing local log</td>
      <td>COSBrowser will record all the performed operations in the `cosbrowser.log` local file</td>
      <td nowrap="nowrap">1. Select **Settings** > **About**.<br>2. Click **Local Log** and the system will open the directory where the local log is stored.</td>
   </tr>
</table>

