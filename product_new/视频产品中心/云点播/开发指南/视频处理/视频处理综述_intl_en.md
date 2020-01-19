Video processing is a process in which a source video is analyzed or processed to generate a new video.

<table>
    <tr>
        <th style="width:15%">
            Category                
        </th>
        <th style="width:15%">
            Name                
        </th>
        <th>
            Description
        </th>
    </tr>
    <tr>
    <tr>
        <td rowspan=2>
            Video production                
        </td>
        <td>
            Video editing             
        </td>
        <td>
				<li>Clipping: cuts a clip out of a video to generate a new video. </li><li>Splicing: splices multiple videos to generate a new video.</li>
        </td>
    </tr>
        <td>
            Video composing
        </td>
        <td>
            Manipulates media files through operations such as clipping, splicing, overlaying, and flipping to achieve effects such as audio mixing, audio extraction, and picture-in-picture.
        </td>
    </tr>
    <tr>
        <td rowspan=6>
            Video conversion                
        </td>
        <td>
            Transcoding               
        </td>
        <td>
            Transcodes a video to a new one in the specified format and with the specified resolution.
        </td>
    </tr>
    <tr>
        <td>
            Screencapturing               
        </td>
        <td>
            Screencaptures a video at the specified time point or interval.
        </td>
    </tr>
    <tr>
        <td>
            Watermarking               
        </td>
        <td>
            Adds a text or image watermark to a video during transcoding.
        </td>
    </tr>
    <tr>
        <td>
            Animated image generating               
        </td>
        <td>
            Converts a video segment into an animated image in GIF or WEBP format.
        </td>
    </tr>
    <tr>
        <td>
            Adaptive bitrate streaming               
        </td>
        <td>
            Transcodes a video to adaptive bitstream in HLS or Dash format.
        </td>
    </tr>
    <tr>
        <td>
            Video encryption               
        </td>
        <td>
            Encrypts a video by using commercial-grade DRM (FairPlay or Widevine)
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            Video AI                
        </td>
        <td>
            Video content audit               
        </td>
        <td>
           Intelligently audits video content (detects porn and politically sensitive information).
        </td>
    </tr>
    <tr>
        <td>
            Video content analysis               
        </td>
        <td>
            Intelligently analyzes video content (e.g., categorization, tagging, and cover generating).
        </th>
    </tr>
    <tr>
        <td>
            Video content recognition                
        </td>
				<td>
				    Intelligently recognizes video content (e.g., faces, speech, and text).
				</td>
		<tr>        
        </th>
    </tr>
</table>

The above is a list of video processing features provided by VOD. In addition to a range of basic processing capabilities such as transcoding, screencapturing, and watermarking, VOD also has the following two distinctive capabilities:
- intelligent content audit, analysis, and recognition with the aid of Tencent Cloud's powerful AI.
- integration with commercial-grade DRM for high-level video encryption.

After a video processing task is initiated, the processing result cannot be output immediately (i.e., the result cannot be obtained synchronously). Therefore, video processing is performed as an offline task. For more information on how to initiate a video processing task and get the task result, please see [Video Processing Task System](https://cloud.tencent.com/document/product/266/33475).
