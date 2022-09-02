## Overview

Media decryption refers to piracy where an unencrypted media file is sent to a third-party player for unauthorized playback or an encrypted media file is maliciously cracked, and the source content is played back in a third-party player. VOD offers HLS private encryption and commercial-grade DRM, both of which can effectively prevent various cracking behaviors and safeguard media copyrights.

<table ><thead ><tr>
<th style="width:150px" >Feature</th><th >Description</th><th >Security Level</th><th >Player Compatibility</th></tr>
</thead><tbody ><tr>
<td>HLS private encryption</td>
<td>VOD's proprietary media content encryption solution. The content key is protected by Tencent Cloud's private protocol.</td>
<td>High: It effectively prevents videos from being decrypted by various browser extensions and cracking tools.</td>
<td>High: It supports playback on almost all mainstream devices.</td>
</tr>
<tr>
<td>Commercial-grade DRM</td>
<td>The copyright protection system promoted by Apple (FairPlay) and Google (Widevine). The content key is protected by the protocol designed in the DRM system.</td>
<td>Very high: It is a hardware-level encryption/decryption solution and can meet the requirements of movie and TV content providers outside the Chinese mainland.</td>
<td>Average: It is highly compatible with iOS, but isn't supported by some Android devices.</td>
</tr>
</tbody>
</table>



## Use cases

<table ><thead ><tr>
<th style="width:150px">Scenario</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Online education</td>
<td>Teaching and training courses incur high production costs and have high requirements for anti-cracking and anti-piracy.<li>If your courses demand high playback device compatibility, we recommend you use HLS private encryption.</li>
<li>If you need very high security at the expense of the compatibility with some devices, you can consider using commercial-grade DRM.</li>
</td>
</tr>
<tr>
<td>Copyrighted TV series</td>
<td>TV series are provided by professional copyright holders, and copyright protection is generally a requirement for this type of content.<li>For TV series produced in the Chinese mainland, we recommend you use HLS private encryption.</li>
<li>If a copyright holder outside the Chinese mainland requires DRM protection, we recommend you use commercial-grade DRM.</li>
</td>
</tr>
</tbody>
</table>



## Directions

* For how to use HLS private encryption, see [HLS Private Encryption](https://intl.cloud.tencent.com/document/product/266/46780).
* For how to use commercial-grade DRM, see [DRM Encryption](https://intl.cloud.tencent.com/document/product/266/46658).
