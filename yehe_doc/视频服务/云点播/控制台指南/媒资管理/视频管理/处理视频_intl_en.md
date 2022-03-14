## Overview
This document describes how to process videos in the VOD console, such as transcoding, watermarking, and auditing videos.

## Directions
1. Log in to the VOD console and select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**. The "Uploaded" page is displayed.
2. Select one or more target video files, click **Process Video** above the list, configure video processing parameters in the "Process Video" pop-up window according to the table below, and click **Confirm** to start executing the video processing task.
![](https://qcloudimg.tencent-cloud.cn/raw/2f3e527fc7a03ece7ffa5a9bbee0fdaf.png)

<table>
     <tr>
         <th nowrap="nowrap">Processing Type</th>  
         <th nowrap="nowrap">Transcoding/Audit/Task Flow Template</th>  
         <th nowrap="nowrap">Watermark Template</th>  
         <th nowrap="nowrap">Video Cover</th>  
     </tr>
	 <tr>      
         <td>Transcoding</td>   
	     <td>If <b>Transcoding</b> is selected as the processing type, this parameter is <b>Transcoding Template</b><ul><li>Click <b>Transcoding Template</b> to select an existing template<li>Click <b>Common Template</b> to select a common template</ul></td>   
	     <td nowrap="nowrap"><ul><li>Select <b> No watermark</b> <li>Select <b>Default watermark</b> <li>Select <b>Select watermark</b></td>   
	     <td>Select whether to use the first frame as the video cover</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Adaptive bitrate streaming</td>   
	     <td>If <b> Adaptive Bitrate Streaming</b> is selected as the processing type, this parameter is <b>Transcoding Template</b>: multiple transcoding templates can be selected</td>   
	     <td><ul><li>Select <b> No watermark</b> <li>Select <b>Default watermark</b> <li>Select <b>Select watermark</b></td>   
	     <td>Select whether to use the first frame as the video cover</td>
     </tr> 
	 <tr>      
         <td>Video audit</td>   
	     <td>If <b> Video Audit</b> is selected as the processing type, this parameter is <b>Audit Template</b>: select an existing audit template </td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
		  <tr>      
         <td>Task flow</td>   
	     <td>If <b> Task Flow</b> is selected as the processing type, this parameter is <b>Task Flow Template</b>: select an existing task flow template </td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
	     </tr> 
</table>

>?For more information on the template and task flow settings, please see [Video Processing Settings](https://intl.cloud.tencent.com/document/product/266/14059).






