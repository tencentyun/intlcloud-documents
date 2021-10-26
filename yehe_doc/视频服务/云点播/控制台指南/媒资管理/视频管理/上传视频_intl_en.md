## Overview
This document describes how to upload videos through the VOD Console, including local upload and video pull.

>! 
>- Formats such as WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, and RMVB are supported.
>- During upload, you can switch to another page of the VOD Console, but do not close the browser to access the console of another product; otherwise, the upload will be interrupted.
>- Web upload supports checkpoint restart and queuing upload in Chrome. Web upload is supported in Chrome and Internet Explorer 10 or higher.


## Local Upload

1. Log in to the VOD Console and select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** to enter the "Uploaded" page by default.
2. Click **Upload Video** to enter the "Upload Video" page.
![](https://qcloudimg.tencent-cloud.cn/raw/50c01e2bc231a24b497310b876dc0d3f.png)
3. Select **Local Upload** to upload a local file to the console. Click **Select Video** to select a local video file or drag and drop the file into the upload list zone.

4. In the upload list, you can check the filename and size of a selected video, modify its name and category, or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/2b5afcb82c221fffcffeaf5f2b1565b3.png)
5. You can choose whether to process the uploaded video.
   - If no processing is needed, select **No Processing After Upload**.
   - If processing is needed, select **Automatic Processing After Upload** and configure video processing parameters according to the table below.

   <table>
     <tr>
         <th nowrap="nowrap">Processing Type</th>  
         <th nowrap="nowrap">Transcoding/Audit/Task Flow Template</th>  
         <th nowrap="nowrap">Watermark Template</th>  
         <th nowrap="nowrap">Video Cover</th>  
     </tr>
	 <tr>      
         <td>Transcoding</td>   
	     <td>If <b>Transcoding</b> is selected as the processing type, this parameter is <b>"Transcoding Template"</b><ul><li>Click <b>Transcoding Template</b> to select an existing template<li>Click <b>Common Template</b> to select a common template</ul></td>   
	     <td nowrap="nowrap"><ul><li>Select <b>No watermark</b> <li>Select <b>Default watermark</b> <li>Select <b>Select watermark template</b></td>   
	     <td>Select whether to use the first frame as the video cover</td>
     </tr> 
	 <tr>      
         <td>Video audit</td>   
	     <td>If <b>Video Audit</b> is selected as the processing type, this parameter is <b>"Audit Template"</b>: select an existing audit template </td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
		  <tr>      
         <td>Task flow</td>   
	     <td>If <b>Task Flow</b> is selected as the processing type, this parameter is <b>"Task Flow Template"</b>: select an existing task flow template </td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
	     </tr> 
</table>

5. Click **Upload** to start uploading the video.

## Video Pull

### Pulling by row
1. Log in to the VOD Console and select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** to enter the "Uploaded" page by default.
2. Click **Upload Video** to enter the "Upload Video" page.
3. Select **Pull Video** to pull a video from the video URL to the console. Click **Add a row** in the upload list section.
4. Enter the information of the source video to be uploaded. Each row represents a video. You can add multiple videos by repeatedly clicking **Add a row** in the upload list zone.
 - Video URL: enter the URL information of the source video.
 - Video Name: enter the name of the source video.
 - Cover URL: enter the URL of the cover to be pulled.
 - Category: select a video category.
5. Click **Pull Video** to upload the video.
![](https://qcloudimg.tencent-cloud.cn/raw/60135e118c111a8ec917a4e72d8f5677.png)

>?It takes several minutes to upload a video. You can view the upload progress in **Video Management** > **Uploading**. After videos are successfully uploaded, you can view and manage all of them in **Video Management** > **Uploaded**.



### Pulling in batches

With the batch pull feature, you can upload a TXT or CSV list, and VOD will directly parse the files in the list into the video pull list.
You need to fill in the TXT or CSV file in the specified format, which can be viewed by downloading the **Sample File**. The columns are as detailed below:

| Column 1 | Column 2 | Column 3 |
|---------|---------|---------|
| Video Resource URL | Video Name | Video Cover URL|

- TXT file: columns should be separated by commas.
- CSV file: columns should be separated by commas (you can directly fill in the table columns in the CSV file).

>?
>- The columns are video resource URL, video name, and video cover URL, respectively. **Please fill in the columns in sequence.**
>- After the list is parsed, please check whether there are any errors and upload after confirmation.
