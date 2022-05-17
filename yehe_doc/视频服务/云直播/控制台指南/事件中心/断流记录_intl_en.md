You can view records of live push interruptions and their causes in the CSS console.

## Prerequisite
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- There is a live stream whose push was interrupted under your account.

## Directions

In the console, select **Event Center** > **[Stream Interruption Records](https://console.cloud.tencent.com/live/tools/streamevent)** on the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/7109f254ed3f4c892bd93632d9f04629.png)

It includes the following fields:
- **Path**: `AppName` in the push URL.
- **Stream Name**: `StreamName` in the push URL.

[](id:erro_code)
## Causes of Stream Interruption
You can use the [DescribeLiveStreamEventList](https://intl.cloud.tencent.com/document/product/267/30800) API to query stream interruptions.

See the table below for a list of the causes of stream interruption: 

<table border='0' >
 <tr>
<th >Cause</td>
 </tr>
 <tr>
<td>Unknown error.</td>
 </tr>
 <tr>
<td>Push client interrupted the push.</td>
 </tr>
 <tr>
<td >CSS system internal error.</td>
 </tr>
 <tr>
<td>Abnormal RTMP protocol content.</td>
 </tr>
 <tr>
<td>Single RTMP frame size exceeds the upper limit.</td>
 </tr>
 <tr>
<td>The system interrupted the stream because no data was generated for a long period.</td>
 </tr>
 <tr>
<td>The proxy layer received an interruption command.</td>
 </tr>
 <tr>
<td>Push client network exceptions.</td>
 </tr>
 <tr  >
<td>Failed to get the user information corresponding to the push URL.</td>
 </tr>
 <tr>
<td>Your CSS service has been suspended.</td>
 </tr>
 <tr  >
<td>Your CSS service has been suspended due to an overdue payment. Please make the payment to resume service.</td>
 </tr>
 <tr>
<td>We have suspended CSS services for your account.</td>
 </tr>
 <tr>
<td>Push via IP address is not allowed.</td>
 </tr>
 <tr>
<td>Cannot recognize the push domain name.</td>
 </tr>
 <tr>
<td>Invalid push domain name.</td>
 </tr>
 <tr>
<td>The push domain name is disabled.</td>
 </tr>
 <tr>
<td>The push application name is disabled.</td>
 </tr>
 <tr>
<td>The stream is disabled.</td>
 </tr>
 <tr>
<td>Channel mode is in use, yet no push channel exists.</td>
 </tr>
 <tr>
<td>Channel mode is in use, yet the current push channel is disabled.</td>
 </tr>
 <tr>
<td>The stream name contains unallowed characters.</td>
 </tr>
 <tr>
<td>The push application name contains unallowed characters.</td>
 </tr>
 <tr  >
<td>The push client IP is in the blocklist.</td>
 </tr>
 <tr>
<td>The push client IP is not in the allowlist.</td>
 </tr>
 <tr  >
<td>The push URL carries no expiration time parameter.</td>
 </tr>
 <tr>
<td  >Reached the expiration time.</td>
 </tr>
 <tr  >
<td>The push URL carries no authentication parameter.</td>
 </tr>
 <tr  >
<td>Authentication failed.</td>
 </tr>
 <tr  >
<td>The number of current push streams exceeds the upper limit.</td>
 </tr>
 <tr>
<td>The number of push streams with this `StreamName` exceeds the upper limit.</td>
 </tr>
 <tr>
<td  >The priority of the push URL is lower than an existing one.</td>
 </tr>
 <tr>
<td>Third-party authentication failed.</td>
 </tr>
 <tr>
<td>CSS received a request for stream interruption from the customer.</td>
 </tr>
 <tr>
<td>CSS received a request to disable the stream from the customer.</td>
 </tr>
 <tr>
<td>A new push URL replaced this one.</td>
 </tr>
 <tr  >
<td>Unknown reason.</td>
 </tr>
 <tr>
<td>RTMP AMF data exception.</td>
 </tr>
</table>


