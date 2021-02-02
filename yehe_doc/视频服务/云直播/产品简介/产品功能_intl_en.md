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
<tr><td>Management method</td><td>Supports management in the LVB console graphically or by calling LVB's TencentCloud APIs.</td></tr>
</table>

### LVB Console
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31054" target="_blank">Overview</a></td><td>Displays data such as real-time LVB bandwidth and traffic. </td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/35970" target="_blank">Domain name management</a></td><td>Supports adding, modifying, disabling, and deleting LVB push and playback domain names as well as configuring domain name CNAME records, HTTPS certificates, and push and playback authentication.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31068" target="_blank">Live stream management</a></td><td>Supports querying the information of real-time and historical live streams.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/34223" target="_blank">Feature module</a></td><td>Supports querying and modifying the configuration information of LVB recording, transcoding, screencapture, porn detection, watermark, and callback.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31076" target="_blank">Statistical analysis</a></td><td>Supports querying the usage statistics of LVB service bandwidth, traffic, requests, concurrent connections, screenshots, channels, and recording channels.</td></tr>
<tr><td>LVB SDK</a></td><td>Supports querying the MLVB SDK quality monitoring data and MLVB mic connect minutes.</td></tr>
</table>


### LVB Security
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31059" target="_blank">Push authentication</a></td><td>Supports configuring push URL hotlink protection and customizing the authentication key and expiration time.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31060" target="_blank">Playback authentication</a></td><td>Supports hotlink protection based on blocklist, allowlist, Referer, and playback URL as well as remote playback authentication.</td></tr>
</table>

​    
### API Management
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Domain management APIs</a></td>
            <td>Used to add domain name, delete domain name, query domain name information, query domain name list, enable domain name, disable domain name, or modify playback domain name information.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Real-time log APIs</a></td>
            <td>Used to get log URLs in batches.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Delayed playback management APIs</a></td>
            <td>Used to delay playback, get delayed playback list, or resume playback.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Recording management APIs</a></td>
            <td>Used to create recording task, create recording rule, create recording template, delete recording task, delete recording rule, delete recording template, get recording rule list, get one single recording template, get recording template list, modify recording template configuration, or terminate recording task.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Screencapture and porn detection APIs</a></td>
            <td>Used to create screencapture rule, create screencapture template, delete screencapture rule, delete screencapture template, get screencapture rule list, get one single screencapture template, get screencapture template list, or modify screencapture template.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Watermark management APIs</a></td>
            <td>Used to add watermark, create watermark rule, delete watermark, delete watermark rule, get one single watermark, get watermark rule list, query watermark list, or update watermark.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">LVB callback APIs</a></td>
            <td>Used to create callback rule, create callback template, delete callback rule, delete callback template, get callback rule list, get one single callback template, get callback template list, or modify callback template.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">LVB pull APIs</a></td>
            <td>Used to add, delete, query, update, or modify status of the live pull configuration.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Live stream management APIs</a></td>
            <td>Used to get forbidden stream list, query stream interruption event, query live stream, query historical stream list, query stream status, interrupt live stream, forbid live stream, or resume live stream.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">LVB transcoding APIs</a></td>
            <td>Used to create transcoding rule, create transcoding template, delete transcoding rule, delete transcoding template, get transcoding rule list, get one single transcoding template, get transcoding template list, or modify transcoding template configuration.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Statistical query APIs</a></td>
            <td>Used to query billable LVB bandwidth and traffic data, query playback data by district and ISP, query HTTP playback status code details, query real-time downstream playback data at domain name level, or query LVB package information.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Certificate management APIs</a></td>
            <td>Used to bind certificate to domain name, add certificate, delete certificate, get certificate information, get certificate information list, get domain name certificate information, modify certificate, modify domain name-certificate binding information, or unbind domain name from certificate.</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">Authentication management APIs</a></td>
            <td>Used to query playback authentication key, query push authentication key, modify playback authentication key, or modify push authentication key.</td>
</tr>
</table>


### Value-Added Services
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31561" target="_blank">LVB transcoding</a></td><td>Supports transcoding live streams in various specifications.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31562" target="_blank">LVB screencapture</a></td><td>Supports taking screenshots during live streaming through the APIs and storing them in COS.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31564" target="_blank">LVB recognition</a></td><td>Supports detecting pornographic information in LVB screenshots with the aid of AI and returning recognition results.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31563" target="_blank">LVB recording</a></td><td>Supports recording live streams through APIs and storing them in the Tencent Cloud VOD platform.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31565" target="_blank">LVB time shifting</a></td><td>Supports playing back the content at any previous time point during live streaming.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31567" target="_blank">Global live streaming acceleration</a></td><td>Supports using the Tencent Cloud LVB service outside the Chinese mainland.</td></tr>
</table>



### LVB SDK
<table>
<tr><th width=15%>Feature</th><th>Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/1071" target="_blank">MLVB SDK</a></td><td>An integrated live streaming SDK that provides various features such as LVB push, basic beauty filters, filters, LVB playback, and LVB time shifting.</td></tr>
<tr><td>Beauty filter SDK</a></td><td>Jointly created by Tencent Cloud, Pitu, and YouTu Lab, this is an advanced video processing solution that has a wide variety of real-time special effects for live video capture such as filters, beauty filters, stickers, and gesture recognition to meet the diversified video capture needs in multiple scenarios.</td></tr>
<tr><td>Interactive live streaming (solution)</a></td><td>Interactive live mic connect solution based on the MLVB SDK.</td></tr>
</table>

