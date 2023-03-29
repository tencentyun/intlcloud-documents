This document provides a list of what you can do with CSS. You can find more information about each feature by reading their documents.

### Push
<table>
<tr><th width=17%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968">Push protocol support</a></td><td>Supports push over RTMP and WebRTC.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31558">Push tool support</a></td><td>Supports Tencent Cloud’s MLVB SDK (which comes in iOS, Android, and web editions) or third-party streaming software such as OBS, XSplit, and FMLE.</td></tr>
<tr><td>Push device support</td><td>Supports common third-party RTMP streaming devices, encoders, and set-top boxes.</td></tr>
</table>

### Playback
<table>
<tr><th width=17%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968">Playback protocol support</a></td><td>Supports playback over RTMP, FLV, HLS, and UDP.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31559">Playback tool support</a></td><td>Supports Tencent Cloud’s MLVB SDK (which comes in iOS, Android, and web editions) or third-party FLV, RTMP, or HLS players.</td></tr>
<tr><td>Playback control</td><td>Plays the original stream or a stream transcoded in real time.</td></tr>
</table>

### Live Streaming Management
<table>
<tr><th width=17%>Feature</th><th>Description</th></tr>
<tr><td>Management</td><td>Manages live streams graphically in the console or using APIs.</td></tr>
</table>

### CSS console
<table>
<tr><th width=17%>Section</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31054" target="_blank">Overview</a></td><td>Displays data such as traffic package usage or real-time bandwidth and traffic usage.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/35970">Domain Management</a></td><td>Supports adding, modifying, disabling and deleting push and playback domains, as well as configuring CNAME, HTTPS certificates, and push and playback authentication.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31068">Stream Management</a></td><td>Supports querying live streams in real time as well as querying historical streams.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/34223">Scenario-Specific Services</a></td><td>Supports viewing and modifying recording, transcoding, screencapturing, porn detection, watermarking, and callback configurations.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31076">Data Center</a></td><td>Supports querying usage statistics including bandwidth, traffic, requests, concurrent connections, screenshots, push channels, and recording channels.</td></tr>
</table>

### Security
<table>
<tr><th width=17%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31059">Push authentication</a></td><td>Generates hotlink protection push URLs (you can use your own key and specify the expiration time).</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31060">Playback authentication</a></td><td>Generates hotlink protection playback URLs using IP allowlist/blocklist or the referer field; supports remote playback authentication.</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/267/48068">DRMencryption</a></td><td>Encrypts videos based on DRM schemes including Widevine, FairPlay, or NormalAES to prevent unauthorized recording and hotlinking.</td></tr>
</table>

### APIs
<table>
<tr><th width=17%>API Category</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Domain management APIs</a></td>
<td>Add, delete, query, enable, and disable push and playback domains, as well as modify playback domains.</td>
</tr>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Delayed Playback management APIs</a></td>
<td>Delay playback, query delayed playbacks, and resume real-time playback.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Recording management APIs</a></td>
<td>Create, delete, and end recording tasks, create, delete, query, and modify recording templates, as well as create, delete, and query recording rules.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Screencapturing and Porn Detection APIs</a></td>
<td>Create, delete, and query recording rules, as well as create, delete, query, and modify recording templates.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Watermark management APIs</a></td>
 <td>Add, delete, query, and modify watermarks, as well as create, delete, and query watermark rules.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Live callback APIs</a></td>
<td>Create, delete, and query callback rules, as well as create, delete, query, and modify callback templates.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Stream pulling APIs</a></td>
<td>Add, delete, query, and modify pull configurations.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Live stream management API</a></td>
<td>Query disabled, ongoing, and historical streams, query push interruptions and stream status, stop streams, block streams, and resume streams.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Live transcoding APIs</a></td>
<td>Create, delete, and query transcoding rules, as well as create, delete, query, and modify transcoding templates.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Billing data query APIs</a></td>
<td>Query billable bandwidth and traffic usage, query playback data by region and ISP, query HTTP status codes for playback requests, query domain-level playback data in real time, and query packages.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Certificate management APIs</a></td>
<td>Add, delete, bind, unbind, and query certificates, as well as query and change the domains bound with a certificate.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Authentication management APIs</a></td>
<td>Query and modify authentication keys for playback and push.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Time shifting APIs</a></td>
<td>Create, delete, query, and modify time shifting templates, create, delete, and query time shifting rules, as well as query time-shifted streams.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Live stream mix APIs</a></td>
<td>Mix streams and cancel stream mixing.</td>
</tr>
</table>

### Value-added services
<table>
<tr><th width=17%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31561">Live transcoding</a></td><td>Transcodes a stream into different specifications.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31563">Live recording</a></td><td>Records live streams (by calling an API) and saves the recording files to Tencent Cloud VOD or COS.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31562">Live screencapturing</a></td><td>Takes screenshots of a live stream (by calling an API) and saves them to Tencent Cloud VOD or COS.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31564">Porn detection</a></td><td>Recognizes pornographic content in live streams.</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/1071/42210">RTC-based communication</a></td><td>Supports communication among participants with ultra-low latency (powered by Tencent Cloud TRTC).</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/267/31565">Time shifting (new)</a></td><td>Plays ongoing streams from earlier time points.</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/267/53400">Standby stream</a></td><td>Shows a video or image that becomes active automatically when a live stream is interrupted (CSS will automatically switch back to the primary stream after it is recovered).</td></tr>
</table>

### SDKs
<table>
<tr><th width=17%>SDK</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/1071">MLVB SDK</a></td><td>Offers capabilities including stream pushing, basic beautification, filters, playback, and time shifting.</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/1143">Tencent Effect SDK</a></td><td>Offers capabilities including filters, beautification, stickers, and gesture recognition for different shooting scenarios (the SDK is a video processing solution developed jointly by Tencent Cloud, Pitu, and YouTu).</td></tr>
</table>