## Overview

Unauthorized video recording is the main form of video piracy. Pirates can use screen recording software to record and share a pirated video, or they may even use a camera to record their screen directly.
An effective way to suppress unauthorized video recording is to track down pirates and use other means to protect copyrighted content, deter piracy, and demand compensation.
VOD supports common image and text watermarking, player floating watermarking, and digital watermarking to help deter and track down pirates.

<table ><thead ><tr>
<th style="width:150px">Feature</th><th >Description</th><th >Characteristics</th></tr>
</thead><tbody ><tr>
<td>Common image and text watermark</td>
<td>An image or text watermark encoded to the video image during transcoding.</td>
<td>High security and high costs: <li>Security: The watermark is encoded to the image to guarantee a high security.</li>
<li>Costs: An individual watermark needs to be added for each viewer. Therefore, multiple transcoded replicas are required, which incur high costs.</li>
</td>
</tr>
<tr>
<td>Player floating watermark</td>
<td>A watermark covering the video layer during playback in the player.</td>
<td>Low security and low costs:<li>Security: The watermark is just a layer above the video, so the pirate may steal the source video stream, which is insecure.</li>
<li>Costs: The watermark is added by the player, which is cost-effective.</li>
</td>
</tr>
<tr>
<td>Digital watermark</td>
<td>Digital watermarking is implemented based on AB stream technology, transcoding, and delivery: <li>Streams A and B are transcoded from the source video and segmented (the difference between streams A and B is the watermark position).</li>
<li>VOD CDN outputs a unique combined stream for each end user.</li>
<li>The watermark sequences are extracted from the pirated video to track down the user ID of the pirate.</li>
</td>
<td>High security and low costs:<li>Security: The watermark is encoded to the image to guarantee a high security.</li>
<li>Costs: A watermark incurs only the fees of transcoding and storing two streams, which is cost-effective.</li>
</td>
</tr>
</tbody>
</table>


In conclusion, we recommend you use a digital watermark or a digital watermark and player floating watermark together, so as to achieve both high security and low costs for piracy tracking.

## Use cases
<table ><thead ><tr>
<th style="width:150px">Scenario</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Online education</td>
<td>Teaching and training courses incur high production costs. Therefore, we recommend you use digital watermarks to prevent piracy and also consider using player floating watermarks.</td>
</tr>
<tr>
<td>Confidential video</td>
<td>For internal confidential videos that should not be disclosed, we recommend you use digital watermarks to prevent piracy and also use player floating watermarks.</td>
</tr>
<tr>
<td>Copyrighted TV series</td>
<td>TV series are provided by professional copyright owners. We recommend you use common image and text watermarks to add the logo of the platform or copyright holder as a watermark and use digital watermarks to prevent piracy.</td>
</tr>
</tbody>
</table>


## Directions

* For more information on how to use common image and text watermarks, see [Watermarking](https://intl.cloud.tencent.com/document/product/266/33939).
* For more information on how to use player floating watermarks, see [Integration Guide](https://intl.cloud.tencent.com/document/product/266/33976).
* For more information on how to use digital watermarks, see [Digital Watermark](https://intl.cloud.tencent.com/document/product/266/47920).
