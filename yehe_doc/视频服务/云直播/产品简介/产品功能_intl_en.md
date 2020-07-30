This document provides a list of features in LVB. For more information on their descriptions and usage, please see the corresponding documents.



### LVB Push
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968" target="_blank">Push protocol</a></td><td>Supports the RTMP protocol for push.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31558" target="_blank">Push method</a></td><td>Supports applications that are integrated with Tencent Cloud LVB Push SDK for iOS, Android, or web as well as common third-party push software programs such as OBS, XSplit, and FMLE.</td></tr>
<tr><td>Push device</td><td>Supports common third-party RTMP push hardware devices, encoders, and set-top boxes.</td></tr>
</table>


### LVB Playback
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968" target="_blank">Playback protocol</a></td><td>Supports RTMP, FLV, and HLS playback protocols.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31559" target="_blank">Playback method</a></td><td>Supports Tencent Cloud LVB Player SDK for iOS, Android, and web as well as common third-party FLV, RTMP, and HLS players.</td></tr>
<tr><td>Playback control</td><td>Plays back an original stream that has the same specification as the input stream or a stream that is transcoded in real time.</td></tr>
</table>


 ### LVB Management
 <table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td>Management method</td><td>Supports management in the LVB Console graphically or by calling LVB's TencentCloud APIs.</td></tr>
</table>

### LVB Console
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31054" target="_blank">Overview</a></td><td>Displays data such as LVB resource package traffic and real-time LVB bandwidth and traffic. </td></tr>
<tr><td>Domain name management</td><td>Supports adding, modifying, disabling, and deleting LVB push and playback domain names as well as configuring domain name CNAME records, HTTPS certificates, and push and playback authentication.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31068" target="_blank">Live stream management</a></td><td>Supports querying the information of real-time and historical live streams.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/34223" target="_blank">Feature module</a></td><td>Supports querying and modifying the configuration information of LVB recording, transcoding, screencapturing, porn detection, watermarking, and callback.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31076" target="_blank">Statistical analysis</a></td><td>Supports querying the usage statistics of LVB service bandwidth, traffic, requests, concurrent connections, screenshots, channels, and recording channels.</td></tr>
<tr><td>LVB SDK</td><td>Supports querying the MLVB SDK quality monitoring data and MLVB mic connect minutes.</td></tr>
</table>


### LVB Security
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31059" target="_blank">Push authentication</a></td><td>Supports configuring push URL hotlink protection and customizing the authentication key and expiration time.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31060" target="_blank">Playback authentication</a></td><td>Supports hotlink protection based on blacklist, whitelist, Referer, and playback URL as well as remote playback authentication.</td></tr>
</table>

​
### API Management
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.9F.9F.E5.90.8D.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Domain management APIs</a></td>
<td>Used to add domain name, delete domain name, query domain name information, query domain name list, enable domain name, disable domain name, or modify playback domain name information.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.AE.9E.E6.97.B6.E6.97.A5.E5.BF.97.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Real-time log APIs</a></td>
<td>Used to get log URLs in batches.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.BB.B6.E6.92.AD.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Delayed playback management APIs</a></td>
<td>Used to delay playback, get delayed playback list, or resume playback.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.BD.95.E5.88.B6.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Recording management APIs</a></td>
<td>Used to create recording task, create recording rule, create recording template, delete recording task, delete recording rule, delete recording template, get recording rule list, get one single recording template, get recording template list, modify recording template configuration, or terminate recording task.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E6.88.AA.E5.9B.BE.E9.89.B4.E9.BB.84.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Screencapturing and porn detection APIs</a></td>
<td>Used to create screencapturing rule, create screencapturing template, delete screencapturing rule, delete screencapturing template, get screencapturing rule list, get one single screencapturing template, get screencapturing template list, or modify screencapturing template.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E6.B0.B4.E5.8D.B0.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Watermark management APIs</a></td>
<td>Used to add watermark, create watermark rule, delete watermark, delete watermark rule, get one single watermark, get watermark rule list, query watermark list, or update watermark.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E5.9B.9E.E8.B0.83.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">LVB callback APIs</a></td>
<td>Used to create callback rule, create callback template, delete callback rule, delete callback template, get callback rule list, get one single callback template, get callback template list, or modify callback template.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E6.8B.89.E6.B5.81.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">LVB pull APIs</a></td>
<td>Used to add, delete, query, update, or modify status of the live pull configuration.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E6.B5.81.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Live stream management APIs</a></td>
<td>Used to get forbidden stream list, query stream interruption event, query live stream, query historical stream list, query stream status, interrupt live stream, forbid live stream, or resume live stream.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E8.BD.AC.E7.A0.81.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">LVB transcoding APIs</a></td>
<td>Used to create transcoding rule, create transcoding template, delete transcoding rule, delete transcoding template, get transcoding rule list, get one single transcoding template, get transcoding template list, or modify transcoding template configuration.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.BB.9F.E8.AE.A1.E6.9F.A5.E8.AF.A2.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Statistical query APIs</a></td>
<td>Used to query billable LVB bandwidth and traffic data, query playback data by district and ISP, query HTTP playback status code details, query real-time downstream playback data at domain name level, or query LVB package information.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E8.AF.81.E4.B9.A6.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Certificate management APIs</a></td>
<td>Used to bind certificate to domain name, add certificate, delete certificate, get certificate information, get certificate information list, get domain name certificate information, modify certificate, modify domain name-certificate binding information, or unbind domain name from certificate.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E9.89.B4.E6.9D.83.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">Authentication management APIs</a></td>
<td>Used to query playback authentication key, query push authentication key, modify playback authentication key, or modify push authentication key.</td>
</tr>
</table>


### Value-Added Services
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31561" target="_blank">LVB transcoding</a></td><td>Supports transcoding live streams in various specifications.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31562" target="_blank">LVB screencapturing</a></td><td>Supports taking screenshots during live streaming through the APIs and storing them in COS.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31564" target="_blank">LVB audit</a></td><td>Supports AI-based audit of live streams for detection of pornographic, terrorism, and politically sensitive information.</td></tr>
<tr><td>LVB recording</td><td>Supports recording live streams through APIs and storing them in the Tencent Cloud VOD platform.</td></tr>
<tr><td>LVB time shifting</td><td>Supports playing back the content at any previous time point during live streaming.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31567" target="_blank">Global live streaming acceleration</a></td><td>Supports using the Tencent Cloud LVB service outside Mainland China.</td></tr>
</table>



### LVB SDK
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td>MLVB SDK</td><td>An integrated live streaming SDK that provides various features such as LVB push, basic beauty filters, filters, LVB playback, and LVB time shifting.</td></tr>
<tr><td>Beauty filter SDK</td><td>Jointly created by Tencent Cloud, Pitu, and YouTu Lab, this is an advanced video processing solution that has a wide variety of real-time special effects for live video capture such as filters, beauty filters, stickers, and gesture recognition to meet the diversified video capture needs in multiple scenarios.</td></tr>
<tr><td>Interactive live streaming (solution)</td><td>Interactive live mic connect solution based on the MLVB SDK.</td></tr>
<tr><td>Mini Program LVB (solution)</td><td>Provides various capabilities such as LVB tag and LVB plugin and supports integration into external Mini Programs to implement cross-platform Mini Program LVB solutions by customers with different qualifications.</td></tr>
</table>
