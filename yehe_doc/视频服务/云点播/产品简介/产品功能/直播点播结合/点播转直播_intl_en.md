## Overview
Based on VOD’s playback control capability, VOD-to-CSS (pseudo-live streaming) adds access controls of "playback time constraint" and "syncing playback progress" to implement pseudo-live streaming. You first generate VOD files, and then specify a time point to use such files for pseudo-live streaming, which incurs lower risks and costs compared with real live streaming. Ongoing pseudo-live streaming cannot be sped up. This feature is commonly used in live courses, live gala, and other scenarios of radio and TV. It has the following strengths:
<table>
    <tr>
        <th style="width:150px">
            Strength              
        </th>
				<th>
           Description
        </th>
    </tr>
		 <tr>
        <td>
            Low development costs
        </td>
				<td>
				To convert a VOD video to a common live stream for delivery, you need to use OBS software to push the video to the live streaming system and integrate with the entire system, which incurs high development costs. In contrast, pseudo-live streaming can be implemented within the VOD platform as long as transcoding and hotlink protection are enabled.
        </td>
 </tr>
 <tr>
        <td>
            Low non-compliance risks
        </td>
				<td>
				Pseudo-live streaming enables you to moderate and edit VOD files in advance to avoid non-compliance risks during live streaming, so as to improve the live streaming quality.
        </td>
	</tr>
	<tr>
        <td>
            Easy and flexible use
        </td>
				<td>
				<li>No live rooms are needed, and any videos can be used for pseudo-live streaming.</li>
				<li>There is no upper limit on concurrency. You can specify a start time of the pseudo-live stream and distribute the playback URL in advance.</li>
        </td>
	</tr>
</table>

## Use cases
Psuedo-live streaming is mainly used in when videos need to be recorded in advance and then live streamed to concurrent viewers at a later scheduled time. Users can get the playback URL in advance but cannot watch the video before the scheduled time. This is useful for scenarios such as online education, event live streaming, and esports events.

<table>
    <tr>
        <th style="width:150px">
            Scenario              
        </th>
				<th>
           Description
        </th>
    </tr>
		 <tr>
        <td>
            Online education platforms
        </td>
				<td>
				A validity period can be set for the playback URL of a recorded video to urge students to study promptly (the video cannot be watched once the URL expires, or students need to pay again to get a new playback URL). A released URL will automatically expire after a certain period of time, so as to protect valuable resources.
        </td>
 </tr>
 <tr>
        <td>
           Radio and TV or OTT
        </td>
				<td>
				Regularly updated variety shows and interview programs can be recorded and edited in advance, and their URLs placed on the preview page, so that the target audience can favorite the page and URLs in advance.
        </td>
	</tr>
	<tr>
        <td>
            Event announcements
        </td>
				<td>
				The event holder can record an event video in advance and then release the playback URL in the event announcement, and viewers will be able to access the video only after the event starts. This allows users to save the URL in advance so they can quickly access it upon the start of the event.
        </td>
	</tr>
</table>

## Directions
For more information, see [How to Make VOD Videos Live Streaming-Like](https://intl.cloud.tencent.com/document/product/266/39442).
