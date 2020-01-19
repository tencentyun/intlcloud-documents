## Operation Scenarios
This document describes how to upload videos through the VOD Console, including local upload and video pull. 

> 
> - Formats such as WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, and RMVB are supported.
- During upload, you can switch to another page of the VOD Console, but do not close the browser to access the console of another product; otherwise, the upload will be interrupted.
- Web upload supports resuming and queuing in Chrome. Web upload is supported in Internet Explorer 10+ or higher and Chrome.


## Local Upload Directions

1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview), click **Media Assets** on the left sidebar to enter the "Uploaded" page by default, and click **Upload Video** to enter the "Upload Video" page.
2. Select **Local Upload** to upload a local file to the console. Click **Select Video** to select a local video file or drag and drop the file to the upload list zone.
 > Batch upload is supported. You can upload up to 5 videos at a time, and all the selected videos will be displayed in the upload list.
3. In the upload list, you can check the filename and size of a selected video, change its name and category, or delete it.
4. You can choose whether to process the uploaded video.
   - If no processing is needed, select **No Processing After Upload**.
   - If processing is needed, select **Automatic Processing After Upload** and configure video processing parameters according to the table below.
   <table>
     <tr>
         <th nowrap="nowrap">Processing Type</th>  
         <th nowrap="nowrap">Transcoding/Audit/Task Flow Template</th>  
         <th nowrap="nowrap">Watermarking Template</th>  
         <th nowrap="nowrap">Video Cover</th>  
     </tr>
	 <tr>      
         <td>Transcoding</td>   
	     <td>When **Transcoding** is selected as the processing type, this parameter is "<b>Transcoding Template</b>" <ul><li> If **General Transcoding Template** is selected in the drop-down list on the left, the default template will be selected in the drop-down list on the right automatically <li>If **Select Transcoding Template** is selected in the drop-down list on the left, multiple transcoding templates can be selected in the drop-down list on the right </ul></td>   
	    <td nowrap="nowrap"><ul><li>Select **No watermark** <li>Select **Default watermark** <li>Select **Select Watermarking Template**</td>   
	     <td>Select whether to use the first frame as the video cover</td>
     </tr> 
		<tr>      
         <td>Video audit</td>   
	     <td>If **Video Audit** is selected as the processing type, this parameter is <b>"Audit Template": </b><br>select an existing audit template </ul></td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
		 </tr>
		   <tr>      
         <td>Task flow</td>   
	     <td>If **Task Flow** is selected as the processing type, this parameter is <b>"Task Flow Template": </b><br>select an existing task flow template </ul></td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
</table>
5. Click **Upload Now** to start uploading the video.
 
## Video Pull Directions
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview), click **Media Assets** on the left sidebar to enter the "Uploaded" page by default, and click **Upload Video** to enter the "Upload Video" page.
2. Select **Video Pull** to pull a video from the video URL to the console. Click **Add a row** in the upload list zone.
3. Enter the information of the source video to be uploaded. Each row represents a video. You can add multiple videos by repeatedly clicking **Add a row** in the upload list zone.
 - Video Resource URL: enter the URL information of the source video.
 - Video Name: enter the name of the source video.
 - MD5 (optional): if you need to set it, enter the `MD5` value.
 - Priority: you can select **High**, **Middle**, or **Low**.
4. Click **Upload Now** to upload the video.

>It takes several minutes to upload a video. You can view the upload progress in **Media Assets** > **Uploading**. After videos are successfully uploaded, you can view and manage all of them in **Media Assets** > **Uploaded**.
	
