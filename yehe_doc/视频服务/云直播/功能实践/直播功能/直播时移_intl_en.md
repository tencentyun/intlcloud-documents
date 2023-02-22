We have recently upgraded the time shifting feature. When you create a time shifting template in the console, you will now be enabling the new time shifting feature. Generate a URL in the required format, and you can use the URL to play content from an earlier time point. API 3.0 is also now available for the time shifting feature. For details, see [Time Shifting APIs](https://intl.cloud.tencent.com/document/product/267/30760). This document shows you how the time shifting feature works and how to make a playback request.

## Must-Knows
- The new time shifting feature currently supports 30,000 concurrent viewers. If you need a higher concurrency, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- If you enabled authentication for your playback domain and configured an expiration time, the time shifting URL will expire after the specified time.
- To use the [old time shifting feature](https://intl.cloud.tencent.com/document/product/267/31565) (which pulls content from a VOD domain), you need to submit a ticket. For a better experience, we recommend you use the new time shifting feature.

## How It Works
CSS enables time shifting by saving live streams as TS segments and information about the playback time of each TS segment in the cloud. This feature is often used to replay TV programs or highlights of sports events. Content is distributed to clients over HLS. You can specify the exact playback time by setting the M3U8 request parameters (for details, see [Playback Request](#play)).

[](id:play)
## Playback Request
The format of time shifting URL is `http://domain/appname/stream.m3u8`. There are two types of time shifting:
- Playing a specific duration. This is suitable for replaying highlights of sports events.
- Playing from a specific time ago. This is suitable if you want to delay the playback of a live stream.

### Request parameters for playing a specific duration
<table id="setmess">
<tr><th width="14%">Parameter</th><th>Description</th><th>Required</th><th>Example</th>
</tr><tr>
<td>txTimeshift</td>
<td>Whether to enable the new time shifting feature (<code>on</code>: Enable).</td>
<td>Yes</td>
<td>txTimeshift=on</td>
</tr><tr>
<td>tsStart</td>
<td>The playback start time.</td>
<td>Yes</td>
<td>tsStart=20121010010101</td>
</tr><tr>
<td>tsEnd</td>
<td>The playback end time.</td>
<td>Yes</td>
<td>td>tsEnd=20121010010102</td>
</tr><tr>
<td>tsFormat</td>
<td><ul style="margin:0">
<li>The format of <code>tsStart</code> and <code>tsEnd</code>. The value of this parameter is in the format of <code>{timeformat}_{unit}_{zone}</code>.</li>
<li>Valid values of <code>timeformat</code>:<ul>
<li/><code>UNIX</code> - Unix timestamp. If you use this format, you don’t need to specify <code>zone</code>.
<li/><code>human</code> - Human-readable time, such as “20121010010101”.</ul></li>
<li>Valid values of <code>unit</code>: <code>s</code>, <code>ms</code>.</li>
<li><code>s</code> indicates second and <code>ms</code> indicates millisecond.</li>
  <li><code>zone</code>: <ul style="margin:0"><li>For an east time zone, use a positive number.<li>For a west time zone, use a negative number.</ul></li>
</ul></td>
<td>Yes</td>
<td>tsFormat=unix_s
tsFormat=human_s_8</td>
</tr><tr>
<td>tsCodecname</td>
<td>For a transcoded stream, set this parameter to the ID of the transcoding template. For original streams or watermarked streams, leave out this parameter.</td>
<td>No</td>
<td>tsCodecname=hd</td>
</tr></table>



#### Request example 1 (Unix timestamp)
```
http://example.domain.com/live/stream.m3u8?txTimeshift=on&tsFormat=unix_s&tsStart=1675302995&tsEnd=1675303025&tsCodecname=test
```
#### Request example 2 (human-readable time)
```
http://example.domain.com/live/stream.m3u8?txTimeshift=on&tsFormat=unix_s_8&tsStart=20230202095635&tsEnd=20230202095705&tsCodecname=test
```

### Request parameters for playing from a specific time ago

| Parameter    | Description                    | Required | Example                                |
| ----------- | ----------------------- | ---------- | ----------------------------------- |
| txTimeshift | Whether to enable the new time shifting feature (`on`: Enable). | Yes         | txTimeshift=on                      |
| tsDelay     | The number of seconds to delay the playback by.    | Yes         | `tsDelay=30` indicates that playback will start from 30 seconds ago. |
| tsCodecname | For a transcoded stream, set this parameter to the ID of the transcoding template.  | No         | tsCodecname=2000                    |

#### Request example
```
http:://example.domain.com/live/stream.m3u8?txTimeshift=on&tsDelay=30&tsCodecname=test
```
### Authentication parameters
The authentication parameters for time shifting are the same as those for playback. For details, see [Playback Authentication Configuration](https://intl.cloud.tencent.com/document/product/267/31060) (HLS URLs generated in the console are only valid for one day).

### Querying time shifted streams
The **Time Shifting > Time shifting details** page of the console shows a list of time shifted streams. You can click **Details** to view the details of a time shifted stream.
You can also use APIs to query time shifted streams and the details of a specific stream. For details, see the following documents:
- [DescribeTimeShiftStreamList](https://www.tencentcloud.com/document/product/267/53719)
- [DescribeTimeShiftRecordDetail](https://www.tencentcloud.com/document/product/267/53720)