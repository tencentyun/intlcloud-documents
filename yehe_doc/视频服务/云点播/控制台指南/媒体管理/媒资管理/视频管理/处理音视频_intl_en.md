## Overview
This document describes how to transcode, watermark, and moderate audio/video files in the VOD console.

## Directions
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video/Audio Management > Uploaded**.
4. Select one or more files and click **Process** above the list. Configure processing parameters in the pop-up window, and click **Confirm** to start processing.
![](https://qcloudimg.tencent-cloud.cn/raw/85406d3e447f48333f4c67593e17d77a.png)

<table>
     <tr>
         <th nowrap="nowrap">Processing Type</th>  
         <th nowrap="nowrap">Transcoding/Moderation/Task Flow Template</th>  
         <th nowrap="nowrap">Watermark Template</th>  
         <th nowrap="nowrap">Thumbnail</th>  
     </tr>
	 <tr>      
         <td>Transcoding</td>   
	     <td>If the processing type is <b>Transcoding</b>, this will be <b>Transcoding Template</b>.<ul><li>Click <b>Transcoding Template</b> to select an existing template <li> or click <b>Common Template</b> to select a frequently used template.</ul></td>   
	     <td nowrap="nowrap"><ul><li><b>No watermark</b><li><b>Default watermark</b><li><b>Select watermark</b></td>   
	     <td>If you select this, the first frame will be used as the thumbnail.</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Transcoding to adaptive bitrate streaming</td>   
	     <td>If the processing type is <b>Adaptive Bitrate Streaming</b>, this will be <b>Transcoding Template</b>. You can select from the drop-down list multiple templates.</td>   
	     <td><ul><li><b>No watermark</b><li><b>Default watermark</b><li><b>Select watermark</b></td>   
	     <td>If you select this, the first frame will be used as the thumbnail.</td>
     </tr> 
	 <tr>      
         <td>Moderation</td>   
	     <td>If the processing type is <b>Moderation</b>, this will be <b>Moderation Template</b>. Select a moderation template from the drop-down list.</td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
		  <tr>      
         <td>Task Flow</td>   
	     <td>If the processing type is <b>Task Flow</b>, this will be <b>Task Flow Template</b>. Select a task flow template from the drop-down list.</td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
	     </tr> 
</table>

>? For more information on template and task flow settings, see [Audio/Video Processing Settings](https://intl.cloud.tencent.com/document/product/266/14059).





