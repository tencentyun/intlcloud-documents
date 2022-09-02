## Overview

Hotlinking refers to a media playback URL from one site being added to another site where it can be played back by non-authorized viewers. It not only threatens the security of copyrighted media but also consumes the CDN bandwidth and traffic of the victim.
VOD hotlink protection can prevent hotlinking based on referer and key.

<table>
   <tr>
      <th style="width:150px">Category</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan="1"><nobr>Referer hotlink protection</td>
      <td>Source page address control</td>
			<td>The referer mechanism based on HTTP identifies the request source through the referer field in the playback request header. You can add specified domain names to a blocklist or allowlist, based on which the CDN node will authenticate to allow or deny the playback requests accordingly.</td>
   </tr>
   <tr>
      <td rowspan="3"><nobr>Key hotlink protection</td>
      <td>URL validity period control</td>
      <td>You can specify the expiration time of a video URL. When the requested video URL expires, the video can no longer be played back. In this way, you can set a validity period for the video URL to prevent malicious users from transferring the URL to other websites for long-term use.</td>
   </tr>
   <tr>
      <td>Viewer count control</td>
      <td>You can specify the number of viewers that can access the video URL. Devices that are not on the same private network generally have different public IPs. You can specify how many viewers are allowed to access a URL by limiting the number of IPs allowed for playback on the URL. This helps prevent unlimited unauthorized viewing if a video URL is maliciously transferred to other websites.</td>
   </tr>
   <tr>
      <td>Video playback duration control</td>
      <td>You can specify the preview duration in a video URL (for example, the first five minutes of a video) to implement preview for non-paying users.</td>
   </tr>
</table>

## Use cases
<table ><thead ><tr>
<th style="width:150px" >Scenario</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Protection for proprietary videos</td>
<td>Some video providers want to make their high-value videos playable only on their own platforms. In this case, they can use referer and key hotlink protection to prevent video links from being stolen by others and played back on other platforms.</td>
</tr>
<tr>
<td>Malicious video hosting prevention</td>
<td>On UGC platforms, malicious users may upload videos irrelevant to the platform’s topic and deliver them by using the platform links, essentially using the platform as a free video hosting service. You can use hotlink protection to prevent this problem. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/266/37545" >How to Prevent Malicious Video Hosting</a>.</td>
</tr>
<tr>
<td>Video previews</td>
<td>Key hotlink protection allows you to implement video previews, so users can view a several minute-long preview of a video before they pay for the full video.</td>
</tr>
</tbody>
</table>


## Directions

* For detailed directions on referer hotlink protection, see [Referer Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33985).
* For detailed directions on key hotlink protection, see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986).
