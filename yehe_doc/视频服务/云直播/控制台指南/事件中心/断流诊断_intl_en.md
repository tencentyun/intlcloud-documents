## Operation Scenarios

Push interruption diagnosis helps you quickly check the records of push interruptions and their reasons.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- There is an interruption in live push under the current Tencent Cloud account.

## Directions

After the live push is interrupted, select **Event Center** > **[Stream Interruption Records](https://console.cloud.tencent.com/live/tools/streamevent)** on the left sidebar to enter the push interruption diagnosis page.
![](https://qcloudimg.tencent-cloud.cn/raw/7109f254ed3f4c892bd93632d9f04629.png)

Here:
- **Path**: `AppName` in the push address.
- **Stream Name**: `StreamName` in the push address.

**The error codes and corresponding reasons are listed in the table below:**

<table border='0'>
 <col>
 <col>
 <tr>
<th colspan='2'>Error Code</td>
<th>Reason</td>
 </tr>
 <tr>
<td colspan='2'>0</td>
<td>Unknown error.</td>
 </tr>
 <tr>
<td colspan='2'>1</td>
<td>The push client actively stopped the push.</td>
 </tr>
 <tr>
<td colspan='2'>2</td>
<td>The push client actively stopped the push.</td>
 </tr>
 <tr>
<td colspan='2'>3</td>
<td>The push client actively stopped the push.</td>
 </tr>
 <tr>
<td colspan='2'>4</td>
<td>The push client actively stopped the push.</td>
 </tr>
 <tr>
<td colspan='2'>5</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td colspan='2'>6</td>
<td>Exception with the RTMP protocol content.</td>
 </tr>
 <tr>
<td colspan='2'>7</td>
<td>The size of a single RTMP frame exceeds the maximum value allowed by the configuration.</td>
 </tr>
 <tr>
<td colspan='2'>8</td>
<td>The system actively disconnected the push as there was no data for a prolonged time.</td>
 </tr>
 <tr>
<td colspan='2'>9</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td colspan='2'>10</td>
<td>The proxy layer received an interruption command.</td>
 </tr>
 <tr>
<td colspan='2'>11</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td colspan='2'>12</td>
<td>Exception with the push linkage network.</td>
 </tr>
 <tr>
<td colspan='2'>13</td>
<td>Exception with the push linkage network.</td>
 </tr>
 <tr>
<td colspan='2'>14</td>
<td>Exception with the push linkage network.</td>
 </tr>
 <tr>
<td colspan='2'>15</td>
<td>Exception with the push linkage network.</td>
 </tr>
 <tr>
<td colspan='2'>16</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td colspan='2'>17</td>
<td>Exception with the push linkage network.</td>
 </tr>
 <tr>
<td rowspan='27'>18</td>
<td>100</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td>101</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td>102</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td>103</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td>104</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td>200</td>
<td>Failed to get the customer information corresponding to the push link.</td>
 </tr>
 <tr>
<td>201</td>
<td>Your CSS service has been disabled.</td>
 </tr>
 <tr>
<td>202</td>
<td>You CSS service has been temporarily disabled due to arrears of your account. Please top up promptly.</td>
 </tr>
 <tr>
<td>203</td>
<td>Your CSS service has been forcibly disabled.</td>
 </tr>
 <tr>
<td>300</td>
<td>Push with an IP address is not allowed.</td>
 </tr>
 <tr>
<td>301</td>
<td>Unable to identify the push domain name.</td>
 </tr>
 <tr>
<td>302</td>
<td>The push domain name is invalid.</td>
 </tr>
 <tr>
<td>303</td>
<td>The push domain name is disabled.</td>
 </tr>
 <tr>
<td>304</td>
<td>The push application name is disabled.</td>
 </tr>
 <tr>
<td>305</td>
<td>The pushed stream name is in forbidden status.</td>
 </tr>
 <tr>
<td>306</td>
<td>The access mode is channel mode, but the corresponding push channel has not been created yet.</td>
 </tr>
 <tr>
<td>307</td>
<td>The access mode is channel mode, but the current push channel has been disabled.</td>
 </tr>
 <tr>
<td>308</td>
<td>The pushed stream name contains invalid characters.</td>
 </tr>
 <tr>
<td>309</td>
<td>The push application name contains invalid characters.</td>
 </tr>
 <tr>
<td>400</td>
<td>The push client IP is in the blocklist.</td>
 </tr>
 <tr>
<td>401</td>
<td>The push client IP is not in the allowlist.</td>
 </tr>
 <tr>
<td>500</td>
<td>The push does not carry the expiration time parameter.</td>
 </tr>
 <tr>
<td>501</td>
<td>The parameter value of the expiration time has expired.</td>
 </tr>
 <tr>
<td>502</td>
<td>The push does not carry the authentication parameter.</td>
 </tr>
 <tr>
<td>503</td>
<td>Authentication parameter verification failed.</td>
 </tr>
 <tr>
<td>600</td>
<td>The current number of pushes exceeds the maximum value allowed by the configuration.</td>
 </tr>
 <tr>
<td>601</td>
<td>The number of pushes corresponding to the current stream name exceeds the maximum value allowed by the configuration.</td>
 </tr>
 <tr>
<td colspan='2'>19</td>
<td>Third-party authentication failed.</td>
 </tr>
 <tr>
<td colspan='2'>20</td>
<td>The system actively disconnected the push as there was no data for a prolonged time.</td>
 </tr>
 <tr>
<td rowspan='3'>21</td>
<td>100</td>
<td>A push interruption request from the client was received. </td>
 </tr>
 <tr>
<td>101</td>
<td>A playback forbidding request from the client was received. </td>
 </tr>
 <tr>
<td>102</td>
<td>A new push link was received to replace the current push.</td>
 </tr>
 <tr>
<td colspan='2'>22</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>23</td>
<td>Exception with the RTMP protocol content.</td>
 </tr>
 <tr>
<td colspan='2'>24</td>
<td>Internal error in the CSS system.</td>
 </tr>
 <tr>
<td colspan='2'>25</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>26</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>27</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>28</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>29</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>30</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>31</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>32</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>33</td>
<td>Exception with the RTMP AMF data.</td>
 </tr>
 <tr>
<td colspan='2'>34</td>
<td>Unknown reason.</td>
 </tr>
 <tr>
<td colspan='2'>35</td>
<td>The push client actively stopped the push.</td>
 </tr>
</table>

CSS also provides an API for queries. For more information, see [DescribeLiveStreamEventList](https://cloud.tencent.com/document/product/267/33186) API overview.
