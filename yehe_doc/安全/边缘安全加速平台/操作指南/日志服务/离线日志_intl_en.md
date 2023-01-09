## Description
Access logs are collected at an hourly granularity, which can be downloaded within the default retention period of 30 days.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Log Service** > **Offline Logs** on the left sidebar.
2. On the page that displays, select a site or the log file of a subdomain name. You can also filter logs by time.
![](https://qcloudimg.tencent-cloud.cn/raw/281cfb26b8b14588d501770c5a09ff3a.png)

<dx-alert infotype="notice">
- The access logs are packed every hour by default. If the selected domain name is not requested during one hour, no log pack will be generated for this hour.
- Each log pack is compressed to a GZ file.
 - Offline logs are stored and queried in UTC+00:00 by default.
- Offline logs are collected from each EdgeOne node, so the delay may vary. Generally, querying and downloading of log packs can be delayed by about 30 minutes. Log packs will be added continuously and will stabilize after 2-3 hours.</dx-alert>


## Field Description
Logs are stored in JSON format by default. The log fields are described as follows:
When a field is not specified:

- For a string field, the field value is set to `-` if the field has no data.
- For an integer field, the field value is set to `-1` if the field has no data.

### Site acceleration logs
<table>
<thead>
<tr>
<th width="15%">Name</th>
<th width="15%">Data Type</th>
<th width="70%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>RequestID</td>
<td>String</td>
<td>Unique ID of the client request</td>
</tr>
<tr>
<td>ClientIP</td>
<td>String</td>
<td>The client IP</td>
</tr>
<tr>
<td>ClientRegion</td>
<td>Sting</td>
<td>Country/Region of the client IP. Format: <a href="https://www.iso.org/iso-3166-country-codes.html">ISO-3166-2</a></td>
</tr>
<tr>
<td>RequestTime</td>
<td>int</td>
<td>The time that the client initiates a request, which is recored in UTC +00:00 and defined in the <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a> standard.</td>
</tr>
<tr>
<td>RequestStatus</td>
<td>int</td>
<td>Status of the client request. Values: `0` (not completed), `1` (completed successfully), `2` (completed abnormally)</td>
</tr>
<tr>
<td>RequestHost</td>
<td>String</td>
<td>Host of the client request</td>
</tr>
<tr>
<td>RequestBytes</td>
<td>int</td>
<td>Size of the client request, in bytes</td>
</tr>
<tr>
<td>RequestMethod</td>
<td>String</td>
<td>The HTTP method used by the client</td>
</tr>
<tr>
<td>RequestUrl</td>
<td>String</td>
<td>The URL for the client request</td>
</tr>
<tr>
<td>RequestUrlQueryString</td>
<td>String</td>
<td>The query string contained in the request URL</td>
</tr>
<tr>
<td>RequestUA</td>
<td>String</td>
<td>The User-Agent sent by the client</td>
</tr>
<tr>
<td>RequestRange</td>
<td>String</td>
<td>The Range parameter sent by the client</td>
</tr>
<tr>
<td>RequestReferer</td>
<td>String</td>
<td>The Referer parameter sent by the client</td>
</tr>
<tr>
<td>RequestProtocol</td>
<td>String</td>
<td>The application layer protocol used by the client. Values: `HTTP/1.0`, `HTTP/1.1`, `HTTP/2.0`, `HTTP/3`, `WebSocket`</td>
</tr>
<tr>
<td>RemotePort</td>
<td>int</td>
<td>The port that connects the client and node over the TCP protocol. Note that a hyphen (-) is used if this port does not exist.</td>
</tr>
<tr>
<td>EdgeCacheStatus</td>
<td>String</td>
<td>Whether the client request results in a cache hit. Values: `HIT` (resources are served by the node cache), `MISS` (resources are served by the origin and can be cached), `Dynamic` (resources cannot be cached)</td>
</tr>
<tr>
<td>EdgeResponseStatusCode</td>
<td>int</td>
<td>The status code that the node returns to the client</td>
</tr>
<tr>
<td>EdgeResponseBytes</td>
<td>int</td>
<td>Size of the response that the node returns to the client, in bytes</td>
</tr>
<tr>
<td>EdgeResponseTime</td>
<td>int</td>
<td>The amount of time elapsed between EdgeOne receiving a request from the client and waiting till the client receives the response from the server side. Unit: ms</td>
</tr>
<tr>
<td>EdgeInternalTime</td>
<td>int</td>
<td>The amount of time elapsed between EdgeOne sending a request to the origin and receiving the first byte of the response from the origin. Unit: ms</td>
</tr>
<tr>
<td>EdgeServerIP</td>
<td>String</td>
<td>IP address of the EdgeOne server, which can be resolved from the host using DNS.</td>
</tr>
<tr>
<td>EdgeServerID</td>
<td>String</td>
<td>The unique ID that identifies the EdgeOne server accessed by the client</td>
</tr>
<tr>
<td>SecurityAction</td>
<td>String</td>
<td>The rule action. Values: `Monitor` (observe), `JSChallenge` (JavaScript challenge), `Deny` (block), `Allow` (allow), `BlockIP` (block the IP), `Redirect` (redirect), `ReturnCustomPage` (return the custom page), `ManagedChallenge` (implement the managed challenge)</td>
</tr>
<tr>
<td>SecurityRuleID</td>
<td>String</td>
<td>ID of the security rule used</td>
</tr>
<tr>
<td>SecurityUserNote</td>
<td>String</td>
<td>The tag defined by the user</td>
</tr>
<tr>
<td>SecurityModule</td>
<td>String</td>
<td>Security feature of the hit security rule. Values: `CustomRule` (custom rules), `BotManagement` (bot management), `RateLimiting` (preset rate limiting rules), `RateLimitingCustomRule` (custom rate limiting rules), `ManagedRule` (managed rules), `BotClientReputation` (client reputation), `BotBehaviorAnalysis` (bot intelligence), `RateLimitingClientFiltering` (client filtering)</td>
</tr>
</tbody></table>


### L4 proxy logs
<table>
<thead>
<tr>
<th width="15%">Name</th>
<th width="15%">Data Type</th>
<th width="70%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>ServiceID</td>
<td>String</td>
<td>Unique ID of the L4 proxy service</td>
</tr>
<tr>
<td>ConnectTimeStamp</td>
<td>String</td>
<td>The time that the connection is established, which is recorded in UTC +0 and defined in the <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a> standard.</td>
</tr>
<tr>
<td>DisconnetTimeStamp</td>
<td>String</td>
<td>The time that the connection disconnects, which is recorded in UTC +0 and defined in the <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a> standard.</td>
</tr>
<tr>
<td>DisconnetReason</td>
<td>String</td>
<td>The disconnection reason.<li>Format: Direction: Reason</li><li>Values of the Direction parameter: `up` (data flows from the client to the origin), `down` (data flows from the origin to the client)</li><li>Values of the Reason parameter:</li><ul><ul><li>`net_exception_peer_error`: The peer returned an error during a read/write attempt.</li><li>`net_exception_peer_close`: The peer closed the connection.</li><li>`create_peer_channel_exception: Failed to create a channel to the next hop.</li><li>`channel_eof_exception`: The channel ended. Once this happens, the error message is sent from the node that ends the request to the adjacent node.</li><li>`net_exception_closed`: The connection is closed.</li><li>`net_exception_timeout`: Read/Write timed out.</li></ul></ul></td>
</tr>
<tr>
<td>ClientRealIP</td>
<td>String</td>
<td>The real client IP</td>
</tr>
<tr>
<td>ClientRegion</td>
<td>String</td>
<td>The 2-digit code that identifies the country/region of the client, which is defined in the <a href="https://www.iso.org/iso-3166-country-codes.html">ISO-3166-2</a> standard.</td>
</tr>
<tr>
<td>EdgeIP</td>
<td>String</td>
<td>IP address of the EdgeOne server accessed</td>
</tr>
<tr>
<td>ForwardProtocol</td>
<td>String</td>
<td>The TCP/UDP forwarding protocol configured by the client</td>
</tr>
<tr>
<td>ForwardPort</td>
<td>Int</td>
<td>The forwarding port configured by the client</td>
</tr>
<tr>
<td>SentBytes</td>
<td>Int</td>
<td>Inbound traffic produced when the log is generated, in bytes</td>
</tr>
<tr>
<td>ReceivedBytes</td>
<td>Int</td>
<td>Outbound traffic produced when the log is generated, in bytes</td>
</tr>
<tr>
<td>LogTimeStamp</td>
<td>Int or String</td>
<td>The time that the log is generated, which is recorded in UTC +0 and defined in the <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a> standard.</td>
</tr>
</tbody></table>

## Notes
- The traffic/bandwidth data (in bytes) recorded in the access log field "EdgeResponseBytes" may be different from the actual billing data for the following reasons:
   - Only application-layer data can be recorded in access logs. During actual data transfer, the traffic generated over the network is around 5-15% more than the application-layer traffic, including the following two parts:
     - Consumption by TCP/IP headers: in TCP/IP-based HTTP requests, each packet has a maximum size of 1,500 bytes and includes TCP and IP headers of 40-60 bytes, which generate traffic during transfer but cannot be counted by the application layer. The overhead of this part is around 3-4%.
     - TCP retransmission: during normal data transfer over the network, around 3% to 10% of packets are lost on the Internet and retransmitted by the server. This type of traffic, which accounts for 3-7% of the total traffic, cannot be counted at the application layer.
- When smart acceleration is enabled, the traffic/bandwidth generated when the client sends a request to the EdgeOne node incurs charges. For more details, see [Billing Overview](https://www.tencentcloud.com/document/product/1145/48705).
