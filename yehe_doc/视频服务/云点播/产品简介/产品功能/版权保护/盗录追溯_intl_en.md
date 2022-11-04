## Overview

Unauthorized video recording is the main form of video piracy. Pirates often use screen recording software to record the video, and may even use a camera to directly record their screen and then distribute the video to others.
One of the most effective ways to suppress and deter unauthorized video recording is to track down pirates and hold them liable or demand compensation from them.
VOD allows you to add common image/text watermarks, player-based floating watermarks, or digital watermarks to videos for piracy tracking.

<table ><thead ><tr>
<th style="width:150px">Feature</th><th >Description</th><th >Characteristics</th></tr>
</thead><tbody ><tr>
<td>Common image and text watermark</td>
<td>An image or text watermark is encoded into the video during transcoding.</td>
<td>High security, high costs, low robustness, compromised viewing experience:<li>Security: The watermark is encoded into the video, which guarantees a high security.</li>
<li>Costs: An individual watermark needs to be added for each viewer. Therefore, multiple transcoded replicas are required, which incur high costs.</li>
<li>Robustness: The watermark is at a fixed position, which makes it easy to crop it out or cover it.</li>
<li>Viewing experience: The watermark affects viewing experience to some extent.</li>
</td>
</tr>
<tr>
<td>Player-based floating watermark</td>
<td>The player places a watermark image layer over the source video during playback.</td>
<td>Low security, low costs, low robustness, and compromised viewing experience:<li>Security: Because the watermark is added as an image layer, a pirate can remove it and get the source video, making the security level relatively low.</li>
<li>Costs: The watermark is added by the player, which is cost-effective.</li>
<li>Robustness: The watermark is at a fixed position, which makes it easy to cover it.</li>
<li>Viewing experience: The watermark affects viewing experience to some extent.</li>
</td>
</tr>
<tr>
<td>Digital watermark</td>
<td>The watermark is encoded into the video, and user ID can be extracted from a pirated video to track the pirate.</td>
<td>High security, high costs, high robustness, excellent viewing experience:<li>Security: The watermark is encoded into the video, which guarantees a high security.</li>
<li>Costs: Each watermarked video is charged only once for transcoding and storage, which is cost-effective.</li>
<li>Robustness: Works under different conditions (resampling, compression, dithering, cropping, scaling, rotation, wave filtering, and so on.)</li>
<li>Viewing experience: The watermark does not affect the video quality and is invisible to the human eye.</li>
</td>
</tr>
</tbody>
</table>

We recommend using a digital watermark or using a digital watermark and player floating watermark together, so as to achieve both high security and low costs for piracy tracking.

## Use Cases
<table ><thead ><tr>
<th style="width:150px">Scenario</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Online education</td>
<td>Teaching and training courses incur high production costs. Therefore, we recommend you use a digital watermark to prevent piracy and also consider using player floating watermark.</td>
</tr>
<tr>
<td>Confidential video</td>
<td>For confidential videos, we recommend you use digital watermarks to deter unauthorized recording and distribution. You can consider adding both digital watermarks and player-based floating watermarks.</td>
</tr>
<tr>
<td>Copyrighted TV series</td>
<td>TV series are protected by copyright. We recommend you add the logo of the copyright holder or the content providing platform as a common text/image watermark to the videos and at the same time use digital watermarks to prevent piracy.</td>
</tr>
</tbody>
</table>


## Directions

* For more information on how to use common image and text watermarks, see [Watermarking](https://intl.cloud.tencent.com/document/product/266/33939).
* For more information on how to use player-based floating watermarks, see [Integration Guide](https://intl.cloud.tencent.com/document/product/266/33976).
* For more information on how to use digital watermarks, see [Digital Watermark](https://intl.cloud.tencent.com/document/product/266/47920).
