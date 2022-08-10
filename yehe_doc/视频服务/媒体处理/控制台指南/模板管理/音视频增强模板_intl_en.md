MPS provides preset audio/video enhancement templates, which can be added directly to a scheme. You can also click **Create template** to customize your own audio/video enhancement templates.

<table>
<thead>
<tr>
<th width=13%>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Template name</td>
<td>Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).</td>
</tr>
<tr>
<td> Container format </td>
<td>MP4, FLV, or HLS</td>
</tr>
<tr>
<td>Type</td>
<td>Video or audio enhancement. Only video enhancement is supported currently.</td>
</tr>
<tr>
<td>Encoding standard</td>
<td>H264, H265, or AV1</td>
</tr>
<tr>
<td>Resolution</td>
<td>You can either specify the long and short sides or width and height of the output video. The valid values are `0` and [128, 4096]. `0` means to keep the dimension the same as the original.</td>
</tr>
<tr>
<td>Frame rate</td>
<td>[0, 100]. `0` means to keep the frame rate the same as the original.</td>
</tr>
<tr>
<td>Super resolution</td>
<td>High resolution model (default) or low resolution model</td>
</tr>
<tr>
<td>Low-light enhancement</td>
<td>Enhance details and contrast in low-light scenes to improve visual experiences.</td>
</tr>
<tr>
<td>HDR</td>
<td>HDR10 or HLG, which delivers a wider color range and more color details.</td>
</tr>
<tr>
<td>Overall enhancement</td>
<td>Leverage AI technologies to balance image textures, remove artifacts, smooth video images, and enhance image details to improve visual experiences.</td>
</tr>
<tr>
<td>Color enhancement</td>
<td>Make colors more real and enhance colors to some degree to improve visual experiences.</td>
</tr>
<tr>
<td>Detail enhancement</td>
<td>Enhance details in videos and increase the clarity of videos.</td>
</tr>
<tr>
<td>Face enhancement</td>
<td>Enhance key facial features based on face recognition technologies.</td>
</tr>
<tr>
<td>Banding removal</td>
<td>Remove banding and reduce noise in videos.</td>
</tr>
<tr>
<td>Smoothing</td>
<td>The compression of videos during transcoding may result in blocking artifacts, ringing artifacts, mosquito noise, and color contamination. This feature fixes such issues.</td>
</tr>
<tr>
<td>Image noise removal</td>
<td>Reduce the noise introduced during the video capturing process without losing details.</td>
</tr>
</tbody></table>