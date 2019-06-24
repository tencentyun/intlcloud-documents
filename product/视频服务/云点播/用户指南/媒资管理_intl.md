Tencent Cloud VOD has strong media processing capabilities. On the **Media Asset Management** page, you can upload and manage video files in the **Uploaded** tab or view the video files being uploaded in the **Uploading** tab.

## Uploaded

Log in to [VOD console](https://console.cloud.tencent.com/video), click **Media Asset Management** in the left sidebar, and select the **Uploaded** tab where you can upload, delete, and process videos, and modify video categories. In the video list, you can view the information (including thumbnail, name, and ID), status, category, source, and creation time of a video.

### Uploading a Video
> 
- Web uploading is supported for Internet Explorer 10+ or higher and Chrome.
- During the upload, do not close the browser to access the other products on the console; otherwise, the upload will be interrupted.
- Web upload supports resuming and queuing in Chrome.

On the **Media Assets** > **Uploaded** page, click **Upload Video**. You can select **Local Upload** or **URL Upload** to upload the video.
- Local Upload: You can upload a local file directly to the VOD console.
- URL Upload: You can download and store a video in the VOD console through the video URL.

![](https://main.qcloudimg.com/raw/bbbbc39b295157b9dee12a6841b712d3.png)

#### Local Upload

1. Select **Local Upload**. Click **Select a video** to select a local video file or drag and drop the file to the upload list zone.
 > ?
 > - Batch upload is supported. You can upload up to 5 videos at a time, and all the selected videos will be displayed in the upload list.
 > - Supported formats: WMV, RM, MOV, MPEG, MP4, 3GP, FLV, and AVI.
 > 
 ![](https://main.qcloudimg.com/raw/691c69539edd072cdbd63f761217a17e.png)
2. In the upload list, you can check the file name and size of a selected video, modify the **Video Name** and **Video Category**, or delete it.
3. You can choose whether to process the uploaded video.
   a. If no processing is needed, select **Upload directly with no processing**.
   b. If processing is needed, select **Process video while uploading** and configure video processing parameters according to the table below.
<table>
     <tr>
         <th nowrap="nowrap">Processing Type</th>  
         <th nowrap="nowrap">Transcoding/Task Flow Template</th>  
         <th nowrap="nowrap">Watermarking Template</th>  
         <th nowrap="nowrap">Video Cover</th>  
     </tr>
     <tr>      
         <td>Transcode using a common template</td>   
         <td>If you select "Transcode using a default template" as the processing type, the parameter is **transcoding template** <br/>No action is required, and all existing transcoding templates are selected by default</td>   
         <td>Select **No watermark** or **Default watermark**</td>   
         <td>Select whether to use the first frame as the video cover</td>
     </tr> 
     <tr>      
         <td>Manually select a template for transcoding</td>   
         <td><td>If you select "Manually select a template for transcoding" as the processing type, the parameter is **Transcoding Template** <br/>Please manually select one or more existing transcoding templates</td>   
         <td>No action is required, and all existing transcoding templates are selected by default</td>   
         <td>Select whether to use the first frame as the video cover</td>
     </tr> 
     <tr>      
         <td>Task Flow</td>   
         <td>If you select "Task Flow" as the processing type, the parameter is **Task Flow Template** <br/>Please select an existing task flow</td>   
         <td>-</td>   
         <td>-</td>
     </tr> 
</table>
4. Click **Upload Now**.
   It takes several minutes to upload a video. You can view the upload progress in **Media Assets** > **Uploading**. After videos are successfully uploaded, you can view and manage all of them in **Media Assets** > **Uploaded**.

#### URL Upload

1. Select **URL Upload** and click **Add a row** in the upload list zone.
  ![](https://main.qcloudimg.com/raw/24fb5618293843de14eb55d6bc417764.png)
2. Enter the information of the source video to be uploaded. Each row represents a video. You can add multiple videos by repeatedly clicking **Add a row** in the upload list zone.
 - Video resource URL: Required. Please enter the URL information of the source video.
 - Video name: Required. Please enter the name of the source video.
 - MD5 (optional): Optional. If you need to set it, please enter the `MD5` value.
 - Priority: Optional. You can select **High**, **Medium**, or **Low**.
3. Click **Upload Now** to upload the video.
   It takes several minutes to upload a video. You can view the upload progress in **Media Assets** > **Uploading**. After videos are successfully uploaded, you can view and manage all of them in **Media Assets** > **Uploaded**.

### Deleting a Video

> A deleted video is **non-recoverable**. It will be completely removed from Tencent Cloud and will not be accessible from CDN nodes. Please be sure before deleting a video.

You can delete the unwanted video files to free up storage space in the following ways:
- Single delete: Click **Delete** in the row of the target video file and click **OK** in the **Delete Video** dialog box to delete it.
  ![](https://main.qcloudimg.com/raw/fb1f31b96bc458c453b96ce51691c407.png)
- Batch delete: Select the target video files, click **Delete** above the files, and click **OK** in the **Delete Video** dialog box to delete all selected videos.
  ![](https://main.qcloudimg.com/raw/545906da3cbe64294a2c599435a58cb5.png)

### Processing a Video

You can select one or more target video files, click **Video Processing** above the files, configure video processing parameters according to the table below and click **OK**.

<table>
     <tr>
         <th nowrap="nowrap">Processing Type</th>  
         <th nowrap="nowrap">Transcoding/Task Flow Template</th>  
         <th nowrap="nowrap">Watermarking Template</th>  
         <th nowrap="nowrap">Video Cover</th>  
     </tr>
     <tr>      
         <td>Transcode using a common template</td>   
         <td>If you select "Transcode using a default template" as the processing type, the parameter is **transcoding template** <br/>No action is required, and all common transcoding templates are selected by default</td>   
         <td>Select **No watermark** or **Default watermark**</td>   
         <td>Select whether to use the first frame as the video cover</td>
     </tr> 
     <tr>      
         <td>Manually select a template for transcoding</td>   
         <td>If you select "Manually select a template for transcoding" as the processing type, the parameter is **Transcoding Template** <br/>Please manually select one or more common transcoding templates</td>   
         <td>No action is required, and all existing transcoding templates are selected by default</td>   
         <td>Select whether to use the first frame as the video cover</td>
     </tr> 
     <tr>      
         <td>Task Flow</td>   
         <td>If you select "Task Flow" as the processing type, the parameter is **Task Flow Template** <br/>Please select an existing task flow</td>   
         <td>-</td>   
         <td>-</td>
     </tr> 
</table>

![](https://main.qcloudimg.com/raw/9696132af45a77daec128bf2ee6c0d69.png)

### Modifying a Video Category

Categories allow you to organize your video files. If you need to modify the category for your video, select the files, click **Modify Video Category** above the files, move the files to the desired category, and click **OK**.
![](https://main.qcloudimg.com/raw/7a8c1eb2824ed5b086769fa13122a44f.png)

For more information about how to manage categories, see [Category Management](https://cloud.tencent.com/document/product/266/14059).

### Filtering Videos by Creation Time

You can filter the uploaded files by creation time:
- Select **All Times** to display all video files by default.
- Select **Customize Times**, set the time period, and click <img src="https://main.qcloudimg.com/raw/7d1947c897c2392e42b59cb70fb1ac17.png"  style="margin:0;"> to display the video files created in the specified time period.
 ![](https://main.qcloudimg.com/raw/55e0635e575ba6a2b080e4c8740f0003.png)

### Quick Access to Video Information

When you move the cursor to the row of a video file, **Quick View** will appear below the video ID. Click **Quick View** and the information window of the video file will appear on the right.
- You can view information about the video in this window, including ID, category, size, duration, creation time, updated time, and description.
- You can also copy the video URL in this window for video processing and playback.

![](https://main.qcloudimg.com/raw/980d7298b9feb113a3ad7f08723d7b32.png)

### Managing a Video

Click **Manage** in the row of the target video file to go to the video management page.

#### Basic Information

On the **Basic Info** page, you can view and edit basic information of the video.
![Basic Info](https://main.qcloudimg.com/raw/7c3d4730127280f7bbacabd7fe6f74e2.png)
Click **Edit** and you can edit the following fields:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Video cover | When you upload a video, a cover will be automatically generated. You can customize the cover by clicking **Change Image** to select and upload a local image. |
| Video name| You can rename the video. A video name can contain up to 20 characters and cannot contain " ' < >. |
| Category | You can change the category of the video. Click **Modify Category**, select the desired category, and click **OK**. |
| Tags | You can set tags for your video files. A tag can contain up to 16 digits, letters or Chinese characters, and multiple tags should be separated by spaces. |
| Description | You can add a simple description to the video with a maximum of 128 characters.                |

> ! Video Cover File Restrictions:
> - Only images in JPG, static GIF, and PNG formats are supported.
> - The image cannot exceed 1 MB in size or 1920 × 1080 in dimensions.
> - The image name cannot contain Chinese characters.

![Edit information](https://main.qcloudimg.com/raw/cf987d2da1f71f344e8a9db7e4e9f111.png)

#### Video Publishing

The URL of a video source file corresponds to a video file of a specific bitrate which does not contain any player information itself. It can be opened directly in a browser and played by a browser or the operating system's built-in player.
On the **Video Publishing** page, you can view the basic information of the video release, copy the URL of the video source file, preview the video, and apply for video link release in your WeChat Official Account. For .mp4 files in SD, you can also get a QR code.

![](https://main.qcloudimg.com/raw/2bb2797edad766d4ef7d28af43611853.png)

#### Web Player Code Generation

 On the **Web Player Code Generation** page, you can manage the player information and web player code.
![](https://main.qcloudimg.com/raw/d8bb878eb86280557d6a4043b1cfcc68.png)

- In the **Parameter Settings** section, you can click **Edit** on the right of **Player**, choose a player in the drop-down box, and click **OK**.
- In the **Web Player Code** section, you can choose the appropriate video resolution in the drop-down box, turn Autoplay on or off as needed, and set **Code Type** to **HTML** or **IFRAME**.
  The web player code corresponding to the specified parameters will be generated in the code output box, which can be copied by clicking **Copy Code**.

## Uploading

Log in to the [VOD Console](https://console.cloud.tencent.com/video), click **Media Assets** in the left sidebar, and select the **Uploading** tab where you can view the information of local videos being uploaded to the VOD console. In the video list, you can view the file name, name, size, category, processing, upload time, and status of a video. Statuses includes uploading, uploaded, and failed.
![](https://main.qcloudimg.com/raw/c5d8a5c27551d18b8cc6c55594d83be2.png)

