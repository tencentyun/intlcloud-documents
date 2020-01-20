## Operation Scenarios
This document describes how to process videos in the VOD Console, such as transcoding, watermarking, and auditing videos.

## Directions
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Media Assets** on the left sidebar to enter the "Uploaded" page by default.
2. Select one or more target video files, click **Process Video** above the list, configure video processing parameters in the "Process Video" pop-up window according to the table below, and click **OK** to start executing the video processing task.
![](https://main.qcloudimg.com/raw/e38db4214a5d6e8e33ae3de26a2acc11.png)
<table>
     <tr>
         <th nowrap="nowrap">Processing Type</th>  
         <th nowrap="nowrap">Transcoding/Audit/Task Flow Template</th>  
         <th nowrap="nowrap">Watermarking Template</th>  
         <th nowrap="nowrap">Video Cover</th>  
     </tr>
	 <tr>      
         <td>Transcoding</td>   
	     <td>If <b>Transcoding</b>> is selected as the processing type, this parameter is <b>"Transcoding Template"</b> <ul><li> If <b>Common Transcoding Template</b>> is selected in the drop-down list on the left, the default template will be selected in the drop-down list on the right automatically <li>If <b>Select Transcoding Template</b>> is selected in the drop-down list on the left, multiple transcoding templates can be selected in the drop-down list on the right </ul></td>   
	     <td nowrap="nowrap"><ul><li>Select <b>No Watermark</b>> <li>Select <b>Default Watermark</b> <li>Select <b>Select Watermarking Template</b>></td>   
	     <td>Select whether to use the first frame as the video cover</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Transcoding to adaptive bitrate streaming</td>   
	     <td>If <b>Transcode to Adaptive Bitrate Streaming</b>> is selected as the processing type, this parameter is <b>"Transcoding Template"</b>: multiple transcoding templates can be selected</td>   
	     <td><ul><li>Select <b>No Watermark</b>> <li>Select <b>Default Watermark</b>> <li>Select <b>Select Watermarking Template</b>></td>   
	     <td>Select whether to use the first frame as the video cover</td>
     </tr> 
	 <tr>      
         <td>Video audit</td>   
	     <td>If <b>Video Audit</b>> is selected as the processing type, this parameter is <b>"Audit Template"</b>: select an existing audit template </td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
		  <tr>      
         <td>Task flow</td>   
	     <td>If **Task Flow** is selected as the processing type, this parameter is <b>"Task Flow Template"</b>: select an existing task flow template </td>   
	     <td align="middle">-</td>   
	     <td align="middle">-</td>
     </tr> 
	     </tr> 
</table>

>For more information on the template and task flow settings, please see [Video Processing Settings](https://intl.cloud.tencent.com/document/product/266/14059).



